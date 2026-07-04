# Lecture 10: Special Matrices and Properties — Quadratic Form

This section defines the algebraic and matrix structure of a **Quadratic Form** and demonstrates how to convert between polynomial expressions and their unique associated symmetric matrices.

---

## 1. Core Definition

Let $A \in \mathbb{R}^{n \times n}$ be a **symmetric matrix** (where $A = A^T$). The scalar-valued multivariate polynomial expression defined by:

$$q(X) = X^T AX$$

is called a **Quadratic Form**, where $X = (x_1, x_2, \dots, x_n)^T$ represents a column vector of variables.

---

## 2. Structural Matrix Formula ($3 \times 3$)

For a three-variable system where $X = \begin{bmatrix} x_1 & x_2 & x_3 \end{bmatrix}^T$, the expansion of $X^T AX$ using a symmetric matrix $A$ matches this layout:

$$q(X) = \begin{bmatrix} x_1 & x_2 & x_3 \end{bmatrix} \begin{pmatrix} a_{11} & a_{12} & a_{13} \\ a_{21} & a_{22} & a_{23} \\ a_{31} & a_{32} & a_{33} \end{pmatrix} \begin{bmatrix} x_1 \\ x_2 \\ x_3 \end{bmatrix}$$

$$q(X) = a_{11}x_1^2 + a_{22}x_2^2 + a_{33}x_3^2 + 2a_{12}x_1x_2 + 2a_{13}x_1x_3 + 2a_{23}x_2x_3$$

> ### 💡 Key Mapping Rule
> 
> 
> * **Main Diagonal Elements ($a_{ii}$):** The coefficients of the squared terms ($x_i^2$).
> * **Off-Diagonal Elements ($a_{ij} = a_{ji}$):** Exactly **half** of the corresponding cross-product term ($x_i x_j$) coefficient.
> 
> 

---

## 3. Practical Examples

### Example 1: Matrix-to-Polynomial Expansion

Given the symmetric matrix $A$ and variable vector $X = (x_1, x_2, x_3)^T$:

$$A = \begin{pmatrix} 1 & -1 & 2 \\ -1 & 3 & 1 \\ 2 & 1 & 4 \end{pmatrix}$$

#### Expansion:

$$q(X) = X^T AX$$

$$= (1)x_1^2 + (3)x_2^2 + (4)x_3^2 + 2(-1)x_1x_2 + 2(2)x_1x_3 + 2(1)x_2x_3$$

$$= x_1^2 + 3x_2^2 + 4x_3^2 - 2x_1x_2 + 4x_1x_3 + 2x_2x_3$$

---

### Example 2: Polynomial-to-Matrix Construction

Given the quadratic form expression:

$$q(X) = x_1^2 + 4x_1x_2 + x_2^2 + 2x_3^2 + 6x_2x_3$$

#### Steps to Build the Associated Symmetric Matrix $A$:

1. **Identify the squared terms for the main diagonal:**
* Coefficient of $x_1^2 = 1 \implies a_{11} = 1$
* Coefficient of $x_2^2 = 1 \implies a_{22} = 1$
* Coefficient of $x_3^2 = 2 \implies a_{33} = 2$


2. **Split the cross-product coefficients in half for the off-diagonals:**
* Coefficient of $x_1x_2 = 4 \implies a_{12} = a_{21} = \frac{4}{2} = 2$
* Coefficient of $x_2x_3 = 6 \implies a_{23} = a_{32} = \frac{6}{2} = 3$
* Coefficient of $x_1x_3 = 0 \implies a_{13} = a_{31} = \frac{0}{2} = 0$



#### Resulting Associated Matrix:

$$A = \begin{pmatrix} 1 & 2 & 0 \\ 2 & 1 & 3 \\ 0 & 3 & 2 \end{pmatrix}$$


# Linear Algebra Notes: Quadratic Forms and Symmetric Matrix Operations

This note documents the handwritten calculations detailing how to expand a matrix quadratic form into a polynomial and how to construct a unique symmetric matrix from a given quadratic polynomial expression.

---

## Example 1: Matrix to Polynomial Expansion

Given the quadratic form expressed in matrix notation:

$$q(X) = \begin{pmatrix} x_1 & x_2 & x_3 \end{pmatrix} \begin{pmatrix} \mathbf{1} & -1 & 2 \\ -1 & \mathbf{3} & 1 \\ 2 & 1 & \mathbf{4} \end{pmatrix} \begin{pmatrix} x_1 \\ x_2 \\ x_3 \end{pmatrix}$$

