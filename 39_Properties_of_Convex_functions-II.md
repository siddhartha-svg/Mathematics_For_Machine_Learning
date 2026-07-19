# Linear Algebra & Convex Optimization: Definiteness of a Matrix

## 1. Core Concept: Definiteness of a Matrix
In optimization and linear algebra, the **definiteness** of a symmetric matrix helps us understand the behavior of quadratic forms. It tells us whether a matrix, when multiplied by any non-zero vector on both sides, always yields a positive, negative, or zero value. 

Let $H$ be a **symmetric matrix** (where $H = H^T$) of order $n \times n$, and let $x \in \mathbb{R}^n$ be a column vector.

### Four Types of Definiteness:
*   **Positive Semi-Definite (PSD):** $x^T H x \ge 0$ for all $x \in \mathbb{R}^n$.
*   **Negative Semi-Definite (NSD):** $x^T H x \le 0$ for all $x \in \mathbb{R}^n$.
*   **Positive Definite (PD):** $x^T H x > 0$ for all $x \in \mathbb{R}^n$ where $x \neq 0$.
*   **Negative Definite (ND):** $x^T H x < 0$ for all $x \in \mathbb{R}^n$ where $x \neq 0$.

> 💡 **Remark:** A symmetric matrix $H$ is negative semi-definite (or negative definite) if and only if $-H$ is positive semi-definite (or positive definite).

---

## 2. Step-by-Step Procedure to Evaluate Definiteness
To manually determine the definiteness using the vector-matrix multiplication approach ($x^T A x$):

*   **Step 1:** Verify if the matrix is symmetric ($A = A^T$).
*   **Step 2:** Define a general vector $x = \begin{pmatrix} x_1 \\ x_2 \\ \vdots \\ x_n \end{pmatrix}$.
*   **Step 3:** Perform the row-vector by matrix multiplication: $x^T A$.
*   **Step 4:** Multiply the resulting row vector by the column vector: $(x^T A)x$.
*   **Step 5:** Simplify the resulting algebraic expression into a sum of squares or factored terms.
*   **Step 6:** Analyze the final sign to conclude the definiteness.

---

## 3. Solved Problems (From Slides)

### 📝 Problem 1: Analyzing Matrix $A$
Given the $2 \times 2$ matrix:
$$A = \begin{pmatrix} 3 & 1 \\ 1 & 3 \end{pmatrix}$$

#### **Step 1: Check Symmetry**
$$A^T = \begin{pmatrix} 3 & 1 \\ 1 & 3 \end{pmatrix} = A \quad \text{(Symmetric! ✅)}$$

#### **Step 2: Setup the Quadratic Form**
Let $x = \begin{pmatrix} x_1 \\ x_2 \end{pmatrix}$, so $x^T = \begin{pmatrix} x_1 & x_2 \end{pmatrix}$.
$$x^T A x = \begin{pmatrix} x_1 & x_2 \end{pmatrix} \begin{pmatrix} 3 & 1 \\ 1 & 3 \end{pmatrix} \begin{pmatrix} x_1 \\ x_2 \end{pmatrix}$$

#### **Step 3: Step-by-Step Calculation**
1. First, multiply the matrix by the column vector:
   $$\begin{pmatrix} 3 & 1 \\ 1 & 3 \end{pmatrix} \begin{pmatrix} x_1 \\ x_2 \end{pmatrix} = \begin{pmatrix} 3x_1 + x_2 \\ x_1 + 3x_2 \end{pmatrix}$$

2. Next, multiply by the row vector $x^T$:
   $$x^T A x = \begin{pmatrix} x_1 & x_2 \end{pmatrix} \begin{pmatrix} 3x_1 + x_2 \\ x_1 + 3x_2 \end{pmatrix}$$
   $$x^T A x = x_1(3x_1 + x_2) + x_2(x_1 + 3x_2)$$
   $$x^T A x = 3x_1^2 + x_1 x_2 + x_2 x_1 + 3x_2^2$$
   $$x^T A x = 3x_1^2 + 2x_1 x_2 + 3x_2^2$$

#### **Step 4: Algebraic Manipulation & Sign Analysis**
Break down the terms to look for clear squares:
$$x^T A x = 2(x_1^2 + x_2^2) + (x_1^2 + x_2^2 + 2x_1 x_2)$$
$$x^T A x = 2(x_1^2 + x_2^2) + (x_1 + x_2)^2$$

