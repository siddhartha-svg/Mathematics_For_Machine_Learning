# Lecture 11: Spectral Decomposition & Eigendecomposition

This section introduces the foundational concepts of **Eigendecomposition** and **Spectral Decomposition**. These matrix factorization methods break down square matrices into their fundamental components (eigenvalues and eigenvectors), which serves as a core mechanism behind many major Machine Learning algorithms.

---

## 1. Why Are These Concepts Important?

Much like basic eigenpairs, breaking a matrix down into its component parts is essential for optimizing complex multi-dimensional computational structures. Key domains include:

* **Principal Component Analysis (PCA):** Reducing dimensional complexity in data science.
* **Spectral Clustering:** Grouping non-linearly separable data clusters.
* **Reinforcement Learning & Statistical ML:** Simplifying state-space transitions and covariance layouts.
* **Image Processing:** Compression, filtering, and computer vision feature mapping.

---

## 2. Eigendecomposition of a Square Matrix

### Core Definition

Let $A \in \mathbb{R}^{n \times n}$ be a **square matrix** of order $n$. Suppose $A$ possesses a complete set of $n$ **linearly independent (LI)** eigenvectors, denoted as $\{v_1, v_2, \dots, v_n\}$.

Under these structural conditions, the matrix $A$ can be factorized or diagonalized into a product of three matrices:

$$A = PDP^{-1}$$

### Detailed Component Mapping:

* **$P$ (Eigenvector Matrix):** An $n \times n$ matrix whose columns are the linearly independent eigenvectors of $A$.

$$P = \begin{bmatrix} \vert & \vert & & \vert \\ v_1 & v_2 & \dots & v_n \\ \vert & \vert & & \vert \end{bmatrix}$$


* **$D$ (Diagonal Eigenvalue Matrix):** An $n \times n$ diagonal matrix whose elements along the main diagonal are the eigenvalues corresponding to the eigenvectors in $P$.

$$D = \begin{bmatrix} \lambda_1 & 0 & \dots & 0 \\ 0 & \lambda_2 & \dots & 0 \\ \vdots & \vdots & \ddots & \vdots \\ 0 & 0 & \dots & \lambda_n \end{bmatrix}$$



In index notation: 
$$D_{ii} = \lambda_i$$



> ### ⚠️ Crucial Constraint
> 
> 
> **Not every square matrix possesses an eigendecomposition.** A square matrix can only be diagonalized via $A = PDP^{-1}$ **if and only if** it has exactly $n$ linearly independent eigenvectors. If a matrix doesn't have enough independent eigenvectors, it is called a *defective matrix*.

---

## 3. Walkthrough Examples

### Example 1: A Valid Diagonalizable Matrix

Let's analyze a simple $2 \times 2$ matrix:

$$A = \begin{bmatrix} 4 & 2 \\ 1 & 3 \end{bmatrix}$$

#### 1. Compute Eigenvalues ($\lambda$)

Solving $\det(A - \lambda I) = 0$:


$$\begin{vmatrix} 4-\lambda & 2 \\ 1 & 3-\lambda \end{vmatrix} = 0 \implies (4-\lambda)(3-\lambda) - 2 = 0$$

$$\lambda^2 - 7\lambda + 10 = 0 \implies (\lambda - 5)(\lambda - 2) = 0$$

$$\implies \lambda_1 = 5, \quad \lambda_2 = 2$$

#### 2. Find Eigenvectors ($v_i$)

* For $\lambda_1 = 5$, the eigenvector calculation yields: $v_1 = \begin{bmatrix} 2 \\ 1 \end{bmatrix}$
* For $\lambda_2 = 2$, the eigenvector calculation yields: $v_2 = \begin{bmatrix} -1 \\ 1 \end{bmatrix}$

Since these two vectors are not multiples of each other, they are linearly independent. We can construct $P$, $D$, and $P^{-1}$:

$$P = \begin{bmatrix} 2 & -1 \\ 1 & 1 \end{bmatrix}, \quad D = \begin{bmatrix} 5 & 0 \\ 0 & 2 \end{bmatrix}, \quad P^{-1} = \frac{1}{3}\begin{bmatrix} 1 & 1 \\ -1 & 2 \end{bmatrix}$$