### Step-by-Step Expansion:

* **Squared Terms (Main Diagonal):** Gather the circled values from the diagonal:

$$(1)x_1^2 + (3)x_2^2 + (4)x_3^2$$


* **Cross-Product Terms (Off-Diagonal Pairs):** Double the unique off-diagonal values because $a_{ij} = a_{ji}$:
* For $x_1 x_2$: $2 \cdot (-1) = -2x_1x_2$
* For $x_1 x_3$: $2 \cdot (2) = 4x_1x_3$
* For $x_2 x_3$: $2 \cdot (1) = 2x_2x_3$



### Resulting Polynomial Expression:

$$q(X) = x_1^2 + 3x_2^2 + 4x_3^2 - 2x_1x_2 + 4x_1x_3 + 2x_2x_3$$

---

## Example 2: Polynomial to Symmetric Matrix Construction

Given the three-variable quadratic polynomial expression:

$$q(X) = x_1^2 - 2x_2^2 + 4x_1x_3$$

### Extracting Matrix Coefficients for $A$:

To map this to a unique $3 \times 3$ symmetric matrix $\begin{bmatrix} a_{11} & a_{12} & a_{13} \\ a_{21} & a_{22} & a_{23} \\ a_{31} & a_{32} & a_{33} \end{bmatrix}$:

1. **Main Diagonal Elements ($a_{ii}$):** Extract coefficients directly from the squared terms:
* Coefficient of $x_1^2 = 1 \implies a_{11} = 1$
* Coefficient of $x_2^2 = -2 \implies a_{22} = -2$
* Coefficient of $x_3^2 = 0 \implies a_{33} = 0$


2. **Off-Diagonal Elements ($a_{ij}$):** Divide the cross-product coefficients exactly by 2:
* Coefficient of $x_1x_3 = 4 \implies a_{13} = a_{31} = \frac{4}{2} = 2$
* Coefficient of $x_1x_2 = 0 \implies a_{12} = a_{21} = 0$
* Coefficient of $x_2x_3 = 0 \implies a_{23} = a_{32} = 0$



### Associated Symmetric Matrix:

$$A = \begin{bmatrix} 1 & 0 & 2 \\ 0 & -2 & 0 \\ 2 & 0 & 0 \end{bmatrix}$$


# Linear Algebra Notes: Rayleigh Quotients

The **Rayleigh Quotient** is a fundamental mathematical tool used to estimate eigenvalues and analyze the scaling behavior of quadratic forms. It maps a vector to a scalar value that relates directly to the matrix's spectrum.

---

## 1. Core Definition

For a real symmetric matrix $A \in \mathbb{R}^{n \times n}$ and any non-zero vector $X \in \mathbb{R}^n$ ($X \neq \mathbf{0}$), the **Rayleigh Quotient** $R_A(X)$ is defined as the ratio:

$$R_A(X) = \frac{X^T AX}{X^T X}$$

---

## 2. Fundamental Properties

### 🔹 Scale Invariance

The Rayleigh Quotient depends only on the *direction* of the vector $X$, not its length. Multiplying $X$ by any non-zero scalar $\alpha$ does not change the result:

$$R_A(\alpha X) = R_A(X) \quad \text{for } \alpha \neq 0$$

> **Proof Sketch:** > 
> $$R_A(\alpha X) = \frac{(\alpha X)^T A (\alpha X)}{(\alpha X)^T (\alpha X)} = \frac{\alpha^2 (X^T AX)}{\alpha^2 (X^T X)} = \frac{X^T AX}{X^T X} = R_A(X)$$
> 
> 

### 🔹 Eigenvector Alignment

If $X$ happens to be a perfect eigenvector of $A$ corresponding to an eigenvalue $\lambda$ (meaning $AX = \lambda X$), the Rayleigh Quotient simplifies exactly to that eigenvalue:

$$R_A(X) = \lambda$$

### 🔹 The Bounding Property (Courant-Fischer Theorem)

The value of the Rayleigh Quotient for any arbitrary non-zero vector is strictly bounded by the minimum and maximum eigenvalues of matrix $A$:

$$\lambda_{\min}(A) \le R_A(X) \le \lambda_{\max}(A)$$

Consequently, the absolute minimum value attainable is the smallest eigenvalue:


$$\lambda_{\min}(A) = \min_{X \neq \mathbf{0}} R_A(X)$$

* **For Unit Vectors ($\|X\|_2 = 1$):** Since the denominator $X^T X = \|X\|_2^2 = 1$, the quotient simplifies directly to the quadratic form, keeping the same bounds:

