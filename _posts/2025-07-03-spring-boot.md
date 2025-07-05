---
layout: post
title: "Tổng hợp kiến thức về Spring Framework"
date: 2025-07-03
---

**I. Tổng quan về Spring Framework**

1. Spring là gì? Tại sao lại dùng Spring?

   - Spring Framework là một framework mã nguồn mở dành cho phát triển ứng dụng java, đặc biệt trong môi trường Java Enterprise(JEE). Nó cung cấp một nền tảng linh hoạt, nhẹ, dễ test để xây dựng các ứng dụng phức tạp và có khả năng mở rộng cao.
     Đặc điểm nổi bật:

     - Inversion of Control(IoC): tách biệt việc khởi tạo & quản lý đối tượng ra khỏi logic nghiệp vụ.
     - Dependency Injection (DI): giảm phụ thuộc giữa các class, dễ test, dễ maintain.
     - Modular: chia thành nhiều module, sử dụng phần nào thì nhúng phần đó.
     - Hỗ trợ AOP: dễ dàng xử lý các logic cross-cutting như logging, transaction,....

Lý do sử dụng Spring:

        |---------------------------------------------------------------------------------------------------------|
        | Lý do                                   | Mô tả                                                         |
        |---------------------------------------------------------------------------------------------------------|
        | Tái sử dụng code & test dễ hơn          | Nhờ Dependency Injection và cấu trúc rõ ràng                  |
        | Tách biệt concern rõ ràng               | Bằng cách sử dụng AOP, tách logic nghiệp vụ với logic phụ trợ |
        | Tích hợp dễ dàng với các công nghệ khác | JDBC, Hibernate, JPA, JMS, Kafka, RabbitMQ...                 |
        | Hỗ trợ mạnh mẽ cho Web/MVC/API          | Spring MVC, RESTful API                                       |
        | Tăng tốc phát triển với Spring Boot     | Giảm cấu hình, hỗ trợ tự động                                 |

2.  Các module chính: Spring Core, Spring Context, Spring AOP, Spring Data, Spring MVC, Spring Boot, Spring Security...

        |---------------------------------------------------------------------------------------|
        | Module               | Mô tả                                                          |
        |---------------------------------------------------------------------------------------|
        | Spring Core          | Cung cấp nền tảng IoC, DI – là phần lõi bắt buộc               |
        | Spring Context       | Mở rộng Spring Core, hỗ trợ ApplicationContext                 |
        | Spring AOP           | Hỗ trợ lập trình hướng khía cạnh, giúp tách biệt logic phụ trợ |
        | Spring Data          | Tầng dữ liệu: hỗ trợ JPA, JDBC, MongoDB, Redis…                |
        | Spring MVC           | Hỗ trợ Web app, RESTful API theo kiến trúc MVC                 |
        | Spring Boot          | Tự động cấu hình, nhanh chóng tạo project Spring               |
        | Spring Security      | Bảo mật (xác thực, phân quyền), JWT, OAuth2                    |
        | Spring Test          | Hỗ trợ viết unit test, integration test                        |

3.  Sự khác biệt giữa Spring Framework và Spring Boot

        |-------------------------------------------------------------------------------------------------------------------|
        | Tiêu chí      | Spring Framework                              | Spring Boot                                       |
        |-------------------------------------------------------------------------------------------------------------------|
        | Cấu hình      | Cần cấu hình thủ công (XML, Java Config)      | Tự động cấu hình dựa trên classpath và cấu trúc   |
        | Tạo project   | Mất thời gian tạo & cấu hình                  | Dễ dàng tạo bằng Spring Initializr                |
        | Testing       | Cần setup nhiều                               | Hỗ trợ test tốt qua starter                       |
        | Phụ thuộc     | Phải tự khai báo từng dependency              | Cung cấp bộ starter chuẩn                         |
        | Web server    | Cần cấu hình servlet container                | Embedded Tomcat/Jetty sẵn                         |
        | Mục tiêu      | Dùng cho ứng dụng truyền thống, cấu hình tay  | Tăng tốc ứng dụng hiện đại, minimal config        |
        | Triển khai    | WAR, EAR                                      | WAR hoặc standalone JAR                           |

