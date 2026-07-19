# Lecture 03: Vector Space - Definition and Examples

## Definition
A **vector space** $V(\mathbb{R})$ over a field $\mathbb{R}$ is a set on which two operations, **vector addition** ($+$) and **scalar multiplication** ($\cdot$), are defined such that the following axioms hold:

---

## Vector Space Axioms

### M1. Abelian Group Under Addition
The algebraic structure $(V, +)$ forms an **abelian group**. This implies five underlying properties for any vectors $u, v, w \in V$:
1. **Closure under Addition:** $u + v \in V$
2. **Associativity:** $(u + v) + w = u + (v + w)$
3. **Identity Element:** There exists a zero vector $0 \in V$ such that $v + 0 = v$
4. **Inverse Element:** There exists an inverse $-v \in V$ such that $v + (-v) = 0$
5. **Commutativity:** $u + v = v + u$

---

### M2. Closure under Scalar Multiplication
The operation $(\cdot)$ is defined between scalars and vectors such that multiplying a scalar by a vector always yields a vector within the same space:

$$\forall \ a \in \mathbb{R} \quad \text{and} \quad v \in V \implies a \cdot v \in V$$

---

### M3. Distributivity of Scalar over Vector Addition
A scalar multiplies distributively over the sum of two vectors:

$$\forall \ a \in \mathbb{R} \quad \text{and} \quad v, w \in V \implies a \cdot (v + w) = a \cdot v + a \cdot w$$

---

### M4. Distributivity of Vector over Scalar Addition
A vector multiplies distributively over the sum of two scalars:

$$\forall \ a, b \in \mathbb{R} \quad \text{and} \quad v \in V \implies (a + b) \cdot v = a \cdot v + b \cdot v$$

---

### M5. Associativity of Scalar Multiplication
When multiplying a vector by multiple scalars, the grouping of the scalar multiplication does not change the result:

$$\forall \ a, b \in \mathbb{R} \quad \text{and} \quad v \in V \implies (ab) \cdot v = a \cdot (b \cdot v)$$

---

### M6. Unitary Law
Multiplying any vector by the scalar identity element ($1$) leaves the vector unchanged:

$$\exists \ 1 \in \mathbb{R} \quad \text{such that} \quad 1 \cdot v = v \quad \forall \ v \in V$$

---

## Conclusion
If all conditions from **M1 to M6** are satisfied, the triplet $(V, +, \cdot)$ is formally recognized as a **vector space**.


# Vector Space Proof Example: $\mathbb{R}^2$ over the Field of Real Numbers

This document provides a step-by-step mathematical proof verifying that the algebraic system $V = \mathbb{R}^2$ forms a valid vector space over the field of real numbers ($\mathbb{R}$).

---

## M1: Verifying $(\mathbb{R}^2, +)$ forms an Abelian Group

To satisfy the **M1 axiom**, the set under component-wise addition must fulfill five independent structural laws:

### 1. Closure Under Addition
For any two elements in the set, their sum must remain inside the set.
* Let $(a,b), (c,d) \in \mathbb{R}^2$. Then:
  $$(a,b) + (c,d) = (a + c, \; b + d)$$
* Since $a,c \in \mathbb{R} \implies (a+c) \in \mathbb{R}$, and $b,d \in \mathbb{R} \implies (b+d) \in \mathbb{R}$:
  $$(a + c, \; b + d) \in \mathbb{R}^2$$
$$\dots \text{Closure property holds in } \mathbb{R}^2.$$

### 2. Commutativity
The order of addition does not alter the resulting vector coordinates.
* Let $(a,b), (c,d) \in \mathbb{R}^2$. Then:
  $$(a,b) + (c,d) = (a + c, \; b + d)$$
  $$\phantom{(a,b) + (c,d)} = (c + a, \; d + b) \quad \text{[By scalar commutativity in } \mathbb{R}\text{]}$$
  $$\phantom{(a,b) + (c,d)} = (c,d) + (a,b)$$
