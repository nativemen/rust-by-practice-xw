# Vector

相比 `[T; N]` 形式的数组， `Vector` 最大的特点就是可以动态调整长度。

### 基本操作

1. 🌟🌟🌟

```rust,editable

fn main() {
    let arr: [u8; 3] = [1, 2, 3];

    let v = Vec::from(arr);
    is_vec(&v);

    let v = vec![1, 2, 3];
    is_vec(&v);

    // vec!(..) 和 vec![..] 是同样的宏，宏可以使用 []、()、{}三种形式，因此...
    let v = vec![1, 2, 3];
    is_vec(&v);

    // ...在下面的代码中, v 是 Vec<[u8; 3]> , 而不是 Vec<u8>
    // 使用 Vec::new 和 `for` 来重写下面这段代码
    let mut v1 = Vec::new();
    for val in &v {
        v1.push(*val);
    }
    is_vec(&v1);

    assert_eq!(v, v1);

    println!("Success!")
}

fn is_vec(v: &Vec<u8>) {}
```

2. 🌟🌟 `Vec` 可以使用 `extend` 方法进行扩展

```rust,editable

// 填空
fn main() {
    let mut v1 = Vec::from([1, 2, 4]);
    v1.pop();
    v1.push(3);

    let mut v2 = Vec::new();
    v2.extend(v1.iter());

    assert_eq!(v1, v2);

    println!("Success!")
}
```

### 将 X 类型转换(From/Into 特征)成 Vec

只要为 `Vec` 实现了 `From<T>` 特征，那么 `T` 就可以被转换成 `Vec`。

3. 🌟🌟🌟

```rust,editable

// 填空
fn main() {
    // array -> Vec
    // impl From<[T; N]> for Vec
    let arr = [1, 2, 3];
    let v1 = Vec::from(arr);
    let v2: Vec<i32> = arr.to_vec();

    assert_eq!(v1, v2);

    // String -> Vec
    // impl From<String> for Vec
    let s = "hello".to_string();
    let v1: Vec<u8> = s.into_bytes();

    let s = "hello".to_string();
    let v2 = s.into_bytes();
    assert_eq!(v1, v2);

    // impl<'_> From<&'_ str> for Vec
    let s = "hello";
    let v3 = Vec::from(s);
    assert_eq!(v2, v3);

    // 迭代器 Iterators 可以通过 collect 变成 Vec
    let v4: Vec<i32> = [0; 10].into_iter().collect();
    assert_eq!(v4, vec![0; 10]);

    println!("Success!")
}
```

### 索引

4. 🌟🌟🌟

```rust,editable

// 修复错误并实现缺失的代码
fn main() {
    let mut v = Vec::from([1, 2, 3, 4, 5]);
    for i in 0..5 {
        println!("{:?}", v[i])
    }

    for i in 0..5 {
        // 实现这里的代码...
        v[i] += 1;
    }

    assert_eq!(v, vec![2, 3, 4, 5, 6]);

    println!("Success!")
}
```

```rust,editable

// 修复错误并实现缺失的代码
fn main() {
    let mut v = Vec::from([1, 2, 3]);
    for i in 0..5 {
        println!("{:?}", v.get(i))
    }

    for i in 0..5 {
        // 实现这里的代码...
        if let Some(val) = v.get(i) {
            v[i] = val + 1;
        } else {
            v.push(i + 2);
        }
    }

    assert_eq!(v, vec![2, 3, 4, 5, 6]);

    println!("Success!")
}
```

### 切片

与 `String` 的切片类似， `Vec` 也可以使用切片。如果说 `Vec` 是可变的，那它的切片就是不可变或者说只读的，我们可以通过 `&` 来获取切片。

在 Rust 中，将切片作为参数进行传递是更常见的使用方式，例如当一个函数只需要可读性时，那传递 `Vec` 或 `String` 的切片 `&[T]` / `&str` 会更加适合。

5. 🌟🌟

