---
title: "Xử lý đa luồng cho Server Socket"
date: 2025-12-28
draft: false
tags: ["MULTITHREAD", "Java", "Socket"]
summary: "Kỹ thuật tối ưu giúp Server xử lý đồng thời nhiều kết nối Client, giải quyết bài toán nghẽn cổ chai trong lập trình mạng."
---

Trong môi trường thực tế, một máy chủ không bao giờ chỉ phục vụ một người dùng duy nhất. Thách thức lớn nhất đối với lập trình viên mạng là làm thế nào để Server có thể phản hồi hàng nghìn yêu cầu cùng lúc mà không làm gián đoạn lẫn nhau.

---

## 1. Mô hình xử lý Đa luồng (Multi-threading)

Mô hình xử lý truyền thống (Sequential) chỉ cho phép một kết nối tại một thời điểm. Với kỹ thuật Multi-threading, mỗi khi một Client kết nối thành công, Server sẽ tạo ra một luồng (Thread) riêng biệt để phục vụ Client đó.

**Quy trình vận hành:**
1. **Main Thread:** Liên tục lắng nghe tại cổng (ServerSocket).
2. **Accept:** Khi có kết nối, gọi phương thức `.accept()`.
3. **Spawn Thread:** Khởi tạo một đối tượng thực thi luồng mới và bàn giao Socket của Client đó cho luồng con.
4. **Independent Work:** Luồng con xử lý dữ liệu độc lập trong khi Luồng chính quay lại lắng nghe Client tiếp theo.

---

## 2. Mã nguồn thực thi tại Server

Dưới đây là cấu trúc mã nguồn tiêu biểu cho một Server đa luồng trong Java:

```java
import java.net.*;
import java.io.*;

public class MultiThreadedServer {
    public static void main(String[] args) throws IOException {
        ServerSocket serverSocket = new ServerSocket(1234);
        System.out.println("Server is running on port 1234...");

        while (true) {
            Socket clientSocket = serverSocket.accept();
            System.out.println("New client connected!");
            
            // Khởi tạo luồng mới cho mỗi Client
            new ClientHandler(clientSocket).start();
        }
    }
}

class ClientHandler extends Thread {
    private Socket socket;
    public ClientHandler(Socket socket) { this.socket = socket; }

    public void run() {
        try {
            // Logic xử lý dữ liệu riêng biệt cho mỗi Client ở đây
            DataInputStream in = new DataInputStream(socket.getInputStream());
            String message = in.readUTF();
            System.out.println("Message from client: " + message);
            socket.close();
        } catch (IOException e) { e.printStackTrace(); }
    }
}