**Kết luận:** Spring Boot là phần mở rộng của Spring Framework giúp đơn giản hóa và tăng tốc phát triển ứng dụng Spring. Chúng ta vẫn đang dùng Spring (Core, MVC, Data...) nhưng được hỗ trợ thêm auto-configuration, starter, embedded server, devtools, v.v...

**II. Spring Core**

1.  IOC Container (Inversion of Control): Bean, BeanFactory, ApplicationContext

    - Inversion of Control (IoC) là nguyên lý mà control tạo & quản lý đối tượng được chuyển từ lập trình viên sang container (Spring quản lý).

    **Các thành phần chính:**

        |----------------------------------------------------------------------------------------------------------------------------|
        | Thành phần         | Mô tả                                                                                                 |
        |----------------------------------------------------------------------------------------------------------------------------|
        | Bean               | Đối tượng được Spring quản lý trong container                                                         |
        | BeanFactory        | Interface cung cấp cơ chế IoC, quản lý các bean (ít dùng trực tiếp)                                   |
        | ApplicationContext | Mở rộng BeanFactory, hỗ trợ nhiều tính năng hơn (i18n, event, AOP, lifecycle hooks...) => thường dùng |

    Ví dụ:

            {% raw %}
            ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
            MyService service = context.getBean(MyService.class);
            {% endraw %}

2.  Dependency Injection (DI): Constructor injection, Setter injection, Field injection

    - Spring inject dependencies (các bean khác) vào object khi khởi tạo – thay vì ta phải tự tạo thủ công bằng new.
    - Các cách inject:

                      |-------------------------------------------------------------------------------------------------------------------|
                      | Cách                  | Mô tả                       | Ưu/nhược điểm                                               |
                      | ----------------------|-----------------------------| ------------------------------------------------------------|
                      | Constructor Injection | Inject qua constructor      | Immutable, test dễ, dùng khi cần dependency bắt buộc        |
                      | Setter Injection      | Inject qua setter method    | Linh hoạt, dễ thay đổi, dễ tạo object không đủ dependency   |
                      | Field Injection       | Inject trực tiếp vào field  | Không nên dùng nhiều, khó test, nhưng tiện                  |

    - Ví dụ Constructor injection:

                        {% raw %}
                        @Component
                        public class OrderService {
                          private final CustomerRepo repo;

                          @Autowired
                          public OrderService(CustomerRepo repo) {
                            this.repo = repo;
                          }
                        }
                        {% endraw %}

    - Ví dụ Setter Injection:

                        {% raw %}
                        @Component
                        public class OrderService {

                          private CustomerRepository customerRepository;

                          @Autowired
                          public void setCustomerRepository(CustomerRepository customerRepository) {
                            this.customerRepository = customerRepository;
                          }

                          public void processOrder() {
                            customerRepository.save(); // sử dụng dependency
                          }
                        }

                        @Repository
                        public class CustomerRepository {

                          public void save() {
                            System.out.println("Customer saved.");
                          }
                        }
                        {% endraw %}

    - Ví dụ Field Injection:

                        {% raw %}
                        @Component
                        public class OrderService {

                          @Autowired
                          private CustomerRepository customerRepository;

                          public void processOrder() {
                            customerRepository.save();
                          }
                        }
                        {% endraw %}

3.  Bean Scope: Singleton, Prototype, Request, Session...

                      |-----------------------------------------------------------------------------------------|
                      | Scope               | Mô tả                                  | Áp dụng                  |
                      | --------------------|----------------------------------------|--------------------------|
                      | singleton (default) | Mỗi bean chỉ có 1 instance duy nhất    | Stateless services       |
                      | prototype           | Mỗi lần gọi getBean() tạo 1 object mới | Stateful, custom scope   |
                      | request             | Mỗi HTTP request sẽ có bean riêng      | Spring Web               |
                      | session             | Bean tồn tại trong session người dùng  | Spring Web               |
                      | application         | Tồn tại trong ServletContext           | Web application          |
                      | websocket           | Bean sống trong WebSocket session      | Realtime apps            |

Ví dụ:

                        {% raw %}
                        @Component
                        @Scope("prototype")
                        public class SomeBean { }
                        {% endraw %}

