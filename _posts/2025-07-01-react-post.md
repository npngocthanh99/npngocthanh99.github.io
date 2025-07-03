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

**Bảng tổng kết phần 1**

         |----------------------------------------------------------------------|
         | Mục tiêu           | Nội dung                                        |
         |----------------------------------------------------------------------|
         | JSX là gì          | Cú pháp mở rộng giúp viết HTML trong JavaScript |
         | Biểu thức          | Dùng {} để nhúng biến, gọi hàm, logic           |
         | Điều kiện          | Dùng &&, ? : để render có điều kiện             |
         | Fragments          | Dùng <>...</> để tránh thẻ cha dư               |
         | Key trong .map()   | Dùng để React biết phần tử nào thay đổi         |

**2. Component**

- Component là đơn vị tái sử dụng giao diện nhỏ nhất trong React.
- Một ứng dụng React là tập hợp các component lồng nhau.
- Mỗi component giống như một “hàm JavaScript” nhưng trả về JSX thay vì giá trị.

a. Function component vs Class component (hiện nay dùng function là chủ yếu)

- Function Component (phổ biến hiện nay):  
  Là component viết bằng function, hỗ trợ đầy đủ tính năng thông qua Hooks (useState, useEffect,...).  
  Ví dụ:

               {% raw %}
                 function Welcome(props) {
                   return <h1>Hello, {props.name}</h1>;
                 }
               {% endraw %}

  Hoặc với arrow function:

               {% raw %}
                 const Welcome = ({ name }) => <h1>Hello, {name}</h1>;
               {% endraw %}

- Class Component (cũ hơn, ít dùng dần):
  Component viết bằng class, phải kế thừa từ React.Component.  
   Ví dụ:

                 {% raw %}
                   class Welcome extends React.Component {
                     render() {
                       return <h1>Hello, {this.props.name}</h1>;
                     }
                   }
                 {% endraw %}

  So sánh:

         |-------------------------------------------------------------------------------------------|
         | Tiêu chí             | Function Component         | Class Component                       |
         |-------------------------------------------------------------------------------------------|
         | Viết ngắn gọn        | ✅                         | ❌ dài dòng                          |
         | Sử dụng Hooks        | ✅ useState, useEffect,... | ❌ không hỗ trợ Hooks                |
         | Lifecycle            | ✅ Qua useEffect()         | ❌ Qua các hàm componentDidMount...  |
         | Khuyến nghị hiện nay | ✅ Chủ yếu dùng            | ❌ Không khuyến khích mới            |

b. Props và State

- Props (Properties)

  - Là dữ liệu truyền từ component cha xuống component con.
  - Là readonly – không được thay đổi trong component con.
  - Dùng để cấu hình/tuỳ biến component.
    Ví dụ:

                 {% raw %}
                   function Greeting(props) {
                     return <h1>Hello, {props.name}</h1>;
                   }

                   // Sử dụng
                   <Greeting name="Thanh" />
                 {% endraw %}

- State

  - Là dữ liệu nội bộ của component, có thể thay đổi trong vòng đời component.
  - Khi state thay đổi, component sẽ re-render lại.
    Dùng trong function component:

                 {% raw %}
                  import { useState } from 'react';

                  function Counter() {
                    const [count, setCount] = useState(0);
                    return <button onClick={() => setCount(count + 1)}>Clicked {count}</button>;
                  }
                 {% endraw %}

c. Lifecycle – Vòng đời Component

- Lifecycle là các giai đoạn trong "vòng đời" của component: tạo, cập nhật, huỷ.
- **Trong Function Component dùng useEffect() để thay thế lifecycle methods**

         |---------------------------------------------------------------------------|
         | Lifecycle (Class)           | Tương đương trong Function                  |
         |---------------------------------------------------------------------------|
         | componentDidMount()         | useEffect(() => { ... }, [])                |
         | componentDidUpdate()        | useEffect(() => { ... })                    |
         | componentWillUnmount()      | useEffect(() => { return () => {...} }, []) |

  Ví dụ:

                     {% raw %}
                       useEffect(() => {
                         console.log("Component mounted");

                         return () => {
                             console.log("Component unmounted");
                         };
                       }, []);
                     {% endraw %}

d. Lifting State Up – Nâng state lên cha

- Khi hai hoặc nhiều component con cần chia sẻ chung một state, ta di chuyển state đó lên component cha và truyền qua props.
  Ví dụ:

                     {% raw %}
                      // Cha
                      function Parent() {
                        const [value, setValue] = useState("");

                        return (
                        <>
                          <Input value={value} onChange={setValue} />
                          <Display value={value} />
                        </>
                        );
                      }

                      // Con 1
                      function Input({ value, onChange }) {
                        return <input value={value} onChange={e => onChange(e.target.value)} />;
                      }

                      // Con 2
                      function Display({ value }) {
                      return <p>Value: {value}</p>;
                      }
                     {% endraw %}

  Lý do:

  - Tránh trùng lặp state ở nhiều nơi.
  - Giúp data flow một chiều, dễ debug, dễ kiểm soát.