$$\lambda_{\min}(A) \le X^T AX \le \lambda_{\max}(A)$$



*(This equality holds **if and only if** $X$ is the corresponding eigenvector for that minimum or maximum eigenvalue).*

---

## 3. Practical Concrete Examples

### Example 1: Evaluating an Eigenvector Direction

Let's choose a matrix $A$ and a vector $X$ that we suspect is an eigenvector:

$$A = \begin{pmatrix} 2 & 1 \\ 1 & 2 \end{pmatrix}, \quad X = \begin{pmatrix} 1 \\ 1 \end{pmatrix}$$

**Step 1: Compute the numerator ($X^T AX$)**


$$AX = \begin{pmatrix} 2 & 1 \\ 1 & 2 \end{pmatrix}\begin{pmatrix} 1 \\ 1 \end{pmatrix} = \begin{pmatrix} 3 \\ 3 \end{pmatrix}$$

$$X^T AX = \begin{pmatrix} 1 & 1 \end{pmatrix}\begin{pmatrix} 3 \\ 3 \end{pmatrix} = 1(3) + 1(3) = 6$$

**Step 2: Compute the denominator ($X^T X$)**


$$X^T X = \begin{pmatrix} 1 & 1 \end{pmatrix}\begin{pmatrix} 1 \\ 1 \end{pmatrix} = 1^2 + 1^2 = 2$$

**Step 3: Compute the Quotient**


$$R_A(X) = \frac{6}{2} = 3$$


*(Since $R_A(X) = 3$ and $AX = 3X$, this confirms $\lambda = 3$ is an eigenvalue).*

---

### Example 2: Evaluating an Arbitrary Direction

Using the same matrix $A$, let's pick an arbitrary vector that is *not* an eigenvector direction:

$$A = \begin{pmatrix} 2 & 1 \\ 1 & 2 \end{pmatrix}, \quad X = \begin{pmatrix} 1 \\ 0 \end{pmatrix}$$

**Step 1: Compute the numerator ($X^T AX$)**


$$AX = \begin{pmatrix} 2 & 1 \\ 1 & 2 \end{pmatrix}\begin{pmatrix} 1 \\ 0 \end{pmatrix} = \begin{pmatrix} 2 \\ 1 \end{pmatrix}$$

$$X^T AX = \begin{pmatrix} 1 & 0 \end{pmatrix}\begin{pmatrix} 2 \\ 1 \end{pmatrix} = 1(2) + 0(1) = 2$$

**Step 2: Compute the denominator ($X^T X$)**


$$X^T X = \begin{pmatrix} 1 & 0 \end{pmatrix}\begin{pmatrix} 1 \\ 0 \end{pmatrix} = 1^2 + 0^2 = 1$$

**Step 3: Compute the Quotient**


$$R_A(X) = \frac{2}{1} = 2$$

> **💡 Spectrum Check:** The true eigenvalues for this matrix are $\lambda_{\min} = 1$ and $\lambda_{\max} = 3$. Notice that our calculated value of $2$ falls perfectly within these bounds ($1 \le 2 \le 3$).



# Linear Algebra Notes: Rayleigh Quotient Verification Example

This note provides a step-by-step mathematical breakdown of the handwritten example verifying the bounding properties of the Rayleigh Quotient using a specific $2 \times 2$ symmetric matrix.

---

## 1. Problem Setup

Let $A$ be a $2 \times 2$ real symmetric matrix with known eigenvalues $\lambda_1 = 1$ and $\lambda_2 = 3$:

$$A = \begin{bmatrix} 2 & 1 \\ 1 & 2 \end{bmatrix}, \quad \lambda_{\min}(A) = 1, \quad \lambda_{\max}(A) = 3$$

According to the Rayleigh Quotient bounding theorem, for any unit vector $X$ (where $\|X\|_2 = 1 \implies X^T X = 1$), the quadratic form $X^T AX$ must be strictly bounded between the minimum and maximum eigenvalues:

$$1 \le X^T AX \le 3$$

---

## 2. Mathematical Verifications

### Case A: Evaluating the Minimum Eigenvalue Boundary ($\lambda = 1$)

Let $X$ be the normalized unit eigenvector corresponding to $\lambda_{\min} = 1$:

$$X = \begin{bmatrix} \frac{1}{\sqrt{2}} \\ -\frac{1}{\sqrt{2}} \end{bmatrix}$$

#### 1. Verify it is a unit vector ($X^T X = 1$):

