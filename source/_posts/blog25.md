---
title: <25> Types & Validation - TypeScript
date: 2025-03-07 09:11:13
tags:
---
# TypeScript Cheatsheet

## 1. Cài đặt TypeScript
```sh
npm install -g typescript
```
Kiểm tra phiên bản:
```sh
tsc --version
```

## 2. Biên dịch TypeScript
```sh
tsc file.ts
```

## 3. Kiểu dữ liệu cơ bản
```ts
let isDone: boolean = false;
let age: number = 25;
let username: string = "Cuongtk2002";
let list: number[] = [1, 2, 3];
let tuple: [string, number] = ["Hello", 10];
let anything: any = "Có thể là bất kỳ thứ gì";
let unknownVar: unknown = 10; // Cần kiểm tra kiểu trước khi sử dụng
```

## 4. Hàm
```ts
function greet(name: string): string {
    return `Hello, ${name}`;
}

const add = (a: number, b: number): number => a + b;
```

## 5. Interface
```ts
interface User {
    id: number;
    name: string;
    isActive: boolean;
}

const user: User = { id: 1, name: "Cuongtk2002", isActive: true };
```

## 6. Class
```ts
class Person {
    name: string;
    age: number;
    
    constructor(name: string, age: number) {
        this.name = name;
        this.age = age;
    }
    
    greet(): string {
        return `Hello, my name is ${this.name}`;
    }
}
```

## 7. Enum
```ts
enum Direction {
    Up = "UP",
    Down = "DOWN",
    Left = "LEFT",
    Right = "RIGHT"
}
```

## 8. Generics
```ts
function identity<T>(arg: T): T {
    return arg;
}

let output = identity<string>("Hello World");
```

## 9. Type Alias
```ts
type Point = { x: number; y: number };
const point: Point = { x: 10, y: 20 };
```

## 10. Optional & Readonly
```ts
interface Person {
    name: string;
    age?: number; // Tuỳ chọn
    readonly id: number; // Chỉ đọc
}
```

## 11. Union & Intersection
```ts
let value: string | number;
value = "Hello";
value = 42;

interface A { a: string; }
interface B { b: number; }
const ab: A & B = { a: "test", b: 123 };
```

## 12. Utility Types
```ts
type PartialUser = Partial<User>;
type RequiredUser = Required<User>;
type ReadonlyUser = Readonly<User>;
type PickUser = Pick<User, "id" | "name">;
type OmitUser = Omit<User, "isActive">;
```

## 13. Mô-đun (Modules)
```ts
// math.ts
export function add(a: number, b: number): number {
    return a + b;
}

// main.ts
import { add } from "./math";
console.log(add(2, 3));
```

## 14. Kiểm tra Non-Null
```ts
function printName(name?: string) {
    console.log(name!.toUpperCase());
}
```

## 15. Dùng với React
```tsx
type Props = {
    name: string;
};
const Greeting: React.FC<Props> = ({ name }) => {
    return <h1>Hello, {name}!</h1>;
};
```

---

Đây là một số kiến thức quan trọng để bạn có thể làm việc với TypeScript một cách nhanh chóng!

