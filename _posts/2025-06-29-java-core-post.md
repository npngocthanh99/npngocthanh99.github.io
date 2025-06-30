---
layout: post
title: "Tổng hợp kiến thức Java Core"
date: 2025-06-29
---

Đây là bài viết mình tổng hợp kiến thức java core theo kiến thức bản thân! Có thể dùng để ôn tập phỏng vấn ...

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
         | Tìm hiểu     | Thành phần         | Dùng để                             |
         |------------- |--------------------|-------------------------------------|
         | JVM          | Máy ảo Java        | Thực thi bytecode                   |
         | JRE          | JVM + thư viện     | Chạy chương trình Java              |
         | JDK          | JRE + công cụ dev  | Viết, biên dịch, chạy chương trình  |
         |-------------------------------------------------------------------------|

**3. Cách Java hoạt động (Compile -> Run)**  
 _3.1. Quy trình chạy một chương trình Java_  
a. Viết mã Java bằng notepad và lưu file với đuôi .java (ví dụ Hello.java)  
 b. Biên dịch(compile): Dùng terminal sử dụng lệnh: javac Hello.java -> để dịch file java thành file bytecode Hello.class  
 c. Chạy chương trình: sử dụng lệnh java Hello (JVM sẽ chạy file Hello.class)  
_3.2. Tóm tắt luồng chính:_ Code Java(.java) -----[javac -compiler]--> Bytecode(.class) -----[java - JVM]-> Chạy chương trình trên OS cụ thể  
_3.3. Tính năng nổi bật của Java runtime:_

- Portable: bytecode chạy trên mọi hệ điều hành.
- Secure: sandbox, kiểm soát bộ nhớ chặt chẽ
- Automatic Memory Management: thông qua Garbage Collector

**II. Biến, Kiểu dữ liệu, Toán tử (Variables, Data Types, Operators)**  
**1. Kiểu dữ liệu nguyên thủy (Primitive Data Types)**

- Java có **8 kiểu dữ liệu nguyên thủy**, dùng để lưu trữ các giá trị đơn giản và hiệu quả về bộ nhớ (lưu ở Stack memory)

         |----------------------------------------------------------------------------------------------------------------------|
         |           Kiểu         | Kích Thước |        Miêu tả                |                Giá trị mặc định                |
         |------------------------|------------|-------------------------------|------------------------------------------------|
         |            | byte      | 1 byte     | Số nguyên nhỏ (-128 đến 127)  |                  0                             |
         |Số Nguyên   | short     | 2 byte     | Số nguyên ngắn                |                  0                             |
         |            | int       | 4 byte     | Số nguyên thường dùng nhất    |                  0                             |
         |            | long      | 8 byte     | Số nguyên lớn                 |                  0L                            |
         |----------------------------------------------------------------------------------------------------------------------|
         |Số Thực/    | float     | 4 byte     | Số thực chính xác đơn         |                  0.0f                          |
         |Số thập phân| double    | 8 byte     | Số thực chính xác kép         |                  0.0d                          |
         |----------------------------------------------------------------------------------------------------------------------|
         |Kí tự       | char      | 2 byte     | Ký tự unicode                 | '\u0000' đại diện cho ký tự có mã Unicode là 0,|
         |            |           |            |                               | hay còn gọi là null character(ký tự null)      |
         |----------------------------------------------------------------------------------------------------------------------|
         | boolean                | 1 bit      | Chỉ nhận 2 giá trị True/False |                  false                         |
         |----------------------------------------------------------------------------------------------------------------------|

**2. Kiểu dữ liệu tham chiểu (Referecen Date Types)**

- Là kiểu dữ liệu không lưu trữ giá trị trực tiếp, mà trỏ tới vùng nhớ nơi chứa đối tượng (lưu ở Heap memory)
- Ví dụ kiểu dữ liệu tham chiếu bao gồm: String, Array, Class, Interface, Enum, Object, List...

**So sánh 2 kiểu dữ liệu nguyên thủy và kiểu dữ liệu tham chiếu.**

