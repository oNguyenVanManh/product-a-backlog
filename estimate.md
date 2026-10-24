# estimate.md — Chấm SWP, quy ra giờ và so với LAB-1

**Báo cáo HTML của skill:** [`reports/estimate-swp-report.html`](./reports/estimate-swp-report.html)
(mở thẳng bằng trình duyệt, tự chứa, không gọi tài nguyên ngoài)

Skill đã dùng: `tkm:estimate-swp`, nguồn là chính GitHub Project
<https://github.com/users/oNguyenVanManh/projects/2>.
Skill chấm **346 issue lá**; 125 issue cha không được chấm trực tiếp — SWP của chúng là **tổng SWP
issue con**, đúng như đề bài yêu cầu.

> **Backlog đã được tách lại SAU khi chấm điểm — đọc mục này trước khi so số.**
>
> Lúc chấm, cap độ hạt là 4 MD/issue lá: **346 lá, 125 cha, tổng 471 issue**. Sau đó phát hiện phép
> tính biện minh cho cap 4 MD là sai (4 MD là 4 ngày công, không phải 3 — xem
> [`task-breakdown.md`](./task-breakdown.md) §1), nên cap hạ xuống **3 MD** và backlog tách lại thành
> **410 lá, 127 cha, tổng 537 issue**.
>
> **Điểm không chấm lại.** Khi một lá bị tách đôi, hai nửa **chia nhau SWP của lá gốc** (ví dụ 5 → 3+2)
> thay vì được chấm lại. Lý do: tách thay đổi *cách theo dõi* công việc, không thay đổi *lượng* công
> việc — và chấm lại sẽ vứt bỏ phần đã qua người kiểm ở mục 1. Tổng SWP vì vậy giữ nguyên **1.392**,
> mọi phân tích ở mục 3 và 4 vẫn đúng.
>
> **Cái giá phải trả, nói thẳng:** SWP của 66 issue mới **không còn là một ô của ma trận
> `Scope × Complexity`** mà là phần chia theo tỷ lệ. Báo cáo HTML trong `reports/` là ảnh chụp **trước
> khi tách**, nên nó có 471 dòng chứ không phải 537. Muốn hai thứ khớp nhau hoàn toàn thì phải chạy
> lại skill trên backlog mới và làm lại vòng kiểm 5 issue mẫu — chi phí đó chưa bỏ ra ở bài này.

---

## 1. Issue mẫu skill chọn để kiểm

Skill tự chọn 5 issue theo quy tắc xác định (thấp nhất · trung vị dưới · cao nhất · ngoại lai ·
confidence thấp nhất) — tôi không chọn tay.

