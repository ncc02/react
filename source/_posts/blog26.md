---
title: <26> Suspense
date: 2025-03-07 09:14:33
tags:
---
## 1. **Tại sao Suspense nằm trong lộ trình React?**
Suspense là một trong những tính năng quan trọng trong lộ trình phát triển của React vì nó giúp quản lý trạng thái tải dữ liệu (loading state) một cách hiệu quả và tối ưu hóa hiệu suất. Mục tiêu chính của Suspense là:
- Giúp React xử lý **tải dữ liệu không đồng bộ** dễ dàng hơn.
- Cho phép **render từng phần của UI** thay vì chờ tất cả dữ liệu tải xong.
- Hỗ trợ **concurrent rendering** giúp UI mượt mà hơn.
- Giảm tải cho developer bằng cách **quản lý trạng thái tải** ngay trong cây component.

## 2. **Suspense là gì?**
Suspense là một cơ chế trong React cho phép trì hoãn hiển thị một phần của UI cho đến khi dữ liệu hoặc tài nguyên cần thiết sẵn sàng. Khi một component con **đang chờ dữ liệu**, React có thể hiển thị một fallback UI (thường là một loading spinner) thay vì để trang trống hoặc bị giật lag.

Hiện tại, **Suspense hỗ trợ chính cho React.lazy() và data fetching với React Server Components**. Trong tương lai, nó sẽ hỗ trợ cho các thư viện fetch dữ liệu như `React Query`, `Relay`, v.v.

---

## 3. **Ví dụ cơ bản về Suspense**
### 📌 **Ví dụ 1: Sử dụng Suspense với React.lazy()**
> **Lazy Loading Component**: Chỉ tải component khi cần thiết, giúp giảm dung lượng bundle ban đầu.

```tsx
import React, { Suspense, lazy } from 'react';

// Import component một cách lazy
const LazyComponent = lazy(() => import('./LazyComponent'));

export default function App() {
  return (
    <div>
      <h1>Ứng dụng React</h1>
      <Suspense fallback={<p>Đang tải component...</p>}>
        <LazyComponent />
      </Suspense>
    </div>
  );
}
```
📌 **Giải thích**:
- `lazy(() => import('./LazyComponent'))` giúp tách LazyComponent thành file JS riêng.
- `Suspense` với `fallback` đảm bảo khi component chưa tải xong, React sẽ hiển thị `Đang tải component...`.

---

### 📌 **Ví dụ 2: Sử dụng Suspense với Fetch Data (React 18 + React Server Components)**
> **Suspense giúp quản lý trạng thái tải dữ liệu tốt hơn mà không cần dùng useState + useEffect.**
```tsx
import { Suspense } from 'react';

// Fake API request bằng hàm delay
const fetchData = async () => {
  return new Promise(resolve => setTimeout(() => resolve("Dữ liệu từ API"), 3000));
};

// Component lấy dữ liệu
const DataComponent = async () => {
  const data = await fetchData();
  return <p>{data}</p>;
};

export default function App() {
  return (
    <div>
      <h1>Ứng dụng React với Suspense</h1>
      <Suspense fallback={<p>Đang tải dữ liệu...</p>}>
        <DataComponent />
      </Suspense>
    </div>
  );
}
```
📌 **Giải thích**:
- React sẽ **tạm dừng render** component `DataComponent` cho đến khi dữ liệu tải xong.
- Trong thời gian đó, React hiển thị **fallback UI** (`Đang tải dữ liệu...`).
- Giúp tránh tình trạng **"loading flash"** khi dữ liệu chưa sẵn sàng.

---

### 📌 **Ví dụ 3: Suspense với Streaming Server Components**
> Trong **Next.js 14 (App Router)**, Suspense có thể giúp streaming dữ liệu.
```tsx
import { Suspense } from 'react';
import Loading from './loading';

// Component tải dữ liệu nặng
const HeavyComponent = async () => {
  await new Promise(resolve => setTimeout(resolve, 3000));
  return <p>Component đã tải xong!</p>;
};

export default function Page() {
  return (
    <div>
      <h1>Trang sử dụng Streaming</h1>
      <Suspense fallback={<Loading />}>
        <HeavyComponent />
      </Suspense>
    </div>
  );
}
```
📌 **Lợi ích**:
- `Suspense` giúp Next.js **gửi trước phần UI sẵn sàng**, rồi **stream dữ liệu** từng phần về client.

---

## 4. **Khi nào nên dùng Suspense?**
✅ Khi muốn **lazy load component** để giảm kích thước bundle.  
✅ Khi muốn **quản lý loading state** mà không cần `useEffect`.  
✅ Khi sử dụng **React Server Components (RSC)** để tối ưu hiển thị dữ liệu.  
✅ Khi cần **stream dữ liệu** từng phần giúp UI tải nhanh hơn.

Bạn đang làm Next.js, nếu muốn áp dụng Suspense vào dự án của mình, có thể thử với React Server Components hoặc kết hợp với `react-query` để tối ưu hơn! 🚀