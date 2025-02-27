---
title: <14> Hooks - useMemo Hook (Advance Hook)
date: 2025-02-27 09:42:24
tags:
---
## 1. **Tại sao `useMemo` nằm trong lộ trình React?**  
`useMemo` là một hook trong React giúp tối ưu hiệu suất bằng cách ghi nhớ (memoize) kết quả của một hàm tính toán tốn kém. Nó nằm trong lộ trình React vì:  

- Giúp tránh việc tính toán lại các giá trị không cần thiết khi component re-render.  
- Cải thiện hiệu suất khi làm việc với dữ liệu lớn hoặc tính toán phức tạp.  
- Hữu ích khi truyền giá trị xuống các component con để tránh re-render không mong muốn.  

## 2. **`useMemo` là gì?**  
`useMemo` là một hook giúp tối ưu hiệu suất bằng cách ghi nhớ giá trị trả về của một hàm và chỉ tính toán lại khi dependencies thay đổi.  

Cú pháp:  
```tsx
const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);
```
- `computeExpensiveValue(a, b)`: Hàm tính toán tốn kém.  
- `[a, b]`: Danh sách dependencies, chỉ khi `a` hoặc `b` thay đổi, `useMemo` mới thực hiện tính toán lại.  
- `memoizedValue`: Giá trị đã được memoize (ghi nhớ).  

---

## 3. **Ví dụ về `useMemo`**

### **Ví dụ 1: Tối ưu tính toán số lớn**
```tsx
import { useState, useMemo } from "react";

function ExpensiveCalculation({ number }) {
  const squaredNumber = useMemo(() => {
    console.log("Tính toán lại...");
    return number ** 2;
  }, [number]);

  return <p>Kết quả: {squaredNumber}</p>;
}

export default function App() {
  const [count, setCount] = useState(0);
  const [number, setNumber] = useState(2);

  return (
    <div>
      <button onClick={() => setCount(count + 1)}>Tăng count: {count}</button>
      <button onClick={() => setNumber(number + 1)}>Tăng number: {number}</button>
      <ExpensiveCalculation number={number} />
    </div>
  );
}
```
**Giải thích:**  
- Khi nhấn tăng `count`, `number` không thay đổi → `useMemo` giúp không cần tính toán lại số bình phương.  
- Khi `number` thay đổi, chỉ lúc đó hàm tính toán mới được gọi lại.  

---

### **Ví dụ 2: Tránh re-render không cần thiết khi truyền props**
```tsx
import { useState, useMemo } from "react";

function ChildComponent({ data }) {
  console.log("ChildComponent re-render");
  return <p>{data.value}</p>;
}

export default function ParentComponent() {
  const [count, setCount] = useState(0);
  const memoizedData = useMemo(() => ({ value: "Dữ liệu memoized" }), []);

  return (
    <div>
      <button onClick={() => setCount(count + 1)}>Tăng count: {count}</button>
      <ChildComponent data={memoizedData} />
    </div>
  );
}
```
**Giải thích:**  
- Nếu không dùng `useMemo`, mỗi lần `count` thay đổi, object `data` mới sẽ được tạo, khiến `ChildComponent` re-render.  
- Với `useMemo`, object `data` không thay đổi trừ khi dependencies thay đổi (ở đây là `[]`, nghĩa là không bao giờ thay đổi).  

---

## 4. **Khi nào nên dùng `useMemo`?**  
- Khi có **tính toán phức tạp** cần tối ưu hiệu suất.  
- Khi truyền **props dạng object, array** vào component con để tránh re-render không cần thiết.  
- Khi làm việc với **dữ liệu lớn hoặc xử lý danh sách** như filter, sort, map.  

**Lưu ý:** Không nên lạm dụng `useMemo` vì có thể làm code phức tạp hơn mà không mang lại lợi ích đáng kể.