# 📋 System Specifications

> *Status: DRAFT.* Tài liệu này định nghĩa đặc tả kỹ thuật — yêu cầu, ràng buộc,
> và các quyết định kỹ thuật xuyên suốt dự án.
> Kiến trúc thiết kế (phân tầng, API, interface contracts) nằm ở [architecture.md](architecture.md).
>
> Các mục đánh dấu `(?)` là những **quyết định chưa đưa ra** — cần giải quyết
> trước khi phase tiếp theo bắt đầu.

---

## Mục lục

- [1. Mục tiêu & Phạm vi dự án](#1-mục-tiêu--phạm-vi-dự-án)
- [2. Yêu cầu chức năng](#2-yêu-cầu-chức-năng)
- [3. Yêu cầu phi chức năng](#3-yêu-cầu-phi-chức-năng)
- [4. Đặc tả phần cứng](#4-đặc-tả-phần-cứng)
- [5. Đặc tả firmware](#5-đặc-tả-firmware)
- [6. Đặc tả software](#6-đặc-tả-software)
- [7. Giao tiếp giữa các thành phần](#7-giao-tiếp-giữa-các-thành-phần)
- [8. Tài liệu tham khảo](#8-tài-liệu-tham-khảo)
- [9. Open Questions](#9-open-questions)

---

## 1. Mục tiêu & Phạm vi dự án

### 1.1 Mục tiêu

Dự án được thực hiện nhằm học tập, giúp hiểu hơn về ML trong việc nhận diện cử chỉ tay.

### 1.2 Phạm vi MVP (Minimum Viable Product)

**Trong scope MVP:**
- Detect được 2 bàn tay
- Phát hiện được các cử chỉ của bàn tay
- Thiết kế các 

**Ngoài scope MVP (làm sau):**
- Phát triển lên trong việc nhận diện cử chỉ tay vào ngôn ngữ hình thể

---

## 2. Yêu cầu chức năng (Functional Requirements)

| ID | Yêu cầu | Mức ưu tiên | Ghi chú |
|----|---------|-------------|---------|
| FR-01 | (?) | Cao / Trung / Thấp | |
| FR-02 | (?) | | |

> Thêm dòng khi có yêu cầu mới.

---

## 3. Yêu cầu phi chức năng (Non-Functional Requirements)

| ID | Yêu cầu | Giá trị mục tiêu | Ghi chú |
|----|---------|-------------------|---------|
| NFR-01 | Thời gian đáp ứng | ≤ (?) ms | |
| NFR-02 | Kích thước / Khối lượng | (?) | *(nếu có ràng buộc vật lý)* |
| NFR-03 | Nguồn điện / Năng lượng | (?) | *(nếu dùng pin)* |

> Thêm / bớt dòng tùy dự án. Không phải dự án nào cũng cần tất cả.

---
## 4. Đặc tả software

> *Bỏ section này nếu dự án không có software host/PC/mobile.*

| Thuộc tính | Giá trị |
|-----------|---------|
| Nền tảng | (?) *(PC / Web / Mobile / …)* |
| Ngôn ngữ | (?) *(Python / C# / JS / …)* |
| Framework / UI | (?) *(PyQt / Electron / React / …)* |
| Chức năng chính | (?) *(GUI hiển thị data / calibration / logging / …)* |

---

## 5. Tài liệu tham khảo

| Loại | Tên | Link / File |
|------|-----|-------------|
| Datasheet | (?) | |
| App Note | (?) | |
| Thư viện | (?) | |

> Đặt file PDF vào `docs/datasheets/` nếu cần lưu offline.

---

## 6. Open Questions — Các quyết định chưa đưa ra

> Tracking câu hỏi thiết kế cần giải quyết. Khi resolved → ghi kết quả và chuyển lên mục tương ứng.

| # | Câu hỏi | Trạng thái | Kết quả |
|---|---------|-----------|---------|
| Q1 | (?) | ⬜ Open | |

> Đánh dấu: ⬜ Open · ✅ Resolved · ❌ Dropped

---

*Cập nhật lần cuối: <!-- DATE -->*
