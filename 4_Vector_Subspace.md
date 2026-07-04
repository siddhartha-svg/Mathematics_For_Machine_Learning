# 4.Vector Subspace - Examples and Properties

## Definition of a Subspace
If $\mathbb{R}^n$ is a vector space over the field of real numbers $\mathbb{R}$, then a subset $S$ of $\mathbb{R}^n$ is said to be a **subspace** of the vector space $\mathbb{R}^n$ if $S$ itself forms a valid vector space over the same field $\mathbb{R}$ under the inherited operations.


---

## Subspace Criteria (Aliter)
To prove that a non-empty subset $S \subseteq \mathbb{R}^n$ is a subspace of $V = \mathbb{R}^n(\mathbb{R})$, you do not need to check all 6 vector space axioms ($M1$ through $M6$). Instead, it is sufficient to verify the following three fundamental conditions:

### a) Existence of the Zero Vector
The subset must contain the additive identity element (the origin):
$$\mathbf{0} \in S$$

### b) Closure Under Vector Addition
Adding any two vectors inside the subset must yield a resultant vector that stays within the subset:
$$x, y \in S \implies x + y \in S$$

### c) Closure Under Scalar Multiplication
Scaling any vector inside the subset by any real constant must yield a vector that stays within the subset:
$$x \in S, \; \alpha \in \mathbb{R} \implies \alpha x \in S$$


# Linear Algebra Theorems: The Subspace Criterion

## Theorem
Let $W$ be a subset of $\mathbb{R}^n$. Then $W$ is a subspace of $\mathbb{R}^n$ if and only if the following conditions hold:

### (a) Non-emptiness
The subset $W$ is non-empty.
$$\left(W \neq \emptyset\right)$$

### (b) Closure Under Linear Combinations
For any scalars $a, b \in \mathbb{R}$ and any vectors $\vec{u}, \vec{v} \in W$, their linear combination remains entirely within the subset:

$$a\vec{u} + b\vec{v} \in W$$

---

> ### 💡 Note on Practical Usage
> This theorem condenses the subspace verification process down into a single operational step. By showing that a subset is closed under linear combinations ($a\vec{u} + b\vec{v}$), you simultaneously prove closure under both vector addition (by setting $a=1, b=1$) and scalar multiplication (by setting $b=0$).


# Linear Algebra Notes: Subspace Definitions and Examples

## 1. Core Definitions

### General Definition
If $\mathbb{R}^n$ is a vector space over $\mathbb{R}$, then a subset $S$ of $\mathbb{R}^n$ is said to be a **subspace** of the vector space $\mathbb{R}^n$ if $S$ is also a vector space over the same field $\mathbb{R}$ under the same operations.

### Subspace Criteria (Aliter)
If $\mathbb{R}^n$ is a vector space, then a subset $S \subseteq \mathbb{R}^n$ is a subspace of $V = \mathbb{R}^n(\mathbb{R})$ if and only if it satisfies the following three conditions:

* **a) Contains the Zero Vector:** $$\mathbf{0} \in S$$
* **b) Closed Under Vector Addition:** $$x, y \in S \implies x + y \in S$$
* **c) Closed Under Scalar Multiplication:** $$x \in S, \; \alpha \in \mathbb{R} \implies \alpha x \in S$$

---

## 2. Examples of Subspaces

Let $V(\mathbb{R})$ be a vector space.

### A. Trivial Subspaces
Every vector space $V$ has at least two standard, guaranteed subspaces:
* (a) $S = \{\mathbf{0}\}$ (The zero subspace)
* (b) $S = V$ (The space itself)

These two cases are called **trivial subspaces** of $V$.

### B. Matrix Space Subspaces
The set of all $3 \times 3$ **skew-symmetric** or **symmetric** matrices forms a valid subspace of the parent vector space defined by:
$$V = \{M_{3 \times 3} \mid M \text{ is a } 3 \times 3 \text{ matrix with real entries}\}$$

### C. Coordinate Plane and Line Subspaces in $\mathbb{R}^3$
* **Example 1 (A Plane through the Origin):** The set $S = \{(x_1, x_2, x_3) \in \mathbb{R}^3 \mid x_1 - x_2 + x_3 = 0\}$ is a valid subspace of $\mathbb{R}^3$.
* **Example 2 (A Line through the Origin):** The set $S = \{(x_1, x_2, x_3) \in \mathbb{R}^3 \mid x_1 = x_2 = x_3\}$ is a valid subspace of $\mathbb{R}^3$.

