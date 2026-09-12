# Phase 5 — Workflow + Problem Statement
**Nhóm 2 · Bài toán: AI có thật sự tìm đúng research gap?**

---

## 1. Workflow hiện tại (thủ công)

| # | Bước | Actor | Input | Output | Thời gian/Tần suất | Bàn giao (handoff) |
|---|------|-------|-------|--------|---------------------|----------------------|
| 1 | Xác định đề tài | Researcher | Mối quan tâm nghiên cứu | Từ khóa / phạm vi | 1–2h, 1 lần/đề tài | Không |
| 2 | Tìm kiếm tài liệu | Researcher | Từ khóa / phạm vi | Danh sách 50–200 paper | 5–10h | Không |
| 3 | Sàng lọc abstract | Researcher | Danh sách paper | Shortlist 20–50 paper | 8–15h | Không |
| 4 | **Đọc & note full-text** | Researcher | Shortlist | Ghi chú/annotation từng paper | **20–40h ⚠ Bottleneck chính** | Không |
| 5 | Tổng hợp phát hiện | Researcher | Ghi chú | Bảng synthesis (pattern/mâu thuẫn) | 5–10h | Không |
| 6 | Đề xuất gap ứng viên | Researcher | Bảng synthesis | Danh sách candidate gap | 3–5h | → chuyển cho Advisor |
| 7 | Duyệt gap | Advisor | Danh sách candidate gap | Hướng nghiên cứu được duyệt | Chờ phản hồi **1–2 tuần** | **Handoff**: Researcher → Advisor → Researcher |
| 8 | Viết problem statement | Researcher | Gap đã duyệt | Problem statement văn bản | 2–4h | Không |

**Tổng: 8 bước, 45–75h công việc chủ động (chưa tính thời gian chờ advisor), 100% thủ công.**

**Bottleneck chính:** Bước 4 — đọc & note full-text — chiếm 20–40h, gần một nửa tổng thời gian, hoàn toàn thủ công, dễ bỏ sót paper quan trọng do giới hạn khả năng đọc của một người.

---

## 2. Workflow tương lai (có AI)

| # | Bước | Ai xử lý | Vai trò | Thời gian | Boundary / Ghi chú |
|---|------|----------|---------|-----------|----------------------|
| 1 | Xác định đề tài & câu hỏi | **Người** | Con người quyết định phạm vi | 1–2h | Ngoài vùng AI — con người luôn làm |
| 2 | Search + trích xuất + cluster gap | **AI / Workflow** | AI đề xuất, kèm nguồn trích dẫn | 2–3h tự động | AI chỉ đề xuất, không tự kết luận |
| 3 | Rule lọc từ khóa (tiền xử lý, trong bước 2) | **Rule** | Lọc thô câu chứa dấu hiệu gap (unknown, research gap, not fully understood…) | Vài giây/paper | Phụ trợ cho bước AI, không thay thế |
| 4 | Spot-check & xác thực gap (mẫu) | **Người** | Kiểm tra chất lượng output AI | 4–8h | **Boundary**: AI không được tự công bố gap khi chưa qua bước này |
| 5 | Duyệt gap (handoff) | **Người** (Advisor) | Quyết định cuối cùng | Chờ 1–2 tuần | Handoff Researcher → Advisor |
| 6 | Viết problem statement | **Người** + AI draft | AI hỗ trợ soạn, người biên tập & chịu trách nhiệm | 2–3h | Người luôn là người ký cuối |

**Boundary tổng quát:** AI/Rule chỉ được hoạt động trong "vùng đề xuất" (search → extract → cluster), luôn phải kèm nguồn trích dẫn để truy vết. Con người giữ toàn quyền xác thực (bước 4) và quyết định cuối (bước 5).