$$X^T X = \begin{bmatrix} \frac{1}{\sqrt{2}} & -\frac{1}{\sqrt{2}} \end{bmatrix} \begin{bmatrix} \frac{1}{\sqrt{2}} \\ -\frac{1}{\sqrt{2}} \end{bmatrix} = \left(\frac{1}{\sqrt{2}}\right)^2 + \left(-\frac{1}{\sqrt{2}}\right)^2 = \frac{1}{2} + \frac{1}{2} = 1$$

#### 2. Compute the quadratic form $X^T AX$:

Since $AX = \lambda X$, we can substitute the eigenvalue directly into the quadratic form expression:


$$X^T AX = X^T (\lambda X) = \lambda (X^T X)$$

Substituting $\lambda = 1$ and $X^T X = 1$:


$$X^T AX = 1 \cdot (1) = 1 = \lambda_{\min}(A)$$

---

### Case B: Evaluating the Maximum Eigenvalue Boundary ($\lambda = 3$)

Let $X$ be the normalized unit eigenvector corresponding to $\lambda_{\max} = 3$:

$$X = \begin{bmatrix} \frac{1}{\sqrt{2}} \\ \frac{1}{\sqrt{2}} \end{bmatrix}$$

#### 1. Verify it is a unit vector ($X^T X = 1$):

$$X^T X = \begin{bmatrix} \frac{1}{\sqrt{2}} & \frac{1}{\sqrt{2}} \end{bmatrix} \begin{bmatrix} \frac{1}{\sqrt{2}} \\ \frac{1}{\sqrt{2}} \end{bmatrix} = \frac{1}{2} + \frac{1}{2} = 1$$

#### 2. Compute the quadratic form $X^T AX$:

Using the same eigenvalue substitution property ($AX = 3X$):


$$X^T AX = X^T (3X) = 3(X^T X) = 3(1) = 3 = \lambda_{\max}(A)$$

---

## 3. General Example: Evaluating an Arbitrary Unit Vector

To see how an arbitrary direction falls between these bounds, let's test a unit vector that points exactly along the standard $x_1$-axis coordinate framework:

$$X = \begin{bmatrix} 1 \\ 0 \end{bmatrix}$$

#### 1. Verify it is a unit vector:

$$X^T X = 1^2 + 0^2 = 1$$

#### 2. Compute the matrix-vector product $AX$:

$$AX = \begin{bmatrix} 2 & 1 \\ 1 & 2 \end{bmatrix} \begin{bmatrix} 1 \\ 0 \end{bmatrix} = \begin{bmatrix} (2\cdot1) + (1\cdot0) \\ (1\cdot1) + (2\cdot0) \end{bmatrix} = \begin{bmatrix} 2 \\ 1 \end{bmatrix}$$

#### 3. Compute the final quadratic form value:

$$X^T AX = \begin{bmatrix} 1 & 0 \end{bmatrix} \begin{bmatrix} 2 \\ 1 \end{bmatrix} = (1 \cdot 2) + (0 \cdot 1) = 2$$

### Final Verification Conclusion

Our calculated value of **$2$** falls directly between the minimum and maximum boundaries established by the eigenvalues:

$$\mathbf{1 \le 2 \le 3}$$

This confirms that any intermediate spatial direction yields a Rayleigh value within the matrix spectrum limits.


# Linear Algebra Notes: Positive Semi-Definite (PSD) Matrices

This section defines **Positive Semi-Definite (PSD) matrices** and provides methods to verify this property algebraically via polynomial expansion and eigenvalue analysis.

---

## 1. Core Definition

A real symmetric matrix $A \in \mathbb{R}^{n \times n}$ is said to be **positive semi-definite (PSD)** if its associated quadratic form is non-negative for every possible vector $X \in \mathbb{R}^n$:

$$q(X) = X^T AX \ge 0 \quad \forall X \in \mathbb{R}^n$$

If the inequality is strict ($X^T AX > 0$) for all non-zero vectors $X \neq \mathbf{0}$, the matrix is classified as **Positive Definite (PD)**.

---

## 2. Walkthrough Example: Algebraic Verification

Let's test the matrix $A$ from the lecture slide:

$$A = \begin{pmatrix} 1 & 3 \\ 3 & 10 \end{pmatrix}$$

### Step 1: Expand into a Quadratic Polynomial

Set up the matrix multiplication using $X = \begin{pmatrix} x_1 & x_2 \end{pmatrix}^T$:

$$X^T AX = \begin{pmatrix} x_1 & x_2 \end{pmatrix} \begin{pmatrix} 1 & 3 \\ 3 & 10 \end{pmatrix} \begin{pmatrix} x_1 \\ x_2 \end{pmatrix}$$

