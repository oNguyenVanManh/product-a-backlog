---
id: ADR-009
title: Kết quả đấu giá phải qua bước xác nhận của 確認者
type: decision
version: "0.1.0"
updated_by: nguyen-van-manh-c
updated: 2026-10-24
status: đã áp dụng
---

# ADR-009 — Kết quả đấu giá phải qua bước xác nhận của 確認者

> ⚠️ **Không có biểu mẫu chuẩn cho ADR.** Bộ spec-standard (QC-01) không quy định loại tài liệu này,
> nên file được viết mới theo yêu cầu LAB-4. Bốn mục dưới đây theo khuôn ADR thông dụng.

> **Phát sinh sau phản hồi LAB-4.** Trục B (khối nghiệp vụ bắt buộc) chỉ đạt 50% vì khối đấu giá
> ghi thẳng kết quả thành giao dịch, không lưu người xác nhận và không theo mô hình trạng thái của
> khách. ADR này ghi lại quyết định sửa.

---

## Bối cảnh

Phiên đấu giá (せり) ở chợ diễn ra bằng lời và ký hiệu tay. Nhân viên ghi kết quả vào hệ thống
**sau khi phiên kết thúc**, dựa trên ghi chép tay của chính mình. Hai điều khiến kết quả đấu giá
khác hẳn giao dịch thỏa thuận:

- **Người ghi không phải người quyết định.** Giao dịch thỏa thuận do hai bên tự chốt với nhau, ghi
  xong là xong. Kết quả đấu giá do nhân viên ghi hộ, nên cần một người có thẩm quyền tại phiên —
  **確認者** — xác nhận rằng con số đúng với phiên vừa diễn ra.
- **Ký hiệu tay dễ đọc nhầm.** SCOPE-OUT-02 cấm dùng OCR, nên ô ký hiệu tay là text nhân viên gõ
  tay. Gõ nhầm một ký hiệu là sai bên mua.

Bản LAB-4 trước đó bỏ qua cả hai: ghi xong là chốt, không ai xác nhận, không lưu vết ai chịu
trách nhiệm.

## Lựa chọn

Kết quả đấu giá đi qua **ba trạng thái**: `chờ xác nhận` → `đã xác nhận` hoặc `bị từ chối`.

| Trạng thái | Nghĩa | Vào bảng đối soát? | Tính thưởng? |
|---|---|---|---|
| `pending_confirm` | Nhân viên đã ghi, chờ 確認者 duyệt | ❌ | ❌ |
| `confirmed` | 確認者 đã xác nhận, có hiệu lực pháp lý | ✅ | ✅ |
| `rejected` | 確認者 từ chối, phải ghi lý do | ❌ | ❌ |

Bảng `trade` thêm ba cột: `confirm_status`, `confirmed_by`, `confirmed_at`.

Giao dịch thỏa thuận (相対取引) **không qua bước này** — `confirm_status` mặc định `confirmed`
ngay khi ghi, vì hai bên đã tự chốt với nhau.

## Phương án đã bỏ

| Phương án | Vì sao bỏ |
|---|---|
| Giữ nguyên: ghi xong là chốt | Chính là chỗ bản LAB-4 bị trừ điểm. Không ai chịu trách nhiệm khi con số sai, và không truy được ai ghi hộ ai |
| Bắt 確認者 tự ghi kết quả | Sai thực tế vận hành: 確認者 đang điều khiển phiên, không rảnh tay nhập liệu |
| Dùng dòng đảo để sửa khi phát hiện ghi nhầm | Dòng đảo sửa được **sau khi** đã có hiệu lực. Không ngăn được việc một kết quả sai lọt vào bảng đối soát ngay từ đầu |
| Thêm cột `is_confirmed` kiểu boolean | Không phân biệt được "chưa ai duyệt" với "đã bị từ chối". Hai thứ này xử lý khác nhau |

## Hệ quả

- Màn **SCR-09** tách làm hai phần: nhân viên ghi kết quả, 確認者 duyệt. Phát sinh thêm màn danh
  sách chờ xác nhận và một API duyệt
- Bảng đối soát và phép tính thưởng phải lọc `confirm_status = 'confirmed'` — **mọi truy vấn đang
  cộng tiền đều phải sửa**
- `confirmed_by` phải khác `created_by`: người ghi không tự xác nhận cho mình. Thi hành bằng trigger
- **Đổi lại:** kết quả đấu giá không còn hiệu lực tức thì. Nếu 確認者 bận, kết quả nằm chờ và không
  vào đối soát ngày hôm đó. Cần cảnh báo khi có kết quả chờ quá lâu trước giờ khoá sổ
- Giao dịch thỏa thuận không đổi gì — 90% khối lượng giao dịch không chịu ảnh hưởng