- Kiểu dữ liệu nguyên thủy ít tốn bộ nhớ hơn, tốc độ xử lý dữ liệu nhanh hơn. Vì kiểu giữ liệu nguyên thủy lưu trữ giá trị trực tiếp. Còn dữ liệu tham chiếu lưu trử trong Heap Memory, mỗi lấy lấy giá trị nó phải lấy địa chỉ lưu trong Stack Memory rồi từ địa chỉ đó trỏ tới giá trị nằm trong Heap Memory.
- Kiểu dữ liệu nguyên thủy không chấp giá trị null. Kiểu dữ liệu tham chiếu chấp giá trị null.
- Để so sánh giá trị nguyên thủy dùng toán tử == . Trong khi kiểu dữ liệu tham chiếu không thể dùng toán tử == vì lúc đó nó sẽ so sánh địa chỉ của chúng, kiểu dữ liệu tham chiếu được hỗ trợ bởi các phương thức có sẵn vì vậy để so sánh giá trị chúng ta dùng phương thức .equals() để so sánh giá trị.

**3. Biến (Variables) - Local, Instance, Static**

- Java có 3 loại biến chính:

a. Local Variable (biến cục bộ)

- Khai báo trong phương thức hoặc khối mã
- Không có giá trị mặc định -> bắt buộc gán giá trị trước khi dùng

{% raw %}

         void show() {
             int x = 10; // local
             System.out.println(x);
          }

{% endraw %}

b. Instance variable (biến đối tượng)

- Khai báo trong class nhưng ngoài phương thức
- Mỗi đối tượng có một bản sao riêng

{% raw %}

          public class Student {
             String name; // instance
          }

{% endraw %}

c. Static variable (biến tĩnh)

- Biến tĩnh là biến được khaai báo với từ khóa static trong một class
- Nó thuộc về lớp(class) chứ không thuộc về bất kỳ đối tượng nào
- Tất cả các đối tượng của class đó **dùng chung một biến tĩnh.**

{% raw %}

         public class Student {
           static String school = "ABC School" // static
         }

{% endraw %}

**Biến tĩnh được dùng như nào ?**

- Dùng để đếm số lượng đối tượng được tạo, ví dụ: Dùng static int counter để đếm
- Chia sẻ cấu hình chung, ví dụ: tên công ty, tỷ lệ thuế...
- Hằng số toàn cục(kết hợp với final), ví dụ public static final double PI = 3.14.

- Ngoài ra còn có loại biến như: Final variable (Biến hằng số), Transient variable(Biến tạm thời), Volatile variable.

**4. Toán tử (Operators)**

- Java hỗ trợ nhiều loại toán tử cho các phép tính toán và logic:

**a. Toán tử số học(Arithmetic Operators)**

         |--------------------------------------------------------------|
         | Toán tử |      Chức năng                | Ví dụ              |
         |--------------------------------------------------------------|
         |    +    |     Cộng                      | a + b              |
         |    -    |     Trừ                       | a - b              |
         |    *    |     Nhân                      | a * b              |
         |    /    |     Chia                      | a / b              |
         |    %    |     Chia lấy phần dư          | a % b              |
         |    ++   |     Tăng 1 (prefix/postfix)   | ++a hoặc a++       |
         |    --   |     Giảm 1 (prefix/postfix)   | --a hoặc a--       |
         |--------------------------------------------------------------|

**b. Toán tử So sánh (Relational Operators)**

         |--------------------------------------------------|
         |  Toán tử  |           Ý nghĩa                    |
         |--------------------------------------------------|
         |   ==      | Bằng                                 |
         |   !=      | Không bằng                           |
         |   >       | Lớn hơn                              |
         |   <       | Nhỏ hơn                              |
         |   >=      | Lớn hơn hoặc bằng                    |
         |   <=      | Nhỏ hơn hoặc bằng                    |
         |--------------------------------------------------|
         - Trả về giá trị **boolean (true/false)

**c. Toán tử Gán (Assignment Operators)**

         |--------------------------------------------------|
         | Toán tử  | Ví dụ     | Ý nghĩa                   |
         |--------------------------------------------------|
         | =        | a = b    | Gán giá trị của b cho a    |
         | +=       | a += 1   | a = a + 1                  |
         | -=       | a -= 1   | a = a - 1                  |
         | *=       | a *= 1   | a = a * 1                  |
         | /=       | a /= 1   | a = /= 1                   |
         | %=       | a %=5    | a = a % 5                  |
         |--------------------------------------------------|

