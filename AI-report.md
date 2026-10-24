# AI-report.md — Cách dùng AI trong LAB-5

## 1. Skill và prompt đã dùng cho từng việc

| Việc | Công cụ | Cách viết prompt |
|---|---|---|
| Sửa bộ thiết kế LAB-4 theo góp ý giảng viên | Claude Code, không dùng skill | Đưa thẳng file feedback HTML của giảng viên, yêu cầu phân loại thành 3 nhóm (A thiếu nghiệp vụ / B sai lệch / C chuẩn tài liệu) rồi sửa toàn bộ, không chọn lọc. Sau mỗi nhóm bắt chạy lại bộ kiểm liên kết và frontmatter. |
| Break task | Claude Code | Không yêu cầu "chia nhỏ ra giúp tôi". Thay vào đó đưa **nguyên tắc trước, dữ liệu sau**: 8 nguyên tắc chia task tôi tự đặt, rồi mới đưa sheet effort LAB-1 và bộ spec. AI bổ sung 2 nguyên tắc nữa (truy vết ngược, tách ràng buộc đặc thù) kèm lý do — tôi giữ cả hai. |
| Sinh 537 issue và đẩy lên GitHub | Claude Code + `gh` CLI | Sinh dữ liệu ra JSON trước, kiểm tổng MD bảo toàn (1.059,1 = 1.059,1), **rồi mới** đẩy. Không để AI vừa nghĩ vừa gọi API. |
| Chấm SWP | `/tkm:estimate-swp <URL Project>` | Skill tự chạy theo hợp đồng của nó: bộ chọn xác định → 5 bộ chấm song song → kiểm → hiệu chỉnh → xuất HTML. |
| Quy SWP ra giờ | tự đặt, không dùng AI sinh số | Tôi tự neo hệ số từ định nghĩa SWP 1 trong thang chấm, rồi mới nhờ AI tính bảng. Nếu để AI tự chọn hệ số, nó sẽ chọn hệ số nào cho ra con số gần LAB-1 nhất. |
| Ghi SWP lên Project | AI Agent gọi GraphQL `updateProjectV2ItemFieldValue` | Ghi theo lô có resume: mỗi lô thành công ghi vào file `pushed.json`, đứt giữa chừng thì chạy lại là tiếp từ chỗ dừng chứ không ghi đè từ đầu. |
| Báo cáo tiến độ | Claude Code | Đưa số liệu thật từ Project, yêu cầu **không** làm đẹp đường burndown. |

**Một nguyên tắc tôi áp xuyên suốt:** mọi thứ AI sinh ra đều phải đi qua một **phép kiểm bằng máy**
trước khi tôi đọc. 537 issue thì không ai đọc hết được bằng mắt; nhưng "tổng MD trước và sau khi chia
có bằng nhau không", "537 issue có khớp 537 node id không", "SWP có đúng ô ma trận không" thì máy
kiểm trong một giây.

---

## 2. Con người review ở đâu, bắt được gì

Tôi review ở **8 chốt**, không phải chỉ ở cuối. Năm chốt đầu bắt lỗi của từng bước; chốt 6 bắt lỗi
nằm **giữa** các bước (tài liệu trôi khỏi hệ thống); chốt 7 bắt lỗi ở tầng cao nhất — **làm đúng thứ
mình định làm, nhưng không phải thứ đề bài yêu cầu.**

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

### Chốt 5 — kiểm 5 issue mẫu (chốt đề bài bắt buộc)

Skill tự chọn 5 issue theo quy tắc xác định. Tôi sửa 3, giữ 2. Chi tiết ở [`estimate.md`](./estimate.md) mục 1.