$$\dots \text{Commutativity holds in } \mathbb{R}^2.$$

### 3. Associativity
Grouping patterns during multi-vector operations do not influence the evaluation outcome.
* Let $(a,b), (c,d), (e,f) \in \mathbb{R}^2$. Then:
  $$(a,b) + \big((c,d) + (e,f)\big) = (a,b) + (c + e, \; d + f)$$
  $$\phantom{(a,b) + \big((c,d) + (e,f)\big)} = \big(a + (c + e), \; b + (d + f)\big)$$
  $$\phantom{(a,b) + \big((c,d) + (e,f)\big)} = \big((a + c) + e, \; (b + d) + f\big) \quad \text{[By scalar associativity in } \mathbb{R}\text{]}$$
  $$\phantom{(a,b) + \big((c,d) + (e,f)\big)} = (a + c, \; b + d) + (e,f)$$
  $$\phantom{(a,b) + \big((c,d) + (e,f)\big)} = \big((a,b) + (c,d)\big) + (e,f)$$
$$\dots \text{Associative property holds in } \mathbb{R}^2.$$

### 4. Existence of an Identity Element
There must be a unique neutral element that leaves any vector unchanged upon addition.
* Let $(a,b) \in \mathbb{R}^2$. There exists an element $(0,0) \in \mathbb{R}^2$ such that:
  $$(0,0) + (a,b) = (0 + a, \; 0 + b) = (a,b)$$
$$\dots (0,0) \text{ is the Identity element of } \mathbb{R}^2.$$

### 5. Existence of an Inverse Element
Every element must possess an opposing element that cancels it out to the identity vector.
* Let $(a,b) \in \mathbb{R}^2$. There exists an additive inverse element $(-a,-b) \in \mathbb{R}^2$ such that:
  $$(a,b) + (-a,-b) = \big(a + (-a), \; b + (-b)\big) = (0,0)$$
$$\dots \text{The above five properties prove that } (\mathbb{R}^2, +) \text{ is an Abelian Group.}$$

---

## M2: Closure Under Scalar Multiplication

Multiplying a vector by any scaling constant from the field must yield an element within the vector space.
* Let $k \in \mathbb{R}$ and $(a,b) \in \mathbb{R}^2$. Then:
  $$k(a,b) = (ka, \; kb)$$
* Since $k, a, b \in \mathbb{R}$, both products $ka$ and $kb$ are real numbers.
$$\implies (ka, \; kb) \in \mathbb{R}^2.$$

---

## M3: Distributivity of Scalar over Vector Addition

Scaling a combined sum matches the sum of each independently scaled coordinate vector.
* Let $k \in \mathbb{R}$ and $(a,b), (c,d) \in \mathbb{R}^2$. Then:
  $$k\big((a,b) + (c,d)\big) = k(a + c, \; b + d)$$
  $$\phantom{k\big((a,b) + (c,d)\big)} = \big(k(a + c), \; k(b + d)\big)$$
  $$\phantom{k\big((a,b) + (c,d)\big)} = (ka + kc, \; kb + kd) \quad \text{[By standard distribution laws in } \mathbb{R}\text{]}$$
  $$\phantom{k\big((a,b) + (c,d)\big)} = (ka, \; kb) + (kc, \; kd)$$
  $$\phantom{k\big((a,b) + (c,d)\big)} = k(a,b) + k(c,d)$$

---

## M4: Distributivity of Vector over Scalar Addition

Distributing a single vector across scaled scalar elements matches component execution partitions.
* Let $k, m \in \mathbb{R}$ and $(a,b) \in \mathbb{R}^2$. Then:
  $$(k + m)(a,b) = \big((k + m)a, \; (k + m)b\big)$$
  $$\phantom{(k+m)(a,b)} = (ka + ma, \; kb + mb)$$
  $$\phantom{(k+m)(a,b)} = (ka, \; kb) + (ma, \; mb)$$
  $$\phantom{(k+m)(a,b)} = k(a,b) + m(a,b)$$

