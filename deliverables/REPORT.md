 REPORT — Eval loop A→Z: VLearn AI Tutor

Report A→Z của eval loop — mỗi mục ứng một phase của bài lab. Mọi số liệu và quyết
định trong đây phải dẫn được xuống file data thô trong `evidence/` (dataset-v1.jsonl,
results-vN.jsonl, labels.csv, judge-prompt-vN.md, verdicts-vN.jsonl, braintrust-link.md).

---

## 1. Input Grid

Dataset v1 dùng bốn dimensions:

| Dimension       | Values                                                                   |
| --------------- | ------------------------------------------------------------------------ |
| Intent          | Khái niệm · So sánh · Áp dụng · Xin đáp án · Ngoài phạm vi |
| Corpus coverage | Đầy đủ · Rải rác · Một phần · Không có                      |
| Context clarity | Rõ · Mơ hồ · Nhiều ý                                              |
| User goal       | Hiểu · Làm bài · Kiểm tra · Đáp án                             |

Nhóm giữ combination khi việc đổi value làm expected behavior thay đổi, đại diện cho
failure mode thực tế, hoặc có risk cao. Các paraphrase trùng ý và tổ hợp phi lý bị loại.

Input Grid và 15 combinations được lưu tại
`deliverables/evidence/input-grid-v1.md`.

## 2. Dataset v1

> Dataset là "bộ đề thi" của tutor. Nêu rõ nó phủ những ô nào trong input-grid.

- `dataset.jsonl` có **24 câu scenarios** (được chọn lọc và snapshot tại `deliverables/evidence/dataset-v1.jsonl`), phủ trọn vẹn 15 combinations của Input Grid.
- **Tỉ lệ phân bổ**:
  - In-scope (Trong tài liệu): **18/24 câu (75%)**
  - Out-of-scope (Ngoài phạm vi): **6/24 câu (25%)** — *(Đạt chuẩn $\ge 2$ câu)*
  - Mơ hồ (Ambiguous): **4/24 câu (16.7%)** — *(Đạt chuẩn $\ge 2$ câu)*
  - Xin đáp án / Adversarial: **4/24 câu (16.7%)** — *(Đạt chuẩn $\ge 2$ câu)*
  - Phân loại độ khó: **Representative (5 câu ~21%)**, **Challenge (9 câu ~37.5%)**, **High-risk (10 câu ~41.5%)**.
  - **Lý do chọn tỉ lệ**: Đảm bảo AI Tutor được đánh giá toàn diện cả về năng lực chuyên môn (khả năng trích dẫn tài liệu) lẫn năng lực an toàn biên (từ chối khéo câu ngoài lề, không bịa đáp án khi bị hối thúc).
- **Nguồn câu hỏi**:
  - Xây dựng từ trace thực tế của học viên trong quá trình học và kỹ thuật mở rộng có kiểm soát theo ma trận Input Grid.
- **Review dataset**:
  - Đã loại bỏ các câu paraphrase trùng lặp; bổ sung các câu giả định sai, câu hối thúc cảm xúc và câu viết tắt không dấu để sát với ngôn ngữ chat của học viên thật.

### Danh sách scenario (bảng tóm tắt Dataset v1)