---

## 3. Non-Subspace Example (Failure Case)

The set $S = \{(x_1, x_2, x_3) \in \mathbb{R}^3 \mid x_1 + x_2 + x_3 = 1\}$ **is NOT a subspace** of $\mathbb{R}^3$.

> ### ❌ Reason for Failure
> This set fails the very first criterion because it **does not contain the zero vector**. If we test the origin $\mathbf{0} = (0, 0, 0)$, the condition yields:
> $$0 + 0 + 0 = 0 \neq 1$$
> Geometrically, this equation describes a flat plane in 3D space that does not pass through the origin, which invalidates it as a subspace.

# Mathematical Proof: Verifying a Vector Subspace in $\mathbb{R}^3$

This document outlines the formal mathematical proof showing that the subset $S$ forms a valid vector subspace of $\mathbb{R}^3$ by satisfying the non-emptiness and linear combination closure criteria.

---

## 1. Problem Statement

Let a subset $S \subseteq \mathbb{R}^3$ be defined by a homogenous linear equation constraint:

$$S = \left\{ (x_1, x_2, x_3) \in \mathbb{R}^3 \;\middle|\; x_1 + x_2 - x_3 = 0 \right\}$$

Prove that $S$ is a subspace of $\mathbb{R}^3$.

---

## 2. Proof Step 1: Non-Emptiness Verification

To show that the subset $S$ is non-empty, we test if it contains the fundamental zero vector identity element of $\mathbb{R}^3$, which is $(0,0,0)$.

* Substituting $(0, 0, 0)$ into the defining condition:
  $$0 + 0 - 0 = 0$$

Since the zero vector satisfies the equation constraint, $\mathbf{0} \in S$.

$$\implies S \text{ is non-empty.}$$

---

## 3. Proof Step 2: Closure Under Linear Combinations

Let $a, b \in \mathbb{R}$ be arbitrary scalar constants, and let $\vec{u} = (x_1, x_2, x_3)$ and $\vec{v} = (y_1, y_2, y_3)$ be any two unique vector elements chosen from $S$. 

Because $\vec{u}, \vec{v} \in S$, they must satisfy the set's equation rules:
1. $$x_1 + x_2 - x_3 = 0 \quad \text{--- (Equation 1)}$$
2. $$y_1 + y_2 - y_3 = 0 \quad \text{--- (Equation 2)}$$

### Constructing the Linear Combination ($a\vec{u} + b\vec{v}$)

We perform scalar multiplication and vector addition to find the component coordinates of the combined vector expression:

$$a(x_1, x_2, x_3) + b(y_1, y_2, y_3) = (ax_1, ax_2, ax_3) + (by_1, by_2, by_3)$$
$$= (ax_1 + by_1, \; ax_2 + by_2, \; ax_3 + by_3)$$

### Evaluating the Constraint Condition

To prove that this combined vector belongs to $S$, its coordinates must satisfy the original structural condition ($\text{Component}_1 + \text{Component}_2 - \text{Component}_3 = 0$):

$$(ax_1 + by_1) + (ax_2 + by_2) - (ax_3 + by_3)$$

Now, regroup and factor out the common scalar constants $a$ and $b$:

$$= a(x_1 + x_2) + b(y_1 + y_2) - (ax_3 + by_3)$$
$$= a(x_1 + x_2 - x_3) + b(y_1 + y_2 - y_3)$$

Substitute the known values from **Equation 1** and **Equation 2** ($0$ and $0$) into the grouped segments:

$$= a \cdot 0 + b \cdot 0$$
$$= 0$$

---

## 4. Final Conclusion

Since the linear combination yields an evaluation of exactly $0$, the condition is satisfied:

$$a(x_1, x_2, x_3) + b(y_1, y_2, y_3) \in S$$

$$\implies S \text{ is a valid subspace of } \mathbb{R}^3.$$





# Linear Algebra Notes: Examples of Subspaces and Counterexamples

## 1. Examples of Subspaces

Let $V(\mathbb{R})$ be a valid parent vector space.

