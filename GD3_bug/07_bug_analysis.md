# Bug Analysis

## 1. BUG-UC06-001: Bỏ trống D.O.B vẫn tạo được Candidate

### Timeline sự kiện

-   **09/08/2026:** Tester đăng nhập hệ thống bằng trình duyệt
    **OperaGX**.
-   **Thao tác:** Mở màn hình *Create candidate* → Để trống trường
    **D.O.B** → Nhập thông tin hợp lệ vào các trường còn lại → Nhấn
    **Submit**.
-   **Phản hồi hệ thống:** Tạo candidate thành công, hiển thị thông báo
    **Successfully created candidate** thay vì chặn và báo lỗi **ME002
    -- Required field**.

### Phân loại bug

-   **Category:** Form Validation Logic
-   **Layer nghi vấn:** FE (Form Validation) / BE (Data Annotation / API
    Model Validation)
-   **Type:** Functional

### Đánh giá Impact

-   **Đối tượng ảnh hưởng:** Recruiter / Role A, B, C khi tạo hồ sơ ứng
    viên.
-   **Mức độ:** Sai lệch dữ liệu hồ sơ nhân sự (thiếu ngày sinh), ảnh
    hưởng đến các tính năng lọc/quản lý hồ sơ về sau.

### Tra cứu Test Case & Requirement

-   **Test Case ID:** `TC-UC06-FUN-006`
-   **Requirement liên quan:** UC06 Screen Component field 8 (`DateA` -
    Bắt buộc) & Business Rule `BRL-6-01` (Cần hiển thị lỗi ME002 khi
    thiếu trường bắt buộc).

### Evidence

-   **Ảnh chụp màn hình:** Đã có / đã được ghi nhận trong test
    execution.
-   **THIẾU EVIDENCE: URL môi trường thực thi.**
-   **THIẾU EVIDENCE: API Request/Response payload (Network Log tab
    DevTools) khi bấm Submit.**
-   **THIẾU EVIDENCE: Trạng thái bản ghi lưu trong Database (trường
    `DOB` lưu `NULL` hay giá trị mặc định).**

------------------------------------------------------------------------

## 2. BUG-UC06-002: Bỏ trống Address vẫn tạo được Candidate

### Timeline sự kiện

-   **09/08/2026:** Tester thực thi kịch bản trên trình duyệt
    **OperaGX**.
-   **Thao tác:** Mở *Create candidate* → Để trống trường **Address** →
    Điền các trường bắt buộc khác → Nhấn **Submit**.
-   **Phản hồi hệ thống:** Hệ thống lưu candidate thành công và hiển thị
    thông báo success.

### Phân loại bug

-   **Category:** Form Validation Logic
-   **Layer nghi vấn:** FE / BE
-   **Type:** Functional

### Đánh giá Impact

-   **Đối tượng ảnh hưởng:** Recruiter / User tạo candidate.
-   **Mức độ:** Mất mát thông tin liên lạc bắt buộc của ứng viên.

### Tra cứu Test Case & Requirement

-   **Test Case ID:** `TC-UC06-FUN-008`
-   **Requirement liên quan:** UC06 Screen Component field 9
    (`TextboxC` - Bắt buộc) & Business Rule `BRL-6-01`.

### Evidence

-   **Ảnh chụp màn hình:** `TC-UC06-FUN-008.png` --- Đã có / đã được ghi
    nhận trong test execution.
-   **THIẾU EVIDENCE: URL môi trường thực thi.**
-   **THIẾU EVIDENCE: API Request/Response log khi submit form.**

------------------------------------------------------------------------

## 3. BUG-UC06-003: Không upload CV Attachment vẫn tạo được Candidate

### Timeline sự kiện

-   **09/08/2026:** Tester thực thi kịch bản trên trình duyệt
    **OperaGX**.
-   **Thao tác:** Mở *Create candidate* → Bỏ qua phần upload **CV
    Attachment** → Nhập các trường còn lại → Nhấn **Submit**.
-   **Phản hồi hệ thống:** Hệ thống ghi nhận tạo thành công candidate
    thay vì báo **Required field**.

### Phân loại bug

-   **Category:** File Upload Validation
-   **Layer nghi vấn:** FE (File input requirement check) / BE
    (Multipart file validation)
-   **Type:** Functional

### Đánh giá Impact

-   **Đối tượng ảnh hưởng:** Người dùng quy trình tuyển dụng (Recruiter,
    Interviewer, Manager).
-   **Mức độ:** Nghiêm trọng đến quy trình nghiệp vụ (hồ sơ ứng viên
    không có CV để phỏng vấn/đánh giá).

### Tra cứu Test Case & Requirement

-   **Test Case ID:** `TC-UC06-FUN-010`
-   **Requirement liên quan:** UC06 Screen Component field 13
    (`UploadA` - Bắt buộc) & Business Rule `BRL-6-01`.

### Evidence

-   **Ảnh chụp màn hình:** `TC-UC06-FUN-010.png` --- Đã có / đã được ghi
    nhận trong test execution.
-   **THIẾU EVIDENCE: URL môi trường kiểm thử.**
-   **THIẾU EVIDENCE: Request Header/Payload (`multipart/form-data`) gửi
    lên server.**

------------------------------------------------------------------------

## 4. BUG-UC06-004: Không giới hạn/chặn khi nhập Note vượt quá 500 ký tự

### Timeline sự kiện

