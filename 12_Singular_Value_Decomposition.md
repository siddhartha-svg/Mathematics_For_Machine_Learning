---

# Lecture 12: Matrix Decompositions

This note covers how we break down matrices into simpler, interpretable parts depending on whether they are square/symmetric or rectangular.

---

## 1. Symmetric Matrices: Orthogonal Diagonalization

When a matrix $A$ is a **square, symmetric matrix** (meaning it is an $n \times n$ matrix where $A = A^T$), it can be diagonalized using an orthogonal matrix.

### The Formula

$$A = P D P^T$$

Where:

* **$A$**: The original $n \times n$ symmetric matrix.
* **$P$**: An $n \times n$ **orthogonal matrix** whose columns are the orthonormal eigenvectors of $A$. (Note: Because it is orthogonal, $P^{-1} = P^T$).
* **$D$**: An $n \times n$ **diagonal matrix** containing the eigenvalues of $A$ along its main diagonal.

### 💡 Example

Let's look at a basic $2 \times 2$ symmetric matrix:

$$A = \begin{pmatrix} 2 & 1 \\ 1 & 2 \end{pmatrix}$$

Through eigenvalue calculation, we find:

* **Eigenvalues:** $\lambda_1 = 3, \lambda_2 = 1$
* **Orthonormal Eigenvectors:** $v_1 = \frac{1}{\sqrt{2}}\begin{pmatrix} 1 \\ 1 \end{pmatrix}, v_2 = \frac{1}{\sqrt{2}}\begin{pmatrix} -1 \\ 1 \end{pmatrix}$

Thus, its decomposition $A = P D P^T$ looks like:

$$A = \begin{pmatrix} \frac{1}{\sqrt{2}} & -\frac{1}{\sqrt{2}} \\ \frac{1}{\sqrt{2}} & \frac{1}{\sqrt{2}} \end{pmatrix} \begin{pmatrix} 3 & 0 \\ 0 & 1 \end{pmatrix} \begin{pmatrix} \frac{1}{\sqrt{2}} & \frac{1}{\sqrt{2}} \\ -\frac{1}{\sqrt{2}} & \frac{1}{\sqrt{2}} \end{pmatrix}$$

---

## 2. Rectangular Matrices: Singular Value Decomposition (SVD)

When a matrix $A$ is **rectangular** ($m \times n$ where $m \neq n$), standard diagonalization fails because the matrix isn't square. Instead, we use **Singular Value Decomposition (SVD)**.

### The Formula

$$A = U \Sigma V^T$$

Where:

* **$A$**: The original $m \times n$ matrix.
* **$U$**: An $m \times m$ orthogonal matrix containing the **left singular vectors** (eigenvectors of $A A^T$).
* **$\Sigma$**: An $m \times n$ diagonal matrix containing the **singular values** ($\sigma_i$) in descending order. These are the square roots of the non-zero eigenvalues of $A^T A$ or $A A^T$.
* **$V^T$**: The transpose of an $n \times n$ orthogonal matrix $V$ containing the **right singular vectors** (eigenvectors of $A^T A$).

### 💡 Example

Consider a $3 \times 2$ rectangular matrix:

$$A = \begin{pmatrix} 1 & 1 \\ 0 & 1 \\ 1 & 0 \end{pmatrix}$$

Its SVD decomposes it into three distinct matrices:

$$A = \underbrace{\begin{pmatrix} \frac{2}{\sqrt{6}} & 0 & \frac{1}{\sqrt{3}} \ \frac{1}{\sqrt{6}} & -\frac{1}{\sqrt{2}} & -\frac{1}{\sqrt{3}} \ \frac{1}{\sqrt{6}} & \frac{1}{\sqrt{2}} & -\frac{1}{\sqrt{3}} \end{pmatrix}}*{U (3 \times 3)} \underbrace{\begin{pmatrix} \sqrt{3} & 0 \ 0 & 1 \ 0 & 0 \end{pmatrix}}*{\Sigma (3 \times 2)} \underbrace{\begin{pmatrix} \frac{1}{\sqrt{2}} & \frac{1}{\sqrt{2}} \ \frac{1}{\sqrt{2}} & -\frac{1}{\sqrt{2}} \end{pmatrix}}_{V^T (2 \times 2)}$

---

## Quick Reference Summary

| Property | Symmetric Matrix Diagonalization | Singular Value Decomposition (SVD) |
| --- | --- | --- |
| **Matrix Dimension** | Square ($n \times n$) | Rectangular or Square ($m \times n$) |
| **Condition** | Must be symmetric ($A = A^T$) | Works on **any** matrix |
| **Decomposition** | $A = P D P^T$ | $A = U \Sigma V^T$ |
| **Core Values** | Eigenvalues ($\lambda$) | Singular Values ($\sigma = \sqrt{\lambda}$) |

---

# Linear Algebra Notes: Singular Values

This section introduces **Singular Values**, which generalize the concept of eigenvalues to non-square or general rectangular matrices. They form the core mathematical foundation for Singular Value Decomposition (SVD) and Principal Component Analysis (PCA).

---

## 1. Core Definition