#### 3. Verify Product Layout ($A = PDP^{-1}$)

$$PDP^{-1} = \begin{bmatrix} 2 & -1 \\ 1 & 1 \end{bmatrix} \begin{bmatrix} 5 & 0 \\ 0 & 2 \end{bmatrix} \left( \frac{1}{3}\begin{bmatrix} 1 & 1 \\ -1 & 2 \end{bmatrix} \right) = \begin{bmatrix} 4 & 2 \\ 1 & 3 \end{bmatrix} = A$$

The decomposition works perfectly.

---

### Example 2: A Counter-Example (Defective Matrix)

Let's look at a square matrix that fails the decomposition rule:

$$B = \begin{bmatrix} 3 & 1 \\ 0 & 3 \end{bmatrix}$$

#### 1. Compute Eigenvalues

$$\det(B - \lambda I) = \begin{vmatrix} 3-\lambda & 1 \\ 0 & 3-\lambda \end{vmatrix} = (3-\lambda)^2 = 0 \implies \lambda = 3 \text{ (with multiplicity 2)}$$

#### 2. Find Eigenvectors

Substitute $\lambda = 3$ back into the system $(B - 3I)v = \mathbf{0}$:


$$\begin{bmatrix} 0 & 1 \\ 0 & 0 \end{bmatrix} \begin{bmatrix} x_1 \\ x_2 \end{bmatrix} = \begin{bmatrix} 0 \\ 0 \end{bmatrix} \implies x_2 = 0$$

This leaves only a single unique eigenvector direction: $v = \begin{bmatrix} 1 \\ 0 \end{bmatrix}$.

#### Conclusion

Because matrix $B$ is a $2 \times 2$ matrix but only possesses **one** linearly independent eigenvector, it is defective. You cannot construct a full square matrix $P$, meaning **matrix $B$ does not possess an eigendecomposition.**



## Conditions for Eigendecomposition (Defective Matrices)

This section details the explicit conditions required to perform an **eigendecomposition** on a square matrix, highlighting the concepts of Algebraic Multiplicity (AM) and Geometric Multiplicity (GM).

---

## 1. Core Condition for Eigendecomposition

For an $n \times n$ square matrix $A$ to be diagonalizable via eigendecomposition ($A = PDP^{-1}$), it must possess a complete set of $n$ linearly independent eigenvectors.

A matrix meets this criteria if and only if the following conditions are satisfied:

* **$\text{AM} = \text{GM}$ for every eigenvalue:** The number of times an eigenvalue appears as a root must exactly match the number of linearly independent eigenvectors it produces.
* **Span the Vector Space:** The total collection of eigenvectors must form a complete basis capable of spanning the $n$-dimensional vector space ($\mathbb{R}^n$).

> ### 🔍 Defining Multiplicities
> 
> 
> * **Algebraic Multiplicity (AM):** The number of times a specific eigenvalue $\lambda$ appears as a root in the characteristic polynomial equation $\det(A - \lambda I) = 0$.
> * **Geometric Multiplicity (GM):** The number of linearly independent eigenvectors associated with that eigenvalue. It corresponds to the dimension of the nullspace (or eigenspace) of $(A - \lambda I)$.
> 
> 
> **The Golden Rule:** $\text{GM}$ can never exceed $\text{AM}$ ($1 \le \text{GM} \le \text{AM}$). If $\text{GM} < \text{AM}$ for even one eigenvalue, the matrix is **defective** and cannot undergo eigendecomposition.

---

## 2. Walkthrough Example: A Defective Matrix

**Problem:** Determine if the following $3 \times 3$ upper triangular matrix $A$ possesses an eigendecomposition:

$$A = \begin{bmatrix} 1 & 1 & 1 \\ 0 & 1 & 1 \\ 0 & 0 & 1 \end{bmatrix}$$

### Step 1: Find the Eigenvalues and Algebraic Multiplicity (AM)

Since $A$ is an upper triangular matrix, its eigenvalues are simply the elements sitting directly on its main diagonal:

$$\lambda = 1, \; 1, \; 1$$

