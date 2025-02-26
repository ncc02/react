---
title: <6> Rendering - High Order Components
date: 2025-02-26 23:07:08
tags:
---
### 1. **Higher-Order Components vì sao nằm trong lộ trình React?**  
Higher-Order Components (HOC) nằm trong lộ trình React vì chúng từng là một trong những cách phổ biến để tái sử dụng logic giữa các component trước khi React Hooks ra đời (từ React 16.8). HOCs giúp:  
- Tránh trùng lặp logic trong nhiều component.  
- Tách biệt các concerns (separation of concerns).  
- Áp dụng các pattern như authorization, logging, hoặc fetching data mà không làm thay đổi cấu trúc của component gốc.  

Mặc dù HOCs không còn phổ biến như trước do sự ra đời của Hooks (useState, useEffect, useContext, v.v.), nhưng chúng vẫn xuất hiện trong nhiều codebase cũ và có thể hữu ích trong một số tình huống đặc biệt.

---

### 2. **Higher-Order Component là gì?**  
Higher-Order Component (HOC) là một **hàm** nhận vào một component và trả về một component mới có thêm logic hoặc props bổ sung. HOC giúp chia sẻ logic giữa các component mà không cần kế thừa.  

Công thức chung:  
```jsx
const withSomething = (WrappedComponent) => {
  return (props) => {
    // Thêm logic vào đây
    return <WrappedComponent {...props} />;
  };
};
```
HOCs được dùng để:  
- **Thêm quyền truy cập (Authorization)**
- **Kết nối với Redux**
- **Fetch data**
- **Thêm hiệu ứng (animation, logging, error handling, v.v.)**

---

### 3. **Ví dụ về Higher-Order Components**  

#### **Ví dụ 1: Thêm quyền truy cập (Authorization HOC)**  
```jsx
const withAuth = (WrappedComponent) => {
  return (props) => {
    if (!props.isLoggedIn) {
      return <p>Vui lòng đăng nhập</p>;
    }
    return <WrappedComponent {...props} />;
  };
};

const UserProfile = (props) => {
  return <h1>Xin chào, {props.username}!</h1>;
};

const ProtectedProfile = withAuth(UserProfile);

// Sử dụng:
<ProtectedProfile isLoggedIn={true} username="Cuongtk2002" />;
```

---

#### **Ví dụ 2: HOC để Fetch Data**  
```jsx
const withDataFetching = (WrappedComponent, url) => {
  return class extends React.Component {
    state = { data: null, loading: true };

    async componentDidMount() {
      const response = await fetch(url);
      const data = await response.json();
      this.setState({ data, loading: false });
    }

    render() {
      if (this.state.loading) return <p>Loading...</p>;
      return <WrappedComponent data={this.state.data} {...this.props} />;
    }
  };
};

// Component hiển thị dữ liệu
const UserList = ({ data }) => (
  <ul>
    {data.map((user) => (
      <li key={user.id}>{user.name}</li>
    ))}
  </ul>
);

// Tạo phiên bản mới của component với HOC
const UsersWithData = withDataFetching(UserList, "https://jsonplaceholder.typicode.com/users");

// Sử dụng:
<UsersWithData />;
```

---

### **So sánh HOC với React Hooks**
| HOC | React Hooks |
|------|------------|
| Dựa trên **hàm bậc cao** để bọc component | Dựa trên **hook** (`useEffect`, `useState`, v.v.) |
| Có thể gây **wrapper hell** (lồng nhiều HOC) | Code dễ đọc, ít lồng ghép |
| Dùng được với cả class component và functional component | Chỉ dùng với functional component |
| Thường dùng với Redux (`connect`) | Chủ yếu dùng với `useSelector`, `useDispatch` |

---

### **Khi nào dùng HOC thay vì Hooks?**
- Khi làm việc với **class component** (vì hooks chỉ dùng được với function component).
- Khi muốn **bọc nhiều component** với cùng một logic mà không viết lại hook nhiều lần.
- Khi cần kiểm soát việc **render hoặc chỉnh sửa component tree** (VD: lazy loading, logging, error boundaries).  

📌 **Tóm lại:** HOC là một kỹ thuật tái sử dụng code trong React, nhưng hiện tại hooks là phương pháp được khuyến khích hơn trong các dự án mới.