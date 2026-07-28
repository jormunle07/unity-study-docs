# 9. MonoBehaviour Lifecycle

## Thứ tự gọi hàm

Unity sẽ gọi các hàm theo trình tự sau:

```text
Awake
↓
OnEnable
↓
Start
↓
Update
↓
LateUpdate
↓
FixedUpdate
↓
OnDisable
↓
OnDestroy
```

## Ý nghĩa từng hàm

- Awake: Khởi tạo ban đầu.
- Start: Chạy sau Awake, thường dùng để khởi tạo dữ liệu.
- Update: Chạy mỗi frame.
- FixedUpdate: Thường dùng cho physics.
- LateUpdate: Thường dùng cho camera hoặc các thao tác sau update.

---
