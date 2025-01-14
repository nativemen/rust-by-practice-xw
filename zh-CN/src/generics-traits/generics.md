# 泛型

### 函数

1. 🌟🌟🌟

```rust,editable

// 填空
struct A;          // 具体的类型 `A`.
struct S(A);       // 具体的类型 `S`.
struct SGen<T>(T); // 泛型 `SGen`.

fn reg_fn(_s: S) {}

fn gen_spec_t(_s: SGen<A>) {}

fn gen_spec_i32(_s: SGen<i32>) {}

fn generic<T>(_s: SGen<T>) {}

fn main() {
    // 使用非泛型函数
    reg_fn(S(A));          // 具体的类型
    gen_spec_t(SGen(A));   // 隐式地指定类型参数  `A`.
    gen_spec_i32(SGen(-1)); // 隐式地指定类型参数`i32`.

    // 显式地指定类型参数 `char`
    generic::<char>(SGen('a'));

    // 隐式地指定类型参数 `char`.
    generic(SGen('b'));
}
```

2. 🌟🌟

```rust,editable

// 实现下面的泛型函数 sum
fn sum<T: std::ops::Add<Output = T>>(x: T, y: T) -> T {
    x + y
}

fn main() {
    assert_eq!(5, sum(2i8, 3i8));
    assert_eq!(50, sum(20, 30));
    assert_eq!(2.46, sum(1.23, 1.23));
}
```

### 结构体和 `impl`

3. 🌟

```rust,editable

// 实现一个结构体 Point 让代码工作
struct Point<T> {
    x: T,
    y: T,
}

fn main() {
    let integer = Point { x: 5, y: 10 };
    let float = Point { x: 1.0, y: 4.0 };
}
```

4. 🌟🌟

```rust,editable

// 修改以下结构体让代码工作
struct Point<T, U> {
    x: T,
    y: U,
}

fn main() {
    // 不要修改这行代码！
    let p = Point{x: 5, y : "hello".to_string()};
}
```

5. 🌟🌟

```rust,editable

// 为 Val 增加泛型参数，不要修改 `main` 中的代码
struct Val<T> {
    val: T,
}

impl<T> Val<T> {
    fn value(&self) -> &T {
        &self.val
    }
}

fn main() {
    let x = Val { val: 3.0 };
    let y = Val {
        val: "hello".to_string(),
    };
    println!("{}, {}", x.value(), y.value());
}
```

### 方法

6. 🌟🌟🌟

```rust,editable
struct Point<T, U> {
    x: T,
    y: U,
}

impl<T, U> Point<T, U> {
    // 实现 mixup，不要修改其它代码！
    fn mixup<V, W>(self, another: Point<V, W>) -> Point<T, W> {
        Point {
            x: self.x,
            y: another.y,
        }
    }
}

fn main() {
    let p1 = Point { x: 5, y: 10 };
    let p2 = Point {
        x: "Hello",
        y: '中',
    };

    let p3 = p1.mixup(p2);

    assert_eq!(p3.x, 5);
    assert_eq!(p3.y, '中');
}
```

7. 🌟🌟

```rust,editable

// 修复错误，让代码工作
struct Point<T> {
    x: T,
    y: T,
}

impl Point<f32> {
    fn distance_from_origin(&self) -> f32 {
        (self.x.powi(2) + self.y.powi(2)).sqrt()
    }
}

fn main() {
    let p = Point {
        x: 5.0f32,
        y: 10.0f32,
    };
    println!("{}", p.distance_from_origin())
}
```

> 你可以在[这里](https://github.com/sunface/rust-by-practice/blob/master/solutions/generics-traits/generics.md)找到答案(在 solutions 路径下)
