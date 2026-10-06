# Risk Analysis – UC06: Create new candidate

## 1. Business Rules

| Rule ID | Business Rule Description | Rule Type | Source |
|---|---|---|---|
| BR-UC06-01 | Tất cả các trường bắt buộc phải được nhập. Nếu thiếu trường bắt buộc, hệ thống hiển thị lỗi `ME002 – Required field`. | Validation | BRL-6-01 |
| BR-UC06-02 | Candidate mới được tạo có Status mặc định là `Open`. | Functional | BRL-6-02, Basic Flow Step 4 |
| BR-UC06-03 | User có thể thiết lập Status của candidate mới thành `Open` hoặc `Banned`. Các Status khác được hệ thống tự động cập nhật dựa trên Interview và Offer. | Functional | BRL-6-02 |
| BR-UC06-04 | Email phải đúng định dạng email. Nếu không đúng định dạng, hệ thống hiển thị `ME009 – Invalid email address`. | Validation | BRL-6-03 |
| BR-UC06-05 | D.O.B phải là một ngày trong quá khứ. Nếu không phải ngày trong quá khứ, hệ thống hiển thị `ME010 – Date of Birth must be in the past`. | Validation | BRL-6-04 |
| BR-UC06-06 | Recruiter owner là trường bắt buộc. Danh sách lựa chọn gồm tên Recruiter và account name. | Validation / Functional | Screen Component 19 |
| BR-UC06-07 | Khi user click `Assign me`, hệ thống tự động điền account của current user vào trường Recruiter owner. | Functional | Screen Component 20 |

---

## 2. Risk Table

| Risk ID | Risk Description | Category | Impact | Likelihood | Risk Level | Source |
|---|---|---|---|---|---|---|
| RISK-UC06-01 | Validation của các trường bắt buộc không chính xác hoặc bị thiếu có thể dẫn đến candidate profile không đầy đủ hoặc dữ liệu không hợp lệ. | Functional | High | Medium | Medium | BRL-6-01 |
| RISK-UC06-02 | Quy tắc Status chưa xác định đầy đủ danh sách Status, Status nào user được chọn, Status nào system tự động cập nhật và điều kiện chuyển Status. | Functional | High | High | High | BRL-6-02, Basic Flow Step 4 |
| RISK-UC06-03 | Quyền và hành vi của `Recruiter owner` và `Assign me` đối với Recruiter, Manager và Admin chưa được xác định đầy đủ. | Permission | High | High | High | Screen Component 19, 20; Actor |
| RISK-UC06-04 | Email validation có thể được triển khai sai hoặc thiếu, dẫn đến candidate được lưu với email không hợp lệ hoặc hiển thị sai error message. | Functional / Data Quality | High | Medium | High | BRL-6-03 |
| RISK-UC06-05 | D.O.B validation có thể được triển khai sai, cho phép ngày hiện tại/ngày tương lai hoặc hiển thị sai error message. | Functional / Data Quality | High | Medium | Medium/High | BRL-6-04 |
| RISK-UC06-06 | Không có permission matrix xác định quyền Create candidate, chọn Recruiter owner, sử dụng Assign me và thiết lập Status cho Recruiter, Manager và Admin. | Permission | High | High | High | Use Case Actor / Pre-condition |
| RISK-UC06-07 | `BRL-6-02` tham chiếu `BR-4-04` để xác định các Status khác và cơ chế auto-update nhưng nội dung `BR-4-04` không được cung cấp. | Functional / Dependency | High | High | High | BRL-6-02 |
| RISK-UC06-08 | Chưa xác định chính sách duplicate candidate theo Email, Phone hoặc thông tin định danh khác, có thể dẫn đến duplicate candidate records. | Data Integrity | High | Medium | High | Screen Description / Business Rules |
| RISK-UC06-09 | Quy tắc validation của CV Attachment chưa xác định đầy đủ file extension, file size, số lượng file và hành vi khi upload file không hợp lệ. | Functional / Data Quality | Medium | Medium | Medium/High | Screen Component 13 |
| RISK-UC06-10 | Format của Phone number chưa được xác định đầy đủ mặc dù Data Type được mô tả là `Number`, có thể gây lỗi với số có mã quốc gia hoặc số 0 ở đầu. | Data Quality | Medium | Medium | Medium | Screen Component 10 |
| RISK-UC06-11 | Quy tắc xác định danh sách Recruiter trong `Recruiter owner` chưa đầy đủ, bao gồm active/inactive recruiter, department và permission filtering. | Permission / Data | High | Medium | Medium/High | Screen Component 19 |
| RISK-UC06-12 | Status xuất hiện trên Mock-up và Business Rules nhưng không có mô tả tương ứng trong Screen Description, gây thiếu nhất quán giữa UI specification và functional specification. | Functional / Specification | High | Medium | High | Mock-up / Screen Description / BRL-6-02 |
