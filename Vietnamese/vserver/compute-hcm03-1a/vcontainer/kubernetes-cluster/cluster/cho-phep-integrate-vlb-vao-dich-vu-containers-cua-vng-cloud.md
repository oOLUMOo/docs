# Cho phép integrate vLB vào dịch vụ Containers của VNG CLOUD

**Nhu cầu:**  Khách hàng có nhu cầu triển khai 2 website: [**httpd.app.com**](http://httpd.app.com/) và [**nginx.app.com**](http://nginx.app.com/) theo kiến trúc microservice trên hạ tầng VNG Cloud.

**Giải pháp:**  Sử dụng dịch vụ vLB(Load Balancer) kết hợp với dịch vụ vContainer trên VNG Cloud.

### **Kiến trúc giải pháp:** <a href="#chophepintegratevlbvaodichvucontainerscuavngcloud-kientrucgiaiphap" id="chophepintegratevlbvaodichvucontainerscuavngcloud-kientrucgiaiphap"></a>

<figure><img src="https://docs.vngcloud.vn/download/attachments/49650186/image2023-5-8_9-39-1.png?version=1&#x26;modificationDate=1683513542000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

***

### **Triển khai:** <a href="#chophepintegratevlbvaodichvucontainerscuavngcloud-trienkhai" id="chophepintegratevlbvaodichvucontainerscuavngcloud-trienkhai"></a>

#### **1. Khởi tạo vLB và vContainer** <a href="#chophepintegratevlbvaodichvucontainerscuavngcloud-1.khoitaovlbvavcontainer" id="chophepintegratevlbvaodichvucontainerscuavngcloud-1.khoitaovlbvavcontainer"></a>

1\. Tạo Network LoadBalancer(Layer 4)

\


<figure><img src="https://docs.vngcloud.vn/download/attachments/49650186/image2023-6-2_13-17-14.png?version=1&#x26;modificationDate=1685686635000&#x26;api=v2&#x26;effects=border-simple,blur-border" alt=""><figcaption></figcaption></figure>

_Note: Như ở trên, chúng ta sẽ tạo 1 Listener trên Port 80. Nếu muốn sử dụng TLS cho website, có thể tạo thêm Listener trên Port 443 và cấu hình TLS ở Ingress Controller. Bài này sẽ chỉ triển khai với Listener Port 80._\
\


<figure><img src="https://docs.vngcloud.vn/download/attachments/49650186/image2023-6-2_13-19-49.png?version=1&#x26;modificationDate=1685686789000&#x26;api=v2&#x26;effects=border-simple,blur-border" alt=""><figcaption></figcaption></figure>

\


<figure><img src="https://docs.vngcloud.vn/download/attachments/49650186/image2023-6-2_13-21-20.png?version=1&#x26;modificationDate=1685686881000&#x26;api=v2&#x26;effects=border-simple,blur-border" alt=""><figcaption></figcaption></figure>

2\. Nhấn **Create Load Balancer** để tạo vLB

3\. Sau đó truy cập vào bảng điều khiển **tạo K8S** tại đường link: [https://hcm-3.console.vngcloud.vn/vserver/container/cluster](https://hcm-3.console.vngcloud.vn/vserver/container/cluster):

<figure><img src="https://docs.vngcloud.vn/download/attachments/49650186/image2023-6-2_13-38-31.png?version=1&#x26;modificationDate=1685687912000&#x26;api=v2&#x26;effects=border-simple,blur-border" alt=""><figcaption></figcaption></figure>

_Note: Khi tạo vContainer, chúng ta có thể chọn Enable Ingress Controller để tạo cluster với Ingress Controller đã được triển khai sẵn. Để sử dụng Ingress Controller với những tính năng phù hợp theo nhu cầu của ứng dụng, trong bài viết này sẽ không chọn Enable Ingress Controller mà sẽ tự triển khai Nginx Ingress Controller, vì thế bạn cần tắt Ingress Control khi khởi tạo K8S._

4\. Kiểm tra việc khởi tạo cluster và tải config file để access cluster:

<figure><img src="https://docs.vngcloud.vn/download/attachments/49650186/image2023-6-2_13-54-22.png?version=1&#x26;modificationDate=1685688862000&#x26;api=v2&#x26;effects=border-simple,blur-border" alt=""><figcaption></figcaption></figure>

\


<figure><img src="https://docs.vngcloud.vn/download/attachments/49650186/image2023-6-2_13-55-56.png?version=1&#x26;modificationDate=1685688957000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

#### 2. Triển khai Nginx Ingress Controller <a href="#chophepintegratevlbvaodichvucontainerscuavngcloud-2.trienkhainginxingresscontroller" id="chophepintegratevlbvaodichvucontainerscuavngcloud-2.trienkhainginxingresscontroller"></a>

1.  Truy cập [https://kubernetes.github.io/ingress-nginx/deploy/#bare-metal-clusters](https://kubernetes.github.io/ingress-nginx/deploy/#bare-metal-clusters)\
    \
    \


    <figure><img src="https://docs.vngcloud.vn/download/attachments/49650186/image2023-6-6_11-29-54.png?version=1&#x26;modificationDate=1686025795000&#x26;api=v2&#x26;effects=border-simple,blur-border" alt=""><figcaption></figcaption></figure>
2.  Copy và chạy command trên để triển khai Nginx Ingress Controller:\
    \
    \
    \


    <figure><img src="https://docs.vngcloud.vn/download/attachments/49650186/image2023-6-2_14-2-27.png?version=1&#x26;modificationDate=1685689348000&#x26;api=v2" alt=""><figcaption></figcaption></figure>
3.  Kiểm tra:\
    \
    \
    \
    → Như vậy chúng ta đã triển khai thành công Nginx Ingress Controller.

    <figure><img src="https://docs.vngcloud.vn/download/attachments/49650186/image2023-6-2_14-3-26.png?version=1&#x26;modificationDate=1685689407000&#x26;api=v2" alt=""><figcaption></figcaption></figure>
4. Service ingress-nginx-controller được khởi tạo với _Type: NodePort_ và lắng nghe trên Port: 30398, 31873 của các Minion Node.

#### 3. Attach vLB với vContainer <a href="#chophepintegratevlbvaodichvucontainerscuavngcloud-3.attachvlbvoivcontainer" id="chophepintegratevlbvaodichvucontainerscuavngcloud-3.attachvlbvoivcontainer"></a>

_Note: Mặc định vLB không thể kết nối tới vContainer Cluster dù nằm trong cùng VPC/Subnet. Do đó cần tạo mới một Security Group và attach cho Minion Node._

1.  Tạo Security Group: Do chỉ có 1 Listener Port 80 trên vLB do đó chỉ cần 1 Inbound rule. Trong trường hợp có Listener Port 443, vui lòng tạo thêm Inbound rule.\
    \
    \
    \
    \


    <figure><img src="https://docs.vngcloud.vn/download/attachments/49650186/image2023-6-6_15-19-10.png?version=1&#x26;modificationDate=1686039551000&#x26;api=v2&#x26;effects=border-simple,blur-border" alt=""><figcaption></figcaption></figure>
2.  Update Security Group cho Minion Node:\


    <figure><img src="https://docs.vngcloud.vn/download/attachments/49650186/image2023-6-2_14-55-40.png?version=1&#x26;modificationDate=1685692541000&#x26;api=v2&#x26;effects=border-simple,blur-border" alt=""><figcaption></figcaption></figure>
3.  Điền 30398. Khi đó Listener sẽ forward traffic tới Backend Pool với port 30398.\
    vLB sẽ định kỳ health check các Pool Member thông qua Monitor Port, traffic sẽ không được gửi tới những member không health check thành công.:\
    \
    \
    \


    <figure><img src="https://docs.vngcloud.vn/download/attachments/49650186/image2023-6-2_14-59-38.png?version=1&#x26;modificationDate=1685692780000&#x26;api=v2&#x26;effects=border-simple,blur-border" alt=""><figcaption></figcaption></figure>
4. Nhấn **Lưu** để hoàn tất attach vLB với vContainer

#### 4. Triển khai ứng dụng <a href="#chophepintegratevlbvaodichvucontainerscuavngcloud-4.trienkhaiungdung" id="chophepintegratevlbvaodichvucontainerscuavngcloud-4.trienkhaiungdung"></a>

1.  Chuẩn bị YAML file: service.yaml, deployment.yaml và app-ingress.yaml\
    \
    \


    <figure><img src="https://docs.vngcloud.vn/download/attachments/49650186/image2023-6-2_15-4-58.png?version=2&#x26;modificationDate=1689752242000&#x26;api=v2" alt=""><figcaption></figcaption></figure>
2.  Triển khai:\
    \
    \
    \


    <figure><img src="https://docs.vngcloud.vn/download/attachments/49650186/image2023-6-2_15-6-30.png?version=1&#x26;modificationDate=1685693191000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


<figure><img src="https://docs.vngcloud.vn/download/attachments/49650186/image2023-6-2_15-6-21.png?version=1&#x26;modificationDate=1685693181000&#x26;api=v2" alt=""><figcaption></figcaption></figure>



1.  Kiểm tra\
    Review the vLB status:\


    <figure><img src="https://docs.vngcloud.vn/download/attachments/49650186/image2023-6-2_15-8-33.png?version=1&#x26;modificationDate=1685693313000&#x26;api=v2&#x26;effects=border-simple,blur-border" alt=""><figcaption></figcaption></figure>
2.  Edit file host trên laptop cá nhân để kiểm tra: _**C:\Windows\System32\drivers\etc\hosts:**_\
    \
    \
    \


    <figure><img src="https://docs.vngcloud.vn/download/attachments/49650186/image2023-6-2_15-10-7.png?version=1&#x26;modificationDate=1685693408000&#x26;api=v2&#x26;effects=border-simple,blur-border" alt=""><figcaption></figcaption></figure>
3.  &#x20;Mở trình duyệt web và kiểm tra:\


    <figure><img src="https://docs.vngcloud.vn/download/attachments/49650186/image2023-6-2_15-11-55.png?version=1&#x26;modificationDate=1685693516000&#x26;api=v2&#x26;effects=border-simple,blur-border" alt=""><figcaption></figcaption></figure>
