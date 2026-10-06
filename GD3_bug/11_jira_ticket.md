# 11 – Jira Ticket

## 1. BUG-UC06-001 – Candidate vẫn được tạo thành công khi bỏ trống D.O.B

**Type:** Bug common  
**Module:** UC06 – Candidate

### Mô tả

Hệ thống cho phép tạo candidate mới ngay cả khi bỏ trống trường bắt buộc D.O.B (Ngày sinh), gây sai lệch dữ liệu hồ sơ ứng viên.

### Steps to Reproduce

1. Đăng nhập vào hệ thống với quyền Admin/Manager/Recruiter.
2. Ở màn hình chính bấm **Candidate** ở thanh công cụ bên trái.
3. Bấm biểu tượng **+ (Create candidate)**.
4. Để trống trường **D.O.B**, nhập hợp lệ các trường còn lại.
5. Nhấn **Submit**.

### Expected Result

Hệ thống chặn tạo candidate và hiển thị thông báo **"ME002 – Required field"** theo **BRL-6-01**.

### Actual Result

Candidate được tạo thành công, hiển thị thông báo **"Successfully created candidate"**.

### Traceability

- **Test Case:** `TC-UC06-FUN-006`
- **Requirement:** UC06 – D.O.B
- **Business Rule:** `BRL-6-01`

---

## 2. BUG-UC06-002 – Candidate vẫn được tạo thành công khi bỏ trống Address

**Type:** Bug common  
**Module:** UC06 – Candidate

### Mô tả

Hệ thống cho phép tạo candidate mới khi không nhập thông tin **Address** (trường bắt buộc), vi phạm quy tắc nghiệp vụ **BRL-6-01**.

### Steps to Reproduce

1. Đăng nhập vào hệ thống với quyền Admin/Manager/Recruiter.
2. Ở màn hình chính bấm **Candidate** ở thanh công cụ bên trái.
3. Bấm biểu tượng **+ (Create candidate)**.
4. Để trống trường **Address**, nhập hợp lệ các trường còn lại.
5. Nhấn **Submit**.

### Expected Result

Hệ thống chặn tạo candidate và hiển thị thông báo **"ME002 – Required field"** theo **BRL-6-01**.

### Actual Result

Candidate được tạo thành công, hiển thị thông báo **"Successfully created candidate"**.

### Traceability

- **Test Case:** `TC-UC06-FUN-008`
- **Requirement:** UC06 Field 9 (`TextboxC`)
- **Business Rule:** `BRL-6-01`

---

## 3. BUG-UC06-003 – Candidate vẫn được tạo thành công khi không upload file CV Attachment

**Type:** Bug  
**Module:** UC06 – Candidate

### Mô tả

Hệ thống bỏ qua điều kiện bắt buộc upload **CV Attachment**, dẫn đến việc hồ sơ candidate được lưu mà không có tệp CV đi kèm.

### Steps to Reproduce

1. Đăng nhập vào hệ thống với quyền Admin/Manager/Recruiter.
2. Ở màn hình chính bấm **Candidate** ở thanh công cụ bên trái.
3. Bấm biểu tượng **+ (Create candidate)**.
4. Để trống trường **CV**, nhập hợp lệ các trường còn lại.
5. Nhấn **Submit**.

### Expected Result

Hệ thống chặn tạo candidate và hiển thị thông báo **"ME002 – Required field"** theo **BRL-6-01**.

### Actual Result

Candidate được tạo thành công, hiển thị thông báo **"Successfully created candidate"**.

### Traceability

- **Test Case:** `TC-UC06-FUN-010`
- **Requirement:** UC06 Field 13 (`UploadA`)
- **Business Rule:** `BRL-6-01`

---

## 4. BUG-UC06-004 – Trường Note nhận quá 500 ký tự và tạo candidate thành công

**Type:** Bug  
**Module:** UC06 – Candidate

### Mô tả

Trường **Note** cho phép nhập và gửi ký tự thứ 501+ mà không bị giới hạn hoặc báo lỗi, trái với quy định tối đa **500 ký tự**.

### Steps to Reproduce

1. Đăng nhập vào hệ thống với quyền Admin/Manager/Recruiter.
2. Bấm vào **Candidate**, sau đó bấm biểu tượng **+ (Create candidate)**.
3. Điền trường Note bằng 501 ký tự. Dán đoạn văn bản đã dùng để kiểm tra.
4. Nhấn **Submit**.

### Expected Result

Giới hạn không cho nhập quá **500 ký tự** hoặc báo lỗi **Failed to create candidate** nếu submit dữ liệu vượt quá 500 ký tự.

### Actual Result

Vẫn nhập được ký tự 501+ và thông báo tạo candidate thành công.

### Traceability

- **Test Case:** `TC-UC06-FUN-018`
- **Requirement:** UC06 – Note
- **Business Rule:** Giới hạn Note tối đa 500 ký tự

---

## 5. BUG-UC18-001 – Màn hình View Detail không hiển thị nút Send Reminder

**Type:** Bug  
**Module:** UC18 – Interview Schedule

### Mô tả

Nút **"Send Reminder"** không xuất hiện trên màn hình xem chi tiết lịch phỏng vấn khi đăng nhập bằng role **HR/Manager/Admin**, ngăn cản việc gửi nhắc lịch phỏng vấn (**UC22**).

### Steps to Reproduce

1. Đăng nhập với quyền Admin/Manager.
2. Mở **View Schedule Detail** tại URL:
   `http://ec2-15-134-127-135.ap-southeast-2.compute.amazonaws.com/interviews/9`
3. Hoặc bấm **Interview** rồi chọn bất kỳ Interview nào.
4. Kiểm tra các action button trên màn hình Interview Schedule Details.

### Expected Result

Nút **"Send Reminder"** hiển thị rõ ràng trên giao diện theo **BR-UC18-001**.

### Actual Result

Nút **"Send Reminder"** bị ẩn/không xuất hiện.

### Traceability

- **Test Case:** `TC-UC18-FUN-006`
- **Requirement:** UC18 – Send Reminder
- **Business Rule:** `BR-UC18-001`
- **Related Use Case:** `UC22 – Send Reminder`

---

## 6. BUG-UC18-002 – Click Breadcrumb "Interview Schedule List" trả về 404 Not Found

**Type:** Bug  
**Module:** UC18 – Interview Schedule

### Mô tả

Khi nhấn vào breadcrumb **"Interview Schedule List"** tại màn hình chi tiết lịch phỏng vấn, hệ thống chuyển hướng người dùng đến trang lỗi **404 Not Found** thay vì quay về danh sách lịch.

### Steps to Reproduce

1. Đăng nhập vào tài khoản với quyền Admin/Manager/Recruiter/Interviewer.
2. Bấm **Interview**, sau đó chọn bất kỳ một Interview → **Interview Schedule Details**.
3. Bấm vào breadcrumb **Interview Schedule List**.

### Expected Result

Chuyển người dùng về màn hình **Interview Schedule List**.

### Actual Result

Hiển thị trang **404 Not Found**. URL trang về `/inteviews`.

### Traceability

- **Test Case:** `TC-UC18-FUN-001`
- **Requirement:** UC18 Field 2 (`BreadcrumbA`)
