### 1. BUG-UC06-001 – Bỏ trống D.O.B vẫn tạo được Candidate

| **Rank** | **Hypothesis**                                                                                          | **Xác suất + lý do** | **Evidence ỦNG HỘ** | **Evidence LOẠI TRỪ** | **Cách verify (đo được)** |
| -------- | ------------------------------------------------------------------------------------------------------- | -------------------- | ------------------- | --------------------- | ------------------------- |
| **1**    | FE Form Validation thiếu rule `required` cho DateA và BE DTO thiếu annotation `@NotNull` / `@NotBlank`. |                      |                     |                       |                           |

**Medium**




(Có 1 evidence trực tiếp)

| Candidate tạo thành công mà không hiển thị lỗi `ME002` (theo mô tả actual result trong test case). | Chưa tìm được bằng chứng chung loại trừ                                                                                                       | Thực hiện gửi API `POST /api/candidates` qua Postman bỏ trường `dob` 5 lần: nếu 5/5 lần trả `201 Created` -> xác nhận BE thiếu validation; nếu trả `400 Bad Request` -> bác bỏ BE, xác nhận lỗi hoàn toàn ở FE. |
| -------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **2**                                                                                              | BE API Controller/Service tự động gán giá trị mặc định (`NULL` hoặc date mặc định) khi field bị rỗng thay vì ném ra validation error `ME002`. |                                                                                                                                                                                                                 |

**Low**




(Chỉ suy luận logic)

| Candidate vẫn được tạo thành công trong hệ thống. | Chưa tìm được bằng chứng chung loại trừ                                                                               | Query trực tiếp DB bản ghi candidate vừa tạo 5 lần: kiểm tra trường `dob`. Nếu 5/5 lần DB lưu giá trị `1970-01-01` hoặc `NULL` mà API không báo lỗi -> xác nhận BE gán default/bỏ qua validation. |
| ------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **3**                                             | Event handler `onSubmit` ở FE không kiểm tra kết quả trả về của hàm `validateForm()` trước khi gọi API tạo candidate. |                                                                                                                                                                                                   |

**Low**




(Chỉ suy luận logic)

| Không có thông báo lỗi `ME002` xuất hiện trên UI. | Chưa tìm được bằng chứng chung loại trừ                                                                         | Inspect tab Sources trên OperaGX, đặt breakpoint tại hàm submit: bấm Submit 3 lần khi để trống D.O.B. Nếu biến `isValid = false` nhưng hàm call API vẫn thực thi -> xác nhận. |
| ------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **4**                                             | Trình duyệt OperaGX tự động truyền giá trị date mặc định vào Request Body khi submit mà không hiển thị trên UI. |                                                                                                                                                                               |

**Low**




(Chỉ suy luận logic)

| Môi trường kiểm thử thực thi trên OperaGX. | Chưa tìm được bằng chứng chung loại trừ                                                           | Mở tab Network trên OperaGX, submit 3 lần; kiểm tra Payload. Nếu Payload chứa `dob: "2026-08-09"` -> xác nhận; nếu `dob: ""` hoặc `null` -> bác bỏ. |
| ------------------------------------------ | ------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| **5**                                      | Schema validation ở FE (Zod/Yup/Joi) định nghĩa trường `dob` là `.optional()` hoặc `.nullable()`. |                                                                                                                                                     |

**Low**




(Chỉ suy luận logic)

| Form cho phép submit thành công sang bước xử lý API. | Chưa tìm được bằng chứng chung loại trừ | Kiểm tra file schema validation của Form Candidate: chạy unit test validate schema với object `{ dob: "" }` 1 lần; nếu kết quả `success = true` -> xác nhận schema FE cấu hình sai. |
| ---------------------------------------------------- | --------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

### 2. BUG-UC06-002 – Bỏ trống Address vẫn tạo được Candidate

| **Rank** | **Hypothesis**                                                                                                | **Xác suất + lý do** | **Evidence ỦNG HỘ** | **Evidence LOẠI TRỪ** | **Cách verify (đo được)** |
| -------- | ------------------------------------------------------------------------------------------------------------- | -------------------- | ------------------- | --------------------- | ------------------------- |
| **1**    | Cả FE và BE đều thiếu quy tắc kiểm tra bắt buộc (`required` / `@NotBlank`) đối với trường TextboxC (Address). |                      |                     |                       |                           |

