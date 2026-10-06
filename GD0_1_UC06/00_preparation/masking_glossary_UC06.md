# MASKING GLOSSARY - UC06 (Create new candidate)

**CANH BAO: FILE NAY CHI GIU OFFLINE. TUYET DOI KHONG UPLOAD LEN AI HOAC GUI CHO HUMAN REVIEW.**
File nay dung de doi chieu nguoc lai giua du lieu that va du lieu da mask trong file `UC06_clean.md`.

## 1. URL / Domain

| Gia tri that | Gia tri da mask |
|---|---|
| https://ims.recruitment.com/candidate-list | https://app.example.local/candidate-list |

## 2. Ten cong ty / he thong

| Gia tri that | Gia tri da mask |
|---|---|
| HR Department (hien thi tren header) | Company |
| IMS (Interview / Recruitment Management System) | HRU System |

## 3. Vai tro noi bo (Role)

Dung nhat quan voi UC18, UC21:

| Gia tri that | Gia tri da mask |
|---|---|
| Recruiter | Role A |
| Manager | Role B |
| Admin | Role C |
| Interviewer | Role D |

## 4. Ten nguoi dung / tai khoan

| Gia tri that | Gia tri da mask |
|---|---|
| hoannk | UserA (da dung o UC18) |
| Hoang Tuan Anh (AnhHT7) - vi du gia tri Recruiter owner trong mockup | UserG |

## 5. Ten cac field (Screen Description)

| Gia tri that | Gia tri da mask | Loai control |
|---|---|---|
| Name of module | LabelA | Label |
| Name of sub-module | BreadcrumbA | Breadcrumb |
| Name of function | LabelB | Label |
| Personal information | LabelC | Label |
| Full name | TextboxA | Textbox |
| Email | TextboxB | Textbox |
| Gender | ComboboxA | Combo-box |
| D.O.B | DateA | Icon + textbox |
| Address | TextboxC | Textbox |
| Phone number | TextboxD | Textbox |
| Status | ComboboxF | Combo-box (REF khong day du trong tai lieu goc) |
| Professional information | LabelD | Label |
| CV Attachment | UploadA | Textbox + file attachment |
| Current position | ComboboxB | Combo-box |
| Skills | ComboboxC | Combo-box |
| Years of experience | TextboxE | Text field |
| Highest level | ComboboxD | Combo-box |
| Recruiter owner | ComboboxE | Combo-box |
| Assign me | LinkButtonA | Button link |
| Note | TextboxF | Textbox |

## 6. Ten cac button

| Gia tri that | Gia tri da mask |
|---|---|
| Submit | ButtonA |
| Cancel | ButtonB |

## 7. Ghi chu

- Cac ma loi (ME002, ME009, ME010, ME011, ME012) la ma he thong dung chung, khong phai du lieu nhay cam nen giu nguyen trong UC06_clean.md.
- Anh mockup (Pic.05 - Create new candidate screen) khong duoc upload; da thay bang bang mo ta component trong UC06_clean.md.
- Truong "Status" xuat hien trong mockup nhung phan REF trong tai lieu goc gui cho AI Fable bi thieu (gap giua REF10 va REF12, REF13 va REF15); da danh dau ro trong UC06_clean.md de nguoi review biet day la thong tin suy ra tu mockup, khong phai tu bang Screen Description day du.
- Mapping Role A/B/C/D va UserA giu nguyen theo cac UC truoc (UC18, UC21) de dam bao tinh nhat quan khi dua nhieu UC vao chung 1 knowledge base tren Dify.