### A. Trivial Subspaces
Every vector space $V$ contains at least two canonical, guaranteed subspaces:
* (a) $S = \{\mathbf{0}\}$ (The zero vector singleton set / zero subspace)
* (b) $S = V$ (The entire vector space itself)

These are formally classified as the **trivial subspaces** of $V$.

### B. Matrix Subspaces
The set of all $3 \times 3$ **skew-symmetric** matrices or **symmetric** matrices forms a valid subspace of the parent space defined by:
$$V = \{M_{3 \times 3} \mid M \text{ is a } 3 \times 3 \text{ matrix with real entries}\}$$

### C. Solution Sets to Homogeneous Linear Equations in $\mathbb{R}^3$
* **A Plane Through the Origin:** The set $S = \{(x_1, x_2, x_3) \in \mathbb{R}^3 \mid x_1 - x_2 + x_3 = 0\}$ is a subspace of $\mathbb{R}^3$.
* **A Line Through the Origin:** The set $S = \{(x_1, x_2, x_3) \in \mathbb{R}^3 \mid x_1 = x_2 = x_3\}$ is a subspace of $\mathbb{R}^3$.

---

## 2. Non-Subspace Counterexample (Proof of Failure)

Consider the subset $S \subseteq \mathbb{R}^3$ defined by an affine constraint:

$$S = \left\{ (x_1, x_2, x_3) \in \mathbb{R}^3 \;\middle|\; x_1 + x_2 + x_3 = 1 \right\}$$

### Proof of Failure via Zero Vector Test

For any subset to qualify as a valid vector subspace, it must explicitly satisfy the identity axiom, meaning it must contain the zero vector of the parent space. The zero vector of $\mathbb{R}^3$ is defined as:

$$\mathbf{0} = (0, 0, 0)$$

Let us test if $(0,0,0)$ satisfies the conditional constraint required to belong to $S$:

$$\implies (0, 0, 0) \implies 0 + 0 + 0 \neq 1$$

### Conclusion
$$\implies (0, 0, 0) \notin S$$
$$\implies S \text{ is NOT a subspace of } \mathbb{R}^3.$$

> ### 💡 Geometric Perspective
> In three-dimensional space, any linear equation of the form $ax + by + cz = d$ defines a flat plane. If $d = 0$, the plane passes through the origin $(0,0,0)$ and forms a valid subspace. If $d \neq 0$ (such as $d = 1$ in this case), the plane is shifted away from the origin. Because it lacks the zero vector pivot point, it cannot support closure properties and fails to be a subspace.


# Geometric Classification of Subspaces in $\mathbb{R}^3$

Every valid vector subspace of the three-dimensional real coordinate space $\mathbb{R}^3$ can be completely classified by its geometric structure. Depending on its dimension, any subspace must be exactly one of the following four geometric configurations:

---

## 1. Zero-Dimensional Subspace: The Origin
* **Dimension:** $0$
* **Geometric Description:** A single point containing only the zero vector identity element.
* **Algebraic Form:** $S = \{(0, 0, 0)\}$

---

## 2. One-Dimensional Subspace: A Line Through the Origin
* **Dimension:** $1$
* **Geometric Description:** A perfectly straight linear path passing directly through the zero pivot point.
* **Algebraic Form:** The span of a single non-zero vector $v_1$:
  $$S = \{k \cdot v_1 \mid k \in \mathbb{R}\}$$


---

## 3. Two-Dimensional Subspace: A Plane Through the Origin
* **Dimension:** $2$
* **Geometric Description:** A flat, infinitely extending two-dimensional surface that contains the zero point.
* **Algebraic Form:** The span of two linearly independent vectors $v_1$ and $v_2$:
  $$S = \{c_1 v_1 + c_2 v_2 \mid c_1, c_2 \in \mathbb{R}\}$$


---

## 4. Three-Dimensional Subspace: The Space $\mathbb{R}^3$ Itself
* **Dimension:** $3$
* **Geometric Description:** The entire three-dimensional ambient coordinate environment.
* **Algebraic Form:** The span of three linearly independent vectors, filling the absolute volume constraint:
  $$S = \mathbb{R}^3$$



# Set Operations on Vector Subspaces

This document covers two major theorems regarding the intersection and union of vector subspaces, complete with geometric representations and algebraic examples.

---

## 1. Theorem on Subspace Intersections

### Theorem Statement
The intersection of any non-empty collection of subspaces of $\mathbb{R}^n$ is a subspace of $\mathbb{R}^n$.

