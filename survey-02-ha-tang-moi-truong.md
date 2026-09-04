# Vietnam Airlines · Lakehouse

# *Phiên bản 1.0*

## Phiếu khảo sát 02 — Hạ tầng và môi trường hệ thống nguồn

Phiếu này thu thập hiện trạng kỹ thuật của **một hệ thống nguồn**: thông tin hệ thống, database, **truy cập và hình thức kết nối tới dữ liệu nguồn**, khả năng đồng bộ (CDC / incremental), near-real-time, file / SFTP, hàng đợi tin nhắn (MQ), cùng inventory dữ liệu và định hướng kiến trúc / tích hợp.

**Đối tượng điền:** đầu mối kỹ thuật hệ thống, DBA, đội hạ tầng / tích hợp.

**Hướng dẫn:** điền **một phiếu cho một hệ thống**. Chỉ trả lời các nhóm áp dụng với hệ thống của quý vị (theo danh sách cuối mục Thông tin phiên). Nhóm không áp dụng xin bỏ qua.

## Thông tin phiên khảo sát

**Hệ thống đang khảo sát:** ________

**Ngày khảo sát:** ________

**Hình thức khảo sát:**

- ☐ Họp trực tiếp
- ☐ Online
- ☐ Email / tài liệu
- ☐ Khác: ________

**Người khảo sát:**

- Họ tên: ________
- Đơn vị: ________

**Người trả lời:**

- Họ tên: ________
- Chức danh: ________
- Đơn vị: ________

**Người tham dự khác:** ________

## 1. System Information (SYS)

### Q01. Tên hệ thống?
________

### Q02. Tên viết tắt?
________

### Q04. Đơn vị sở hữu hệ thống?
________

### Q05. Đơn vị vận hành?
________

### Q06. Đầu mối nghiệp vụ?

**Trả lời:**

| Họ tên | Chức danh | Liên hệ |
| ------ | --------- | ------- |
|        |           |         |

### Q07. Đầu mối kỹ thuật?

**Trả lời:**

| Họ tên | Chức danh | Liên hệ |
| ------ | --------- | ------- |
|        |           |         |

### Q08. Vendor / nhà cung cấp?

---

### Q10. Công nghệ sử dụng?

---

### Q11. Database engine?

---

### Q12. Version database?

---

### Q13. Hệ thống đang triển khai On-premise hay Cloud?

- ☐ On-premise · ☐ Cloud · ☐ Hybrid · ☐ Chưa rõ

**Chi tiết (nơi đặt / nhà cung cấp cloud):** ________

### Q14. Hệ thống có kế hoạch upgrade / migration / replacement không?

- Quyết định: ☐ Có · ☐ Không · ☐ Chưa rõ

**Nếu có:**

| Hạng mục                               | Nội dung |
| -------------------------------------- | -------- |
| Nền tảng / hệ thống đích               |          |
| Thời điểm dự kiến                      |          |
| Ảnh hưởng tới việc lấy dữ liệu cho ODS |          |

## 2. Database (DB)

### Q16. Có bao nhiêu database / schema?

**Trả lời:**

| Loại     | Số lượng | Tên (liệt kê) |
| -------- | -------- | ------------- |
| Database |          |               |
| Schema   |          |               |

### Q17. Có bao nhiêu table?

---

### Q18. Tổng dung lượng database hiện tại?

---

### Q19. Dung lượng tăng trưởng trung bình mỗi ngày / tháng?

**Trả lời:**

| Mốc     | Tăng trưởng | Ghi chú |
| ------- | ----------- | ------- |
| / ngày  |             |         |
| / tháng |             |         |

### Q20. Những table nào có dữ liệu lớn nhất?

**Trả lời:**

| Table | Schema | Dung lượng / số record (ước tính) | Ghi chú |
| ----- | ------ | --------------------------------- | ------- |
|       |        |                                   |         |
|       |        |                                   |         |
|       |        |                                   |         |

### Q21. Có partition không?