4.  Bean Lifecycle: init-method, destroy-method, @PostConstruct, @PreDestroy

    - Bean Lifecycle là chuỗi các bước mà một Spring Bean trải qua — từ lúc được tạo ra trong container cho đến khi bị huỷ.
    - Quy trình vòng đời Bean cơ bản:

      1. Bean được tạo (bằng constructor)
      2. Dependency được inject (DI)
      3. Các hook được gọi: @PostConstruct hoặc init-method
      4. Bean sẵn sàng được sử dụng
      5. Khi Spring container shutdown: @PreDestroy hoặc destroy-method được gọi

5.  Annotation vs XML vs Java-based configuration

                                  |---------------------------------------------------------------------------------------------------|
                                  | Loại cấu hình    | Cách làm                                      | Dùng khi nào                   |
                                  | -----------------|-----------------------------------------------|--------------------------------|
                                  | Annotation-based | Dùng các annotation như @Component, @Service, | Phổ biến nhất hiện nay         |
                                  |                  | @Configuration, @Bean, @Autowired...          |                                |
                                  | XML-based        | Cấu hình trong file applicationContext.xml,   | Cũ, dùng khi không thể dùng    |
                                  |                  | khai báo <bean>...                            | annotation                     |
                                  | Java-based       | Dùng class @Configuration và method @Bean     | Rõ ràng, mạnh mẽ, dễ kiểm soát |
                                  |                  |                                               |                                |

    a. Annotation-based Configuration

    - Đặc điểm: Rút gọn code, Dễ đọc, dễ quản lý, Không cần XML
    - Ví dụ:

                                {% raw %}
                                @Component
                                public class MyService {
                                  public void doSomething() { }
                                }

                                @Service
                                public class OrderService {
                                  private final MyService myService;

                                  @Autowired
                                  public OrderService(MyService myService) {
                                    this.myService = myService;
                                  }
                                }
                                {% endraw %}

    b. XML-based Configuration (Cũ)

    - Đặc điểm: Không phụ thuộc annotation, Tách riêng phần config khỏi code - Nhược điểm: Dài dòng, khó maintain, Không hỗ trợ refactoring tốt.
    - Ví dụ:

                          {% raw %}
                          <beans>
                            <bean id="myService" class="com.example.MyService" />
                            <bean id="orderService" class="com.example.OrderService">
                              <constructor-arg ref="myService" />
                            </bean>
                          </beans>
                          {% endraw %}

    c. Java-based Configuration (@Configuration + @Bean)

    - Đặc điểm: Viết cấu hình bằng Java thuần, Không cần annotation ở class, Rất mạnh khi cấu hình phức tạp, conditional logic
    - Ví dụ:

                          {% raw %}
                          @Configuration
                          public class AppConfig {

                            @Bean
                            public MyService myService() {
                              return new MyService();
                            }

                            @Bean
                            public OrderService orderService() {
                              return new OrderService(myService());
                            }
                          }
                          {% endraw %}

