---
title: <15> Hooks - Rules of Hooks (Basic)
date: 2025-02-28 10:00:04
tags:
---
**Rules of Hooks** là một tập hợp các nguyên tắc quan trọng giúp bạn sử dụng các hooks trong React một cách chính xác. Chúng được đưa ra để đảm bảo rằng hooks được sử dụng trong môi trường React một cách nhất quán và tránh gây lỗi. Các rules này là phần quan trọng trong lộ trình học React vì chúng giúp bạn tránh được những vấn đề phổ biến khi sử dụng hooks.

### **Rules of Hooks là gì?**

Rules of Hooks là những quy tắc bạn cần tuân theo khi sử dụng hooks trong React. Có ba quy tắc chính:

1. **Chỉ gọi hooks ở cấp cao nhất (top level)**:
   - Bạn chỉ nên gọi hooks ở cấp cao nhất trong component hoặc trong các custom hooks. Điều này có nghĩa là không gọi hooks trong các vòng lặp, điều kiện hoặc hàm lồng nhau. Mục tiêu là để React dễ dàng theo dõi việc gọi hooks giữa các lần render.
   - **Sai**:
     ```js
     if (isLoggedIn) {
       useEffect(() => { console.log("User is logged in"); }, []);
     }
     ```
   - **Đúng**:
     ```js
     useEffect(() => {
       if (isLoggedIn) {
         console.log("User is logged in");
       }
     }, [isLoggedIn]);
     ```

2. **Chỉ gọi hooks trong function component hoặc custom hook**:
   - Hooks không thể được gọi trong các component dạng class hoặc các hàm thông thường. Chúng chỉ được phép sử dụng trong các function component hoặc custom hooks.
   - **Sai**:
     ```js
     class MyComponent extends React.Component {
       componentDidMount() {
         useEffect(() => { console.log("Mounted!"); }, []);
       }
     }
     ```
   - **Đúng**:
     ```js
     function MyComponent() {
       useEffect(() => { console.log("Mounted!"); }, []);
     }
     ```

3. **Chỉ gọi hooks trong function component hoặc custom hook**:
   - Điều này đảm bảo rằng React có thể xác định được chính xác thứ tự của hooks giữa các lần render và giúp React cập nhật đúng cách.
   - **Sai**:
     ```js
     const useCustomHook = () => {
       useEffect(() => { console.log("Effect in custom hook"); }, []);
     }
     ```
   - **Đúng**:
     ```js
     function MyComponent() {
       useCustomHook();
     }
     
     const useCustomHook = () => {
       useEffect(() => { console.log("Effect in custom hook"); }, []);
     }
     ```

### **Ví dụ về Rules of Hooks:**

1. **Sử dụng hooks ở cấp cao nhất**:
   ```js
   function MyComponent() {
     const [count, setCount] = useState(0);

     useEffect(() => {
       document.title = `You clicked ${count} times`;
     }, [count]);

     return (
       <div>
         <p>You clicked {count} times</p>
         <button onClick={() => setCount(count + 1)}>Click me</button>
       </div>
     );
   }
   ```

2. **Không gọi hooks trong điều kiện**:
   ```js
   // Sai
   function MyComponent({ isLoggedIn }) {
     if (isLoggedIn) {
       useEffect(() => {
         console.log('User logged in');
       }, []);
     }
   }

   // Đúng
   function MyComponent({ isLoggedIn }) {
     useEffect(() => {
       if (isLoggedIn) {
         console.log('User logged in');
       }
     }, [isLoggedIn]);
   }
   ```

Những nguyên tắc này giúp bạn tránh những lỗi không mong muốn và giữ cho ứng dụng React của bạn ổn định và dễ bảo trì.