# Complexity Theory

Complexity theory studies the **time and space requirements** to solve computational problems as the size of the input grows. Understanding complexity helps determine which problems are feasible to solve efficiently and which are not.

---

## Introduction to Complexity

We classify problems according to how the time required to solve them scales with input size $$\(n\)$$. 

- **Polynomial-time problems (P)**: If the time required grows as $$\(O(n^k)\)$$ for some constant $$\(k\)$$, the problem is considered tractable.
- **Verification**: We are also interested in how long it takes to **verify** a proposed solution once found.

**Example**: The Travelling Salesman Problem (TSP) aims to find the shortest route visiting each city exactly once.

- For 3 cities, all routes can be checked quickly.
- For 20 cities, brute-forcing becomes computationally infeasible.

---


![complex theory](img/Screenshot%202022-03-01%20at%2011.04.49.png)

--- 
# Decision Problems and Complexity Classes

---

## Decision Problems

A **decision problem** is a computational problem where the answer is strictly **yes** or **no**.

### Examples
- "Is a given number prime?" → Yes/No  
- "Does this graph contain a cycle?" → Yes/No  

These problems are often used to study computational complexity because they allow us to clearly classify problems into categories.

---

## Key Complexity Classes

| Term | Definition |
|------|------------|
| **P** | Problems solvable in polynomial time |
| **NP** | Problems where "yes" solutions can be verified in polynomial time |
| **NP-Complete** | Hardest problems in NP; any NP problem can be reduced to them |
| **NP-Hard** | Problems at least as hard as NP-complete, not necessarily in NP |

---

## Class **P**

- **Definition**: Problems that can be solved in **polynomial time** by a deterministic algorithm.  
- **Meaning**: The time required grows reasonably (like $n^2$ or $n^3$) with input size $n$.  
- **Example**: Sorting a list of numbers.  
- **Example**: Checking if a number is prime (using modern deterministic algorithms).

If a problem is in **P**, it is considered **efficiently solvable**.

---

## Class **NP**

- **Definition**: Problems for which a "yes" answer can be **verified in polynomial time** if given a certificate (proof).  
- **Meaning**: Even if finding the solution is hard, checking a candidate solution is easy.  
- **Example**: Given a Sudoku puzzle solution, checking if it is correct takes polynomial time.  
- **Example**: In cryptography, verifying a digital signature is quick, even though finding the secret key is hard.

NP does **not** mean "not polynomial". It means **nondeterministic polynomial verification**.

---

## NP-Complete Problems

- **Definition**: Problems in **NP** that are at least as hard as every other NP problem.  
- **Formal requirement**:
  1. The problem is in **NP**.  
  2. Every problem in NP can be **reduced** to it in polynomial time.  

- **Intuition**: If you find a fast algorithm for one NP-complete problem, you can solve **all NP problems** efficiently.  

### Examples
- Boolean satisfiability problem (**SAT**)  
- Traveling Salesman Problem (decision version: "Is there a tour shorter than $k$?")  
- Graph coloring (e.g., "Can this graph be colored with 3 colors?")

**Key point**: No polynomial-time algorithm is known for NP-complete problems, but if one is found, it changes everything (P = NP).

---

## NP-Hard Problems

- **Definition**: Problems at least as hard as NP-complete problems.  
- **Difference from NP-complete**: They are **not required to be decision problems** and may not even belong to NP.  
- **Example**: Optimization version of Traveling Salesman (find the shortest route, not just yes/no).  
- **Example**: Some video game challenges, like specific levels of **Tetris** or **Super Mario**, have been proven NP-hard.

---

## Relationships Between Classes

- **P** ⊆ **NP**  
- **NP-Complete** ⊆ **NP**  
- **NP-Hard** ⊇ **NP-Complete**

### Summary Table

| Class | In NP? | Must be Decision Problem? | Example |
|-------|--------|----------------------------|---------|
| **P** | Yes | Yes | Sorting numbers |
| **NP** | Yes | Yes | Sudoku solution checking |
| **NP-Complete** | Yes | Yes | SAT problem |
| **NP-Hard** | Not always | Not always | TSP optimization |

---

## The Big Question: **P vs NP**

The famous **P vs NP problem** asks:

- **Is P = NP?**  
- In other words: If a problem's solution can be verified quickly, can it also be **solved quickly**?

This is one of the **biggest open problems** in computer science. A correct answer would have enormous consequences for cryptography, algorithms, and our understanding of computation.

---
# Interactive Proofs (IP)

---

## What Are Interactive Proofs?

An **interactive proof (IP)** is a protocol between two parties:

- **Prover (P):** Wants to convince the verifier that a statement is true.  
- **Verifier (V):** Checks the validity of the statement but should not learn any extra secrets.

Unlike classical proofs, interactive proofs involve **back-and-forth communication**.

---

