---
layout: post
title: "Tổng hợp kiến thức về Spring Framework"
date: 2025-07-01
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
4.  Bean Lifecycle: init-method, destroy-method, @PostConstruct, @PreDestroy
5.  Annotation vs XML vs Java-based configuration
6.  @Component, @Service, @Repository, @Controller, @Configuration, @Bean, @Autowired, @Qualifier

**III. Spring AOP (Aspect-Oriented Programming)**

1. AOP là gì?
2. Các khái niệm: Aspect, JoinPoint, Pointcut, Advice, Weaving
3. Các loại Advice: Before, After, Around, AfterReturning, AfterThrowing
4. Ứng dụng AOP để làm gì: Logging, Transaction, Authorization...

**IV. Spring Data JPA / Spring JDBC**

1. ORM là gì?
2. Spring Data JPA với JpaRepository, CrudRepository, PagingAndSortingRepository
3. Viết custom query bằng JPQL, native SQL, hoặc @Query
4. Transaction management với @Transactional
5. Entity Lifecycle (Persist, Merge, Remove, Detach)
6. Cách tạo các mối quan hệ: OneToOne, OneToMany, ManyToOne, ManyToMany
7. Lazy vs Eager Loading

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
