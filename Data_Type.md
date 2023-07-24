# Data Type

| Type | Variable | Variable Size (Byte) | Variable Location | Value Location |
|:---:|:---:|:---:|:---:|:---:|
| char | let x: char = '1' | 4 | stack | variable and value are stored together |
| u8 | let x: u8 = 1 | 1 | stack | variable and value are stored together |
| Array, [T; num] | let x: [u8; 10] = [1; 10] | mem::size_of::<[u8; 3]>() | stack | stack |
| Array slice, &[T] | let as: [u8; 3] = &x[0..3] | 16(8B pointer, 8B length) | stack | stack |
| String | let s = String::from("hello") | 24 (8B pointer, 8B capacity, 8B length) | stack | **`Heap`** |
| Vec | let s = !vec[1, 2, 3] | 24 (8B pointer, 8B capacity, 8B length) | stack | **`Heap`** |
