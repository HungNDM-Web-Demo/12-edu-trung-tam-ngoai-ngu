# Kịch bản kiểm thử nghiệm thu — Quản lý Trung tâm Ngoại ngữ

> Test case theo use case trong `03-USE-CASE.md`. Phần nền (đăng nhập, phân quyền, đặt lại dữ liệu) dùng TC-SYS-01 đến TC-SYS-10 trong `ZDOCS/03-KIEN-TRUC/USE-CASE-NEN.md` §8.

---

## 1. Cách chạy

| Mục | Nội dung |
| :--- | :--- |
| Môi trường | Chạy cả hai chế độ: dữ liệu mẫu (`mock`) và BE thật (`api`) |
| Dữ liệu | Đặt lại dữ liệu demo trước mỗi lượt test; test case ghi "Sau TC-xx" thì chạy nối tiếp trong cùng lượt |
| Tài khoản | Theo cột "Vai trò" của từng test case, dùng "Đăng nhập nhanh": `quanly`, `nhanvien` (Giáo vụ), `giaovien`, `phuhuynh` |
| Thiết bị | Test case vai trò Giáo viên, Phụ huynh chạy ở cửa sổ rộng 390 px; cần hai vai trò song song thì dùng thêm cửa sổ ẩn danh |
| Test liên quan ngày | TC-18, TC-19 phụ thuộc số buổi còn lại trong tháng hiện tại; ghi ngày chạy và số buổi thực tế vào biên bản rồi tính lại theo BR-07 |
| Đạt | Kết quả thực tế khớp toàn bộ cột "Kết quả mong đợi" |

Dữ liệu mẫu dùng trong test (dữ liệu giả):

| Loại | Giá trị |
| :--- | :--- |
| Khóa học | `GT-B1` Tiếng Anh giao tiếp B1: 36 buổi × 90 phút, thang 10, F 5.400.000 ₫, M 2.000.000 ₫, S 12, sĩ số 6–15. `IE-45` IELTS Foundation 4.5: 40 buổi × 120 phút, band mục tiêu 4.5, F 9.600.000 ₫, không có học phí tháng. `KID-ST` Tiếng Anh thiếu nhi Starters: 48 buổi × 90 phút, thang 10, F 7.200.000 ₫, M 1.300.000 ₫, S 8, sĩ số 6–12 |
| Ưu đãi | Anh chị em ruột 10%; Học viên cũ 5% |
| Giáo viên | `GV01` Nguyễn Thảo Vy (tài khoản `giaovien`); `GV02` Lê Hoàng Nam |
| Phòng | Phòng 201 sức chứa 16; Phòng 202 sức chứa 12; Phòng 301 sức chứa 20 |
| Lớp | GT-B1 lớp A: GV01, Phòng 201, 18:00–19:30, các thứ học có ngày hôm nay, đã học 12 buổi, sĩ số 14/15. GT-B1 lớp B: GV02, Phòng 301, 18:00–19:30 các thứ khác lớp A, đã học 14 buổi, sĩ số 15/15. GT-B1 lớp C: GV02, Phòng 202, 19:45–21:15 cùng các thứ với lớp A, đã học 10 buổi, sĩ số 10/12. IE-45 lớp A: đã học 8 buổi, sĩ số 9/12. KID-ST lớp A: đã học 10 buổi, sĩ số 8/12 |
| Phụ huynh | Trần Văn Hùng, 0903456789, tài khoản `phuhuynh`, có 2 con dưới đây |
| Học viên | `HV00126` Trần Bảo Ngọc, 15 tuổi, GT-B1 lớp A, trọn khóa đã đóng đủ; 12 buổi đã diễn ra: 10 Có mặt, 1 Đi muộn, buổi 12 Vắng có phép chưa học bù. `HV00125` Trần Minh Khang, 9 tuổi, KID-ST lớp A theo tháng; khoản tháng trước đã đóng 800.000 ₫, còn nợ 500.000 ₫ (quá hạn); khoản tháng này 1.300.000 ₫ chưa đóng. `HV00130` Phạm Đức Anh, GT-B1 lớp A trọn khóa từ buổi 1, phải thu 4.860.000 ₫ đã đóng đủ, đã học 12 buổi. `HV00140` Vũ Thị Mai Anh, 20 tuổi, GT-B1 lớp A theo tháng, khoản 2.000.000 ₫ quá hạn 20 ngày. `HV00150` Lý Gia Bảo, số dư 300.000 ₫, khoản tháng 2.000.000 ₫ chưa tới hạn |

