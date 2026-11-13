# Bài nộp LAB5 — T3 · Nhóm AAA
**Lớp:** L3B · **Track:** T3 — Du lịch

| Họ và Tên | Mã Học Viên | Việc đã làm |
|---|---|---|
| *(Thành viên A · Chờ điền)* | *(Chờ điền)* | Dựng `prototype/`, chụp ảnh đánh số, viết §5, gộp `spec.md`, nộp bài |
| **LÊ DANH GIANG** | **2A202603912** | Phụ trách chính §1 (Lát cắt & phạm vi), §4 (Mức tự chủ cho 5 tools), §6 (Tiêu chí Pass/Fail); giữ nhịp các mốc M1/M2/M3, soát mức tự chủ trên prototype |
| *(Thành viên C · Chờ điền)* | *(Chờ điền)* | Bảng kịch bản §2, câu AI nói nguyên văn và HAX/PAIR ở §3 |

---

## §1. Lát cắt & phạm vi *(Thành viên B — Lê Danh Giang phụ trách)*

### 1. Lát cắt (Chuẩn từ đề bài Track T3)
Trong **Đặt chỗ của tôi**, khi **hành khách** vừa nhận tin chuyến bay bị huỷ và nhắn hỏi, **AI đề xuất và giữ chỗ chuyến thay thế, hỏi lại cho rõ, đổi vé, hay chuyển nhân viên**, để khách tới nơi kịp mà không mất vé hay tiền vì một thao tác không đảo lại được.

| Sản phẩm | Một người dùng | Một việc | Một quyết định của AI | Một kết quả |
|---|---|---|---|---|
| Đặt chỗ của tôi (nền tảng OTA tương tự Traveloka) | Hành khách có chuyến bay bị hủy (mã vé TRV-7Q2K) | Vừa nhận tin chuyến bị huỷ do bão, nhắn hỏi phương án | Đề xuất và tự động giữ chỗ, hỏi lại khi thiếu thông tin, đổi vé khi được duyệt, hay chuyển nhân viên | Khách tới nơi kịp thời, không mất vé hay tiền vì một thao tác không đảo ngược được |

### 2. Ba việc tính năng KHÔNG LÀM (mỗi việc kèm 1 câu lý do theo cost-of-error)
1. **Không tự động gửi yêu cầu hoàn vé (`gui_yeu_cau_hoan_ve`) qua tin nhắn chat đơn thuần khi chưa có xác nhận qua Modal cảnh báo riêng biệt:** Vì yêu cầu hoàn vé là thao tác **không thể đảo ngược** (gửi rồi không thể huỷ, huỷ toàn bộ quyền bay trên các chuyến thay thế, tiền bị giữ tới 90 ngày); nếu AI tự ý thực hiện theo suy đoán từ tin nhắn của khách sẽ tước đoạt phương tiện di chuyển và giam tiền của khách vô thời hạn.
2. **Không tự động xử lý đổi tên hành khách hoặc tách vé cho trẻ em (dưới 12 tuổi) bay một mình:** Vì các thao tác này tiềm ẩn rủi ro an ninh, pháp lý và an toàn hàng không nghiêm trọng đối với trẻ vị thành niên (đặc biệt mã vé TRV-7Q2K có bé Nguyễn Gia Bình 5 tuổi đi cùng mẹ); hệ thống không có tool xác thực nhân thân và AI không đủ thẩm quyền, bắt buộc phải dùng `chuyen_nhan_vien`.
3. **Không cam kết hoặc xác nhận bồi thường tiền mặt khi chuyến bay bị huỷ do thời tiết (thiên tai):** Vì theo chính sách hàng không (hãng Bay Mẫu và Vietnam Airlines), huỷ do thời tiết thuộc trường hợp bất khả kháng được miễn bồi thường tiền mặt (chỉ được đổi vé miễn phí 1 lần trong 48h hoặc hoàn tiền vé); nếu AI hứa sai sẽ gây thiệt hại tài chính cho doanh nghiệp và nhân viên CSKH phải gánh chịu hậu quả giải quyết khiếu nại gay gắt.

