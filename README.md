# Product A — Backlog LAB-5

**Dự án:** Hệ thống hỗ trợ vận hành chợ bán buôn thủy sản (giả lập)
**Mã học viên:** nguyen-van-manh-c
**Đề:** **Product A** — sàn đấu giá thủy sản

---

## 1. Tổng quan

Backlog này break từ bộ thiết kế **LAB-4 nộp ngày 11/10/2026**, bản **đã sửa theo góp ý của giảng
viên** (3 nhóm A/B/C). Bản đã sửa đặt trong repo tại [`specs-revised/`](./specs-revised/) — 131 file
markdown, 93 tài liệu nghiệp vụ.

**[`PREMISE.md`](./PREMISE.md) CÓ thay đổi so với LAB-4:** 12 dòng spec thêm/sửa, 6 giả định bổ sung,
4 hướng đã chốt. Backlog bám bản đã sửa, không bám bản LAB-4 nguyên gốc.

| | |
|---|---|
| Epic | **19** (13 nhóm chức năng + 6 hạng mục xuyên suốt) |
| Issue | 110 |
| Sub-issue | 408 |
| **Tổng issue trên Project** | **537** |
| Tổng SWP (đã qua người kiểm) | **1.701** |
| Tổng giờ ước lượng | **8.524 h** = 1.065,5 MD |
| Sprint giả lập đã chạy | **Sprint 1** (02/11 – 08/11/2026), 9 issue, 29 SWP, hoàn thành 37,9 % |
| Sprint đã xếp lịch | **Sprint 2–12** (09/11/2026 – 31/01/2027), 137 issue — kế hoạch, chưa chạy |
| Iteration phủ | **146/537 issue lá** = 27 % backlog, tức 12 tuần đầu. Phần còn lại giữ ở mức epic, xếp lịch khi tới gần |

---

## 2. Link

| | |
|---|---|
| Repo | <https://github.com/oNguyenVanManh/product-a-backlog> |
| GitHub Project | <https://github.com/users/oNguyenVanManh/projects/2> |
| Báo cáo HTML của skill chấm SWP | [`reports/estimate-swp-report.html`](./reports/estimate-swp-report.html) |

Cả repo và Project đã được kiểm truy cập **không kèm thông tin đăng nhập** (yêu cầu HTTP sạch cookie):
repo, file markdown và trang Project đều trả về 200 và hiện đủ nội dung. Người review nên mở lại bằng
cửa sổ ẩn danh để tự xác nhận.

Báo cáo HTML tự chứa (1,3 MB, không gọi tài nguyên ngoài) — tải về mở bằng trình duyệt là chạy.
GitHub không render HTML trong repo, nên cần bấm **Download raw file** rồi mở.

---

## 3. Cấu trúc repo

| File / thư mục | Nội dung |
|---|---|
| [`README.md`](./README.md) | File này — tổng quan, link, cấu trúc, bảng Spec → epic |
| [`PREMISE.md`](./PREMISE.md) | Tiền đề: backlog khác bản LAB-4 đã nộp ở đâu, vì sao, ảnh hưởng tới issue nào |
| [`task-breakdown.md`](./task-breakdown.md) | 10 nguyên tắc chia task · bảng Spec → issue · hạng mục chịu ràng buộc đặc thù · chỗ hở spec phát hiện khi break |
| [`estimate.md`](./estimate.md) | Kiểm 5 issue mẫu · cách quy SWP ra giờ · tổng theo epic · so với estimate LAB-1 |
| [`progress-report.md`](./progress-report.md) | Báo cáo tiến độ Sprint 1: trạng thái, burndown, rủi ro trễ |
| [`AI-report.md`](./AI-report.md) | Cách dùng AI: skill và prompt, con người review ở đâu, chỗ AI sai và cách bắt |
| [`reports/`](./reports/) | Báo cáo HTML do skill `tkm:estimate-swp` xuất ra |
| [`assets/`](./assets/) | Biểu đồ burndown Sprint 1 (SVG) |
| [`specs-revised/`](./specs-revised/) | Bộ thiết kế LAB-4 **đã sửa** — nguồn để break task |

Không có thư mục `skills/`: bài này dùng skill có sẵn của kit (`tkm:estimate-swp`), không tự viết skill mới.

---

## 4. Spec → epic