**Bảng tổng kết phần 2**

         |----------------------------------------------------------------------|
         | Kiến thức          | Nội dung chính                                  |
         |----------------------------------------------------------------------|
         | Component          | Đơn vị giao diện trong React                    |
         | Function vs Class  | Nên dùng function + hooks                       |
         | Props              | Dữ liệu truyền từ cha → con (readonly)          |
         | State              | Dữ liệu nội bộ có thể thay đổi                  |
         | Lifecycle          | Quản lý bằng useEffect() trong function         |
         | Lifting State Up   | Khi cần chia sẻ state giữa các component con    |

**3. Hooks (Rất quan trọng)**  
- Hooks là các hàm đặc biệt trong React cho phép chúng ta sử  dụng state, lifecycle, context,... trong function component mà trước đây chỉ có class component mới có thể làm được.  
- React Hooks ra đời từ phiên bản 16.8 và trở thành tiêu chuẩn phát triển hiện đại.  

a. useState - Quản lý state cục bộ  
- Dùng để  tạo và cập nhật state bên trong function component.  

                     {% raw %}
                     import { useState } from 'react';

                     function Counter() {
                      const [count, setCount] = useState(0);
                      return <button onClick={() => setCount(count + 1)}>Clicked {count}</button>;
                     }

                     {% endraw %}        

- useState(0) -> 0 là giá trị khởi tạo
- Trả về một mảng [giá_trị, hàm_cập_nhật]  

b.  useEffect - Lifecycle Hook  
- Dùng để  xử  lý side effect như: gọi API, subcribe, thao tác DOM,...sau khi component render.  

                    {% raw %}
                    import { useEffect } from 'react';

                    useEffect(() => {
                      console.log('Component mounted');

                      return () => {
                        console.log('Component unmounted');
                      };
                    }, []);
                    {% endraw %} 

   - [] : Chạy một lần duy nhất(như componentDidMount)  
   - [dependency] : Chạy lại khi dependency thay đổi  
   - Không có [] : Chạy lại mỗi lần render  

   Dùng để :  
     - Gọi API  
     - Lắng nghe sự kiện  
     - Cleanup (xoá listener, clearInverval,...)                      

c. useRef – Tham chiếu tới DOM hoặc lưu giá trị không làm re-render  
- Dùng để giữ giá trị không thay đổi khi re-render hoặc thao tác với DOM.  

                    {% raw %}
                    const inputRef = useRef();

                    const handleFocus = () => {
                      inputRef.current.focus(); // Truy cập DOM node
                    };

                    return <input ref={inputRef} />;
                    {% endraw %} 

   Ngoài thao tác DOM, useRef còn dùng để:  
      - Lưu giá trị trước đó  
      - Lưu biến cục bộ không gây re-render  

d. useMemo – Ghi nhớ giá trị tính toán  
- Tránh tính toán lại các giá trị tốn hiệu năng, khi dependency không thay đổi.

                    {% raw %}
                    const total = useMemo(() => {
                      return calculateTotal(items); // Hàm tính toán nặng
                    }, [items]);
                    {% endraw %} 
  
  - Chỉ re-calculate khi items thay đổi
  - Dùng để tối ưu performance (tránh re-compute không cần thiết)

e. useCallback – Ghi nhớ hàm  
- Tránh tạo hàm mới mỗi lần re-render, dùng nhiều trong truyền props xuống component con.

                    {% raw %}
                    const handleClick = useCallback(() => {
                      console.log('clicked');
                    }, []);
                    {% endraw %} 

  - Giúp tránh re-render không cần thiết ở component con được bọc React.memo

f. useContext – Truyền dữ liệu toàn cục  
- Dùng để truy cập giá trị từ Context API, tránh "drilling" props nhiều cấp.

  Tạo Context:

                    {% raw %}
                    const ThemeContext = React.createContext('light');
                    {% endraw %} 

  Dùng:

                    {% raw %}
                    const theme = useContext(ThemeContext);
                    {% endraw %} 

  Phù hợp với:

    - Theme, ngôn ngữ (i18n)
    - Thông tin user, quyền hạn
    - Dữ liệu cấu hình toàn app 

