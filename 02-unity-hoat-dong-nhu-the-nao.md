# 2. Unity hoạt động như thế nào

[⬅ Quay lại](01-cai-dat-moi-truong.md) | [Tiếp theo ➡](03-giao-dien-unity.md)

## Khái niệm chính

Unity hoạt động theo mô hình Component, trong đó mỗi đối tượng trong scene được xây dựng từ nhiều thành phần khác nhau.

## Ví dụ minh họa

```text
Scene
├── Player
│   ├── Transform
│   ├── Animator
│   ├── CharacterController
│   └── PlayerController.cs
├── Enemy
│   ├── Transform
│   ├── Animator
│   ├── NavMeshAgent
│   └── EnemyController.cs
```

## Ghi nhớ

- GameObject không làm gì cả một cách tự động.
- Mọi chức năng đều được thêm bằng Component.

---
