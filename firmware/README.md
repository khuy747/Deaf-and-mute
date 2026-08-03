# ⚙️ Firmware

> Mô tả firmware của dự án.

---

## Mục lục

- [1. Thông tin](#1-thông-tin)
- [2. Cấu trúc thư mục](#2-cấu-trúc-thư-mục)
- [3. Cách build & flash](#3-cách-build--flash)
- [4. Cách test](#4-cách-test)
- [5. Module README Template](#5-module-readme-template)

---

## 1. Thông tin

| Thuộc tính | Giá trị |
|-----------|---------|
| MCU | (?) |
| IDE / Toolchain | (?) |
| HAL / Framework | (?) |
| RTOS | (?) *(bare-metal / FreeRTOS / ...)* |

---

## 2. Cấu trúc thư mục

```
firmware/
├── <project_name>/             # Project IDE
│   ├── Core/                   # Application code
│   │   ├── Src/main.c
│   │   └── Inc/
│   ├── Drivers/
│   │   ├── peri_*/             # Peripheral drivers (gọi HAL)
│   │   └── algo_*/             # Algorithms (KHÔNG gọi HAL)
│   └── ...
└── README.md                   # File này
```

> Kiến trúc phân tầng: `Application → algo_* → peri_* → HAL`
> Chi tiết xem tại [PROJECT_RULES.md](../PROJECT_RULES.md#2-kiến-trúc-phân-tầng-firmware).

---

## 3. Cách build & flash

(?)

---

## 4. Cách test

> Quy ước test dùng `#ifdef TEST_<MODULE>` trong `main.c`.
> Chi tiết xem tại [PROJECT_RULES.md](../PROJECT_RULES.md#4-quy-ước-test-firmware).

---

## 5. Module README Template

> Mỗi folder `peri_*/` và `algo_*/` **phải có** `README.md` khi hoàn thành.
> Copy mẫu bên dưới vào folder module, lưu thành `README.md`, điền nội dung.

### Mẫu:

````markdown
# `<tên_module>` — *(mô tả 1 dòng)*

## Chức năng

*(Module này làm gì? Giải quyết vấn đề gì trong hệ thống?)*

## Files

| File | Mô tả |
|------|-------|
| `<tên>.c` | *(implementation chính)* |
| `<tên>.h` | *(public API + defines)* |

## API

```c
void    Module_Init(void);           // Khởi tạo — gọi 1 lần
void    Module_SetX(type param);     // Điều khiển
type    Module_GetY(void);           // Đọc giá trị
bool    Module_IsZ(void);            // Kiểm tra trạng thái
```

## Phần cứng *(bỏ nếu là algo)*

| Thuộc tính | Giá trị |
|-----------|---------|
| IC / Sensor | *(tên linh kiện)* |
| Interface | *(I2C / SPI / ADC / TIM PWM)* |
| Chân MCU | *(PA0, PB6...)* |
| Ghi chú | *(pull-up, tần số PWM, địa chỉ I2C...)* |

## Cách sửa / mở rộng

- **Đổi chân**: sửa `XXX_PIN` trong `.h`
- **Đổi thông số**: sửa `XXX_CONFIG` trong `Module_Init()`
- **Thêm tính năng**: *(gợi ý hướng mở rộng nếu có)*

## Lưu ý

- *(Gotchas, timing constraints, thứ tự init, lỗi hay gặp)*
- *(Những thứ mà nếu không đọc sẽ mất thời gian debug)*

## Test

1. Uncomment `#define TEST_<MODULE>` trong main.c
2. Build → Flash → Serial Monitor
3. Kết quả mong đợi: *(mô tả output đúng)*
````
