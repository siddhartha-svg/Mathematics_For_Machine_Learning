# Lecture 09: Eigenvalues and Eigenvectors — Motivation

This note introduces the geometric and algebraic motivation behind eigenvalues and eigenvectors by examining how a matrix transformation alters a vector's magnitude and direction.

---

## Geometric Motivation: Matrix Transformations as Functions

A matrix $A$ acts as a linear transformation or mapping function that takes an input vector $x$ and outputs a transformed vector $y$.

In most cases, multiplying a vector by a matrix changes **both** its length (magnitude) and its orientation (direction) in space.

---

## Numerical Example

Let a $2 \times 2$ transformation matrix $A$ and an input vector $x$ be defined as:

$$A = \begin{bmatrix} 1 & 2 \\ 2 & 1 \end{bmatrix}, \quad x = \begin{bmatrix} 1 \\ 3 \end{bmatrix}$$

### Matrix Multiplication Calculation

We evaluate the output vector $y = Ax$ by performing standard row-by-column matrix multiplication:

$$y = Ax = \begin{bmatrix} 1 & 2 \\ 2 & 1 \end{bmatrix} \begin{bmatrix} 1 \\ 3 \end{bmatrix} = \begin{bmatrix} (1 \cdot 1) + (2 \cdot 3) \\ (2 \cdot 1) + (1 \cdot 3) \end{bmatrix} = \begin{bmatrix} 1 + 6 \\ 2 + 3 \end{bmatrix} = \begin{bmatrix} 7 \\ 5 \end{bmatrix}$$

---

## Geometric Analysis of the Result

* **Input Vector ($x$):** Points from the origin $(0,0)$ to the coordinate $(1,3)$.
* **Output Vector ($y$):** Points from the origin $(0,0)$ to the new coordinate $(7,5)$.

> ### The Underlying Question
> 
> 
> As seen in this example, vector $y$ points in a completely different directional path than vector $x$.
> **The Eigenproblem Motivation:** Are there any special, unique vectors $x$ for a given matrix $A$ that *do not* change their spatial direction when multiplied? In other words, where the output vector $y$ is just a scaled version of the input vector $x$ ($Ax = \lambda x$)? Those special directions are our **eigenvectors**, and their scaling factors are the **eigenvalues**.


This note follows the previous motivation example to demonstrate what happens when a matrix transforms a vector along a **special direction**—known as an eigenvector direction.

---

## Geometric Motivation: Direction-Preserving Transformations

Unlike the general case where a matrix multiplication changes both the length and direction of a vector, there exist certain special vectors that **maintain their spatial orientation** after the transformation.

When a matrix acts on these specific vectors, the output vector points along the exact same line as the input vector. The transformation behaves purely as a **scalar scaling operation**.

---

## Numerical Example

Using the same $2 \times 2$ transformation matrix $A$, let us choose a different input vector $x$:

$$A = \begin{bmatrix} 1 & 2 \\ 2 & 1 \end{bmatrix}, \quad x = \begin{bmatrix} 1 \\ 1 \end{bmatrix}$$

### Matrix Multiplication Calculation

We evaluate the output vector $y = Ax$ using standard matrix multiplication:

$$y = Ax = \begin{bmatrix} 1 & 2 \\ 2 & 1 \end{bmatrix} \begin{bmatrix} 1 \\ 1 \end{bmatrix} = \begin{bmatrix} (1 \cdot 1) + (2 \cdot 1) \\ (2 \cdot 1) + (1 \cdot 1) \end{bmatrix} = \begin{bmatrix} 1 + 2 \\ 2 + 1 \end{bmatrix} = \begin{bmatrix} 3 \\ 3 \end{bmatrix}$$

### Factoring the Output

Notice that we can factor out a scalar constant of $3$ from the resulting vector:

$$\begin{bmatrix} 3 \\ 3 \end{bmatrix} = 3 \begin{bmatrix} 1 \\ 1 \end{bmatrix}$$

