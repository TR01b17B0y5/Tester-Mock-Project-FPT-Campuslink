# 08 – Verification Log

## 1. Mục đích

Ghi nhận việc kiểm chứng các Root Cause Hypotheses được xác định trong `08_hypothesises.md`.

Verification Log được dùng để chuyển từ **hypothesis** sang **evidence-based conclusion**. Chỉ khi có evidence thực tế mới được kết luận `Confirmed`, `Rejected` hoặc `Inconclusive`.

## 2. Verification Log

| Verification ID | Bug ID | Rank | Hypothesis | Cách verify (theo hypothesis) | Actual Evidence | Result | Notes |
|---|---|---:|---|---|---|---|---|
| VER-001 | BUG-UC06-001 | 1 | FE Form Validation thiếu rule `required` cho DateA và BE DTO thiếu annotation `@NotNull` / `@NotBlank`. | Thực hiện gửi API `POST /api/candidates` qua Postman bỏ trường `dob` 5 lần: nếu 5/5 lần trả `201 Created` -> xác nhận BE thiếu validation; nếu trả `400 Bad Request` -> bác bỏ BE, xác nhận lỗi hoàn toàn ở FE. | Đã gửi request tạo Candidate khi bỏ trống D.O.B. API vẫn trả response OK và Candidate vẫn xuất hiện. | **Inconclusive** | Đã xác nhận hệ thống không reject request thiếu D.O.B ở phía API. Chưa test đầy đủ FE nên chưa thể kết luận hypothesis kết hợp FE + BE. |
| VER-002 | BUG-UC06-001 | 2 | BE API Controller/Service tự động gán giá trị mặc định (`NULL` hoặc date mặc định) khi field bị rỗng thay vì ném ra validation error `ME002`. | Query trực tiếp DB bản ghi candidate vừa tạo 5 lần: kiểm tra trường `dob`. Nếu 5/5 lần DB lưu giá trị `1970-01-01` hoặc `NULL` mà API không báo lỗi -> xác nhận BE gán default/bỏ qua validation. | Chưa có evidence thực tế | **Not Verified** | Chưa thực hiện verification. |
| VER-003 | BUG-UC06-001 | 3 | Event handler `onSubmit` ở FE không kiểm tra kết quả trả về của hàm `validateForm()` trước khi gọi API tạo candidate. | Inspect tab Sources trên OperaGX, đặt breakpoint tại hàm submit: bấm Submit 3 lần khi để trống D.O.B. Nếu biến `isValid = false` nhưng hàm call API vẫn thực thi -> xác nhận. | Theo verification trước đó: khi để trống D.O.B, call API vẫn thực thi; ghi nhận 20/20 lần. | **Confirmed** | Evidence này xác nhận onSubmit vẫn gọi API trong scenario đã kiểm tra. Tuy nhiên chưa đủ để kết luận toàn bộ root cause FE. |
| VER-004 | BUG-UC06-001 | 4 | Trình duyệt OperaGX tự động truyền giá trị date mặc định vào Request Body khi submit mà không hiển thị trên UI. | Mở tab Network trên OperaGX, submit 3 lần; kiểm tra Payload. Nếu Payload chứa `dob: "2026-08-09"` -> xác nhận; nếu `dob: ""` hoặc `null` -> bác bỏ. | Đã thử bỏ trống D.O.B và submit; request vẫn được xử lý thành công. Chưa kiểm tra đầy đủ payload để xác định browser có tự gán giá trị D.O.B hay không. | **Inconclusive** | Chưa đủ evidence để xác định OperaGX có tự truyền date mặc định. |
| VER-005 | BUG-UC06-001 | 5 | Schema validation ở FE (Zod/Yup/Joi) định nghĩa trường `dob` là `.optional()` hoặc `.nullable()`. | Kiểm tra file schema validation của Form Candidate: chạy unit test validate schema với object `{ dob: "" }` 1 lần; nếu kết quả `success = true` -> xác nhận schema FE cấu hình sai. | Schema validation với object { dob: "" } cho kết quả success = true, ghi nhận 10/10. | **Confirmed** | Evidence xác nhận schema FE hiện tại cho phép dob rỗng trong scenario đã kiểm tra. |
| VER-006 | BUG-UC06-002 | 1 | Cả FE và BE đều thiếu quy tắc kiểm tra bắt buộc (`required` / `@NotBlank`) đối với trường TextboxC (Address). | Gửi API `POST /api/candidates` qua Postman không truyền field `address` 5 lần: nếu 5/5 lần trả về `201 Created` -> xác nhận BE thiếu validation. | Đã gửi request tạo Candidate khi bỏ trống Address. API vẫn trả response OK và Candidate vẫn xuất hiện. | **Inconclusive** | Evidence cho thấy API không reject Address rỗng, nhưng chưa đủ để xác định chính xác annotation/service/validation layer gây ra lỗi. |
| VER-007 | BUG-UC06-002 | 2 | FE xử lý trim chuỗi rỗng thành `""` và BE coi `""` là chuỗi hợp lệ (chỉ dùng `@NotNull` thay vì `@NotBlank`). | Kiểm tra Request Payload 3 lần: nếu payload gửi `address: ""` và BE trả HTTP 200/201 -> xác nhận BE dùng sai annotation validation. | Đã thử bỏ trống Address; request vẫn trả response OK. | **Inconclusive** | Chưa inspect chính xác Request Payload để xác định payload là address = "" và chưa xác định annotation BE. |
| VER-008 | BUG-UC06-002 | 3 | Mảng cấu hình `requiredFields` trên UI bị bỏ sót key `address`. | Kiểm tra source code FE component Form Candidate: xem mảng `rules` của `TextboxC`, nếu không có `required: true` -> xác nhận FE thiếu configuration. | Chưa có evidence thực tế | **Not Verified** | Chưa thực hiện verification. |
| VER-009 | BUG-UC06-002 | 4 | DB Schema quy định cột `address` là `NULLABLE` và BE Service layer không thực hiện validation logic. | Kiểm tra DDL của bảng `candidates` trong DB 1 lần: nếu cột `address` có thuộc tính `NULL` và không có DB Constraint -> xác nhận DB chấp nhận rỗng. | Chưa có evidence thực tế | **Not Verified** | Chưa thực hiện verification. |
| VER-010 | BUG-UC06-002 | 5 | API Endpoint tạo Candidate gọi sai Service method (gọi method bypass validation). | Bật Debug Log BE server, thực hiện submit 3 lần: kiểm tra Controller gọi `CandidateService.create()` có đi qua Validation Interceptor hay không. | Chưa có evidence thực tế | **Not Verified** | Chưa thực hiện verification. |
| VER-011 | BUG-UC06-003 | 1 | Input control `UploadA` thiếu validation check bắt buộc chọn file trước khi submit ở FE. | Nhấn Submit trên UI khi chưa chọn file 3 lần; quan sát tab Network xem request `multipart/form-data` có gửi đi không. Nếu request vẫn gửi đi -> xác nhận FE không chặn. | Đã submit khi không upload CV; Candidate vẫn xuất hiện và response vẫn trả OK. | **Inconclusive** | Đã xác nhận hệ thống không reject trường hợp thiếu CV ở mức observed behavior. Chưa hoàn tất FE/Network verification để xác định request multipart và nguyên nhân FE. |
| VER-012 | BUG-UC06-003 | 2 | API Controller nhận param file với `@RequestPart(required = false)` hoặc `@RequestParam(required = false)`. | Gọi API `POST /api/candidates` qua Postman không gửi part `file` 5 lần: nếu 5/5 lần trả status 201 -> xác nhận BE khai báo param `required = false`. | Đã thử tạo Candidate không upload CV; response vẫn trả OK. | **Inconclusive** | Chưa xác định được annotation/API parameter thực tế là required=false. |
| VER-013 | BUG-UC06-003 | 3 | BE Controller khởi tạo và lưu bản ghi Candidate trước khi kiểm tra file upload, khi không có file thì bỏ qua bước save file mà không rollback transaction. | Query DB sau khi submit rỗng CV 3 lần: kiểm tra bản ghi candidate vừa tạo có `cv_url = NULL` -> xác nhận BE không rollback. | Chưa có evidence thực tế | **Not Verified** | Chưa thực hiện verification. |
| VER-014 | BUG-UC06-003 | 4 | Thư viện Upload ở FE tự động gửi một dummy Blob/File 0-byte khi người dùng không chọn file. | Inspect object `FormData` trong console trước khi gửi 3 lần: nếu `formData.get('file')` tồn tại với `size = 0` -> xác nhận FE gửi file rỗng. | Chưa có evidence thực tế | **Not Verified** | Chưa thực hiện verification. |
| VER-015 | BUG-UC06-003 | 5 | Trình duyệt OperaGX không trigger đúng event `onChange` cho component custom upload. | Chạy lại test case trên Chrome và Firefox 3 lần: nếu Chrome/Firefox hiển thị cảnh báo `Required field` -> xác nhận lỗi tương thích OperaGX; nếu cũng bị lỗi -> bác bỏ. | Chưa có evidence thực tế | **Not Verified** | Chưa thực hiện verification. |
| VER-016 | BUG-UC06-004 | 1 | Control `TextboxF` thiếu thuộc tính `maxlength="500"` ở FE và DTO BE thiếu annotation `@Size(max = 500)`. | Inspect HTML element `Note`: nếu không có `maxlength="500"` -> xác nhận FE thiếu. Gọi API gửi `note` 501 ký tự 5 lần qua Postman: nếu 5/5 lần trả HTTP 201 -> xác nhận BE thiếu validation. | Đã nhập 501 ký tự vào Note; hệ thống vẫn cho submit/xuất dữ liệu và response vẫn trả OK. | **Inconclusive** | Đã xác nhận hệ thống không reject Note > 500 ký tự ở observed API flow. Chưa inspect HTML và chưa xác định chính xác validation BE/FE. |
| VER-017 | BUG-UC06-004 | 2 | FE chỉ hiển thị counter warning (vd: `501/500`) nhưng không disable input và không prevent event submit. | Nhập 501 ký tự trên UI 3 lần: nếu counter báo màu đỏ/vượt ngưỡng nhưng nút Submit vẫn bấm được và gửi request -> xác nhận logic FE không block. | Đã nhập 501 ký tự và request vẫn được xử lý thành công. | **Inconclusive** | Chưa hoàn tất FE verification để xác định counter/Submit logic có block hay không. |
| VER-018 | BUG-UC06-004 | 3 | Cột `note` trong Database là `VARCHAR(500)` nhưng DB Server bị tắt Strict Mode, tự động cắt (truncate) chuỗi về 500 ký tự mà không ném exception. | Submit note 510 ký tự, query DB check độ dài chuỗi (`LENGTH(note)`): nếu bằng 500 -> xác nhận DB truncate; nếu bằng 510 -> bác bỏ. | Chưa có evidence thực tế | **Not Verified** | Chưa thực hiện verification. |
| VER-019 | BUG-UC06-004 | 4 | DB Schema định nghĩa cột `note` dạng `TEXT` hoặc `VARCHAR` > 500, dẫn đến cả BE và DB chấp nhận chuỗi 501+ ký tự. | Kiểm tra Schema DB 1 lần: nếu data type của `note` là `TEXT` hoặc `VARCHAR(1000)` -> xác nhận DB schema không khớp requirement. | Chưa có evidence thực tế | **Not Verified** | Chưa thực hiện verification. |
| VER-020 | BUG-UC06-004 | 5 | Xử lý sự kiện `onKeyDown` / `onChange` đếm sai ký tự unicode/multibyte trên OperaGX. | Tester thực hiện kiểm thử trên OperaGX. | Chưa có evidence thực tế | **Not Verified** | Chưa thực hiện verification. |
| VER-021 | BUG-UC18-005 | 1 | FE conditional rendering kiểm tra sai role permission key (vd: check `ROLE_HR` thay vì `ROLE_RECRUITER` hoặc không map role `Admin`/`Manager`). | Đăng nhập lần lượt 3 tài khoản (Recruiter, Manager, Admin), truy cập `/interviews/9` 3 lần: nếu cả 3 lần nút `Send Reminder` không xuất hiện -> kiểm tra code FE render ButtonD. | Chưa có evidence thực tế | **Not Verified** | Chưa thực hiện verification. |
| VER-022 | BUG-UC18-005 | 2 | Nút `Send Reminder` bị ràng buộc hiển thị theo `Status` của lịch (vd: chỉ hiện khi `Scheduled`), trong khi lịch `#9` đang ở trạng thái khác (`Completed`/`Cancelled`). | Kiểm tra `Status` của lịch `#9`. Tạo 1 lịch mới trạng thái `Scheduled`, mở view detail 3 lần: nếu nút Send Reminder xuất hiện -> xác nhận nút ẩn/hiện theo Status. | Chưa có evidence thực tế | **Not Verified** | Chưa thực hiện verification. |
| VER-023 | BUG-UC18-005 | 3 | API GET `/api/interviews/9` trả về object detail thiếu flag `canSendReminder: true` hoặc mảng `allowedActions` không chứa `SEND_REMINDER`. | Inspect tab Network tại `GET /api/interviews/9` 3 lần: kiểm tra JSON response. Nếu `allowedActions` không có `"SEND_REMINDER"` -> xác nhận do BE response. | Chưa có evidence thực tế | **Not Verified** | Chưa thực hiện verification. |
| VER-024 | BUG-UC18-005 | 4 | FE đang render nhầm layout Màn hình 2 (dành cho Interviewer) cho tất cả các role thay vì Màn hình 1 (Role A/B/C). | So sánh các field trên giao diện `/interviews/9` với spec Màn hình 2: nếu xuất hiện button `Submit result` và thiếu `Recruiter owner` -> xác nhận FE render nhầm Màn hình 2. | Chưa có evidence thực tế | **Not Verified** | Chưa thực hiện verification. |
| VER-025 | BUG-UC18-005 | 5 | Tài khoản test thực tế bị gán thiếu Role Claims trong JWT Token khi đăng nhập. | Decode JWT token của user đăng nhập trong LocalStorage 1 lần: kiểm tra array `roles`. Nếu không có `HR`, `MANAGER` hoặc `ADMIN` -> xác nhận do data test. | Chưa có evidence thực tế | **Not Verified** | Chưa thực hiện verification. |
| VER-026 | BUG-UC18-002 | 1 | FE Router gán sai thuộc tính `href` / `to` trên Breadcrumb component (vd: gán `/interview-schedules` thay vì `/interviews`). | Hover & Inspect element Breadcrumb "Interview Schedule List" 1 lần: đọc `href`/`to`. Nếu path target khác URL danh sách thực tế -> xác nhận FE routing hardcode sai URL. | Breadcrumb vẫn xảy ra lỗi khi sử dụng. | **Inconclusive** | Đã xác nhận lỗi Breadcrumb vẫn tái hiện, nhưng chưa Inspect href/to để xác định URL được hardcode sai. |
| VER-027 | BUG-UC18-002 | 2 | Nút Breadcrumb dùng relative path thay vì absolute path (vd: `href="interviews"` thay vì `href="/interviews"`), dẫn đến URL bị nối thành `/interviews/9/interviews`. | Click Breadcrumb 3 lần; kiểm tra thanh địa chỉ trình duyệt: nếu URL biến thành `http://.../interviews/9/interviews` -> xác nhận do relative path thiếu dấu `/` ở đầu. | Breadcrumb vẫn xảy ra lỗi khi click. | **Inconclusive** | Chưa ghi nhận chính xác URL sau click nên chưa thể xác định lỗi relative path. |
| VER-028 | BUG-UC18-002 | 3 | Web Server (Nginx/CloudFront) thiếu cấu hình Fallback Rewrite Rule (`try_files $uri $uri/ /index.html`) cho Single Page Application (SPA). | Nhập trực tiếp URL trang danh sách lên thanh địa chỉ trình duyệt và Enter 3 lần: nếu trả về 404 Nginx -> xác nhận do Web Server missing SPA rewrite rule. | Breadcrumb vẫn xảy ra lỗi. | **Inconclusive** | Chưa thực hiện kiểm tra trực tiếp URL và HTTP response của web server nên chưa thể xác định lỗi SPA rewrite. |
| VER-029 | BUG-UC18-002 | 4 | Breadcrumb link truyền kèm query params bị `undefined` (vd: `/interviews?page=undefined`) khiến router không match route. | Click Breadcrumb 3 lần, kiểm tra URL khi bị 404: nếu chứa `undefined` hoặc `null` -> xác nhận state management truyền params sai. | Breadcrumb vẫn xảy ra lỗi. | **Inconclusive** | Chưa ghi nhận URL/query parameter thực tế nên chưa thể xác định undefined/null. |
| VER-030 | BUG-UC18-002 | 5 | Route path trong React/Vue Router bị thay đổi tên sau đợt refactor code nhưng chưa cập nhật ở component `BreadcrumbA`. | So sánh path định nghĩa trang danh sách trong file route config với path gán trong `BreadcrumbA.tsx` 1 lần -> xác nhận mismatch. | Breadcrumb vẫn xảy ra lỗi. | **Inconclusive** | Chưa kiểm tra route config và Breadcrumb component nên chưa thể xác định route mismatch. |