---

## M5: Associativity of Scalar Multiplication

Sequential scaling calculations remain invariant regardless of multi-scalar parsing rules.
* Let $k, m \in \mathbb{R}$ and $(a,b) \in \mathbb{R}^2$. Then:
  $$k\big(m(a,b)\big) = k(ma, \; mb)$$
  $$\phantom{k\big(m(a,b)\big)} = \big(k(ma), \; k(mb)\big)$$
  $$\phantom{k\big(m(a,b)\big)} = \big((km)a, \; (km)b\big)$$
  $$\phantom{k\big(m(a,b)\big)} = (km)(a,b)$$

---

## M6: Unitary Law

Scaling a coordinate element by the absolute standard unity value preserves the target space coordinates.
* Let $(a,b) \in \mathbb{R}^2$. Then:
  $$1(a,b) = (1a, \; 1b) = (a,b)$$

---

## Final Verification Summary
$$\text{Since axioms M1 through M6 are completely satisfied, }(\mathbb{R}^2, +, \cdot) \text{ is proven to be a valid Vector Space.}$$


# Vector Space Proof Example: Matrix Space $M_{m \times n}$ over $\mathbb{R}$

This document continues the structural vector space verification, showing that the set $V = M_{m \times n}$ (the set of all matrices of order $m \times n$) forms a valid vector space over the field of real numbers ($\mathbb{R}$). 

Below is the step-by-step mathematical translation of the proof, focusing on a concrete example using $2 \times 2$ matrices ($M_{2 \times 2}$).

---

## M1: Verifying $(M_{2 \times 2}, +)$ forms an Abelian Group

To establish the **M1 axiom**, entry-wise matrix addition must fulfill standard group properties:

### 1. Closure Under Addition
Adding two matrices of order $2 \times 2$ results in another matrix that remains within the space $M_{2 \times 2}$.

* Let $\begin{pmatrix} a_{11} & a_{12} \\ a_{21} & a_{22} \end{pmatrix}, \begin{pmatrix} b_{11} & b_{12} \\ b_{21} & b_{22} \end{pmatrix} \in M_{2 \times 2}$. Then:

  $$\begin{pmatrix} a_{11} & a_{12} \\ a_{21} & a_{22} \end{pmatrix} + \begin{pmatrix} b_{11} & b_{12} \\ b_{21} & b_{22} \end{pmatrix} = \begin{pmatrix} a_{11} + b_{11} & a_{12} + b_{12} \\ a_{21} + b_{21} & a_{22} + b_{22} \end{pmatrix}$$

* Since the elements $a_{ij}$ and $b_{ij}$ are real numbers, their element-wise sums $(a_{ij} + b_{ij})$ are also real numbers. 

$$\implies \begin{pmatrix} a_{11} & a_{12} \\ a_{21} & a_{22} \end{pmatrix} + \begin{pmatrix} b_{11} & b_{12} \\ b_{21} & b_{22} \end{pmatrix} \in M_{2 \times 2}$$

$$\dots \text{Closure property holds in } M_{2 \times 2}.$$

---

### 2. Associativity Under Addition
The grouping of terms during addition does not impact the final entry-wise calculation of the matrix.