* The single unique eigenvalue is $\lambda = 1$.
* Because it repeats three times, its **Algebraic Multiplicity is 3** ($\text{AM} = 3$).

---

### Step 2: Compute the Geometric Multiplicity (GM)

To find the number of independent eigenvectors, we evaluate the homogeneous system $(A - \lambda I)v = \mathbf{0}$ for $\lambda = 1$:

$$(A - 1I)v = \mathbf{0}$$

$$\begin{bmatrix} 1-1 & 1 & 1 \\ 0 & 1-1 & 1 \\ 0 & 0 & 1-1 \end{bmatrix} \begin{bmatrix} v_1 \\ v_2 \\ v_3 \end{bmatrix} = \begin{bmatrix} 0 \\ 0 \\ 0 \end{bmatrix}$$

$$\begin{bmatrix} 0 & 1 & 1 \\ 0 & 0 & 1 \\ 0 & 0 & 0 \end{bmatrix} \begin{bmatrix} v_1 \\ v_2 \\ v_3 \end{bmatrix} = \begin{bmatrix} 0 \\ 0 \\ 0 \end{bmatrix}$$

Let's expand this matrix system into individual linear algebraic equations:

1. From Row 2: $0v_1 + 0v_2 + 1v_3 = 0 \implies \mathbf{v_3 = 0}$
2. From Row 1: $0v_1 + 1v_2 + 1v_3 = 0 \implies v_2 + 0 = 0 \implies \mathbf{v_2 = 0}$
3. The variable $v_1$ has no constraints placed upon it, meaning it acts as our single free parameter variable.

Setting the free variable $v_1 = 1$, we obtain only **one** distinct base eigenvector direction:

$$v = \begin{bmatrix} 1 \\ 0 \\ 0 \end{bmatrix}$$

* Because this single eigenvalue yields only one linearly independent eigenvector, its **Geometric Multiplicity is 1** ($\text{GM} = 1$).

---

### Step 3: Check the Eigendecomposition Condition

Let's compare our structural results:

$$\text{AM} = 3, \quad \text{GM} = 1 \implies \mathbf{\text{AM} \neq \text{GM}}$$

### Final Conclusion

Because $\text{GM} < \text{AM}$, the matrix lacks enough independent eigenvectors to build a full $3 \times 3$ matrix $P$.

$$\text{Therefore, we do not have an eigendecomposition for matrix } A.$$

---

## 3. Comparative Example: A Diagonalizable Matrix

To see how a repeating root *can* pass the test, let's examine the $3 \times 3$ identity matrix $I$:

$$I = \begin{bmatrix} 1 & 0 & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 1 \end{bmatrix}$$

### 1. Analyze Multiplicities

* **Eigenvalues:** $\lambda = 1, 1, 1 \implies \mathbf{\text{AM} = 3}$
* **Evaluate $(I - 1I)v = \mathbf{0}$:**

$$\begin{bmatrix} 0 & 0 & 0 \\ 0 & 0 & 0 \\ 0 & 0 & 0 \end{bmatrix} \begin{bmatrix} v_1 \\ v_2 \\ v_3 \end{bmatrix} = \begin{bmatrix} 0 \\ 0 \\ 0 \end{bmatrix}$$



### 2. Determine GM

Here, all three variables ($v_1, v_2, v_3$) are completely free. We can choose three independent basis vectors:

$$v_1 = \begin{bmatrix} 1 \\ 0 \\ 0 \end{bmatrix}, \quad v_2 = \begin{bmatrix} 0 \\ 1 \\ 0 \end{bmatrix}, \quad v_3 = \begin{bmatrix} 0 \\ 0 \\ 1 \end{bmatrix} \implies \mathbf{\text{GM} = 3}$$

### Conclusion

Since $\text{AM} = \text{GM} = 3$, this system passes the criteria perfectly and can be successfully decomposed.




This section introduces **Spectral Decomposition**, a special form of eigendecomposition that is mathematically guaranteed to exist for every real symmetric matrix.

---

## 1. Core Framework and The Spectral Theorem

If $A \in \mathbb{R}^{n \times n}$ is a **real symmetric matrix** ($A = A^T$), its eigendecomposition is **always guaranteed** to exist. You never have to worry about a real symmetric matrix being defective.

