---
title: <11> Hooks - useReducer (Medium Hook)
date: 2025-02-27 09:21:37
tags:
---
### 1. Tại sao `useReducer` nằm trong lộ trình React?  
`useReducer` là một hook quan trọng trong React, đặc biệt hữu ích khi quản lý state phức tạp. Nó cung cấp một cách tiếp cận tương tự Redux nhưng nhẹ hơn, giúp quản lý state theo kiểu reducer pattern thay vì `useState`.  

🔹 Khi nào nên dùng `useReducer`?  
- Khi state có nhiều nhánh và logic cập nhật phức tạp.  
- Khi cần tách biệt logic cập nhật state khỏi component.  
- Khi cần tối ưu performance (giảm số lần render lại không cần thiết).  

---

### 2. `useReducer` là gì?  
`useReducer` là một hook trong React dùng để quản lý state bằng cách sử dụng reducer function. Cú pháp của nó như sau:  

```tsx
const [state, dispatch] = useReducer(reducer, initialState);
```  

- `reducer(state, action)`: Một hàm nhận state hiện tại và action để trả về state mới.  
- `initialState`: Giá trị khởi tạo của state.  
- `dispatch(action)`: Gửi action để reducer xử lý.  

`useReducer` hoạt động theo mô hình **reducer pattern**, tương tự Redux nhưng không cần store toàn cục.  

---

### 3. Ví dụ về `useReducer`  

#### 🟢 Ví dụ 1: Counter đơn giản  
```tsx
import { useReducer } from "react";

// 1. Định nghĩa reducer function
const reducer = (state, action) => {
  switch (action.type) {
    case "increment":
      return { count: state.count + 1 };
    case "decrement":
      return { count: state.count - 1 };
    case "reset":
      return { count: 0 };
    default:
      return state;
  }
};

// 2. Giá trị khởi tạo
const initialState = { count: 0 };

export default function Counter() {
  const [state, dispatch] = useReducer(reducer, initialState);

  return (
    <div>
      <h2>Count: {state.count}</h2>
      <button onClick={() => dispatch({ type: "increment" })}>+</button>
      <button onClick={() => dispatch({ type: "decrement" })}>-</button>
      <button onClick={() => dispatch({ type: "reset" })}>Reset</button>
    </div>
  );
}
```
✅ Khi nhấn nút, `dispatch` gửi action đến `reducer`, cập nhật state theo logic đã định nghĩa.  

---

#### 🟢 Ví dụ 2: Quản lý Todo List với `useReducer`
```tsx
import { useReducer, useState } from "react";

// 1. Định nghĩa reducer
const reducer = (state, action) => {
  switch (action.type) {
    case "add":
      return [...state, { id: Date.now(), text: action.payload }];
    case "remove":
      return state.filter(todo => todo.id !== action.payload);
    case "clear":
      return [];
    default:
      return state;
  }
};

// 2. Giá trị khởi tạo
const initialState = [];

export default function TodoApp() {
  const [state, dispatch] = useReducer(reducer, initialState);
  const [input, setInput] = useState("");

  return (
    <div>
      <h2>Todo List</h2>
      <input value={input} onChange={(e) => setInput(e.target.value)} />
      <button onClick={() => dispatch({ type: "add", payload: input })}>
        Add
      </button>
      <button onClick={() => dispatch({ type: "clear" })}>Clear All</button>
      <ul>
        {state.map((todo) => (
          <li key={todo.id}>
            {todo.text} 
            <button onClick={() => dispatch({ type: "remove", payload: todo.id })}>
              X
            </button>
          </li>
        ))}
      </ul>
    </div>
  );
}
```
✅ Ứng dụng cho phép thêm, xoá và xóa tất cả các công việc trong danh sách.  

---

### 4. So sánh `useState` và `useReducer`
| Tiêu chí | `useState` | `useReducer` |
|----------|-----------|-------------|
| Cấu trúc state | Đơn giản | Phức tạp |
| Cập nhật state | Trực tiếp | Qua reducer function |
| Khi nào nên dùng? | State nhỏ, đơn giản | State nhiều nhánh, có logic cập nhật phức tạp |

💡 Nếu state có nhiều logic hoặc có liên quan chặt chẽ giữa các phần tử, `useReducer` là một lựa chọn tốt hơn `useState`.

---

### 5. Khi nào nên dùng `useReducer` thay vì `useState`?
✅ Khi state phức tạp, có nhiều logic cập nhật.  
✅ Khi cần tách biệt logic cập nhật state ra khỏi component (dễ bảo trì).  
✅ Khi muốn tối ưu hiệu năng bằng cách hạn chế render lại không cần thiết.  

🔹 **Gợi ý**: Nếu đang dùng `useReducer` mà thấy quá phức tạp, có thể cân nhắc sử dụng **Redux Toolkit** để quản lý state dễ dàng hơn.  

Bạn có cần thêm ví dụ nào nữa không? 🚀