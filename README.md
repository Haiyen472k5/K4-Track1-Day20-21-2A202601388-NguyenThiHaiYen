# Track 1 Day 21 — AI Evaluation

## Thông tin cá nhân và nhóm

- **Mã học viên:** `2A202601388`
- **Họ và tên:** Nguyễn Thị Hải Yến
- **Thành viên nhóm:** Đồng Đại Huy, Nguyễn Thị Hải Yến
- **Case:** VLearn AI Tutor — đánh giá chất lượng AI Tutor tiếng Việt
- **Eval Pack:** dataset canonical 24 rows của nhóm.

## Sơ đồ sáu phase và artifact

| Phase                    | Artifact trong repo                                              |
| ------------------------ | ---------------------------------------------------------------- |
| 1. Thiết kế coverage   | `deliverables/evidence/input-grid-v1.md`, `dataset-v1.jsonl` |
| 2. Human baseline        | `labels.csv`, `disagreement-v1.md`, `results-v1.jsonl`     |
| 3. Rubric & routing      | Mục 3–4 trong`deliverables/REPORT.md`                        |
| 4. Scale & calibrate     | `judge-prompt-v1/v2.md`, `verdicts-v1/v2.jsonl`              |
| 5. Scorecard & threshold | `scorecard-v1.md`, `threshold-v1.md`                         |
| 6. Verdict               | Mục 7 trong`deliverables/REPORT.md`                           |

## Đóng góp cá nhân

1. Đồng bộ dataset 24 rows và Input Grid gồm 4 dimensions, 15 combinations.
2. Kiểm tra coverage, ambiguous/high-risk/out-of-scope slices và tính nhất quán giữa dataset root và evidence.
3. Đọc lại các trace bất đồng, xây synthetic baseline theo rubric blocker do giáo viên cho phép AI mô phỏng evaluator.
4. Thực hiện code checks, viết và calibrate judge prompt qua hai vòng, phân tích confusion matrix.

## Verdict của nhóm

**HOLD.**

Synthetic gold có 9/24 rows pass. Code checks cho thấy schema đạt 23/24, citation
đạt 23/23 rows parseable, nhưng quote verbatim chỉ đạt 12/23. Judge v2 đạt 50%
agreement và chỉ bắt đúng 26.7% output fail. Vì vậy chưa đủ an toàn để ship.

Ưu tiên tiếp theo: sửa quote/citation lấy nguyên văn từ retrieval, sửa scope contract
cho câu out-of-scope, và xử lý output bị truncated.

## Bài học mang về dự án thật

- Thiết kế ma trận kiểm thử trước khi sinh test case; số lượng hàng không thay thế được độ phủ rủi ro.
- Tách bạch deterministic rules (schema, format, quote) xử lý bằng code trước khi gọi LLM judge ngữ nghĩa.
- Human baseline là mốc chuẩn; LLM judge chưa calibrate đối chiếu không được coi là ground truth.
- hông để điểm Pass Rate trung bình làm lu mờ lỗi tại các lát cắt nguy cấp
- Khóa chặt tiêu chí nghiệm thu và ngưỡng đạt trước khi chạy thử nghiệm để đảm bảo tính khách quan.

Xem báo cáo đầy đủ tại [`deliverables/REPORT.md`](deliverables/REPORT.md), raw evidence
tại [`deliverables/evidence/`](deliverables/evidence/) và lịch sử sử dụng AI tại
[`ai-support-log.md`](ai-support-log.md).
