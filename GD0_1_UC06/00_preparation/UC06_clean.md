## 3.6 UC06: Create new candidate

### 3.6.1 Overview

| Field | Content |
|---|---|
| ID and Name | Create new candidate |
| Description | This use case allows user to create a candidate profile in the system |
| Actor | Role A, Role B, Role C |
| Trigger | User clicks "Add" button in the Candidate list |
| Pre-condition | User has logged into system as Role A, Role B, Role C |
| Post-condition | System shows Create candidate profile |

Ghi chu: Role A/B/C dung nhat quan voi cac UC khac trong bo tai lieu (xem masking_glossary_UC06.md)

### 3.6.2 Flow of events

#### 3.6.2.1 Basic Flow

| Step | Actor | Action | Next |
|---|---|---|---|
| 1 | User (Role A/B/C) | Click "Add" button in the Candidate list | 2 |
| 2 | System | Display Create new candidate screen | 3 |
| 3 | User | Enter information and click ButtonA | 4 |
| 4 | System | Save the candidate in the system and automatically set status to Open | 5 |
| 5 | System | The flow ends | N/A |

### 3.6.3 Screen Components (mo ta thay cho mockup)

**Man hinh - Create new candidate**

| Vi tri | Thanh phan | Ten field da mask | Loai control | Data Type | Mo ta |
|---|---|---|---|---|---|
| 1 | Name of module | LabelA | Label | N/A | Hien thi "Candidate" |
| 2 | Name of sub-module | BreadcrumbA | Breadcrumb | N/A | Hien thi "Candidate list". Click de quay lai man hinh candidate list |
| 3 | Name of function | LabelB | Label | N/A | Hien thi "Create candidate" |
| 4 | Personal information | LabelC | Label | N/A | Hien thi nhom thong tin ca nhan |
| 5 | Full name | TextboxA | Textbox | Text | Bat buoc. Mac dinh trong. Nhap ten ung vien |
| 6 | Email | TextboxB | Textbox | Text | Bat buoc. Mac dinh trong. Nhap dung dinh dang Localpart@domainpart |
| 7 | Gender | ComboboxA | Combo-box | Text | Bat buoc. Mac dinh trong. Danh sach: Male, Female, Others |
| 8 | D.O.B | DateA | Icon + textbox | Date | Bat buoc. Mac dinh trong. Chon ngay qua icon lich hoac nhap. Phai la ngay trong qua khu |
| 9 | Address | TextboxC | Textbox | Text | Bat buoc. Mac dinh trong. Nhap dia chi ung vien |
| 10 | Phone number | TextboxD | Textbox | Number | Bat buoc. Mac dinh trong. Nhap so dien thoai ung vien |
| - | Status | ComboboxF | Combo-box | Text | Xuat hien trong mockup nhung REF khong duoc cung cap day du trong tai lieu goc. Mac dinh Open theo BRL-6-02 |
| 12 | Professional information | LabelD | Label | N/A | Hien thi nhom thong tin nghe nghiep |
| 13 | CV Attachment | UploadA | Textbox + file attachment | N/A | Bat buoc. Chon file PDF hoac Word tu may |
| 15 | Current position | ComboboxB | Combo-box | Text | Bat buoc. Mac dinh trong. Chon 1 gia tri. Danh sach: theo common component |
| 16 | Skills | ComboboxC | Combo-box | Text | Bat buoc. Mac dinh trong. Cho phep chon nhieu. Danh sach: theo common component |
| 17 | Years of experience | TextboxE | Text field | Number | Cho phep nhap so nam kinh nghiem |
| 18 | Highest level | ComboboxD | Combo-box | Text | Bat buoc. Mac dinh trong. Chon 1 gia tri. Danh sach: theo Business Rule |
| 19 | Recruiter owner | ComboboxE | Combo-box | Text | Bat buoc. Mac dinh trong. Chon 1 gia tri. Danh sach: ten va tai khoan cua Role A (xem vi du trong glossary) |
| 20 | Assign me | LinkButtonA | Button link (icon) | N/A | Click de tu dong dien tai khoan nguoi dang dang nhap vao truong Recruiter owner |
| 21 | Note | TextboxF | Textbox | Text | Cho phep nhap ghi chu, toi da 500 ky tu |
| 22 | ButtonA | Button | N/A | N/A | Khi click, tao candidate moi va quay lai man hinh Candidate list. Neu that bai -> hien thi ME011 "Failed to created candidate". Neu thanh cong -> hien thi ME012 "Successfully created candidate" |
| 23 | ButtonB | Button | N/A | N/A | Khi click, quay lai man hinh truoc do |

### 3.6.4 Business Rules

| Business Rule ID | Business Rule Description |
|---|---|
| BRL-6-01 | User phai dien day du cac truong bat buoc. Neu khong, hien thi loi ME002 "Required field" |
| BRL-6-02 | Trang thai candidate mac dinh la Open. Voi candidate moi tao, user co the set trang thai la Open hoac Banned. Cac trang thai khac (theo BRL-4-04) se tu dong cap nhat dua tren interview va offer |
| BRL-6-03 | Dinh dang email phai dung. Neu khong, hien thi loi ME009 "Invalid email address" |
| BRL-6-04 | D.O.B phai la ngay trong qua khu (som hon ngay hien tai). Neu khong, hien thi loi ME010 "Date of Birth must be in the past" |
