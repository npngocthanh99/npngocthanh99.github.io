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
         | -=       | a -= 2   | a = a - 2                  |
         | *=       | a *= 3   | a = a * 3                  |
         | /=       | a /= 4   | a = a / 4                  |
         | %=       | a %= 5    | a = a % 5                 |
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
         | Dùng trong môi trường | Bất kỳ    | Single-thread | Multi-thread    |
         |---------------------------------------------------------------------|

**V. Lập trình hướng đối tượng - OOP (Object-Oriented Programming)**

**Lập trình hướng đối tượng(OOP)** là một phương pháp lập trình mà ở đó, chúng ta tổ chức và thiết kế chương trình dựa trên các đối tượng thay vì các hàm hay logic. Mục tiêu chính của OOP là **tái sử dụng mã nguồn**, giúp chương trình **dễ quản lý, mở rộng và bảo trì hơn.**

**1. Lớp và Đối tượng(Class & Object)**

- **Lớp(Class)** có thể hình dung như một **bản thiết kế** hoặc một **khuôn mẫu** để tạo ra các đối tượng. Nó định nghĩa các **thuộc tính(attribute)** và **hành vi(methods)** mà các đối tượng thuộc lớp đó sẽ có. Ví dụ: chúng ta có một lớp **ConNguoi** có các thuộc tính như **tên, tuổi** và cách hành vi như **ăn, ngủ**.

- **Đối tượng(Object)** chính là một thể hiện cụ thể của một lớp. Hay nói cách khác, nó là một 'sản phẩm' được tạo ra từ bản thiết kế đó. Ví dụ: 'Anh Hoàn' với 25 tuổi là một đối tượng cụ thể của lớp **ConNguoi**, hoặc 'Chị Thư' với 30 tuổi cũng là một đối tượng khác của lớp **ConNguoi**.

**2. Tính đóng gói(Encapsulation)**

- **Tính đóng gói(Encapsulation)** là một trong những nguyên lý cơ bản của OOP, hiểu đơn giản là việc **gom các thuộc tính và hành vi có liên quan lại thành một thể thống nhất** (là một lớp) và **ẩn đi các chi tiết triển khai bên trong**, chỉ cho phép truy cập thông qua các giao diện công khai (public methods)

- Trong lập trình, tính đóng gói giúp **bảo vệ dữ liệu khỏi bị truy cập hoặc thay đổi trực tiếp một cách không mong muốn**, từ đó giúp mã nguồn **an toàn và dễ bảo trì hơn**.

- **Kinh nghiệm dự án:** Với những dự án lớn có nhiều thành viên trong team, thì tính đóng gói giúp ngăn chặn các truy cập thay đổi, nhầm lẫn từ các thành viên khác. Khi khai báo các thuộc tính, và phương thức với access modifiers có thể hạn chế điều đó.

**3. Kế thừa(Inheritance)**

- **Kế thừa(Inheritance)** là một cơ chế trong OOP cho phép một **lớp con(subclass)** có thể **thừa hưởng các thuộc tính và hành vi từ một lớp cha(superclass)**. Điều này giúp chúng ta **tái sử dụng mã nguồn**, tránh việc phải viết lại những phần giống nhau.
  - Ví dụ: chúng ta có lớp cha là **DongVat**. Các lớp con như **Cho**, **Meo**, **Chim** đều có thể kế thừa các thuộc tính chung như **soChan**, **mauLong** và các hành vi như **diChuyen**, **an**. Sau đó, mỗi lớp con có thể thêm vào những đặc điểm hoặc hành vi riêng của mình, ví dụ **Cho** có thêm hành vi **sua**, **Meo** có thêm hành vi **keuMeoMeo**.

**4. Đa hình (Polymorphism)**

- **Đa hình(Polymorphism)** nghĩa là một đối tượng có thể mang nhiều hình thái khác nhau, hoặc một hành động có thể được thực hiện theo nhiều cách khác nhau tùy thuộc vào ngữ cảnh. Có hai loại đã hình chính là:

  - **Đa hình lúc biên dịch(Compile-time Polymorphism)**, thường được biết đến qua **nạp chồng phương thức(Method Overloading)**. tức là trong một lớp, chúng ta có thể có nhiều phương thức cùng tên nhưng khác nhau về số lượng hoặc kiểu dữ liệu của tham số, hoặc dữ liệu trả về. Ví dụ phương thức **tinhTong(int a, int b)** và **tinhTong(double a, double b, double c)**.
  - **Đa hình lúc chạy(Runtime Polymorphism)**, thường được biết đến qua **ghi đè phương thức(Method Overriding)**. Tức là lớp con định nghĩa lại một phương thức đã có ở lớp cha. Ví dụ, lớp **DongVat** có phương thức **tiengKeu()**, nhưng lớp **Cho** và **Meo** đều ghi đè phương thức này để phát ra tiếng kêu riêng của chúng ('gâu gâu' và 'meo meo'). Điều này giúp chương trình linh hoạt hơn khi xử lý các đối tượng thuộc các lớp khác nhau nhưng có cùng một hành vi chung."