### Set Diagram Representation
When two individual subspaces $S_1$ and $S_2$ are part of a parent vector space $V$, their shared region must also satisfy the criteria to form an independent subspace:

```
       Subspace S1               Subspace S2
     .───────────.             .───────────.
    /             \           /             \
   /               \         /               \
  │       V         ;───────;         V       │
  │                /  █████  \                │
   \              │  ███████  │              /
    \             │  ███████  │             /
     '───────────' \  █████  / '───────────'
                    '───────'
                     S1 ∩ S2 
              (Always a subspace of V)

```

### Analytical Example in $\mathbb{R}^3$

Let us define two valid subspaces of $\mathbb{R}^3$:

* **$S_1$ (A plane through the origin):** 
$$S_1 = \left\{ (x_1, x_2, x_3) \in \mathbb{R}^3 \;\middle|\; x_1 + x_2 - x_3 = 0 \right\}$$


* **$S_2$ (A line through the origin):** 
$$S_2 = \left\{ (x_1, x_2, x_3) \in \mathbb{R}^3 \;\middle|\; x_1 = x_2 = x_3 \right\}$$



#### Finding the Intersection ($S_1 \cap S_2$)

To determine the elements that satisfy both constraints simultaneously, substitute the conditions of $S_2$ ($x_1 = x_2 = x_3$) directly into the system constraint of $S_1$:

$$x_1 + x_2 = x_3$$

Since $x_2 = x_1$ and $x_3 = x_1$:


$$x_1 + x_1 = x_1$$

$$2x_1 = x_1 \implies x_1 = 0$$

Since $x_1 = x_2 = x_3$, it follows that:


$$x_1 = 0, \quad x_2 = 0, \quad x_3 = 0$$

The intersection set contains only a single coordinate triplet:


$$S_1 \cap S_2 = \left\{ (0, 0, 0) \right\}$$

> **Conclusion:** The resulting set is the trivial zero subspace, which validates the intersection theorem because the zero point alone is still a valid subspace of $\mathbb{R}^3$.

---

## 2. Theorem on Subspace Unions

### Theorem Statement

The union of two subspaces of $\mathbb{R}^n$ is a subspace of $\mathbb{R}^n$ **if and only if** one of them is entirely contained within the other.

### Set Diagram Representation

Unlike intersections, the union of two random subspaces does *not* typically form a subspace unless a subset inclusion condition ($S_1 \subseteq S_2$ or $S_2 \subseteq S_1$) is met:

```
    Case 1: S2 is contained in S1         Case 2: S1 is contained in S2
          (S2 ⊆ S1)                             (S1 ⊆ S2)

        .─────────────────.                   .─────────────────.
       /   Subspace S1     \                 /   Subspace S2     \
      /     .─────────.     \               /     .─────────.     \
     │     /  Subspace \     │             │     /  Subspace \     │
     │    │     S2      │    │             │    │     S1      │    │
     │     \           /     │             │     \           /     │
      \     '─────────'     /               \     '─────────'     /
       \                   /                 \                   /
        '─────────────────'                   '─────────────────'
           Union (S1 ∪ S2) = S1                  Union (S1 ∪ S2) = S2
           (Valid Subspace)                      (Valid Subspace)

```

> **Why Unions Broadly Fail:** If you take a vector from line $S_1$ and another from line $S_2$ on a flat 2D plane, adding them creates a resultant vector that shoots off into the open space between the lines. Because that new vector is not on line $S_1$ or line $S_2$, the union set fails the additive closure requirement.



# Linear Algebra Notes: Linear Span

## Definition
Let $V(F)$ be a vector space over a field $F$. Let $S = \{v_1, v_2, \dots, v_n\}$ be a non-empty subset of $V$. The **linear span** of the set $S$, denoted by $L(S)$ or $\text{span}(S)$, is the set containing all possible linear combinations of the vectors in $S$:

$$L(S) = \left\{ c_1 v_1 + c_2 v_2 + \dots + c_n v_n \;\middle|\; c_i \in F, \; 1 \le i \le n \right\}$$

---

## Core Operational Examples

### 1. Spanning Two-Dimensional Real Space ($\mathbb{R}^2$)
Let $S = \{(1, 0), (0, 1)\} \subseteq \mathbb{R}^2$. Evaluating its linear combinations yields:

$$L(S) = \{c_1(1, 0) + c_2(0, 1) \mid c_1, c_2 \in \mathbb{R}\}$$
$$L(S) = \{(c_1, c_2) \mid c_1, c_2 \in \mathbb{R}\} = \mathbb{R}^2$$

$$\implies \mathbb{R}^2 = L(\{(1, 0), (0, 1)\})$$

---

### 2. Spanning Three-Dimensional Real Space ($\mathbb{R}^3$)
Let $S = \{(1, 0, 0), (0, 1, 0), (0, 0, 1)\} \subseteq \mathbb{R}^3$. Evaluating its linear combinations yields:

$$L(S) = \left\{ c_1(1, 0, 0) + c_2(0, 1, 0) + c_3(0, 0, 1) \;\middle|\; c_1, c_2, c_3 \in \mathbb{R} \right\}$$
$$L(S) = \{(c_1, c_2, c_3) \mid c_1, c_2, c_3 \in \mathbb{R}\} = \mathbb{R}^3$$

$$\implies \mathbb{R}^3 = L(\{(1, 0, 0), (0, 1, 0), (0, 0, 1)\})$$

---

### 3. The Empty Set Rule
If $S$ is an empty set ($S = \emptyset$), its linear span defaults to the zero vector singleton set:
$$L(S) = \{\mathbf{0}\}$$

---

### 4. Advanced Algebraic Reduction Examples in $\mathbb{R}^3$

#### Example A
Let $S = \{(1, 1, 1), (2, 1, 3)\} \subseteq \mathbb{R}^3$ over the field $F = \mathbb{R}$.

1. **Construct the combination set:**
   $$L(S) = \{c_1(1, 1, 1) + c_2(2, 1, 3) \mid c_1, c_2 \in \mathbb{R}\}$$

2. **Simplify into component parameters:**
   $$L(S) = \{(c_1 + 2c_2, \; c_1 + c_2, \; c_1 + 3c_2) \mid c_1, c_2 \in \mathbb{R}\}$$

3. **Convert to implicit equation constraint form:**
   Let $x_1 = c_1 + 2c_2$, $x_2 = c_1 + c_2$, and $x_3 = c_1 + 3c_2$. Eliminating constants $c_1$ and $c_2$ yields the linear constraint system:
   $$L(S) = \left\{ (x_1, x_2, x_3) \in \mathbb{R}^3 \;\middle|\; 2x_1 - x_2 = x_3 \right\}$$

#### Example B
Let $S = \{(1, 2, 0), (1, 1, -1)\} \subseteq \mathbb{R}^3$.

1. **Construct the combination set:**
   $$L(S) = \{c_1(1, 2, 0) + c_2(1, 1, -1) \mid c_1, c_2 \in \mathbb{R}\}$$

2. **Simplify into coordinate parameters:**
   $$L(S) = \{(c_1 + c_2, \; 2c_1 + c_2, \; -c_2) \mid c_1, c_2 \in \mathbb{R}\}$$



# Linear Algebra Example: Finding the Implicit Equation of a Linear Span

This document provides a clean, structured transcription of the handwritten example showing how to convert the linear span of a set of vectors into an implicit equation constraint in $\mathbb{R}^3$.

---

## Problem Statement

Given a set of vectors $S \subseteq \mathbb{R}^3$:

$$S = \{(1, 1, 1), \; (2, 1, 3)\}$$

Find the implicit coordinate constraint for its linear span, $L(S)$.

---

## Step-by-Step Mathematical Simplification

### 1. Set Up the Linear Combination Set
By definition, the linear span consists of all possible linear combinations of the vectors in $S$ using real scalar constants $c_1, c_2 \in \mathbb{R}$:

$$L(S) = \left\{ c_1(1, 1, 1) + c_2(2, 1, 3) \;\middle|\; c_1, c_2 \in \mathbb{R} \right\}$$

### 2. Combine into a Parametric Vector
Distribute the scalars and add the components together:

$$L(S) = \left\{ \big((c_1 + 2c_2), \; (c_1 + c_2), \; (c_1 + 3c_2)\big) \;\middle|\; c_1, c_2 \in \mathbb{R} \right\}$$

