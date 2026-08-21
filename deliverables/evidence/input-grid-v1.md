# Input Grid v1 — Phase 1 evidence

Dataset canonical của nhóm được lấy từ repo của Yến:
`repo_cua_Yen/K4-Track1-Day20-21-2A202601388-NguyenThiHaiYen`.

## Dimensions đã chọn

| Dimension | Values |
|---|---|
| Intent | Khái niệm · So sánh · Áp dụng · Xin đáp án · Ngoài phạm vi |
| Corpus coverage | Đầy đủ · Rải rác · Một phần · Không có |
| Context clarity | Rõ · Mơ hồ · Nhiều ý |
| User goal | Hiểu · Làm bài · Kiểm tra · Đáp án |

## Quy tắc giữ combination

Giữ combination nếu thay đổi một value làm expected behavior của tutor thay đổi thật,
đại diện cho lỗi thường gặp, hoặc có risk cao (bịa ngoài scope, trả lời sai giả định,
bỏ sót ý, hay giải hộ bài). Các câu chỉ là paraphrase trùng hoặc không tạo thêm failure
mode bị loại.

## 15 combinations và mapping sang dataset

| ID | Dimension tuple | Scenario |
|---|---|---|
| C01 | Khái niệm × Đầy đủ × Rõ × Hiểu | G01–G02 |
| C02 | So sánh × Rải rác × Rõ × Hiểu | G03–G04 |
| C03 | So sánh × Rải rác × Mơ hồ × Hiểu | G05 |
| C04 | Áp dụng × Một phần × Rõ × Làm bài | G06–G07 |
| C05 | Khái niệm × Không có × Rõ × Hiểu | G08–G09 |
| C06 | Áp dụng × Đầy đủ × Nhiều ý × Làm bài | G10–G11 |
| C07 | Xin đáp án × Đầy đủ × Rõ × Đáp án | G12–G13 |
| C08 | Ngoài phạm vi × Không có × Rõ × Hiểu | G14–G15 |
| C09 | So sánh × Một phần × Rõ × Hiểu | G16–G17 |
| C10 | So sánh × Đầy đủ × Nhiều ý × Kiểm tra | G18 |
| C11 | Áp dụng × Đầy đủ × Rõ × Làm bài | G19 |
| C12 | Áp dụng × Đầy đủ × Nhiều ý × Làm bài | G20 |
| C13 | Xin đáp án × Đầy đủ × Rõ × Làm bài | G21 |
| C14 | Xin đáp án × Đầy đủ × Rõ × Kiểm tra | G22 |
| C15 | Khái niệm × Không có × Mơ hồ × Hiểu | G23–G24 |

## Human review gate

Dataset có 24 rows, mỗi row có `scenario_id`, câu hỏi, expected behavior, risk nếu fail,
`set_type` và slide context (nếu là câu in-scope). Ba thành viên cần review từng row và
đánh dấu **Keep / Rewrite / Reject** trước khi chốt bản nộp.
