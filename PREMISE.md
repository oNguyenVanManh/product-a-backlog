# PREMISE — Tiền đề của backlog so với bản LAB-4 đã nộp

Bản LAB-4 đã nộp là mốc. File này khai từng khác biệt giữa backlog LAB-5 và bản mốc đó.
Bản thiết kế đã sửa nằm trong repo tại [`specs-revised/`](./specs-revised/); backlog bám bản đã sửa.

**Nguồn của mọi thay đổi dưới đây:** góp ý review LAB-4 của giảng viên (3 nhóm A/B/C) và các chỗ hở
phát hiện khi break task.

---

## 1. Spec thêm / bỏ / sửa so với LAB-4

| Spec (mã/file) | Thêm/Bỏ/Sửa | Trước → sau | Vì sao | Issue bị ảnh hưởng |
|---|---|---|---|---|
| `_extra/decisions/ADR-009-xac-nhan-ket-qua-dau-gia.md` | Thêm | *(không có)* → ADR mới, 4 mục | Góp ý review LAB-4 (A1): LAB-4 mô tả phiên đấu giá せり nhưng không nói kết quả phiên được **xác nhận** ra sao trước khi thành giao dịch chính thức. Thiếu mốc này thì sổ chỉ-ghi-thêm không có điểm bắt đầu hợp lệ. | `EP-04` · `IS-FNC-014` · `IS-FNC-015` |
| `specs/system-design/database-design/trading/TRADE_DB.md` | Sửa | thiếu trạng thái xác nhận → thêm `confirm_status`, `confirmed_by`, `confirmed_at` | Hệ quả trực tiếp của ADR-009 — không có 3 cột này thì không ghi được ai xác nhận, lúc nào. | `IS-FNC-014` · `IS-PRJ-05` |
| `specs/trading/screen-specification/SCR_09_SPEC.md` | Sửa | không có sơ đồ trạng thái → thêm state diagram + 3 ràng buộc chuyển trạng thái | Góp ý review LAB-4 (A1): màn ghi kết quả phiên không nói rõ trạng thái nào cho sửa, trạng thái nào khoá. | `IS-FNC-014` |
| `specs/system-design/database-design/incentive/INCENTIVE_DB.md` | Sửa | ghi đè dòng thưởng → thêm `entry_type`, `adjusts_id`, `posted_period`; đổi UNIQUE key | Góp ý review LAB-4 (A2): LAB-4 cho phép tính lại và **ghi đè** dòng thưởng đã chốt kỳ. Sai với sổ chỉ-ghi-thêm và sai với 完納奨励金 — điều chỉnh sau khi chốt kỳ phải là bút toán mới. | `EP-07` toàn bộ · `IS-FNC-036` |
| 20 file `technical-design/{FNC}_TECH.md` | Thêm | chỉ có tên chức năng → mỗi file có cơ chế kích hoạt, dữ liệu, quy tắc, xử lý lỗi, sequence diagram | Góp ý review LAB-4 (A3): 20 chức năng (không phải 15 như góp ý ước) mới chỉ có tên, dev không triển khai được nếu không hỏi lại. | 20 issue cha tương ứng |
| `specs/system-design/database-design/settlement/PAYMENT_STATUS_DB.md` | Sửa | thiếu `paid_date` → thêm cột + ghi chú `null` = chưa trả ⇒ thưởng 0 | Góp ý review LAB-4 (B4): không có ngày trả thì không tính được "đúng hạn". | `IS-FNC-035` · `IS-FNC-036` |
| `_extra/architecture.md` | Sửa | cụt ở mục 3 → khôi phục "Luồng dữ liệu chính" và "Nhánh loại giao dịch" | Góp ý review LAB-4 (B5): hai mục bị cắt mất, trong đó có định nghĩa 業務日 02:00–10:00 JST và 休市日. | `EP-15` · `IS-PRJ-04` |
| `specs/system-design/database-design/authentication/APP_USER_DB.md` | Sửa | CHECK 4 giá trị → 6 vai trò | Góp ý review LAB-4 (B6): LAB-4 có 6 vai trò ứng dụng nhưng ràng buộc CHECK trong CSDL mới liệt kê 4. | `EP-02` |
| 30 file `screen-specification/SCR_*_SPEC.md` | Sửa | `id:` frontmatter đánh số rời (`SPEC-09-23`) → truy ngược được tên file (`SPEC-SCR_07`) | Góp ý review LAB-4 (C1): không truy vết được từ mã sang file. | — (chỉ ảnh hưởng truy vết) |
| 12 file `database-design/**/*_DB.md` | Sửa | cấu trúc tự do → đúng 4 mục của template BM-2-901-50 + ER diagram từng bảng | Góp ý review LAB-4 (C2): lệch template chuẩn công ty. | — |
| `specs/settlement/screen-specification/SCR_12_SPEC.md` | Sửa | `exception_reason` bắt buộc luôn → chỉ bắt buộc khi `status = exception` | Góp ý review LAB-4 (C4): validation mâu thuẫn với luồng thường. | `IS-FNC-032` |
| `specs/incentive/screen-specification/SCR_20_SPEC.md` | Sửa | 0 nhánh lỗi → 4 nhánh (`M_50`, `M_30`, `M_41`, nhánh điều chỉnh) | Góp ý review LAB-4 (C5): màn không mô tả hành vi khi lỗi. | `IS-FNC-037` |