### 3. Eliminate Parameters to Find the Coordinate Relationship
We map the parametric entries to standard spatial variables $(x_1, x_2, x_3)$:
* $x_1 = c_1 + 2c_2$
* $x_2 = c_1 + c_2$
* $x_3 = c_1 + 3c_2$

To find the dependency constraint equation, evaluate the combination expression $2x_1 - x_3$:

$$2x_1 - x_3 = 2(c_1 + 2c_2) - (c_1 + 3c_2)$$
$$2x_1 - x_3 = 2c_1 + 4c_2 - c_1 - 3c_2$$
$$2x_1 - x_3 = c_1 + c_2$$

Since $x_2 = c_1 + c_2$, we substitute $x_2$ directly into the equation:

$$2x_1 - x_3 = x_2$$

---

## Final Set Representation

The linear span of these two vectors describes a flat two-dimensional subspace (a plane passing through the origin) inside the ambient space $\mathbb{R}^3$:

$$L(S) = \left\{ (x_1, x_2, x_3) \;\middle|\; 2x_1 - x_3 = x_2 \right\} \subseteq \mathbb{R}^3$$



# Linear Algebra Notes: Important Results on Linear Spans

This section covers critical theoretical results and core algebraic theorems regarding the structural properties of the linear span $L(S)$ within a vector space.

---

## Theorem 1: Subspace Generation by a Linear Span

### Theorem Statement
Let $V(F)$ be a vector space over a field $F$ and let $S$ be a non-empty subset of $V$. Then the linear span $L(S)$ is a valid subspace of $V$.

### Proof:
To verify that $L(S)$ is a valid subspace of $V$, we must show it satisfies the non-emptiness condition and remains closed under linear combinations.

1. **Non-emptiness Verification:**
   Since $S$ is non-empty, there exists at least one vector $v \in S$. The linear span contains all linear combinations of elements in $S$. By setting the scalar coefficient to $0 \in F$, we find:
   $$0 \cdot v = \mathbf{0}$$
   Therefore, the zero vector $\mathbf{0}$ is an element of $L(S)$, proving that $L(S) \neq \emptyset$.

2. **Closure under Linear Combinations:**
   Let $x, y \in L(S)$ and let $\alpha, \beta \in F$ be arbitrary scalar constants. 
   By definition of a linear span, both $x$ and $y$ can be expressed as finite linear combinations of vectors from $S$:
   $$x = \sum_{i=1}^k c_i v_i \quad \text{where } c_i \in F, \, v_i \in S$$
   $$y = \sum_{j=1}^m d_j w_j \quad \text{where } d_j \in F, \, w_j \in S$$

   Now, construct the linear combination $\alpha x + \beta y$:
   $$\alpha x + \beta y = \alpha \left( \sum_{i=1}^k c_i v_i \right) + \beta \left( \sum_{j=1}^m d_j w_j \right)$$
   $$\alpha x + \beta y = \sum_{i=1}^k (\alpha c_i) v_i + \sum_{j=1}^m (\beta d_j) w_j$$

   Since $F$ is a field, the scalar products $(\alpha c_i)$ and $(\beta d_j)$ are also valid scalars in $F$. The resulting sum remains a finite linear combination of vectors $\{v_1, \dots, v_k, w_1, \dots, w_m\}$ which all belong to $S$.
   $$\implies \alpha x + \beta y \in L(S)$$

Since $L(S)$ is non-empty and closed under linear combinations, it is a valid subspace of $V$.

---

## Theorem 2: The Minimal Subspace Property

### Theorem Statement
Let $S$ be a non-empty subset of a vector space $V$. Then $L(S)$ is the **smallest subspace** of $V(F)$ containing $S$.

### Proof:
To prove this result, we must establish two distinct conditions:
1. The linear span $L(S)$ explicitly contains the subset $S$.
2. If there is any other arbitrary subspace $W$ of $V$ that contains $S$, then $L(S)$ must be completely contained within $W$ ($L(S) \subseteq W$).

#### Part 1: Showing $S \subseteq L(S)$
Let $v$ be an arbitrary vector such that $v \in S$. We can write $v$ as a trivial linear combination using the scalar multiplicative identity element $1 \in F$:
$$v = 1 \cdot v$$
Since $v$ is expressed as a linear combination of an element from $S$, it follows by definition that $v \in L(S)$. 
$$\implies S \subseteq L(S)$$

