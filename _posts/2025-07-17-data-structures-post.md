---
layout: post
title: "Ôn tập kiến thức về Cấu trúc dữ liệu"
date: 2025-07-17
---

**I. Cấu trúc Dữ liệu là gì?**

- Cấu trúc dữ liệu là cách tổ chức, lưu trữ và quản lý dữ liệu để có thể truy xuất và xử lý hiệu quả.
- Là nền tảng cho thuật toán hoạt động hiệu quả về thời gian (time) và bộ nhớ (space).

**II. Phân loại chính**

        |-------------------------------------------|------------------------------------------|
        | Nhóm                    | Loại            | Đặc điểm                                 |
        |-------------------------------------------|------------------------------------------|
        | Tuyến tính (Linear)     | Array (mảng)    | Truy cập chỉ số, lưu trữ cố định         |
        |                         | Linked List     | Danh sách liên kết các node              |
        |                         | Stack           | LIFO – Last In First Out                 |
        |                         | Queue           | FIFO – First In First Out                |
        | Phi tuyến (Non-linear)  | Tree            | Cấu trúc phân cấp gồm node cha – con     |
        |                         | Graph           | Mô hình đỉnh và cạnh                     |
        | Cấu trúc khác           | Hash Table      | Bảng băm, ánh xạ key → value             |

**III. Phân tích từng cấu trúc**

1.  Array (Mảng)
    a. Khái niệm

    - Array (mảng) là một cấu trúc dữ liệu tuyến tính, lưu trữ tập hợp các phần tử cùng kiểu dữ liệu, đặt cạnh nhau trong bộ nhớ.
    - Các phần tử trong mảng được truy cập thông qua chỉ số (index), thường bắt đầu từ 0.
    - Ví dụ:

      {% raw %}
      int[] arr = {10, 20, 30, 40, 50};
      System.out.println(arr[2]); // Kết quả: 30
      {% endraw %}

    b. Đặc điểm

    - Truy cập ngẫu nhiên (Random Access): Do các phần tử được lưu liền kề, nên việc truy cập phần tử theo index có độ phức tạp O(1).
    - Kích thước cố định: Một mảng tĩnh có kích thước không thể thay đổi sau khi khai báo (trừ khi dùng cấu trúc động như ArrayList trong Java hoặc vector trong C++).
    - Đồng nhất: Các phần tử trong mảng có cùng kiểu dữ liệu.

    c. Ưu điểm

    - Truy cập nhanh: Tìm phần tử theo chỉ số cực nhanh → O(1).
    - Đơn giản: Dễ khai báo, dễ sử dụng.
    - Tối ưu bộ nhớ cache: Do các phần tử lưu liền kề nên tận dụng CPU cache tốt.

    d. Nhược điểm

    - Kích thước cố định: Không thể thay đổi sau khi khai báo (trong ngôn ngữ như C, Java).
    - Chi phí chèn/xoá cao:
      - Xoá hoặc thêm 1 phần tử giữa mảng phải dịch chuyển các phần tử còn lại → O(n).
      - Thêm cuối mảng có thể nhanh (O(1)) nếu còn chỗ, nhưng nếu đầy thì phải cấp phát lại (trong mảng động).
    - Lãng phí bộ nhớ: Nếu khai báo kích thước lớn mà dùng ít → dư thừa.

    e. Các thao tác cơ bản và độ phức tạp

        |--------------------------------------------|
        | Thao tác                    | Độ phức tạp  |
        |--------------------------------------------|
        | Truy cập arr[i]             | O(1)         |
        | Cập nhật arr[i] = x         | O(1)         |
        | Tìm kiếm tuyến tính         | O(n)         |
        | Thêm/Xoá cuối (nếu còn chỗ) | O(1)         |
        | Thêm/Xoá giữa mảng          | O(n)         |

2.  Linked List

3.  Stack

4.  Queue

5.  Hash Table / HashMap

6.  Tree (Cây)

7.  Graph (Đồ thị)

**III. Các câu hỏi thường gặp trong phỏng vấn**

1. So sánh Array vs Linked List
2. So sánh Array vs ArrayList (Java)
