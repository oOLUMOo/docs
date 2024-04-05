# Date Parser

### Tổng quan

Date Parser là một bộ lọc giúp phân tích và chuyển đổi các chuỗi ký tự biểu diễn ngày tháng sang một định dạng khác, thường là một đối tượng ngày tháng (date object) có thể sử dụng được trong các ngôn ngữ lập trình.

***

### Cấu hình Date Parser

Để cáu hình Date Parser, hãy làm theo hướng dẫn bên dưới:&#x20;

1. Tại mục **Processor information**, nhập các thông tin chung cho một processor theo hướng dẫn tại [Processor](https://docs.vngcloud.vn/display/VPV/Processor). Trong nội dung này thì bạn sẽ chọn **Processor type** là **Date Parser**.
2. Tại mục **Parsing rule**, nhập các thông tin sau đây:

2.1 Nhập **Source field**: field chứa logs sẽ cần parse.

2.2 Nhập **Locate:** ngôn ngữ được sử dụng cho định dạng date mà bạn mong muốn. Locale ảnh hưởng đến cách hiển thị và sắp xếp thứ, ngày, tháng và các ký tự phân cách, ví dụ năm-tháng-ngày, ngày-tháng-năm hoặc tháng-ngay-nam.

2.3 Nhập **Timezone:** múi giờ của một vùng địa lý. Timezone ảnh hưởng đến giá trị của ngày tháng, bởi vì cùng một thời điểm có thể có giá trị ngày tháng khác nhau tùy thuộc vào múi giờ.&#x20;

Nếu bạn không lựa chọn **Locale** và **Timezone** thì chúng tôi sẽ mặc định lấy Locale và Timezone của hệ thống.

2.4 Nhập **Target field**: field sẽ được ghi đè bên destination log project, thông thường bạn sẽ không cần nhập thông tin này&#x20;

2.5 Nhập **Pattern:** chứa date pattern để matching với source field và parse ra theo cấu trúc.&#x20;

Ví dụ:&#x20;

| Items            | Value                      | Ý nghĩa                                                                  | Source logs                                                                 | Destination logs                                                                     |
| ---------------- | -------------------------- | ------------------------------------------------------------------------ | --------------------------------------------------------------------------- | ------------------------------------------------------------------------------------ |
| **Source field** | date                       | Field nguồn cần parser là **date**.                                      | <pre><code>{
  "date": "Apr 17 09:32:01"
}
</code></pre><p><br><br><br></p> | <pre><code>{
"date": "2023-08-01T07:45:11.130Z", 
}
</code></pre><p><br><br><br></p> |
| **Locate**       | Vietnamese                 | Ngôn ngữ sử dụng là **Vietnamese**.                                      |                                                                             |                                                                                      |
| **Timezone**     | N/A                        | Múi giờ lấy theo hệ thống.                                               |                                                                             |                                                                                      |
| **Target field** | date\_parser               | Field được parser sẽ ghi đè vô Destination log ở field **date\_parser**. |                                                                             |                                                                                      |
| **Pattern**      | yyyy-MM-dd'T'HH:mm:ss.SSSZ | Định dạng ngày tháng của field **date**.                                 |                                                                             |                                                                                      |

\
![](http://docs.vngcloud.vn/download/attachments/59802010/image2023-8-2\_14-14-38.png?version=1\&modificationDate=1690960480000\&api=v2)\


***

### Lưu trữ và tái sử dụng Parsing rule

* Bạn có thể lưu trữ một parsing rule bằng cách tích chọn vào **Save this rule**, sau đó nhập tên gợi nhớ cho parsing rule mà bạn muốn lưu trữ. Tên gợi nhớ có chiều dài tối thiểu là 5 ký tự, chiều dài tối đa là 255 ký tự và chỉ có thể bao gồm các chữ cái viết hoa, viết thường (a-z, A-Z), số (0-9), dấu chấm (.), khoảng trắng ( ), dấu gạch dưới (\_), dấu gạch ngang (-) và ký tự @.
* Sau khi parsing rule đã được lưu trữ, trong các lần tạo processor kế tiếp bạn có thể tái sử dụng rule này bằng cách chọn **Rule presets** tại mục Pasing rule.&#x20;