* Let $\begin{pmatrix} a_{11} & a_{12} \\ a_{21} & a_{22} \end{pmatrix}, \begin{pmatrix} b_{11} & b_{12} \\ b_{21} & b_{22} \end{pmatrix}, \begin{pmatrix} c_{11} & c_{12} \\ c_{21} & c_{22} \end{pmatrix} \in M_{2 \times 2}$. Then:

  $$\begin{pmatrix} a_{11} & a_{12} \\ a_{21} & a_{22} \end{pmatrix} + \left( \begin{pmatrix} b_{11} & b_{12} \\ b_{21} & b_{22} \end{pmatrix} + \begin{pmatrix} c_{11} & c_{12} \\ c_{21} & c_{22} \end{pmatrix} \right)$$

  $$= \begin{pmatrix} a_{11} & a_{12} \\ a_{21} & a_{22} \end{pmatrix} + \begin{pmatrix} b_{11} + c_{11} & b_{12} + c_{12} \\ b_{21} + c_{21} & b_{22} + c_{22} \end{pmatrix}$$

  $$= \begin{bmatrix} a_{11} + (b_{11} + c_{11}) & a_{12} + (b_{12} + c_{12}) \\ a_{21} + (b_{21} + c_{21}) & a_{22} + (b_{22} + c_{22}) \end{bmatrix}$$

* Because standard scalar addition inside $\mathbb{R}$ is associative, we can shift the parentheses for each element:

  $$= \begin{bmatrix} (a_{11} + b_{11}) + c_{11} & (a_{12} + b_{12}) + c_{12} \\ (a_{21} + b_{21}) + c_{21} & (a_{22} + b_{22}) + c_{22} \end{bmatrix}$$

  $$= \begin{pmatrix} a_{11} + b_{11} & a_{12} + b_{12} \\ a_{21} + b_{21} & a_{22} + b_{22} \end{pmatrix} + \begin{pmatrix} c_{11} & c_{12} \\ c_{21} & c_{22} \end{pmatrix}$$

  $$= \left( \begin{pmatrix} a_{11} & a_{12} \\ a_{21} & a_{22} \end{pmatrix} + \begin{pmatrix} b_{11} & b_{12} \\ b_{21} & b_{22} \end{pmatrix} \right) + \begin{pmatrix} c_{11} & c_{12} \\ c_{21} & c_{22} \end{pmatrix}$$

$$\dots \text{Associative property holds in } M_{2 \times 2}.$$


# Additional Examples of Vector Spaces over $\mathbb{R}$

The following mathematical systems satisfy all the foundational vector space axioms ($M1$ through $M6$) under their standard operations:

---

## 1. Real Coordinate Space ($\mathbb{R}^n$)
The set of all ordered $n$-tuples of real numbers forms a vector space over the field $\mathbb{R}$.

$$V = \mathbb{R}^n = \{(x_1, x_2, \dots, x_n) \mid x_i \in \mathbb{R}\}$$

* **Vector Addition:** Component-wise addition.
* **Scalar Multiplication:** Distributing a real constant across all coordinates.

---

## 2. Polynomial Space ($P$)
The set $V = P$ containing all real-valued polynomials of any degree in an independent variable $x$ forms an infinite-dimensional vector space over $\mathbb{R}$.

$$P = \{a_m x^m + a_{m-1} x^{m-1} + \dots + a_1 x + a_0 \mid m \in \mathbb{N}_0 \text{ and } a_i \in \mathbb{R}\}$$

* **Definition:** The set of all polynomials in variable $x$ with coefficients chosen from the real numbers $\mathbb{R}$.

---

## 3. Polynomial Space of Bounded Degree ($P_n$)
The set $V = P_n$ containing all real-valued polynomials whose maximum degree does not exceed $n$ forms a finite-dimensional vector space over $\mathbb{R}$.

$$P_n = \{a_k x^k + a_{k-1} x^{k-1} + \dots + a_1 x + a_0 \mid k \le n \text{ and } a_i \in \mathbb{R}\}$$

* **Definition:** The set of all polynomials of degree **at most $n$** in variable $x$ with coefficients from $\mathbb{R}$.

---

## 4. Convergent Sequence Space
The set of all mathematically convergent numerical sequences forms a vector space over $\mathbb{R}$.

$$V = \{\langle a_n \rangle \mid \langle a_n \rangle \text{ is a convergent sequence where } \lim_{n \to \infty} a_n = L, \; L \in \mathbb{R}\}$$

