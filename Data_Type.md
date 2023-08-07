# Data Type

The below table shows common data type information.

| Type | Variable | Variable Size (Byte) | Variable Location | Value Location | Value Owner | Assignment |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| char | let x: char = '1' | 4 | stack | variable and value are stored together | - | Copy |
| u8 | let x: u8 = 1 | 1 | stack | variable and value are stored together | - | Copy |
| Array, [T; num] | let x: [u8; 10] = [1; 10] | mem::size_of::<[u8; 3]>() | stack | variable and value are stored together | - | Copy |
| Array Reference, &[T; num] | let rx: &[u8; 10] = &x | mem::size_of::<[u8; 3]>() | stack | variable and value are stored together | - | Copy |
| Slice, &[T] | let as: &[u8] = &x[0..3] | 16 (8B pointer, 8B length) | stack | stack | not owner | Copy |
|||||||
| String | let s = String::from("hello") | 24 (8B pointer, 8B capacity, 8B length) | stack | **`Heap`** | owner | **`Move`** |
| String Reference, &String | let ss = &s | 8 (8B pointer) | stack | stack | not owner | Copy |
| String Slice, &str | let s: &str = "123" | 16 (8B pointer, 8B length) | stack | .data section | not owner | Copy |
|||||
| Vec | let v = vec![1, 2, 3] | 24 (8B pointer, 8B capacity, 8B length) | stack | **`Heap`** | owner | **`Move`** |
| Vec Reference, &Vec | let vs = &v | 8 (8B pointer) | stack | stack | not owner | Copy |
| Slice, &[T] | let vs = &v.as_slice() | 16 (8B pointer, 8B length) | stack | stack | not owner | Copy |
||||||
| Box<T> | let b = Box::new(u8) | 8 (8B pointer) | stack | **`Heap`** | owner | **`Move`** |

As we can find the following three important characters:
1. Smart pointer types (Box, String, Vec) are pointers essentially in stack, but point to data in heap;
2. Smart pointer types own the value, but reference not;
3. Move only happens in smart pointer types assignment.

The above three findings are very interesting, as they reveal a **`Design Principle`** of Rust language:
- No matter of programming language, data stored in stack will be freed automatically by OS. To guarantee the safety, Rust only needs to take care of data in heap.
- **`Rust proposes ownership for memory safety`**. So, ownership transfer (i.e., Move) only happens on data in heap, which frees heap memory safety.
- For data in stack, Rust uses Copy to handle the "ownership" concept.

  ## Reference vesus Slice
  Reference is pointer points to the **entire** varibale, and its size is 8B.
  Slice is a reference to **part** of the variable, and its size is 16B (pointer + length).
