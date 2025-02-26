---
title: <1> Rendering - Component Life Cycle
date: 2025-02-26 14:14:48
tags:
---


Trong đoạn code này:  
```tsx
useEffect(() => {
  console.log("Component mounted");

  return () => {
    console.log("Component unmounted"); // Chạy khi component bị unmount
  };
}, []);
```
👉 **"Component unmounted" sẽ được log khi component bị gỡ khỏi DOM.**

---

## **Khi nào component sẽ bị unmount?**
### **1️⃣ Khi component bị ẩn (Conditional Rendering)**
Ví dụ, nếu bạn có một nút để ẩn hiện component:
```tsx
import { useState } from "react";
import Counter from "./Counter";

const App = () => {
  const [show, setShow] = useState(true);

  return (
    <div>
      <button onClick={() => setShow(!show)}>Toggle Counter</button>
      {show && <Counter />}
    </div>
  );
};

export default App;
```
- Khi **App render lần đầu**, `Counter` được mount → log `"Component mounted"`.
- Khi bạn **nhấn nút Toggle để ẩn Counter**, component bị unmount → log `"Component unmounted"`.

---

### **2️⃣ Khi component bị thay thế bởi component khác**
Ví dụ, thay vì ẩn, ta thay `Counter` bằng một component khác:
```tsx
const App = () => {
  const [showFirst, setShowFirst] = useState(true);

  return (
    <div>
      <button onClick={() => setShowFirst(!showFirst)}>Switch Component</button>
      {showFirst ? <Counter /> : <AnotherComponent />}
    </div>
  );
};
```
- Khi chuyển từ `Counter` sang `AnotherComponent`, component `Counter` bị unmount → log `"Component unmounted"`.

---

### **3️⃣ Khi chuyển trang trong Next.js hoặc React Router**
Nếu bạn có một trang `/about` chứa `Counter`, khi chuyển sang trang khác (`/home`), `Counter` sẽ bị unmount:
```tsx
import { useEffect } from "react";

const About = () => {
  useEffect(() => {
    console.log("Component mounted");

    return () => {
      console.log("Component unmounted");
    };
  }, []);

  return <h1>About Page</h1>;
};

export default About;
```
**Nếu bạn chuyển từ `/about` sang `/home`, component `About` sẽ bị unmount và log `"Component unmounted"`**.

---

### **4️⃣ Khi React Strict Mode gây double mount/unmount (trong development)**
Nếu bạn đang dùng **React 18 với `StrictMode` trong `main.tsx` hoặc `_app.tsx`**, bạn có thể thấy `"Component mounted"` **2 lần** và `"Component unmounted"` **1 lần**.  
📌 Điều này chỉ xảy ra trong **development mode** để giúp phát hiện lỗi tiềm ẩn:
```tsx
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App";

ReactDOM.createRoot(document.getElementById("root")!).render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
```
👉 **Khi chạy ứng dụng trong development**, React mount rồi unmount ngay lập tức để kiểm tra side effects.

---

## **Tóm tắt**
🟢 `"Component mounted"` chạy khi component được render lần đầu.  
🔴 `"Component unmounted"` chạy khi:
1. Component bị ẩn (bị loại khỏi DOM).
2. Component bị thay thế bởi component khác.
3. Chuyển trang trong React Router / Next.js.
4. **React Strict Mode** chạy trong development (gây double mount/unmount).

🚀 Bạn có thể thử với `console.log` hoặc đặt một `alert()` để dễ kiểm tra hơn.