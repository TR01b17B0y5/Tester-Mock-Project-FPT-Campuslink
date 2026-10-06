# 14_GO_NO_GO_DECISION

## 1. Quyết định

### **NO-GO – CHƯA PHÁT HÀNH**

Dựa trên dữ liệu kiểm thử hiện tại, quyết định đề xuất là:

- [ ] GO – Đồng ý phát hành
- [x] **NO-GO – Chưa phát hành**
- [ ] GO with conditions – Phát hành kèm điều kiện

## 2. Căn cứ trực tiếp từ dữ liệu

| Yếu tố | Dữ liệu | Ảnh hưởng |
|---|---:|---|
| Tổng test case | 52 | Toàn bộ phạm vi đã có trạng thái |
| Failed | **7** | Chưa đạt |
| Blocked | **4** | Một số chức năng chưa thể xác nhận |
| Critical bug | **0** | Đạt |
| Major bug | **3** | Chưa đạt điều kiện release |
| Minor bug | **4** | Còn tồn đọng |

## 3. Yếu tố nghiệp vụ quan trọng

### CV Attachment

Ngoài các con số execution, có một yếu tố nghiệp vụ cần được xem xét:

**CV Attachment là dữ liệu quan trọng đối với workflow candidate/interview.**

Theo thông tin người dùng cung cấp, nếu candidate được tạo khi **không có CV**, người dùng có thể không có CV để xem và sử dụng trong quá trình hẹn lịch/phỏng vấn.

Vì vậy, `TC-UC06-FUN-010 – CV Attachment là field bắt buộc` không nên được xem như một lỗi validation nhỏ đơn thuần.

Nếu hệ thống cho phép:

```text
Create Candidate
        ↓
Candidate không có CV
        ↓
Người dùng cần xem CV để phục vụ workflow interview
        ↓
Không có CV để xem
        ↓
Ảnh hưởng workflow downstream
```

thì lỗi này có khả năng ảnh hưởng trực tiếp đến quy trình nghiệp vụ.

> **Đây là yếu tố nghiệp vụ do người dùng cung cấp trong context hiện tại, không phải một con số được suy ra từ execution log.**

## 4. Lý do không GO

Quyết định NO-GO dựa trên tổng hợp các yếu tố:

1. **7 test case Failed** chưa được chứng minh là đã hoàn tất investigation và re-test.
2. **4 test case Blocked**, trong đó vẫn còn nguyên nhân Blocked chưa được ghi nhận đầy đủ.
3. Có **3 Major bug** còn mở.
4. Chức năng **Edit** đang gặp lỗi `500 Internal Server Error`, làm cản trở việc xác nhận workflow.
5. **Send Reminder** chưa hoạt động/không hiển thị trong các test case liên quan.
6. **CV Attachment validation bị Failed**, trong khi CV có vai trò quan trọng đối với workflow downstream theo thông tin nghiệp vụ được cung cấp.
7. Chưa có bằng chứng đầy đủ về regression/re-test cho các bug đã fix.
8. Chưa có xác nhận cuối cùng của QA/Test Lead và stakeholder.

## 5. Điều kiện để chuyển sang GO / GO with conditions

Trước khi xem xét phát hành, cần tối thiểu:

- Fix và re-test `TC-UC06-FUN-010` về CV Attachment.
- Xác nhận candidate không thể được tạo khi thiếu CV nếu đây là business requirement đã được chốt.
- Fix và re-test chức năng Edit.
- Fix và re-test Send Reminder.
- Hoàn tất investigation cho toàn bộ 7 Failed test case.
- Làm rõ nguyên nhân của các Blocked test case còn thiếu thông tin.
- Regression các bug đã fix.
- Xác nhận xử lý đối với 3 Major và 4 Minor bug.
- QA/Test Lead và stakeholder phê duyệt kết quả.

## 6. Kết luận

> **NO-GO – Chưa phát hành.**

Lý do chính không chỉ là còn Failed test case, mà là còn **Major bug, chức năng Blocked và một lỗi CV Attachment có khả năng ảnh hưởng workflow nghiệp vụ downstream**.

Nếu các lỗi trên được xử lý và regression/re-test đạt yêu cầu, quyết định có thể được đánh giá lại.

**Người quyết định:** Tùng      

**Ngày:**12/08/2026
