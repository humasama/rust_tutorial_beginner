# Rust Language Principle

There are two concepts are extreme important in Rust:
1. Onwership (Move/Copy): propose for memory safety.
2. Borrowing Check: propose for safe pointer access.

## Ownership
As we discussed in ![Data Type](https://github.com/humasama/rust_tutorial_beginner/blob/main/Data_Type.md),
ownership is proposed for heap data to safely free.

Ownership makes Rust to make memory safety guarantees without needing a garbage collector.
Memory is managed through a system of ownership with a set of rules that the **`compiler`** checks.
1. Every value has an owner (i.e., variable).
2. Assignment operation causes the data either moved or copied. Once move happens, the old variable is invalid anymore.
3. Any group of simple scalar values can implement Copy trait. **`Nothing`** that **`requires allocation`** or is some form of resource can implement **`Copy`**.
4. When the variable goes out of scope, the value will be **`dropped`**.

## Borrowing Check
The Rust version of C pointer is reference.
As we know in C, pointers can be simultaneously by threads, and C doesn't provide any limitations on pointer access.
Different from C, a reference is guaranteed to point to a valid value of a particular type for the life of that reference.
We call the action of creating a reference as ***Borrowing***.
As in real life, if a person owns something, you can borrow it.
When you are done, you must give it back. You **DON'T OWN** it.


1. To avoid **`Race Condition`**:
- at any time, you can either have one mutable reference or multiple immutable references.
2. To avoid **`Dangling Reference`** (i.e., value is dropped, but reference still alive):
- Reference must be valid. It is not allowed in any case that the reference may **outlive** the varibale.
- **Lifetime** allows us to give compiler enough information about borrowed variables so that it can ensure references will be valid in more situations than it could wihtou our help.
