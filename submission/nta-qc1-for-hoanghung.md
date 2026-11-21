# Phiếu QC 1 — Road v1.0

Lô được kiểm: Hoàng Mạnh Hùng (`hoanghung`). Người kiểm: Ngô Trí Anh (`nta`)

Ngày kiểm: 21/11/2026. Guideline: Road v1.0.

File: `hoanghung-front.zip`, `hoanghung-fisheye.zip`, revision 1.

Mẫu: A01, A02, A04, A05, B02, B08; 6 ảnh, 21 shape + 24 tag = **45 nhãn**. Đã đọc XML và xem ảnh gốc; ảnh chồng nhãn ở `qc-evidence/`. Các ID `#` là thứ tự shape trong XML, không phải ID giao diện CVAT.

**Trạng thái: bản kiểm có bằng chứng, cần người kiểm xác nhận trước khi nộp.** Chưa có GT; chưa xác nhận toàn bộ màu đèn, độ lệch 5 px, điểm dừng và phạm vi label theo slide kế hoạch. Số lỗi dưới đây là các lỗi đã xác định, không phải khẳng định các phần còn lại đều đúng. Không dùng bài nta làm GT.

## Tổng hợp theo mã

| Mã                               | Loại lỗi                  |                                 Số mục kiểm |                              Số lỗi xác định | Mức           |
| --------------------------------- | --------------------------- | ---------------------------------------------: | ------------------------------------------------: | -------------- |
| QC1-01 camera                     | sai thuộc tính / bỏ sót |             6 camera; kiểm thêm 18 tag khác |                                                 0 | nặng          |
| QC1-02 đủ L1/R1                 | bỏ sót                    |                  8 vị trí trên 4 ảnh front | 0 độc lập; A02 tính ở QC1-03, A05 chờ miễn | nặng          |
| QC1-03 position                   | sai thuộc tính            |                                        11 lane |                                                 4 | nặng          |
| QC1-04 chiều, tâm, điểm dừng | sai phạm vi                |        10 lane front, đã đối chiếu chiều |                                                 2 | chính         |
| QC1-05 đứt, che                 | sai phạm vi / thuộc tính |            10 lane front, rà tính liên tục |                                     0 xác định | chính         |
| QC1-06 style/color/kind           | sai thuộc tính            |                                        11 lane |                                                 3 | chính         |
| QC1-07 vùng lái/crosswalk       | sai phạm vi / bỏ sót     |      2 crosswalk; 0 drivable để đối chiếu |                       chưa kết luận hình học | chính         |
| QC1-08 đèn, màu                | sai thuộc tính / phạm vi | 5 box đèn, rà vị trí; màu chờ xác minh |                             chưa kết luận màu | nặng / chính |
| QC1-09 facing/type/group          | sai thuộc tính            |                           5 box đèn; 0 biển |                        chưa kết luận toàn bộ | chính         |
| QC1-10 đủ biển / hình in      | bỏ sót / thừa            |                                    rà 6 cảnh | chưa kết luận tính đầy đủ theo kế hoạch | chính         |
| QC1-11 fisheye                    | sai thuộc tính / phạm vi |                          6 shape của B02, B08 |                                                 3 | chính         |
| QC1-12 file                       | lỗi file                   |                     2 ZIP, 45 nhãn trong mẫu |                     0 lỗi cấu trúc xác định | nhẹ / nặng   |

Các mục ghi “chưa kết luận” cần bổ sung; không được diễn giải thành 0 lỗi. Cảnh báo ít điểm trên B08 không tự động tính là lỗi vì cần đo độ cong. Hai lane trùng L1 trên A01 là hai vạch khác nhau; xác định là sai position, không tính thêm lỗi tách vạch QC1-05.

## Danh sách lỗi

