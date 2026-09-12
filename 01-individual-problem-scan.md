| # | Subsidiary | Lens | Mô tả ngắn bài toán                                                                                                                                                                                                                                                                                                                                                  |
|---|------------|------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1 | **Giáo dục** | AI-upgrade | Giáo viên không có công cụ theo dõi điểm mạnh/yếu riêng của từng học sinh (đọc hiểu, nghe nói...) theo thời gian thực để giao bài tập cá nhân hóa, phải dạy đại trà, học sinh yếu bị bỏ lại, giáo viên quá tải vì lặp lại giải thích cùng dạng bài nhiều lần.                                                                                                        |
| 2 | **Nghiên cứu khoa học** | AI-upgrade | Researcher tốn nhiều thời gian đọc literature để tìm gap. Các agent hiện có (research-hub, gap-to-topic, AnswerThis...) chỉ dừng ở so sánh phương pháp, phát hiện dữ liệu tái sử dụng, đánh giá độ tin cậy tuyên bố khoa học — chưa ai kiểm chứng độ chính xác của việc AI "tự đề xuất gap" so với chuyên gia con người.                                             |
| 3 | **Truyền thông / Xã hội** | Pain từ người khác | Người dùng phổ thông khó tự kiểm chứng tin tức lan truyền nhanh trên mạng xã hội. Các hệ thống hiện tại (FactAgent, MAD-Sherlock, FactGuard...) chỉ tối ưu độ chính xác phân loại thật/giả — nghiên cứu CHI 2026 cho thấy báo cáo AI bị đánh giá kém hữu ích hơn báo cáo con người, tức độ chính xác cao không đồng nghĩa thay đổi được niềm tin/hành vi người dùng. |
| 4 | **Giáo dục** | Tốn thời gian | Người học khó tìm tài liệu học tập phù hợp vì tài liệu trên internet quá nhiều, phân mảnh, không có lộ trình chuẩn; mỗi nguồn/tài khoản chỉ đăng giới hạn số bài nên người học phải tự lắp ghép và sắp xếp thứ tự học từ nhiều nơi khác nhau.                                                                                                                        |
| 5 | **Giáo dục** | Tốn thời gian | Người học khó biết trước cuốn sách nào phù hợp trình độ/mục tiêu vì có quá nhiều đầu sách cùng chủ đề; mua thử nhiều cuốn tốn kém mà không chắc chắn hiệu quả, chỉ biết được sau khi đã đọc dở, nhiều tài liệu có kiến thức không chuẩn |                                                                                                                             |



# Problem Cards — Top 3 Bài Toán

---

## 1. Giáo dục — Lộ trình học tập cá nhân hóa

**Problem (1 câu):** Giáo viên không có công cụ theo dõi điểm mạnh/yếu riêng của từng học sinh theo thời gian thực để giao bài tập cá nhân hóa, dẫn đến dạy đại trà và quá tải khi phải giải thích lặp lại.

**Actor:** Giáo viên (người thiết lập, giám sát), Học sinh (người học)

**Bối cảnh:** Lớp học 30-40 học sinh, mỗi em có điểm mạnh/yếu khác nhau (đọc hiểu, nghe nói, tính toán...); giáo án chung cho cả lớp; đánh giá năng lực chủ yếu qua kiểm tra định kỳ theo học kỳ.

