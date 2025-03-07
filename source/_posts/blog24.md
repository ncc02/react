---
title: <24> Forms - React Hook Form
date: 2025-03-07 09:05:20
tags:
---
### 1. **Tại sao React Hook Form nằm trong lộ trình React?**  
React Hook Form là một thư viện giúp quản lý biểu mẫu (forms) trong React một cách tối ưu và dễ dàng. Nó nằm trong lộ trình học React vì:  

- **Tối ưu hiệu suất**: React Hook Form tối ưu hóa re-render, giúp form hoạt động nhanh hơn so với cách truyền thống.  
- **Tích hợp tốt với React Hooks**: Sử dụng `useForm` hook để quản lý trạng thái form.  
- **Hỗ trợ xác thực dễ dàng**: Có thể tích hợp với các thư viện như Yup hoặc Zod để kiểm tra dữ liệu đầu vào.  
- **Giảm code boilerplate**: Ít code hơn so với cách dùng `useState` hoặc `useReducer` để quản lý form.  

---

### 2. **React Hook Form là gì?**  
React Hook Form là một thư viện quản lý biểu mẫu (forms) cho React, được xây dựng dựa trên React Hooks. Nó giúp quản lý trạng thái, xác thực, và thu thập dữ liệu từ các input trong form một cách hiệu quả.  

👉 **Cài đặt thư viện**:  
```bash
pnpm add react-hook-form
```

---

### 3. **Ví dụ cơ bản**  

#### **Ví dụ 1: Form đơn giản**
```tsx
import { useForm } from "react-hook-form";

type FormData = {
  username: string;
  email: string;
};

export default function App() {
  const { register, handleSubmit } = useForm<FormData>();

  const onSubmit = (data: FormData) => {
    console.log(data);
  };

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <input {...register("username")} placeholder="Username" />
      <input {...register("email")} placeholder="Email" />
      <button type="submit">Submit</button>
    </form>
  );
}
```
✅ Khi người dùng submit form, dữ liệu được console log.  

---

#### **Ví dụ 2: Thêm xác thực dữ liệu**
```tsx
import { useForm } from "react-hook-form";

type FormData = {
  email: string;
  password: string;
};

export default function App() {
  const {
    register,
    handleSubmit,
    formState: { errors },
  } = useForm<FormData>();

  const onSubmit = (data: FormData) => {
    console.log(data);
  };

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <input
        {...register("email", { required: "Email không được để trống" })}
        placeholder="Email"
      />
      {errors.email && <p>{errors.email.message}</p>}

      <input
        {...register("password", {
          required: "Mật khẩu không được để trống",
          minLength: { value: 6, message: "Mật khẩu ít nhất 6 ký tự" },
        })}
        type="password"
        placeholder="Mật khẩu"
      />
      {errors.password && <p>{errors.password.message}</p>}

      <button type="submit">Đăng nhập</button>
    </form>
  );
}
```
✅ Nếu người dùng nhập sai, lỗi sẽ hiển thị ngay lập tức.  

---

#### **Ví dụ 3: Kết hợp với Yup để xác thực nâng cao**
```tsx
import { useForm } from "react-hook-form";
import { yupResolver } from "@hookform/resolvers/yup";
import * as yup from "yup";

const schema = yup.object({
  email: yup.string().email("Email không hợp lệ").required("Vui lòng nhập email"),
  password: yup.string().min(6, "Mật khẩu ít nhất 6 ký tự").required("Vui lòng nhập mật khẩu"),
});

type FormData = yup.InferType<typeof schema>;

export default function App() {
  const {
    register,
    handleSubmit,
    formState: { errors },
  } = useForm<FormData>({
    resolver: yupResolver(schema),
  });

  const onSubmit = (data: FormData) => {
    console.log(data);
  };

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <input {...register("email")} placeholder="Email" />
      {errors.email && <p>{errors.email.message}</p>}

      <input {...register("password")} type="password" placeholder="Mật khẩu" />
      {errors.password && <p>{errors.password.message}</p>}

      <button type="submit">Đăng nhập</button>
    </form>
  );
}
```
✅ Yup giúp viết validation ngắn gọn và dễ hiểu hơn.  

---

### 🔥 **Tóm lại**:
- React Hook Form giúp quản lý form dễ dàng, hiệu suất cao.  
- Hỗ trợ tích hợp với Yup/Zod để xác thực dữ liệu.  
- Code ngắn gọn hơn so với cách dùng `useState` để quản lý form.  

Bạn có cần thêm ví dụ nào khác không? 🚀