Let $A \in \mathbb{R}^{m \times n}$ be an $m \times n$ real matrix (which can be rectangular or square).

If we construct the matrix product $A^T A$, the resulting matrix has the following guaranteed structural properties:

* It is a square $n \times n$ matrix.
* It is **symmetric** ($(A^T A)^T = A^T A$).
* It is **Positive Semi-Definite (PSD)**, meaning its eigenvalues are always real and non-negative.

Let the eigenvalues of $A^T A$ be arranged in descending order:

$$\lambda_1 \ge \lambda_2 \ge \dots \ge \lambda_n \ge 0$$

The **singular values** of matrix $A$, denoted by $\sigma_i$ (sigma), are defined as the square roots of these eigenvalues:

$$\sigma_i = \sqrt{\lambda_i} \quad \text{for } i = 1, 2, \dots, n$$

Consequently, the singular values are also ordered hierarchically and are strictly non-negative:

$$\sigma_1 \ge \sigma_2 \ge \dots \ge \sigma_n \ge 0$$

---

## 2. Geometric Interpretation (In Simple Terms)

While eigenvalues tell you how much a matrix stretches vectors along its *eigenvector* directions, singular values tell you the absolute **maximum stretching power** of a matrix along mutually perpendicular axes.

Geometrically, if you apply a linear transformation $A$ to a unit circle/sphere:

* The circle deforms into an ellipse/ellipsoid.
* The lengths of the principal semi-axes of this new ellipse are exactly equal to the **singular values** ($\sigma_1, \sigma_2, \dots$).
* $\sigma_1$ represents the maximum elongation factor achieved by the transformation.

---

## 3. Walkthrough Example

Let's calculate the singular values for the following rectangular $2 \times 3$ matrix $A$:

$$A = \begin{pmatrix} 1 & 1 & 0 \\ 0 & 1 & 1 \end{pmatrix}$$

### Step 1: Compute the symmetric matrix $A^T A$

Multiply the transpose $A^T$ (size $3 \times 2$) by $A$ (size $2 \times 3$):

$$A^T A = \begin{pmatrix} 1 & 0 \\ 1 & 1 \\ 0 & 1 \end{pmatrix} \begin{pmatrix} 1 & 1 & 0 \\ 0 & 1 & 1 \end{pmatrix} = \begin{pmatrix} 1 & 1 & 0 \\ 1 & 2 & 1 \\ 0 & 1 & 1 \end{pmatrix}$$

Notice that the resulting matrix is a square $3 \times 3$ symmetric matrix.

### Step 2: Find the eigenvalues ($\lambda$) of $A^T A$

Set up the characteristic equation $\det(A^T A - \lambda I) = 0$:

$$\begin{vmatrix} 1-\lambda & 1 & 0 \\ 1 & 2-\lambda & 1 \\ 0 & 1 & 1-\lambda \end{vmatrix} = 0$$

Expanding this determinant yields the polynomial:


$$(1-\lambda) \left[ (2-\lambda)(1-\lambda) - 1 \right] - 1 \left[ 1(1-\lambda) - 0 \right] = 0$$

$$(1-\lambda)(\lambda^2 - 3\lambda + 1) - (1-\lambda) = 0$$

$$(1-\lambda)(\lambda^2 - 3\lambda + 1 - 1) = 0$$

$$(1-\lambda)(\lambda^2 - 3\lambda) = 0$$

$$\lambda(1-\lambda)(\lambda - 3) = 0$$

Sorting the roots (eigenvalues) in descending order:

* $\lambda_1 = 3$
* $\lambda_2 = 1$
* $\lambda_3 = 0$

### Step 3: Compute the Singular Values ($\sigma$)

Take the positive square root of each calculated eigenvalue:

* $\sigma_1 = \sqrt{\lambda_1} = \mathbf{\sqrt{3}} \approx 1.732$
* $\sigma_2 = \sqrt{\lambda_2} = \sqrt{1} = \mathbf{1}$
* $\sigma_3 = \sqrt{\lambda_3} = \sqrt{0} = \mathbf{0}$

### Summary of Results:

The singular values for our matrix are $\{\sqrt{3}, 1, 0\}$.



# Linear Algebra Notes: Singular Value Decomposition (SVD)

Singular Value Decomposition (SVD) is a powerful matrix factorization technique that decomposes any arbitrary real matrix into three constituent matrices containing essential geometric and structural data.

---

## 1. Core Definition

Let $A$ be a general $m \times n$ matrix with a mathematical rank denoted by $\text{rank}(A) = r$. The **Singular Value Decomposition** of $A$ factorizes the matrix as follows:

$$A = U \Sigma V^T$$

### Detailed Matrix Components:

* **$U$ (Left Singular Vectors):**
An $m \times m$ **orthogonal matrix** ($U^T U = UU^T = I$). The columns of $U$ are eigenvectors of the symmetric matrix product $AA^T$.
* **$V$ (Right Singular Vectors):**
An $n \times n$ **orthogonal matrix** ($V^T V = VV^T = I$). The columns of $V$ are eigenvectors of the symmetric matrix product $A^T A$.
* **$\Sigma$ (Singular Value Matrix):**
An $m \times n$ rectangular diagonal matrix. The diagonal elements along the first $r$ rows contain the sorted, strictly positive **singular values** of $A$ ($\sigma_1 \ge \sigma_2 \ge \dots \ge \sigma_r > 0$). The remainder of the matrix cells outside this primary rank block are completely filled with zeros.

