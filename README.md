# Learning how to Rust

## Hello, World!

```rust
fn main() {
    println!("Hello, world!");
}
```

### Compile and Run

- `rustc main.rs`
- `./main`

### Notes

- `println!` is not a normal function, it ends with a `!`, therefore, it is a macro
  - macros don’t always follow the same rules as functions.
- `;` to end lines
- Rust is an _ahead-of-time compiled_ language, meaning you can compile a program and give the executable to someone else, and they can run it even without having Rust installed.

---

## Using Cargo

```bash
cargo new <project_name>
```

### Building and Running a Cargo Project

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
