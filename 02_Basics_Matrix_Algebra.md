# 2.Basics of Matrices Algebra: 

## Definition (Layman's Perspective)
A **matrix** is a two-dimensional array of scalars with one or more columns and one or more rows *(Note: This is a practical, conceptual definition rather than a strict abstract mathematical one)*.

---

## General Representation

A matrix is denoted by a set of elements enclosed in brackets, indexed by rows ($i$) and columns ($j$):

$$\{a_{ij}\}_{m \times n}$$

Where:
* $i = 1, 2, \dots, m$ (Row index)
* $j = 1, 2, \dots, n$ (Column index)
* $m \times n$ represents the **dimensions** (Rows $\times$ Columns) of the matrix.

---

## Core Examples and Dimensions

### 1. Square Matrices
When the number of rows equals the number of columns.

* **$3 \times 3$ Matrix Example:**
  $$\begin{bmatrix} 5 & 8 & 7 \\ 0 & 3 & 8 \\ 0 & 0 & 1 \end{bmatrix}_{3 \times 3}$$

  **Element breakdown from this example:**
  * Row 1 elements: $a_{11} = 5$, $a_{12} = 8$, $a_{13} = 7$
  * Specific element index: $a_{32} = 0$ (Row 3, Column 2)

* **$2 \times 2$ Matrix Example:**
  $$\begin{bmatrix} 1 & -1 \\ 2 & 3 \end{bmatrix}_{2 \times 2}$$

### 2. Column and Row Vectors as Matrices

Matrices can also scale down to a single row or column, bridging the concept between vectors and matrices.

* **Column Matrix ($3 \times 1$):**
  $$\begin{bmatrix} 1 \\ 2 \\ 3 \end{bmatrix}_{3 \times 1}$$

* **Row Matrix ($1 \times 3$):**
  $$\begin{bmatrix} 3 & 5 & 2 \end{bmatrix}_{1 \times 3}$$

# Diagonal and Triangular Matrix

## Diagonal Matrix
A square matrix whose off-diagonal elements are all zero.
The main diagonal contains elements where the row index equals the column index ($i = j$).

$$\begin{bmatrix} 2 & 0 & 0 \\ 0 & 3 & 0 \\ 0 & 0 & 1 \end{bmatrix}$$

* **Main Diagonal Elements ($i = j$):** $a_{11} = 2$, $a_{22} = 3$, $a_{33} = 1$

### Zero Matrix
A special case where all elements in the matrix are zero:

$$\begin{bmatrix} 0 & 0 & 0 \\ 0 & 0 & 0 \\ 0 & 0 & 0 \end{bmatrix}$$

---

## Triangular Matrix
A square matrix whose elements above or below the main diagonal are all zero.

### 1. Upper Triangular Matrix
A matrix where all entries **below** the main diagonal are zero.

$$\begin{bmatrix} 5 & 8 & 7 \\ 0 & 3 & 8 \\ 0 & 0 & 1 \end{bmatrix}$$

### 2. Lower Triangular Matrix
A matrix where all entries **above** the main diagonal are zero.

$$\begin{bmatrix} 4 & 0 & 0 \\ 3 & 2 & 0 \\ 5 & 0 & 3 \end{bmatrix}$$  

# Identity Matrix

## Definition
A diagonal matrix whose all diagonal entries are all $1$.

---

## Examples

### 2x2 Identity Matrix ($I_2$)
$$I_2 = \begin{bmatrix} 1 & 0 \\ 0 & 1 \end{bmatrix}$$

### 3x3 Identity Matrix ($I_3$)
$$I_3 = \begin{bmatrix} 1 & 0 & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 1 \end{bmatrix}$$


# Matrix Algebra - Matrix Equality

## Definition
Two matrices are said to be **equal** if their dimensions are equal and all corresponding elements are equal. 

$$\text{Formally: } A = B \iff a_{ij} = b_{ij} \quad \forall \text{ } i \text{ and } j$$

