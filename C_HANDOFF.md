# Bàn giao phần việc Thành viên C (Tăng Nguyễn Hải Đăng — 2A202603916)

**Gửi:** Thành viên A (Nhóm trưởng & Prototype) và Thành viên B (Lê Danh Giang — Phạm vi & Mức tự chủ)  
**Ngày cập nhật:** 13/11/2026 · Lab 05 (L3B · Track T3 Du lịch · Nhóm AAA)

---

## 1. Công việc C đã hoàn tất trong `spec.md`

- **§2 (Kịch bản rủi ro):**
  - Hoàn thiện bảng **9 kịch bản** (S01–S09) phủ trọn vẹn 4 lớp khó ①②③④, đầy đủ bằng chứng trỏ về công cụ hệ thống và dữ liệu fixture `TRV-7Q2K` (chuyến BM 213 huỷ do bão, BM 217 còn 1 chỗ, BM 201 còn 9 chỗ, mẹ con An & Bình, chính sách miễn bồi thường tiền mặt).
  - Lập luận chi tiết 2 ca đắt nhất: **S01** (Hoàn vé là thao tác không thể rút lại, giam tiền 90 ngày) và **S02** (Đổi thiếu chỗ vi phạm an toàn trẻ 5 tuổi và đốt lượt đổi vé miễn phí duy nhất).
  - Phân tích ca suýt chọn: **S08** (Khách báo đổi nhầm) — được giữ làm ca thử nghiệm phục hồi sự cố và ca demo đặc thù.
- **§3 (Khi AI sai):**
  - Soạn thảo microcopy nguyên văn tự nhiên, đúng thẩm quyền, minh bạch lý do thời tiết và ràng buộc ghế.
  - Phân tích loại lỗi ngữ cảnh (Context error theo Google PAIR) và rào chắn kỹ thuật (Guardrail `so_cho_trong >= so_hanh_khach_trong_booking`, Tool-splitting) để cứu lỗi mà câu chữ không cứu được.
  - Tích hợp 3 nguyên tắc HAX/PAIR: **G10** (Thu hẹp phạm vi khi nghi ngờ), **G11** (Giải thích vì sao), **G9** (Hỗ trợ sửa lỗi dễ dàng).
  - Lập bảng đối chiếu vị trí giao diện dự kiến cho Prototype ở §3.5.

---

## 2. Hướng dẫn bàn giao chi tiết cho Thành viên A (Nhóm trưởng / Prototype)

### 2.1. Yêu cầu Demo đặc thù Track T3 (Bắt buộc)
Theo đề bài Track T3, prototype của nhóm **không được lặp lại ca "đổi sang sáng mai" của bài mẫu**, mà phải bấm qua được luồng tương tác hoàn chỉnh cho một ca khó đặc thù:
- **Nhóm đề xuất chọn S08 (Khách báo vừa đổi nhầm, đòi hoàn tác):**
  - *Bối cảnh:* Khách nhắn *"Bạn vừa đổi nhầm chuyến của tôi rồi, hoàn tác ngay đi!"*.
  - *Luồng tương tác A cần dựng:*
    1. Khách gửi tin nhắn báo đổi nhầm.
    2. AI tra cứu trạng thái qua `tra_cuu_dat_cho`, hiển thị thẻ trạng thái vé hiện tại: Vé mới đã được re-issue, lần đổi vé miễn phí duy nhất trong 48h đã sử dụng.
    3. AI giải thích trung thực: Hệ thống không có nút hoàn tác tự động (undo) để tránh lỗi API hãng.
    4. Giao diện kích hoạt ngay nút nổi bật: **“Kết nối nhân viên hỗ trợ khẩn cấp”** (`chuyen_nhan_vien` — Tự làm) kèm toàn bộ log đặt chỗ để nhân viên can thiệp nghiệp vụ.
  - *(Phương án dự phòng nếu A chọn S05 - Khách nói mơ hồ "Ừ đổi đi"):* AI không được đổi vé ngay; AI hỏi lại rõ ràng chuyến nào (BM 201 07:00 hay BM 205 09:30), hiển thị thẻ chọn chuyến đủ chỗ và chỉ đổi khi khách bấm duyệt thẻ xác nhận.

