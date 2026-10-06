# 06 Self-Review Log – UC06: Create new candidate

## 1. Trả lời Human Review

### HR3-01 – AI Self-Review tự tìm được BAO NHIÊU vấn đề thật?

Output AI có **19 mục phát hiện** được chia thành:

| Nhóm | Số mục |
|---|---:|
| Hallucination | 3 |
| Traceability | 7 |
| Coverage | 6 |
| Priority | 0 |
| Quality | 3 |
| **Tổng** | **19** |

Trong 19 mục này:

- **17 mục có thể đối chiếu trực tiếp với UC06 và được tài liệu cung cấp hỗ trợ.**
- **2 mục không thể xác nhận độc lập từ nguồn hiện có** vì cần xem nội dung test case đầy đủ:
  - Expected Result của `TC-UC06-USA-002-01` có thực sự mâu thuẫn hay không.
  - Expected Result của tất cả test case có thực sự bị cắt ngắn hay không.

Lưu ý: 19 là **số phát hiện được liệt kê**, không phải 19 lỗi hoàn toàn độc lập. Một số phát hiện bị overlap giữa Hallucination, Traceability và Quality.

---

### HR3-02 – AI có SÓT vấn đề nào mà học viên/người review đã chỉ? So sánh 2 con số

**Không thể tính chính xác số vấn đề AI sót so với Human Review từ nguồn hiện tại**, vì ảnh HR3 chỉ chứa câu hỏi Human Review, không chứa danh sách lỗi do học viên/người review phát hiện.

Do đó:

| Chỉ số | Kết quả |
|---|---:|
| AI tự tìm được | 19 phát hiện |
| Human Review tìm được | Chưa có dữ liệu |
| AI bỏ sót so với Human | Chưa thể xác định |
| Tỷ lệ overlap AI ↔ Human | Chưa thể tính |

Không tự suy đoán số lỗi Human Review để tránh làm sai chỉ số đánh giá.

---

### HR3-03 – AI có báo vấn đề giả để tránh "có review" không?

**Không phát hiện vấn đề giả rõ ràng trong 17 mục có thể kiểm chứng từ tài liệu UC06.**

Các phát hiện có cơ sở gồm:

- `BR-UC06-01`, `BR-UC06-02`, `BR-UC06-03` không phải ID Business Rule gốc trong UC.
- Permission Role B/C không được đặc tả trong UC.
- Validation file attachment không được đặc tả đầy đủ.
- Button Cancel chưa có test case.
- Phone number chưa có validation riêng.
- Note 500 ký tự chưa có test case.
- ME011 chưa có test case.
- ME010 chưa có coverage rõ ràng.
- Các nguồn traceability không liên quan bị gắn vào một số test case.

Có **2 phát hiện chưa thể xác nhận** vì không có toàn bộ test case source để đối chiếu:

1. `TC-UC06-USA-002-01` có Expected Result mâu thuẫn.
2. Expected Result của tất cả test case bị cắt ngắn.

Vì vậy không nên đánh dấu 2 mục này là false positive; trạng thái phù hợp là **Unverified**.

---

### HR3-04 – Kiếm bằng Traceability? Có GAP nào không?

**Có. Traceability có nhiều GAP.**

Các GAP/traceability lỗi mà AI tìm được:

| Test Case | Vấn đề |
|---|---|
| `TC-UC06-SEC-001-01,02,03` | `BR-UC06-03` không tồn tại trong UC |
| `TC-UC06-USA-002-01` | `BR-UC06-03` không tồn tại trong UC |
| `TC-UC06-FUN-002-01,02,03,04` | `BR-UC06-01` không phải source ID gốc; source đúng là `BRL-6-01` |
| `TC-UC06-FUN-004-01,02,03,04` | `BR-UC06-02` không phải source ID gốc; source đúng là `BRL-6-02` |
| `TC-UC06-FUN-003-01,02,03,04,05` | `BRL-6-03`, `BRL-6-04` không phải source cho attachment validation |
| `TC-UC06-USA-001-01` | `BRL-6-01`, `BRL-6-03`, `BRL-6-04` không phải source trực tiếp cho ME012 |
| `TC-UC06-USA-001-02` | `BRL-6-03`, `BRL-6-04` không phải source trực tiếp cho ME002 |
| `TC-UC06-USA-001-03` | `BRL-6-01`, `BRL-6-04` không phải source trực tiếp cho ME009 |

