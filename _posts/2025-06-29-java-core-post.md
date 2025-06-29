---
layout: post
title: "Tổng hợp kiến thức Java Core"
date: 2025-06-29
---

Đây là bài viết mình tổng hợp kiến thức java core theo kiến thức bản thân! Có thể dùng để ôn tập phỏng vấn .....

Lưu ý: Vì là kiến thức bản thân tớ nên có thể sai sót mong mọi người góp ý !!!!

**I. Giới thiệu về Java**
  **1. Lịch sử và phiên bản Java**
       - Lịch sử ra đời: Java được phát triển năm 1991 bởi James Gosling và nhóm Green Team tại Sun Microsystems. Phát hành chính thức lần đầu vào năm 1995, và năm 1996 thì phiên bản Java 1.0 (Phiên bản đầu tiên) chính thức phát hành. Năm 2010, Oracle Corporation chính thức mua lại Sun Microsystems, bao gồm toàn bộ công nghệ và tài sản trí tuệ liên quan đến Java. Từ đó, Oracle trở thành đơn vị quản lý và phát triển Java Standard Edition (SE), Java Enterprise Edition (EE) và công cụ phát triền Java như JDK, JRE.
       - Mục tiêu ban đầu: Viết một lần, chạy mọi nơi (Write Once, Run Anywhere -WORA). Java nổi bật với sự an toàn, đơn giản, hướng đối tượng, hỗ trợ đa nền tảng (cross-flatform)
  **2. JVM (Java Virtual Machine), JDK (Java Development Kit), JRE (Java Runtime Environment) là gì ?**
       - JVM - Java Virtual Machine: Là một máy ảo, chịu trách nhiệm chạy mã byteCode (.class). JVM dịch mã bytecode thành mã máy phù hợp với hệ điều hành cụ thể (Windows/Linux...) chạy cùng với Garbage Collector và quản lý bộ nhớ.
       - JRE - Java Runtime Environment: Là môi trường chạy Java. Nó bao gồm JVM + các thư viện chuẩn(Java Class Libraries). Đề chạy ứng dụng Java, chỉ cần cài JRE.
       - JDK - Java Development Kit: Là bộ công cụ phát triển Java. Nó bao gồm JRE + các công cụ để viết và biên dịch code Java(javac,java,javadoc,jarsigner,...). Đề lập trình Java cần cài JDK.
       - Mình sẽ tóm tắt gọn bằng bảng dưới đây:
           |    Tìm hiểu  | Thành phần         | Dùng để                             |
           |------------- |--------------------|-------------------------------------|
           | JVM          | Máy ảo Java        | Thực thi bytecode                   |
           | JRE          | JVM + thư viện     | Chạy chương trình Java              |
           | JDK          | JRE + công cụ dev  | Viết, biên dịch, chạy chương trình  |
  **3. Cách Java hoạt động (Compile -> Run)**  
       *3.1. Quy trình chạy một chương trình Java*  
         a. Viết mã Java bằng notepad và lưu file với đuôi .java (ví dụ Hello.java)  
         b. Biên dịch(compile):  
              + Dùng terminal sử dụng lệnh: javac Hello.java -> để dịch file java thành file bytecode Hello.class  
         c. Chạy chương trình: sử dụng lệnh java Hello (JVM sẽ chạy file Hello.class)  
       *3.2. Tóm tắt luồng chính:* Code Java(.java) -----[javac -compiler]--> Bytecode(.class) -----[java - JVM]-> Chạy chương trình trên OS cụ thể  
       *3.3. Tính năng nổi bật của Java runtime*  
            + Portable: bytecode chạy trên mọi hệ điều hành.  
            + Secure: sandbox, kiểm soát bộ nhớ chặt chẽ  
            + Automatic Memory Management: thông qua Garbage Collector  
