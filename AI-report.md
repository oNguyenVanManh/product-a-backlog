# AI-report.md — Cách dùng AI trong LAB-5

## 1. Skill và prompt đã dùng cho từng việc

| Việc | Công cụ | Cách viết prompt |
|---|---|---|
| Sửa bộ thiết kế LAB-4 theo góp ý giảng viên | Claude Code, không dùng skill | Đưa thẳng file feedback HTML của giảng viên, yêu cầu phân loại thành 3 nhóm (A thiếu nghiệp vụ / B sai lệch / C chuẩn tài liệu) rồi sửa toàn bộ, không chọn lọc. Sau mỗi nhóm bắt chạy lại bộ kiểm liên kết và frontmatter. |
| Break task | Claude Code | Không yêu cầu "chia nhỏ ra giúp tôi". Thay vào đó đưa **nguyên tắc trước, dữ liệu sau**: 8 nguyên tắc chia task tôi tự đặt, rồi mới đưa sheet effort LAB-1 và bộ spec. AI bổ sung 2 nguyên tắc nữa (truy vết ngược, tách ràng buộc đặc thù) kèm lý do — tôi giữ cả hai. |
| Sinh 471 issue và đẩy lên GitHub | Claude Code + `gh` CLI | Sinh dữ liệu ra JSON trước, kiểm tổng MD bảo toàn (1.059,1 = 1.059,1), **rồi mới** đẩy. Không để AI vừa nghĩ vừa gọi API. |
| Chấm SWP | `/tkm:estimate-swp <URL Project>` | Skill tự chạy theo hợp đồng của nó: bộ chọn xác định → 5 bộ chấm song song → kiểm → hiệu chỉnh → xuất HTML. |
| Quy SWP ra giờ | tự đặt, không dùng AI sinh số | Tôi tự neo hệ số từ định nghĩa SWP 1 trong thang chấm, rồi mới nhờ AI tính bảng. Nếu để AI tự chọn hệ số, nó sẽ chọn hệ số nào cho ra con số gần LAB-1 nhất. |
| Ghi SWP lên Project | AI Agent gọi GraphQL `updateProjectV2ItemFieldValue` | Ghi theo lô có resume: mỗi lô thành công ghi vào file `pushed.json`, đứt giữa chừng thì chạy lại là tiếp từ chỗ dừng chứ không ghi đè từ đầu. |
| Báo cáo tiến độ | Claude Code | Đưa số liệu thật từ Project, yêu cầu **không** làm đẹp đường burndown. |

**Một nguyên tắc tôi áp xuyên suốt:** mọi thứ AI sinh ra đều phải đi qua một **phép kiểm bằng máy**
trước khi tôi đọc. 471 issue thì không ai đọc hết được bằng mắt; nhưng "tổng MD trước và sau khi chia
có bằng nhau không", "471 issue có khớp 471 node id không", "SWP có đúng ô ma trận không" thì máy
kiểm trong một giây.

---

## 2. Con người review ở đâu, bắt được gì

Tôi review ở **5 chốt**, không phải chỉ ở cuối.

### Chốt 1 — sau khi AI lập bản đồ `FEA → thư mục spec`

AI ghép hai danh sách (13 nhóm chức năng và 13 thư mục spec) **theo thứ tự**. Bảy cặp đầu trùng khớp
ngẫu nhiên nên bảng trông rất đúng. Năm cặp cuối sai hẳn: `FEA-11 Thông báo` bị trỏ vào
`rule-management`, `FEA-12 Liên kết kế toán` trỏ vào `notification`.

**Cách bắt:** in bảng ra rồi đọc tên epic đặt cạnh tên thư mục. Phần đúng ngẫu nhiên ở đầu bảng suýt
che mất phần sai ở cuối.

**Đây là nhóm lỗi nguy hiểm nhất trong cả bài**: AI không bịa gì cả, nó suy luận hợp lý từ dữ liệu
không đủ, và kết quả có vẻ ngoài hoàn toàn bình thường.

**Phòng ngừa:** sau đó tôi bắt AI **kiểm chứng lại bản đồ bằng dữ liệu thật** — mở từng thư mục, đọc
title của màn hình đầu tiên, đặt cạnh tên nhóm chức năng. 13/13 khớp mới đi tiếp.

### Chốt 2 — sau khi AI chạy truy vấn phân trang GraphQL

