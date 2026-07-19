# 5.Basis and Dimension — Relevance with Machine Learning (ML)

In linear algebra and machine learning, vectors are used to represent data features. The concept of a **basis** acts as the foundational coordinate framework used to build and analyze these spaces.

---

## Why Basis Vectors Matter in ML Algorithms

In many core machine learning architectures, we rely on specific properties of basis vectors to process information efficiently:

* **Linear Combinations of Independent Vectors:** We often need to represent complex high-dimensional feature vectors as a linear combination of a standard set of **linearly independent vectors** or **orthogonal vectors** (vectors perpendicular to each other).
* **Feature Space Representation:** Every unique vector inside the entire feature space of our dataset can be reconstructed exactly as a unique linear combination of these core basis vectors.

---

## Core Applications in Modern ML

The definition of a basis becomes particularly crucial when trying to compress data or look for hidden structural patterns:

### 1. Dimensionality Reduction

Algorithms like Principal Component Analysis (PCA) find a new set of orthogonal basis vectors (principal components) along the directions of maximum variance. This allows us to project high-dimensional data onto a lower-dimensional subspace while keeping the most critical information intact.

### 2. Dictionary Learning Algorithms

These methods aim to find a sparse representation of input data in the form of a linear combination of basic elements. These elements are chosen from an overcomplete template collection called a "dictionary."

### 3. Wavelet-Based Algorithms

Wavelet transforms approximate complex, continuous functions using a set of orthogonal basis functions generated from a single baseline function known as the **mother wavelet**. This is highly useful for signal processing, denoising, and image compression tasks.



# Linear Algebra Notes: Basis of a Vector Space

## Definition

Let $V(F)$ be a vector space over a field $F$. A **basis** for $V$ is a set of vectors in $V$ that satisfies two core properties simultaneously:

1. **Linear Independence:** No vector in the set can be written as a linear combination of the remaining vectors.
2. **Spanning:** The linear span of the set equals the entire vector space ($L(S) = V$).

---

## Key Terminology & Extensions

* **Basis Vector:** An individual vector belonging to a chosen basis set.
* **Finite-Dimensional Space:** The vector space $V$ is classified as finite-dimensional if it contains a finite basis set. The total number of vectors in this basis defines the **dimension** of the space.

---

## Canonical Examples: Standard Bases

The most common examples of bases are the standard bases for real coordinate spaces, where each basis vector contains a single $1$ positioned at a unique coordinate index, with all other entries set to $0$:

### (1) Standard Basis for $\mathbb{R}^2$

The standard basis for the two-dimensional Cartesian plane consists of two vectors:


$$S = \{(1, 0), \; (0, 1)\}$$

### (2) Standard Basis for $\mathbb{R}^3$

The standard basis for three-dimensional spatial coordinates consists of three vectors:


$$S = \{(1, 0, 0), \; (0, 1, 0), \; (0, 0, 1)\}$$

### (3) Standard Basis for $\mathbb{R}^n$

The standard basis generalizes to an arbitrary $n$-dimensional real coordinate space as a collection of $n$ unique coordinate vectors:


$$S = \{(1, 0, \dots, 0), \; (0, 1, 0, \dots, 0), \; \dots, \; (0, 0, \dots, 0, 1)\}$$



# Linear Algebra Notes: Structural Definition of a Basis

This section outlines the precise mathematical criteria that a set of vectors must fulfill to form a basis for an $n$-dimensional vector space, followed by standard coordinate plane examples.

---

## 1. Formal Definition of a Basis

A set of vectors $B = \{v_1, v_2, \dots, v_n\}$ is a **basis** of an $n$-dimensional vector space $V$ over a field $F$ if and only if it satisfies the following two conditions:

### Condition I: Linear Independence

The vectors in the set must be completely linearly independent. This means no vector in $B$ can be written as a linear combination of the others:


$$\{v_1, v_2, \dots, v_n\} \text{ is linearly independent.}$$

### Condition II: Spanning Property

The set must completely span the vector space $V$. For any arbitrary vector $v \in V$, it can be expressed uniquely as a linear combination of the vectors in $B$:


$$v = \alpha_1 v_1 + \alpha_2 v_2 + \dots + \alpha_n v_n$$


where $\alpha_1, \alpha_2, \dots, \alpha_n$ are scalar coefficients chosen from the field $F$.

---

## 2. Canonical Examples of Standard Bases

The most common examples of bases are the standard bases for real coordinate spaces over the field $\mathbb{R}$:

### Example I: Two-Dimensional Real Space $\mathbb{R}^2(\mathbb{R})$

