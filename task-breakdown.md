# task-breakdown — Chia việc từ thiết kế LAB-4 thành backlog

## 1. Nguyên tắc chia task

Backlog được chia theo 10 nguyên tắc. Tám nguyên tắc đầu là chuẩn chung; nguyên tắc 9 và 10 là
hai nguyên tắc tôi bổ sung cho riêng đề này, lý do ghi ngay bên cạnh.

| # | Nguyên tắc | Áp dụng cụ thể ở backlog này |
|---|---|---|
| 1 | **Deliverable-based, ở cấp issue cha** | **Issue cha** đẻ ra một chức năng chạy được đầu-cuối. **Sub-issue** là phần đóng góp của một vai trò vào chức năng đó — tự nó chưa phải thứ người dùng xem được. Không có issue kiểu "nghiên cứu thêm" ở bất kỳ cấp nào |
| 2 | **Lát ngang theo vai trò, phụ thuộc được khai báo** | Backlog chia **ngang theo tầng** (BE/FE/Native/QA) để giao việc đúng người trong đội offshore 8 vai trò. Đây **không** phải lát dọc, nên sub-issue **không độc lập với nhau**: FE chờ hợp đồng API của BE, QA chờ cả hai. Đổi lại phải quản lý phụ thuộc tường minh — xem §4 |
| 3 | **Ước lượng được** | Mọi issue lá có **SWP** (chấm bằng `tkm:estimate-swp`, đã qua người kiểm) và **Giờ ước lượng** trên Project. MD của LAB-1 giữ trong thân issue làm **đối chiếu lịch sử**, không dùng để chấm — xem [`estimate.md`](./estimate.md) §2 |
| 4 | **Đủ nhỏ** | **Cap 3 MD/issue lá.** 3 MD = 3 ngày công của một người, tức **60% sprint 1 tuần** (5 ngày làm việc) — còn đệm cho việc phát sinh và cho người làm song song nhiều việc. Quá 3 MD thì tách cả ô vai trò thành `phần 1/N … N/N` với các phần đều nhau. **Ngoại lệ:** việc đóng khung bởi lịch (EP-19 quản trị) không áp cap — xem ghi chú dưới bảng |
| 5 | **Không chồng lấn** | Sheet Functions (code tính năng) và sheet Project (khung, hạ tầng, kiểm thử, chuyển đổi) không giao nhau — đã đối chiếu từng dòng |
| 6 | **Có định nghĩa xong, riêng cho từng chức năng** | 63 issue chức năng mang DoD viết từ chính file thiết kế: dẫn tên field, mã lỗi, quy tắc nghiệp vụ cụ thể. **290 dòng DoD, không dòng nào trùng dòng nào.** Issue hạ tầng/quy trình dùng DoD theo vai trò vì bản chất công việc là lặp lại |
| 7 | **Gom theo nhóm chức năng** | 13 epic đầu bám đúng `FEA-01..13` của feature list LAB-1 |
| 8 | **Trackable** | Mỗi issue có `Status`, `SWP`, `Giờ ước lượng` trên GitHub Project; `Iteration` xếp cho **146 issue lá của 12 tuần đầu** (27 % backlog), phần còn lại giữ ở mức epic cho tới khi tới gần |
| 9 | **Truy vết ngược tới tài liệu đích danh** *(bổ sung)* | Mỗi issue chức năng trỏ thẳng tới **file thiết kế cụ thể** — `SCR_19_SPEC.md`, `INC_CALC_TECH.md`, `INCENTIVE_DB.md` — chứ không chỉ tên thư mục. Dev mở issue là biết đọc file nào. Lý do: break từ thư mục thì vẫn phải đoán trong 5 màn của nhóm xem màn nào là của mình |
| 10 | **Tách riêng ràng buộc nghiệp vụ đặc thù** *(bổ sung)* | Issue chạm vào quy tắc đặc thù Nhật mang nhãn `kc-*` và nhắc lại quy tắc ngay trong thân issue. Lý do: đây đúng là nhóm lỗi mà LAB-2 bắt được nhiều nhất — dev đọc issue mà không thấy quy tắc thì sẽ áp khuôn phổ thông |