According to the **Spectral Theorem**, any real symmetric matrix can be orthogonally diagonalized:

$$A = PDP^{-1}$$

### The Orthogonal Matrix Property ($P^{-1} = P^T$)

Because $A$ is symmetric, its eigenvectors $\{v_1, v_2, \dots, v_n\}$ can be chosen to be completely **orthonormal** (mutually perpendicular and scaled to a unit length of 1).

For any matrix $P$ constructed from orthonormal columns, it is an **orthogonal matrix**, which gives it a unique computational shortcut: its inverse is simply its transpose!

$$P^{-1} = P^T$$

Substituting this back into the core equation yields the primary structural layout for Spectral Decomposition:

$$A = PDP^T$$

---

## 2. Matrix Expansion Layout

Let $\lambda_1, \lambda_2, \dots, \lambda_n$ be the eigenvalues of the symmetric matrix $A$, and let $v_1, v_2, \dots, v_n$ be their corresponding normalized column eigenvectors. The full matrix layout expands like this:

$$A = \begin{bmatrix} \vert & \vert & & \vert \\ v_1 & v_2 & \dots & v_n \\ \vert & \vert & & \vert \end{bmatrix} \begin{bmatrix} \lambda_1 & 0 & \dots & 0 \\ 0 & \lambda_2 & \dots & 0 \\ \vdots & \vdots & \ddots & \vdots \\ 0 & 0 & \dots & \lambda_n \end{bmatrix} \begin{bmatrix} \longleftarrow & v_1^T & \longleftarrow \\ \longleftarrow & v_2^T & \longleftarrow \\ & \vdots & \\ \longleftarrow & v_n^T & \longleftarrow \end{bmatrix}$$

---

## 3. Walkthrough Verification Example

Let's look at a concrete, step-by-step example using a $2 \times 2$ symmetric matrix:

$$A = \begin{bmatrix} 2 & 1 \\ 1 & 2 \end{bmatrix}$$

### Step 1: Find the Eigenvalues ($\lambda$)

Set up the characteristic polynomial equation $\det(A - \lambda I) = 0$:

$$\begin{vmatrix} 2-\lambda & 1 \\ 1 & 2-\lambda \end{vmatrix} = 0 \implies (2-\lambda)^2 - 1 = 0$$

$$\lambda^2 - 4\lambda + 3 = 0 \implies (\lambda - 3)(\lambda - 1) = 0$$

$$\implies \lambda_1 = 3, \quad \lambda_2 = 1$$

---

### Step 2: Compute Orthonormal Eigenvectors ($v_i$)

* **For $\lambda_1 = 3$:**

$$(A - 3I)v_1 = \mathbf{0} \implies \begin{bmatrix} -1 & 1 \\ 1 & -1 \end{bmatrix} \begin{bmatrix} x_1 \\ x_2 \end{bmatrix} = \begin{bmatrix} 0 \\ 0 \end{bmatrix} \implies x_1 = x_2$$



Choosing $x_1 = 1$ gives $\begin{bmatrix} 1 \\ 1 \end{bmatrix}$. Normalizing it to a unit length gives:

$$v_1 = \begin{bmatrix} \frac{1}{\sqrt{2}} \\ \frac{1}{\sqrt{2}} \end{bmatrix}$$


* **For $\lambda_2 = 1$:**

$$(A - 1I)v_2 = \mathbf{0} \implies \begin{bmatrix} 1 & 1 \\ 1 & 1 \end{bmatrix} \begin{bmatrix} x_1 \\ x_2 \end{bmatrix} = \begin{bmatrix} 0 \\ 0 \end{bmatrix} \implies x_1 = -x_2$$



Choosing $x_2 = 1$ gives $\begin{bmatrix} -1 \\ 1 \end{bmatrix}$. Normalizing it to a unit length gives:

$$v_2 = \begin{bmatrix} -\frac{1}{\sqrt{2}} \\ \frac{1}{\sqrt{2}} \end{bmatrix}$$



---

### Step 3: Assemble the Matrices $P$ and $D$