The standard basis for the Cartesian plane consists of two orthogonal unit vectors:


$$\text{Standard Basis } S = \{(1, 0), \; (0, 1)\}$$

Any arbitrary vector $(\alpha, \beta) \in \mathbb{R}^2$ can be decomposed uniquely into a linear combination of these two vectors:


$$(\alpha, \beta) = \alpha(1, 0) + \beta(0, 1)$$

### Example II: Three-Dimensional Real Space $\mathbb{R}^3(\mathbb{R})$

The standard basis for 3D coordinate space is composed of three mutually perpendicular unit vectors:


$$\text{Standard Basis } S = \{(1, 0, 0), \; (0, 1, 0), \; (0, 0, 1)\}$$

### Example III: Arbitrary $n$-Dimensional Real Space $\mathbb{R}^n(\mathbb{R})$

This coordinate structure generalizes to higher dimensions. The standard basis for an $n$-dimensional real vector space contains exactly $n$ distinct coordinate unit vectors:


$$\text{Standard Basis } S = \{(1, 0, \dots, 0), \; (0, 1, \dots, 0), \; \dots, \; (0, 0, \dots, 1)\}$$



# Linear Algebra Notes: Standard Bases for Matrix Vector Spaces

This section covers the standard basis sets for the vector space of all $2 \times 2$ real matrices and the subspace of $2 \times 2$ real symmetric matrices.

---

## Example IV: The Space of All $2 \times 2$ Real Matrices

Let $V$ be the set containing all possible $2 \times 2$ matrices with real coefficients:

$$V = \left\{ M_{2 \times 2} \;\middle|\; \text{set of all } 2 \times 2 \text{ real matrices} \right\}$$

The algebraic structure $V(\mathbb{R})$ forms a valid vector space over the field of real numbers $\mathbb{R}$.

### Standard Basis Set

The canonical standard basis for this space consists of **4** distinct linearly independent matrices, each containing a single $1$ at a unique position, with all other entries set to $0$:

$$\text{Standard Basis } S = \left\{ \begin{pmatrix} 1 & 0 \\ 0 & 0 \end{pmatrix}, \; \begin{pmatrix} 0 & 1 \\ 0 & 0 \end{pmatrix}, \; \begin{pmatrix} 0 & 0 \\ 1 & 0 \end{pmatrix}, \; \begin{pmatrix} 0 & 0 \\ 0 & 1 \end{pmatrix} \right\}$$

$$\implies \dim(V) = 4$$

---

## Example V: The Subspace of $2 \times 2$ Real Symmetric Matrices

Let $V$ be restricted to the set containing only $2 \times 2$ matrices with real coefficients that are symmetric (where the matrix equals its transpose, $A = A^T$):

$$V = \left\{ M_{2 \times 2} \;\middle|\; \text{set of all } 2 \times 2 \text{ real symmetric matrices} \right\}$$

A general symmetric $2 \times 2$ matrix takes the mathematical form:


$$\begin{pmatrix} a & b \\ b & c \end{pmatrix} \quad \text{where } a, b, c \in \mathbb{R}$$

### Standard Basis Set

Because the off-diagonal entries are constrained to be identical, it requires only **3** independent basis matrices to span the entire subspace:

$$\text{Standard Basis } S = \left\{ \begin{pmatrix} 1 & 0 \\ 0 & 0 \end{pmatrix}, \; \begin{pmatrix} 0 & 1 \\ 1 & 0 \end{pmatrix}, \; \begin{pmatrix} 0 & 0 \\ 0 & 1 \end{pmatrix} \right\}$$

$$\implies \dim(V) = 3$$



# Linear Algebra Notes: Dimension of a Vector Space

## Definition

The total number of vectors contained within a valid basis of a vector space $V(F)$ is called the **dimension** of the vector space, denoted as $\dim(V)$.

---

## Key Dimensional Examples

The following table summarizes the dimensions of common vector spaces over the field of real numbers $\mathbb{R}$:

| Vector Space | Description | Dimension |
| --- | --- | --- |
| **$\mathbb{R}^2(\mathbb{R})$** | Real coordinate plane | $2$ |
| **$\mathbb{R}^n(\mathbb{R})$** | $n$-dimensional real coordinate space | $n$ |
| **$M_{m \times n}(\mathbb{R})$** | Set of all $m \times n$ real matrices | $m \times n$ |
| **$P_n(\mathbb{R})$** | Polynomials of degree at most $n$ | $n + 1$ |
| **$P$** | Set of all polynomials of any degree | $\infty$ |

---

## Detailed Breakdown of Examples