6.  @Component, @Service, @Repository, @Controller, @Configuration, @Bean, @Autowired, @Qualifier
    a. @Component

    - Là annotation gốc để Spring biết rằng class này là một Bean cần quản lý trong IoC Container.
    - Các annotation như @Service, @Repository, @Controller đều là biến thể (specialization) của @Component.
    - Ví dụ:

                            {% raw %}
                            @Component
                            public class EmailSender {
                              public void send(String message) { }
                            }
                            {% endraw %}

    b. @Service

    - Annotation dành riêng cho tầng service – logic nghiệp vụ.
    - Giúp code rõ ràng hơn về mặt kiến trúc (phân tầng).
    - Về bản chất, giống @Component.
    - Ví dụ:

                            {% raw %}
                            @Service
                            public class OrderService {
                              public void processOrder() { }
                            }
                            {% endraw %}

    c. @Repository

    - Annotation cho DAO layer (Data Access Layer)
    - Giống @Component, nhưng có thêm xử lý ngoại lệ tự động:
      | Chuyển đổi JDBC exceptions thành Spring DataAccessException.
    - Ví dụ:

                            {% raw %}
                            @Repository
                            public class UserRepository {
                              public void save(User u) { }
                            }
                            {% endraw %}

    d. @Controller

    - Dùng cho Spring MVC Controller, xử lý request HTTP.
    - Trả về View (HTML) nếu không kết hợp với @ResponseBody
    - Ví dụ:

                            {% raw %}
                            @Controller
                            public class HomeController {
                              @GetMapping("/")
                              public String home() {
                                return "index"; // trả về view name
                              }
                            }
                            {% endraw %}

    e. @Configuration

    - Dùng để đánh dấu class Java config, nơi bạn khai báo các @Bean.
    - Tương đương với file applicationContext.xml trong cấu hình XML.
    - Ví dụ:

                            {% raw %}
                            @Configuration
                            public class AppConfig {
                              @Bean
                              public EmailSender emailSender() {
                                return new EmailSender();
                              }
                            }
                            {% endraw %}

    f. @Bean

    - Dùng trong class @Configuration để khai báo một bean thủ công (không dùng @Component).
    - Hữu ích khi cần khởi tạo bean từ class không thể sửa, hoặc có logic tạo phức tạp.
    - Ví dụ:

                            {% raw %}
                            @Bean
                            public DataSource dataSource() {
                              return new HikariDataSource();
                            }
                            {% endraw %}

    g. @Autowired

    - Annotation dùng để inject dependency tự động theo kiểu (by type).
    - Có thể dùng cho:

      - Constructor (khuyến khích)
      - Field
      - Setter
      - Ví dụ:

                            {% raw %}
                            @Service
                            public class NotificationService {
                              private final EmailSender emailSender;

                              @Autowired
                              public NotificationService(EmailSender emailSender) {
                                this.emailSender = emailSender;
                              }
                            }
                            {% endraw %}

    h. @Qualifier

    - Dùng để chỉ định rõ bean nào sẽ được inject, khi có nhiều bean cùng type.
    - Kết hợp với @Autowired.
    - Ví dụ:

                            {% raw %}
                            @Autowired
                            @Qualifier("smsSender")
                            private MessageSender sender;
                            {% endraw %}

                            {% raw %}
                            @Component("smsSender")
                            public class SmsSender implements MessageSender { }

                            @Component("emailSender")
                            public class EmailSender implements MessageSender { }
                            {% endraw %}

**Tổng quan mối quan hệ giữa các annotation**

                            {% raw %}
                            @Component     ←  Gốc chung
                              ├── @Service        →    Service Layer
                              ├── @Repository     →    DAO Layer, bắt exception
                              └── @Controller     →    Web Layer

                            @Configuration → class khai báo Bean thủ công
                            @Bean → method tạo Bean trong class @Configuration

                            @Autowired → Inject dependency
                            @Qualifier → Chọn đúng bean nếu có nhiều
                            {% endraw %}

**III. Spring AOP (Aspect-Oriented Programming)**

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

**IV. Spring Data JPA / Spring JDBC**

1.  ORM là gì?

    - ORM (Object Relational Mapping) là kỹ thuật ánh xạ giữa object trong Java và bảng trong CSDL.

      - Mỗi class Java ↔ một bảng trong DB
      - Mỗi field ↔ một cột
      - Mỗi instance ↔ một dòng dữ liệu

    Mục đích: giúp truy vấn DB bằng Java object, không cần viết SQL thủ công nhiều.

2.  Spring Data JPA với JpaRepository, CrudRepository, PagingAndSortingRepository

    a. Spring Data JPA là gì?

    - Spring Data JPA là một abstraction trên JPA giúp tự động sinh code truy vấn CRUD.
    - Nó tích hợp với JPA Provider như Hibernate.

    b. Các interface chính trong Spring Data JPA

            |-------------------------------------------------------------------------------------------------------------|
            | Interface                         | Chức năng                                                               |
            |-------------------------------------------------------------------------------------------------------------|
            | CrudRepository<T, ID>             | Cung cấp các hàm CRUD cơ bản (save, findById, delete...)                |
            | PagingAndSortingRepository<T, ID> | Thêm hỗ trợ phân trang & sắp xếp                                        |
            | JpaRepository<T, ID>              | Kế thừa tất cả trên + nhiều tính năng mở rộng như batch, flush, khóa... |

    - Ví dụ:

            {% raw %}
             public interface UserRepository extends JpaRepository<User, Long> {
               List<User> findByName(String name);
             }
            {% endraw %}

