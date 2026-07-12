
# Gram Schmidt Process

### Linear Algebra Notes: Orthogonal Sets, Orthonormal Sets, and Orthogonal Projections

This note details the core definitions of orthogonality, orthonormality, and the geometric projection of vectors onto subspaces, preparing the groundwork for the Gram-Schmidt orthogonalization process.

---

## 1. Concept Name: Orthogonal and Orthonormal Sets

### Simple Meaning 💡
* **Orthogonal Set:** A collection of vectors where every single pair of distinct vectors is perpendicular to each other. In any general inner product space, this means their inner product (dot product proxy) is exactly $0$.
* **Orthonormal Set:** An orthogonal set where every vector also has a length (norm) of exactly $1$. Think of them as a customized set of perpendicular unit directional anchors.


---

### Foundational Definitions and Theorems
Let $V$ be a vector space equipped with an inner product $\langle \cdot, \cdot \rangle$.

1. **Orthogonal Set Criterion:** A set of non-zero vectors $\{v_1, v_2, \dots, v_k\} \in V$ forms an orthogonal set if:
   $$\langle v_i, v_j \rangle = 0 \quad \text{for all } i \neq j$$

2. **Orthonormal Set Criterion:** A set forms an orthonormal set if it is orthogonal and every vector satisfies:
   $$\|v_i\| = \sqrt{\langle v_i, v_i \rangle} = 1$$

3. **Core Theorem:** **Any orthogonal set of non-zero vectors is linearly independent.** This means no vector in the set can be built from a combination of the others, ensuring they form a valid coordinate basis for their span.

---

## 2. Concept Name: Orthogonal Projection

### Simple Meaning 💡
Imagine casting a shadow of a floating vector vector $x$ directly down onto a flat two-dimensional tabletop surface subspace $V_0$. 
* The shadow vector that lies flat on the table is called the **orthogonal projection ($p$)**.
* The vertical vector running straight down from the tip of vector $x$ to the table surface is the **orthogonal error component ($o$)**. Because it drops straight down, it is completely perpendicular ($\perp$) to everything on the tabletop subspace.


---

### The Orthogonal Decomposition Theorem
Let $V$ be an inner product space, and let $V_0$ be a finite-dimensional subspace of $V$. Any vector $x \in V$ can be uniquely decomposed as:

$$x = p + o$$

Where:
* $p \in V_0$ is the **orthogonal projection** of $x$ onto the subspace $V_0$.
* $o \perp V_0$ is the component orthogonal to $V_0$.
* The minimum geometric distance from the tip of vector $x$ to the subspace plane $V_0$ is exactly the length of the error vector: $\|o\|$.

---

### Step-by-Step Projection Coordinate Calculation
If $\{v_1, v_2, \dots, v_n\}$ forms an **orthogonal basis** for the target destination subspace $V_0$, the shadow component vector $p$ is computed analytically by summing individual vector projections:

$$p = \frac{\langle x, v_1 \rangle}{\langle v_1, v_1 \rangle}v_1 + \frac{\langle x, v_2 \rangle}{\langle v_2, v_2 \rangle}v_2 + \dots + \frac{\langle x, v_n \rangle}{\langle v_n, v_n \rangle}v_n$$

> **The Unit Norm Shorthand 💡:** If your subspace basis is already **orthonormal** (meaning all denominators $\langle v_i, v_i \rangle = \|v_i\|^2 = 1$), the fraction terms disappear completely, simplifying the formula to:
> $$p = \langle x, v_1 \rangle v_1 + \langle x, v_2 \rangle v_2 + \dots + \langle x, v_n \rangle v_n$$

---

## 3. Supplementary Practice Problems with Solutions