**Phương án quay về nếu AI sai:**
- Nếu spot-check phát hiện gap bị hallucinate, trích sai nguồn, hoặc cluster gán nhãn sai chủ đề → quay lại bước 2, chạy lại với query hẹp hơn cho riêng nhánh lỗi, hoặc chuyển sang tìm thủ công cho nhánh đó.
- Audit định kỳ: lấy mẫu ~10% output mỗi tuần, đối chiếu với search thủ công độc lập.
- Nếu tỷ lệ lỗi trên mẫu kiểm tra vượt ngưỡng đặt trước (ví dụ >20%) → tạm dừng pipeline tự động, rà lại prompt/nguồn dữ liệu trước khi chạy tiếp.

---

## 3. Bảng Before / After Impact

| Chỉ số | Before (thủ công) | After (có AI) |
|---|---|---|
| Số bước | 8 | 5–6 (tuỳ có tách Rule thành bước riêng) |
| Tổng thời gian | 45–75h (chưa tính chờ advisor) | 12–20h (ước tính, chưa tính chờ advisor) |
| Số bước thủ công | 8/8 (100%) | 3/6 (~50%) — vẫn giữ người ở bước xác định đề tài, spot-check, duyệt/viết PS |
| Bottleneck mới | — | Spot-check & xác thực gap (bước 4), ~4–8h — ít giờ hơn nhưng đòi hỏi kỹ năng đánh giá chất lượng AI thay vì chỉ đọc |
| Rủi ro mới | — | "False confidence" — gap AI đưa ra trông hợp lý, có trích dẫn, nhưng có thể generic/hallucinate; nguy cơ over-reliance khiến researcher mất khả năng tự đánh giá độc lập |

*Lưu ý: số giờ "after" là ước tính dựa trên tỷ lệ tiết kiệm 22,6–26,9% (nghiên cứu LEADS) đến 50–70% (một số công cụ thương mại) được báo cáo trong các nghiên cứu literature-review AI — cần đo thực tế trên case của nhóm để xác nhận, không nên coi là số cố định.*

---

## 4. Problem Statement v0

| Field | Nội dung |
|---|---|
| **Actor** | Nhà nghiên cứu (early-stage) đang làm literature review để xác định hướng nghiên cứu mới |
| **Workflow** | Hiện tại: 8 bước, 45–75h, 100% thủ công, bottleneck ở bước đọc full-text. Tương lai: AI agent tự động search + extract + cluster gap (giảm còn ~5–6 bước, 12–20h), nhưng thiếu bước kiểm chứng độ tin cậy của gap do AI đề xuất |
| **Bottleneck** | Các agent hiện có (SciSpace, GapFinder, AnswerThis, nghiên cứu BERTopic/JMIR) đều dừng ở việc *tạo ra* danh sách gap — chưa ai công bố benchmark định lượng đo % gap do AI đề xuất được chuyên gia độc lập xác nhận là "gap thật, đáng nghiên cứu" |
| **Impact** | Nếu không kiểm chứng, researcher có nguy cơ theo đuổi gap "trông mới nhưng không có giá trị thực khi triển khai" — đúng như hiện tượng ideation-execution gap đã quan sát được ở nghiên cứu so sánh ý tưởng AI vs con người — gây lãng phí hàng chục giờ nghiên cứu |
| **Success Metric** | **Hiện trạng**: 0/3 case đã khảo sát (SciSpace, GapFinder, nghiên cứu JMIR/BERTopic) công bố số liệu agreement-rate giữa gap do AI đề xuất và đánh giá của chuyên gia độc lập. **Mục tiêu**: đạt ≥70% gap do agent đề xuất được ≥2/3 chuyên gia độc lập đồng thuận là "gap thật, khả thi". **Cách đo**: thiết kế thí nghiệm blind review — panel chuyên gia chấm điểm song song gap do AI và do người đề xuất (giấu nguồn), tính agreement rate + so sánh điểm trước/sau khi thử triển khai |
| **Boundary** | Chỉ đánh giá gap ở cấp câu hỏi nghiên cứu cụ thể (không đánh giá gap chiến lược ngành); AI chỉ đề xuất & xếp hạng kèm nguồn trích dẫn, con người luôn là người quyết định cuối cùng, không tự động hoá bước duyệt |