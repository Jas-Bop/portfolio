---
layout: post
title: Library 3.17 Algorithmic Efficiency Homework
author: Jas-Bop
permalink: /homework/3-17/
---

## Popcorn

```python
# Library 3.17 Popcorn - Expand the catalog
import math

n = 16
linear_checks = n
binary_checks = 0 if n == 0 else math.floor(math.log2(n)) + 1

print(n)
print(linear_checks)
print(binary_checks)
```

Prediction: For `n = 8`, linear search needs `8` worst-case checks, and binary search needs `4` worst-case checks. After changing `n` to `16`, linear search doubles to `16`, while binary search only increases to `5`.

Actual output for `n = 16`:

```text
16
16
5
```

Recommendation: For a large catalog that is already sorted and searched many times, binary search is better because its worst-case checks grow slowly. Linear search can still win on a specific target near the front, like book `3` in the warm-up.

## MCQ

MCQ 3.17: 4/4 | answers: A,B,B,C

1. A - Binary search requires a sorted catalog with direct access to entries.
2. B - Work and memory growth help compare two correct searches.
3. B - A quadratic model with `100` checks at `n = 10` uses `400` at `n = 20`.
4. C - A short-books-first heuristic can be useful without guaranteeing the best list.

## Homework

```python
# Library 3.17 Homework - compare catalog growth
n = 12

visits = n
pairs = n * n

print("Books:", n)
print("Visits:", visits)
print("Ordered pairs:", pairs)
```

Prediction: For `n = 12`, the output should be `12`, `12`, and `144` because the scan visits each book once and the ordered-pairs model multiplies `12 * 12`.

Actual output:

```text
Books: 12
Visits: 12
Ordered pairs: 144
```

Doubling explanation: When the catalog doubles from `12` to `24`, visits double from `12` to `24` because visits grow linearly. Ordered pairs grow from `144` to `576` because pairs grow quadratically, and doubling `n` makes `n * n` four times larger.

1,000-book search recommendation:

```python
import math

n = 1000
linear_checks = n
binary_checks = 0 if n == 0 else math.floor(math.log2(n)) + 1

print("Linear worst-case checks:", linear_checks)
print("Binary worst-case checks:", binary_checks)
```

Output:

```text
Linear worst-case checks: 1000
Binary worst-case checks: 10
```

For repeated searches of an already sorted catalog, I recommend binary search because `10` worst-case checks is much better than `1000`. If the catalog is unsorted, the librarian either has to sort it first, which costs extra time, or keep an extra sorted copy, which costs extra memory.

## Tests

Test 1 - doubled catalog.

```python
n = 24

visits = n
pairs = n * n

print("Books:", n)
print("Visits:", visits)
print("Ordered pairs:", pairs)
```

Actual output:

```text
Books: 24
Visits: 24
Ordered pairs: 576
```

Test 2 - empty catalog.

```python
n = 0

visits = n
pairs = n * n

print("Books:", n)
print("Visits:", visits)
print("Ordered pairs:", pairs)
```

Actual output:

```text
Books: 0
Visits: 0
Ordered pairs: 0
```

Growth explanation: The empty catalog confirms both formulas start at zero. The doubled catalog shows that linear work adds one visit per book, while quadratic work compares every book with every book.

## Design Thinking

Librarian need: A librarian needs to choose a search method that still works when the catalog becomes large.

Goal: My goal was to compare correct algorithms by the amount of work they do, not by how short the code looks.

Methods considered: I compared linear search, binary search, and ordered-pair comparison. Linear search works on any catalog, binary search needs sorted direct-access data, and pair comparison is only appropriate when the task really needs every pair.

Prototype: I built small calculators for visits, ordered pairs, and worst-case search checks so the output labels explain the result clearly.

Test/revision: I tested `n = 12`, `n = 24`, `n = 0`, and `n = 1000`. The `n = 1000` test made the recommendation clearer because it shows binary search using only `10` checks compared with linear search’s `1000`.
