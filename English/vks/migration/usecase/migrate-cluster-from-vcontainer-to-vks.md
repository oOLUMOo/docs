# Migration Cluster from vContainer to VKS

Để migrate một Cluster từ hệ thống vContainer tới hệ thống VKS, hãy thực hiện theo các bước theo tài liệu này. Giả sử, tại Cluster nguồn, tôi đã triển khai một service nginx như sau:&#x20;

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
    --bucket mybucket \
    --backup-location-config region=hcm03,s3ForcePathStyle="true",s3Url=https://hcm03.vstorage.vngcloud.vn \
    --default-volumes-to-fs-backup

# flag `--default-volumes-to-fs-backup` will backup all persistent volume as file system volume
```

***

## Tại Cluster nguồn

* Thực hiện backup theo cú pháp:

```bash
velero backup create mybackup --include-cluster-scoped-resources="" \
    --include-namespace-scoped-resources="*" \
    --include-namespaces mynamespace \
    --wait

# velero backup create mybackup \
#   --exclude-namespaces kube-system,kube-public,kube-node-lease,velero,default \
#   --wait

velero backup describe mybackup --details
```

***

## Tại Cluster đích

* Thực hiện tạo một Storage Class mới bằng cách apply file sau:

```yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name:  ssd-3000                           # [1] The StorageClass name, CAN be changed
provisioner: bs.csi.vngcloud.vn                     # The CSI driver name, MUST set this value
parameters:
  type: vtype-61c3fc5b-f4e9-45b4-8957-8aa7b6029018  # Change it to your volume type UUID from portal
  ispoc: "true"
allowVolumeExpansion: true
```

* Tạo file mapping Storage Class giữa Cluster nguồn và đích:

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
  sc-nvme-5000-delete: ssd-3000
```

* Thực hiện restore theo lệnh:

```bash
velero restore create --from-backup mybackup
```
