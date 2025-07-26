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
         | Dùng trong môi trường | VBất kỳ   | Single-thread | Multi-thread    |
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

**VI. Các thành phần OOP nâng cao(Advanced OOP Concepts)** _(TODO)_

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
         | Quy tắc | VBất kỳ           | Tham số khác nhau (kiểu, số lượng, thứ tự)         | Phải giống hoàn toàn về tên, kiểu, thứ tự tham số   |
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
                        // System.out.println(outerValue); // ❌ Error: Cannot access non-static
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

**VII. Phạm vi truy cập(Access Modifiers)** _(TODO)_

1. Private

2. Default(package-private)

3. Protected

4. Public

5. Tóm tắt về khả năng truy cập

**VIII. Xử lý ngoại lệ(Exception Handlling)** _(TODO)_

1. Try - Catch - Finally

2. Throw và Throws

3. Checked vs Unchecked Exception

4. Tạo ngoại lệ tùy chỉnh(Custom Exception)

**IX. Collection Framework** _(TODO)_

1. Interfaces: List, Set, Map, Queue

2. Implementations: ArrayList, LinkedList, HashSet, TreeSet, HashMap, TreeMap

3. Iterator, ListIterator, for-each

4. So sánh HashMap vs Hashtable

**X. Generics** _(TODO)_

1. Generic Class, Method

2. Wildcards: ?, ? extends, ? super

3. Type Inference (Diamond operator)

**XI. Java I/O (Input/Output)** _(TODO)_

1. File, FileReader, FileWriter

2. BufferedReader, BufferedWriter

3. InputStream, OutputStream

4. Serialization / Deserialization

**XII. Đa luồng & Xử lý đồng thời (Multithreading and Concurrency)** _(TODO)_

1. Tạo Thread: Thread, Runnable

2. Lifecycle của Thread

3. synchronized, volatile, wait, notify, join

4. ExecutorService, Callable, Future

**XIII. Java 8+ Features** _(TODO)_

1. Lambda Expression

2. Functional Interface (Function, Predicate, Consumer, Supplier)

3. Stream API

4. Optional

5. Method Reference, Constructor Reference

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