---

## 2. Structural Breakdown of $\Sigma$

Depending on the size constraints of $A$, the rectangular diagonal matrix $\Sigma$ takes the following block layout structure:

$$\Sigma = \begin{pmatrix} 
\sigma_1 & 0 & \dots & 0 & \dots & 0 \\ 
0 & \sigma_2 & \dots & 0 & \dots & 0 \\ 
\vdots & \vdots & \ddots & \vdots & \dots & \vdots \\ 
0 & 0 & \dots & \sigma_r & \dots & 0 \\ 
\vdots & \vdots & \dots & \vdots & \ddots & \vdots \\
0 & 0 & \dots & 0 & \dots & 0 
\end{pmatrix}$$

Where the number of non-zero singular values matches the rank ($r$) of matrix $A$.


---

## 1. Matrix Dimensional Layout ($m < n$)

When the matrix $A$ is a "wide" rectangular matrix where the number of rows is strictly less than the number of columns ($m < n$), the decomposition $A = U \Sigma V^T$ takes the following structural dimensions:

$$A_{m \times n} = U_{m \times m} \Sigma_{m \times n} V^T_{n \times n}$$

### Visual Structure of the Components

* **$A$** ($m \times n$): The input rectangular matrix.
* **$U$** ($m \times m$): A square orthogonal matrix.
* **$\Sigma$** ($m \times n$): A rectangular diagonal matrix filled with singular values ($\sigma_i$) along its main diagonal, padded with columns of zeros on the right side because $m < n$:

$$\Sigma = \begin{bmatrix} 
\sigma_1 & 0 & \cdots & 0 \\ 
0 & \sigma_2 & \cdots & 0 \\ 
0 & 0 & \ddots & 0 \\ 
0 & 0 & 0 & \sigma_r \\
0 & 0 & 0 & 0 
\end{bmatrix}_{m \times n}$$

* **$V^T$** ($n \times n$): A square orthogonal matrix (transposed).

---

## 2. Mathematical Definition of Matrices $U$ and $V$

The component matrices $U$ and $V$ are constructed using the eigenvalues and eigenvectors of the symmetric matrix pairs $A^T A$ and $A A^T$.

### The Right Singular Vectors ($V$)

* The columns of $V$ are the **orthonormal eigenvectors** $v_1, v_2, \dots, v_n$ of the square symmetric matrix $A^T A$.
* They satisfy the standard eigen-relationship:

$$A^T A v_i = \sigma_i^2 v_i$$



### The Left Singular Vectors ($U$)

* Similarly, the columns of $U$ are the **orthonormal eigenvectors** $u_1, u_2, \dots, u_m$ of the square symmetric matrix $A A^T$.
* They satisfy the relationship:

$$A A^T u_i = \sigma_i^2 u_i$$



> 📌 **Note:** The singular values $\sigma_i$ are the positive square roots of the non-zero eigenvalues ($\lambda_i$) shared by both $A^T A$ and $A A^T$, sorted in descending order:
> 
> $$\sigma_i = \sqrt{\lambda_i}$$
> 
> 

---


# Linear Algebra Notes: Deriving the $V$ Matrix in SVD

This section breaks down how to construct the right singular vector matrix $V$ in Singular Value Decomposition (SVD) using the eigenvectors of the symmetric matrix product $A^T A$.

---

## 1. Mathematical Framework & Properties

Let $A$ be a general $m \times n$ real matrix. The matrix product $A^T A$ forms an $n \times n$ square, symmetric, Positive Semi-Definite (PSD) matrix. Because it is symmetric, the **Spectral Theorem** guarantees that it can be orthogonally diagonalized.

### Core Properties:

* **Eigenpair Equation:** We can find $n$ eigenvectors $\{v_1, v_2, \dots, v_n\}$ for $A^T A$ such that:

$$A^T A v_i = \sigma_i^2 v_i$$



where $\sigma_i^2 = \lambda_i$ represents the eigenvalues of $A^T A$, and $\sigma_i$ are the singular values of $A$.
* **Pairwise Orthogonality:** These eigenvectors $v_i$ are naturally perpendicular to each other when they correspond to distinct eigenvalues. If there are repeated eigenvalues, we can explicitly choose an orthogonal basis for that eigenspace.
* **Orthonormal Set:** By dividing each vector by its length (normalizing them), the collection $\{v_1, v_2, \dots, v_n\}$ forms an **orthonormal set**, meaning:

$$v_i^T v_j = \begin{cases} 1 & \text{if } i = j \\ 0 & \text{if } i \neq j \end{cases}$$



---

## 2. Constructing the Matrix $V$

The $n \times n$ orthogonal matrix $V$ used in the SVD factorization ($A = U\Sigma V^T$) is formed by placing these normalized eigenvectors side-by-side as its columns:

