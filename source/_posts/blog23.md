---
title: <23> Testing - ViTest + React Testing Library + Playwright 
date: 2025-03-05 11:20:38
tags:
---

Vitest & Jest: Công cụ kiểm thử đơn vị (Unit Testing)
react-testing-library: Thư viện hỗ trợ kiểm thử React
Cypress & Playwright: Công cụ kiểm thử giao diện người dùng (E2E - End-to-End Testing)

---
### 1. Tại sao **Vitest** nằm trong lộ trình React?
**Vitest** là một thư viện dùng để kiểm thử (testing) trong JavaScript, đặc biệt phù hợp với **React** vì nó:
- Cung cấp cách viết **test đơn giản**, tương tự như Jest.
- Tích hợp tốt với **Vite**, công cụ build phổ biến trong hệ sinh thái React.
- Hỗ trợ kiểm thử **component React** nhanh hơn so với Jest nhờ tận dụng cơ chế **ESM + native browser**.
- Cho phép chạy test **song song (parallel) và thông minh hơn**, giúp tối ưu hiệu suất.

### 2. **Vitest là gì?**
**Vitest** là một thư viện test dành cho JavaScript/TypeScript, thường được sử dụng trong các dự án dùng **Vite**. Nó hỗ trợ kiểm thử **unit test, component test, mock function**, và có API tương tự như Jest.

Một số điểm nổi bật:
- Chạy test **nhanh** nhờ cơ chế caching và parallel execution.
- Tích hợp **TypeScript** mà không cần cấu hình phức tạp.
- Hỗ trợ **mocking/stubbing** tương tự như Jest.
- Dễ dàng kết hợp với các thư viện test UI như **Testing Library**.

---

### 3. **Ví dụ đơn giản về Vitest**
#### 3.1. Cài đặt Vitest trong dự án React
```sh
pnpm add vitest -D
```
Hoặc nếu dùng npm/yarn:
```sh
npm install vitest -D
# hoặc
yarn add vitest -D
```

#### 3.2. Cấu hình trong `package.json`
Thêm vào phần `scripts`:
```json
"scripts": {
  "test": "vitest"
}
```

#### 3.3. Viết test đơn giản với Vitest
##### **Ví dụ 1: Kiểm thử một hàm tính tổng**
```js
// sum.js
export function sum(a, b) {
  return a + b;
}
```

```js
// sum.test.js
import { describe, expect, test } from "vitest";
import { sum } from "./sum";

describe("sum function", () => {
  test("adds 1 + 2 to equal 3", () => {
    expect(sum(1, 2)).toBe(3);
  });
});
```

##### **Ví dụ 2: Kiểm thử component React**
```jsx
// Button.jsx
export function Button({ label, onClick }) {
  return <button onClick={onClick}>{label}</button>;
}
```

```jsx
// Button.test.jsx
import { render, screen, fireEvent } from "@testing-library/react";
import { describe, it, expect, vi } from "vitest";
import { Button } from "./Button";

describe("Button component", () => {
  it("renders correctly", () => {
    render(<Button label="Click me" />);
    expect(screen.getByText("Click me")).toBeInTheDocument();
  });

  it("handles click event", () => {
    const mockClick = vi.fn();
    render(<Button label="Click me" onClick={mockClick} />);
    fireEvent.click(screen.getByText("Click me"));
    expect(mockClick).toHaveBeenCalledTimes(1);
  });
});
```

#### 3.4. Chạy test
```sh
pnpm test
```
Hoặc:
```sh
npm test
```

---

### **Kết luận**
- **Vitest** là một lựa chọn mạnh mẽ cho React thay thế Jest, đặc biệt khi dùng với **Vite**.
- **Tốc độ nhanh, hỗ trợ TypeScript, tích hợp tốt với Testing Library**.
- Nếu dự án React của bạn dùng **Vite**, Vitest là một lựa chọn lý tưởng để kiểm thử.

