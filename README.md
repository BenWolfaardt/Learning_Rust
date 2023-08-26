# Learning how to Rust

## Chapter 1

### 1.1 Installation

```bash
curl --proto '=https' --tlsv1.2 https://sh.rustup.rs -sSf | sh
# A script to manage different Rust versions
```

- If it errors you'll need a `linker` (`C`) compiler
  - MacOS: `xcode-select --install`
  - Ubuntu: `apt-get install build-essential`

- Add `$HOME/.cargo/env` to your `$PATH`
- `rustc --version`

- Also install
  - `rustup component add rustfmt`  # automatic formatting
  - `rustup component add clippy`  # more linting
    - `cargo clippy`

- Useful
  - `rustup update`
  - `rustup self uninstall`
  - `rustup doc`  # local docs
  - Format any Cargo project with `cargo fmt`
  - `cargo fix`  # automatically fix basic issues the compiler complains about

### 1.2 Hello, World!

```rust
fn main() {
    println!("Hello, world!");
}
```

- Notes
  - `println!` is not a normal function, it ends with a `!`, therefore, it is a macro
    - macros don’t always follow the same rules as functions.
  - `;` to end lines
  - Rust is an _ahead-of-time compiled_ language, meaning you can compile a program and give the executable to someone else, and they can run it even without having Rust installed.

- Compile and Run
  - `rustc main.rs`
  - `./main`

### 1.3 Hello, Cargo!

```bash
cargo new <project_name>
```

- Building and Running a Cargo Project

```bash
cargo build
```

- Creates a binary file at: `target/debug/<project_name>`
- Run binary with `./target/debug/<project_name>`

- Run and Compile in one go

```bash
cargo run
```

- `cargo check` - to check that your ccode can run without producing an executable use
- `cargo build --release` - to build an optimized executable that will take longer to compile, but runs faster for none development work.
