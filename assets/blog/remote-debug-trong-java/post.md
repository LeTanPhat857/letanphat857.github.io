---
title: Remote debug trong Java
slug: remote-debug-trong-java
date: 2023-09-02
author: Phat
tags:
  - debugging
  - java
image-path: assets/blog/remote-debug-trong-java
---

## Remote debug là gì?

Remote debug là cách để debug một ứng dụng chạy ở một chương trình khác hoặc một máy khác.

## Tại sao cần remote debug?

Một số trường hợp cần dùng remote debug là:

- Không thể tái hiện bug ở môi trường dev, chúng ta có thể dùng remote debug trực tiếp trên môi trường test hoặc production.
- Các web app chạy trên web server app. Trường hợp này là hai chương trình khác nhau cho nên khi debug cần dùng remote debug để kết nối.

## JDWP: The Java Debug Wire Protocol

The Java Debug Wire Protocol là giao thức của Java dùng trong giao tiếp giữa một ứng dụng được debug (debuggee) và một ứng dụng dùng để debug (debugger).

Debuggee và debugger có thể chạy trên cùng một máy hoặc trên các máy khác nhau.

**JDWP cung cấp một số option:**

- *transport*: bắt buộc. Dùng để xác định cách giao tiếp (transport mechanism).
    - dt_shmem: chỉ hoạt động với Window OS, hai chương trình chung một máy
    - dt_socket: tương thích với mọi hệ điều hành, cho phép các chương trình chạy trên các máy khác nhau
- *server*: không bắt buộc. Dùng để xác cách kết nối với debugger. Cho phép xuất ra một cổng kết nối thông qua *address.* Giá trị là **y** hoặc **n**. Nếu là y thì cần xác định thêm *address*, nếu là n thì JDWP sẽ dùng giá trị mặc định.
- *address*: dùng để chứa address, thường là một port, được cung cấp bởi debuggee.
- *suspend*: dùng để xác định xem JVM có dừng và chờ debugger kết nối (attach) tới hay không.

**Java 8-**

> java -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=8000 OurApplication

**Java 9+**

> java -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=127.0.0.1:8000 OurApplication

**Note:** Theo cách cũ, address=8000 tương đương address=*:8000. Cách này không bảo mật. Khuyến nghị dùng theo cách mới là xác định rõ địa chỉ IP, address=127.0.0.1:8000

## Cách remote debug một Web app với Tomcat và IntelliJ

Tomcat hỗ trợ remote debug cho các web app chạy trên nó. Như vậy, các web app chạy trên Tomcat là debuggees, IntilliJ xem như là một debugger. Để debug, các bạn làm theo các bước sau:

**Bước 1: Chạy Tomcat với chế độ debug**

> Vào thư mục tomcat > bin > mở catalina.bat
> Tìm và chỉnh sửa các option mặc định theo mong muốn.
>
> ![This is an image](assets/blog/remote-debug-trong-java/Untitled.png)
>
> Mở cmd tại thư mục bin, gõ: **catalina.bat jpda run**
>
> ![This is an image](assets/blog/remote-debug-trong-java/Untitled%201.png)
>
> Vì mình bật option suspend nên Tomcat sẽ chờ debugger kết nối tới

**Bước 2: Chạy config debug trên IntilliJ**

> Cấu hình debugger cho phù hợp (transport, host, port) với debuggee
>
> ![This is an image](assets/blog/remote-debug-trong-java/Untitled%202.png)
>
> Lưu config và chạy
>
> Quay lại màn hình debuggee sẽ thấy được kết nối với debugger
>
> ![This is an image](assets/blog/remote-debug-trong-java/Untitled%203.png)

**Bước 3: Đặt breakpoint và debug thôi**

## Tham khảo

[https://www.baeldung.com/java-application-remote-debugging](https://www.baeldung.com/java-application-remote-debugging)

[https://viblo.asia/p/java-remote-debugging-debug-ung-dung-java-chay-tren-may-tinh-khac-vlZL9NQDVQK](https://viblo.asia/p/java-remote-debugging-debug-ung-dung-java-chay-tren-may-tinh-khac-vlZL9NQDVQK)

Hết.
