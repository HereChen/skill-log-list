# Rust Lang

> <https://www.rust-lang.org>, <https://github.com/rust-lang/book>

```bash
# install
curl https://sh.rustup.rs -sSf | sh

# demo
cargo new hello_world
cargo run
```

## Basic Command

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
// variables, mutability, constants
let foo = 5; // immutable
let mut bar = 5; // mutable
const MAX_POINTS: u32 = 100_000; // constants

// println!
let x = 5;
let y = 10;
println!("x = {} and y = {}", x, y);

// shadowing
let x = 5;
println!("x 1: {}", x);
let x = x + 1;
println!("x 2: {}", x);
```