---

## Example (Checking for Equality)

Consider the two $2 \times 2$ matrices $A$ and $B$:

$$A = \begin{bmatrix} 1 & -1 \\ 2 & 0 \end{bmatrix}_{2 \times 2} \quad \text{and} \quad B = \begin{bmatrix} 1 & -1 \\ 2 & 3 \end{bmatrix}_{2 \times 2}$$

### Step-by-Step Element Comparison:

* Comparing Row 1:
  $$a_{11} = 1 = b_{11}$$
  $$a_{12} = -1 = b_{12}$$

* Comparing Row 2:
  $$a_{21} = 2 = b_{21}$$
  $$a_{22} = 0 \quad \text{and} \quad b_{22} = 3 \implies a_{22} \neq b_{22}$$

### Conclusion
Since there is at least one element position where the values do not match ($a_{22} \neq b_{22}$), the matrices are not equal:

$$\implies A \neq B$$


## Matrix Algebra - Addition and Subtraction

## Fundamental Rule
The addition or subtraction of two matrices, $\mathbf{A}$ and $\mathbf{B}$ of the **same size** yields a third matrix $\mathbf{C}$ of that same size.

Operations are performed element-by-element (component-wise):
$$c_{ij} = a_{ij} \pm b_{ij} \quad \text{for all } i, j$$

> ### ⚠️ Crucial Remark
> Matrices of **different sizes** cannot be added or subtracted.

---

## Algebraic Laws for Matrix Addition

Matrix addition obeys standard arithmetic laws, assuming all matrices ($\mathbf{A}$, $\mathbf{B}$, and $\mathbf{C}$) share identical dimensions:

### 1. Commutative Law
The order in which you add the matrices does not change the result:
$$\mathbf{A} + \mathbf{B} = \mathbf{B} + \mathbf{A}$$

### 2. Associative Law
The grouping of the matrices does not change the result:
$$\mathbf{A} + (\mathbf{B} + \mathbf{C}) = (\mathbf{A} + \mathbf{B}) + \mathbf{C} = \mathbf{A} + \mathbf{B} + \mathbf{C}$$


## Matrix Algebra - Addition and Subtraction Example

Operations follow the entry-wise rule:
$$c_{ij} = a_{ij} \pm b_{ij} \quad \text{for all } i, j$$

---

## Example

Given two $2 \times 3$ matrices $A$ and $B$:

$$A = \begin{bmatrix} 1 & -1 & 3 \\ 2 & 0 & 1 \end{bmatrix}_{2 \times 3} \quad \text{and} \quad B = \begin{bmatrix} 1 & 1 & 0 \\ 2 & 1 & 3 \end{bmatrix}_{2 \times 3}$$

### 1. Matrix Addition ($A + B$)

$$A + B = \begin{bmatrix} 1+1 & -1+1 & 3+0 \\ 2+2 & 0+1 & 1+3 \end{bmatrix} = \begin{bmatrix} 2 & 0 & 3 \\ 4 & 1 & 4 \end{bmatrix}$$

> **Property Verified:** Matrix addition is commutative: $A + B = B + A$

### 2. Matrix Subtraction ($A - B$)

$$A - B = \begin{bmatrix} 1-1 & -1-1 & 3-0 \\ 2-2 & 0-1 & 1-3 \end{bmatrix} = \begin{bmatrix} 0 & -2 & 3 \\ 0 & -1 & -2 \end{bmatrix}$$

---

> ### ⚠️ Reminders
> * Matrices of **different sizes** cannot be added or subtracted.


# Scalar Multiplication

## Definition
Matrices can be multiplied by a scalar (constant). If a matrix is multiplied by a scalar, every individual element inside the matrix is multiplied by that scalar.