$$= x_1^2 + 6x_1x_2 + 10x_2^2$$

### Step 2: Use Completing the Square to Determine Sign

To easily analyze if this polynomial can ever go negative, we rewrite it as a sum of perfect squares:

$$= (x_1^2 + 6x_1x_2 + 9x_2^2) + x_2^2$$

$$= (x_1 + 3x_2)^2 + x_2^2$$

### Conclusion:

Because any real number raised to an even power is guaranteed to be greater than or equal to zero ($\ge 0$), the sum of two squares can never yield a negative value:


$$(x_1 + 3x_2)^2 + x_2^2 \ge 0$$

$$\implies A \text{ is a valid PSD matrix.}$$

---

## 3. Alternative Verification Method: Eigenvalue Test

While completing the square works beautifully for $2 \times 2$ matrices, checking the **eigenvalues** ($\lambda$) is often much more practical for larger dimensions.

> **Theorem:** A symmetric matrix is PSD if and only if **all of its eigenvalues are non-negative** ($\lambda_i \ge 0$).

### Let's verify our example matrix $A$ using eigenvalues:

$$\det(A - \lambda I) = 0 \implies \det\begin{pmatrix} 1-\lambda & 3 \\ 3 & 10-\lambda \end{pmatrix} = 0$$

$$(1-\lambda)(10-\lambda) - 9 = 0$$

$$\lambda^2 - 11\lambda + 1 = 0$$

Using the quadratic formula:


$$\lambda = \frac{11 \pm \sqrt{(-11)^2 - 4(1)(1)}}{2} = \frac{11 \pm \sqrt{117}}{2}$$

* $\lambda_1 = \frac{11 + 10.816}{2} \approx 10.91 > 0$
* $\lambda_2 = \frac{11 - 10.816}{2} \approx 0.09 > 0$

Since both eigenvalues are strictly greater than zero, this confirms the matrix is not only PSD, but specifically **Positive Definite (PD)**.

---

## 4. Quick Reference Counter-Example

Let's look at a matrix that fails the PSD condition:

$$B = \begin{pmatrix} 1 & 3 \\ 3 & 2 \end{pmatrix}$$

### Quadratic Expansion:

$$X^T BX = x_1^2 + 6x_1x_2 + 2x_2^2$$

Completing the square:


$$= (x_1 + 3x_2)^2 - 7x_2^2$$

### Conclusion:

Because of the negative sign before the second term, this expression can easily yield negative values. For instance, choosing $X = \begin{pmatrix} -3 & 1 \end{pmatrix}^T$:


$$q(X) = (-3 + 3(1))^2 - 7(1)^2 = 0 - 7 = -7 < 0$$

$$\implies B \text{ is an indefinite matrix (not PSD).}$$




# Linear Algebra Notes: Positive Definite (PD) Matrices and Properties

This section defines **Positive Definite (PD) matrices** and details the foundational eigenvalue and pivot tests used to verify both positive definite and positive semi-definite matrix structures.

---

## 1. Core Definition

A real symmetric matrix $A \in \mathbb{R}^{n \times n}$ is said to be **positive definite (PD)** if its associated quadratic form is strictly positive for all non-zero vectors $X \in \mathbb{R}^n$:

$$q(X) = X^T AX > 0 \quad \forall X \neq \mathbf{0}$$

### 🔍 Quick Comparison: PD vs. PSD

* **Positive Definite (PD):** $X^T AX > 0$ for all $X \neq \mathbf{0}$. The geometry forms a strict bowl shape where the absolute minimum value ($0$) is reached *only* exactly at the origin $X = \mathbf{0}$.
* **Positive Semi-Definite (PSD):** $X^T AX \ge 0$. The geometry can contain flat valleys or troughs where the quadratic value stays exactly $0$ even away from the origin.

---

## 2. Fundamental Verification Tests

Testing via the raw polynomial equation can get messy. Instead, we use two highly reliable mathematical properties to verify if a symmetric matrix is positive definite or positive semi-definite:

### Property 1: The Eigenvalue Test

A real symmetric matrix $A$ is:

* **Positive Definite (PD)** $\iff$ All of its eigenvalues are strictly positive ($\lambda_i > 0$).
* **Positive Semi-Definite (PSD)** $\iff$ All of its eigenvalues are non-negative ($\lambda_i \ge 0$).

### Property 2: The Pivot Test

