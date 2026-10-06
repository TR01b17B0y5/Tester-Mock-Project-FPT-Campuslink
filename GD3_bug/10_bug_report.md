# Bug Reports

### A. BUG REPORT

#### A1. Thông tin định danh

- **Bug ID:** `BUG-UC06-001`
- **Title:** Tạo candidate thành công khi để trống trường D.O.B
- **Reported by:** QA Team
- **Reported Date:** 09/08/2026
- **Status:** New

#### A2. Phân loại

- **Severity:** Major *(đề xuất — chờ người chốt)*
- **Priority:** P1 *(đề xuất — chờ người chốt)*
- **Bug Type:** Functional / Data
- **Component:** UC-06 / Candidate / Create Candidate
- **Affects Version:** N/A — cần bổ sung

#### A3. Môi trường

- **Environment:** Staging / Test
- **Build version:** N/A — cần bổ sung
- **OS / Device:** N/A — cần bổ sung
- **Browser:** OperaGX
- **Cấu hình liên quan:** N/A — cần bổ sung
- **Test data dùng:** N/A — cần bổ sung

#### A4. Mô tả lỗi

- **Preconditions:** User đã đăng nhập hệ thống với quyền tạo candidate (Role A/B/C).
- **Steps to Reproduce:**
  1. Mở màn hình Create Candidate (`UC-06`).
  2. Để trống trường D.O.B (Date of Birth).
  3. Điền đầy đủ thông tin hợp lệ vào các trường khác.
  4. Nhấn **Submit** (ButtonA).
- **Repro Rate:** `1/1` *(cần bổ sung số liệu kiểm thử mở rộng)*
- **Expected Result:** Hệ thống không cho phép tạo candidate và hiển thị thông báo lỗi **ME002 – Required field** tại trường D.O.B (theo Business Rule `BRL-6-01` & Screen Component `DateA`).
- **Actual Result:** Candidate vẫn được tạo thành công vào hệ thống. Màn hình hiển thị thông báo **Successfully created candidate** (`ME012`).

#### A5. Evidence

- **Screenshot / Video:** `screenshots/TC-UC06-FUN-006.png`
- **Log / Stack trace:** `THIẾU EVIDENCE: Log server/Console log`
- **Request / Response:** `THIẾU EVIDENCE: Request/Response payload (Network Log DevTools)`
- **DB / State:** `THIẾU EVIDENCE: Trạng thái bản ghi lưu trong DB`
- **Evidence còn thiếu:** URL môi trường kiểm thử, Network Log khi Submit, giá trị thực tế trong DB.

#### A6. Root Cause

- **Root cause đã verify:** `[CHƯA VERIFY]` *(Chưa có dữ liệu kiểm chứng thực nghiệm từ người dùng)*
- **Cách verify:** `[CHƯA VERIFY]` *(Cần gửi API POST /api/candidates thiếu field dob 5 lần để xác nhận)*
- **Số liệu verify:** `[CHƯA VERIFY]`
- **Giả thuyết bị loại trừ:** `[CHƯA VERIFY]`

#### A7. Trace

- **Test Case ID:** `TC-UC06-FUN-006`
- **Requirement / AC:** UC06 Screen Component field 8 (`DateA`), Business Rule `BRL-6-01`
- **Related bugs:** N/A — cần bổ sung

#### A8. Suggested Fix (đề xuất từ QA)

1. **FE:** Thêm rule `required` bắt buộc chọn/nhập D.O.B trước khi trigger event Submit.
2. **BE:** Bổ sung Validation Annotation `@NotNull` / `@NotBlank` cho DTO field `dob`.


### A. BUG REPORT

#### A1. Thông tin định danh

- **Bug ID:** `BUG-UC06-002`
- **Title:** Tạo candidate thành công khi để trống trường Address
- **Reported by:** QA Team
- **Reported Date:** 09/08/2026
- **Status:** New

#### A2. Phân loại

- **Severity:** Major *(đề xuất — chờ người chốt)*
- **Priority:** P1 *(đề xuất — chờ người chốt)*
- **Bug Type:** Functional / Data
- **Component:** UC-06 / Candidate / Create Candidate
- **Affects Version:** N/A — cần bổ sung