**d. Toán tử Logic (Logical Operators)**

         |---------------------------------------------------------------------------------------------------------------|
         | Toán tử | Tên gọi       | Ý nghĩa                                            | Ví dụ         | Kết quả ví dụ  |
         |---------------------------------------------------------------------------------------------------------------|
         |    &&   | Logical AND   | Đúng nếu cả hai biểu thức trước đều đúng           | true && false | false          |
         |    ||   | Logical OR    | Đúng nếu ít nhất một biểu thức đúng                | true || false | true           |
         |    !    | Logical NOT   | Phủ định giá trị boolean(trả về giá trị ngược lại) | !true         | false          |
         |---------------------------------------------------------------------------------------------------------------|

**e. Toán tử Bit (Bitwise Operators)**

- Bitwise Operators - Thao tác trên bit:

         |--------------------------|
         | Toán tử | Tác dụng       |
         | -------------------------|
         | &       | AND            |
         | |       | OR             |
         | ^       | XOR            |
         | ~       | NOT            |
         | <<      | Dịch trái      |
         | >>      | Dịch phải      |
         |--------------------------|

**f. Ternary Operator (Toán tử điều kiện 3 ngôi):**

- Cú pháp:
  &lt;điều kiện&gt; ? &lt;giá trị nếu true&gt; : &lt;giá trị nếu false&gt;

**III. Câu lệnh điều kiện và Vòng lặp (Control Flow Statements)**

_1. Câu lệnh if, else if, else_

- Cú pháp:

{% raw %}

         if(điều kiện 1) {
           // thực thi block code nếu điều kiện 1 đúng
         } else if(điều kiện 2) {
           // nếu điều kiện 1 sai, kiểm tra điều kiện 2, nếu đúng thì thực thị block code này
         } else {
           // thực thi block code này nếu không có điều kiện nào đúng
         }

{% endraw %}

_2. Switch case_

- Cú pháp:

{% raw %}

         switch (biểu thức) {
           case giá_trị_1:
             // code
             break;
           case giá_trị_2:
             // code
             break;
           default:
           // nếu không trùng case nào
         }

{% endraw %}

**Lưu ý:**

- Nếu không có **Break**, chương trình sẽ chạy liên tiếp các case sau(gọi là fall through).
- Từ Java 14+ cú pháp switch mới với ->.

_3. Vòng lặp for, while, do-while_

a. for - vòng lặp xác định số lần lặp

{% raw %}

         for (int i = 0; i < 5; i++) {
           System.out.println("Lần thứ " + i);
         }

{% endraw %}

b. while - lặp khi điều kiện còn đúng

{% raw %}

         int i = 0;
         while (i < 5) {
           System.out.println("While lần " + i);
           i++;
         }

{% endraw %}

c. do-while – luôn chạy ít nhất 1 lần

{% raw %}

         int i = 0;
         do {
             System.out.println("Do-while lần " + i);
             i++;
         } while (i < 5);

{% endraw %}

**- Khác biệt:**

- while: kiểm tra trước – nếu sai, không chạy.
- do-while: chạy trước – kiểm tra sau, luôn chạy ít nhất 1 lần.

_4. Câu lệnh điều hướng vòng lặp break, continue, return_

         |-------------------------------------------------------------------|
         | Lệnh      | Ý nghĩa                                               |
         |-------------------------------------------------------------------|
         | break     | Thoát hoàn toàn khỏi vòng lặp hoặc switch             |
         | continue  | Bỏ qua vòng lặp hiện tại, chuyển sang lần lặp kế tiếp |
         | return    | Trả về giá trị và thoát khỏi phương thức ngay lập tức |
         |-------------------------------------------------------------------|

**IV. Mảng và Chuỗi (Arrays and Strings)**

_1. Mảng 1 chiều, 2 chiều (1D/2D Arrays)_  
a. Mảng 1 chiều (1D array)  
-Lưu trữ danh sách các phần tử cùng kiểu, với chỉ số bắt đầu từ 0.

