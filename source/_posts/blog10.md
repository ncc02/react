---
title: <10> Hooks - useContext Hook (Advance Hook)
date: 2025-02-27 09:08:18
tags:
---
### 1. **Tại sao `useContext` nằm trong lộ trình React?**  
`useContext` là một trong những Hook quan trọng của React, giúp quản lý trạng thái toàn cục mà không cần phải truyền props qua nhiều cấp (prop drilling). Nó được sử dụng để chia sẻ dữ liệu giữa các component mà không cần truyền từng cấp một.

Trong lộ trình React, `useContext` được đưa vào để:  
- Giúp quản lý state hiệu quả hơn, tránh việc truyền props sâu vào component con.  
- Giúp code gọn gàng, dễ bảo trì hơn.  
- Được sử dụng cùng với các thư viện quản lý state như Redux Toolkit, Zustand hoặc React Query.  

---

### 2. **`useContext` Hook là gì?**  
`useContext` là một Hook trong React dùng để truy cập giá trị từ một Context mà không cần sử dụng component wrapper `<Context.Consumer>`.  

Cú pháp:  
```jsx
const value = useContext(MyContext);
```
- `MyContext` là Context được tạo bằng `React.createContext()`.
- `value` là giá trị được cung cấp bởi `MyContext.Provider`.

---

### 3. **Ví dụ về `useContext` Hook**  

#### Ví dụ 1: **Quản lý chủ đề (Theme)**
```jsx
import React, { createContext, useContext, useState } from "react";

// Tạo Context
const ThemeContext = createContext();

const ThemeProvider = ({ children }) => {
  const [theme, setTheme] = useState("light");

  // Hàm toggle theme
  const toggleTheme = () => {
    setTheme((prevTheme) => (prevTheme === "light" ? "dark" : "light"));
  };

  return (
    <ThemeContext.Provider value={{ theme, toggleTheme }}>
      {children}
    </ThemeContext.Provider>
  );
};

const ThemeButton = () => {
  const { theme, toggleTheme } = useContext(ThemeContext);
  return (
    <button onClick={toggleTheme} style={{ background: theme === "light" ? "#fff" : "#333", color: theme === "light" ? "#000" : "#fff" }}>
      Chế độ: {theme}
    </button>
  );
};

const App = () => (
  <ThemeProvider>
    <ThemeButton />
  </ThemeProvider>
);

export default App;
```
🔥 **Giải thích:**  
- Tạo `ThemeContext` bằng `createContext()`.  
- `ThemeProvider` quản lý state `theme` và cung cấp hàm `toggleTheme`.  
- `ThemeButton` sử dụng `useContext` để lấy `theme` và `toggleTheme`.  

---

#### Ví dụ 2: **Quản lý user đăng nhập**
```jsx
import React, { createContext, useContext, useState } from "react";

// Tạo Context
const AuthContext = createContext();

const AuthProvider = ({ children }) => {
  const [user, setUser] = useState(null);

  const login = (name) => setUser({ name });
  const logout = () => setUser(null);

  return (
    <AuthContext.Provider value={{ user, login, logout }}>
      {children}
    </AuthContext.Provider>
  );
};

const Profile = () => {
  const { user, logout } = useContext(AuthContext);
  return user ? (
    <div>
      <h3>Xin chào, {user.name}!</h3>
      <button onClick={logout}>Đăng xuất</button>
    </div>
  ) : (
    <h3>Chưa đăng nhập</h3>
  );
};

const LoginButton = () => {
  const { login } = useContext(AuthContext);
  return <button onClick={() => login("Cuongtk2002")}>Đăng nhập</button>;
};

const App = () => (
  <AuthProvider>
    <Profile />
    <LoginButton />
  </AuthProvider>
);

export default App;
```
🔥 **Giải thích:**  
- `AuthContext` lưu trạng thái user đăng nhập.  
- `AuthProvider` cung cấp hàm `login`, `logout` và thông tin user.  
- `Profile` và `LoginButton` dùng `useContext` để truy cập trạng thái đăng nhập.  

---

### 4. **Khi nào nên dùng `useContext`?**
✅ Khi cần chia sẻ dữ liệu giữa nhiều component (theme, authentication, ngôn ngữ, v.v.).  
✅ Khi muốn tránh prop drilling (truyền props qua nhiều cấp).  
❌ Không nên lạm dụng nếu dữ liệu không cần chia sẻ rộng rãi, vì có thể gây re-render không cần thiết.  

Nếu ứng dụng lớn, có thể kết hợp `useContext` với **Redux Toolkit** hoặc **Zustand** để quản lý state tốt hơn. 🚀