---

## 2. Test case

### 2.1. Khóa học, giáo viên, phòng học

| Mã | UC | Tình huống | Vai trò | Các bước | Kết quả mong đợi |
| :--- | :--- | :--- | :--- | :--- | :--- |
| TC-01 | UC-01 | Thêm khóa chỉ thu trọn khóa | Quản lý | 1. Khóa học → Thêm 2. Mã `TOEIC-650`, "TOEIC 650+", 30 buổi × 120 phút, thang 10, F 5.100.000 ₫, để trống học phí tháng 3. Lưu 4. Mở lớp khóa này, ghi danh một học viên | Hiện bình quân 170.000 ₫/buổi; khóa có trong danh sách; khi ghi danh chỉ có hình thức trọn khóa |
| TC-02 | UC-01 | Dữ liệu khóa sai | Quản lý | 1. Nhập số buổi 6 2. Nhập S = 20 3. Nhập F 5.100.500 ₫ | Cả ba báo lỗi tại ô, không lưu |
| TC-03 | UC-01 | Xóa khóa đã có lớp | Quản lý | 1. Chọn `GT-B1`, bấm Xóa | Hệ thống từ chối, gợi ý ngừng khóa |
| TC-04 | UC-02 | Gắn tài khoản giáo viên | Quản lý | 1. Thêm giáo viên, chọn tài khoản `giaovien` 2. Chọn một tài khoản vai trò Giáo viên mới chưa gắn, lưu | Bước 1 báo tài khoản đã gắn với GV01; bước 2 lưu được, mã `GV` + 2 số kế tiếp |
| TC-05 | UC-02 | Giảm sức chứa phòng đang dùng | Quản lý | 1. Sửa Phòng 201 sức chứa 12 2. Lưu | Từ chối, liệt kê GT-B1 lớp A (sĩ số tối đa 15) |
| TC-06 | UC-02 | Ngày nghỉ làm lùi lịch | Quản lý | 1. Phòng học → Ngày nghỉ → thêm ngày của buổi sắp tới gần nhất của GT-B1 lớp A, tên "Nghỉ đột xuất" 2. Xác nhận | Bước 1 liệt kê buổi bị ảnh hưởng của mọi lớp học ngày đó; sau bước 2, buổi đó dời sang ngày học kế tiếp theo lịch, các buổi sau lùi theo, ngày kết thúc dự kiến lùi một buổi; tổng số buổi vẫn là 36 |

### 2.2. Lớp và lịch học

| Mã | UC | Tình huống | Vai trò | Các bước | Kết quả mong đợi |
| :--- | :--- | :--- | :--- | :--- | :--- |
| TC-07 | UC-03 | Mở lớp hợp lệ | Quản lý | 1. Lớp học → Mở lớp 2. Khóa `GT-B1`, GV02, Phòng 301, thứ 2-4-6, 18:00, khai giảng thứ 2 tuần sau 3. Lưu | Mã lớp dạng `GT-B1-{yyMM}{chữ cái}`; 36 buổi 18:00–19:30; nếu không có ngày nghỉ thì buổi 36 là thứ 6, sau ngày khai giảng 81 ngày; trạng thái "Đang tuyển sinh", sĩ số 0/15 |
| TC-08 | UC-03 | Trùng giáo viên | Quản lý | 1. Mở lớp `GT-B1`, GV01, Phòng 301, cùng các thứ và giờ 18:00 với GT-B1 lớp A | Báo GV01 đã dạy GT-B1 lớp A ở buổi cụ thể (thứ, giờ, phòng), không lưu |
| TC-09 | UC-03 | Phòng nhỏ hơn sĩ số tối đa | Quản lý | 1. Mở lớp `GT-B1` sĩ số tối đa 15 ở Phòng 202 | Báo lỗi sức chứa tại ô phòng |
| TC-10 | UC-03 | Khai giảng sai thứ | Quản lý | 1. Chọn thứ 2-4-6, ngày khai giảng là một ngày thứ 3 | Báo "Ngày khai giảng phải là một trong các thứ học" |
| TC-11 | UC-03 | Hủy lớp | Quản lý | 1. Sau TC-07, hủy lớp vừa mở, lý do "Không đủ học viên" 2. Mở GT-B1 lớp A | Bước 1: lớp "Đã hủy"; bước 2: không có nút "Hủy lớp" |
| TC-12 | UC-04 | Hủy một buổi | Quản lý | 1. Thời khóa biểu → buổi sắp tới của GT-B1 lớp A → Hủy buổi, lý do "Giáo viên ốm" 2. Đổi sang Phụ huynh | Buổi "Đã hủy"; một buổi mới thêm vào cuối lịch, ngày kết thúc dự kiến lùi; cổng phụ huynh của Ngọc có thông báo đổi lịch |