- Quyết định: ☐ Có · ☐ Không · ☐ Chưa rõ

**Nếu có, mô tả cách partition:** ________

### Q22. Có View / Materialized View không?

- Quyết định: ☐ Có View · ☐ Có Materialized View · ☐ Không · ☐ Chưa rõ

**Nếu có, liệt kê các view quan trọng:**

| Tên | Loại                         | Ghi chú |
| --- | ---------------------------- | ------- |
|     | ☐ View · ☐ Materialized View |         |
|     | ☐ View · ☐ Materialized View |         |

### Q23. Có Stored Procedure / Function phục vụ nghiệp vụ không?

- Quyết định: ☐ Có · ☐ Không · ☐ Chưa rõ

**Nếu có, liệt kê những procedure / function nghiệp vụ quan trọng:**

| Tên | Vai trò nghiệp vụ | Ghi chú |
| --- | ----------------- | ------- |
|     |                   |         |
|     |                   |         |

### Q24. Có bảng nào chứa dữ liệu lịch sử không?

- Quyết định: ☐ Có · ☐ Không · ☐ Chưa rõ

**Nếu có:**

| Table | Cách lưu lịch sử | Ghi chú |
| ----- | ---------------- | ------- |
|       |                  |         |
|       |                  |         |

## 3. Truy cập hệ thống nguồn và hình thức kết nối

*Nhóm câu hỏi áp dụng cho mọi hệ thống nguồn cần đưa dữ liệu vào Lakehouse / ODS. Không yêu cầu cung cấp mật khẩu hay secret trong phiếu này.*

### Q84. Đội Lakehouse / ODS được phép truy cập hệ thống nguồn theo hình thức nào?

- ☐ Đọc trực tiếp database production
- ☐ Đọc qua database replica / read-only
- ☐ API
- ☐ File / SFTP
- ☐ Message Queue (MQ / Kafka)
- ☐ CDC / log-based
- ☐ Database replication
- ☐ Chưa xác định
- ☐ Khác: ________

**Hình thức ưu tiên (nếu có nhiều lựa chọn):** ________

### Q85. Môi trường nào được phép kết nối để lấy dữ liệu nguồn?

- ☐ Production · ☐ UAT · ☐ Development · ☐ Staging · ☐ Read replica · ☐ Khác: ________

**Môi trường khuyến nghị dùng cho đồng bộ thường xuyên:** ________

### Q86. Có thể cấp tài khoản / credential đọc dữ liệu riêng cho Lakehouse / ODS không?

- Quyết định: ☐ Có · ☐ Không · ☐ Cần phê duyệt · ☐ Chưa rõ

**Loại credential:**

- ☐ DB user (read-only) · ☐ Service account · ☐ API key / token · ☐ Certificate · ☐ Khác: ________

**Đơn vị / người cấp quyền:** ________

### Q87. Ai phê duyệt quyền truy cập dữ liệu hệ thống nguồn?

**Trả lời:**

| Vai trò | Người / đơn vị | Ghi chú |
| ------- | -------------- | ------- |
| Phê duyệt nghiệp vụ | | |
| Phê duyệt kỹ thuật / DBA | | |
| Phê duyệt bảo mật / mạng | | |

### Q88. Yêu cầu mạng / hạ tầng để kết nối tới hệ thống nguồn là gì?

- ☐ Kết nối nội bộ (LAN / VLAN)
- ☐ VPN
- ☐ Firewall whitelist IP
- ☐ Jump host / bastion
- ☐ Private Link / peering
- ☐ Internet công cộng (có bảo mật)
- ☐ Chưa rõ
- ☐ Khác: ________

**Mô tả điều kiện mạng:** ________

### Q89. Giao thức / cổng kết nối tới dữ liệu nguồn?

**Trả lời:**

| Hình thức kết nối | Giao thức | Cổng (nếu biết) | Ghi chú |
| ----------------- | --------- | --------------- | ------- |
| Database (JDBC / ODBC / native) | | | |
| API | ☐ REST · ☐ SOAP · ☐ GraphQL · ☐ Khác | | |
| File / SFTP | | | |
| MQ / Kafka | | | |
| Khác | | | |