#### A3. Môi trường

- **Environment:** Staging / Test
- **Build version:** N/A — cần bổ sung
- **OS / Device:** N/A — cần bổ sung
- **Browser:** OperaGX
- **Cấu hình liên quan:** N/A — cần bổ sung
- **Test data dùng:** N/A — cần bổ sung

#### A4. Mô tả lỗi

- **Preconditions:** User đã đăng nhập hệ thống với quyền tạo candidate (Role A/B/C).
- **Steps to Reproduce:**
  1. Mở màn hình Create Candidate (`UC-06`).
  2. Để trống trường Address.
  3. Điền đầy đủ thông tin hợp lệ vào các trường khác.
  4. Nhấn **Submit** (ButtonA).
- **Repro Rate:** `1/1` *(cần bổ sung số liệu kiểm thử mở rộng)*
- **Expected Result:** Hệ thống báo lỗi **ME002 – Required field**; candidate không được tạo (theo Business Rule `BRL-6-01` & Screen Component `TextboxC`).
- **Actual Result:** Candidate vẫn được tạo thành công dù để trống trường Address. Hiển thị thông báo success created candidate.

#### A5. Evidence

- **Screenshot / Video:** `THIẾU EVIDENCE: Ảnh chụp màn hình TC-UC06-FUN-008.png`
- **Log / Stack trace:** `THIẾU EVIDENCE: Log server/Console log`
- **Request / Response:** `THIẾU EVIDENCE: API Request/Response payload`
- **DB / State:** `THIẾU EVIDENCE: Trạng thái bản ghi lưu trong DB`
- **Evidence còn thiếu:** Screenshot, URL môi trường, Network log, DB state.

#### A6. Root Cause

- **Root cause đã verify:** `[CHƯA VERIFY]` *(Chưa có dữ liệu kiểm chứng thực nghiệm từ người dùng)*
- **Cách verify:** `[CHƯA VERIFY]` *(Cần gửi API POST không truyền field address 5 lần để xác nhận)*
- **Số liệu verify:** `[CHƯA VERIFY]`
- **Giả thuyết bị loại trừ:** `[CHƯA VERIFY]`

#### A7. Trace

- **Test Case ID:** `TC-UC06-FUN-008`
- **Requirement / AC:** UC06 Screen Component field 9 (`TextboxC`), Business Rule `BRL-6-01`
- **Related bugs:** N/A — cần bổ sung

#### A8. Suggested Fix (đề xuất từ QA)

1. **FE:** Bổ sung validation rule `required` cho input `TextboxC`.
2. **BE:** Khai báo constraint `@NotBlank` cho field `address` trong DTO.


### A. BUG REPORT

#### A1. Thông tin định danh

- **Bug ID:** `BUG-UC06-003`
- **Title:** Tạo candidate thành công khi không upload CV Attachment
- **Reported by:** QA Team
- **Reported Date:** 09/08/2026
- **Status:** New

#### A2. Phân loại

- **Severity:** Critical *(đề xuất — chờ người chốt)*
- **Priority:** P1 *(đề xuất — chờ người chốt)*
- **Bug Type:** Functional / File Handling
- **Component:** UC-06 / Candidate / Create Candidate
- **Affects Version:** N/A — cần bổ sung

#### A3. Môi trường

- **Environment:** Staging / Test
- **Build version:** N/A — cần bổ sung
- **OS / Device:** N/A — cần bổ sung
- **Browser:** OperaGX
- **Cấu hình liên quan:** N/A — cần bổ sung
- **Test data dùng:** N/A — cần bổ sung

#### A4. Mô tả lỗi

- **Preconditions:** User đã đăng nhập hệ thống với quyền tạo candidate (Role A/B/C).
- **Steps to Reproduce:**
  1. Mở màn hình Create Candidate (`UC-06`).
  2. Không đính kèm/upload file CV Attachment (`UploadA`).
  3. Điền đầy đủ thông tin vào các field bắt buộc khác.
  4. Nhấn **Submit** (ButtonA).
