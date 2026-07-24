# K4 — Ngày 1: Bài Tập & Phản Ánh
## Khám Phá LLM API | Phiếu Thực Hành

**Thời lượng:** 14h00–18h00
**Cách làm:** Trả lời từng câu ngay sau khi hoàn thành block tương ứng —
đừng để dồn hết về cuối buổi. Thay dòng `*Câu trả lời của bạn*` bằng câu
trả lời thật (chấm tự động sẽ đếm số câu đã trả lời).

---

## Block 1 — API Cơ Bản (trả lời sau Checkpoint 1)

### Câu 1.1 — Độ nhạy của temperature
Gọi `call_openai` với temperature 0.0, 0.7, 1.2 và 1.8 dùng prompt
**"Hãy kể cho tôi một sự thật thú vị về Hà Nội."**

**Bạn nhận thấy quy luật gì qua bốn phản hồi? Ở mức nào phản hồi bắt đầu
kém mạch lạc?** (2–3 câu)
> Khi tăng temperature từ 0.0 lên 1.8, các phản hồi có xu hướng trở nên đa dạng và sáng tạo hơn. Ở temperature thấp (0.0, 0.7), câu trả lời thường ổn định, rõ ràng và tập trung vào thông tin chính; khi tăng lên 1.2, 1.8, mô hình có nhiều cách diễn đạt mới nhưng đôi khi thêm thông tin chi tiết không cần thiết hoặc kém chính xác. Phản hồi bắt đầu có dấu hiệu kém mạch lạc hơn ở khoảng temperature 1.8.

### Câu 1.2 — Chọn temperature cho sản phẩm
**Bạn sẽ đặt temperature bao nhiêu cho trợ lý soạn thảo hợp đồng pháp lý,
và bao nhiêu cho trợ lý viết slogan quảng cáo? Giải thích khác biệt.**
> Đối với trợ lý soạn thảo hợp đồng pháp lý, temperature đặt khoảng 0.0 – 0.2 vì cần câu trả lời chính xác, nhất quán, ít sáng tạo và hạn chế sinh ra nội dung sai lệch hoặc diễn giải không phù hợp. Đối với trợ lý viết slogan quảng cáo, temperature khoảng 0.8 – 1.2 vì cần khả năng sáng tạo, đưa ra nhiều ý tưởng mới lạ và cách diễn đạt đa dạng hơn. Temperature cao giúp mô hình linh hoạt hơn trong việc tạo câu chữ, nhưng cần kiểm soát để tránh nội dung thiếu phù hợp với thương hiệu.

### Câu 1.3 — Đánh đổi chi phí
Kịch bản: 20.000 người dùng hoạt động mỗi ngày, mỗi người gọi API 2 lần,
mỗi lần trung bình ~500 token đầu ra.

**Ước tính chi phí mỗi ngày của model lớn so với model nhỏ cho workload này
(dựa trên bảng giá trong template). Nêu một trường hợp model lớn xứng đáng
với chi phí và một trường hợp model nhỏ là lựa chọn đúng:**
> Với 20.000 người dùng mỗi ngày, mỗi người gọi API 2 lần, tổng cộng có 40.000 lượt gọi/ngày. Mỗi lượt tạo trung bình 500 token đầu ra nên tổng lượng token là 20.000.000 token. Theo bảng giá trong template, GPT-4o có giá output 0.010 USD/1K token nên chi phí khoảng 200 USD/ngày, trong khi GPT-4o-mini có giá output 0.0006 USD/1K token nên chi phí khoảng 12 USD/ngày. Model lớn phù hợp với các tác vụ quan trọng cần độ chính xác và khả năng suy luận cao như phân tích pháp lý, nghiên cứu hoặc xử lý quyết định phức tạp. Ngược lại, model nhỏ là lựa chọn tốt cho các tác vụ có số lượng lớn nhưng yêu cầu đơn giản như chatbot hỗ trợ khách hàng, hỏi đáp thông thường hoặc tạo nội dung cơ bản vì tiết kiệm chi phí và có tốc độ phản hồi nhanh hơn.

---

## Block 2 — System Prompt & Token (trả lời sau Checkpoint 2)

