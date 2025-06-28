---
layout: post
title: "Bài viết đầu tiên...Hướng dẫn tạo Blog trên GitHub"
date: 2025-06-28
---

<h2>Đây là bài viết đầu tiên mình viết bằng GitHub Pages + Jekyll Minima. Rất đơn giản và thú vị!</h2><br />
<br />
<p>
Mình xin phép được hướng dẫn các bước để cách viết blog trên GitHub (sử dụng GitHub Pages + Jekyll) như sau: <br />
✅ Bước 1: Tạo repository trên GitHub  <br />
  1. Truy cập: https://github.com/new -> Tạo repository với format tên như sau : ten_tai_khoan.github.io<br />
  2. Ví dụ: Nếu tài khoản là npngocthanh99, tên repo là npngocthanh99.github.io<br />
  3. Đặt là Public<br />
  4. Check chọn “Initialize this repository with a README” -> Bấm “Create repository” <br />
✅ Bước 2: Kích hoạt GitHub Pages<br />
  1. Vào repo bạn vừa tạo -> Click Settings > Tab Pages<br />
  2. Ở mục Source, chọn:<br />
     - Branch: main <br />
     - Folder: / (root) <br />
  3. Bấm Save <br />
  4. GitHub sẽ build trang blog tại: https://ten_tai_khoan.github.io ( trang blog của mình tại npngocthanh99.github.io)<br />
✅ Bước 3: Cài giao diện blog với Jekyll (ví dụ: Minima)<br />
  1. Tạo file index.md với nội dung sau:<br />
<br />
     ---<br />
     layout: home<br />
     title: My Blog<br />
     ---<br />
     <br />
  2. Tạo file _config.yml với nội dung cấu hình:<br />
     <br />
     title: My Blog<br />
     description: Welcome to my GitHub blog!<br />
     theme: minima<br />
<br />
  3. Commit và push các file lên GitHub (push trên nhánh chính cho dễ và nhanh nhá hihi ^_^ )<br />
✅ Bước 4: Tạo bài viết mới<br />
  1. Tạo thư mục mới: _posts<br />
  2. Tạo file bài viết với cú pháp: YYYY-MM-DD-ten-bai-viet.md<br />
     Ví dụ: _posts/2025-06-28-hello-github-blog.md<br />
  3. Nội dung bài viết mẫu:<br />
<br />
     ---<br />
     layout: post<br />
     title: "Hello GitHub Blog"<br />
     date: 2025-06-28<br />
     ---<br />
Đây là bài viết đầu tiên của mình trên GitHub Pages!<br />
✅ Bước 5: Push và xem blog<br />
  1. Commit & push tất cả file lên GitHub<br />
  2. Truy cập: https://ten_tai_khoan.github.io<br />
🎨 Tuỳ chỉnh giao diện<br />
 Bạn có thể:<br />
   - Sử dụng các theme Jekyll có sẵn: https://jekyllthemes.io/free<br />
   - Clone một theme về và chỉnh trong _config.yml<br />
   - Tuỳ chỉnh layout, css trong thư mục _layouts, _includes, assets<br />
📦 Option: Tạo blog bằng template có sẵn<br />
 Bạn có thể fork template có sẵn như:<br />
   - chirpy<br />
   - minimal-mistakes<br />
 Sau đó vào Settings > Pages để kích hoạt GitHub Pages.<br />
</p>