Since squares are always non-negative ($x_1^2 \ge 0$, $x_2^2 \ge 0$, and $(x_1+x_2)^2 \ge 0$):
$$2(x_1^2 + x_2^2) + (x_1 + x_2)^2 \ge 0 \quad \forall x \in \mathbb{R}^2$$

#### **Conclusion:**
Matrix $A$ is **Positive Semi-Definite**. *(Note: Because both terms only simultaneously become $0$ when $x_1=0$ and $x_2=0$, it is actually strictly Positive Definite as well).*

---

### 📝 Problem 2: Analyzing Matrix $M$
Given the $2 \times 2$ matrix:
$$M = \begin{pmatrix} 2 & -2 \\ -2 & 2 \end{pmatrix}$$

#### **Step 1: Check Symmetry**
$$M^T = \begin{pmatrix} 2 & -2 \\ -2 & 2 \end{pmatrix} = M \quad \text{(Symmetric! ✅)}$$

#### **Step 2: Setup the Quadratic Form**
$$x^T M x = \begin{pmatrix} x_1 & x_2 \end{pmatrix} \begin{pmatrix} 2 & -2 \\ -2 & 2 \end{pmatrix} \begin{pmatrix} x_1 \\ x_2 \end{pmatrix}$$

#### **Step 3: Step-by-Step Calculation**
1. Multiply the matrix by the column vector:
   $$\begin{pmatrix} 2 & -2 \\ -2 & 2 \end{pmatrix} \begin{pmatrix} x_1 \\ x_2 \end{pmatrix} = \begin{pmatrix} 2x_1 - 2x_2 \\ -2x_1 + 2x_2 \end{pmatrix}$$

2. Multiply by the row vector $x^T$:
   $$x^T M x = \begin{pmatrix} x_1 & x_2 \end{pmatrix} \begin{pmatrix} 2x_1 - 2x_2 \\ -2x_1 + 2x_2 \end{pmatrix}$$
   $$x^T M x = x_1(2x_1 - 2x_2) + x_2(-2x_1 + 2x_2)$$
   $$x^T M x = 2x_1^2 - 2x_1 x_2 - 2x_2 x_1 + 2x_2^2$$
   $$x^T M x = 2x_1^2 - 4x_1 x_2 + 2x_2^2$$

#### **Step 4: Algebraic Manipulation & Sign Analysis**
Factor out the common scalar $2$:
$$x^T M x = 2(x_1^2 - 2x_1 x_2 + x_2^2)$$
Recognize the perfect square identity $(a-b)^2 = a^2 - 2ab + b^2$:
$$x^T M x = 2(x_1 - x_2)^2$$

Since any real value squared is greater than or equal to zero:
$$2(x_1 - x_2)^2 \ge 0 \quad \forall (x_1, x_2) \in \mathbb{R}^2$$

#### **Conclusion:**
Matrix $M$ is **Positive Semi-Definite** (Notice that if $x_1 = x_2$, such as vector $\begin{pmatrix}1 \\ 1\end{pmatrix}$, $x^T M x = 0$ even though the vector is non-zero).

---

## 4. Visualizing Definiteness Geometric Meaning
Below is a graphical concept representation of how the output space behaves for these matrices:

```text
       ▲ Quadratic Form Output Value: f(x) = xᵀHx
       │
       │       *               *    ◄── Positive Definite (Always strictly above 0)
       │        *             *
       │         *           *
───────┼──────────*─────────*──────────► Vector Space (x)
       │           *       *
       │            *     *         ◄── Positive Semi-Definite (Touches 0 line)
───────┼─────────────*───*─────────────►
       │               *

```

# Tests for Definiteness of a Matrix

This document covers two major methods for identifying the mathematical property known as the **Definiteness of a Matrix**: the **Eigenvalue Test** and the **Principal Minor Test**.

---

## 1. Concept: Eigenvalue Test

Let $A$ be a real symmetric matrix of order $n$. The signs of its eigenvalues uniquely determine its category of definiteness:

*   **Positive Definite:** All eigenvalues are strictly positive ($> 0$).
*   **Positive Semi-Definite:** All eigenvalues are non-negative ($\ge 0$).
*   **Negative Definite:** All eigenvalues are strictly negative ($< 0$).
*   **Negative Semi-Definite:** All eigenvalues are non-positive ($\le 0$).
*   **Indefinite:** There is at least one positive eigenvalue and at least one negative eigenvalue.

---

## 2. Concept: Principal Minor Test

### Defining a Principal Minor
A **principal minor** $D_k$ of a matrix $A$ of order $k$ is the determinant of a submatrix formed by deleting any $(n - k)$ rows and $(n - k)$ columns *with the same indices/numbers*. 