| Spec (file LAB-4, hoặc dòng PREMISE) | Epic trên Project | Ghi chú — ràng buộc đặc thù |
|---|---|---|
| [`specs-revised/specs/party-management/`](./specs-revised/specs/party-management/) | [#1](https://github.com/oNguyenVanManh/product-a-backlog/issues/1) — Quản lý bên tham gia và tư cách giao dịch | Hai cấp quyền pháp lý 許可 (仲卸) và 承認 (売買参加者), không gộp |
| [`specs-revised/specs/authentication/`](./specs-revised/specs/authentication/) | [#2](https://github.com/oNguyenVanManh/product-a-backlog/issues/2) — Xác thực và phân quyền | — |
| [`specs-revised/specs/lot-intake/`](./specs-revised/specs/lot-intake/) | [#3](https://github.com/oNguyenVanManh/product-a-backlog/issues/3) — Tiếp nhận lô và thẩm định | Giữ người trong vòng lặp — CAP-HUMAN-01, SCOPE-OUT-01/02 |
| [`specs-revised/specs/trading/`](./specs-revised/specs/trading/) | [#4](https://github.com/oNguyenVanManh/product-a-backlog/issues/4) — Giao dịch thỏa thuận và đấu giá | 相対取引 chiếm ~90% giá trị, là luồng chính chứ không phải nhánh phụ của đấu giá |
| [`specs-revised/specs/delivery/`](./specs-revised/specs/delivery/) | [#5](https://github.com/oNguyenVanManh/product-a-backlog/issues/5) — Theo dõi giao hàng | — |
| [`specs-revised/specs/settlement/`](./specs-revised/specs/settlement/) | [#6](https://github.com/oNguyenVanManh/product-a-backlog/issues/6) — Đối soát, chốt sổ và điều chỉnh | 業務日 02:00–10:00 JST, 休市日; khoá ngày chặn bằng trigger CSDL |
| [`specs-revised/specs/incentive/`](./specs-revised/specs/incentive/) | [#7](https://github.com/oNguyenVanManh/product-a-backlog/issues/7) — Tiền khuyến khích thanh toán đúng hạn | 完納奨励金 — tra tỷ lệ theo ngày nghiệp vụ, điều chỉnh bằng bút toán mới |
| [`specs-revised/specs/rule-management/`](./specs-revised/specs/rule-management/) | [#8](https://github.com/oNguyenVanManh/product-a-backlog/issues/8) — Quản lý quy định và biểu suất | — |
| [`specs-revised/specs/reporting/`](./specs-revised/specs/reporting/) | [#9](https://github.com/oNguyenVanManh/product-a-backlog/issues/9) — Báo cáo và xuất dữ liệu | — |
| [`specs-revised/specs/audit/`](./specs-revised/specs/audit/) | [#10](https://github.com/oNguyenVanManh/product-a-backlog/issues/10) — Kiểm toán và lưu trữ | — |
| [`specs-revised/specs/notification/`](./specs-revised/specs/notification/) | [#11](https://github.com/oNguyenVanManh/product-a-backlog/issues/11) — Thông báo | — |
| [`specs-revised/specs/accounting-interface/`](./specs-revised/specs/accounting-interface/) | [#12](https://github.com/oNguyenVanManh/product-a-backlog/issues/12) — Liên kết hệ thống kế toán | — |
| [`specs-revised/specs/master-data/`](./specs-revised/specs/master-data/) | [#13](https://github.com/oNguyenVanManh/product-a-backlog/issues/13) — Danh mục nền và đồng bộ offline | — |
| *(xuyên suốt — không gắn thư mục spec)* | [#14](https://github.com/oNguyenVanManh/product-a-backlog/issues/14) — Yêu cầu và thiết kế xuyên suốt | — |
| *(xuyên suốt — không gắn thư mục spec)* | [#15](https://github.com/oNguyenVanManh/product-a-backlog/issues/15) — Nền tảng ứng dụng và hạ tầng | 業務日 02:00–10:00 JST, 休市日; khoá ngày chặn bằng trigger CSDL |
| *(xuyên suốt — không gắn thư mục spec)* | [#16](https://github.com/oNguyenVanManh/product-a-backlog/issues/16) — Kiểm thử và chất lượng | — |
| *(xuyên suốt — không gắn thư mục spec)* | [#17](https://github.com/oNguyenVanManh/product-a-backlog/issues/17) — Chuyển đổi dữ liệu | — |
| *(xuyên suốt — không gắn thư mục spec)* | [#18](https://github.com/oNguyenVanManh/product-a-backlog/issues/18) — UAT, phát hành và bàn giao | — |
| *(xuyên suốt — không gắn thư mục spec)* | [#19](https://github.com/oNguyenVanManh/product-a-backlog/issues/19) — Quản trị dự án và cầu nối nghiệp vụ | — |
| [`PREMISE.md`](./PREMISE.md) §1 — ADR-009 xác nhận kết quả đấu giá | [#4](https://github.com/oNguyenVanManh/product-a-backlog/issues/4) — EP-04 | Spec mới thêm sau LAB-4 |
| [`PREMISE.md`](./PREMISE.md) §1 — `entry_type`/`adjusts_id` cho bút toán điều chỉnh | [#7](https://github.com/oNguyenVanManh/product-a-backlog/issues/7) — EP-07 | Spec sửa sau LAB-4 |
| [`PREMISE.md`](./PREMISE.md) §1 — 20 file technical-design mới | 20 issue cha rải khắp EP-01…EP-13 | Spec mới thêm sau LAB-4 |

Mỗi issue chức năng mang nhãn ưu tiên **`P0`** (190 issue) hoặc **`P1`** (96 issue) lấy từ cột
`Ưu tiên` của function list LAB-1, và **138 sub-issue** mang dòng `**Chờ:** #xxx` khai phụ thuộc
theo chuỗi BE → FE/Native → QA — xem [`task-breakdown.md`](./task-breakdown.md) §4.

Mỗi issue chức năng trỏ thẳng tới **tài liệu thiết kế LAB-4 đích danh** (screen spec, technical
design, API, database) chứ không chỉ tên thư mục — xem bảng Truy vết trong thân từng issue.

Năm nhóm ràng buộc nghiệp vụ đặc thù được gắn nhãn riêng trên GitHub (`kc-incentive`,
`kc-negotiated`, `kc-two-tier`, `kc-human`, `kc-business-day`) và phủ **174 issue**. Chi tiết vì sao
tách riêng: [`task-breakdown.md`](./task-breakdown.md) mục 3.

---

## 5. Tuân thủ luật repo công khai

- Chỉ chứa issue và markdown do tôi tự viết.
- **Không** chép đoạn RFP hay đề gốc.
- **Không** có dữ liệu thật, dữ liệu cá nhân hay khoá bí mật. Đã quét toàn repo bằng mẫu tìm
  JWT, `ghp_`/`gho_`, private key và chuỗi mật khẩu — không có kết quả nào là giá trị khoá thật.
- Người ngoài mở được bằng trình duyệt, không cần đăng nhập.
