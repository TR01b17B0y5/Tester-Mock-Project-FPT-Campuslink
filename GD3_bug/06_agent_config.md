# 06 – Agent Config

## 1. Thông tin nền tảng

| Thành phần | Giá trị |
|---|---|
| Nền tảng | Gemini Gem |
| Tên Agent | Phân tích bug |
| Model | Gemini Flash 3.5 |
| Ngôn ngữ làm việc | Tiếng Việt / English |
| Mục đích | Phân tích testcase, execution result, bug, root-cause hypothesis và verification evidence |


---

## 2. Knowledge / Files đã upload

Danh sách file hiển thị trong phần **Kiến thức (Knowledge)** của Agent:

| STT | File | Định dạng | Vai trò |
|---:|---|---|---|
| 1 | `jiraticket` | MD | Tài liệu liên quan Jira ticket |
| 2 | `bugreport` | MD | Tài liệu / mẫu bug report |
| 3 | `UC06_clean` | MD | Tài liệu UC-06 |
| 4 | `UC18_clean` | MD | Tài liệu UC-18 |
| 5 | `testcaseUC18` | MD | Bộ testcase UC-18 |
| 6 | `testcaseUC06` | MD | Bộ testcase UC-06 |
| 7 | `UC18_busin..._rules_risk` | MD | Business Rules / Risk của UC-18 |

### Ghi chú

- Danh sách trên được lấy theo **những file nhìn thấy trong ảnh cấu hình Agent**.
- Tên `UC18_busin..._rules_risk` bị rút gọn trên giao diện nên không thể xác định chính xác phần tên bị cắt; không tự suy đoán tên đầy đủ.
- Ảnh cấu hình cũng cho thấy Agent hiện đang ở trạng thái **Không có công cụ mặc định**.

---

## 3. Cấu hình Knowledge hiện tại


```

### Knowledge

Agent có các nguồn kiến thức dạng Markdown (`MD`) như danh sách ở trên.

### Phạm vi sử dụng

Các knowledge file phục vụ chủ yếu cho:

1. Phân tích yêu cầu UC-06 và UC-18.
2. Đối chiếu testcase với business rules.
3. Phân tích testcase Passed / Failed / Blocked.
4. Xác định và mô tả bug.
5. Phân tích root-cause hypotheses.
6. Verification và evidence-based conclusion.
7. Hỗ trợ tạo các tài liệu:
   - `execution.md`
   - `bug_list.md`
   - `08_hypothesises.md`
   - `08_verification_log.md`
   - các tài liệu bug analysis liên quan.

---

## 4. Nguyên tắc sử dụng dữ liệu

- Ưu tiên nội dung trong Knowledge files khi phân tích project.
- Không tự bịa Actual Result, Evidence, Severity hoặc Root Cause khi nguồn chưa cung cấp.
- Phân biệt rõ:
  - **Observed Evidence**: điều đã thực sự kiểm tra/quan sát.
  - **Hypothesis**: giả thuyết nguyên nhân.
  - **Verification**: phương pháp kiểm chứng.
  - **Confirmed Root Cause**: chỉ kết luận khi có evidence đủ mạnh.
- Khi chưa đủ evidence, sử dụng trạng thái `Not Verified` hoặc `Inconclusive` thay vì tự kết luận.
