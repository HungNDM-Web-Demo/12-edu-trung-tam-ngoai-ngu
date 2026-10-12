# Kịch bản demo — Quản lý Trung tâm Ngoại ngữ

> Dùng khi trình bày cho chủ trung tâm ngoại ngữ, trung tâm dạy thêm. Thời lượng 12–15 phút. Đi theo một ngày của trung tâm: xem tình hình, mở lớp, tư vấn ghi danh, thu học phí, giáo viên điểm danh, phụ huynh nhận thông báo, nhắc nợ, bảo lưu, xem báo cáo.

---

## 1. Chuẩn bị trước buổi demo

- [ ] Mở sẵn link demo, thử "Đăng nhập nhanh" cả 5 vai trò
- [ ] Đặt lại dữ liệu demo (thanh công cụ demo → Đặt lại dữ liệu) để có 90 ngày dữ liệu, buổi dạy hôm nay cho tài khoản `giaovien`, khoảng 12% học viên nợ quá hạn
- [ ] Đổi tên trung tâm, logo, màu theo thương hiệu khách (Cài đặt → Thương hiệu) nếu đã biết
- [ ] Mở 2 cửa sổ rộng 390 px giả lập điện thoại: cửa sổ thường cho Giáo viên, cửa sổ ẩn danh cho Phụ huynh, để hai vai trò đăng nhập song song; cửa sổ desktop cho Quản lý, Giáo vụ
- [ ] Ghi nhớ dữ liệu mẫu: phụ huynh Trần Văn Hùng có 2 con: Trần Bảo Ngọc (`HV00126`, lớp Giao tiếp B1 của cô Nguyễn Thảo Vy) và Trần Minh Khang (`HV00125`, lớp Thiếu nhi Starters, còn nợ học phí tháng này); học viên Phạm Đức Anh (đóng trọn khóa Giao tiếp B1, đang học)
- [ ] Chuẩn bị điện thoại có app ngân hàng để quét thử QR (chỉ để xem, không chuyển tiền)

| Link | Ghi chú |
| :--- | :--- |
| FE | `http://localhost:3112` hoặc link online |
| Cổng phụ huynh | `http://localhost:3112/phu-huynh` (mở trên điện thoại) |
| Swagger | `https://localhost:7112/swagger` (khi khách hỏi về tích hợp) |

| Tài khoản | Vai trò | Dùng để cho xem |
| :--- | :--- | :--- |
| `admin` | Quản trị viên | Phân quyền, thương hiệu |
| `quanly` | Quản lý | Tổng quan, khóa học, mở lớp, thời khóa biểu, báo cáo |
| `nhanvien` | Giáo vụ | Học viên, ghi danh, học phí, nhắc nợ, học bù, bảo lưu |
| `giaovien` | Giáo viên (GV01 Nguyễn Thảo Vy) | Điểm danh trên điện thoại, nhập điểm, nhận xét |
| `phuhuynh` | Phụ huynh (Trần Văn Hùng) | Thông báo vắng, lịch học, học phí, xin nghỉ |

Mật khẩu: giá trị `DEMO_PASSWORD` trong `.env`, hoặc bấm "Đăng nhập nhanh".

---

## 2. Câu chuyện demo

> Mở đầu: "Anh/chị hình dung hôm nay là một ngày bình thường của trung tâm. Em đi từ sáng lúc anh/chị xem tình hình, tới tối lúc giáo viên điểm danh và phụ huynh nhận thông báo."

