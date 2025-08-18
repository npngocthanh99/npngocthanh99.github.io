---
layout: post
title: "Tổng hợp kiến thức về Spring Security"
date: 2025-07-07
---

**II. Tổng quan về Spring security**

**1. Giới thiệu Spring Security**

- Spring Security là một framework của Spring cung cấp giải pháp toàn diện về Authentication (xác thực) và Authorization (phân quyền) cho các ứng dụng Java, đặc biệt là Spring Boot.

- Ngoài ra, nó còn hỗ trợ:

  - Bảo mật API với JWT, OAuth2.
  - Cấu hình linh hoạt qua Java Config hoặc Annotation.
  - Tích hợp dễ dàng với cơ sở dữ liệu, LDAP, SSO, v.v.

**2. Các khái niệm chính**

- Authentication (Xác thực):
  Kiểm tra danh tính của người dùng (username/password, token, SSO...).
  → Xác định bạn là ai.

- Authorization (Phân quyền):
  Xác định người dùng đã xác thực có quyền truy cập vào tài nguyên nào.
  → Xác định bạn được làm gì.

- Security Context & Authentication Object:
  Thông tin người dùng đã đăng nhập được lưu trong SecurityContextHolder.

- Filter Chain:
  Spring Security sử dụng chuỗi filter (DelegatingFilterProxy → FilterChainProxy) để xử lý request trước khi đến Controller.

**3. Luồng hoạt động cơ bản**

    1.  Người dùng gửi request (ví dụ login với username/password).
    2.Request đi qua Spring Security Filter Chain.
    3. Authentication Manager gọi đến Authentication Provider (VD: DaoAuthenticationProvider) để xác thực.
    4. Nếu thành công → tạo đối tượng Authentication lưu vào SecurityContext.
    5. Dựa trên role/authority, Spring Security quyết định cho phép hoặc từ chối request.

**4. Cách cấu hình trong Spring Boot**

- Spring Security Starter (spring-boot-starter-security) tự động thêm cơ chế bảo mật mặc định.
- Có thể cấu hình:

  - InMemoryUserDetailsManager (tài khoản hardcode).
  - JDBC/Custom UserDetailsService (lấy user từ DB).
  - JWT/OAuth2 cho REST API.

- Sử dụng annotation:

  - @EnableWebSecurity bật cấu hình bảo mật.
  - @PreAuthorize, @Secured kiểm soát truy cập ở mức method.

**5. Ưu điểm & điểm mạnh**

- Tích hợp chặt chẽ với Spring ecosystem.
- Linh hoạt, có thể thay thế hoặc mở rộng các cơ chế mặc định.
- Hỗ trợ JWT, OAuth2, SSO hiện đại.
- Có sẵn nhiều filter bảo mật (CSRF, CORS, Session Fixation, ...).

**6. Một số tình huống thực tế**

- Trong dự án xây dựng API, mình thường kết hợp Spring Security + JWT:

  - Khi login thành công, trả về token JWT.
  - Các request sau đó client gửi kèm token trong Header.
  - Spring Security viết custom filter để validate token, parse user info → set vào SecurityContext.

- Với hệ thống nội bộ, có thể dùng Role-based access control hoặc Permission-based access control thông qua annotation.

**II. Chi tiết về Spring Security**

1. Authentication vs Authorization
2. Filter Chain
3. Basic Auth, JWT, OAuth2
4. Cấu hình WebSecurityConfigurerAdapter (trước Spring Security 6)
5. @EnableWebSecurity, @PreAuthorize, @Secured
6. CSRF, CORS, Session Management
