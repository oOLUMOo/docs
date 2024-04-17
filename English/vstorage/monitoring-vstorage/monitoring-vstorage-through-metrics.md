# Monitoring vStorage Through Metrics

#### What is metrics? <a href="#monitoringvstoragethroughmetrics-whatismetrics" id="monitoringvstoragethroughmetrics-whatismetrics"></a>

A metric (or indicator) is a data point that we obtain through measurement, by establishing measurements, tracking, and evaluating a specific activity in context.

***

#### Why are metrics useful? <a href="#monitoringvstoragethroughmetrics-whyaremetricsuseful" id="monitoringvstoragethroughmetrics-whyaremetricsuseful"></a>

Metrics provide an overall picture of your system. You can use them to assess the health of your system at the present moment. For vStorage, metrics can help you adjust storage scale and responsiveness, so you can adjust your needs and accurately determine the amount of resources you need to consume, which can help you save money or improve performance.

***

#### **Monitoring vStorage through vStorage metrics on the vMonitor Platform** <a href="#monitoringvstoragethroughmetrics-monitoringvstoragethroughvstoragemetricsonthevmonitorplatform" id="monitoringvstoragethroughmetrics-monitoringvstoragethroughvstoragemetricsonthevmonitorplatform"></a>

Monitoring vStorage through metrics is easy when you use the vMonitor Platform. We have transferred metrics from vStorage to vMonitor Platform regularly every 5 minutes. Rest assured that vMonitor Platform is also a product of the VNG Cloud ecosystem. You can use vMonitor Platform to configure monitoring features based on these parameters. Of course, to be able to monitor, you need to purchase a metric quota package for the vMonitor Platform service. For details, please refer to vMonitor Platform. Here is a list of vStorage metrics that we have provided for monitoring purposes:

| **STT**     | **Account metric**                   | **Type**           | **Fields**                                                                                                       | **Interval**                                                                                                                  |                                                                    |                          |
| ----------- | ------------------------------------ | ------------------ | ---------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------ | ------------------------ |
| **Fields**  | **Unit**                             | **Description**    |                                                                                                                  |                                                                                                                               |                                                                    |                          |
| 1           | account\_stats                       | gauge              | bytes\_used                                                                                                      | byte                                                                                                                          | Lượng data sử dụng                                                 | 5 phút                   |
| 2           | container\_count                     | number             | Lượng container đang tồn tại                                                                                     |                                                                                                                               |                                                                    |                          |
| 3           | object\_count                        | number             | Số object đang có                                                                                                |                                                                                                                               |                                                                    |                          |
| 4           | quota\_bytes                         | byte               | Tổng quota mua theo bytes                                                                                        |                                                                                                                               |                                                                    |                          |
| 5           | used\_percent                        | %                  | Phần trăm sử dụng theo thời gian (bytes\_used/ quota\_bytes \*100)                                               |                                                                                                                               |                                                                    |                          |
| <p><br></p> | diff                                 | bytes\_used\_diff  | byte                                                                                                             | <p><br></p>                                                                                                                   |                                                                    |                          |
| <p><br></p> | container\_count\_diff               | number             | Số lượng container sinh ra hoặc giảm xuống theo chu kỳ 5 phút                                                    |                                                                                                                               |                                                                    |                          |
| <p><br></p> | object\_count\_diff                  | number             | Số lượng object sinh ra hoặc giảm xuống theo chu kỳ 5 phút                                                       |                                                                                                                               |                                                                    |                          |
| 6           | account\_net                         | counter            | bytes\_recvd                                                                                                     | byte                                                                                                                          | Lưu lượng data proxy nhận với action upload theo chu kỳ 1 phút     | 1 phút                   |
| 7           | bytes\_sent                          | byte               | Lưu lượng data proxy truyền đi với action download theo chu kỳ 1 phút                                            |                                                                                                                               |                                                                    |                          |
| 8           | bytes\_sum                           | byte               | Tổng lưu lượng data 2 chiều (bytes\_recvd+ bytes\_sent) theo chu kỳ 1 phút                                       |                                                                                                                               |                                                                    |                          |
| <p><br></p> | rate                                 | bytes\_recvd\_rate | pcs                                                                                                              | Tốc độ dữ liệu tải lên tính theo vận tốc trên giây (bytes/s)                                                                  | <p><br></p>                                                        |                          |
| <p><br></p> | bytes\_sent\_rate                    | pcs                | Tốc độ dữ liệu tải xuống tính theo vận tốc trên giây (bytes/s)                                                   | <p><br></p>                                                                                                                   |                                                                    |                          |
| <p><br></p> | bytes\_sum\_rate                     | pcs                | Tốc độ dữ liệu tải lên + tải xuống tính theo vận tốc trên giây (bytes/s)                                         | <p><br></p>                                                                                                                   |                                                                    |                          |
| 9           | account\_net\_country                | counter            | bytes\_recvd                                                                                                     | byte                                                                                                                          | Lưu lượng data proxy nhận với action upload trong chu kỳ 1 phút    | 1 phút                   |
| 10          | bytes\_sent                          | byte               | Lưu lượng data proxy truyền đi với action download trong chu kỳ 1 phút                                           |                                                                                                                               |                                                                    |                          |
| 11          | bytes\_sum                           | byte               | Tổng lưu lượng data 2 chiều (bytes\_recvd+ bytes\_sent) trong chu kỳ 1 phút                                      |                                                                                                                               |                                                                    |                          |
| <p><br></p> | rate                                 | bytes\_recvd\_rate | pcs                                                                                                              | Tốc độ tải lên dữ liệu tính theo vận tốc trên giây (bytes/s) theo từng quốc gia                                               | <p><br></p>                                                        |                          |
| <p><br></p> | bytes\_sent\_rate                    | pcs                | Tốc độ tải xuống dữ liệu tính theo vận tốc trên giây (bytes/s) theo từng quốc gia                                | <p><br></p>                                                                                                                   |                                                                    |                          |
| <p><br></p> | bytes\_sum\_rate                     | pcs                | Tốc độ tải lên + tải xuống dữ liệu tính theo vận tốc trên giây (bytes/s) theo từng quốc gia                      | <p><br></p>                                                                                                                   |                                                                    |                          |
| 12          | account\_net\_vngcloud               | counter            | bytes\_recvd                                                                                                     | byte                                                                                                                          | Lưu lượng data hệ thống nhận với action upload trong chu kỳ 1 phút | 1 phút                   |
| 13          | bytes\_sent                          | byte               | Lưu lượng data hệ thống truyền đi với action download trong chu kỳ 1 phút                                        |                                                                                                                               |                                                                    |                          |
| 14          | bytes\_sum                           | byte               | Tổng lưu lượng data 2 chiều (bytes\_recvd +  bytes\_sent) trong chu kỳ 1 phút                                    |                                                                                                                               |                                                                    |                          |
| <p><br></p> | rate                                 | bytes\_recvd\_rate | pcs                                                                                                              | Tốc độ tải lên dữ liệu tính theo vận tốc trên giây (bytes/s) với nguồn xuất phát từ VNG Cloud                                 | <p><br></p>                                                        |                          |
| <p><br></p> | bytes\_sent\_rate                    | pcs                | Tốc độ tải xuống dữ liệu tính theo vận tốc trên giây (bytes/s) với nguồn xuất phát từ VNG Cloud                  | <p><br></p>                                                                                                                   |                                                                    |                          |
| <p><br></p> | bytes\_sum\_rate                     | pcs                | Tốc độ  tải lên, tải xuống dữ liệu tính theo vận tốc trên giây (bytes/s) với nguồn xuất phát từ VNG Cloud        | <p><br></p>                                                                                                                   |                                                                    |                          |
| 15          | account\_net\_user                   | counter            | bytes\_recvd                                                                                                     | byte                                                                                                                          | Lưu lượng data hệ thống nhận với action upload trong chu kỳ 1 phút | 1 phút                   |
| 16          | bytes\_sent                          | byte               | Lưu lượng data hệ thống truyền đi với action download trong chu kỳ 1 phút                                        |                                                                                                                               |                                                                    |                          |
| 17          | bytes\_sum                           | byte               | Tổng lưu lượng data 2 chiều (bytes\_recvd + bytes\_sent) trong chu kỳ 1 phút                                     |                                                                                                                               |                                                                    |                          |
| <p><br></p> | rate                                 | bytes\_recvd\_rate | pcs                                                                                                              | Tốc độ tải lên dữ liệu tính theo vận tốc trên giây (bytes/s) với nguồn xuất phát từ bên ngoài internet                        | <p><br></p>                                                        |                          |
| <p><br></p> | bytes\_sent\_rate                    | pcs                | Tốc độ tải xuống dữ liệu tính theo vận tốc trên giây (bytes/s) với nguồn xuất phát từ bên ngoài internet         | <p><br></p>                                                                                                                   |                                                                    |                          |
| <p><br></p> | bytes\_sum\_rate                     | pcs                | Tốc độ tải lên tải xuống dữ liệu tính theo vận tốc trên giây (bytes/s) với nguồn xuất phát từ bên ngoài internet | <p><br></p>                                                                                                                   |                                                                    |                          |
| 18          | account\_requests.request\_total     | counter            | value                                                                                                            | number                                                                                                                        | Số lượng request xử lý tính theo chu kỳ 1 phút                     | 1 phút                   |
| <p><br></p> | rate                                 | value\_rate        | psc                                                                                                              | Tổng số request/s trên từng project tính theo chu kỳ 1 phút                                                                   | <p><br></p>                                                        |                          |
| 19          | account\_requests.status             | counter            | value                                                                                                            | number                                                                                                                        | Số lượng request xử lý tính theo chu kỳ 1 phút                     | 1 phút                   |
| <p><br></p> | rate                                 | value\_rate        | psc                                                                                                              | Tổng số request/s trên từng project được phân nhóm theo trạng thái trả về của request và được tính theo chu kỳ 1 phút         | <p><br></p>                                                        |                          |
| 20          | account\_requests.method             | counter            | value                                                                                                            | number                                                                                                                        | Số lượng request xử lý tính theo chu kỳ 1 phút                     | 1 phút                   |
| <p><br></p> | rate                                 | value\_rate        | psc                                                                                                              | Tổng số request/s trên từng project được phân nhóm theo loại request (GET, PUT, POST, DELETE) và được tính theo chu kỳ 1 phút | <p><br></p>                                                        |                          |
| 21          | account\_requests.features           | counter            | value                                                                                                            | number                                                                                                                        | Số lượng request xử lý theo chu kỳ 1 phút                          | 1 phút                   |
| <p><br></p> | rate                                 | value\_rate        | psc                                                                                                              | Tổng số request/s trên từng project được nhóm theo tính năng người dùng sử dụng và tính theo chu kỳ 1 phút                    | <p><br></p>                                                        |                          |
| 22          | account\_requests.request\_time      | timing             | count                                                                                                            | number                                                                                                                        | Số lượng request trong interval                                    | <p>1 phút</p><p><br></p> |
| 23          | lower                                | second             | Giá trị thấp nhất trong dãy value nhận được                                                                      |                                                                                                                               |                                                                    |                          |
| 24          | mean                                 | second             | Giá trị bình quân trong dãy value nhận được                                                                      |                                                                                                                               |                                                                    |                          |
| 26          | stddev                               | second             | Biên độ giao động trong dãy value nhận được                                                                      |                                                                                                                               |                                                                    |                          |
| 26          | sum                                  | second             | Tổng thời gian xử lý của các request                                                                             |                                                                                                                               |                                                                    |                          |
| 27          | upper                                | second             | Giá trị cao nhất trong dãy value nhận được                                                                       |                                                                                                                               |                                                                    |                          |
| 28          | 90\_percentile                       | second             | Mức giá trị chiếm 90% trong dãy value nhận được                                                                  |                                                                                                                               |                                                                    |                          |
| 29          | 99\_percentile                       | second             | Mức giá trị chiếm 99% trong dãy value nhận được                                                                  |                                                                                                                               |                                                                    |                          |
| 30          | account\_requests.bytes\_per\_second | timing             | count                                                                                                            | number                                                                                                                        | Số lượng request trong interval                                    | <p>1 phút</p><p><br></p> |
| 31          | lower                                | byte/s             | Giá trị thấp nhất trong dãy value nhận được                                                                      |                                                                                                                               |                                                                    |                          |
| 32          | mean                                 | byte/s             | Giá trị bình quân trong dãy value nhận được                                                                      |                                                                                                                               |                                                                    |                          |
| 33          | stddev                               | byte/s             | Biên độ giao động trong dãy value nhận được                                                                      |                                                                                                                               |                                                                    |                          |
| 34          | sum                                  | byte/s             | Tổng thời gian xử lý của các request                                                                             |                                                                                                                               |                                                                    |                          |
| 35          | upper                                | byte/s             | Giá trị cao nhất trong dãy value nhận được                                                                       |                                                                                                                               |                                                                    |                          |
| 36          | 90\_percentile                       | byte/s             | Mức giá trị chiếm 90% trong dãy value nhận được                                                                  |                                                                                                                               |                                                                    |                          |
| 37          | 99\_percentile                       | byte/s             | Mức giá trị chiếm 99% trong dãy value nhận được                                                                  |                                                                                                                               |                                                                    |                          |
| 38          | container\_stats                     | gauge              | bytes\_used                                                                                                      | byte                                                                                                                          | Lượng data sử dụng                                                 | 5 phút                   |
| 39          | object\_count                        | number             | Số object đang có                                                                                                | <p><br></p>                                                                                                                   |                                                                    |                          |
| 40          | quota\_bytes                         | byte               | Quota mua theo bytes                                                                                             | <p><br></p>                                                                                                                   |                                                                    |                          |
| 41          | diff                                 | bytes\_used\_diff  | byte                                                                                                             | Tổng số bytes dữ liệu tăng thêm hoặc giảm đi trên từng container theo chu kỳ 5 phút                                           | <p><br></p>                                                        |                          |
| 42          | object\_count\_diff                  | number             | Tổng số object tăng thêm hoặc giảm đi trên từng container theo chu kỳ 5 phút                                     | <p><br></p>                                                                                                                   |                                                                    |                          |