# task-breakdown — Chia việc từ thiết kế LAB-4 thành backlog

## 1. Nguyên tắc chia task

Backlog được chia theo 10 nguyên tắc. Tám nguyên tắc đầu là chuẩn chung; nguyên tắc 9 và 10 là
hai nguyên tắc tôi bổ sung cho riêng đề này, lý do ghi ngay bên cạnh.

| # | Nguyên tắc | Áp dụng cụ thể ở backlog này |
|---|---|---|
| 1 | **Deliverable-based** — mỗi issue đẻ ra một thứ xem được | Issue lá luôn là một vai trò làm xong một phần việc cụ thể, không có issue kiểu "nghiên cứu thêm" |
| 2 | **Độc lập** — làm được mà không chờ issue cùng cấp | Chia theo vai trò (BE/FE/Native/QA) nên BE và FE chạy song song trên cùng một chức năng |
| 3 | **Ước lượng được** | Mọi issue lá đều có MD lấy từ sheet effort LAB-1, không có issue "chưa biết bao lâu" |
| 4 | **Đủ nhỏ** | **Cap 4 MD/issue lá.** Quá 4 MD thì tách tiếp (`phần 1/3`, `2/3`…). 4 MD ≈ 3 ngày, gọn trong nửa sprint 1 tuần |
| 5 | **Không chồng lấn** | Sheet Functions (code tính năng) và sheet Project (khung, hạ tầng, kiểm thử, chuyển đổi) không giao nhau — đã đối chiếu từng dòng |
| 6 | **Có định nghĩa xong** | Mỗi issue mang checklist "Định nghĩa xong" theo vai trò, không dùng câu chung chung |
| 7 | **Gom theo nhóm chức năng** | 13 epic đầu bám đúng `FEA-01..13` của feature list LAB-1 |
| 8 | **Trackable** | Mỗi issue có trường Status, Iteration, SWP, Giờ ước lượng trên GitHub Project |
| 9 | **Truy vết ngược được** *(bổ sung)* | Mỗi issue mang bảng Truy vết: epic → file spec LAB-4 → màn hình → ID yêu cầu RFP → user story. Lý do: LAB-2 cho thấy gói nào không truy vết được thì người ngoài không kiểm chứng được phạm vi |
| 10 | **Tách riêng ràng buộc nghiệp vụ đặc thù** *(bổ sung)* | Issue chạm vào quy tắc đặc thù Nhật mang nhãn `kc-*` và nhắc lại quy tắc ngay trong thân issue. Lý do: đây đúng là nhóm lỗi mà LAB-2 bắt được nhiều nhất — dev đọc issue mà không thấy quy tắc thì sẽ áp khuôn phổ thông |

**Độ hạt — dừng ở đâu:** chia tới mức *một vai trò · một phần việc · ≤ 4 MD*. Không chia nhỏ hơn,
vì dưới mức đó chi phí quản lý issue vượt giá trị theo dõi.

**Khi nào tách issue con:** issue cha có **từ 2 vai trò trở lên**, hoặc **một vai trò nhưng > 4 MD**.
Chức năng chỉ có 1 vai trò và ≤ 4 MD thì issue cha chính là issue lá — không đẻ issue con rỗng nghĩa
(có 4 trường hợp như vậy).

**Ba cấp trên Project:**

```
Epic      (19)   nhãn `epic`      — SWP = tổng issue con, không chấm trực tiếp
 └ Issue  (110)  nhãn `issue`     — một chức năng / hạng mục LAB-1
    └ Sub (342)  nhãn `sub-issue` — một vai trò, ≤ 4 MD
```

---

## 2. Spec → issue

