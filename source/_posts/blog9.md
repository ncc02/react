---
title: <8> Hooks - useEffect Hook (Basic Hook)
date: 2025-02-27 09:02:52
tags:
---
### 1. **useEffect Hook tại sao lại nằm trong lộ trình React?**  
`useEffect` nằm trong lộ trình React vì nó giúp xử lý **side effects** trong function components. Trước đây, khi sử dụng class components, chúng ta phải sử dụng các lifecycle methods như `componentDidMount`, `componentDidUpdate` và `componentWillUnmount` để thực hiện các tác vụ như:  
- Gọi API  
- Lắng nghe sự kiện (event listeners)  
- Quản lý subscriptions (WebSocket, Firebase, v.v.)  
- Tương tác với DOM  

Khi React chuyển sang sử dụng function components với Hooks, `useEffect` ra đời để thay thế và hợp nhất những lifecycle methods trên, giúp code dễ đọc và bảo trì hơn.

---

### 2. **useEffect Hook là gì?**  
`useEffect` là một hook trong React dùng để thực thi các **side effects** trong function components. Nó nhận vào 2 tham số:  
```tsx
useEffect(callback, [dependencies])
```
- **`callback`**: Hàm chứa logic cần thực hiện.  
- **`dependencies`**: Danh sách các biến phụ thuộc (optional). Nếu dependencies thay đổi, `callback` sẽ được gọi lại.  

Tùy vào cách sử dụng `dependencies`, `useEffect` có thể hoạt động như:  
1. `componentDidMount`: Chạy một lần khi component mount.  
2. `componentDidUpdate`: Chạy mỗi khi dependencies thay đổi.  
3. `componentWillUnmount`: Cleanup khi component bị unmount.  

---

### 3. **Ví dụ về useEffect Hook**
#### 🔹 **Ví dụ 1: Gọi API khi component mount**
```tsx
import { useEffect, useState } from "react";

function UsersList() {
  const [users, setUsers] = useState([]);

  useEffect(() => {
    fetch("https://jsonplaceholder.typicode.com/users")
      .then((response) => response.json())
      .then((data) => setUsers(data));
  }, []); // Dependency array rỗng -> chạy 1 lần khi component mount

  return (
    <ul>
      {users.map((user) => (
        <li key={user.id}>{user.name}</li>
      ))}
    </ul>
  );
}

export default UsersList;
```

#### 🔹 **Ví dụ 2: Cập nhật tiêu đề trang khi state thay đổi**
```tsx
import { useEffect, useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    document.title = `Count: ${count}`;
  }, [count]); // Chạy lại mỗi khi `count` thay đổi

  return (
    <div>
      <p>{count}</p>
      <button onClick={() => setCount(count + 1)}>Increase</button>
    </div>
  );
}

export default Counter;
```

#### 🔹 **Ví dụ 3: Cleanup effect khi component unmount**
```tsx
import { useEffect, useState } from "react";

function Timer() {
  const [seconds, setSeconds] = useState(0);

  useEffect(() => {
    const interval = setInterval(() => {
      setSeconds((prev) => prev + 1);
    }, 1000);

    return () => {
      clearInterval(interval); // Cleanup interval khi component bị unmount
    };
  }, []);

  return <p>Time: {seconds} seconds</p>;
}

export default Timer;
```

---
### 🔥 Tổng kết:
- `useEffect` giúp thực thi side effects trong function components.  
- Nó có thể thay thế các lifecycle methods trong class components.  
- `useEffect` chạy theo nhiều cách khác nhau tùy vào dependency array.  
- Có thể cleanup effect bằng cách return một hàm trong `useEffect`.

🚀 Bạn có muốn mình làm thêm một ví dụ nâng cao như tối ưu hóa hiệu suất với `useEffect` không? 😃