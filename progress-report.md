# progress-report.md — Báo cáo tiến độ Sprint 1

**Iteration trên Project:** `Sprint 1`
**Khoảng thời gian giả lập:** 02/11/2026 – 08/11/2026 (1 tuần, 5 ngày làm việc)
**Nguồn số liệu:** [GitHub Project #2](https://github.com/users/oNguyenVanManh/projects/2) — trường `Status`, `SWP`, `Giờ ước lượng`, `Sprint`

> Đây là sprint **giả lập**. Trạng thái issue được cập nhật như sau một sprint chạy thật để
> minh hoạ cách báo cáo, không phải tiến độ của một đội đang làm việc.

---

## 1. Phạm vi Sprint 1

Sprint 1 chỉ lấy các hạng mục **pha Requirement**, đúng bằng sức chứa một tuần của đội khởi động
(2 BrSE, 1 PM, 1 BE, 1 Design — chưa có FE, Native, QA, Infra vào việc).

| Issue | Vai trò | SWP | Giờ |
|---|---|--:|--:|
| [#318](https://github.com/oNguyenVanManh/product-a-backlog/issues/318) [PRJ-01·BrSE 1/2] Phân tích yêu cầu chi tiết | BrSE | 6 | 24 |
| [#319](https://github.com/oNguyenVanManh/product-a-backlog/issues/319) [PRJ-01·BrSE 2/2] Phân tích yêu cầu chi tiết | BrSE | 6 | 24 |
| [#320](https://github.com/oNguyenVanManh/product-a-backlog/issues/320) [PRJ-01·BE] Ma trận truy vết | BE | 3 | 12 |
| [#321](https://github.com/oNguyenVanManh/product-a-backlog/issues/321) [PRJ-02·BrSE 1/2] Luồng nghiệp vụ TO-BE | BrSE | 5 | 20 |
| [#323](https://github.com/oNguyenVanManh/product-a-backlog/issues/323) [PRJ-02·Design] Luồng nghiệp vụ TO-BE | Design | 3 | 12 |
| [#324](https://github.com/oNguyenVanManh/product-a-backlog/issues/324) [PRJ-03·PM] Chốt 20 tiền đề | PM | 3 | 12 |
| [#325](https://github.com/oNguyenVanManh/product-a-backlog/issues/325) [PRJ-03·BrSE] Nhật ký làm rõ yêu cầu | BrSE | 3 | 12 |
| **Tổng cam kết** | | **29** | **116** |

Sức chứa BrSE tuần này là 2 người × 40 h = 80 h, và Sprint 1 giao đúng 80 h cho BrSE — không có đệm.
Đó là một quyết định cố ý để thấy chuyện gì xảy ra khi tuần đầu gặp phụ thuộc bên ngoài.

**Hai issue quản trị tháng 1 ([#452] PM, [#462] BrSE) cố tình KHÔNG xếp vào Sprint 1.** Chúng là việc
trải theo lịch cả tháng (112 h và 80 h), nhét vào một iteration 1 tuần sẽ làm burndown sai hẳn. Chúng
được theo dõi riêng ngoài sprint — cùng lý do với quy tắc B ở [`estimate.md`](./estimate.md).

---

## 2. Trạng thái cuối sprint

| Trạng thái | Số issue | Tổng SWP | Ghi chú |
|---|--:|--:|---|
| Done | 4 | 15 | #318, #320, #324, #325 — đạt định nghĩa xong |
| In Review | 1 | 6 | #319 viết xong, chờ khách xác nhận |
| In Progress | 1 | 5 | #321 mới bắt đầu ngày thứ 4 |
| Blocked | 1 | 3 | #323 bị chặn, xem mục 4 |
| **Tổng** | **7** | **29** | hoàn thành **15/29 = 51,7 %** |

---

## 3. Burndown

<img src="./assets/burndown-sprint-1.svg" alt="Burndown Sprint 1" width="640">

| Mốc | Kế hoạch (SWP còn lại) | Thực tế | Lệch | Việc đóng trong ngày |
|---|--:|--:|--:|---|
| Bắt đầu | 29,0 | 29 | 0 | — |
| Hết T2 | 23,2 | 29 | +5,8 | chưa đóng gì — ngày họp khởi động |
| Hết T3 | 17,4 | 26 | +8,6 | #324 chốt 20 tiền đề (3) |
| Hết T4 | 11,6 | 23 | +11,4 | #325 nhật ký làm rõ (3) |
| Hết T5 | 5,8 | 20 | +14,2 | #320 ma trận truy vết (3) |
| Hết T6 | 0,0 | 14 | +14,0 | #318 phân tích yêu cầu 1/2 (6) |

**Thực tế lệch kế hoạch ở đâu:** đường thực tế nằm ngang suốt ngày đầu và chỉ bắt đầu đi xuống từ
ngày thứ ba. Nguyên nhân không phải đội làm chậm, mà là **cách chia việc**: 4 trong 7 issue có kích
thước 5–6 SWP, tức gần trọn 3 ngày công, nên không có gì đóng được trong hai ngày đầu. Đường kế hoạch
tuyến tính giả định việc đóng rải đều — giả định đó sai với backlog có issue cỡ 6 SWP trong sprint 1 tuần.

**Rút ra cho Sprint 2:** cap 3 MD/issue vẫn hợp lý cho cả backlog, nhưng với sprint 1 tuần thì issue
cỡ 5–6 SWP nên tách đôi để burndown có tín hiệu sớm. Đây là **chỗ hở của chính nguyên tắc chia task**,
ghi lại ở [`task-breakdown.md`](./task-breakdown.md) mục 1.

---

> **Ghi chú đọc board:** ba issue chưa xong của Sprint 1 (#319, #321, #323) vẫn giữ nguyên
> `Sprint 1` trên Project để giữ đúng lịch sử cam kết và để burndown ở trên khớp với board. Việc
> chuyển chúng sang Sprint 2 diễn ra ở buổi lập kế hoạch Sprint 2, không phải bây giờ. Sprint 2–4
> trên board hiện chứa **việc mới**, chưa gồm phần tồn này.

## 4. Rủi ro trễ

| Rủi ro | Issue | Ảnh hưởng tới mốc nào | Hành động | Ai làm, khi nào |
|---|---|---|---|---|
| **Khách chưa xác nhận luồng TO-BE** nên wireframe không khởi động được. #323 bị chặn bởi #319 đang chờ duyệt. | [#323](https://github.com/oNguyenVanManh/product-a-backlog/issues/323) ← [#319](https://github.com/oNguyenVanManh/product-a-backlog/issues/319) | Cổng duyệt Basic Design ([#326](https://github.com/oNguyenVanManh/product-a-backlog/issues/326) PRJ-09), dự kiến cuối tháng 11 | Đặt lịch họp xác nhận luồng TO-BE trong 3 ngày đầu Sprint 2; nếu khách chưa duyệt kịp thì Design bám bản nháp và ghi rõ là giả định | BrSE đặt lịch, chậm nhất 05/11/2026 |
| **Pha Requirement là pha nặng nhất** (263 MD theo LAB-1). Sprint 1 chỉ đạt 51,7 % nên phần hụt dồn sang các sprint sau. | [#321](https://github.com/oNguyenVanManh/product-a-backlog/issues/321), [#322](https://github.com/oNguyenVanManh/product-a-backlog/issues/322) | Mốc kết thúc Requirement | Chuyển #319, #321, #323 sang Sprint 2 và **không** nhận thêm việc mới vào Sprint 2 cho tới khi cả ba đóng | PM, đầu Sprint 2 |
| **完納奨励金 chưa được khách chốt chi tiết.** Quy tắc tra tỷ lệ theo ngày nghiệp vụ và cách ghi bút toán điều chỉnh mới là giả định của ta, chưa có văn bản khách xác nhận. | [#7](https://github.com/oNguyenVanManh/product-a-backlog/issues/7) EP-07 (69 SWP) | Toàn bộ EP-07; làm lại thì mất tới 69 SWP ≈ 276 h | Đưa câu hỏi vào nhật ký làm rõ ([#325](https://github.com/oNguyenVanManh/product-a-backlog/issues/325)) và **chặn mọi issue EP-07 khỏi Sprint 2–3** cho tới khi có trả lời bằng văn bản | BrSE gửi câu hỏi trong Sprint 2 |
| **業務日 02:00–10:00 JST và 休市日 chưa có lịch thật của chợ.** Thiếu lịch thì không kiểm được trigger khoá ngày. | [#98](https://github.com/oNguyenVanManh/product-a-backlog/issues/98) PRJ-16, EP-15 | Khung ứng dụng và mọi test liên quan khoá sổ | Xin lịch chợ 12 tháng gần nhất làm dữ liệu mẫu | BrSE, trong Sprint 2 |
| **Sức chứa BrSE đã kín 100 %** ngay sprint đầu, không còn đệm cho việc phát sinh từ phía khách. | #318, #319, #321, #325 | Mọi mốc phụ thuộc BrSE | Hoặc giảm tải BrSE xuống 80 % trong Sprint 2, hoặc chấp nhận trễ và nói trước với khách | PM quyết trước 09/11/2026 |