*Không điền mật khẩu / connection string có secret vào phiếu.*

### Q90. Có tài liệu endpoint / connection info (không gồm secret) để bàn giao không?

- Quyết định: ☐ Có · ☐ Đang soạn · ☐ Không · ☐ Chưa rõ

**Vị trí tài liệu / đầu mối cung cấp:** ________

### Q91. Kết nối tới dữ liệu nguồn có bắt buộc mã hóa in-transit (TLS / SSL) không?

- Quyết định: ☐ Bắt buộc · ☐ Khuyến nghị · ☐ Không yêu cầu · ☐ Chưa rõ

**Chi tiết:** ________

### Q92. Có giới hạn số kết nối đồng thời, thời gian kết nối hoặc tốc độ đọc không?

- Quyết định: ☐ Có · ☐ Không · ☐ Chưa rõ

**Nếu có:**

| Loại giới hạn | Mức giới hạn | Ghi chú |
| ------------- | ------------ | ------- |
| Concurrent connection | | |
| Thời gian / cửa sổ được phép kết nối | | |
| Tốc độ đọc / rate limit | | |

### Q93. Khi mất kết nối tới hệ thống nguồn, yêu cầu xử lý phía Lakehouse / ODS như thế nào?

- ☐ Buffer / queue · ☐ Retry tự động · ☐ Tạm dừng luồng · ☐ Cảnh báo vận hành
- ☐ Backfill khi khôi phục · ☐ Khác: ________

**Chi tiết / SLA khôi phục:** ________

## 4. CDC / Incremental (CDC)

*Chỉ điền nếu Question Matrix đánh Required hoặc Conditional cho nhóm CDC.*

### Q25. Hệ thống có cột CreatedDate / UpdatedDate không?

- Quyết định: ☐ Có cả hai · ☐ Chỉ CreatedDate · ☐ Chỉ UpdatedDate · ☐ Không · ☐ Chưa rõ

**Tên cột thực tế:**

| Ý nghĩa | Tên cột | Kiểu |
| ------- | ------- | ---- |
| Created |         |      |
| Updated |         |      |

### Q26. Có cơ chế xác định record INSERT / UPDATE / DELETE không?

- Quyết định: ☐ Có · ☐ Không · ☐ Chưa rõ

**Mô tả cơ chế:**

- ☐ Timestamp · ☐ Flag / status · ☐ Soft delete · ☐ Hard delete · ☐ Audit table · ☐ Khác: ________

**Chi tiết:** ________

### Q27. Có CDC không?

- Quyết định: ☐ Có · ☐ Không · ☐ Chưa rõ

**Nếu có, công cụ / cơ chế CDC:** ________

### Q28. Có database transaction log / binlog / WAL có thể sử dụng không?

- Quyết định: ☐ Có · ☐ Không · ☐ Chưa rõ · ☐ Không được phép dùng

**Loại log:**

- ☐ Redo / archive log · ☐ Binlog · ☐ WAL · ☐ Khác: ________

**Điều kiện sử dụng:** ________

### Q29. Có thể sử dụng database replication không?

- Quyết định: ☐ Có · ☐ Không · ☐ Chưa rõ

**Cơ chế replication hiện có:** ________

### Q30. Có thể tạo read replica cho ODS không?

- Quyết định: ☐ Có · ☐ Không · ☐ Chưa quyết

**Điều kiện / hạn chế:** ________

### Q31. Có thể truy cập trực tiếp database production không?

- Quyết định: ☐ Có · ☐ Không · ☐ Chưa quyết

**Điều kiện / hạn chế:** ________

### Q32. Nếu không, có database replica / read-only database không?

- Quyết định: ☐ Có replica · ☐ Có read-only · ☐ Không · ☐ Không áp dụng (đã truy cập được production) · ☐ Chưa rõ

