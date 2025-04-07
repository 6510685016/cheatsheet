# 🦀 **Rust Quiz Summary Sheet (QUIZ 1 - 8)**  
> รวมทุกเนื้อหาสำคัญ + ตัวอย่าง พร้อมใช้งานจริง

---

## 📖 1. ประวัติและภาพรวมของภาษา Rust

- พัฒนาโดย: **Mozilla Research**
- เปิดตัวครั้งแรก: **ปี 2010**  
- Rust เป็นภาษาระดับ System Programming เช่นเดียวกับ C/C++
- ได้รับความนิยมจากการที่ **ปลอดภัยแต่ยังเร็ว**

### ✅ ใช้กับอะไรได้บ้าง
- Game Engine
- Embedded System
- WebAssembly
- Blockchain
- Backend System (เช่น web server, API)

---

## 🌟 2. จุดเด่นของ Rust

### ✅ Memory Safety โดยไม่มี Garbage Collector
- ใช้ระบบ Ownership → ป้องกัน Memory Leak
- ป้องกัน Null Pointer, Data Race, Use-after-free

### ✅ Performance ใกล้เคียง C/C++

### ✅ Concurrency อย่างปลอดภัย
- ใช้ `async`, `tokio`, `thread`, `mutex`, `channel` อย่างเป็นระบบ

### ✅ Cross-platform

---

## ⚠️ 3. จุดด้อยของ Rust

- Syntax ใหม่และซับซ้อน โดยเฉพาะ `lifetimes`, `borrowing`
- Compile ช้ากว่า C/C++
- Library ecosystem ยังไม่ใหญ่เท่า JavaScript, Python

---

## 📦 4. การจัดการ Memory: Ownership / Borrowing / Lifetimes

### 🔑 Concepts สำคัญ:
1. **Ownership** – ตัวแปรหนึ่งตัวเป็นเจ้าของค่าหนึ่งได้เพียงตัวเดียว
2. **Borrowing (& / &mut)** – ยืมค่ามาใช้โดยไม่ย้าย ownership
3. **Lifetimes** – บอกว่าค่าจะถูกใช้ได้นานแค่ไหน (หลีกเลี่ยง dangling pointer)

### 🧪 Example:
```rust
fn main() {
    let s1 = String::from("Hello");
    let s2 = s1; // ownership moved
    // println!("{}", s1); ❌ Error: s1 ไม่สามารถใช้ได้แล้ว
}
```

---

## ✏️ 5. การใช้ `mut`, `let`, `const`

### 🔧 `let` vs `mut`
```rust
let x = 5;        // immutable
let mut y = 10;   // mutable
y += 1;           // ✅ เปลี่ยนค่าได้
```

### 🔧 `const` = ค่าคงที่ ไม่สามารถเปลี่ยนค่าได้ และต้องระบุ type
```rust
const PI: f64 = 3.14;
```

---

## 🔘 6. Enum และ Pattern Matching

### 🔹 สร้าง enum:
```rust
enum IpAddr {
    V4(String),
    V6(String),
}
```

### 🔹 ใช้กับ `match`:
```rust
let ip = IpAddr::V4(String::from("127.0.0.1"));

match ip {
    IpAddr::V4(addr) => println!("IPv4: {}", addr),
    IpAddr::V6(addr) => println!("IPv6: {}", addr),
}
```

---

## ❓ 7. Option<T>

### 💡 แทน null แบบปลอดภัย

```rust
let some_number = Some(5);
let no_number: Option<i32> = None;
```

### 🔍 ใช้กับ match:
```rust
match some_number {
    Some(x) => println!("Value is {}", x),
    None => println!("No value"),
}
```

---

## ❗ 8. Result<T, E>

### ✅ สำหรับจัดการ Error

```rust
fn divide(a: i32, b: i32) -> Result<i32, String> {
    if b == 0 {
        Err("Cannot divide by zero".to_string())
    } else {
        Ok(a / b)
    }
}
```

### 🧪 ใช้งาน:
```rust
match divide(10, 2) {
    Ok(result) => println!("Result: {}", result),
    Err(e) => println!("Error: {}", e),
}
```

---

## ⏱️ 9. Asynchronous Programming และ Tokio (QUIZ8)

### 📌 ทำไมต้อง Async?
- เหมาะกับงาน I/O: เช่นอ่านไฟล์, call API, TCP
- ไม่ block thread → รันหลายงานพร้อมกัน

### 📦 `tokio` คืออะไร?
- Async Runtime ที่ใช้รัน async function
- ใช้ `tokio::main`, `tokio::spawn`, `join!`

### 🧪 ตัวอย่าง:
```rust
#[tokio::main]
async fn main() {
    let task1 = tokio::spawn(async {
        println!("Task 1 start");
    });

    let task2 = tokio::spawn(async {
        println!("Task 2 start");
    });

    let _ = tokio::join!(task1, task2);
}
```

---

## 📌 ข้อมูลเสริมที่ควรรู้

### 🔹 Cargo
- ระบบจัดการโปรเจกต์และ dependency
- `cargo new`, `cargo build`, `cargo run`, `cargo test`

### 🔹 Crate
- หน่วยของ library หรือ binary
- มีแบบ `lib.rs` และ `main.rs`

### 🔹 Macro
- `println!`, `vec!`, `format!` เป็น macro
- ใช้ `!` เสมอ

### 🔹 การจัดการ Module
```rust
mod math;

fn main() {
    math::add(1, 2);
}
```

---