**5. Trừu tượng (Abstraction)**

- **Trừu tượng(Abstraction)** là quá trình **ẩn đi các chi tiết phức tạp** và chỉ **hiển thị những thông tin cần thiết** ra bên ngoài. Nó tập trung vào **'cái gì'** hơn là **'làm như thế nào'**. Trong OOP, chúng ta thường đạt được tính trừu tượng thông qua **lớp trừu tượng(Abstract Class)** và **giao diện(Interface)**.
  - Ví dụ: Khi thiết kế phần xử lý thanh toán đơn hàng. Cụ thể, ta tạo một interface là **PaymentMethod** - trong đó định nghĩa các hành vi chung như **processPayment()** và **refund()**. Sau đó, chúng ta triển khai nhiều class khác nhau như **CreditCardPayment**, **PaypalPayment**, và **BankTransferPayment**, mỗi class sẽ có cách xử lý thanh toán riêng phù hợp với từng phương thức cụ thể. Nhờ vậy, ở bussiness logic, ví dụ như khi xử lý đơn hàng, chúng ta chỉ cần gọi **paymentMethod.processPayment()** mà không cần quan tâm chi tiết nó là thanh toán qua thẻ, qua PayPal hay chuyển khoản ngân hàng. Điều này giúp code dễ mở rộng, ví dụ sau này có thêm MOMO hay ZaloPay thì chỉ cần tạo thêm một class mới implement **PaymentMethod** mà không phải sửa code xử lý đơn hàng.

**VI. Các thành phần OOP nâng cao(Advanced OOP Concepts)**

1. this, super

- this: đại diện cho một đối tượng hiện tại.

  - Truy cập biến hoặc phương thức của đối tượng đó.
  - Gọi constructor khác trong cùng class

        {% raw %}
        class Person {
          String name;
          Person(String name) {
            this.name = name; // phân biệt biến instance và tham số
          }
        }
        {% endraw %}

- super: đại diện cho lớp cha (supper class)

  - Dùng để gọi constructor hoặc phương thức của lớp cha.

        {% raw %}
        class Animal {
          void speak() {
            System.out.println("Animal speaks");
          }
        }

        class Dog extends Animal {
          void speak() {
            super.speak(); // gọi phương thức lớp cha
            System.out.println("Dog barks");
          }
        }
        {% endraw %}

2. Constructor - Constructor overloading

- Constructor: phương thức đặc biệt, cùng tên class, không có kiểu dữ liệu trả về.

        {% raw %}
        class Student {
          String name;
          Student(String n) {
            name = n;
          }
        }
        {% endraw %}

- Constructor overloading: nhiều constructor cùng tên nhưng khác tham số.

        {% raw %}
        class Student {
          String name;
          int age;

          Student(String n) {
            name = n;
          }

          Student(String n, int a) {
            this.name = n;
            this.age = a;
          }
        }
        {% endraw %}

3.  Method Overloading vs Overriding

         |----------------------------------------------------------------------------------------------------------------------------------------|
         |       Đặc điểm              | Overloading                                        | Overriding                                          |
         |----------------------------------------------------------------------------------------------------------------------------------------|
         | Định nghĩa                  | Cùng tên phương thức, khác tham số trong cùng lớp  | Cùng tên, cùng tham số, khác lớp (cha - con)        |
         | Mục đích                    | Tăng tính đa hình tĩnh (compile time polymorphism) | Tăng tính đa hình động (runtime polymorphism)       |
         | Quan hệ lớp                 | Trong cùng một lớp                                 | Giữa lớp cha và lớp con                             |
         | Quy tắc | Bất kỳ            | Tham số khác nhau (kiểu, số lượng, thứ tự)         | Phải giống hoàn toàn về tên, kiểu, thứ tự tham số   |
         | Thời điểm quyết định        | Compile time                                       | Runtime                                             |
         | Annotation dùng được không? | Không dùng @Override                               | Nên dùng @Override để tránh lỗi đánh máy            |
         |----------------------------------------------------------------------------------------------------------------------------------------|

Ví dụ:

**Overloading:**

        {% raw %}
        class Calculator {
          int add(int a, int b) { return a + b; }
          double add(double a, double b) { return a + b; }
        }
        {% endraw %}

**Overriding:**

        {% raw %}
        class Animal {
          void sound() { System.out.println("Some sound"); }
        }

        class Dog extends Animal {
        @Override
          void sound() { System.out.println("Woof"); }
        }
        {% endraw %}

4.  final, static, abstract, interface, enum

a. final

         |-------------------------------------------------------------------------|
         | Trường hợp sử dụng |       Ý nghĩa                                      |
         |-------------------------------------------------------------------------|
         | Biến (variable)    | Không thể thay đổi giá trị sau khi gán (hằng số)   |
         | Phương thức        | Không thể override ở lớp con                       |
         | Lớp (class)        | Không thể kế thừa                                  |
         |-------------------------------------------------------------------------|

ví dụ:

        {% raw %}
        final class Constants {
          public static final double PI = 3.14159;
        }
        {% endraw %}

