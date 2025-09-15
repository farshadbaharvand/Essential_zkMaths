# Elliptic Curves

Elliptic curves are fundamental objects in **modern cryptography**, particularly for digital signatures, key exchange, and zero-knowledge proofs. They form a **mathematical group** under a special addition operation.

---

## Definition

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

## Group Structure

Elliptic curves form a **group** under the **point addition operation**. This means they satisfy the standard group axioms:

1. **Closure**: Adding any two points \(P\) and \(Q\) on the curve produces another point \(R\) on the curve.
2. **Commutativity**: \(P + Q = Q + P\)
3. **Associativity**: \((P + Q) + R = P + (Q + R)\)
4. **Identity element**: The point at infinity $$\(\mathcal{O}\)$$ acts as the identity: \(P + $$\(\mathcal{O}\)$$ = P\)
5. **Inverse element**: For each \(P = (x, y)\), there exists \(-P = (x, -y)\) such that \(P + (-P) = $$\(\mathcal{O}\)$$)

### Point Addition

The **geometric rule** for adding two points \(P\) and \(Q\):

- Draw a straight line through \(P\) and \(Q\)
- The line intersects the curve at a third point \(-R\)
- Reflect \(-R\) over the x-axis to get \(R = P + Q\)

```text
P + Q = R
```

- If \(P = Q\), the line is the **tangent** to the curve at \(P\) (point doubling).
- Point addition defines **scalar multiplication**: \(kP = P + P + \dots + P\) (k times).


![Montgomery](img/mont.jpeg)

### Example: Point Addition on an Elliptic Curve

Suppose we have an elliptic curve:

$$
E: y^2 = x^3 + 2x + 3 \pmod{97}
$$

and two points on the curve:

$$
P = (3, 6), \quad Q = (10, 7).
$$

#### Step 1: Compute the slope
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

#### Step 2: Compute the resulting point
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

#### Final Answer:
$$
P + Q = (86, 62).
$$

---
## Interactive Visualization: Elliptic Curve Point Addition