### 1. Real Coordinate Space ($\mathbb{R}^2$ and $\mathbb{R}^n$)

* For $\mathbb{R}^2$, the standard basis contains exactly 2 vectors: $\{(1,0), (0,1)\}$. Thus, the dimension is **2**.
* For an arbitrary $\mathbb{R}^n$ space, the standard basis contains $n$ vectors. Thus, the dimension is **$n$**.

### 2. Matrix Spaces ($M_{m \times n}$)

The space of all $m \times n$ real matrices requires an independent basis element for each cell entry.

* For example, a $2 \times 3$ matrix space requires $2 \times 3 = 6$ basis matrices.
* Thus, $\dim(M_{m \times n}(\mathbb{R})) =$ **$m \times n$**.

### 3. Bounded Polynomial Space ($P_n$)

The vector space $P_n(\mathbb{R})$ contains all real-valued polynomials of degree **at most $n$**. A general polynomial takes the form:


$$p(x) = a_n x^n + a_{n-1} x^{n-1} + \dots + a_1 x + a_0$$

The standard basis is given by the set of monomials:


$$S = \{1, x, x^2, \dots, x^n\}$$

Counting from $x^0 = 1$ up to $x^n$ yields a total vector count of:


$$\implies \dim(P_n(\mathbb{R})) = \mathbf{n + 1}$$

### 4. Infinite-Dimensional Polynomial Space ($P$)

When a polynomial space has no upper bound constraint on its maximum degree, it is represented as:


$$P = \{ \text{set of all polynomials with coefficients from } \mathbb{R} \}$$

Because there is no finite cap on the power of $x$, a basis for this set requires an infinite sequence of linearly independent monomials ($\{1, x, x^2, x^3, \dots\}$).


$$\implies \dim(P) = \mathbf{\infty}$$



# Linear Algebra Notes: Key Theorems on Basis size and Extension

This section outlines two fundamental results regarding the cardinalities of linearly independent and spanning sets within finite-dimensional vector spaces.

---

## Theorem 1: The Size Limitation for Linear Independence

### Theorem Statement

Let $\{v_1, v_2, \dots, v_n\}$ be a basis of a given vector space $V(F)$. If $S$ is a subset of vectors containing more than $n$ vectors, then the set $S$ is **linearly dependent**.

> ### 💡 Conceptual takeaway
> 
> 
> Since a basis sets the absolute structural benchmark for a space's size, any subset inside an $n$-dimensional space containing $n+1$ or more vectors automatically contains redundant directional information. It is impossible to maintain linear independence with more vectors than the dimension of the space.

---

## Theorem 2: The Basis Extension Theorem

### Theorem Statement

Let $\{v_1, v_2, \dots, v_k\}$ be a linearly independent subset of an $n$-dimensional vector space $V(F)$, where $k < n$. Then the subset $S$ can always be **extended** to form a complete basis of $V(F)$.

### How It Works Mechanically

If your independent set is too small ($k < n$) to span the space:

1. You identify an element in $V$ that does not lie within the current linear span:

$$v_{k+1} \notin L(\{v_1, v_2, \dots, v_k\})$$


2. Appending this new vector preserves linear independence:

$$\{v_1, v_2, \dots, v_k, v_{k+1}\}$$


3. You repeat this progressive inclusion process until you accumulate exactly $n$ vectors, matching the dimension requirement to yield a full basis.


# Linear Algebra Notes: Advanced Theorems on Dimension

This section covers two essential theorems regarding the invariance of basis size and the relationship between the dimensions of intersecting and joining subspaces.

---

## Theorem 1: Invariance of Basis Cardinality

### Theorem Statement

Let $V(F)$ be a finite-dimensional vector space over a field $F$. Then any two bases of $V$ must contain exactly the same number of vectors.

> ### 💡 Conceptual Takeaway
> 
> 
> While a vector space can have infinitely many different choices of bases, the size of those bases is a fixed fundamental property of the space. This invariant quantity uniquely defines the **dimension** of the vector space.

---

## Theorem 2: Grassmann's Dimension Formula for Subspaces

### Theorem Statement

Let $V(F)$ be a finite-dimensional vector space over a field $F$, and let $S_1$ and $S_2$ be two valid subspaces of $V$. Then the dimensions of their sum and intersection satisfy the following linear relationship:

$$\dim(S_1) + \dim(S_2) = \dim(S_1 + S_2) + \dim(S_1 \cap S_2)$$

*Alternative common rearrangement:*


$$\dim(S_1 + S_2) = \dim(S_1) + \dim(S_2) - \dim(S_1 \cap S_2)$$

