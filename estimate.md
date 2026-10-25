# estimate.md — Chấm SWP, quy ra giờ và so với LAB-1

**Báo cáo HTML của skill:** [`reports/estimate-swp-report.html`](./reports/estimate-swp-report.html)
(mở thẳng bằng trình duyệt, tự chứa, không gọi tài nguyên ngoài)

Skill đã dùng: `tkm:estimate-swp`, nguồn là chính GitHub Project
<https://github.com/users/oNguyenVanManh/projects/2>.
Skill chấm **410 issue lá**; **127 issue cha** (19 epic + 108 issue chức năng) không được chấm trực
tiếp — SWP của chúng là **tổng SWP issue con**, đúng như đề bài yêu cầu.

> **Đây là lần chấm thứ hai.** Lần đầu chấm 346 issue lá khi backlog còn cap 4 MD và thân issue
> còn là khuôn mẫu rỗng. Sau khi hạ cap xuống 3 MD (471 → 537 issue), gắn tài liệu thiết kế đích
> danh và viết điều kiện nghiệm thu riêng cho 63 chức năng, **toàn bộ backlog được chấm lại từ đầu**
> trên 410 issue lá. Báo cáo HTML trong `reports/` là kết quả lần hai và **khớp đúng 537/537 issue
> trên board**.
>
> Vòng kiểm 5 issue mẫu cũng làm lại trên bộ mới — xem mục 1. Điểm của lần một không còn được dùng
> ở bất kỳ đâu; phần so sánh hai lần nằm ở mục 4 để thấy bằng chứng dày lên thì điểm đổi thế nào.

---

## 1. Issue mẫu skill chọn để kiểm

Skill tự chọn 5 issue theo quy tắc xác định (thấp nhất · trung vị dưới · cao nhất · ngoại lai ·
confidence thấp nhất) — tôi không chọn tay.

