# Phân công nhóm AAA — LAB5 · L3B · T3 Du lịch

**Repo nộp:** https://github.com/MinhNGD76/K5-L3B-Day05-T3-AAA
**Hạn nộp:** 23:59 ngày 13/11/2026
**Nhóm trưởng (người dựng prototype và nộp bài):** Thành viên A

> Điền tên thật vào bảng bên dưới. Sau buổi lab, chép cột "Việc đã làm" sang bảng thành viên ở đầu `spec.md`, kèm **mã học viên đúng**.

| Vai | Họ và tên | Mã học viên | Phụ trách chính |
|---|---|---|---|
| **A · Nhóm trưởng + Prototype** | *(Chờ A điền)* | *(Chờ A điền)* | Dựng `prototype/`, chụp ảnh đánh số, viết §5, gộp `spec.md`, nộp bài |
| **B · Phạm vi & Mức tự chủ** | LÊ DANH GIANG | 2A202603912 | §1, §4, §6, giữ giờ 3 mốc M1/M2/M3, soát mức tự chủ trên prototype |
| **C · Câu chữ AI & Kịch bản** | TĂNG NGUYỄN HẢI ĐĂNG | 2A202603916 | Bảng kịch bản §2, câu AI nói nguyên văn và HAX/PAIR ở §3 |

**Luật chung:** chặng 1–4 cả nhóm cùng làm. Từ chặng 5, mỗi người giữ phần của mình. Ai cũng phải giải thích được phần có tên mình: TA sẽ hỏi bất kỳ ai, không giải thích được thì phần đó 0 điểm.

---

## Lịch theo chặng