$$V = \begin{bmatrix} \vert & \vert & & \vert \\ v_1 & v_2 & \dots & v_n \\ \vert & \vert & & \vert \end{bmatrix}_{n \times n}$$

Because its columns are orthonormal, $V$ is an **orthogonal matrix**, satisfying the property:


$$V^T V = V V^T = I$$

---

## 3. Walkthrough Verification Example

Let's look at a concrete example to make this crystal clear. Suppose we computed $A^T A$ for a matrix, resulting in:

$$A^T A = \begin{bmatrix} 2 & 1 \\ 1 & 2 \end{bmatrix}$$

### Step 1: Find the Eigenvalues ($\sigma_i^2$)

Set up the characteristic equation $\det(A^T A - \lambda I) = 0$:

$$\begin{vmatrix} 2-\lambda & 1 \\ 1 & 2-\lambda \end{vmatrix} = 0 \implies (2-\lambda)^2 - 1 = 0$$

$$\lambda^2 - 4\lambda + 3 = 0 \implies (\lambda - 3)(\lambda - 1) = 0$$

* $\lambda_1 = \sigma_1^2 = 3$
* $\lambda_2 = \sigma_2^2 = 1$

### Step 2: Find the Orthonormal Eigenvectors ($v_i$)

#### For $\lambda_1 = 3$:

$$(A^T A - 3I)v = 0 \implies \begin{bmatrix} -1 & 1 \\ 1 & -1 \end{bmatrix} \begin{bmatrix} x_1 \\ x_2 \end{bmatrix} = \begin{bmatrix} 0 \\ 0 \end{bmatrix} \implies x_1 = x_2$$


Choosing $x_1 = 1$ gives $\begin{bmatrix} 1 \\ 1 \end{bmatrix}$. Normalizing it to a unit length gives:


$$v_1 = \begin{bmatrix} \frac{1}{\sqrt{2}} \\ \frac{1}{\sqrt{2}} \end{bmatrix}$$

#### For $\lambda_2 = 1$:

$$(A^T A - 1I)v = 0 \implies \begin{bmatrix} 1 & 1 \\ 1 & 1 \end{bmatrix} \begin{bmatrix} x_1 \\ x_2 \end{bmatrix} = \begin{bmatrix} 0 \\ 0 \end{bmatrix} \implies x_1 = -x_2$$


Choosing $x_2 = 1$ gives $\begin{bmatrix} -1 \\ 1 \end{bmatrix}$. Normalizing it to a unit length gives:


$$v_2 = \begin{bmatrix} -\frac{1}{\sqrt{2}} \\ \frac{1}{\sqrt{2}} \end{bmatrix}$$

### Step 3: Assemble Matrix $V$

Stack $v_1$ and $v_2$ column-wise to build $V$:

$$V = \begin{bmatrix} \frac{1}{\sqrt{2}} & -\frac{1}{\sqrt{2}} \\ \frac{1}{\sqrt{2}} & \frac{1}{\sqrt{2}} \end{bmatrix}$$

### Quick Orthogonality Double-Check:

Multiply $V^T$ by $V$ to make sure it yields the identity matrix:


$$V^T V = \begin{bmatrix} \frac{1}{\sqrt{2}} & \frac{1}{\sqrt{2}} \\ -\frac{1}{\sqrt{2}} & \frac{1}{\sqrt{2}} \end{bmatrix} \begin{bmatrix} \frac{1}{\sqrt{2}} & -\frac{1}{\sqrt{2}} \\ \frac{1}{\sqrt{2}} & \frac{1}{\sqrt{2}} \end{bmatrix} = \begin{bmatrix} (\frac{1}{2}+\frac{1}{2}) & (-\frac{1}{2}+\frac{1}{2}) \\ (-\frac{1}{2}+\frac{1}{2}) & (\frac{1}{2}+\frac{1}{2}) \end{bmatrix} = \begin{bmatrix} 1 & 0 \\ 0 & 1 \end{bmatrix} = I$$

The check passes perfectly!



# Linear Algebra Notes: Deriving the $U$ Matrix in SVD

This section outlines how to construct the left singular vector matrix $U$ in Singular Value Decomposition (SVD) using the eigenvectors of the symmetric matrix product $AA^T$.

---

## 1. Mathematical Framework & Properties

Let $A$ be a general $m \times n$ real matrix. The matrix product $AA^T$ forms an $m \times m$ square, symmetric, Positive Semi-Definite (PSD) matrix. Because it is symmetric, it is guaranteed to be orthogonally diagonalizable according to the **Spectral Theorem**.

### Core Properties:

* **Eigenpair Equation:** We can compute $m$ eigenvectors $\{u_1, u_2, \dots, u_m\}$ for $AA^T$ such that:

$$AA^T u_i = \sigma_i^2 u_i \quad \text{for } i = 1, 2, \dots, m$$



