# 🔌 Hardware

> Mô tả thiết kế phần cứng của dự án.

## Cấu trúc

```
hardware/
├── schematics/             # Schematic files
├── pcb/                    # PCB layout files
├── bom/                    # Bill of Materials
└── README.md               # File này
```

## Thông tin

| Thuộc tính | Giá trị |
|-----------|---------|
| EDA tool | (?) *(KiCad / Altium / EasyEDA / ...)* |
| Board version | (?) |
| Số lớp PCB | (?) |

## Phiên bản board

| Version | Ngày | Trạng thái | Ghi chú |
|---------|------|-----------|---------|
| v1.0 | (?) | (?) | |

## Test Checklist

> Dùng khi nhận board mới hoặc sau khi hàn/sửa phần cứng.
> Đánh dấu `[x]` khi test pass, `[!]` khi có vấn đề.

### 1. Kiểm tra nguồn (TRƯỚC KHI CẮM MCU)

- [ ] Kiểm tra ngắn mạch VCC-GND (phải hở mạch)
- [ ] Cấp nguồn, đo VCC tại chân MCU = *(ghi giá trị)* V
- [ ] Đo dòng tiêu thụ không tải = *(ghi giá trị)* mA

### 2. Kiểm tra MCU

- [ ] Programmer nhận MCU
- [ ] Flash chương trình blink LED thành công

### 3. Kiểm tra ngoại vi

- [ ] *(Thêm từng ngoại vi khi thiết kế xong)*

---

| Ngày test  | Board version | Kết quả     | Ghi chú            |
| ---------- | ------------- | ----------- | -------------------|
| *(ngày)*   | v1.0          | *(pass/fail)* | *(vấn đề nếu có)* |

