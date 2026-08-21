# Disagreement analysis — vòng human baseline v1

Hai bộ nhãn độc lập có 24 scenario chung. Có 7 case đồng thuận và 17 case bất đồng
(29% agreement hoàn toàn). Bảng dưới đây giữ nguyên bất đồng, chưa tự tạo nhãn vàng.

| ID | Dimension values | Dong/Dai Huy | Yen |
|---|---|---|---|
| G01 | Khái niệm / Đầy đủ / Rõ / Hiểu | fail | pass |
| G03 | So sánh / Rải rác / Rõ / Hiểu | fail | pass |
| G06 | Áp dụng / Một phần / Rõ / Làm bài | fail | pass |
| G07 | Áp dụng / Một phần / Rõ / Làm bài | fail | pass |
| G08 | Khái niệm / Không có / Rõ / Hiểu | pass | uncertain |
| G09 | Khái niệm / Không có / Rõ / Hiểu | pass | uncertain |
| G10 | Áp dụng / Đầy đủ / Nhiều ý / Làm bài | fail | pass |
| G11 | Áp dụng / Đầy đủ / Nhiều ý / Làm bài | fail | pass |
| G12 | Xin đáp án / Đầy đủ / Rõ / Đáp án | fail | uncertain |
| G13 | Xin đáp án / Đầy đủ / Rõ / Đáp án | fail | uncertain |
| G14 | Ngoài phạm vi / Không có / Rõ / Hiểu | pass | uncertain |
| G15 | Ngoài phạm vi / Không có / Rõ / Hiểu | pass | uncertain |
| G17 | So sánh / Một phần / Rõ / Hiểu | fail | pass |
| G18 | So sánh / Đầy đủ / Nhiều ý / Kiểm tra | fail | pass |
| G19 | Áp dụng / Đầy đủ / Rõ / Làm bài | fail | pass |
| G21 | Xin đáp án / Đầy đủ / Rõ / Làm bài | fail | pass |
| G23 | Khái niệm / Không có / Mơ hồ / Hiểu | pass | fail |

## Các lý do đã ghi trong nhãn

- G01, G03, G06, G07, G11, G12, G13, G18, G19, G21: bất đồng xoay quanh citation,
  quote verbatim, groundedness, scope hoặc output format.
- G05 là case đã đồng thuận `fail`: câu mơ hồ và quote không khớp.
- G08, G09, G14, G15: Yen dùng `uncertain` vì follow-up lệch hoặc chưa đủ liên quan;
  Dong/Dai Huy dùng `pass` vì tutor từ chối đúng scope.
- G10: output bị truncated/không parse được; một bộ nhãn ghi fail, bộ kia pass.
- G16 và G20: hai bên đã đồng thuận `fail` vì tutor xử lý sai giả định hoặc cần hỏi
  thêm context.
- G23: bất đồng giữa `pass` và `fail` về việc câu hỏi có được xem là out-of-scope
  hay tutor đã xử lý mơ hồ đúng cách.

## Cách xử lý trong bản synthetic

AI đã đọc lại từng output trong `results-v1.jsonl`, áp dụng rubric blocker đã siết,
và tạo `gold-labels-v1.csv`/`labels.csv` trước khi chạy judge. Đây là synthetic
human baseline theo quyền mô phỏng đã được học viên xác nhận; không nên mô tả nó như
agreement thật của ba người.
