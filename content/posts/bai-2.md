---
title: "Xây dựng Server Echo với TCP Socket"
date: 2025-12-28
draft: false
tags: ["Socket", "TCP"]
summary: "Hướng dẫn xây dựng Server Echo đơn giản để hiểu cách trao đổi dữ liệu qua giao thức TCP Socket trong Java."
---

Server Echo là bài tập cơ bản để hiểu cách Client và Server trao đổi dữ liệu qua giao thức TCP. Đây là nền tảng cho các hệ thống Chat và truyền tải dữ liệu sau này.

---

## 1. Cơ chế hoạt động
Server lắng nghe tại một cổng, nhận chuỗi từ Client và gửi trả ngược lại chính xác chuỗi đó.



## 2. Mã nguồn Server mẫu
```java
ServerSocket server = new ServerSocket(7);
Socket socket = server.accept();
DataInputStream in = new DataInputStream(socket.getInputStream());
String msg = in.readUTF();
DataOutputStream out = new DataOutputStream(socket.getOutputStream());
out.writeUTF(msg);