* **Vector Addition:** Adding corresponding index values of the two sequences ($\langle a_n \rangle + \langle b_n \rangle = \langle a_n + b_n \rangle$).
* **Scalar Multiplication:** Scaling every sequence element uniformly ($k\langle a_n \rangle = \langle k a_n \rangle$).



# Non-Examples: Sets Not Forming a Vector Space over $\mathbb{R}$

To fail to be a vector space, a set only needs to violate a single axiom among the required properties ($M1$ through $M6$). Below are two common examples of algebraic structures that fail to form a vector space.

---

## Example 1: Set of All Polynomials of Exact Degree $n$

Let $V$ be the set of all polynomials of **exactly** degree $n$. This set does not form a vector space over $\mathbb{R}$.

* **Reason:** Vector addition is **not closed**. Adding two polynomials of degree $n$ can result in the highest-degree terms cancelling out, yielding a polynomial of a lower degree that is no longer in $V$.

### Counterexample ($n = 3$)
Let $V$ be the set of all polynomials of exactly degree $3$. Consider two vectors $v_1, v_2 \in V$:

$$v_1 = 2x^3 + 5x^2 + x + 7 \in V$$
$$v_2 = -2x^3 + 3x^2 + 4x + 1 \in V$$

Now, compute their sum ($v_1 + v_2$):
$$v_1 + v_2 = (2x^3 - 2x^3) + (5x^2 + 3x^2) + (x + 4x) + (7 + 1)$$
$$v_1 + v_2 = 8x^2 + 5x + 8$$

* **Conclusion:** The resulting polynomial has a degree of $2$, meaning $v_1 + v_2 \notin V$. Because the **closure property does not hold**, it is not a vector space.

---

## Example 2: $\mathbb{R}^2(\mathbb{R})$ with Non-Standard Addition

Consider the set $\mathbb{R}^2$ over the field $\mathbb{R}$, but with custom, non-standard operations defined as follows:

* **Vector Addition:** $(x_1, y_1) + (x_2, y_2) = (x_1 + x_2, \; y_1 + 2y_2)$
* **Scalar Multiplication:** $k(x_1, y_1) = (kx_1, \; ky_1)$

* **Reason:** under these non-standard operations, $(\mathbb{R}^2(\mathbb{R}), +)$ is **not an abelian group**. Specifically, it violates the commutative property of vector addition.

### Proof of Failure (Commutativity Violation)
Let us add the vectors in reversed order to check for commutativity:

1. **Left-to-Right Addition:**
   $$(x_1, y_1) + (x_2, y_2) = (x_1 + x_2, \; y_1 + 2y_2)$$

2. **Right-to-Left Addition:**
   $$(x_2, y_2) + (x_1, y_1) = (x_2 + x_1, \; y_2 + 2y_1)$$

Comparing the second components:
$$y_1 + 2y_2 \neq y_2 + 2y_1 \quad \text{(in general)}$$

$$\implies (x_1, y_1) + (x_2, y_2) \neq (x_2, y_2) + (x_1, y_1)$$

* **Conclusion:** Because vector addition is not commutative, $(\mathbb{R}^2, +)$ fails to form an abelian group, disqualifying it from being a valid vector space.

# Mathematical Proof: Failure of Commutativity under Non-Standard Addition

This document provides a detailed structural breakdown of the handwritten proof showing how a non-standard vector addition definition violates the **Commutative Property**, preventing the algebraic system from forming a valid vector space.

---

## The Non-Standard Operational Rule

Let vector addition on $\mathbb{R}^2$ be explicitly defined such that adding any second vector duplicates its $y$-coordinate value before computing the sum:

$$(x_1, y_1) + (x_2, y_2) = (x_1 + x_2, \; y_1 + 2y_2)$$

---

## Step-by-Step Mathematical Proof

To verify if the commutative property holds, we must evaluate the operation in both directional permutations.

