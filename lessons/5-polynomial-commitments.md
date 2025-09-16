
# Polynomial Commitment Schemes

## Introduction

**Commitment schemes** are cryptographic primitives that allow a party to **commit to a value** while keeping it hidden, with the ability to later reveal it. They provide two essential properties:

1. **Binding**: Given a commitment $$c$$, it is hard to find a different pair $$(m', r')$$ such that the commitment equals $$c$$`. This ensures that once a commitment is made, it cannot be changed without detection.
2. **Hiding**: Given a commitment $$c$$, it is computationally hard to learn anything about the committed value $$m$$. This ensures that the committed value remains secret until revealed.

A **polynomial commitment** is a commitment that represents a polynomial succinctly, allowing verification of **evaluations at specific points** without revealing or transmitting the entire polynomial.  

- Given a commitment $$c$$ representing polynomial $$P(x)$$, a prover can convince a verifier of $$P(z)$$ for some chosen $$z$$.
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


