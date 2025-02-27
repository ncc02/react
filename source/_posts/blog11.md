---
title: <12> Hooks - useRef Hook (Advance Hook)
date: 2025-02-27 09:27:46
tags:
---
### 📌 **Tại sao `useRef` nằm trong lộ trình React?**
`useRef` là một trong những Hook quan trọng của React, giúp giải quyết một số vấn đề như:
1. **Tránh re-render không cần thiết**: Không giống như `useState`, thay đổi giá trị của `useRef` không làm component re-render.
2. **Truy cập DOM trực tiếp**: Hữu ích khi cần lấy tham chiếu đến một phần tử DOM mà không dùng `document.querySelector`.
3. **Lưu trữ giá trị giữa các lần render**: `useRef` có thể giữ dữ liệu trong suốt vòng đời của component mà không bị reset khi component re-render.

---

### 📌 **useRef Hook là gì?**
`useRef` là một Hook trong React giúp tạo một tham chiếu (reference) có thể thay đổi mà **không làm component re-render**. Nó trả về một object có thuộc tính `.current`, dùng để lưu trữ giá trị có thể thay đổi mà không ảnh hưởng đến vòng đời của component.

**Cú pháp:**
```jsx
const refContainer = useRef(initialValue);
```
- `refContainer.current`: Chứa giá trị hiện tại của `useRef`.

---

### 📌 **Ví dụ về `useRef`**
#### 🟢 1. **Truy cập DOM trực tiếp**
Dùng `useRef` để focus vào một ô input khi component mount.
```jsx
import { useRef, useEffect } from "react";

function InputFocus() {
  const inputRef = useRef(null);

  useEffect(() => {
    inputRef.current.focus(); // Focus vào input khi component mount
  }, []);

  return <input ref={inputRef} placeholder="Nhập nội dung..." />;
}

export default InputFocus;
```
📌 **Giải thích:**
- `useRef(null)`: Tạo một tham chiếu ban đầu là `null`.
- Gán `ref={inputRef}` vào thẻ `<input>` để `inputRef.current` trỏ đến input.
- Dùng `useEffect` để gọi `inputRef.current.focus()` khi component mount.

---

#### 🔵 2. **Giữ giá trị mà không làm re-render**
Dùng `useRef` để lưu biến đếm số lần component render mà **không làm component re-render**.

```jsx
import { useRef, useState, useEffect } from "react";

function Counter() {
  const [count, setCount] = useState(0);
  const renderCount = useRef(0);

  useEffect(() => {
    renderCount.current += 1; // Tăng biến đếm sau mỗi lần render
  });

  return (
    <div>
      <p>Count: {count}</p>
      <p>Số lần render: {renderCount.current}</p>
      <button onClick={() => setCount(count + 1)}>Tăng Count</button>
    </div>
  );
}

export default Counter;
```
📌 **Giải thích:**
- `renderCount` lưu trữ số lần render mà **không bị reset** mỗi khi component re-render.
- `useRef` giữ giá trị giữa các lần render mà không làm component bị render lại.

---

#### 🔴 3. **Giữ tham chiếu đến giá trị trước đó**
Dùng `useRef` để lưu giá trị trước đó của `count`.

```jsx
import { useRef, useState, useEffect } from "react";

function PreviousValue() {
  const [count, setCount] = useState(0);
  const prevCountRef = useRef(0);

  useEffect(() => {
    prevCountRef.current = count; // Cập nhật giá trị trước đó mỗi lần count thay đổi
  }, [count]);

  return (
    <div>
      <p>Giá trị hiện tại: {count}</p>
      <p>Giá trị trước đó: {prevCountRef.current}</p>
      <button onClick={() => setCount(count + 1)}>Tăng Count</button>
    </div>
  );
}

export default PreviousValue;
```
📌 **Giải thích:**
- `prevCountRef` lưu giá trị trước đó của `count` mà không làm component re-render.

---

### 📌 **Khi nào nên dùng `useRef`?**
- Khi cần truy cập trực tiếp vào DOM (focus input, lấy kích thước phần tử, v.v.).
- Khi cần lưu trữ giá trị giữa các lần render mà **không làm component render lại**.
- Khi cần giữ giá trị trước đó của một state mà không làm ảnh hưởng đến vòng đời component.

💡 **Tóm lại**: `useRef` giúp tối ưu hiệu suất trong React bằng cách **giữ dữ liệu mà không làm component re-render**, đồng thời cung cấp quyền truy cập trực tiếp vào DOM.

Bạn có đang gặp vấn đề gì cần dùng `useRef` không? 🚀