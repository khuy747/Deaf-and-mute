# 🏗️ System Architecture

> *Status: DRAFT.* Tài liệu này mô tả kiến trúc và thiết kế hệ thống.
> Đặc tả kỹ thuật (yêu cầu, linh kiện, thông số) nằm ở [specs.md](specs.md).
>
> Các mục đánh dấu `(?)` là những **quyết định chưa đưa ra** — cần giải quyết
> trước khi phase tiếp theo bắt đầu.

---

## Mục lục

- [1. Nguyên tắc thiết kế](#1-nguyên-tắc-thiết-kế)
- [2. Tổng quan hệ thống](#2-tổng-quan-hệ-thống)
  - [2.1 Sơ đồ khối](#21-sơ-đồ-khối)
  - [2.2 Giải thích luồng hoạt động](#22-giải-thích-luồng-hoạt-động)
- [3. Interface Contracts — Giao kèo giữa các module](#3-interface-contracts--giao-kèo-giữa-các-module)
  - [3.1 Peri_MOTOR → Application](#31-peri_motor--application)
  - [3.2 Peri_IR → Application](#32-peri_ir--application)
  - [3.3 Algorithm → Application](#33-algorithm--application)

---

## 1. Nguyên tắc thiết kế

*(Những triết lý xuyên suốt khi đưa ra mọi quyết định trong dự án.)*

| # | Nguyên tắc | Giải thích |
|---|-----------|------------|
| 1 | (?) | *(ví dụ: "Modular — mỗi module có interface rõ ràng, thay thế được")* |
| 2 | (?) | *(ví dụ: "Đơn giản trước — làm cho chạy rồi mới tối ưu")* |
| 3 | (?) | *(ví dụ: "Giá rẻ — dùng linh kiện phổ biến, dễ mua")* |

---

## 2. Tổng quan hệ thống

### 2.1 Sơ đồ khối

```
┌───────────────────────────────────────────────┐
│                  Host / PC                    │
└───────────────────────┬───────────────────────┘
                        │
┌───────────────────────┼───────────────────────┐
│                       ▼                       │
│                  MCU (?)                      │
│                                               │
│  ┌─────────────────────────────────────────┐  │
│  │  Application   (main.c, app logic)      │  │
│  ├─────────────────────────────────────────┤  │
│  │  Algorithm     (algo_*/)                │  │
│  ├─────────────────────────────────────────┤  │
│  │  Peri Drivers  (peri_*/)                │  │
│  ├─────────────────────────────────────────┤  │
│  │  HAL / CMSIS   (IDE-managed)            │  │
│  └─────────────────────────────────────────┘  │
│                       │                       │
│          ┌────────────┴────────────┐          │
│          │    Peripherals (?)      │          │
│          └─────────────────────────┘          │
│                                               │
└───────────────────────┬───────────────────────┘
                        │
┌───────────────────────┼───────────────────────┐
│                       ▼                       │
│                  Hardware                     │
└───────────────────────────────────────────────┘
```

> Thay thế bằng sơ đồ chính xác khi thiết kế phần cứng hoàn thiện.

### 2.2 Giải thích luồng hoạt động

*(Mô tả bằng lời: data chảy thế nào từ sensor → MCU → xử lý → actuator? Host can thiệp ở đâu?)*

(?)

---

## 3. Interface Contracts — Giao kèo giữa các module

> Mỗi module chỉ giao tiếp qua API đã định nghĩa.
> Sửa nội bộ module → OK. Sửa interface → phải thông báo tất cả module liên quan.
>
> **Status:** ⬜ Chưa implement · ✅ Đã implement + test pass

### 3.1 Peri_MOTOR → Application

```c
// Interface mà Application sẽ gọi:
void    Motor_Init(void);                              // ⬜
void    Motor_SetSpeed(MotorID id, int8_t percent);    // ⬜  -100 đến +100
void    Motor_Stop(void);                              // ⬜
int32_t Encoder_GetCount(EncoderID id);                // ⬜
void    Encoder_Reset(EncoderID id);                   // ⬜
```

> (?) — điền khi viết driver thật. Đây là mẫu.

### 3.2 Peri_IR → Application

```c
void     IR_Init(void);                                           // ⬜
uint16_t IR_Read(IR_Channel ch);                                  // ⬜  Trả về giá trị ADC raw
bool     IR_IsWallDetected(IR_Channel ch, uint16_t threshold);    // ⬜
```

> (?)

### 3.3 Algorithm → Application

```c
// PID không gọi HAL — nhận data qua parameters
void  PID_Init(PID_Controller *pid, float Kp, float Ki, float Kd);         // ⬜
float PID_Compute(PID_Controller *pid, float setpoint, float measured);    // ⬜
void  PID_Reset(PID_Controller *pid);                                      // ⬜
```

> (?)

---

*Cập nhật lần cuối: <!-- DATE -->*