| Spec (LAB-4) | Epic | Issue / sub-issue | Phần spec chưa thành issue và vì sao |
|---|---|---|---|
| `specs/party-management/` | `[EP-01 #1](https://github.com/oNguyenVanManh/product-a-backlog/issues/1)` Quản lý bên tham gia và tư cách giao dịch | 6 issue (FNC-001…FNC-006) + 15 sub | — |
| `specs/authentication/` | `[EP-02 #2](https://github.com/oNguyenVanManh/product-a-backlog/issues/2)` Xác thực và phân quyền | 7 issue (FNC-007…FNC-013) + 20 sub | — |
| `specs/lot-intake/` | `[EP-03 #3](https://github.com/oNguyenVanManh/product-a-backlog/issues/3)` Tiếp nhận lô và thẩm định | 4 issue (FNC-014…FNC-017) + 15 sub | — |
| `specs/trading/` | `[EP-04 #4](https://github.com/oNguyenVanManh/product-a-backlog/issues/4)` Giao dịch thỏa thuận và đấu giá | 5 issue (FNC-018…FNC-022) + 14 sub | — |
| `specs/delivery/` | `[EP-05 #5](https://github.com/oNguyenVanManh/product-a-backlog/issues/5)` Theo dõi giao hàng | 6 issue (FNC-023…FNC-028) + 23 sub | — |
| `specs/settlement/` | `[EP-06 #6](https://github.com/oNguyenVanManh/product-a-backlog/issues/6)` Đối soát, chốt sổ và điều chỉnh | 6 issue (FNC-029…FNC-034) + 20 sub | — |
| `specs/incentive/` | `[EP-07 #7](https://github.com/oNguyenVanManh/product-a-backlog/issues/7)` Tiền khuyến khích thanh toán đúng hạn | 5 issue (FNC-035…FNC-039) + 17 sub | — |
| `specs/rule-management/` | `[EP-08 #8](https://github.com/oNguyenVanManh/product-a-backlog/issues/8)` Quản lý quy định và biểu suất | 4 issue (FNC-040…FNC-043) + 14 sub | — |
| `specs/reporting/` | `[EP-09 #9](https://github.com/oNguyenVanManh/product-a-backlog/issues/9)` Báo cáo và xuất dữ liệu | 4 issue (FNC-044…FNC-047) + 9 sub | — |
| `specs/audit/` | `[EP-10 #10](https://github.com/oNguyenVanManh/product-a-backlog/issues/10)` Kiểm toán và lưu trữ | 4 issue (FNC-048…FNC-051) + 9 sub | — |
| `specs/notification/` | `[EP-11 #11](https://github.com/oNguyenVanManh/product-a-backlog/issues/11)` Thông báo | 4 issue (FNC-052…FNC-055) + 11 sub | — |
| `specs/accounting-interface/` | `[EP-12 #12](https://github.com/oNguyenVanManh/product-a-backlog/issues/12)` Liên kết hệ thống kế toán | 3 issue (FNC-056…FNC-058) + 7 sub | — |
| `specs/master-data/` | `[EP-13 #13](https://github.com/oNguyenVanManh/product-a-backlog/issues/13)` Danh mục nền và đồng bộ offline | 5 issue (FNC-059…FNC-063) + 14 sub | `specs/_common/error-codes.md` và `log-convention.md` không thành issue riêng — là quy ước, được thực thi trong từng issue |
| *(xuyên suốt, không gắn thư mục spec)* | `[EP-14 #14](https://github.com/oNguyenVanManh/product-a-backlog/issues/14)` Yêu cầu và thiết kế xuyên suốt | 8 issue (PRJ-01…PRJ-13) + 24 sub | — |
| *(xuyên suốt, không gắn thư mục spec)* | `[EP-15 #15](https://github.com/oNguyenVanManh/product-a-backlog/issues/15)` Nền tảng ứng dụng và hạ tầng | 13 issue (PRJ-04…PRJ-32) + 24 sub | — |
| *(xuyên suốt, không gắn thư mục spec)* | `[EP-16 #16](https://github.com/oNguyenVanManh/product-a-backlog/issues/16)` Kiểm thử và chất lượng | 12 issue (PRJ-21…PRJ-33) + 47 sub | `specs/_templates/` không thành issue: là khuôn mẫu tài liệu, không phải việc |
| *(xuyên suốt, không gắn thư mục spec)* | `[EP-17 #17](https://github.com/oNguyenVanManh/product-a-backlog/issues/17)` Chuyển đổi dữ liệu | 5 issue (PRJ-34…PRJ-38) + 14 sub | — |
| *(xuyên suốt, không gắn thư mục spec)* | `[EP-18 #18](https://github.com/oNguyenVanManh/product-a-backlog/issues/18)` UAT, phát hành và bàn giao | 7 issue (PRJ-39…PRJ-45) + 25 sub | — |
| *(xuyên suốt, không gắn thư mục spec)* | `[EP-19 #19](https://github.com/oNguyenVanManh/product-a-backlog/issues/19)` Quản trị dự án và cầu nối nghiệp vụ | 2 issue (PRJ-46…PRJ-47) + 20 sub | Không có spec — là công quản trị trải đều 10 tháng |