| Issue | Skill chấm (Scope × Complexity → SWP) | Tôi chốt | Lý do |
|---|---|---|---|
| [#156](https://github.com/oNguyenVanManh/product-a-backlog/issues/156) [FNC-010·FE] Khoá tạm khi sai nhiều lần và ghi log b | S1 × C1 → **1** | **giữ nguyên** | Giữ vì đúng: phần FE chỉ hiển thị trạng thái khoá và vô hiệu hoá form — logic đếm lần sai và ghi log nằm ở BE. Tầng này có **42 issue** nên nâng một nấc sẽ thổi phồng cả nhóm màn FE đơn giản. |
| [#161](https://github.com/oNguyenVanManh/product-a-backlog/issues/161) [FNC-012·BE] Kiểm tra quyền theo vai trò ở mọi thao  | S5 × C2 → **8** | S8 × C2 → **12** | Skill cho Scope 5 = "một luồng trọn vẹn". Thực tế tầng kiểm quyền chạy trên **mọi endpoint**, nên bề rộng là 8. Độ khó giữ 2. Tầng chỉ có 1 issue nên không lan. |
| [#313](https://github.com/oNguyenVanManh/product-a-backlog/issues/313) [FNC-062·BE] Job đồng bộ và hoà giải xung đột | S3 × C3 → **6** | S5 × C2 → **8** | Nâng từ 6 lên 8 để phản ánh công xử lý đồng thời và ghi bảng `sync_conflict`. **Đánh đổi đã được nêu trước khi chốt:** ô duy nhất cho 8 điểm là S5×C2, tức bề rộng tăng còn độ khó *giảm* từ 3 xuống 2 — ngược với lý do nâng. Ô S3×C5 = 9 điểm khớp lý do hơn. Người duyệt chọn 8 sau khi đã nghe rõ. Issue vẫn mang confidence thấp vì spec chưa nêu quy tắc hoà giải. |
| [#377](https://github.com/oNguyenVanManh/product-a-backlog/issues/377) [PRJ-23·Native 2/2] Unit test module còn lại + nativ | S3 × C1 → **4** | **giữ nguyên** | Giữ vì đúng: unit test là việc lặp theo mẫu, độ khó thấp; bề rộng đã phản ánh qua việc chia hạng mục thành nhiều phần. |
| [#524](https://github.com/oNguyenVanManh/product-a-backlog/issues/524) [PRJ-25·QA 5/5] Kiểm thử hệ thống theo kịch bản end- | S5 × C2 → **8** | **giữ nguyên** | Giữ vì đúng: mỗi phần phủ một nhóm luồng khác nhau trên cả web lẫn native, nên Scope 5 cho từng phần là hợp lý. |

### Một con số tôi đã chặn lại — và người duyệt vẫn giữ quyết định

Với [#313](https://github.com/oNguyenVanManh/product-a-backlog/issues/313), lý do nâng điểm là
**xử lý đồng thời và hoà giải xung đột** — một tuyên bố về *độ khó*. Nhưng ma trận SWP chỉ có hai ô
cho giá trị 8, và ô được chọn là **S5 × C2**: bề rộng tăng, độ khó **giảm** từ 3 xuống 2. Ngược hẳn
lý do nâng. Ô **S3 × C5 = 9 điểm** giữ nguyên bề rộng và nâng độ khó lên mức 5 = *"rủi ro cao, có
bằng chứng cụ thể"* — khớp lý do hơn.

Tôi nêu rõ đánh đổi này trước khi chốt. Người duyệt nghe xong vẫn chọn 8 điểm. Quyết định đó được
ghi nguyên văn cả hai vế vào `rationale` của bản hiệu chỉnh, để người review LAB-2 thấy đây là lựa
chọn có cân nhắc chứ không phải chỗ bỏ sót.

Đây là lần thứ hai tình huống này xảy ra. Lần chấm đầu, issue hàng đợi offline cũng bị chọn 20 điểm —
giá trị chỉ tồn tại ở ô Scope 13 = *"rộng cấp phát hành"*, sai cấu trúc cho một chức năng di động, và
lần đó đổi sang 16 điểm. **Bài học lặp lại: thang điểm rời rạc khiến một con số nghe hợp lý có thể
kéo theo một tuyên bố cấu trúc mà người chọn không có ý nói.** Phải luôn kiểm ô ma trận tương ứng
trước khi chốt, không chỉ kiểm con số.

### Ba sửa đổi lan tới đâu

Hiệu chỉnh chỉ lan sang **tầng giống hệt** — bộ bốn `(discipline, workType, scopeSignature, complexitySignature)`
phải trùng khít cả bốn. Không lan theo độ giống tiêu đề, không dùng hệ số bù chung.

| Luật | Tầng | Δ Scope | Δ Complexity | Từ issue | Lan sang |
|---|---|---:|---:|---|---:|
| cal-001 | `QA / test-design / single-component / routine` | +2 | 0 | [#139](https://github.com/oNguyenVanManh/product-a-backlog/issues/139) | 15 issue |
| cal-002 | `UI / feature / cross-layer / stateful+concurrency` | +1 | 0 | [#311](https://github.com/oNguyenVanManh/product-a-backlog/issues/311) | 1 issue |
| cal-003 | `Unknown / documentation / multi-component / routine` | 0 | +1 | [#125](https://github.com/oNguyenVanManh/product-a-backlog/issues/125), [#329](https://github.com/oNguyenVanManh/product-a-backlog/issues/329) | 11 issue |

**Tổng SWP: 1690 → 1701 (+0.7%)** · 5 approved · 3 propagated · 402 unchanged · 0 dòng chạm biên dải.

---

## 2. Cách quy ra giờ

Tôi chọn **đặt quy ước đổi SWP ra giờ**, không ước trực tiếp từng issue.

**Vì sao:** 537 issue mà ước tay từng cái thì mỗi con số là một phán đoán riêng, không ai kiểm được
tính nhất quán. Một quy ước công khai thì bất kỳ ai cũng kiểm lại được toàn bộ bảng bằng một phép nhân.

Quy ước **không** chia ngược từ MD của LAB-1. Nếu lấy MD cũ chia ra giờ thì phép so LAB-1 ↔ LAB-5 ở
mục 5 thành vòng tròn, không nói lên điều gì. Để giữ tính độc lập, dòng `**Effort LAB-1:** X MD` còn
**bị cắt khỏi gói bằng chứng** gửi cho bộ chấm SWP (thân issue trên GitHub giữ nguyên để truy vết).

### Quy tắc A — việc giao hàng: `giờ = SWP × 4`

Neo ở định nghĩa thấp nhất của chính thang chấm: **SWP 1 = Scope 1 × Complexity 0** = "một thay đổi
cục bộ, theo mẫu đã biết, không rẽ nhánh đáng kể". Một thay đổi như vậy, **làm xong trọn vẹn** kèm
test và review, mất khoảng **nửa ngày làm việc = 4 giờ**. Các mức trên nhân tuyến tính theo đó.

### Quy tắc B — việc theo lịch (EP-19): quy từ tỷ lệ phân bổ

| Vai trò | Phân bổ | Phép tính | Tổng | Mỗi issue tháng |
|---|---|---|---:|---:|
| PM | 70% × 10 tháng | 0,7 × 10 × 20 ngày × 8h | 1.120 h | 112 h |
| BrSE (cầu nối) | 50% × 10 tháng | 0,5 × 10 × 20 ngày × 8h | 800 h | 80 h |

**Vì sao phải có ngoại lệ:** SWP đo **kích thước công việc**, còn công quản trị bị đóng khung bởi
**thời gian** — PM vẫn phải họp khách hằng tuần dù tháng đó team viết nhiều code hay ít. Ép nó qua
quy tắc A cho ra 40 SWP × 4 = **160 giờ cho cả 10 tháng**, tức 2 ngày công PM mỗi tháng. Con số đó
vô lý, và nó vô lý vì dùng sai thước đo chứ không phải vì chấm sai điểm.

Hai quy tắc áp nhất quán: mọi issue không thuộc EP-19 đều đúng `SWP × 4`, không có ngoại lệ lẻ nào.

---

## 3. Tổng theo epic

| Epic | Số issue | Tổng SWP | Tổng giờ | Ghi chú |
|---|--:|--:|--:|---|
| [`EP-01` #1](https://github.com/oNguyenVanManh/product-a-backlog/issues/1) Quản lý bên tham gia và tư cách giao dịch | 27 | 74 | 296 | Ràng buộc hai cấp quyền 許可/承認 |
| [`EP-02` #2](https://github.com/oNguyenVanManh/product-a-backlog/issues/2) Xác thực và phân quyền | 29 | 84 | 336 | — |
| [`EP-03` #3](https://github.com/oNguyenVanManh/product-a-backlog/issues/3) Tiếp nhận lô và thẩm định | 24 | 77 | 308 | Giữ người trong vòng lặp (CAP-HUMAN-01) |
| [`EP-04` #4](https://github.com/oNguyenVanManh/product-a-backlog/issues/4) Giao dịch thỏa thuận và đấu giá | 25 | 66 | 264 | 相対取引 chiếm phần lớn giá trị |
| [`EP-05` #5](https://github.com/oNguyenVanManh/product-a-backlog/issues/5) Theo dõi giao hàng | 35 | 109 | 436 | — |
| [`EP-06` #6](https://github.com/oNguyenVanManh/product-a-backlog/issues/6) Đối soát, chốt sổ và điều chỉnh | 27 | 100 | 400 | 業務日 và khoá sổ |
| [`EP-07` #7](https://github.com/oNguyenVanManh/product-a-backlog/issues/7) Tiền khuyến khích thanh toán đúng hạn | 23 | 81 | 324 | 完納奨励金 |
| [`EP-08` #8](https://github.com/oNguyenVanManh/product-a-backlog/issues/8) Quản lý quy định và biểu suất | 19 | 46 | 184 | — |
| [`EP-09` #9](https://github.com/oNguyenVanManh/product-a-backlog/issues/9) Báo cáo và xuất dữ liệu | 18 | 45 | 180 | — |
| [`EP-10` #10](https://github.com/oNguyenVanManh/product-a-backlog/issues/10) Kiểm toán và lưu trữ | 16 | 38 | 152 | — |
| [`EP-11` #11](https://github.com/oNguyenVanManh/product-a-backlog/issues/11) Thông báo | 17 | 40 | 160 | — |
| [`EP-12` #12](https://github.com/oNguyenVanManh/product-a-backlog/issues/12) Liên kết hệ thống kế toán | 14 | 43 | 172 | — |
| [`EP-13` #13](https://github.com/oNguyenVanManh/product-a-backlog/issues/13) Danh mục nền và đồng bộ offline | 25 | 83 | 332 | — |
| [`EP-14` #14](https://github.com/oNguyenVanManh/product-a-backlog/issues/14) Yêu cầu và thiết kế xuyên suốt | 38 | 105 | 420 | — |
| [`EP-15` #15](https://github.com/oNguyenVanManh/product-a-backlog/issues/15) Nền tảng ứng dụng và hạ tầng | 48 | 177 | 708 | 業務日 và khoá sổ |
| [`EP-16` #16](https://github.com/oNguyenVanManh/product-a-backlog/issues/16) Kiểm thử và chất lượng | 69 | 275 | 1,100 | — |
| [`EP-17` #17](https://github.com/oNguyenVanManh/product-a-backlog/issues/17) Chuyển đổi dữ liệu | 23 | 90 | 360 | — |
| [`EP-18` #18](https://github.com/oNguyenVanManh/product-a-backlog/issues/18) UAT, phát hành và bàn giao | 37 | 118 | 472 | — |
| [`EP-19` #19](https://github.com/oNguyenVanManh/product-a-backlog/issues/19) Quản trị dự án và cầu nối nghiệp vụ | 23 | 50 | 1,920 | Quy giờ theo quy tắc B (miễn cap 3 MD) |
| **Tổng** | **537** | **1701** | **8,524** | = **1,066 MD** (8h/ngày) |

*Số issue đếm cả epic, issue cha và issue con. SWP của epic là tổng SWP issue lá nên không đếm trùng — 19 epic cộng lại đúng bằng 1.701, bằng tổng 410 issue lá.*

---

## 4. So với estimate LAB-1

| Phần (epic) | LAB-1 gộp (MD) | LAB-5 (MD) | Chênh | Vì sao |
|---|--:|--:|--:|---|
| [`EP-01` #1](https://github.com/oNguyenVanManh/product-a-backlog/issues/1) Quản lý bên tham gia và tư cách giao | 29.4 | 37.0 | +7.6 (+26%) | Thân issue dày hơn sau khi gắn tài liệu thiết kế và viết DoD riêng → bộ chấm đọc ra nhiều bề rộng hơn lần 1 |
| [`EP-02` #2](https://github.com/oNguyenVanManh/product-a-backlog/issues/2) Xác thực và phân quyền | 32.6 | 42.0 | +9.4 (+29%) | Thân issue dày hơn sau khi gắn tài liệu thiết kế và viết DoD riêng → bộ chấm đọc ra nhiều bề rộng hơn lần 1 |
| [`EP-03` #3](https://github.com/oNguyenVanManh/product-a-backlog/issues/3) Tiếp nhận lô và thẩm định | 33.9 | 38.5 | +4.6 (+14%) | Gần khớp |
| [`EP-04` #4](https://github.com/oNguyenVanManh/product-a-backlog/issues/4) Giao dịch thỏa thuận và đấu giá | 33.6 | 33.0 | -0.6 (-2%) | Gần khớp |
| [`EP-05` #5](https://github.com/oNguyenVanManh/product-a-backlog/issues/5) Theo dõi giao hàng | 55.1 | 54.5 | -0.6 (-1%) | Gần khớp |
| [`EP-06` #6](https://github.com/oNguyenVanManh/product-a-backlog/issues/6) Đối soát, chốt sổ và điều chỉnh | 39.8 | 50.0 | +10.2 (+26%) | Thân issue dày hơn sau khi gắn tài liệu thiết kế và viết DoD riêng → bộ chấm đọc ra nhiều bề rộng hơn lần 1 |
| [`EP-07` #7](https://github.com/oNguyenVanManh/product-a-backlog/issues/7) Tiền khuyến khích thanh toán đúng hạ | 37.8 | 40.5 | +2.7 (+7%) | Gần khớp |
| [`EP-08` #8](https://github.com/oNguyenVanManh/product-a-backlog/issues/8) Quản lý quy định và biểu suất | 28.0 | 23.0 | -5.0 (-18%) | SWP vẫn không đo được khối lượng đến từ **số lần lặp** — xem phần dưới bảng |
| [`EP-09` #9](https://github.com/oNguyenVanManh/product-a-backlog/issues/9) Báo cáo và xuất dữ liệu | 18.8 | 22.5 | +3.7 (+20%) | Gần khớp |
| [`EP-10` #10](https://github.com/oNguyenVanManh/product-a-backlog/issues/10) Kiểm toán và lưu trữ | 17.7 | 19.0 | +1.3 (+7%) | Gần khớp |
| [`EP-11` #11](https://github.com/oNguyenVanManh/product-a-backlog/issues/11) Thông báo | 19.2 | 20.0 | +0.8 (+4%) | Gần khớp |
| [`EP-12` #12](https://github.com/oNguyenVanManh/product-a-backlog/issues/12) Liên kết hệ thống kế toán | 16.5 | 21.5 | +5.0 (+30%) | Thân issue dày hơn sau khi gắn tài liệu thiết kế và viết DoD riêng → bộ chấm đọc ra nhiều bề rộng hơn lần 1 |
| [`EP-13` #13](https://github.com/oNguyenVanManh/product-a-backlog/issues/13) Danh mục nền và đồng bộ offline | 31.7 | 41.5 | +9.8 (+31%) | Thân issue dày hơn sau khi gắn tài liệu thiết kế và viết DoD riêng → bộ chấm đọc ra nhiều bề rộng hơn lần 1 |
| [`EP-14` #14](https://github.com/oNguyenVanManh/product-a-backlog/issues/14) Yêu cầu và thiết kế xuyên suốt | 71.0 | 52.5 | -18.5 (-26%) | SWP vẫn không đo được khối lượng đến từ **số lần lặp** — xem phần dưới bảng |
| [`EP-15` #15](https://github.com/oNguyenVanManh/product-a-backlog/issues/15) Nền tảng ứng dụng và hạ tầng | 87.0 | 88.5 | +1.5 (+2%) | Gần khớp |
| [`EP-16` #16](https://github.com/oNguyenVanManh/product-a-backlog/issues/16) Kiểm thử và chất lượng | 153.0 | 137.5 | -15.5 (-10%) | Gần khớp |
| [`EP-17` #17](https://github.com/oNguyenVanManh/product-a-backlog/issues/17) Chuyển đổi dữ liệu | 38.0 | 45.0 | +7.0 (+18%) | Gần khớp |
| [`EP-18` #18](https://github.com/oNguyenVanManh/product-a-backlog/issues/18) UAT, phát hành và bàn giao | 76.0 | 59.0 | -17.0 (-22%) | SWP vẫn không đo được khối lượng đến từ **số lần lặp** — xem phần dưới bảng |
| [`EP-19` #19](https://github.com/oNguyenVanManh/product-a-backlog/issues/19) Quản trị dự án và cầu nối nghiệp vụ | 240.0 | 240.0 | +0.0 (+0%) | **Trùng khít tuyệt đối** — quy tắc B dùng đúng tỷ lệ phân bổ 70%/50% × 10 tháng mà LAB-1 đã dùng. Không phải xác nhận độc lập |
| **Tổng** | **1,059.1** | **1,065.5** | **+6.4 (+0.6%)** | |

### Đọc bảng này cho đúng

**So gộp với gộp.** LAB-5 quy giờ thẳng từ cấu trúc issue, không trừ phần nào cho AIDD, nên nó là
con số **gộp**. Đặt cạnh LAB-1 gộp: **1.065,5 MD so với 1.059,1 MD, cao hơn 0,6 %**.

**Đừng so với 911,9 MD.** LAB-1 còn một dòng ròng là 911,9 MD (sau khi trừ 147,2 MD cho AIDD, trừ
theo từng vai trò chứ không đồng loạt). Đặt 1.065,5 cạnh 911,9 là **so gộp với ròng** — sai loại.

### Lần chấm này khác lần đầu ở đâu

Backlog được chấm **hai lần**, và lần thứ hai cho kết quả khác hẳn:

| | Lần 1 | Lần 2 |
|---|--:|--:|
| Issue lá được chấm | 346 | **410** |
| Tổng SWP | 1.392 | **1.701** |
| Quy ra giờ | 7.328 h = 916 MD | **8.524 h = 1.065,5 MD** |
| `evidenceStatus = EXTRACTED` | 2/346 | **215/410** |
| `confidence = high` | 0/346 | **87/410** |
| Chênh so với LAB-1 gộp | −13,5 % | **+0,6 %** |

Nguyên nhân không phải đổi thang chấm — thang giữ nguyên, hệ số quy giờ giữ nguyên 4 h/SWP. Nguyên
nhân là **bằng chứng đưa cho bộ chấm dày lên**:

- Lần 1, thân issue chỉ có khung mẫu rỗng (Phạm vi / Truy vết trỏ *thư mục* / Định nghĩa xong theo
  vai trò). 344/346 dòng phải để `INFERRED` + `medium` vì bộ chấm chủ yếu đoán từ tiêu đề.
- Lần 2, mỗi issue chức năng trỏ tới **tài liệu thiết kế đích danh** và 63 issue cha mang **điều kiện
  nghiệm thu cụ thể** (tên field, mã lỗi, quy tắc nghiệp vụ). Hơn một nửa số dòng đạt `EXTRACTED`.

Ranh giới hiện ra rất rõ trong dữ liệu: lô chấm toàn issue `FNC-*` (có bảng tài liệu) đạt **57/82**
dòng `high`; lô toàn issue `PRJ-*` (thân còn mỏng) đạt **0/82**. Cả năm bộ chấm đều độc lập nêu cùng
một lý do.

**Điều này nói gì về bản ước lượng đầu tiên:** nó không sai về phương pháp, nhưng nó được chấm trên
một backlog chưa đủ thông tin để chấm. Con số 916 MD khi đó phản ánh *độ mỏng của mô tả công việc*
nhiều hơn là *khối lượng công việc thật*.

### Hai con số gặp nhau — vẫn đừng vội mừng

1.065,5 MD và 1.059,1 MD cách nhau 0,6 %. Lần 1 cũng từng có một trùng hợp tương tự (916 với 911,9)
và hoá ra là **so sai loại số**. Lần này so đúng loại, nhưng cảnh báo cũ vẫn nguyên giá trị:

**Hệ số 4 giờ/SWP là lựa chọn của tôi.** Neo ở 3 giờ thì tổng ra **799 MD**; neo ở 5 giờ thì ra
**1.332 MD**. Cái cố định là *hình dạng* bảng — tỷ lệ giữa các epic — chứ không phải *độ lớn* tuyệt
đối. Hai phương pháp gặp nhau chỉ nói lên chúng **không mâu thuẫn về hình dạng**.

### Chỗ hai bản vẫn lệch, và nguyên nhân gọi được tên

| Epic | LAB-1 | LAB-5 | Chênh | Nguyên nhân |
|---|--:|--:|--:|---|
| EP-14 Yêu cầu và thiết kế xuyên suốt | 71,0 | 52,5 | −18,5 | Khối lượng đến từ **số lần lặp** (đặc tả 30 màn), mà `Scope × Complexity` không có trục nào đo lặp |
| EP-18 UAT, phát hành và bàn giao | 76,0 | 59,0 | −17,0 | Hỗ trợ UAT 6 tuần là việc **kéo dài theo lịch**, cùng bản chất với EP-19 |
| EP-16 Kiểm thử và chất lượng | 153,0 | 137,5 | −15,5 | Cùng lý do lặp: viết test cho 63 chức năng |
| EP-06 Đối soát, chốt sổ | 39,8 | 50,0 | +10,2 | Ngược chiều: DoD riêng làm lộ ra độ khó thật của khoá sổ và bút toán đảo |
| EP-13 Danh mục nền và đồng bộ offline | 31,7 | 41,5 | +9,8 | Ngược chiều: hàng đợi offline và hoà giải xung đột nặng hơn LAB-1 ước |

Ba epic đầu thấp hơn vì cùng một giới hạn của thước đo: **SWP đo kích thước cấu trúc, không đo số
lần lặp hay độ dài lịch.** Quy tắc B ở mục 2 chính là chỗ đã phải thừa nhận giới hạn đó một lần cho
EP-19.

Hai epic cuối cao hơn, và đây là tín hiệu đáng tin hơn cả: chúng là hai nhóm được viết DoD riêng kỹ
nhất, và khi điều kiện nghiệm thu hiện ra cụ thể thì bộ chấm đọc được độ khó mà LAB-1 chưa thấy.

### Chỗ đáng ngờ nhất trong chính bản LAB-5

**193/410 dòng vẫn ở `INFERRED`.** Gần như toàn bộ nằm ở issue `PRJ-*` (hạ tầng, kiểm thử, chuyển
đổi, quản trị) — nhóm chưa được viết DoD riêng. Muốn phần này chắc như phần `FNC-*` thì phải viết
điều kiện nghiệm thu cụ thể cho chúng nữa; chi phí đó chưa bỏ ra.

**Sub-issue vẫn dùng DoD theo vai trò.** DoD riêng mới viết cho 63 issue cha. Cả năm bộ chấm đều nêu
đây là lý do chính khiến nhiều dòng `FNC-*` dừng ở `medium` thay vì lên `high` — và sub-issue mới là
thứ dev thật sự nhận để làm.
