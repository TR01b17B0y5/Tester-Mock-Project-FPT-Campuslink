## 3.18 UC18: View interview schedule details

### 3.18.1 Overview

| Field | Content |
|---|---|
| Name | View interview schedule details |
| Description | This use case allows user to view an interview schedule |
| Actor | Role A, Role B, Role C, Role D |
| Trigger | User clicks View in the interview schedule screen |
| Pre-condition | User has logged into system as Role A, Role B, Role C |
| Post-condition | System shows interview schedule details |

Ghi chu: Role A = Recruiter, Role B = Manager, Role C = Admin, Role D = Interviewer (xem masking_glossary.md)

### 3.18.2 Flow of events

#### 3.18.2.1 Basic Flow

| Step | Actor | Action | Next |
|---|---|---|---|
| 6 | User (Role A/B/C) | Click "View" icon in interview schedule list | 7 |
| 7 | System | Show interview schedule details | 8 |
| 8 | System | Flow ends | N/A |

### 3.18.3 Screen Components (mo ta thay cho mockup)

**Man hinh 1 - Interview schedule details (hien thi cho Role A, Role B)**

| Vi tri | Thanh phan | Ten field da mask | Loai control | Mo ta |
|---|---|---|---|---|
| 1 | Ten module | LabelA | Label | Hien thi ten module "interview schedule" |
| 2 | Ten sub-module (breadcrumb) | BreadcrumbA | Breadcrumb | Hien thi duong dan "Interview Schedule List > New Interview Schedule" |
| 4 | Schedule title | TextboxA | Label/Text | Hien thi tieu de lich phong van |
| - | Candidate name | TextboxH | Label/Text | Hien thi ten ung vien (du lieu nguoi dung nhap) |
| - | Schedule Time | DatetimeB | Label/Date time | Hien thi ngay gio phong van, dinh dang DD/MM/YYYY, From HH:MM To HH:MM |
| 5 | Interviewer | ComboboxA | Label/Box | Hien thi nguoi phong van (da mask theo UserX) |
| 9 | Location | TextboxB | Label/Text | Hien thi dia diem phong van |
| 10 | Job | TextboxC | Label/Text | Hien thi ten vi tri tuyen dung |
| 11 | Recruiter owner | TextboxD | Label/Text | Hien thi nguoi phu trach (da mask theo UserX) |
| - | Meeting ID | LinkuploadA | Label/Link | Duong dan phong hop truc tuyen (du lieu nguoi dung nhap) |
| 13 | Notes | TextboxE | Label/Text | Hien thi ghi chu |
| 14 | Status | TextboxF | Label/Text | Hien thi trang thai lich phong van |
| 16 | Results | TextboxG | Label/Text | Hien thi ket qua do Role D nhap, neu chua co hien thi "N/A" |
| 18 | ButtonA | Button | N/A | Khi user click ButtonA, he thong hien thi man hinh Edit interview schedule. Trigger UC20. Ap dung cho Role A, Role B, Role C |
| 19 | ButtonB | Button | N/A | Khi click, quay lai man hinh truoc do |
| 21 | Created on | LabelC | Label | Hien thi ngay tao. Neu ngay tao = hom nay -> hien "today". Neu khac -> hien DD/MM/YYYY |
| 22 | Last updated by | LabelD | Label | Hien thi tai khoan va thoi gian cap nhat gan nhat (ten day du da mask theo UserX; neu ngay cap nhat = hom nay -> hien "today", khac -> hien DD/MM/YYYY) |
| 23 | ButtonD | Button | N/A | Click de trigger UC22 (gui nhac lich). Ap dung cho Role A, Role B, Role C |

**Man hinh 2 - Interview schedule details (hien thi cho Role D)**

Tuong tu man hinh 1, nhung khong co field "Recruiter owner", va thay ButtonA/ButtonB bang:

| Vi tri | Thanh phan | Ten field da mask | Loai control | Mo ta |
|---|---|---|---|---|
| 20 | ButtonC | Button | N/A | Chi ap dung cho Role D. Click de chuyen sang man hinh Submit result, gui ket qua phong van. Trigger UC19 |
| 19 | ButtonB | Button | N/A | Khi click, quay lai man hinh truoc do |

### 3.18.4 Business Rules

| Business Rule ID | Business Rule Description |
|---|---|
| N/A | N/A |