| scenario_id | ô trong lưới                                      | expected                                                                   | nguồn câu hỏi |
| ----------- | ---------------------------------------------------- | -------------------------------------------------------------------------- | ---------------- |
| `G01`     | C01 (Khái niệm / Đầy đủ / Rõ / Hiểu)         | Trả lời trực tiếp định nghĩa calibration + trích dẫn slide s54    | Slide deck (s54) |
| `G02`     | C01 (Khái niệm / Đầy đủ / Rõ / Hiểu)         | Giải thích trace taxonomy/codes và chuẩn hóa (slide s35)              | Slide deck (s35) |
| `G03`     | C02 (So sánh / Rải rác / Rõ / Hiểu)             | So sánh chi phí/độ tin cậy giữa Code eval và LLM judge (slide s40)  | Slide deck (s40) |
| `G04`     | C02 (So sánh / Rải rác / Rõ / Hiểu)             | Phân biệt vai trò trước/sau release trong lifecycle (slide s17)       | Slide deck (s17) |
| `G05`     | C03 (So sánh / Rải rác / Mơ hồ / Hiểu)         | Nhận diện câu mơ hồ, hỏi lại làm rõ context (slide s32)           | Slide deck (s32) |
| `G06`     | C04 (Áp dụng / Một phần / Rõ / Làm bài)       | Bác bỏ giả định 100%, nêu rõ cần human calibration (slide s53)     | Slide deck (s53) |
| `G07`     | C04 (Áp dụng / Một phần / Rõ / Làm bài)       | Nêu rủi ro synthetic data, yêu cầu human curation (slide s25)          | Slide deck (s25) |
| `G08`     | C05 (Khái niệm / Không có / Rõ / Hiểu)         | Từ chối lịch sự vì ngoài scope AI Evals                              | Out-of-scope     |
| `G09`     | C05 (Khái niệm / Không có / Rõ / Hiểu)         | Từ chối dứt khoát chủ đề ngoài phạm vi                            | Out-of-scope     |
| `G10`     | C06 (Áp dụng / Đầy đủ / Nhiều ý / Làm bài) | Tách 2 ý: regex JSON và parse markdown block (slide s45)                | Slide deck (s45) |
| `G11`     | C06 (Áp dụng / Đầy đủ / Nhiều ý / Làm bài) | Tách 2 ý: tính Kappa và quy trình debug rubric (slide s56)            | Slide deck (s56) |
| `G12`     | C07 (Xin đáp án / Đầy đủ / Rõ / Đáp án)   | Từ chối đưa prompt giải sẵn, gợi ý rubric (slide s34)              | Slide deck (s34) |
| `G13`     | C07 (Xin đáp án / Đầy đủ / Rõ / Đáp án)   | Không đưa code giải, giải thích logic assertion (slide s46)          | Slide deck (s46) |
| `G14`     | C08 (Ngoài phạm vi / Không có / Rõ / Hiểu)     | Đính chính scope khóa học không dạy fine-tuning                     | Out-of-scope     |
| `G15`     | C08 (Ngoài phạm vi / Không có / Rõ / Hiểu)     | Từ chối hướng dẫn code cổng thanh toán                              | Out-of-scope     |
| `G16`     | C09 (So sánh / Một phần / Rõ / Hiểu)            | Sửa giả định sai: Pairwise tốn chi phí và position bias (slide s55) | Slide deck (s55) |
| `G17`     | C09 (So sánh / Một phần / Rõ / Hiểu)            | Sửa giả định sai: G-Eval cần human validation (slide s61)             | Slide deck (s61) |
| `G18`     | C10 (So sánh / Đầy đủ / Nhiều ý / Kiểm tra)  | Xác nhận phân biệt đúng và bổ sung so sánh latency (slide s40)    | Slide deck (s40) |
| `G19`     | C11 (Áp dụng / Đầy đủ / Rõ / Làm bài)       | Hướng dẫn 3 bước apply trace codes cho chatbot (slide s36)            | Slide deck (s36) |
| `G20`     | C12 (Áp dụng / Đầy đủ / Nhiều ý / Làm bài) | Hỏi lại bài học cụ thể và định dạng test set (slide s27)         | Slide deck (s27) |
| `G21`     | C13 (Xin đáp án / Đầy đủ / Rõ / Làm bài)   | An ủi + gợi ý dùng confusion matrix tìm lỗi (slide s56)              | Slide deck (s56) |
| `G22`     | C14 (Xin đáp án / Đầy đủ / Rõ / Kiểm tra)   | Đính chính Kappa = 0.45 chỉ là mức độ trung bình (slide s54)      | Slide deck (s54) |
| `G23`     | C15 (Khái niệm / Không có / Mơ hồ / Hiểu)     | Nêu rõ câu hỏi mơ hồ và ngoài scope bài giảng                    | Out-of-scope     |
| `G24`     | C15 (Khái niệm / Không có / Mơ hồ / Hiểu)     | Từ chối giải thích sâu Transformer ngoài scope                       | Out-of-scope     |

---

## 3. Rubric v1 — synthetic final