AI viết truy vấn với biến tên `$c`, nhưng `gh --paginate` chỉ nhận đúng tên `$endCursor`. Con trỏ
không bao giờ tiến, lệnh lặp lại trang đầu cho tới khi GitHub ngắt kết nối. File kết quả phình thành
**215.000 dòng toàn bản sao của 100 issue đầu**, và trong suốt 2 phút chạy **không có lỗi nào hiện ra**.

**Cách bắt:** đếm số dòng duy nhất (100) đặt cạnh số dòng tổng (215.000). Nếu chỉ nhìn "lệnh chạy
không báo lỗi" thì đã nối nhầm quan hệ cha–con cho 100 issue và bỏ sót 371 issue còn lại.

**Phòng ngừa:** bỏ truy vấn thủ công, dùng lệnh có sẵn `gh issue list --json number,id --limit 600`.

### Chốt 3 — khi bộ chấm SWP chuyên dụng từ chối làm việc

Hai agent `estimate-swp-worker` đầu tiên trả về BLOCKED: chúng chạy cô lập, không có công cụ đọc file,
nên không nhận được gói bằng chứng. Cả hai **từ chối chấm thay vì đoán bừa**, và nói thẳng "chấm 70
issue mà không có rubric thì sẽ phải bịa số, tôi không làm vậy".

Đây là hành vi đúng và tôi ghi lại vì nó là **đối chứng**: nếu agent ấy cứ chấm đại, tôi sẽ nhận được
346 con số trông hoàn toàn hợp lý mà không có cách nào biết chúng vô căn cứ.

**Xử lý:** đổi sang agent đa dụng, giới hạn chỉ đọc đúng hai file (thang chấm + gói của chính nó). Đây
là **sai lệch so với hợp đồng worker** của skill (worker đúng chuẩn phải không có công cụ nào) và tôi
ghi nó vào caveat của báo cáo HTML thay vì giấu đi.

### Chốt 4 — sau khi 5 bộ chấm trả kết quả

Một agent khai rằng nó **sinh JSON bằng script Python** chứ không đọc từng issue. Nghe như chấm theo
khuôn.

**Cách kiểm:** đếm số rationale duy nhất. Lô 1 cho 68/70 khác nhau và dẫn đúng nội dung từng issue
("Terraform gồm S3, lifecycle Glacier, Secrets Manager"), 10 cặp (Scope, Complexity) khác nhau → chấm
thật. Lô 5 chỉ có 36/69 duy nhất, nhưng cụm lặp lớn nhất là 10 issue PM-theo-tháng và 10 issue
BrSE-theo-tháng — cùng một việc lặp hằng tháng, rationale giống nhau là **đúng** chứ không phải lười.

Sau đó chạy bộ kiểm máy trên cả 346 dòng: SWP có khớp ô ma trận không, chữ ký có đúng từ vựng đóng và
đúng thứ tự không, `routine` có đứng một mình không, `single-component` và `multi-component` có loại
trừ nhau không. **0 lỗi.**

### Chốt 5 — kiểm 5 issue mẫu (chốt quan trọng nhất)

Skill tự chọn 5 issue theo quy tắc xác định. Tôi sửa 3, giữ 2. Chi tiết ở [`estimate.md`](./estimate.md) mục 1.

Đáng kể nhất: lần đầu tôi chọn **20 điểm** cho issue hàng đợi offline. Ma trận SWP chỉ có **đúng một
ô** cho giá trị 20 — Scope 13, nghĩa là *"rộng cấp phát hành hoặc xuyên hệ thống"*. Gán nhãn đó cho
một chức năng di động là sai cấu trúc, và vì hiệu chỉnh lan theo tầng nên nó sẽ kéo theo issue khác.
Đổi sang 16 (Scope 8 × Complexity 3).

**Chỗ này AI chặn tôi lại, không phải ngược lại.** Tôi nêu lý do là *độ khó đồng bộ*, nhưng con số tôi
chọn lại phát biểu một điều về *bề rộng*. Nếu AI cứ nhận con số 20 thì bản estimate sẽ mang một tuyên
bố cấu trúc mà chính tôi không có ý nói.

### Một lỗi tôi mắc và phải sửa công khai