3.  Viết custom query bằng JPQL, native SQL, hoặc @Query

    a. Query Method:

           {% raw %}
            List<User> findByEmailAndStatus(String email, String status);
           {% endraw %}

    b. JPQL - Java Persistence Query Language(@Query):

           {% raw %}
            @Query("SELECT u FROM User u WHERE u.email = :email")
            User findByEmail(@Param("email") String email);
           {% endraw %}

    c. JPQL (@Query):

           {% raw %}
            @Query(value = "SELECT * FROM users WHERE email = ?1", nativeQuery = true)
            User findByEmailNative(String email);
           {% endraw %}

4.  Transaction management với @Transactional

    - Giúp đảm bảo thao tác DB là toàn vẹn (ACID).
    - Nếu có lỗi xảy ra, sẽ rollback toàn bộ.
    - Ví dụ:

           {% raw %}
            @Transactional
            public void transferMoney() {
              withdraw();
              deposit();
            }
           {% endraw %}

    - Mặc định @Transactional chỉ áp dụng trên public method.
    - Có thể cấu hình rollback, propagation, isolation...

5.  Entity Lifecycle (Persist, Merge, Remove, Detach)

            |---------------------------------------------------------------------------|
            | Trạng thái           | Mô tả                                              |
            |---------------------------------------------------------------------------|
            | New (Transient)      | Entity mới tạo, chưa được persist                  |
            | Managed (Persistent) | Entity được quản lý bởi EntityManager              |
            | Detached             | Entity đã từng persist nhưng giờ không còn quản lý |
            | Removed              | Entity sẽ bị xoá khỏi DB                           |

    - Các method liên quan:
      - persist(entity) – thêm mới
      - merge(entity) – cập nhật
      - remove(entity) – xoá
      - detach(entity) – tách khỏi context

6.  Cách tạo các mối quan hệ: OneToOne, OneToMany, ManyToOne, ManyToMany

                    |-------------------------------------------------------------------------------|
                    | Annotation   | Mối quan hệ | Ghi chú                                          |
                    |-------------------------------------------------------------------------------|
                    | @OneToOne    |  1 - 1      | Một đối tượng liên kết với đúng 1 đối tượng khác |
                    | @OneToMany   |  1 - N      | Một đối tượng có nhiều đối tượng con             |
                    | @ManyToOne   |  N - 1      | N đối tượng con trỏ về cùng 1 đối tượng cha      |
                    | @ManyToMany  |  N - N      | N đối tượng liên kết với N đối tượng khác        |

    a. Ví dụ @OneToOne – Một-một (Một User có một Profile):

                   {% raw %}
                    @Entity
                    public class User {
                      @Id @GeneratedValue
                      private Long id;
                      private String username;

                      @OneToOne(mappedBy = "user", cascade = CascadeType.ALL)
                      private Profile profile;
                    }

                    @Entity
                    public class Profile {
                      @Id @GeneratedValue
                      private Long id;
                      private String bio;

                      @OneToOne
                      @JoinColumn(name = "user_id")
                      private User user;
                    }
                   {% endraw %}

    - Giải thích:
      - @OneToOne(mappedBy = "user"): quan hệ được điều khiển bởi Profile
      - @JoinColumn(name = "user_id"): khoá ngoại

    b. Ví dụ @OneToMany - Một-Nhiều (Một Customer có nhiều Order) và @ManyToOne - Nhiều-Một (Nhiều Order có chung một Customer)

                   {% raw %}
                    @Entity
                    public class Customer {
                      @Id @GeneratedValue
                      private Long id;
                      private String name;

                      @OneToMany(mappedBy = "customer", cascade = CascadeType.ALL)
                      private List<Order> orders = new ArrayList<>();
                    }

                    @Entity
                    public class Order {
                      @Id @GeneratedValue
                      private Long id;
                      private String orderCode;

                      @ManyToOne
                      @JoinColumn(name = "customer_id")
                      private Customer customer;
                    }
                   {% endraw %}

    - Giải thích:
      - Order là bên sở hữu quan hệ, chứa @JoinColumn
      - Customer là bên không sở hữu, dùng mappedBy = "customer"
    - Thêm đơn hàng:

                  {% raw %}
                   Customer c = new Customer();
                   Order o1 = new Order(); o1.setCustomer(c);
                   Order o2 = new Order(); o2.setCustomer(c);
                   c.setOrders(List.of(o1, o2));
                   customerRepository.save(c); // cascade ALL nên tự lưu luôn orders
                  {% endraw %}

    c. Ví dụ @ManyToMany – Nhiều-nhiều (Student học nhiều Course, Course có nhiều Student)

                  {% raw %}
                  @Entity
                  public class Student {
                    @Id @GeneratedValue
                    private Long id;
                    private String name;

                    @ManyToMany
                    @JoinTable(name = "student_course",
                      joinColumns = @JoinColumn(name = "student_id"),
                      inverseJoinColumns = @JoinColumn(name = "course_id"))
                    private Set<Course> courses = new HashSet<>();
                  }

                  @Entity
                  public class Course {
                    @Id @GeneratedValue
                    private Long id;
                    private String title;

                    @ManyToMany(mappedBy = "courses")
                    private Set<Student> students = new HashSet<>();
                  }
                  {% endraw %}

    - Giải thích:

      - @JoinTable tạo bảng trung gian student_course
      - mappedBy = "courses" để định nghĩa quan hệ 2 chiều

    - Gán khóa học cho sinh viên:

                  {% raw %}
                  Student s = new Student();
                  Course c1 = new Course(); c1.setTitle("Java");
                  Course c2 = new Course(); c2.setTitle("Spring");

                  s.getCourses().addAll(List.of(c1, c2));
                  c1.getStudents().add(s);
                  c2.getStudents().add(s);
                  studentRepository.save(s); // sẽ lưu tất cả do cascade
                  {% endraw %}

