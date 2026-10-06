# Phân tích Ambiguity – UC06: Create new candidate

## 1. Mục đích

Tài liệu này đánh giá output của Agent khi phân tích ambiguity/risk cho UC06 – **Create new candidate**, đối chiếu với Use Case Overview, Basic Flow, Mock-up Screen, Screen Description và Business Rules.

Ngoài việc đánh giá output của Agent, tài liệu bổ sung các issue/ambiguity mà Agent chưa phát hiện.

---

# 2. Tóm tắt output của Agent

Agent xác định 3 Business Rule:

### BR-UC06-01 – Mandatory fields
Tất cả mandatory fields phải được điền; nếu không hiển thị `ME002 – Required field`.

Nguồn: `BRL-6-01`.

### BR-UC06-02 – Candidate status
Candidate mới mặc định là `Open`. User có thể chọn `Open` hoặc `Banned`; các status khác được cập nhật tự động.

Nguồn: `BRL-6-02`.

### BR-UC06-03 – Recruiter owner / Assign me
Agent suy luận:

> Recruiter owner must be a Role A user. "Assign me" button populates field with current user's account.

Nguồn: Screen Component 19, 20.

Agent đánh dấu rule này là `inferred = true`.

---

# 3. Đánh giá từng output của Agent

## 3.1 BR-UC06-01 – Mandatory fields

### Đánh giá: ĐÚNG

Business Rule `BRL-6-01` ghi rõ:

- User phải điền tất cả trường bắt buộc.
- Nếu thiếu, hiển thị `ME002: "Required field"`.

Do đó Agent xác định đây là Business Rule loại Validation là chính xác.

### Điểm còn thiếu

Agent chưa chỉ ra rằng tài liệu chưa có một danh sách authoritative duy nhất về **toàn bộ mandatory fields**.

Screen Description đánh dấu Mandatory cho nhiều field như:

- Full name
- Email
- Gender
- D.O.B
- Address
- Phone number
- CV Attachment
- Current position
- Skills
- Highest level
- Recruiter owner

Nhưng chưa có bảng tổng hợp chính thức để xác định toàn bộ danh sách required.

### Kết luận

Rule đúng và có thể dùng để thiết kế test case, nhưng cần authoritative mandatory-field list để tránh thiếu coverage.

---

# 4. BR-UC06-02 – Status

## Đánh giá: ĐÚNG MỘT PHẦN

Agent xác định đúng:

- Candidate mới mặc định `Open`.
- User có thể chọn `Open`.
- User có thể chọn `Banned`.

Tuy nhiên Agent kết luận có:

> "conflicting post-condition"

### Đánh giá: CHƯA CHÍNH XÁC

Basic Flow ghi:

> System save the candidate in the system and automatically set status to Open.

Business Rule `BRL-6-02` ghi:

> For newly created candidate, user can set status to Open or Banned. Other statuses ... auto-updated based on interview and offer.

Hai thông tin này **không nhất thiết mâu thuẫn**.

Cách hiểu hợp lý là:

- Giá trị mặc định của candidate mới là `Open`.
- User có thể thay đổi thành `Banned`.
- Các status khác có thể được system tự động cập nhật dựa trên Interview/Offer.

### Ambiguity thực sự cần clarify

1. Status nào user được chọn thủ công?
2. Status nào chỉ được system tự động cập nhật?
3. "Other statuses" cụ thể là status nào?
4. Điều kiện chuyển sang từng status là gì?
5. Status có thể thay đổi sau khi candidate được tạo không?
6. Nếu user chọn `Banned`, Interview/Offer có được phép thay đổi status không?
7. `BR-4-04` được tham chiếu nhưng không có trong tài liệu được cung cấp.

### Kết luận

`RISK-UC06-02` là hợp lý và nên giữ mức **High**, nhưng rationale của Agent cần sửa.

---

# 5. BR-UC06-03 – Recruiter owner / Assign me

## Đánh giá: AGENT SUY DIỄN QUÁ MỨC

Agent đưa ra:

> Recruiter owner must be a Role A user.

Điều này **không có bằng chứng trực tiếp trong tài liệu**.

Use Case chỉ ghi Actor:

- Recruiter
- Manager
- Admin