**Không bỏ tính năng nào** so với LAB-4. Không thêm màn hình mới — vẫn 30 màn web + 7 màn native.

---

## 2. Giả định bổ sung

Giả định chỉ lấp chỗ RFP/spec để ngỏ. Chỗ nào RFP đã nêu rõ thì không ghi đè.

| Giả định | Chỗ spec/RFP để ngỏ | Ảnh hưởng tới issue/estimate |
|---|---|---|
| Một sprint = 1 tuần, 5 ngày làm việc | RFP không nói nhịp lặp | Quyết định cap 4 MD/issue (≈3 ngày, gọn trong nửa sprint) → quyết định số issue = 471 |
| Đội hình giữ nguyên 8 vai trò của cost sheet LAB-1 trong suốt 10 tháng | RFP không ràng buộc đội hình | `EP-19` chia PM 140 MD và BrSE 100 MD đều cho 10 tháng, mỗi tháng 1 issue con |
| Người phụ trách giả định: gán toàn bộ cho `oNguyenVanManh` | Bài tập không có đội thật | Không ảnh hưởng effort; chỉ để board có trường assignee |
| Chức năng chỉ có 1 vai trò và ≤ 4 MD thì **không** tạo issue con | Không có chuẩn nào quy định | 4 issue cha là issue lá — giảm 4 issue rỗng nghĩa |
| AIDD giảm 5% effort gộp, áp đều mọi vai trò | LAB-1 đã giả định AIDD nhưng không nói áp ở đâu | 1.059,1 MD gộp → 912 MD ròng (xem `estimate.md`) |
| Sprint giả lập là **Sprint 1** của pha Requirement + khởi động nền tảng | Bài yêu cầu "ít nhất 1 sprint" | Quyết định issue nào vào Iteration đầu trong `progress-report.md` |

---

## 3. Hướng đã chốt

| Vấn đề | Các phương án ở LAB-4 | Phương án chốt | Vì sao |
|---|---|---|---|
| Xác nhận kết quả phiên đấu giá | LAB-4 để ngỏ: (a) ghi thẳng thành giao dịch, (b) qua bước xác nhận của người điều hành phiên | (b) — hai bước, có `confirm_status` | Sổ chỉ-ghi-thêm không cho sửa. Nếu ghi thẳng, mọi sai sót khi hô giá đều phải đảo bút toán, rất nặng với phiên せり nhịp nhanh. ADR-009 ghi lại cả phương án bị loại. |
| Điều chỉnh tiền thưởng sau khi chốt kỳ | LAB-4 ngầm định ghi đè | Bút toán điều chỉnh (`entry_type='adjust'`) | Nhất quán với nguyên tắc chỉ-ghi-thêm đã chốt ở ADR-002, và giữ được vết kiểm toán cho 完納奨励金. |
| Khoá ngày nghiệp vụ | LAB-4 nêu cả chặn ở tầng ứng dụng lẫn trigger CSDL | Trigger CSDL (`day_is_locked()`) | Chặn ở ứng dụng thì job nền và công cụ nạp dữ liệu đi vòng qua được. Đã có trong prototype LAB-3. |
| Quy đổi SWP → giờ | LAB-4 không bàn | Quy ước độc lập, dựng mới ở `estimate.md`, **không** lấy MD của LAB-1 chia ngược | Nếu quy giờ từ chính MD của LAB-1 thì phép so LAB-1 ↔ LAB-5 thành vòng tròn, không nói lên điều gì. |