### Problem 1: Verifying Orthogonality and Normalizing a Set
**Scenario:** Consider two vectors in standard Euclidean space $\mathbb{R}^3$:
$$v_1 = \begin{bmatrix} 1 \\ 1 \\ 0 \end{bmatrix}, \quad v_2 = \begin{bmatrix} -1 \\ 1 \\ 5 \end{bmatrix}$$
1. Prove that the set $\{v_1, v_2\}$ is an orthogonal set under the standard dot product inner product.
2. Convert this set into a fully qualified **orthonormal** set.

#### Step-by-Step Calculation:
1. **Compute the Inner Product $\langle v_1, v_2 \rangle$:**
   $$\langle v_1, v_2 \rangle = (1)(-1) + (1)(1) + (0)(5) = -1 + 1 + 0 = \mathbf{0}$$
   Since the inner product is exactly 0, **the set is orthogonal**.

2. **Compute individual vector norms ($\|v_i\| = \sqrt{\langle v_i, v_i \rangle}$):**
   $$\|v_1\| = \sqrt{1^2 + 1^2 + 0^2} = \mathbf{\sqrt{2}}$$
   $$\|v_2\| = \sqrt{(-1)^2 + 1^2 + 5^2} = \sqrt{1 + 1 + 25} = \mathbf{\sqrt{27}}$$

3. **Scale each vector by its inverse length to normalize:**
   $$u_1 = \frac{1}{\|v_1\|}v_1 = \mathbf{\begin{bmatrix} \frac{1}{\sqrt{2}} \\ \frac{1}{\sqrt{2}} \\ 0 \end{bmatrix}}, \quad u_2 = \frac{1}{\|v_2\|}v_2 = \mathbf{\begin{bmatrix} -\frac{1}{\sqrt{27}} \\ \frac{1}{\sqrt{27}} \\ \frac{5}{\sqrt{27}} \end{bmatrix}}$$

#### Solution Conclusion:
The constructed set $\{u_1, u_2\}$ is an **orthonormal set**.

---

### Problem 2: Calculating an Orthogonal Projection Coordinate
**Scenario:** Let a 1D line subspace $V_0$ be spanned by the single basis vector $v_1 = \begin{bmatrix} 2 \\ 1 \end{bmatrix}$. Compute the orthogonal projection vector $p$ of the floating point vector $x = \begin{bmatrix} 4 \\ 8 \end{bmatrix}$ onto $V_0$, and isolate the resulting error component $o$.

#### Step-by-Step Calculation:
1. **Compute the inner product numerator $\langle x, v_1 \rangle$:**
   $$\langle x, v_1 \rangle = (4)(2) + (8)(1) = 8 + 8 = 16$$

2. **Compute the scaling denominator $\langle v_1, v_1 \rangle$:**
   $$\langle v_1, v_1 \rangle = (2)(2) + (1)(1) = 4 + 1 = 5$$

3. **Compute the projection vector $p = \frac{\langle x, v_1 \rangle}{\langle v_1, v_1 \rangle}v_1$:**
   $$p = \frac{16}{5} \begin{bmatrix} 2 \\ 1 \end{bmatrix} = \begin{bmatrix} 6.4 \\ 3.2 \end{bmatrix}$$

4. **Isolate the perpendicular error vector component ($o = x - p$):**
   $$o = \begin{bmatrix} 4 \\ 8 \end{bmatrix} - \begin{bmatrix} 6.4 \\ 3.2 \end{bmatrix} = \mathbf{\begin{bmatrix} -2.4 \\ 4.8 \end{bmatrix}}$$

#### Final Verification Check 💡
Let's verify that our error vector $o$ is truly perpendicular ($\perp$) to our subspace basis vector $v_1$:
$$\langle o, v_1 \rangle = (-2.4)(2) + (4.8)(1) = -4.8 + 4.8 = 0$$
The inner product is exactly 0. This confirms that our decomposition is correct, splitting the vector into a flat projection components shadow and a perfectly perpendicular error drop line.


# Linear Algebra Notes: Gram-Schmidt Orthogonalization Process