- Cú pháp:

{% raw %}

          int[] numbers = new int[5]; // mảng có 5 phần tử
          int[] scores = {90, 80, 70}; // khai báo và khởi tạo

{% endraw %}

- Duyệt mảng:

{% raw %}

         for (int i = 0; i < scores.length; i++) {
            System.out.println(scores[i]);
         }

{% endraw %}

b. Mảng 2 chiều (2D array)

- Giống như bảng hoặc ma trận.
- Cú pháp:

{% raw %}

         int[][] matrix = new int[3][2]; // 3 hàng, 2 cột

         int[][] matrix2 = {{1, 2}, {3, 4}, {5, 6}};

{% endraw %}

- Duyệt mảng:

{% raw %}

      for (int i = 0; i &lt; matrix.length; i++) {

       for (int j = 0; j &lt; matrix[i].length; j++) {

          System.out.print(matrix[i][j] + " ");

       }
        System.out.println();
      }

{% endraw %}

_2. Duyệt mảng bằng for-each (Enhanced for loop)_

-Dùng để duyệt qua các phần tử trong mảng (array) hoặc collection (List, Set,...) mà không cần chỉ số (index).

{% raw %}

         for (Kiểu_dữ_liệu biến : tập_hợp) {
           // xử lý với biến
         }

{% endraw %}

**- Lưu ý:**

- for-each không dùng được khi bạn cần biết chỉ số phần tử (index) hoặc muốn sửa giá trị trong mảng.
- Nếu cần thêm/xóa phần tử trong vòng lặp, nên dùng Iterator thay vì for-each.

_3. String và thao tác chuỗi (substring, replace, split, etc.)_

- String trong Java là immutable (bất biến):

{% raw %}

           String s = "Hello";
           s.toUpperCase(); // không thay đổi s

{% endraw %}

- Các phương thức thông dụng:

         |-------------------------------------------------------------------------------------------------------------|
         | Phương thức        | Mô tả                               | Ví dụ                                            |
         |-------------------------------------------------------------------------------------------------------------|
         | substring()        | Cắt chuỗi con                       | "hello".substring(1, 3) → "el"                   |
         | replace()          | Thay thế ký tự                      | "java".replace('a', 'o') → "jovo"                |
         | split()            | Tách chuỗi thành mảng               | "a,b,c".split(",") → ["a", "b", "c"]             |
         | indexOf()          | Vị trí ký tự/chuỗi con đầu tiên     | "java".indexOf("v") → 2                          |
         | equals()           | So sánh nội dung                    | "abc".equals("abc") → true                       |
         | equalsIgnoreCase() | So sánh bỏ qua hoa/thường           | "Java".equalsIgnoreCase("java") → true           |
         |-------------------------------------------------------------------------------------------------------------|

_4. StringBuilder, StringBuffer – hiệu suất thao tác chuỗi_

- StringBuilder :
  - Mutable (có thể thay đổi nội dung).
  - Không đồng bộ (non-synchronized) → Nhanh hơn StringBuffer
  - Dùng trong các ứng dụng single-thread.
- StringBuffer:
  - Mutable và synchronized → Thread-safe, dùng trong multi-threaded environments
  - Nhưng do việc đồng bộ nên sẽ chậm hơn StringBuilder.

_5. So sánh hiệu suất_

         |---------------------------------------------------------------------|
         | Tính năng             | String    | StringBuilder | StringBuffer    |
         |---------------------------------------------------------------------|
         | Tính bất biến         | Có        | Không         | Không           |
         | Thread-safe           | Không     | Không         | Có              |
         | Hiệu suất thao tác    | Chậm nhất | Nhanh nhất    | Trung bình      |
         | Dùng trong môi trường | VBất kỳ   | Single-thread | Multi-thread    |
         |---------------------------------------------------------------------|

**V. Lập trình hướng đối tượng - OOP (Object-Oriented Programming)**

**1. Lớp và Đối tượng (Class & Object)**

**2. Tính đóng gói (Encapsulation)**

**3. Kế thừa (Inheritance)**

**4. Đa hình (Polymorphism)**

**5. Trừu tượng (Abstraction)**