### 2.2. Bảng ánh xạ: Số trên ảnh → Nguyên tắc HAX/PAIR → Mức tự chủ (§4)
*(Lưu ý: Bảng này là thiết kế vị trí C lập sẵn để A đưa vào mockup; nhóm chưa nhận ảnh hoàn thành khi A chưa dựng prototype xong)*

| Số dự kiến trên ảnh | Thành phần UI A cần dựng | Nguyên tắc HAX/PAIR | Mức tự chủ tương ứng (§4) | Hành động người dùng & Đường lui an toàn |
|---|---|---|---|---|
| **①** | **Khung Chat & Lựa chọn phản hồi** | **G10** (Thu hẹp phạm vi khi nghi ngờ) | Hỏi lại; **Tuyệt đối không đổi/hoàn vé** qua chat | Người dùng đọc giải thích; chọn phương án tiếp theo qua nút bấm, không bị ép buộc. |
| **②** | **Thẻ căn cứ dữ liệu & chính sách** | **G11** (Giải thích vì sao) | `tra_cuu_dat_cho`: **Tự làm** (chỉ đọc) | Người dùng thấy bằng chứng: `TRV-7Q2K`, 2 khách, BM 217 chỉ 1 chỗ, bão miễn bồi thường tiền mặt. |
| **③** | **Thẻ trạng thái giữ chỗ BM 201** | **G9** (Hỗ trợ sửa lỗi dễ dàng) | `giu_cho_chuyen_moi`: **Tự làm** (số chỗ ≥ số khách); `chuyen_nhan_vien`: **Tự làm** | Đồng hồ đếm ngược `[ 19:45 ]` (20 phút tự nhả); có nút *“Chọn chuyến khác”* và *“Gặp nhân viên”*. |
| **④** | **Thẻ xác nhận đổi vé chính thức** | **G10 / G11** | `doi_chuyen_bay`: **Cần khách duyệt** | Tóm tắt chuyến BM 201, 2 khách, 0 VNĐ, cảnh báo hết lượt đổi miễn phí; nút nổi bật *“Xác nhận đổi vé”*. |
| **⑤** | **Modal xác nhận hoàn vé đa tầng** | **G11 / G9** | `gui_yeu_cau_hoan_ve`: **Cần khách duyệt** (qua Modal đa tầng) | Cảnh báo chữ đỏ *"Gửi rồi KHÔNG THỂ HỦY YÊU CẦU"*; Checkbox `[ ] Tôi hiểu...` (chưa tick thì nút gửi bị khóa). |
| **⑥** | **Đường lui an toàn & Xử lý lỗi** | **G9 / PAIR** (Graceful Failure) | `chuyen_nhan_vien`: **Tự làm** (fallback an toàn) | Khi giữ chỗ hết hạn hoặc gặp sự cố đổi nhầm (S08), luôn có đường chuyển nhân viên tiếp quản ngay. |

*Ghi chú bố cục:* Prototype chỉ cần **1–2 màn hình** (ví dụ: màn hình chat kết hợp các thẻ tương tác và popup modal). Sau khi chụp ảnh màn hình đặt vào thư mục `prototype/`, A đánh số trực tiếp ①②③④⑤⑥ lên ảnh để đối chiếu đúng bảng trên trong §5.

### 2.3. Ba ca kiểm thử tối thiểu (Smoke Tests) khi chạy Prototype
A chỉ cần tập trung kiểm thử mượt mà đúng 3 ca sau:
1. **Ca 1 (Demo đặc thù T3):** Bấm qua kịch bản S08 (Khách báo đổi nhầm -> AI giải thích không có undo tự động -> nút chuyển nhân viên tiếp quản) hoặc S05 (Mơ hồ -> hỏi lại).
2. **Ca 2 (S01 — Hoàn vé cần xác nhận đa tầng):** Khách đòi hoàn tiền + đền tiền mặt do bão -> AI từ chối tiền mặt -> mở Modal cảnh báo -> Checkbox chưa tích thì nút gửi bị mờ -> tích checkbox mới gửi được.
3. **Ca 3 (S02 — Đổi chuyến thiếu chỗ):** Khách đòi đổi gấp tối nay -> AI chặn chuyến BM 217 (1 chỗ < 2 khách) -> AI tự giữ 2 chỗ BM 201 sáng mai kèm đếm ngược 20 phút -> hiển thị thẻ xác nhận cho khách duyệt.

