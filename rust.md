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
