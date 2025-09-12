# Numbers and Terminology: A Beginner-Friendly Guide

# Numbers 

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

# A Guide to Modular Arithmetic

Modular arithmetic is a special kind of arithmetic where numbers **wrap around** after reaching a certain value, called the **modulus**. This guide will walk you step-by-step through the concepts, examples, and applications of modular arithmetic. We will also use formulas, diagrams, and tables to make everything intuitive.

---

## 1. Introduction to Modular Arithmetic

In modular arithmetic, we only care about the **remainder** after dividing a number by some fixed positive integer, called the **modulus**.

- **Definition**: Given integers $$a, b,$$ and a positive integer $$n,$$ we say:

$$
a \equiv b \pmod{n}
$$

if $$n$$ divides $$(a - b)$$.  
In other words, $$a$$ and $$b$$ leave the **same remainder** when divided by $$n$$.

---

## 2. Clock Analogy

One of the most common examples of modular arithmetic is the **12-hour clock**.

- On a 12-hour clock, after 12 comes 1 again.
- If the clock shows 7, and 8 hours pass, the time will be 3, not 15.

This is written as:

$$
7 + 8 \equiv 3 \pmod{12}
$$

### Visualization


![Modular Arithmetic](img/Screenshot%202022-02-21%20at%2009.03.23.png)

*On a clock, numbers wrap around after 12. This is exactly how modular arithmetic works.*

---

## 3. Basic Properties of Modular Arithmetic

Here are some important rules:

| Operation | Property | Example (mod 12) |
|-----------|----------|------------------|
| Addition  | $$(a+b) \bmod n = [(a \bmod n) + (b \bmod n)] \bmod n$$ | $7+8 \equiv 3 \pmod{12}$ |
| Subtraction | $$(a-b) \bmod n = [(a \bmod n) - (b \bmod n)] \bmod n$$ | $5-9 \equiv -4 \equiv 8 \pmod{12}$ |
| Multiplication | $$(a \cdot b) \bmod n = [(a \bmod n) \cdot (b \bmod n)] \bmod n$$ | $2 \cdot 8 \equiv 16 \equiv 4 \pmod{12}$ |
| Zero equivalence | $$n \equiv 0 \pmod{n}$$ | $12 \equiv 0 \pmod{12}$ |

**Note:** Negative results can always be shifted into the range $$0 \leq r < n$$ by adding the modulus.

---

## 4. Step-by-Step Examples

### Example 1: Addition
Find $$15 \pmod{12}$$.

1. Divide 15 by 12: $$15 = 12 \times 1 + 3$$
2. The remainder is **3**.  
So:  
$$15 \equiv 3 \pmod{12}$$

---

### Example 2: Subtraction
Find $$5 - 9 \pmod{12}$$.

1. Compute directly: $$5 - 9 = -4$$
2. Add modulus: $$-4 + 12 = 8$$  
So:  
$$5 - 9 \equiv 8 \pmod{12}$$

---

### Example 3: Multiplication
Find $$2 \times 8 \pmod{12}$$.

1. Multiply: $$2 \times 8 = 16$$
2. Divide by 12: $$16 = 12 \times 1 + 4$$
3. The remainder is **4**.  
So:  
$$2 \times 8 \equiv 4 \pmod{12}$$

---

## 5. Modular Arithmetic in Practice

### 5.1 Cryptography
Modern encryption (RSA, Diffie–Hellman) uses modular arithmetic with very large primes.

### 5.2 Computer Science
Hash functions, pseudorandom number generators, and cyclic redundancy checks use modular arithmetic.

### 5.3 Daily Life
- Calculating days of the week (mod 7).
- Determining leap years (mod 4).
- Scheduling cycles.

---

## 6. Examples with Days of the Week

Since there are 7 days in a week:

- If today is Monday (let’s call it day 1), what day will it be after 10 days?

$$1 + 10 \equiv 11 \equiv 4 \pmod{7}$$

Day 4 is **Thursday**.

---

## 7. Extended Concepts

### 7.1 Modular Exponentiation
This is very important in cryptography.

Example: Compute $$2^{10} \pmod{7}$$.

1. Compute power: $$2^{10} = 1024$$
2. Divide by 7: $$1024 = 146 \times 7 + 2$$  
So:  
$$2^{10} \equiv 2 \pmod{7}$$

---

### 7.2 Modular Inverses
The **modular inverse** of $$a \pmod{n}$$ is a number $$x$$ such that:

$$a \cdot x \equiv 1 \pmod{n}$$

Example: Find inverse of $$3 \pmod{7}$$.

- Try $$x = 5$$: $$3 \cdot 5 = 15 \equiv 1 \pmod{7}$$  
So the inverse of 3 modulo 7 is **5**.

---

## 8. Summary Table

| Concept               | Example                       | Result                  |
|-----------------------|-------------------------------|-------------------------|
| Congruence            | $$15 \equiv 3 \pmod{12}$$     | Same remainder          |
| Addition              | $$7+8 \equiv 3 \pmod{12}$$    | Wraps around            |
| Subtraction           | $$5-9 \equiv 8 \pmod{12}$$    | Negative to positive    |
| Multiplication        | $$2 \times 8 \equiv 4 \pmod{12}$$ | Works like addition |
| Exponentiation        | $$2^{10} \equiv 2 \pmod{7}$$  | Cryptography use        |
| Modular inverse       | $$3 \cdot 5 \equiv 1 \pmod{7}$$ | Inverse is 5          |

---

## 9. Common Pitfalls and Tips

- **Pitfall:** Forgetting to reduce after subtraction (negative results).  
  **Tip:** Always add the modulus to keep results in $$[0, n-1]$$.

- **Pitfall:** Assuming inverses always exist.  
  **Tip:** An inverse exists **only if** $$\gcd(a, n) = 1$$.

- **Pitfall:** Mixing up modulo with division remainder in programming languages.  
  **Tip:** Some languages (like Python, C++) handle negative remainders differently. Always normalize results.


---






## Group Theory

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

## Fields

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