| Issue | Skill chấm (Scope × Complexity → SWP) | Tôi chốt | Lý do |
|---|---|---|---|
| [#139](https://github.com/oNguyenVanManh/product-a-backlog/issues/139) [FNC-004·QA] Bảng theo dõi hiệu lực tư cách | S1 × C1 → **1** | S3 × C1 → **4** | Skill đọc "bảng theo dõi" thành một thành phần hẹp. Thực tế QA màn này phải phủ **cả hai cấp quyền pháp lý** 許可 (仲卸) và 承認 (売買参加者), cộng ca hết hạn tư cách — bề rộng là 3, không phải 1. Độ khó giữ nguyên vì vẫn là validation quen thuộc. |
| [#125](https://github.com/oNguyenVanManh/product-a-backlog/issues/125) [PRJ-43] Ma trận tuân thủ + traceability | S3 × C1 → **4** | **giữ nguyên** *(nay là issue cha)* | Giữ vì đúng: là việc tài liệu lặp lại, không có quyết định kỹ thuật nào. **Sau khi hạ cap xuống 3 MD, issue này vượt cap nên thành issue cha có 2 con; SWP 4 anh duyệt giữ nguyên dưới dạng tổng 2+2.** Bề rộng 3 phản ánh việc phải quét hết các ID yêu cầu; độ khó 1 phản ánh không có tích hợp hay trạng thái phức tạp. |
| [#311](https://github.com/oNguyenVanManh/product-a-backlog/issues/311) [FNC-061·Native] Hàng đợi offline trên thiết bị | S5 × C3 → **10** | S8 × C3 → **16** | Hàng đợi offline phải chạy trên iOS, Android **và** phía server nhận lại — đó là nhiều nền tảng, bề rộng 8 chứ không phải 5. Độ khó giữ 3. |
| [#329](https://github.com/oNguyenVanManh/product-a-backlog/issues/329) [PRJ-10·BrSE] Đặc tả 30 màn hình web | S8 × C1 → **10** | S8 × C2 → **12** | Skill cho độ khó 1 ("từng màn theo mẫu"). Thực tế đặc tả phải viết cho khách Nhật duyệt và phải diễn đạt đúng hai cấp quyền trên từng màn — độ khó 2. Bề rộng giữ 8. |
| [#398](https://github.com/oNguyenVanManh/product-a-backlog/issues/398) [PRJ-29·BE] Kiểm thử hồi quy sau mỗi vòng sửa lỗi | S2 × C1 → **3** | **giữ nguyên** | Giữ vì đúng: chạy lại bộ ca đã có là việc lặp. Bề rộng thực của hồi quy nằm ở issue QA của từng chức năng, không ở phần BE này — gộp vào đây là đếm hai lần. |

### Một con số tôi đã chặn lại

Lần đầu tôi chọn **20 điểm** cho [#311](https://github.com/oNguyenVanManh/product-a-backlog/issues/311). Ma trận SWP chỉ có **đúng một ô** cho giá trị 20:
Scope 13 × Complexity 2. Scope 13 nghĩa là *"rộng cấp phát hành hoặc xuyên hệ thống"* — gán nhãn đó
cho hàng đợi offline của **một** chức năng di động là sai về cấu trúc, và vì hiệu chỉnh lan theo tầng
nên nó sẽ kéo theo issue khác. Đổi sang **16 điểm** (Scope 8 × Complexity 3): vẫn mức khó, nhưng bề
rộng được ghi đúng là "nhiều nền tảng" chứ không phải "cấp phát hành".

### Ba sửa đổi lan tới đâu

Hiệu chỉnh chỉ lan sang **tầng giống hệt** — bộ bốn `(discipline, workType, scopeSignature, complexitySignature)`
phải trùng khít cả bốn. Không lan theo độ giống tiêu đề, không dùng hệ số bù chung.

| Luật | Tầng | Δ Scope | Δ Complexity | Từ issue | Lan sang |
|---|---|---:|---:|---|---:|
| cal-001 | `QA / test-design / single-component / routine` | +2 | 0 | [#139](https://github.com/oNguyenVanManh/product-a-backlog/issues/139) | 15 issue |
| cal-002 | `UI / feature / cross-layer / stateful+concurrency` | +1 | 0 | [#311](https://github.com/oNguyenVanManh/product-a-backlog/issues/311) | 1 issue |
| cal-003 | `Unknown / documentation / multi-component / routine` | 0 | +1 | [#125](https://github.com/oNguyenVanManh/product-a-backlog/issues/125), [#329](https://github.com/oNguyenVanManh/product-a-backlog/issues/329) | 11 issue |

**Tổng SWP: 1.323 → 1.392 (+5,2%)** · 5 approved · 26 propagated · 315 unchanged · 0 dòng chạm biên dải.

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
| [`EP-01` #1](https://github.com/oNguyenVanManh/product-a-backlog/issues/1) Quản lý bên tham gia và tư cách giao dịch | 27 | 52 | 208 | Ràng buộc hai cấp quyền 許可/承認 |
| [`EP-02` #2](https://github.com/oNguyenVanManh/product-a-backlog/issues/2) Xác thực và phân quyền | 29 | 67 | 268 | — |
| [`EP-03` #3](https://github.com/oNguyenVanManh/product-a-backlog/issues/3) Tiếp nhận lô và thẩm định | 24 | 62 | 248 | Giữ người trong vòng lặp (CAP-HUMAN-01) |
| [`EP-04` #4](https://github.com/oNguyenVanManh/product-a-backlog/issues/4) Giao dịch thỏa thuận và đấu giá | 25 | 54 | 216 | 相対取引 chiếm phần lớn giá trị |
| [`EP-05` #5](https://github.com/oNguyenVanManh/product-a-backlog/issues/5) Theo dõi giao hàng | 35 | 89 | 356 | — |
| [`EP-06` #6](https://github.com/oNguyenVanManh/product-a-backlog/issues/6) Đối soát, chốt sổ và điều chỉnh | 27 | 71 | 284 | 業務日 và khoá sổ |
| [`EP-07` #7](https://github.com/oNguyenVanManh/product-a-backlog/issues/7) Tiền khuyến khích thanh toán đúng hạn | 23 | 69 | 276 | 完納奨励金 |
| [`EP-08` #8](https://github.com/oNguyenVanManh/product-a-backlog/issues/8) Quản lý quy định và biểu suất | 19 | 46 | 184 | — |
| [`EP-09` #9](https://github.com/oNguyenVanManh/product-a-backlog/issues/9) Báo cáo và xuất dữ liệu | 18 | 43 | 172 | — |
| [`EP-10` #10](https://github.com/oNguyenVanManh/product-a-backlog/issues/10) Kiểm toán và lưu trữ | 16 | 32 | 128 | — |
| [`EP-11` #11](https://github.com/oNguyenVanManh/product-a-backlog/issues/11) Thông báo | 17 | 40 | 160 | — |
| [`EP-12` #12](https://github.com/oNguyenVanManh/product-a-backlog/issues/12) Liên kết hệ thống kế toán | 14 | 27 | 108 | — |
| [`EP-13` #13](https://github.com/oNguyenVanManh/product-a-backlog/issues/13) Danh mục nền và đồng bộ offline | 25 | 76 | 304 | — |
| [`EP-14` #14](https://github.com/oNguyenVanManh/product-a-backlog/issues/14) Yêu cầu và thiết kế xuyên suốt | 38 | 117 | 468 | — |
| [`EP-15` #15](https://github.com/oNguyenVanManh/product-a-backlog/issues/15) Nền tảng ứng dụng và hạ tầng | 48 | 112 | 448 | 業務日 và khoá sổ |
| [`EP-16` #16](https://github.com/oNguyenVanManh/product-a-backlog/issues/16) Kiểm thử và chất lượng | 69 | 197 | 788 | — |
| [`EP-17` #17](https://github.com/oNguyenVanManh/product-a-backlog/issues/17) Chuyển đổi dữ liệu | 23 | 76 | 304 | — |
| [`EP-18` #18](https://github.com/oNguyenVanManh/product-a-backlog/issues/18) UAT, phát hành và bàn giao | 37 | 122 | 488 | — |
| [`EP-19` #19](https://github.com/oNguyenVanManh/product-a-backlog/issues/19) Quản trị dự án và cầu nối nghiệp vụ | 23 | 40 | 1,920 | Quy giờ theo quy tắc B (miễn cap 3 MD) |
| **Tổng** | **537** | **1392** | **7,328** | = **916 MD** (8h/ngày) |

*Số issue đếm cả epic, issue cha và issue con. SWP của epic là tổng SWP issue lá nên không đếm trùng — 19 epic cộng lại đúng bằng 1.392, bằng tổng 410 issue lá.*

---

## 4. So với estimate LAB-1

| Phần (epic) | LAB-1 gộp (MD) | LAB-5 (MD) | Chênh | Vì sao |
|---|--:|--:|--:|---|
| [`EP-01` #1](https://github.com/oNguyenVanManh/product-a-backlog/issues/1) Quản lý bên tham gia và tư cách giao d | 29.4 | 26.0 | -3.4 (-12%) | Giảm nhẹ dù QA đã được nâng ở [#139](https://github.com/oNguyenVanManh/product-a-backlog/issues/139) — phần BE/FE vẫn thấp hơn LAB-1. |
| [`EP-02` #2](https://github.com/oNguyenVanManh/product-a-backlog/issues/2) Xác thực và phân quyền | 32.6 | 33.5 | +0.9 (+3%) | Gần như trùng khít. |
| [`EP-03` #3](https://github.com/oNguyenVanManh/product-a-backlog/issues/3) Tiếp nhận lô và thẩm định | 33.9 | 31.0 | -2.9 (-9%) | — |
| [`EP-04` #4](https://github.com/oNguyenVanManh/product-a-backlog/issues/4) Giao dịch thỏa thuận và đấu giá | 33.6 | 27.0 | -6.6 (-20%) | — |
| [`EP-05` #5](https://github.com/oNguyenVanManh/product-a-backlog/issues/5) Theo dõi giao hàng | 55.1 | 44.5 | -10.6 (-19%) | 7 màn native + luồng offline: LAB-1 cấp 55,1 MD, SWP đọc là 44,5 MD. |
| [`EP-06` #6](https://github.com/oNguyenVanManh/product-a-backlog/issues/6) Đối soát, chốt sổ và điều chỉnh | 39.8 | 35.5 | -4.3 (-11%) | — |
| [`EP-07` #7](https://github.com/oNguyenVanManh/product-a-backlog/issues/7) Tiền khuyến khích thanh toán đúng hạn | 37.8 | 34.5 | -3.3 (-9%) | — |
| [`EP-08` #8](https://github.com/oNguyenVanManh/product-a-backlog/issues/8) Quản lý quy định và biểu suất | 28.0 | 23.0 | -5.0 (-18%) | — |
| [`EP-09` #9](https://github.com/oNguyenVanManh/product-a-backlog/issues/9) Báo cáo và xuất dữ liệu | 18.8 | 21.5 | +2.7 (+14%) | Tăng nhẹ: SWP đọc trung tâm báo cáo rộng hơn LAB-1 ước. |
| [`EP-10` #10](https://github.com/oNguyenVanManh/product-a-backlog/issues/10) Kiểm toán và lưu trữ | 17.7 | 16.0 | -1.7 (-10%) | — |
| [`EP-11` #11](https://github.com/oNguyenVanManh/product-a-backlog/issues/11) Thông báo | 19.2 | 20.0 | +0.8 (+4%) | Gần như trùng khít. |
| [`EP-12` #12](https://github.com/oNguyenVanManh/product-a-backlog/issues/12) Liên kết hệ thống kế toán | 16.5 | 13.5 | -3.0 (-18%) | — |
| [`EP-13` #13](https://github.com/oNguyenVanManh/product-a-backlog/issues/13) Danh mục nền và đồng bộ offline | 31.7 | 38.0 | +6.3 (+20%) | **Hướng ngược lại.** Tăng vì tôi nâng hàng đợi offline [#311](https://github.com/oNguyenVanManh/product-a-backlog/issues/311) từ 10 lên 16 SWP khi kiểm issue mẫu — bề rộng thật là iOS + Android + server. |
| [`EP-14` #14](https://github.com/oNguyenVanManh/product-a-backlog/issues/14) Yêu cầu và thiết kế xuyên suốt | 71.0 | 58.5 | -12.5 (-18%) | Đặc tả 30 màn đã được tôi nâng từ 10 lên 12 SWP, nhưng vẫn thấp hơn 17 MD của LAB-1 vì cùng lý do lặp. |
| [`EP-15` #15](https://github.com/oNguyenVanManh/product-a-backlog/issues/15) Nền tảng ứng dụng và hạ tầng | 87.0 | 56.0 | -31.0 (-36%) | Cùng nguyên nhân: 4 issue Terraform và CI/CD được SWP đọc theo số thành phần, LAB-1 ước theo số môi trường phải dựng thật. |
| [`EP-16` #16](https://github.com/oNguyenVanManh/product-a-backlog/issues/16) Kiểm thử và chất lượng | 153.0 | 98.5 | -54.5 (-36%) | **Chênh lớn nhất.** SWP đọc "unit test module nghiệp vụ lõi" là một việc bề rộng vừa, độ khó vừa. LAB-1 cấp 24 MD vì phải viết test cho 63 chức năng — khối lượng đến từ **số lần lặp**, mà SWP không đo lặp. |
| [`EP-17` #17](https://github.com/oNguyenVanManh/product-a-backlog/issues/17) Chuyển đổi dữ liệu | 38.0 | 38.0 | +0.0 (+0%) | Trùng khít, ngẫu nhiên. |
| [`EP-18` #18](https://github.com/oNguyenVanManh/product-a-backlog/issues/18) UAT, phát hành và bàn giao | 76.0 | 61.0 | -15.0 (-20%) | Hỗ trợ UAT 6 tuần là việc kéo dài theo lịch, giống EP-19 — SWP đo kích thước nên đọc nhỏ hơn thực tế. |
| [`EP-19` #19](https://github.com/oNguyenVanManh/product-a-backlog/issues/19) Quản trị dự án và cầu nối nghiệp vụ | 240.0 | 240.0 | +0.0 (+0%) | **Trùng khít tuyệt đối**, vì quy tắc B dùng đúng tỷ lệ phân bổ 70%/50% × 10 tháng mà LAB-1 đã dùng. Đây không phải xác nhận độc lập. |
| **Tổng** | **1,059.1** | **916.0** | **-143.1 (-13.5%)** | |

### Đọc bảng này cho đúng

**So gộp với gộp.** LAB-5 quy giờ thẳng từ cấu trúc issue, không trừ phần nào cho AIDD, nên nó là
con số **gộp**. Đặt cạnh LAB-1 gộp: **916 MD so với 1.059,1 MD, thấp hơn 13,5%**.

**Đừng so với 911,9 MD.** LAB-1 còn một dòng ròng là 911,9 MD (sau khi trừ 147,2 MD cho AIDD, trừ
theo từng vai trò chứ không đồng loạt). Con số 916 của LAB-5 tình cờ nằm sát 911,9, nhưng đặt hai số
đó cạnh nhau là **so gộp với ròng** — sai loại. Tôi ghi ra đây vì chính tôi đã suýt rơi vào cái bẫy
số học này khi làm bài.

### Chênh 143 MD đến từ đâu — và nó nói lên giới hạn của SWP

Mười bảy trên mười chín epic thấp hơn LAB-1. Ba epic chiếm quá nửa khoảng chênh:

| Epic | Chênh | Bản chất công việc |
|---|--:|---|
| EP-16 Kiểm thử và chất lượng | −54,5 MD | viết test cho 63 chức năng |
| EP-15 Nền tảng và hạ tầng | −31,0 MD | dựng Terraform cho nhiều môi trường |
| EP-18 UAT và bàn giao | −15,0 MD | hỗ trợ khách 6 tuần |

Cả ba có chung một đặc điểm: **khối lượng đến từ số lần lặp hoặc độ dài lịch, không từ bề rộng cấu
trúc.** Thang SWP đo `Scope × Complexity` — bề rộng nhân độ khó. Nó không có trục nào cho "việc này
đơn giản nhưng phải làm 63 lần". Viết unit test cho chức năng thứ 60 không khó hơn chức năng đầu,
nên cả cụm bị đọc là một việc bề rộng vừa.

Đây **không** phải lỗi chấm điểm, và cũng không phải lỗi của LAB-1. Đây là giới hạn của thước đo:
SWP là thước đo tốt cho việc *thiết kế và cài đặt*, kém cho việc *lặp lại và chờ đợi*. Quy tắc B ở
mục 2 chính là chỗ tôi đã phải thừa nhận giới hạn đó một lần rồi, cho EP-19.

**Nếu phải chốt một con số gửi khách**, tôi dùng LAB-1 gộp 1.059,1 MD làm mốc và coi 916 MD của
LAB-5 là **giới hạn dưới** — phần việc nhìn thấy được từ cấu trúc backlog. Khoảng 143 MD chênh lệch
là phần công việc có thật nhưng không hiện ra trong cấu trúc issue, và nó phải được cộng lại bằng
phán đoán, không bằng phép nhân.

### Chỗ đáng ngờ nhất trong chính bản LAB-5

344/346 issue mang `evidenceStatus = INFERRED` và `confidence = medium`, vì thân issue theo khuôn mẫu
sinh tự động nên bộ chấm chủ yếu dựa vào tiêu đề và nhãn vai trò. Đây là ước lượng dựa trên **cấu
trúc** backlog, chưa phải dựa trên mô tả hành vi chi tiết. Muốn chắc hơn thì phải viết thân issue dày
lên rồi chấm lại — chi phí đó chưa bỏ ra ở bài này.

**Hệ số 4 giờ/SWP là lựa chọn của tôi.** Neo ở 3 giờ thì tổng ra 687 MD; neo ở 5 giờ thì ra 1.145 MD.
Cái cố định là *hình dạng* bảng — tỷ lệ giữa các epic — chứ không phải *độ lớn* tuyệt đối. Chỗ đáng
tin hơn cả là nơi hai bản **lệch** nhau có nguyên nhân gọi được tên, như ba epic ở trên.