**Chi tiết:** ________

### Q33. Có giới hạn tải lên database production không?

- Quyết định: ☐ Có · ☐ Không · ☐ Chưa rõ

**Nếu có, mô tả giới hạn:** ________

### Q34. Có maintenance window cho việc đồng bộ dữ liệu không?

- Quyết định: ☐ Có · ☐ Không · ☐ Chưa rõ

**Nếu có:**

| Hạng mục                        | Nội dung |
| ------------------------------- | -------- |
| Thời gian window                |          |
| Tần suất                        |          |
| Việc được phép làm trong window |          |

## 5. Near-real-time (NRT)

*Chỉ điền nếu Question Matrix đánh Required hoặc Conditional cho nhóm NRT.*

### Q35. Dữ liệu nào yêu cầu near-real-time?

**Trả lời:**

| Nhóm dữ liệu / table | Lý do cần NRT | Ghi chú |
| -------------------- | ------------- | ------- |
|                      |               |         |
|                      |               |         |

### Q36. Mức latency yêu cầu là bao nhiêu?

**Trả lời:**

| Nhóm dữ liệu | Latency mong muốn                                        | Ghi chú |
| ------------ | -------------------------------------------------------- | ------- |
|              | ☐ < 1 phút · ☐ < 5 phút · ☐ < 15 phút · ☐ Khác: ________ |         |
|              | ☐ < 1 phút · ☐ < 5 phút · ☐ < 15 phút · ☐ Khác: ________ |         |

### Q37. Có yêu cầu event-driven không?

- Quyết định: ☐ Có · ☐ Không · ☐ Chưa quyết

**Phạm vi:** ________

### Q38. Hệ thống có phát event không?

- Quyết định: ☐ Có · ☐ Không · ☐ Chưa rõ

**Nếu có, kênh / topic / event type:** ________

### Q39. Có Kafka / RabbitMQ / MQ / Message Queue không?

- Quyết định: ☐ Kafka · ☐ RabbitMQ · ☐ MQ khác · ☐ Không · ☐ Chưa rõ

**Chi tiết (cluster / queue / topic):** ________

### Q40. Có thể sử dụng CDC cho near-real-time không?

- Quyết định: ☐ Có · ☐ Không · ☐ Chưa rõ

**Ghi chú:** ________

### Q41. Có thể sử dụng PostgreSQL logical replication không?

- Quyết định: ☐ Có · ☐ Không · ☐ Không áp dụng (không phải PostgreSQL) · ☐ Chưa rõ

**Ghi chú:** ________

### Q42. Nếu không thể near-real-time, batch nhỏ nhất có thể chạy là bao lâu?

**Trả lời:**

- ☐ 1 phút · ☐ 5 phút · ☐ 15 phút · ☐ 1 giờ · ☐ Nhiều giờ · ☐ 1 ngày · ☐ Khác: ________

**Giải thích:** ________

## 6. File / SFTP (FILE)

*Chỉ điền nếu Question Matrix đánh Required hoặc Conditional cho nhóm FILE.*

### Q43. Dữ liệu được xuất thành file định dạng gì?

**Trả lời:**

- ☐ CSV · ☐ TXT · ☐ XML · ☐ JSON · ☐ Excel · ☐ Khác: ________

**Chi tiết:** ________

### Q44. File được tạo với tần suất bao lâu?

**Trả lời:**

- ☐ Realtime / liên tục · ☐ Theo giờ · ☐ Theo ngày · ☐ Theo sự kiện · ☐ Khác: ________

**Chi tiết lịch:** ________

### Q45. File được đặt ở đâu?

---

### Q46. SFTP server nằm ở đâu?

---

### Q47. Ai quản lý SFTP?

---

### Q48. Naming convention của file?

---

### Q49. File có timestamp không?

- Quyết định: ☐ Có · ☐ Không · ☐ Chưa rõ

**Vị trí timestamp (tên file / nội dung):** ________

### Q50. Có sequence number không?

