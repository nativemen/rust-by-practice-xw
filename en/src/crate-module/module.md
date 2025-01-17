# Module

Modules let us organize the code within a crate into groups for readability and ease of reuse. Module also controls the privacy of items, which is whether an item can be seen by outside code( public ), or is just an internal implementation and not available for outside code( private ).

We have created a package named `hello-package` in previous chapter, and it looks like this:

```shell
.
├── Cargo.toml
├── src
│   ├── lib.rs
│   └── main.rs
```

Now it's time to create some modules in the library crate and use them in the binary crate, let's start.

1. 🌟🌟 Implement module `front_of_house` based on the module tree below:

```shell
library crate root
 └── front_of_house
     ├── hosting
     │   ├── add_to_waitlist
     │   └── seat_at_table
     └── serving
         ├── take_order
         ├── serve_order
         ├── take_payment
         └── complain
```

```rust,editable
// FILL in the blank
// in lib.rs

mod front_of_house {
    // IMPLEMENT this module..
    mod hosting {
        fn add_to_waitlist() {}
        fn seat_at_table() {}
    }

    mod serving {
        fn take_order() {}
        fn serve_order() {}
        fn take_payment() {}
        fn complain() {}
    }
}
```

2. 🌟🌟 Let's call `add_to_waitlist` from a function `eat_at_restaurant` which is within the library crate root.

```rust,editable
// In lib.rs

// FILL in the blanks and FIX the errors
// You need to make something public with `pub` to provide accessibility for outside code `fn eat_at_restaurant()`
pub mod front_of_house {
    /* ...snip... */
    pub mod hosting {
        pub fn add_to_waitlist() {}
        pub fn seat_at_table() {}
    }

    pub mod serving {
        pub fn take_order() {}
        pub fn serve_order() {}
        pub fn take_payment() {}
        pub fn complain() {}
    }
}

pub fn eat_at_restaurant() {
    // Call add_to_waitlist with **absolute path**:
    crate::front_of_house::hosting::add_to_waitlist();

    // Call with **relative path**
     front_of_house::hosting::add_to_waitlist();
}
```

3. 🌟🌟 You can use `super` to import items within the parent module

```rust,editable
// In lib.rs

mod back_of_house {
    fn fix_incorrect_order() {
        cook_order();
        // FILL in the blank in three ways
        //1. using keyword `super`
        //2. using absolute path
        super::front_of_house::serving::serve_order();
        crate::front_of_house::serving::serve_order();
        front_of_house::serving::serve_order();
    }

    fn cook_order() {}
}
```

### Separating modules into different files

```rust,editable
// In lib.rs
pub mod front_of_house {
    pub mod hosting {
        pub fn add_to_waitlist() {}

        pub fn seat_at_table() -> String {
            String::from("sit down please")
        }
    }

    pub mod serving {
        pub fn take_order() {}

        pub fn serve_order() {}

        pub fn take_payment() {}

        // Maybe you don't want the guest hearing the your complaining about them
        // So just make it private
        fn complain() {}
    }
}

pub fn eat_at_restaurant() -> String {
    front_of_house::hosting::add_to_waitlist();

    back_of_house::cook_order();

    String::from("yummy yummy!")
}

pub mod back_of_house {
    pub fn fix_incorrect_order() {
        cook_order();
        crate::front_of_house::serving::serve_order();
    }

    pub fn cook_order() {}
}
```

4. 🌟🌟🌟🌟 Please separate the modules and codes above into files resident in below dir tree :

```shell
.
├── Cargo.toml
├── src
│   ├── back_of_house.rs
│   ├── front_of_house
│   │   ├── hosting.rs
│   │   ├── mod.rs
│   │   └── serving.rs
│   ├── lib.rs
│   └── main.rs
```

```rust,editable
// In src/lib.rs

// IMPLEMENT...
pub mod front_of_house;
pub mod back_of_house;

pub fn eat_at_restaurant() -> String {
    front_of_house::hosting::add_to_waitlist();

    back_of_house::cook_order();

    String::from("yummy yummy!")
}
```

```rust,editable
// In src/back_of_house.rs

// IMPLEMENT...
use crate::front_of_house;

pub fn fix_incorrect_order() {
    cook_order();
    front_of_house::serving::serve_order();
}

pub fn cook_order() {}
```

```rust,editable
// In src/front_of_house/mod.rs

// IMPLEMENT...
pub mod hosting;
pub mod serving;
```

```rust,editable
// In src/front_of_house/hosting.rs

// IMPLEMENT...
pub fn add_to_waitlist() {}

pub fn seat_at_table() -> String {
    String::from("sit down please")
}
```

```rust,editable
// In src/front_of_house/serving.rs

// IMPLEMENT...
pub fn take_order() {}

pub fn serve_order() {}

pub fn take_payment() {}

// Maybe you don't want the guest hearing the your complaining about them
// So just make it private
fn complain() {}
```

### Accessing code in library crate from binary crate

**Please ensure you have completed the 4th exercise before making further progress.**

You should have below structures and the corresponding codes in them when reaching here:

```shell
.
├── Cargo.toml
├── src
│   ├── back_of_house.rs
│   ├── front_of_house
│   │   ├── hosting.rs
│   │   ├── mod.rs
│   │   └── serving.rs
│   ├── lib.rs
│   └── main.rs
```

5. 🌟🌟🌟 Now we will call a few library functions from the binary crate.

```rust,editable
// In src/main.rs

// FILL in the blank and FIX the errors
fn main() {
    assert_eq!(hello-package1::front_of_house::hosting::seat_at_table(), "sit down please");
    assert_eq!(hello-package1::eat_at_restaurant(),"yummy yummy!");
}
```

> You can find the solutions [here](https://github.com/sunface/rust-by-practice/blob/master/solutions/crate-module/module.md) (under the solutions path), but only use it when you need it :)