Let $A$ be an $m \times n$ matrix:
$$A = \begin{bmatrix} 
a_{11} & a_{12} & \dots & a_{1n} \\ 
a_{21} & a_{22} & \dots & a_{2n} \\ 
\vdots & \vdots & \ddots & \vdots \\ 
a_{m1} & a_{m2} & \dots & a_{mn} 
\end{bmatrix}_{m \times n}$$

For any scalar $\alpha \in \mathbb{R} \text{ or } \mathbb{C}$ (Real or Complex numbers):

$$\alpha A = \begin{bmatrix} 
\alpha a_{11} & \alpha a_{12} & \dots & \alpha a_{1n} \\ 
\alpha a_{21} & \alpha a_{22} & \dots & \alpha a_{2n} \\ 
\vdots & \vdots & \ddots & \vdots \\ 
\alpha a_{m1} & \alpha a_{m2} & \dots & \alpha a_{mn} 
\end{bmatrix}$$

---

## Example

Given the $2 \times 2$ matrix $A$ and scalar $\alpha = 5$:

$$A = \begin{bmatrix} 2 & 1 \\ -1 & 4 \end{bmatrix}$$

Multiplying the matrix by $5$:

$$5A = \begin{bmatrix} 5(2) & 5(1) \\ 5(-1) & 5(4) \end{bmatrix} = \begin{bmatrix} 10 & 5 \\ -5 & 20 \end{bmatrix}$$


# Matrix Multiplication

## Core Rules & Conditions

* The product of two matrices is another matrix.
* **The Necessary Condition:** For two matrices $A$ and $B$ to be multiplied ($A \times B$), the **number of columns of $A$ must equal the number of rows of $B$**.

---

## Dimension Matching Mechanics

If matrix $A$ has dimensions $m \times n$ and matrix $B$ has dimensions $n \times p$, they can be multiplied because the inner dimensions match ($n = n$). The resulting matrix $C$ will have the outer dimensions ($m \times p$).

### Dimensional Example from Slide

$$A \times B = C$$

$$\begin{matrix} A \\ (5 \times \mathbf{3}) \end{matrix} \quad \times \quad \begin{matrix} B \\ (\mathbf{3} \times 4) \end{matrix} \quad = \quad \begin{matrix} C \\ (5 \times 4) \end{matrix}$$

> **Key Takeaway:** > * **Inner numbers match:** $3 = 3$ (Multiplication is **valid**).
> * **Outer numbers determine product size:** $5$ and $4$ create a **$5 \times 4$** matrix.


# Matrix Multiplication Mechanics

## Matrix Multiplication Formula Layout

When multiplying matrix $A$ (size $2 \times 3$) by matrix $B$ (size $3 \times 2$), the resulting matrix $C$ is a $2 \times 2$ matrix:

$$\begin{bmatrix} 
a_{11} & a_{12} & a_{13} \\ 
a_{21} & a_{22} & a_{23} 
\end{bmatrix}_{2 \times 3}
\begin{bmatrix} 
b_{11} & b_{12} \\ 
b_{21} & b_{22} \\ 
b_{31} & b_{32} 
\end{bmatrix}_{3 \times 2}
= 
\begin{bmatrix} 
c_{11} & c_{12} \\ 
c_{21} & c_{22} 
\end{bmatrix}_{2 \times 2}$$


$$
\begin{bmatrix}
a_{11} & a_{12} & a_{13} \\
a_{21} & a_{22} & a_{23}
\end{bmatrix}_{2 \times 3}
\;
\begin{bmatrix}
b_{11} & b_{12} \\
b_{21} & b_{22} \\
b_{31} & b_{32}
\end{bmatrix}_{3 \times 2}
=
\begin{bmatrix}
c_{11} & c_{12} \\
c_{21} & c_{22}
\end{bmatrix}_{2 \times 2}
$$

## Fundamental Operational Rule

Every element $c_{ij}$ in the product matrix is computed as the **dot product** of the $i$-th row of matrix $A$ and the $j$-th column of matrix $B$:

$$c_{ij} = (i\text{-th row of } A) \cdot (j\text{-th column of } B)$$

### Concrete Calculation for Element $c_{11}$
To find the top-left element ($c_{11}$), multiply the elements of **Row 1 of $A$** by **Column 1 of $B$** and sum them up:

$$c_{11} = \begin{pmatrix} a_{11} & a_{12} & a_{13} \end{pmatrix} \begin{pmatrix} b_{11} \\ b_{21} \\ b_{31} \end{pmatrix} = a_{11}b_{11} + a_{12}b_{21} + a_{13}b_{31}$$

---

## When is Matrix Multiplication NOT Possible?

Matrix multiplication $A \times B$ is **impossible** if the inner dimensions do not match. Specifically:
> The **number of columns in Matrix $A$** must be **equal** to the **number of rows in Matrix $B$**.

### ❌ Incompatible Example 
Consider attempting to multiply these two matrices:

$$A = \begin{bmatrix} 1 & 2 \\ 3 & 4 \end{bmatrix}_{2 \times \mathbf{2}} \quad \text{and} \quad B = \begin{bmatrix} 5 & 6 & 7 \\ 8 & 9 & 0 \\ 1 & 2 & 3 \end{bmatrix}_{\mathbf{3} \times 3}$$

* Number of columns in $A = \mathbf{2}$
* Number of rows in $B = \mathbf{3}$

$$\mathbf{2} \neq \mathbf{3} \implies \text{Multiplication is NOT possible!}$$

If you tried to map the first row of $A$ across the first column of $B$, you would run out of elements from matrix $A$ to complete the calculation.


# Linear Algebra Notes: Matrix Multiplication Example

## Setup and Compatibility Check

Given a $2 \times 2$ matrix $A$ and a $2 \times 3$ matrix $B$:

$$A = \begin{bmatrix} 1 & -1 \\ 2 & 1 \end{bmatrix}_{2 \times \mathbf{2}} \quad \text{and} \quad B = \begin{bmatrix} 1 & -1 & 0 \\ 0 & 1 & 1 \end{bmatrix}_{\mathbf{2} \times 3}$$

* **Compatibility Check:** The number of columns in $A$ matches the number of rows in $B$ ($2 = 2$). 
* **Output Dimensions:** The product matrix $C$ will have dimensions $2 \times 3$.

---

## Resulting Product Matrix

$$C = A \times B = \begin{bmatrix} 1 & -2 & -1 \\ 2 & -1 & 1 \end{bmatrix}_{2 \times 3}$$

---

## Step-by-Step Calculation Breakdown

Every entry $c_{ij}$ is found by taking the dot product of the $i$-th row of $A$ and the $j$-th column of $B$:

### Finding Element $c_{11}$ (Row 1 of $A$ $\cdot$ Column 1 of $B$)
$$c_{11} = (1, -1) \cdot (1, 0) = (1 \times 1) + (-1 \times 0) = 1 + 0 = 1$$

### Finding Element $c_{12}$ (Row 1 of $A$ $\cdot$ Column 2 of $B$)
$$c_{12} = (1, -1) \cdot (-1, 1) = (1 \times -1) + (-1 \times 1) = -1 - 1 = -2$$

### Remaining Elements Quick Math (for your reference)
* $c_{13} = (1, -1) \cdot (0, 1) = (1 \times 0) + (-1 \times 1) = -1$
* $c_{21} = (2, 1) \cdot (1, 0) = (2 \times 1) + (1 \times 0) = 2$
* $c_{22} = (2, 1) \cdot (-1, 1) = (2 \times -1) + (1 \times 1) = -1$
* $c_{23} = (2, 1) \cdot (0, 1) = (2 \times 0) + (1 \times 1) = 1$


#  Matrix Multiplication Rules

## Fundamental Laws