### Step 1: Forward Evaluation
Evaluate the addition of vector 1 to vector 2:
$$(x_1, y_1) + (x_2, y_2) = \big(x_1 + x_2, \; \mathbf{y_1 + 2y_2}\big) \quad \text{--- (Equation 1)}$$

### Step 2: Reverse Evaluation
Evaluate the addition of vector 2 to vector 1. According to the operational rule, the *second* operand in the expression always has its $y$-value scaled by $2$:
$$(x_2, y_2) + (x_1, y_1) = \big(x_2 + x_1, \; \mathbf{y_2 + 2y_1}\big) \quad \text{--- (Equation 2)}$$

---

## Analysis and Comparison

Let us compare the individual components of **Equation 1** and **Equation 2**:

* **$x$-components:** $$x_1 + x_2 = x_2 + x_1 \quad \text{(True, by standard real scalar commutativity)}$$

* **$y$-components:** $$y_1 + 2y_2 \neq y_2 + 2y_1 \quad \text{(In general, except when } y_1 = y_2\text{)}$$

### Concrete Numerical Counterexample
Let $(x_1, y_1) = (0, 1)$ and $(x_2, y_2) = (0, 3)$:

1. **Forward:** $(0, 1) + (0, 3) = (0 + 0, \; 1 + 2(3)) = (0, \; \mathbf{7})$
2. **Reverse:** $(0, 3) + (0, 1) = (0 + 0, \; 3 + 2(1)) = (0, \; \mathbf{5})$

Since $(0, 7) \neq (0, 5)$, we establish that:
$$(x_1, y_1) + (x_2, y_2) \neq (x_2, y_2) + (x_1, y_1)$$

---

## Conclusion
$$\mathbf{\text{Commutative property does not hold.}}$$

Because commutativity fails, the structure $(\mathbb{R}^2, +)$ cannot form an **Abelian Group**, which is a mandatory prerequisite axiom ($M1$) for any mathematical system to be classified as a **Vector Space**.




# Geometric Interpretation of Real Coordinate Spaces ($\mathbb{R}^n$)

For dimensional parameters $n = 1, 2, \text{ or } 3$, the real coordinate space $\mathbb{R}^n$ maps directly to physical space, providing an intuitive geometric framework for visualizing algebraic vectors.

---

## 1. One-Dimensional Space ($n = 1$): The Number Line

When $n = 1$, the vector space corresponds to the set of real numbers ($V = \mathbb{R}$). A vector in this space is represented by a single real scalar value, mapping geometrically to a directed coordinate vector along a linear path.

$$v = (x)$$

### Graphic Visualization

```text
               v = (-2)                       v = (5)
          <======================        =========================>
   +------+------+------+------+------+------+------+------+------+------+
  -4     -3     -2     -1      0      1      2      3      4      5

```

* **Example Vector $v = (5)$:** Represented by a forward horizontal arrow extending from the origin ($0$) to the position coordinate $5$.
* **Example Vector $v = (-2)$:** Represented by a backward horizontal arrow extending from the origin ($0$) to the position coordinate $-2$.

---

## 2. Two-Dimensional Space ($n = 2$): The Cartesian Plane

When $n = 2$, the vector space corresponds to the Cartesian coordinate plane ($V = \mathbb{R}^2$). A vector is defined as an ordered pair of real number coordinates.

$$v = (x, y)$$

Geometrically, the vector represents a directed arrow pointing from the origin coordinate $(0,0)$ to the termination point coordinate point $(x, y)$.

### Graphic Visualization
```

                  y ▲
                    │         vector v = (x, y)
                    │             ┌───► (x, y)
                    │            ╱
                    │           ╱ 
                    │          ╱  
                    │         ╱   
                    │        ╱    
  ──────────────────┼─────── caste ────────► x
                    │(0,0)
                    │
                    │
```


---

## 3. Three-Dimensional Space ($n = 3$): Physical Space

When $n = 3$, the vector space corresponds to three-dimensional physical space ($V = \mathbb{R}^3$). A vector is represented as an ordered triplet of real numbers.

