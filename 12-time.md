# 12. Time

## Khái niệm

Time trong Unity giúp bạn làm việc với thời gian và khung hình một cách chính xác.

## Các thuộc tính thường dùng

```c#
Time.deltaTime
Time.time
Time.fixedDeltaTime
```

## Quy tắc quan trọng

Luôn nhân movement với deltaTime để chuyển động mượt mà trên các máy cấu hình khác nhau.

### Sai

```c#
transform.Translate(Vector3.forward);
```

### Đúng

```c#
transform.Translate(Vector3.forward * speed * Time.deltaTime);
```

---