Đáng kể nhất: lần đầu tôi chọn **20 điểm** cho issue hàng đợi offline
([#311](https://github.com/oNguyenVanManh/product-a-backlog/issues/311)). Ma trận SWP chỉ có **đúng một
ô** cho giá trị 20 — Scope 13, nghĩa là *"rộng cấp phát hành hoặc xuyên hệ thống"*. Gán nhãn đó cho
một chức năng di động là sai cấu trúc, và vì hiệu chỉnh lan theo tầng nên nó sẽ kéo theo issue khác.
Đổi sang 16 (Scope 8 × Complexity 3).

**Chỗ này AI chặn tôi lại, không phải ngược lại.** Tôi nêu lý do là *độ khó đồng bộ*, nhưng con số tôi
chọn lại phát biểu một điều về *bề rộng*. Nếu AI cứ nhận con số 20 thì bản estimate sẽ mang một tuyên
bố cấu trúc mà chính tôi không có ý nói.

### Chốt 6 — đối chiếu cả bộ nộp với hệ thống thật, sau khi đã viết xong

Năm chốt trên đều kiểm **trong lòng một bước**: bản đồ có đúng không, truy vấn có chạy đủ không, điểm
có khớp ma trận không. Khi mọi file đã viết xong, tôi chạy thêm một lượt khác hẳn về bản chất: **đếm
trên GitHub rồi so với chữ trong tài liệu.**

Lượt này bắt được 7 lỗi, trong đó 3 lỗi nghiêm trọng:

| Lỗi | Tài liệu nói | Thực tế | Đã xử lý |
|---|---|---|---|
| Số issue mang nhãn ràng buộc đặc thù | `task-breakdown.md`: **144**<br>`README.md`: **45** | **45** | Gắn nhãn cho 105 sub-issue còn thiếu → cả ba nơi đều **150** |
| Ngày nộp bản LAB-4 mà backlog bám theo | **20/10/2026** | **11/10/2026** | Sửa theo ngày thật của file |
| Trường `Status` trên Project | mô tả đầy đủ 5 mức | **464/537 item bỏ trống** | Đặt `Todo` cho toàn bộ item ngoài Sprint 1 |

Bốn lỗi còn lại ở mức trung bình và nhỏ: 5 chỗ trong `estimate.md` viết `[#139]` trông như link nhưng
không có đích; mã nội bộ `IS-FNC-014` trong `PREMISE.md` không tra được trên GitHub vì tiền tố `IS-`
chỉ tồn tại trong script của tôi; một tham chiếu treo trong `task-breakdown.md` §4 trỏ tới dòng
`PREMISE.md` §2 chưa hề tồn tại; và `README.md` khai "đã mở thử bằng cửa sổ ẩn danh" trong khi tôi
mới kiểm bằng HTTP request sạch cookie.

**Ba lỗi nghiêm trọng thuộc cùng một họ:** tài liệu và hệ thống thật kể hai câu chuyện khác nhau, mà
mỗi bên **đọc riêng đều có vẻ ổn**. Không file nào tự mâu thuẫn. Con số 144 nằm trong một bảng được
trình bày đàng hoàng. Ngày 20/10 không bị gì trong tài liệu phản bác. Board trắng phần `Status` chỉ
sai khi đặt cạnh đoạn văn mô tả 5 mức trạng thái.

Chúng **không lộ ra khi đọc lại tài liệu** — tôi đã đọc, và không thấy gì. Chúng chỉ lộ khi chạy
`gh issue list --label kc-incentive | wc -l` rồi đặt kết quả cạnh con số trong file.

**Bài học tôi rút ra cho cách làm việc với AI ở quy mô này:** khi AI sinh ra vừa *hệ thống* (537 issue
trên GitHub) vừa *tài liệu mô tả hệ thống đó*, hai thứ được sinh từ hai lần chạy khác nhau và **sẽ
trôi khỏi nhau** — không phải vì AI bịa, mà vì công thức đếm ở hai bên khác nhau một chi tiết nhỏ
(bên đếm cả sub-issue, bên chỉ gắn nhãn tới issue cha). Review bằng cách *đọc* không bắt được loại
trôi này. Phải có một bước **đối chiếu lời khai với nguồn sự thật**, và bước đó nên tự động hoá thành
script chứ không làm bằng mắt.

### Chốt 7 — tự chấm bài mình theo vai giảng viên

Sau khi bộ nộp đã hoàn chỉnh và đã push, tôi chấm lại nó theo đúng tiêu chí của đề bài, cố tình đi
tìm chỗ yếu trước chỗ mạnh. Lượt này bắt được một lỗi **nặng hơn tất cả bảy lỗi ở chốt 6 cộng lại**,
và nó là loại lỗi mà không phép kiểm máy móc nào bắt được: **break sai nguồn.**

Đề bài nói rõ *"detail design LAB-4 là nguồn break task chính; estimate LAB-1 dùng để **so với** SWP
và số giờ mới"*. Tôi làm ngược: đơn vị chia việc là `FNC-001…063` và `PRJ-01…47` — mã của **sheet
effort LAB-1** — còn LAB-4 chỉ được dùng làm liên kết truy vết ở mức thư mục. Đếm được trên GitHub:
**0 issue trỏ tới một tài liệu thiết kế cụ thể**, 264 issue chỉ trỏ tới tên thư mục. 85 tài liệu
thiết kế của LAB-4 không có issue nào tương ứng đích danh.

Hệ quả thực tế: dev nhận issue "Nhập trạng thái thanh toán" không biết mở `SCR_19_SPEC.md` hay file
nào — bảng truy vết chỉ nói "xem thư mục `incentive/`", trong đó có 5 màn hình.

Lượt tự chấm còn bắt thêm ba chỗ:

| Chỗ yếu | Bằng chứng | Đã xử lý |
|---|---|---|
| DoD là khuôn mẫu | 1.067 dòng DoD trên toàn backlog, chỉ **14 câu khác nhau**; câu "Đã review chéo" lặp 342 lần | Viết lại DoD cho 63 issue chức năng, bám chính file thiết kế: **290 dòng, không dòng nào trùng** |
| "Chỗ hở spec phát hiện khi break" phần lớn là đồ cũ | 7/9 dòng là mục giảng viên đã chỉ ra ở feedback LAB-4, tức biết trước khi break | Tách §4 thành 4.1 (đã biết) và 4.2 (phát hiện khi break), bổ sung **11 chỗ hở mới** tìm ra trong lúc viết DoD |
| Backlog chưa được xếp lịch | Iteration phủ 7/537 issue = 1,5 % | Xếp thêm Sprint 2–4, phủ 26 issue |

**Vì sao chốt 6 không bắt được lỗi này.** Chốt 6 hỏi *"con số trong tài liệu có khớp hệ thống không"*
— và mọi con số đều khớp. 537 issue là thật, 1.392 SWP là thật, bảng truy vết có tồn tại. Lỗi nằm ở
tầng trên: **truy vết tới đúng chỗ nhưng chưa đủ sâu**, và cấu trúc backlog bám nguồn sai. Không có
phép đếm nào phát hiện ra chuyện đó; phải đọc lại đề bài rồi hỏi "mình có làm đúng thứ được yêu cầu
không", chứ không phải "mình có làm đúng thứ mình định làm không".

Đây là lý do tôi giữ chốt 7 tách khỏi chốt 6 trong báo cáo này: hai chốt hỏi hai câu khác nhau, và
câu thứ hai khó hơn nhiều.

### Chốt 8 — sau khi tách lại backlog, kiểm chính lệnh sửa hàng loạt

Vòng tách lại (cap 4 MD → 3 MD) đổi hàng loạt con số trong 6 file. Tôi dùng một lệnh thay thế hàng
loạt bằng biểu thức chính quy cho nhanh. **Nó vừa phá hai chỗ vừa sót ba chỗ.**

| Hỏng thế nào | Hậu quả nếu không bắt |
|---|---|
| Luật `cap 4 MD → cap 3 MD` áp cả vào **câu kể lịch sử** | `task-breakdown.md` thành *"Bản đầu đặt cap 3 MD với lý do 4 MD ≈ 3 ngày"* — câu tự mâu thuẫn, và xoá mất lý do vì sao phải sửa |
| Mẫu `= **471**` không khớp cách viết trong README | README vẫn khai 471 issue trong khi GitHub có 537 |
| Lượt sửa link trước đó tạo link lồng nhau | 20 link trong `estimate.md` hỏng cú pháp markdown, hiện ra dưới dạng `[``EP-16`` [#16](url)](url)` |
| Số `342` trong câu *"lặp 342 lần"* (đếm dòng DoD) trùng với số sub-issue cũ | Suýt bị đổi thành 408, biến một phép đếm đúng thành số bịa |

Chỗ cuối là chỗ đáng sợ nhất: **hai đại lượng khác nhau tình cờ có cùng giá trị**. Lệnh thay thế không
biết 342 nào là số sub-issue và 342 nào là số lần lặp của một câu. Nếu tôi viết luật rộng hơn một
chút, nó đã lặng lẽ biến một dữ kiện đã kiểm chứng thành con số sai mà không ai đọc ra được.

**Cách bắt:** sau mỗi lệnh thay thế hàng loạt, in ra **mọi dòng còn chứa số cũ** rồi đọc từng dòng
một. Mất hai phút và bắt được cả năm chỗ.

**Rút ra:** thay thế hàng loạt an toàn khi sửa *mã nguồn* — trình biên dịch sẽ la lên. Nó nguy hiểm
khi sửa *văn bản*, vì văn bản sai vẫn "chạy" được. Với tài liệu thì luật phải hẹp đến mức gần như
liệt kê từng chỗ, hoặc đừng dùng.

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

**Dùng bất biến thay vì đọc duyệt.** Với 537 issue, "tổng MD trước và sau khi chia có bằng nhau
không" là câu hỏi máy trả lời được trong một giây và bắt được đúng loại lỗi mà mắt người bỏ sót.

### Chỗ chưa tốt, làm thật phải cải thiện

**344/346 issue mang `confidence = medium` và `evidenceStatus = INFERRED`.** Thân issue do tôi sinh
theo khuôn mẫu (Phạm vi / Truy vết / Định nghĩa xong), không mô tả hành vi, nên bộ chấm chủ yếu dựa
vào tiêu đề và nhãn vai trò. Nói thẳng: đây là ước lượng dựa trên **cấu trúc** backlog, chưa phải dựa
trên nội dung công việc. Làm thật thì phải viết thân issue dày lên rồi chấm lại. Lần này tôi không làm
vì chi phí token cho 537 issue quá lớn so với giá trị bài tập.

**Tôi không chạy được bộ chấm thứ hai để đối chứng.** Skill có chế độ `--high`/`--max` chạy thêm một
bộ chấm bằng model khác để lộ ra chỗ hai bên bất đồng. Tôi chạy `medium`, nên không có số liệu nào nói
cho tôi biết phần nào trong 346 điểm là chắc và phần nào may rủi. Đây là chỗ tôi thấy tiếc nhất.

**Cap 3 MD/issue tốt cho cả backlog nhưng không tốt cho sprint 1 tuần.** Sprint 1 có 4/7 issue cỡ 5–6
SWP nên burndown nằm ngang suốt hai ngày đầu. Tôi chỉ phát hiện ra khi vẽ burndown, tức là **sau** khi
đã tạo xong 537 issue. Lẽ ra phải thử xếp một sprint mẫu trước khi chốt độ hạt.

**Chốt 6 chạy quá muộn, và chỉ chạy một lần.** Phép đối chiếu lời khai với GitHub chỉ được làm sau
khi cả 6 file đã viết xong. Nếu nó chạy ngay sau bước gắn nhãn thì tôi đã bắt được chuyện 105
sub-issue thiếu nhãn **trước khi** viết `task-breakdown.md`, thay vì phải sửa cả tài liệu lẫn hệ
thống. Làm thật thì phép đối chiếu này nên là một script chạy sau mỗi lần AI sinh ra thứ gì đó lên
hệ thống thật — rẻ, chạy vài giây, và nó bắt đúng loại lỗi mà đọc lại tài liệu không bao giờ thấy.

**Tôi chưa kiểm được chéo chất lượng giữa 5 lô chấm.** Mỗi lô do một agent khác nhau chấm, và tôi chỉ
kiểm tính hợp lệ (đúng ma trận, đúng từ vựng) chứ không kiểm **tính nhất quán giữa các lô** — liệu
agent lô 2 và agent lô 4 có chấm cùng một mức độ khó cho hai issue tương đương không. Với 5 agent độc
lập thì đây là rủi ro thật, và tôi chưa có cách rẻ để đo.