where $\sigma_i^2 = \lambda_i$ represents the eigenvalues of $AA^T$, and $\sigma_i$ are the singular values of $A$.
* **Pairwise Orthogonality:** These eigenvectors $u_i$ are perpendicular to each other when they correspond to distinct eigenvalues.
* **Orthonormal Set:** By normalizing each vector to have a length of 1, the collection $\{u_1, u_2, \dots, u_m\}$ forms an **orthonormal set**, meaning:

$$u_i^T u_j = \begin{cases} 1 & \text{if } i = j \\ 0 & \text{if } i \neq j \end{cases}$$



---

## 2. Constructing the Matrix $U$

The $m \times m$ orthogonal matrix $U$ used in the SVD factorization ($A = U\Sigma V^T$) is constructed by placing these normalized eigenvectors side-by-side as its columns:

$$U = \begin{bmatrix} \vert & \vert & & \vert \\ u_1 & u_2 & \dots & u_m \\ \vert & \vert & & \vert \end{bmatrix}_{m \times m}$$

Because its columns are orthonormal, $U$ is an **orthogonal matrix**, which satisfies:


$$U^T U = U U^T = I$$

---

## 3. Walkthrough Verification Example

Let's look at a concrete example to clarify how this works. Suppose we have a $2 \times 3$ matrix $A$, and we compute the $2 \times 2$ product $AA^T$:

$$AA^T = \begin{bmatrix} 2 & 1 \\ 1 & 2 \end{bmatrix}$$

### Step 1: Find the Eigenvalues ($\sigma_i^2$)

Set up the characteristic equation $\det(AA^T - \lambda I) = 0$:

$$\begin{vmatrix} 2-\lambda & 1 \\ 1 & 2-\lambda \end{vmatrix} = 0 \implies (2-\lambda)^2 - 1 = 0$$

$$\lambda^2 - 4\lambda + 3 = 0 \implies (\lambda - 3)(\lambda - 1) = 0$$

* $\lambda_1 = \sigma_1^2 = 3$
* $\lambda_2 = \sigma_2^2 = 1$

### Step 2: Find the Orthonormal Eigenvectors ($u_i$)

#### For $\lambda_1 = 3$:

$$(AA^T - 3I)u = 0 \implies \begin{bmatrix} -1 & 1 \\ 1 & -1 \end{bmatrix} \begin{bmatrix} x_1 \\ x_2 \end{bmatrix} = \begin{bmatrix} 0 \\ 0 \end{bmatrix} \implies x_1 = x_2$$


Choosing $x_1 = 1$ gives $\begin{bmatrix} 1 \\ 1 \end{bmatrix}$. Normalizing it to a unit length yields:


$$u_1 = \begin{bmatrix} \frac{1}{\sqrt{2}} \\ \frac{1}{\sqrt{2}} \end{bmatrix}$$

#### For $\lambda_2 = 1$:

$$(AA^T - 1I)u = 0 \implies \begin{bmatrix} 1 & 1 \\ 1 & 1 \end{bmatrix} \begin{bmatrix} x_1 \\ x_2 \end{bmatrix} = \begin{bmatrix} 0 \\ 0 \end{bmatrix} \implies x_1 = -x_2$$


Choosing $x_2 = 1$ gives $\begin{bmatrix} -1 \\ 1 \end{bmatrix}$. Normalizing it to a unit length yields:


$$u_2 = \begin{bmatrix} -\frac{1}{\sqrt{2}} \\ \frac{1}{\sqrt{2}} \end{bmatrix}$$

### Step 3: Assemble Matrix $U$

Place $u_1$ and $u_2$ column-wise to build $U$:

$$U = \begin{bmatrix} \frac{1}{\sqrt{2}} & -\frac{1}{\sqrt{2}} \\ \frac{1}{\sqrt{2}} & \frac{1}{\sqrt{2}} \end{bmatrix}$$

### Quick Orthogonality Double-Check:

Multiply $U^T$ by $U$ to ensure it results in the identity matrix:


$$U^T U = \begin{bmatrix} \frac{1}{\sqrt{2}} & \frac{1}{\sqrt{2}} \\ -\frac{1}{\sqrt{2}} & \frac{1}{\sqrt{2}} \end{bmatrix} \begin{bmatrix} \frac{1}{\sqrt{2}} & -\frac{1}{\sqrt{2}} \\ \frac{1}{\sqrt{2}} & \frac{1}{\sqrt{2}} \end{bmatrix} = \begin{bmatrix} (\frac{1}{2}+\frac{1}{2}) & (-\frac{1}{2}+\frac{1}{2}) \\ (-\frac{1}{2}+\frac{1}{2}) & (\frac{1}{2}+\frac{1}{2}) \end{bmatrix} = \begin{bmatrix} 1 & 0 \\ 0 & 1 \end{bmatrix} = I$$

The check passes perfectly!

# Linear Algebra Notes: Deriving the $\Sigma$ Matrix in SVD

This section details how to construct the rectangular diagonal singular value matrix $\Sigma$ (Sigma) in Singular Value Decomposition (SVD), based on a matrix's dimensions and its rank.

---

## 1. Mathematical Framework & Rules

Let $A$ be a general $m \times n$ matrix with mathematical rank $\text{rank}(A) = r$. The rank cannot exceed the dimensions of the matrix, meaning:

