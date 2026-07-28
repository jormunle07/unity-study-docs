# 18. Event

[⬅ Quay lại](17-scriptableobject.md) | [Tiếp theo ➡](19-singleton.md)

## Khái niệm

Event dùng để thông báo một thay đổi cho các hệ thống khác mà không cần gọi trực tiếp lẫn nhau.

## Ví dụ

```text
Player chết
↓
UI cập nhật
↓
Audio phát
↓
Quest cập nhật
↓
Achievement cập nhật
```

## Ghi nhớ

- Không nên gọi trực tiếp giữa các hệ thống khi có thể dùng event.

---