## Why Are Interactive Proofs Important?

- They are the foundation of **zero-knowledge proofs (ZKPs)**.  
- The verifier becomes convinced of the truth of a statement without gaining access to the hidden data.  
- Widely used in **cryptography** and **blockchain protocols**.

---

## Key Properties

An interactive proof system has two main properties:

1. **Completeness**  
   - If the statement is **true**, an honest prover can convince the verifier with high probability.  
   - Example: If $x$ is indeed in a certain set, then the verifier should accept after interaction.  

2. **Soundness**  
   - If the statement is **false**, no cheating prover can convince the verifier (except with small probability).  
   - Example: If $x$ is not in the set, the verifier should reject, regardless of the prover’s strategy.  

---

## Example: Graph Non-Isomorphism

Suppose the prover wants to convince the verifier that **two graphs $G_1$ and $G_2$ are not isomorphic** (cannot be transformed into each other by renaming nodes).

### Protocol Steps:
1. The verifier randomly picks one of the two graphs ($G_1$ or $G_2$) and permutes (relabels) it to form $H$.  
2. The verifier sends $H$ to the prover.  
3. The prover must answer which graph ($G_1$ or $G_2$) $H$ came from.  

- If $G_1$ and $G_2$ are not isomorphic, the prover can always answer correctly.  
- If they are isomorphic, the prover cannot do better than guessing (50% success).  

This interactive process convinces the verifier **without revealing isomorphism mappings**.

---

## Interactive Proofs vs Classical Proofs

| Feature | Classical Proof | Interactive Proof |
|---------|-----------------|-------------------|
| **Format** | One-way, static | Two-way, interactive |
| **Verifier’s Role** | Reads and checks proof | Asks questions and verifies responses |
| **Information Leakage** | May reveal secret | Can hide secret (basis for ZKPs) |
| **Applications** | Mathematics, formal logic | Cryptography, blockchain, ZKPs |

---

## From Interactive Proofs to Zero-Knowledge Proofs

An **interactive proof** can be strengthened into a **zero-knowledge proof** if it satisfies an additional property:

- **Zero-Knowledge**: The verifier learns nothing beyond the validity of the statement.  

This is done by designing the protocol so that the verifier’s view can be simulated **without** interaction with the prover.

---

## Formal Class: IP

- **IP** is the class of problems that can be solved using interactive proofs.  
- A famous result:  
  $$ \text{IP} = \text{PSPACE} $$  
  Meaning, anything that can be computed with polynomial space can also be verified with an interactive proof.

---

## Applications in Blockchain and Cryptography

- **Zero-Knowledge Proofs (ZKPs):** SNARKs, STARKs.  
- **Authentication protocols:** Prove identity without revealing password.  
- **Secure multiparty computation:** Parties jointly compute functions without revealing inputs.  

---

## Summary

- **Interactive Proofs (IP)** involve dialogue between prover and verifier.  
- They ensure **completeness** (true statements accepted) and **soundness** (false statements rejected).  
- They are the **foundation of ZKPs**, which add the **zero-knowledge** property.  
- They are deeply connected to complexity theory ($\text{IP} = \text{PSPACE}$).  
- Widely applied in **blockchains, privacy, and cryptography**.  

**Reference**: [Everything provable is provable in zero knowledge](https://dl.acm.org/doi/pdf/10.5555/88314.88333)

---

# Big O Notation

**Big O notation** expresses the **upper bound** of time or space complexity as input size \(n\) grows.


## Summary Table of Common Time Complexities

| Complexity | Formula | Description | Example |
|------------|---------|-------------|---------|
| **Constant** | $$O(1)$$ | Takes the same time regardless of input size | Accessing an array element |
| **Logarithmic** | $$O(\log n)$$ | Grows very slowly as input increases | Binary search |
| **Linear** | $$O(n)$$ | Time grows proportionally with input size | Summing array elements |
| **Linearithmic** | $$O(n \log n)$$ | Common in efficient divide-and-conquer algorithms | Merge sort, Quick sort (avg) |
| **Quadratic** | $$O(n^2)$$ | Time grows with the square of input size | Bubble sort, checking all pairs |
| **Exponential** | $$O(2^n)$$ | Doubles in time with each extra input element | Brute force SAT solving |
| **Factorial** | $$O(n!)$$ | Extremely fast growth, infeasible for large inputs | Brute-forcing TSP |

**Example**:

```text
for i in 1..n:
    for j in 1..n:
        do_something()
```

- The above algorithm is $$\(O(n^2)\)$$ because the inner operation runs $$\(n \times n\)$$ times.

### Visualization of Growth Rates

![Big O Growth](img/Comparison_computational_complexity.png)

*Figure: Growth of different complexity classes as input size increases.*



#### We use this notation when comparing ZKP systems


![Big O ](img/SH7BExt.webp)
--
