# Execution Log


## 1. Execution Summary

| Metric | Count |
|---|---:|
| Total test cases | **52** |
| Passed | **41** |
| Failed | **7** |
| Blocked | **4** |

## 2. Execution Results

## UC-06

| ID | Test Type | Priority | Test Case | Result | Test Date | Bug ID | Note |
|---|---|---|---|---|---|---|---|
| TC-UC06-FUN-001 | Functionality | P1 | Tạo candidate   thành công với dữ liệu hợp lệ | **Passed** |  |  |  |
| TC-UC06-FUN-002 | Functionality | P1 | Full   name không được bỏ trống | **Passed** |  |  |  |
| TC-UC06-FUN-003 | Functionality | P1 | Email   không được bỏ trống | **Passed** |  |  |  |
| TC-UC06-FUN-004 | Functionality | P1 | Email   phải đúng format | **Passed** |  |  |  |
| TC-UC06-FUN-005 | Functionality | P1 | Gender   là field bắt buộc và có danh sách giá trị hợp lệ | **Passed** |  |  |  |
| TC-UC06-FUN-006 | Functionality | P1 | D.O.B   không được bỏ trống | **Failed** |  | BUG-UC06-001 |  |
| TC-UC06-FUN-007 | Functionality | P1 | D.O.B   phải là ngày trong quá khứ | **Passed** |  |  |  |
| TC-UC06-FUN-008 | Functionality | P1 | Address   không được bỏ trống | **Failed** |  |  | Bug ID chưa có trong source/context hiện tại. |
| TC-UC06-FUN-009 | Functionality | P1 | Phone   number không được bỏ trống | **Passed** |  |  |  |
| TC-UC06-FUN-010 | Functionality | P1 | CV   Attachment là field bắt buộc | **Failed** |  |  | Bug ID chưa có trong source/context hiện tại. |
| TC-UC06-FUN-011 | Functionality | P1 | Current   position không được bỏ trống | **Passed** |  |  |  |
| TC-UC06-FUN-012 | Functionality | P1 | Skills   không được bỏ trống | **Passed** |  |  |  |
| TC-UC06-FUN-013 | Functionality | P2 | Skills   hỗ trợ chọn nhiều giá trị | **Passed** |  |  |  |
| TC-UC06-FUN-014 | Functionality | P2 | Years   of experience nhận dữ liệu số | **Passed** |  |  |  |
| TC-UC06-FUN-015 | Functionality | P1 | Highest   level không được bỏ trống | **Passed** |  |  |  |
| TC-UC06-FUN-016 | Functionality | P1 | Recruiter   owner không được bỏ trống | **Passed** |  |  |  |
| TC-UC06-FUN-017 | Functionality | P2 | Assign   me tự động điền Recruiter owner | **Passed** |  |  |  |
| TC-UC06-FUN-018 | Functionality | P2 | Note   tối đa 500 ký tự | **Failed** |  |  | Bug ID chưa có trong source/context hiện tại. |
| TC-UC06-FUN-019 | Functionality | P1 | Submit   thất bại hiển thị ME011 | **Passed** |  |  |  |
| TC-UC06-FUN-020 | Functionality | P1 | Candidate   mới tự động có Status = Open | **Passed** |  |  |  |
| TC-UC06-FUN-021 | Functionality | P2 | Cancel   quay lại màn hình trước | **Passed** |  |  |  |
| TC-UC06-GUI-001 | GUI | P2 | Kiểm   tra toàn bộ thành phần GUI của Create candidate | **Passed** |  |  |  |
| TC-UC06-USAB-001 | Usability | P3 | Thông báo thành công ME012 | **Passed** |  |  |  |
| TC-UC06-USAB-002 | Usability | P3 | Thông báo lỗi ME002 | **Passed** |  |  |  |
| TC-UC06-FLOW-001 | Flow | P1 | Tạo   candidate và kiểm tra candidate xuất hiện trong Candidate List | **Passed** |  |  |  |
| TC-UC06-DATA-001 | Data | P1 | Dữ   liệu candidate được lưu đúng sau khi tạo thành công | **Passed** |  |  |  |
| TC-UC06-DATA-003 | Data | P2 | Dữ   liệu nhiều Skills được lưu và hiển thị đúng | **Passed** |  |  |  |
| TC-UC06-INT-001 | Integration | P1 | Create   Candidate tích hợp thành công với Candidate List | **Passed** |  |  |  |
| TC-UC06-INT-002 | Integration | P1 | Create   Candidate xử lý lỗi từ hệ thống tạo candidate | **Passed** |  |  |  |

## UC18

