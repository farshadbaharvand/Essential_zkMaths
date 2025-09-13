# Elliptic Curves

Elliptic curves are fundamental objects in **modern cryptography**, particularly for digital signatures, key exchange, and zero-knowledge proofs. They form a **mathematical group** under a special addition operation.

---

## 1. Definition

An **elliptic curve** over a field is the set of points \((x, y)\) that satisfy an equation of the form:

$$
y^2 = x^3 + ax + b
$$

where \(a\) and \(b\) are constants that satisfy the **non-singularity condition**:

$$
4a^3 + 27b^2 \neq 0
$$

- This condition ensures that the curve has no **cusps or self-intersections**.
- The curve also includes a special point called the **point at infinity**, which acts as the **identity element** in the group.

---

## 2. Group Structure

Elliptic curves form a **group** under the **point addition operation**. This means they satisfy the standard group axioms:

1. **Closure**: Adding any two points \(P\) and \(Q\) on the curve produces another point \(R\) on the curve.
2. **Commutativity**: \(P + Q = Q + P\)
3. **Associativity**: \((P + Q) + R = P + (Q + R)\)
4. **Identity element**: The point at infinity $$\(\mathcal{O}\)$$ acts as the identity: \(P + $$\(\mathcal{O}\)$$ = P\)
5. **Inverse element**: For each \(P = (x, y)\), there exists \(-P = (x, -y)\) such that \(P + (-P) = $$\(\mathcal{O}\)$$)

### 2.1 Point Addition

The **geometric rule** for adding two points \(P\) and \(Q\):

- Draw a straight line through \(P\) and \(Q\)
- The line intersects the curve at a third point \(-R\)
- Reflect \(-R\) over the x-axis to get \(R = P + Q\)

```text
P + Q = R
```

- If \(P = Q\), the line is the **tangent** to the curve at \(P\) (point doubling).
- Point addition defines **scalar multiplication**: \(kP = P + P + \dots + P\) (k times).

## Example: Point Addition on an Elliptic Curve

Suppose we have an elliptic curve:

$$
E: y^2 = x^3 + 2x + 3 \pmod{97}
$$

and two points on the curve:

$$
P = (3, 6), \quad Q = (10, 7).
$$

### Step 1: Compute the slope
Since $$\(P \neq Q\)$$, we use:

$$
m = \frac{y_2 - y_1}{x_2 - x_1} \pmod{97}
$$

Substitute values:

$$
m = \frac{7 - 6}{10 - 3} = \frac{1}{7} \pmod{97}.
$$

Now compute the modular inverse of $$\(7 \pmod{97}\)$$:

$$
7^{-1} \equiv 14 \pmod{97}.
$$

So:

$$
m = 1 \cdot 14 = 14 \pmod{97}.
$$

### Step 2: Compute the resulting point
We now compute the coordinates:

$$
x_3 = m^2 - x_1 - x_2 \pmod{97},
$$

$$
x_3 = 14^2 - 3 - 10 = 196 - 13 = 183 \equiv 86 \pmod{97}.
$$

Then:

$$
y_3 = m(x_1 - x_3) - y_1 \pmod{97},
$$

$$
y_3 = 14(3 - 86) - 6 = 14(-83) - 6.
$$

Reduce modulo \(97\):

$$
14 \cdot (-83) = -1162 \equiv 68 \pmod{97}.
$$

So:

$$
y_3 = 68 - 6 = 62 \pmod{97}.
$$

### Final Answer:
$$
P + Q = (86, 62).
$$

---

## 3. Families of Curves

### 3.1 Montgomery Curves

![Montgomery](img/mont.jpeg)

Montgomery curves have the form:

$$
By^2 = x^3 + Ax^2 + x
$$

- Efficient for **scalar multiplication**, widely used in key exchange.
- **Example curves**:

| Curve | Equation | Usage | Security |
|-------|---------|-------|----------|
| Curve25519 | \(y^2 = x^3 + 486662x^2 + x\) | ECDH key exchange | 128-bit |
| BN254 / BN_128 | Pairing-friendly | Ethereum ZKSNARKS | 128-bit |
| BLS12-381 | Pairing-friendly | ZCash | 128-bit |

**Notes**:

- Montgomery curves allow fast and secure **ECDH operations**.
- They are resistant to certain side-channel attacks when implemented carefully.

---

### 3.2 Edwards Curves

Edwards curves have the general equation:

$$
ax^2 + y^2 = 1 + dx^2y^2
$$

- \(a = 1\) is the standard form; if \(a \neq 1\), called **Twisted Edwards Curves**.
- They are **birationally equivalent** to Montgomery curves.
- Advantages:
  - Unified formulas for addition and doubling
  - Faster implementations for signatures

**Example:**

- Twisted Edwards curve for Ed25519:

$$
-x^2 + y^2 = 1 + \frac{-121665}{121666} x^2y^2
$$

**Tips**:

- Edwards curves are preferred for **digital signatures** due to speed and simplicity.
- Montgomery curves are preferred for **key exchange** due to secure scalar multiplication.

---

## 4. Scalar Multiplication

**Scalar multiplication** is the repeated addition of a point:

$$
kP = \underbrace{P + P + \dots + P}_{k \text{ times}}
$$

- Fundamental for **ECC cryptography**.
- Hard to reverse (Elliptic Curve Discrete Logarithm Problem, ECDLP).
- Security relies on the difficulty of solving ECDLP.

---

## 5. Summary Table

| Property | Montgomery Curves | Edwards Curves |
|----------|-----------------|----------------|
| Equation | \(By^2 = x^3 + Ax^2 + x\) | \(ax^2 + y^2 = 1 + dx^2y^2\) |
| Fast Addition | Moderate | Very Fast |
| Fast Doubling | Moderate | Very Fast |
| Common Use | Key Exchange | Digital Signatures |
| Side-Channel Resistance | Moderate | High |

---

## 6. Key Notes

1. **Identity element** is the point at infinity \(\mathcal{O}\).
2. **Point addition** rules ensure the group structure.
3. **Montgomery vs Edwards**: Choice depends on application.
4. Security is based on **ECDLP**, which is hard to solve with classical computers.
5. **Pairing-friendly curves** (BN, BLS) are used in **ZK-SNARKs** and advanced cryptography.

---

### References

