---
layout: post
title: "Kiến thức về Docker"
date: 2025-08-16
---

**I. Kiến thức cơ bản về Docker?**

**1. Docker là gì**

- Docker là một nền tảng để tạo, triển khai và chạy ứng dụng trong container.
- Container đóng gói ứng dụng và tất cả dependencies (thư viện, cấu hình) để chạy đồng nhất trên mọi môi trường.
- So với VM (Virtual Machine):

  - VM có OS riêng → nặng hơn.
  - Container dùng chung kernel → nhẹ, nhanh, khởi động nhanh hơn.

**2. Thành phần chính của Docker**

- Docker Engine: Nền tảng chạy container.
- Docker Image: File template dùng để tạo container. (VD: nginx:latest)
- Docker Container: Thực thể chạy từ image.
- Dockerfile: File mô tả cách build image.
- Docker Hub / Registry: Nơi lưu trữ image.
- Docker Compose: Tool để chạy nhiều container cùng lúc (multi-container).

**3. Nguyên tắc container**

- Immutable: Container không nên chỉnh sửa trực tiếp; nếu cần thay đổi → tạo image mới.
- Ephemeral: Container có thể bị xóa và tạo lại.
- Isolation: Container chạy độc lập về process, network, file system.

**II. Các lệnh Docker cơ bản**

1.  Quản lý image

        {% raw %}
        docker pull nginx:latest       # Tải image từ Docker Hub
        docker images                  # Liệt kê image đã có
        docker rmi <image_id>          # Xóa image
        docker build -t myapp:v1 .     # Build image từ Dockerfile
        {% endraw %}

2.  Quản lý container

        {% raw %}
        docker run -d --name mynginx -p 8080:80 nginx:latest   # Chạy container
        docker ps                    # Xem container đang chạy
        docker ps -a                 # Xem tất cả container
        docker stop mynginx          # Dừng container
        docker start mynginx         # Khởi động container đã dừng
        docker rm mynginx            # Xóa container
        docker logs mynginx          # Xem log container
        docker exec -it mynginx bash # Vào bash container
        {% endraw %}

3.  Docker Compose

- docker-compose.yml định nghĩa nhiều container, network, volume.

        {% raw %}
        version: "3"
        services:
          web:
            image: nginx:latest
            ports:
              - "8080:80"
          db:
            image: mysql:8
            environment:
              MYSQL_ROOT_PASSWORD: example
        {% endraw %}

- Lệnh thường dùng:

        {% raw %}
        docker-compose up -d    # Chạy tất cả service
        docker-compose down     # Dừng và xóa
        docker-compose logs -f  # Xem log
        {% endraw %}

**III. Docker trong thực tế**

1. Triển khai ứng dụng

- Backend Spring Boot, Node.js, Python:

  - Tạo Dockerfile.
  - Build image → push lên registry → deploy container.

- Frontend:

  - Docker dùng Nginx serve SPA.
  - Mount code vào container để dev nhanh.

b. Docker và môi trường

- Dev / Test / Prod:
  - Sử dụng cùng image → tránh lỗi "ở máy chạy được mà prod không chạy".
  - Docker Compose quản lý nhiều service.

c. Persistent Data

- Volume: dùng lưu dữ liệu, không bị mất khi container xóa.

        {% raw %}
        docker run -v /host/path:/container/path nginx
        {% endraw %}

d. Networking

- Docker tạo network riêng cho container.
- Container có thể ping nhau bằng tên service.

**IV. Best practices(Ưu điểm)**

- Image nhẹ → dùng alpine thay vì ubuntu nếu không cần.
- Dockerfile: build multi-stage để giảm size.
- Không lưu dữ liệu trong container → dùng volume.
- Quản lý environment: .env file hoặc docker-compose.override.yml.
- Chỉ expose port cần thiết.
- Container không nên chạy root user.