### The Test
*   **For Positive Semi-Definiteness:** A symmetric matrix is positive semi-definite if and only if **all possible principal minors** are non-negative ($\ge 0$).
*   *Note on Positive Definiteness:* If **all possible principal minors** are strictly greater than zero ($> 0$), the matrix is positive definite.

---

## 3. Step-by-Step Problem and Calculations

### 📝 Problem 1: Principal Minor Analysis (From Image)
Determine the definiteness of the following $3 \times 3$ matrix $M$:

$$M = \begin{pmatrix} 4 & 2 & 3 \\ 2 & 3 & 2 \\ 3 & 2 & 4 \end{pmatrix}$$

#### **Step 1: Check Symmetry**
Confirm if $M = M^T$:
Transposing rows to columns gives the exact same matrix, so it is a **real symmetric matrix**.

#### **Step 2: Calculate Minors of Order $1 \times 1$**
These are simply the single elements sitting along the main diagonal (formed by keeping 1 row/column pair and deleting the other 2 pairs):
*   $M_{11} = 4$
*   $M_{22} = 3$
*   $M_{33} = 4$

Values: **$4, 3, 4$**. All are $> 0$.

#### **Step 3: Calculate Minors of Order $2 \times 2$**
These are the determinants of the $2 \times 2$ submatrices along the diagonal:

1.  **Deleting Row 1 & Col 1:**
    $$\begin{vmatrix} 3 & 2 \\ 2 & 4 \end{vmatrix} = (3 \times 4) - (2 \times 2) = 12 - 4 = 8$$

2.  **Deleting Row 2 & Col 2:**
    $$\begin{vmatrix} 4 & 3 \\ 3 & 4 \end{vmatrix} = (4 \times 4) - (3 \times 3) = 16 - 9 = 7$$

3.  **Deleting Row 3 & Col 3:**
    $$\begin{vmatrix} 4 & 2 \\ 2 & 3 \end{vmatrix} = (4 \times 3) - (2 \times 2) = 12 - 4 = 8$$

Values: **$8, 7, 8$**. All are $> 0$.

#### **Step 4: Calculate Minor of Order $3 \times 3$ (The Full Determinant)**
Evaluate the determinant of the full matrix $M$:
$$\text{det}(M) = \begin{vmatrix} 4 & 2 & 3 \\ 2 & 3 & 2 \\ 3 & 2 & 4 \end{vmatrix}$$

$$\text{det}(M) = 4 \cdot \begin{vmatrix} 3 & 2 \\ 2 & 4 \end{vmatrix} - 2 \cdot \begin{vmatrix} 2 & 2 \\ 3 & 4 \end{vmatrix} + 3 \cdot \begin{vmatrix} 2 & 3 \\ 3 & 2 \end{vmatrix}$$
$$\text{det}(M) = 4(12 - 4) - 2(8 - 6) + 3(4 - 9)$$
$$\text{det}(M) = 4(8) - 2(2) + 3(-5)$$
$$\text{det}(M) = 32 - 4 - 15 = 13$$

Since $13 > 0$, this minor is strictly positive.

#### **Conclusion:**
Because every single calculated principal minor across orders 1, 2, and 3 is strictly positive ($> 0$), **$M$ is positive definite**.

---

### 📝 Problem 2: Alternative Scenario (Indefinite Matrix Example)
Let's look at another matrix evaluated via the Eigenvalue Test.

$$A = \begin{pmatrix} 1 & 2 \\ 2 & 1 \end{pmatrix}$$

#### **Step 1: Find Characteristic Equation**
$$\text{det}(A - \lambda I) = 0 \implies \begin{vmatrix} 1-\lambda & 2 \\ 2 & 1-\lambda \end{vmatrix} = 0$$

#### **Step 2: Calculate Eigenvalues**
$$(1-\lambda)^2 - (2 \times 2) = 0$$
$$1 - 2\lambda + \lambda^2 - 4 = 0$$
$$\lambda^2 - 2\lambda - 3 = 0$$
$$(\lambda - 3)(\lambda + 1) = 0$$

$$\lambda_1 = 3, \quad \lambda_2 = -1$$

#### **Conclusion:**
Since one eigenvalue is positive ($3$) and one eigenvalue is negative ($-1$), the matrix is **Indefinite**.

---

## 4. Concept Visualization Graph

Below is a conceptual graph showcasing how Eigenvalues map to the different classifications of Definiteness:

