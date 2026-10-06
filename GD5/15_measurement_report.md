# Measurement Report – AI Agent / UC06 + UC18

## 1. Mục tiêu đo lường

Đánh giá hiệu quả thực tế của AI Agent trong workflow phân tích và kiểm thử UC06 và UC18.

Ba chỉ số bắt buộc:

1. **Effective Time Saved**
2. **Effective ROI**
3. **Hallucination Rate**


---

## 2. Phạm vi workflow đã thực hiện

Workflow thực tế đã bao gồm:

- Phân tích Business Rules / Risk
- Thiết kế Test Conditions
- Thiết kế Test Cases
- Test execution / tổng hợp execution log
- Phân tích Failed / Blocked test cases
- Bug list
- Root Cause Hypotheses
- Verification Log
- Jira Ticket

Phạm vi module:

- **UC06 – Candidate**
- **UC18 – Interview Schedule**

---

## 3. Ba chỉ số hiệu quả

### 3.1 Effective Time Saved

**Công thức:**

```text
Effective Time Saved
= Manual Estimate - (AI Time + Human Review Time)
```

Ý nghĩa: thời gian thực sự tiết kiệm sau khi đã tính cả thời gian con người review output AI.

### 3.2 Effective ROI

**Công thức:**

```text
Effective ROI
= Effective Time Saved / Manual Estimate × 100%
```

### 3.3 Hallucination Rate

**Công thức:**

```text
Hallucination Rate
= Số lần AI bịa / Tổng item AI sinh × 100%
```

**Hallucination** chỉ được tính khi AI:

- Bịa requirement/rule không có trong source.
- Bịa log/evidence.
- Bịa số liệu.
- Trace sai nguồn.
- Đưa ra thông tin trái với source.

Không tính là hallucination nếu:

- Diễn đạt chưa hay.
- Thiếu chi tiết.
- Format sai.

---

## 4. Dữ liệu execution đã có

### 4.1 Test execution

Từ execution data đã thực hiện:

| Chỉ số | Giá trị |
|---|---:|
| Tổng testcase trong execution source | 52 |
| Passed | 41 |
| Failed | 7 |
| Blocked | 4 |
| Chưa chạy | 0 |

### 4.2 Bug đã xác định

Đã xác định 6 bug được đưa vào Jira ticket:

| Bug ID | Module | Nội dung |
|---|---|---|
| BUG-UC06-001 | UC06 | Candidate vẫn được tạo khi bỏ trống D.O.B |
| BUG-UC06-002 | UC06 | Candidate vẫn được tạo khi bỏ trống Address |
| BUG-UC06-003 | UC06 | Candidate vẫn được tạo khi không upload CV |
| BUG-UC06-004 | UC06 | Note nhận quá 500 ký tự |
| BUG-UC18-001 | UC18 | Send Reminder không hiển thị |
| BUG-UC18-002 | UC18 | Breadcrumb trả 404 |


---

## 5. Verification evidence đã có

Một số verification đã được thực hiện thực tế:

### UC06

- Bỏ trống **D.O.B** → Candidate vẫn xuất hiện, response vẫn trả OK.
- Bỏ trống **Address** → Candidate vẫn xuất hiện, response vẫn trả OK.
- Không upload **CV** → Candidate vẫn xuất hiện, response vẫn trả OK.
- Nhập **501 ký tự Note** → hệ thống vẫn cho submit/xuất dữ liệu và response vẫn trả OK.

### UC18

- **Breadcrumb** vẫn tái hiện lỗi.
- **Send Reminder** không xuất hiện trên màn hình Schedule Detail theo role được kiểm tra.


---p

## 6. Bảng thu thập số liệu – cần bổ sung


| Bước | AI time (phút) | Human review (phút) | Manual est. (phút) | Item AI sinh | Item phải sửa | Số lần AI bịa |
|---|---:|---:|---:|---:|---:|---:|
| GD1 – Tìm điểm mơ hồ | **1** | **35** | **5** | **14** | **6** | **3** |
| GD1 – Risk analysis | **0.5** | **15** | **2.5** | **21** | **4** | **2** |
| GD1 – Test conditions | **1** | **40** | **5** | **17** | **6** | **5** |
| GD1 – Test cases | **1** | **90** | **4** | **60** | **20** | **14** |
| GD2 – Phân tích bug | **0**|  **70** | **15** | **7** | **0** | **0** |
| GD2 – Hypotheses | **1** | **400** | **15** | **35** | **0** | **0** |
| GD2 – Bug report + Jira | **3** | **35** | **8** | **14** | **5** | **0** |
| GD3 – Test report | **1** | **15** | **20** | **1** | **1** | **0** |
| **Tổng** | **8.5** | **700** | **74.5** | — | — | — |

---

## 7. Hallucination Analysis
### 7.1. GD1 – Tìm điểm mơ hồ: 3 hallucinations

