# Complexity Theory

Complexity theory studies the **time and space requirements** to solve computational problems as the size of the input grows. Understanding complexity helps determine which problems are feasible to solve efficiently and which are not.

---

## Introduction to Complexity

We classify problems according to how the time required to solve them scales with input size \(n\). 

- **Polynomial-time problems (P)**: If the time required grows as \(O(n^k)\) for some constant \(k\), the problem is considered tractable.
- **Verification**: We are also interested in how long it takes to **verify** a proposed solution once found.

**Example**: The Travelling Salesman Problem (TSP) aims to find the shortest route visiting each city exactly once.

- For 3 cities, all routes can be checked quickly.
- For 20 cities, brute-forcing becomes computationally infeasible.

---


![complex theory](img/Screenshot%202022-03-01%20at%2011.04.49.png)


## Decision Problems

A **decision problem** is one with a **yes/no** answer.

| Term | Definition |
|------|-----------|
| **P** | Problems solvable in polynomial time |
| **NP** | Problems where “yes” solutions can be verified in polynomial time |
| **NP-Complete** | Hardest problems in NP; any NP problem can be reduced to them |
| **NP-Hard** | Problems at least as hard as NP-complete, not necessarily in NP |

---

## Complexity Classes

### P

- Represents decision problems solvable in polynomial time.
- Example: Checking if a number is prime using deterministic algorithms.

### NP

- Problems where “yes” instances have proofs verifiable in polynomial time.
- **Example**: Recovering a secret key when the plaintext is known. Verifying a candidate key is easy, finding it may not be.

### NP-Complete

- Problems in NP to which any other NP problem can be **reduced** in polynomial time.
- **Intuition**: Solving one NP-complete problem efficiently solves all NP problems efficiently.

### NP-Hard

- Problems **at least as hard** as NP-complete problems.
- They do not need to be decision problems and may not even belong to NP.

**Example**: Some video game challenges, such as certain levels in Tetris or Super Mario, have been proven NP-complete.

---

## Interactive Proofs (IP)

Interactive proofs are the foundation of **zero-knowledge proofs (ZKPs)**:

- Instead of static proofs, they allow a prover and verifier to interact.
- The verifier gains confidence in the correctness of a statement without learning the underlying secret.
- IP systems are widely used in ZKP constructions.

**Reference**: [Everything provable is provable in zero knowledge](https://dl.acm.org/doi/pdf/10.5555/88314.88333)


---

# Big O Notation

**Big O notation** expresses the **upper bound** of time or space complexity as input size \(n\) grows.


## Summary Table of Common Time Complexities

| Complexity | Formula | Description | Example |
|------------|---------|-------------|---------|
| **Constant** | $$O(1)$$ | Takes the same time regardless of input size | Accessing an array element |
| **Logarithmic** | $$O(\log n)$$ | Grows very slowly as input increases | Binary search |
| **Linear** | $$O(n)$$ | Time grows proportionally with input size | Summing array elements |
| **Linearithmic** | $$O(n \log n)$$ | Common in efficient divide-and-conquer algorithms | Merge sort, Quick sort (avg) |
| **Quadratic** | $$O(n^2)$$ | Time grows with the square of input size | Bubble sort, checking all pairs |
| **Exponential** | $$O(2^n)$$ | Doubles in time with each extra input element | Brute force SAT solving |
| **Factorial** | $$O(n!)$$ | Extremely fast growth, infeasible for large inputs | Brute-forcing TSP |

**Example**:

```text
for i in 1..n:
    for j in 1..n:
        do_something()
```

- The above algorithm is \(O(n^2)\) because the inner operation runs \(n \times n\) times.

### Visualization of Growth Rates

![Big O Growth](img/Comparison_computational_complexity.png)

*Figure: Growth of different complexity classes as input size increases.*



#### We use this notation when comparing ZKP systems


![Big O ](img/SH7BExt.webp)
--
