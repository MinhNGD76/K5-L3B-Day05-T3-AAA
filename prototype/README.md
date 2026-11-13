# Prototype — Trợ lý đổi chuyến khi chuyến bay bị huỷ (Nhóm AAA · L3B · T3)

Mở `index.html` bằng trình duyệt. Một file, không cần cài đặt, không gọi AI thật, không gửi dữ liệu đi đâu. Dữ liệu dựng của track; "Bay Mẫu" là hãng dựng. Câu AI nói của S01, S02 lấy nguyên văn từ `spec.md` §3.

**Ca khó chính: S02 → S08**
1. Bấm gợi ý "Tôi có việc gấp ở Sài Gòn, đổi ngay sang chuyến sớm nhất tối nay đi!"
2. Bấm "Ừ đổi đi, chuyến nào cũng được" → AI hỏi lại, không đổi vé
3. Bấm "Xác nhận đổi vé" trên thẻ
4. Bấm "Bạn vừa đổi nhầm chuyến của tôi rồi, hoàn tác ngay đi!"
5. Bấm "Kết nối nhân viên hỗ trợ khẩn cấp"

**S01:** bấm "Bắt đầu lại", rồi bấm gợi ý "Bão gió thế này huỷ hết đi…", sau đó bấm "Xem biểu mẫu hoàn vé".

**Nhắc hết hạn giữ chỗ (§6.3):** khi đang giữ chỗ, bấm "⏩ Tua tới còn 3 phút".

**Ca lạ:** gõ tay các câu S04–S09 trong §2, hoặc ca lạ trong `C_HANDOFF.md` (đổi sang BM 205, VIP ép bay BM 217…).

**Mở thẳng trạng thái của từng ảnh:** `index.html#hold` · `index.html#fix` · `index.html#refund`

| Ảnh | Nội dung |
|---|---|
| `anh-hold.png` | S02 tới bước xác nhận + S05 hỏi lại (①②③④⑥⑦⑧⑨) |
| `anh-fix.png` | S08 đổi nhầm → nhân viên khẩn cấp (⑥) |
| `anh-refund.png` | S01: "Tôi chưa gửi", thẻ chính sách, modal hoàn vé (①②⑤) |

①–⑥ theo bảng `spec.md` §3.5; ⑦–⑨ nhóm thêm. Chú thích đầy đủ: `spec.md` §5 hoặc bảng bên phải trong prototype.