$$\vec{v} = (x, y, z)$$

Geometrically, the space is mapped using three mutually perpendicular axes ($x$, $y$, and $z$). The vector is a directed arrow stretching from the central origin point $(0,0,0)$ out to its spatial position coordinates $(x,y,z)$.

### Graphic Visualization


                     z ▲
                       │   
                       │      ╱  vector v = (x, y, z)
                       │     ╱┌───► (x, y, z)
                       │    ╱╱
                       │   ╱╱  
                       │  ╱╱   
                       │ ╱╱    
                       │╱╱     
                       ┼────────────────► y
                      ╱ (0,0,0)
                     ╱
                    ╱
                   ▼ x




# Geometric Interpretation of Vector Addition and Linear Independence in $\mathbb{R}^3$

## 1. Geometric Interpretation of Vector Addition

In three-dimensional space ($\mathbb{R}^3$), vector addition is performed component-wise. 

If we have two vectors $v_1$ and $v_2$ defined by their spatial coordinates:
$$v_1 = (x_1, y_1, z_1) \in \mathbb{R}^3$$
$$v_2 = (x_2, y_2, z_2) \in \mathbb{R}^3$$

Their sum, $v_1 + v_2$, forms a new resultant vector in $\mathbb{R}^3$:
$$v_1 + v_2 = (x_1 + x_2, \; y_1 + y_2, \; z_1 + z_2) \in \mathbb{R}^3$$

### Geometric Representation (The Parallelogram Law)

Geometrically, when you place the tails of $v_1$ and $v_2$ at the origin of a 3D coordinate system, their addition follows the **Parallelogram Law**. The sum $v_1 + v_2$ is represented by the directed diagonal vector of the parallelogram formed by using $v_1$ and $v_2$ as adjacent sides.

```
                     z ▲
                       │      
                       │        /▲ v1 + v2 (Resultant Diagonal)
                       │       / │
                       │     v2  │
                       │     ╱   │ 
                       │   ┌►    │  
                       │  ╱      │   
                       │ ╱       │   
                       │╱        ▼ v1
                       ┼────────────────► y
                      ╱ (0,0,0)
                     ╱
                    ╱
                   ▼ x

```

---

## 2. Geometric Conditions for Linear Independence in $\mathbb{R}^3$

Linear independence among vectors can be interpreted via spatial dimensions (lines and planes). For a set of three vectors $\{v_1, v_2, v_3\}$ to be **linearly independent**, they must span a full three-dimensional space rather than collapsing into a line or a single flat plane.

If vectors $v_1$, $v_2$, and $v_3$ are linearly independent, it implies two geometric rules:

1. **$v_1$ and $v_2$ are not collinear:** They point along different directional paths and do not lie on the exact same straight line passing through the origin. Together, they uniquely span a two-dimensional flat plane.
2. **$v_3$ does not lie in the plane of $v_1$ and $v_2$:** The third vector $v_3$ must point outward, completely independent of the flat 2D surface spanned by the first two vectors. It cannot be coplanar with them.


# Linear Algebra Notes: Euclidean Space

## Definition
The vectors in Euclidean space consist of ordered $n$-tuples of real numbers:

$$x = (x_1, x_2, \dots, x_n)$$

---

## Purpose and Geometric Notions
Euclidean space is used to mathematically represent physical space. It equips the coordinate vector structure with concrete geometric properties, providing precise definitions for notions such as:

* **Distance** (the separation between two coordinate elements)
* **Length** (the magnitude or norm of an individual vector)
* **Angles** (the directional relationship between two intersecting vectors)


---

## Generalization to Higher Dimensions
* For lower dimensions ($n = 1, 2, \text{ or } 3$), these spaces align with our physical realities (lines, planes, and 3D space) and are straightforward to graph.
* Although it becomes hard to visualize spaces where $n > 3$, these fundamental concepts of distance, length, and angles generalize mathematically in obvious, consistent ways.