- **Repro Rate:** `1/1` *(cần bổ sung số liệu kiểm thử mở rộng)*
- **Expected Result:** Hệ thống thông báo lỗi **Required field**; candidate không được tạo (theo Business Rule `BRL-6-01` & Screen Component `UploadA`).
- **Actual Result:** Candidate vẫn được tạo thành công dù chưa upload CV. Màn hình hiển thị thông báo success created candidate.

#### A5. Evidence

- **Screenshot / Video:** `THIẾU EVIDENCE: Ảnh chụp màn hình TC-UC06-FUN-010.png`
- **Log / Stack trace:** `THIẾU EVIDENCE: Log server/Console log`
- **Request / Response:** `THIẾU EVIDENCE: Multipart form-data Request`
- **DB / State:** `THIẾU EVIDENCE: Trạng thái bản ghi cv_url trong DB`
- **Evidence còn thiếu:** Screenshot, URL môi trường, Multipart Request Log.

#### A6. Root Cause

- **Root cause đã verify:** `[CHƯA VERIFY]` *(Chưa có dữ liệu kiểm chứng thực nghiệm từ người dùng)*
- **Cách verify:** `[CHƯA VERIFY]` *(Cần test gọi API multipart không đính kèm file 5 lần để xác nhận)*
- **Số liệu verify:** `[CHƯA VERIFY]`
- **Giả thuyết bị loại trừ:** `[CHƯA VERIFY]`

#### A7. Trace

- **Test Case ID:** `TC-UC06-FUN-010`
- **Requirement / AC:** UC06 Screen Component field 13 (`UploadA`), Business Rule `BRL-6-01`
- **Related bugs:** N/A — cần bổ sung

#### A8. Suggested Fix (đề xuất từ QA)

1. **FE:** Bổ sung validation kiểm tra đối tượng file đính kèm trước khi cho phép Submit.
2. **BE:** Yêu cầu MultipartFile param bắt buộc (`@RequestPart("file") MultipartFile file` không đặt `required = false`).


### A. BUG REPORT

#### A1. Thông tin định danh

- **Bug ID:** `BUG-UC06-004`
- **Title:** Tạo candidate thành công khi nhập Note vượt quá 500 ký tự
- **Reported by:** QA Team
- **Reported Date:** 09/08/2026
- **Status:** New

#### A2. Phân loại

- **Severity:** Minor *(đề xuất — chờ người chốt)*
- **Priority:** P2 *(đề xuất — chờ người chốt)*
- **Bug Type:** Functional / Boundary Validation
- **Component:** UC-06 / Candidate / Create Candidate
- **Affects Version:** N/A — cần bổ sung

#### A3. Môi trường

- **Environment:** Staging / Test
- **Build version:** N/A — cần bổ sung
- **OS / Device:** N/A — cần bổ sung
- **Browser:** OperaGX
- **Cấu hình liên quan:** N/A — cần bổ sung
- **Test data dùng:** N/A — cần bổ sung

#### A4. Mô tả lỗi

- **Preconditions:** User đã đăng nhập hệ thống với quyền tạo candidate (Role A/B/C).
- **Steps to Reproduce:**
  1. Mở màn hình Create Candidate (`UC-06`).
  2. Nhập 500 ký tự vào ô Note (`TextboxF`).
  3. Tiếp tục nhập thêm ký tự thứ 501 vào ô Note.
  4. Nhấn **Submit** (ButtonA).
- **Repro Rate:** `1/1` *(cần bổ sung số liệu kiểm thử mở rộng)*
- **Expected Result:** Khung nhập chỉ chấp nhận tối đa 500 ký tự; ký tự thứ 501 không thể nhập được. Nếu cố tình gửi > 500 ký tự, hệ thống hiển thị thông báo lỗi **ME011 – Failed to create candidate** (theo Screen Component `TextboxF` & `TC-UC06-FUN-018`).
- **Actual Result:** Ký tự thứ 501 vẫn nhập được bình thường, hệ thống tạo candidate thành công và hiển thị thông báo success to created candidate.

#### A5. Evidence

- **Screenshot / Video:** `THIẾU EVIDENCE: Ảnh chụp màn hình TC-UC06-FUN-018.png`
- **Log / Stack trace:** `THIẾU EVIDENCE: Log server/Console log`
- **Request / Response:** `THIẾU EVIDENCE: Request Body (Note field content)`
- **DB / State:** `THIẾU EVIDENCE: Chiều dài thực tế chuỗi note trong DB`
- **Evidence còn thiếu:** Screenshot, URL môi trường, Chuỗi ký tự test thực tế.

