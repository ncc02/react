---
title: <21> API Calls - Axios
date: 2025-02-28 16:22:44
tags:
---
## 1. **Axios là gì?**  
Axios là một thư viện JavaScript dùng để gửi HTTP request từ trình duyệt hoặc Node.js. Nó hỗ trợ các phương thức như `GET`, `POST`, `PUT`, `DELETE`, giúp giao tiếp với API dễ dàng hơn. Axios được sử dụng phổ biến trong **React** để gọi API và lấy dữ liệu hiển thị trên giao diện.

## 2. **Tại sao Axios nằm trong lộ trình học React?**  
Trong React, dữ liệu thường được lấy từ API (RESTful API hoặc GraphQL) và hiển thị lên giao diện. Axios giúp React thực hiện việc này một cách đơn giản, dễ đọc, hỗ trợ:  
- **Tự động chuyển đổi JSON**: Axios tự động chuyển đổi dữ liệu nhận được thành JSON.  
- **Hỗ trợ async/await**: Axios dễ dàng kết hợp với `async/await` để xử lý dữ liệu bất đồng bộ.  
- **Quản lý lỗi tốt hơn**: Axios cung cấp cơ chế bắt lỗi (`catch()`) rõ ràng.  
- **Tích hợp token (Authorization)**: Axios dễ dàng cấu hình để gửi token xác thực khi gọi API.  

## 3. **Ví dụ về Axios trong React**  

### **Cài đặt Axios**
Trước tiên, cài đặt Axios bằng npm hoặc pnpm:
```bash
pnpm add axios
```
hoặc:
```bash
npm install axios
```

---

### **Ví dụ 1: Gửi yêu cầu GET để lấy dữ liệu**  
#### 🔹 Cách dùng Axios với `useEffect`
```jsx
import { useEffect, useState } from "react";
import axios from "axios";

const UserList = () => {
  const [users, setUsers] = useState([]);

  useEffect(() => {
    axios.get("https://jsonplaceholder.typicode.com/users")
      .then(response => {
        setUsers(response.data); // Lưu dữ liệu vào state
      })
      .catch(error => {
        console.error("Lỗi khi lấy dữ liệu:", error);
      });
  }, []);

  return (
    <div>
      <h2>Danh sách người dùng</h2>
      <ul>
        {users.map(user => (
          <li key={user.id}>{user.name} - {user.email}</li>
        ))}
      </ul>
    </div>
  );
};

export default UserList;
```
✅ Ở đây, `useEffect` giúp gọi API khi component được render.

---

### **Ví dụ 2: Gửi yêu cầu POST để thêm dữ liệu**  
#### 🔹 Cách dùng Axios với `async/await`
```jsx
import { useState } from "react";
import axios from "axios";

const AddUser = () => {
  const [name, setName] = useState("");

  const handleSubmit = async (e) => {
    e.preventDefault();
    try {
      const response = await axios.post("https://jsonplaceholder.typicode.com/users", {
        name: name
      });
      console.log("User added:", response.data);
    } catch (error) {
      console.error("Lỗi khi thêm người dùng:", error);
    }
  };

  return (
    <form onSubmit={handleSubmit}>
      <input 
        type="text" 
        value={name} 
        onChange={(e) => setName(e.target.value)} 
        placeholder="Nhập tên" 
      />
      <button type="submit">Thêm người dùng</button>
    </form>
  );
};

export default AddUser;
```
✅ Ở đây, `async/await` giúp code dễ đọc hơn khi gửi request `POST` đến API.

---

### **Ví dụ 3: Gửi yêu cầu DELETE để xóa dữ liệu**
```jsx
const deleteUser = async (id) => {
  try {
    await axios.delete(`https://jsonplaceholder.typicode.com/users/${id}`);
    console.log(`Đã xóa user có ID: ${id}`);
  } catch (error) {
    console.error("Lỗi khi xóa người dùng:", error);
  }
};

// Gọi hàm xóa user có ID = 3
deleteUser(3);
```
✅ Axios giúp việc gửi request DELETE trở nên đơn giản.

---

### **Kết luận**  
Axios là một thư viện mạnh mẽ giúp React gọi API dễ dàng. Nếu bạn muốn quản lý API tốt hơn, bạn có thể kết hợp Axios với **Redux Toolkit Query** hoặc **React Query** để tối ưu hóa hiệu suất. 🚀