b. static

         |---------------------------------------------------------------------------------------------------------------|
         | Trường hợp sử dụng | Ý nghĩa                                                                                  |
         |---------------------------------------------------------------------------------------------------------------|
         | Biến (variable)    | Biến dùng chung cho tất cả các đối tượng của lớp                                         |
         | Phương thức        | Gọi mà không cần tạo đối tượng                                                           |
         | Block              | Được chạy một lần duy nhất khi class được load, được thực thi trước cả main() và trước   |
         |                    | khi tạo đối tượng                                                                        |
         | Lớp (class)        | Chỉ dùng với nested class (lớp bên trong), không thể truy cập biến non-static bên ngoài  |
         |---------------------------------------------------------------------------------------------------------------|

ví dụ:
**static block**

        {% raw %}
        public class StaticBlockExample {
          static int value;

          // static block
          static {
            System.out.println("Static block executed");
            value = 100;
          }

          public StaticBlockExample() {
            System.out.println("Constructor called");
          }

          public static void main(String[] args) {
            System.out.println("Main method started");
            StaticBlockExample obj = new StaticBlockExample();
            System.out.println("Value = " + StaticBlockExample.value);
          }
        }
        {% endraw %}

**static class**

        {% raw %}
        public class OuterClass {
          int outerValue = 10;
          static int staticOuterValue = 20;

          static class StaticNestedClass {
            void display() {
              // System.out.println(outerValue); // Error: Cannot access non-static
              System.out.println("Static outer value: " + staticOuterValue);
            }
          }

          public static void main(String[] args) {
            OuterClass.StaticNestedClass nested = new OuterClass.StaticNestedClass();
            nested.display();
          }
        }
        {% endraw %}

c. abstract

         |--------------------------------------------------------------------|
         | Trường hợp sử dụng | Ý nghĩa                                       |
         |--------------------------------------------------------------------|
         | Phương thức        | Không có thân hàm, bắt buộc lớp con override  |
         | Lớp (class)        | Không thể tạo đối tượng, chỉ để kế thừa       |
         |--------------------------------------------------------------------|

Ví dụ:

        {% raw %}
        abstract class Animal {
          abstract void sound();
        }

        class Cat extends Animal {
          void sound() { System.out.println("Meow"); }
        }
        {% endraw %}

d. interface

- Là một tập hợp các phương thức trừu tượng (Java 8 trở đi hỗ trợ default + static method)
- Một lớp có thể implement nhiều interface
  Ví dụ:

        {% raw %}
        interface Movable {
          void move();
        }

        class Car implements Movable {
          public void move() {
            System.out.println("Car is moving");
          }
        }
        {% endraw %}

e. enum

- Đại diện cho một tập hợp hằng số có định danh
- Có thể có constructor, phương thức, biến
- Ví dụ:

       {% raw %}
       enum Day {
         MONDAY, TUESDAY, WEDNESDAY;
       }
       {% endraw %}

**VII. Phạm vi truy cập(Access Modifiers)**

1. Private

- **Phạm vi:**Chỉ truy cập được trong cùng một class.
- **Không thể** truy cập từ class khác, kể cả trong cùng package.
- **Thường dùng cho:**

  - Thuộc tính (fields) để bảo vệ dữ liệu.
  - Hàm hỗ trợ (helper methods) nội bộ.

Ví dụ:

        {% raw %}
        class MyClass {
          private int data;

          private void helperMethod() {
          // chỉ dùng nội bộ
          }
        }
        {% endraw %}

2. Default(package-private)

- **Phạm vi:** Truy cập được trong cùng package.
- **Không thể** truy cập từ bên ngoài package.
- **Thường dùng cho:**

  - Class cấp package (helper class)
  - Những method không cần public nhưng vẫn cần dùng trong các class cùng package.

Ví dụ:

        {% raw %}
        class MyClass { // default class
          int count;    // default field

          void increase() { // default method
            count++;
          }
        }
        {% endraw %}

3. Protected

- **Phạm vi:** Truy cập được trong:

  - Cùng package
  - Lớp con (subclass), kể cả khi subclass ở package khác.

- **Thường dùng cho:**

  - Class cha muốn cho phép lớp con kế thừa và sử dụng.
  - Một cách tiếp cận giữa private và public.

Ví dụ:

        {% raw %}
        public class Animal {
          protected void makeSound() {
            System.out.println("Some sound");
          }
        }

        class Dog extends Animal {
          void bark() {
            makeSound(); // hợp lệ do kế thừa
          }
        }
        {% endraw %}

4. Public

- Phạm vi: Mọi nơi đều truy cập được.
- Thường dùng cho:
  - API bên ngoài
  - Class chính, method chính (như public static void main).

Ví dụ:

        {% raw %}
        public class Person {
          public String name;

          public void sayHello() {
            System.out.println("Hello");
          }
        }
        {% endraw %}