**Medium**




(Có 1 evidence trực tiếp)

| Candidate vẫn được tạo thành công và hiển thị thông báo thành công. | Chưa tìm được bằng chứng chung loại trừ                                                                       | Gửi API `POST /api/candidates` qua Postman không truyền field `address` 5 lần: nếu 5/5 lần trả về `201 Created` -> xác nhận BE thiếu validation. |
| ------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| **2**                                                               | FE xử lý trim chuỗi rỗng thành `""` và BE coi `""` là chuỗi hợp lệ (chỉ dùng `@NotNull` thay vì `@NotBlank`). |                                                                                                                                                  |

**Low**




(Chỉ suy luận logic)

| Form submit thành công không kích hoạt thông báo `ME002`. | Chưa tìm được bằng chứng chung loại trừ                         | Kiểm tra Request Payload 3 lần: nếu payload gửi `address: ""` và BE trả HTTP 200/201 -> xác nhận BE dùng sai annotation validation. |
| --------------------------------------------------------- | --------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| **3**                                                     | Mảng cấu hình `requiredFields` trên UI bị bỏ sót key `address`. |                                                                                                                                     |

**Low**




(Chỉ suy luận logic)

| Trường Address không hiển thị cảnh báo đỏ khi Submit. | Chưa tìm được bằng chứng chung loại trừ                                                              | Kiểm tra source code FE component Form Candidate: xem mảng `rules` của `TextboxC`, nếu không có `required: true` -> xác nhận FE thiếu configuration. |
| ----------------------------------------------------- | ---------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| **4**                                                 | DB Schema quy định cột `address` là `NULLABLE` và BE Service layer không thực hiện validation logic. |                                                                                                                                                      |

**Low**




(Chỉ suy luận logic)

| Database chấp nhận lưu bản ghi candidate mới. | Chưa tìm được bằng chứng chung loại trừ                                           | Kiểm tra DDL của bảng `candidates` trong DB 1 lần: nếu cột `address` có thuộc tính `NULL` và không có DB Constraint -> xác nhận DB chấp nhận rỗng. |
| --------------------------------------------- | --------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| **5**                                         | API Endpoint tạo Candidate gọi sai Service method (gọi method bypass validation). |                                                                                                                                                    |

**Low**




(Chỉ suy luận logic)

| Candidate được tạo thành công trong DB. | Chưa tìm được bằng chứng chung loại trừ | Bật Debug Log BE server, thực hiện submit 3 lần: kiểm tra Controller gọi `CandidateService.create()` có đi qua Validation Interceptor hay không. |
| --------------------------------------- | --------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ |

### 3. BUG-UC06-003 – Không upload CV Attachment vẫn tạo được Candidate

| **Rank** | **Hypothesis**                                                                           | **Xác suất + lý do** | **Evidence ỦNG HỘ** | **Evidence LOẠI TRỪ** | **Cách verify (đo được)** |
| -------- | ---------------------------------------------------------------------------------------- | -------------------- | ------------------- | --------------------- | ------------------------- |
| **1**    | Input control `UploadA` thiếu validation check bắt buộc chọn file trước khi submit ở FE. |                      |                     |                       |                           |

**Medium**




(Có 1 evidence trực tiếp)

| Candidate được tạo mà không có file CV đính kèm. | Chưa tìm được bằng chứng chung loại trừ                                                                     | Nhấn Submit trên UI khi chưa chọn file 3 lần; quan sát tab Network xem request `multipart/form-data` có gửi đi không. Nếu request vẫn gửi đi -> xác nhận FE không chặn. |
| ------------------------------------------------ | ----------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **2**                                            | API Controller nhận param file với `@RequestPart(required = false)` hoặc `@RequestParam(required = false)`. |                                                                                                                                                                         |

**Low**




(Chỉ suy luận logic)

| BE trả về kết quả thành công mà không báo lỗi thiếu file. | Chưa tìm được bằng chứng chung loại trừ                                                                                                                    | Gọi API `POST /api/candidates` qua Postman không gửi part `file` 5 lần: nếu 5/5 lần trả status 201 -> xác nhận BE khai báo param `required = false`. |
| --------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| **3**                                                     | BE Controller khởi tạo và lưu bản ghi Candidate trước khi kiểm tra file upload, khi không có file thì bỏ qua bước save file mà không rollback transaction. |                                                                                                                                                      |