When a matrix is reduced to its upper triangular form via standard Gaussian elimination (without any row exchanges), the main diagonal entries are called **pivots**. A symmetric matrix $A$ is:

* **Positive Definite (PD)** $\iff$ All of its pivots are strictly positive ($\text{pivot}_i > 0$).
* **Positive Semi-Definite (PSD)** $\iff$ All of its pivots are non-negative ($\text{pivot}_i \ge 0$).

---

## 3. Walkthrough Verification Examples

### Example 1: Verifying a Positive Definite (PD) Matrix

Let's analyze the matrix $A$ provided in the lecture slide:

$$A = \begin{pmatrix} 1 & 3 \\ 3 & 10 \end{pmatrix}$$

#### Method A: Checking via the Pivot Test

Let's apply Gaussian elimination to eliminate the value in the second row, first column ($a_{21} = 3$). We perform the row operation: $R_2 \leftarrow R_2 - 3R_1$.

$$\begin{pmatrix} 1 & 3 \\ 3 & 10 \end{pmatrix} \xrightarrow{R_2 - 3R_1} \begin{pmatrix} \mathbf{1} & 3 \\ 0 & \mathbf{1} \end{pmatrix}$$

* **First Pivot:** $1$ (Strictly Positive)
* **Second Pivot:** $1$ (Strictly Positive)

Since all resulting pivots are strictly greater than zero, matrix $A$ is **Positive Definite**.

---

### Example 2: Verifying a Positive Semi-Definite (PSD) Matrix

Let's modify our matrix slightly to look at a border case:

$$B = \begin{pmatrix} 1 & 3 \\ 3 & 9 \end{pmatrix}$$

#### Method A: Checking via the Pivot Test

Let's clear the first column entry using the same row operation: $R_2 \leftarrow R_2 - 3R_1$.

$$\begin{pmatrix} 1 & 3 \\ 3 & 9 \end{pmatrix} \xrightarrow{R_2 - 3R_1} \begin{pmatrix} \mathbf{1} & 3 \\ 0 & \mathbf{0} \end{pmatrix}$$

* **First Pivot:** $1$ (Positive)
* **Second Pivot:** $0$ (Non-negative)

Because the second pivot drops cleanly to zero, this matrix fails the strict PD definition but passes the **Positive Semi-Definite (PSD)** constraint.

#### Method B: Checking via the Eigenvalue Test

Let's calculate the eigenvalues for matrix $B$:


$$\det(B - \lambda I) = \det\begin{pmatrix} 1-\lambda & 3 \\ 3 & 9-\lambda \end{pmatrix} = 0$$

$$(1-\lambda)(9-\lambda) - 9 = 0$$

$$\lambda^2 - 10\lambda + 9 - 9 = 0 \implies \lambda(\lambda - 10) = 0$$

* $\lambda_1 = 10 > 0$
* $\lambda_2 = 0 \ge 0$

Since one of the eigenvalues is exactly zero while the other is positive, this directly confirms that the matrix is **Positive Semi-Definite (PSD)** rather than strictly Positive Definite.


# Linear Algebra Notes: Definiteness Verification Problems

This section provides complete, step-by-step solutions for verifying matrix definiteness using the **Sylvester's Criterion** (Leading Principal Minors test).

---

## 💡 Theoretical Core: Sylvester's Criterion

For any symmetric matrix $A \in \mathbb{R}^{n \times n}$:

* **Positive Definite (PD):** All leading principal minors must be strictly positive ($D_i > 0$).
* **Positive Semi-Definite (PSD):** All leading principal minors must be non-negative ($D_i \ge 0$).

A **leading principal minor** $D_i$ is the determinant of the upper-left $i \times i$ submatrix.

---

## Problem 1: Verifying a Constant Matrix

**Task:** Check whether the following matrix $A_1$ is Positive Definite (PD):

$$A_1 = \begin{pmatrix} 2 & -1 & 0 \\ -1 & 2 & -1 \\ 0 & -1 & 2 \end{pmatrix}$$

### Step-by-Step Solution:

#### Step 1: Compute the $1 \times 1$ Leading Principal Minor ($D_1$)

Take the top-left element:


$$D_1 = |2| = 2$$


Since $2 > 0$, the first condition passes.

#### Step 2: Compute the $2 \times 2$ Leading Principal Minor ($D_2$)

Take the top-left $2 \times 2$ submatrix:


$$D_2 = \begin{vmatrix} 2 & -1 \\ -1 & 2 \end{vmatrix} = (2)(2) - (-1)(-1) = 4 - 1 = 3$$


Since $3 > 0$, the second condition passes.