-   **09/08/2026:** Tester thực thi kịch bản trên **OperaGX**.
-   **Thao tác:** Mở *Create candidate* → Nhập 500 ký tự vào ô Note →
    Nhập tiếp ký tự thứ 501 → Nhấn **Submit**.
-   **Phản hồi hệ thống:** Hệ thống vẫn nhận ký tự thứ 501+ và thông báo
    tạo candidate thành công.

### Phân loại bug

-   **Category:** Boundary Input Validation
-   **Layer nghi vấn:** FE (Thiếu attribute `maxlength="500"`) / BE
    (Thiếu constraint `@Size(max=500)` hoặc string truncation logic)
-   **Type:** Functional / GUI

### Đánh giá Impact

-   **Đối tượng ảnh hưởng:** Recruiter.
-   **Mức độ:** Có nguy cơ vỡ layout khi hiển thị Note dài, hoặc gây lỗi
    DB Data Truncation (HTTP 500) nếu cột Database bị giới hạn độ dài
    strict.

### Tra cứu Test Case & Requirement

-   **Test Case ID:** `TC-UC06-FUN-018`
-   **Requirement liên quan:** UC06 Screen Component field 21
    (`TextboxF` - Tối đa 500 ký tự).

### Evidence

-   **Ảnh chụp màn hình:** `TC-UC06-FUN-018.png` --- Đã có / đã được ghi
    nhận trong test execution.
-   **THIẾU EVIDENCE: URL thực thi.**
-   **THIẾU EVIDENCE: Chuỗi ký tự thực tế đã gửi trong Request Payload
    và dữ liệu lưu thực tế trong DB.**

------------------------------------------------------------------------

## 5. BUG-UC18-005: Ẩn nút "Send Reminder" ở trang View Schedule Detail

### Timeline sự kiện

-   **09/08/2026:** Tester thực thi trên **OperaGX** tại địa chỉ:
    `http://ec2-15-134-127-135.ap-southeast-2.compute.amazonaws.com/interviews/9`.
-   **Thao tác:** Đăng nhập tài khoản role HR/Manager/Admin → Mở xem chi
    tiết lịch phỏng vấn id `#9`.
-   **Phản hồi hệ thống:** Không tìm thấy nút **Send Reminder** trên
    giao diện chi tiết.

### Phân loại bug

-   **Category:** Role-based Access Control (RBAC) / Component
    Visibility
-   **Layer nghi vấn:** FE (Conditional rendering check sai role) / BE
    (API không trả về permission flag cho action `Send Reminder`)
-   **Type:** Functional / GUI

### Đánh giá Impact

-   **Đối tượng ảnh hưởng:** HR, Manager, Admin.
-   **Mức độ:** Chặn hoàn toàn khả năng kích hoạt quy trình gửi nhắc
    lịch phỏng vấn (UC22).

### Tra cứu Test Case & Requirement

-   **Test Case ID:** `TC-UC18-FUN-006`
-   **Requirement liên quan:** UC18 Screen Component field 23
    (`ButtonD` - Kích hoạt UC22) & Business Rule `BR-UC18-001`.

### Evidence

-   **Ảnh chụp màn hình:** Đã có / đã được ghi nhận trong test
    execution.
-   **URL môi trường:** Đã có ---
    `http://ec2-15-134-127-135.ap-southeast-2.compute.amazonaws.com/interviews/9`.
-   **THIẾU EVIDENCE: Tên tài khoản / Role chính xác đang dùng để đăng
    nhập khi thực hiện test.**
-   **THIẾU EVIDENCE: API Response chi tiết lịch phỏng vấn (kiểm tra
    trường status hoặc user permissions object).**

------------------------------------------------------------------------

## 6. BUG-UC18-002: Breadcrumb trên View Detail dẫn tới trang 404 Not Found

### Timeline sự kiện

-   **Thời gian thực thi:** **THIẾU EVIDENCE: Ngày / giờ thực hiện kiểm
    thử.**
-   **Thao tác:** Đăng nhập tài khoản Recruiter/Manager/Admin → Vào
    *Interview Schedule List* → Bấm **View** một lịch → Tại trang
    Detail, click vào đường dẫn Breadcrumb **Interview Schedule List**.
-   **Phản hồi hệ thống:** Trình duyệt chuyển hướng đến trang **404 Not
    Found**.

### Phân loại bug

-   **Category:** Routing / Broken Link
-   **Layer nghi vấn:** FE (Router path/href attribute của Breadcrumb
    chỉ định sai đường dẫn)
-   **Type:** Navigation

### Đánh giá Impact

-   **Đối tượng ảnh hưởng:** Toàn bộ người dùng sử dụng màn hình UC18.
-   **Mức độ:** Gián đoạn luồng điều hướng, làm giảm trải nghiệm người
    dùng (phải dùng nút Back trình duyệt hoặc chuyển qua menu khác).

### Tra cứu Test Case & Requirement

-   **Test Case ID:** `TC-UC18-FUN-001`
-   **Requirement liên quan:** UC18 Screen Component field 2
    (`BreadcrumbA` - Hiển thị đường dẫn và cho phép click để quay lại
    màn hình list).

### Evidence

-   **Ảnh chụp màn hình:** Đã có / đã được ghi nhận trong test
    execution.
-   **THIẾU EVIDENCE: URL chính xác của trang 404 (giá trị attribute
    `href` trên liên kết breadcrumb).**
-   **THIẾU EVIDENCE: Trình duyệt & Môi trường thực thi.**
-   **THIẾU EVIDENCE: Ngày / giờ thực hiện kiểm thử.**