Assuming the matrices $\mathbf{A}$, $\mathbf{B}$, and $\mathbf{C}$ are of conformable sizes such that the operations are defined, and $\mathbf{I}$ is the identity matrix:

1. **Identity Property:**
   $$\mathbf{AI} = \mathbf{IA} = \mathbf{A}$$

2. **Associative Law:**
   $$\mathbf{A}(\mathbf{BC}) = (\mathbf{AB})\mathbf{C} = \mathbf{ABC}$$

3. **First Distributive Law (Left Distributive):**
   $$\mathbf{A}(\mathbf{B} + \mathbf{C}) = \mathbf{AB} + \mathbf{AC}$$

4. **Second Distributive Law (Right Distributive):**
   $$(\mathbf{A} + \mathbf{B})\mathbf{C} = \mathbf{AC} + \mathbf{BC}$$

---

## ⚠️ Caution! (How Matrix Algebra Differs from Scalar Algebra)

Unlike regular number algebra where $xy = yx$ or if $xy = 0 \implies x=0 \text{ or } y=0$, matrix multiplication follows strict counter-intuitive rules:

### 1. Non-Commutativity
Matrix multiplication is generally **not commutative**:
$$\mathbf{AB} \neq \mathbf{BA}$$
*Furthermore, even if $\mathbf{AB}$ can be calculated, $\mathbf{BA}$ might not be conformable (impossible to multiply due to dimension mismatch).*

### 2. Zero Product Property Does Not Apply
If $\mathbf{AB} = \mathbf{0}$, it does **not** mean that either $\mathbf{A}$ or $\mathbf{B}$ must be a zero matrix.

* **Handwritten Example from Slide:**
  $$\begin{bmatrix} 1 & 0 \\ 0 & 0 \end{bmatrix} \begin{bmatrix} 0 & 0 \\ 0 & 1 \end{bmatrix} = \begin{bmatrix} 0 & 0 \\ 0 & 0 \end{bmatrix}$$
  *(Neither starting matrix is zero, yet their product is a zero matrix).*

### 3. Failure of the Cancellation Law
If $\mathbf{AB} = \mathbf{AC}$ and $\mathbf{A} \neq \mathbf{0}$, it does **not** necessarily mean that $\mathbf{B} = \mathbf{C}$. 
$$\mathbf{AB} = \mathbf{AC} \centernot\implies \mathbf{B} = \mathbf{C}$$



# Determinant of a Matrix

## Core Principles
* Every **square matrix** has a determinant.
* The determinant of a matrix is a single scalar **number**.

---

## Formula for a 2x2 Matrix
For a general $2 \times 2$ matrix $A$:
$$A = \begin{bmatrix} a & b \\ c & d \end{bmatrix}$$

The determinant is calculated by cross-multiplying the main diagonal and subtracting the product of the off-diagonal:
$$|A| \text{ or } \det(A) = ad - bc$$

---

## Numerical Example from Slide

Given the $2 \times 2$ matrix $A$:
$$A = \begin{bmatrix} 1 & -1 \\ 2 & 3 \end{bmatrix}$$

### Calculation Breakdown:
By cross-multiplying the elements along the arrows:
* Main diagonal product: $1 \times 3 = 3$
* Off-diagonal product: $(-1) \times 2 = -2$

$$\det(A) = (1 \times 3) - (-1 \times 2)$$
$$\det(A) = 3 - (-2) = 5$$

$$\implies |A| \text{ or } \det(A) = 5$$


# Inverse of a Matrix

## Scalar Analogy (Reciprocal)
Consider a scalar constant $k$. Its inverse is simply its reciprocal, or the division of 1 by that scalar.
* **Example:** If $k = 7$, the inverse of $k$ (written as $k^{-1}$) is:
  $$k^{-1} = \frac{1}{k} = \frac{1}{7}$$

---