#### A6. Root Cause

- **Root cause đã verify:** `[CHƯA VERIFY]` *(Chưa có dữ liệu kiểm chứng thực nghiệm từ người dùng)*
- **Cách verify:** `[CHƯA VERIFY]` *(Cần inspect element FE xem maxlength và test API payload note 501 ký tự 5 lần)*
- **Số liệu verify:** `[CHƯA VERIFY]`
- **Giả thuyết bị loại trừ:** `[CHƯA VERIFY]`

#### A7. Trace

- **Test Case ID:** `TC-UC06-FUN-018`
- **Requirement / AC:** UC06 Screen Component field 21 (`TextboxF`)
- **Related bugs:** N/A — cần bổ sung

#### A8. Suggested Fix (đề xuất từ QA)

1. **FE:** Bổ sung thuộc tính `maxlength="500"` cho control `TextboxF`.
2. **BE:** Thêm validation `@Size(max = 500)` cho field `note` trong DTO.


### A. BUG REPORT

#### A1. Thông tin định danh

- **Bug ID:** `BUG-UC18-005`
- **Title:** Không hiển thị nút Send Reminder ở trang View Schedule Detail đối với HR/Manager/Admin
- **Reported by:** QA Team
- **Reported Date:** 09/08/2026
- **Status:** New

#### A2. Phân loại

- **Severity:** Major *(đề xuất — chờ người chốt)*
- **Priority:** P2 *(đề xuất — chờ người chốt)*
- **Bug Type:** Functional / UI Access Control
- **Component:** UC18 / Interview Schedule / View Schedule Details
- **Affects Version:** N/A — cần bổ sung

#### A3. Môi trường

- **Environment:** Staging / AWS EC2
- **Build version:** N/A — cần bổ sung
- **OS / Device:** N/A — cần bổ sung
- **Browser:** OperaGX
- **Cấu hình liên quan:** URL `[http://ec2-15-134-127-135.ap-southeast-2.compute.amazonaws.com/interviews/9](http://ec2-15-134-127-135.ap-southeast-2.compute.amazonaws.com/interviews/9)`
- **Test data dùng:** Tài khoản thuộc role HR / Manager / Admin

#### A4. Mô tả lỗi

- **Preconditions:** User đăng nhập hệ thống với quyền HR/Manager/Admin và đã có lịch phỏng vấn ID `#9`.
- **Steps to Reproduce:**
  1. Đăng nhập với tài khoản role HR/Manager/Admin.
  2. Mở danh sách lịch phỏng vấn và bấm View lịch phỏng vấn `#9` (hoặc truy cập trực tiếp URL).
  3. Quan sát các nút chức năng trên màn hình View Schedule Detail.
- **Repro Rate:** `1/1` *(cần bổ sung số liệu kiểm thử mở rộng)*
- **Expected Result:** Nút **Send Reminder** (`ButtonD`) xuất hiện trên giao diện để người dùng kích hoạt gửi nhắc lịch (trigger UC22) (theo Business Rule `BR-UC18-001` & Screen Component `ButtonD`).
- **Actual Result:** Không thấy nút **Send Reminder** xuất hiện ở màn hình View Schedule Detail.

#### A5. Evidence

- **Screenshot / Video:** `screenshots/TC-UC18-FUN-006.png`
- **Log / Stack trace:** `THIẾU EVIDENCE: Console log/BE log`
- **Request / Response:** `THIẾU EVIDENCE: Response JSON của GET /interviews/9`
- **DB / State:** `THIẾU EVIDENCE: Status của record schedule #9 trong DB`
- **Evidence còn thiếu:** Username/Role chính xác dùng khi test, API GET Response.

#### A6. Root Cause

- **Root cause đã verify:** `[CHƯA VERIFY]` *(Chưa có dữ liệu kiểm chứng thực nghiệm từ người dùng)*
- **Cách verify:** `[CHƯA VERIFY]` *(Cần test đăng nhập lần lượt 3 role HR, Manager, Admin truy cập /interviews/9 3 lần để xác nhận)*
- **Số liệu verify:** `[CHƯA VERIFY]`
- **Giả thuyết bị loại trừ:** `[CHƯA VERIFY]`