5.  Tóm tắt về khả năng truy cập

         |--------------------------------------------------------------------------------------|
         | Access Modifier | Cùng class | Cùng package | Subclass(khác package) |   Bên ngoài   |
         |--------------------------------------------------------------------------------------|
         |    private      |    ✅     |       ❌     |           ❌           |     ❌       |
         |--------------------------------------------------------------------------------------|
         |    default      |    ✅     |       ✅     |           ❌           |     ❌       |
         |--------------------------------------------------------------------------------------|
         |    protected    |    ✅     |       ✅     |           ✅           |     ❌       |
         |--------------------------------------------------------------------------------------|
         |    public       |    ✅     |       ✅     |           ✅           |     ✅       |
         |--------------------------------------------------------------------------------------|

**VIII. Xử lý ngoại lệ(Exception Handlling)**

Trong Java, Exception Handling giúp chương trình xử lý lỗi một cách an toàn mà không bị crash, duy trì luồng chạy mạch lạc và kiểm soát logic khi có tình huống bất thường xảy ra.

1. Try - Catch - Finally

- Mục đích:
  - try: chứa đoạn code có thể xảy ra lỗi.
  - catch: xử lý ngoại lệ nếu xảy ra.
  - finally: luôn thực hiện, dù có hay không có lỗi – thường dùng để đóng tài nguyên.
- Cú pháp:

        {% raw %}
        try {
          // đoạn code có thể ném lỗi
        } catch (ExceptionType e) {
          // xử lý lỗi
        } finally {
          // luôn thực hiện (ví dụ: đóng file, kết nối DB)
        }
        {% endraw %}

- Ví dụ:

        {% raw %}
        try {
          int result = 10 / 0; // ArithmeticException
        } catch (ArithmeticException e) {
          System.out.println("Không thể chia cho 0!");
        } finally {
          System.out.println("Kết thúc xử lý!");
        }
        {% endraw %}

2. Throw và Throws

- throw: dùng để ném một ngoại lệ cụ thể trong code.

        {% raw %}
        throw new IllegalArgumentException("Sai tham số!");
        {% endraw %}

- throws: dùng trong chữ ký method để khai báo rằng method này có thể ném ra ngoại lệ.

        {% raw %}
        public void readFile(String file) throws IOException {
          // logic đọc file
        }
        {% endraw %}

- Ví dụ đầy đủ:

          {% raw %}
          public void divide(int a, int b) throws ArithmeticException {
            if (b == 0) {
              throw new ArithmeticException("Không chia được cho 0");
            }
            System.out.println(a / b);
          }
          {% endraw %}

3.  Checked vs Unchecked Exception

         |--------------------------------------------------------------------------------------------------------------|
         | Loại        | Kế thừa từ                       | Compiler bắt buộc xử lý        | Ví dụ                      |
         |--------------------------------------------------------------------------------------------------------------|
         | Checked     | Exception (trừ RuntimeException) | Bắt buộc try-catch hoặc throws | IOException,               |
         |             |                                  |                                | SQLException,              |
         |             |                                  |                                | ParseException             |
         |--------------------------------------------------------------------------------------------------------------|
         | Unchecked   | RuntimeException                 | Không bắt buộc xử lý           | NullPointerException,      |
         |             |                                  |                                | IllegalArgumentException,  |
         |             |                                  |                                | ArithmeticException        |
         |--------------------------------------------------------------------------------------------------------------|

- Ví dụ Checked:

          {% raw %}
          public void readFile(String path) throws IOException {
            FileReader fr = new FileReader(path); // IOException là checked
          }
          {% endraw %}

- Ví dụ Unchecked:

          {% raw %}
          int[] arr = new int[3];
          arr[5] = 10; // ArrayIndexOutOfBoundsException – Unchecked
          {% endraw %}

4.  Tạo ngoại lệ tùy chỉnh(Custom Exception)

- Trường hợp sử dụng:
  - Khi muốn đại diện cho lỗi nghiệp vụ cụ thể.
  - Giúp code rõ ràng, dễ hiểu, dễ bảo trì.
- Cách tạo:

          {% raw %}
          // 1. Tạo class kế thừa Exception hoặc RuntimeException
          public class InvalidAgeException extends RuntimeException {
            public InvalidAgeException(String message) {
              super(message);
            }
          }

          // 2. Dùng throw để ném lỗi
          public void checkAge(int age) {
            if (age < 18) {
              throw new InvalidAgeException("Tuổi phải lớn hơn 18");
            }
          }
          {% endraw %}

**IX. Collection Framework**

Java Collection Framework là tập hợp các interface và class dùng để lưu trữ, xử lý và thao tác dữ liệu theo dạng collection (danh sách, tập hợp, ánh xạ, hàng đợi, v.v.).

1.  Interfaces: List, Set, Map, Queue

         |-----------------------------------------------------------------------------------------------------------------------|
         | Interface | Đặc điểm                                    | Dùng khi cần                                                |
         |-----------------------------------------------------------------------------------------------------------------------|
         | List      | Cho phép phần tử trùng, có thứ tự,          | Danh sách có thứ tự (ArrayList, LinkedList)                 |
         |           | truy cập theo chỉ số                        |                                                             |
         |-----------------------------------------------------------------------------------------------------------------------|
         | Set       | Không cho phép phần tử trùng                | Lưu tập hợp không trùng lặp (HashSet, TreeSet)              |
         |-----------------------------------------------------------------------------------------------------------------------|
         | Map       | Lưu theo cặp key-value, không cho key trùng | Bản đồ ánh xạ (HashMap, TreeMap)                            |
         |-----------------------------------------------------------------------------------------------------------------------|
         | Queue     | Cấu trúc FIFO (First-In-First-Out)          | Hàng đợi, xử lý theo thứ tự vào (LinkedList, PriorityQueue) |
         |-----------------------------------------------------------------------------------------------------------------------|