```text
               EIGENVALUE SIGN SPECTRUM MAP
               
   Negative Definite       Indefinite       Positive Definite
  (All Values < 0)     (Mixed Sign Values)   (All Values > 0)
<───────────────────────┼────────────────────────>
 -5    -4    -3    -2   0   +1    +2    +3    +4    +5
                        │
                        ▼
               [ Semi-Definite Zone ]
            If values touch 0 but don't 
            cross to the opposing sign.

```

# Convex Optimization: Characterization of Convex Functions via Hessian Matrix

## 1. Concept Name: Second-Order Condition for Convexity

### Simple Meaning
A function with two derivatives (twice differentiable) is **convex** if and only if its slope never decreases as you move forward. In higher dimensions, this translates to checking the **Hessian matrix** (a matrix filled with its second-order partial derivatives). If this Hessian matrix is always **positive semi-definite** (meaning its values or behavior never curve downwards), then the function is globally convex.

---

## 2. Core Theorem & Proof Structure

### Theorem Statement
Let $S$ be a non-empty open convex subset of $\mathbb{R}^n$ and $f : S \longrightarrow \mathbb{R}$ be twice differentiable on $S$. Then $f$ is a **convex function** on $S$ if and only if the Hessian matrix $\nabla^2 f(x)$ is **positive semi-definite** $\forall x \in S$.

$$f \text{ is convex on } S \iff \nabla^2 f(x) \succeq 0 \quad \forall x \in S$$

---

### Step-by-Step Proof Breakdowns

#### **Part 1: If $f$ is convex $\implies \nabla^2 f(x)$ is Positive Semi-Definite**
1. **Setup:** Let $f$ be convex on $S$ and choose a point $\bar{x} \in S$. We want to prove that $x^T \nabla^2 f(\bar{x}) x \ge 0$ for any vector $x \in \mathbb{R}^n$.
2. **Taylor Expansion:** Since $S$ is open, for a tiny step scalar $\lambda > 0$, the point $(\bar{x} + \lambda x)$ is also in $S$. Expanding $f(\bar{x} + \lambda x)$ using its second-order Taylor series yields:
   $$f(\bar{x} + \lambda x) = f(\bar{x}) + (\lambda x)^T \nabla f(\bar{x}) + \frac{1}{2}(\lambda x)^T \nabla^2 f(\bar{x})(\lambda x) + \beta(\bar{x}, \lambda x)\Vert{}\lambda x\Vert{}^2$$
   where the error term $\beta(\bar{x}, \lambda x) \to 0$ as $\lambda \to 0$.
3. **Using Convexity Property:** A known property for any differentiable convex function is:
   $$f(\bar{x} + \lambda x) - f(\bar{x}) \ge (\lambda x)^T \nabla f(\bar{x})$$
4. **Substitution & Limiting:** Replacing this inequality into our expansion gives:
   $$\frac{1}{2}\lambda^2 x^T \nabla^2 f(\bar{x})x + \lambda^2 \beta(\bar{x}, \lambda x)\Vert{}x\Vert{}^2 \ge 0$$
   Divide the whole expression by $\lambda^2$:
   $$\frac{1}{2} x^T \nabla^2 f(\bar{x})x + \beta(\bar{x}, \lambda x)\Vert{}x\Vert{}^2 \ge 0$$
   Taking the limit as $\lambda \to 0^+$, the error term disappears, leaving:
   $$\frac{1}{2} x^T \nabla^2 f(\bar{x})x \ge 0 \implies x^T \nabla^2 f(\bar{x})x \ge 0$$

#### **Part 2: If $\nabla^2 f(x) \succeq 0 \implies f$ is convex**
1. Take any two points $x_1, x_2 \in S$.
2. By the **Mean Value Theorem** (Extended form), there exists an intermediate point $\hat{x} = \lambda x_1 + (1-\lambda)x_2$ such that:
   $$f(x_1) = f(x_2) + (x_1 - x_2)^T \nabla f(x_2) + \frac{1}{2}(x_1 - x_2)^T \nabla^2 f(\hat{x})(x_1 - x_2)$$
3. Since the Hessian is assumed to be positive semi-definite everywhere, the quadratic term must be non-negative: $\frac{1}{2}(x_1 - x_2)^T \nabla^2 f(\hat{x})(x_1 - x_2) \ge 0$.
4. Dropping that non-negative term simplifies the equation to the classic condition for convexity:
   $$f(x_1) - f(x_2) \ge (x_1 - x_2)^T \nabla f(x_2) \implies f \text{ is convex on } S$$

---

