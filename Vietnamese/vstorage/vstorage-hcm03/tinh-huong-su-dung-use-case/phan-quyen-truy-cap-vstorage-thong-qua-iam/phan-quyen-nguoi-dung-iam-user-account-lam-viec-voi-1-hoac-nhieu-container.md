# Phân quyền người dùng IAM User Account làm việc với 1 hoặc nhiều container

#### Kịch bản <a href="#phanquyennguoidungiamuseraccountlamviecvoi1hoacnhieucontainer-kichban" id="phanquyennguoidungiamuseraccountlamviecvoi1hoacnhieucontainer-kichban"></a>

* Giả sử bạn là người dùng **Root User Account** và bạn đã khởi tạo và tải lên tệp tin vào 2 project: **Project01** và **Project02**.
* Hiện tại, bạn muốn tạo 2 một người dùng mới, trong đó
  * Người dùng Leo có thể **đăng nhập vào vStorage Portal** và có quyền đọc tất cả dữ liệu trên **Container01** thuộc **Project01**.
  * Người dùng Anne có thể **đăng nhập vào vStorage Portal** và có quyền đọc và ghi trên **Container01** thuộc **Project01** và **Container02** thuộc **Project02**.

Minh họa cấu trúc lưu trữ dữ liệu của bạn trên vStorage:

```
Project01 - HAN01            
Container01                                          
    └── Directory01                                            
           ├── object01.txt                                
           ├── object02.jpg
    └── object03.png
    └── object04.txt
Container03
    └── object10.png
Container04
-------------------------------
Project02 - HCM01          
Container02
    └── Directory02                                            
           ├── object05.txt                                
           ├── object06.jpg
    └── object07.png
    └── object08.txt
Container05
```

#### Để giải quyết bài toán phân quyền này, hãy làm theo các bước bên dưới: <a href="#phanquyennguoidungiamuseraccountlamviecvoi1hoacnhieucontainer-degiaiquyetbaitoanphanquyennay-haylamt" id="phanquyennguoidungiamuseraccountlamviecvoi1hoacnhieucontainer-degiaiquyetbaitoanphanquyennay-haylamt"></a>

**Bước 1: Khởi tạo tài khoản IAM User Account**

Thực hiện khởi tạo 2 tài khoản IAM User Account theo hướng dẫn tại [Khởi tạo tài khoản IAM User Account](../../quan-ly-truy-cap/quan-ly-tai-khoan-truy-cap-vstorage/tai-khoan-nguoi-dung-iam/khoi-tao-tai-khoan-iam-user-account.md). Giả sử 2 tài khoản IAM User Account được khởi tạo là:

* **IAM\_User\_Leo**
* **IAM\_User\_Anne**\


<figure><img src="https://docs.vngcloud.vn/download/attachments/64554258/image2023-9-19_10-59-55.png?version=1&#x26;modificationDate=1696822783000&#x26;api=v2" alt=""><figcaption></figcaption></figure>



**Bước 2: Khởi tạo policy cho 2 IAM User Account( IAM\_User\_Leo và IAM\_User\_Anne)**

Thực hiện khởi tạo policy cho 2 IAM User Account theo hướng dẫn tại [Khởi tạo policy cho IAM User Account](../../quan-ly-truy-cap/quan-ly-tai-khoan-truy-cap-vstorage/tai-khoan-nguoi-dung-iam/khoi-tao-policy-cho-iam-user-account.md). Cụ thể:

| Thành phần     | Policy cho IAM\_User\_Leo                                                                                               | Policy cho IAM\_User\_Anne                                                                                                                      |                                                                         |
| -------------- | ----------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| Product        | vstorage                                                                                                                | vstorage                                                                                                                                        |                                                                         |
| Action         | <ul><li><strong>List</strong></li><li><strong>Read</strong></li></ul><p>(Bao gồm tất cả các actions trong mỗi nhóm)</p> | <ul><li><strong>All vstorage actions</strong>. (List, Read, Write)</li></ul><p>(Bao gồm tất cả các actions trong mỗi nhóm)).</p>                |                                                                         |
| Resource       | Region                                                                                                                  | <ul><li><strong>HAN01</strong></li></ul>                                                                                                        | <ul><li><strong>HAN01</strong></li><li><strong>HCM01</strong></li></ul> |
| Project\_ID    | <ul><li><strong>Project_ID</strong> của <strong>Project01</strong></li></ul>                                            | <ul><li><strong>Project_ID</strong> của <strong>Project01</strong></li><li><strong>Project_ID</strong> của <strong>Project02</strong></li></ul> |                                                                         |
| Container name | <ul><li><strong>Container01</strong></li></ul>                                                                          | <ul><li><strong>Container01</strong></li><li><strong>Container02</strong></li></ul>                                                             |                                                                         |
| Object name    | <ul><li>Any</li></ul>                                                                                                   | <ul><li>Any</li></ul>                                                                                                                           |                                                                         |

<figure><img src="https://docs.vngcloud.vn/download/attachments/64554258/image2023-10-9_11-9-51.png?version=1&#x26;modificationDate=1696824593000&#x26;api=v2" alt=""><figcaption></figcaption></figure>



<figure><img src="https://docs.vngcloud.vn/download/attachments/64554258/image2023-10-9_11-11-30.png?version=1&#x26;modificationDate=1696824692000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


**Bước 3: Liên kết (Gán quyền) tài khoản IAM User Account với policy tương ứng.**

Thực hiện liên kết (gán quyền) 2 tài khoản IAM User Account với policy đã tạo ở bước 2 theo hướng dẫn tại [Liên kết tài khoản IAM User Account với policy tương ứng](../../quan-ly-truy-cap/quan-ly-tai-khoan-truy-cap-vstorage/tai-khoan-nguoi-dung-iam/lien-ket-tai-khoan-iam-user-account-voi-policy-tuong-ung.md).&#x20;

<figure><img src="https://docs.vngcloud.vn/download/attachments/64554258/image2023-10-9_10-34-15.png?version=1&#x26;modificationDate=1696822782000&#x26;api=v2" alt=""><figcaption></figcaption></figure>



<figure><img src="https://docs.vngcloud.vn/download/attachments/64554258/image2023-10-9_10-34-34.png?version=1&#x26;modificationDate=1696822782000&#x26;api=v2" alt=""><figcaption></figcaption></figure>



**Bước 4: Truy cập vStorage Portal sử dụng IAM User Account**

Thực hiện truy cập vStorage Portal sử dụng tài khoản IAM User Account theo hướng dẫn tại [Truy cập tài nguyên sử dụng tài khoản người dùng IAM](../../quan-ly-truy-cap/quan-ly-truy-cap-tai-nguyen-vstorage/truy-cap-tai-nguyen-su-dung-tai-khoan-nguoi-dung-iam.md).

<figure><img src="https://docs.vngcloud.vn/download/attachments/64554258/image2023-10-9_10-35-43.png?version=1&#x26;modificationDate=1696822782000&#x26;api=v2" alt=""><figcaption></figcaption></figure>