2.  Implementations: ArrayList, LinkedList, HashSet, TreeSet, HashMap, TreeMap

         |----------------------------------------------------------------------------------|
         |   Class    | Implements  | Đặc điểm chính                                        |
         |----------------------------------------------------------------------------------|
         | ArrayList  | List        | Mảng động, truy cập nhanh, chèn/xóa chậm              |
         |----------------------------------------------------------------------------------|
         | LinkedList | List, Queue | Danh sách liên kết, chèn/xóa nhanh, truy cập chậm     |
         |----------------------------------------------------------------------------------|
         | HashSet    | Set         | Không cho phép phần tử trùng, không đảm bảo thứ tự    |
         |----------------------------------------------------------------------------------|
         | TreeSet    | Set         | Sắp xếp phần tử theo thứ tự tự nhiên hoặc comparator  |
         |----------------------------------------------------------------------------------|
         | HashMap    | Map         | Cho phép null key/value, không sắp xếp                |
         |----------------------------------------------------------------------------------|
         | TreeMap    | Map         | Sắp xếp theo thứ tự key (Comparable/Comparator)       |
         |----------------------------------------------------------------------------------|

3.  Iterator, ListIterator, for-each

- Iterator:

  - Duyệt qua collection.
  - Hỗ trợ xóa phần tử khi duyệt.

            {% raw %}
            Iterator<String> it = list.iterator();
            while(it.hasNext()) {
              String s = it.next();
              if(s.equals("x")) it.remove(); // xóa phần tử khi duyệt
            }
            {% endraw %}

- ListIterator:

  - Chỉ dùng với List
  - Duyệt hai chiều (next/previous), cho phép thêm, sửa, xóa trong quá trình lặp.

- for-each:

  - Dễ dùng, ngắn gọn, không chỉnh sửa collection được.

            {% raw %}
            for (String s : list) {
              System.out.println(s);
            }
            {% endraw %}

4.  So sánh HashMap vs Hashtable

         |------------------------------------------------------------------------------------------------------------------------|
         |   Tiêu chí              | HashMap                                   | Hashtable                                        |
         |------------------------------------------------------------------------------------------------------------------------|
         | Đồng bộ (Synchronized)  | Không                                     | Có                                               |
         |------------------------------------------------------------------------------------------------------------------------|
         | Hiệu suất               | Tốt hơn (trong môi trường đơn luồng)      | Kém hơn (do đồng bộ)                             |
         |------------------------------------------------------------------------------------------------------------------------|
         | Cho phép null           | 1 null key, nhiều null value              | Không cho null key/value                         |
         |------------------------------------------------------------------------------------------------------------------------|
         | Thay thế hiện đại       | ConcurrentHashMap dùng thay cho Hashtable | Đã lỗi thời                                      |
         |------------------------------------------------------------------------------------------------------------------------|
         | Môi trường sử dụng      | Dùng cho đa số ứng dụng                   | Không nên dùng nữa (trừ khi cần đồng bộ cổ điển) |
         |------------------------------------------------------------------------------------------------------------------------|

**X. Generics**

Generics giúp bạn viết code tổng quát, tái sử dụng, an toàn kiểu dữ liệu mà không cần ép kiểu thủ công.

1. Generic Class, Method

- Generic Class: cho phép định nghĩa class có kiểu dữ liệu tổng quát.

  - Ví dụ:

            {% raw %}
            public class Box<T> {
              private T value;
              public void set(T value) { this.value = value; }
              public T get() { return value; }
            }
            {% endraw %}

  - Sử dụng:

            {% raw %}
            Box<String> stringBox = new Box<>();
            stringBox.set("Hello");
            String val = stringBox.get(); // không cần ép kiểu
            {% endraw %}

- Generic Method: kiểu dữ liệu tổng quát ngay trong method.

  - Ví dụ:

                {% raw %}
                public class Utils {
                  public static <T> void printArray(T[] array) {
                    for (T item : array) {
                      System.out.println(item);
                    }
                  }
                }
                {% endraw %}

2.  Wildcards: ?, ? extends, ? super

         |-------------------------------------------------------------------|
         |  Ký hiệu    | Ý nghĩa               | Dùng khi                    |
         |-------------------------------------------------------------------|
         | ?           | Bất kỳ kiểu nào       | Không cần biết kiểu cụ thể  |
         |-------------------------------------------------------------------|
         | ? extends T | Bất kỳ kiểu con của T | Đọc (read) dữ liệu an toàn  |
         |-------------------------------------------------------------------|
         | ? super T   | Bất kỳ kiểu cha của T | Ghi (write) dữ liệu an toàn |
         |-------------------------------------------------------------------|