Stack the unit eigenvectors column-wise to build $P$, and arrange the matching eigenvalues along the diagonal of $D$:

$$P = \begin{bmatrix} \frac{1}{\sqrt{2}} & -\frac{1}{\sqrt{2}} \\ \frac{1}{\sqrt{2}} & \frac{1}{\sqrt{2}} \end{bmatrix}, \quad D = \begin{bmatrix} 3 & 0 \\ 0 & 1 \end{bmatrix}$$

Because the columns of $P$ are orthonormal, we don't need to perform any long matrix inversions. The inverse matrix is simply its transpose:

$$P^T = \begin{bmatrix} \frac{1}{\sqrt{2}} & \frac{1}{\sqrt{2}} \\ -\frac{1}{\sqrt{2}} & \frac{1}{\sqrt{2}} \end{bmatrix}$$

---

### Step 4: Verify the Decomposition ($PDP^T$)

Let's multiply the matrices back together to verify that they reconstruct our original matrix $A$:

$$PDP^T = \left( \begin{bmatrix} \frac{1}{\sqrt{2}} & -\frac{1}{\sqrt{2}} \\ \frac{1}{\sqrt{2}} & \frac{1}{\sqrt{2}} \end{bmatrix} \begin{bmatrix} 3 & 0 \\ 0 & 1 \end{bmatrix} \right) \begin{bmatrix} \frac{1}{\sqrt{2}} & \frac{1}{\sqrt{2}} \\ -\frac{1}{\sqrt{2}} & \frac{1}{\sqrt{2}} \end{bmatrix}$$

First, multiply $P$ and $D$:


$$PD = \begin{bmatrix} \frac{3}{\sqrt{2}} & -\frac{1}{\sqrt{2}} \\ \frac{3}{\sqrt{2}} & \frac{1}{\sqrt{2}} \end{bmatrix}$$

Now, multiply $(PD)$ by $P^T$:


$$A = \begin{bmatrix} \frac{3}{\sqrt{2}} & -\frac{1}{\sqrt{2}} \\ \frac{3}{\sqrt{2}} & \frac{1}{\sqrt{2}} \end{bmatrix} \begin{bmatrix} \frac{1}{\sqrt{2}} & \frac{1}{\sqrt{2}} \\ -\frac{1}{\sqrt{2}} & \frac{1}{\sqrt{2}} \end{bmatrix}$$

$$A = \begin{bmatrix} (\frac{3}{2} + \frac{1}{2}) & (\frac{3}{2} - \frac{1}{2}) \\ (\frac{3}{2} - \frac{1}{2}) & (\frac{3}{2} + \frac{1}{2}) \end{bmatrix} = \begin{bmatrix} 2 & 1 \\ 1 & 2 \end{bmatrix}$$

The verification matches perfectly!




---

## 1. Core Framework: The Outer Product Expansion

Let $A \in \mathbb{R}^{n \times n}$ be a real symmetric matrix ($A = A^T$). Because it is symmetric, its eigenvectors $\{v_1, v_2, \dots, v_n\}$ form an orthonormal basis, making the eigenvector matrix $P$ orthogonal:

$$P = \begin{bmatrix} \vert & \vert & & \vert \\ v_1 & v_2 & \dots & v_n \\ \vert & \vert & & \vert \end{bmatrix} \implies P^{-1} = P^T = \begin{bmatrix} \longleftarrow & v_1^T & \longleftarrow \\ \longleftarrow & v_2^T & \longleftarrow \\ & \vdots & \\ \longleftarrow & v_n^T & \longleftarrow \end{bmatrix}$$

Substituting this into the standard diagonalization form $A = PDP^{-1}$ gives:

$$A = \begin{bmatrix} \vert & \vert & & \vert \\ v_1 & v_2 & \dots & v_n \\ \vert & \vert & & \vert \end{bmatrix} \begin{bmatrix} \lambda_1 & 0 & \dots & 0 \\ 0 & \lambda_2 & \dots & 0 \\ \vdots & \vdots & \ddots & \vdots \\ 0 & 0 & \dots & \lambda_n \end{bmatrix} \begin{bmatrix} \longleftarrow & v_1^T & \longleftarrow \\ \longleftarrow & v_2^T & \longleftarrow \\ & \vdots & \\ \longleftarrow & v_n^T & \longleftarrow \end{bmatrix}$$