$$r \le \min(m, n)$$

The matrix $\Sigma$ is an **$m \times n$ rectangular matrix** structured as follows:

* The singular values are arranged on its main diagonal in descending order: $\sigma_1 \ge \sigma_2 \ge \dots \ge \sigma_r > 0$.
* The number of strictly positive singular values matches the rank $r$. All remaining elements are zero ($\sigma_{r+1} = \sigma_{r+2} = \dots = 0$).

---

## 2. Structural Cases Based on Dimensions

### Case A: Tall Matrices ($m \ge n$)

When there are more rows than columns, the matrix $\Sigma$ is tall. The top $n \times n$ block contains the diagonal singular values, and the bottom rows are completely filled with zeros.

$$\Sigma = \begin{bmatrix} 
\sigma_1 & 0 & \dots & 0 \\ 
0 & \sigma_2 & \dots & 0 \\ 
\vdots & \vdots & \ddots & \vdots \\ 
0 & 0 & \dots & \sigma_r \\ 
\hline
0 & 0 & \dots & 0 \\ 
\vdots & \vdots & \ddots & \vdots \\ 
0 & 0 & \dots & 0 
\end{bmatrix}_{m \times n}$$

#### 📝 Example: $5 \times 2$ Matrix with Rank 1

Let $A$ be a $5 \times 2$ matrix ($m=5, n=2$) with a rank of $r=1$.

* Since $r=1$, we have $\sigma_1 > 0$ and $\sigma_2 = 0$.
* $\Sigma$ must match the dimensions of $A$ ($5 \times 2$).

$$\Sigma = \begin{bmatrix} 
\sigma_1 & 0 \\ 
0 & 0 \\ 
0 & 0 \\ 
0 & 0 \\ 
0 & 0 
\end{bmatrix}_{5 \times 2}$$

---

### Case B: Wide Matrices ($m \le n$)

When there are more columns than rows, the matrix $\Sigma$ is wide. The leftmost $m \times m$ block houses the diagonal singular values, and the trailing columns to the right are completely filled with zeros.

$$\Sigma = \left[ \begin{array}{cccc|ccc} 
\sigma_1 & 0 & \dots & 0 & 0 & \dots & 0 \\ 
0 & \sigma_2 & \dots & 0 & 0 & \dots & 0 \\ 
\vdots & \vdots & \ddots & \vdots & \vdots & \ddots & \vdots \\ 
0 & 0 & \dots & \sigma_m & 0 & \dots & 0 
\end{array} \right]_{m \times n}$$

#### 📝 Example: $3 \times 5$ Matrix with Rank 2

Let $A$ be a $3 \times 5$ matrix ($m=3, n=5$) with a rank of $r=2$.

* Since $r=2$, we have $\sigma_1 \ge \sigma_2 > 0$.
* The remaining diagonal position must be zero: $\sigma_3 = 0$.
* $\Sigma$ must match the dimensions of $A$ ($3 \times 5$).

$$\Sigma = \begin{bmatrix} 
\sigma_1 & 0 & 0 & 0 & 0 \\ 
0 & \sigma_2 & 0 & 0 & 0 \\ 
0 & 0 & 0 & 0 & 0 
\end{bmatrix}_{3 \times 5}$$

---

## 3. Visualizing SVD Matrix Layouts

The block-geometry of SVD alterations shifts dynamically depending on whether your linear mapping works with a tall or wide layout:

```text
 Tall Layout (m > n):                  Wide Layout (m < n):
 
   [   A   ] = [ U ] [ Σ ] [ Vᵀ ]        [   A   ] = [ U ] [   Σ   ] [ Vᵀ ]
   |       |   |   | |   | |    |        |       |   |   | |       | |    |
   |       |   |   | | o | |____|        |_______|   |___| | o  o  | |____|
   |       |   |   | |   |                             | o  o  | 
   |_______|   |___| |___|                             |_______|
                     | 0 |
                     |___|

```

> **Key Rule of Thumb:** Always look at the dimensions of your original matrix $A$. Your singular value matrix $\Sigma$ **must** duplicate those exact row and column dimensions ($m \times n$), acting as a structural placeholder for the system transformation scales.

# Linear Algebra Notes: Full SVD Calculation Walkthroughs

This section provides comprehensive, step-by-step solutions for calculating the **Singular Value Decomposition (SVD)** ($A = U\Sigma V^T$) of both square and rectangular matrices using analytical methods.

---

## 💡 Core Calculation Framework

To find the SVD of any real $m \times n$ matrix $A$:

1. **Find $V$ and $\Sigma$:** Compute the $n \times n$ symmetric product $A^TA$. Find its eigenvalues $\lambda_i$ and corresponding normalized eigenvectors $v_i$.
* The singular values are $\sigma_i = \sqrt{\lambda_i}$ arranged in descending order to form the $m \times n$ matrix $\Sigma$.
* The normalized eigenvectors $v_i$ form the columns of the $n \times n$ orthogonal matrix $V$.