**Low**




(Chỉ suy luận logic)

| Bản ghi Candidate tồn tại trong DB nhưng không có đường dẫn CV. | Chưa tìm được bằng chứng chung loại trừ                                                     | Query DB sau khi submit rỗng CV 3 lần: kiểm tra bản ghi candidate vừa tạo có `cv_url = NULL` -> xác nhận BE không rollback. |
| --------------------------------------------------------------- | ------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------- |
| **4**                                                           | Thư viện Upload ở FE tự động gửi một dummy Blob/File 0-byte khi người dùng không chọn file. |                                                                                                                             |

**Low**




(Chỉ suy luận logic)

| Form bypass qua bước check empty ở client. | Chưa tìm được bằng chứng chung loại trừ                                              | Inspect object `FormData` trong console trước khi gửi 3 lần: nếu `formData.get('file')` tồn tại với `size = 0` -> xác nhận FE gửi file rỗng. |
| ------------------------------------------ | ------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------- |
| **5**                                      | Trình duyệt OperaGX không trigger đúng event `onChange` cho component custom upload. |                                                                                                                                              |

**Low**




(Chỉ suy luận logic)

| Môi trường test thực thi trên OperaGX. | Chưa tìm được bằng chứng chung loại trừ | Chạy lại test case trên Chrome và Firefox 3 lần: nếu Chrome/Firefox hiển thị cảnh báo `Required field` -> xác nhận lỗi tương thích OperaGX; nếu cũng bị lỗi -> bác bỏ. |
| -------------------------------------- | --------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

### 4. BUG-UC06-004 – Không giới hạn/chặn khi nhập Note > 500 ký tự

| **Rank** | **Hypothesis**                                                                                            | **Xác suất + lý do** | **Evidence ỦNG HỘ** | **Evidence LOẠI TRỪ** | **Cách verify (đo được)** |
| -------- | --------------------------------------------------------------------------------------------------------- | -------------------- | ------------------- | --------------------- | ------------------------- |
| **1**    | Control `TextboxF` thiếu thuộc tính `maxlength="500"` ở FE và DTO BE thiếu annotation `@Size(max = 500)`. |                      |                     |                       |                           |

**Medium**




(Có 1 evidence trực tiếp)

| Nhập 501 ký tự vẫn submit thành công và tạo candidate. | Chưa tìm được bằng chứng chung loại trừ                                                                  | Inspect HTML element `Note`: nếu không có `maxlength="500"` -> xác nhận FE thiếu. Gọi API gửi `note` 501 ký tự 5 lần qua Postman: nếu 5/5 lần trả HTTP 201 -> xác nhận BE thiếu validation. |
| ------------------------------------------------------ | -------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **2**                                                  | FE chỉ hiển thị counter warning (vd: `501/500`) nhưng không disable input và không prevent event submit. |                                                                                                                                                                                             |

**Low**




(Chỉ suy luận logic)

| Ký tự 501 vẫn nhập được và nút Submit vẫn hoạt động. | Chưa tìm được bằng chứng chung loại trừ                                                                                                           | Nhập 501 ký tự trên UI 3 lần: nếu counter báo màu đỏ/vượt ngưỡng nhưng nút Submit vẫn bấm được và gửi request -> xác nhận logic FE không block. |
| ---------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| **3**                                                | Cột `note` trong Database là `VARCHAR(500)` nhưng DB Server bị tắt Strict Mode, tự động cắt (truncate) chuỗi về 500 ký tự mà không ném exception. |                                                                                                                                                 |

**Low**




(Chỉ suy luận logic)

| Hệ thống không báo lỗi HTTP 500 Data Truncation khi submit. | Chưa tìm được bằng chứng chung loại trừ                                                                           | Submit note 510 ký tự, query DB check độ dài chuỗi (`LENGTH(note)`): nếu bằng 500 -> xác nhận DB truncate; nếu bằng 510 -> bác bỏ. |
| ----------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| **4**                                                       | DB Schema định nghĩa cột `note` dạng `TEXT` hoặc `VARCHAR` > 500, dẫn đến cả BE và DB chấp nhận chuỗi 501+ ký tự. |                                                                                                                                    |

