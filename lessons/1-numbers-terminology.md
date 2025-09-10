# Essential Maths for Zero Knowledge Proofs

## Laurence Kirk - Extropy.IO

These notes available at our [website](https://maths.extropy.io) or as a single [pdf](https://bit.ly/ExtropyMathsForZK)

![QR Code](img/bit.ly_ExtropyMathsForZK.png)

**Extropy.IO**

Pester me via  
Twitter : @Extropy  
Email : info@extropy.io  
Discord : [https://discord.gg/VSCHXqQE](https://discord.gg/VSCHXqQE)

---

## Quote from Remco Bloemen remco@0x.org

> Disclaimer: contains maths  
>  
> If you don’t understand something  
> - Not your fault, this stuff is hard  
> - Nobody understands it fully  
>  
> If you don’t understand anything  
> - My fault, anything can be explained at some level  
>  
> If you do understand everything  
> - Collect your Turing Award & Fields Medal  

**My advice**  
- Don't try to understand everything at once  
- Get familiar with the terminology even if you don't know all the details  
- 'Chunk' topics / areas  

---

## Numbers and Terminology

The set of **Integers** is denoted by $$\mathbb Z$$ e.g. {⋯,−4,−3,−2,−1,0,1,2,3,4,⋯}

The set of **Rational Numbers** is denoted by $$\mathbb Q$$ e.g. $$\{...1,\tfrac{3}{2},2,\tfrac{22}{7}...\}$$

The set of **Real Numbers** is denoted by $$\mathbb R$$ e.g. $$\{2, −4, 613, \pi, \sqrt{2}, …\}$$

**Fields** are denoted by $$\mathbb F$$ if they are finite fields, or $$\mathbb K$$ for a field of real or complex numbers.  
We also use $$\mathbb Z^*_p$$ to represent a finite field of integers mod prime $$p$$ with multiplicative inverses.

We use finite fields for cryptography because elements have “short”, exact representations and useful properties.

---

## Modular Arithmetic

See this [introduction](https://www.khanacademy.org/computing/computer-science/cryptography/modarithmetic/a/what-is-modular-arithmetic)

![Modular Arithmetic](img/Screenshot%202022-02-21%20at%2009.03.23.png)

When we write $$n \mod k$$ we mean simply the remainder when $$n$$ is divided by $$k$$.  

**Examples**  
- $$25 \mod 3 = 1$$  
- $$15 \mod 4 = 3$$  

The remainder should be positive.

---

## Group Theory

Simply put, a **group** is a set of elements {a,b,c,...} plus a binary operation, here represented as •.

To be considered a group, this combination needs to have certain properties:

1. **Closure**  
   For all a, b in G, the result of the operation, a • b, is also in G.  
2. **Associativity**  
   For all a, b and c in G, (a • b) • c = a • (b • c).  
3. **Identity element**  
   There exists an element e in G such that, for every element a in G, the equation e • a = a • e = a holds. Such an element is unique.  
4. **Inverse element**  
   For each a in G, there exists an element b in G, commonly denoted $$a^{−1}$$ (or −a, if the operation is denoted "+"), such that a • b = b • a = e.  

### Subgroups
If a subset of the elements in a group also satisfies the group properties, then that is a subgroup of the original group.

### Cyclic groups and generators
A finite group can be **cyclic**. That means it has a generator element.  
If you start at any point and then apply the group operation with the generator as argument a certain number of times, you go around the whole group and end in the same place.

---

## Fields

A **field** is a set (e.g. Integers) together with two operations called addition and multiplication.

One example of a field is the **Real Numbers** under addition and multiplication.  
Another is a set of Integers mod a prime number with addition and multiplication. 

The field operations are required to satisfy the following axioms (where a, b, c are arbitrary elements of the field $$\mathbb F$$):

1. **Associativity of addition and multiplication**  
   $$a + (b + c) = (a + b) + c \quad \text{and} \quad a \cdot (b \cdot c) = (a \cdot b) \cdot c$$  
2. **Commutativity of addition and multiplication**  
   $$a + b = b + a \quad \text{and} \quad a \cdot b = b \cdot a$$  
3. **Additive and multiplicative identity**  
   There exist two different elements 0 and 1 in $$\mathbb F$$ such that $$a + 0 = a$$ and $$a \cdot 1 = a$$.  
4. **Additive inverses**  
   For every a in F, there exists an element in F, denoted −a, called the additive inverse of a, such that $$a + (−a) = 0$$.  
5. **Multiplicative inverses**  
   For every $$a \neq 0$$ in F, there exists an element in F, denoted by $$a^{−1}$$, such that $$a \cdot a^{−1} = 1$$.  
6. **Distributivity of multiplication over addition**  
   $$a \cdot (b + c) = (a \cdot b) + (a \cdot c)$$  

### Finite fields and generators

A **finite field** is a field with a finite set of elements, such as the set of integers mod p where p is a prime.

Try operations on finite fields here: [https://asecuritysite.com/encryption/finite](https://asecuritysite.com/encryption/finite)

The **order** of the field is the number of elements in the field’s set.

For a finite field the order must be either:  
- prime (a prime field), or  
- the power of a prime (an extension field).  

An element can be represented as an integer greater or equal than 0 and less than the field’s order: {0, 1, ..., p-1} in a simple field.

Every finite field has a **generator**. A generator is capable of generating all of the elements in the set by exponentiating the generator.

So for generator g we can take $$g^0, g^1, g^2,...$$ and eventually this will give us all elements in the group.

**Example**: Taking the set of integers with prime p = 5, we get the group $$\mathbb Z^*_5 = \{0,1,2,3,4\}$$.  
- Operations are carried out modulo 5.  
  For example, $$3 \times 4 = 12 \Rightarrow 12 \mod 5 = 2$$.  

$$\mathbb Z^*_5$$ is cyclic and has two generators: 2 and 3.  

---

# Extracted Links

- [https://maths.extropy.io](https://maths.extropy.io)  
- [https://bit.ly/ExtropyMathsForZK](https://bit.ly/ExtropyMathsForZK)  
- [https://discord.gg/VSCHXqQE](https://discord.gg/VSCHXqQE)  
- [https://www.khanacademy.org/computing/computer-science/cryptography/modarithmetic/a/what-is-modular-arithmetic](https://www.khanacademy.org/computing/computer-science/cryptography/modarithmetic/a/what-is-modular-arithmetic)  
- [https://asecuritysite.com/encryption/finite](https://asecuritysite.com/encryption/finite)  



----



# Complexity Theory

**Complexity theory** studies how much **time** or **space** is required to solve a problem, especially as the **input size** grows.  
Some problems can be solved efficiently, while others require trying all possibilities (brute force).  

---

## Example: Travelling Salesman Problem (TSP)

The **Travelling Salesman Problem** asks for the shortest route visiting every city exactly once.  

- For **3 cities**, we can quickly test all routes.  
- For many cities, the number of routes grows extremely fast and becomes unfeasible.  

This shows why we classify problems based on **how solution time grows with input size $n$**.

---

## Growth of Time with Input Size

- If the worst-case time grows as a **polynomial** in $n$, e.g. $$O(n^k)$$ for some $k$,  
  the problem is in **P** (Polynomial time).  
- Problems in **P** are considered **tractable**.  

We also ask: how long does it take to **verify a solution** once found?

---

## Decision Problems

A **decision problem** has a **yes/no** answer.  
For example: *Does a Hamiltonian path exist in this graph?*  

---

## Complexity Classes

### P
- Problems solvable in **polynomial time**.  
- Example: Sorting numbers is in P.

### NP
- Problems where a **yes-answer** can be **verified** in polynomial time.  
- Example:  
  - Guess a secret key for encryption.  
  - **Verification**: Encrypt the plaintext with the guessed key and check against the ciphertext.  
  - Verification is fast (polynomial), but **finding** the key may not be.

### NP-Complete
- Problems in NP to which **every NP problem can be reduced** in polynomial time.  
- Intuition: If we can solve one NP-Complete problem quickly, we can solve all NP problems quickly.  
- Formal definition:  
  - For problems $X$ (NP-complete) and $Y$ (NP),  
  - There exists a polynomial-time function $$f$$ such that $$y \in Y \iff f(y) \in X$$.

### NP-hard
- At least as hard as NP-complete problems.  
- They don’t need to be in NP and don’t need to be decision problems.  
- If one NP-hard problem has a polynomial solution, **all NP problems** do.  

---

## Fun Fact: Video Games and Complexity

Even **video games** can be **NP-complete** or **NP-hard**!  

Examples:  
- **Tetris, Super Mario Bros., Pokémon, Candy Crush Saga**.  
- Reference: ["Classic Nintendo Games Are (Computationally) Hard"](https://arxiv.org/abs/1203.1895).  

---

## Zero-Knowledge Proofs (ZKP) Connection

From ["Everything provable is provable in zero knowledge"](https://dl.acm.org/doi/pdf/10.5555/88314.88333):

- Assuming secure probabilistic encryption:  
  - Every language with an interactive proof has a **zero-knowledge interactive proof**.  
- Extends result of Goldreich, Micali, Wigderson:  
  - **All NP problems admit zero-knowledge proofs** under the same assumption.  

---

## Interactive Proofs (IP)

- **Interactive Proofs (IP)** are central to **zero-knowledge proofs**.  
- Unlike static proofs, they involve **interaction between prover and verifier**.  
- Widely used in **modern zk systems**.  

📺 [Video lecture by Alessandro Chiesa](https://www.youtube.com/watch?v=pMzpQ82Q88Q)

---

# Big O Notation

**Big O notation** describes the **complexity** of an algorithm using algebraic terms.  

- It shows how **time or space** grows with input size $n$ in the **worst case**.  
- Example:  
  - $$O(n^2)$$ means time grows roughly proportional to $$n^2$$.  
  - If input doubles, runtime grows by about 4 times.  

---

## Common Big O Complexities

| Complexity | Name             | Example Task                                |
|------------|------------------|---------------------------------------------|
| $$O(1)$$   | Constant         | Array lookup by index                       |
| $$O(\log n)$$ | Logarithmic   | Binary search                               |
| $$O(n)$$   | Linear           | Scanning a list                             |
| $$O(n \log n)$$ | Log-linear  | Merge sort, Quick sort (average case)       |
| $$O(n^2)$$ | Quadratic        | Checking all pairs in a list                |
| $$O(2^n)$$ | Exponential      | Brute force solving of SAT                  |
| $$O(n!)$$  | Factorial        | Travelling Salesman (brute force)           |

---

## Visual Example

Consider $$O(n^2)$$:  

- If $$n = 10$$, steps ≈ $$100$$.  
- If $$n = 100$$, steps ≈ $$10,000$$.  

This shows why **polynomial vs. exponential** makes a big difference.

---

# Key Takeaways

1. **P** = problems solvable in polynomial time.  
2. **NP** = problems where solutions can be verified in polynomial time.  
3. **NP-Complete** = hardest problems in NP; solve one, solve them all.  
4. **NP-hard** = at least as hard as NP-complete, may go beyond decision problems.  
5. **Interactive Proofs (IP)** are essential for **Zero-Knowledge Proofs**.  
6. **Big O notation** is a mathematical tool to measure and compare complexities.  

---