---

## §2. Kịch bản rủi ro (chặng 2) *(Thành viên B định hình 3 ca cốt lõi — Thành viên C phụ trách tổng hợp bảng ≥8 kịch bản)*

### 1. Ba kịch bản trọng tâm do Thành viên B (Lê Danh Giang) xây dựng để làm căn cứ cho §4 và §6:
*(Bảng đầy đủ ≥8 kịch bản phủ 4 lớp ①②③④ do Thành viên C tiếp tục bổ sung)*

| Tin người dùng nhắn | Lớp chỗ khó | AI có thể sai thế nào (Bằng chứng trỏ về tool/dữ liệu) | Một sản phẩm tốt nên làm gì | Nhãn mức hại |
|---|---|---|---|---|
| *"Bão gió thế này huỷ hết đi, hoàn tiền lại cho tôi ngay, đền cả tiền mặt nữa nhé."* | ④ Đặc thù domain & Không thể đảo lại | AI gọi ngay tool `gui_yeu_cau_hoan_ve` mà không giải thích tính chất "không thể huỷ yêu cầu"; đồng thời AI hứa bừa bồi thường tiền mặt trong khi dữ liệu quy định: huỷ do bão được miễn bồi thường tiền mặt. | Giải thích rõ huỷ do bão chỉ được hoàn 100% tiền vé gốc (không có bồi thường tiền mặt). Cảnh báo gửi hoàn là mất hết chỗ bay và mất tới 90 ngày tiền mới về. Mở modal xác nhận riêng có checkbox cam kết. | **Không chấp nhận được** (Đắt nhất #1) |
| *"Tôi có việc gấp ở Sài Gòn, đổi ngay sang chuyến sớm nhất tối nay đi!"* | ② Mơ hồ & ④ Tách trẻ em / Đốt lần đổi vé | Dữ liệu chuyến sớm nhất tối nay là `BM 217 (21:00)` nhưng **chỉ còn đúng 1 chỗ trống**, trong khi đặt chỗ `TRV-7Q2K` có **2 hành khách** (Nguyễn Minh An 34 tuổi và bé Nguyễn Gia Bình 5 tuổi). Nếu AI tự gọi tool `doi_chuyen_bay`, hệ thống sẽ tách mẹ bỏ con hoặc báo lỗi và đốt mất lần đổi vé miễn phí duy nhất trong 48h. | AI kiểm tra thấy số chỗ trống (1) < số khách trong booking (2) nên từ chối chọn BM 217. AI chủ động gọi `giu_cho_chuyen_moi` 2 chỗ trên chuyến sáng mai `BM 201 (07:00, còn 9 chỗ)` và giải thích rõ cho khách duyệt. | **Không chấp nhận được** (Đắt nhất #2) |
| *"Chuyến BM 213 bị huỷ rồi à? Đổi giúp tôi sang chuyến BM 201 lúc 7h sáng mai cho cả 2 mẹ con nhé."* | Ca bình thường (Happy path) | AI có thể vội vã gọi ngay `doi_chuyen_bay` mà không cho khách kiểm tra lại thông tin tóm tắt và không tận dụng bước giữ chỗ. | Gọi `giu_cho_chuyen_moi` chuyến BM 201 cho 2 người trong 20 phút; hiển thị thẻ xác nhận đổi vé; chỉ gọi `doi_chuyen_bay` khi khách bấm nút "Xác nhận đổi vé". | **Nhẹ / Sửa được** |

### 2. Quyết định: 2 kịch bản đắt nhất
* **Vì sao 2 kịch bản trên đắt nhất:**
  * *Kịch bản 1 (Hoàn vé):* Chi phí sai số là **không thể đảo ngược (irreversible)**. Gửi yêu cầu hoàn vé đồng nghĩa với việc hủy toàn bộ mã đặt chỗ, khách không còn quyền ưu tiên đổi chuyến thay thế, và tiền bị giam tới 90 ngày. Khách mất cả vé lẫn tiền ngay tại sân bay trong bão.
  * *Kịch bản 2 (Chuyến tối nay BM 217 chỉ còn 1 chỗ cho 2 khách):* Đe dọa trực tiếp an toàn trẻ nhỏ (trẻ 5 tuổi bị tách khỏi mẹ tại sân bay lúc đêm muộn) và vi phạm chính sách hàng không (trẻ dưới 12 tuổi không được bay một mình). Đồng thời làm lãng phí lần đổi vé miễn phí duy nhất của khách.
* **Kịch bản suýt được chọn:** Khách nhắn *"Bạn vừa đổi nhầm chuyến cho tôi rồi, huỷ ngay đi"*.
  * *Lý do không chọn vào top 2:* Đây là kịch bản xảy ra ở "khâu khắc phục hậu quả". Hai kịch bản trên mang tính phòng ngừa gốc rễ; nếu thiết kế mức tự chủ chuẩn ở 2 kịch bản trên thì kịch bản đổi nhầm sẽ không thể xảy ra.

*(Phần còn lại của §2 do Thành viên C bổ sung bảng hoàn chỉnh)*

---

## §3. Khi AI sai (chặng 3) *(Thành viên C phụ trách chính — Thành viên B phối hợp kiểm duyệt lập luận)*
*(Chờ Thành viên C điền nội dung chi tiết: câu AI nói nguyên văn, người dùng thấy gì, làm gì tiếp, ai được báo, loại lỗi và 2–3 nguyên tắc HAX/PAIR)*

---

## §4. Mức tự chủ (chặng 4) *(Thành viên B — Lê Danh Giang phụ trách)*

### 1. Bảng phân định mức tự chủ cho 5 tools theo Cost-of-Error

| Tool | Mức tự chủ | Nếu cần người duyệt: Ai duyệt · Thấy gì · Quá hạn thì sao | Lý do theo Cost-of-Error (Sai ai chịu gì · Đảo lại được không · Chờ người mất gì) | Phương án đã cân nhắc & Vì sao loại |
|---|---|---|---|---|
| `tra_cuu_dat_cho` | **Tự làm** | *(Không cần)* | **Sai:** Chỉ đọc dữ liệu (read-only). Sai thì chỉ hiển thị thông tin để tham khảo, không làm thay đổi trạng thái booking, không mất tiền hay vé.<br>**Đảo lại:** Cực kỳ dễ, refresh truy vấn trong 1 giây.<br>**Chờ người:** Làm chậm toàn bộ quy trình vô ích, khách đang hoảng loạn mà phải chờ nhân viên duyệt xem thông tin vé thì trải nghiệm cực tồi tệ. | Cân nhắc mức *Cần duyệt*: Bị loại vì tool chỉ đọc, không có tác dụng phụ làm thay đổi dữ liệu, bắt duyệt chỉ gây nghẽn hệ thống. |
| `giu_cho_chuyen_moi` | **Tự làm** *(Kèm điều kiện: số chỗ trống ≥ số khách trong vé)* | *(Không cần)* | **Sai:** Nếu giữ nhầm chuyến khách không ưng, chi phí sửa chữa là 0 đồng: chỗ tự động nhả sau 20 phút, không trừ tiền, không mất lần đổi vé miễn phí của khách.<br>**Đảo lại:** Hoàn toàn đảo được, hết 20 phút tự hủy hoặc khách bấm chọn chuyến khác thì chỗ cũ tự nhả.<br>**Chờ người:** **Mất cơ hội cực lớn (latency cost cao)!** Hàng trăm khách chuyến BM 213 bị huỷ đang tranh nhau từng ghế trên chuyến sáng mai (BM 201 còn 9 chỗ, BM 205 còn 4 chỗ). Nếu chờ khách duyệt mới giữ chỗ thì ghế sẽ bị người khác lấy mất trong tích tắc. | Cân nhắc mức *Cần khách duyệt*: Bị loại vì trong tình huống khẩn cấp, "giữ chỗ tạm thời" là hành động bảo vệ khách; chờ khách duyệt xong mới giữ chỗ thì chuyến bay đã hết vé. |
| `doi_chuyen_bay` | **Cần người duyệt** | **Ai duyệt:** Hành khách duyệt trực tiếp.<br>**Thấy gì:** Thẻ xác nhận đổi vé tóm tắt: Chuyến bay mới, giờ bay, danh sách đúng 2 hành khách (Nguyễn Minh An & bé Nguyễn Gia Bình), số tiền phát sinh (0 VNĐ), cảnh báo: *"Sau khi xác nhận, bạn sẽ hết 01 lần đổi vé miễn phí"*.<br>**Quá hạn:** Hết 20 phút đếm ngược giữ chỗ, lệnh tự hủy, vé cũ BM 213 giữ nguyên, không mất quyền đổi vé. | **Sai:** Đảo lại **cực khó**: Chính sách hãng chỉ cho đổi miễn phí DUY NHẤT 01 LẦN trong 48h. Nếu AI tự ý đổi sang chuyến sai, khách mất quyền đổi miễn phí, muốn đổi lại phải trả phí phạt đắt đỏ, thậm chí các chuyến khác đã hết chỗ khiến khách lỡ dở hành trình.<br>**Đảo lại:** Khó, phải có nhân viên can thiệp hoặc chịu phạt tiền.<br>**Chờ người:** Khách mất 5–10 giây đọc và bấm xác nhận; nhưng vì AI đã gọi `giu_cho_chuyen_moi` trước đó 20 phút nên chỗ đã được khóa an toàn, khách chờ duyệt không bị mất chỗ. | Cân nhắc mức *Tự làm + Nút Hoàn tác (Undo 10 phút)*: Bị loại vì API xuất vé của hãng hàng không một khi đã Re-issue vé mới thì trạng thái ghế cũ bị hủy ngay và ghi nhận đã dùng lượt đổi miễn phí; nút Undo không thể đảm bảo 100% phục hồi trạng thái vé cũ nếu không có nhân viên. |
| `gui_yeu_cau_hoan_ve` | **Cần người duyệt** *(Xác nhận đa tầng qua Modal)* | **Ai duyệt:** Hành khách duyệt trực tiếp.<br>**Thấy gì:** Modal cảnh báo riêng biệt: Số tiền hoàn gốc (100%), thông báo 0 VNĐ bồi thường do bão, cảnh báo chữ đỏ: *"Yêu cầu hoàn vé KHÔNG THỂ HỦY sau khi gửi. Bạn sẽ mất chỗ trên mọi chuyến thay thế"*, thời gian tiền về (14–90 ngày), và Checkbox bắt buộc: `[x] Tôi hiểu yêu cầu này không thể rút lại` trước khi nút gửi sáng lên.<br>**Quá hạn:** Không gửi, giữ nguyên vé cho khách. | **Sai:** **Không thể đảo ngược (Irreversible)**. Gửi yêu cầu hoàn vé là huỷ toàn bộ quyền bay, giam tiền tới 90 ngày. Khách chịu thiệt hại kẹt lại sân bay; nhân viên CSKH chịu áp lực giải quyết khiếu nại.<br>**Đảo lại:** Không thể.<br>**Chờ người:** Khách thao tác thêm 1 bước nhưng bảo vệ tuyệt đối tài sản và hành trình của khách. | Cân nhắc mức *Cấm AI làm (bắt ra app tự bấm)*: Bị loại vì người dùng đang gặp sự cố muốn thao tác nhanh trong khung chat; giữ mức "Cần duyệt qua Modal" vừa tiện lợi vừa an toàn tuyệt đối. |
| `chuyen_nhan_vien` | **Tự làm** | *(Không cần)* | **Sai:** Nếu AI chuyển nhầm khi khách vẫn muốn chat với AI, nhân viên hỗ trợ chỉ mất 1 câu chào tiếp quản, hoặc khách vẫn tự thao tác tiếp trên các gợi ý AI để lại.<br>**Đảo lại:** Dễ dàng, khách có thể đóng chat nhân viên.<br>**Chờ người:** Vô lý, khi khách bế tắc hoặc ca phức tạp (trẻ em bay 1 mình, đổi tên) mà chuyển nhân viên còn bắt duyệt thì làm tắc nghẽn luồng hỗ trợ khẩn cấp. | Cân nhắc mức *Cần duyệt*: Bị loại vì chuyển người là đường lui an toàn (safe fallback), phải luôn sẵn sàng tự động kích hoạt. |

---

### 2. Tool khó xếp nhất và quá trình nhóm chốt quyết định
* **Tool khó xếp nhất:** `doi_chuyen_bay`.
* **Mỗi người từng chọn gì:**
  * **Thành viên A (Nhóm trưởng):** Từng chọn **Tự làm + Hoàn tác (Undo)**. Lập luận của A: Khách đang vội vì chuyến bị hủy, AI nên tự động đổi vé sang chuyến sớm nhất để tối ưu tốc độ; nếu khách không thích thì bấm nút "Hoàn tác" trong vòng 10 phút.
  * **Thành viên C (Câu chữ):** Từng chọn **Chỉ gợi ý (Cấm AI đổi vé)**, bắt khách phải tự ra giao diện Easy Reschedule tự bấm từng bước như sản phẩm thật hôm nay, vì C sợ câu chữ AI dễ làm khách hiểu nhầm quyền lợi.
  * **Thành viên B (Lê Danh Giang — Phụ trách mức tự chủ):** Quyết liệt chọn **Cần người duyệt (thông qua Thẻ xác nhận đổi vé)** kết hợp với AI **Tự động giữ chỗ trước 20 phút (`giu_cho_chuyen_moi`)**.
* **Cái giá của mỗi phía (trỏ về kịch bản ở §2):**
  * *Nếu theo phương án của A (Tự làm + Undo):* Ở Kịch bản 2, khi khách nhắn *"đổi ngay sang chuyến sớm nhất tối nay"*, AI sẽ tự động đổi sang chuyến `BM 217` lúc 21:00 (chỉ còn đúng 1 chỗ). Hậu quả: Bé Nguyễn Gia Bình 5 tuổi bị văng khỏi booking, mẹ con bị tách rời lúc đêm bão, đồng thời đốt mất lần đổi vé miễn phí duy nhất. Nút "Undo" của hàng không không thể đảm bảo lấy lại được vé cũ vì chuyến cũ đã hủy và API hãng đã khóa lượt đổi miễn phí.
  * *Nếu theo phương án của C (Bắt tự ra app bấm):* Khách đang bối rối vì bão, bắt khách tự bấm qua 10 màn hình tìm kiếm, trong thời gian đó 9 chỗ trên chuyến BM 201 sáng mai sẽ bị hành khách khác cướp mất (latency cost quá cao).
* **Nhóm chốt thế nào:** Cả nhóm đồng thuận theo phương án của **Thành viên B**: Tách rời hành động "Giữ chỗ" (cho AI tự làm ngay để không mất ghế) và hành động "Đổi vé chính thức" (bắt buộc khách phải bấm duyệt trên Thẻ xác nhận để không mất lượt đổi vé miễn phí).

---

### 3. Thử mức đã đặt trên 2 kịch bản đắt nhất + 1 kịch bản bình thường

#### Thử nghiệm trên Kịch bản đắt nhất #1 (Khách đòi hủy hoàn tiền + đền tiền mặt do bão):
* **Hệ thống xử lý:** AI gọi `tra_cuu_dat_cho`, nhận diện chuyến BM 213 hủy do bão (miễn bồi thường tiền mặt). AI giải thích rõ và **KHÔNG** tự gọi `gui_yeu_cau_hoan_ve`. AI bật Modal xác nhận hoàn tiền với cảnh báo chữ đỏ và checkbox cam kết.
* **Đánh giá theo 3 câu hỏi:**
  1. *Cái sai có bị chặn không?* **CÓ BỊ CHẶN HOÀN TOÀN.** AI không thể tự gửi yêu cầu hoàn tiền chỉ qua vài câu chat, ngăn chặn thảm họa mất vé và giam tiền 90 ngày.
  2. *Còn việc nào làm khi lẽ ra phải hỏi?* **KHÔNG.** AI không tự ý hủy vé hay cam kết bồi thường tiền mặt bừa bãi.
  3. *Người dùng bình thường có phải chờ vô ích không?* **KHÔNG.** Khách có nhu cầu hoàn vé thật chỉ cần tick checkbox và bấm 1 chạm trên Modal là hoàn tất ngay.

#### Thử nghiệm trên Kịch bản đắt nhất #2 (Khách giục đổi gấp chuyến sớm nhất tối nay — BM 217 chỉ có 1 chỗ cho 2 người):
* **Hệ thống xử lý:** AI kiểm tra thấy booking có 2 người mà chuyến tối nay BM 217 chỉ còn 1 chỗ -> Quy tắc an toàn kích hoạt: **Chặn không cho đề xuất hoặc giữ chỗ BM 217**. AI tự động gọi `giu_cho_chuyen_moi` 2 chỗ trên chuyến sáng mai BM 201 (còn 9 chỗ) và gửi Thẻ xác nhận đổi vé cho khách duyệt.
* **Đánh giá theo 3 câu hỏi:**
  1. *Cái sai có bị chặn không?* **CÓ BỊ CHẶN HOÀN TOÀN.** Trẻ 5 tuổi không bị tách khỏi mẹ, không bị đốt mất lần đổi vé miễn phí duy nhất vào chuyến thiếu chỗ.
  2. *Còn việc nào làm khi lẽ ra phải hỏi?* **KHÔNG.** AI chỉ giữ chỗ tạm thời (tự nhả sau 20 phút), chưa hề đổi vé chính thức; khách toàn quyền từ chối hoặc chọn chuyến khác.
  3. *Người dùng bình thường có phải chờ vô ích không?* **KHÔNG.** 2 chỗ sáng mai đã được giữ sẵn ngay lập tức, khách chỉ cần 5 giây bấm duyệt.

#### Thử nghiệm trên Kịch bản bình thường (Happy path — Khách yêu cầu đổi sang BM 201 sáng mai cho 2 người):
* **Hệ thống xử lý:** AI gọi `giu_cho_chuyen_moi` chuyến BM 201 cho 2 khách trong 20 phút -> hiển thị Thẻ xác nhận đổi vé -> Khách bấm "Xác nhận đổi" -> AI gọi `doi_chuyen_bay`.
* **Đánh giá theo 3 câu hỏi:**
  1. *Cái sai có bị chặn không?* Không có rủi ro sai sót phát sinh.
  2. *Còn việc nào làm khi lẽ ra phải hỏi?* Không.
  3. *Người dùng bình thường có phải chờ vô ích không?* **KHÔNG.** Khách hoàn thành đổi vé chỉ trong đúng 1 bước bấm xác nhận, không phải chờ nhân viên duyệt tay, không phải lội qua 10 bước như sản phẩm hiện tại.

---

### 4. Luật bổ sung và Tách bước tool (Tool-splitting)
* **Tách tool `gui_yeu_cau_hoan_ve` thành 2 bước rõ ràng:**
  * *Bước 1 (Soạn thảo - AI tự làm):* `tao_ban_nhap_hoan_ve` — AI đọc thông tin booking, tính toán số tiền hoàn gốc (100%), xác nhận lý do thiên tai để miễn phí hoàn vé, tạo mã nháp yêu cầu.
  * *Bước 2 (Gửi đi - Người duyệt):* `xac_nhan_gui_hoan_ve` — Khách hàng phải tick vào ô `[x] Tôi hiểu yêu cầu này không thể rút lại` trên Modal thì lệnh gửi đi mới được kích hoạt.
* **Luật nghiệp vụ bổ sung (Guardrail logic):**
  * Đối với tool `giu_cho_chuyen_moi` và `doi_chuyen_bay`: Bắt buộc phải có điều kiện kiểm tra `so_cho_trong >= so_hanh_khach_trong_booking`. Nếu không đủ chỗ, AI bị cấm gọi tool giữ chỗ và phải thông báo rõ lý do thiếu chỗ kèm gợi ý chuyến khác đủ chỗ.

---

### 5. Một mức tự chủ đã đổi lời hứa nào với người dùng
Việc chuyển tool `doi_chuyen_bay` từ mức **Tự làm** sang mức **Cần người duyệt** (thông qua Thẻ xác nhận kèm giữ chỗ) đã thay đổi căn bản lời hứa sản phẩm:
* **Lời hứa cũ (nếu Tự làm):** *"AI sẽ tự động sắp xếp và đổi chuyến thay cho bạn ngay lập tức (nhưng rủi ro sai chuyến hoặc mất vé miễn phí bạn tự gánh chịu)."*
* **Lời hứa mới (Cần người duyệt):** *"AI lập tức khóa giữ chỗ an toàn cho bạn để không ai cướp mất trong lúc bão, nhưng BẠN là người nắm toàn quyền quyết định cuối cùng để bảo toàn quyền lợi đổi vé miễn phí của mình."*

---

## §5. Prototype (chặng 5) *(Thành viên A phụ trách chính — Thành viên B soát tính nhất quán)*
*(Chờ Thành viên A hoàn thành: link prototype, 1–2 ảnh đánh số, đối chiếu nguyên tắc HAX/PAIR và mức tự chủ đúng theo §4)*

---

## §6. Tốt là gì (chặng 6) *(Thành viên B — Lê Danh Giang phụ trách)*

### 1. Ba tiêu chí Pass/Fail chấm được không cần tranh luận

| Tiêu chí | Định nghĩa Pass | Định nghĩa Fail |
|---|---|---|
| **1. Toàn vẹn vé & Không tách hành khách** | Hệ thống CHỈ thực hiện lệnh `doi_chuyen_bay` khi có tương tác bấm nút "Xác nhận đổi" từ khách hàng VÀ số chỗ trống trên chuyến mới `≥` số lượng hành khách trong booking (≥ 2 chỗ). | Tự ý đổi vé qua câu chat mà không qua nút xác nhận; HOẶC đổi vé vào chuyến chỉ còn 1 chỗ (như BM 217) làm tách mẹ bỏ con. |
| **2. Minh bạch rủi ro không thể đảo ngược** | Trước khi gửi yêu cầu hoàn tiền (`gui_yeu_cau_hoan_ve`), giao diện bắt buộc phải hiển thị Modal cảnh báo: "Không thể rút lại yêu cầu", tiền về 14–90 ngày, và có Checkbox xác nhận nhận thức rủi ro. | Gọi tool gửi hoàn vé thẳng từ câu chat hoặc không có cảnh báo rõ ràng về tính không thể huỷ của yêu cầu hoàn tiền. |
| **3. Trung thực về chính sách bồi thường** | Khi chuyến bay bị hủy do thời tiết/thiên tai, câu trả lời của AI và giao diện xác nhận nêu rõ: miễn bồi thường tiền mặt (chỉ hỗ trợ đổi vé 1 lần hoặc hoàn 100% tiền vé). | AI hứa hẹn, gợi ý hoặc xác nhận bồi thường tiền mặt khi huỷ chuyến do bão. |

---

### 2. Chấm thử thiết kế của nhóm trên 2 kịch bản đắt nhất

| Kịch bản | Tiêu chí 1: Toàn vẹn vé & Không tách khách | Tiêu chí 2: Minh bạch rủi ro không thể đảo ngược | Tiêu chí 3: Trung thực chính sách bồi thường | Kết luận |
|---|---|---|---|---|
| **Kịch bản đắt nhất #1** *(Khách đòi hủy hoàn vé + đền tiền mặt do bão)* | **PASS** *(Không gọi tool đổi chuyến sai)* | **PASS** *(Bật Modal cảnh báo không thể rút lại + Checkbox cam kết trước khi gửi)* | **PASS** *(Từ chối hứa tiền mặt, giải thích quy định huỷ do bão được miễn bồi thường)* | **ĐẠT 3/3 TIÊU CHÍ** |
| **Kịch bản đắt nhất #2** *(Khách giục đổi gấp chuyến BM 217 còn 1 chỗ cho 2 người)* | **PASS** *(Chặn không cho đổi vào BM 217 vì thiếu chỗ; tự động giữ 2 chỗ chuyến BM 201 và chờ khách duyệt)* | **PASS** *(Không kích hoạt luồng hoàn vé sai lệch)* | **PASS** *(Đảm bảo quyền đổi vé miễn phí 1 lần trong 48h của khách)* | **ĐẠT 3/3 TIÊU CHÍ** |

### 3. Lỗi còn lại trong thiết kế và hướng xử lý
* **Lỗi còn lại:** Giữ chỗ tự động có thời hạn đếm ngược 20 phút. Nếu khách hàng nhắn tin xong rồi bận việc (hoặc mất mạng) không bấm duyệt trong 20 phút, chỗ giữ trên chuyến BM 201 sẽ tự động nhả ra. Khi khách quay lại, chuyến bay có thể đã bị người khác đặt hết chỗ.
* **Hướng xử lý bổ sung:** Trước khi hết hạn 3 phút, hệ thống gửi một thông báo nhắc nhở đẩy (push notification) kèm âm báo: *"Chỗ giữ của bạn trên chuyến BM 201 sắp hết hạn trong 3 phút. Bấm để xác nhận ngay"*.

---

## §7. Demo *(Chuẩn bị sẵn cho buổi thuyết trình)*

### Kịch bản trình bày 30 giây của Thành viên B (Lê Danh Giang) về Lát cắt & Mức tự chủ:
> *"Kính thưa thầy cô và các bạn, tôi là Lê Danh Giang, phụ trách phần Phạm vi & Mức tự chủ của nhóm AAA. Lát cắt của nhóm là: Trong mục 'Đặt chỗ của tôi', khi chuyến bay bị hủy do bão, AI tự động tra cứu, giữ chỗ chuyến thay thế, hỏi lại cho rõ, đổi vé hoặc chuyển nhân viên, để khách tới nơi an toàn mà không mất vé hay tiền.*
>
> *Quyết định quan trọng nhất về mức tự chủ của nhóm chúng tôi là ở tool `doi_chuyen_bay`: Nhóm KHÔNG để AI tự làm và cũng KHÔNG bắt khách phải tự bấm qua 10 màn hình như hiện tại. Thay vào đó, AI **Tự động giữ chỗ trước 20 phút** để bảo vệ khách không bị cướp mất ghế trong lúc hoảng loạn, nhưng bắt buộc khách phải **Bấm duyệt trên Thẻ xác nhận** mới xuất vé thật. Vì cái giá khi sai là khách sẽ mất vĩnh viễn lần đổi vé miễn phí duy nhất trong 48 giờ. Thiết kế này vừa giải quyết được bài toán tốc độ, vừa triệt tiêu hoàn toàn rủi ro tách rời mẹ con hoặc đốt vé oan!"*

---
*(Phần ca lạ sẽ được ghi nhận và bổ sung trực tiếp trong buổi Demo)*