## Why Direct "Matrix Division" Does Not Exist
Direct division of matrices is not defined in linear algebra. This is primarily because matrix operations do not follow standard scalar algebra cancellation properties; for instance, you can have an equation where:
$$\mathbf{AB} = \mathbf{AC}$$ 
even when matrix $\mathbf{B}$ and matrix $\mathbf{C}$ are **not equal** ($\mathbf{B} \neq \mathbf{C}$). 

Because we cannot simply "divide out" matrix $\mathbf{A}$, we use **matrix inversion** instead.

---

## Formal Definition of Matrix Inversion

The inverse of a square matrix $\mathbf{A}$, if it exists, is the unique matrix denoted as $\mathbf{A}^{-1}$ that satisfies the following property:

$$\mathbf{AA}^{-1} = \mathbf{A}^{-1}\mathbf{A} = \mathbf{I}$$

*(Where $\mathbf{I}$ is the Identity Matrix of corresponding dimensions).*


# Linear Algebra Notes: Properties of the Inverse of a Matrix

## Core Algebraic Properties

Assuming matrices $A$ and $B$ are invertible square matrices and $k$ is a non-zero scalar:

1. **Product Inverse Rule (Socks-and-Shoes Property):**
   $$(AB)^{-1} = B^{-1}A^{-1}$$
   *(Note: The order of multiplication reverses)*

2. **Double Inverse Rule:**
   $$(A^{-1})^{-1} = A$$

3. **Transpose and Inverse Commutativity:**
   $$(A^T)^{-1} = (A^{-1})^T$$

4. **Scalar Inverse Rule:**
   $$(kA)^{-1} = \frac{1}{k} A^{-1}$$

---

## Matrix Classification: Singular vs. Nonsingular

The existence of an inverse matrix directly connects to its classification and its determinant value:

* **Nonsingular Matrix:** A square matrix that **has an inverse**.
* **Singular Matrix:** A matrix that **does not have an inverse**.

### The Determinant Rule
* Square matrices have inverses **except when the determinant is zero**.
* When the determinant of a matrix is zero ($\det(A) = 0$), the matrix is **singular** (uninvertible).




# Linear Algebra with Python: Matrix Addition & Shape Incompatibility in NumPy

## 1. Scenario A: Incompatible Shapes (ValueError)

When trying to add two matrices of different dimensions, NumPy will throw a `ValueError` because the arrays cannot be element-wise matched or broadcast together.

```python
import numpy as np

# Define a 3x2 matrix
P = np.array([[1, 7], [2, 1], [3, 2]])
print("Matrix P:\n", P)

# Define a 2x2 matrix
Q = np.array([[1, 1], [1, -1]])
print("Matrix Q:\n", Q)

# Attempt addition
C1 = np.add(P, Q)

```

**Output Error:**

```text
ValueError: operands could not be broadcast together with shapes (3,2) (2,2)

```

---

## 2. Scenario B: Compatible Shapes (Successful Addition)

To perform matrix addition, both matrices must share the exact same dimensions ($m \times n$). Here, both `P` and `Q` are defined as $3 \times 2$ matrices.

```python
import numpy as np

# Define a 3x2 matrix
P = np.array([[1, 7], [2, 1], [3, 2]])

# Define a matching 3x2 matrix
Q = np.array([[1, 1], [1, -1], [1, 0]])

# Perform element-wise addition
C1 = np.add(P, Q)
print(C1)

```

**Output:**

```text
[[2 8]
 [3 0]
 [4 2]]

```

> ### 💡 Key Takeaway
> 
> 
> Matrix addition in NumPy requires the operands to have identical shapes so that every unique row index $i$ and column index $j$ can be added directly via $c_{ij} = a_{ij} + b_{ij}$.



# Matrix Subtraction, Dot Product, and Determinants in NumPy

## 1. Matrix Subtraction
Matrix subtraction is performed element-wise. For this operation to be valid, both matrices must share identical dimensions ($3 \times 2$).

