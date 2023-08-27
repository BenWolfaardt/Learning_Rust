# Learning how to Rust

## Chapter 1

### 1.1 Installation

```bash
curl --proto '=https' --tlsv1.2 https://sh.rustup.rs -sSf | sh
# A script to manage different Rust versions
```

- If it errors you'll need a `linker` (`C` compiler)
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

- Compile and Run
  - `rustc main.rs`
  - `./main`

- Notes
  - `println!` is not a normal function, it ends with a `!`, therefore, it is a macro
    - macros don’t always follow the same rules as functions.
  - `;` to end lines
  - Rust is an _ahead-of-time compiled_ language, meaning you can compile a program and give the executable to someone else, and they can run it even without having Rust installed.


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

## Chapter 2 - Programming a Guessing Game

```rust
use std::io;

fn main() {
    println!("Guess the number!");

    println!("Please input your guess.");

    let mut guess = String::new();

    io::stdin()
      .read_line(&mut guess)
      .expect("Failed to read the l");

    println!("You guessed: {guess}");
}
```

- Notes
  - `let` statement to create the variable
    - variables are immutable by default
  - `let mut` to create a mutable variable
  - The `::` syntax in the `::new` line indicates that `new` is an associated function of the `String` type.
    - An _associated function_ is a function that’s implemented on a type, in this case `String`.
  - The `&` indicates that this argument is a _reference_, which gives you a way to let multiple parts of your code access one piece of data without needing to copy that data into memory multiple times.
    - Like variables, references are immutable by default.
  - If you don’t call expect, the program will compile, but you’ll get a warning:
  - Update dependencies with `cargo update` remembering that the default semantic versioning `"x.y.z"` actually implies `^`, therefore, the max version the file could become is `"x.y.<z+a>"`.
  - `cargo doc --open` command will build documentation provided by all your dependencies locally and open it in your browser.

## Cahpter 3 - Common Programming Concepts

- Keywords - [Appendix A](https://doc.rust-lang.org/book/appendix-01-keywords.html)

### 3.1 Variables and Mutability

- By default, variables are immutable.
  - You can make them mutable by adding `mut` in front of the variable name.

#### Constants

- You aren’t allowed to use `mut` with constants.
  - Constants aren’t just immutable by default—they’re always immutable.
- You declare constants using the `const` keyword instead of the `let` keyword, and the type of the value _must_ be annotated.
- The last difference is that constants may be set only to a constant expression, not the result of a value that could only be computed at runtime.

`const THREE_HOURS_IN_SECONDS: u32 = 60 * 60 * 3;`

- Rust’s naming convention for constants is to use all uppercase with underscores between words.

> See the [Rust Reference’s section on constant evaluation](https://doc.rust-lang.org/reference/const_eval.html) for more information on what operations can be used when declaring constants.

#### Shadowing

- You can declare a new variable with the same name as a previous variable.
  - Rustaceans say that the first variable is shadowed by the second, which means that the second variable is what the compiler will see when you use the name of the variable.
  - In effect, the second variable overshadows the first, taking any uses of the variable name to itself until either it itself is shadowed or the scope ends.
- We can shadow a variable by using the same variable’s name and repeating the use of the `let` keyword as follows:

```rust
fn main() {
    let x = 5;

    let x = x + 1;

    {
        let x = x * 2;
        println!("The value of x in the inner scope is: {x}");
    }

    println!("The value of x is: {x}");
}
```

```bash
The value of x in the inner scope is: 12
The value of x is: 6
```

> Shadowing is different from marking a variable as mut because we’ll get a compile-time error if we accidentally try to reassign to this variable without using the let keyword.

> By using let, we can perform a few transformations on a value but have the variable be immutable after those transformations have been completed.

- The other difference between mut and shadowing is that because we’re effectively creating a new variable when we use the let keyword again, we can change the type of the value but reuse the same name.

```rust
    let spaces = "   ";
    let spaces = spaces.len();
```

- However, if we try to use mut for this, as shown here, we’ll get a compile-time error:

```rust
    let mut spaces = "   ";
    spaces = spaces.len();
```

```bash
$ cargo run
   Compiling variables v0.1.0 (file:///projects/variables)
error[E0308]: mismatched types
 --> src/main.rs:3:14
  |
2 |     let mut spaces = "   ";
  |                      ----- expected due to this value
3 |     spaces = spaces.len();
  |              ^^^^^^^^^^^^ expected `&str`, found `usize`

For more information about this error, try `rustc --explain E0308`.
error: could not compile `variables` due to previous error
```