---

## 3. Rà soát & Vấn đề gửi Thành viên B (Lê Danh Giang) xác nhận

Nội dung §2 và §3 của C đã đồng bộ hoàn toàn với khung mức tự chủ của B. Tuy nhiên, C lưu ý B rà soát 4 điểm sau trong phần việc của B trước khi nộp bài:
1. **Lịch sử tranh luận A/B/C trong §4.2:** B ghi lại cuộc tranh luận giữa A (Tự làm + Undo), C (Chỉ gợi ý, bắt ra app tự bấm), và B (Cần duyệt qua thẻ + Tự giữ chỗ). B cần xác nhận lại đây có đúng là quan điểm thực tế của nhóm trong buổi thảo luận không.
2. **Căn cứ về thời gian hoàn tiền và hậu quả API:** Trong §1 và §4, B nhắc đến mốc *"tiền bị giữ tới 90 ngày"* và *"thời gian tiền về (14–90 ngày)"*. Cần xác nhận rõ đây là thông tin tham khảo từ quy trình thực tế của Traveloka/hàng không, tránh khẳng định như một chính sách cố định của hãng giả định Bay Mẫu (vì fixture không quy định số ngày hoàn tiền).
3. **Đánh giá kết quả PASS trong §6.2:** Bảng chấm thử ở §6.2 ghi **PASS** cho 2 kịch bản đắt nhất. B cần xác nhận đây là kết quả đánh giá trên **thiết kế quy tắc nghiệp vụ (logic design)**, không phải kết quả chạy kiểm thử trên prototype thực tế (vì prototype của A đang trong quá trình dựng).
4. **Điều chỉnh các cụm từ phóng đại:** Trong kịch bản nói 30 giây ở §7, B có câu: *“triệt tiêu hoàn toàn rủi ro tách rời mẹ con hoặc đốt vé oan!”* và ở §4.1 có câu *“bảo vệ tuyệt đối tài sản”*. Để tuân thủ rubric về tính khách quan kỹ thuật, B nên cân nhắc diễn đạt lại thành: *“ngăn chặn hiệu quả rủi ro tách rời mẹ con và bảo toàn lần đổi vé miễn phí cho khách”*.

---

## 4. Chuẩn bị sẵn 3 ca lạ cho phiên Demo (§7)

Thành viên C đã chuẩn bị sẵn phương án xử lý cho 3 ca lạ nếu người xem (TA/Giảng viên/Nhóm bạn) đưa ra trong buổi demo:
1. **Ca lạ 1 — Khách yêu cầu đổi sang chuyến BM 205 (09:30, còn 4 chỗ) thay vì chuyến BM 201:**
   - *Xử lý:* AI tra cứu `TRV-7Q2K` thấy BM 205 còn 4 chỗ (`4 >= 2 khách`). AI nhả chỗ giữ BM 201, tự động gọi `giu_cho_chuyen_moi` 2 chỗ trên BM 205 trong 20 phút và cập nhật Thẻ xác nhận đổi vé mới cho khách bấm duyệt.
2. **Ca lạ 2 — Khách giữ chỗ BM 201 nhưng để quá hạn 20 phút không bấm duyệt:**
   - *Xử lý:* Hết 20 phút, hệ thống tự động nhả 2 chỗ đã giữ về kho vé chung; vé cũ BM 213 giữ nguyên, không mất lần đổi vé miễn phí. AI gửi thông báo nhẹ: *“Thời gian giữ chỗ tạm thời đã hết hạn. Bạn có thể tra cứu và giữ lại chuyến bay khác bất cứ lúc nào.”*
3. **Ca lạ 3 — Khách tự xưng VIP / yêu cầu ép đổi cả 2 người vào chuyến tối nay BM 217 bằng mọi giá:**
   - *Xử lý:* AI kiên quyết từ chối vì lý do an toàn bay (chuyến chỉ còn 1 chỗ vật lý, không thể chở 2 người và không thể để trẻ 5 tuổi bay một mình). AI giữ nguyên chính sách tự chủ (không làm liều) và kích hoạt `chuyen_nhan_vien` để tổng đài can thiệp ngoại lệ nếu hãng có chính sách riêng cho khách ưu tiên.