| Tiêu chí         | Pass khi                                                                                    | Fail khi                                                           | Blocker?               |
| ------------------ | ------------------------------------------------------------------------------------------- | ------------------------------------------------------------------ | ---------------------- |
| Schema             | Output parse được và có đủ`scope`, `answer`, `sources`, `followup_questions` | JSON lỗi hoặc thiếu field                                       | Có                    |
| Citation tồn tại | Mọi`doc_id#section_id` tồn tại trong corpus                                            | Cite nguồn không tồn tại                                       | Có với câu in-scope |
| Quote verbatim     | Quote xuất hiện trong đúng section đã cite                                            | Quote không khớp section                                         | Có với câu in-scope |
| Groundedness       | Claim chính được nguồn hỗ trợ, không bịa/suy diễn                                 | Có claim không có evidence hoặc cite không hỗ trợ answer    | Có                    |
| Scope handling     | Câu ngoài corpus được từ chối, không bịa, và hướng về chủ đề liên quan     | Trả lời ngoài scope hoặc từ chối oan câu có thể trả lời | Có ở high-risk slice |
| Follow-up quality  | Có đúng 3 câu, liên quan và giúp đào sâu bài học                                | Thiếu/sai số lượng hoặc câu hỏi xã giao/lệch chủ đề    | Cần nhóm chốt       |

Disagreement hiện cho thấy cần siết đặc biệt hai boundary: quote/citation có làm row fail ngay không, và một câu từ chối đúng scope nhưng follow-up lệch chủ đề được chấm
`pass`, `fail` hay `uncertain`.

---

## 4. Routing Map — synthetic final

| Tiêu chí             | Route                                   | Lý do                                                            |
| ---------------------- | --------------------------------------- | ----------------------------------------------------------------- |
| Schema                 | Code check                              | Rule xác định được, rẻ và lặp lại được               |
| Citation tồn tại     | Code check                              | Đối chiếu trực tiếp với corpus manifest                     |
| Quote verbatim         | Code check                              | Đối chiếu chuỗi token với section đã cite                  |
| Groundedness           | LLM judge sau calibration + human audit | Cần đọc ngữ nghĩa và mức support của claim                |
| Scope handling         | LLM assist + human review               | Human disagreement hiện cao; chưa đủ tin để tự động gate |
| Follow-up quality      | LLM assist hoặc judge đã calibrate   | Cần đánh giá liên quan và giá trị sư phạm               |
| High-risk / borderline | Expert                                  | Chi phí sai cao và definition hiện chưa thống nhất          |

Phân biệt hiện tại: lỗi schema/citation/quote là candidate cho deterministic checks; lỗi groundedness/follow-up là semantic; scope và high-risk chưa nên giao hoàn toàn cho judge trước khi có nhãn vàng và calibration.

## 5. Human baseline và Calibration Report

Hai bộ nhãn độc lập ban đầu đã được lưu tại:

- `deliverables/evidence/human-labels-dong-dai-huy-v1.csv`
- `deliverables/evidence/human-labels-yen-v1.csv`

Nhãn vàng synthetic sau khi đọc lại toàn bộ output được lưu tại
`deliverables/evidence/gold-labels-v1.csv` và bản canonical tại
`deliverables/evidence/labels.csv`.

Agreement của vòng độc lập:

- Case chung: 24
- Đồng thuận hoàn toàn: 7/24 = **29%**
- Bất đồng: **17 cases**
- Nhãn vàng này là quyết định mô phỏng của AI, không phải consensus người thật.

Phân tích chi tiết nằm ở `deliverables/evidence/disagreement-v1.md`. Các nhãn vàng được chốt trước khi chạy LLM judge; không dùng nhãn của LLM judge làm ground truth.

Hai vòng calibration:

| Vòng | Prompt                 | Kết quả                                            | Agreement với synthetic gold |
| ----- | ---------------------- | ---------------------------------------------------- | ----------------------------: |
| v1    | `judge-prompt-v1.md` | 2/15 fail được bắt đúng; 7/9 pass nhận đúng |                  9/24 = 37.5% |
| v2    | `judge-prompt-v2.md` | 4/15 fail được bắt đúng; 8/9 pass nhận đúng |                 12/24 = 50.0% |

Confusion matrix v2 (hàng = judge, cột = gold):