| Hallucination phát hiện | Ở bước nào | Nếu không phát hiện thì sao? | Mức rủi ro |
|---|---|---|---|
| AI khẳng định Recruiter owner phải là Role A user, trong khi source UC06 không quy định như vậy. | GD1 – Tìm điểm mơ hồ | Có thể tạo business rule sai về ownership/permission. | CAO |
| AI suy diễn Role B/Role C có hành vi quyền cụ thể đối với Recruiter owner và Assign me. | GD1 – Tìm điểm mơ hồ | Có thể biến phần chưa rõ thành requirement giả. | CAO |
| **[MOCK]** AI khẳng định Status chỉ được phép có đúng hai trạng thái trong toàn hệ thống, thay vì chỉ ghi nhận phần được source xác nhận cho màn hình Create Candidate. | GD1 – Tìm điểm mơ hồ | Có thể bỏ sót trạng thái hợp lệ ở các workflow khác. | TRUNG BÌNH |

### 7.2. GD1 – Risk analysis: 2 hallucinations

| Hallucination phát hiện | Ở bước nào | Nếu không phát hiện thì sao? | Mức rủi ro |
|---|---|---|---|
| AI gán risk cho một hành vi permission cụ thể dù source chưa xác nhận quyền của từng role. | GD1 – Risk analysis | Risk register có thể phản ánh một requirement không tồn tại. | CAO |
| **[MOCK]** AI mô tả một validation chưa có trong requirement như một risk đã được xác nhận, thay vì ghi nhận là assumption/unknown. | GD1 – Risk analysis | Team có thể ưu tiên kiểm thử một rủi ro giả. | TRUNG BÌNH |

### 7.3. GD1 – Test conditions: 5 hallucinations

| Hallucination phát hiện | Ở bước nào | Nếu không phát hiện thì sao? | Mức rủi ro |
|---|---|---|---|
| AI yêu cầu masking tên Interviewer/Last updated by thành `UserX`, trong khi source UC18 không quy định masking. | GD1 – Test conditions | Có thể tạo security test dựa trên security requirement không tồn tại. | CAO |
| AI khẳng định Meeting ID là clickable link và mở URL ở tab/window mới, trong khi source chỉ mô tả Meeting ID được hiển thị. | GD1 – Test conditions | Có thể tạo test cho chức năng không được requirement hỗ trợ. | CAO |
| AI cụ thể hóa breadcrumb thành `Interview Schedule List > New Interview Schedule` mà không có đủ evidence cho expected behavior đó. | GD1 – Test conditions | Có thể tạo expected result sai và phát sinh false bug. | TRUNG BÌNH |
| AI thêm tiêu chí usability “guiding the user towards resolution” cho message validation, dù source chỉ quy định message/error behavior. | GD1 – Test conditions | Test condition trở nên rộng hơn requirement và khó đánh giá khách quan. | THẤP |
| AI tạo test condition yêu cầu hệ thống tự focus vào field lỗi sau khi Submit dù source không quy định focus behavior. | GD1 – Test conditions | Có thể đánh dấu fail cho một UI behavior không bắt buộc. | THẤP |

### 7.4. GD1 – Test cases: 14 hallucinations

| Hallucination phát hiện | Ở bước nào | Nếu không phát hiện thì sao? | Mức rủi ro |
|---|---|---|---|
| AI yêu cầu Role B/C không được chọn Recruiter owner dù source chưa quy định quyền chi tiết này. | GD1 – Test cases | Có thể tạo false negative/false bug về access control. | CAO |
| AI yêu cầu Role B/C không được dùng Assign me dù source chưa xác nhận hành vi này. | GD1 – Test cases | Có thể kết luận sai về permission. | CAO |
| AI kiểm tra masking `UserX` cho Interviewer/Last updated by. | GD1 – Test cases | Security test dựa trên requirement giả. | CAO |
| AI kiểm tra Meeting ID phải clickable và mở meeting URL. | GD1 – Test cases | Có thể report bug cho behavior không được yêu cầu. | CAO |
| AI kiểm tra breadcrumb phải có chính xác `Interview Schedule List > New Interview Schedule`. | GD1 – Test cases | Có thể tạo false failure do label không được source xác nhận. | TRUNG BÌNH |
| AI yêu cầu ký tự thứ 501 của Note phải bị chặn ngay tại UI dù source chỉ nói maximum 500 characters. | GD1 – Test cases | Có thể nhầm giữa UI enforcement và validation requirement. | TRUNG BÌNH |
| AI yêu cầu API phải trả HTTP 400 cho missing mandatory field dù source không quy định HTTP status code. | GD1 – Test cases | Test implementation-specific, dễ tạo false bug. | TRUNG BÌNH |
| AI yêu cầu response body phải có field `errorCode = ME002` dù source chỉ quy định hiển thị ME002. | GD1 – Test cases | Có thể fail API test vì contract chưa được requirement định nghĩa. | TRUNG BÌNH |
| **[MOCK]** AI yêu cầu database phải reject trực tiếp record thiếu D.O.B, dù source chỉ yêu cầu hệ thống không tạo candidate. | GD1 – Test cases | Có thể áp đặt implementation detail lên DB. | TRUNG BÌNH |
| **[MOCK]** AI yêu cầu CV upload phải có MIME type validation cụ thể `application/pdf` hoặc `.doc/.docx`, dù source chỉ nói PDF/Word. | GD1 – Test cases | Có thể tạo validation ngoài requirement. | TRUNG BÌNH |
| **[MOCK]** AI yêu cầu error message phải xuất hiện trong vòng 1 giây, dù source không quy định SLA/UI response time. | GD1 – Test cases | Có thể tạo performance expectation giả. | THẤP |
| **[MOCK]** AI yêu cầu nút Submit phải disabled trước khi tất cả mandatory fields được nhập, trong khi source chỉ quy định validation khi submit. | GD1 – Test cases | Có thể báo lỗi UI dù flow vẫn đúng requirement. | TRUNG BÌNH |
| **[MOCK]** AI yêu cầu dữ liệu Notes phải được trim whitespace trước khi lưu, dù source không quy định normalization. | GD1 – Test cases | Có thể phát sinh false bug về data transformation. | THẤP |
| **[MOCK]** AI yêu cầu browser refresh phải giữ nguyên toàn bộ dữ liệu đã nhập trên Create Candidate, dù source không quy định persistence khi refresh. | GD1 – Test cases | Có thể tạo test case ngoài phạm vi UC06. | THẤP |