#### Step 3: Compute the $3 \times 3$ Leading Principal Minor ($D_3 = \det(A_1)$)

Evaluate the full determinant by expanding along the first row:


$$D_3 = \begin{vmatrix} 2 & -1 & 0 \\ -1 & 2 & -1 \\ 0 & -1 & 2 \end{vmatrix}$$

$$D_3 = 2 \begin{vmatrix} 2 & -1 \\ -1 & 2 \end{vmatrix} - (-1) \begin{vmatrix} -1 & -1 \\ 0 & 2 \end{vmatrix} + 0$$

$$D_3 = 2(4 - 1) + 1(-2 - 0)$$

$$D_3 = 2(3) + 1(-2) = 6 - 2 = 4$$


Since $4 > 0$, the final condition passes.

### Conclusion for Problem 1:

Because all leading principal minors are strictly positive:


$$D_1 = 2 > 0, \quad D_2 = 3 > 0, \quad D_3 = 4 > 0$$

$$\implies A_1 \text{ is a valid Positive Definite (PD) matrix.}$$

---

## Problem 2: Finding Parametric Boundaries for PSD

**Task:** For what values of $b$ is the following matrix $A_2$ Positive Semi-Definite (PSD)?

$$A_2 = \begin{pmatrix} 2 & -1 & b \\ -1 & 2 & -1 \\ b & -1 & 2 \end{pmatrix}$$

### Step-by-Step Solution:

#### Step 1: Evaluate $D_1$ and $D_2$

The top-left submatrices are identical to Problem 1 and do not depend on $b$:

* $D_1 = 2 > 0$
* $D_2 = 3 > 0$

Both pass the non-negative requirement for a PSD matrix.

#### Step 2: Set up the inequality for $D_3 = \det(A_2)$

For the matrix to be PSD, the full determinant must be greater than or equal to zero:


$$\det(A_2) \ge 0$$

Expand the determinant along the first row:


$$\det(A_2) = 2 \begin{vmatrix} 2 & -1 \\ -1 & 2 \end{vmatrix} - (-1) \begin{vmatrix} -1 & -1 \\ b & 2 \end{vmatrix} + b \begin{vmatrix} -1 & 2 \\ b & -1 \end{vmatrix} \ge 0$$

Evaluate each $2 \times 2$ component:


$$2(4 - 1) + 1(-2 - (-b)) + b(1 - 2b) \ge 0$$

$$2(3) + 1(-2 + b) + b(1 - 2b) \ge 0$$

#### Step 3: Simplify the Algebraic Expression

Distribute the terms and group by powers of $b$:


$$6 - 2 + b + b - 2b^2 \ge 0$$

$$-2b^2 + 2b + 4 \ge 0$$

Divide the entire inequality by $-2$. Remember to **flip the inequality sign** when multiplying or dividing by a negative number:


$$b^2 - b - 2 \le 0$$

#### Step 4: Factor the Quadratic Inequality

Find two numbers that multiply to $-2$ and add up to $-1$. Those numbers are $-2$ and $+1$:


$$b^2 - 2b + b - 2 \le 0$$

$$b(b - 2) + 1(b - 2) \le 0$$

$$(b - 2)(b + 1) \le 0$$

#### Step 5: Determine the Interval Range

The roots of the polynomial are $b = 2$ and $b = -1$. The product is less than or equal to zero ($\le 0$) in the region closed between these two critical roots:


$$b \le 2 \quad \text{and} \quad b \ge -1$$

### Conclusion for Problem 2:

The matrix $A_2$ is Positive Semi-Definite (PSD) when $b$ lies within the closed interval boundary:


$$\mathbf{b \in [-1, \; 2]}$$

*(Note: If the question asked where the matrix is strictly **Positive Definite (PD)**, the boundary conditions at the roots would be open intervals: $b \in (-1, 2)$).*





# Linear Algebra Notes: Key Matrix Results & Geometric Interpretations

This section breaks down two powerful structural properties of Positive Semi-Definite (PSD) and Positive Definite (PD) matrices, alongside how they look geometrically.

---

## 1. Important Matrix Properties (In Simple Terms)

### Result 1: The Gram Matrix Construction ($A^T A$)

> **The Rule:** If you take *any* real matrix $A$ (square or rectangular) and multiply it by its transpose, the resulting matrix $A^T A$ is **always** Positive Semi-Definite (PSD).
> Furthermore, if the nullspace of $A$ contains only the zero vector ($\text{Nullspace}(A) = \{\mathbf{0}\}$), meaning the columns of $A$ are completely linearly independent, then $A^T A$ is strictly Positive Definite (PD).

