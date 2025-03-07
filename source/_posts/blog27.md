---
title: <27> Error Boundaries
date: 2025-03-07 09:24:45
tags:
---
### 1. **Error Boundaries tại sao lại nằm trong lộ trình React?**
Error Boundaries nằm trong lộ trình React vì:
- **Xử lý lỗi ở Component Tree**: React không có cơ chế mặc định để bắt lỗi JavaScript bên trong các component con. Nếu một component con gặp lỗi trong vòng đời của nó, lỗi đó có thể làm sập toàn bộ ứng dụng.
- **Cải thiện trải nghiệm người dùng**: Thay vì để trang trắng hoặc crash toàn bộ ứng dụng, Error Boundaries giúp hiển thị UI dự phòng (fallback UI).
- **Debug dễ hơn**: Error Boundaries giúp log lỗi chính xác, giúp developer dễ dàng theo dõi và sửa chữa vấn đề.

---

### 2. **Error Boundaries là gì?**
Error Boundaries (Biên Giới Lỗi) là các React component đặc biệt có thể bắt lỗi JavaScript xảy ra trong quá trình render, lifecycle methods, hoặc các component con. Error Boundaries sử dụng các lifecycle methods sau:
- `static getDerivedStateFromError(error)`: Cập nhật state để hiển thị UI dự phòng khi có lỗi.
- `componentDidCatch(error, info)`: Ghi log lỗi.

> **Lưu ý**: Error Boundaries **chỉ bắt lỗi trong render, lifecycle methods, nhưng không bắt lỗi trong event handlers, asynchronous code (setTimeout, fetch, Promise), hoặc lỗi xảy ra bên ngoài React.**

---

### 3. **Ví dụ về Error Boundaries cơ bản**
#### 🔹 **Tạo một Error Boundary component**
```tsx
import React, { Component, ErrorInfo } from "react";

class ErrorBoundary extends Component<{ children: React.ReactNode }, { hasError: boolean }> {
  constructor(props: any) {
    super(props);
    this.state = { hasError: false };
  }

  static getDerivedStateFromError(error: Error) {
    return { hasError: true };
  }

  componentDidCatch(error: Error, errorInfo: ErrorInfo) {
    console.error("Error caught by ErrorBoundary:", error, errorInfo);
  }

  render() {
    if (this.state.hasError) {
      return <h2>Đã xảy ra lỗi! Vui lòng thử lại.</h2>;
    }
    return this.props.children;
  }
}

export default ErrorBoundary;
```

#### 🔹 **Sử dụng Error Boundary trong ứng dụng**
```tsx
import React, { useState } from "react";
import ErrorBoundary from "./ErrorBoundary";

const BuggyComponent = () => {
  const [crash, setCrash] = useState(false);

  if (crash) {
    throw new Error("Component này bị lỗi!");
  }

  return <button onClick={() => setCrash(true)}>Gây lỗi</button>;
};

export default function App() {
  return (
    <ErrorBoundary>
      <BuggyComponent />
    </ErrorBoundary>
  );
}
```
**🔹 Kết quả:**  
- Ban đầu, ứng dụng hiển thị nút "Gây lỗi".
- Khi nhấn nút, component `BuggyComponent` gặp lỗi, `ErrorBoundary` sẽ bắt lỗi và hiển thị UI fallback: `"Đã xảy ra lỗi! Vui lòng thử lại."`

---

### 4. **Khi nào nên dùng Error Boundaries?**
- **Bọc toàn bộ ứng dụng** để tránh crash toàn bộ UI.
- **Bọc các component quan trọng** như sidebar, navbar, form...
- **Khi tích hợp API của bên thứ ba** có thể xảy ra lỗi khi fetch dữ liệu.

---

### 5. **Error Boundaries có bắt được lỗi không?**
| Trường hợp | Error Boundaries có bắt lỗi không? |
|------------|--------------------------------|
| Render component | ✅ Có |
| Lifecycle methods | ✅ Có |
| Sự kiện (onClick, onChange...) | ❌ Không |
| setTimeout, fetch, Promise | ❌ Không |
| Lỗi trong React Hooks | ✅ Có (nếu xảy ra trong render) |

> **Mẹo**: Với event handler hoặc async code, hãy dùng `try/catch` hoặc `.catch()` để xử lý lỗi.

---

### **Tóm tắt**
- **Error Boundaries giúp React ứng dụng không bị crash toàn bộ khi có lỗi trong component.**
- **Dùng Error Boundaries để hiển thị UI fallback thay vì để lỗi làm sập ứng dụng.**
- **Chỉ áp dụng cho lỗi trong render và lifecycle, không áp dụng cho sự kiện hay async code.**
- **Error Boundaries nên được bọc ở cấp độ cao hoặc quanh các component quan trọng.**

Bạn có cần thêm ví dụ nâng cao về Error Boundaries không? 🚀