By performing this matrix multiplication block-by-block, the product simplifies into a sum of outer products:

$$A = \lambda_1 v_1 v_1^T + \lambda_2 v_2 v_2^T + \dots + \lambda_n v_n v_n^T$$

Written compactly using summation notation, this yields the **Spectral Decomposition of $A$**:

$$A = \sum_{i=1}^{n} \lambda_i v_i v_i^T$$

---

## 2. Geometric Interpretation: Orthogonal Projections

Each individual component matrix $v_i v_i^T$ in the sum has unique structural properties:

* **Dimensions:** It is an $n \times n$ square symmetric matrix.
* **Rank-1 Property:** Because it is formed by a column vector multiplied by a row vector, its rank is exactly 1.
* **Projection Mapping:** The matrix $v_i v_i^T$ acts as an **orthogonal projection operator** onto the 1-dimensional subspace (line) spanned by the eigenvector $v_i$.

> ### 💡 The Projection Map Function
> 
> 
> If you apply this component to an arbitrary vector $x$, the projection function $\underline{P}(x)$ isolates the component of $x$ pointing in the direction of $v_j$:
> $$\underline{P}(x) = (v_j v_j^T) x = v_j (v_j^T x)$$
> 
> 
> Here, the scalar dot product $(v_j^T x)$ acts as a coordinate weight, showing how far $x$ extends along the $v_j$ axis.

---

## 3. Walkthrough Concrete Example

Let's look at a step-by-step example using a $2 \times 2$ symmetric matrix:

$$A = \begin{bmatrix} 2 & 1 \\ 1 & 2 \end{bmatrix}$$

From our previous derivations, the orthonormal eigenpairs for this matrix are:

* **For $\lambda_1 = 3$:** $v_1 = \begin{bmatrix} \frac{1}{\sqrt{2}} \\ \frac{1}{\sqrt{2}} \end{bmatrix}$
* **For $\lambda_2 = 1$:** $v_2 = \begin{bmatrix} -\frac{1}{\sqrt{2}} \\ \frac{1}{\sqrt{2}} \end{bmatrix}$

### Step 1: Construct the Rank-1 Projection Matrices ($v_i v_i^T$)

Let's compute the outer product for the first eigenvector path:


$$v_1 v_1^T = \begin{bmatrix} \frac{1}{\sqrt{2}} \\ \frac{1}{\sqrt{2}} \end{bmatrix} \begin{bmatrix} \frac{1}{\sqrt{2}} & \frac{1}{\sqrt{2}} \end{bmatrix} = \begin{bmatrix} \frac{1}{2} & \frac{1}{2} \\ \frac{1}{2} & \frac{1}{2} \end{bmatrix}$$

Now, let's compute the outer product for the second eigenvector path:


$$v_2 v_2^T = \begin{bmatrix} -\frac{1}{\sqrt{2}} \\ \frac{1}{\sqrt{2}} \end{bmatrix} \begin{bmatrix} -\frac{1}{\sqrt{2}} & \frac{1}{\sqrt{2}} \end{bmatrix} = \begin{bmatrix} \frac{1}{2} & -\frac{1}{2} \\ -\frac{1}{2} & \frac{1}{2} \end{bmatrix}$$

---

### Step 2: Assemble the Weighted Spectral Sum ($\sum \lambda_i v_i v_i^T$)

Scale each projection matrix by its corresponding eigenvalue and add them together:

$$A = \lambda_1 (v_1 v_1^T) + \lambda_2 (v_2 v_2^T)$$

$$A = 3 \begin{bmatrix} \frac{1}{2} & \frac{1}{2} \\ \frac{1}{2} & \frac{1}{2} \end{bmatrix} + 1 \begin{bmatrix} \frac{1}{2} & -\frac{1}{2} \\ -\frac{1}{2} & \frac{1}{2} \end{bmatrix}$$