#### A7. Trace

- **Test Case ID:** `TC-UC18-FUN-006`
- **Requirement / AC:** UC18 Screen Component field 23 (`ButtonD`), Business Rule `BR-UC18-001`
- **Related bugs:** N/A — cần bổ sung

#### A8. Suggested Fix (đề xuất từ QA)

1. **FE:** Kiểm tra điều kiện render component `ButtonD` theo đúng role claim (Recruiter/HR, Manager, Admin) trong JWT Token.
2. **BE:** Kiểm tra thuộc tính `canSendReminder` hoặc `allowedActions` trong API response chi tiết lịch phỏng vấn.


### A. BUG REPORT

#### A1. Thông tin định danh

- **Bug ID:** `BUG-UC18-002`
- **Title:** Bấm vào Breadcrumb "Interview Schedule List" bị chuyển hướng sang trang 404 Not Found
- **Reported by:** QA Team
- **Reported Date:** N/A — cần bổ sung
- **Status:** New

#### A2. Phân loại

- **Severity:** Major *(đề xuất — chờ người chốt)*
- **Priority:** P1 *(đề xuất — chờ người chốt)*
- **Bug Type:** Functional / Navigation / Routing
- **Component:** UC18 / Interview Schedule / View Schedule Details
- **Affects Version:** N/A — cần bổ sung

#### A3. Môi trường

- **Environment:** Staging / Test
- **Build version:** N/A — cần bổ sung
- **OS / Device:** N/A — cần bổ sung
- **Browser:** N/A — cần bổ sung
- **Cấu hình liên quan:** N/A — cần bổ sung
- **Test data dùng:** N/A — cần bổ sung

#### A4. Mô tả lỗi

- **Preconditions:** User đã đăng nhập hệ thống bằng quyền Recruiter/Manager/Admin.
- **Steps to Reproduce:**
  1. Mở danh sách lịch phỏng vấn (Interview Schedule List).
  2. Bấm **View** một lịch phỏng vấn bất kỳ để mở Interview Schedule Details.
  3. Tại thanh điều hướng Breadcrumb, nhấn vào liên kết **Interview Schedule List**.
- **Repro Rate:** `1/1` *(cần bổ sung số liệu kiểm thử mở rộng)*
- **Expected Result:** Hệ thống chuyển người dùng quay về màn hình **Interview Schedule List** và hiển thị danh sách các lịch phỏng vấn (theo Screen Component `BreadcrumbA`).
- **Actual Result:** Trình duyệt chuyển hướng đến trang **404 Not Found**.

#### A5. Evidence

- **Screenshot / Video:** `00126cd4-892b-4d13-9a40-78df68be45a6.png`
- **Log / Stack trace:** `THIẾU EVIDENCE: Console error/Router log`
- **Request / Response:** `THIẾU EVIDENCE: Target URL trên liên kết Breadcrumb`
- **DB / State:** N/A
- **Evidence còn thiếu:** Target URL của thẻ `<a>`/Link component, Trình duyệt & Ngày/Giờ thực thi.

#### A6. Root Cause

- **Root cause đã verify:** `[CHƯA VERIFY]` *(Chưa có dữ liệu kiểm chứng thực nghiệm từ người dùng)*
- **Cách verify:** `[CHƯA VERIFY]` *(Cần hover inspect href trên Breadcrumb 1 lần để check routing URL)*
- **Số liệu verify:** `[CHƯA VERIFY]`
- **Giả thuyết bị loại trừ:** `[CHƯA VERIFY]`

#### A7. Trace

- **Test Case ID:** `TC-UC18-FUN-001`
- **Requirement / AC:** UC18 Screen Component field 2 (`BreadcrumbA`)
- **Related bugs:** N/A — cần bổ sung

#### A8. Suggested Fix (đề xuất từ QA)

1. **FE:** Cập nhật đường dẫn điều hướng (`href` / `to`) của Breadcrumb `Interview Schedule List` về đúng route danh sách (ví dụ: `/interviews` hoặc `/interview-schedules`).