**Workflow hiện tại:**
1. Giáo viên soạn giáo án chung (30')
2. Giảng bài trên lớp (45')
3. Giao bài tập đại trà, không phân hóa (5')
4. Chấm bài, ghi nhận lỗi sai thủ công cho từng em (60')
5. Học sinh hỏi lại khi không hiểu → giáo viên giải thích lặp lại (30'/tuần)
6. Kiểm tra định kỳ mới phát hiện học sinh yếu (theo học kỳ, quá trễ)

**Bottleneck:** Bước 4 (chấm bài + ghi nhận lỗi thủ công) và bước 5 (giải thích lặp lại) — không scale theo số học sinh, và không có dữ liệu chẩn đoán liên tục.

**Impact:** Học sinh yếu bị bỏ lại phía sau; giáo viên quá tải; điểm trung bình lớp khó cải thiện.

**Success metric:** Tăng điểm TB học sinh 10%/học kỳ; giảm 50% thời gian giáo viên dành giải thích lại.

**Non-AI alternative:** Dạy phân hóa thủ công (chia nhóm theo trình độ) hoặc thuê trợ giảng — tốn nhân lực, khó nhân rộng, phụ thuộc ngân sách trường.

**AI hypothesis:** AI có thể chẩn đoán điểm yếu qua lịch sử làm bài, tự sinh bài tập cá nhân hóa bám giáo án, và trả lời dạng Socratic thay vì đưa đáp án — giảm tải chấm bài và giải thích lặp lại cho giáo viên.

**Quick gut:** **Agent** — cần theo dõi liên tục, chẩn đoán động, sinh nội dung theo từng học sinh, tương tác nhiều vòng.

### Workflow trước/sau

```
CURRENT STATE — ~135 phút/tuần (trên 1 lớp)

[Soạn giáo án chung: 30']
→ [Giảng bài: 45']
→ [Giao bài đại trà: 5']
→ [Chấm bài + ghi nhận lỗi: 60']       <-- bottleneck
→ [Giải thích lại khi HS hỏi: 30'/tuần] <-- bottleneck
→ [Kiểm tra định kỳ mới phát hiện HS yếu: theo học kỳ]

FUTURE STATE — ~50 phút/tuần

[GV upload giáo án: 5' — 1 lần]
→ [AI chẩn đoán năng lực từng HS: 2']
→ [AI sinh bài tập cá nhân hóa: 2']
→ [HS tự luyện + hỏi AI kiểu Socratic: tự động]
→ [AI tổng hợp báo cáo điểm yếu theo tuần: 1']
→ [GV xem dashboard, can thiệp đúng HS cần: 30']  <-- human boundary
→ [GV giải thích trực tiếp chỉ case khó: 10']

Fallback: AI giải thích sai / HS vẫn không hiểu → escalate cho GV.
```

---

## 2. Nghiên cứu khoa học — Đánh giá gap do AI đề xuất

**Problem (1 câu):** Researcher tốn nhiều thời gian đọc literature để tìm gap nghiên cứu, trong khi chưa có công cụ nào tự đề xuất gap được kiểm chứng độ tin cậy ngang chuyên gia con người.

**Actor:** Researcher/Nghiên cứu sinh, Reviewer/GVHD

**Bối cảnh:** Cần tìm đề tài mới trước khi bắt đầu luận văn/bài báo; số lượng bài báo mới xuất bản mỗi tuần trong lĩnh vực vượt khả năng đọc thủ công.

**Workflow hiện tại:**
1. Tìm từ khóa trên Google Scholar/arXiv (30')
2. Đọc abstract, lọc bài liên quan (60')
3. Đọc chi tiết các bài đã lọc (5-8 giờ)
4. Ghi chú, tổng hợp các hướng đã làm (60')
5. Brainstorm/thảo luận với GVHD để tìm gap (60')
6. Viết proposal gap (30')

**Bottleneck:** Bước 3 (đọc chi tiết) và bước 5 (brainstorm với GVHD) — chiếm phần lớn thời gian và phụ thuộc lịch của GVHD.

**Impact:** Trì hoãn tiến độ nghiên cứu vài tuần đến vài tháng; rủi ro chọn nhầm gap đã có người làm hoặc không khả thi.

**Success metric:** Tỷ lệ gap AI đề xuất được bài báo sau này thực sự lấp đạt 70-80% so với gap do reviewer con người đề xuất; giảm 50% thời gian literature review.

**Non-AI alternative:** Công cụ citation mapping thủ công (VOSviewer, Connected Papers) — vẫn cần người tự suy luận ra gap.

**AI hypothesis:** AI tổng hợp literature nhanh hơn, tự đề xuất gap kèm trích dẫn minh chứng và chấm điểm độ tin cậy, rút ngắn vòng lặp brainstorm với GVHD.

**Quick gut:** **Agent** — cần tra cứu đa nguồn, tổng hợp, suy luận nhiều bước, không phải rule cố định.

### Workflow trước/sau

```
CURRENT STATE — ~10-15 giờ/tuần

[Tìm từ khóa: 30']
→ [Lọc abstract: 60']
→ [Đọc chi tiết bài liên quan: 5-8h]      <-- bottleneck
→ [Ghi chú tổng hợp: 60']
→ [Brainstorm với GVHD: 60']              <-- bottleneck
→ [Viết proposal gap: 30']

FUTURE STATE — ~3-4 giờ/tuần

[Nhập từ khóa/lĩnh vực: 5']
→ [AI quét & tổng hợp literature: 15']
→ [AI đề xuất gap kèm nguồn + confidence score: 10']
→ [Researcher review, loại gap không phù hợp: 60']  <-- human boundary
→ [Thảo luận với GVHD chỉ về gap đã lọc: 30']
→ [Viết proposal: 30']

Fallback: Gap AI đề xuất không thuyết phục → researcher quay lại tự đọc literature như cũ.
```

---

## 3. Truyền thông/Xã hội — Kiểm chứng tin lan truyền nhanh

**Problem (1 câu):** Người dùng phổ thông khó tự kiểm chứng tin tức lan truyền nhanh trên mạng xã hội trước khi chia sẻ tiếp.

**Actor:** Người dùng phổ thông, Nền tảng mạng xã hội/báo chí (bên tích hợp)

**Bối cảnh:** Tin giả lan truyền nhanh hơn tốc độ xác minh của con người; người dùng thiếu kỹ năng/thời gian tự tra nguồn.

**Workflow hiện tại:**
1. Tin xuất hiện trên MXH (0')
2. Người dùng lan truyền/chia sẻ ngay nếu thấy hợp lý (<1')
3. Một số ít tự tra cứu thêm nếu nghi ngờ (5-10')
4. Hỏi bạn bè/group để xác nhận (10-30')
5. Chờ báo chí chính thống xác minh (vài giờ đến vài ngày)

**Bottleneck:** Bước 2 (chia sẻ ngay, xảy ra trước khi kiểm chứng) và bước 5 (xác minh chính thống quá chậm so với tốc độ lan truyền).

**Impact:** Tin giả lan rộng trước khi được xác minh; ảnh hưởng nhận thức cộng đồng, đặc biệt rủi ro cao trong bầu cử, y tế, khủng hoảng.

**Success metric:** Tăng 30% tỷ lệ người dùng đổi hành vi (ngừng chia sẻ/tự kiểm tra thêm) sau cảnh báo; điểm "hữu ích" đạt ≥80% so với báo cáo con người.

**Non-AI alternative:** Fact-checker con người (Reuters Fact Check, AFP...) — chính xác cao nhưng chậm, không scale theo tốc độ lan truyền.

**AI hypothesis:** AI phát hiện tin lan truyền bất thường, tổng hợp bằng chứng đa nguồn nhanh, trình bày dễ hiểu để thực sự thay đổi hành vi người dùng — không chỉ gắn nhãn đúng/sai.

**Quick gut:** **Agent** — cần retrieval đa nguồn + suy luận + trình bày thuyết phục, nhiều bước phối hợp.

### Workflow trước/sau

```
CURRENT STATE — vài giờ đến vài ngày

[Tin xuất hiện trên MXH: 0']
→ [Người dùng chia sẻ ngay: <1']            <-- bottleneck (trước khi kiểm chứng)
→ [Một số ít tự tra cứu: 5-10']
→ [Hỏi bạn bè/group: 10-30']
→ [Chờ báo chí chính thống xác minh: vài giờ-vài ngày] <-- bottleneck
→ [Tin đính chính xuất hiện nhưng ít người thấy lại]

FUTURE STATE — vài phút

[Hệ thống phát hiện tin lan truyền bất thường: tự động]
→ [AI thu thập bằng chứng đa nguồn: 1-2']
→ [AI trình bày mức độ tin cậy + nguồn dễ hiểu: 1']
→ [Cảnh báo hiển thị ngay dưới bài đăng: tức thời]
→ [Người dùng tự quyết định đọc thêm/dừng chia sẻ: 1-2']  <-- human boundary
→ [Định kỳ đối chiếu với fact-checker con người để hiệu chỉnh: batch]

Fallback: AI không chắc chắn (confidence thấp) → chuyển hàng chờ cho fact-checker con người, không gắn nhãn vội.
```