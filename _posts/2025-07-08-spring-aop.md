---
layout: post
title: "Tổng hợp kiến thức về Spring AOP (Aspect-Oriented Programming)"
date: 2025-07-08
---

1.  AOP là gì?

- AOP (Aspect-Oriented Programming) là lập trình hướng khía cạnh, giúp tách biệt logic phụ (cross-cutting concerns) như logging, transaction, bảo mật… ra khỏi logic chính của ứng dụng.
- Mục tiêu:

  - Làm code gọn hơn, dễ reuse
  - Tăng tính module hóa
  - Giảm trùng lặp code
  - **Ví dụ trước - sau dùng AOP**

    - Chưa dùng AOP:

      {% raw %}
      public void createOrder() {
      log.info("Start");
      // business logic
      log.info("End");
      }
      {% endraw %}

    - Dùng AOP:

      {% raw %}
      public void createOrder() {
      // chỉ business logic
      }
      {% endraw %}

      Logging được tách ra riêng bằng AOP → sạch hơn, dễ maintain hơn

2.  Các khái niệm: Aspect, JoinPoint, Pointcut, Advice, Weaving

        |--------------------------------------------------------------------------------------------------|
        | Khái niệm   | Mô tả                                                                              |
        |--------------------------------------------------------------------------------------------------|
        | Aspect      | Mô tả logic phụ tách ra (logging, security, transaction...)                        |
        | JoinPoint   | Điểm trong chương trình mà Aspect có thể can thiệp vào (VD: method được gọi)       |
        | Pointcut    | Điều kiện lọc để xác định JoinPoint nào được áp dụng (theo tên method, package...) |
        | Advice      | Hành động (code) thực sự được thực thi tại JoinPoint                               |
        | Weaving     | Quá trình kết hợp Aspect vào target object tại runtime/compile time                |
        | Proxy       | Spring tạo ra một đối tượng proxy bao quanh bean gốc để thực hiện AOP              |

3.  Các loại Advice: Before, After, Around, AfterReturning, AfterThrowing

        |-----------------------------------------------------------------------------------|
        | Loại Advice/Annotation | Khi nào được gọi                                         |
        |-----------------------------------------------------------------------------------|
        | @Before                | Trước khi method được gọi                                |
        | @After                 | Sau khi method kết thúc (dù thành công hay exception)    |
        | @AfterReturning        | Sau khi method trả về thành công                         |
        | @AfterThrowing         | Khi method ném ra exception                              |
        | @Around                | Bao quanh method (có thể chặn, sửa, thực thi trước/sau)  |

- Ví dụ: Logging Aspect

      {% raw %}
      @Aspect
      @Component
      public class LoggingAspect {

       @Before("execution(* com.example.service.*.*(..))")
       public void logBefore(JoinPoint joinPoint) {
         System.out.println("Start method: " + joinPoint.getSignature().getName());
       }

       @AfterReturning(pointcut = "execution(* com.example.service.*.*(..))", returning = "result")
       public void logAfter(Object result) {
         System.out.println("Method returned: " + result);
       }

      }
      {% endraw %}

4.  Ứng dụng AOP để làm gì: Logging, Transaction, Authorization...

            |------------------------------------------------------------------|
            | Ứng dụng            | Mô tả                                      |
            |------------------------------------------------------------------|
            | Logging             | Ghi log trước/ sau method                  |
            | Transaction         | Quản lý giao dịch tự động (@Transactional) |
            | Authorization       | Kiểm tra quyền trước khi thực hiện         |
            | Performance Monitor | Đo thời gian chạy của hàm                  |
            | Exception Handling  | Bắt và xử lý ngoại lệ toàn cục             |
            | Audit               | Theo dõi hành động người dùng              |

5.  Spring AOP hoạt động như thế nào?

    - Dùng Proxy pattern (JDK dynamic proxy hoặc CGLIB) để gói bean gốc lại
    - Khi method được gọi, proxy sẽ kiểm tra xem có Aspect nào áp dụng → nếu có thì thực hiện Advice tương ứng

**Tóm tắt**

    - Spring AOP cho phép tách logic phụ như logging, transaction ra khỏi logic chính nhờ khái niệm Aspect. Chúng ta thường dùng @Before, @After, @Around để log method, kiểm soát thời gian, hoặc validate quyền.
    - Các điểm chính trong AOP gồm:

         + Aspect: logic phụ
         + JoinPoint: điểm có thể can thiệp (thường là method)
         + Pointcut: định nghĩa nơi aspect được áp dụng
         + Advice: hành động khi aspect được thực thi
         + Weaving: quá trình gắn aspect vào chương trình