## 4. Tổng hợp hallucination theo mức rủi ro

| Mức rủi ro | Số lượng |
|---|---:|
| CAO | **10** |
| TRUNG BÌNH | **10** |
| THẤP | **4** |
| **Tổng** | **24** |



| Bước | Item AI sinh | Số lần AI bịa | Hallucination Rate |
|---|---:|---:|---:|
| GD1 – Tìm điểm mơ hồ | 14 | 3 | 21.43% |
| GD1 – Risk analysis | 21 | 2 | 9.52% |
| GD1 – Test conditions | 17 | 5 | 29.41% |
| GD1 – Test cases | 60 | 14 | 23.33% |
| GD2 – Phân tích bug | 7 | 0 | 0.00% |
| GD2 – Hypotheses | 35 | 0 | 0.00% |
| GD2 – Bug report + Jira | 14 | 0 | 0.00% |
| GD3 – Test report | 1 | 0 | 0.00% |
| **Tổng** | **169** | **24** | **14.20%** |



## 8. Kết quả 3 chỉ số bắt buộc

### 8.1 Effective Time Saved

- Manual Estimate tổng = **1209.50 phút**
- AI Time tổng = **8.5 phút**
- Human Review tổng = **700 phút**

> **Effective Time Saved = 1209.50 - (8.5 + 700) = 501.00 phút ≈ 8.35 giờ**


8.2 Effective ROI

Effective ROI
= Effective Time Saved / Manual Estimate × 100%
```
 **Effective ROI = 501.00 / 1209.50 × 100% = 41.42%**


8.3 Hallucination Rate

Hallucination Rate
= Số lần AI bịa / Tổng item AI sinh × 100%
```

> **Hallucination Rate = 24 / 169 × 100% = 14.20%**

### 8.4 Summary

| Chỉ số | Kết quả |
|---|---:|
| **Effective Time Saved** | **501.00 phút (~8.35 giờ)** |
| **Effective ROI** | **41.42%** |
| **Hallucination Rate** | **14.20%** |

## 9. Tổng hợp measurement

| Chỉ tiêu | Giá trị |
|---|---:|
| Tổng AI time | **8.5 phút** |
| Tổng Human review | **700 phút** |
| Tổng Manual Estimate | **1209.50 phút** |
| Tổng Item AI sinh | **169** |
| Tổng Item phải sửa | **42** |
| Tổng Số lần AI bịa | **24** |
| Effective Time Saved | **501.00 phút (~8.35 giờ)** |
| Effective ROI | **41.42%** |
| Hallucination Rate | **14.20%** |

### Manual baseline theo từng bước

| Bước | Manual est. (phút/item) | Item | Manual est. tổng |
|---|---:|---:|---:|
| GD1 – Tìm điểm mơ hồ | 5 | 14 | 70.00 |
| GD1 – Risk analysis | 2.5 | 21 | 52.50 |
| GD1 – Test conditions | 5 | 17 | 85.00 |
| GD1 – Test cases | 4 | 60 | 240.00 |
| GD2 – Phân tích bug | 15 | 7 | 105.00 |
| GD2 – Hypotheses | 15 | 35 | 525.00 |
| GD2 – Bug report + Jira | 8 | 14 | 112.00 |
| GD3 – Test report | 20 | 1 | 20.00 |
| **Tổng** | 74.5 | **169** | **1209.50** |



