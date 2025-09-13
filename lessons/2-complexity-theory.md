# Complexity Theory

Complexity theory studies the **time and space requirements** to solve computational problems as the size of the input grows. Understanding complexity helps determine which problems are feasible to solve efficiently and which are not.

---

## 1. Introduction to Complexity

We classify problems according to how the **time required** to solve them scales with input size \(n\). 

- **Polynomial-time problems (P)**: If the time required grows as \(O(n^k)\) for some constant \(k\), the problem is considered **tractable**.
- **Verification**: We are also interested in how long it takes to **verify** a proposed solution once found.

**Example**: The **Travelling Salesman Problem (TSP)** aims to find the shortest route visiting each city exactly once.

- For 3 cities, all routes can be checked quickly.
- For 20 cities, brute-forcing becomes computationally infeasible since the number of possible tours grows as \((n-1)!\).

---

![complex theory](img/Screenshot%202022-03-01%20at%2011.04.49.png)

*Figure: Relations between complexity classes P, NP, NP-complete, and NP-hard.*

---

## 2. Decision Problems

A **decision problem** is one with a **yes/no** answer.

| Term | Definition |
|------|------------|
| **P** | Problems solvable in polynomial time |
| **NP** | Problems where “yes” solutions can be verified in polynomial time |
| **NP-Complete** | Hardest problems in NP; any NP problem can be reduced to them |
| **NP-Hard** | Problems at least as hard as NP-complete, not necessarily in NP |

**Example**:  
- **Decision version of TSP**: “Is there a tour shorter than distance \(D\)?”  
- This makes TSP a decision problem instead of an optimization problem.

---

## 3. Complexity Classes

### Class P

- Represents decision problems solvable in **polynomial time**.
- Example: Checking if a number is prime using deterministic algorithms like the **AKS primality test**.

### Class NP

- Problems where **“yes” instances** have proofs verifiable in polynomial time.
- Example: Given a set of integers, does a subset sum to exactly zero?  
  - Verifying a candidate subset is easy.
  - Finding the subset may be difficult.

### NP-Complete

- Problems in NP to which any other NP problem can be **reduced** in polynomial time.
- Intuition: If one NP-complete problem is solved efficiently, then **all NP problems** can be solved efficiently.

**Examples**:
- Boolean satisfiability problem (**SAT**)
- Hamiltonian cycle
- TSP (decision version)

### NP-Hard

- Problems **at least as hard** as NP-complete problems.
- They are not required to be decision problems and may not even belong to NP.

**Example**:  
Certain video game challenges, such as **Tetris** or **Super Mario Bros.**, have been shown to be NP-hard.

---

## 4. Interactive Proofs (IP)

Interactive proofs form the foundation of **zero-knowledge proofs (ZKPs)**:

- Instead of static proofs, they allow a **prover** and a **verifier** to interact.
- The verifier gains confidence in the correctness of a statement **without learning the underlying secret**.
- Widely used in cryptography and blockchain systems.

**Key Idea**:  
- The prover convinces the verifier of a fact.  
- The verifier should become convinced **only of the truth of the statement**, not of any hidden information.

