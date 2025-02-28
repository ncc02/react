---
title: <18> Styling - Tailwincss
date: 2025-02-28 14:23:18
tags:
---
Dưới đây là một số lớp tiện ích phổ biến trong Tailwind CSS mà bạn có thể tham khảo để nhanh chóng nhớ lại và áp dụng trong quá trình phát triển giao diện:

**1. Màu sắc nền (Background Color):**
- `bg-{color}-{shade}`: Đặt màu nền cho phần tử. Ví dụ: `bg-blue-500` áp dụng màu xanh lam với độ đậm 500.

**2. Màu chữ (Text Color):**
- `text-{color}-{shade}`: Đặt màu chữ cho phần tử. Ví dụ: `text-red-700` áp dụng màu đỏ với độ đậm 700.

**3. Kích thước chữ (Font Size):**
- `text-xs`, `text-sm`, `text-base`, `text-lg`, `text-xl`, `text-2xl`, `text-3xl`, `text-4xl`, `text-5xl`, `text-6xl`: Đặt kích thước chữ từ nhỏ đến lớn.

**4. Độ đậm chữ (Font Weight):**
- `font-thin`, `font-extralight`, `font-light`, `font-normal`, `font-medium`, `font-semibold`, `font-bold`, `font-extrabold`, `font-black`: Đặt độ đậm của chữ.

**5. Căn lề (Margin):**
- `m-{size}`: Đặt margin cho tất cả các phía. Ví dụ: `m-4` đặt margin 1rem (16px).
- `mt-{size}`, `mr-{size}`, `mb-{size}`, `ml-{size}`: Đặt margin cho từng phía (trên, phải, dưới, trái).

**6. Khoảng đệm (Padding):**
- `p-{size}`: Đặt padding cho tất cả các phía. Ví dụ: `p-2` đặt padding 0.5rem (8px).
- `pt-{size}`, `pr-{size}`, `pb-{size}`, `pl-{size}`: Đặt padding cho từng phía.

**7. Bo góc (Border Radius):**
- `rounded-none`, `rounded-sm`, `rounded`, `rounded-md`, `rounded-lg`, `rounded-full`: Đặt độ bo góc cho phần tử.

**8. Đổ bóng (Box Shadow):**
- `shadow-sm`, `shadow`, `shadow-md`, `shadow-lg`, `shadow-xl`, `shadow-2xl`, `shadow-inner`, `shadow-none`: Đặt hiệu ứng đổ bóng cho phần tử.

**9. Hiển thị (Display):**
- `block`, `inline-block`, `inline`, `flex`, `inline-flex`, `grid`, `inline-grid`, `hidden`: Đặt kiểu hiển thị cho phần tử.

**10. Căn chỉnh trong Flexbox (Flexbox Alignment):**
- `justify-start`, `justify-center`, `justify-end`, `justify-between`, `justify-around`, `justify-evenly`: Căn chỉnh các phần tử con theo trục ngang.
- `items-start`, `items-center`, `items-end`, `items-baseline`, `items-stretch`: Căn chỉnh các phần tử con theo trục dọc.

**11. Kích thước (Width & Height):**
- `w-{size}`: Đặt chiều rộng cho phần tử. Ví dụ: `w-1/2` đặt chiều rộng bằng 50% container.
- `h-{size}`: Đặt chiều cao cho phần tử. Ví dụ: `h-64` đặt chiều cao 16rem (256px).

**12. Vị trí (Positioning):**
- `static`, `relative`, `absolute`, `fixed`, `sticky`: Đặt kiểu vị trí cho phần tử.
- `top-{size}`, `right-{size}`, `bottom-{size}`, `left-{size}`: Đặt vị trí của phần tử khi sử dụng `relative`, `absolute`, `fixed` hoặc `sticky`.

**13. Hiệu ứng khi hover (Hover Effects):**
- Sử dụng tiền tố `hover:` trước lớp tiện ích để áp dụng kiểu khi người dùng di chuột vào. Ví dụ: `hover:bg-blue-700` thay đổi màu nền thành xanh đậm khi hover.

**14. Responsive Design:**
- Sử dụng các tiền tố như `sm:`, `md:`, `lg:`, `xl:`, `2xl:` để áp dụng kiểu cho các kích thước màn hình khác nhau. Ví dụ: `md:text-lg` đặt kích thước chữ lớn khi màn hình đạt kích thước medium.

Để biết thêm chi tiết và khám phá đầy đủ các lớp tiện ích, bạn có thể tham khảo tài liệu chính thức của Tailwind CSS tại [https://tailwindcss.com/docs](https://tailwindcss.com/docs).

Hy vọng danh sách này sẽ giúp bạn nhanh chóng nhớ lại và áp dụng các lớp tiện ích của Tailwind CSS trong dự án của mình. 