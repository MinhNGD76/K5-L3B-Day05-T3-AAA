# Phân công nhóm AAA — LAB5 · L3B · T3 Du lịch

**Repo nộp:** https://github.com/MinhNGD76/K5-L3B-Day05-T3-AAA
**Hạn nộp:** 23:59 ngày 13/11/2026
**Nhóm trưởng (người dựng prototype và nộp bài):** Thành viên A

> Điền tên thật vào bảng bên dưới. Sau buổi lab, chép cột "Việc đã làm" sang bảng thành viên ở đầu `spec.md`, kèm **mã học viên đúng**.

| Vai | Họ và tên | Mã học viên | Phụ trách chính |
|---|---|---|---|
| **A · Nhóm trưởng + Prototype** | *(Chờ A điền)* | *(Chờ A điền)* | Dựng `prototype/`, chụp ảnh đánh số, viết §5, gộp `spec.md`, nộp bài |
| **B · Phạm vi & Mức tự chủ** | LÊ DANH GIANG | 2A202603912 | §1, §4, §6, giữ giờ 3 mốc M1/M2/M3, soát mức tự chủ trên prototype |
| **C · Câu chữ AI & Kịch bản** | *(Chờ C điền)* | *(Chờ C điền)* | Bảng kịch bản §2, câu AI nói nguyên văn và HAX/PAIR ở §3 |

**Luật chung:** chặng 1–4 cả nhóm cùng làm. Từ chặng 5, mỗi người giữ phần của mình. Ai cũng phải giải thích được phần có tên mình: TA sẽ hỏi bất kỳ ai, không giải thích được thì phần đó 0 điểm.

---

## Lịch theo chặng

| Phút | Chặng | A · Nhóm trưởng + Prototype | B · Phạm vi & Mức tự chủ (Lê Danh Giang) | C · Câu chữ & Kịch bản |
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

## Sản phẩm từng người

**A · Nhóm trưởng + Prototype**
- [ ] `prototype/index.html` (hoặc `prototype/README.md` có link): 1–2 màn hình, dữ liệu dựng, không backend
- [ ] Ca khó **khác** ca "sáng mai" của mẫu. Đề xuất: chuyến BM 217 lúc 21:00 chỉ còn 1 chỗ cho 2 hành khách, hoặc khách báo "bạn vừa đổi nhầm"
- [ ] Màn hình phải có: căn cứ AI dựa vào · đếm ngược giữ chỗ · thẻ xác nhận đổi vé · nút hoàn tác · nút chuyển nhân viên · việc bị cấm thì không có nút làm
- [ ] 1–2 ảnh PNG có đánh số ①②③… trong `prototype/`
- [ ] Viết §5: link/file, công cụ, phần nào mock, có gọi AI thật không, cách hiện đã chọn và các cách đã loại
- [ ] Gộp bài, kiểm checklist nộp bên dưới, push và nộp link

**B · Phạm vi & Mức tự chủ (LÊ DANH GIANG)**
- [x] §1, §4, §6 trong `spec.md`
- [x] Giữ giờ: M1 phút 45, M2 phút 125, M3 phút 200. Đến mốc nào thì gọi TA kiểm mốc đó
- [x] Trong §4 ghi rõ tool khó xếp nhất: mỗi người chọn gì, nhóm chốt thế nào
- [x] Soát prototype: mức tự chủ trên màn hình phải khớp §4

**C · Câu chữ AI & Kịch bản**
- [ ] §2: ≥8 kịch bản, mỗi kịch bản trỏ về một tool hoặc một dòng dữ liệu, có nhãn mức hại
- [ ] §3: câu AI nói nguyên văn cho 2 kịch bản đắt nhất, 2–3 nguyên tắc HAX/PAIR, chỉ ra một lỗi mà sửa câu chữ không cứu được
- [ ] Bảng "số trên ảnh → nguyên tắc → mức tự chủ" để đưa vào §5
- [ ] Kịch bản demo và chuẩn bị sẵn 3 ca lạ có thể bị hỏi