**Tổng:** 19 epic · 110 issue · 342 sub-issue = **471 issue trên GitHub**, phủ **1.059,1 MD gộp / 912 MD ròng** của estimate LAB-1.

---

## 3. Hạng mục chịu ràng buộc nghiệp vụ đặc thù

Tách riêng, không gộp vào issue chung, vì đây là nhóm dễ làm sai nhất khi dev áp kiến thức phổ thông
lên spec cụ thể. Mỗi issue dưới đây mang nhãn tương ứng và nhắc lại quy tắc ngay trong thân issue.

| Ràng buộc | Nhãn | Issue | Vì sao tách riêng |
|---|---|---|---|
| 完納奨励金 — thưởng thanh toán đúng hạn | `kc-incentive` | [EP-07 #7](https://github.com/oNguyenVanManh/product-a-backlog/issues/7) — **23 issue** | Tỷ lệ tra theo **ngày nghiệp vụ của giao dịch**, không lấy bản ghi mới nhất; điều chỉnh sau chốt kỳ phải là bút toán mới, không ghi đè. Gộp vào issue tính toán chung thì dev gần như chắc chắn sẽ viết `ORDER BY effective_from DESC LIMIT 1`. |
| 相対取引 chiếm phần lớn giá trị | `kc-negotiated` | [EP-04 #4](https://github.com/oNguyenVanManh/product-a-backlog/issues/4) — **20 issue** | Tên đề là "sàn đấu giá" nhưng ~90% giá trị đến từ thoả thuận trực tiếp. Tách riêng để không ai dựng せり làm luồng mặc định rồi gắn 相対 vào sau. |
| Hai cấp quyền pháp lý 許可 / 承認 | `kc-two-tier` | [EP-01 #1](https://github.com/oNguyenVanManh/product-a-backlog/issues/1) — **22 issue** | 許可 (xét duyệt có điều kiện → 仲卸) và 承認 (thủ tục nhẹ hơn → 売買参加者) khác nhau về bản chất pháp lý. Gộp thành một trường trạng thái là sai luật, không chỉ sai thiết kế. 買出人 không có tư cách giao dịch trực tiếp. |
| Giữ người trong vòng lặp (CAP-HUMAN-01) | `kc-human` | [EP-03 #3](https://github.com/oNguyenVanManh/product-a-backlog/issues/3) — **20 issue** | Thẩm định độ tươi bằng mắt và ký hiệu viết tay **nằm ngoài phạm vi** (SCOPE-OUT-01/02). Tách riêng để không ai tự ý thêm chấm điểm tự động hay OCR. |
| 業務日 02:00–10:00 JST và khoá sổ | `kc-business-day` | [EP-06 #6](https://github.com/oNguyenVanManh/product-a-backlog/issues/6), [EP-15 #15](https://github.com/oNguyenVanManh/product-a-backlog/issues/15) — **65 issue** | Ngày nghiệp vụ khác ngày lịch; khoá ngày do **trigger CSDL** chặn chứ không phải tầng ứng dụng. Chặn ở ứng dụng thì job nền và công cụ nạp dữ liệu đi vòng qua được. |

Tổng cộng **150 issue** mang nhãn ràng buộc đặc thù: 6 epic + 39 issue cha + 105 sub-issue.
Nhãn được gắn tới tận **issue lá**, không chỉ ở issue cha — dev nhận một sub-issue BE lẻ vẫn thấy
ngay quy tắc đặc thù trong thân issue và trên nhãn, không phải mở issue cha mới biết.

---

## 4. Chỗ hở hoặc mâu thuẫn của spec LAB-4 phát hiện khi break

| Spec | Chỗ hở / mâu thuẫn | Xử lý |
|---|---|---|
| `specs/trading/` — phiên đấu giá | Không nói kết quả phiên được xác nhận ra sao trước khi thành giao dịch chính thức. Với sổ chỉ-ghi-thêm thì đây là chỗ hở chặn: không có mốc hợp lệ để bắt đầu ghi. | **Đã sửa thiết kế** → `PREMISE.md` §1 dòng ADR-009 |
| `INCENTIVE_DB.md` | Cho phép tính lại và ghi đè dòng thưởng đã chốt kỳ — mâu thuẫn trực tiếp với ADR-002 (chỉ-ghi-thêm). | **Đã sửa thiết kế** → `PREMISE.md` §1 dòng `INCENTIVE_DB.md` |
| `PAYMENT_STATUS_DB.md` | Thiếu `paid_date`, nhưng toàn bộ 完納奨励金 dựa trên "trả đúng hạn hay không". | **Đã sửa thiết kế** → `PREMISE.md` §1 |
| `APP_USER_DB.md` vs `architecture.md` | Thiết kế nói 6 vai trò ứng dụng, ràng buộc CHECK trong CSDL chỉ liệt kê 4. | **Đã sửa thiết kế** → `PREMISE.md` §1 |
| 20 file `technical-design/` | Chỉ có tên chức năng, không có cơ chế kích hoạt / quy tắc / xử lý lỗi. Không break được thành issue có định nghĩa xong. | **Đã sửa thiết kế** → `PREMISE.md` §1 (sinh đủ 20 file) |
| `SCR_12_SPEC.md` | `exception_reason` đánh dấu bắt buộc luôn, mâu thuẫn với luồng đối soát thường (không có ngoại lệ thì không có lý do để nhập). | **Đã sửa thiết kế** → `PREMISE.md` §1 |
| `SCR_20_SPEC.md` | Không mô tả nhánh lỗi nào. | **Đã sửa thiết kế** → `PREMISE.md` §1 (thêm 4 nhánh) |
| RFP — hạn mức dữ liệu chuyển đổi | RFP không nói rõ **bao nhiêu năm** dữ liệu lịch sử phải chuyển sang hệ thống mới. `[EP-17 #17](https://github.com/oNguyenVanManh/product-a-backlog/issues/17)` đang ước lượng theo giả định 3 năm của LAB-1. | **Giả định** → [`PREMISE.md`](./PREMISE.md) §2, dòng "Chuyển đổi 3 năm dữ liệu lịch sử" |
| `specs/notification/` | Spec nói gửi thông báo nhưng không chốt kênh (email / SMS / in-app). Ảnh hưởng tới effort `[EP-12 #12](https://github.com/oNguyenVanManh/product-a-backlog/issues/12)`. | **Để mở** — đây là câu hỏi đã nằm trong Q&A sheet LAB-1 (chưa có đáp án từ khách). Giữ ước lượng theo kênh in-app + email như LAB-1, ghi rủi ro ở `progress-report.md` |
