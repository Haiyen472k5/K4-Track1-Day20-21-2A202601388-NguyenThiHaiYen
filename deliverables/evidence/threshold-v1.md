# Khóa ngưỡng đánh giá (Threshold Lock) — Cổng nghiệm thu Synthetic Final

Ngưỡng nghiệm thu được khóa cố định trước khi đọc kết quả hiệu chỉnh (calibration) v2 và trước khi ra quyết định gate cuối cùng. Lượt chạy `results-v1.jsonl` trước đó mang tính chất khám phá; mọi chỉ số được ghi nhận trung thực và giữ nguyên, tuyệt đối không điều chỉnh ngược ngưỡng để hợp thức hóa kết quả.

| Tiêu chí | Ngưỡng đạt (Threshold) | Loại cổng (Gate Type) |
|---|---:|---|
| Schema hợp lệ | 100% | Blocker |
| Trích dẫn (Citation) tồn tại | 100% các câu parse được | Blocker |
| Trích dẫn nguyên văn (Quote verbatim) | ≥95% | Blocker |
| Tính xác thực từ nguồn (Groundedness) | ≥90% | Blocker |
| Xử lý phạm vi ở lát cắt rủi ro cao (Scope handling) | 100% | Blocker |
| Chất lượng câu hỏi gợi mở (Follow-up quality) | ≥90% | Non-blocker (chỉ xét khi không có suy giảm ở lát cắt rủi ro cao) |

Không đánh đổi bất kỳ tiêu chí Blocker nào để làm đẹp tỉ lệ pass rate tổng thể. Chỉ cần một câu bị lỗi JSON, trích dẫn/quote không có cơ sở, hoặc xử lý sai phạm vi ở nhóm rủi ro cao là toàn hệ thống bị CHẶN (Không cho phép Ship).

Đây là quyết định thiết lập ngưỡng mô phỏng (synthetic threshold) do AI thực hiện dựa trên quy định cho phép mô phỏng của giáo viên hướng dẫn.
