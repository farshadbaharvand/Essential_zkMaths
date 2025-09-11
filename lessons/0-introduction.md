# Essential Maths for Zero Knowledge Proofs

## Laurence Kirk - Extropy.IO

These notes are available at our [website](https://maths.extropy.io) or as a single [pdf](https://bit.ly/ExtropyMathsForZK)

![QR Code](img/bit.ly_ExtropyMathsForZK.png)

**Extropy.IO**

Pester me via  
- **Twitter**: @Extropy  
- **Email**: info@extropy.io  
- **Discord**: https://discord.gg/VSCHXqQE  

---

## Quote from Remco Bloemen (remco@0x.org)

> **Disclaimer: contains maths**  
>  
> If you don’t understand something:  
> - Not your fault, this stuff is hard  
> - Nobody understands it fully  
>  
> If you don’t understand anything:  
> - My fault, anything can be explained at some level  
>  
> If you do understand everything:  
> - Collect your Turing Award & Fields Medal  

### Advice
- **Don’t try to understand everything at once**  
- **Get familiar with the terminology** even if you don’t know all the details  
- **Chunk topics** into smaller areas  

---

# Numbers and Terminology: A Beginner-Friendly Guide

This guide introduces the **basic number sets** and **fields**, with examples, tables, and step-by-step explanations. It is designed to be fully formatted in Markdown and ready to save as a `.md` file.

---

## 1. Integers

The set of **Integers** is denoted by:

$$
\mathbb{Z} = \{\dots, -4, -3, -2, -1, 0, 1, 2, 3, 4, \dots \}
$$

**Explanation:**  
Integers include negative numbers, zero, and positive numbers. They are the fundamental building blocks for arithmetic operations like addition, subtraction, multiplication, and division (excluding fractions).

**Examples:**
- Positive integers: 1, 2, 3
- Negative integers: -1, -2, -3
- Zero: 0

**Table: Integers Examples**

| Negative | Zero | Positive |
|----------|------|----------|
| -3       | 0    | 1        |
| -2       |      | 2        |
| -1       |      | 3        |

---

## 2. Rational Numbers

The set of **Rational Numbers** is denoted by:

$$
\mathbb{Q} = \{ \frac{p}{q} \ \bigg|\ p \in \mathbb{Z},\ q \in \mathbb{Z} \setminus \{0\}\}
$$

**Explanation:**  
Rational numbers are numbers that can be expressed as the fraction of two integers. They include integers (where the denominator is 1) and fractions like 1/2 or 22/7.

**Examples:**
- $\frac{3}{2}$ (fraction)
- $2$ (integer, since $2 = \frac{2}{1}$)
- $\frac{22}{7}$ (approximation of $\pi$)

**Tips:**  
- Rational numbers can always be written as terminating or repeating decimals.
- Fractions must have a **non-zero denominator**.

---

## 3. Real Numbers

The set of **Real Numbers** is denoted by:

$$
\mathbb{R} = \{ 2, -4, 613, \pi, \sqrt{2}, \dots \}
$$

**Explanation:**  
Real numbers include all rational and irrational numbers. Irrational numbers, like $\pi$ and $\sqrt{2}$, cannot be written as fractions.

**Examples:**
- Rational: $4$, $-7$, $\frac{3}{4}$
- Irrational: $\pi$, $\sqrt{2}$

**Table: Real Numbers Categories**

| Type       | Examples        |
|------------|----------------|
| Rational   | 1/2, -3, 4     |
| Irrational | π, √2, e       |

---

## 4. Fields

A **field** is a set equipped with two operations: **addition** and **multiplication**, satisfying certain properties (closure, associativity, identity, inverses, distributivity).

**Notation:**
- Finite field: $\mathbb{F}$
- Real or complex field: $\mathbb{K}$
- Integers modulo a prime $p$ with multiplicative inverses: $\mathbb{Z}^*_p$

**Explanation:**  
Fields are used in cryptography because:
- Elements have **short, exact representations**
- They support **arithmetic operations with inverses**
- They enable **modular arithmetic** and advanced protocols like zero-knowledge proofs

**Example: Finite Field modulo 5**

$$
\mathbb{Z}_5^* = \{1, 2, 3, 4\}
$$

**Operations mod 5:**
- $3 + 4 \equiv 2 \ (\text{mod } 5)$
- $2 \times 3 \equiv 1 \ (\text{mod } 5)$

**Table: Finite Field Elements and Operations (mod 5)**

| a | b | a + b (mod 5) | a × b (mod 5) |
|---|---|----------------|----------------|
| 1 | 2 | 3              | 2              |
| 3 | 4 | 2              | 2              |
| 2 | 3 | 0              | 1              |

**Notes:**
- Modular arithmetic ensures results stay **within the field**.
- Finite fields are **cyclic**, meaning a generator element can produce all elements of the field by repeated multiplication.

---

**Summary Table: Number Sets**

| Set               | Symbol        | Includes                       |
|------------------|---------------|--------------------------------|
| Integers          | $\mathbb{Z}$ | ..., -2, -1, 0, 1, 2, ...     |
| Rational Numbers  | $\mathbb{Q}$ | Fractions of integers          |
| Real Numbers      | $\mathbb{R}$ | Rational + Irrational numbers  |
| Finite Fields     | $\mathbb{F}$ | Elements mod prime p           |

---

# Modular Arithmetic, Group Theory, and Fields: A Comprehensive Guide

This guide provides a **step-by-step, beginner-friendly explanation** of modular arithmetic, group theory, and fields, complete with **formulas, tables, examples, diagrams, and tips**. All content is formatted in Markdown and ready to save as a `.md` file.

---

## 1. Modular Arithmetic

**Definition:**  
Modular arithmetic deals with integers and a **modulus**, denoted as `n mod k`, meaning the **remainder** when `n` is divided by `k`.

**Examples:**

$$
25 \mod 3 = 1
$$

$$
15 \mod 4 = 3
$$

**Note:** The remainder should always be positive.

**Explanation:**  
Modular arithmetic is often called "clock arithmetic" because numbers wrap around after reaching the modulus. It is widely used in cryptography, computer science, and number theory.

**Table: Examples of Modulo Operation**

| n   | k | n mod k |
|-----|---|---------|
| 25  | 3 | 1       |
| 15  | 4 | 3       |
| 7   | 5 | 2       |

**Tips:**  
- Modular arithmetic is **cyclic**: after reaching k, it resets to 0.  
- Useful for **hashing, cryptography, and random number generation**.

---

## 2. Group Theory

**Definition:**  
A **group** is a set of elements $\{a, b, c, ...\}$ with a **binary operation** (denoted `•`) that satisfies **four properties**:

1. **Closure:**  
   For all $a, b \in G$, $a • b \in G$.
2. **Associativity:**  
   $(a • b) • c = a • (b • c)$ for all $a, b, c \in G$.
3. **Identity element:**  
   There exists $e \in G$ such that $e • a = a • e = a$ for all $a \in G$.
4. **Inverse element:**  
   For each $a \in G$, there exists $a^{-1} \in G$ such that $a • a^{-1} = a^{-1} • a = e$.

**Subgroups:**  
A **subgroup** is a subset of a group that itself satisfies all group properties.

**Cyclic Groups and Generators:**  
A **cyclic group** has a generator $g$ such that repeatedly applying the group operation generates all elements of the group:

$$
g^0, g^1, g^2, ..., g^{n-1} = \text{all elements of the group}
$$

**Example Table: Cyclic Group of Order 4**

| Element | Powers of g |
|---------|-------------|
| $$g$$       | $$g^0=1, g^1=g, g^2=g^2, g^3=g^3$$ |

---

## 3. Fields

**Definition:**  
A **field** is a set of elements with **two operations**: addition `+` and multiplication `·`, satisfying the **field axioms**.

### Field Axioms

Let $a, b, c \in \mathbb{F}$:

1. **Associativity:**  
   $a + (b + c) = (a + b) + c$,  $a · (b · c) = (a · b) · c$
2. **Commutativity:**  
   $a + b = b + a$,  $a · b = b · a$
3. **Identity elements:**  
   $0$ for addition: $a + 0 = a$,  
   $1$ for multiplication: $a · 1 = a$
4. **Additive inverses:**  
   For every $a$, there exists $-a$ such that $a + (-a) = 0$
5. **Multiplicative inverses:**  
   For every $a \ne 0$, there exists $a^{-1}$ such that $a · a^{-1} = 1$
6. **Distributivity:**  
   $a · (b + c) = (a · b) + (a · c)$

---

### Finite Fields and Generators

**Definition:**  
A **finite field** has a finite set of elements, often integers modulo a prime $p$: $\mathbb{Z}_p = \{0, 1, ..., p-1\}$.

**Order of a field:**  
The number of elements in the field's set. Must be either:
- **Prime** (prime field)  
- **Power of a prime** (extension field)

**Generator in a Finite Field:**  
An element $g$ such that exponentiating it generates all nonzero elements:

$$
g^0, g^1, g^2, ..., g^{p-2} = \text{all nonzero elements}
$$

**Example: Finite Field $\mathbb{Z}^*_5$**

$$
\mathbb{Z}^*_5 = \{1, 2, 3, 4\}
$$

**Operations modulo 5:**

| a | b | a + b (mod 5) | a × b (mod 5) |
|---|---|----------------|----------------|
| 3 | 4 | 2              | 2              |
| 2 | 3 | 0              | 1              |

**Generators:**  
- 2 and 3 are generators:  
  - Powers of 2: $2^1=2, 2^2=4, 2^3=3, 2^4=1$  
  - Powers of 3: $3^1=3, 3^2=4, 3^3=2, 3^4=1$

**Tips:**  
- Finite fields are **cyclic**, and generators allow compact representation.  
- Modular arithmetic ensures results **stay within the field**, crucial for cryptography.

---

### Summary Table: Number Sets and Fields

| Concept          | Symbol         | Elements / Properties                                    |
|-----------------|----------------|---------------------------------------------------------|
| Modular arithmetic | n mod k       | Remainder after division                                  |
| Group            | G             | Closure, associativity, identity, inverses              |
| Cyclic Group     | -             | Has generator g                                         |
| Field            | $\mathbb{F}$  | Two operations (+, ·), satisfies field axioms          |
| Finite Field     | $\mathbb{Z}_p$| Elements modulo prime, cyclic, has generators          |

---


# Complexity Theory and Big O Notation

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

## 4. Interactive Proofs (IP)

Interactive proofs are the foundation of **zero-knowledge proofs (ZKPs)**:

- Instead of static proofs, they allow a prover and verifier to interact.
- The verifier gains confidence in the correctness of a statement without learning the underlying secret.
- IP systems are widely used in ZKP constructions.

**Reference**: [Everything provable is provable in zero knowledge](https://dl.acm.org/doi/pdf/10.5555/88314.88333)

---

## 5. Big O Notation

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

---

## 6. Summary Notes

- **P vs NP**: P ⊆ NP. Whether P = NP is unknown.
- **NP-Complete**: Hardest problems in NP.
- **NP-Hard**: May not even be in NP but are at least as difficult as NP-Complete.
- **Big O**: Describes algorithm growth; always consider worst-case scenario.
- **Interactive Proofs**: Key for zero-knowledge protocols, allowing verification without revealing secrets.

---

### Tips

1. **Brute force** solutions are feasible only for small inputs.
2. **Polynomial-time verification** is different from polynomial-time solution.
3. Use **reduction techniques** to relate unknown problems to known NP-complete problems.
4. In ZKP, understanding IP is critical: the verifier never learns the secret.

---

### References

1. [Khan Academy: Modular Arithmetic](https://www.khanacademy.org/computing/computer-science/cryptography/modarithmetic/a/what-is-modular-arithmetic)
2. [Classic Nintendo Games Are Computationally Hard](https://arxiv.org/abs/1203.1895)
3. Chiesa, A. [Interactive Proof Videos](https://www.youtube.com/watch?v=pMzpQ82Q88Q)
4. Goldreich, MiCali, Wigderson. *Zero-Knowledge Proofs and Complexity Theory*

