---
layout: post
title: "Bài viết đầu tiên...Hướng dẫn tạo Blog trên GitHub"
date: 2025-06-28
tag: other
---

Đây là bài viết đầu tiên mình viết bằng GitHub Pages + Jekyll Minima. Rất đơn giản và thú vị!

**I. Cách viết blog trên GitHub (sử dụng GitHub Pages + Jekyll) như sau:**

✅ Bước 1: Tạo repository trên GitHub

1. Truy cập: https://github.com/new -> Tạo repository với format tên như sau : ten_tai_khoan.github.io
2. Ví dụ: Nếu tài khoản là NPNgocThanh99, tên repo là NPNgocThanh99.github.io
3. Đặt là Public
4. Check chọn “Initialize this repository with a README” -> Bấm “Create repository”

✅ Bước 2: Kích hoạt GitHub Pages

1. Vào repo bạn vừa tạo -> Click Settings > Tab Pages
2. Ở mục Source, chọn:
   - Branch: main
   - Folder: / (root)
3. Bấm Save
4. GitHub sẽ build trang blog tại: https://ten_tai_khoan.github.io ( trang blog của mình tại NPNgocThanh99.github.io)

✅ Bước 3: Cài giao diện blog với Jekyll (ví dụ: Minima)

1. Tạo file index.md với nội dung sau:

   ````markdown
   ```yaml
   ---
   layout: home
   title: My Blog
   ---
   ```
   ````

2. Tạo file \_config.yml với nội dung cấu hình:

   ````markdown
   ```yaml
   title: My Blog
   description: Welcome to my GitHub blog!
   theme: minima
   ```
   ````

3. Commit và push các file lên GitHub (push trên nhánh chính cho dễ và nhanh nhá hihi ^\_^ )

✅ Bước 4: Tạo bài viết mới

1. Tạo thư mục mới: \_posts
2. Tạo file bài viết với cú pháp: YYYY-MM-DD-ten-bai-viet.md
   Ví dụ: \_posts/2025-06-28-hello-github-blog.md
3. Nội dung bài viết mẫu:

   ````markdown
   ```yaml
   ---
   layout: post
   title: "Hello GitHub Blog"
   date: 2025-06-28
   ---
   Đây là bài viết đầu tiên của mình trên GitHub Pages!
   ```
   ````

✅ Bước 5: Push và xem blog

1. Commit & push tất cả file lên GitHub
2. Truy cập: https://ten_tai_khoan.github.io

🎨 Tuỳ chỉnh giao diện
Bạn có thể:

- Sử dụng các theme Jekyll có sẵn: https://jekyllthemes.io/free
- Clone một theme về và chỉnh trong \_config.yml
- Tuỳ chỉnh layout, css trong thư mục \_layouts, \_includes, assets

📦 Option: Tạo blog bằng template có sẵn
Bạn có thể fork template có sẵn như:

- chirpy
- minimal-mistakes  
   Sau đó vào Settings > Pages để kích hoạt GitHub Pages.  
  **II. Hướng dẫn sử dụng Markdown**

````
      |Cấu trúc        |Mục đích                                   |               Cú pháp               |
      |----------------|-------------------------------------------|-------------------------------------|
      | # Tiêu đề      | Tạo các cấp tiêu đề (H1–H6)               | # đến ######                        |
      | **in đậm**     | In đậm chữ                                | **chữ** hoặc __chữ__                |
      | *in nghiêng*   | In nghiêng chữ                            | *chữ* hoặc _chữ_                    |
      | - danh sách    | Tạo danh sách gạch đầu dòng               | -, *, +                             |
      | 1. danh sách   | Tạo danh sách có thứ tự                   | 1., 2....                           |
      | [liên kết](url)| Tạo hyperlink                             | [Google](https://google.com)        |
      | ![ảnh](link)   | Hiển thị hình ảnh                         | ![alt](url)                         |
      | `code`         | Inline code                               | Dùng dấu backtick                   |
      | ```code```     | Block code nhiều dòng                     | Dùng 3 dấu backtick                 |
      | sử dụng &lt;   | Hiển thị <                                | Less than – dấu "nhỏ hơn"           |
      | sử dụng &gt;   | Hiển thị >                                | Greater than – dấu "lớn hơn"        |
      | sử dụng &amp;  | Hiển thị &                                | Ampersand – dấu &, dùng trong URL   |
      | sử dụng &quot; | Hiển thị "                                | Double quote – dấu ngoặc kép        |
      | sử dụng &apos; | Hiển thị '                                | Single quote – dấu nháy đơn         |
````