### Coverage GAP được AI xác định

- Screen Component 23 – `Cancel`.
- Phone number validation.
- Một số mandatory fields chưa có validation riêng.
- Note maximum 500 characters.
- ME011 – `Failed to created candidate`.
- ME010 – coverage/Expected Result chưa rõ ràng.

---

### HR3-05 – Test case nào phải sửa? Sửa gì?

| Test Case | Thao tác cần thực hiện |
|---|---|
| `TC-UC06-SEC-001-01,02,03` | Sửa traceability; bỏ/sửa các expectation về Role B/C nếu chưa có requirement; không dùng `BR-UC06-03` |
| `TC-UC06-FUN-002-01,02,03,04` | Đổi source `BR-UC06-01` → `BRL-6-01`; bổ sung coverage cụ thể cho mandatory fields |
| `TC-UC06-FUN-003-01,02,03,04,05` | Tách Email/DOB khỏi attachment nếu cần; bỏ source `BRL-6-03/04` khỏi attachment validation; bổ sung source chính xác cho attachment |
| `TC-UC06-FUN-004-01,02,03,04` | Đổi source `BR-UC06-02` → `BRL-6-02`; làm rõ Status visibility/editability |
| `TC-UC06-USA-001-01` | Chỉ giữ source trực tiếp liên quan đến ME012 |
| `TC-UC06-USA-001-02` | Chỉ giữ source liên quan đến ME002 |
| `TC-UC06-USA-001-03` | Chỉ giữ source liên quan đến ME009 |
| `TC-UC06-USA-002-01` | Kiểm tra và sửa Expected Result; bỏ `BR-UC06-03` nếu không phải source hợp lệ |
| GUI conditions | Bổ sung condition cho Cancel nếu mục tiêu là cover toàn bộ Screen Component |
| Functional conditions | Bổ sung Phone number, Note 500 chars, ME011 và ME010 |

---

### HR3-06 – Thời gian: AI nhanh hơn Human Review không?

Output AI có:

```text
latency = 47.124 seconds
```

Không có thời gian Human Review trong dữ liệu được cung cấp.

Do đó chưa thể kết luận AI nhanh hơn Human.

Công thức:

```text
Human Time = thời gian học viên/người review thực tế

AI Time = 47.124 giây

Time Saved = Human Time - 47.124 giây
```

Nếu Human Review mất trên `47.124 giây`, AI nhanh hơn về thời gian xử lý.

Tỷ lệ tiết kiệm thời gian:

```text
Time Saving (%) =
(Human Time - AI Time) / Human Time × 100
```

---

## 2. Chốt bản Test Case cuối cùng

### Trạng thái hiện tại

**CHƯA CHỐT FINAL ngay ở phiên bản hiện tại.**

Các thay đổi bắt buộc trước khi chốt:

1. Sửa toàn bộ traceability ID không hợp lệ.
2. Loại bỏ hoặc đánh dấu `Needs Clarification` đối với expectation không có nguồn requirement.
3. Sửa Expected Result của `TC-UC06-USA-002-01` nếu đối chiếu test case xác nhận có mâu thuẫn.
4. Bổ sung test condition/test case cho `Cancel`.
5. Bổ sung Phone number validation.
6. Bổ sung Note maximum 500 characters.
7. Bổ sung ME011.
8. Bổ sung coverage rõ ràng cho ME010.
9. Bổ sung coverage cụ thể cho các mandatory fields.
10. Làm rõ attachment validation.
11. Làm rõ Status và không tự suy diễn các permission chưa có trong UC.

### Final decision

```text
TEST CASE STATUS = NEED REVISION
```

Sau khi hoàn thành các thay đổi trên:

```text
FINAL TEST CASE = READY FOR BASELINE
```

---

## 3. Số liệu dùng cho báo cáo

| Metric | Giá trị |
|---|---:|
| AI self-review findings | 19 |
| Findings có thể kiểm chứng từ UC | 17 |
| Findings chưa xác minh được | 2 |
| Human findings | Chưa có dữ liệu |
| AI missed vs Human | Chưa thể tính |
| Traceability GAP | Có |
| Coverage GAP | Có |
| False positive rõ ràng | Không phát hiện |
| AI latency | 47.124 giây |
| Final Test Case | Need Revision |

