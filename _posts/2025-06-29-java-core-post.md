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
       
           |-------------------------------------------------------------------------|
           |    Tìm hiểu  | Thành phần         | Dùng để                             |  
           |------------- |--------------------|-------------------------------------|  
           | JVM          | Máy ảo Java        | Thực thi bytecode                   |  
           | JRE          | JVM + thư viện     | Chạy chương trình Java              |  
           | JDK          | JRE + công cụ dev  | Viết, biên dịch, chạy chương trình  |  
           |-------------------------------------------------------------------------|
        
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
            
**II. Biến, Kiểu dữ liệu, Toán tử (Variables, Data Types, Operators)**  
    **1. Kiểu dữ liệu nguyên thủy (Primitive Data Types)**  
        - Java có **8 kiểu dữ liệu nguyên thủy**, dùng để lưu trữ các giá trị đơn giản và hiệu quả về bộ nhớ (lưu ở Stack memory)  
        
            |--------------------------------------------------------------------------------------------------------------------|
            |          Kiểu        | Kích Thước |            Miêu tả            |                Giá trị mặc định                |
            |----------------------|------------|-------------------------------|------------------------------------------------|  
            |            | byte    | 1 byte     | Số nguyên nhỏ (-128 đến 127)  | 0                                              |  
            |Số Nguyên   | short   | 2 byte     | Số nguyên ngắn                | 0                                              |    
            |            | int     | 4 byte     | Số nguyên thường dùng nhất    | 0                                              |  
            |            | long    | 8 byte     | Số nguyên lớn                 | 0L                                             |  
            |--------------------------------------------------------------------------------------------------------------------|   
            |Số Thực/    | float   | 4 byte     | Số thực chính xác đơn         | 0.0f                                           |          
            |Số thập phân| double  | 8 byte     | Số thực chính xác kép         | 0.0d                                           |   
            |--------------------------------------------------------------------------------------------------------------------|  
            |Kí tự       | char    | 2 byte     | Ký tự unicode                 | '\u0000' đại diện cho ký tự có mã Unicode là 0,|   
            |            |         |            |                               |  hay còn gọi là null character(ký tự null      |   
            |--------------------------------------------------------------------------------------------------------------------|   
            |    boolean           | 1 bit      | Chỉ nhận 2 giá trị True/False | false                                          |  
            |--------------------------------------------------------------------------------------------------------------------|  
   **2. Kiểu dữ liệu tham chiểu (Referecen Date Types)**  
        - Là kiểu dữ liệu không lưu trữ giá trị trực tiếp, mà trỏ tới vùng nhớ nơi chứa đối tượng (lưu ở Heap memory)  
        - Ví dụ kiểu dữ liệu tham chiếu bao gồm: String, Array, Class, Interface, Enum, Object, List...  
    **Lưu ý: So sánh 2 kiểu dữ liệu nguyên thủy và kiểu dữ liệu tham chiếu.**  
        + Kiểu dữ liệu nguyên thủy ít tốn bộ nhớ hơn, tốc độ xử lý dữ liệu nhanh hơn. Vì kiểu giữ liệu nguyên thủy lưu trữ giá trị trực tiếp. Còn dữ liệu tham chiếu lưu trử trong Heap Memory, mỗi lấy lấy giá trị nó phải lấy địa chỉ lưu trong Stack Memory rồi từ địa chỉ đó trỏ tới giá trị nằm trong Heap Memory.  
        + Kiểu dữ liệu nguyên thủy không chấp giá trị null. Kiểu dữ liệu tham chiếu chấp giá trị null.  
        + Để so sánh giá trị nguyên thủy dùng toán tử == . Trong khi kiểu dữ liệu tham chiếu không thể dùng toán tử == vì lúc đó nó sẽ so sánh địa chỉ của chúng, kiểu dữ liệu tham chiếu được hỗ trợ bởi các phương thức có sẵn vì vậy để so sánh giá trị chúng ta dùng phương thức .equals() để so sánh giá trị.  
   **3. Biến (Variables) - Local, Instance, Static**  
      - Java có 3 loại biến chính:  
         a. Local Variable (biến cục bộ)  
             + Khai báo trong phương thức hoặc khối mã  
             + Không có giá trị mặc định -> bắt buộc gán giá trị trước khi dùng  

                void show(){  
                        int x = 10; // local  
                        System.out.pribtln(x);  
                }  

        b. Instance variable (biến đối tượng)  
            + Khai báo trong class nhưng ngoài phương thức  
            + Mỗi đối tượng có một bản sao riêng  

                   public class Student {  
                      String name; // instance  
                   }  

       c. Static variable (biến tĩnh)  
            + Biến tĩnh là biến được khaai báo với từ khóa static trong một class  
            + Nó thuộc về lớp(class) chứ không thuộc về bất kỳ đối tượng nào  
            + Tất cả các đối tượng của class đó **dùng chung một biến tĩnh.**  

            public class Student {   
                static String school = "ABC School" // static  
            }   

            + **Biến tĩnh được dùng như nào ?**  
            Dùng để đếm số lượng đối tượng được tạo, ví dụ: Dùng static int counter để đếm  
            Chia sẻ cấu hình chung, ví dụ: tên công ty, tỷ lệ thuế...  
            Hằng số toàn cục(kết hợp với final), ví dụ public static final double PI = 3.14.  
     - Ngoài ra còn có loại biến như: Final variable (Biến hằng số), Transient variable(Biến tạm thời), Volatile variable.  
  **4. Toán tử (Operators)**  


 