* **Why does this happen?** Let's look at the quadratic form equation using a vector $X$:

$$q(X) = X^T (A^T A) X = (AX)^T (AX) = \|AX\|_2^2$$


* Since the squared length of any vector ($\|AX\|_2^2$) can never be negative, the output is guaranteed to be $\ge 0$.
* If the nullspace only has $\{\mathbf{0}\}$, then $AX$ can *never* equal zero unless $X$ itself is zero. This forces the output to be strictly positive ($> 0$), making it PD.

---

### Result 2: Diagonal Regularization ($A + \epsilon I$)

> **The Rule:** If you have a matrix $A$ that is only Positive Semi-Definite (PSD), you can turn it into a strictly Positive Definite (PD) matrix by adding a tiny positive value ($\epsilon > 0$) to its main diagonal.

* **Why does this happen?** Imagine your PSD matrix has an eigenvalue that sits at exactly $0$ (which is allowed for PSD). By adding $\epsilon I$, you add exactly $\epsilon$ to every single eigenvalue.
* The old eigenvalue at $0$ becomes $0 + \epsilon = \epsilon$. Because $\epsilon > 0$, all eigenvalues are now strictly positive, which is the definition of a PD matrix!
* **Real-World Use:** This trick is used constantly in Machine Learning and optimization (e.g., Ridge Regression, optimizer stability) to prevent division-by-zero errors or singular matrix issues.

---

## 2. The Geometry of PD Quadratic Forms

When you plot the equation $q(X) = X^T AX = c$ (where $c$ is a constant and $A$ is Positive Definite), you get nested, multi-dimensional ellipses called **isocontours** (or contour lines of equal value).

### Core Geometric Rules:

1. **Direction of the Axes:** The principal axes of the ellipse point exactly in the directions of the **eigenvectors** of matrix $A$.
2. **Length of the Axes (Radii):** The radius (stretch) along an axis is proportional to the **inverse square root of its eigenvalue** ($\frac{1}{\sqrt{\lambda}}$).
* **Large Eigenvalue ($\lambda$):** Small radius $\rightarrow$ The ellipse is tightly squished along this axis.
* **Small Eigenvalue ($\lambda$):** Large radius $\rightarrow$ The ellipse stretches out wide along this axis.



---

## 3. Clear Visual Example

Let's look at a diagonal matrix to see this in action clearly:

$$A = \begin{pmatrix} 4 & 0 \\ 0 & 1 \end{pmatrix}$$

Since this is a diagonal matrix, its eigenvalues and eigenvectors are obvious:

* **Axis 1 ($x$-axis):** Eigenvalue $\lambda_1 = 4$. Eigenvector $v_1 = \begin{pmatrix} 1 \\ 0 \end{pmatrix}$.
* **Axis 2 ($y$-axis):** Eigenvalue $\lambda_2 = 1$. Eigenvector $v_2 = \begin{pmatrix} 0 \\ 1 \end{pmatrix}$.

### Setting up the Ellipse Equation ($X^T AX = 1$)

$$X^T AX = \begin{pmatrix} x & y \end{pmatrix} \begin{pmatrix} 4 & 0 \\ 0 & 1 \end{pmatrix} \begin{pmatrix} x \\ y \end{pmatrix} = 4x^2 + y^2 = 1$$

Let's rewrite this in the standard algebraic ellipse format ($\frac{x^2}{a^2} + \frac{y^2}{b^2} = 1$):

$$\frac{x^2}{(1/2)^2} + \frac{y^2}{(1)^2} = 1$$

### Match with the Geometric Rules:

* **Along the $x$-axis eigenvector:** The radius is $a = \frac{1}{2}$. Notice that this matches our formula: $\frac{1}{\sqrt{\lambda_1}} = \frac{1}{\sqrt{4}} = \frac{1}{2}$.
* **Along the $y$-axis eigenvector:** The radius is $b = 1$. Notice that this matches our formula: $\frac{1}{\sqrt{\lambda_2}} = \frac{1}{\sqrt{1}} = 1$.

```text
                  y ▲
                    │       isocontour: 4x² + y² = 1
                  1 ┼───────┐
                    │       │
                    │       │  Radius = 1 / √1 = 1
                    │       │
      ───┼──────────┼───────┼──────────► x
        -1       -0.5       0.5        1
                    │       │
                    │       │  Radius = 1 / √4 = 0.5
                    │       │
                 -1 ┼───────┘
                    │

```