- Ví dụ:

            {% raw %}
            List<? extends Number> numbers; // List của Integer, Double, Float đều được
            List<? super Integer> ints;     // List của Integer, Number, Object
            {% endraw %}

- Hiểu đơn giản:

         |---------------------------------------|
         |  Hiểu đơn giản:        | 	Dùng       |
         |---------------------------------------|
         | Đọc là chính           | ? extends T  |
         |---------------------------------------|
         | Ghi là chính           | ? super T    |
         |---------------------------------------|
         | Không quan tâm kiểu gì |      ?       |
         |---------------------------------------|

3.  Type Inference (Diamond operator)

- Từ Java 7, có thể không cần ghi lại kiểu dữ liệu ở bên phải khi khởi tạo.

- Trước Java 7:

            {% raw %}
            List<String> list = new ArrayList<String>();
            {% endraw %}

- Từ Java 7 trở đi – Diamond operator:

            {% raw %}
            List<String> list = new ArrayList<>();
            {% endraw %}

  - Trình biên dịch sẽ tự suy ra kiểu dữ liệu (Type Inference) từ bên trái.

**XI. Java I/O (Input/Output)**

1. File, FileReader, FileWriter

- File :

  - Đại diện cho đường dẫn tới file hoặc thư mục.
  - **Chức năng:** kiểm tra file tồn tại, tạo mới file/thư mục, xóa, lấy thông tin file.

            {% raw %}
            File file = new File("data.txt");
            if (!file.exists()) {
              file.createNewFile();
            }
            System.out.println("Tên file: " + file.getName());
            {% endraw %}

- FileReader,FileWriter

  - Đọc và ghi ký tự (text) vào file, dùng cho file văn bản.

            {% raw %}
            // Ghi file
            FileWriter writer = new FileWriter("data.txt");
            writer.write("Xin chào Java!");
            writer.close();

            // Đọc file
            FileReader reader = new FileReader("data.txt");
            int c;
            while ((c = reader.read()) != -1) {
              System.out.print((char) c);
            }
            reader.close();
            {% endraw %}

2. BufferedReader, BufferedWriter

- Gói ngoài FileReader/FileWriter để tăng hiệu năng nhờ bộ nhớ đệm.
- Hỗ trợ đọc, ghi dòng văn bản (line-based).

            {% raw %}
            // Ghi file bằng BufferedWriter
            BufferedWriter bw = new BufferedWriter(new FileWriter("data.txt"));
            bw.write("Dòng 1");
            bw.newLine();
            bw.write("Dòng 2");
            bw.close();

            // Đọc file bằng BufferedReader
            BufferedReader br = new BufferedReader(new FileReader("data.txt"));
            String line;
            while ((line = br.readLine()) != null) {
              System.out.println(line);
            }
            br.close();
            {% endraw %}

3. InputStream, OutputStream

- Dùng để đọc/ghi byte, phù hợp với file nhị phân (ảnh, âm thanh…).
- Là lớp cha của các stream như: FileInputStream, BufferedInputStream.

          {% raw %}
          // Đọc file nhị phân
          FileInputStream fis = new FileInputStream("image.jpg");
          int b;

          while ((b = fis.read()) != -1) {
          // Xử lý byte b
          }
          fis.close();

          // Ghi file nhị phân
          FileOutputStream fos = new FileOutputStream("copy.jpg");
          fos.write(123); // ghi byte
          fos.close();
          {% endraw %}

4. Serialization / Deserialization

- Serialization: biến object thành chuỗi byte để lưu vào file hoặc truyền qua mạng.
- Deserialization: đọc chuỗi byte và tạo lại object.

- Class phải implement Serializable.

          {% raw %}
          // Serializable class
          class Student implements Serializable {
          private String name;
          private int age;
          // constructor, getter, setter
          }

          // Serialization
          ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("student.ser"));
          oos.writeObject(new Student("Nam", 20));
          oos.close();

          // Deserialization
          ObjectInputStream ois = new ObjectInputStream(new FileInputStream("student.ser"));
          Student s = (Student) ois.readObject();
          System.out.println(s.getName());
          ois.close();
          {% endraw %}

**XII. Đa luồng & Xử lý đồng thời (Multithreading and Concurrency)**

1. Tạo Thread: Thread, Runnable

- Cách 1: implement Runnable (Interface):

  - Cách tạo thread bằng cách triển khai interface Runnable và override run():
  - Ưu điểm:

    - Linh hoạt, có thể kế thừa lớp khác.
    - Tách biệt logic run() ra khỏi Thread, tốt cho thiết kế hướng đối tượng (OOP).
    - Nên dùng trong thực tế hơn cách kế thừa Thread.

                {% raw %}
                class MyRunnable implements Runnable {
                  public void run() {
                    System.out.println("Thread đang chạy bằng cách implement Runnable.");
                  }
                }

                public class Main {
                  public static void main(String[] args) {
                    Thread t1 = new Thread(new MyRunnable());
                    t1.start();
                  }
                }
                {% endraw %}

