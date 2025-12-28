---
title: "Lập trình kết nối Cơ sở dữ liệu Java"
date: 2025-12-28
draft: false
tags: ["Java", "Database", "JDBC"]
summary: "Hướng dẫn chi tiết cách thiết lập kết nối JDBC để quản lý và truy xuất dữ liệu trong ứng dụng Java."
---

Trong lập trình ứng dụng, việc kết nối CSDL là bước quan trọng nhất để lưu trữ dữ liệu. Java cung cấp JDBC để làm việc với MySQL và SQL Server.

---

## 1. Tổng quan về kết nối JDBC
Để kết nối thành công, chúng ta cần nạp Driver tương ứng và thiết lập chuỗi Connection URL phù hợp với hệ quản trị CSDL.



## 2. Mã nguồn mẫu kết nối MySQL
```java
import java.sql.Connection;
import java.sql.DriverManager;

public class DBConnect {
    public static void main(String[] args) {
        try {
            // Nạp Driver
            Class.forName("com.mysql.cj.jdbc.Driver");
            String url = "jdbc:mysql://localhost:3306/ql_sinhvien";
            Connection conn = DriverManager.getConnection(url, "root", "");
            System.out.println("Kết nối CSDL thành công!");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}