A highly recommended resource to **see elliptic curve operations in action** is the interactive website [The Animated Elliptic Curve](https://curves.xargs.org/).

This tool allows you to:
- Visualize how points on an elliptic curve are added.
- Understand the role of the **tangent line** when doubling a point.
- Explore how the **point at infinity** serves as the identity element.
- Experiment with different elliptic curves by adjusting parameters.


You can try it yourself here: [curves.xargs.org](https://curves.xargs.org/)

[GITHUB curves.xargs.org](https://github.com/syncsynchalt/animated-curves)



---
## Families of Curves (Montgomery Curves and Edwards Curves )

### Montgomery Curves

![Montgomery](img/mont.jpeg)

Montgomery curves have the form:

$$
By^2 = x^3 + Ax^2 + x
$$

- Efficient for **scalar multiplication**, widely used in key exchange.
- **Example curves**:

| Curve | Equation | Usage | Security |
|-------|---------|-------|----------|
| Curve25519 | $$\(y^2 = x^3 + 486662x^2 + x\)$$ | ECDH key exchange | 128-bit |
| BN254 / BN_128 | Pairing-friendly | Ethereum ZKSNARKS | 128-bit |
| BLS12-381 | Pairing-friendly | ZCash | 128-bit |

**Notes**:

- Montgomery curves allow fast and secure **ECDH operations**.
- They are resistant to certain side-channel attacks when implemented carefully.

---

### Edwards Curves

Edwards curves have the general equation:

$$
ax^2 + y^2 = 1 + dx^2y^2
$$

- $$\(a = 1\)$$ is the standard form; if $$\(a \neq 1\)$$, called **Twisted Edwards Curves**.
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

### Summary Table

| Property | Montgomery Curves | Edwards Curves |
|----------|-----------------|----------------|
| Equation | $$\(By^2 = x^3 + Ax^2 + x\)$$ | $$\(ax^2 + y^2 = 1 + dx^2y^2\)$$ |
| Fast Addition | Moderate | Very Fast |
| Fast Doubling | Moderate | Very Fast |
| Common Use | Key Exchange | Digital Signatures |
| Side-Channel Resistance | Moderate | High |

---

### Key Notes

1. **Identity element** is the point at infinity $$\(\mathcal{O}\)$$.
2. **Point addition** rules ensure the group structure.
3. **Montgomery vs Edwards**: Choice depends on application.
4. Security is based on **ECDLP**, which is hard to solve with classical computers.
5. **Pairing-friendly curves** (BN, BLS) are used in **ZK-SNARKs** and advanced cryptography.

---

#### References

1. [Curve25519 - DJB](https://cr.yp.to/ecdh.html)
2. [BLS12-381 Curve](https://electriccoin.co/blog/new-snark-curve/)
3. [Edwards Curves](https://ed25519.cr.yp.to/)
4. Handbook of Elliptic and Hyperelliptic Curve Cryptography, Cohen et al.

---

# Elliptic Curve Scalar Multiplication and Roots of Unity

Elliptic curves are not only useful for defining points and addition but also for **scalar multiplication**, which forms the backbone of elliptic curve cryptography (ECC). This section explains scalar multiplication and introduces **roots of unity** on elliptic curves.


## Scalar Multiplication

Scalar multiplication is the process of adding a point on an elliptic curve to itself repeatedly. Formally, given:

- An elliptic curve \(E\) defined by:
$$y^2 = x^3 + ax + b$$
- A point $$\(P = (x, y)\)$$ on the curve
- A scalar $$\(k \in \mathbb{Z}^+\)$$

The **scalar multiplication** is defined as:

$$
kP = \underbrace{P + P + \dots + P}_{k \text{ times}}
$$

where the addition $$\(+\)$$ is the **elliptic curve point addition**.

### Step-by-Step Example

Suppose we have a point $$\(P\)$$ on a curve $$\(E\)$$:

1. $$\(1P = P\)$$
2. $$\(2P = P + P\)$$ (point doubling)
3. $$\(3P = 2P + P\)$$
4. Continue this process up to $$\(kP\)$$

**Important Notes**:

- Scalar multiplication is **computationally easy** in the forward direction (computing $$\(kP\)$$).
- Finding $$\(k\)$$ given $$\(P\)$$ and $$\(kP\)$$ is hard, known as the **Elliptic Curve Discrete Logarithm Problem (ECDLP)**.
- This asymmetry underlies the security of ECC.

---

## Roots of Unity on Elliptic Curves

Over a finite field $$\(\mathbb{F}_p\)$$ (where $$\(p\)$$ is prime), an elliptic curve has a **finite number of points**, including the **point at infinity** $$\(\mathcal{O}\)$$, which acts as the **identity element**.

### Definition

A **root of unity** on an elliptic curve is a point $$\(P\)$$ such that when added to itself a certain number of times, it results in the identity element $$\(\mathcal{O}\)$$:

$$
nP = \underbrace{P + P + \dots + P}_{n \text{ times}} = \mathcal{O}
$$

- The integer $$\(n\)$$ is called the **order of the point** $$\(P\)$$.
- The smallest positive integer $$\(n\)$$ satisfying this condition is the **exact order** of $$\(P\)$$.

**Example Table of Orders**:

| Point \(P\) | Scalar \(k\) | Result \(kP\) |
|-------------|--------------|----------------|
| $$\(P\)$$       | 1            | $$\(P\)$$          |
| $$\(P\)$$       | 2            | $$\(2P = P + P\)$$ |
| $$\(P\)$$       | 3            | $$\(3P = 2P + P\)$$|
| ...         | ...          | ...            |
| $$\(P\)$$       | $$\(n\)$$        | $$\(nP = \mathcal{O}\)$$ |

### Key Notes:

- Points of finite order are important in **cryptography**, especially in **group generation**.
- The **generator point** of an elliptic curve is a point with **maximum order**, capable of generating all points in the group by scalar multiplication.

---

## Visualizations

Scalar multiplication can be visualized geometrically:



![Visualizations](img/Screenshot%202022-02-19%20at%2016.01.36.png)

- **Step 1:** Start with point $$\(P\)$$
- **Step 2:** Add $$\(P\)$$ to itself to get $$\(2P\)$$ (point doubling)
- **Step 3:** Continue adding $$\(P\)$$ to reach $$\(3P, 4P, \dots\)$$
- **Step 4:** Eventually, for some $$\(n\)$$, $$\(nP = \mathcal{O}\)$$

These geometric visualizations help understand why the group structure holds.

---

## References and Further Reading

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

## Introduction

A **pairing** (or **bilinear map**) is a function that takes two inputs from two elliptic curve groups and outputs an element in a third group:

$$
e: \mathbb{G}_1 \times \mathbb{G}_2 \rightarrow \mathbb{G}_T
$$

where:

- $$\(\mathbb{G}_1, \mathbb{G}_2\)$$ are groups of **prime order \(p\)**
- $$\(\mathbb{G}_T\)$$ is a target group of the same order
- $$\(p\)$$ is a **large prime** defining the group order

### Key Properties

Pairings have two main properties that make them useful:

1. **Non-degeneracy**  
   Ensures the pairing is not trivial: there exist points $$\(P \in \mathbb{G}_1\)$$ and $$\(Q \in \mathbb{G}_2\)$$ such that:
   $$e(P, Q) \neq 1$$
   This prevents all outputs from collapsing to the identity element.

2. **Bilinearity**  
   For all $$\(u \in \mathbb{G}_1\)$$, $$\(v \in \mathbb{G}_2\)$$, and scalars $$\(a, b \in \mathbb{Z}_p\)$$:
   $$e(u^a, v^b) = e(u, v)^{ab}$$

   **Implications:**

   - Scalar multiplication in the input maps predictably to exponentiation in the output.
   - Allows efficient verification of linear relationships in cryptographic protocols.

### Linear Properties Derived

Pairings also satisfy additive properties:

$$e(P + P', Q) = e(P, Q) \cdot e(P', Q)$$


$$e(P, Q + Q') = e(P, Q) \cdot e(P, Q')$$

These properties are crucial for constructing and verifying **arithmetic circuits** in ZKPs.

---

## Why Pairings Matter

Pairings enable **checking relationships between points efficiently**. For example:

- In **BLS signatures**, pairings allow aggregation of multiple signatures into a single short signature.
- In **KZG commitments**, pairings help verify polynomial evaluations without revealing the polynomial.
- In **SNARKs**, pairings allow succinct verification of large computations.

**Example: Verification with a Pairing**

Suppose we have:

- Generator points $$\(G_1 \in \mathbb{G}_1\)$$, $$\(G_2 \in \mathbb{G}_2\)$$
- Scalars $$\(a, b \in \mathbb{Z}_p\)$$
- Points $$\(P = aG_1\), \(Q = bG_2\)$$

Then:

$$e(P, Q) = e(aG_1, bG_2) = e(G_1, G_2)^{ab}$$

This allows a verifier to check relationships **without knowing the scalars explicitly**.

---

## Summary Table of Properties

| Property           | Definition | Example |
|-------------------|------------|---------|
| Non-degeneracy     | $$\(e(P, Q) \neq 1\)$$ for some $$\(P, Q\)$$ | Ensures pairing produces meaningful outputs |
| Bilinearity        | $$\(e(u^a, v^b) = e(u, v)^{ab}\)$$ | Enables scalar multiplication verification |
| Additivity         | $$\(e(P + P', Q) = e(P, Q) \cdot e(P', Q)\)$$ | Useful for linear combination checks in circuits |
| Commutativity w.r.t scalars | $$\(e(u^a, v) = e(u, v)^a\)$$| Allows flexible verification |

---

## Visual Representation

```
   G1 Elements      x       G2 Elements
      P   ------------------> Q
            e(P, Q)
               |
               v
             GT Element
```

- Pairing maps two elliptic curve points into a target group element.
- Linear operations in $$\(\mathbb{G}_1\)$$ or $$\(\mathbb{G}_2\)$$ reflect in $$\(\mathbb{G}_T\)$$.

---

## Notes and Tips

- Pairings are **computationally expensive**, so cryptographic schemes aim to minimize the number of pairings required.
- Bilinearity enables **succinct proofs**, which is why pairings are heavily used in **zk-SNARKs**.
- Be careful when implementing: **incorrect handling of group elements** can lead to trivial pairings and insecure protocols.
- For further reading, Vitalik Buterin’s explanation is excellent: [Exploring ECP](https://vitalik.eth.limo/general/2017/01/14/exploring_ecp.html).

---

## Applications in Arithmetic Circuits

Pairings allow verifying relationships in computations:

- If a circuit computes $$\(y = a \cdot b\)$$
- Represent $$\(a\)$$ in $$\(\mathbb{G}_1\)$$, $$\(b\)$$ in $$\(\mathbb{G}_2\)$$
- Use pairing to check:
$$e(aG_1, bG_2) = e(G_1, G_2)^y$$

This enables **zero-knowledge verification** without revealing \(a\) or \(b\).

**Tip:** Always use standardized pairing-friendly curves (e.g., **BN254**, **BLS12-381**) to avoid security pitfalls.

