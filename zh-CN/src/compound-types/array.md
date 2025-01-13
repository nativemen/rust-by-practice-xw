# 数组

数组的类型是 `[T; Length]`，就如你所看到的，数组的长度是类型签名的一部分，因此数组的长度必须在编译期就已知，例如你不能使用以下方式来声明一个数组:

```rust
fn create_arr(n: i32) {
    let arr = [1; n];
}
```

以上函数将报错，因为编译器无法在编译期知道 `n` 的具体大小。

1. 🌟

```rust,editable

fn main() {
    // 使用合适的类型填空
    let arr: [i32; 5] = [1, 2, 3, 4, 5];

    // 修改以下代码，让它顺利运行
    assert!(arr.len() == 5);
}
```

2. 🌟🌟

```rust,editable

fn main() {
    // 很多时候，我们可以忽略数组的部分类型，也可以忽略全部类型，让编译器帮助我们推导
    let arr0 = [1, 2, 3];
    let arr: [_; 3] = ['a', 'b', 'c'];

    // 填空
    // 数组分配在栈上， `std::mem::size_of_val` 函数会返回整个数组占用的内存空间
    // 数组中的每个 char 元素占用 4 字节的内存空间，因为在 Rust 中， char 是 Unicode 字符
    assert!(std::mem::size_of_val(&arr) == 12);
}
```

3. 🌟 数组中的所有元素可以一起初始化为同一个值

```rust,editable

fn main() {
    // 填空
    let list: [i32; 100] = [1; 100];

    assert!(list[0] == 1);
    assert!(list.len() == 100);
}
```

4. 🌟 数组中的所有元素必须是同一类型

```rust,editable

fn main() {
    // 修复错误
    let _arr = [1, 2, 3];
}
```

5. 🌟 数组的下标索引从 0 开始.

```rust,editable

fn main() {
    let arr = ['a', 'b', 'c'];

    let ele = arr[0]; // 只修改此行来让代码工作

    assert!(ele == 'a');
}
```

6. 🌟 越界索引会导致代码的 `panic`.

```rust,editable

// 修复代码中的错误
fn main() {
    let names = [String::from("Sunfei"), "Sunface".to_string()];

    // `get` 返回 `Option<T>` 类型，因此它的使用非常安全
    let name0 = names.get(0).unwrap();

    // 但是下标索引就存在越界的风险了
    let _name1 = &names[1];
}
```

> 你可以在[这里](https://github.com/sunface/rust-by-practice/blob/master/solutions/compound-types/array.md)找到答案(在 solutions 路径下)