### 2.3. Học viên và ghi danh

| Mã | UC | Tình huống | Vai trò | Các bước | Kết quả mong đợi |
| :--- | :--- | :--- | :--- | :--- | :--- |
| TC-13 | UC-05 | Thêm học viên nhỏ tuổi | Giáo vụ | 1. Thêm "Trần Gia Hân", sinh cách đây 7 năm, không nhập phụ huynh, Lưu 2. Thêm phụ huynh Trần Văn Hùng, 0903456789 3. Lưu | Bước 1 báo "Học viên dưới 18 tuổi cần ít nhất một phụ huynh"; bước 2 gợi ý "Có thể là anh chị em của HV00125, HV00126"; bước 3 cấp mã `HV` + 5 số kế tiếp |
| TC-14 | UC-05 | Trùng họ tên và ngày sinh | Giáo vụ | 1. Thêm học viên "Trần Bảo Ngọc" cùng ngày sinh với HV00126 | Hộp "Có thể trùng học viên" liệt kê HV00126 |
| TC-15 | UC-05 | Hồ sơ học viên | Giáo vụ | 1. Mở hồ sơ HV00126 | Tab Lớp học có GT-B1 lớp A, chuyên cần 11 / 12 = 91,7%; tab Học phí có khoản trọn khóa "Đã đóng"; tab Thông tin có phụ huynh Trần Văn Hùng |
| TC-16 | UC-06 | Ghi danh trọn khóa từ buổi 1 | Giáo vụ | 1. Sau TC-07 (chưa chạy TC-11), ghi danh học viên "Nguyễn Hoàng Long" (thêm mới, 22 tuổi) vào lớp vừa mở, trọn khóa, không ưu đãi 2. Xác nhận | Học phí 5.400.000 ₫, phải thu 5.400.000 ₫, hạn đóng là ngày khai giảng; ghi danh "Chờ học", mã `GD{yyMMdd}{nnn}`; sĩ số 1/15 |
| TC-17 | UC-06 | Vào giữa khóa có ưu đãi anh chị em | Giáo vụ | 1. Sau TC-13, ghi danh Trần Gia Hân vào KID-ST lớp A từ buổi 11, trọn khóa, ưu đãi Anh chị em ruột | Học phí 7.200.000 × 38 / 48 = 5.700.000 ₫; giảm 570.000 ₫; phải thu 5.130.000 ₫; sĩ số KID-ST lớp A 9/12 |
| TC-18 | UC-06 | Ghi danh theo tháng | Giáo vụ | 1. Ghi danh học viên mới "Đỗ Thu Hà" (22 tuổi) vào GT-B1 lớp C theo tháng, từ buổi kế tiếp 2. Ghi lại số buổi còn lại trong tháng của học viên | Khoản tháng đầu = min(2.000.000, 2.000.000 × số buổi / 12), làm tròn xuống 1.000 ₫. Vd còn 9 buổi: 1.500.000 ₫; còn 13 buổi: 2.000.000 ₫. Hạn đóng là ngày 10 hoặc ngày buổi bắt đầu, lấy ngày muộn hơn |
| TC-19 | UC-06 | Làm tròn khoản tháng | Giáo vụ | 1. Ghi danh theo tháng vào KID-ST lớp A vào thời điểm học viên còn 7 buổi trong tháng | Khoản tháng = 1.300.000 × 7 / 8 = 1.137.500, làm tròn xuống còn 1.137.000 ₫ |
| TC-20 | UC-06 | Lớp đầy, ghi danh trùng | Giáo vụ | 1. Ghi danh một học viên vào khóa `GT-B1` 2. Ghi danh HV00126 vào GT-B1 lớp A | Bước 1: GT-B1 lớp B (15/15) hiện mờ, không chọn được; bước 2: báo "Học viên đã có trong lớp" |
| TC-21 | UC-06 | Khóa không có học phí tháng | Giáo vụ | 1. Ghi danh một học viên vào IE-45 lớp A | Chỉ có hình thức trọn khóa; học phí từ buổi 9 = 9.600.000 × 32 / 40 = 7.680.000 ₫ |

