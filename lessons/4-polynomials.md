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

- $$A(0) + B(0) = C(0)$$  
- $$A(1) + B(1) = C(1)$$  
- $$A(2) + B(2) = C(2)$$  
- $$A(3) + B(3) = C(3)$$  

This property is fundamental in cryptography, particularly in **zero-knowledge proofs (ZKPs)**.


---

# Adding, Multiplying, and Dividing Polynomials

In this guide, we will break down how to **add**, **multiply**, and **divide** polynomials step by step, with clear explanations, and examples.

See more: [Polynomial arithmetic](https://en.wikipedia.org/wiki/Polynomial_arithmetic)

---

A **polynomial** is an expression made up of terms that are constants multiplied by powers of a variable.

Example:

$$
P(x) = 3x^3 + 2x^2 - 5x + 7
$$

- **Coefficient**: Numbers like 3, 2, -5, 7.
- **Variable**: The letter $x$.
- **Degree**: The highest power of $x$ (here, degree = 3).
- **Constant term**: A number without a variable (here, 7).

---

## Adding Polynomials

### Rule
To add polynomials:
- **Combine like terms** (terms with the same variable and power).
- Add their coefficients.

### Example
$$
P(x) = 3x^2 + 5x + 1
$$
$$
Q(x) = 2x^2 - 3x + 4
$$

**Step 1:** Line them up by powers of $x$:
$$(3x^2 + 5x + 1) + (2x^2 - 3x + 4)$$

**Step 2:** Add coefficients of like terms:
$$(3+2)x^2 + (5-3)x + (1+4)$$

**Result:**
$$P(x) + Q(x) = 5x^2 + 2x + 5$$

✅ **Tip:** Always align terms by their degree to avoid mistakes.

---

## 3. Subtracting Polynomials

### Rule
To subtract polynomials:
- Distribute the minus sign.
- Then combine like terms.

### Example
$$P(x) = 4x^3 - 2x + 6$$
$$Q(x) = x^3 + 5x - 3$$

**Step 1:** Write subtraction:
$$(4x^3 - 2x + 6) - (x^3 + 5x - 3)$$

**Step 2:** Distribute the minus:
$$4x^3 - 2x + 6 - x^3 - 5x + 3$$

**Step 3:** Combine like terms:
$$(4-1)x^3 + (-2-5)x + (6+3)$$

**Result:**
$$3x^3 - 7x + 9$$

---

## 4. Multiplying Polynomials

### Rule
Use the **distributive property**: multiply each term of one polynomial by every term of the other.

### Example (Binomial × Binomial)
$$
(2x + 3)(x + 4)
$$

**Step 1:** Distribute each term (FOIL method):
- First: $2x \cdot x = 2x^2$
- Outer: $2x \cdot 4 = 8x$
- Inner: $3 \cdot x = 3x$
- Last: $3 \cdot 4 = 12$

**Step 2:** Add results:
$$
2x^2 + 8x + 3x + 12
$$

**Step 3:** Combine like terms:
$$
2x^2 + 11x + 12
$$

---

### Example (Polynomial × Polynomial)
$$
(3x^2 + 2x)(x^2 - x + 4)
$$

Multiply each term of the first polynomial:

- $3x^2 \cdot x^2 = 3x^4$
- $3x^2 \cdot (-x) = -3x^3$
- $3x^2 \cdot 4 = 12x^2$
- $2x \cdot x^2 = 2x^3$
- $2x \cdot (-x) = -2x^2$
- $2x \cdot 4 = 8x$

**Now combine:**
$$
3x^4 + (-3x^3 + 2x^3) + (12x^2 - 2x^2) + 8x
$$

**Result:**
$$
3x^4 - x^3 + 10x^2 + 8x
$$

---

## 5. Dividing Polynomials

### Rule
Use **long division** (like dividing numbers) or **synthetic division** (shortcut for special cases).

---

### Example (Polynomial Long Division)

Divide:
$$
\frac{2x^3 + 3x^2 - x + 5}{x + 1}
$$

**Step 1:** Divide first terms:
$$
\frac{2x^3}{x} = 2x^2
$$

**Step 2:** Multiply divisor by $2x^2$:
$$
(x+1)(2x^2) = 2x^3 + 2x^2
$$

**Step 3:** Subtract:
$$
(2x^3 + 3x^2 - x + 5) - (2x^3 + 2x^2) = x^2 - x + 5
$$

**Step 4:** Repeat process:
- Divide $x^2 / x = x$.
- Multiply: $(x+1)(x) = x^2 + x$.
- Subtract: $(x^2 - x + 5) - (x^2 + x) = -2x + 5$.

**Step 5:** Divide again:
- $-2x / x = -2$.
- Multiply: $(x+1)(-2) = -2x - 2$.
- Subtract: $(-2x + 5) - (-2x - 2) = 7$.

**Final Result:**
$$
2x^2 + x - 2 + \frac{7}{x+1}
$$

✅ **Quotient:** $2x^2 + x - 2$  
✅ **Remainder:** $7$

---

## 6. Summary Table

| Operation | Rule | Example | Result |
|-----------|------|---------|--------|
| Addition  | Combine like terms | $(3x^2+5x+1)+(2x^2-3x+4)$ | $5x^2+2x+5$ |
| Subtraction | Distribute minus, combine like terms | $(4x^3-2x+6)-(x^3+5x-3)$ | $3x^3-7x+9$ |
| Multiplication | Distributive property (FOIL/binomial expansion) | $(2x+3)(x+4)$ | $2x^2+11x+12$ |
| Division | Polynomial long division | $\frac{2x^3+3x^2-x+5}{x+1}$ | $2x^2+x-2+\frac{7}{x+1}$ |

---

## 7. Visual Example of Polynomial Long Division

![Polynomial Long Division](https://upload.wikimedia.org/wikipedia/commons/thumb/f/fd/Polynomial_long_division.png/500px-Polynomial_long_division.png)

*Figure: Step-by-step process of dividing polynomials using long division.*

---

## 8. Key Takeaways

- **Addition/Subtraction**: Combine like terms.  
- **Multiplication**: Use distributive property; be systematic to avoid missing terms.  
- **Division**: Long division works like with numbers; quotient + remainder form.  
- Always double-check by multiplying the quotient and divisor, then adding remainder.

---

## 9. Extra Notes

⚠️ **Common Pitfall:** Forgetting to subtract properly in long division. Always distribute the minus sign!  
💡 **Tip:** Write polynomials in **standard form** (descending powers of $x$) before operating.  
📘 **Application:** Polynomial arithmetic is used in coding theory, computer graphics, and cryptography (e.g., finite fields, elliptic curves).  

---




---

## Roots of Polynomials

For a polynomial $$P(x)$$ over a field $$\mathbb{K}$$, a **root** $$r$$ satisfies:

$$
P(r) = 0
$$

**Divisibility**:

A polynomial $$B(x)$$ divides another polynomial $$A(x)$$ if there exists a polynomial $$C(x)$$ such that:

$$
A(x) = B(x) \cdot C(x)
$$

Notation: $$B | A$$

**Factoring using a root**:

If $$r$$ is a known root of a polynomial $$P(x)$$ of degree $$n$$, we can factor:

$$
P(x) = (x - r) Q(x)
$$

where $$Q(x)$$ is a polynomial of degree $$n-1$$ obtained from polynomial division.

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