Không có mapping xác nhận:

- Role A = Recruiter
- Role B = Manager
- Role C = Admin

Việc Agent đánh dấu `inferred = true` là đúng về mặt kỹ thuật, nhưng Agent vẫn không nên biến giả định này thành một business rule.

### Điều có thể khẳng định

Screen Component 19:

> Recruiter owner – Combo-box – Mandatory.

Screen Component 20:

> Khi click "Assign me", system tự động điền account của current user.

### Điều chưa thể khẳng định

Chưa biết:

- Recruiter owner chỉ được chọn Recruiter hay có thể chọn Manager/Admin.
- Manager có được chọn Recruiter owner không.
- Admin có được chọn Recruiter owner không.
- Manager/Admin có được dùng Assign me không.
- Assign me xử lý thế nào nếu current user không phải Recruiter.
- Danh sách Recruiter được filter theo permission nào.

### Kết luận

Đây là **High-risk ambiguity**, nhưng rule nên viết là:

> Permission and role mapping for Recruiter owner and Assign me are not defined.

Không nên viết:

> Recruiter owner must be a Role A user.

---

# 6. Các issue Agent phát hiện đúng

## ISSUE-01 – Status có trên Mock-up nhưng thiếu trong Screen Description

Mock-up có field `Status`, Business Rule cũng có rule về Status, nhưng Screen Description không có dòng riêng cho Status.

Chưa rõ:

- Control type
- Mandatory/optional
- Default value
- Allowed values
- Editable/read-only
- Permission

### Mức độ: HIGH

---

## ISSUE-02 – Thiếu định nghĩa BR-4-04

`BRL-6-02` tham chiếu:

> Other status as mentioned in BR-4-04 will need to be auto-updated based on interview and offer.

Nhưng tài liệu được cung cấp không có nội dung `BR-4-04`.

Không thể xác định:

- Các status còn lại.
- Điều kiện chuyển status.
- Interview nào trigger status.
- Offer nào trigger status.

### Mức độ: HIGH

---

# 7. Các issue Agent BỎ SÓT

## ISSUE-03 – Không có Permission Matrix

Use Case có 3 actor:

- Recruiter
- Manager
- Admin

Nhưng chưa có permission matrix cho:

| Chức năng | Recruiter | Manager | Admin |
|---|---|---|---|
| Create candidate | ? | ? | ? |
| Select Recruiter owner | ? | ? | ? |
| Assign me | ? | ? | ? |
| Set Open | ? | ? | ? |
| Set Banned | ? | ? | ? |

### Mức độ: HIGH

---

## ISSUE-04 – Mapping Actor và Role chưa rõ

Agent dùng Role A/B/C nhưng Use Case dùng Recruiter/Manager/Admin.

Không có bằng chứng mapping giữa hai cách gọi.

### Mức độ: HIGH

Đây là một unsupported inference của Agent.

---

## ISSUE-05 – Mandatory fields chưa có authoritative list

Các field bắt buộc được mô tả rải rác trong Screen Description nhưng chưa có một danh sách chính thức.

### Mức độ: MEDIUM

---

## ISSUE-06 – Agent bỏ sót Email validation

Business Rule `BRL-6-03` ghi:

> Email address must be in correct format. If not, display ME009 "Invalid email address".

Agent không extract rule này.

Đây là omission rõ ràng.

### Mức độ: HIGH

Nên test tối thiểu:

- Email hợp lệ.
- Email thiếu `@`.
- Email thiếu domain.
- Email sai format.
- Email rỗng và sự khác biệt giữa `ME002` và `ME009`.

---

## ISSUE-07 – Agent bỏ sót DOB validation

`BRL-6-04` ghi:

> D.O.B must be a past date. If not, display ME010 "Date of Birth must be in the past".

Agent không extract rule này.

### Mức độ: HIGH

Nên test:

- Ngày quá khứ → valid.
- Ngày hiện tại → cần clarify.
- Ngày tương lai → `ME010`.
- Input date sai format nếu textbox cho phép nhập trực tiếp.

---

## ISSUE-08 – CV Attachment validation chưa đầy đủ

Screen Description nói chọn PDF hoặc Word file nhưng chưa quy định:

- `.pdf`, `.doc`, `.docx`.
- File type không hợp lệ.
- Maximum size.
- Multiple files.
- Corrupt file.
- Duplicate filename.

### Mức độ: MEDIUM/HIGH

---

## ISSUE-09 – Phone number format chưa rõ

Screen Description ghi Data Type = `Number`.

Điều này gây ambiguity vì số điện thoại có thể cần:

- `+84`.
- Số 0 ở đầu.
- Độ dài khác nhau.
- Khoảng trắng hoặc dấu `-`.

### Mức độ: MEDIUM

Cần clarify format, length và ký tự được phép.

---

## ISSUE-10 – Duplicate candidate chưa được quy định

Chưa có rule về:

- Duplicate email.
- Duplicate phone.
- Duplicate candidate.
- Error message khi duplicate.

### Mức độ: HIGH

Đây là data-integrity risk Agent bỏ sót.

---

## ISSUE-11 – Recruiter owner list chưa rõ

Screen Description ghi list Recruiter's name và account name nhưng chưa rõ:

- Recruiter nào xuất hiện.
- Có filter theo department không.
- Inactive recruiter có xuất hiện không.
- Current user có luôn xuất hiện không.
- Có permission filtering không.

### Mức độ: MEDIUM/HIGH

---

## ISSUE-12 – Assign me chưa rõ với Manager/Admin

Nếu Manager hoặc Admin click `Assign me` thì chưa biết:

1. Có cho phép và gán họ vào Recruiter owner?
2. Không cho phép?
3. Disable button?
4. Hiển thị error?
5. Chỉ hiển thị button với Recruiter?

### Mức độ: HIGH

---

# 8. Corrected Ambiguity Register

| ID | Ambiguity / Issue | Mức độ | Agent phát hiện? | Kết luận |
|---|---|---|---|---|
| AMB-001 | Recruiter owner / Assign me permission chưa rõ | HIGH | Có | Giữ |
| AMB-002 | Status transition chưa đầy đủ | HIGH | Có, nhưng rationale chưa chuẩn | Sửa |
| AMB-003 | Thiếu BR-4-04 | HIGH | Có | Giữ |
| AMB-004 | Thiếu permission matrix cho 3 actor | HIGH | Chưa | Bổ sung |
| AMB-005 | Role A/B/C không được định nghĩa | HIGH | Chưa | Bổ sung |
| AMB-006 | Email validation bị bỏ sót | HIGH | Chưa | Bổ sung |
| AMB-007 | DOB validation bị bỏ sót | HIGH | Chưa | Bổ sung |
| AMB-008 | Duplicate candidate chưa định nghĩa | HIGH | Chưa | Bổ sung |
| AMB-009 | Status có trên UI nhưng thiếu Screen Description | HIGH | Chưa | Bổ sung |
| AMB-010 | CV attachment constraint chưa đầy đủ | MEDIUM/HIGH | Chưa | Bổ sung |
| AMB-011 | Phone number format chưa rõ | MEDIUM | Chưa | Bổ sung |
| AMB-012 | Recruiter owner list/filter chưa rõ | MEDIUM/HIGH | Chưa | Bổ sung |
| AMB-013 | Assign me behavior với Manager/Admin chưa rõ | HIGH | Chưa | Bổ sung |
| AMB-014 | Mandatory field list chưa có authoritative source | MEDIUM | Chưa | Bổ sung |

---

# 9. Business Rules mà Agent nên extract

### BR-UC06-01
Tất cả mandatory fields phải được nhập. Nếu thiếu, hiển thị `ME002 – Required field`.

Nguồn: `BRL-6-01`.

### BR-UC06-02
Candidate mới có status mặc định là `Open`.

Nguồn: `BRL-6-02` và Basic Flow.

### BR-UC06-03
User có thể chọn `Open` hoặc `Banned` theo `BRL-6-02`.

### BR-UC06-04
Email phải đúng format. Nếu sai, hiển thị `ME009 – Invalid email address`.

Nguồn: `BRL-6-03`.

### BR-UC06-05
D.O.B phải là ngày trong quá khứ. Nếu không, hiển thị `ME010 – Date of Birth must be in the past`.