### 2.4. Chuyển lớp, bảo lưu, nghỉ học

| Mã | UC | Tình huống | Vai trò | Các bước | Kết quả mong đợi |
| :--- | :--- | :--- | :--- | :--- | :--- |
| TC-22 | UC-07 | Bảo lưu | Giáo vụ | 1. Hồ sơ HV00130 → GT-B1 lớp A → Bảo lưu từ hôm nay, lý do "Thi học sinh giỏi" 2. Xác nhận | Số buổi chưa học 24; giá trị bảo lưu 4.860.000 × 24 / 36 = 3.240.000 ₫; hạn bảo lưu hôm nay + 180 ngày; ghi danh "Bảo lưu"; sĩ số GT-B1 lớp A còn 13/15 |
| TC-23 | UC-07 | Chuyển sang khóa khác | Giáo vụ | 1. Hồ sơ HV00130 (chưa bảo lưu) → Chuyển lớp → IE-45 lớp A từ buổi 9 2. Xác nhận | Giá trị còn lại 3.240.000 ₫; học phí mới 7.680.000 ₫; chênh lệch 4.440.000 ₫ tạo khoản "Thu thêm chuyển lớp"; ghi danh cũ "Đã chuyển lớp", ghi danh mới ở IE-45 lớp A |
| TC-24 | UC-07 | Chuyển lớp khi còn nợ quá hạn | Giáo vụ | 1. Hồ sơ HV00140 → Chuyển lớp | Báo "Học viên còn khoản quá hạn, cần đóng trước khi chuyển lớp", không chuyển |
| TC-25 | UC-07 | Nghỉ học theo tháng | Giáo vụ | 1. Hồ sơ HV00140 → Nghỉ học từ hôm nay | Khoản quá hạn 2.000.000 ₫ vẫn còn trong công nợ; không còn khoản tháng sau; ghi danh "Đã nghỉ" |

### 2.5. Điểm danh và học bù

