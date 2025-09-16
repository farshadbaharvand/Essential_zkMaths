
# Polynomial Commitment Schemes

## Introduction

**Commitment schemes** are cryptographic primitives that allow a party to **commit to a value** while keeping it hidden, with the ability to later reveal it. They provide two essential properties:

1. **Binding**: Given a commitment $$c$$, it is hard to find a different pair $$(m', r')$$ such that the commitment equals $$c$$. This ensures that once a commitment is made, it cannot be changed without detection.
2. **Hiding**: Given a commitment $$c$$, it is computationally hard to learn anything about the committed value $$m$$. This ensures that the committed value remains secret until revealed.

A **polynomial commitment** is a commitment that represents a polynomial succinctly, allowing verification of **evaluations at specific points** without revealing or transmitting the entire polynomial.  

- Given a commitment $$c$$ representing polynomial $$P(x)$$, a prover can convince a verifier of $$P(z)$$ for some chosen $$z$$.
- This is particularly useful in **Zero-Knowledge Proofs (ZKPs)**, where polynomials can have **millions of terms**.

**Workflow in ZKPs**:

1. Commit to each polynomial using a commitment scheme.
2. Select a random evaluation point $$z$$.
3. Prover computes polynomial evaluations at $$z$$ and generates **proofs**.
4. Verifier checks evaluations and proofs instead of the full polynomials.

**Merkle Tree Approach**:

- Store polynomial evaluations as leaves in a Merkle tree.
- Verifier selects random leaves to check, along with Merkle proofs of membership.
- Provides **succinctness** and **verifiability**.

---

## Role in ZKPs

Polynomial commitments address the challenge of **succinctly proving statements about large polynomials**:

- Polynomials in ZKPs can have sizes like $$10^8$$ terms.
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