Giữa chừng tôi khẳng định "916 MD của LAB-5 và 912 MD của LAB-1 chỉ cách nhau 0,4 %, hai phương pháp
độc lập gặp nhau". **Sai loại số.** 916 là con số **gộp** (quy thẳng từ cấu trúc, không trừ gì cho
AIDD); 911,9 là con số **ròng** của LAB-1 (đã trừ 147,2 MD cho AIDD). So đúng loại thì phải là 916 với
**1.059,1 MD gộp**, tức LAB-5 thấp hơn **13,5 %**.

Phép so sai ấy nghe rất thuyết phục vì hai con số sát nhau. Nó chỉ lộ ra khi tôi mở lại sheet Summary
gốc của LAB-1 thay vì tin con số đang nhớ. Đã sửa trong [`estimate.md`](./estimate.md) mục 4 và ghi rõ
cái bẫy ngay tại đó.

---

## 3. Điểm đặc biệt trong cách dùng AI

### Chỗ tôi tin là hiệu quả

**Tách "sinh dữ liệu" khỏi "gọi API".** Mọi thứ được sinh ra JSON và kiểm bằng máy trước, đẩy lên
GitHub sau. Nhờ vậy khi GitHub trả HTTP 502 giữa chừng, tôi chỉ cần chạy lại — không có trạng thái
nào bị hỏng, không có issue nào bị tạo hai lần.

**Đặt quy ước trước khi nhìn thấy kết quả.** Hệ số 4 giờ/SWP được neo từ định nghĩa "SWP 1 = một thay
đổi cục bộ thường quy, xong trọn vẹn kèm test và review ≈ nửa ngày". Nếu tôi tính tổng trước rồi mới
chọn hệ số, tôi gần như chắc chắn sẽ chọn hệ số cho ra con số gần LAB-1 — và bản so sánh thành vô nghĩa.

**Cắt con số cũ khỏi gói bằng chứng.** Dòng `Effort LAB-1: X MD` bị gỡ khỏi dữ liệu gửi bộ chấm SWP
(thân issue trên GitHub giữ nguyên để truy vết). Không làm thế thì SWP sẽ bám theo MD cũ và phép so
hai bản thành vòng tròn.

**Dùng bất biến thay vì đọc duyệt.** Với 471 issue, "tổng MD trước và sau khi chia có bằng nhau
không" là câu hỏi máy trả lời được trong một giây và bắt được đúng loại lỗi mà mắt người bỏ sót.

### Chỗ chưa tốt, làm thật phải cải thiện

**344/346 issue mang `confidence = medium` và `evidenceStatus = INFERRED`.** Thân issue do tôi sinh
theo khuôn mẫu (Phạm vi / Truy vết / Định nghĩa xong), không mô tả hành vi, nên bộ chấm chủ yếu dựa
vào tiêu đề và nhãn vai trò. Nói thẳng: đây là ước lượng dựa trên **cấu trúc** backlog, chưa phải dựa
trên nội dung công việc. Làm thật thì phải viết thân issue dày lên rồi chấm lại. Lần này tôi không làm
vì chi phí token cho 471 issue quá lớn so với giá trị bài tập.

**Tôi không chạy được bộ chấm thứ hai để đối chứng.** Skill có chế độ `--high`/`--max` chạy thêm một
bộ chấm bằng model khác để lộ ra chỗ hai bên bất đồng. Tôi chạy `medium`, nên không có số liệu nào nói
cho tôi biết phần nào trong 346 điểm là chắc và phần nào may rủi. Đây là chỗ tôi thấy tiếc nhất.

**Cap 4 MD/issue tốt cho cả backlog nhưng không tốt cho sprint 1 tuần.** Sprint 1 có 4/7 issue cỡ 5–6
SWP nên burndown nằm ngang suốt hai ngày đầu. Tôi chỉ phát hiện ra khi vẽ burndown, tức là **sau** khi
đã tạo xong 471 issue. Lẽ ra phải thử xếp một sprint mẫu trước khi chốt độ hạt.

**Tôi chưa kiểm được chéo chất lượng giữa 5 lô chấm.** Mỗi lô do một agent khác nhau chấm, và tôi chỉ
kiểm tính hợp lệ (đúng ma trận, đúng từ vựng) chứ không kiểm **tính nhất quán giữa các lô** — liệu
agent lô 2 và agent lô 4 có chấm cùng một mức độ khó cho hai issue tương đương không. Với 5 agent độc
lập thì đây là rủi ro thật, và tôi chưa có cách rẻ để đo.
