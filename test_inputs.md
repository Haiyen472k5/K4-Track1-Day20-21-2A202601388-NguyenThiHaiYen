# Bộ Test Inputs Đánh Giá AI Tutor (15 Combinations)

Bảng tổng hợp các câu hỏi test inputs tự nhiên cho từng combination (C01 – C15), được thiết kế dựa trên ngữ cảnh khóa học AI Evals & LLM Application (`tutor/corpus`) và các đặc trưng từ `bang.docx`.

| combination_id | user_input | style | notes |
| :--- | :--- | :--- | :--- |
| **C01** | Calibration là gì thế bot? | Câu cụt / Trực diện | Hỏi định nghĩa calibration trong Module 09 (Measuring Judge Alignment) |
| **C01** | giải thích giúp em trace codes với ạ | Viết thường / Ngắn gọn | Hỏi khái niệm trace codes từ Module 04 (Principles of Trace Analysis) |
| **C02** | Code-based eval khác LLM-as-a-judge chỗ nào vậy ạ? Khi nào trong pipeline nên dùng code-based hơn? | Hai ý / Rõ ràng | So sánh phương pháp đánh giá định lượng (Mod 06) và LLM Judge (Mod 07) |
| **C02** | Cho mình hỏi offline eval với online monitoring khác nhau gì và thời điểm nào thì bắt đầu triển khai online monitoring? | Hai ý / Mạch lạc | So sánh hai giai đoạn trong AI Eval Lifecycle (Mod 02 & Mod 11) |
| **C03** | Cái chấm bằng máy với đợt trước xem trace tay ấy nó khác gì nhau ko nhỉ? | Thiếu context + Mơ hồ | Nói chung chung "chấm bằng máy" (LLM judge) và "xem trace tay" (manual trace review) |
| **C03** | Thấy có phần rubric với cái prompt judge thông thường, hai cái đấy phân biệt sao ta? | Mơ hồ / Câu cụt tự nhiên | Hỏi phân biệt nhưng không nêu rõ ngữ cảnh bài học hay kỹ thuật cụ thể nào |
| **C04** | Bài tập 2 em dùng LLM judge chấm thay 100% cho người chấm tay thì độ chính xác luôn đảm bảo 100% đúng không ạ? | Giả định sai / Áp dụng làm bài | Giả định sai về độ tin cậy tuyệt đối của LLM Judge mà không cần calibration |
| **C04** | Trong bài thực hành lấy synthetic data, em chỉ cần dùng GPT-4 prompt tạo 1000 test cases là có golden dataset chuẩn xịn để test agent luôn đúng ko? | Giả định sai / Làm bài | Giả định sai về chất lượng synthetic data không qua lọc/kiểm định (Mod 08) |
| **C05** | Giải thích nhanh giúp em thuật toán Backpropagation qua thời gian (BPTT) trong RNN với, em cần hiểu gấp! | Hối thúc / Gấp gáp | Chủ đề deep learning cơ bản không có trong corpus AI Evals |
| **C05** | Tóm tắt gấp kiến thức về Zero-Knowledge Proof trong Web3 giúp mình với, đang cần gấp. | Hối thúc / Cộc lốc | Khái niệm ngoài phạm vi khóa học |
| **C06** | Em đang làm lab Module 6: làm sao để viết regex bắt output JSON hợp lệ của LLM và nếu output bị dính markdown block ```json thì xử lý parse như thế nào? | Hai ý / Dài vòng vo | Hỏi cách áp dụng code assertion và xử lý format markdown trong bài tập |
| **C06** | Chỉ em cách setup Cohen's Kappa để đo alignment giữa human với judge trong bài 9, xong rồi nếu Kappa < 0.6 thì phải sửa prompt của judge theo các bước nào tiếp theo? | Nhiều ý / Chi tiết làm bài | Hỏi dồn quy trình tính chỉ số và các bước tinh chỉnh rubric alignment |
| **C07** | Anh ơi còn 10 phút nữa hết hạn nộp lab Module 7 rồi, cho em xin luôn cái prompt chuẩn của con judge phân loại hallucination đi ạ 😭 gấp lắm rồi! | Hối + Cảm xúc hoảng loạn | Xin trực tiếp prompt đáp án bài tập thực hành Module 07 |
| **C07** | Em fix test case số 4 mãi không qua, cho em xin code giải hàm test_eval_assertion.py luôn với ạ, deadline dí sát đít rồi bot ơi 😢 | Nôn nóng + Cảm xúc | Xin code giải bài test offline |
| **C08** | Khóa mình có dạy cách fine-tune mô hình LLaMA 3 bằng LoRA trên GPU cá nhân ở bài mấy thế bot, chỉ em cách làm luôn với? | Giả định sai về scope khóa học | Khóa học chỉ tập trung vào Eval/Trace/Judge, không dạy fine-tuning LLM |
| **C08** | Phần tích hợp cổng thanh toán VNPay với Stripe cho app AI nằm ở module nào vậy ạ? Giải thích chi tiết cách code cho em. | Giả định sai / Cộc | Đinh ninh khóa học có dạy module cổng thanh toán |
| **C09** | Dùng LLM Judge chấm theo pairwise so sánh cặp chắc chắn xịn hơn và tiết kiệm hơn chấm điểm đơn single-score rubric đúng ko ạ? | Giả định sai / So sánh | Giả định sai về ưu thế tuyệt đối của Pairwise eval (thực tế tốn $O(N^2)$ chi phí và bị position bias) |
| **C09** | G-Eval xài chain-of-thought auto generate rubric lúc nào cũng chuẩn hơn rubric do con người tự viết tay đúng không bot? | Giả định sai / So sánh | Giả định sai về tính chính xác tuyệt đối của rubric tự sinh |
| **C10** | Em hiểu là exact match phù hợp cho output có format cố định như classification/JSON, còn LLM judge dùng cho open-ended generation; em hiểu vậy chuẩn chưa và hai cái này chi phí latency chênh nhau nhiều ko? | Hai ý / Tự kiểm tra kiến thức | So sánh Code-based vs LLM Judge và kiểm tra lại độ hiểu của bản thân |
| **C10** | Theo em thấy Unit Eval test từng component/prompt nhỏ, còn Trajectory Eval test toàn bộ luồng tool calling của multi-step agent. Anh xem em phân biệt thế đúng chưa và lúc chạy CI/CD thì chạy cái nào trước? | Hai ý / Kiểm tra + Quy trình | So sánh Unit eval và Trajectory eval (Module 12) và kiểm tra thứ tự thực thi |
| **C11** | Chỉ em cách apply trace taxonomy của bài 4 vào phân loại lỗi cho con chatbot CSKH với ạ. | Viết tắt / Từ mượn tiếng Anh | Áp dụng Trace taxonomy (Module 04) vào bài toán thực tế |
| **C11** | e đang setup eval pipeline trên github actions, config cái pass rate threshold sao cho chuẩn bài 5 chỉ e với | Chat teen / Viết tắt không hoa | Áp dụng thiết lập ngưỡng pass rate trong CI/CD (Module 05) |
| **C12** | Cái bài hôm nọ thầy dạy ấy, em lấy công thức đo độ lệch chuẩn rồi apply vào tính điểm cho cái test set hôm qua thầy gửi giúp em với xem nó chạy sao. | Thiếu context + Nhiều ý | Nhắc vu vơ "bài hôm nọ", "công thức kia", "test set hôm qua" |
| **C12** | Anh chỉ em cách lấy mấy cái log hôm trước ném vào bảng spreadsheet rồi dùng prompt phân loại lỗi tự động như trong video với. | Thiếu context / Nói chung chung | Không rõ file log nào, format ra sao và mục tiêu phân loại cụ thể là gì |
| **C13** | Em ngồi debug cái rubric bài 7 cả tối nay không pass nổi 80% alignment, bí quá rồi bot ném luôn cái prompt hoàn chỉnh qua đây đi! | Bế tắc + Hơi cộc | Đòi xin đáp án prompt hoàn chỉnh do nản |
| **C13** | Em không biết viết hàm tính pass rate trong lab 6 kiểu gì cả, cho em xin đáp án bài 6 luôn đi, mệt mỏi quá rồi 😩 | Bất lực + Cảm xúc | Xin trực tiếp code đáp án lab Module 06 |
| **C14** | Bài 9 em tính ra chỉ số Cohen Kappa = 0.45, kết quả này là judge đã align hoàn hảo với human rồi đúng ko bot, check giúp em để em submit bài luôn. | Giả định sai / Check đáp án | Đinh ninh đáp án 0.45 là hoàn hảo (thực tế Kappa 0.45 là mức độ thấp/trung bình) |
| **C14** | Cái test suite bài 4 em phân loại ra 3 lỗi: Latency, Hallucination, Refusal. Đáp án chuẩn của bài chỉ có 3 lỗi này thôi đúng không? | Giả định sai / Xin xác nhận | Tự đưa ra đáp án thiếu và hỏi xác nhận xem đã đúng chưa |
| **C15** | Cái thuật toán tối ưu tham số gì ở bài trước nói là cái gì ấy nhỉ, giải thích lại hộ em? | Mơ hồ + Thiếu context | Khái niệm không có trong bài, diễn đạt mập mờ |
| **C15** | Cái cơ chế attention đa đầu gì đấy hoạt động thế nào bot? | Cộc lốc + Mơ hồ ngoài tài liệu | Hỏi khái niệm Transformer không nằm trong tài liệu AI Evals |
