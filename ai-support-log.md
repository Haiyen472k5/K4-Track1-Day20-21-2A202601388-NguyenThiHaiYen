# AI Support Log

> Ghi lại bạn đã dùng AI (ChatGPT/Claude/Kimi...) ở những bước nào khi làm deliverables. Trung thực là một phần của bài nộp — không ai làm một mình, quan trọng là bạn giữ quyền kiểm soát chất lượng.

| # | Bước                      | AI dùng để làm gì                                                                                                        | Bạn kiểm chứng kết quả thế nào                                                          |
| - | --------------------------- | ----------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| 1 | Phase 1                     | Brain storm ra các dimension gợi ý, Dùng để tạo ra các câu input test cho các combinations đã tạo ra | Đọc lại các câu hỏi có thực sự đại diện cho các conbinations không. |
| 2 | Phase 3 — Rubric & routing | Soạn nháp tiêu chí và routing map                                                                                        | Giữ code cho schema/citation/quote; giữ human review cho scope/high-risk                     |
| 3 | Phase 4                     | Soạn judge prompt, chạy hai vòng và phân tích confusion matrix                                                          | Lưu prompt/verdict từng vòng; chuyển judge sang LLM assist vì fail recall thấp           |
| 4 | Phase 5 - 6                 | Tổng hợp scorecard, threshold và report                                                                                    | Khóa threshold trước final gate và quyết định HOLD dựa trên slice breakdown           |

- Phần nào AI gợi ý mà bạn **bác bỏ**? Vì sao?

  - Loại bỏ các câu paraphase trùng.
  - Không dùng judge chưa calibrate làm nhãn vàng.
  - Không dùng các nhãn gán do AI tạo làm nhãn thật.
- Phần nào bạn **hoàn toàn tự làm**?

  - Gán nhãn thủ công, tranh luận với teammate để đưa ra được nhãn vàng.