$$A = \begin{bmatrix} \frac{3}{2} & \frac{3}{2} \\ \frac{3}{2} & \frac{3}{2} \end{bmatrix} + \begin{bmatrix} \frac{1}{2} & -\frac{1}{2} \\ -\frac{1}{2} & \frac{1}{2} \end{bmatrix}$$

$$A = \begin{bmatrix} (\frac{3}{2} + \frac{1}{2}) & (\frac{3}{2} - \frac{1}{2}) \\ (\frac{3}{2} - \frac{1}{2}) & (\frac{3}{2} + \frac{1}{2}) \end{bmatrix} = \begin{bmatrix} 2 & 1 \\ 1 & 2 \end{bmatrix}$$

### Conclusion

The matrix summation matches our original matrix $A$ perfectly. This confirms that the linear transformation $A$ can be viewed as taking an input vector, splitting it into components along the orthogonal axes $v_1$ and $v_2$, scaling those components by $3$ and $1$ respectively, and recombining them.




This section documents the specific step-by-step example from the lecture slides that verifies the expansion of a $2 \times 2$ symmetric matrix into a sum of rank-1 projection matrices.

---

## 1. Problem Formulation

Given a $2 \times 2$ real symmetric matrix $A$, verify its spectral decomposition using two equivalent approaches:

1. **The Standard $PDP^T$ Layout:** Matrix diagonalization via an orthogonal eigenvector matrix $P$ and diagonal eigenvalue matrix $D$.
2. **The Rank-1 Outer Product Sum:** Expressing the transformation as a weighted sum of geometric projection matrices ($A = \lambda_1 v_1 v_1^T + \lambda_2 v_2 v_2^T$).

### Given Structural Data:

* **Eigenvalues:** $\lambda_1 = 3, \quad \lambda_2 = 1$
* **Orthonormal Eigenvectors:**

$$v_1 = \begin{bmatrix} \frac{1}{\sqrt{2}} \\ \frac{1}{\sqrt{2}} \end{bmatrix}, \quad v_2 = \begin{bmatrix} -\frac{1}{\sqrt{2}} \\ \frac{1}{\sqrt{2}} \end{bmatrix}$$



---

## 2. Approach 1: Verification via Matrix Multiplication ($PDP^T$)

We assemble the matrices $P$, $D$, and $P^T$ using the given structural components:

$$P = \begin{bmatrix} \frac{1}{\sqrt{2}} & -\frac{1}{\sqrt{2}} \\ \frac{1}{\sqrt{2}} & \frac{1}{\sqrt{2}} \end{bmatrix}, \quad D = \begin{bmatrix} 3 & 0 \\ 0 & 1 \end{bmatrix}, \quad P^T = \begin{bmatrix} \frac{1}{\sqrt{2}} & \frac{1}{\sqrt{2}} \\ -\frac{1}{\sqrt{2}} & \frac{1}{\sqrt{2}} \end{bmatrix}$$

### Step-by-Step Multiplication:

1. **Multiply the first two matrices ($PD$):**

$$PD = \begin{bmatrix} \frac{1}{\sqrt{2}} & -\frac{1}{\sqrt{2}} \\ \frac{1}{\sqrt{2}} & \frac{1}{\sqrt{2}} \end{bmatrix} \begin{bmatrix} 3 & 0 \\ 0 & 1 \end{bmatrix} = \begin{bmatrix} \frac{3}{\sqrt{2}} & -\frac{1}{\sqrt{2}} \\ \frac{3}{\sqrt{2}} & \frac{1}{\sqrt{2}} \end{bmatrix}$$


2. **Multiply the result by the final matrix ($(PD) \cdot P^T$):**

$$A = \begin{bmatrix} \frac{3}{\sqrt{2}} & -\frac{1}{\sqrt{2}} \\ \frac{3}{\sqrt{2}} & \frac{1}{\sqrt{2}} \end{bmatrix} \begin{bmatrix} \frac{1}{\sqrt{2}} & \frac{1}{\sqrt{2}} \\ -\frac{1}{\sqrt{2}} & \frac{1}{\sqrt{2}} \end{bmatrix}$$