#### Part 2: Showing $L(S)$ is minimal
Let $W$ be any alternative subspace of $V$ such that $S \subseteq W$. We want to show that $L(S) \subseteq W$.

Let $u$ be an arbitrary vector belonging to the linear span ($u \in L(S)$). By the definition of a span, $u$ is a finite linear combination of vectors from $S$:
$$u = c_1 v_1 + c_2 v_2 + \dots + c_n v_n \quad \text{where } c_i \in F \text{ and } v_i \in S$$

Because $S \subseteq W$, every vector $v_i$ used in the linear combination must also belong to $W$:
$$v_1, v_2, \dots, v_n \in W$$

Since $W$ is a valid vector subspace, it is fundamentally closed under scalar multiplication and vector addition. Therefore, any finite linear combination of its elements must stay within $W$:
$$c_1 v_1 + c_2 v_2 + \dots + c_n v_n \in W \implies u \in W$$

Since any arbitrary element $u \in L(S)$ is also an element of $W$, we establish that:
$$L(S) \subseteq W$$

### Conclusion
Because $L(S)$ is a valid subspace containing $S$, and it is nested within any other potential subspace $W$ that contains $S$, $L(S)$ is proven to be the absolute minimal (smallest) subspace containing $S$.


# Linear Algebra Notes: Fundamental Subspaces of a Matrix

This section defines the fundamental vector subspaces derived from a general matrix and outlines their structural properties.

---

## Matrix Definition

Let $A_{m \times n}$ be an $m \times n$ matrix containing real numerical entries:

$$A_{m \times n} = \begin{pmatrix} 
a_{11} & a_{12} & \dots & a_{1n} \\ 
a_{21} & a_{22} & \dots & a_{2n} \\ 
\vdots & \vdots & \ddots & \vdots \\ 
a_{m1} & a_{m2} & \dots & a_{mn} 
\end{pmatrix} \quad \text{where } a_{ij} \in \mathbb{R}$$

By applying the linear span operator $L(S)$, we define four fundamental vector spaces associated with matrix $A$:

---

## The Four Fundamental Subspaces

### 1) Row Space of $A$

The row space is the set of all possible linear combinations of the individual row vectors of matrix $A$. It forms a valid vector subspace of $\mathbb{R}^n(\mathbb{R})$.

$$\text{Row Space}(A) = L\left(\left\{ (a_{11}, a_{12}, \dots, a_{1n}), \; (a_{21}, a_{22}, \dots, a_{2n}), \; \dots, \; (a_{m1}, a_{m2}, \dots, a_{mn}) \right\}\right)$$

---

### 2) Column Space of $A$

The column space is the set of all possible linear combinations of the individual column vectors of matrix $A$. It forms a valid vector subspace of $\mathbb{R}^m(\mathbb{R})$.

$$\text{Column Space}(A) = L\left(\left\{ \begin{pmatrix} a_{11} \\ a_{21} \\ \vdots \\ a_{m1} \end{pmatrix}, \; \begin{pmatrix} a_{12} \\ a_{22} \\ \vdots \\ a_{m2} \end{pmatrix}, \; \dots, \; \begin{pmatrix} a_{1n} \\ a_{2n} \\ \vdots \\ a_{mn} \end{pmatrix} \right\}\right)$$

---

### 3) Nullspace of $A$, denoted $N(A)$

The nullspace (or kernel) consists of all domain vector solutions $X$ that satisfy the homogeneous linear equation system $AX = 0$. It forms a valid vector subspace of $\mathbb{R}^n$.

$$N(A) = \left\{ X \in \mathbb{R}^n \;\middle|\; AX = 0 \right\}$$

---

### 4) Range of $A$, denoted $R(A)$

The range (or image) of $A$ consists of all output vectors $b \in \mathbb{R}^m$ that can be generated by multiplying matrix $A$ by an arbitrary domain vector $X \in \mathbb{R}^n$. It forms a valid vector subspace of $\mathbb{R}^m$.

$$R(A) = \left\{ b \in \mathbb{R}^m \;\middle|\; AX = b \text{ for some } X \in \mathbb{R}^n \right\}$$

---

## Core Identity Relationship

In general matrix mapping theory, the space spanned by the columns of a matrix is identical to the set of reachable target outputs:

$$\mathbf{\text{Column Space}(A) = R(A)}$$