## 3. Solved Problems with Step-by-Step Calculations

### 📝 Problem 1 (From Slide)
Determine if the function $f: \mathbb{R}^3 \to \mathbb{R}$ is convex:
$$f(x, y, z) = x^2 + 4y^2 + z^2 + 4xy + 4yz + 2xz$$

#### **Step 1: Compute First-Order Partial Derivatives**
Find the first derivative with respect to each variable:
*   $f_x = \frac{\partial f}{\partial x} = 2x + 4y + 2z$
*   $f_y = \frac{\partial f}{\partial y} = 8y + 4x + 4z$
*   $f_z = \frac{\partial f}{\partial z} = 2z + 4y + 2x$

#### **Step 2: Construct the Hessian Matrix $\nabla^2 f$**
The Hessian is formed by taking the second-order partial derivatives:
$$\nabla^2 f = \begin{pmatrix} f_{xx} & f_{xy} & f_{xz} \\ f_{yx} & f_{yy} & f_{yz} \\ f_{zx} & f_{zy} & f_{zz} \end{pmatrix} = \begin{pmatrix} 2 & 4 & 2 \\ 4 & 8 & 4 \\ 2 & 4 & 2 \end{pmatrix}$$

#### **Step 3: Test for Definiteness using Principal Minors**
We must check all principal minors to ensure they are all $\ge 0$:

*   **Order $1 \times 1$ Minors (Diagonal Elements):**
    $$D_1 = 2, \quad D_1 = 8, \quad D_1 = 2 \quad (\text{All } \ge 0)$$

*   **Order $2 \times 2$ Minors:**
    1. Top-left $2 \times 2$: $\begin{vmatrix} 2 & 4 \\ 4 & 8 \end{vmatrix} = (2 \times 8) - (4 \times 4) = 16 - 16 = 0$
    2. Bottom-right $2 \times 2$: $\begin{vmatrix} 8 & 4 \\ 4 & 2 \end{vmatrix} = (8 \times 2) - (4 \times 4) = 16 - 16 = 0$
    3. Outer corners $2 \times 2$: $\begin{vmatrix} 2 & 2 \\ 2 & 2 \end{vmatrix} = (2 \times 2) - (2 \times 2) = 4 - 4 = 0$
    All $2 \times 2$ minors are exactly $0$ ($\ge 0$).

*   **Order $3 \times 3$ Minor (Full Determinant):**
    $$\text{det}(\nabla^2 f) = 2(16 - 16) - 4(8 - 8) + 2(16 - 16) = 2(0) - 4(0) + 2(0) = 0$$

#### **Conclusion:**
Since all principal minors are non-negative ($\ge 0$), the matrix $\nabla^2 f$ is **positive semi-definite**. Therefore, the function $f$ is **convex** on $\mathbb{R}^3$.

---

### 📝 Problem 2 (Additional Practice Example)
Test the convexity of $f(x, y) = x^4 + y^2$.

#### **Step 1: Compute Partial Derivatives**
*   $f_x = 4x^3 \implies f_{xx} = 12x^2, \quad f_{xy} = 0$
*   $f_y = 2y \implies f_{yy} = 2, \quad f_{yx} = 0$

#### **Step 2: Construct Hessian Matrix**
$$\nabla^2 f(x,y) = \begin{pmatrix} 12x^2 & 0 \\ 0 & 2 \end{pmatrix}$$

#### **Step 3: Evaluate Minors**
*   $D_1 = 12x^2 \ge 0$ (since $x^2$ is always $\ge 0$ for any real number $x$).
*   $D_2 = (12x^2 \times 2) - (0 \times 0) = 24x^2 \ge 0$.

#### **Conclusion:**
Since both principal minors are $\ge 0$ for all values of $x$ and $y$, the Hessian is positive semi-definite everywhere, proving the function is **globally convex**.

---

## 4. Concept Graph Visualization

The graph below visually explains the relationship between a function's geometric curvature shape and its structural Hessian Matrix definition:

```text
       ▲ Curvature Value f(x)
       │
       │        *             *        ◄── Convex Curve (U-Shaped Bowl)
       │         *           *             Hessian ∇²f(x) ≥ 0 (Positive Semi-Definite)
       │          *         *              Slope is constant or increasing.
───────┼───────────*───────*───────────► Input Space (x)
       │            *******
       │
       │            .......
       │          .         .          ◄── Concave Curve (Inverted Bowl)
       │         .           .             Hessian ∇²f(x) ≤ 0 (Negative Semi-Definite)
       │        .             .            Slope is decreasing.            