# Introduction
This is the basic introduction for Rust.
Layout:
- Rust compiler
- Rustup

## Rust Compiler
rustc is the compiler for the Rust programming language,
provided by the project itself.
Compilers take your source code and produce **binary code**, either as a library or executable.

### 1. rustc
rustc turns Rust source code into LLVM IR.
So it is a front-end of LLVM.

### 2. LLVM
rustc uses LLVM for code generation,
which turns high level representations of source into an **executable binary**.

### 3. Procedure of Compiling Rust Program
```
Source code
|
| lexing
|
A stream of atomic source code units known as tokens
|
| parsing
|
Abstract Syntax Tree (ATS)
|
|
High-Level Intermediate Representation (HIR): desugaring for async fn etc.
|
|
Mid-level Intermediate Representation (MIR): borrow checking
|
|
-------------------------------------------
LLVM Intermediate Representation (LLVM IR)|
|                                         |
|                                         | (Code generation by LLVM)
Binary code                               |
------------------------------------------
```

## Rustup
Rust toolchain is a complete installation of the Rust compiler (rustc) and related tools (like cargo).
Rustup is a tool to manage Rust toolchain,
and it installs rustc and cargo executable binary under **`~/.cargo/bin`**.

### Command
There are different versions of toolchains can be installed and used.
```
rustup update //update the default toolchain
rustup show //show the default toolchain
rustup default nightly //switch the default toolchain into nightly
```
### Toolchain
The toolchain includes a **`std crate`** that abstracts OS functions, like `use std::os::fd::*`.

## Links
- https://rustc-dev-guide.rust-lang.org/overview.html
