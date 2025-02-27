---
title: <13> Hooks - useCallback Hook (Advance Hook)
date: 2025-02-27 09:35:37
tags:
---
### 1. **Tại sao `useCallback` nằm trong lộ trình React?**
React tập trung vào tối ưu hiệu suất và cải thiện trải nghiệm lập trình bằng cách giảm số lần re-render không cần thiết. Hook `useCallback` là một trong những công cụ giúp tối ưu hóa hiệu suất, đặc biệt trong các tình huống khi:

- Một function được truyền xuống component con gây re-render không cần thiết.
- Function cần được ghi nhớ để tránh tạo lại khi component re-render.
- Tối ưu hóa kết hợp với `useMemo` hoặc khi sử dụng trong dependency array của `useEffect`.

Vì vậy, `useCallback` là một phần quan trọng trong lộ trình học React nâng cao, giúp cải thiện hiệu suất ứng dụng.

---

### 2. **`useCallback` là gì?**
`useCallback` là một hook trong React dùng để **ghi nhớ (memoize) một function**, giúp tránh việc tạo lại function không cần thiết khi component re-render.

Cú pháp:
```tsx
const memoizedCallback = useCallback(callback, dependencies);
```
- `callback`: Hàm cần ghi nhớ.
- `dependencies`: Danh sách các dependency, khi một trong số chúng thay đổi, function sẽ được tạo lại.

---

### 3. **Ví dụ về `useCallback`**
#### 🌟 **Ví dụ 1: Tránh re-render component con không cần thiết**
Khi truyền một function xuống component con, nếu không dùng `useCallback`, function sẽ bị tạo lại mỗi lần component cha re-render, gây re-render không cần thiết cho component con.

##### 🔹 **Không dùng `useCallback` (component con re-render không cần thiết)**
```tsx
import { useState } from "react";

function Parent() {
  const [count, setCount] = useState(0);

  // Function này bị tạo lại mỗi lần Parent re-render
  const handleClick = () => {
    console.log("Clicked!");
  };

  return (
    <div>
      <h1>Count: {count}</h1>
      <button onClick={() => setCount(count + 1)}>Increase</button>
      <Child handleClick={handleClick} />
    </div>
  );
}

function Child({ handleClick }) {
  console.log("Child component re-rendered!");
  return <button onClick={handleClick}>Click me</button>;
}

export default Parent;
```
📌 **Vấn đề:**  
- Mỗi lần `Parent` re-render (do `count` thay đổi), `handleClick` bị tạo lại.
- Điều này khiến `Child` cũng re-render, mặc dù nó không thay đổi gì.

---

##### 🔹 **Dùng `useCallback` để tối ưu**
```tsx
import { useState, useCallback } from "react";

function Parent() {
  const [count, setCount] = useState(0);

  // Ghi nhớ function, không tạo mới khi count thay đổi
  const handleClick = useCallback(() => {
    console.log("Clicked!");
  }, []);

  return (
    <div>
      <h1>Count: {count}</h1>
      <button onClick={() => setCount(count + 1)}>Increase</button>
      <Child handleClick={handleClick} />
    </div>
  );
}

function Child({ handleClick }) {
  console.log("Child component re-rendered!");
  return <button onClick={handleClick}>Click me</button>;
}

export default Parent;
```
📌 **Lợi ích khi dùng `useCallback`:**  
- `handleClick` **chỉ được tạo một lần** và không thay đổi khi `count` thay đổi.
- Component `Child` không bị re-render khi `Parent` re-render → **Cải thiện hiệu suất.**

---

#### 🌟 **Ví dụ 2: Kết hợp `useCallback` với `useMemo` để tối ưu danh sách lọc**
Nếu có một danh sách lớn, ta có thể kết hợp `useCallback` và `useMemo` để tối ưu hóa quá trình tính toán danh sách lọc.

```tsx
import { useState, useCallback, useMemo } from "react";

const items = ["Apple", "Banana", "Orange", "Mango", "Pineapple"];

function App() {
  const [query, setQuery] = useState("");

  // useCallback giúp ghi nhớ function filterItems
  const filterItems = useCallback(
    (query) => {
      console.log("Filtering items...");
      return items.filter((item) =>
        item.toLowerCase().includes(query.toLowerCase())
      );
    },
    []
  );

  // useMemo giúp lưu kết quả filter để tránh tính toán lại không cần thiết
  const filteredItems = useMemo(() => filterItems(query), [query, filterItems]);

  return (
    <div>
      <input
        type="text"
        value={query}
        onChange={(e) => setQuery(e.target.value)}
        placeholder="Search..."
      />
      <ul>
        {filteredItems.map((item) => (
          <li key={item}>{item}</li>
        ))}
      </ul>
    </div>
  );
}

export default App;
```
📌 **Lợi ích của `useCallback` ở đây:**  
- `filterItems` không bị tạo lại khi component re-render, giúp tối ưu hiệu suất.  
- `useMemo` chỉ chạy khi `query` thay đổi, tránh tính toán lại danh sách không cần thiết.

---

### 📌 **Tóm tắt**
✅ **`useCallback` giúp:**  
- Tránh tạo lại function không cần thiết khi component re-render.  
- Giúp component con không bị re-render không cần thiết khi function truyền xuống không thay đổi.  
- Tối ưu hiệu suất khi sử dụng với `useMemo`, `useEffect`, hoặc danh sách dependency.  

🚀 **Khi nào nên dùng `useCallback`?**  
- Khi truyền function xuống component con.  
- Khi function sử dụng trong `useEffect` hoặc `useMemo` mà không muốn nó bị tạo lại.  
- Khi có nhiều logic phức tạp và muốn tối ưu hiệu suất.  

🛑 **Khi nào không nên dùng `useCallback`?**  
- Nếu function không được truyền xuống component con hoặc không ảnh hưởng hiệu suất, thì không cần dùng.  
- Nếu function không gây re-render không cần thiết thì không cần tối ưu quá sớm.  

---