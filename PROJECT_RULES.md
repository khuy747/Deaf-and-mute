# 📏 PROJECT_RULES — Quy tắc dự án

> Tất cả quy ước của dự án nằm ở đây. Đây là **single source of truth**.
> Các file README khác chỉ mô tả cấu trúc thư mục và trỏ link về file này.

---

## 1. Quy ước đặt file

- **CẤM** tạo file `.c`, `.h`, `.py` trực tiếp tại root.


- Thư viện bên thứ 3: Đặt vào `firmware/<project>/Drivers/` hoặc tạo `ThirdParty/`.
---
### File được phép tại root:

- `README.md`             
- `.gitignore`          
- `LICENSE`               
- `PROJECT_RULES.md`      

---

## 2. Kiến trúc phân tầng firmware

```
┌──────────────────────────────────────┐
│     Application  (Core/Src/main.c)   │  ← Gọi driver + algorithm
├──────────────────────────────────────┤
│     algo_*/                          │  ← Tầng logic
│     (không gọi HAL trực tiếp)        │
├──────────────────────────────────────┤
│     peri_*/                          │  ← Gói HAL thành API cấp module
│     (gọi HAL_* bên trong)            │
├──────────────────────────────────────┤
│     HAL / CMSIS  (IDE-managed)       │  ← KHÔNG sửa
└──────────────────────────────────────┘
```

### Quy tắc phụ thuộc:
- Application (`Core/`) gọi `peri_*/` và `algo_*/` — **hạn chế** gọi `HAL_*` trực tiếp.
- `algo_*/` **KHÔNG** include header HAL — nhận data qua parameters.
- `peri_*/` là tầng duy nhất gọi hàm `HAL_*` trực tiếp.

### Quy ước đặt tên thư mục:

| Thư mục              | Đặt tên folder              | Ví dụ                       |
| -------------------- | --------------------------- | --------------------------- |
| Peripheral driver    | `peri_<TÊN_MODULE>/`        | `peri_motor/`, `peri_ir/`   |
| Algorithm            | `algo_*/`                   | `algo_pid/`, `algo_floodfill/`|
| Application          | `core/src/` + `core/inc/`   | *(IDE-managed)*             |

### Quy ước đặt tên file:

**Tất cả file đều dùng `snake_case` (viết thường, dấu cách = `_`).**

| Loại | Quy tắc | Ví dụ ✅ | Sai ❌ |
|------|---------|---------|--------|
| Source file | `<chức_năng_module>.c` | `drive_motor.c` | `Drive.c`, `motor.c` |
| Header file | `<chức_năng_module>.h` | `drive_motor.h` | `DriveMotor.h` |
| Python script | `<chức_năng_tool>.py` | `flash_tool.py` | `FlashTool.py` |
| Tài liệu | `<tên_nội_dung>.md` | `task_tracking.md` | `TaskTracking.md` |

### Quy ước đặt tên trong code C:

| Thành phần | Quy tắc | Ví dụ |
|-----------|---------|-------|
| **Hàm** | `Module_Action()` — PascalCase với prefix module | `Motor_Init()`, `Motor_SetSpeed()`, `PID_Compute()` |
| **Biến local** | `snake_case` | `int32_t encoder_count;` |
| **Biến global** | `g_snake_case` (prefix `g_`) | `volatile uint32_t g_tick_count;` |
| **Hằng số / macro** | `UPPER_SNAKE_CASE` | `#define MAX_SPEED 100`, `#define IR_LEFT 0` |
| **Typedef struct** | `PascalCase_t` | `typedef struct { ... } PID_t;` |
| **Enum** | `UPPER_SNAKE_CASE` | `enum { MOTOR_LEFT, MOTOR_RIGHT };` |
| **Tham số hàm** | `snake_case` | `void Motor_SetSpeed(MotorID id, int8_t percent)` |

### Quy ước Action cho hàm:

Dùng **Action chuẩn** để ai đọc code cũng đoán được hàm làm gì:

| Action | Khi nào dùng | Ví dụ |
|--------|-------------|-------|
| `_Init()` | Khởi tạo module (gọi 1 lần khi bắt đầu) | `Motor_Init()`, `IR_Init()` |
| `_DeInit()` | Giải phóng / tắt module | `Motor_DeInit()` |
| `_Start()` / `_Stop()` | Bật / tắt hoạt động liên tục | `Motor_Start()`, `Motor_Stop()` |
| `_Get<X>()` | Đọc giá trị (không tác dụng phụ) | `Encoder_GetCount()` |
| `_Set<X>()` | Ghi / thay đổi giá trị | `Motor_SetSpeed()` |
| `_Read()` / `_Write()` | Đọc/ghi I/O phần cứng (có tác dụng phụ) | `IR_ReadRaw()`, `UART_Write()` |
| `_Is<X>()` | Kiểm tra trạng thái → trả về `bool` | `IR_IsWallDetected()` |
| `_Reset()` | Đưa về trạng thái ban đầu | `PID_Reset()`, `Encoder_Reset()` |
| `_Compute()` / `_Process()` | Tính toán / xử lý 1 chu kỳ | `PID_Compute()` |
| `_IRQHandler()` | Xử lý ngắt (ISR) — chỉ HAL callback | `Motor_IRQHandler()` |

