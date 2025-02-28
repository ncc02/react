---
title: <19> Component/Libraries - Material UI 
date: 2025-02-28 15:16:13
tags:
---
### **1. Material UI tại sao nằm trong lộ trình React?**  
Material UI (MUI) nằm trong lộ trình React vì đây là một thư viện giao diện người dùng phổ biến, được thiết kế để giúp các lập trình viên xây dựng giao diện đẹp mắt, nhất quán và tuân theo Material Design của Google. Một số lý do khiến MUI quan trọng trong hệ sinh thái React:  
- **Tối ưu hóa cho React**: Được xây dựng bằng React, giúp dễ dàng tích hợp vào các dự án React.  
- **Tăng tốc phát triển**: Cung cấp nhiều thành phần sẵn có như Button, Card, Table, Form, giúp lập trình viên tiết kiệm thời gian.  
- **Tùy chỉnh linh hoạt**: Hỗ trợ theme, CSS-in-JS và Styled Components để dễ dàng tùy chỉnh giao diện theo yêu cầu.  
- **Hiệu suất cao**: Được tối ưu hóa tốt, hỗ trợ SSR (Server-Side Rendering) và tree-shaking để giảm kích thước bundle.  

---

### **2. Material UI là gì?**  
Material UI (MUI) là một thư viện giao diện người dùng mã nguồn mở dành cho React, dựa trên **Material Design** của Google. Nó cung cấp các thành phần giao diện đẹp, hiện đại và dễ sử dụng như **Button, Card, Table, Modal, Dialog, Form, Grid**, giúp lập trình viên tạo UI nhanh hơn và nhất quán hơn.  

📌 **Website chính thức:** [https://mui.com/](https://mui.com/)  

---

### **3. Một số ví dụ về Material UI**  

#### **Cài đặt Material UI**  
Trước tiên, bạn cần cài đặt MUI trong dự án React:  
```sh
pnpm add @mui/material @emotion/react @emotion/styled
```

---

#### **Ví dụ 1: Tạo một Button với Material UI**  
```tsx
import React from "react";
import Button from "@mui/material/Button";

export default function MyButton() {
  return (
    <Button variant="contained" color="primary">
      Click me
    </Button>
  );
}
```
📌 **Giải thích:**  
- `variant="contained"`: Tạo button có nền màu.  
- `color="primary"`: Button có màu chủ đạo của theme.  

---

#### **Ví dụ 2: Sử dụng Card để hiển thị thông tin**  
```tsx
import React from "react";
import { Card, CardContent, Typography } from "@mui/material";

export default function MyCard() {
  return (
    <Card sx={{ maxWidth: 300, boxShadow: 3 }}>
      <CardContent>
        <Typography variant="h5">Material UI</Typography>
        <Typography variant="body2" color="text.secondary">
          Đây là một ví dụ về Card trong MUI.
        </Typography>
      </CardContent>
    </Card>
  );
}
```
📌 **Giải thích:**  
- `Card`: Một thành phần giao diện giống thẻ thông tin.  
- `Typography`: Giúp hiển thị văn bản với các biến thể khác nhau.  

---

#### **Ví dụ 3: Sử dụng Grid để tạo bố cục**  
```tsx
import React from "react";
import { Grid, Paper, Typography } from "@mui/material";

export default function MyGrid() {
  return (
    <Grid container spacing={2}>
      <Grid item xs={6}>
        <Paper sx={{ padding: 2, textAlign: "center" }}>
          <Typography>Box 1</Typography>
        </Paper>
      </Grid>
      <Grid item xs={6}>
        <Paper sx={{ padding: 2, textAlign: "center" }}>
          <Typography>Box 2</Typography>
        </Paper>
      </Grid>
    </Grid>
  );
}
```
📌 **Giải thích:**  
- `Grid container spacing={2}`: Tạo lưới với khoảng cách 2.  
- `Grid item xs={6}`: Mỗi cột chiếm 6 phần trong lưới (tổng cộng 12 phần).  

---

### **Tóm lại**  
✅ **Material UI** giúp tăng tốc phát triển giao diện React với các thành phần đẹp, dễ dùng, theo chuẩn Material Design.  
✅ **Linh hoạt & mạnh mẽ**, hỗ trợ tùy chỉnh theme, style và bố cục dễ dàng.  
✅ **Dễ học & dễ triển khai**, chỉ cần import và sử dụng như các component React thông thường.  

Bạn đang dùng Tailwind CSS, nếu muốn kết hợp với Material UI thì mình có thể hướng dẫn thêm! 🚀