# Test Cases — UC06: Create new candidate

## Functionality

| ID | Test Type | Priority | Test Case | Steps | Expected Result |
|---|---|:---:|---|---|---|
| TC-UC06-FUN-001 | Functionality | P1 | Tạo candidate thành công với dữ liệu hợp lệ | 1. Mở Create candidate.<br>2. Nhập toàn bộ field bắt buộc hợp lệ.<br>3. Nhập Note hợp lệ.<br>4. Nhấn Submit. | Candidate được tạo thành công; status tự động = **Open**; hiển thị **ME012**; quay về Candidate list. |
| TC-UC06-FUN-002 | Functionality | P1 | Full name không được bỏ trống | 1. Để trống Full name.<br>2. Điền các field bắt buộc khác.<br>3. Submit. | Hiển thị **ME002 – Required field**; candidate không được tạo. |
| TC-UC06-FUN-003 | Functionality | P1 | Email không được bỏ trống | 1. Để trống Email.<br>2. Điền các field bắt buộc khác.<br>3. Submit. | Hiển thị **ME002 – Required field**; candidate không được tạo. |
| TC-UC06-FUN-004 | Functionality | P1 | Email phải đúng format | 1. Nhập email sai format, ví dụ `abc.com`.<br>2. Điền các field khác hợp lệ.<br>3. Submit. | Hiển thị **ME009 – Invalid email address**; candidate không được tạo. |
| TC-UC06-FUN-005 | Functionality | P1 | Gender là field bắt buộc và có danh sách giá trị hợp lệ | 1. Mở Gender dropdown.<br>2. Kiểm tra các giá trị.<br>3. Để Gender trống.<br>4. Điền các field khác.<br>5. Submit. | Dropdown có **Male, Female, Others**. Nếu bỏ trống Gender, hệ thống hiển thị **ME002** và không tạo candidate. |
| TC-UC06-FUN-006 | Functionality | P1 | D.O.B không được bỏ trống | 1. Để trống D.O.B.<br>2. Điền các field khác.<br>3. Submit. | Hiển thị **ME002 – Required field**; candidate không được tạo. |
| TC-UC06-FUN-007 | Functionality | P1 | D.O.B phải là ngày trong quá khứ | 1. Chọn D.O.B là ngày hiện tại hoặc tương lai.<br>2. Điền các field khác hợp lệ.<br>3. Submit. | Hiển thị **ME010 – Date of Birth must be in the past**; candidate không được tạo. |
| TC-UC06-FUN-008 | Functionality | P1 | Address không được bỏ trống | 1. Để trống Address.<br>2. Điền các field khác.<br>3. Submit. | Hiển thị **ME002**; candidate không được tạo. |
| TC-UC06-FUN-009 | Functionality | P1 | Phone number không được bỏ trống | 1. Để trống Phone number.<br>2. Điền các field khác.<br>3. Submit. | Hiển thị **ME002**; candidate không được tạo. |
| TC-UC06-FUN-010 | Functionality | P1 | CV Attachment là field bắt buộc | 1. Không upload CV.<br>2. Điền các field bắt buộc khác.<br>3. Submit. | Hệ thống báo **Required field**; candidate không được tạo. |
| TC-UC06-FUN-011 | Functionality | P1 | Current position không được bỏ trống | 1. Để trống Current position.<br>2. Điền các field khác.<br>3. Submit. | Hiển thị **ME002**; candidate không được tạo. |
| TC-UC06-FUN-012 | Functionality | P1 | Skills không được bỏ trống | 1. Không chọn Skill.<br>2. Điền các field khác.<br>3. Submit. | Hiển thị **ME002**; candidate không được tạo. |
| TC-UC06-FUN-013 | Functionality | P2 | Skills hỗ trợ chọn nhiều giá trị | 1. Mở Skills.<br>2. Chọn từ hai skill trở lên.<br>3. Điền các field khác hợp lệ.<br>4. Submit. | Có thể chọn nhiều skill; các skill được chọn được hiển thị trong field. |
| TC-UC06-FUN-014 | Functionality | P2 | Years of experience nhận dữ liệu số | 1. Nhập giá trị số vào Years of experience.<br>2. Điền các field khác hợp lệ.<br>3. Submit. | Field chấp nhận giá trị số và không phát sinh lỗi do kiểu dữ liệu. |
| TC-UC06-FUN-015 | Functionality | P1 | Highest level không được bỏ trống | 1. Để trống Highest level.<br>2. Điền các field khác.<br>3. Submit. | Hiển thị **ME002**; candidate không được tạo. |
| TC-UC06-FUN-016 | Functionality | P1 | Recruiter owner không được bỏ trống | 1. Để trống Recruiter owner.<br>2. Điền các field khác.<br>3. Submit. | Hiển thị **ME002**; candidate không được tạo. |
| TC-UC06-FUN-017 | Functionality | P2 | Assign me tự động điền Recruiter owner | 1. Đăng nhập với tài khoản Recruiter.<br>2. Để Recruiter owner trống.<br>3. Nhấn Assign me. | Recruiter owner được tự động điền bằng tài khoản hiện tại. |
| TC-UC06-FUN-018 | Functionality | P2 | Note tối đa 500 ký tự | 1. Nhập đúng 500 ký tự vào Note.<br>2. Nhập thêm ký tự thứ 501. | 500 ký tự được chấp nhận; ký tự thứ 501 không được nhập. |
| TC-UC06-FUN-019 | Functionality | P1 | Submit thất bại hiển thị ME011 | 1. Nhập dữ liệu hợp lệ.<br>2. Giả lập/trigger tình huống hệ thống không thể tạo candidate.<br>3. Nhấn Submit. | Hệ thống hiển thị **ME011 – Failed to create candidate**; candidate không được tạo. |
| TC-UC06-FUN-020 | Functionality | P1 | Candidate mới tự động có Status = Open | 1. Nhập toàn bộ dữ liệu hợp lệ.<br>2. Submit.<br>3. Kiểm tra candidate vừa tạo. | Candidate được tạo và **Status = Open**. |
| TC-UC06-FUN-021 | Functionality | P2 | Cancel quay lại màn hình trước | 1. Mở Create candidate từ Candidate list.<br>2. Nhấn Cancel. | Hệ thống quay lại màn hình trước đó, tức **Candidate list**. |

## GUI

| ID | Test Type | Priority | Test Case | Steps | Expected Result |
|---|---|:---:|---|---|---|
| TC-UC06-GUI-001 | GUI | P2 | Kiểm tra toàn bộ thành phần GUI của Create candidate | 1. Mở Create candidate.<br>2. Kiểm tra module name, breadcrumb, function name, các field, Submit, Cancel, Assign me.<br>3. Kiểm tra trạng thái mặc định. | Các component được hiển thị đúng theo Screen Description; required field có trạng thái phù hợp; Breadcrumb hiển thị **Candidate List** và có thể click; Submit/Cancel hiển thị đúng. |

## Usability

| ID | Test Type | Priority | Test Case | Steps | Expected Result |
|---|---|:---:|---|---|---|
| TC-UC06-USA-001 | Usability | P3 | Thông báo thành công ME012 | 1. Nhập dữ liệu hợp lệ.<br>2. Submit. | **ME012 – Successfully created candidate** hiển thị rõ ràng sau khi tạo thành công. |
| TC-UC06-USA-002 | Usability | P3 | Thông báo lỗi ME002 | 1. Bỏ trống một required field.<br>2. Submit. | **ME002 – Required field** được hiển thị rõ ràng tại vị trí phù hợp với field lỗi. |

**Tổng: 24 Test Cases**