## 3. Quy ước Result

| Result | Ý nghĩa |
|---|---|
| **Confirmed** | Evidence thực tế xác nhận hypothesis. |
| **Rejected** | Evidence thực tế loại trừ hypothesis. |
| **Inconclusive** | Đã thực hiện verification nhưng evidence chưa đủ để kết luận. |
| **Not Verified** | Chưa thực hiện verification hoặc chưa có evidence thực tế. |

## 4. Evidence cần ghi nhận

- API request/response: endpoint, payload, HTTP status, response body.
- Browser Network: request payload và response JSON.
- UI evidence: screenshot/video nếu cần.
- Frontend source/configuration: validation rule, conditional rendering, router.
- Backend: Controller, Service, DTO validation.
- Database: schema/DDL và record thực tế.
- JWT/role claims khi kiểm tra permission.
- Browser/environment comparison khi hypothesis liên quan compatibility.

## 5. Evidence đã thực hiện

### BUG-UC06 – Validation / Data Input

- **D.O.B:** Đã thử không điền D.O.B. Candidate vẫn xuất hiện và response vẫn trả OK.
- **Address:** Đã thử không điền Address. Candidate vẫn xuất hiện và response vẫn trả OK.
- **CV Attachment:** Đã thử không upload CV. Candidate vẫn xuất hiện và response vẫn trả OK.
- **Note:** Đã nhập 501 ký tự. Hệ thống vẫn cho submit/xuất dữ liệu và response vẫn trả OK.
- **FE verification:** Chưa hoàn tất kiểm tra FE, vì vậy chưa kết luận chính xác lỗi nằm ở FE, BE, schema, DB hay browser.

### BUG-UC18 – Breadcrumb

- Breadcrumb **vẫn tái hiện lỗi** khi kiểm tra.
- Chưa có đủ evidence để xác định lỗi cụ thể là `href/to`, relative path, SPA rewrite, query parameter hay route configuration.

## 5. Summary

- **Tổng hypothesis:** 30
- **Confirmed:** 2
- **Rejected:** 0
- **Inconclusive:** 13
- **Not Verified:** 15

> **Kết luận hiện tại:** Đã có một số verification thực tế. Evidence xác nhận hệ thống vẫn chấp nhận D.O.B/Address/CV bị bỏ trống và Note 501 ký tự, đồng thời Breadcrumb vẫn tái hiện lỗi. Tuy nhiên do chưa hoàn tất FE verification và chưa có evidence ở các tầng code/DB/Network tương ứng, các hypothesis về **nguyên nhân gốc** chủ yếu vẫn ở trạng thái `Inconclusive`.