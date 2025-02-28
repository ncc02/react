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

---
Để sử dụng hiệu quả Redux Toolkit trong các dự án tương lai, bạn nên ghi nhớ các từ khóa và khái niệm quan trọng sau:

1. **configureStore**: Hàm này giúp tạo và cấu hình store Redux một cách dễ dàng, tự động thiết lập các middleware cần thiết và tích hợp Redux DevTools. citeturn0search0

2. **createSlice**: Hàm này kết hợp việc tạo action và reducer trong một cấu trúc duy nhất gọi là "slice", giúp quản lý logic trạng thái liên quan một cách gọn gàng và hiệu quả. citeturn0search1

3. **createAsyncThunk**: Hàm này hỗ trợ xử lý các tác vụ bất đồng bộ (như gọi API) trong Redux, tự động quản lý các trạng thái pending, fulfilled và rejected của promise. citeturn0search1

4. **createEntityAdapter**: Hàm này cung cấp các bộ công cụ để quản lý các tập hợp dữ liệu theo chuẩn hóa, như danh sách các đối tượng, giúp đơn giản hóa việc thao tác với các thực thể trong state. citeturn0search1

5. **useSelector và useDispatch**: Hai hooks này từ thư viện react-redux cho phép bạn truy cập vào state và gửi action trong các functional component của React. citeturn0search1

Nắm vững các từ khóa và khái niệm trên sẽ giúp bạn áp dụng Redux Toolkit một cách hiệu quả trong việc quản lý trạng thái ứng dụng React của mình. 