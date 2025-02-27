---
title: Hooks - Writing Custom Hooks
date: 2025-02-27 08:49:23
tags:
---

### 1. **Tại sao "Writing Custom Hooks" nằm trong lộ trình React?**
"Writing Custom Hooks" nằm trong lộ trình React vì:  
- **Tái sử dụng logic:** Hooks giúp chia sẻ logic giữa các component mà không cần sử dụng HOC (Higher-Order Components) hoặc Render Props.  
- **Giảm lặp code:** Khi nhiều component có chung logic (ví dụ: gọi API, xử lý form, debounce...), ta có thể viết một Custom Hook để tái sử dụng.  
- **Dễ bảo trì:** Khi logic được tách biệt khỏi component, code dễ hiểu và dễ sửa lỗi hơn.  
- **Đồng bộ với Hook API:** Custom Hooks tận dụng các Hook có sẵn như `useState`, `useEffect`, `useContext`, giúp code rõ ràng và ngắn gọn hơn.  

---

### 2. **Writing Custom Hooks là gì?**
Custom Hook là một hàm JavaScript sử dụng các Hook có sẵn của React (ví dụ: `useState`, `useEffect`, `useRef`, `useMemo`...), giúp tái sử dụng logic giữa các component mà không làm thay đổi cấu trúc của chúng.  
- Custom Hook luôn bắt đầu bằng tiền tố **`use`** (ví dụ: `useFetch`, `useLocalStorage`...) để React có thể nhận diện và quản lý trạng thái đúng cách.  
- Custom Hook không thể được sử dụng bên trong vòng lặp, điều kiện hoặc function lồng nhau (giống như Hook thông thường).  

---

### 3. **Ví dụ về Custom Hook**
#### a) **Custom Hook `useFetch` để gọi API**
```tsx
import { useState, useEffect } from "react";

function useFetch(url: string) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    setLoading(true);
    fetch(url)
      .then((res) => {
        if (!res.ok) throw new Error("Network response was not ok");
        return res.json();
      })
      .then((data) => setData(data))
      .catch((error) => setError(error))
      .finally(() => setLoading(false));
  }, [url]);

  return { data, loading, error };
}
```
📌 **Sử dụng trong component:**
```tsx
function App() {
  const { data, loading, error } = useFetch("https://jsonplaceholder.typicode.com/posts");

  if (loading) return <p>Loading...</p>;
  if (error) return <p>Error: {error.message}</p>;

  return (
    <ul>
      {data.map((post) => (
        <li key={post.id}>{post.title}</li>
      ))}
    </ul>
  );
}
```
---

#### b) **Custom Hook `useLocalStorage` để lưu dữ liệu vào Local Storage**
```tsx
import { useState } from "react";

function useLocalStorage(key: string, initialValue: any) {
  const [storedValue, setStoredValue] = useState(() => {
    try {
      const item = window.localStorage.getItem(key);
      return item ? JSON.parse(item) : initialValue;
    } catch (error) {
      console.error(error);
      return initialValue;
    }
  });

  const setValue = (value: any) => {
    try {
      setStoredValue(value);
      window.localStorage.setItem(key, JSON.stringify(value));
    } catch (error) {
      console.error(error);
    }
  };

  return [storedValue, setValue];
}
```
📌 **Sử dụng trong component:**
```tsx
function Counter() {
  const [count, setCount] = useLocalStorage("count", 0);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increase</button>
    </div>
  );
}
```
---

### **Tổng kết**
✅ **Writing Custom Hooks giúp:**  
- Dễ dàng tái sử dụng logic giữa các component.  
- Tách biệt logic khỏi UI, giúp code sạch hơn.  
- Giảm sự phụ thuộc vào các patterns cũ như HOC hoặc Render Props.  

👉 Nếu bạn sử dụng React thường xuyên, viết Custom Hooks là kỹ năng quan trọng cần học! 🚀