This note details the theoretical mechanics, properties, and step-by-step algorithms of the **Gram-Schmidt Process**, used to convert any arbitrary vector basis into a clean, mutually perpendicular **orthogonal** or **orthonormal** basis.

---

## 1. Concept Name: The Gram-Schmidt Process

### Simple Meaning 💡
Imagine you are given an unaligned, skewed set of coordinate axes $\{x_1, x_2, \dots, x_n\}$ that map out a geometric space. Navigating or projecting onto these axes is computationally difficult because they lean toward each other. 

The **Gram-Schmidt Process** is a systematic algorithm that takes this skewed base and straightens it out. It strips away overlapping shadows (dependent projections) step-by-step, generating a brand new set of axes $\{v_1, v_2, \dots, v_n\}$ that map out the exact same space but are **mutually perpendicular (orthogonal)** to one another.


---

### The Step-by-Step Inductive Algorithm

Let $\{x_1, x_2, \dots, x_n\}$ be an arbitrary basis for an inner product space $V$. We construct the orthogonal set $\{v_1, v_2, \dots, v_n\}$ sequentially:

* **Step 1: Set the baseline direction**
  We choose the first vector unmodified to serve as our anchor axis:
  $$v_1 = x_1$$

* **Step 2: Isolate the second perpendicular axis**
  We take the second raw vector $x_2$ and subtract its shadow projection along our first axis $v_1$:
  $$v_2 = x_2 - \frac{\langle x_2, v_1 \rangle}{\langle v_1, v_1 \rangle}v_1$$

* **Step 3: Isolate the third perpendicular axis**
  We take the third raw vector $x_3$ and subtract its simultaneous projections along *both* previously established axes ($v_1$ and $v_2$):
  $$v_3 = x_3 - \frac{\langle x_3, v_1 \rangle}{\langle v_1, v_1 \rangle}v_1 - \frac{\langle x_3, v_2 \rangle}{\langle v_2, v_2 \rangle}v_2$$

* **General Step $n$:**
  $$v_n = x_n - \sum_{j=1}^{n-1} \frac{\langle x_n, v_j \rangle}{\langle v_j, v_j \rangle}v_j$$

The resulting set $\{v_1, v_2, \dots, v_n\}$ forms a fully **orthogonal set**.

---

### Mathematical Proof of Perpendicularity ($\langle v_1, v_2 \rangle = 0$)
Let's verify that the algorithm successfully forces $v_1$ and $v_2$ to be perpendicular by computing their inner product:

$$\langle v_1, v_2 \rangle = \left\langle v_1, \; x_2 - \frac{\langle x_2, v_1 \rangle}{\langle v_1, v_1 \rangle}v_1 \right\rangle$$

Using the linearity properties of inner products, we distribute $v_1$ across the terms:

$$\langle v_1, v_2 \rangle = \langle v_1, x_2 \rangle - \left\langle v_1, \; \frac{\langle x_2, v_1 \rangle}{\langle v_1, v_1 \rangle}v_1 \right\rangle$$
$$\langle v_1, v_2 \rangle = \langle v_1, x_2 \rangle - \frac{\langle x_2, v_1 \rangle}{\langle v_1, v_1 \rangle} \langle v_1, v_1 \rangle$$

The matching $\langle v_1, v_1 \rangle$ scalar terms cancel out perfectly:

$$\langle v_1, v_2 \rangle = \langle v_1, x_2 \rangle - \langle x_2, v_1 \rangle$$

Since inner products are symmetric ($\langle v_1, x_2 \rangle = \langle x_2, v_1 \rangle$):

$$\langle v_1, v_2 \rangle = 0 \quad \mathbf{(Proven)}$$

---

## 2. Structural Properties of the Process (Slide 2)

When running Gram-Schmidt, several key structural properties hold true at every stage $k$:

1. **Subspace Preservation:** The span of the newly generated orthogonal vectors matches the span of the original vectors exactly at each step:
   $$\text{span}(v_1, v_2, \dots, v_k) = \text{span}(x_1, x_2, \dots, x_k)$$
2. **Orthogonal Correction Structure:** Every new vector $v_k$ can be viewed as the raw vector $x_k$ minus its projection $p_k$ onto the preceding subspace:
   $$v_k = x_k - p_k$$
3. **Distance Properties:** The geometric length of the newly generated vector, $\|v_k\|$, represents the shortest possible distance from the raw vector $x_k$ to the subspace spanned by the preceding variables $\{x_1, x_2, \dots, x_{k-1}\}$.

---

## 3. Extending to an Orthonormal Basis ($w_n$)

If our final goal is an **orthonormal basis** (where every vector is perpendicular *and* has a length of exactly $1$), we simply scale each orthogonal vector $v_i$ by its inverse length (norm):

$$w_i = \frac{v_i}{\|v_i\|}$$

Using these normalized vectors simplifies our projection calculations, changing our iterative framework to:

$$v_1 = x_1 \implies w_1 = \frac{v_1}{\|v_1\|}$$
$$v_2 = x_2 - \langle x_2, w_1 \rangle w_1 \implies w_2 = \frac{v_2}{\|v_2\|}$$
$$v_3 = x_3 - \langle x_3, w_1 \rangle w_1 - \langle x_3, w_2 \rangle w_2 \implies w_3 = \frac{v_3}{\|v_3\|}$$

---

## 4. Comprehensive Numerical Walkthrough (Slide 4)

### Problem Statement
Let $P$ be a two-dimensional plane subspace in $\mathbb{R}^3$ spanned by the raw vector basis:
$$x_1 = (1, 2, 2), \quad x_2 = (-1, 0, 2)$$
1. Find an **orthonormal basis** $\{w_1, w_2\}$ for the plane $P$.
2. Extend this basis to map the entire three-dimensional space $\mathbb{R}^3$.

---

### Part 4.1: Compute the Orthonormal Basis for Plane $P$

#### Step 1: Compute the first vector $w_1$
Set $v_1 = x_1 = (1, 2, 2)$. Calculate its geometric length:
$$\|v_1\| = \sqrt{1^2 + 2^2 + 2^2} = \sqrt{1 + 4 + 4} = \sqrt{9} = 3$$

Normalize $v_1$ to find our first orthonormal vector $w_1$:
$$w_1 = \frac{v_1}{\|v_1\|} = \mathbf{\frac{1}{3}(1, 2, 2) = \left(\frac{1}{3}, \frac{2}{3}, \frac{2}{3}\right)}$$

---

#### Step 2: Compute the second vector $w_2$
Subtract the shadow projection of $x_2$ along our normalized $w_1$ axis:
$$v_2 = x_2 - \langle x_2, w_1 \rangle w_1$$

First, compute the inner product term $\langle x_2, w_1 \rangle$:
$$\langle x_2, w_1 \rangle = (-1)\left(\frac{1}{3}\right) + (0)\left(\frac{2}{3}\right) + (2)\left(\frac{2}{3}\right) = -\frac{1}{3} + 0 + \frac{4}{3} = \frac{3}{3} = 1$$

Now, compute the orthogonal component $v_2$:
$$v_2 = (-1, 0, 2) - 1 \cdot \left(\frac{1}{3}, \frac{2}{3}, \frac{2}{3}\right)$$
$$v_2 = \left(-1 - \frac{1}{3}, \; 0 - \frac{2}{3}, \; 2 - \frac{2}{3}\right) = \mathbf{\left(-\frac{4}{3}, -\frac{2}{3}, \frac{4}{3}\right)}$$

