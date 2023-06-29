# Collection Types
There are 3 important collection types: `vector`, `array`, and `string`.
In addition, the `slice` type is quite useful to use the three collection types.
So, we have 4 important types.

## Vector and Array
Array:
- Array is a fixed-size list of elements of the same type, implemented as the standard library type **`[T; N]`**.
- Array is allocated from **`stack`**.

Vector:
- Vector is a dynamic or "growable" array, implemented as the standard library type **`Vec<T>`**.
- Vector is allocated from **`heap`**.

```
 let v: Vec<usize> = vec![1, 2, 3, 4, 5, 6];
let a: [usize; 6] = [1, 2, 3, 4, 5, 6];
```

## Slice
Slice is a reference to an **array**, implemented as the standard library type **`&[T]`**.
It is useful for allowing safe, efficient access to a portion of an array without copying.
We can get slice from vector and array.
```
let v_slice: &[usize] = v.as_slice(); // 1, 2, 3, 4, 5, 6
let v_part_slice: &[usize] = &v[0..4]; // 1, 2, 3, 4
let a_slice: &[usize] = a.as_slice(); // 1, 2, 3, 4, 5, 6
let a_part_slice: &[usize] = &a[0..4]; // 1, 2, 3, 4
```

## Type Cast
1. `Vec<T> -> Array [T; N]`

It requires the size of array os equal to the element number of vector.
```
// convert success
let v: Vec<usize> = vec![1, 2, 3, 4, 5, 6];
let v2a: [usize; 6] = v.try_into().unwrap_or_else(|v: Vec<usize>| panic!("Require the vector size is 6, but it is {}", v.len()));
println!("{:?}", &v2a); // [1, 2, 3, 4, 5, 6]

// convert fail
let v: Vec<usize> = vec![1, 2, 3, 4, 5, 6];
let v2a: [usize; 10] = v.try_into().unwrap_or_else(|v: Vec<usize>| panic!("Require the vector size is 10, but it is {}", v.len()));

// convert fail
let v: Vec<usize> = vec![1, 2, 3, 4, 5, 6];
let v2a: [usize; 3] = v.try_into().unwrap_or_else(|v: Vec<usize>| panic!("Require the vector size is 3, but it is {}", v.len()));
```

2. `Array [T; N] -> Vec<T>`
```
let a: [usize; 6] = [1, 2, 3, 4, 5, 6];
let a_slice: &[usize] = a.as_slice();
let a_part_slice: &[usize] = &a[0..4];
let a2v = a_slice.to_owned();
let a2v_part = a_part_slice.to_owned();
println!("a2v: {:?}, av2_part: {:?}", a2v, a2v_part); // a2v: [1, 2, 3, 4, 5, 6], av2_part: [1, 2, 3, 4]
```