| Mã | UC | Tình huống | Vai trò | Các bước | Kết quả mong đợi |
| :--- | :--- | :--- | :--- | :--- | :--- |
| TC-26 | UC-08 | Điểm danh và báo vắng | Giáo viên, Phụ huynh | 1. Đăng nhập `giaovien` trên điện thoại, mở "Buổi dạy hôm nay" → GT-B1 lớp A (buổi 13) trong khoảng 15 phút trước giờ học tới hết hạn 2. Đặt Trần Bảo Ngọc "Vắng không phép", Vũ Thị Mai Anh "Đi muộn", nhập bài tập về nhà 3. Lưu 4. Mở cổng phụ huynh bằng `phuhuynh` | 14 học viên mặc định "Có mặt"; sau lưu hiện "Có mặt 12, Đi muộn 1, Vắng 1", buổi đánh dấu đã điểm danh; cổng phụ huynh có tin "{Tên trung tâm}: Trần Bảo Ngọc vắng buổi 13 lớp {mã lớp} ngày {hôm nay}…" và bài tập về nhà |
| TC-27 | UC-08 | Nhãn cần gặp giáo vụ | Giáo viên | 1. Mở danh sách điểm danh GT-B1 lớp A | Vũ Thị Mai Anh (quá hạn 20 ngày) có nhãn "Cần gặp giáo vụ", không hiện số tiền; Trần Bảo Ngọc không có nhãn |
| TC-28 | UC-08 | Điểm danh ngoài thời hạn | Giáo viên | 1. Mở buổi 11 của GT-B1 lớp A 2. Mở buổi 14 | Buổi 11: nút lưu khóa, hiện "Đã hết hạn điểm danh, liên hệ giáo vụ"; buổi 14: hiện "Chưa tới giờ điểm danh" |
| TC-29 | UC-08 | Mở lớp không dạy | Giáo viên | 1. Gõ thẳng URL điểm danh của GT-B1 lớp B | Chuyển tới `/forbidden`; danh sách lớp của giáo viên không có lớp B |
| TC-30 | UC-08 | Giáo vụ sửa sau hạn | Giáo vụ | 1. Chi tiết GT-B1 lớp A → Buổi học → buổi 11 → sửa một học viên sang "Vắng có phép" 2. Lưu không lý do 3. Nhập lý do, lưu | Bước 2 bị chặn, yêu cầu lý do; bước 3 lưu được, nhật ký ghi tài khoản `nhanvien`, giá trị trước và sau |
| TC-31 | UC-08 | Mất kết nối khi lưu (chế độ `api`) | Giáo viên | 1. Chọn trạng thái cho vài học viên 2. Ngắt mạng, bấm Lưu 3. Bật mạng, bấm Lưu lại | Bước 2 báo "Chưa lưu được, thử lại", lựa chọn giữ nguyên; bước 3 lưu thành công, mỗi học viên chỉ có một bản ghi điểm danh |
| TC-32 | UC-09 | Xếp học bù | Giáo vụ | 1. Hồ sơ HV00126 → buổi 12 "Vắng có phép" → Xếp học bù 2. Chọn buổi 11 của GT-B1 lớp C 3. Khi buổi đó được điểm danh "Có mặt" cho Ngọc, mở lại hồ sơ | Bước 1 chỉ gợi ý các buổi 11–14 chưa diễn ra của lớp C (10/12); không có lớp B (đầy), không có buổi 15 trở đi; bước 2 Ngọc có trong danh sách điểm danh buổi đó với nhãn "Học bù"; bước 3 buổi 12 gốc "Đã học bù", được tính vào chuyên cần (vd 12 buổi đã diễn ra, 10 Có mặt, 1 Đi muộn, 1 Đã học bù thì 100%) |
| TC-33 | UC-09 | Không học bù buổi vắng không phép | Giáo vụ | 1. Sau TC-26, mở hồ sơ HV00126, buổi 13 | Buổi 13 "Vắng không phép" không có nút "Xếp học bù" |

### 2.6. Điểm và nhận xét

| Mã | UC | Tình huống | Vai trò | Các bước | Kết quả mong đợi |
| :--- | :--- | :--- | :--- | :--- | :--- |
| TC-34 | UC-10 | Kết quả cuối khóa thang 10 | Giáo viên | 1. Học viên P: giữa khóa 6,0, cuối khóa 7,5, chuyên cần 91,7% 2. Học viên Q: giữa khóa 4,0, cuối khóa 5,0 3. Học viên R: giữa khóa 6,0, cuối khóa 7,5, chuyên cần 75,0% | P: 0,4 × 6,0 + 0,6 × 7,5 = 6,9, Đạt; Q: 4,6, Chưa đạt; R: 6,9 nhưng Chưa đạt vì chuyên cần dưới 80% |
| TC-35 | UC-10 | Điểm sai bước | Giáo viên | 1. Nhập 7,3 cho bài thang 10 2. Nhập band 5,25 cho bài IELTS 3. Nhập 10,5 | Cả ba báo lỗi tại ô; 7,25 và 5,5 thì lưu được |
| TC-36 | UC-10 | Nhận xét tháng | Giáo viên, Phụ huynh | 1. Viết nhận xét cho Ngọc 10 ký tự, Lưu 2. Viết đủ 5 tiêu chí và lời nhận xét 60 ký tự, Lưu nháp 3. Phụ huynh xem 4. Giáo viên bấm Gửi, phụ huynh xem lại | Bước 1 báo tối thiểu 20 ký tự; bước 3 phụ huynh chưa thấy nhận xét; bước 4 phụ huynh thấy 5 tiêu chí và lời nhận xét |

### 2.7. Học phí

