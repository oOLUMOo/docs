# Migration

### Tổng quan

Migration từ một cluster sang một cluster là quá trình chuyển dữ liệu, ứng dụng, và các dịch vụ từ một nhóm máy chủ này sang một nhóm máy chủ khác. Mục đích của việc này thường là để nâng cấp hệ thống, tăng cường tính sẵn sàng và khả năng chịu lỗi, hoặc để mở rộng quy mô hệ thống.&#x20;

Trong quá trình migration, các tài nguyên như ổ đĩa, và các dịch vụ liên quan sẽ được chuyển từ cluster cũ sang cluster mới mà không làm gián đoạn hoạt động của hệ thống. Điều này đảm bảo rằng các ứng dụng quan trọng có thể tiếp tục hoạt động mà không bị ảnh hưởng bởi quá trình di chuyển.&#x20;

***

### Mô hình tổng quan

<figure><img src="../../.gitbook/assets/image (299).png" alt=""><figcaption></figcaption></figure>

***

### Các bước thực hiện

<figure><img src="../../.gitbook/assets/image (301).png" alt=""><figcaption></figcaption></figure>

Cụ thể:&#x20;

* **Bước 1:** Prepard target resource
* **Bước 2**: Migrate resources private outside cluster
* **Bước 3**: Install Velero tool
* **Bước 4**: Backup
* **Bước 5**: Restore
* **Bước 6**: Update resource config