To make calculations easier, we factor out a scalar constant: $v_2 = \frac{1}{3}(-4, -2, 4)$. Next, calculate its length:
$$\|v_2\| = \sqrt{\left(-\frac{4}{3}\right)^2 + \left(-\frac{2}{3}\right)^2 + \left(\frac{4}{3}\right)^2} = \sqrt{\frac{16}{9} + \frac{4}{9} + \frac{16}{9}} = \sqrt{\frac{36}{9}} = \sqrt{4} = 2$$

Normalize $v_2$ to find our second orthonormal vector $w_2$:
$$w_2 = \frac{v_2}{\|v_2\|} = \frac{\frac{1}{3}(-4, -2, 4)}{2} = \frac{1}{6}(-4, -2, 4) = \mathbf{\frac{1}{3}(-2, -1, 2)}$$

The set **$\{w_1, w_2\}$** forms our final orthonormal basis for the plane $P$.

---

### Part 4.2: Extend the System to a Basis for $\mathbb{R}^3$

To expand our 2D plane basis to cover the entire 3D space ($\mathbb{R}^3$), we introduce a third independent vector that does not lie on the plane. Let's select the standard unit vector $x_3 = (0, 0, 1)$.

#### Step 3: Compute the third vector $w_3$
We subtract the projections of $x_3$ along both $w_1$ and $w_2$:
$$v_3 = x_3 - \langle x_3, w_1 \rangle w_1 - \langle x_3, w_2 \rangle w_2$$

1. Compute the first inner product term $\langle x_3, w_1 \rangle$:
   $$\langle x_3, w_1 \rangle = (0)\left(\frac{1}{3}\right) + (0)\left(\frac{2}{3}\right) + (1)\left(\frac{2}{3}\right) = \frac{2}{3}$$
2. Compute the second inner product term $\langle x_3, w_2 \rangle$:
   $$\langle x_3, w_2 \rangle = (0)\left(-\frac{2}{3}\right) + (0)\left(-\frac{1}{3}\right) + (1)\left(\frac{2}{3}\right) = \frac{2}{3}$$

Substitute these values back into the equation to calculate the orthogonal vector $v_3$:
$$v_3 = (0, 0, 1) - \frac{2}{3}\left(\frac{1}{3}, \frac{2}{3}, \frac{2}{3}\right) - \frac{2}{3}\left(-\frac{2}{3}, -\frac{1}{3}, \frac{2}{3}\right)$$
$$v_3 = (0, 0, 1) - \left(\frac{2}{9}, \frac{4}{9}, \frac{4}{9}\right) - \left(-\frac{4}{9}, -\frac{2}{9}, \frac{4}{9}\right)$$
$$v_3 = \left(0 - \frac{2}{9} + \frac{4}{9}, \;\; 0 - \frac{4}{9} + \frac{2}{9}, \;\; 1 - \frac{4}{9} - \frac{4}{9}\right) = \mathbf{\left(\frac{2}{9}, -\frac{2}{9}, \frac{1}{9}\right)}$$

Factoring out the scalar gives $v_3 = \frac{1}{9}(2, -2, 1)$. Next, calculate its length:
$$\|v_3\| = \sqrt{\left(\frac{2}{9}\right)^2 + \left(-\frac{2}{9}\right)^2 + \left(\frac{1}{9}\right)^2} = \sqrt{\frac{4}{81} + \frac{4}{81} + \frac{1}{81}} = \sqrt{\frac{9}{81}} = \frac{3}{9} = \frac{1}{3}$$

Normalize $v_3$ to find our third orthonormal vector $w_3$:
$$w_3 = \frac{v_3}{\|v_3\|} = \frac{\frac{1}{9}(2, -2, 1)}{\frac{1}{3}} = \mathbf{\frac{1}{3}(2, -2, 1)}$$

#### Final Basis for $\mathbb{R}^3$:
$$\left\{ \frac{1}{3}(1, 2, 2), \;\; \frac{1}{3}(-2, -1, 2), \;\; \frac{1}{3}(2, -2, 1) \right\}$$