## 3. Quy ước docs

### Docs cho thư mục lớn

Mỗi thư mục lớn (`firmware/`, `hardware/`, `software/`) có sẵn `README.md` mô tả:
- Nội dung và cấu trúc thư mục
- Công cụ / toolchain sử dụng
- Cách setup, build, hoặc sử dụng

> Khi bắt đầu làm phần nào → điền `README.md` tương ứng.

### Docs cho module firmware

Mỗi folder `peri_*/` và `algo_*/` **phải có** `README.md` khi module hoàn thành.

#### Nội dung bắt buộc:
- **Chức năng** — module làm gì
- **API** — danh sách hàm public
- **Phần cứng** — IC, interface, chân MCU *(bỏ nếu là algo)*
- **Cách sửa** — đổi chân, đổi config ở đâu
- **Lưu ý** — gotchas, timing, lỗi hay gặp

#### Template:
Xem mẫu ở cuối [firmware/README.md](firmware/README.md#module-readme-template) — copy vào folder module, đổi tên thành `README.md`, điền nội dung.

#### Quy trình:
```
Viết code → Test pass → Viết README.md → Commit cùng code
```

> Module chưa có README.md = chưa xong.



## 4. Quy ước test firmware

### Cách làm: dùng `#ifdef TEST_<MODULE>`

Trong `main.c`, thêm block test cho mỗi module. Đổi dòng `#define` để chọn module test:

```c
// ===== TEST MODE — Uncomment 1 dòng để test =====
// #define TEST_MOTOR
// #define TEST_IR
// #define TEST_IMU

int main(void) {
    HAL_Init();
    SystemClock_Config();
    // ... init ...

#ifdef TEST_MOTOR
    Motor_Init();
    printf("=== TEST MOTOR ===\r\n");
    while(1) {
        Motor_SetSpeed(50);
        HAL_Delay(2000);
        Motor_Stop();
        printf("Enc: %ld\r\n", Encoder_GetCount());
        HAL_Delay(1000);
    }
#endif

    // Chế độ chạy chính (khi không define TEST nào)
    while(1) { /* state machine */ }
}
```

### Quy trình test module mới:

```
1. Viết driver (Drivers/peri_XXX/)
2. Thêm include path trong IDE
3. Thêm block #ifdef TEST_XXX vào main.c
4. Uncomment #define TEST_XXX
5. Build → Flash → Serial Monitor
6. PASS → comment lại #define
   FAIL → sửa driver → lặp lại
```

### Lưu ý:
- **Giữ code test trong main.c** — không xoá, sau này cần test lại
---

## 5. Quy ước Commit Message

```
[PREFIX] mô tả ngắn gọn bằng tiếng Việt hoặc tiếng Anh
```

### Bảng prefix:

| Prefix    | Dùng khi                                      | Ví dụ                                        |
| --------- | --------------------------------------------- | --------------------------------------------- |
| `[FW]`    | Thay đổi firmware (driver, algorithm, app)    | `[FW] thêm driver MPU6050`                   |
| `[HW]`    | Thay đổi file phần cứng (schematic, PCB, BOM) | `[HW] hoàn thiện schematic v1.0`             |
| `[MECH]`  | Thay đổi file cơ khí (CAD, STL)               | `[MECH] update chassis v2`                   |
| `[SW]`    | Thay đổi software host (GUI, script)           | `[SW] thêm serial monitor`                   |
| `[TOOL]`  | Thay đổi tools / scripts                       | `[TOOL] thêm script flash tự động`           |
| `[DOC]`   | Thay đổi tài liệu (docs, README, specs)       | `[DOC] cập nhật pinout`                      |
| `[CFG]`   | Thay đổi config (.gitignore, rules, CI)        | `[CFG] thêm rule ignore Keil`                |
| `[FIX]`   | Sửa bug                                        | `[FIX] sửa PID reset khi đổi hướng`         |
| `[REFAC]` | Refactor / dọn code                            | `[REFAC] tách hàm init ra file riêng`        |
|`[STRUC]`| Chỉnh sửa cấu trúc của project                          | `[STRUC] update README.md`       |

### Quy tắc bổ sung:

- Có thể ghi thêm phase: `[FW] P3.2 — thêm driver encoder`


---

*Mọi thay đổi quy tắc cần được chủ dự án phê duyệt trước khi commit.*