2. **Find $U$:** For non-zero singular values ($\sigma_i \neq 0$), compute the columns of the $m \times m$ orthogonal matrix $U$ using the transformation property:

$$u_i = \frac{Av_i}{\sigma_i}$$



*(If $A^TA$ yields any zero singular values, complete the basis for $U$ by finding an orthonormal vector orthogonal to the existing columns using the nullspace of $A^T$ or Gram-Schmidt).*

---

## Example 1: SVD of a $3 \times 3$ Matrix

**Problem:** Find the Singular Value Decomposition of the matrix:

$$A = \begin{bmatrix} 0 & 1 & 1 \\ \sqrt{2} & 2 & 0 \\ 0 & 1 & 1 \end{bmatrix}$$

### Step 1: Compute $AA^T$ (to find eigenvalues and $U$)

Alternatively, we can find $U$ first by computing $AA^T$. Let's perform the matrix multiplication:

$$AA^T = \begin{bmatrix} 0 & 1 & 1 \\ \sqrt{2} & 2 & 0 \\ 0 & 1 & 1 \end{bmatrix} \begin{bmatrix} 0 & \sqrt{2} & 0 \\ 1 & 2 & 1 \\ 1 & 0 & 1 \end{bmatrix} = \begin{bmatrix} 2 & 2 & 2 \\ 2 & 6 & 2 \\ 2 & 2 & 2 \end{bmatrix}$$

### Step 2: Calculate Eigenvalues ($\lambda$) and Singular Values ($\sigma$)

Find the characteristic polynomial by setting $\det(AA^T - \lambda I) = 0$:

$$\begin{vmatrix} 2-\lambda & 2 & 2 \\ 2 & 6-\lambda & 2 \\ 2 & 2 & 2-\lambda \end{vmatrix} = 0 \implies \lambda_1 = 8, \quad \lambda_2 = 2, \quad \lambda_3 = 0$$

Take the square roots of the eigenvalues in descending order to construct $\Sigma$:

* $\sigma_1 = \sqrt{8} = 2\sqrt{2}$
* $\sigma_2 = \sqrt{2}$
* $\sigma_3 = 0$

$$\Sigma = \begin{bmatrix} 2\sqrt{2} & 0 & 0 \\ 0 & \sqrt{2} & 0 \\ 0 & 0 & 0 \end{bmatrix}$$

### Step 3: Compute Left Singular Vectors ($U$)

Find the normalized eigenvectors for $AA^T$ corresponding to each eigenvalue:

* **For $\lambda_1 = 8$:** Solving $(AA^T - 8I)u_1 = \mathbf{0}$ yields the unit vector:

$$u_1 = \begin{bmatrix} \frac{1}{\sqrt{6}} \\ \frac{2}{\sqrt{6}} \\ \frac{1}{\sqrt{6}} \end{bmatrix}$$


* **For $\lambda_2 = 2$:** Solving $(AA^T - 2I)u_2 = \mathbf{0}$ yields the unit vector:

$$u_2 = \begin{bmatrix} -\frac{1}{\sqrt{3}} \\ \frac{1}{\sqrt{3}} \\ -\frac{1}{\sqrt{3}} \end{bmatrix}$$


* **For $\lambda_3 = 0$:** Solving $(AA^T - 0I)u_3 = \mathbf{0}$ yields the unit vector:

$$u_3 = \begin{bmatrix} \frac{1}{\sqrt{2}} \\ 0 \\ -\frac{1}{\sqrt{2}} \end{bmatrix}$$



Assembling the columns gives the orthogonal matrix $U$:

$$U = \begin{bmatrix} \frac{1}{\sqrt{6}} & -\frac{1}{\sqrt{3}} & \frac{1}{\sqrt{2}} \\ \frac{2}{\sqrt{6}} & \frac{1}{\sqrt{3}} & 0 \\ \frac{1}{\sqrt{6}} & -\frac{1}{\sqrt{3}} & -\frac{1}{\sqrt{2}} \end{bmatrix}$$

### Step 4: Compute Right Singular Vectors ($V$)

Following a similar verification for $A^TA$, the normalized unit columns assemble into $V$:

$$V = \begin{bmatrix} \frac{1}{\sqrt{6}} & \frac{1}{\sqrt{3}} & \frac{1}{\sqrt{2}} \\ \frac{3}{\sqrt{12}} & 0 & -\frac{1}{2} \\ \frac{1}{\sqrt{12}} & -\frac{2}{\sqrt{6}} & \frac{1}{2} \end{bmatrix}$$

---

## Example 2: SVD of a Rectangular $2 \times 3$ Matrix

**Problem:** Find the Singular Value Decomposition of the wide matrix:

$$A = \begin{bmatrix} 4 & 11 & 14 \\ 8 & 7 & -2 \end{bmatrix}$$

### Step 1: Compute the $3 \times 3$ Matrix Product $A^TA$

Multiply the transpose $A^T$ (size $3 \times 2$) by $A$ (size $2 \times 3$):

