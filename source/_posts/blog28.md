---
title: <28> Portals
date: 2025-03-07 09:31:38
tags:
---
### 1. **Portals là gì?**
Portals trong React là một cơ chế cho phép bạn render một phần tử con (child) ra bên ngoài cây DOM của phần tử cha (parent) mà không phá vỡ hệ thống React reconciliation. Điều này hữu ích khi bạn cần hiển thị một phần tử ở một vị trí khác trong DOM, nhưng vẫn giữ được tính năng quản lý trạng thái của React.

Portals thường được sử dụng để render **modals, tooltips, dropdowns**, nơi mà bạn muốn chúng xuất hiện ở một vị trí khác trên cây DOM (ví dụ: trong `<body>`) để tránh vấn đề **CSS overflow, z-index, clipping**.

---

### 2. **Tại sao Portals lại nằm trong lộ trình React?**
Portals giúp giải quyết một số vấn đề quan trọng trong UI, đặc biệt khi làm việc với các phần tử cần hiển thị trên cùng một tầng cao hơn so với vị trí logic của chúng trong cây component. Một số lý do chính:
- **Giúp tránh vấn đề CSS clipping**: Nếu bạn đặt một modal bên trong một phần tử có `overflow: hidden`, modal có thể bị cắt mất. Portals giúp đưa modal ra ngoài để hiển thị đúng cách.
- **Tăng khả năng kiểm soát UI**: Bạn có thể đặt các thành phần như tooltips, popups, modals vào `<body>` thay vì bị giới hạn trong một component cụ thể.
- **Giữ nguyên trạng thái React**: Mặc dù được render ở một vị trí khác trong DOM, nhưng các sự kiện và trạng thái của component vẫn hoạt động như bình thường.

---

### 3. **Ví dụ đơn giản về Portals**
#### 🟢 **Ví dụ 1: Tạo một modal đơn giản với Portals**
```tsx
import React from "react";
import ReactDOM from "react-dom";

const Modal = ({ isOpen, onClose }) => {
  if (!isOpen) return null;

  return ReactDOM.createPortal(
    <div style={styles.overlay}>
      <div style={styles.modal}>
        <h2>Đây là một Modal</h2>
        <p>Nội dung của modal nằm ngoài cây DOM của component cha.</p>
        <button onClick={onClose}>Đóng</button>
      </div>
    </div>,
    document.getElementById("modal-root") // Render ra ngoài #modal-root
  );
};

const styles = {
  overlay: {
    position: "fixed",
    top: 0,
    left: 0,
    width: "100vw",
    height: "100vh",
    background: "rgba(0, 0, 0, 0.5)",
    display: "flex",
    justifyContent: "center",
    alignItems: "center",
  },
  modal: {
    background: "white",
    padding: "20px",
    borderRadius: "8px",
  },
};

const App = () => {
  const [isOpen, setIsOpen] = React.useState(false);

  return (
    <div>
      <h1>Trang chính</h1>
      <button onClick={() => setIsOpen(true)}>Mở Modal</button>
      <Modal isOpen={isOpen} onClose={() => setIsOpen(false)} />
    </div>
  );
};

export default App;
```
📝 **Lưu ý**: Bạn cần thêm một phần tử `<div id="modal-root"></div>` trong `index.html` để Portals render đúng vị trí.

---

#### 🟢 **Ví dụ 2: Tooltip sử dụng Portals**
```tsx
import React from "react";
import ReactDOM from "react-dom";

const Tooltip = ({ text, targetRef }) => {
  if (!targetRef.current) return null;

  const { top, left, width } = targetRef.current.getBoundingClientRect();
  return ReactDOM.createPortal(
    <div
      style={{
        position: "absolute",
        top: top - 30,
        left: left + width / 2,
        background: "black",
        color: "white",
        padding: "5px 10px",
        borderRadius: "4px",
        whiteSpace: "nowrap",
      }}
    >
      {text}
    </div>,
    document.body
  );
};

const App = () => {
  const buttonRef = React.useRef(null);
  const [showTooltip, setShowTooltip] = React.useState(false);

  return (
    <div style={{ padding: "100px" }}>
      <button
        ref={buttonRef}
        onMouseEnter={() => setShowTooltip(true)}
        onMouseLeave={() => setShowTooltip(false)}
      >
        Di chuột vào tôi
      </button>
      {showTooltip && <Tooltip text="Đây là tooltip" targetRef={buttonRef} />}
    </div>
  );
};

export default App;
```

---

### 🔥 **Khi nào nên dùng Portals?**
✅ Khi bạn cần:
- Hiển thị **modals, dialogs, popups** trên toàn màn hình.
- Render **dropdowns hoặc tooltips** nằm ngoài giới hạn của component cha.
- Giải quyết vấn đề **z-index và clipping** trong CSS.

❌ Không cần thiết nếu:
- Bạn không gặp vấn đề về vị trí render trong cây DOM.
- Nội dung vẫn hiển thị đúng mà không cần tách ra ngoài component cha.

---

### **Tóm lại**
- **Portals** giúp render component ra ngoài cây DOM hiện tại mà vẫn giữ được logic của React.
- Được sử dụng phổ biến trong **modals, tooltips, dropdowns** để tránh các vấn đề về CSS.
- Cú pháp chính:  
  ```tsx
  ReactDOM.createPortal(element, targetNode)
  ```
- Portals giúp **giữ vững nguyên tắc của React**, nhưng **cải thiện khả năng hiển thị UI**.

Bạn đã từng gặp trường hợp nào cần dùng Portals chưa? 🚀