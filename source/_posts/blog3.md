---
title: <3> Rendering - Render Props
date: 2025-02-26 16:49:16
tags:
---
Dưới đây là **hai cách tiếp cận** để giải quyết cùng một bài toán: **theo dõi vị trí chuột**  
- Cách **1: Sử dụng Render Props**  
- Cách **2: Sử dụng React Hook (`useState`, `useEffect`)**  

---

## ✅ **Cách 1: Dùng Render Props**
Dùng Render Props để truyền logic về vị trí chuột cho component con.

```jsx
import { useState } from "react";

function MouseTracker({ render }) {
  const [position, setPosition] = useState({ x: 0, y: 0 });

  const handleMouseMove = (event) => {
    setPosition({ x: event.clientX, y: event.clientY });
  };

  return (
    <div style={{ height: "200px", border: "1px solid black" }} onMouseMove={handleMouseMove}>
      {render(position)}
    </div>
  );
}

function App() {
  return (
    <MouseTracker
      render={({ x, y }) => (
        <h2>Mouse position: ({x}, {y})</h2>
      )}
    />
  );
}

export default App;
```

### 🔹 **Giải thích cách hoạt động**
- `MouseTracker` quản lý vị trí chuột và gọi `render(position)`, truyền dữ liệu xuống component con.
- Component `App` có thể quyết định cách hiển thị dữ liệu mà không cần thay đổi logic bên trong `MouseTracker`.

---

## ✅ **Cách 2: Dùng Hook (`useState` + `useEffect`)**
Dùng Hook để quản lý logic **ngay trong component**, giúp code đơn giản hơn.

```jsx
import { useState, useEffect } from "react";

function useMousePosition() {
  const [position, setPosition] = useState({ x: 0, y: 0 });

  useEffect(() => {
    const handleMouseMove = (event) => {
      setPosition({ x: event.clientX, y: event.clientY });
    };

    window.addEventListener("mousemove", handleMouseMove);
    return () => {
      window.removeEventListener("mousemove", handleMouseMove);
    };
  }, []);

  return position;
}

function App() {
  const { x, y } = useMousePosition();

  return <h2>Mouse position: ({x}, {y})</h2>;
}

export default App;
```

### 🔹 **Giải thích cách hoạt động**
- **Hook `useMousePosition`** quản lý state vị trí chuột và cập nhật nó khi con trỏ di chuyển.
- **Component `App`** chỉ cần gọi `useMousePosition()` để lấy vị trí chuột, không cần truyền function như Render Props.

---

## 🆚 **So sánh Render Props vs Hook**
| Tiêu chí | Render Props | Hook (`useState` + `useEffect`) |
|----------|-------------|------------------------------|
| **Độ phức tạp** | Cồng kềnh do cần truyền function `render` | Ngắn gọn, dễ đọc |
| **Khả năng tái sử dụng** | Có thể tái sử dụng, nhưng phức tạp hơn | Dễ tái sử dụng với Custom Hook |
| **Hiệu suất** | Có thể gây re-render không cần thiết | Tối ưu hơn do sử dụng `useEffect` |

---

## 🎯 **Khi nào nên dùng cái nào?**
- ✅ **Dùng Hooks** khi muốn code đơn giản, dễ hiểu và tối ưu hiệu suất.
- ✅ **Dùng Render Props** nếu cần linh hoạt thay đổi giao diện dựa trên dữ liệu mà không làm thay đổi component cha.

💡 **Tóm lại:** Render Props là cách tiếp cận cũ nhưng vẫn hữu ích trong một số trường hợp. Tuy nhiên, **Hooks là cách tiếp cận hiện đại hơn** và thường được ưu tiên trong các dự án React hiện nay.