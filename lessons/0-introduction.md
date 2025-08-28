# Numbers and Terminology

## Introduction
Understanding **numbers and their properties** is fundamental for zero-knowledge proofs (ZKPs). Cryptography relies heavily on different types of numbers and fields to ensure security, efficiency, and mathematical rigor.

## Explanation

### Integers
The set of **Integers** is denoted by $$\mathbb{Z}$$.  
Example:  
$$\mathbb{Z} = \{\dots, -4, -3, -2, -1, 0, 1, 2, 3, 4, \dots\}$$

### Rational Numbers
The set of **Rational Numbers** is denoted by $$\mathbb{Q}$$.  
Example:  
$$\mathbb{Q} = \left\{ \dots, -\frac{3}{2}, -1, 0, \frac{1}{2}, 1, \frac{3}{2}, \dots \right\}$$

### Real Numbers
The set of **Real Numbers** is denoted by $$\mathbb{R}$$.  
Example:  
$$\mathbb{R} = \{ -4, 0, 2, \pi, \sqrt{2}, 613, \dots \}$$

### Fields
A **field** is a set with two operations: **addition** and **multiplication**, satisfying certain axioms: associativity, commutativity, identities, inverses, and distributivity.  

- Finite fields are denoted by $$\mathbb{F}$$  
- Real or complex fields are denoted by $$\mathbb{K}$$  
- Integers modulo a prime $$p$$: $$\mathbb{Z}^*_p$$

We use **finite fields** in cryptography because their elements have **short, exact representations** and useful mathematical properties.

### Example: Finite Field
For prime $$p = 5$$, the finite field is:  
$$\mathbb{Z}^*_5 = \{0,1,2,3,4\}$$

Operations are done **modulo 5**. For example:  
$$3 \times 4 = 12 \equiv 2 \pmod{5}$$

This field is **cyclic** and has **generators** 2 and 3, meaning repeated powers of the generator produce all elements:

~~~~
# Cyclic generation example
g = 2
2^0 mod 5 = 1
2^1 mod 5 = 2
2^2 mod 5 = 4
2^3 mod 5 = 3
2^4 mod 5 = 1  # cycle repeats
~~~~

## Tables

| Number Type | Symbol | Example |
|-------------|--------|---------|
| Integers | $$\mathbb{Z}$$ | -2, 0, 3 |
| Rational | $$\mathbb{Q}$$ | 1/2, 2, -3/4 |
| Real | $$\mathbb{R}$$ | √2, π, 5 |
| Finite Field | $$\mathbb{Z}^*_5$$ | 0,1,2,3,4 |

## Key Takeaways

- **Integers, rationals, and reals** form the foundation of numbers in ZKPs.  
- **Fields** provide a structured set with addition and multiplication rules.  
- **Finite fields** are critical in cryptography and ZK proofs due to their compact representation.  
- **Generators** in cyclic fields allow traversal of all elements via repeated operations.  


---

# Big O Notation

## Introduction
Understanding **Big O notation** is crucial for evaluating the efficiency of algorithms and zero-knowledge proof (ZKP) systems. It allows us to describe how **time or space requirements** grow as the size of the input increases, which is vital for designing scalable cryptographic protocols.

## Explanation

### What is Big O?
**Big O notation** expresses the **upper bound** on the time or space complexity of an algorithm. It captures how the resource usage grows **in the worst case** as a function of input size $$n$$.

- Example: An algorithm with complexity $$O(n^2)$$ means that if the input size doubles, the time required roughly quadruples.

Mathematically, if a function $$f(n)$$ represents the time taken for input size $$n$$, we write:  

$$
f(n) = O(g(n))
$$

where $$g(n)$$ is a simpler function (like $$n$$, $$n^2$$, $$\log n$$) representing the growth rate.

### Why Big O Matters in ZKPs
In **ZKP systems**, we often deal with large proofs, circuits, or cryptographic operations. Big O notation helps us:

1. Compare different proof systems (e.g., zkSNARKs vs zkSTARKs).  
2. Predict how computation or proof verification scales as **problem size increases**.  
3. Identify bottlenecks in cryptographic constructions.

### Examples

- **Linear Complexity:** $$O(n)$$  
  Doubling input doubles the work.
  
- **Quadratic Complexity:** $$O(n^2)$$  
  Doubling input quadruples the work.

- **Logarithmic Complexity:** $$O(\log n)$$  
  Increasing input size has a mild effect on time.

#### Example in ZKP
Suppose a ZKP circuit has $$n$$ constraints.  
- A naive verification may take $$O(n^2)$$ time.  
- An optimized zkSNARK protocol may reduce verification to $$O(\log n)$$.

~~~~
# Pseudocode example
for i in 1..n:
    for j in 1..n:
        check_constraint(i, j)  # O(n^2) complexity
~~~~