Since $\begin{bmatrix} 1 \\ 1 \end{bmatrix}$ is our original vector $x$, this reveals the fundamental relationship:

$$Ax = 3x$$

---

## Geometric Analysis of the Result

```text
         y ▲
           │
         4 │                  y = [3, 3]^T
           │                 /
         3 │               / 
           │             /  
         2 │           /    
           │         /      
         1 │       / ── x = [1, 1]^T
           │     /
           └─────┴─────┴─────┴─────┴─────►
           0     1     2     3     4    x

```

* **Input Vector ($x$):** Points from the origin $(0,0)$ to the coordinate $(1,1)$.
* **Output Vector ($y$):** Points from the origin $(0,0)$ to the coordinate $(3,3)$.

> ### 💡 Definition Alignment
> 
> 
> Because the output vector $y$ lies on the exact same linear path as the input vector $x$, this system satisfies the characteristic equation:
> 
> $$Ax = \lambda x$$
> 
> 
> * **The Eigenvector:** $x = \begin{bmatrix} 1 \\ 1 \end{bmatrix}$ is an eigenvector of matrix $A$.
> * **The Eigenvalue:** $\lambda = 3$ is the corresponding eigenvalue, representing the exact factor by which the vector was stretched.
 



This note outlines the formal mathematical definition of eigenvalues, eigenvectors, and eigenpairs for square matrices.

---

## Formal Definition: Eigenpairs

Let $A \in \mathbb{R}^{n \times n}$ be a square matrix. We say that a **non-zero vector** $v \in \mathbb{R}^n$ is an **eigenvector** of $A$ corresponding to the **eigenvalue** $\lambda$ (a scalar constant) if it satisfies the fundamental relation:

$$Av = \lambda v$$

Together, the matching scalar and vector set $(\lambda, v)$ is referred to as an **eigenpair**.

---

## Conceptual and Geometric Meaning

The structural equation tells us that when a matrix (acting as a linear transformation) $A$ is applied to its eigenvector $v$, it **scales $v$ by an amount $\lambda$** without changing its directional line.

### Key Properties & Constraints

* **Non-Zero Vector Constraint ($v \neq \mathbf{0}$):** By definition, an eigenvector *cannot* be the zero vector. If $v = \mathbf{0}$, the equation $A\mathbf{0} = \lambda\mathbf{0}$ simplifies trivially to $\mathbf{0} = \mathbf{0}$ for any scalar value, making it mathematically meaningless.
* **The Scalar $\lambda$:** Unlike the vector, the eigenvalue scalar *can* be zero ($\lambda = 0$), negative, or even a complex number.

---

## Visualizing the Scaling Effect

Depending on the value of the eigenvalue $\lambda$, the linear transformation alters the eigenvector along its axis in the following ways:

```text
       λ > 1 (Stretching)                   0 < λ < 1 (Compressing)
       
       ▲                                    ▲
       │     / Av = 2v                      │   / v
       │    /                               │  /
       │   /                                │ /  Av = 0.5v
       │  / ── v                            │/ ── 
       └─────────────────►                  └─────────────────►
                                            
       λ < 0 (Reversing Direction)
       
       ▲
       │     / v
       │    / 
       │  ─/───
       │  /
       │ /  Av = -1.5v
       ▼

```


A step-by-step mathematical walkthrough for finding the eigenvalues and corresponding eigenvectors of a $3 \times 3$ real matrix.

---

## 1. Theoretical Framework

To find the eigenpairs $(\lambda, v)$ of a square matrix $A$, we begin with the characteristic definition:

$$Av = \lambda v$$

Rearranging this equation to group the vector terms yields:

$$Av - \lambda v = 0 \implies (A - \lambda I)v = \mathbf{0} \quad \text{--- (★)}$$

where $I$ is the identity matrix of matching size. For a non-trivial solution ($v \neq \mathbf{0}$), the matrix coefficient $(A - \lambda I)$ must be singular (non-invertible). Therefore, its determinant must equal zero:

$$\det(A - \lambda I) = 0$$