$$A^TA = \begin{bmatrix} 4 & 8 \\ 11 & 7 \\ 14 & -2 \end{bmatrix} \begin{bmatrix} 4 & 11 & 14 \\ 8 & 7 & -2 \end{bmatrix} = \begin{bmatrix} 80 & 100 & 40 \\ 100 & 170 & 140 \\ 40 & 140 & 200 \end{bmatrix}$$

### Step 2: Compute Eigenvalues and Construct $\Sigma$

Solving the characteristic equation $\det(A^TA - \lambda I) = 0$ for this $3 \times 3$ matrix yields:

$$\lambda_1 = 360, \quad \lambda_2 = 90, \quad \lambda_3 = 0$$

Take the square roots of the positive values to find the singular values:

* $\sigma_1 = \sqrt{360} = 6\sqrt{10}$
* $\sigma_2 = \sqrt{90} = 3\sqrt{10}$

Because $A$ is a $2 \times 3$ matrix, $\Sigma$ **must** also be a $2 \times 3$ matrix. Using an array line to isolate the wide padding zeros:

$$\Sigma = \left[ \begin{array}{cc|c} 6\sqrt{10} & 0 & 0 \\ 0 & 3\sqrt{10} & 0 \end{array} \right]$$

### Step 3: Compute Right Singular Vectors ($V$)

Find the normalized eigenvectors of $A^TA$ for each eigenvalue:

* **For $\lambda_1 = 360$:** Gives the unit column vector $v_1 = \begin{bmatrix} \frac{1}{3} & \frac{2}{3} & \frac{2}{3} \end{bmatrix}^T$
* **For $\lambda_2 = 90$:** Gives the unit column vector $v_2 = \begin{bmatrix} -\frac{2}{3} & -\frac{1}{3} & \frac{2}{3} \end{bmatrix}^T$
* **For $\lambda_3 = 0$:** Gives the unit column vector $v_3 = \begin{bmatrix} \frac{2}{3} & -\frac{2}{3} & \frac{1}{3} \end{bmatrix}^T$

Stacking these vectors column-by-column yields the $3 \times 3$ orthogonal matrix $V$:

$$V = \begin{bmatrix} 1/3 & -2/3 & 2/3 \\ 2/3 & -1/3 & -2/3 \\ 2/3 & 2/3 & 1/3 \end{bmatrix}$$

### Step 4: Compute Left Singular Vectors ($U$)

Since $A$ has only 2 rows, $U$ must be a $2 \times 2$ matrix. We compute its columns directly using the non-zero singular values from the relation $u_i = \frac{Av_i}{\sigma_i}$:

#### 1. Calculate $u_1$:

$$Av_1 = \begin{bmatrix} 4 & 11 & 14 \\ 8 & 7 & -2 \end{bmatrix} \begin{bmatrix} 1/3 \\ 2/3 \\ 2/3 \end{bmatrix} = \begin{bmatrix} \frac{4}{3} + \frac{22}{3} + \frac{28}{3} \\ \frac{8}{3} + \frac{14}{3} - \frac{4}{3} \end{bmatrix} = \begin{bmatrix} 18 \\ 6 \end{bmatrix}$$

$$u_1 = \frac{1}{6\sqrt{10}} \begin{bmatrix} 18 \\ 6 \end{bmatrix} = \begin{bmatrix} \frac{3}{\sqrt{10}} \\ \frac{1}{\sqrt{10}} \end{bmatrix}$$

#### 2. Calculate $u_2$:

$$Av_2 = \begin{bmatrix} 4 & 11 & 14 \\ 8 & 7 & -2 \end{bmatrix} \begin{bmatrix} -2/3 \\ -1/3 \\ 2/3 \end{bmatrix} = \begin{bmatrix} -\frac{8}{3} - \frac{11}{3} + \frac{28}{3} \\ -\frac{16}{3} - \frac{7}{3} - \frac{4}{3} \end{bmatrix} = \begin{bmatrix} 3 \\ -9 \end{bmatrix}$$

$$u_2 = \frac{1}{3\sqrt{10}} \begin{bmatrix} 3 \\ -9 \end{bmatrix} = \begin{bmatrix} \frac{1}{\sqrt{10}} \\ -\frac{3}{\sqrt{10}} \end{bmatrix}$$

Assembling the columns yields the final $2 \times 2$ orthogonal matrix $U$:

$$U = \begin{bmatrix} \frac{3}{\sqrt{10}} & \frac{1}{\sqrt{10}} \\ \frac{1}{\sqrt{10}} & -\frac{3}{\sqrt{10}} \end{bmatrix}$$

### Final Decomposed Form Verification

The complete SVD factorization components are established:

$$A = \begin{bmatrix} \frac{3}{\sqrt{10}} & \frac{1}{\sqrt{10}} \\ \frac{1}{\sqrt{10}} & -\frac{3}{\sqrt{10}} \end{bmatrix} \left[ \begin{array}{cc|c} 6\sqrt{10} & 0 & 0 \\ 0 & 3\sqrt{10} & 0 \end{array} \right] \begin{bmatrix} 1/3 & 2/3 & 2/3 \\ -2/3 & -1/3 & 2/3 \\ 2/3 & -2/3 & 1/3 \end{bmatrix}$$

















































