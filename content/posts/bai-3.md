---
title: "Lập trình tính toán số học qua mạng"
date: 2025-12-28
draft: false
tags: ["Java", "Math"]
summary: ""
---

Bài viết này hướng dẫn cách gửi các con số và nhận kết quả tính toán từ Server.

---

## 1. Logic xử lý
Client gửi hai số `a`, `b` và toán tử. Server thực hiện phép tính và trả về giá trị.

## 2. Mã nguồn xử lý tại Server
```java
int a = in.readInt();
int b = in.readInt();
int tong = a + b;
out.writeInt(tong);