Solving this equation yields the **characteristic polynomial**, whose roots are the eigenvalues $\lambda$.

---

## 2. Step 1: Finding the Eigenvalues

Given the $3 \times 3$ matrix $A$:

$$A = \begin{bmatrix} 2 & -2 & 3 \\ 1 & 1 & 1 \\ 1 & 3 & -1 \end{bmatrix}$$

### Constructing $(A - \lambda I)$

Subtract $\lambda$ from the main diagonal elements:

$$A - \lambda I = \begin{bmatrix} 2-\lambda & -2 & 3 \\ 1 & 1-\lambda & 1 \\ 1 & 3 & -1-\lambda \end{bmatrix}$$

### Evaluating the Characteristic Determinant

Set $\det(A - \lambda I) = 0$ and expand along the first row:

$$\det(A - \lambda I) = (2-\lambda)\Big((1-\lambda)(-1-\lambda) - 3\Big) + 2\Big((-1-\lambda) - 1\Big) + 3\Big(3 - (1-\lambda)\Big) = 0$$

Solving this polynomial equation yields three distinct real roots:

$$\lambda = 3, \; 1, \; -2$$

---

## 3. Step 2: Finding the Eigenvectors

We substitute each eigenvalue back into the system equation $(A - \lambda I)v = \mathbf{0}$ where $v = \begin{bmatrix} v_1 & v_2 & v_3 \end{bmatrix}^T$.

### Case A: For Eigenvalue $\lambda = 3$

Substitute $\lambda = 3$ into the system equation:

$$(A - 3I)v = \mathbf{0} \implies \begin{bmatrix} 2-3 & -2 & 3 \\ 1 & 1-3 & 1 \\ 1 & 3 & -1-3 \end{bmatrix} \begin{bmatrix} v_1 \\ v_2 \\ v_3 \end{bmatrix} = \begin{bmatrix} 0 \\ 0 \\ 0 \end{bmatrix}$$

$$\begin{bmatrix} -1 & -2 & 3 \\ 1 & -2 & 1 \\ 1 & 3 & -4 \end{bmatrix} \begin{bmatrix} v_1 \\ v_2 \\ v_3 \end{bmatrix} = \begin{bmatrix} 0 \\ 0 \\ 0 \end{bmatrix}$$

Evaluating this linear system yields the dependency relationship:


$$v_1 = v_2 = v_3$$

Choosing a free parameter value of $1$, the normalized basis eigenvector is:

$$v = \begin{bmatrix} 1 \\ 1 \\ 1 \end{bmatrix}$$

---

### Case B: For Eigenvalue $\lambda = 1$

Substitute $\lambda = 1$ into the system equation:

$$(A - 1I)v = \mathbf{0} \implies \begin{bmatrix} 2-1 & -2 & 3 \\ 1 & 1-1 & 1 \\ 1 & 3 & -1-1 \end{bmatrix} \begin{bmatrix} v_1 \\ v_2 \\ v_3 \end{bmatrix} = \begin{bmatrix} 0 \\ 0 \\ 0 \end{bmatrix}$$

$$\begin{bmatrix} 1 & -2 & 3 \\ 1 & 0 & 1 \\ 1 & 3 & -2 \end{bmatrix} \begin{bmatrix} v_1 \\ v_2 \\ v_3 \end{bmatrix} = \begin{bmatrix} 0 \\ 0 \\ 0 \end{bmatrix}$$

Solving the homogeneous linear equations yields the relationship:


$$v_1 = 1, \; v_2 = -1, \; v_3 = -1$$

Thus, the corresponding eigenvector is:

$$v = \begin{bmatrix} 1 \\ -1 \\ -1 \end{bmatrix}$$

---

### Case C: For Eigenvalue $\lambda = -2$

Following the identical system reduction method by evaluating $(A - (-2)I)v = \mathbf{0}$, the third unique directional eigenvector direction can be derived.

---

## 4. Geometric Visualization of the Eigenvector Directions

Since these eigenvectors exist within a three-dimensional coordinate framework ($\mathbb{R}^3$), each eigenvalue scales its corresponding vector along an independent directional axis:

```text
               z ▲          /  v = [1, 1, 1]^T  (λ = 3)
                 │         /
                 │        /
                 │       /
                 │      /   
                 │     /     / v = [1, -1, -1]^T (λ = 1)
                 │    /     /
                 │   /     /
  ───────────────┼──/─────/──────────► x
                 │ /     /
                 │/     /
                 │     /
                 │    /
                 ▼
                 y

```




This one presents an intuitive, geometric view of eigenvalues and eigenvectors using a 2D image transformation (stretching a piece of toast covered by a slice of cheese).

---

## 1. Geometric Perspective: Image Stretching

Consider a linear transformation $T$ in $\mathbb{R}^2$ defined by the diagonal matrix:

$$T = \begin{bmatrix} 2 & 0 \\ 0 & 1 \end{bmatrix}$$

When this matrix acts on an arbitrary coordinate vector $\begin{bmatrix} x_1 \\ x_2 \end{bmatrix}$, it stretches the horizontal component while leaving the vertical component completely unchanged:

$$\begin{bmatrix} 2 & 0 \\ 0 & 1 \end{bmatrix} \begin{bmatrix} x_1 \\ x_2 \end{bmatrix} = \begin{bmatrix} 2x_1 \\ x_2 \end{bmatrix}$$

### Visual Intuition

Imagine a square slice of cheese sitting on half a piece of bread. When the transformation $T$ is applied, the bread and cheese are stretched horizontally along the $x_1$-axis by a factor of $2$, while their vertical heights along the $x_2$-axis remain identical.

---

## 2. Algebraic Calculation of the Eigenpairs

Let the eigenvalues of the diagonal matrix $T$ be given by its diagonal entries: $\lambda = 2$ and $\lambda = 1$.

### Case A: Finding the Eigenvector for $\lambda = 2$

We substitute $\lambda = 2$ into the characteristic system $(T - \lambda I)v = \mathbf{0}$:

$$\begin{bmatrix} 2-2 & 0 \\ 0 & 1-2 \end{bmatrix} \begin{bmatrix} v_1 \\ v_2 \end{bmatrix} = \begin{bmatrix} 0 \\ 0 \end{bmatrix} \implies \begin{bmatrix} 0 & 0 \\ 0 & -1 \end{bmatrix} \begin{bmatrix} v_1 \\ v_2 \end{bmatrix} = \begin{bmatrix} 0 \\ 0 \end{bmatrix}$$

From the second row, this explicitly forces:


$$-v_2 = 0 \implies v_2 = 0$$

The horizontal parameter $v_1$ is a free variable. Setting $v_1 = 1$ yields the eigenvector:

$$v = \begin{bmatrix} 1 \\ 0 \end{bmatrix} \quad \text{(Points along the } x_1\text{-axis / X-axis)}$$

---

### Case B: Finding the Eigenvector for $\lambda = 1$

We substitute $\lambda = 1$ into the characteristic system $(T - 1I)v = \mathbf{0}$:

$$\begin{bmatrix} 2-1 & 0 \\ 0 & 1-1 \end{bmatrix} \begin{bmatrix} v_1 \\ v_2 \end{bmatrix} = \begin{bmatrix} 0 \\ 0 \end{bmatrix} \implies \begin{bmatrix} 1 & 0 \\ 0 & 0 \end{bmatrix} \begin{bmatrix} v_1 \\ v_2 \end{bmatrix} = \begin{bmatrix} 0 \\ 0 \end{bmatrix}$$

From the first row, this forces:


$$1 \cdot v_1 = 0 \implies v_1 = 0$$

The vertical parameter $v_2$ is a free variable. Setting $v_2 = 1$ yields the corresponding eigenvector:

$$v = \begin{bmatrix} 0 \\ 1 \end{bmatrix} \quad \text{(Points along the } x_2\text{-axis / Y-axis)}$$

---

## 3. Geometric Summary