| #  | Mã    | Ảnh | Nhãn trong XML           | Mức   | Mô tả và hướng sửa                                                                                                                               |
| -- | ------ | ---- | ------------------------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 1  | QC1-03 | A01  | lane#2@(365,499)          | nặng  | Vạch trắng đôi ngoài bên trái đang mang L1; đổi L2. Lane#0 là vạch đứt sát trái làn xe.                                               |
| 2  | QC1-04 | A01  | lane#2@(365,499)          | chính | Vẽ xa → gần: y đầu 499.4, y cuối 603.1. Đảo thứ tự điểm để gần → xa.                                                                   |
| 3  | QC1-03 | A02  | lane#1@(557,504)          | nặng  | Vạch sát bên trái làn đang đi bị gán R2; cần L1. Không đếm thêm thiếu L1 cho cùng nguyên nhân.                                       |
| 4  | QC1-06 | A02  | lane#1@(557,504)          | chính | Vạch trắng đứt đang mang style=solid; sửa dashed.                                                                                                |
| 5  | QC1-03 | A04  | lane#1@(493,360)          | nặng  | Vạch đôi vàng bên trái làn đang đi mang R1; cần L1.                                                                                          |
| 6  | QC1-03 | A04  | lane#3@(723,537)          | nặng  | Vạch trắng đứt bên phải làn đang đi mang L1; cần R1.                                                                                         |
| 7  | QC1-04 | A04  | lane#1@(493,360)          | chính | Điểm đầu y=359.9, điểm cuối y=554.17: không theo gần → xa; thứ tự còn quay ngược tại điểm giữa, cần sắp lại theo đường vạch. |
| 8  | QC1-06 | A04  | lane#1@(493,360)          | chính | Vạch đôi vàng liền bị gán white/dashed; cần yellow/solid, giữ double. Hai thuộc tính trên cùng shape gộp một dòng.                     |
| 9  | QC1-06 | A04  | lane#3@(723,537)          | chính | Vạch trắng đứt đơn bị gán solid/double; cần dashed/single. Gộp thành một lỗi thuộc tính của shape.                                     |
| 10 | QC1-11 | B02  | traffic_light#1@(110,101) | chính | edge_zone=false dù tâm box ngoài 80% bán kính theo quy ước checker; bật true.                                                                  |
| 11 | QC1-11 | B02  | traffic_light#2@(1100,19) | chính | edge_zone=false, tâm box ở vùng rìa; bật true.                                                                                                    |
| 12 | QC1-11 | B02  | traffic_light#3@(1062,74) | chính | edge_zone=false, tâm box ở vùng rìa; bật true.                                                                                                    |

## Ca mơ hồ / phần phải xác minh

| Ảnh      | Câu hỏi                                                                         | Hiện trạng                                                                                              |
| --------- | --------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| A05       | Ảnh không thấy vạch sơn L1/R1; coach xác nhận miễn QC1-02 được không? | Quan sát không thấy vạch; chưa có xác nhận coach. Không vẽ thêm.                               |
| A04       | Hai đèn facing=front đang mang red có đúng không?                          | Ảnh tổng thể có dấu hiệu đèn xanh; cần phóng to cụm đèn trước khi kết luận QC1-08 nặng. |
| B08       | Lane 3 điểm có bám cung trong 5 px không?                                    | Chưa đo; không tính cảnh báo lint thành lỗi chắc chắn.                                          |
| Các ảnh | Nhóm label bắt buộc cụ thể trong slide Task 1/2?                             | Chưa có slide; đặc biệt chưa kết luận bỏ sót drivable.                                          |

Chưa có ảnh nào được xác nhận toàn diện “không lỗi”; cần bổ sung một ảnh kiểm đủ để coach đối chiếu. Không ghi A05 là “không lỗi” khi chưa có miễn và chưa kiểm hết nhóm label.

## Quyết định

Lỗi đã xác định: **4 nặng; 8 chính / 45 nhãn = 17,78%; 0 nhẹ xác định**. Tỷ lệ là số sự kiện lỗi chính chia số shape + tag đã kiểm, không phải tỷ lệ ảnh lỗi. Một shape có thể có lỗi ở nhiều mã.

**Rework**: đã có lỗi nặng được xác định, đồng thời tỷ lệ lỗi chính vượt 5%. Các câu hỏi còn chờ không làm thay đổi quyết định Rework. Chưa có dữ liệu xác nhận việc gửi hoặc phản hồi của người ghép cặp. Quyết định áp dụng bộ revision 1 đã kiểm.
