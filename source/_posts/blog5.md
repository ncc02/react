---
title: <5> Rendering - Events
date: 2025-02-26 21:55:44
tags:
---
### 1. **Tại sao Events là một phần trong roadmap React?**  
Sự kiện (**Events**) là một phần quan trọng trong React vì chúng giúp ứng dụng phản hồi lại các hành động của người dùng, chẳng hạn như click chuột, nhập dữ liệu, di chuyển chuột, v.v. Nếu không có sự kiện, các ứng dụng React sẽ không thể tương tác được mà chỉ hiển thị dữ liệu tĩnh.

Trong roadmap học React, **Events** thường được đề cập sớm vì chúng liên quan trực tiếp đến cách người dùng tương tác với ứng dụng. Hiểu cách xử lý sự kiện giúp bạn xây dựng các UI động, quản lý state và điều hướng luồng dữ liệu trong React.

---

### 2. **Events là gì?**  
Trong React, **Events** là các sự kiện giao diện người dùng, giống như trong JavaScript thuần (DOM Events). React cung cấp một hệ thống xử lý sự kiện dựa trên **SyntheticEvent**, một lớp trừu tượng giúp đảm bảo tính nhất quán giữa các trình duyệt.

Một số điểm quan trọng về React Events:
- Tên sự kiện sử dụng **camelCase** (ví dụ: `onClick`, `onChange` thay vì `onclick`, `onchange`).
- Truyền một **hàm**, không phải chuỗi, vào event handler.
- Có thể dùng `event.preventDefault()` để ngăn chặn hành vi mặc định.
- Có thể truyền tham số vào event handler bằng cách dùng arrow function.

---

### 3. **Ví dụ về Events trong React**  

#### 📌 **Ví dụ 1: Xử lý sự kiện Click**
```jsx
import { useState } from "react";

export default function ClickCounter() {
  const [count, setCount] = useState(0);

  function handleClick() {
    setCount(count + 1);
  }

  return <button onClick={handleClick}>Clicked {count} times</button>;
}
```
📝 **Giải thích**:
- Khi người dùng nhấn nút, hàm `handleClick` được gọi và tăng giá trị `count` lên 1.

---

#### 📌 **Ví dụ 2: Ngăn chặn hành vi mặc định của sự kiện Form Submit**
```jsx
function handleSubmit(event) {
  event.preventDefault();
  alert("Form submitted!");
}

export default function MyForm() {
  return (
    <form onSubmit={handleSubmit}>
      <button type="submit">Submit</button>
    </form>
  );
}
```
📝 **Giải thích**:
- `event.preventDefault()` giúp ngăn form tải lại trang sau khi submit.

---

#### 📌 **Ví dụ 3: Lấy giá trị từ input (`onChange` event)**
```jsx
import { useState } from "react";

export default function InputExample() {
  const [text, setText] = useState("");

  function handleChange(event) {
    setText(event.target.value);
  }

  return (
    <div>
      <input type="text" value={text} onChange={handleChange} />
      <p>You typed: {text}</p>
    </div>
  );
}
```
📝 **Giải thích**:
- Khi người dùng nhập vào ô input, sự kiện `onChange` cập nhật state `text`, làm React render lại UI.

---

#### 📌 **Ví dụ 4: Truyền tham số vào Event Handler**
```jsx
function handleClick(name) {
  alert(`Hello, ${name}!`);
}

export default function GreetingButton() {
  return <button onClick={() => handleClick("Cuong")}>Say Hello</button>;
}
```
📝 **Giải thích**:
- Ta dùng arrow function `() => handleClick("Cuong")` để truyền tham số vào hàm `handleClick`.

---

### 4. **Tổng kết**  
- **Events trong React** giúp xử lý các tương tác của người dùng với ứng dụng.  
- **Sự khác biệt so với DOM Events**:
  - Sử dụng **camelCase** thay vì lowercase.
  - Truyền **hàm**, không phải chuỗi.
  - Dựa trên `SyntheticEvent` để đảm bảo tính nhất quán.  
- **Các loại Events phổ biến trong React**:
  - `onClick`
  - `onChange`
  - `onSubmit`
  - `onMouseOver`
  - `onKeyDown`
  - `onFocus`, `onBlur`
  - `onScroll`

👉 **Nắm vững cách xử lý sự kiện là bước quan trọng khi học React vì nó giúp xây dựng các ứng dụng động và tương tác.** 🚀