*Note: Matrix `P` is carried over from the previous context as:*
$$P = \begin{bmatrix} 1 & 7 \\ 2 & 1 \\ 3 & 2 \end{bmatrix}$$

```python
import numpy as np

# Define a 3x2 matrix Q
Q = np.array([[1, 1], [1, -1], [1, 0]])
print("Matrix Q:\n", Q)

# Element-wise subtraction (P - Q)
C1 = np.subtract(P, Q)
print("Subtraction Result (C1):\n", C1)

```

**Output:**

```text
Matrix Q:
 [[ 1  1]
 [ 1 -1]
 [ 1  0]]

Subtraction Result (C1):
 [[0 6]
 [1 2]
 [2 2]]

```

---

## 2. Matrix Multiplication (Dot Product)

To multiply matrix `P` ($3 \times \mathbf{2}$) by matrix `R` ($\mathbf{2} \times 3$), the inner dimensions must match ($2 = 2$). The resulting matrix `C2` will have the outer dimensions ($3 \times 3$).

```python
# Define a 2x3 matrix R
R = np.array([[1, 3, 1], [1, 0, 1]])
print("Matrix R:\n", R)

# Compute the matrix product
C2 = np.dot(P, R)
print("Dot Product Result (C2):\n", C2)

```

**Output:**

```text
Matrix R:
 [[1 3 1]
 [1 0 1]]

Dot Product Result (C2):
 [[8 3 8]
 [3 6 3]
 [5 9 5]]

```

---

## 3. Matrix Determinant

The determinant can only be calculated for a square matrix. `np.linalg.det()` is used here to find the determinant of the $3 \times 3$ matrix `C2`.

```python
# Calculate the determinant of the square matrix C2
det = np.linalg.det(C2)
print("Determinant of C2:", det)

```

**Output:**

```text
Determinant of C2: 0.0

```

> ### 💡 Key Takeaway
> 
> 
> Since the determinant of matrix `C2` is exactly `0.0`, `C2` is classified as a **singular matrix**, meaning it does not possess a multiplicative inverse ($C2^{-1}$ does not exist).



# Linear Algebra with Python: Matrix Inversion & Singularity Errors in NumPy

## 1. Scenario A: Inverting a Singular Matrix (LinAlgError)
An error occurs when attempting to compute the inverse of matrix `C2`. Because its determinant is exactly `0.0`, the matrix is mathematically **singular** and cannot be inverted. 

Additionally, note the typo in the image (`no.linalg` instead of `np.linalg`). Fixing the typo to `np.linalg.inv(C2)` on a matrix with a 0 determinant will trigger a NumPy execution error.

```python
import numpy as np

# C2 is a singular matrix (det = 0.0) from the previous multiplication step
C2 = np.array([[8, 3, 8], 
               [3, 6, 3], 
               [5, 9, 5]])

# This will raise an error because the matrix has no inverse
S2 = np.linalg.inv(C2)

```

**Expected NumPy Error Output:**

```text
LinAlgError: Singular matrix

```

---

## 2. Scenario B: Inverting a Non-Singular Matrix (Successful Inversion)

When a square matrix has a non-zero determinant ($\det(M) \neq 0$), it is **non-singular** and its inverse can be successfully computed using `np.linalg.inv()`.

```python
import numpy as np

# Define a 2x2 non-singular matrix M
M = np.array([[1, -1], 
              [2, 3]])

# Compute the multiplicative inverse
M_inverse = np.linalg.inv(M)
print(M_inverse)

```

**Output:**

```text
[[ 0.6  0.2]
 [-0.4  0.2]]

```

> ### 💡 Key Takeaway
> 
> 
> Always verify that a matrix is non-singular ($\det \neq 0$) before using `np.linalg.inv()`. Mathematically, computing the inverse involves dividing by the determinant; since division by zero is undefined, singular matrices cannot be inverted.

