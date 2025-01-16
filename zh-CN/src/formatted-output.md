# 格式化输出

## 位置参数

1.🌟🌟

```rust,editable
/* 填空 */
fn main() {
    println!("{0}, this is {1}. {1}, this is {0}", "Alice", "Bob"); // => Alice, this is Bob. Bob, this is Alice
    assert_eq!(format!("{1}{0}", 1, 2), "21");
    assert_eq!(format!("{1}{}{0}{}", 1, 2), "2112");
    println!("Success!");
}
```

## 具名参数

2.🌟🌟

```rust,editable
fn main() {
    println!("{argument}", argument = "test"); // => "test"

    /* 填空 */
    assert_eq!(format!("{name}{}", 1, name = 2), "21");
    assert_eq!(format!("{a} {c} {b}", a = "a", b = 'b', c = 3), "a 3 b");

    /* 修复错误 */
    // 具名参数必须放在其它参数后面
    println!("{abc} {}", 2, abc = "def");

    println!("Success!")
}
```

## 字符串对齐

3.🌟🌟 默认情况下，通过空格来填充字符串

```rust,editable
fn main() {
    // 下面两个都是通过 5 个空格来填充
    println!("Hello {:5}!", "x"); // =>  "Hello x    !"
    println!("Hello {:1$}!", "x", 5); // =>  "Hello x    !"

    /* 填空 */
    assert_eq!(format!("Hello {1:0$}!", 5, "x"), "Hello x    !");
    assert_eq!(format!("Hello {:width$}!", "x", width = 5), "Hello x    !");

    println!("Success!")
}
```

4.🌟🌟🌟 左对齐, 右对齐, 使用指定的字符填充

```rust,editable
fn main() {
    // 左对齐
    println!("Hello {:<5}!", "x"); // => Hello x    !

    // 右对齐
    assert_eq!(format!("Hello {:>5}!", "x"), "Hello     x!");

    // 居中对齐
    assert_eq!(format!("Hello {:^5}!", "x"), "Hello   x  !");

    // 左对齐，并使用 `&` 填充
    assert_eq!(format!("Hello {:&<5}!", "x"), "Hello x&&&&!");

    println!("Success!")
}
```

5.🌟🌟 我们还能使用 0 来填充数字

```rust,editable
fn main() {
    println!("Hello {:5}!", 5); // => Hello     5!
    println!("Hello {:+}!", 5); // =>  Hello +5!
    println!("Hello {:05}!", 5); // => Hello 00005!
    println!("Hello {:05}!", -5); // => Hello -0005!

    /* 填空 */
    assert!(format!("{number:0>width$}", number = 1, width = 6) == "000001");

    println!("Success!")
}
```

## 精度

6.🌟🌟 浮点数精度

```rust,editable

/* 填空 */
fn main() {
    let v = 3.1415926;

    println!("{:.1$}", v, 4); // same as {:.4} => 3.1416

    assert_eq!(format!("{:.2}", v), "3.14");
    assert_eq!(format!("{:+.2}", v), "+3.14");
    assert_eq!(format!("{:.0}", v), "3");

    println!("Success!")
}
```

7.🌟🌟🌟 字符串长度

```rust,editable
fn main() {
    let s = "Hello, world!";

    println!("{0:.5}", s); // => Hello

    assert_eq!(format!("Hello {1:.0$}!", 3, "abcdefg"), "Hello abc!");

    println!("Success!")
}
```

## 二进制, 八进制, 十六进制

- format!("{}", foo) -> "3735928559"
- format!("0x{:X}", foo) -> "0xDEADBEEF"
- format!("0o{:o}", foo) -> "0o33653337357"

8.🌟🌟

```rust,editable
fn main() {
    assert_eq!(format!("0b{:b}", 27), "0b11011");
    assert_eq!(format!("0o{:o}", 27), "0o33");
    assert_eq!(format!("0x{:x}", 27), "0x1b");
    assert_eq!(format!("0x{:X}", 27), "0x1B");

    println!("{:x}!", 27); // 没有前缀的十六进制 => 1b

    println!("{:#010b}", 27); // 使用 0 来填充二进制，宽度为 10 => 0b00011011

    println!("Success!")
}
```

```rust,editable
fn main() {
    assert_eq!(format!("{:#b}", 27), "0b11011");
    assert_eq!(format!("{:#o}", 27), "0o33");
    assert_eq!(format!("{:#x}", 27), "0x1b");
    assert_eq!(format!("{:#X}", 27), "0x1B");

    println!("{:x}!", 27); // 没有前缀的十六进制 => 1b

    println!("{:#010b}", 27); // 使用 0 来填充二进制，宽度为 10 => 0b00011011

    println!("Success!")
}
```

## 捕获环境中的值

9.🌟🌟🌟

```rust,editable
fn get_person() -> String {
    String::from("sunface")
}

fn get_format() -> (usize, usize) {
    (4, 1)
}

fn main() {
    let person = get_person();
    println!("Hello, {person}!");

    let (width, precision) = get_format();
    let scores = [("sunface", 99.12), ("jack", 60.34)];
    /* 让下面的代码输出:
    sunface: 99.1
    jack: 60.3
    */
    for (name, score) in scores {
        println!("{name}: {score:width$.precision$}");
    }
}
```

## Others

**Example**

```rust,editable
fn main() {
    // 指数
    println!("{:2e}", 1000000000); // => 1e9
    println!("{:2E}", 1000000000); // => 1E9

    // 指针地址
    let v= vec![1, 2, 3];
    println!("{:p}", v.as_ptr()); // => 0x600002324050

    // 转义
    println!("Hello {{}}"); // => Hello {}
}
```

> 你可以在[这里](https://github.com/sunface/rust-by-practice/blob/master/solutions/formatted-output/formatting.md)找到答案(在 solutions 路径下)
