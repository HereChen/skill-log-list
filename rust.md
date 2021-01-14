# Rust Lang

> <https://www.rust-lang.org>, <https://github.com/rust-lang/book>

```bash
# install
curl https://sh.rustup.rs -sSf | sh

# demo
cargo new hello_world
cargo run
```

## Rust Commands

```bash
# version
rustc --version

# upgrade
rustup update

# uninstall
rustup self uninstall

# local doc
rustup doc

# compile
rustc main.rs
```

## Cargo (dependency manager and build tool)

> <https://doc.rust-lang.org/cargo/>

```bash
cargo --version

# format code
cargo fmt

# create package
cargo new hello_world

# compile package
cargo build

# compile without executable file
cargo check

# compile with optimization
cargo build --release

# compile and run
cargo run

# install dependency
cargo install wasm-pack

# update dependency (va.b.c -> va.b.d)
cargo update
```

## Rust-Lang

```rust
/*
 * variables, mutability, constants
 */
let foo = 5; // immutable
let mut bar = 5; // mutable
const MAX_POINTS: u32 = 100_000; // constants
```

```rust
/*
 * println!
 */
let x = 5;
let y = 10;
println!("x = {} and y = {}", x, y);
```

```rust
/*
 * shadowing
 */
let x = 5;
println!("x 1: {}", x);
let x = x + 1;
println!("x 2: {}", x);
```

```rust
/*
 * data types: scalar types, compound types
 *
 * scalar types: integers, floating-point numbers, Booleans, and characters.
 * Integer Types: i8/u8, i16/u16, i32/u32, i64/u64, i128/u128, isize/usize
 * Floating-Point Types: f32, f64
 * The Boolean Type: bool
 * The Character Type: char
 *
 * compound types: tuples and array
 * The Tuple Type: `let tup: (i32, f64, u8) = (500, 6.4, 1);`
 * The Array Type: `let a: [i32; 5] = [1, 2, 3, 4, 5];`
 */
```

```rust
/*
 * functions
 */
fn plus_one(x: i32) -> i32 {
    x + 1
}
```

```rust
/*
 * comments
 */
// This is a single line comment.
```

```rust
/*
 * control flow
 * if, loop, while, for
 */
// if
if number < 5 {
    println!("condition was true");
} else {
    println!("condition was false");
}

// if in a let statement
let condition = true;
let number = if condition { 5 } else { 6 };

// loop
loop {
    println!("again!");
}

// return value from loop
let mut counter = 0;
let result = loop {
    counter += 1;
    if counter == 10 {
        break counter * 2;
    }
};

// while
let mut number = 3;
while number != 0 {
    println!("{}!", number);
    number -= 1;
}

// for
let a = [10, 20, 30, 40, 50];
for element in a.iter() {
    println!("the value is: {}", element);
}
```

```rust
/*
 * ownership
 * 有所有权的变量，当该变量不再需要时，会释放对应的内存
 */
// only copy stack data, s1 move to s2 (take ownership)
let s1 = String::from("hello");
let s2 = s1;

// s1 is invalid，因为 s2 获取了数据内存的所有权，s1 被回收
println!("{}, world!", s1);

// copy stack and heap data
let s1 = String::from("hello");
let s2 = s1.clone();

println!("s1 = {}, s2 = {}", s1, s2);

// references (does not have ownership )
fn main() {
    let s1 = String::from("hello");
    // &s1 reference s1
    let len = calculate_length(&s1); // calculate_length borrowing s1
    println!("The length of '{}' is {}.", s1, len);
}

fn calculate_length(s: &String) -> usize {
    s.len()
}

// mutable references (does not have ownership)
fn main() {
    let mut s = String::from("hello");
    change(&mut s);
}

fn change(some_string: &mut String) {
    some_string.push_str(", world");
}

// slice (does not have ownership)
let s = String::from("hello");

let len = s.len();

let slice = &s[0..len];
let slice = &s[..];
```

```rust
/*
 * structs
 */
// structs
struct User {
    username: String,
    email: String,
    sign_in_count: u64,
    active: bool,
}

let user1 = User {
    email: String::from("someone@example.com"),
    username: String::from("someusername123"),
    active: true,
    sign_in_count: 1,
};

// ..
let user2 = User {
    email: String::from("another@example.com"),
    username: String::from("anotherusername567"),
    ..user1
};

// tuple structs
struct Color(i32, i32, i32);
struct Point(i32, i32, i32);

let black = Color(0, 0, 0);
let origin = Point(0, 0, 0);

// pringt struct
#[derive(Debug)]
struct Rectangle {
    width: u32,
    height: u32,
}

/*
 * methods
 * their first parameter is always self
 */
#[derive(Debug)]
struct Rectangle {
    width: u32,
    height: u32,
}

impl Rectangle {
    fn area(&self) -> u32 {
        self.width * self.height
    }
}

/**
 * associated functions: Rectangle::square(3)
 * > they don’t have an instance of the struct to work with.
 */ 
impl Rectangle {
    fn square(size: u32) -> Rectangle {
        Rectangle {
            width: size,
            height: size,
        }
    }
}

// multiple impl Blocks
impl Rectangle {
    fn area(&self) {}
}
impl Rectangle {
    fn can_hold(&self) {}
}
```

```rust
/*
 * enum
 * https://doc.rust-lang.org/stable/book/ch06-01-defining-an-enum.html#defining-an-enum
 */
enum IpAddrKind {
    V4,
    V6,
}

let four = IpAddrKind::V4;
let six = IpAddrKind::V6;
fn route(ip_kind: IpAddrKind) {}

// with type
enum Message {
    Quit,
    Move { x: i32, y: i32 },
    Write(String),
    ChangeColor(i32, i32, i32),
}

impl Message {
    fn call(&self) {
        // method body would be defined here
    }
}

let m = Message::Write(String::from("hello"));
m.call();

// option
// https://doc.rust-lang.org/stable/book/ch06-01-defining-an-enum.html#the-option-enum-and-its-advantages-over-null-values
enum Option<T> {
    Some(T),
    None,
}

fn main() {
    let some_number = Some(5);
    let some_string = Some("a string");

    let absent_number: Option<i32> = None;
}

// match
enum Coin {
    Penny,
    Nickel,
    Dime,
    Quarter,
}

fn value_in_cents(coin: Coin) -> u8 {
    match coin {
        Coin::Penny => 1,
        Coin::Nickel => 5,
        Coin::Dime => 10,
        Coin::Quarter => 25,
    }
}
```