---

> ### ⚠️ Note on a Typo in Lecture Slide
> 
> 
> Please note that the image contains a slight copy-paste typo in the final term, showing $\dots + \dim(S_1 \cap S_1)$.
> Mathematically, it must intersect the two *distinct* subspaces, meaning the correct formula is:
> 
> $$\dim(S_1 \cap S_2)$$
> 
> 

---

### 🔍 Intuitive Analogy

This theorem works exactly like the **Inclusion-Exclusion Principle** found in set theory or probability. When you add the dimensions of $S_1$ and $S_2$ together, any basis vectors that are shared in their overlapping intersection region ($S_1 \cap S_2$) get counted twice. Subtracting the intersection dimension balances the equation perfectly to find the dimension of the joined space ($S_1 + S_2$).


# Linear Algebra Notes: Examples of Bases and Subspace Dimension

This section covers different bases choices for $\mathbb{R}^3(\mathbb{R})$ and demonstrates how to algebraically calculate the basis and dimension of given subspaces.

---

## 1. Multiple Bases for the Same Vector Space

A single vector space can have infinitely many different valid bases. As long as a set contains exactly $n$ linearly independent vectors in an $n$-dimensional space, it qualifies as a basis.

### Examples in $\mathbb{R}^3(\mathbb{R})$

* **$B_1$ (The Standard Canonical Basis):**

$$B_1 = \{(1, 0, 0), \; (0, 1, 0), \; (0, 0, 1)\}$$


* **$B_2$ (An Alternative Non-Standard Basis):**

$$B_2 = \{(1, 0, 0), \; (1, 1, 0), \; (1, 1, 1)\}$$



Both sets contain exactly 3 linearly independent vectors, meaning both successfully span the entire three-dimensional space $\mathbb{R}^3$.

---

## 2. Calculating the Basis and Dimension of Subspaces

### Example 1: Finding the Basis of a 2D Plane

Find a basis and the dimension of the subspace $S \subseteq \mathbb{R}^3$ defined by the homogeneous equation:


$$S = \left\{ (x_1, x_2, x_3) \in \mathbb{R}^3 \;\middle|\; x_1 + x_2 - x_3 = 0 \right\}$$

#### Solution Steps:

1. **Express one variable in terms of the others:**
Rearranging the plane constraint equation gives:

$$x_3 = x_1 + x_2$$


2. **Substitute this back into a general vector:**
Write out the coordinate triplet using only the free parameters ($x_1$ and $x_2$):

$$S = \left\{ (x_1, \; x_2, \; x_1 + x_2) \right\}$$


3. **Separate out the individual parameters:**
Decompose the parametric vector into a linear combination:

$$= \left\{ (x_1, 0, x_1) + (0, x_2, x_2) \right\}$$


$$= \left\{ x_1(1, 0, 1) + x_2(0, 1, 1) \right\}$$



The vectors multiplying the free parameters form the spanning set.

* **Basis of $S$:** $\{(1, 0, 1), \; (0, 1, 1)\}$
* **Dimension:** $\dim(S) = 2$ (Geometrically, this is a flat plane cutting through the origin).

---

### Example 2: Finding the Basis of a 1D Line

Find a basis and the dimension of the subspace $W \subseteq \mathbb{R}^3$ defined by the system:


$$W = \left\{ (x_1, x_2, x_3) \in \mathbb{R}^3 \;\middle|\; x_1 = x_2 = x_3 \right\}$$

#### Solution Steps:

1. **Reduce parameters to a single free variable:**
Since all three coordinates are constrained to be equal, we can replace all instances with a single variable, say $x_1$:

$$W = \left\{ (x_1, \; x_1, \; x_1) \right\}$$


2. **Factor out the free parameter:**

$$= \left\{ x_1(1, 1, 1) \right\}$$



The single vector left inside forms the spanning set.

* **Basis of $W$:** $\{(1, 1, 1)\}$
* **Dimension:** $\dim(W) = 1$ (Geometrically, this describes a straight line shooting through the origin).


# Linear Algebra: Subspaces, Bases, and Dimensions

## 1. Subspace $S$

Given the vector space $V = \mathbb{R}^3(\mathbb{R})$, we define the subspace $S$ as follows:

$$
\begin{aligned}
S &= \{ (x_1, x_2, x_3) \in \mathbb{R}^3 \mid x_1 + x_2 - x_3 = 0 \} \\
  &= \{ (x_1, x_2, x_3) \in \mathbb{R}^3 \mid x_1 + x_2 = x_3 \} \\
  &= \{ (x_1, x_2, x_1 + x_2) \in \mathbb{R}^3 \} \\
  &= \{ x_1(1, 0, 1) + x_2(0, 1, 1) \}