g. useReducer – Quản lý state phức tạp  
- Dùng thay thế useState khi state có nhiều trạng thái hoặc logic phức tạp.

                    {% raw %}
                    const reducer = (state, action) => {
                      switch(action.type) {
                        case 'increment': return { count: state.count + 1 };
                        case 'decrement': return { count: state.count - 1 };
                        default: return state;
                      }
                    };

                    const [state, dispatch] = useReducer(reducer, { count: 0 });
                    {% endraw %} 

  -Tương tự Redux: có state, dispatch, action
  -Hữu ích cho form lớn, table phức tạp, flow điều hướng

h. Custom Hook – Tạo hook riêng  
- Khi bạn có logic dùng lại nhiều lần, hãy đóng gói nó thành Custom Hook.
- Ví dụ:

                    {% raw %}
                    function useWindowWidth() {
                      const [width, setWidth] = useState(window.innerWidth);

                      useEffect(() => {
                        const handleResize = () => setWidth(window.innerWidth);
                        window.addEventListener('resize', handleResize);
                        return () => window.removeEventListener('resize', handleResize);
                      }, []);

                    return width;
                    }

                    // Sử dụng
                    const width = useWindowWidth();
                    {% endraw %} 

   - Tên custom hook phải bắt đầu bằng use, có thể dùng các hook khác bên trong.

**Bảng tổng kết Phần 3**

         |-------------------------------------------------------------------|
         | Hook         | Công dụng chính                                    |
         |-------------------------------------------------------------------|
         | useState     | Khai báo state trong function component            |
         | useEffect    | Lifecycle: mount, update, unmount                  |
         | useRef       | Tham chiếu DOM hoặc lưu biến cục bộ                |
         | useMemo      | Ghi nhớ giá trị tính toán lại                      |
         | useCallback  | Ghi nhớ hàm, tránh re-render con                   |
         | useContext   | Truy cập context toàn cục                          |
         | useReducer   | Quản lý state phức tạp (tương tự Redux)            |
         | Custom Hook  | Tái sử dụng logic, đóng gói logic có trạng thái    |

**4. Event Handling**

- Bắt sự kiện: onClick, onChange, onSubmit, ...
- Ngăn chặn mặc định (event.preventDefault())

**5. Conditional Rendering**

- if, &&, ternary, logical operators

**6. List Rendering**

- Dùng .map() để render list
- Sử dụng key đúng cách để tránh lỗi

**7. Forms**

- Controlled vs uncontrolled components
- Form validation cơ bản
- Thư viện hỗ trợ: react-hook-form, formik, yup

**II. Kiến thức nâng cao**

**1. Routing – Điều hướng**

- Thư viện react-router-dom
- Routes, Route, useNavigate, useParams

**2. State Management (Quản lý trạng thái)**

- Context API
- Redux Toolkit hoặc Zustand, Recoil
- Global state vs local state

**3. Call API**

- fetch, axios
- Dùng useEffect để gọi API
- Async/Await
- Error handling

**4. Component Communication**

- Cha → Con: props
- Con → Cha: callback props
- Con → Con: thông qua cha hoặc Context/Redux

**5. Performance Optimization**

- React.memo, useMemo, useCallback
- Lazy loading (React.lazy, Suspense)
- Split code, Virtualization (ví dụ: react-window)

**6. Testing**

- Unit test: Jest, React Testing Library
- E2E test: Cypress, Playwright

**III. Các phần cần chú trọng để phát triển một dự án React**

**1. Cấu trúc thư mục rõ ràng**

- components/, pages/, hooks/, services/, constants/, utils/, store/, ...
- Dễ maintain, scale

**2. Quản lý state**

- Dùng Context cho state nhỏ, Redux Toolkit cho state lớn
- Phân biệt rõ local và global state

**3. Giao tiếp với Backend**

- Tạo service layer dùng axios hoặc fetch
- Gắn token, handle lỗi, retry,...

**4. Giao diện và UI/UX**

- Dùng thư viện: Ant Design, Material UI, TailwindCSS
- Responsive, mobile-friendly
- Loading state, error state

**5. Testing**

- Test logic, component, flow chính

**6. Dev Tools và Linter**

- ESLint, Prettier
- Husky, lint-staged
- Git hook để kiểm tra code trước khi commit

**7. Internationalization (i18n) nếu đa ngôn ngữ**

- react-i18next hoặc tương đương

**8. Bảo mật**

- Không lộ API key
- Xử lý token an toàn
- Validate form đầu vào

**9. Tối ưu hiệu năng**

- Chia nhỏ component
- Giảm re-render
- Lazy load page/component không cần thiết ngay

**10. Triển khai (Deployment)**

- Build với vite hoặc webpack
- Deploy lên Netlify, Vercel, Firebase, Cloud (AWS, GCP, Azure)
