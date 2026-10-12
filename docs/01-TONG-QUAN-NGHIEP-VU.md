# Tổng quan nghiệp vụ — Quản lý Trung tâm Ngoại ngữ

> Mô tả demo này cho ai, giải quyết vấn đề gì. Cập nhật khi phạm vi thay đổi.

---

## 1. Thông tin chung

| Mục | Nội dung |
| :--- | :--- |
| Tên demo | Quản lý Trung tâm Ngoại ngữ |
| Mã dự án | `edu-trung-tam-ngoai-ngu` |
| Ngành / loại khách hàng | Trung tâm ngoại ngữ, trung tâm dạy thêm |
| Loại sản phẩm | Web quản lý + cổng phụ huynh, học viên trên điện thoại |
| Ý tưởng gốc | 4.1 · Quản lý trung tâm ngoại ngữ / dạy thêm (`ZDOCS/02-KE-HOACH/DANH-SACH-Y-TUONG.md`) |
| Người phụ trách | |
| Trạng thái | Có tài liệu nghiệp vụ (SRS, use case, kịch bản demo, kịch bản kiểm thử), chưa code |

## 2. Vấn đề của khách hàng

- Xếp lớp, lịch học bằng Excel
- Điểm danh bằng giấy
- Học phí ai đóng, ai nợ không rõ
- Phụ huynh không nắm được tình hình học

## 3. Giải pháp demo thể hiện

- Khóa học, lớp, lịch học, phòng học
- Ghi danh học viên vào lớp
- Giáo viên điểm danh trên điện thoại
- Học phí theo khóa hoặc tháng, phiếu thu, nhắc nợ
- Nhận xét, điểm kiểm tra; phụ huynh xem điểm danh và học phí

## 4. Vai trò người dùng

| Vai trò | Mã | Dùng trên | Làm được gì |
| :--- | :--- | :--- | :--- |
| Quản trị viên | ADMIN | Desktop | Toàn quyền |
| Quản lý | MANAGER | Desktop | Khóa học, lớp, báo cáo |
| Giáo vụ | STAFF | Desktop | Ghi danh, xếp lớp, thu học phí |
| Giáo viên | TEACHER | Điện thoại | Điểm danh, nhận xét, nhập điểm |
| Phụ huynh | PARENT | Điện thoại | Xem điểm danh, điểm, học phí |

## 5. Phân hệ và chức năng

| Area | Chức năng | Màn hình (route FE dự kiến) | Ưu tiên |
| :--- | :--- | :--- | :---: |
| `System` | Đăng nhập, tài khoản, vai trò, cài đặt | Có sẵn | — |
| `Edu` | Tổng quan trong ngày | `/dashboard` | P1 |
| `Edu` | Giáo viên, phòng học, ngày nghỉ | `/teachers`, `/rooms` | P1 |
| `Edu` | Khóa học, lớp, lịch học | `/courses`, `/classes` | P1 |
| `Edu` | Học viên, ghi danh | `/students` | P1 |
| `Edu` | Điểm danh | `/classes/[id]/attendance` | P1 |
| `Edu` | Điểm, nhận xét | `/classes/[id]/grades` | P2 |
| `Finance` | Học phí, phiếu thu | `/tuition` | P1 |
| `Finance` | Nhắc nợ học phí | `/tuition/debts` | P1 |
| `Edu` | Cổng phụ huynh | `/phu-huynh` | P2 |
| `Edu` | Báo cáo | `/reports` | P2 |

P1 = bắt buộc có để demo · P2 = nên có · P3 = làm thêm nếu còn thời gian.

## 6. Luồng nghiệp vụ chính

```mermaid
flowchart LR
    S0["Tư vấn, ghi danh vào lớp"] --> S1["Thu học phí"] --> S2["Điểm danh mỗi buổi"] --> S3["Nhận xét, nhập điểm"] --> S4["Nhắc nợ, gia hạn khóa"]
```

## 7. Phạm vi

**Có trong demo:**

- Lớp, lịch học, điểm danh, học phí, cổng phụ huynh

**Không làm (nói rõ với khách nếu được hỏi):**

- Học trực tuyến
- Gửi Zalo thật
- Các kết nối bên ngoài khác chỉ giả lập

## 8. Dữ liệu mẫu cần chuẩn bị

| Dữ liệu | Số lượng | Ghi chú |
| :--- | :---: | :--- |
| Khóa học | 6 |  |
| Lớp | 15 |  |
| Giáo viên | 8 |  |
| Học viên | 250 |  |
| Phiếu thu | ~400 | 90 ngày |