### Câu 2.1 — Sức mạnh của persona
Gọi `chat_with_system_prompt` hai lần với cùng câu hỏi
**"Giải thích máy học (machine learning) là gì?"** nhưng hai system prompt
khác nhau:
- "Bạn là một nhà thơ, trả lời mọi thứ bằng hình ảnh ví von, tránh thuật ngữ."
- "Bạn là kỹ sư phần mềm senior, trả lời chính xác, có ví dụ code khi phù hợp."

**Hai phản hồi khác nhau như thế nào (giọng văn, độ dài, mức kỹ thuật)?
Từ đó rút ra system prompt điều khiển được những khía cạnh nào của phản hồi?**
(3–4 câu)
> Hai phản hồi có sự khác biệt rõ rệt về phong cách và mức độ kỹ thuật. Với system prompt yêu cầu nhà thơ, câu trả lời thường dùng hình ảnh ví von, ngôn ngữ giàu cảm xúc, dễ hiểu nhưng ít đi sâu vào khái niệm kỹ thuật. Với system prompt yêu cầu kỹ sư phần mềm senior, câu trả lời có cấu trúc rõ ràng hơn, sử dụng thuật ngữ chuyên môn, giải thích chi tiết và có thể kèm ví dụ code. Qua đó có thể thấy system prompt có khả năng điều khiển vai trò, giọng văn, mức độ chuyên sâu, cách trình bày và phạm vi kiến thức mà mô hình sử dụng khi trả lời.

### Câu 2.2 — tiktoken vs đếm từ
Chọn một đoạn văn tiếng Việt ~150 từ. So sánh số token theo `count_tokens`
(tiktoken) với ước lượng `số từ / 0.75` mà Part 1 đã dùng.

**Hai con số chênh nhau bao nhiêu phần trăm? Nếu dùng ước lượng thô để dự
toán ngân sách API cho ứng dụng tiếng Việt, bạn sẽ dự toán thiếu hay thừa —
và vì sao?**
> Đoạn văn tiếng Việt khoảng 150 từ và dùng count_tokens bằng tiktoken để đếm được khoảng 172 token. Theo cách ước lượng ở Part 1, số token dự kiến là 150 / 0.75 = 200 token. Hai kết quả chênh lệch khoảng (200 - 172) / 172 × 100 ≈ 16,28%. Nếu dùng cách ước lượng số từ/0.75 để dự toán ngân sách API cho ứng dụng tiếng Việt, có thể sẽ dự toán thiếu/thừa một chút vì tiếng Việt có nhiều từ ghép, dấu câu và ký tự có thể được tokenizer tách thành nhiều token hơn so với tiếng Anh. Vì vậy, khi triển khai thực tế nên dùng số token đo bằng tokenizer của đúng model để có dự toán chi phí chính xác hơn.

---

## Block 3 — Streaming & Độ Bền (trả lời sau Checkpoint 3)

### Câu 3.1 — Trải nghiệm người dùng với streaming
**Xét ba ứng dụng: (a) chatbot văn bản, (b) trợ lý giọng nói đọc to phản hồi,
(c) pipeline dịch tài liệu chạy ngầm ban đêm. Ứng dụng nào hưởng lợi nhiều
nhất từ streaming, ứng dụng nào không cần — và tại sao?** (1 đoạn văn)
> Streaming mang lại lợi ích lớn nhất cho (a) chatbot văn bản vì người dùng có thể nhìn thấy câu trả lời xuất hiện từng phần ngay lập tức thay vì phải chờ toàn bộ phản hồi được tạo xong, giúp giảm cảm giác chờ đợi và tăng tính tương tác. (b) Trợ lý giọng nói đọc to phản hồi cũng hưởng lợi nhiều vì có thể bắt đầu phát âm thanh ngay khi nhận được các đoạn đầu tiên, tạo trải nghiệm hội thoại tự nhiên hơn. Ngược lại, (c) pipeline dịch tài liệu chạy ngầm ban đêm gần như không cần streaming vì người dùng không chờ trực tiếp kết quả; quan trọng hơn là xử lý hoàn thành chính xác và tối ưu tài nguyên. Vì vậy, streaming phù hợp nhất với các ứng dụng tương tác thời gian thực, còn các tác vụ nền có thể dùng xử lý batch thông thường.

