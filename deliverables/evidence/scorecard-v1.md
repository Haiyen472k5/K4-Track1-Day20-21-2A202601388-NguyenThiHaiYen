# Scorecard v1 — Phân tích chi tiết theo lát cắt (Slice Breakdown)

Synthetic gold: 9 pass / 15 fail tổng thể (tỉ lệ pass 37.5%). Kết quả kiểm tra bằng code (code checks) dựa trên `results-v1.jsonl`; kiểm tra trích dẫn nguyên văn (quote pass) loại trừ G10 do JSON bị lỗi không parse được.

## Phân theo nhóm độ khó (Set Type)

| Lát cắt (Slice) | Số câu (Rows) | Gold pass | Gold fail | Quote pass | Schema pass |
|---|---:|---:|---:|---:|---:|
| Đại diện (Representative) | 5 | 2 | 3 | 2 | 5 |
| Thách thức (Challenge) | 10 | 1 | 9 | 5 | 9 |
| Rủi ro cao (High-risk) | 9 | 6 | 3 | 6 | 9 |

## Phân theo ý định hỏi (Intent)

| Lát cắt (Slice) | Số câu (Rows) | Gold pass | Gold fail | Quote pass |
|---|---:|---:|---:|---:|
| Áp dụng | 6 | 0 | 6 | 2 |
| Khái niệm | 6 | 5 | 1 | 5 |
| Ngoài phạm vi | 2 | 2 | 0 | 2 |
| So sánh | 6 | 1 | 5 | 3 |
| Xin đáp án | 4 | 1 | 3 | 1 |

## Phân theo độ rõ ràng của ngữ cảnh (Context Clarity)

| Lát cắt (Slice) | Số câu (Rows) | Gold pass | Gold fail | Quote pass |
|---|---:|---:|---:|---:|
| Mơ hồ | 3 | 2 | 1 | 2 |
| Nhiều ý | 4 | 0 | 4 | 2 |
| Rõ | 17 | 7 | 10 | 9 |

## Đánh giá và Diễn giải điều kiện Release Gate

Lát cắt rủi ro cao (high-risk) đạt 6/9 gold pass, nhưng cổng chất lượng tổng thể (overall quality gate) bị đánh trượt (FAIL) do tỉ lệ trích dẫn nguyên văn (quote verbatim) chỉ đạt 52.2% và schema có 1 lỗi nghiêm trọng thuộc nhóm blocker. Các cụm hành vi yếu nhất của model hiện tại là: câu hỏi áp dụng, câu hỏi chứa nhiều ý/mục tiêu, và độ trung thực của trích dẫn (citation fidelity).