**Reference**: [Goldwasser, Micali, Rackoff (1985)](https://dl.acm.org/doi/pdf/10.5555/88314.88333)

---

## 5. Big O Notation

**Big O notation** expresses the **upper bound** of time or space complexity as input size \(n\) grows.

### Common Complexities

- \(O(1)\): Constant time
- \(O($$\log n$$)\): Logarithmic time
- \(O(n)\): Linear time
- \(O(n \log n)\): Linearithmic time
- \(O(n^2)\): Quadratic time
- \(O(2^n)\): Exponential time
- \(O(n!)\): Factorial time

### Example

```python
for i in range(n):
    for j in range(n):
        do_something()
```

- The above algorithm runs \(n \times n = n^2\) times.
- Complexity = \(O(n^2)\).

---

### Summary Table

| Complexity | Growth Rate | Example Algorithm |
|------------|-------------|-------------------|
| \(O(1)\)   | Constant | Accessing an array element |
| \(O(\log n)\) | Logarithmic | Binary search |
| \(O(n)\)   | Linear | Summing an array |
| \(O(n \log n)\) | Linearithmic | Merge sort |
| \(O(n^2)\) | Quadratic | Bubble sort |
| \(O(2^n)\) | Exponential | Solving SAT with brute force |
| \(O(n!)\)  | Factorial | TSP brute force |

---

### Visualization of Growth Rates

![Big O Growth](https://upload.wikimedia.org/wikipedia/commons/7/7e/Comparison_computational_complexity.svg)

*Figure: Growth of different complexity classes as input size increases.*

---

## 6. Reductions and Completeness

A **reduction** is a way to show that solving one problem allows us to solve another.

- If we can reduce problem A to problem B in polynomial time:
  - Solving B efficiently means we can solve A efficiently.

**NP-Completeness Proof Strategy**:
1. Show the problem is in NP.
2. Reduce a known NP-complete problem to it.

---

## 7. Common Pitfalls and Notes

- **Polynomial vs. Exponential**:  
  Polynomial time (\(n^k\)) grows much slower than exponential time (\(2^n\)).  
  For \(n=1000\):
  - \(n^2 = 10^6\) (manageable).
  - \(2^n \approx 10^{301}\) (impossible).

- **Not all exponential problems are impossible**:  
  With small inputs, exponential algorithms can still be practical.

- **P vs NP Question**:  
  It remains one of the **biggest unsolved problems** in computer science:  
  - Is \(P = NP\)?  
  - Clay Mathematics Institute offers a $1M prize for its solution.

---

## 8. Summary

- **P**: Efficiently solvable problems.  
- **NP**: Problems with efficiently verifiable solutions.  
- **NP-Complete**: The hardest problems in NP.  
- **NP-Hard**: At least as hard as NP-complete, possibly harder.  
- **Big O notation**: Describes scaling behavior of algorithms.  
- **Reductions**: Tools to compare problem difficulty.  
- **Interactive Proofs**: Basis of modern cryptography and zero-knowledge systems.  

Understanding complexity theory is essential for identifying **what computers can realistically solve** and for designing algorithms that make the most efficient use of time and space.

---






# Complexity Theory

Complexity theory studies the **time and space requirements** to solve computational problems as the size of the input grows. Understanding complexity helps determine which problems are feasible to solve efficiently and which are not.

---

## 1. Introduction to Complexity

We classify problems according to how the time required to solve them scales with input size \(n\). 

- **Polynomial-time problems (P)**: If the time required grows as \(O(n^k)\) for some constant \(k\), the problem is considered tractable.
- **Verification**: We are also interested in how long it takes to **verify** a proposed solution once found.

**Example**: The Travelling Salesman Problem (TSP) aims to find the shortest route visiting each city exactly once.

- For 3 cities, all routes can be checked quickly.
- For 20 cities, brute-forcing becomes computationally infeasible.

---


![complex theory](img/Screenshot%202022-03-01%20at%2011.04.49.png)


## 2. Decision Problems

A **decision problem** is one with a **yes/no** answer.

| Term | Definition |
|------|-----------|
| **P** | Problems solvable in polynomial time |
| **NP** | Problems where “yes” solutions can be verified in polynomial time |
| **NP-Complete** | Hardest problems in NP; any NP problem can be reduced to them |
| **NP-Hard** | Problems at least as hard as NP-complete, not necessarily in NP |

---

## 3. Complexity Classes

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

## Big O Notation

**Big O notation** expresses the **upper bound** of time or space complexity as input size \(n\) grows.

- \(O(1)\): Constant time
- \(O(n)\): Linear time
- \(O(n^2)\): Quadratic time
- \(O(2^n)\): Exponential time

**Example**:

```text
for i in 1..n:
    for j in 1..n:
        do_something()
```

- The above algorithm is \(O(n^2)\) because the inner operation runs \(n \times n\) times.

| Complexity | Description | Example |
|------------|------------|---------|
| O(1) | Constant | Accessing an array element by index |
| O(log n) | Logarithmic | Binary search |
| O(n) | Linear | Summing elements of an array |
| O(n log n) | Linearithmic | Merge sort |
| O(n^2) | Quadratic | Bubble sort |

**Visualization**:

![Big O Graph](http://science.slc.edu/jmarshall/courses/2002/spring/cs50/BigO/polynomials.gif)



--