| Mã | UC | Tình huống | Vai trò | Các bước | Kết quả mong đợi |
| :--- | :--- | :--- | :--- | :--- | :--- |
| TC-37 | UC-11 | Thu đủ bằng tiền mặt | Giáo vụ | 1. Sau TC-16, Học phí → tìm Nguyễn Hoàng Long 2. Chọn khoản 5.400.000 ₫, Tiền mặt, khách đưa 5.500.000 ₫ 3. Hoàn tất | Tiền thối 100.000 ₫; phiếu thu mã `PT{yyMMdd}{nnnn}`; khoản "Đã đóng"; bản in A5 có số tiền bằng chữ "Năm triệu bốn trăm nghìn đồng" |
| TC-38 | UC-11 | Thu một phần, phân bổ theo hạn | Giáo vụ | 1. Tìm Trần Minh Khang, chọn cả hai khoản (còn nợ 500.000 ₫ và 1.300.000 ₫) 2. Sửa số tiền 1.500.000 ₫, Tiền mặt, Hoàn tất | Xem trước phân bổ: 500.000 ₫ vào khoản tháng trước, 1.000.000 ₫ vào khoản tháng này; sau khi lưu, tháng trước "Đã đóng", tháng này "Đóng một phần" còn nợ 300.000 ₫ |
| TC-39 | UC-11 | Thu vượt số còn nợ | Giáo vụ | 1. Khang, chọn cả hai khoản 2. Nhập 2.000.000 ₫ | Báo "Số tiền tối đa 1.800.000 ₫", không lưu |
| TC-40 | UC-11 | Tiền khách đưa không đủ | Giáo vụ | 1. Khang, thu 1.800.000 ₫ 2. Nhập tiền khách đưa 1.500.000 ₫ | Nút Hoàn tất khóa, hiện "Còn thiếu 300.000 ₫" |
| TC-41 | UC-11 | Trừ số dư, chuyển khoản | Giáo vụ | 1. Tìm Lý Gia Bảo, chọn khoản 2.000.000 ₫ 2. Tick "Trừ số dư 300.000 ₫" 3. Chuyển khoản → Đã nhận tiền | Số cần thu 1.700.000 ₫; QR hiện 1.700.000 ₫, nội dung là mã phiếu thu; khoản "Đã đóng"; số dư về 0 ₫ |
| TC-42 | UC-11 | Khoản tháng tự tạo | Giáo vụ | 1. Học phí → lọc tháng hiện tại, hình thức theo tháng | Mọi ghi danh theo tháng đang học có đúng một khoản tháng này, ngày tạo ngày 1, hạn ngày 10 (khoản tháng đầu theo BR-09) |
| TC-43 | UC-11 | Bấm Hoàn tất hai lần (chế độ `api`) | Giáo vụ | 1. Bấm Hoàn tất hai lần thật nhanh | Chỉ một phiếu thu được tạo |
| TC-44 | UC-11 | Hủy phiếu thu | Giáo vụ, Quản lý | 1. Sau TC-38, giáo vụ mở phiếu thu 1.500.000 ₫ 2. Đổi sang Quản lý, Hủy, lý do "Thu nhầm học viên" | Bước 1 không có nút Hủy; bước 2 phiếu "Đã hủy", khoản tháng trước về "Đóng một phần" còn nợ 500.000 ₫, khoản tháng này về "Chưa đóng" 1.300.000 ₫ |

### 2.8. Nhắc nợ

| Mã | UC | Tình huống | Vai trò | Các bước | Kết quả mong đợi |
| :--- | :--- | :--- | :--- | :--- | :--- |
| TC-45 | UC-12 | Danh sách và lọc nợ | Giáo vụ | 1. Mở Nhắc nợ 2. Lọc "Quá hạn 16–30 ngày" | Bước 1 có Vũ Thị Mai Anh (quá hạn 20 ngày, chữ đỏ) và Trần Minh Khang; Lý Gia Bảo không có nếu hạn còn hơn 3 ngày; bước 2 còn Vũ Thị Mai Anh |
| TC-46 | UC-12 | Gửi tin nhắc, chặn gửi lại | Giáo vụ | 1. Chọn Vũ Thị Mai Anh → Gửi tin nhắc 2. Bấm gửi lại | Tin giả lập đúng mẫu BR-25 (tên trung tâm, tên khoản, họ tên, 2.000.000 ₫, hạn dd/MM/yyyy); bước 2 nút khóa, chú thích "Đã nhắc ngày {hôm nay}, gửi lại từ ngày {hôm nay + 3}" |
| TC-47 | UC-12 | Ghi kết quả gọi điện | Giáo vụ | 1. Mai Anh → Ghi kết quả "Hẹn đóng", ngày mai, ghi chú "Mẹ hẹn chuyển khoản" | Dòng hiện ngày hẹn đóng; hồ sơ học viên tab Lịch sử có lần nhắc |
| TC-48 | UC-12 | Gửi hàng loạt | Giáo vụ | 1. Sau TC-46, chọn Mai Anh và Khang → Gửi tin nhắc | Báo "Đã tạo 1 tin, bỏ qua 1 học viên đã nhắc trong 3 ngày"; chỉ Khang có tin mới |

