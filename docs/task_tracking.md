# 📌 Task Tracking — Tiến độ dự án

> **File này theo dõi tổng quan phase + task-level.**
> Chia nhỏ chi tiết từng task lớn → xử lý trên nháp (Sheets, giấy, scratch) — xong bỏ được.
> Docs kết quả → ghi vào `README.md` của module / thư mục tương ứng.

---

## 📊 Tổng quan tiến độ

| Phase | Tên                        | Trạng thái | Ghi chú                |
| ----- | -------------------------- | ---------- | ---------------------- |
| 0     | Khởi tạo dự án            | ✅ Done     | Cấu trúc + docs xong  |
| 3     | Software                   | ⬜ Todo     |                        |
| 5     | Test & Release             | ⬜ Todo     |                        |

**Ký hiệu**: ✅ Done · 🔨 Đang làm · ⚠️ Blocked · ⬜ Todo

---

## 🔧 Chi tiết từng Phase

### Phase 0 — Khởi tạo dự án ✅

- [x] Tạo cấu trúc thư mục
- [x] Viết PROJECT_RULES.md
- [x] Viết specs.md (draft)
- [x] Viết task_tracking.md

---
### Phase 3 — Software ⬜

- [ ] Setup project
- [ ] Giao tiếp với firmware
- [ ] UI / chức năng chính

> *Thêm / sửa task khi bắt đầu phase này.*

---

### Phase 5 — Test & Release ⬜

- [ ] Sửa bug còn lại
- [ ] Hoàn thiện docs
- [ ] Release v1.0

---

## 🏁 Milestone chính

| #  | Milestone                              | Phase | Deadline   | Trạng thái |
| -- | -------------------------------------- | ----- | ---------- | ---------- |
| M1 | Cấu trúc repo + specs hoàn chỉnh      | 0     | *(ngày)*   | ✅         |
| M2 | Software test pass             | 2     | *(ngày)*   | ⬜         |
| M3 | Hệ thống chạy end-to-end              | 3     | *(ngày)*   | ⬜         |
| M4 | Release v1.0                           | 4     | *(ngày)*   | ⬜         |

---

## 📝 Nhật ký dự án

| Ngày       | Phase | Đã làm                              | Kết quả / Blockers        | ➡️ Việc tiếp              |
| ---------- | ----- | ----------------------------------- | -------------------------- | -------------------------- |
| *(ngày)*   | 0     | Tạo cấu trúc project template      | ✅ OK                      | Bắt đầu điền specs.md     |

---

## Hướng dẫn cập nhật

1. **Khi bắt đầu task** → tick `[ ]` thành `[/]` (đang làm), ghi 1 dòng nhật ký.
2. **Khi xong task** → tick `[x]`, viết `README.md` cho module, commit cùng code.
3. **Khi phase chuyển trạng thái** → update bảng tổng quan.
4. **Khi đạt milestone** → update bảng milestone.
5. **Chia nhỏ task lớn** → dùng nháp (Sheets / giấy / scratch) — xong bỏ được.

> 💡 Khi commit, ghi tóm tắt tiến độ phase vào commit message.
> Ví dụ: `[FW] P2.1 — driver encoder xong, test pass`
