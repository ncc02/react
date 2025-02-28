---
title: <16> Routers - React Router
date: 2025-02-28 11:26:46
tags:
---
React Router là một thư viện định tuyến được thiết kế dành riêng cho các ứng dụng React. Nó cho phép bạn xây dựng các ứng dụng dạng Single Page Application (SPA) với khả năng chuyển đổi giữa các “trang” (view) mà không cần tải lại toàn bộ trang web. Đây là một trong những công cụ cơ bản trong lộ trình học React vì nó giúp quản lý điều hướng (routing) trong ứng dụng, tạo ra trải nghiệm người dùng mượt mà và nhất quán.

---

## Tại sao React Router nằm trong lộ trình React?

- **Quản lý định tuyến trong SPA:** Ứng dụng React thường là các SPA, nghĩa là toàn bộ ứng dụng được tải một lần. Việc điều hướng giữa các phần khác nhau của ứng dụng (tương ứng với các URL khác nhau) đòi hỏi một giải pháp định tuyến hiệu quả. React Router giải quyết vấn đề này bằng cách ánh xạ URL tới các component tương ứng mà không cần reload trang, giúp cải thiện hiệu năng và trải nghiệm người dùng. citeturn0search0

- **Phân tách giao diện theo component:** React khuyến khích chia giao diện thành các component nhỏ và tái sử dụng. React Router giúp liên kết các component đó với các đường dẫn (routes) cụ thể, từ đó tổ chức cấu trúc ứng dụng rõ ràng và dễ bảo trì. citeturn0search1

- **Kỹ năng thiết yếu cho developer React:** Hầu hết các ứng dụng React hiện đại đều cần có khả năng điều hướng linh hoạt. Do đó, nắm vững React Router là một bước quan trọng trong việc trở thành một developer React chuyên nghiệp. citeturn0search3

---

## React Router là gì?

React Router là một thư viện cung cấp các công cụ để định tuyến (routing) trong ứng dụng React. Cụ thể:

- **BrowserRouter:** Thành phần bao bọc toàn bộ ứng dụng để đồng bộ URL trên trình duyệt với trạng thái của ứng dụng.  
- **Routes & Route:** Cho phép khai báo các tuyến đường, ánh xạ giữa URL và các component cần render.  
- **Link & NavLink:** Giúp tạo liên kết điều hướng giữa các trang mà không làm tải lại trang.  
- **Hooks như useParams và useNavigate:** Cho phép truy xuất các tham số từ URL và điều hướng một cách linh hoạt qua code.

Nhờ vào những tính năng này, React Router giúp việc chuyển đổi giữa các “trang” trong ứng dụng trở nên dễ dàng và trực quan. citeturn0search8

---

## Một số ví dụ về React Router

### Ví dụ 1: Cấu hình định tuyến cơ bản

```jsx
import { BrowserRouter, Routes, Route } from 'react-router-dom';
import Home from './Home';
import About from './About';

function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
      </Routes>
    </BrowserRouter>
  );
}

export default App;
```

Trong ví dụ này, khi người dùng truy cập vào đường dẫn “/” thì component `Home` sẽ được hiển thị, và khi truy cập “/about” thì component `About` sẽ xuất hiện.

---

### Ví dụ 2: Sử dụng Link để điều hướng

```jsx
import { Link } from 'react-router-dom';

function Navbar() {
  return (
    <nav>
      <Link to="/">Trang Chủ</Link>
      <Link to="/about">Giới Thiệu</Link>
    </nav>
  );
}

export default Navbar;
```

Ở đây, thay vì dùng thẻ `<a>`, sử dụng `<Link>` giúp điều hướng mà không làm tải lại trang, giữ cho trải nghiệm người dùng mượt mà. citeturn0search7

---

### Ví dụ 3: Lấy tham số từ URL với useParams

```jsx
import { useParams } from 'react-router-dom';

function UserDetail() {
  const { id } = useParams();
  return <div>Thông tin người dùng có ID: {id}</div>;
}

export default UserDetail;
```

Ví dụ này minh họa cách sử dụng hook `useParams` để lấy các tham số động từ URL (ví dụ: `/user/123` sẽ trả về id là 123). citeturn0search8

---

Dưới đây là một ví dụ đơn giản về cách sử dụng hook **useNavigate** trong React Router (v6):

```jsx
import { useNavigate } from 'react-router-dom';

function Login() {
  const navigate = useNavigate();

  const handleLogin = () => {
    // Giả sử đăng nhập thành công, chuyển hướng người dùng đến trang dashboard
    navigate('/dashboard');
  };

  return (
    <div>
      <h2>Đăng nhập</h2>
      <button onClick={handleLogin}>Đăng nhập ngay</button>
    </div>
  );
}

export default Login;
```

**Giải thích:**

- **useNavigate:** Hook này trả về một hàm dùng để điều hướng chương trình. Bạn có thể gọi hàm này và truyền vào đường dẫn mới mà bạn muốn chuyển đến.
- Trong ví dụ trên, khi người dùng nhấn vào nút "Đăng nhập ngay", hàm `handleLogin` được gọi và thực hiện chuyển hướng tới đường dẫn `/dashboard`.

Việc sử dụng useNavigate giúp bạn điều hướng từ code mà không cần phải sử dụng thành phần `<Link>` hay `<NavLink>`. Đây là một công cụ hữu ích khi bạn muốn chuyển hướng sau một hành động như đăng nhập, gửi form hay các thao tác tương tự. citeturn0search8


Dưới đây là một ví dụ nâng cao sử dụng hook **useParams** để lấy nhiều tham số từ URL, ví dụ về trang chi tiết sản phẩm:

**Cấu hình định tuyến (App.js):**

```jsx
import { BrowserRouter, Routes, Route } from 'react-router-dom';
import Home from './Home';
import ProductDetail from './ProductDetail';

function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/" element={<Home />} />
        {/* Đường dẫn chứa 2 tham số: categoryId và productId */}
        <Route path="/category/:categoryId/product/:productId" element={<ProductDetail />} />
      </Routes>
    </BrowserRouter>
  );
}

export default App;
```

**Component ProductDetail (ProductDetail.js):**

```jsx
import React from 'react';
import { useParams } from 'react-router-dom';

function ProductDetail() {
  // useParams trả về đối tượng chứa các tham số lấy từ URL
  const { categoryId, productId } = useParams();

  return (
    <div>
      <h2>Chi tiết sản phẩm</h2>
      <p>Danh mục: {categoryId}</p>
      <p>Mã sản phẩm: {productId}</p>
    </div>
  );
}

export default ProductDetail;
```

**Giải thích:**

- Khi người dùng truy cập vào URL như `/category/electronics/product/123`, hook **useParams** sẽ trả về đối tượng:  
  `{ categoryId: 'electronics', productId: '123' }`  
- Dựa vào các tham số này, component `ProductDetail` có thể hiển thị thông tin cụ thể về sản phẩm dựa trên danh mục và mã sản phẩm. citeturn0search8


Nhìn chung, việc nắm vững React Router là một phần không thể thiếu trong lộ trình học React, giúp bạn xây dựng các ứng dụng web hiện đại với khả năng điều hướng linh hoạt và trải nghiệm người dùng tốt hơn.