| # | Vai trò | Thao tác | Điểm cần nhấn mạnh |
| :---: | :--- | :--- | :--- |
| 1 | Quản lý | Đăng nhập, mở Tổng quan: học viên đang học, thực thu tháng này, nợ quá hạn, chuyên cần 30 ngày, lớp IELTS sắp khai giảng còn thiếu sĩ số | Mở máy là biết tháng này thu được bao nhiêu, ai đang nợ, lớp nào cần đẩy tuyển sinh |
| 2 | Quản lý | Mở lớp Thiếu nhi Starters thứ 7, chủ nhật 08:00; chọn phòng đang có lớp khác cùng giờ để thấy báo trùng, đổi phòng; xem trước 48 buổi, ngày kết thúc tự lùi qua kỳ nghỉ Tết | Không còn xếp lịch bằng Excel, không trùng phòng, trùng giáo viên; nghỉ lễ tự lùi lịch |
| 3 | Giáo vụ | Đổi sang Giáo vụ. Anh Hùng đến đăng ký thêm cho bé Trần Gia Hân 7 tuổi: tạo hồ sơ, hệ thống nhận ra số điện thoại phụ huynh và gợi ý ưu đãi anh chị em 10% | Hệ thống tự nhớ gia đình học viên, không bỏ sót ưu đãi, không giảm tùy tiện |
| 4 | Giáo vụ | Ghi danh bé Hân vào lớp Starters đang học (đã qua 10/48 buổi): học phí 7.200.000 × 38/48 = 5.700.000 ₫, giảm 10% còn 5.130.000 ₫. Thu tiền mặt 3.000.000 ₫, còn nợ 2.130.000 ₫; in phiếu thu | Vào giữa khóa vẫn tính đúng theo buổi còn lại; đóng nhiều lần vẫn rõ ràng từng đồng |
| 5 | Giáo viên | Trên điện thoại, đăng nhập Giáo viên: "Buổi dạy hôm nay" lớp Giao tiếp B1; điểm danh: Trần Bảo Ngọc vắng không phép, một bạn đi muộn; thấy nhãn "Cần gặp giáo vụ" cạnh một học viên; ghi bài tập về nhà, lưu | Điểm danh dưới 1 phút ngay trong lớp; giáo viên nhắc học viên gặp giáo vụ mà không thấy số tiền |
| 6 | Phụ huynh | Trên cửa sổ thứ hai, đăng nhập Phụ huynh: thông báo "Ngọc vắng buổi …" đã có; xem lịch tuần, chuyên cần của Ngọc; chuyển sang Khang xem học phí còn nợ, mã QR chuyển khoản; gửi xin nghỉ buổi tới cho Ngọc | Phụ huynh biết con vắng ngay trong buổi học; xem học phí, đóng tiền không cần lên trung tâm |
| 7 | Giáo vụ | Mở hồ sơ Ngọc: buổi xin nghỉ có nút "Xếp học bù"; hệ thống chỉ gợi ý buổi tương ứng của lớp Giao tiếp B1 khác còn chỗ; chọn một buổi | Học bù có quy tắc rõ ràng, không lộn xộn sĩ số lớp khác |
| 8 | Giáo vụ | Mở Nhắc nợ, lọc quá hạn trên 15 ngày, gửi tin nhắc hàng loạt (giả lập Zalo); gọi một phụ huynh, ghi "Hẹn đóng thứ 6" | Biết chính xác ai nợ, nợ bao lâu, đã nhắc chưa; không nhắc trùng gây phiền phụ huynh |
| 9 | Giáo vụ | Phạm Đức Anh xin bảo lưu vì đi thi học sinh giỏi: bấm Bảo lưu; hệ thống tính giá trị bảo lưu theo số buổi chưa học, vd đã đóng 4.860.000 ₫, học 12/36 buổi thì bảo lưu 3.240.000 ₫, hạn 180 ngày | Hết tranh cãi "em còn bao nhiêu buổi"; hạn bảo lưu tự theo dõi |
| 10 | Giáo viên | Quay lại Giáo viên: nhập điểm giữa khóa, viết nhận xét tháng cho Ngọc theo 5 tiêu chí, bấm Gửi; chuyển sang cửa sổ Phụ huynh thấy nhận xét mới | Phụ huynh thấy con học thế nào hằng tháng, trung tâm chuyên nghiệp hơn |
| 11 | Quản lý | Đổi sang Quản lý, mở Báo cáo: thực thu 6 tháng, công nợ theo tuổi nợ, tỉ lệ lấp đầy lớp, giờ dạy giáo viên tháng này | Có số liệu để quyết định mở thêm lớp, gộp lớp vắng, tính lương giáo viên |
| 12 | Quản trị viên | Đổi sang Quản trị viên, mở ma trận quyền: Giáo viên không có quyền xem học phí; đổi màu thương hiệu | Phân quyền tới từng nút; cổng phụ huynh mang thương hiệu trung tâm |

> Kết: "Toàn bộ học viên, phụ huynh anh/chị vừa thấy là dữ liệu mẫu. Bản triển khai thật sẽ nhập khóa học, bảng học phí, lớp đang chạy của trung tâm mình, và gửi Zalo thật cho phụ huynh."

---

## 3. Câu hỏi khách hay hỏi

| Câu hỏi | Trả lời gợi ý |
| :--- | :--- |
| Có gửi Zalo thật cho phụ huynh không? | Demo chỉ giả lập và hiển thị nội dung tin trên cổng phụ huynh. Bản triển khai kết nối Zalo OA hoặc Zalo ZNS, phí tin do Zalo tính. |
| Phụ huynh có phải cài app không? | Không. Phụ huynh mở link trên điện thoại, có thể thêm biểu tượng ra màn hình chính. App riêng là phần mở rộng nếu trung tâm cần. |
| Học phí tính theo buổi thực học được không? | Demo có trọn khóa và theo tháng, tháng có ngày nghỉ lễ tự giảm theo số buổi. Tính theo buổi thực học (vắng trừ tiền) có thể cấu hình khi triển khai. |
| Học viên nghỉ thì có hoàn học phí không? | Demo không hoàn tiền, chỉ ghi số dư hoặc bảo lưu. Chính sách hoàn tiền theo quy định của trung tâm có thể bổ sung. |
| Có tính lương giáo viên không? | Demo có báo cáo số buổi, số giờ dạy mỗi tháng, kể cả dạy thay. Tính lương theo giờ là phần mở rộng hoặc nối với demo Quản lý nhân sự. |
| Có dạy online, bài tập online không? | Ngoài phạm vi demo. Bản triển khai có thể gắn link Zoom, Google Meet cho từng buổi. |
| Có quản lý khách tư vấn, tuyển sinh không? | Demo có học thử một buổi. Quản lý tư vấn đầy đủ có sẵn ở demo CRM riêng, có thể kết nối. |
| Chuyển khoản có tự xác nhận không? | Demo để giáo vụ bấm xác nhận. Bản triển khai có thể nối với ngân hàng để tự gạch nợ khi tiền về. |
| Có xuất hóa đơn điện tử không? | Có thể kết nối nhà cung cấp hóa đơn điện tử trung tâm đang dùng. Demo chưa kết nối. |
| Có quản lý nhiều cơ sở không? | Bản triển khai có: mỗi cơ sở phòng học, lớp riêng, chủ trung tâm xem gộp. Demo chạy một cơ sở. |

---

## 4. Sau buổi demo

- [ ] Ghi lại yêu cầu khách nêu thêm vào `01-TONG-QUAN-NGHIEP-VU.md`
- [ ] Ghi lại số học viên, số phòng, các khóa đang dạy, cách thu học phí hiện tại (trọn khóa, theo tháng, theo buổi), chính sách bảo lưu, hoàn tiền
- [ ] Gửi link demo và tài khoản `nhanvien`, `giaovien`, `phuhuynh` cho khách tự trải nghiệm (nếu đồng ý)