**Low**




(Chỉ suy luận logic)

| Lưu thành công toàn bộ chuỗi ký tự vào hệ thống. | Chưa tìm được bằng chứng chung loại trừ                                              | Kiểm tra Schema DB 1 lần: nếu data type của `note` là `TEXT` hoặc `VARCHAR(1000)` -> xác nhận DB schema không khớp requirement. |
| ------------------------------------------------ | ------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------- |
| **5**                                            | Xử lý sự kiện `onKeyDown` / `onChange` đếm sai ký tự unicode/multibyte trên OperaGX. |                                                                                                                                 |

**Low**




(Chỉ suy luận logic)

| Tester thực hiện kiểm thử trên OperaGX. | Chưa tìm được bằng chứng chung loại trừ | Thực thi test case với 501 ký tự ASCII (`A`) trên cả Chrome và OperaGX 3 lần: nếu cả 2 đều bị -> bác bỏ nghi ngờ do trình duyệt. |
| --------------------------------------- | --------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------- |

### 5. BUG-UC18-005 – Ẩn nút "Send Reminder" ở trang View Schedule Detail

| **Rank** | **Hypothesis**                                                                                                                                  | **Xác suất + lý do** | **Evidence ỦNG HỘ** | **Evidence LOẠI TRỪ** | **Cách verify (đo được)** |
| -------- | ----------------------------------------------------------------------------------------------------------------------------------------------- | -------------------- | ------------------- | --------------------- | ------------------------- |
| **1**    | FE conditional rendering kiểm tra sai role permission key (vd: check `ROLE_HR` thay vì `ROLE_RECRUITER` hoặc không map role `Admin`/`Manager`). |                      |                     |                       |                           |

**High**




(Có 2 evidence trực tiếp: Ảnh screenshot `TC-UC18-FUN-006.png` & URL thực tế `/interviews/9`)

| Screenshot cho thấy giao diện thiếu ButtonD; URL thực tế truy cập đúng lịch phỏng vấn nhưng không render nút. | Chưa tìm được bằng chứng chung loại trừ                                                                                                                                | Đăng nhập lần lượt 3 tài khoản (Recruiter, Manager, Admin), truy cập `/interviews/9` 3 lần: nếu cả 3 lần nút `Send Reminder` không xuất hiện -> kiểm tra code FE render ButtonD. |
| ------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **2**                                                                                                         | Nút `Send Reminder` bị ràng buộc hiển thị theo `Status` của lịch (vd: chỉ hiện khi `Scheduled`), trong khi lịch `#9` đang ở trạng thái khác (`Completed`/`Cancelled`). |                                                                                                                                                                                  |

**Medium**




(Có 1 evidence trực tiếp: URL `/interviews/9` trỏ tới bản ghi cụ thể)

| URL `/interviews/9` chỉ tới 1 record cụ thể có status riêng. | Chưa tìm được bằng chứng chung loại trừ                                                                                                    | Kiểm tra `Status` của lịch `#9`. Tạo 1 lịch mới trạng thái `Scheduled`, mở view detail 3 lần: nếu nút Send Reminder xuất hiện -> xác nhận nút ẩn/hiện theo Status. |
| ------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **3**                                                        | API GET `/api/interviews/9` trả về object detail thiếu flag `canSendReminder: true` hoặc mảng `allowedActions` không chứa `SEND_REMINDER`. |                                                                                                                                                                    |

**Low**




(Chỉ suy luận logic)

| UI không render nút ButtonD. | Chưa tìm được bằng chứng chung loại trừ                                                                           | Inspect tab Network tại `GET /api/interviews/9` 3 lần: kiểm tra JSON response. Nếu `allowedActions` không có `"SEND_REMINDER"` -> xác nhận do BE response. |
| ---------------------------- | ----------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **4**                        | FE đang render nhầm layout Màn hình 2 (dành cho Interviewer) cho tất cả các role thay vì Màn hình 1 (Role A/B/C). |                                                                                                                                                            |

**Low**




(Chỉ suy luận logic)