## Tables

| Growth Type | Big O | Example Scenario |
|------------|-------|----------------|
| Constant | O(1) | Check a single proof element |
| Logarithmic | O(log n) | Optimized verification of proof |
| Linear | O(n) | Verify n constraints sequentially |
| Quadratic | O(n^2) | Nested loop over n circuit elements |
| Cubic | O(n^3) | Multi-level combinatorial checks |

## Key Takeaways

- **Big O notation** describes the **upper bound** of algorithmic complexity.  
- It focuses on **worst-case growth** relative to input size $$n$$.  
- Essential for **analyzing ZKP performance** and scaling cryptographic systems.  
- Helps identify **efficient vs inefficient** operations in proof generation and verification.



---


# Elliptic Curves

## Introduction — why this topic matters in ZKPs or cryptography
**Elliptic curves** are foundational in modern cryptography, including **zero-knowledge proofs (ZKPs)**. They allow us to perform secure operations like key exchange, digital signatures, and polynomial commitments efficiently. Their algebraic structure ensures strong security while keeping computation manageable.

## Explanation

### What is an Elliptic Curve?
An **elliptic curve** is a set of points $P = (x, y)$ satisfying an equation such as:

$$
y^2 = x^3 + ax + b
$$

where $a$ and $b$ are constants. In addition to these points, there is an **identity element** called the **point at infinity**.

Certain elliptic curves satisfy the **group axioms**:

1. **Closure:** Every two points can be added to produce a third point.  
2. **Commutativity:** The order of addition does not matter.  
3. **Associativity:** The sum of multiple points does not depend on grouping.  
4. **Identity element:** There exists a unique point that acts as zero under addition.  

### Point Addition
The **point addition** operation combines two points on the curve to produce another point on the curve. Geometrically:

- Draw a line through two points on the curve.  
- The line intersects the curve at a third point.  
- Reflect that point over the x-axis to get the sum.  

This operation allows us to define **scalar multiplication**, the basis of elliptic curve cryptography.

~~~~
# Mermaid diagram: point addition
graph TD
A[Point P] --> C[Sum P+Q]
B[Point Q] --> C
~~~~

### Families of Elliptic Curves
We often use two main families:

#### Montgomery Curves
General form:  

$$
y^2 = x^3 + Ax^2 + x
$$

- Example: **Curve25519**  

$$
y^2 = x^3 + 486662x^2 + x
$$

- Security: 128-bit  
- Usage: Diffie–Hellman key exchange (ECDH)  
- Other curves: **BN254 / BN_128** (Ethereum zkSNARKs), **BLS12-381** (ZCash)

#### Edwards Curves
General form:  

$$
x^2 + y^2 = 1 + dx^2y^2
$$

- Special case: $a=1$  
- If $a \neq 1$: **Twisted Edwards Curves**  
- Equivalent to Montgomery curves via birational transformation

### Scalar Multiplication
**Scalar multiplication** is repeated addition of a point:

$$
[k]P = \underbrace{P + P + \dots + P}_{k \text{ times}}
$$

Where $k$ is a scalar and $+$ is point addition. This operation underlies most elliptic curve cryptography operations.

### Roots of Unity
Over a finite field $\mathbb{F}_p$, an elliptic curve has a finite number of points, including the **identity element** $O$.  

- **Roots of unity** are points $P$ such that:

$$
[n]P = O
$$

- $n$ is the **order of the point** $P$  
- Essential for cyclic subgroups used in ZKPs

### Pairings
**Pairings** are bilinear maps used in advanced ZKP techniques (KZG commitments, BLS signatures):

$$
e: G_1 \times G_2 \rightarrow G_T
$$

where $G_1, G_2, G_T$ are groups of prime order $p$.  

Properties:

1. **Non-degeneracy:** $e(P, Q) \neq 1$ for all non-zero points  
2. **Bilinearity:**  

$$
e(aP, bQ) = e(P, Q)^{ab}
$$

#### Use in ZKPs
Pairings allow verification of arithmetic relationships without revealing inputs, crucial for **verifying computations on circuits**.

~~~~
# Example: verifying a pairing relationship
P --> Q
Q --> R
R --> S[Check e(P,Q) = e(R,S)]
~~~~

## Tables

| Concept | Definition | Example / Usage |
|---------|------------|----------------|
| Elliptic Curve | Set of points $(x, y)$ satisfying $y^2 = x^3 + ax + b$ | Curve25519, BLS12-381 |
| Point Addition | Combines two points on the curve | $P + Q = R$ |
| Scalar Multiplication | Repeated point addition | $[k]P$ |
| Roots of Unity | Points returning to identity after repeated addition | $[n]P = O$ |
| Pairings | Bilinear map between groups | $e: G_1 \times G_2 \to G_T$ |

## Key Takeaways

