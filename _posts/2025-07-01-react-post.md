---
layout: post
title: "Tổng hợp kiến thức về ReactJS"
date: 2025-07-01
---

**I. Kiến thức cơ bản cần nắm vững trong ReactJS**

**1. JSX (JavaScript XML)**

JSX là một cú pháp mở rộng của JavaScript, cho phép chúng ta viết mã HTML bên trong JavaScript. JSX giúp chúng ta tạo ra React elements, từ đó render ra giao diện người dùng.

Ví dụ đơn giản:

        {% raw %}
           const element = <h1>Hello, React!</h1>;
        {% endraw %}

JSX không bắt buộc trong React, nhưng nó được sử dụng rất phổ biến vì:

- Gần giống HTML nên dễ đọc, dễ viết.
- Có thể kết hợp logic JavaScript vào giao diện.

a. Cách viết HTML trong JavaScript

- JSX trông giống HTML nhưng thực chất là JavaScript.
- Mỗi thẻ HTML được biên dịch thành React.createElement.
  Ví dụ:

         {% raw %}
           return <div className="greeting">Welcome to React!</div>;
         {% endraw %}

**Lưu ý khác biệt nhỏ với HTML:**

         |-----------------------|
         | HTML      | JSX       |
         |-----------------------|
         | class     | className |
         | for       | htmlFor   |
         | onclick   | onClick   |

b. Biểu thức trong JSX ({}) Dùng để nhúng logic

- Chúng ta có thể chèn bất kỳ biểu thức JavaScript hợp lệ nào vào JSX bằng dấu {}.
  Ví dụ:

             {% raw %}
               const name = "Thanh";
               return <h1>Hello, {name}!</h1>; // => Hello, Thanh!
             {% endraw %}

  Chúng ta có thể dùng {} để:

  - Hiển thị giá trị
  - Gọi hàm
  - Tính toán trong dòng

c. Điều kiện trong JSX: &&, ? : (ternary)

- && – Điều kiện đơn giản  
  Hiển thị một phần tử nếu điều kiện đúng.

             {% raw %}
               {isLoggedIn && <p>Welcome back!</p>}
             {% endraw %}

- ? : – Ternary operator  
  Hiển thị A nếu đúng, B nếu sai.

               {% raw %}
                 {isLoggedIn ? <p>Hi user!</p> : <p>Please login.</p>}
               {% endraw %}

- **Lưu ý: Không dùng if trực tiếp bên trong JSX. Thay vào đó, đặt logic if bên ngoài JSX hoặc dùng biểu thức như trên.**

d. Fragments (<></>) – Tránh thẻ cha dư thừa  
React yêu cầu mỗi component phải trả về một element duy nhất. Nếu bạn muốn trả về nhiều thẻ mà không tạo thêm <div>, hãy dùng Fragment.

Ví dụ:

             {% raw %}
                 return (
                   <>
                     <h1>Title</h1>
                     <p>Description</p>
                   </>
                 );
             {% endraw %}

e. key khi dùng .map() – Tránh lỗi và tối ưu render  
Khi render danh sách component bằng .map(), bạn phải thêm key duy nhất cho mỗi phần tử để React tối ưu hóa hiệu năng khi cập nhật UI.

Ví dụ:

             {% raw %}
                 const todos = ["Eat", "Sleep", "Code"];
                 return (
                   <ul>
                     {todos.map((item, index) => (
                       <li key={index}>{item}</li>
                     ))}
                   </ul>
                 );
             {% endraw %}

**Lưu ý:** key nên là giá trị duy nhất và ổn định, tránh dùng index nếu danh sách có thể thay đổi thứ tự.

**2. Component**

- Function component vs Class component (hiện nay dùng function là chủ yếu)
- Props và State
- Lifecycle (trong function dùng Hook như useEffect)
- Lifting state up (nâng state lên cha)

3. Hooks (Rất quan trọng)

- useState, useEffect
- useRef, useMemo, useCallback
- useContext, useReducer
- Custom Hooks

4. Event Handling

- Bắt sự kiện: onClick, onChange, onSubmit, ...
- Ngăn chặn mặc định (event.preventDefault())

5. Conditional Rendering

- if, &&, ternary, logical operators

6. List Rendering

- Dùng .map() để render list
- Sử dụng key đúng cách để tránh lỗi

7. Forms

- Controlled vs uncontrolled components
- Form validation cơ bản
- Thư viện hỗ trợ: react-hook-form, formik, yup

II. Kiến thức nâng cao

1. Routing – Điều hướng

- Thư viện react-router-dom
- Routes, Route, useNavigate, useParams

2. State Management (Quản lý trạng thái)

- Context API
- Redux Toolkit hoặc Zustand, Recoil
- Global state vs local state

3. Call API

- fetch, axios
- Dùng useEffect để gọi API
- Async/Await
- Error handling

4. Component Communication

- Cha → Con: props
- Con → Cha: callback props
- Con → Con: thông qua cha hoặc Context/Redux

5. Performance Optimization

- React.memo, useMemo, useCallback
- Lazy loading (React.lazy, Suspense)
- Split code, Virtualization (ví dụ: react-window)

6. Testing

- Unit test: Jest, React Testing Library
- E2E test: Cypress, Playwright

III. Các phần cần chú trọng để phát triển một dự án React

1. Cấu trúc thư mục rõ ràng

- components/, pages/, hooks/, services/, constants/, utils/, store/, ...
- Dễ maintain, scale

2. Quản lý state

- Dùng Context cho state nhỏ, Redux Toolkit cho state lớn
- Phân biệt rõ local và global state

3. Giao tiếp với Backend

- Tạo service layer dùng axios hoặc fetch
- Gắn token, handle lỗi, retry,...

4. Giao diện và UI/UX

- Dùng thư viện: Ant Design, Material UI, TailwindCSS
- Responsive, mobile-friendly
- Loading state, error state

5. Testing

- Test logic, component, flow chính

6. Dev Tools và Linter

- ESLint, Prettier
- Husky, lint-staged
- Git hook để kiểm tra code trước khi commit

7. Internationalization (i18n) nếu đa ngôn ngữ

- react-i18next hoặc tương đương

8. Bảo mật

- Không lộ API key
- Xử lý token an toàn
- Validate form đầu vào

9. Tối ưu hiệu năng

- Chia nhỏ component
- Giảm re-render
- Lazy load page/component không cần thiết ngay

10. Triển khai (Deployment)

- Build với vite hoặc webpack
- Deploy lên Netlify, Vercel, Firebase, Cloud (AWS, GCP, Azure)