**Độ hạt — dừng ở đâu:** chia tới mức *một vai trò · một phần việc · ≤ 3 MD*. Không chia nhỏ hơn,
vì dưới mức đó chi phí quản lý issue vượt giá trị theo dõi.

**Vì sao 3 MD chứ không phải 4.** Bản đầu đặt cap **4 MD** với lý do "4 MD ≈ 3 ngày, gọn trong nửa sprint".
Phép tính đó **sai**: 4 MD là 4 ngày công của một người, tức 80% của sprint 1 tuần, không phải nửa.
Hệ quả thấy ngay ở Sprint 1 giả lập — 4 trên 7 issue cỡ 4 MD nên burndown nằm ngang suốt hai ngày đầu,
không có gì đóng được sớm (xem [`progress-report.md`](./progress-report.md) §3). Cap hạ xuống **3 MD**
để một issue luôn chiếm dưới hai phần ba sprint, và backlog được tách lại theo mức đó: **66 issue lá
mới**, không issue giao hàng nào còn vượt 3 MD.

**Khi nào tách issue con:** issue cha có **từ 2 vai trò trở lên**, hoặc **một vai trò nhưng > 3 MD**.
Chức năng chỉ có 1 vai trò và ≤ 3 MD thì issue cha chính là issue lá — không đẻ issue con rỗng nghĩa
(sau khi hạ cap còn 2 trường hợp như vậy).

**Ngoại lệ có chủ ý — việc đóng khung bởi lịch.** 20 issue của `EP-19` (PM 14 MD/tháng, BrSE 10 MD/tháng
× 10 tháng) **không** áp cap. Chia "PM quản trị dự án tháng 3" thành 5 phần 2,8 MD không tạo ra 5 thứ
giao được — việc đó bị đóng khung bởi **thời gian**, không bởi kích thước. Đây cùng một lập luận với
quy tắc B khi quy SWP ra giờ ([`estimate.md`](./estimate.md) §2).

**Ba cấp trên Project:**

```
Epic      (19)   nhãn `epic`      — SWP = tổng issue con, không chấm trực tiếp
 └ Issue  (108)  nhãn `issue`     — một chức năng, gắn với tài liệu thiết kế LAB-4 đích danh
    └ Sub (408)  nhãn `sub-issue` — một vai trò, ≤ 3 MD
```

---

## 2. Spec → issue

