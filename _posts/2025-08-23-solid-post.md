---
layout: post
title: "Kiến thức về nguyên tắc SOLID"
date: 2025-08-23
---

SOLID là viết tắt của 5 nguyên tắc thiết kế giúp code dễ đọc, dễ mở rộng, dễ bảo trì và hạn chế code smell(code xấu).

1. S – Single Responsibility Principle (SRP)

- Mỗi class chỉ nên chịu trách nhiệm về một việc duy nhất.
- Nếu một class có nhiều hơn một lý do để thay đổi → vi phạm SRP.

2. O – Open/Closed Principle (OCP)
3. L – Liskov Substitution Principle (LSP)
4. I – Interface Segregation Principle (ISP)
5. D – Dependency Inversion Principle (DIP)

**Tóm lại:**

- S: Mỗi class chỉ nên làm 1 việc.
- O: Mở rộng dễ dàng, không sửa code cũ.
- L: Lớp con phải thay thế được lớp cha.
- I: Interface nhỏ gọn, đúng mục đích.
- D: Phụ thuộc vào abstraction, không phụ thuộc implementation.