```text
         x2 ▲
            │       Before               After Transformation
          4 │     ┌───────┐                  ┌───────────────┐
            │     │       │                  │               │
          3 │     │ Cheese│     ────►        │    Cheese     │
            │     │       │                  │               │
          2 │     └───────┘                  └───────────────┘
            │   (1,0) Vector               (2,0) Vector
          1 │     ──►                        ────►
            │
            └─────┴─────┴─────┴─────┴─────┴─────┴─────► x1
            0     1     2     3     4     5     6 

```

* **The Horizontal Basis Vector $\begin{bmatrix} 1 \\ 0 \end{bmatrix}$:** Points along the $x_1$-axis. After the transformation, it points in the exact same direction but is scaled to $\begin{bmatrix} 2 \\ 0 \end{bmatrix}$. This matches $\lambda = 2$.
* **The Vertical Basis Vector $\begin{bmatrix} 0 \\ 1 \end{bmatrix}$:** Points along the $x_2$-axis. After the transformation, it remains completely unaltered as $\begin{bmatrix} 0 \\ 1 \end{bmatrix}$. This matches $\lambda = 1$.
* **Any Off-Axis Vector:** Any vector pointing diagonally (like the crust corners of the bread) changes both its angle and orientation under the transformation, meaning diagonal lines are **not** eigenvectors for this matrix.



This note provides a geometric visualization of eigenvalues/eigenvectors using standard spatial shearing and lists key algebraic algebraic properties of eigenpairs.

---

## 1. Geometric Intuition: Guessing Eigenpairs from Transformations

Consider a linear transformation matrix $A \in \mathbb{R}^{2 \times 2}$ applied to a unit square centered with diagonal lines:

$$A = \begin{pmatrix} 1.5 & 0.5 \\ 0.5 & 1.5 \end{pmatrix}$$

When this matrix transforms the shape, the square is stretched diagonally into a rhombus along specific axes. By identifying which vectors **do not change their directional path**, we can visually determine the eigenvectors and eigenvalues.

### Analyzing the Special Directions

```text
               x2 ▲
                  │     /  Line along [1, 1]^T  (Stretched by 2)
                  │    /   
                  │   / ───►  
                  │  / 
                  │ /     
                  │/─────────────► x1
                 /│
                / │
               /  │
  Line along [1, -1]^T 
  (Unchanged length, λ = 1)

```

1. **The Main Diagonal Direction ($\mathbf{v_1 = \begin{bmatrix} 1 \\ 1 \end{bmatrix}}$):**
Looking at the primary diagonal pointing up and to the right, this directional axis remains completely unbent. However, its length doubles.

$$\implies \text{Eigenvector: } \begin{bmatrix} 1 \\ 1 \end{bmatrix} \implies \text{Eigenvalue: } \lambda = 2$$


2. **The Off-Diagonal Direction ($\mathbf{v_2 = \begin{bmatrix} 1 \\ -1 \end{bmatrix}}$):**
Looking at the diagonal pointing down and to the right, its spatial line is also preserved under the transform, and its length is completely unchanged.

$$\implies \text{Eigenvector: } \begin{bmatrix} 1 \\ -1 \end{bmatrix} \implies \text{Eigenvalue: } \lambda = 1$$



---

## 2. Fundamental Algebraic Properties of Eigenpairs

Let $A$ be an $n \times n$ invertible matrix with a valid eigenpair $(\lambda, X)$ satisfying the characteristic relationship $AX = \lambda X$. The following core algebraic rules apply:

### 1) Inverse Matrix Property

If $A$ has an eigenvalue $\lambda$, then its matrix inverse $A^{-1}$ has the reciprocal eigenvalue $\frac{1}{\lambda}$:

$$A^{-1}AX = A^{-1}(\lambda X)$$

$$I X = \lambda (A^{-1}X) \implies A^{-1}X = \left(\frac{1}{\lambda}\right)X$$

---

### 2) Matrix Powers and Exponential Property

If matrix $A$ is multiplied by itself to a power $k$, its eigenvectors remain completely identical, while its corresponding eigenvalues are raised to that same power $k$:

* **For $A^2$:** 
$$A^2X = A(AX) = A(\lambda X) = \lambda(AX) = \lambda(\lambda X) = \lambda^2 X$$


* **Generalized for $A^k$:** 
$$A^kX = \lambda^k X \quad \text{where } k \in \mathbb{Z}^+$$



---

### 3) The Trace Property

The **trace** of a matrix (the algebraic sum of its main diagonal entries) is always identically equal to the sum of all its individual eigenvalues:

$$\text{Trace}(A) = \sum_{i=1}^n a_{ii} = \sum_{i=1}^n \lambda_i$$

#### Verification with Example Matrix $A$:

$$\text{Trace}(A) = 1.5 + 1.5 = 3$$

$$\text{Sum of Eigenvalues} = \lambda_1 + \lambda_2 = 2 + 1 = 3 \quad \text{(Matches Perfectly!)}$$

---

### 4) The Determinant Property

The **determinant** of a matrix is always identically equal to the absolute product of all its individual eigenvalues:

$$\det(A) = \prod_{i=1}^n \lambda_i$$

#### Verification with Example Matrix $A$:

$$\det(A) = (1.5)(1.5) - (0.5)(0.5) = 2.25 - 0.25 = 2$$

$$\text{Product of Eigenvalues} = \lambda_1 \cdot \lambda_2 = 2 \cdot 1 = 2 \quad \text{(Matches Perfectly!)}$$


---

## Example 1: General $3 \times 3$ Matrix

### Code

```python
import numpy as np

# Define a general 3x3 matrix
A = np.array([[2, -2, 3], 
              [1, 1, 1], 
              [1, 3, -1]])
print("Matrix A:")
print(A)

# Calculate eigenpairs
values, vectors = np.linalg.eig(A)

print("\nEigenvalues:")
print(values)

print("\nEigenvectors (column-wise):")
print(vectors)

```

### Output

```text
Matrix A:
[[ 2 -2  3]
 [ 1  1  1]
 [ 1  3 -1]]

Eigenvalues:
[ 3.  1. -2.]

Eigenvectors (column-wise):
[[ 0.57735027  0.57735027 -0.61648937]
 [ 0.57735027 -0.57735027 -0.05607722]
 [ 0.57735027 -0.57735027  0.78508102]]

```

> **Note on interpreting `np.linalg.eig` outputs:** > NumPy returns eigenvectors as **normalized unit vectors** (length of 1). For example, the first eigenvector corresponding to $\lambda = 3$ is printed as:
> 
> $$\begin{bmatrix} 0.57735027 \\ 0.57735027 \\ 0.57735027 \end{bmatrix} \approx \begin{bmatrix} 1/\sqrt{3} \\ 1/\sqrt{3} \\ 1/\sqrt{3} \end{bmatrix}$$
> 
> 
> 
> This is exactly equivalent to the analytical direction $\begin{bmatrix} 1 & 1 & 1 \end{bmatrix}^T$.

---

## Example 2: Diagonal Matrix

### Code

```python
import numpy as np

# Define a 3x3 diagonal matrix
A = np.array([[2, 0, 0], 
              [0, 1, 0], 
              [0, 0, -1]])
print("Diagonal Matrix A:")
print(A)

# Calculate eigenpairs
values, vectors = np.linalg.eig(A)

print("\nEigenvalues:")
print(values)

print("\nEigenvectors (column-wise):")
print(vectors)

```

### Output

```text
Diagonal Matrix A:
[[ 2  0  0]
 [ 0  1  0]
 [ 0  0 -1]]

Eigenvalues:
[ 2.  1. -1.]

Eigenvectors (column-wise):
[[1. 0. 0.]
 [0. 1. 0.]
 [0. 0. 1.]]

```

> **Key Takeaway:** For any pure diagonal matrix, the **eigenvalues** are exactly the elements along the main diagonal, and the corresponding **eigenvectors** are the standard basis vectors (columns of the identity matrix).