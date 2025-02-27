---
title: <8> Hooks - useState Hook (Basic Hook)
date: 2025-02-27 08:59:19
tags:
---
### 🔹 useState Hook là gì?
`useState` là một Hook trong React giúp quản lý state (trạng thái) trong các **functional component**. Khi gọi `useState`, nó trả về một **mảng gồm 2 phần tử**:  
1. **Giá trị state hiện tại**  
2. **Hàm để cập nhật state**  

📌 **Cú pháp:**  
```jsx
const [state, setState] = useState(initialValue);
```
- `state`: Biến lưu giá trị của state.
- `setState`: Hàm dùng để cập nhật state.
- `initialValue`: Giá trị khởi tạo cho state.

---

### 🔹 Tại sao useState Hook nằm trong lộ trình React?
Trước đây, **class component** sử dụng `this.state` để quản lý state, nhưng khi React chuyển sang **functional component**, cần có cách thay thế để quản lý state mà không cần class.  
Vì thế, `useState` được giới thiệu từ React **16.8**, giúp các **functional component** có thể quản lý trạng thái mà không cần class.

📌 **Ưu điểm của `useState` so với `this.state` trong class component:**  
✅ Dễ sử dụng hơn, không cần `this`.  
✅ Code ngắn gọn, dễ đọc hơn.  
✅ Kết hợp tốt với các Hook khác (`useEffect`, `useReducer`,...).  
✅ Không cần phải kế thừa từ `Component`, giúp code linh hoạt hơn.

---

### 🔹 Ví dụ về useState Hook

#### 1️⃣ **Ví dụ đơn giản: Tăng/giảm số đếm**
```jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Số đếm: {count}</p>
      <button onClick={() => setCount(count + 1)}>Tăng</button>
      <button onClick={() => setCount(count - 1)}>Giảm</button>
    </div>
  );
}

export default Counter;
```
📌 **Giải thích:**  
- `count` là biến state, ban đầu có giá trị `0`.  
- `setCount` là hàm cập nhật state, khi bấm nút, giá trị `count` sẽ thay đổi.  

---

#### 2️⃣ **Ví dụ: Quản lý chuỗi ký tự**
```jsx
import { useState } from "react";

function InputField() {
  const [text, setText] = useState("");

  return (
    <div>
      <input 
        type="text" 
        value={text} 
        onChange={(e) => setText(e.target.value)} 
      />
      <p>Nhập: {text}</p>
    </div>
  );
}

export default InputField;
```
📌 **Giải thích:**  
- `text` là state chứa giá trị nhập vào từ ô input.  
- Khi người dùng gõ chữ, `setText(e.target.value)` sẽ cập nhật state.  

---

#### 3️⃣ **Ví dụ: Quản lý danh sách (mảng)**
```jsx
import { useState } from "react";

function TodoList() {
  const [tasks, setTasks] = useState([]);

  const addTask = () => {
    setTasks([...tasks, `Công việc ${tasks.length + 1}`]);
  };

  return (
    <div>
      <button onClick={addTask}>Thêm công việc</button>
      <ul>
        {tasks.map((task, index) => (
          <li key={index}>{task}</li>
        ))}
      </ul>
    </div>
  );
}

export default TodoList;
```
📌 **Giải thích:**  
- `tasks` là state chứa danh sách công việc (mảng).  
- Khi nhấn nút **"Thêm công việc"**, state sẽ cập nhật bằng cách thêm phần tử mới vào mảng.  

---

### 🚀 Kết luận:
`useState` là một trong những **Hook quan trọng nhất** trong React, giúp functional component có thể quản lý state dễ dàng hơn so với cách truyền thống trong class component.  

Bạn muốn tìm hiểu thêm về `useState` hay muốn thử nghiệm với bài toán cụ thể nào không? 😊
