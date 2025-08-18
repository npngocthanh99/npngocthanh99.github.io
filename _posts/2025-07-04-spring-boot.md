---
layout: post
title: "Tổng hợp kiến thức về Spring Framework"
date: 2025-07-04
---

1.  Spring Boot là gì? Ưu điểm?

    - Spring Boot là một framework giúp đơn giản hoá việc cấu hình và chạy ứng dụng Spring, bằng cách cung cấp:
      - cấu hình mặc định,
      - auto configuration,
      - embedded server (Tomcat/Jetty),
      - starter dependencies.
    - Mục tiêu:
      - Giúp bạn có thể "Just Run" ứng dụng Spring mà không cần cấu hình rườm rà.
    - Ưu điểm của Spring boot:

             |--------------------------------------------------------------------------------------------------|
             | Ưu điểm                               | Giải thích                                               |
             |--------------------------------------------------------------------------------------------------|
             | Tự động cấu hình (Auto Configuration) | Không cần cấu hình XML phức tạp                          |
             | Tích hợp server nội bộ                | Không cần cài Tomcat ngoài, chỉ cần main() là chạy       |
             | Starter dependencies                  | Gom nhóm dependency theo mục đích (web, jpa, security)   |
             | Đơn giản hóa cấu trúc dự án           | Tự sinh project theo mẫu chuẩn                           |
             | Hỗ trợ hot reload                     | Qua DevTools, không cần restart lại app                  |
             | Quản lý môi trường (Profiles)         | Cấu hình theo môi trường: dev, test, prod                |
             | Dễ triển khai (jar)                   | Gói app thành .jar có thể chạy bằng java -jar            |

2.  application.properties vs application.yml

             |-----------------------------------------------------------------------|
             | Thuộc tính            | application.properties | application.yml      |
             |-----------------------------------------------------------------------|
             | Cú pháp               | key=value              | YAML định dạng khối  |
             | Dễ đọc                | đơn giản               | cấu hình phức tạp    |
             | Hỗ trợ cấu trúc lồng  | khó                    | tốt hơn              |

    - Ví dụ cấu hình bằng application.properties:

                       {% raw %}
                       server.port=8081
                       spring.datasource.url=jdbc:mysql://localhost:3306/demo
                       {% endraw %}

    - Ví dụ cấu hình bằng application.properties:

                      {% raw %}
                      server:
                        port: 8081

                      spring:
                        datasource:
                          url: jdbc:mysql://localhost:3306/demo
                      {% endraw %}

          👉 YAML được dùng nhiều hơn trong microservice hoặc cấu hình nhiều profile.

3.  Cấu hình tự động (Auto Configuration)

    - Khi bạn thêm starter (VD: spring-boot-starter-web), Spring Boot sẽ tự động cấu hình các bean cần thiết, như DispatcherServlet, Jackson, v.v.
    - Tắt auto config cho một số class:

                      {% raw %}
                      @SpringBootApplication(exclude = {DataSourceAutoConfiguration.class})
                      {% endraw %}

4.  Spring Boot Starter

             |------------------------------------------------------------------|
             | Starter                          | Chức năng                     |
             |------------------------------------------------------------------|
             | spring-boot-starter-web          | REST API, Tomcat, Jackson     |
             | spring-boot-starter-data-jpa     | JPA + Hibernate               |
             | spring-boot-starter-security     | Spring Security               |
             | spring-boot-starter-validation   | Bean Validation               |
             | spring-boot-starter-test         | JUnit, Mockito, Spring Test   |

           👉 Không cần tự tìm từng thư viện, chỉ cần 1 dòng thêm starter.

5.  Cấu trúc chuẩn một ứng dụng Spring Boot

          {% raw %}
          src/
            └── main/
                  ├── java/
                  │    └── com/example/demo/
                  │        ├── DemoApplication.java            # File main, entry point -> hàm main() chạy ứng dụng
                  |
                  │        ├── config/                         # Cấu hình app (security, swagger, beans, CORS, Security...)
                  │        │   ├── WebSecurityConfig.java
                  │        │   └── SwaggerConfig.java
                  |
                  │        ├── controller/                     # Web/API layer - xử lý HTTP request
                  |
                  │        ├── service/                        # Business logic layer
                  |        |   ├── UserService.java
                  │        |   └── impl/                       # Implement của service (nếu có interface)
                  |        |        └── UserServiceImpl.java
                  |
                  │        ├── repository/                     # DAO layer - giao tiếp DB
                  |        |    └── UserRepository.java
                  |
                  │        └── model/                          # Chứa các class mô hình (Entity, DTO, Mapper)
                  |        |    ├── entity/                    # JPA Entity - ánh xạ bảng dữ liệu
                  |        |    |     └── User.java
                  |        |    ├── dto/                       # Data Transfer Object - nhận & trả dữ liệu
                  │        │    │    └── UserDto.java
                  |        |    └── mapper/                    # Converter hoặc MapStruct mapper
                  │        │         └── UserMapper.java
                  |
                  │        ├── exception/                      # Custom exceptions & global handler
                  │        │    ├── GlobalExceptionHandler.java
                  │        │    └── ResourceNotFoundException.java
                  |
                  |        ├── util/                           # Hàm tiện ích dùng chung
                  │        │    ├── DateUtil.java
                  │        │    ├── StringHelper.java
                  │        │    └── EnumUtils.java
                  |
                  |        ├── constant/                       # Các hằng số toàn cục
                  │        │    ├── AppConstants.java
                  │        │    └── MessageConstants.java
                  |
                  |        ├── enums/                          # Enum dùng toàn hệ thống
                  │        │    ├── UserStatus.java
                  │        │    └── CurrencyType.java
                  |
                  |        └── validator/                      # Custom annotation validator
                  │             ├── ValidPhoneNumber.java
                  │             ├── ValidPhoneNumberValidator.java
                  │             └── EnumValidator.java
                  |
                  └── resources/
                        ├── application.yml                    # Cấu hình chính
                        ├── application-dev.yml                # Cấu hình cho môi trường dev
                        ├── application-prod.yml               # Cấu hình cho môi trường production
                        └── static/                            # Assets tĩnh (nếu có)
          {% endraw %}

6.  DevTools, Actuator, Profiles

             |----------------------------------------------------------------------------------------------------|
             | Tính năng   | Mô tả                                                                                |
             |----------------------------------------------------------------------------------------------------|
             | DevTools    | Tự động reload khi thay đổi code                                                     |
             | Actuator    | Theo dõi health check, metrics, bean info (/actuator/health, /actuator/beans, v.v.)  |
             | Profiles    | Cấu hình đa môi trường: application-dev.yml, application-prod.yml                    |

    - Kích hoạt profile:

            {% raw %}
            # application.yml
            spring:
              profiles:
                active: dev
            {% endraw %}

7.  Embedded Tomcat, cấu hình port, hot reload

    - Spring Boot dùng Tomcat nhúng (Embedded) theo mặc định.
    - Có thể đổi sang Jetty, Undertow nếu cần.
    - Đổi port:

                {% raw %}
                server:
                  port: 8081
                {% endraw %}

    - Hot reload với DevTools:
      Thêm vào pom.xml:

              {% raw %}
              <dependency>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-devtools</artifactId>
                <optional>true</optional>
              </dependency>
              {% endraw %}

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