1. [Curve25519 - DJB](https://cr.yp.to/ecdh.html)
2. [BLS12-381 Curve](https://electriccoin.co/blog/new-snark-curve/)
3. [Edwards Curves](https://ed25519.cr.yp.to/)
4. Handbook of Elliptic and Hyperelliptic Curve Cryptography, Cohen et al.

---

# Elliptic Curve Scalar Multiplication and Roots of Unity

Elliptic curves are not only useful for defining points and addition but also for **scalar multiplication**, which forms the backbone of elliptic curve cryptography (ECC). This section explains scalar multiplication and introduces **roots of unity** on elliptic curves.

---

## 1. Scalar Multiplication

Scalar multiplication is the process of adding a point on an elliptic curve to itself repeatedly. Formally, given:

- An elliptic curve \(E\) defined by:
$$
y^2 = x^3 + ax + b
$$
- A point \(P = (x, y)\) on the curve
- A scalar \(k \in \mathbb{Z}^+\)

The **scalar multiplication** is defined as:

$$
kP = \underbrace{P + P + \dots + P}_{k \text{ times}}
$$

where the addition \(+\) is the **elliptic curve point addition**.

### Step-by-Step Example

Suppose we have a point \(P\) on a curve \(E\):

1. \(1P = P\)
2. \(2P = P + P\) (point doubling)
3. \(3P = 2P + P\)
4. Continue this process up to \(kP\)

**Important Notes**:

- Scalar multiplication is **computationally easy** in the forward direction (computing \(kP\)).
- Finding \(k\) given \(P\) and \(kP\) is hard, known as the **Elliptic Curve Discrete Logarithm Problem (ECDLP)**.
- This asymmetry underlies the security of ECC.

---

## 2. Roots of Unity on Elliptic Curves

Over a finite field \(\mathbb{F}_p\) (where \(p\) is prime), an elliptic curve has a **finite number of points**, including the **point at infinity** \(\mathcal{O}\), which acts as the **identity element**.

### Definition

A **root of unity** on an elliptic curve is a point \(P\) such that when added to itself a certain number of times, it results in the identity element \(\mathcal{O}\):

$$
nP = \underbrace{P + P + \dots + P}_{n \text{ times}} = \mathcal{O}
$$

- The integer \(n\) is called the **order of the point** \(P\).
- The smallest positive integer \(n\) satisfying this condition is the **exact order** of \(P\).

**Example Table of Orders**:

| Point \(P\) | Scalar \(k\) | Result \(kP\) |
|-------------|--------------|----------------|
| \(P\)       | 1            | \(P\)          |
| \(P\)       | 2            | \(2P = P + P\) |
| \(P\)       | 3            | \(3P = 2P + P\)|
| ...         | ...          | ...            |
| \(P\)       | \(n\)        | \(nP = \mathcal{O}\) |

### Key Notes:

- Points of finite order are important in **cryptography**, especially in **group generation**.
- The **generator point** of an elliptic curve is a point with **maximum order**, capable of generating all points in the group by scalar multiplication.

---

## 3. Visualizations

Scalar multiplication can be visualized geometrically:



![Visualizations](img/Screenshot%202022-02-19%20at%2016.01.36.png)

- **Step 1:** Start with point \(P\)
- **Step 2:** Add \(P\) to itself to get \(2P\) (point doubling)
- **Step 3:** Continue adding \(P\) to reach \(3P, 4P, \dots\)
- **Step 4:** Eventually, for some \(n\), \(nP = \mathcal{O}\)

These geometric visualizations help understand why the group structure holds.

---

## 4. References and Further Reading

- **Book**: Serious Cryptography, Jean-Philippe Aumasson


- **Video Tutorial**: [Elliptic Curve Arithmetic](https://www.youtube.com/watch?v=_JiPcvtr8sY)

**Tips**:

1. Remember that **scalar multiplication is repeated point addition**.
2. Always check the **order of points** when selecting a generator for cryptography.
3. Visual aids greatly help in understanding elliptic curve operations.

----

# Pairing in Cryptography

Pairings are fundamental in many advanced cryptographic constructions, particularly in **Zero-Knowledge Proofs (ZKPs)**, **SNARKs**, and **BLS signatures**. This guide explains pairing in a beginner-friendly, step-by-step manner, with formulas, examples, and visualizations.

---

## 1. Introduction

A **pairing** (or **bilinear map**) is a function that takes two inputs from two elliptic curve groups and outputs an element in a third group:

$$
e: \mathbb{G}_1 \times \mathbb{G}_2 \rightarrow \mathbb{G}_T
$$

where:

- \(\mathbb{G}_1, \mathbb{G}_2\) are groups of **prime order \(p\)**
- \(\mathbb{G}_T\) is a target group of the same order
- \(p\) is a **large prime** defining the group order

### Key Properties

Pairings have two main properties that make them useful:

1. **Non-degeneracy**  
   Ensures the pairing is not trivial: there exist points \(P \in \mathbb{G}_1\) and \(Q \in \mathbb{G}_2\) such that:
   $$
   e(P, Q) \neq 1
   $$
   This prevents all outputs from collapsing to the identity element.

2. **Bilinearity**  
   For all \(u \in \mathbb{G}_1\), \(v \in \mathbb{G}_2\), and scalars \(a, b \in \mathbb{Z}_p\):
   $$
   e(u^a, v^b) = e(u, v)^{ab}
   $$

   **Implications:**

   - Scalar multiplication in the input maps predictably to exponentiation in the output.
   - Allows efficient verification of linear relationships in cryptographic protocols.

### Linear Properties Derived

Pairings also satisfy additive properties:

$$
e(P + P', Q) = e(P, Q) \cdot e(P', Q)
$$

$$
e(P, Q + Q') = e(P, Q) \cdot e(P, Q')
$$`

These properties are crucial for constructing and verifying **arithmetic circuits** in ZKPs.

---

## 2. Why Pairings Matter

Pairings enable **checking relationships between points efficiently**. For example:

- In **BLS signatures**, pairings allow aggregation of multiple signatures into a single short signature.
- In **KZG commitments**, pairings help verify polynomial evaluations without revealing the polynomial.
- In **SNARKs**, pairings allow succinct verification of large computations.

**Example: Verification with a Pairing**

Suppose we have:

- Generator points \(G_1 \in \mathbb{G}_1\), \(G_2 \in \mathbb{G}_2\)
- Scalars \(a, b \in \mathbb{Z}_p\)
- Points \(P = aG_1\), \(Q = bG_2\)

Then:

$$
e(P, Q) = e(aG_1, bG_2) = e(G_1, G_2)^{ab}
$$`

This allows a verifier to check relationships **without knowing the scalars explicitly**.

---

## 3. Summary Table of Properties

| Property           | Definition | Example |
|-------------------|------------|---------|
| Non-degeneracy     | \(e(P, Q) \neq 1\) for some \(P, Q\) | Ensures pairing produces meaningful outputs |
| Bilinearity        | \(e(u^a, v^b) = e(u, v)^{ab}\) | Enables scalar multiplication verification |
| Additivity         | \(e(P + P', Q) = e(P, Q) \cdot e(P', Q)\) | Useful for linear combination checks in circuits |
| Commutativity w.r.t scalars | \(e(u^a, v) = e(u, v)^a\) | Allows flexible verification |

---

## 4. Visual Representation

```
   G1 Elements      x       G2 Elements
      P   ------------------> Q
            e(P, Q)
               |
               v
             GT Element
```

- Pairing maps two elliptic curve points into a target group element.
- Linear operations in \(\mathbb{G}_1\) or \(\mathbb{G}_2\) reflect in \(\mathbb{G}_T\).

---

## 5. Notes and Tips

- Pairings are **computationally expensive**, so cryptographic schemes aim to minimize the number of pairings required.
- Bilinearity enables **succinct proofs**, which is why pairings are heavily used in **zk-SNARKs**.
- Be careful when implementing: **incorrect handling of group elements** can lead to trivial pairings and insecure protocols.
- For further reading, Vitalik Buterin’s explanation is excellent: [Exploring ECP](https://vitalik.eth.limo/general/2017/01/14/exploring_ecp.html).

---

## 6. Applications in Arithmetic Circuits

Pairings allow verifying relationships in computations:

- If a circuit computes \(y = a \cdot b\)
- Represent \(a\) in \(\mathbb{G}_1\), \(b\) in \(\mathbb{G}_2\)
- Use pairing to check:
$$
e(aG_1, bG_2) = e(G_1, G_2)^y
$$

This enables **zero-knowledge verification** without revealing \(a\) or \(b\).

**Tip:** Always use standardized pairing-friendly curves (e.g., **BN254**, **BLS12-381**) to avoid security pitfalls.

----

# Polynomial Introduction

A **polynomial** is an expression constructed from constants and variables using **addition**, **multiplication**, and **exponentiation to a non-negative integer power**. 

Example:

$$
3x^{2} + 4x + 3
$$

---

### Why Polynomials Matter

Vitalik Buterin notes:

> "There are many things that are fascinating about polynomials. But here we are going to zoom in on a particular one: **polynomials are a single mathematical object that can contain an unbounded amount of information**."

A **single polynomial equation** can represent an **unbounded number of equations between numbers**. For example, if:

$$
A(x) + B(x) = C(x)
$$

then this also implies:

- $A(0) + B(0) = C(0)$  
- $A(1) + B(1) = C(1)$  
- $A(2) + B(2) = C(2)$  
- $A(3) + B(3) = C(3)$  

This property is fundamental in cryptography, particularly in **zero-knowledge proofs (ZKPs)**.

---

## Adding, Multiplying, and Dividing Polynomials

Polynomials can be:

- **Added**: sum coefficients of like powers
- **Multiplied**: distributive property applied
- **Divided**: polynomial long division

See more: [Polynomial arithmetic](https://en.wikipedia.org/wiki/Polynomial_arithmetic)

---

## Roots of Polynomials

For a polynomial $P(x)$ over a field $\mathbb{K}$, a **root** $r$ satisfies:

$$
P(r) = 0
$$

**Divisibility**:

A polynomial $B(x)$ divides another polynomial $A(x)$ if there exists a polynomial $C(x)$ such that:

$$
A(x) = B(x) \cdot C(x)
$$

Notation: $B | A$

**Factoring using a root**:

If $r$ is a known root of a polynomial $P(x)$ of degree $n$, we can factor:

$$
P(x) = (x - r) Q(x)
$$

where $Q(x)$ is a polynomial of degree $n-1$ obtained from polynomial division.

---

## Schwartz-Zippel Lemma

This lemma provides a probabilistic guarantee about polynomials:

- If two polynomials $f$ and $g$ of degree at most $d$ are **not equal**, they can intersect at **no more than $d$ points**.
- In large fields, two low-degree polynomials are either **identical** or **different almost everywhere**.

Example visualization:



![Schwartz-Zippel Lemma](img/Screenshot%202022-03-01%20at%2012.25.07.png)

- If $f(x) = g(x)$ for all $x$, polynomials are equal.
- If $f(x) \neq g(x)$ for almost all $x$, they are different.

**Important Note:**  
Equality in finite fields is subtle. Polynomials can take the same values at all points in the field without having identical coefficients.

Example:

- Field of size $q$ satisfies $x = x$
- Polynomials $X^q$ and $X$ evaluate the same at all points, but their coefficients differ.

---

## Lagrange Interpolation

**Lagrange interpolation** allows constructing a polynomial that passes through a given set of points.

- 2 points → unique straight line (degree 1)  
- 3 points → unique parabola (degree 2)  
- $n$ points → polynomial of degree $n-1$

Example for 3 points:

$$
P(x) = 5x^2 + 2x + 1
$$

This property is extensively used in cryptography and ZKPs to **encode information in a polynomial**.

Visualization:

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/4/41/Interpolation_example_polynomial.svg/440px-Interpolation_example_polynomial.svg.png" alt="" style="object-fit: scale-down">

---

## Summary Table: Polynomial Concepts

| Concept                  | Definition / Rule                                         | Example                            |
|---------------------------|-----------------------------------------------------------|------------------------------------|
| Polynomial               | Expression with constants and variables                   | $3x^2 + 4x + 3$                   |
| Root                     | $r$ s.t. $P(r) = 0$                                      | $x-2$ divides $x^2 -4$            |
| Divisibility             | $B | A$ iff $A = BC$                                     | $(x-1) | (x^2-1)$                  |
| Factoring                | $P(x) = (x-r)Q(x)$                                       | $x^2-3x+2 = (x-1)(x-2)$           |
| Schwartz-Zippel Lemma    | Two non-equal polynomials intersect at ≤ degree points   | $f(x) \neq g(x)$ at most $d$ points|
| Lagrange Interpolation   | Polynomial passes through $n$ points                     | 3 points → degree 2 polynomial     |

---

### Notes and Tips

- Polynomials are **powerful abstractions** for encoding multiple equations compactly.
- In **finite fields**, be cautious: **evaluation equality ≠ coefficient equality**.
- Lagrange interpolation is central in **secret sharing schemes**, **commitments**, and **ZKPs**.
- Visualizing roots and intersections helps understand polynomial behavior.

----

## Representations

Polynomials can be represented in **two main ways**:

1. **Coefficient Form**  
   Expressed directly using coefficients for each power of $x$:

   $$
   f(x) = a_0 + a_1 x + a_2 x^2 + a_3 x^3 + \dots
   $$

   This is convenient for algebraic manipulation, addition, multiplication, and storing the polynomial compactly.

2. **Point-Value Form**  
   Represented as a set of points:

   $$
   (x_1, y_1), (x_2, y_2), \dots
   $$

   Here, each $y_i = f(x_i)$. This form is convenient for **evaluation-based protocols**, like those in zero-knowledge proofs.

**Conversion Between Forms**:  

- **Coefficient → Point**: Evaluate the polynomial at chosen points.
- **Point → Coefficient**: Use **Lagrange interpolation** or similar techniques.

---

# Transformations

In the context of **Zero-Knowledge Proofs (ZKPs)**, transformations are crucial.  

- Start with a statement, e.g., "I know the square root of 25".
- Transform the problem into a **polynomial representation** that encodes the statement.
- Each transformation must **preserve correctness** and **prevent cheating**.
- Result: the verifier checks simple polynomial relations instead of directly solving the problem.

**Intuition**: Think of transforming a complex claim into a **polynomial equation** whose truth can be efficiently checked.

---

# Polynomials in ZKPs

Polynomials are central in ZKPs because they allow **succinct and probabilistic verification**.

### Simple Protocol for Verifying a Polynomial

1. **Verifier** picks a random value $z$ and evaluates their local polynomial.
2. **Verifier** sends $z$ to the prover.
3. **Prover** evaluates their polynomial at $z$ and returns the result.
4. **Verifier** checks if the returned value matches the local evaluation.  

> If it matches, the statement is likely true with **high confidence**.

This is the basis of **polynomial commitment schemes**, which allow verifiers to check claims about **large polynomials** efficiently.

---

### Zero Polynomial Factorization

If a polynomial $P$ is **zero on a set**:

$$
S = \{x_1, x_2, \dots, x_n\}
$$

then it can be expressed as:

$$
P(x) = Z(x) \cdot H(x)
$$

where:

- $Z(x) = (x - x_1)(x - x_2) \dots (x - x_n)$ is the **vanishing polynomial** for $S$.
- $H(x)$ is another polynomial.

**Interpretation**:  
> Any polynomial that equals zero on a set is a **multiple of the minimal polynomial that vanishes on that set**.

---

### Random Evaluation Guarantees

A powerful result in polynomial-based ZKPs:

- Over a **large field**, evaluating polynomials at a **random point $z$** gives a strong probabilistic guarantee about their **general equality**.

Example:

If, for a random $z$:

$$
P(z) \cdot Q(z) + R(z) = S(z) + 5
$$

then, with overwhelming probability:

$$
P(x) \cdot Q(x) + R(x) = S(x) + 5 \quad \text{for all } x
$$

This is the **core idea behind probabilistic polynomial checks**: verifying at a single random point is sufficient to gain high confidence about the whole polynomial.

---

### Summary Table: Polynomials in ZKPs

| Concept                           | Explanation                                                                 | Example / Formula                                    |
|----------------------------------|----------------------------------------------------------------------------|-----------------------------------------------------|
| Coefficient Form                  | Polynomial expressed by coefficients of powers of $x$                      | $f(x) = a_0 + a_1 x + a_2 x^2 + \dots$           |
| Point-Value Form                  | Polynomial represented by set of evaluated points                           | $(x_1, y_1), (x_2, y_2), \dots$                  |
| Vanishing Polynomial              | Polynomial that is zero on a set $S$                                        | $Z(x) = (x-x_1)(x-x_2)\dots(x-x_n)$              |
| Polynomial Factorization          | Zero polynomial factorized into vanishing polynomial × another polynomial  | $P(x) = Z(x) \cdot H(x)$                          |
| Random Evaluation Check           | Evaluating at random $z$ gives probabilistic confidence for whole polynomial| $P(z) \cdot Q(z) + R(z) = S(z) + 5 \implies P(x) \cdot Q(x) + R(x) = S(x) + 5$ |

---

### Notes and Tips

- **Coefficient vs Point Form**: Use coefficient form for algebra, point form for evaluation-based protocols.
- **Random Point Checks**: Evaluating a polynomial at a single random point gives strong guarantees, but only over a sufficiently large field.
- **Vanishing Polynomials**: Essential in **ZKPs and polynomial commitments** to check that a polynomial vanishes on a set.
- Always ensure the **field is large enough** to avoid collisions in random evaluation.

----

# Polynomial Commitment Schemes

## Introduction

**Commitment schemes** are cryptographic primitives that allow a party to **commit to a value** while keeping it hidden, with the ability to later reveal it. They provide two essential properties:

1. **Binding**: Given a commitment `$c$`, it is hard to find a different pair `(m', r')` such that the commitment equals `$c$`. This ensures that once a commitment is made, it cannot be changed without detection.
2. **Hiding**: Given a commitment `$c$`, it is computationally hard to learn anything about the committed value `$m$`. This ensures that the committed value remains secret until revealed.

A **polynomial commitment** is a commitment that represents a polynomial succinctly, allowing verification of **evaluations at specific points** without revealing or transmitting the entire polynomial.  

- Given a commitment `$c$` representing polynomial `$P(x)$`, a prover can convince a verifier of `$P(z)$` for some chosen `$z$`.
- This is particularly useful in **Zero-Knowledge Proofs (ZKPs)**, where polynomials can have **millions of terms**.

**Workflow in ZKPs**:

1. Commit to each polynomial using a commitment scheme.
2. Select a random evaluation point `$z$`.
3. Prover computes polynomial evaluations at `$z$` and generates **proofs**.
4. Verifier checks evaluations and proofs instead of the full polynomials.

**Merkle Tree Approach**:

- Store polynomial evaluations as leaves in a Merkle tree.
- Verifier selects random leaves to check, along with Merkle proofs of membership.
- Provides **succinctness** and **verifiability**.

---

## Role in ZKPs

Polynomial commitments address the challenge of **succinctly proving statements about large polynomials**:

- Polynomials in ZKPs can have sizes like `$10^8$` terms.
- Polynomial commitments reduce communication complexity between prover and verifier.
- They allow **efficient evaluation checks** at randomly chosen points, ensuring correctness with high probability.

---

## Types of Polynomial Commitment Schemes (PCS)

There are several types of PCS, differing in efficiency and cryptographic assumptions:

1. **Kate Commitments (KZG)**  
   - Based on **pairings over elliptic curves**.
   - Very efficient for evaluation proofs.
   - Proof size is **constant**, independent of polynomial degree.

2. **Bulletproofs Polynomial Commitments**  
   - Based on **discrete logarithm assumptions**.
   - Proof size grows **logarithmically** with polynomial degree.
   - No trusted setup required.

3. **Inner Product Argument Based Schemes**  
   - Use **inner-product arguments** for succinct proofs.
   - Proof size grows **logarithmically**.
   - Often used in **STARKs** and **SNARKs** variants.

4. **Merkle Tree Based Commitments**  
   - Polynomial evaluations stored as **Merkle tree leaves**.
   - Proof involves **Merkle paths**.
   - Simple and post-quantum secure, but proof size grows with log(n).


![Polynomial Commitment Schemes](img/Screenshot%202024-08-21%20at%2008.24.43.png)

---

## Comparison of PCS Schemes

| Scheme Type         | Proof Size       | Trust Setup | Security Assumptions          | Notes                                      |
|--------------------|----------------|-------------|------------------------------|-------------------------------------------|
| KZG / Kate          | Constant       | Trusted Setup | Pairing-based assumptions    | Extremely efficient, popular in zk-SNARKs |
| Bulletproofs        | Logarithmic    | None         | Discrete Log                 | No trusted setup, slightly larger proofs  |
| Inner Product Arg.  | Logarithmic    | Optional     | Discrete Log / Fiat-Shamir   | Efficient for STARKs, recursive proofs   |
| Merkle Tree Commit. | Logarithmic    | None         | Hash function                | Post-quantum secure, widely understood   |

> Source: [ZKP Study Group Video](https://www.youtube.com/watch?v=bz16BURH_u8), [Slides](https://docs.google.com/presentation/d/1YJX_MgWjhsFHiubHoCMb5F27rtN9AcxgaKMswGFf8I4/edit#slide=id.p)

---

### Illustrations

- **KZG / Kate Commitments**: Constant-size proofs regardless of polynomial degree.
- **Bulletproofs / Inner Product Arguments**: Proof size grows logarithmically.
- **Merkle Tree Commitments**: Proofs consist of Merkle paths to leaves representing evaluations.


![KZG Illustration](img/Screenshot%202023-08-03%20at%2004.36.25.png)
![Bulletproofs Illustration](img/Screenshot%202023-08-03%20at%2004.49.51.png)
![Inner Product Argument Illustration](img/Screenshot%202023-08-03%20at%2004.53.35.png)
![Merkle Tree Illustration](img/Screenshot%202023-08-03%20at%2004.55.45.png)



---

### Notes and Tips

- **Trusted Setup**: Some schemes (e.g., KZG) require a trusted setup; others (e.g., Bulletproofs) do not.
- **Proof Size**: Choose a scheme depending on required proof succinctness and scalability.
- **Security**: Ensure cryptographic assumptions match the application (pairing, discrete log, hash function security).
- **Efficiency**: KZG is highly efficient for large polynomials, often used in Ethereum and zk-SNARK implementations.

---


# Error Correcting Codes

Error correcting codes are techniques that allow us to **detect and correct errors** in transmitted or stored data. The basic idea is:

- We have a **message**.
- We add **redundancy**.
- The result is a **codeword**, which is longer than the original message but allows for error detection and correction.

---

# Reed-Solomon Codes

Reed-Solomon (RS) codes are a type of **systematic linear code**, meaning the original message is embedded within the encoded data along with extra **redundant symbols**.

- A Reed-Solomon codeword has **length `$n$`**, composed of symbols of `$m$` bits each.  
- `$n$` must satisfy `$n \leq 2^m$`.
- `$k$` symbols carry the **original information**; the remaining `$n-k$` symbols are **redundant**.

**Error correction capability**:

- If up to `$t \leq \frac{n-k}{2}$` symbols are in error, the correct message can still be recovered.
- If `$s$` symbols are **erased** and `$t$` are in error, recovery is possible if:

$$s + 2t \leq n-k$$

**Code rate**:

$$\text{Rate} = \frac{k}{n}$$

> The **decoder** is the device or algorithm that reconstructs the original message from a potentially faulty codeword.

---

## Using Polynomials for Error Correction

RS codes are built using **polynomial arithmetic over finite fields**:

1. Represent the message as polynomial coefficients:

$$A(x) = a_0 + a_1 x + a_2 x^2 + \dots + a_{d-1}x^{d-1}$$

2. Compute the **redundant symbols** as evaluations of the polynomial at selected points:

$$A(1), A(w), A(w^2), \dots, A(w^{n-1}) \quad \text{where } n \gg d$$

- Fast Fourier Transforms (FFTs) can be used for efficient evaluation.

**Application in ZKPs**:

- In **STARKs**, computations are converted into polynomials (**arithmetization**).
- These polynomials are **encoded with Reed-Solomon codes**, extending evaluation points.
- **Error amplification**: A small error in the computation spreads across the extended polynomial, allowing the verifier to detect inconsistencies.



![Reed-Solomon Encoding](img/Screenshot%202023-02-19%20at%2018.28.18.png)


---

# Inner Product Argument

The **inner product** generalizes the dot product from Euclidean spaces:

$$\vec{a} \cdot \vec{b} = a_0 b_0 + a_1 b_1 + \dots + a_{n-1} b_{n-1}$$

Where:

$$\vec{a} = (a_0, a_1, \dots, a_{n-1}), \quad \vec{b} = (b_0, b_1, \dots, b_{n-1})$$

**Polynomial evaluation via inner product**:

- Let $\vec{b} = (1, z, z^2, \dots, z^{n-1})$, then:

$$\vec{a} \cdot \vec{b} = \sum_{i=0}^{n-1} a_i z^i = f(z)$$

- This evaluates the polynomial with coefficients `$\vec{a}$` at point `$z$`.

---

## Inner Product Argument in ZKPs

- Used in **Bulletproofs** for vector commitments.
- Pedersen vector commitment:

$$C = a_0 g_0 + a_1 g_1 + \dots + a_{n-1} g_{n-1}$$

Where `$g_i$` are elliptic curve points, and `$a_i$` are scalars.

- Provides a **binding commitment**: it's infeasible to find another vector that yields the same `$C$`.
- The **inner product argument** allows **succinct verification** of vector properties (like inner product) without revealing all vector elements.
- Verification involves recursively **halving vector size**, reducing the check to a scalar equation.

> For full details, see [Dankrad Feist's article](https://dankradfeist.de/ethereum/2021/07/27/inner-product-arguments.html)

---

# Where to Go Next

## Resources

- [Extropy Awesome Maths Repo](https://github.com/ExtropyIO/AwesomeMaths)  
- [Mina / Kimchi Article](https://extropy-io.medium.com/why-is-mina-so-tasty-part-1-kimchi-5cc8603a4e69)  
- [Introduction to zkML](https://extropy-io.medium.com/when-buzzwords-collide-zkml-1eb2247874e8)  
- [Bootcamps - ZKP / zkML](https://www.encode.club/programmes)  
- [Discord Server](https://discord.gg/VSCHXqQE)  