Bạn muốn demo thêm về **mock API hoặc test hooks** không? 🚀
---
### 1. **Tại sao React Testing Library nằm trong lộ trình React?**
React Testing Library (RTL) là một thư viện giúp kiểm thử các thành phần UI trong React một cách trực quan và gần với cách người dùng thực sự tương tác. Nó nằm trong lộ trình React vì:  
- **Giúp kiểm thử giao diện hiệu quả**: RTL giúp đảm bảo các component hoạt động đúng bằng cách mô phỏng cách người dùng thực sự sử dụng ứng dụng.  
- **Tích hợp tốt với React**: RTL được thiết kế để làm việc mượt mà với các component React, giúp kiểm thử dễ dàng hơn.  
- **Hướng đến trải nghiệm người dùng**: RTL tập trung vào kiểm thử dựa trên hành vi người dùng thay vì kiểm tra trực tiếp các chi tiết triển khai.  
- **Khuyến khích kiểm thử tốt hơn**: Nó giúp viết test theo cách gần với thực tế hơn, tránh phụ thuộc vào các chi tiết nội bộ của component.  

---

### 2. **React Testing Library là gì?**
React Testing Library (RTL) là một thư viện kiểm thử dành cho React, giúp kiểm tra các component theo cách người dùng tương tác với chúng. Nó dựa trên [Testing Library](https://testing-library.com/) và được thiết kế để làm cho kiểm thử giao diện người dùng dễ dàng hơn mà không phụ thuộc quá nhiều vào implementation details.  

#### **Các đặc điểm chính của RTL:**
- Tập trung vào cách component hiển thị và hoạt động như người dùng thực sự.
- Không kiểm tra trực tiếp cấu trúc DOM hoặc state nội bộ.
- Sử dụng Jest để chạy test.
- Hỗ trợ kiểm tra các thao tác phổ biến như click, nhập văn bản, kiểm tra trạng thái của component.  

---

### 3. **Ví dụ đơn giản về React Testing Library**
#### **Cài đặt React Testing Library**
Nếu chưa cài đặt, bạn có thể thêm thư viện bằng lệnh:
```sh
pnpm add --save-dev @testing-library/react @testing-library/jest-dom
```

#### **Ví dụ 1: Kiểm tra xem một button có hiển thị đúng không**
Giả sử bạn có component `Button.tsx`:
```tsx
import React from "react";

const Button = ({ label }: { label: string }) => {
  return <button>{label}</button>;
};

export default Button;
```
Viết test cho `Button.tsx`:
```tsx
import { render, screen } from "@testing-library/react";
import Button from "./Button";

test("hiển thị đúng nội dung của button", () => {
  render(<Button label="Nhấn vào đây" />);
  const buttonElement = screen.getByText(/Nhấn vào đây/i);
  expect(buttonElement).toBeInTheDocument();
});
```

#### **Ví dụ 2: Kiểm tra sự kiện click**
Giả sử có một component `Counter.tsx`:
```tsx
import React, { useState } from "react";

const Counter = () => {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p data-testid="counter-value">Giá trị: {count}</p>
      <button onClick={() => setCount(count + 1)}>Tăng</button>
    </div>
  );
};

export default Counter;
```
Viết test để kiểm tra khi bấm vào nút "Tăng":
```tsx
import { render, screen, fireEvent } from "@testing-library/react";
import Counter from "./Counter";

test("tăng giá trị khi nhấn nút", () => {
  render(<Counter />);
  
  const buttonElement = screen.getByText(/Tăng/i);
  const counterValue = screen.getByTestId("counter-value");

  expect(counterValue).toHaveTextContent("Giá trị: 0");

  fireEvent.click(buttonElement);

  expect(counterValue).toHaveTextContent("Giá trị: 1");
});
```

---

### **Tóm tắt**
- **React Testing Library** giúp kiểm thử giao diện React theo cách gần giống với cách người dùng thực sự tương tác.
- RTL nằm trong lộ trình React vì nó hỗ trợ kiểm thử UI hiệu quả, giúp viết test tốt hơn.
- Các test sử dụng `render()`, `screen.getByText()`, `fireEvent.click()` để kiểm tra UI.
- Test tập trung vào hành vi thay vì chi tiết triển khai.

Bạn có muốn thêm ví dụ nào phức tạp hơn không? 🚀