| Spec (LAB-4) | Epic | Issue / sub-issue | Phần spec chưa thành issue và vì sao |
|---|---|---|---|
| `specs/party-management/` | [EP-01 #1](https://github.com/oNguyenVanManh/product-a-backlog/issues/1) Quản lý bên tham gia và tư cách giao dịch | 6 issue (FNC-001…FNC-006) + 15 sub | — |
| `specs/authentication/` | [EP-02 #2](https://github.com/oNguyenVanManh/product-a-backlog/issues/2) Xác thực và phân quyền | 7 issue (FNC-007…FNC-013) + 20 sub | — |
| `specs/lot-intake/` | [EP-03 #3](https://github.com/oNguyenVanManh/product-a-backlog/issues/3) Tiếp nhận lô và thẩm định | 4 issue (FNC-014…FNC-017) + 15 sub | — |
| `specs/trading/` | [EP-04 #4](https://github.com/oNguyenVanManh/product-a-backlog/issues/4) Giao dịch thỏa thuận và đấu giá | 5 issue (FNC-018…FNC-022) + 14 sub | — |
| `specs/delivery/` | [EP-05 #5](https://github.com/oNguyenVanManh/product-a-backlog/issues/5) Theo dõi giao hàng | 6 issue (FNC-023…FNC-028) + 23 sub | — |
| `specs/settlement/` | [EP-06 #6](https://github.com/oNguyenVanManh/product-a-backlog/issues/6) Đối soát, chốt sổ và điều chỉnh | 6 issue (FNC-029…FNC-034) + 20 sub | — |
| `specs/incentive/` | [EP-07 #7](https://github.com/oNguyenVanManh/product-a-backlog/issues/7) Tiền khuyến khích thanh toán đúng hạn | 5 issue (FNC-035…FNC-039) + 17 sub | — |
| `specs/rule-management/` | [EP-08 #8](https://github.com/oNguyenVanManh/product-a-backlog/issues/8) Quản lý quy định và biểu suất | 4 issue (FNC-040…FNC-043) + 14 sub | — |
| `specs/reporting/` | [EP-09 #9](https://github.com/oNguyenVanManh/product-a-backlog/issues/9) Báo cáo và xuất dữ liệu | 4 issue (FNC-044…FNC-047) + 9 sub | — |
| `specs/audit/` | [EP-10 #10](https://github.com/oNguyenVanManh/product-a-backlog/issues/10) Kiểm toán và lưu trữ | 4 issue (FNC-048…FNC-051) + 9 sub | — |
| `specs/notification/` | [EP-11 #11](https://github.com/oNguyenVanManh/product-a-backlog/issues/11) Thông báo | 4 issue (FNC-052…FNC-055) + 11 sub | — |
| `specs/accounting-interface/` | [EP-12 #12](https://github.com/oNguyenVanManh/product-a-backlog/issues/12) Liên kết hệ thống kế toán | 3 issue (FNC-056…FNC-058) + 7 sub | — |
| `specs/master-data/` | [EP-13 #13](https://github.com/oNguyenVanManh/product-a-backlog/issues/13) Danh mục nền và đồng bộ offline | 5 issue (FNC-059…FNC-063) + 14 sub | `specs/_common/error-codes.md` và `log-convention.md` không thành issue riêng — là quy ước, được thực thi trong từng issue |
| *(xuyên suốt, không gắn thư mục spec)* | [EP-14 #14](https://github.com/oNguyenVanManh/product-a-backlog/issues/14) Yêu cầu và thiết kế xuyên suốt | 8 issue (PRJ-01…PRJ-13) + 24 sub | — |
| *(xuyên suốt, không gắn thư mục spec)* | [EP-15 #15](https://github.com/oNguyenVanManh/product-a-backlog/issues/15) Nền tảng ứng dụng và hạ tầng | 13 issue (PRJ-04…PRJ-32) + 24 sub | — |
| *(xuyên suốt, không gắn thư mục spec)* | [EP-16 #16](https://github.com/oNguyenVanManh/product-a-backlog/issues/16) Kiểm thử và chất lượng | 12 issue (PRJ-21…PRJ-33) + 47 sub | `specs/_templates/` không thành issue: là khuôn mẫu tài liệu, không phải việc |
| *(xuyên suốt, không gắn thư mục spec)* | [EP-17 #17](https://github.com/oNguyenVanManh/product-a-backlog/issues/17) Chuyển đổi dữ liệu | 5 issue (PRJ-34…PRJ-38) + 14 sub | — |
| *(xuyên suốt, không gắn thư mục spec)* | [EP-18 #18](https://github.com/oNguyenVanManh/product-a-backlog/issues/18) UAT, phát hành và bàn giao | 7 issue (PRJ-39…PRJ-45) + 25 sub | — |
| *(xuyên suốt, không gắn thư mục spec)* | [EP-19 #19](https://github.com/oNguyenVanManh/product-a-backlog/issues/19) Quản trị dự án và cầu nối nghiệp vụ | 2 issue (PRJ-46…PRJ-47) + 20 sub | Không có spec — là công quản trị trải đều 10 tháng |

**Mười sáu tài liệu LAB-4 cố ý không thành issue** — ghi ra đây vì đó chính là câu hỏi cột cuối đặt:

| Tài liệu | Số file | Vì sao không thành issue |
|---|--:|---|
| `_extra/decisions/ADR-*.md` | 9 | Là **quyết định đã chốt**, không phải việc phải làm. Chúng ràng buộc cách làm của issue khác (ví dụ ADR-002 chỉ-ghi-thêm chi phối toàn bộ EP-04 và EP-06), và được nhắc lại trong thân issue liên quan |
| `specs/_common/` (`error-codes.md`, `api-list.md`, `log-convention.md`) | 3 | Là **quy ước dùng chung**, được thực thi bên trong từng issue chứ không làm riêng. Mã lỗi `M_xx` xuất hiện trực tiếp trong DoD của các issue dùng chúng |
| `requirements/REQ-00*.md` | 4 | Là **tài liệu yêu cầu đầu vào**, sản phẩm của pha Requirement chứ không phải việc của pha sau. Việc viết chúng nằm ở `PRJ-01`…`PRJ-03` thuộc [EP-14](https://github.com/oNguyenVanManh/product-a-backlog/issues/14) |

Nếu khách yêu cầu cập nhật một ADR giữa dự án thì đó là **thay đổi phạm vi**, phải mở issue mới và
khai ở [`PREMISE.md`](./PREMISE.md) — không nằm trong backlog hiện tại.

**Tổng:** 19 epic · 110 issue · 408 sub-issue = **537 issue trên GitHub**, phủ **1.059,1 MD gộp / 912 MD ròng** của estimate LAB-1.

---

## 3. Hạng mục chịu ràng buộc nghiệp vụ đặc thù

Tách riêng, không gộp vào issue chung, vì đây là nhóm dễ làm sai nhất khi dev áp kiến thức phổ thông
lên spec cụ thể. Mỗi issue dưới đây mang nhãn tương ứng và nhắc lại quy tắc ngay trong thân issue.

| Ràng buộc | Nhãn | Issue | Vì sao tách riêng |
|---|---|---|---|
| 完納奨励金 — thưởng thanh toán đúng hạn | `kc-incentive` | [EP-07 #7](https://github.com/oNguyenVanManh/product-a-backlog/issues/7) — **23 issue** | Tỷ lệ tra theo **ngày nghiệp vụ của giao dịch**, không lấy bản ghi mới nhất; điều chỉnh sau chốt kỳ phải là bút toán mới, không ghi đè. Gộp vào issue tính toán chung thì dev gần như chắc chắn sẽ viết `ORDER BY effective_from DESC LIMIT 1`. |
| 相対取引 chiếm phần lớn giá trị | `kc-negotiated` | [EP-04 #4](https://github.com/oNguyenVanManh/product-a-backlog/issues/4) — **25 issue** | Tên đề là "sàn đấu giá" nhưng ~90% giá trị đến từ thoả thuận trực tiếp. Tách riêng để không ai dựng せり làm luồng mặc định rồi gắn 相対 vào sau. |
| Hai cấp quyền pháp lý 許可 / 承認 | `kc-two-tier` | [EP-01 #1](https://github.com/oNguyenVanManh/product-a-backlog/issues/1) — **27 issue** | 許可 (xét duyệt có điều kiện → 仲卸) và 承認 (thủ tục nhẹ hơn → 売買参加者) khác nhau về bản chất pháp lý. Gộp thành một trường trạng thái là sai luật, không chỉ sai thiết kế. 買出人 không có tư cách giao dịch trực tiếp. |
| Giữ người trong vòng lặp (CAP-HUMAN-01) | `kc-human` | [EP-03 #3](https://github.com/oNguyenVanManh/product-a-backlog/issues/3) — **24 issue** | Thẩm định độ tươi bằng mắt và ký hiệu viết tay **nằm ngoài phạm vi** (SCOPE-OUT-01/02). Tách riêng để không ai tự ý thêm chấm điểm tự động hay OCR. |
| 業務日 02:00–10:00 JST và khoá sổ | `kc-business-day` | [EP-06 #6](https://github.com/oNguyenVanManh/product-a-backlog/issues/6), [EP-15 #15](https://github.com/oNguyenVanManh/product-a-backlog/issues/15) — **75 issue** | Ngày nghiệp vụ khác ngày lịch; khoá ngày do **trigger CSDL** chặn chứ không phải tầng ứng dụng. Chặn ở ứng dụng thì job nền và công cụ nạp dữ liệu đi vòng qua được. |

Tổng cộng **174 issue** mang nhãn ràng buộc đặc thù (6 epic + 39 issue cha + 129 sub-issue).
Nhãn được gắn tới tận **issue lá**, không chỉ ở issue cha — dev nhận một sub-issue BE lẻ vẫn thấy
ngay quy tắc đặc thù trong thân issue và trên nhãn, không phải mở issue cha mới biết.


---

## 4. Phụ thuộc và thứ tự làm

Backlog chia **ngang theo vai trò** (nguyên tắc 2), nên phụ thuộc là chuyện mặc định chứ không phải
ngoại lệ. Bỏ qua mục này thì người lập sprint không trả lời được câu hỏi cơ bản nhất: *issue này đã
sẵn sàng để làm chưa, hay đang chờ cái khác?*

### 4.1 Quy ước thứ tự trong một chức năng

Mỗi chức năng có một chuỗi cố định. 63 chức năng là 63 chuỗi chạy song song:

```
BE  ──▶  FE / Native  ──▶  QA
 │            │
 └── hợp đồng API      └── màn hình chạy được
```

| Quan hệ | Lý do | Được phép chồng lấn không |
|---|---|---|
| FE/Native **chờ** BE | Cần hợp đồng API (đường dẫn, tham số, mã lỗi) | Có — FE bắt đầu được khi hợp đồng API đã chốt, không cần chờ BE code xong |
| QA **chờ** cả BE và FE/Native | Không test được luồng chưa chạy | Không — QA viết ca test sớm được, nhưng issue QA chỉ đóng khi chạy thật |
| Design **chờ** BrSE | Wireframe cần luồng nghiệp vụ đã xác nhận | Không — đã thấy ở Sprint 1: [#323](https://github.com/oNguyenVanManh/product-a-backlog/issues/323) bị chặn bởi [#319](https://github.com/oNguyenVanManh/product-a-backlog/issues/319) |

### 4.2 Ghi phụ thuộc ở đâu

GitHub Project không có trường phụ thuộc, nên quy ước là **ghi trong thân issue**:

```
**Chờ:** #237, #238
```

Mọi sub-issue FE/Native/QA của một chức năng đều mang dòng này, trỏ tới sub-issue cùng chức năng mà
nó phụ thuộc. Người lập sprint lọc nhãn `role:qa`, mở issue, thấy ngay nó chờ ai.

**Giới hạn đã biết:** đây là quy ước thủ công, GitHub không tự chặn việc đóng issue sai thứ tự và
không vẽ được sơ đồ phụ thuộc. Làm dự án thật nên dùng tracker có quan hệ *blocks / is blocked by*
(Jira, Linear) hoặc trường tự tạo trên Project. Ghi ra đây để người đọc không tưởng là đã có cơ chế
cưỡng chế.

### 4.3 Ưu tiên

Mỗi issue chức năng mang nhãn **`P0`** hoặc **`P1`** lấy từ cột `Ưu tiên` của function list LAB-1:

| Nhãn | Nghĩa | Khi trễ tiến độ |
|---|---|---|
| `P0` | Chức năng lõi — thiếu nó thì chợ không vận hành được bằng hệ thống mới | Không được cắt. Nếu trễ thì lùi mốc, không giảm phạm vi |
| `P1` | Cần có, nhưng chợ vẫn chạy được tạm thời bằng cách cũ | Là nơi cắt trước khi lùi mốc |

Không có ưu tiên thì khi trễ — mà [`progress-report.md`](./progress-report.md) đã dự báo trễ ngay từ
Sprint 1 — không có cơ sở nào để quyết bỏ cái gì. Thông tin này đã có sẵn ở LAB-1, chỉ việc đưa lên board.

---

## 5. Chỗ hở hoặc mâu thuẫn của spec LAB-4 phát hiện khi break

Tách làm hai phần, vì hai loại có giá trị khác nhau: phần 4.1 là chỗ **đã biết trước** khi break
(giảng viên chỉ ra ở feedback LAB-4), phần 4.2 là chỗ **chỉ lộ ra trong lúc chia việc và viết điều
kiện nghiệm thu cho từng chức năng**.

### 5.1 Đã biết từ feedback LAB-4, sửa trước khi break

| Spec | Chỗ hở / mâu thuẫn | Xử lý |
|---|---|---|
| `specs/trading/` — phiên đấu giá | Không nói kết quả phiên được xác nhận ra sao trước khi thành giao dịch chính thức. Với sổ chỉ-ghi-thêm thì đây là chỗ hở chặn. | **Đã sửa thiết kế** → [`PREMISE.md`](./PREMISE.md) §1 dòng ADR-009 |
| `INCENTIVE_DB.md` | Cho phép tính lại và ghi đè dòng thưởng đã chốt kỳ — mâu thuẫn với ADR-002 (chỉ-ghi-thêm). | **Đã sửa thiết kế** → [`PREMISE.md`](./PREMISE.md) §1 |
| `PAYMENT_STATUS_DB.md` | Thiếu `paid_date`, nhưng toàn bộ 完納奨励金 dựa trên "trả đúng hạn hay không". | **Đã sửa thiết kế** → [`PREMISE.md`](./PREMISE.md) §1 |
| `APP_USER_DB.md` vs `architecture.md` | Thiết kế nói 6 vai trò ứng dụng, CHECK trong CSDL chỉ liệt kê 4. | **Đã sửa thiết kế** → [`PREMISE.md`](./PREMISE.md) §1 |
| 20 file `technical-design/` | Chỉ có tên chức năng, không có cơ chế kích hoạt / quy tắc / xử lý lỗi. | **Đã sửa thiết kế** → [`PREMISE.md`](./PREMISE.md) §1 |
| `SCR_12_SPEC.md` | `exception_reason` đánh dấu bắt buộc luôn, mâu thuẫn với luồng đối soát thường. | **Đã sửa thiết kế** → [`PREMISE.md`](./PREMISE.md) §1 |
| `SCR_20_SPEC.md` | Không mô tả nhánh lỗi nào. | **Đã sửa thiết kế** → [`PREMISE.md`](./PREMISE.md) §1 (thêm 4 nhánh) |

### 5.2 Phát hiện khi break — trong lúc viết điều kiện nghiệm thu cho từng chức năng

Những chỗ dưới đây **không ai chỉ ra trước**. Chúng lộ ra vì mỗi chức năng phải được viết thành điều
kiện kiểm chứng được, và lúc đó mới thấy spec không trả lời được câu hỏi "đúng thì trông thế nào".

| Spec | Chỗ hở / mâu thuẫn | Xử lý |
|---|---|---|
| `SCR_20_SPEC.md` mục 6 vs bảng lỗi | **Tự mâu thuẫn:** mục 6 ghi kết quả tính thưởng "ghi đè được bằng upsert", bảng lỗi cùng file lại ghi "không ghi đè, sinh dòng chênh lệch". Hai câu loại trừ nhau, và đây đúng là quy tắc lõi của 完納奨励金. | **Tạo issue làm rõ** — ảnh hưởng [#55](https://github.com/oNguyenVanManh/product-a-backlog/issues/55) và [#58](https://github.com/oNguyenVanManh/product-a-backlog/issues/58) |
| `FNC_037_TECH.md`, `FNC_038_TECH.md` vs ADR | **Giá trị `entry_type` không thống nhất:** ràng buộc nghiệp vụ dùng `'adjust'`, hai file technical-design dùng `'adjustment'`. Một trong hai sẽ làm vỡ ràng buộc UNIQUE khi chạy thật. | **Tạo issue làm rõ** — ảnh hưởng [#56](https://github.com/oNguyenVanManh/product-a-backlog/issues/56), [#57](https://github.com/oNguyenVanManh/product-a-backlog/issues/57) |
| `SCR_30_SPEC.md` mục 4.2 vs ma trận quyền | **Tự mâu thuẫn:** mục 4.2 ghi màn "chỉ đọc", nhưng ma trận quyền cùng file cho `ROLE_SYS_ADMIN` quyền sửa. | **Tạo issue làm rõ** — ảnh hưởng [#79](https://github.com/oNguyenVanManh/product-a-backlog/issues/79) |
| `SCR_09_SPEC.md` | Mô tả là **màn chỉ đọc** nhưng lại gọi `POST /api/trades`. Không rõ màn này ghi hay không ghi. | **Tạo issue làm rõ** — ảnh hưởng [#40](https://github.com/oNguyenVanManh/product-a-backlog/issues/40) |
| `specs/settlement/` — toàn nhóm | Ràng buộc 業務日 **02:00–10:00 JST** và 休市日 được nêu ở `architecture.md` nhưng **không file thiết kế nào của nhóm đối soát nhắc lại**. Dev đọc spec nhóm này sẽ mặc định ngày lịch. | **Để mở** — đã ghi vào DoD của [#48](https://github.com/oNguyenVanManh/product-a-backlog/issues/48), [#49](https://github.com/oNguyenVanManh/product-a-backlog/issues/49) dưới dạng điều kiện đề xuất, chờ khách xác nhận mốc giờ |
| `RATE_VERSION_DB.md` | Thiếu cột `recorded_at`. Không có nó thì không phân biệt được "biểu suất có hiệu lực từ ngày nào" với "ta biết về nó từ lúc nào" — tức mất một nửa của mô hình lưỡng thời gian đã chốt ở ADR. | **Để mở** — ghi nợ N-03, ảnh hưởng [#62](https://github.com/oNguyenVanManh/product-a-backlog/issues/62) |
| `LOT-*_API.md` | Ràng buộc CHECK `remaining_kg >= 0` được spec gọi là "hiện còn thiếu". Chặn bán quá số lượng mới có ở tầng ứng dụng. | **Để mở** — ghi nợ R-03, ảnh hưởng [#35](https://github.com/oNguyenVanManh/product-a-backlog/issues/35) |
| `TRD-*_API.md` | Quy tắc "một dòng gốc chỉ được đảo một lần" mới kiểm ở tầng API, **chưa có ràng buộc UNIQUE** ở CSDL. Hai request đồng thời sẽ tạo hai bút toán đảo. | **Để mở** — ghi nợ R-06, ảnh hưởng [#39](https://github.com/oNguyenVanManh/product-a-backlog/issues/39) |
| `SCR_14_SPEC.md` | Chỉ mô tả đối soát **tiền** theo ngày, không có quy tắc so khớp **số lượng giao** với số quyết toán — nhưng đó chính là việc mà chức năng đối chiếu giao hàng phải làm. | **Để mở** — `REQ-001` cũng đánh dấu chức năng này là "một phần", ảnh hưởng [#46](https://github.com/oNguyenVanManh/product-a-backlog/issues/46) |
| `USR-2_API.md` | Phần mô tả bị **lẫn mã nguồn** vào văn bản đặc tả. | **Để mở** — lỗi trình bày, ảnh hưởng [#30](https://github.com/oNguyenVanManh/product-a-backlog/issues/30) |
| `SCR_02_SPEC.md` | Có nút Bật/Tắt tài khoản nhưng **không có thao tác tạo tài khoản hay đổi vai trò**, trong khi chức năng quản lý tài khoản yêu cầu cả hai. | **Để mở** — ảnh hưởng [#30](https://github.com/oNguyenVanManh/product-a-backlog/issues/30) |
| RFP — hạn mức dữ liệu chuyển đổi | RFP không nói rõ **bao nhiêu năm** dữ liệu lịch sử phải chuyển. | **Giả định** → [`PREMISE.md`](./PREMISE.md) §2, dòng "Chuyển đổi 3 năm dữ liệu lịch sử" |
| `specs/notification/` | Spec nói gửi thông báo nhưng không chốt kênh (email / SMS / in-app). | **Để mở** — câu hỏi đã nằm trong Q&A sheet LAB-1, chưa có đáp án từ khách |

**Cách phát hiện:** 54/63 chức năng có ít nhất một chỗ spec không nói đủ để viết điều kiện nghiệm thu.
Mỗi issue như vậy mang một khối cảnh báo ngay trong thân, nêu rõ phần DoD nào là **điều kiện đề xuất**
chứ không phải điều kiện đã chốt với khách. Dev đọc issue biết ngay chỗ nào phải hỏi lại trước khi làm.
