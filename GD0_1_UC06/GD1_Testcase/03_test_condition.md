# Test Condition Review – UC06: Create new candidate

## 1. Kết quả kiểm tra

### Câu 1 – Mỗi AC có đủ >= 2 condition chưa? (đếm bằng mắt)

**Kết quả: CHƯA THỂ XÁC NHẬN ĐẦY ĐỦ.**

Output hiện có **9 test conditions**:

1. `TC-UC06-SEC-001` – Role-based access to Recruiter owner and Assign me
2. `TC-UC06-GUI-001` – Screen layout and component display
3. `TC-UC06-GUI-002` – Field properties and default states
4. `TC-UC06-FUN-001` – Successful candidate creation
5. `TC-UC06-FUN-002` – Mandatory field validation
6. `TC-UC06-FUN-003` – Data format and business rule validations
7. `TC-UC06-FUN-004` – Candidate Status handling
8. `TC-UC06-USA-001` – Error and success message clarity
9. `TC-UC06-USA-002` – Assign me button functionality

Nguồn output cho thấy 9 condition này nhưng **không có danh sách Acceptance Criteria (AC) riêng và mapping AC → condition**. Vì vậy không thể kết luận chắc chắn rằng *mỗi AC* đã có ít nhất 2 condition.

Nếu xét theo các nhóm chức năng chính có thể thấy:

- Mandatory field: có condition.
- Email/DOB/CV validation: có condition.
- Status: có condition.
- Recruiter owner/Assign me: có Security + Usability condition.
- Successful creation: có condition.
- GUI: có 2 condition.
- Error/success message: có condition.

Tuy nhiên cần có AC list và mapping chính thức để xác nhận tiêu chí `>= 2 condition / AC`.

---

### Câu 2 – Có condition nào viết quá chi tiết, thành test case không?

**Kết quả: CÓ.**

Một số condition đang chứa quá nhiều chi tiết của test case, đặc biệt là expected behavior.

#### `TC-UC06-FUN-002`

Condition mô tả:

- Liệt kê toàn bộ mandatory fields.
- Click ButtonA.
- Kiểm tra ME002.
- Kiểm tra candidate không được save.

Nội dung này gần với một test case hoàn chỉnh hơn là test condition.

#### `TC-UC06-FUN-003`

Condition gộp nhiều validation khác nhau:

- Email invalid.
- DOB invalid.
- CV file type.

Đây thực tế là **3 nhóm test condition riêng**, không nên gộp thành một condition nếu mục tiêu là tạo test condition độc lập.

#### `TC-UC06-FUN-001`

Condition chứa cả:

- Save candidate.
- Status = Open.
- ME012.
- Navigate về Candidate list.

Đây cũng gần với test case end-to-end hơn là một condition đơn.

#### `TC-UC06-GUI-002`

Condition gộp:

- Mandatory indication.
- Default state.
- Textbox.
- Combobox.
- Date picker.
- File upload.

Có thể tách thành nhiều condition nhỏ hơn.

#### `TC-UC06-SEC-001`

Condition gộp behavior của nhiều role và cả Recruiter owner + Assign me. Nên tách theo permission/role scenario.

**Kết luận:** Có hiện tượng **condition quá rộng và chứa expected behavior chi tiết**, cần giảm xuống mức test condition.

---

### Câu 3 – Có nhánh điều kiện nào bị bỏ sót?

**Kết quả: CÓ.**

Các nhánh quan trọng bị thiếu:

#### 1. Permission theo Actor

Use Case có:

- Recruiter
- Manager
- Admin

Nhưng output sử dụng:

- Role A
- Role B
- Role C

và chưa có condition riêng cho từng Actor theo tài liệu gốc.

Cần có các condition cho:

- Recruiter create candidate.
- Manager create candidate.
- Admin create candidate.
- Quyền chọn Recruiter owner.
- Quyền sử dụng `Assign me`.

#### 2. Mandatory field combinations

Hiện chỉ có một condition chung cho mandatory validation.

Thiếu các nhánh:

- Từng mandatory field bị bỏ trống.
- Nhiều mandatory fields cùng bỏ trống.
- Tất cả mandatory fields hợp lệ.

#### 3. Email validation

Có invalid email nhưng thiếu các partition rõ ràng:

- Valid email.
- Invalid email.
- Empty email.
- Boundary/format cases.

#### 4. D.O.B

Có nhánh DOB không phải quá khứ nhưng thiếu:

- Past date.
- Today.
- Future date.

#### 5. Status

Có default Open và Open/Banned, nhưng thiếu:

- Status field có visible hay không.
- Status có editable hay không.
- Danh sách status đầy đủ.
- Các status system-controlled.
- Transition dựa trên Interview.
- Transition dựa trên Offer.
- Behavior khi status = Banned.

#### 6. Recruiter owner / Assign me

Thiếu:

- Chọn recruiter khác.
- Current user là recruiter.
- Current user không phải recruiter.
- Manager/Admin click Assign me.
- Empty recruiter owner.
- Danh sách recruiter có filter/permission.

#### 7. CV Attachment

Output chỉ nói PDF/Word, thiếu:

- Valid PDF.
- Valid Word.
- Invalid extension.
- File quá lớn.
- File lỗi/corrupt.
- Multiple files nếu có khả năng upload nhiều file.

#### 8. Duplicate candidate

Không có condition cho candidate trùng:

- Email.
- Phone.
- Các thông tin định danh khác.

#### 9. Cancel / Breadcrumb

Mock-up có `Cancel` và breadcrumb `Candidate list`, nhưng test conditions chưa có condition riêng cho:

- Cancel.
- Quay lại Candidate list bằng breadcrumb.

---

### Câu 4 – Có condition nào trùng lặp?

**Kết quả: CÓ một số overlap.**

#### Overlap 1 – Assign me

`TC-UC06-SEC-001` và `TC-UC06-USA-002` đều kiểm tra:

> Assign me → tự động điền current user's account.

Khác nhau chủ yếu ở test type:

- Security
- Usability

Nhưng phần functional behavior bị lặp.

Nên tách rõ:

- Security: permission/visibility/role behavior.
- Functional/Usability: button thực hiện populate đúng current user.

#### Overlap 2 – Status

`TC-UC06-FUN-001` và `TC-UC06-FUN-004` cùng đề cập:

> Status = Open sau khi tạo.

Nên tránh lặp expected behavior. Một condition nên kiểm tra successful creation, condition khác kiểm tra status behavior.

#### Overlap 3 – Mandatory fields / GUI

`TC-UC06-GUI-002` và `TC-UC06-FUN-002` cùng bao phủ mandatory fields.

Có thể giữ cả hai nếu mục đích khác nhau:

- GUI: required indicator.
- Functional: validation khi Submit.

Nhưng phải phân biệt rõ phạm vi để không tạo duplicate test case.

#### Overlap 4 – Error messages

`TC-UC06-FUN-003` và `TC-UC06-USA-001` đều đề cập ME009/ME010.

Nên phân biệt:

- Functional: message xuất hiện đúng điều kiện.
- Usability: nội dung/khả năng hiểu của message.

---

## 2. Số lượng condition

### AI sinh

**9 conditions**

| # | Condition ID | Loại |
|---:|---|---|
| 1 | TC-UC06-SEC-001 | Security |
| 2 | TC-UC06-GUI-001 | GUI |
| 3 | TC-UC06-GUI-002 | GUI |
| 4 | TC-UC06-FUN-001 | Functionality |
| 5 | TC-UC06-FUN-002 | Functionality |
| 6 | TC-UC06-FUN-003 | Functionality |
| 7 | TC-UC06-FUN-004 | Functionality |
| 8 | TC-UC06-USA-001 | Usability |
| 9 | TC-UC06-USA-002 | Usability |

### Số condition cần sửa

**6/9 condition nên sửa hoặc tách lại**:

- `TC-UC06-SEC-001`
- `TC-UC06-GUI-002`
- `TC-UC06-FUN-001`
- `TC-UC06-FUN-002`
- `TC-UC06-FUN-003`
- `TC-UC06-FUN-004`

### Condition có thể giữ tương đối

- `TC-UC06-GUI-001`
- `TC-UC06-USA-001`
- `TC-UC06-USA-002`

Tuy nhiên `TC-UC06-USA-002` vẫn cần tách khỏi phần permission nếu tiếp tục dùng cho Security.

---

## 3. Tổng kết Human Review

| Tiêu chí | Kết quả |
|---|---|
| AI sinh | **9 conditions** |
| Condition cần sửa/tách | **6/9** |
| Condition có overlap | **Có** |
| Condition quá chi tiết | **Có** |
| Nhánh bị bỏ sót | **Có** |
| Có đủ >=2 condition cho mỗi AC | **Chưa xác nhận được – thiếu AC mapping** |
| Cần bổ sung | **Có** |

### Các nhóm cần bổ sung chính

1. Actor/Permission.
2. Mandatory field combinations.
3. Email validation.
4. DOB boundary.
5. Status lifecycle.
6. Recruiter owner.
7. Assign me.
8. CV attachment.
9. Duplicate candidate.
10. Cancel.
11. Breadcrumb navigation.
12. Status/permission boundary cases.