- Cách 2: extend Thread (Class):

  - Có thể kế thừa lớp Thread và override run():
  - Ưu điểm:
    - Dễ viết, trực tiếp override phương thức run().
  - Nhược điểm:

    - Không thể kế thừa lớp khác vì Java chỉ cho kế thừa một lớp (single inheritance).

                {% raw %}
                class MyThread extends Thread {
                  public void run() {
                      System.out.println("Thread đang chạy bằng cách kế thừa Thread.");
                  }
                }

                public class Main {
                  public static void main(String[] args) {
                    MyThread t1 = new MyThread();
                    t1.start(); // KHÔNG dùng t1.run()
                  }
                }
                {% endraw %}

- So sánh Thread vs Runnable

         |-------------------------------------------------------------------------------------------------------|
         |  Tiêu chí             | Thread (extends)                     | Runnable (implements)                  |
         |-------------------------------------------------------------------------------------------------------|
         | Kế thừa lớp khác      | Không thể                            | Có thể                                 |
         |-------------------------------------------------------------------------------------------------------|
         | Tái sử dụng đối tượng | Ít linh hoạt                         | Dễ tái sử dụng                         |
         |-------------------------------------------------------------------------------------------------------|
         | Khuyến nghị sử dụng   | Trong hầu hết các trường hợp         | Thực tế khuyên dùng                    |
         |-------------------------------------------------------------------------------------------------------|
         | Gắn logic riêng       | Gắn trực tiếp trong run() của Thread | Gắn vào class riêng, truyền cho Thread |
         |-------------------------------------------------------------------------------------------------------|

2. Lifecycle của Thread

- Các trạng thái chính:

         |---------------------------------------------------------|
         |  Trạng thái           | Mô tả                           |
         |---------------------------------------------------------|
         | NEW                   | Thread được tạo nhưng chưa chạy |
         | RUNNABLE              | Thread đang chờ CPU để chạy     |
         | RUNNING               | Thread đang thực thi            |
         | BLOCKED               | Thread chờ khóa (monitor lock)  |
         | WAITING/TIMED_WAITING | Chờ điều kiện hoặc thời gian    |
         | TERMINATED            | Thread kết thúc                 |
         |---------------------------------------------------------|

- Dùng thread.getState() để kiểm tra trạng thái.

3. synchronized, volatile, wait, notify, join

- synchronized

  - Dùng để đồng bộ truy cập tài nguyên.

            {% raw %}
            synchronized (this) {
              // chỉ một thread được vào đây tại 1 thời điểm
            }
            {% endraw %}

- volatile

  - Báo cho JVM biết biến luôn được đọc trực tiếp từ bộ nhớ chính (main memory) — không cache ở thread-local.

            {% raw %}
            volatile boolean running = true;
            {% endraw %}

- wait() / notify() / notifyAll()

  - Dùng cho giao tiếp giữa các thread đang chia sẻ monitor lock.

            {% raw %}
            synchronized (obj) {
              obj.wait();      // Thread tạm dừng và nhả lock
              obj.notify();    // Đánh thức 1 thread đang chờ obj
            }
            {% endraw %}

  - Sự khác biệt giữa wait() và sleep():
    - wait() nhả lock, còn sleep() không nhả lock.

- join

  - Cho phép một thread chờ thread khác kết thúc.

            {% raw %}
            Thread t = new Thread(() -> {...});
            t.start();
            t.join();  // main thread sẽ chờ t kết thúc
            {% endraw %}

4. ExecutorService, Callable, Future

- ExecutorService

  - Cung cấp một pool các thread quản lý hiệu quả hơn.

            {% raw %}
            ExecutorService executor = Executors.newFixedThreadPool(3);
            executor.submit(() -> System.out.println("Task"));
            executor.shutdown();
            {% endraw %}

- Callable<V> & Future<V>

  - Khác với Runnable, Callable có thể trả về kết quả và ném exception.

            {% raw %}
            Callable<Integer> task = () -> 1 + 1;
            Future<Integer> future = executor.submit(task);
            Integer result = future.get(); // get() sẽ block nếu chưa có kết quả
            {% endraw %}

- Sự khác nhau giữa submit() và execute() trong Executor: submit() trả về Future, còn execute() thì không.

**XIII. Java 8+ Features**

1. Lambda Expression

- Là cách viết ngắn gọn của anonymous class implement một functional interface (interface chỉ có 1 method abstract duy nhất).
- Cú pháp:

            {% raw %}
            (parameters) -> expression
            hoặc:
            (parameters) -> { statements }
            {% endraw %}

- Ví dụ:

            {% raw %}
            // Thay vì:
            Runnable r = new Runnable() {
              public void run() {
                System.out.println("Hello");
              }
            };

            // Dùng Lambda:
            Runnable r = () -> System.out.println("Hello");
            {% endraw %}

- Ứng dụng:
  - Thường dùng với các API hỗ trợ functional (ví dụ List.forEach(), Stream.map()...)

2. Functional Interface (Function, Predicate, Consumer, Supplier)