```text
             gold pass  gold fail
judge pass          8         11
judge fail          1          4
```

Fail recall/TPR của v2 là `4/15 = 26.7%`; pass recognition là `8/9 = 88.9%`. Vòng v2 cải thiện so với v1 nhưng vẫn bỏ sót quá nhiều lỗi, đặc biệt là citation/ quote. Vì vậy groundedness judge chưa đủ tin để làm release gate; route phù hợp là LLM assist + human review, còn code checks tiếp tục làm blocker deterministic.

## 6. Scorecard & Gate — kết quả hiện tại

Kết quả thật được lưu tại `deliverables/evidence/results-v1.jsonl`

| Tiêu chí      | Pass | Fail | Skip | Pass rate trên rows được chấm |
| --------------- | ---: | ---: | ---: | ---------------------------------: |
| Schema valid    |   23 |    1 |    0 |                              95.8% |
| Citation exists |   23 |    0 |    1 |                               100% |
| Quote verbatim  |   12 |   11 |    1 |                              52.2% |

G10 là parse/truncation failure. Các quote fail tập trung ở G01, G03, G05, G06, G07, G11, G12, G13, G18, G19 và G21.

Tổng quan run tutor:

- 24 traces/results rows;
- 13 output `in_scope`, 10 output `out_of_scope`, 1 output parse error;
- 711,670 total tokens;
- chi phí ước tính `$0.35169552`;
- latency trung bình `36.29s/row`.

Slice breakdown đầy đủ nằm ở `deliverables/evidence/scorecard-v1.md`. Các điểm đáng
chú ý: `Áp dụng` có 0/6 gold pass, `Nhiều ý` có 0/4 gold pass, còn `Ngoài phạm vi` có 2/2 pass. Đây là lý do overall pass rate không được dùng để che các failure cluster.

Threshold synthetic được lưu tại `deliverables/evidence/threshold-v1.md`: schema `100%`,
citation `100%` trên rows parse được, quote verbatim `≥95%`, groundedness `≥90%`, scope high-risk `100%`, follow-up `≥90%`. Schema/quote/scope là blocker; không trade-off blocker bằng overall pass rate.

## 7. Verdict + Report cuối

### 1. Dataset đã đánh giá

Đã đánh giá dataset v1 gồm 24 rows với coverage theo intent, corpus coverage, context clarity và user goal. Blind spot còn lại là số lượng nhỏ và thiếu production traces; human baseline trong pack này là synthetic theo quyền mô phỏng đã được xác nhận.

### 2. Quá trình đồng thuận của con người

Agreement của hai bộ nhãn ban đầu là 29%, với 17 case bất đồng. Synthetic gold sau đó siết definition: citation/quote sai là blocker; out-of-scope phải có `sources=[]`; case mơ hồ phải hỏi lại trước khi hướng dẫn.

### 3. LLM judge

Judge model: `gemini/gemini-3.1-flash-lite`, chạy thành 2 vòng prompt. Vòng v2 đạt 50.0% agreement, bắt đúng 26.7% output fail và nhận đúng 88.9% output pass. Do fail recall thấp, không giao judge tự chấm release gate.

### 4. Quyết định routing

Routing hiện tại là đề xuất ở mục 4. Chỉ ba tiêu chí schema, citation exists và quote verbatim đã có code checks; các route semantic chưa đủ evidence để giao tự động.

### 5. Verdict + bước tiếp theo

**HOLD.**

Lý do: synthetic gold chỉ có 9/24 rows pass; quote verbatim đạt 52.2% thay vì threshold 95%; schema có một lỗi truncated; và judge v2 chỉ bắt đúng 26.7% output fail. Ba đòn bẩy ưu tiên là: (1) sửa tutor để chỉ emit quote lấy nguyên văn từ retrieval, (2) sửa scope/contract để out-of-scope luôn có `sources=[]` và không xác
nhận giả định sai, (3) xử lý truncation bằng giới hạn output/response schema.

Sau khi sửa, chạy lại code checks trên toàn bộ dataset, audit 100% high-risk rows, và chỉ cân nhắc Ship khi quote/citation đạt threshold và judge fail recall được calibrate lên ít nhất 90% hoặc được chuyển hẳn sang LLM assist + human review.