| Màn hình 2 theo spec UC18 không có ButtonD (`Send Reminder`). | Chưa tìm được bằng chứng chung loại trừ                                        | So sánh các field trên giao diện `/interviews/9` với spec Màn hình 2: nếu xuất hiện button `Submit result` và thiếu `Recruiter owner` -> xác nhận FE render nhầm Màn hình 2. |
| ------------------------------------------------------------- | ------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **5**                                                         | Tài khoản test thực tế bị gán thiếu Role Claims trong JWT Token khi đăng nhập. |                                                                                                                                                                              |

**Low**




(Chỉ suy luận logic)

| Môi trường test dùng tài khoản cụ thể. | Chưa tìm được bằng chứng chung loại trừ | Decode JWT token của user đăng nhập trong LocalStorage 1 lần: kiểm tra array `roles`. Nếu không có `HR`, `MANAGER` hoặc `ADMIN` -> xác nhận do data test. |
| -------------------------------------- | --------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |

### 6. BUG-UC18-002 – Breadcrumb trên View Detail dẫn tới trang 404 Not Found

| **Rank** | **Hypothesis**                                                                                                               | **Xác suất + lý do** | **Evidence ỦNG HỘ** | **Evidence LOẠI TRỪ** | **Cách verify (đo được)** |
| -------- | ---------------------------------------------------------------------------------------------------------------------------- | -------------------- | ------------------- | --------------------- | ------------------------- |
| **1**    | FE Router gán sai thuộc tính `href` / `to` trên Breadcrumb component (vd: gán `/interview-schedules` thay vì `/interviews`). |                      |                     |                       |                           |

**Medium**




(Có 1 evidence trực tiếp: Ảnh screenshot `00126cd4...png` thể hiện trang 404)

| Trình duyệt chuyển sang 404 Not Found ngay sau khi click Breadcrumb. | Chưa tìm được bằng chứng chung loại trừ                                                                                                                              | Hover & Inspect element Breadcrumb "Interview Schedule List" 1 lần: đọc `href`/`to`. Nếu path target khác URL danh sách thực tế -> xác nhận FE routing hardcode sai URL. |
| -------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **2**                                                                | Nút Breadcrumb dùng relative path thay vì absolute path (vd: `href="interviews"` thay vì `href="/interviews"`), dẫn đến URL bị nối thành `/interviews/9/interviews`. |                                                                                                                                                                          |

**Low**




(Chỉ suy luận logic)

| Lỗi xảy ra khi điều hướng từ trang detail `/interviews/9`. | Chưa tìm được bằng chứng chung loại trừ                                                                                                    | Click Breadcrumb 3 lần; kiểm tra thanh địa chỉ trình duyệt: nếu URL biến thành `http://.../interviews/9/interviews` -> xác nhận do relative path thiếu dấu `/` ở đầu. |
| ---------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **3**                                                      | Web Server (Nginx/CloudFront) thiếu cấu hình Fallback Rewrite Rule (`try_files $uri $uri/ /index.html`) cho Single Page Application (SPA). |                                                                                                                                                                       |

**Low**




(Chỉ suy luận logic)

| Màn hình trả về trang 404 của Web Server. | Chưa tìm được bằng chứng chung loại trừ                                                                                   | Nhập trực tiếp URL trang danh sách lên thanh địa chỉ trình duyệt và Enter 3 lần: nếu trả về 404 Nginx -> xác nhận do Web Server missing SPA rewrite rule. |
| ----------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **4**                                     | Breadcrumb link truyền kèm query params bị `undefined` (vd: `/interviews?page=undefined`) khiến router không match route. |                                                                                                                                                           |

**Low**




(Chỉ suy luận logic)

| Trang bị chuyển hướng 404. | Chưa tìm được bằng chứng chung loại trừ                                                                                | Click Breadcrumb 3 lần, kiểm tra URL khi bị 404: nếu chứa `undefined` hoặc `null` -> xác nhận state management truyền params sai. |
| -------------------------- | ---------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| **5**                      | Route path trong React/Vue Router bị thay đổi tên sau đợt refactor code nhưng chưa cập nhật ở component `BreadcrumbA`. |                                                                                                                                   |

**Low**




(Chỉ suy luận logic)

| Màn hình hiển thị lỗi điều hướng. | Chưa tìm được bằng chứng chung loại trừ | So sánh path định nghĩa trang danh sách trong file route config với path gán trong `BreadcrumbA.tsx` 1 lần -> xác nhận mismatch. |
| --------------------------------- | --------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------- |