$$A = \begin{bmatrix} \left(\frac{3}{2} + \frac{1}{2}\right) & \left(\frac{3}{2} - \frac{1}{2}\right) \\ \left(\frac{3}{2} - \frac{1}{2}\right) & \left(\frac{3}{2} + \frac{1}{2}\right) \end{bmatrix} = \begin{bmatrix} 2 & 1 \\ 1 & 2 \end{bmatrix}$$



---

## 3. Approach 2: Verification via Sum of Rank-1 Projections

We split the matrix expansion explicitly into independent geometric channels:

$$A = \lambda_1 v_1 v_1^T + \lambda_2 v_2 v_2^T$$

### Step-by-Step Outer Product Computations:

1. **Calculate the first projection component matrix ($\lambda_1 v_1 v_1^T$):**
First, evaluate the outer product of the column vector and the row vector:

$$v_1 v_1^T = \begin{bmatrix} \frac{1}{\sqrt{2}} \\ \frac{1}{\sqrt{2}} \end{bmatrix} \begin{bmatrix} \frac{1}{\sqrt{2}} & \frac{1}{\sqrt{2}} \end{bmatrix} = \begin{bmatrix} \frac{1}{2} & \frac{1}{2} \\ \frac{1}{2} & \frac{1}{2} \end{bmatrix}$$


Now, scale this rank-1 matrix by its corresponding eigenvalue ($\lambda_1 = 3$):

$$\lambda_1 v_1 v_1^T = 3 \begin{bmatrix} \frac{1}{2} & \frac{1}{2} \\ \frac{1}{2} & \frac{1}{2} \end{bmatrix} = \begin{bmatrix} \frac{3}{2} & \frac{3}{2} \\ \frac{3}{2} & \frac{3}{2} \end{bmatrix} \quad \text{(Rank-1 Matrix)}$$


2. **Calculate the second projection component matrix ($\lambda_2 v_2 v_2^T$):**
Evaluate the outer product of the second column vector and row vector:

$$v_2 v_2^T = \begin{bmatrix} -\frac{1}{\sqrt{2}} \\ \frac{1}{\sqrt{2}} \end{bmatrix} \begin{bmatrix} -\frac{1}{\sqrt{2}} & \frac{1}{\sqrt{2}} \end{bmatrix} = \begin{bmatrix} \frac{1}{2} & -\frac{1}{2} \\ -\frac{1}{2} & \frac{1}{2} \end{bmatrix}$$


Scale this rank-1 matrix by its corresponding eigenvalue ($\lambda_2 = 1$):

$$\lambda_2 v_2 v_2^T = 1 \begin{bmatrix} \frac{1}{2} & -\frac{1}{2} \\ -\frac{1}{2} & \frac{1}{2} \end{bmatrix} = \begin{bmatrix} \frac{1}{2} & -\frac{1}{2} \\ -\frac{1}{2} & \frac{1}{2} \end{bmatrix} \quad \text{(Rank-1 Matrix)}$$


3. **Sum the two independent spatial channels together:**

$$A = \begin{bmatrix} \frac{3}{2} & \frac{3}{2} \\ \frac{3}{2} & \frac{3}{2} \end{bmatrix} + \begin{bmatrix} \frac{1}{2} & -\frac{1}{2} \\ -\frac{1}{2} & \frac{1}{2} \end{bmatrix} = \begin{bmatrix} \left(\frac{3}{2} + \frac{1}{2}\right) & \left(\frac{3}{2} - \frac{1}{2}\right) \\ \left(\frac{3}{2} - \frac{1}{2}\right) & \left(\frac{3}{2} + \frac{1}{2}\right) \end{bmatrix} = \begin{bmatrix} 2 & 1 \\ 1 & 2 \end{bmatrix}$$



---

## 4. Key Takeaways for Notes

* **Equivalence:** Both expressions evaluate to the exact same matrix $A = \begin{bmatrix} 2 & 1 \\ 1 & 2 \end{bmatrix}$.
* **Rank-1 Building Blocks:** The individual outer products ($v_i v_i^T$) form square, symmetric matrices of rank 1. They represent an orthogonal projection onto a 1-dimensional line inside the space.
* **Spectral Synthesis:** A symmetric matrix can always be viewed as a weighted combination of these simple projection filters, where the weights are exactly the eigenvalues.