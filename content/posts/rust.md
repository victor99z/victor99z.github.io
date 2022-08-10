---
title: "Rust"
date: 2022-08-08T21:32:24-03:00
draft: false
math: true
---

# What is Lorem Ipsum?

> Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown `printer` took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged. It was popularised in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages, and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum.

$$
\relax{x} = \int_{-\infty}^\infty
    \hat\xi\,e^{2 \pi i \xi x}
    \,d\xi
$$

$$ f(x,y) = \sqrt{x^2} $$

```rust
fn merge<T: Copy + PartialOrd>(x1: &[T], x2: &[T], y: &mut [T]) {
    assert_eq!(x1.len() + x2.len(), y.len());
    let mut i = 0;
    let mut j = 0;
    let mut k = 0;
    while i < x1.len() && j < x2.len() {
        if x1[i] < x2[j] {
            y[k] = x1[i];
            k += 1;
            i += 1;
        } else {
            y[k] = x2[j];
            k += 1;
            j += 1;
        }
    }
    if i < x1.len() {
        y[k..].copy_from_slice(&x1[i..]);
    }
    if j < x2.len() {
        y[k..].copy_from_slice(&x2[j..]);
    }
}

fn merge_sort<T: Copy + Ord>(x: &mut [T]) {
	let n = x.len();
	let m = n / 2;
 
	if n <= 1 {
		return;
	}
 
	merge_sort(&mut x[0..m]);
	merge_sort(&mut x[m..n]);
 
	let mut y: Vec<T> = x.to_vec();
 
	merge(&x[0..m], &x[m..n], &mut y[..]);
 
	x.copy_from_slice(&y);
}

fn main() {
    println!("Sort numbers ascending");
    let mut numbers = [4, 65, 2, -31, 0, 99, 2, 83, 782, 1];
    println!("Before: {:?}", numbers);
    merge_sort(&mut numbers);
    println!("After:  {:?}\n", numbers);

    println!("Sort strings alphabetically");
    let mut strings = ["beach", "hotel", "airplane", "car", "house", "art"];
    println!("Before: {:?}", strings);
    merge_sort(&mut strings);
    println!("After:  {:?}\n", strings);
}

```