- Quyết định: ☐ Có · ☐ Không · ☐ Chưa rõ

**Cách đánh số:** ________

### Q51. Có checksum không?

- Quyết định: ☐ Có · ☐ Không · ☐ Chưa rõ

**Thuật toán / file checksum:** ________

### Q52. Có cơ chế xác nhận file đã nhận đầy đủ không?

- Quyết định: ☐ Có · ☐ Không · ☐ Chưa rõ

**Mô tả cơ chế:** ________

### Q53. Nếu file bị thiếu / mất / corrupt thì xử lý như thế nào?

---

### Q54. Có thể nhận lại file cũ không?

- Quyết định: ☐ Có · ☐ Không · ☐ Chưa rõ

**Điều kiện / thời hạn lưu file:** ________

### Q55. File có chứa dữ liệu trùng lặp không?

- Quyết định: ☐ Có · ☐ Không · ☐ Chưa rõ

**Cách xử lý trùng:** ________

## 7. MQ (MQ)

*Chỉ điền nếu Question Matrix đánh Required hoặc Conditional cho nhóm MQ.*

### Q56. MQ đang sử dụng loại Message Queue nào?

**Trả lời:**

- ☐ Kafka · ☐ RabbitMQ · ☐ IBM MQ · ☐ ActiveMQ · ☐ Khác: ________

### Q57. MQ nằm ở đâu?

---

### Q58. Queue nào chứa dữ liệu cần lấy?

**Trả lời:**

| Queue / topic | Dữ liệu | Ghi chú |
| ------------- | ------- | ------- |
|               |         |         |
|               |         |         |

### Q59. Message format là gì?

**Trả lời:**

- ☐ JSON · ☐ XML · ☐ Avro · ☐ Protobuf · ☐ Text · ☐ Khác: ________

**Ví dụ / tài liệu schema:** ________

### Q60. Message có schema / documentation không?

- Quyết định: ☐ Có schema · ☐ Có tài liệu · ☐ Cả hai · ☐ Không · ☐ Chưa rõ

**Vị trí tài liệu:** ________

### Q61. Message có unique ID không?

- Quyết định: ☐ Có · ☐ Không · ☐ Chưa rõ

**Tên field:** ________

### Q62. Có sequence number không?

- Quyết định: ☐ Có · ☐ Không · ☐ Chưa rõ

**Tên field / cách đánh số:** ________

### Q63. Có timestamp / event timestamp không?

- Quyết định: ☐ Có · ☐ Không · ☐ Chưa rõ

**Tên field:** ________

### Q64. Có cơ chế retry không?

- Quyết định: ☐ Có · ☐ Không · ☐ Chưa rõ

**Mô tả retry:** ________

### Q65. Có cơ chế dead-letter queue không?

- Quyết định: ☐ Có · ☐ Không · ☐ Chưa rõ

**Tên DLQ / cách xử lý:** ________

### Q66. Có thể replay message không?

- Quyết định: ☐ Có · ☐ Không · ☐ Chưa rõ

**Điều kiện replay:** ________

### Q67. Có yêu cầu đảm bảo không mất message không?

- Quyết định: ☐ Có · ☐ Không · ☐ Chưa quyết

**Mức đảm bảo (at-least-once / exactly-once / ...):** ________

### Q68. Có yêu cầu ordering message không?

- Quyết định: ☐ Có · ☐ Không · ☐ Chưa quyết

**Phạm vi ordering (toàn cục / theo key):** ________

## 8. Data Architecture (ARC)

*Nhóm cross-cutting. Điền ở mức hệ thống đang khảo sát; các câu về nền tảng ODS chung có thể trả lời một lần rồi tái sử dụng cho các phiếu hệ thống khác.*

### Q69. Có yêu cầu Enterprise Data Model không?

- Quyết định: ☐ Có · ☐ Không · ☐ Chưa quyết

**Phạm vi / ghi chú:** ________

### Q70. Domain Model hiện tại đã tồn tại chưa?

