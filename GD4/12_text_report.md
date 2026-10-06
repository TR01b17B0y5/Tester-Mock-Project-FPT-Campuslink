# TEST SUMMARY REPORT

## 1. SỐ LIỆU THỰC THI

| Chỉ số | Giá trị |
|---|---:|
| Tổng test case | **52** |
| Đã thực thi | **52** |
| Pass | **37** |
| Fail | **8** |
| Blocked | **7** |

### Danh sách Test Case Fail

1. `TC-UC06-FUN-006` – D.O.B không được bỏ trống
2. `TC-UC06-FUN-008` – Address không được bỏ trống
3. `TC-UC06-FUN-010` – CV Attachment là field bắt buộc
4. `TC-UC06-FUN-018` – Note tối đa 500 ký tự
5. `TC-UC18-FUN-006` – HR/Manager/Admin kích hoạt Send Reminder
6. `TC-UC18-INT-001` – Interview Schedule Detail trigger đúng UC khi thực hiện Edit
7. `TC-UC18-INT-003` – Interview Schedule Detail trigger Send Reminder

### Tình trạng Blocked

Có **4 test case Blocked**. Các nguyên nhân được ghi nhận trong execution log gồm:

- Không thể truy cập chức năng **Edit** do lỗi hệ thống `500 Internal Server Error`.
- Chức năng **Send Reminder** không hiển thị.
- Hai test case còn lại bị Blocked theo execution log nhưng nguyên nhân chi tiết chưa được cung cấp trong dữ liệu hiện tại.

---

## 2. TÌNH TRẠNG BUG

| Mức độ | Số lượng còn mở |
|---|---:|
| Critical | **0** |
| Major | **3** |
| Minor | **4** |
| **Tổng** | **7** |


---

## 3. NHẬN XÉT VỀ KẾT QUẢ KIỂM THỬ

### 3.1. Nhận xét tổng quan về chất lượng

Trong tổng số **52 test case**, có **41 test case Passed**, **7 test case Failed** và **4 test case Blocked**.

Các chức năng trong phạm vi UC06 và UC18 đã được thực thi, tuy nhiên vẫn còn các lỗi liên quan đến validation dữ liệu bắt buộc, giới hạn dữ liệu và các chức năng của Interview Schedule.

### 3.2. Điểm đáng lo ngại nhất

Các vấn đề đáng chú ý gồm:

- D.O.B bắt buộc nhưng test case tương ứng Failed.
- Address bắt buộc nhưng test case tương ứng Failed.
- CV Attachment bắt buộc nhưng test case tương ứng Failed.
- Note có giới hạn 500 ký tự nhưng test case tương ứng Failed.
- Chức năng Send Reminder không hoạt động/không hiển thị theo các test case liên quan.
- Chức năng Edit bị Blocked do lỗi `500 Internal Server Error`.

Trong số này, **CV Attachment là rủi ro nghiệp vụ đáng chú ý**. Theo thông tin được cung cấp, CV là dữ liệu cần thiết để người dùng có thể xem CV và sử dụng thông tin đó trong quá trình hẹn lịch/phỏng vấn. Vì vậy, lỗi validation cho phép tạo candidate khi thiếu CV có thể ảnh hưởng đến workflow downstream, không chỉ là một lỗi UI validation đơn lẻ.

### 3.3. Rủi ro còn tồn đọng

Các rủi ro còn tồn đọng gồm:

1. **Validation dữ liệu candidate chưa đáng tin cậy**, đặc biệt với CV Attachment.
2. **Edit chưa thể kiểm thử đầy đủ** do lỗi 500.
3. **Send Reminder chưa thể xác nhận hoạt động đúng**.

Các rủi ro này cần được xem xét trước quyết định phát hành.

---

## 4. DANH SÁCH TEST CASE FAIL

