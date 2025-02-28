---
title: <22> API Calls - React Query
date: 2025-02-28 16:31:47
tags:
---
### 1. **Tại sao React Query nằm trong lộ trình React?**  
React Query nằm trong lộ trình học React vì nó giúp quản lý trạng thái dữ liệu bất đồng bộ (async state) trong ứng dụng React một cách hiệu quả. Mặc dù React đã có state management bằng `useState` và `useReducer`, nhưng chúng không phù hợp để quản lý dữ liệu từ API vì:  
- Dữ liệu từ API cần caching, revalidation, pagination, refetching, v.v.  
- `useState` không thể tự động refetch khi dữ liệu thay đổi.  
- Redux/Context API có thể giúp lưu trữ dữ liệu, nhưng việc fetch API và caching vẫn phải tự xử lý.  

React Query giúp giải quyết những vấn đề này bằng cách:  
- **Tự động caching** dữ liệu API.  
- **Refetching thông minh** khi dữ liệu cần cập nhật.  
- **Xử lý background fetching**, giảm số lần gọi API không cần thiết.  
- **Quản lý trạng thái tải, lỗi, thành công** dễ dàng.  

---

### 2. **React Query là gì?**  
React Query là một thư viện giúp quản lý dữ liệu bất đồng bộ trong React, chủ yếu là dữ liệu từ API. Nó giúp tối ưu hóa việc fetch, caching, synchronizing và updating dữ liệu với rất ít code.  

📌 **Cài đặt:**  
```sh
pnpm add @tanstack/react-query
```

📌 **Khởi tạo React Query:**
```tsx
import { QueryClient, QueryClientProvider } from "@tanstack/react-query";

// Tạo một instance của QueryClient
const queryClient = new QueryClient();

export default function App() {
  return (
    <QueryClientProvider client={queryClient}>
      <MyComponent />
    </QueryClientProvider>
  );
}
```

---

### 3. **Ví dụ về React Query**  
#### 🟢 **Fetch danh sách users từ API**  
```tsx
import { useQuery } from "@tanstack/react-query";
import axios from "axios";

const fetchUsers = async () => {
  const { data } = await axios.get("https://jsonplaceholder.typicode.com/users");
  return data;
};

export default function Users() {
  const { data, isLoading, error } = useQuery({
    queryKey: ["users"],
    queryFn: fetchUsers,
  });

  if (isLoading) return <p>Loading...</p>;
  if (error) return <p>Error: {error.message}</p>;

  return (
    <ul>
      {data.map((user) => (
        <li key={user.id}>{user.name}</li>
      ))}
    </ul>
  );
}
```

---

#### 🟢 **Mutations: Tạo user mới**  
React Query hỗ trợ **mutation** để cập nhật dữ liệu server-side (POST, PUT, DELETE).  
```tsx
import { useMutation, useQueryClient } from "@tanstack/react-query";
import axios from "axios";

const createUser = async (user) => {
  const { data } = await axios.post("https://jsonplaceholder.typicode.com/users", user);
  return data;
};

export default function AddUser() {
  const queryClient = useQueryClient();
  const mutation = useMutation({
    mutationFn: createUser,
    onSuccess: () => {
      queryClient.invalidateQueries({ queryKey: ["users"] });
    },
  });

  return (
    <button
      onClick={() => mutation.mutate({ name: "New User" })}
      disabled={mutation.isPending}
    >
      {mutation.isPending ? "Adding..." : "Add User"}
    </button>
  );
}
```
✅ **Giải thích:**  
- `useMutation` dùng để thực hiện hành động thay đổi dữ liệu.  
- `onSuccess` giúp **refetch lại danh sách users** sau khi thêm mới thành công.  

---

### 4. **Lợi ích của React Query**  
✅ **Tự động caching** dữ liệu từ API để giảm số lần gọi API.  
✅ **Hỗ trợ pagination, infinite scrolling** dễ dàng.  
✅ **Tối ưu hiệu suất** với background fetching.  
✅ **Giảm code phức tạp** khi xử lý dữ liệu API.  

Bạn có muốn ví dụ về pagination hoặc infinite scroll không? 🚀