- Là Interface chỉ có một phương thức trừu tượng. Có thể có default/static methods.
- Annotation hỗ trợ: @FunctionalInterface giúp compiler cảnh báo nếu bạn vi phạm định nghĩa functional interface.
- Các interface phổ biến:

         |------------------------------------------------------------|
         |  Interface     | Input | Output  | 	Mô tả                 |
         |------------------------------------------------------------|
         | Function<T, R> |   T   |   R     | Nhận T, trả về R        |
         | Predicate<T>   |   T   | boolean | Đánh giá đúng/sai với T |
         | Consumer<T>    |   T   |  void   | Nhận T, không trả về gì |
         | Supplier<T>    |  none |   T     | Không đầu vào, trả về T |
         |------------------------------------------------------------|

- Ví dụ:

            {% raw %}
            Predicate<String> isEmpty = s -> s.isEmpty();
            Function<String, Integer> lengthFunc = s -> s.length();
            Consumer<String> print = s -> System.out.println(s);
            Supplier<Double> random = () -> Math.random();
            {% endraw %}

3. Stream API

- Là API hỗ trợ xử lý dữ liệu theo hướng functional với collection, cung cấp pipeline các thao tác như map, filter, reduce.
- Các thao tác chính:
  - Intermediate: map, filter, sorted, distinct, limit, skip
  - Terminal: collect, forEach, reduce, count, anyMatch, allMatch, noneMatch
- Ví dụ:

            {% raw %}
            List<String> names = Arrays.asList("John", "Alice", "Bob");
            List<String> filtered = names.stream()
                             .filter(name -> name.startsWith("A"))
                             .map(String::toUpperCase)
                             .collect(Collectors.toList());
            {% endraw %}

- Ưu điểm:
  - Dễ đọc
  - Dễ xử lý song song: .parallelStream()
  - Code ngắn gọn, expressive

4. Optional

- Là Wrapper class giúp xử lý null an toàn, tránh NullPointerException.
- Cách tạo:

            {% raw %}
            Optional<String> name = Optional.of("Thanh");
            Optional<String> empty = Optional.empty();
            Optional<String> maybeNull = Optional.ofNullable(getName());
            {% endraw %}

- Một số method quan trọng:
  - isPresent(), ifPresent(Consumer)
  - orElse(T), orElseGet(Supplier)
  - map(Function), flatMap(Function)
  - filter(Predicate)
- Ví dụ:

            {% raw %}
            Optional<String> name = Optional.ofNullable(getName());
            String result = name.map(String::toUpperCase)
                                .orElse("Unknown");
            {% endraw %}

5. Method Reference, Constructor Reference

- Là viết gọn lại lambda expression khi đã có method hoặc constructor tương ứng.
- Cú pháp:

         |-----------------------------------------------------------------------------------------|
         |   Kiểu                          | Lambda                       | Method Reference       |
         |-----------------------------------------------------------------------------------------|
         | Static method                   | s -> MyClass.staticMethod(s) | MyClass::staticMethod  |
         | Instance method (có sẵn object) | x -> obj.method(x)           | obj::method            |
         | Instance method (trên class)    | (a, b) -> a.compareTo(b)     | String::compareTo      |
         | Constructor                     | () -> new MyClass()          | MyClass::new           |
         |-----------------------------------------------------------------------------------------|

- Ví dụ:

            {% raw %}
            List<String> names = Arrays.asList("a", "b", "c");
            names.forEach(System.out::println); // method reference

            Supplier<List<String>> listSupplier = ArrayList::new; // constructor reference
            {% endraw %}

**XIV. Annotation** _(TODO)_

1. Annotation cơ bản: @Override, @Deprecated, @SuppressWarnings

2. Annotation tùy chỉnh (Custom Annotation)

3. Meta-annotations: @Target, @Retention

**XV. Reflection** _(TODO)_

1. Lấy thông tin class: Class<?>

2. Truy cập method, field, constructor qua Reflection

3. Gọi method, tạo instance bằng Reflection

**XVI. Date & Time API** _(TODO)_

1. Date, Calendar (truyền thống)

2. Java 8: LocalDate, LocalTime, LocalDateTime

3. Period, Duration

4. DateTimeFormatter

**XVII. Lớp lồng nhau (Nested & Inner Classes)** _(TODO)_

1. Static Nested Class

2. Member Inner Class

3. Local Class

4. Anonymous Inner Class

**XVIII. Quản lý bộ nhớ (Memory Management)** _(TODO)_

1. Stack vs Heap

2. Garbage Collector

3. Strong / Weak / Soft / Phantom References

**XIX. Cơ chế hoạt động của JVM (JVM Internals)** _(TODO)_

1. Classloader

2. Memory Areas (Method Area, Heap, Stack, etc.)

3. Bytecode & Execution Engine

4. Garbage Collection Algorithms

**XX. Best Practices & Clean Code** _(TODO)_

1. Quy tắc đặt tên (Naming Conventions)

2. Immutability

3. Đọc hiểu code rõ ràng

4. Tối ưu performance

5. SOLID principles (nâng cao)

**------------------------------------------------------------ TO BE CONTINUED ----------------------------------------------------------**