- Quyết định: ☐ Đã có · ☐ Có một phần · ☐ Chưa có · ☐ Chưa rõ

**Vị trí tài liệu:** ________

### Q71. Có Canonical Data Model không?

- Quyết định: ☐ Có · ☐ Không · ☐ Chưa rõ

**Ghi chú:** ________

### Q72. Có Data Domain Boundary không?

- Quyết định: ☐ Có · ☐ Không · ☐ Chưa rõ

**Mô tả boundary:** ________

### Q73. Entity nào dùng chung giữa các domain?

**Trả lời:**

| Entity | Các domain dùng chung | System of Record | Ghi chú |
| ------ | --------------------- | ---------------- | ------- |
|        |                       |                  |         |
|        |                       |                  |         |

### Q74. Có yêu cầu MDM không?

- Quyết định: ☐ Có · ☐ Không · ☐ Chưa quyết

**Phạm vi master data:** ________

### Q75. ODS dự kiến triển khai trên nền tảng nào?

---

### Q76. Storage engine / database nào?

---

### Q77. Có phân tầng Landing → Staging → ODS → Golden Zone → Data Mart hay không?

- Quyết định: ☐ Có, đủ các tầng · ☐ Có, một phần · ☐ Không · ☐ Chưa quyết

**Tầng nào có / không có:** ________

### Q78. Có yêu cầu HA / DR không?

- Quyết định: ☐ HA · ☐ DR · ☐ Cả hai · ☐ Không · ☐ Chưa quyết

**Mô tả yêu cầu:** ________

### Q79. RPO?

---

### Q80. RTO?

---

### Q81. Data retention?

**Trả lời:**

| Vùng dữ liệu | Thời gian lưu | Ghi chú |
| ------------ | ------------- | ------- |
| Nguồn        |               |         |
| ODS          |               |         |
| Data Mart    |               |         |

### Q82. Backup?

**Trả lời:**

| Hạng mục                 | Nội dung                   |
| ------------------------ | -------------------------- |
| Có backup không          | ☐ Có · ☐ Không · ☐ Chưa rõ |
| Tần suất                 |                            |
| Thời gian giữ bản backup |                            |

### Q83. Archive?

- Quyết định: ☐ Có · ☐ Không · ☐ Chưa quyết

**Cách archive / thời hạn:** ________

## 9. Data Integration (INT)

*Dùng Integration Matrix, không hỏi lặp lại ở nhiều tài liệu. Điền các luồng liên quan hệ thống đang khảo sát.*

### 9.1. Thông tin luồng

| Source | Data Owner | Technical Owner | Database | Integration                                     | Frequency | Volume/day | Size/day |
| ------ | ---------- | --------------- | -------- | ----------------------------------------------- | --------- | ---------- | -------- |
|        |            |                 |          | ☐ JDBC · ☐ CDC · ☐ MQ · ☐ API · ☐ SFTP · ☐ Khác |           |            |          |
|        |            |                 |          | ☐ JDBC · ☐ CDC · ☐ MQ · ☐ API · ☐ SFTP · ☐ Khác |           |            |          |
|        |            |                 |          | ☐ JDBC · ☐ CDC · ☐ MQ · ☐ API · ☐ SFTP · ☐ Khác |           |            |          |

### 9.2. SLA, chất lượng và migration

| Source | Growth/month | Latency / SLA | CDC            | History        | Delete         | DQ  | Security | Downstream | Migration | Owner Approval |
| ------ | ------------ | ------------- | -------------- | -------------- | -------------- | --- | -------- | ---------- | --------- | -------------- |
|        |              |               | ☐ Có · ☐ Không | ☐ Có · ☐ Không | ☐ Có · ☐ Không |     |          |            |           |                |
|        |              |               | ☐ Có · ☐ Không | ☐ Có · ☐ Không | ☐ Có · ☐ Không |     |          |            |           |                |
|        |              |               | ☐ Có · ☐ Không | ☐ Có · ☐ Không | ☐ Có · ☐ Không |     |          |            |           |                |
