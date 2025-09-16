

# Error Correcting Codes

Error correcting codes are techniques that allow us to **detect and correct errors** in transmitted or stored data. The basic idea is:

- We have a **message**.
- We add **redundancy**.
- The result is a **codeword**, which is longer than the original message but allows for error detection and correction.

---

# Reed-Solomon Codes

Reed-Solomon (RS) codes are a type of **systematic linear code**, meaning the original message is embedded within the encoded data along with extra **redundant symbols**.

- A Reed-Solomon codeword has **length $$n$$**, composed of symbols of $$m$$ bits each.  
- $$n$$ must satisfy $$n \leq 2^m$$.
- $$k$$ symbols carry the **original information**; the remaining $$n-k$$ symbols are **redundant**.

**Error correction capability**:

- If up to $$t \leq \frac{n-k}{2}$$ symbols are in error, the correct message can still be recovered.
- If $$s$$ symbols are **erased** and $$t$$ are in error, recovery is possible if:

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

- This evaluates the polynomial with coefficients $$\vec{a}$$ at point $$z$$.

---

## Inner Product Argument in ZKPs

- Used in **Bulletproofs** for vector commitments.
- Pedersen vector commitment:

$$C = a_0 g_0 + a_1 g_1 + \dots + a_{n-1} g_{n-1}$$

Where $$g_i$$ are elliptic curve points, and $$a_i$$ are scalars.

- Provides a **binding commitment**: it's infeasible to find another vector that yields the same $$C$$.
- The **inner product argument** allows **succinct verification** of vector properties (like inner product) without revealing all vector elements.
- Verification involves recursively **halving vector size**, reducing the check to a scalar equation.

> For full details, see [Dankrad Feist's article](https://dankradfeist.de/ethereum/2021/07/27/inner-product-arguments.html)

---
