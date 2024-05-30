# Migration Cluster from vContainer to VKS



Để migrate một Cluster từ hệ thống vContainer tới hệ thống VKS, hãy thực hiện theo các bước theo tài liệu này.&#x20;

## Điều kiện cần

* Tạo một vStorage Project , Container, S3 key, file credential trên hệ thống vStorage.
* Thực hiện tải xuống helper bash script và grand execute permission cho file này ([velero\_helper.sh](https://raw.githubusercontent.com/vngcloud/velero/main/velero\_helper.sh))
* (Optional) Triển khai một vài service để kiểm tra tính đúng đắn của việc migrate. Giả sử, tại Cluster nguồn, tôi đã triển khai một service nginx như sau:
  * File triển khai:

```yaml
---
apiVersion: v1
kind: Namespace
metadata:
  name: mynamespace
---
apiVersion: v1
kind: Service
metadata:
  name: nginx
  namespace: mynamespace
  labels:
    app: nginx
spec:
  ports:
  - port: 80
    name: web
  selector:
    app: nginx
  type: NodePort
---
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: web
  namespace: mynamespace
spec:
  selector:
    matchLabels:
      app: nginx
  serviceName: "nginx"
  replicas: 1
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx
        ports:
        - containerPort: 80
          name: web
        volumeMounts:
        - name: disk-ssd
          mountPath: /usr/share/nginx/html
  volumeClaimTemplates:
  - metadata:
      name: disk-ssd
      namespace: mynamespace
    spec:
      accessModes: [ "ReadWriteOnce" ]
      storageClassName: sc-nvme-5000-delete
      resources:
        requests:
          storage: 20Gi
```

```bash
kubectl exec -n mynamespace -it web-0 bash
cd /usr/share/nginx/html
echo -e "<html>\n<head>\n  <title>MyVNGCloud</title>\n</head>\n<body>\n  <h1>Hello, MyVNGCloud</h1>\n</body>\n</html>" > index.html
```

* Lúc này, khi bạn truy cập vào Public IP của Node, bạn sẽ thấy "Hello, MyVNGCloud".

***

## Trên cả 2 Cluster (source and target)

* Tạo một vStorage Project, Container làm nơi nhận dữ liệu backup của cụm theo hướng dẫn tại [đây](../../../vstorage/vstorage-hcm03/cac-tinh-nang-cua-vstorage/lam-viec-voi-project/khoi-tao-project.md).
* Khởi tạo S3 key tương ứng với vStorage Project này theo hướng dẫn tại đây.
* Tạo file credentials-velero với nội dung sau:

```yaml
[default]
aws_access_key_id=<AWS_ACCESS_KEY_ID>
aws_secret_access_key=<AWS_SECRET_ACCESS_KEY>
```

* Cài đặt Velero CLI:

```bash
curl -OL https://github.com/vmware-tanzu/velero/releases/download/v1.13.2/velero-v1.13.2-linux-amd64.tar.gz
tar -xvf velero-v1.13.2-linux-amd64.tar.gz
cp velero-v1.13.2-linux-amd64/velero /usr/local/bin
```

* Cài đặt Velero trên 2 cụm của bạn theo lệnh:

```bash
velero install \
    --provider aws \
    --plugins velero/velero-plugin-for-aws:v1.9.0 \
    --use-node-agent \
    --use-volume-snapshots=false \
    --secret-file ./credentials-velero \
    --bucket mycontainer \
    --backup-location-config region=hcm03,s3ForcePathStyle="true",s3Url=https://hcm03.vstorage.vngcloud.vn
```

***

## Tại Cluster nguồn

*   Annotate các Persistent Volume và lable resource cần loại trừ khỏi bản backup

    ```yaml
    ./velero_helper.sh mark_volume -c
    ./velero_helper.sh mark_exclude -c
    ```
* Thực hiện backup theo cú pháp:

```bash
velero backup create vcontainer-full-backup --exclude-namespaces velero \
    --include-cluster-resources=true \
    --wait
```

{% hint style="info" %}
**Chú ý:**

* Bạn phải tạo 2 phiên bản backup cho Cluster Resource và Namespace Resource.
{% endhint %}

***

## Tại Cluster đích

* Tạo file mapping Storage Class giữa Cluster nguồn và đích, thực hiện apply file này trên Cluster đích của bạn:

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: change-storage-class-config
  namespace: velero
  labels:
    velero.io/plugin-config: ""
    velero.io/change-storage-class: RestoreItemAction
data:
  _______old_storage_class_______: _______new_storage_class_______  # <= Adjust here
  _______old_storage_class_______: _______new_storage_class_______  # <= Adjust here
```

* Thực hiện restore theo lệnh:

```bash
velero restore create --item-operation-timeout 1m --from-backup vcontainer-full-backup
```