\end{aligned}
$$

### Basis and Dimension of $S$
From the linear combination above, the generating set forms the basis:

$$\Rightarrow B_S = \{ (1, 0, 1), (0, 1, 1) \}$$

$$\text{Dim}(S) = 2$$

---

## 2. Subspace $W$

Given the same vector space $V = \mathbb{R}^3(\mathbb{R})$, we define the subspace $W$ as follows:

$$
\begin{aligned}
W &= \{ (x_1, x_2, x_3) \mid x_1 = x_2 = x_3 \} \\
  &= \{ (x_1, x_1, x_1) \in \mathbb{R}^3 \} \\
  &= \{ x_1(1, 1, 1) \}
\end{aligned}
$$

### Basis and Dimension of $W$
From the linear combination above, the generating set forms the basis:

$$B_W = \{ (1, 1, 1) \}$$

$$\text{Dim}(W) = 1$$


## 3. Intersection Subspace $S \cap W$

### Basis of $S \cap W$

We evaluate the intersection of subspaces $S$ and $W$ by combining their constraints:

$$
\begin{aligned}
S \cap W &= \{ (x_1, x_2, x_3) \in \mathbb{R}^3 \mid x_1 + x_2 - x_3 = 0 \text{ \& } x_1 = x_2 = x_3 \} \\
         &= \{ (x_1, x_2, x_1 + x_2) \mid x_1 = x_2 = x_3 \}
\end{aligned}
$$

> *Note: The handwritten line following this step in the image was crossed out, as substituting $x_1 = x_2$ into the vector yields $(x_1, x_1, 2x_1)$, but the condition $x_3 = x_1$ forces $2x_1 = x_1$, meaning $x_1 = 0$. Thus, only the zero vector satisfies both conditions.*

$$B_{S \cap W} = \{ (0,0,0) \}$$

$$\text{Dim}(S \cap W) = 0$$


# Problem 3: Subspaces in $\mathbb{R}^4$

## Problem Statement

Find the basis and dimension of $S_1$, $S_2$, and $S_1 \cap S_2$, where:

* $S_1 = \{ (x_1, x_2, x_3, x_4) \in \mathbb{R}^4 \mid x_1 + x_2 - x_3 + x_4 = 0, \, x_1 + x_2 + x_3 + x_4 = 0 \}$
* $S_2 = \{ (x_1, x_2, x_3, x_4) \in \mathbb{R}^4 \mid x_1 - x_2 - x_3 + x_4 = 0, \, x_1 + 2x_2 - x_4 = 0 \}$

---

## Solution Summary

* **Basis of $S_1$** $= \{ (1, 0, 0, -1), (0, 1, 0, -1) \}$
* $\text{dim}(S_1) = 2$
* **Basis of $S_2$** $= \{ (1, 0, 2, 1), (0, 1, 1, 2) \}$
* $\text{dim}(S_2) = 2$
* **Basis of $S_1 \cap S_2$** $= \{ (0, 0, 0, 0) \}$

---

## Detailed Evaluation of Subspace $S_1$

We define $S_1$ using its system of constraints:

$$
S_1 =
\left\{
(x_1, x_2, x_3, x_4)
\mid
\begin{aligned}
x_1 + x_2 - x_3 + x_4 &= 0 \\
x_1 + x_2 + x_3 + x_4 &= 0
\end{aligned}
\right\}
$$

### Step-by-Step Simplification

1. Subtract the first equation from the second:

$$
(x_1 + x_2 + x_3 + x_4) -
(x_1 + x_2 - x_3 + x_4)
= 0
\Rightarrow
2x_3 = 0
\Rightarrow
x_3 = 0
$$

2. Substitute $x_3 = 0$ into either equation:

$$
x_1 + x_2 + x_4 = 0
\Rightarrow
x_4 = -x_1 - x_2
$$

3. Express the general vector using the free variables $x_1$ and $x_2$:

$$
\begin{aligned}
S_1
&=
\left\{
(x_1, x_2, 0, -x_1 - x_2)
\mid
x_1, x_2 \in \mathbb{R}
\right\} \\
&=
\operatorname{span}
\left\{
(1,0,0,-1),
(0,1,0,-1)
\right\}
\end{aligned}
$$

### Basis of $S_1$

$$
B_{S_1}
=
\left\{
(1,0,0,-1),
(0,1,0,-1)
\right\}
$$
