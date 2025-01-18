# Borrowing

1. 🌟🌟

```rust,editable
// FIX the error without removing any code line
struct test {
    list: Vec<i32>,
    a: i32,
}

impl test {
    pub fn new() -> Self {
        test {
            list: vec![1, 2, 3, 4, 5, 6, 7],
            a: 0,
        }
    }

    pub fn run(&mut self) {
        for i in self.list.clone().into_iter() {
            self.do_something(i)
        }
    }

    pub fn do_something(&mut self, n: i32) {
        self.a = n;
    }
}

fn main() {}
```

```rust,editable
// FIX the error without removing any code line
struct test {
    list: Vec<i32>,
    a: i32,
}

impl test {
    pub fn new() -> Self {
        test {
            list: vec![1, 2, 3, 4, 5, 6, 7],
            a: 0,
        }
    }

    pub fn run(&mut self) {
        for idx in 0..self.list.len() {
            let i = self.list[idx];
            self.do_something(i)
        }
    }

    pub fn do_something(&mut self, n: i32) {
        self.a = n;
    }
}

fn main() {}
```

```rust,editable
// FIX the error without removing any code line
struct test {
    list: Vec<i32>,
    a: i32,
}

impl test {
    pub fn new() -> Self {
        test {
            list: vec![1, 2, 3, 4, 5, 6, 7],
            a: 0,
        }
    }

    pub fn run(&mut self) {
        for i in self.list.drain(..).collect::<Vec<_>>() {
            self.do_something(i)
        }
    }

    pub fn do_something(&mut self, n: i32) {
        self.a = n;
    }
}

fn main() {}
```

```rust,editable
// FIX the error without removing any code line
struct test {
    list: Vec<i32>,
    a: i32,
}

impl test {
    pub fn new() -> Self {
        test {
            list: vec![1, 2, 3, 4, 5, 6, 7],
            a: 0,
        }
    }

    pub fn run(&mut self) {
        for i in self.list.clone() {
            self.do_something(i)
        }
    }

    pub fn do_something(&mut self, n: i32) {
        self.a = n;
    }
}

fn main() {}
```

```rust,editable
// FIX the error without removing any code line
struct test {
    list: Vec<i32>,
    a: i32,
}

impl test {
    pub fn new() -> Self {
        test {
            list: vec![1, 2, 3, 4, 5, 6, 7],
            a: 0,
        }
    }

    pub fn run(&mut self) {
        let v = self.list.iter().cloned().collect::<Vec<_>>();
        for i in v {
            self.do_something(i)
        }
    }

    pub fn do_something(&mut self, n: i32) {
        self.a = n;
    }
}

fn main() {}
```

```rust,editable
// FIX the error without removing any code line
struct test {
    list: Vec<i32>,
    a: i32,
}

impl test {
    pub fn new() -> Self {
        test {
            list: vec![1, 2, 3, 4, 5, 6, 7],
            a: 0,
        }
    }

    pub fn run(&mut self) {
        while let Some(i) = self.list.pop() {
            self.do_something(i);
        }
    }

    pub fn do_something(&mut self, n: i32) {
        self.a = n;
    }
}

fn main() {}
```

```rust,editable
// FIX the error without removing any code line
struct test {
    list: Vec<i32>,
    a: i32,
}

impl test {
    pub fn new() -> Self {
        test {
            list: vec![1, 2, 3, 4, 5, 6, 7],
            a: 0,
        }
    }

    pub fn run(&mut self) {
        for i in self.list.clone().iter() {
            self.do_something(*i)
        }
    }

    pub fn do_something(&mut self, n: i32) {
        self.a = n;
    }
}

fn main() {}
```

```rust,editable
// FIX the error without removing any code line
struct test {
    list: Vec<i32>,
    a: i32,
}

impl test {
    pub fn new() -> Self {
        test {
            list: vec![1, 2, 3, 4, 5, 6, 7],
            a: 0,
        }
    }

    pub fn run(&mut self) {
        for i in self.list.clone().iter_mut() {
            self.do_something(*i)
        }
    }

    pub fn do_something(&mut self, n: i32) {
        self.a = n;
    }
}

fn main() {}
```

```rust,editable
// FIX the error without removing any code line
struct test {
    list: Vec<i32>,
    a: i32,
}

impl test {
    pub fn new() -> Self {
        test {
            list: vec![1, 2, 3, 4, 5, 6, 7],
            a: 0,
        }
    }

    pub fn run(&mut self) {
        for i in self.list.clone().into_iter() {
            self.do_something(i)
        }
    }

    pub fn do_something(&mut self, n: i32) {
        self.a = n;
    }
}

fn main() {}
```

```rust,editable
// FIX the error without removing any code line
struct test {
    list: Vec<i32>,
    a: i32,
}

impl test {
    pub fn new() -> Self {
        test {
            list: vec![1, 2, 3, 4, 5, 6, 7],
            a: 0,
        }
    }

    pub fn run(&mut self) {
        self.list.clone().iter().for_each(|i| self.do_something(*i));
    }

    pub fn do_something(&mut self, n: i32) {
        self.a = n;
    }
}

fn main() {}
```

```rust,editable
// FIX the error without removing any code line
struct test {
    list: Vec<i32>,
    a: i32,
}

impl test {
    pub fn new() -> Self {
        test {
            list: vec![1, 2, 3, 4, 5, 6, 7],
            a: 0,
        }
    }

    pub fn run(&mut self) {
        self.list
            .iter()
            .cloned()
            .collect::<Vec<_>>()
            .iter()
            .for_each(|i| self.do_something(*i));
    }

    pub fn do_something(&mut self, n: i32) {
        self.a = n;
    }
}

fn main() {}
```

```rust,editable
// FIX the error without removing any code line
struct test {
    list: Vec<i32>,
    a: i32,
}

impl test {
    pub fn new() -> Self {
        test {
            list: vec![1, 2, 3, 4, 5, 6, 7],
            a: 0,
        }
    }

    pub fn run(&mut self) {
        self.list
            .drain(..)
            .collect::<Vec<_>>()
            .iter()
            .for_each(|i| self.do_something(*i));
    }

    pub fn do_something(&mut self, n: i32) {
        self.a = n;
    }
}

fn main() {}
```

> You can find the solutions [here](https://github.com/sunface/rust-by-practice/blob/master/solutions/fight-compiler/borrowing.md)(under the solutions path), but only use it when you need it :)