```rust,editable

// 修复错误
fn main() {
    let mut v = vec![1, 2, 3];

    let slice1 = &v[..];
    // 越界访问将导致 panic.
    // 修改时必须使用 `v.len`
    let slice2 = &v[0..v.len()];

    assert_eq!(slice1, slice2);

    // 切片是只读的
    // 注意：切片和 `&Vec` 是不同的类型，后者仅仅是 `Vec` 的引用，并可以通过解引用直接获取 `Vec`
    let vec_ref: &mut Vec<i32> = &mut v;
    (*vec_ref).push(4);
    let slice3 = &mut v[0..4];
    slice3[3] = 5;

    assert_eq!(slice3, &[1, 2, 3, 5]);

    println!("Success!")
}
```

### 容量

容量 `capacity` 是已经分配好的内存空间，用于存储未来添加到 `Vec` 中的元素。而长度 `len` 则是当前 `Vec` 中已经存储的元素数量。如果要添加新元素时，长度将要超过已有的容量，那容量会自动进行增长：Rust 会重新分配一块更大的内存空间，然后将之前的 `Vec` 拷贝过去，因此，这里就会发生新的内存分配( 目前 Rust 的容量调整策略是加倍，例如 2 -> 4 -> 8 ..)。

若这段代码会频繁发生，那频繁的内存分配会大幅影响我们系统的性能，最好的办法就是提前分配好足够的容量，尽量减少内存分配。

6. 🌟🌟

```rust,editable
// 修复错误
fn main() {
    let mut vec = Vec::with_capacity(10);

    assert_eq!(vec.len(), 0);
    assert_eq!(vec.capacity(), 10);

    // 由于提前设置了足够的容量，这里的循环不会造成任何内存分配...
    for i in 0..10 {
        vec.push(i);
    }
    assert_eq!(vec.len(), 10);
    assert_eq!(vec.capacity(), 10);

    // ...但是下面的代码会造成新的内存分配
    vec.push(11);
    assert_eq!(vec.len(), 11);
    assert!(vec.capacity() >= 11);

    // 填写一个合适的值，在 `for` 循环运行的过程中，不会造成任何内存分配
    let mut vec = Vec::with_capacity(100);
    for i in 0..100 {
        vec.push(i);
    }

    assert_eq!(vec.len(), 100);
    assert_eq!(vec.capacity(), 100);

    println!("Success!")
}
```

### 在 Vec 中存储不同类型的元素

`Vec` 中的元素必须是相同的类型，例如以下代码会发生错误:

```rust
fn main() {
   let v = vec![1, 2.0, 3];
}
```

但是我们可以使用枚举或特征对象来存储不同的类型.

7. 🌟🌟

```rust,editable
#[derive(Debug, PartialEq)]
enum IpAddr {
    V4(String),
    V6(String),
}
fn main() {
    // 填空
    let v: Vec<IpAddr> = vec![
        IpAddr::V4("127.0.0.1".to_string()),
        IpAddr::V6("::1".to_string()),
    ];

    // 枚举的比较需要派生 PartialEq 特征
    assert_eq!(v[0], IpAddr::V4("127.0.0.1".to_string()));
    assert_eq!(v[1], IpAddr::V6("::1".to_string()));

    println!("Success!")
}
```

8. 🌟🌟

```rust,editable
trait IpAddr {
    fn display(&self);
}

struct V4(String);
impl IpAddr for V4 {
    fn display(&self) {
        println!("ipv4: {:?}", self.0)
    }
}
struct V6(String);
impl IpAddr for V6 {
    fn display(&self) {
        println!("ipv6: {:?}", self.0)
    }
}

fn main() {
    // 填空
    let v: Vec<Box<dyn IpAddr>> = vec![
        Box::new(V4("127.0.0.1".to_string())),
        Box::new(V6("::1".to_string())),
    ];

    for ip in v {
        ip.display();
    }
}
```

> 你可以在[这里](https://github.com/sunface/rust-by-practice/blob/master/solutions/collections/Vector.md)找到答案(在 solutions 路径下)