### 2.9. Cổng phụ huynh

| Mã | UC | Tình huống | Vai trò | Các bước | Kết quả mong đợi |
| :--- | :--- | :--- | :--- | :--- | :--- |
| TC-49 | UC-13 | Chỉ thấy con mình | Phụ huynh | 1. Đăng nhập `phuhuynh` 2. Gõ thẳng URL hồ sơ của HV00140 | Bước 1 có nút đổi giữa Trần Minh Khang và Trần Bảo Ngọc, không có học viên khác; bước 2 bị chặn |
| TC-50 | UC-13 | Học phí trên cổng | Phụ huynh | 1. Chọn Trần Minh Khang → Học phí | Hai khoản còn nợ 500.000 ₫ và 1.300.000 ₫, tổng 1.800.000 ₫, hạn đóng từng khoản, QR giả lập 1.800.000 ₫, lịch sử phiếu thu |
| TC-51 | UC-13 | Xin nghỉ | Phụ huynh, Giáo viên | 1. Chọn Ngọc, buổi kế tiếp sau hôm nay → Xin nghỉ, lý do "Đi khám răng" 2. Giáo viên mở danh sách buổi đó 3. Phụ huynh xin nghỉ buổi hôm nay khi còn dưới 2 giờ tới giờ học | Bước 1 buổi hiện "Đã xin nghỉ"; bước 2 Ngọc hiện sẵn "Vắng có phép" kèm lý do; bước 3 báo "Cần gửi trước giờ học ít nhất 2 giờ" |

### 2.10. Tổng quan và báo cáo

| Mã | UC | Tình huống | Vai trò | Các bước | Kết quả mong đợi |
| :--- | :--- | :--- | :--- | :--- | :--- |
| TC-52 | UC-14 | Tổng quan cập nhật theo phiếu thu | Quản lý | 1. Ghi lại "Thực thu tháng này", "Nợ quá hạn" 2. Chạy TC-37, TC-38 3. Quay lại Tổng quan | Thực thu tăng 6.900.000 ₫ (5.400.000 + 1.500.000); nợ quá hạn giảm đúng phần TC-38 phân bổ vào khoản quá hạn (ít nhất 500.000 ₫) |
| TC-53 | UC-14 | Giáo viên, phụ huynh không có Tổng quan | Giáo viên, Phụ huynh | 1. Đăng nhập nhanh Giáo viên 2. Đăng nhập nhanh Phụ huynh 3. Gõ thẳng `/dashboard` | Giáo viên vào thẳng Lớp học, phụ huynh vào thẳng Cổng phụ huynh; bước 3 chuyển tới `/forbidden` |
| TC-54 | UC-15 | Giờ dạy giáo viên | Quản lý | 1. Ghi lại giờ dạy tháng này của GV01 2. Chạy TC-26 3. Mở lại báo cáo | Giờ dạy GV01 tăng 1 buổi, 1,5 giờ |
| TC-55 | UC-15 | Tỉ lệ lấp đầy | Quản lý | 1. Báo cáo → Lớp học | GT-B1 lớp A 14/15 = 93,3%; lớp B 15/15 = 100%; lớp C 10/12 = 83,3% |
| TC-56 | UC-15 | Phiếu thu hủy không tính | Quản lý | 1. Sau TC-44, xem Thực thu và tab Phiếu thu đã hủy | Thực thu không gồm phiếu 1.500.000 ₫ đã hủy; phiếu có trong tab Phiếu thu đã hủy kèm người hủy, lý do |

---

## 3. Biên bản chạy thử

| Ngày | Người test | Chế độ | Số TC đạt / tổng | Lỗi ghi nhận |
| :--- | :--- | :--- | :---: | :--- |
| | | | | |