| Test Case ID | Nội dung | Kết quả |
|---|---|---|
| `TC-UC06-FUN-006` | D.O.B không được bỏ trống | **Failed** |
| `TC-UC06-FUN-008` | Address không được bỏ trống | **Failed** |
| `TC-UC06-FUN-010` | CV Attachment là field bắt buộc | **Failed** |
| `TC-UC06-FUN-018` | Note tối đa 500 ký tự | **Failed** |
| `TC-UC18-FUN-006` | HR/Manager/Admin kích hoạt Send Reminder | **Failed** |
| `TC-UC18-INT-001` | Interview Schedule Detail trigger đúng UC khi thực hiện Edit | **Failed** |
| `TC-UC18-INT-003` | Interview Schedule Detail trigger Send Reminder | **Failed** |

---

## 5. TEST CASE BỊ BLOCK

| Nhóm nguyên nhân | Tình trạng |
|---|---|
| Edit | Không thể vào chức năng Edit do lỗi `500 Internal Server Error` |
| Send Reminder | Không hiển thị nút Send Reminder |
| Hai test case Blocked còn lại | Chưa có nguyên nhân chi tiết trong dữ liệu hiện tại |

---

## 6. ĐÁNH GIÁ TIÊU CHÍ THOÁT

| Tiêu chí | Mục tiêu | Thực tế | Đạt/Không |
|---|---|---|---|
| Test execution | 100% được thực thi hoặc Blocked có giải thích | 52/52 có trạng thái; 4 Blocked nhưng 2 nguyên nhân chưa được cung cấp đầy đủ | **Không đạt** |
| Critical/P0 bug | Không còn | Critical = 0 | **Đạt** |
| P1/Major bug ảnh hưởng chức năng chính | Không còn | Major = 3 | **Không đạt** |
| Failed test case được điều tra | Tất cả Failed được điều tra | Có 7 Failed; dữ liệu hiện tại chưa chứng minh tất cả đã được điều tra đầy đủ | **Không đạt** |
| Fixed bug được regression/re-test | Tất cả bug đã fix phải được re-test | Chưa có dữ liệu chứng minh đầy đủ | **Không đạt** |
| P2/P3 bug | Có ghi nhận và quyết định xử lý | Có 4 Minor còn mở; chưa có quyết định xử lý cụ thể trong dữ liệu | **Không đạt** |
| Evidence/documentation | Đầy đủ | Có execution data, nhưng chưa đủ evidence để xác nhận toàn bộ tiêu chí | **Không đạt** |
| QA/Test Lead & stakeholder approval | Có phê duyệt | Chưa có thông tin phê duyệt | **Chưa đạt** |

---

## 7. QUYẾT ĐỊNH

- [ ] GO – Đồng ý phát hành
- [x] **NO-GO – Chưa phát hành**
- [ ] GO with conditions – Phát hành kèm điều kiện

### Lý do quyết định

Dựa trên số liệu kiểm thử hiện tại, **chưa đủ điều kiện để GO**.

Các lý do chính:

1. Có **7 Failed test case**.
2. Có **4 test case Blocked**, trong đó còn test case chưa có nguyên nhân Blocked đầy đủ.
3. Có **3 Major bug** còn mở.
4. Chưa có bằng chứng đầy đủ rằng toàn bộ Failed test case đã được điều tra và các bug đã fix đã được regression/re-test.
5. **CV Attachment là một rủi ro nghiệp vụ quan trọng**: nếu candidate được tạo khi thiếu CV, người dùng có thể không có CV để xem và sử dụng trong workflow hẹn lịch/phỏng vấn. Đây là yếu tố ảnh hưởng downstream workflow và cần được xử lý trước khi phát hành.

### Điều kiện tối thiểu để xem xét lại quyết định

- Fix và re-test các Failed test case, ưu tiên CV Attachment.
- Xác nhận và re-test chức năng Edit.
- Xác nhận và re-test Send Reminder.
- Hoàn tất investigation cho tất cả Failed test case.
- Làm rõ nguyên nhân của các test case Blocked còn thiếu thông tin.
- Regression các bug đã fix.
- Có xác nhận cuối cùng của QA/Test Lead và stakeholder.

**Người quyết định:** Tùng

**Ngày:**12/08/2026
