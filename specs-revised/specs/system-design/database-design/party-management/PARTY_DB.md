---
id: DB-PARTY
title: Bên tham gia chợ
type: database
table: party
feature: party-management
version: "0.1.0"
updated_by: nguyen-van-manh-c
updated: 2026-10-11
related: []
---

# PARTY — Bên tham gia chợ (`party`)

> Biểu mẫu: **BM-2-901-50 v1.1** — Database Design · SUN ASTERISK VIETNAM CO., LTD · ISO/IEC 27001:2013 & ISO 9001:2015

---

## 1. Lịch sử sửa đổi

| No | Version | Action | Nội dung thay đổi | Ngày | Người sửa |
|---|---|---|---|---|---|
| 1 | 0.1.0 | Add New | Trích từ `supabase/01_schema.sql` của prototype LAB-3 | 2026-10-11 | nguyen-van-manh-c |

---

## 2. Danh sách bảng

| Mục | Giá trị |
|---|---|
| System Name | Hệ thống hỗ trợ vận hành chợ bán buôn thủy sản |
| Schema | `public` |
| Logical table name | Bên tham gia chợ |
| Physics table name | `party` |
| CHARACTER SET | UTF-8 |
| Overview | Bên tham gia chợ |

---

## 3. ER Diagram

```mermaid
erDiagram
    party {
        _ _ "bảng không tham chiếu bảng nào khác"
    }
```

Quan hệ trực tiếp của `party`. Sơ đồ toàn hệ thống ở [`_extra/database-overview.md`](../../../../_extra/database-overview.md).

---
## 4. Định nghĩa bảng

| No. | Key | Logical name | Physic name | Data Type | Not Null | Default | Ghi chú |
|---|---|---|---|---|---|---|---|
| 1 | PK | id | `id` | `uuid` | ✓ | `gen_random_uuid()` |  |
| 2 | UK | code | `code` | `text` | ✓ |  |  |
| 3 |  | name | `name` | `text` | ✓ |  |  |
| 4 |  | kind | `kind` | `party_kind` | ✓ |  |  |
| 5 |  | phone | `phone` | `text` |  |  |  |
| 6 |  | is_active | `is_active` | `boolean` | ✓ | `true` |  |
| 7 |  | created_at | `created_at` | `timestamptz` | ✓ | `now()` |  |

---

### Ràng buộc và ghi chú

Không có ràng buộc nghiệp vụ đặc biệt ngoài khoá ngoại và CHECK đã nêu ở mục 3.