Nguồn: `BRL-6-04`.

### BR-UC06-06
Recruiter owner là mandatory và danh sách chứa Recruiter's name/account.

Nguồn: Screen Component 19.

### BR-UC06-07
Click `Assign me` sẽ tự động điền current user's account vào Recruiter owner.

Nguồn: Screen Component 20.

**Lưu ý:** Không được tự động kết luận current user bắt buộc là Recruiter/Role A nếu chưa có permission matrix hoặc tài liệu mapping xác nhận.

---

# 10. Đánh giá chất lượng Agent

## Điểm mạnh

- Phát hiện đúng mandatory-field rule.
- Phát hiện đúng status rule ở mức cơ bản.
- Phát hiện ambiguity về Recruiter owner.
- Có đánh dấu inferred.
- Có risk assessment.
- Có gate BLOCK thay vì cố sinh test case khi requirement chưa rõ.

## Điểm yếu

### 1. Bỏ sót Business Rules

Agent bỏ qua:

- `BRL-6-03` – Email validation.
- `BRL-6-04` – DOB validation.

Đây là lỗi coverage đáng kể.

### 2. Inference quá mạnh

Agent biến Recruiter owner / Assign me thành:

> Recruiter owner must be a Role A user.

Trong tài liệu không có bằng chứng cho mapping này.

### 3. Hiểu chưa chính xác ambiguity về Status

Agent gọi đây là conflicting post-condition, trong khi vấn đề chính là thiếu status-transition definition và thiếu `BR-4-04`.

### 4. Không phát hiện duplicate candidate

Đây là data-integrity issue quan trọng.

### 5. Không cross-check đầy đủ giữa các section

Agent nên kiểm tra:

`Mockup → Screen Description → Business Rules → Basic Flow → Actor/Permission`

Nếu làm vậy sẽ dễ phát hiện Status xuất hiện trên UI nhưng thiếu Screen Description.

---

# 11. Đánh giá Gate

Agent trả:

```text
decision = BLOCK
quality_pass = 1
blocking_risk_ids = [
  RISK-UC06-02,
  RISK-UC06-03
]
```

## Đánh giá: BLOCK là hợp lý

Tuy nhiên blocking risks chưa đầy đủ.

Nên bổ sung:

- Missing BR-4-04.
- Missing permission matrix.
- Missing email validation trong output.
- Missing DOB validation trong output.
- Duplicate candidate behavior chưa được xác định.

### Gate đề xuất

```text
QUALITY GATE = BLOCK
```

Lý do: ambiguity có thể làm Agent sinh Expected Result sai, đặc biệt ở:

- Permission.
- Status.
- Validation.
- Data integrity.

---

# 12. Đánh giá tổng thể Agent

| Tiêu chí | Điểm |
|---|---:|
| Business Rule extraction | 6/10 |
| Ambiguity detection | 7/10 |
| Risk identification | 7/10 |
| Cross-section consistency | 5/10 |
| Tránh unsupported inference | 5/10 |
| Coverage | 5/10 |
| Gate decision | 8/10 |

### Tổng thể: khoảng 6/10

Agent có hướng tiếp cận tốt nhưng **chưa production-ready**.

---

# 13. Kết luận cuối cùng

Requirement UC06 **chưa đủ rõ để sinh test case high-confidence**.

Nên giữ:

```text
QUALITY GATE = BLOCK
```

Trước khi chuyển sang Test Case Generation cần clarify tối thiểu:

1. Permission của Recruiter / Manager / Admin.
2. Mapping Role A/B/C nếu hệ thống thực sự sử dụng Role A/B/C.
3. Behavior của Recruiter owner.
4. Behavior của Assign me với từng actor.
5. Danh sách status đầy đủ.
6. Điều kiện chuyển từng status.
7. Nội dung `BR-4-04`.
8. Email validation.
9. DOB validation.
10. Duplicate candidate policy.
11. CV attachment constraints.
12. Phone number format.
13. Danh sách mandatory fields chính thức.

**Nguyên tắc quan trọng cho Agent:** Khi requirement không có bằng chứng, Agent phải ghi `Unknown / Needs Clarification` thay vì tự tạo business rule hoặc Expected Result.