### Câu 3.2 — Vì sao backoff theo cấp số nhân?
**Khi API quá tải và hàng nghìn client cùng retry, exponential backoff giúp
gì so với delay cố định? Tra cứu thêm: kỹ thuật "jitter" (thêm độ trễ ngẫu
nhiên) giải quyết vấn đề gì còn sót lại?**
> Exponential backoff giúp hệ thống giảm áp lực khi API đang quá tải bằng cách tăng dần thời gian chờ giữa các lần thử lại (ví dụ: 0.1s, 0.2s, 0.4s, 0.8s), thay vì để hàng nghìn client gửi lại yêu cầu cùng lúc như khi dùng delay cố định. Điều này giúp API có thời gian phục hồi và tránh tình trạng "bão retry" làm quá tải thêm hệ thống. Tuy nhiên, nếu tất cả client đều bắt đầu retry theo cùng một lịch trình, chúng vẫn có thể gửi request đồng thời tại cùng thời điểm. Kỹ thuật jitter giải quyết vấn đề này bằng cách thêm một khoảng trễ ngẫu nhiên vào thời gian backoff, giúp phân tán các lần retry của client, giảm hiện tượng đồng bộ và tăng khả năng request thành công.

---

## Block 4 — Mini-Project (trả lời sau Checkpoint 4)

### Câu 4.1 — Thiết kế persona
**Viết lại system prompt bạn dùng cho trợ lý của mình. Chỉ ra 2 chỗ trong
prompt mà nếu xóa đi, hành vi trợ lý sẽ thay đổi rõ rệt — và mô tả thay đổi
đó:**
> System prompt của tôi: "Bạn là một trợ lý AI hỗ trợ học tập về lập trình và trí tuệ nhân tạo. Hãy giải thích các khái niệm một cách dễ hiểu, từng bước, sử dụng ví dụ thực tế khi cần thiết. Trả lời bằng tiếng Việt, ưu tiên câu trả lời ngắn gọn nhưng đầy đủ, tập trung vào giải pháp có thể áp dụng.". Hai phần quan trọng nếu xóa đi sẽ làm thay đổi hành vi trợ lý rõ rệt: (1) Nếu xóa phần "giải thích các khái niệm một cách dễ hiểu, từng bước, sử dụng ví dụ thực tế", trợ lý có thể trả lời thiên về lý thuyết, khó hiểu hơn và ít hỗ trợ người mới học. (2) Nếu xóa phần "trả lời bằng tiếng Việt, ưu tiên câu trả lời ngắn gọn nhưng đầy đủ", trợ lý có thể chuyển sang ngôn ngữ khác hoặc tạo câu trả lời dài dòng hơn, làm giảm tính phù hợp khi sử dụng trong môi trường học tập.

### Câu 4.2 — Hạn chế & cải thiện
**Trợ lý của bạn giữ history 4 lượt cuối. Hãy mô tả một tình huống hội thoại
cụ thể mà giới hạn này khiến trợ lý trả lời sai/mất ngữ cảnh, và đề xuất một
cách khắc phục (ví dụ: tóm tắt các lượt cũ, tăng giới hạn có chọn lọc...):**
> Một tình huống cụ thể là khi người dùng trao đổi với trợ lý về một dự án lập trình kéo dài nhiều lượt. Ở những lượt đầu, người dùng đã cung cấp thông tin quan trọng như mục tiêu dự án, cấu trúc dữ liệu và các quy tắc cần tuân thủ, nhưng sau nhiều câu hỏi khác nhau, các thông tin này bị loại khỏi history do chỉ giữ lại 4 lượt gần nhất. Khi người dùng quay lại hỏi tiếp về phần ban đầu, trợ lý có thể không còn nhớ yêu cầu trước đó và đưa ra câu trả lời không phù hợp. Một cách khắc phục là thay vì chỉ xóa các lượt hội thoại cũ, hệ thống có thể tự động tóm tắt những thông tin quan trọng trước khi loại bỏ history. Ngoài ra, có thể áp dụng cơ chế lưu có chọn lọc, giữ lại các thông tin quan trọng như mục tiêu, yêu cầu kỹ thuật hoặc quyết định trước đó, trong khi chỉ loại bỏ những câu trao đổi không cần thiết.

---

## Danh Sách Kiểm Tra Nộp Bài

- [x] `python grade.py` — xem điểm tự động, mục tiêu ≥ 75/100
- [x] Cả 4 checkpoint pytest đều pass
- [x] Tất cả 9 câu trong file này đã được trả lời
- [x] Đã copy bài làm vào folder `solution/`, push lên GitHub cá nhân và nộp link repo vào vlearn (theo hướng dẫn README)