- **Elliptic curves** provide a group structure enabling cryptographic operations.  
- **Point addition** and **scalar multiplication** are fundamental operations.  
- **Roots of unity** define cyclic subgroups used in ZKPs.  
- **Pairings** allow verification of arithmetic relations in proofs without revealing secrets.  
- Different **curve families** (Montgomery, Edwards) offer trade-offs in performance and security.


---


# Polynomials in Cryptography and ZKPs

## Introduction — why this topic matters in ZKPs or cryptography
**Polynomials** are central in cryptography and **zero-knowledge proofs (ZKPs)** because they can compactly encode large amounts of information. For instance, a single polynomial equation can represent an unbounded set of equations between numbers. Polynomials enable efficient **commitments, evaluations, and verifications** in zk proving systems.

## Explanation

### What is a Polynomial?
A **polynomial** is an expression built from constants and variables using **addition**, **multiplication**, and **exponentiation to non-negative integers**.  

Example:

$$
P(x) = 3x^3 + 2x^2 - 5x + 7
$$

Vitalik Buterin notes:

> "Polynomials are a single mathematical object that can contain an unbounded amount of information (think of them as a list of integers). A single equation between polynomials can represent an unbounded number of equations between numbers."

For example, if:

$$
A(x) + B(x) = C(x)
$$

then this implies:

$$
\begin{align}
A(0)+B(0) &= C(0) \\
A(1)+B(1) &= C(1) \\
A(2)+B(2) &= C(2) \\
A(3)+B(3) &= C(3) \\
&\dots
\end{align}
$$

### Adding, Multiplying, and Dividing Polynomials
Polynomials can be combined using:

- **Addition:** Combine coefficients of the same degree  
- **Multiplication:** Distribute terms across polynomials  
- **Division:** Factor polynomials if a root is known  

Example: If a polynomial $P(x)$ has a root $r$, we can factor it as:

$$
P(x) = (x - r) Q(x)
$$

where $Q(x)$ is a polynomial of one degree lower.

### Roots of Polynomials
For a polynomial $P(x)$ over a field $\mathbb{F}$, a **root** is an element $r \in \mathbb{F}$ such that:

$$
P(r) = 0
$$

- If $r$ is a root, $P(x)$ is divisible by $(x - r)$.  
- Polynomial long division allows factoring when roots are known.

### Schwartz-Zippel Lemma
A key property of polynomials:

> "Different polynomials are different at most points."

Formally, if $P(x)$ and $Q(x)$ are distinct polynomials of degree at most $d$, then they intersect at no more than $d$ points.  

- **Equal polynomials:** Evaluate to the same value at all points or have identical coefficients.  
- **Non-equal polynomials:** For most inputs, $P(x) \neq Q(x)$, especially in large finite fields.

**Example:** Over a finite field of size $p$:

$$
x^p - x = 0 \quad \forall x \in \mathbb{F}_p
$$

Polynomials $x^p - x$ and $0$ take the same values at all points but have different coefficients.

### Lagrange Interpolation
Given a set of $n$ points, **Lagrange interpolation** produces a unique polynomial of degree $n-1$ passing through all points.

- **2 points:** Single straight line  
- **3 points:** Single quadratic curve  
- **n points:** Polynomial of degree $n-1$

This is useful in ZKPs for constructing polynomials that encode secret values or evaluations.

### Polynomial Representations
Polynomials can be represented in two main ways:

1. **Coefficient form:** List of coefficients  
   $$
   P(x) = a_0 + a_1 x + a_2 x^2 + \dots + a_n x^n
   $$
2. **Point-value form:** List of points $(x_i, P(x_i))$  

Conversion between forms:

- **Evaluation:** Coefficient → Point-value  
- **Interpolation:** Point-value → Coefficient

## Tables

| Concept | Definition | Example / Usage |
|---------|------------|----------------|
| Polynomial | Expression with variables and constants | $3x^3 + 2x^2 - 5x + 7$ |
| Root | Value where polynomial evaluates to 0 | $r$ s.t. $P(r)=0$ |
| Factorization | Express polynomial in terms of roots | $P(x) = (x-r)Q(x)$ |
| Schwartz-Zippel | Polynomials differ at most $d$ points | Detect equality efficiently in large fields |
| Lagrange Interpolation | Polynomial passing through given points | Constructing secret-sharing polynomials |
| Representations | Coefficient form or point-value form | Switch via evaluation/interpolation |

## Key Takeaways

- **Polynomials encode unbounded information** in a compact mathematical form.  
- **Roots and factorization** are essential for dividing and manipulating polynomials.  
- **Schwartz-Zippel lemma** ensures distinct polynomials rarely collide on large fields.  
- **Lagrange interpolation** allows constructing polynomials through given points.  
- **Two representations** (coefficient vs point-value) enable flexible computation in ZKPs.