| Phút | Chặng | A · Nhóm trưởng + Prototype | B · Phạm vi & Mức tự chủ (Lê Danh Giang) | C · Câu chữ & Kịch bản (Tăng Nguyễn Hải Đăng) |
|---|---|---|---|---|
| 0–10 | 1 · Đọc đề | Xem prototype mẫu 3 phút, chọn công cụ | Viết §1: lát cắt và 3 việc không làm | Đọc mục Hard tests và tin mồi |
| 10–45 | 2 · Kịch bản → **M1** | Viết 3 kịch bản, chốt 2 kịch bản đắt nhất cùng nhóm | Viết 3 kịch bản, kiểm đủ 4 lớp ①②③④ | Gộp thành bảng ≥8 kịch bản trong §2 |
| 45–90 | 3 · Khi AI sai | Phác màn hình trên giấy theo §3 | Kiểm lập luận "đã loại gì, vì sao" | Viết §3: câu AI nói, người dùng thấy gì, làm gì tiếp, ai được báo, loại lỗi, HAX/PAIR |
| 90–125 | 4 · Mức tự chủ → **M2** | 5' đầu mỗi người tự xếp mức cho 5 tool; sau đó tranh luận | B ghi lại chỗ lệch, chốt và viết §4 | Thử mức đã chốt trên 2 kịch bản đắt nhất + 1 kịch bản bình thường |
| 125–140 | Nghỉ | | | |
| 140–200 | 5 · Prototype → **M3** | Dựng 1–2 màn hình bấm được, chụp 1–2 ảnh có đánh số, viết §5 | Soát prototype đúng với §4 | Đưa câu chữ vào prototype, ghi chú: số trên ảnh → nguyên tắc G__ → mức tự chủ |
| 200–210 | 6 · Tốt là gì | Sửa lỗi prototype | Viết 3 tiêu chí Pass/Fail và chấm thử | Soạn kịch bản demo 4 phút |
| 210–240 | Demo | Bấm prototype qua ca khó | Trình bày lát cắt (30") và một mức tự chủ + cái giá khi sai | Trả lời ca lạ, ghi ca lạ vào §7 |

---

## Sản phẩm từng người & Trạng thái hoàn thành

**A · Nhóm trưởng + Prototype (Chờ A xác nhận thông tin & thực hiện)**
- [ ] `prototype/index.html` (hoặc `prototype/README.md` có link): 1–2 màn hình, dữ liệu dựng, không backend
- [ ] Dựng ca khó đặc thù T3: S02 (BM 217 chỉ 1 chỗ cho 2 khách) hoặc S08 (khách báo đổi nhầm) hoặc S05 (khách nói mơ hồ)
- [ ] Màn hình có đủ: căn cứ AI dựa vào · đếm ngược giữ chỗ 20p · thẻ xác nhận đổi vé · modal hoàn vé có checkbox · nút chuyển nhân viên · việc cấm thì không có nút làm
- [ ] 1–2 ảnh PNG có đánh số ①②③… đặt trong thư mục `prototype/`
- [ ] Viết §5 trong `spec.md`: link/file, công cụ, phần nào mock, có gọi AI thật không, cách hiện đã chọn và các cách đã loại; đối chiếu ảnh đánh số với HAX/PAIR và mức tự chủ §4
- [ ] Gộp bài, kiểm tra checklist nộp bên dưới, push lên GitHub và nộp link

**B · Phạm vi & Mức tự chủ (LÊ DANH GIANG)**
- [x] §1 (Lát cắt & 3 việc không làm), §4 (Mức tự chủ 5 tools), §6 (3 tiêu chí Pass/Fail) trong `spec.md`
- [x] Trong §4 ghi rõ tool khó xếp nhất (`doi_chuyen_bay`): mỗi người từng chọn gì, cái giá mỗi phía, cách nhóm chốt
- [ ] Giữ giờ 3 mốc: M1 (phút 45 - xong kịch bản), M2 (phút 125 - xong mức tự chủ), M3 (phút 200 - prototype bấm được); gọi TA kiểm tra trực tiếp
- [ ] Soát prototype: đối chiếu mức tự chủ trên màn hình prototype của A với quy định tại §4 (chờ A hoàn thiện mockup)

**C · Câu chữ AI & Kịch bản (TĂNG NGUYỄN HẢI ĐĂNG)**
- [x] §2 trong `spec.md`: Bảng 9 kịch bản phủ 4 lớp ①②③④, bằng chứng trỏ về tool/dữ liệu fixture `TRV-7Q2K`, nhãn mức hại; lập luận 2 ca đắt nhất (S01, S02) và 1 ca suýt chọn (S08)
- [x] §3 trong `spec.md`: Microcopy nguyên văn, phân loại lỗi ngữ cảnh/hệ thống, 3 nguyên tắc HAX/PAIR (G10, G11, G9), phân tích lỗi sửa câu chữ không cứu được và bảng đối chiếu vị trí UI
- [x] Soạn `C_HANDOFF.md`: Bàn giao chi tiết 6 thành phần tương tác cho A, 3 ca smoke test, đối chiếu mức tự chủ với B và chuẩn bị sẵn 3 ca lạ cho Demo
- [ ] Phối hợp với A đưa câu chữ vào prototype và ánh xạ mã số ảnh thật vào §5 (chờ A dựng prototype)
- [ ] Tham gia thuyết trình và xử lý ca lạ trong phiên Demo tại lớp

---

## Hướng dẫn bàn giao nội bộ giữa A, B và C

1. **Từ B sang A & C:** B giữ vai trò trọng tài về mức tự chủ (§4) và tiêu chí nghiệm thu (§6). A và C bám sát 5 mức tự chủ đã chốt để thiết kế giao diện và microcopy, không tự ý nới lỏng quyền hạn của AI.
2. **Từ C sang A:** C đã bàn giao chi tiết câu thoại nguyên văn, các trạng thái cảnh báo, và bảng đối chiếu 6 vị trí thành phần UI tại §3.5 của `spec.md` và trong `C_HANDOFF.md`. A dựa vào bảng này để dựng mockup mà không cần sáng tác thêm câu chữ.
3. **Từ A sang nhóm:** A dựng xong prototype và chụp 1–2 ảnh màn hình đánh số ①②③… Sau đó A điền link/file vào §5 và báo nhóm để B soát mức tự chủ, C soát microcopy trước khi nộp.

---

## Quy trình nộp bài chuẩn (Lớp L3B · Track T3)

- **Repo nộp bài:** `https://github.com/MinhNGD76/K5-L3B-Day05-T3-AAA` (Tạo repo mới, không fork repo mẫu).
- **Chế độ hiển thị:** Bắt buộc để **Public (Công khai)**. Kiểm tra bằng cách mở link trên tab ẩn danh (Incognito window).
- **Thời hạn chót (Deadline):** **23:59 ngày 13/11/2026** (áp dụng cho lớp L3B).
- **Kênh nộp:** Nộp đường link repo GitHub vào biểu mẫu/kênh nộp do giảng viên thông báo trong buổi học.

---

## Checklist nộp bài cuối cùng (A kiểm trước khi push & nộp link)

- [ ] **Bảng thành viên ở đầu `spec.md`:** Đã điền đầy đủ họ tên thật, mã học viên đúng của cả 3 thành viên A, B, C; cột việc đã làm khớp với thực tế.
- [ ] **Tính toàn vẹn của `spec.md`:** Đủ 7 phần (§1 đến §7) theo đúng cấu trúc template; không còn các ghi chú nháp hoặc placeholder chưa điền.
- [ ] **Thư mục `prototype/`:** Chứa file mã nguồn chạy được (`index.html`) hoặc file `README.md` dẫn link trực tiếp tới prototype online (Figma/Lovable/v0...).
- [ ] **Ảnh chụp minh chứng:** Có ít nhất 1–2 ảnh chụp màn hình PNG rõ nét đặt trong `prototype/`, có đánh số các vị trí tương tác ①②③...
- [ ] **Khớp nối §5:** Nội dung §5 trong `spec.md` giải thích rõ ràng từng số trên ảnh tương ứng với nguyên tắc HAX/PAIR nào và mức tự chủ nào (§4).
- [ ] **Kịch bản khó đặc thù:** Prototype bấm qua được ca khó đã chọn (S02 hoặc S08 hoặc S05), thể hiện rõ luồng sửa lỗi hoặc chuyển nhân viên.
- [ ] **An toàn & Bảo mật:** Kiểm tra không có API key, token bí mật hoặc dữ liệu cá nhân thật trong repo.
- [ ] **Kiểm tra truy cập Public:** Đã mở thử link repo từ trình duyệt ẩn danh không đăng nhập, đảm bảo không bị lỗi 404 hoặc Private repo.
