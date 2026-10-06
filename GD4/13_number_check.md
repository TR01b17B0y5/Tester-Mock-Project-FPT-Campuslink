# 13_NUMBER_CHECK

## 1. Mục đích

Đối chiếu từng con số trong `12_text_report.md` với dữ liệu execution và bug summary được cung cấp.

## 2. Bảng đối chiếu

| # | Số liệu trong report | Giá trị report | Data gốc | Kiểm tra | Ghi chú |
|---|---|---:|---:|---|---|
| 1 | Tổng test case | 52 | 52 | **Khớp** | Execution log |
| 2 | Đã thực thi | 52 | 52 | **Khớp** | 41 Passed + 7 Failed + 4 Blocked = 52 |
| 3 | Pass | 41 | 41 | **Khớp** | Execution log |
| 4 | Fail | 7 | 7 | **Khớp** | Danh sách Failed |
| 5 | Blocked | 4 | 4 | **Khớp** | Execution log |
| 6 | Critical bug còn mở | 0 | 0 | **Khớp** | Bug summary được cung cấp |
| 7 | Major bug còn mở | 3 | 3 | **Khớp** | Bug summary được cung cấp |
| 8 | Minor bug còn mở | 4 | 4 | **Khớp** | Bug summary được cung cấp |
| 9 | Tổng bug còn mở | 7 | 7 | **Khớp** | 3 Major + 4 Minor |
| 10 | Failed – UC06-FUN-006 | 1 | 1 | **Khớp** | Failed list |
| 11 | Failed – UC06-FUN-008 | 1 | 1 | **Khớp** | Failed list |
| 12 | Failed – UC06-FUN-010 | 1 | 1 | **Khớp** | Failed list |
| 13 | Failed – UC06-FUN-018 | 1 | 1 | **Khớp** | Failed list |
| 14 | Failed – UC18-FUN-006 | 1 | 1 | **Khớp** | Failed list |
| 15 | Failed – UC18-INT-001 | 1 | 1 | **Khớp** | Failed list |
| 16 | Failed – UC18-INT-003 | 1 | 1 | **Khớp** | Failed list |
| 17 | Tổng Failed list | 7 | 7 | **Khớp** | 4 UC06 + 3 UC18 |

## 3. Kiểm tra phép cộng execution

```text
Passed + Failed + Blocked
= 41 + 7 + 4
= 52
```

→ **Khớp Tổng test case.**

## 4. Kiểm tra bug severity

```text
Critical + Major + Minor
= 0 + 3 + 4
= 7
```

→ **Khớp Tổng bug còn mở được cung cấp.**

## 5. Điểm cần lưu ý

| Vấn đề | Trạng thái |
|---|---|
| Có 7 Failed test case nhưng chỉ một phần đã có Bug ID trong execution log | **Cần bổ sung traceability** |
| 4 Blocked test case nhưng chỉ có một số nguyên nhân Blocked được cung cấp | **Cần bổ sung evidence/reason** |
| Không có số liệu chứng minh tất cả bug đã được regression/re-test | **Chưa thể xác nhận exit criterion** |
| Không có số liệu phê duyệt của QA/Test Lead/Stakeholder | **Chưa thể xác nhận exit criterion** |

> **Kết luận number check:** Các con số execution và bug severity được dùng trong report đều khớp với data gốc được cung cấp. Các phần thiếu là **evidence/traceability**, không phải số học.
