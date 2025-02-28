---
title: <17> State Management - Redux Toolkit
date: 2025-02-28 13:44:41
tags:
---
Redux Toolkit là một thư viện chính thức của Redux, được thiết kế để đơn giản hóa quá trình phát triển ứng dụng bằng cách cung cấp các công cụ và cấu hình mặc định giúp giảm thiểu mã nguồn cần viết và tăng hiệu quả quản lý trạng thái. Nó giải quyết các vấn đề phổ biến khi sử dụng Redux truyền thống, như cấu hình phức tạp, yêu cầu thêm nhiều thư viện bổ sung và quá nhiều mã lặp. 

**Ví dụ đơn giản về Redux Toolkit:**

Dưới đây là một ví dụ về cách sử dụng Redux Toolkit để tạo một bộ đếm đơn giản:

1. **Cài đặt Redux Toolkit:**

   ```bash
   npm install @reduxjs/toolkit react-redux
   ```


2. **Tạo slice cho bộ đếm:**

   ```javascript
   // features/counter/counterSlice.js
   import { createSlice } from '@reduxjs/toolkit';

   const counterSlice = createSlice({
     name: 'counter',
     initialState: 0,
     reducers: {
       increment: state => state + 1,
       decrement: state => state - 1,
       incrementByAmount: (state, action) => state + action.payload,
     },
   });

   export const { increment, decrement, incrementByAmount } = counterSlice.actions;
   export default counterSlice.reducer;
   ```


3. **Cấu hình store:**

   ```javascript
   // app/store.js
   import { configureStore } from '@reduxjs/toolkit';
   import counterReducer from '../features/counter/counterSlice';

   const store = configureStore({
     reducer: {
       counter: counterReducer,
     },
   });

   export default store;
   ```


4. **Sử dụng trong component React:**

   ```javascript
   // App.js
   import React from 'react';
   import { useSelector, useDispatch } from 'react-redux';
   import { increment, decrement, incrementByAmount } from './features/counter/counterSlice';

   function App() {
     const count = useSelector(state => state.counter);
     const dispatch = useDispatch();

     return (
       <div>
         <h1>{count}</h1>
         <button onClick={() => dispatch(increment())}>Tăng</button>
         <button onClick={() => dispatch(decrement())}>Giảm</button>
         <button onClick={() => dispatch(incrementByAmount(5))}>Tăng 5</button>
       </div>
     );
   }

   export default App;
   ```


5. **Kết nối store với ứng dụng:**

   ```javascript
   // index.js
   import React from 'react';
   import ReactDOM from 'react-dom';
   import { Provider } from 'react-redux';
   import App from './App';
   import store from './app/store';

   ReactDOM.render(
     <Provider store={store}>
       <App />
     </Provider>,
     document.getElementById('root')
   );
   ```


Với Redux Toolkit, việc thiết lập và quản lý trạng thái trong ứng dụng React trở nên đơn giản và hiệu quả hơn, giúp giảm thiểu mã nguồn và tăng tính nhất quán trong cấu trúc code. 