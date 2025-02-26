### 1. **Tại sao Refs lại cần cho roadmap React?**  
Refs là một phần quan trọng trong React vì chúng cung cấp một cách để truy cập trực tiếp vào DOM hoặc component con mà không cần thông qua props hay state. Trong roadmap React, việc hiểu và sử dụng Refs giúp bạn:  

- Quản lý focus text selection hoặc media playback (ví dụ: tự động focus vào input khi component mount).  
- Kích hoạt animations bằng cách thao tác trực tiếp trên DOM.  
- Tích hợp với thư viện bên ngoài (như thư viện chart, video player, v.v.) cần truy cập vào phần tử DOM.  
- Giữ giá trị không gây re-render (ví dụ: đếm số lần click mà không làm component render lại).  

---

### 2. **Refs là gì?**  
Refs (viết tắt của **references**) là một cách để truy cập DOM nodes hoặc React elements được tạo trong quá trình render. Trong React, refs được tạo bằng `useRef` (trong functional component) hoặc `createRef` (trong class component).  

---

### 3. **Ví dụ về Refs**  

#### **Ví dụ 1: Dùng `useRef` để focus vào input khi component mount**
```tsx
import { useEffect, useRef } from "react";

export default function AutoFocusInput() {
  const inputRef = useRef(null);

  useEffect(() => {
    inputRef.current.focus(); // Focus vào input khi component mount
  }, []);

  return <input ref={inputRef} placeholder="Nhập gì đó..." />;
}
```

#### **Ví dụ 2: Dùng `useRef` để lưu giá trị mà không làm re-render**
```tsx
import { useRef, useState } from "react";

export default function Counter() {
  const countRef = useRef(0);
  const [state, setState] = useState(0);

  const handleClick = () => {
    countRef.current += 1;
    console.log("Giá trị countRef:", countRef.current);
    setState(state + 1);
  };

  return (
    <div>
      <p>State: {state}</p>
      <p>Ref: {countRef.current}</p>
      <button onClick={handleClick}>Tăng</button>
    </div>
  );
}
```
📌 **Lưu ý:**  
- `countRef.current` thay đổi mà không gây re-render, trong khi `state` thay đổi sẽ khiến component render lại.  
- Điều này hữu ích khi bạn cần lưu trữ giá trị giữa các lần render nhưng không muốn re-render mỗi lần thay đổi.  

Refs là công cụ mạnh giúp React linh hoạt hơn, nhưng nên sử dụng đúng lúc để tránh phá vỡ quy tắc dataflow trong React. 🚀