7.  Lazy vs Eager Loading

            |----------------------------------------------------------------------------------------------------|
            | Kiểu   | Mô tả                                  | Ưu/nhược                                         |
            |----------------------------------------------------------------------------------------------------|
            | LAZY   | Chỉ load khi cần (lazy initialization) | Tốt hơn về hiệu năng nếu không cần dữ liệu ngay  |
            | EAGER  | Load luôn khi entity được lấy          | Gây N+1 query, giảm performance                  |

    - Ví dụ:

           {% raw %}
           @OneToMany(fetch = FetchType.LAZY)
           private List<Order> orders;
           {% endraw %}

**V. Spring MVC (Web Layer)**

1. Kiến trúc MVC
2. @Controller, @RestController, @RequestMapping, @GetMapping, @PostMapping, @PathVariable, @RequestParam, @RequestBody, @ResponseBody
3. Binding dữ liệu: DTO, Form object
4. Exception handling: @ControllerAdvice, @ExceptionHandler
5. Validations: @Valid, @Validated, Bean Validation API (JSR-303)

**VI. Spring Boot**

1. Spring Boot là gì? Ưu điểm?
2. application.properties vs application.yml
3. Cấu hình tự động (Auto Configuration)
4. Spring Boot Starter
5. Cấu trúc chuẩn một ứng dụng Spring Boot
6. DevTools, Actuator, Profiles
7. Embedded Tomcat, cấu hình port, hot reload

**VII. Spring Security**

1. Authentication vs Authorization
2. Filter Chain
3. Basic Auth, JWT, OAuth2
4. Cấu hình WebSecurityConfigurerAdapter (trước Spring Security 6)
5. @EnableWebSecurity, @PreAuthorize, @Secured
6. CSRF, CORS, Session Management

**VIII. Spring Test**

1. Viết unit test với @SpringBootTest, @WebMvcTest, @DataJpaTest
2. MockBean, TestRestTemplate, MockMvc
3. Test controller, service, repository

**IX. Các chủ đề nâng cao (phỏng vấn trung - cao cấp)**

1. Event trong Spring (ApplicationEventPublisher, @EventListener)
2. Spring Retry, Spring Batch, Spring WebFlux (Reactive Programming)
3. Tích hợp Spring với:
4. Redis, RabbitMQ, Kafka
5. Elasticsearch, MongoDB
6. Caching: @Cacheable, @CachePut, @CacheEvict
7. Custom annotation
8. Multi-module Spring Boot project

**X. Các kiến thức liên quan khác (rất quan trọng)**

1. Kiến trúc RESTful API
2. Exception Handling toàn cục
3. DTO vs Entity
4. Swagger/OpenAPI
5. Build tool: Maven, Gradle
6. Docker hóa ứng dụng Spring Boot
7. Triển khai Spring Boot lên server/cloud