| ID | Test Type | Priority | Test Case | Result | Test Date | Bug ID | Note |
|---|---|---|---|---|---|---|---|
| TC-UC18-FUN-001 | Functionality | P1 | Xem chi tiết   lịch phỏng vấn từ Interview Schedule List | **Passed** | 46244 | BUG-UC18-002 |  |
| TC-UC18-FUN-002 | Functionality | P1 | Manager   mở màn hình Edit qua Button Edit | **Blocked** | 46244 |  |  |
| TC-UC18-FUN-003 | Functionality | P1 | Admin   mở màn hình Edit qua Button Edit | **Blocked** |  |  |  |
| TC-UC18-FUN-004 | Functionality | P1 | Interviewer   mở màn hình Submit result | **Passed** |  |  |  |
| TC-UC18-FUN-005 | Functionality | P2 | Cancel   từ màn hình chi tiết lịch | **Passed** |  |  |  |
| TC-UC18-FUN-006 | Functionality | P2 | HR/Manager/Admin   kích hoạt Send Reminder | **Failed** |  |  | Không hiển thị nút Send Reminder Bug ID chưa có trong source/context hiện tại. |
| TC-UC18-FUN-007 | Functionality | P1 | Interviewer   không có Edit | **Passed** |  |  |  |
| TC-UC18-FUN-008 | Functionality | P1 | Recruiter/Manager/Admin   không có Submit result | **Passed** |  |  |  |
| TC-UC18-GUI-001 | GUI | P2 | Kiểm   tra module, sub-module và function name | **Passed** |  |  |  |
| TC-UC18-GUI-002 | GUI | P2 | Kiểm   tra toàn bộ thông tin chi tiết lịch phỏng vấn | **Passed** |  |  |  |
| TC-UC18-GUI-003 | GUI | P2 | Kiểm   tra định dạng Interview Schedule | **Passed** |  |  |  |
| TC-UC18-GUI-004 | GUI | P2 | Kiểm   tra Results khi chưa có kết quả | **Passed** |  |  |  |
| TC-UC18-GUI-005 | GUI | P2 | Kiểm   tra Created on khi tạo hôm nay | **Blocked** |  |  |  |
| TC-UC18-GUI-006 | GUI | P2 | Kiểm   tra Created on khi tạo ngày khác | **Passed** |  |  |  |
| TC-UC18-GUI-007 | GUI | P2 | Kiểm   tra Last updated by khi cập nhật hôm nay | **Blocked** |  |  |  |
| TC-UC18-GUI-008 | GUI | P2 | Kiểm   tra Last updated by khi cập nhật ngày khác | **Passed** |  |  |  |
| TC-UC18-GUI-009 | GUI | P2 | Kiểm   tra màn hình riêng của Interviewer | **Passed** |  |  |  |
| TC-UC18-SEC-001 | Security | P1 | Kiểm   tra action button theo màn hình Interviewer | **Passed** |  |  |  |
| TC-UC18-FLOW-002 | Flow | P1 | Interviewer   xem Schedule Detail và Submit Interview Result | **Passed** |  |  |  |
| TC-UC18-DATA-001 | Data | P1 | Thông   tin Interview Schedule được hiển thị đúng trên Detail | **Passed** |  |  |  |
| TC-UC18-DATA-002 | Data | P2 | Schedule   chưa có Interview Result hiển thị N/A | **Passed** |  |  |  |
| TC-UC18-INT-001 | Integration | P1 | Interview   Schedule Detail trigger đúng UC khi thực hiện Edit | **Failed** |  |  | Edit không truy cập được Bug ID chưa có trong source/context hiện tại. |
| TC-UC18-INT-003 | Integration | P1 | Interview   Schedule Detail trigger Send Reminder | **Failed** |  |  | Không có nút Send Reminder Bug ID chưa có trong source/context hiện tại. |

## 3. Failed / Bug Traceability

| Test Case | Bug ID | Actual observation |
|---|---|---|
| TC-UC06-FUN-006 | **BUG-UC06-001** | D.O.B bỏ trống nhưng candidate vẫn được tạo; không hiển thị ME002. |
| TC-UC06-FUN-008 | — | Address bỏ trống nhưng validation không đạt expected result. |
| TC-UC06-FUN-010 | — | CV Attachment bỏ trống nhưng validation Required field không đạt expected result. |
| TC-UC06-FUN-018 | — | Note vượt 500 ký tự nhưng testcase Failed. |
| TC-UC18-FUN-001 | **BUG-UC18-002** | Click Interview Schedule List breadcrumb dẫn tới 404 Not Found. |
| TC-UC18-FUN-006 | — | Không hiển thị nút Send Reminder. |
| TC-UC18-INT-001 | — | Không truy cập được Edit. |
| TC-UC18-INT-003 | — | Không có nút Send Reminder. |
