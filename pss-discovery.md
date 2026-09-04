# PSS – Kiến trúc luồng dữ liệu hiện tại

## 1. Tổng quan

* **Nguồn dữ liệu:** AMADEUS
* **Đối tác truyền dữ liệu:** Viettel
* **Đặc điểm:** Streaming Queue, yêu cầu gần realtime (near real-time).

## 2. Luồng dữ liệu tổng thể

```text
MQ HUB 1A
    ↓
MQ Server-to-Server
    ↓
HDFS
    ↓
ETL
    ↓
Oracle DB
(DIH Latest / DIH History)
```

### Chi tiết luồng

* MQ HUB 1A đẩy dữ liệu sang phía VNA dưới dạng **JSON**.
* Dữ liệu được truyền qua mô hình **MQ Server-to-Server**.
* Dữ liệu được phân tách theo **channel/topic** tương ứng với từng domain:

  * **SKD:** Lịch bay
  * **PNR:** Booking
  * **TKT:** Vé
  * **DCS_CM_PAX:** Check-in hành khách
  * **DCS_CM_BAGGAGE:** Check-in hành lý
* Dữ liệu sau khi nhận được sẽ được lưu trữ trên **HDFS**.
* **ETL** đọc dữ liệu từ HDFS, xử lý và phát sinh dữ liệu vào **Oracle Database**.

## 3. Tổ chức dữ liệu theo Domain

* Có tài liệu quy định cách tổ chức bảng theo từng domain.
* Mỗi domain có các bảng **PROCESSED** để lưu trữ/thể hiện thông tin chính đã được xử lý của domain đó.

## 4. Quy mô dữ liệu

* Tổng số bảng **DIH:** khoảng **120 bảng**.
* Dữ liệu bao gồm toàn bộ các giao dịch được truyền qua hệ thống.
* Tuy nhiên, hệ thống không lưu toàn bộ lịch sử giao dịch do khối lượng dữ liệu rất lớn.
* Logic lưu trữ tập trung vào việc lọc và giữ bản ghi cập nhật mới nhất (**Latest / Current State**) của hệ thống.

### Tóm tắt

PSS nhận dữ liệu streaming từ AMADEUS thông qua MQ HUB 1A theo từng domain/topic → lưu dữ liệu raw trên HDFS → ETL xử lý → cập nhật khoảng 120 bảng DIH trên Oracle, trong đó dữ liệu được tối ưu theo hướng giữ trạng thái mới nhất thay vì lưu toàn bộ lịch sử giao dịch.

## 5. Vấn đề về lưu trữ History

* Hiện tại hệ thống không lưu trữ toàn bộ lịch sử của người đặt vé.
* Do đó phát sinh phương án sử dụng DB khác để lưu trữ lịch sử.
* Định hướng hiện tại là **lưu trữ chung trong một DB**, nhưng cần đảm bảo tối ưu.
* **History Data:** lưu trữ trong **1 năm**, theo Quy định TCT.
* **Latest Data:** lưu trữ **mãi mãi**.

## 6. Ý nghĩa của Latest Data và History Data

### Latest Data

* Là dữ liệu mới nhất / trạng thái hiện tại của dữ liệu.
* Mục đích sử dụng: **thống kê, báo cáo**.
* Latest Data cần được lưu vào **ODS**.
* Yêu cầu cập nhật Latest Data qua MQ theo hướng **near real-time**.

### History Data

* Là dữ liệu phục vụ mục đích **truy vết**.
* Theo định hướng hiện tại, History Data được lưu trữ trong **1 năm**, theo Quy định TCT.

## 7. Mối quan hệ PSS – DIH

* **PSS:** Passenger Service System.
* **DIH:** Dynamic Intelligence Hub.
* Mỗi lần phát sinh giao dịch, **PSS sẽ sinh ra các message JSON và lưu trữ tại DIH**.

## 8. Tài liệu VNA có thể cung cấp

### 8.1. Mô tả kiến trúc file JSON trên từng Topic

* Sample JSON IBM MQ.
* Tài liệu có thể khác với thực tế.

### 8.2. Cấu trúc, thiết kế các bảng

* Đang thiết kế theo 1A.
* Có mô tả bảng và các trường dữ liệu.
* Có tài khoản được cấp quyền view các bảng.

### 8.3. Logic từ JSON → Bảng

* Không cung cấp code.
* Có thể có đầu mối để trao đổi về logic xử lý.

## 9. Yêu cầu tương lai

### 9.1. Quản trị IBM MQ

* VNA đang cài đặt IBM MQ để nhận dữ liệu từ 1A.
* Dữ liệu không chỉ được sử dụng trong Lakehouse.
* Sau khi kết thúc hợp đồng, Lakehouse sẽ tiếp nhận việc **quản trị và vận hành trong 5 năm**.

### 9.2. Lưu trữ và khai thác dữ liệu

Hệ thống mới cần:

* Phân tích và lưu trữ được dữ liệu lịch sử.
* Có thể expose API để tra cứu và sử dụng dữ liệu.
* Latest Data cần được lưu vào ODS.
* Latest Data truyền qua MQ theo hướng **near real-time**.

### 9.3. Tần suất cập nhật

* Hiện tại **chưa đo tần suất để xác định SLA**.
* Dự kiến khoảng **4–5 phút**, tương tự như Viettel đang xử lý.

> 4–5 phút hiện mới là giá trị dự kiến/tham chiếu, chưa phải SLA chính thức.

## 10. Khả năng lưu trữ dữ liệu trên Cloud

* Dữ liệu lịch sử có thể được lưu trữ trên Cloud.
* Việc lưu trữ dữ liệu thực hiện theo **quy định về bảo mật và lưu trữ dữ liệu**.

## 11. Hệ thống mới và DIH

* **Hệ thống mới sẽ thay thế DIH.**
* Yêu cầu: hệ thống mới phải **đáp ứng đầy đủ các nghiệp vụ** của hệ thống hiện tại.
