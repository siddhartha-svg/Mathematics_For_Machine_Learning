# Lecture 06: Linear Transformations

## Relevance in Machine Learning

* **Abstract Mathematics & Computer Science:** Linear transformations are used in both fields. Within calculus, they serve as a way of tracking change, also known as **derivatives**.
* **Machine Learning Applications:** They are highly useful in modeling **2D and 3D animation**, where an object's size and shape need to be transformed from one viewing angle to the next.
* **Geometric Transformations:** An object can be rotated and scaled within a space using a specific type of linear transformation known as a geometric transformation.
* **Data Projection:** Linear transformations are used to project data from one space to another. Sometimes, a dataset is not **linearly separable** in its original space. Therefore, we need to transform (project) the data into another space with different dimensions. This can be achieved using either a **'linear transformation'** or **'kernels'**.

## Linear Transformation

Let $V$ and $W$ be vector spaces over a field $F$ of dimensions $n$ and $m$, respectively. 

A **linear transformation** is a mapping $T : V^{(n)}(F) \longrightarrow W^{(m)}(F)$ such that:

1. $T(v_1 + v_2) = T(v_1) + T(v_2) \quad \forall v_1, v_2 \in V$
2. $T(\alpha v) = \alpha T(v) \quad \forall v \in V \text{ and } \alpha \in F$

### Examples

* $T : \mathbb{R}^2 \longrightarrow \mathbb{R}^2$ such that:
  $$T(x_1, x_2) = (x_1, x_1 + x_2)$$

* $T : \mathbb{R}^3 \longrightarrow \mathbb{R}^3$ such that:
  $$T(x_1, x_2, x_3) = (x_2, x_1, 0)$$

### Remarks

* A linear map from a vector space to itself is called a **linear operator**.
* A linear map from a vector space to its underlying field is called a **linear functional**.

## Example: Verifying a Linear Transformation

Let $T : \mathbb{R}^2 \longrightarrow \mathbb{R}^2$ such that $T(x_1, x_2) = (x_1, x_1 + x_2)$.

Let $v_1 = (x_1, x_2)$ and $v_2 = (y_1, y_2) \in V = \mathbb{R}^2(\mathbb{R})$.

---

### 1. Condition 1: Additivity

First, evaluate the individual transformations:
* $T(v_1) = T(x_1, x_2) = (x_1, x_1 + x_2)$
* $T(v_2) = T(y_1, y_2) = (y_1, y_1 + y_2)$

Now, evaluate the transformation of their sum:
$$
\begin{aligned}
T(v_1 + v_2) &= T(x_1 + y_1, x_2 + y_2) \\
             &= (x_1 + y_1, \, x_1 + y_1 + x_2 + y_2) \\
             &= (x_1, x_1 + x_2) + (y_1, y_1 + y_2) \\
             &= T(v_1) + T(v_2) \quad \checkmark
\end{aligned}
$$

---

### 2. Condition 2: Homogeneity

Evaluate the transformation of a scaled vector, where $\alpha \in \mathbb{R}$:
$$
\begin{aligned}
T(\alpha v_1) &= T(\alpha x_1, \alpha x_2) \\
              &= (\alpha x_1, \, \alpha x_1 + \alpha x_2) \\
              &= (\alpha x_1, \, \alpha(x_1 + x_2)) \\
              &= \alpha(x_1, x_1 + x_2) \\
              &= \alpha T(v_1) \quad \checkmark
\end{aligned}
$$

### Conclusion
Since both conditions are satisfied, **$T$ is a linear transformation**.


---

## Linear Transformations on $\mathbb{R}^2$

### 1. Original Space (Domain)

* **Unit Square Coordinates:** $(0,0) \to (1,0) \to (1,1) \to (0,1)$
* **Alternative Input:** Rotated Square (Linear combination / Rotation)

---

### 2. Transformation Mapping Table

| Transformation Formula | Geometric Effect | Output Visual Description |
| --- | --- | --- |
| $T(x_1, x_2) = (2x_1, 2x_2)$ | **Uniform Scaling (Dilation)** | A larger square with a width of 2 and a height of 2 along the axes. |
| $T(x_1, x_2) = (x_1, 2x_2)$ | **Vertical Stretch** | A vertical rectangle with a width of 1 and a height of 2. |
| $T(x_1, x_2) = (x_1, 0)$ | **Orthogonal Projection** | The 2D square collapses entirely onto a 1D line segment on the $x_1$-axis from 0 to 1. |

---

### 3. Visual Representation (Text-Based Graphs)

#### Uniform Scaling: $(2x_1, 2x_2)$

```
   x2 ▲
      │  ┌───────┐ 
    2 │  │       │
      │  │       │
      └──┴───────┴────► x1
         0       2

```

#### Vertical Stretch: $(x_1, 2x_2)$

```
   x2 ▲
      │  ┌───┐ 
    2 │  │   │
      │  │   │
      └──┴───┴────────► x1
         0   1

```

#### Projection onto $x_1$-Axis: $(x_1, 0)$

```
   x2 ▲
      │  
    0 │  ■━━━━━━━■
      └──┴───────┴────► x1
         0       1

```

---

## 2D Rotation Transformation

The linear transformation $T: \mathbb{R}^2 \to \mathbb{R}^2$ rotates a vector counterclockwise by an angle $\theta$:

$$T(x_1, x_2) = (x_1 \cos\theta - x_2 \sin\theta, \; x_1 \sin\theta + x_2 \cos\theta)$$

### Matrix Representation

This transformation can be expressed compactly in matrix-vector form as:

$$= \begin{bmatrix} \cos\theta & -\sin\theta \\ \sin\theta & \cos\theta \end{bmatrix} \begin{bmatrix} x_1 \\ x_2 \end{bmatrix}$$

$$\text{R} \quad\quad\quad \text{X}$$

Where:

* **$\text{R}$** is the standard 2D rotation matrix.
* **$\text{X}$** is the column vector being transformed.


---

## Examples: Checking for Linear Maps

Determine which of the following mappings are linear maps:

### 1. Vector Space Mappings ($\mathbb{R}^n \to \mathbb{R}^m$)

* **Example 1:**

$$T : \mathbb{R}^2 \longrightarrow \mathbb{R}^3 \quad \text{s.t.} \quad T(x_1, x_2) = (x_1 + x_2 + 1, \; 2x_1 - x_2, \; x_1 + x_2)$$


* **Example 2:**

$$T : \mathbb{R}^2 \longrightarrow \mathbb{R}^2 \quad \text{s.t.} \quad T(x_1, x_2) = (x_1 - x_2, \; 2x_1^2 - x_2^2)$$


* **Example 3:**

$$T : \mathbb{R}^2 \longrightarrow \mathbb{R}^2 \quad \text{s.t.} \quad T(x_1, x_2) = (x_1 - x_2, \; |x_1|)$$


* **Example 4:**

$$T : \mathbb{R}^2 \longrightarrow \mathbb{R}^4 \quad \text{s.t.} \quad T(x_1, x_2) = (x_1 + x_2, \; x_1 - x_2, \; 2x_1 + x_2, \; 3x_1 - 4x_2)$$


* **Example 5:**

$$T : \mathbb{R}^3 \longrightarrow \mathbb{R}^3 \quad \text{s.t.} \quad T(x_1, x_2, x_3) = (x_3, \; x_2, \; x_1)$$



---

### 2. Matrix Space Mappings ($M_2(\mathbb{R}) \to M_2(\mathbb{R})$)

* **Example 6:**

$$T : M_2(\mathbb{R}) \longrightarrow M_2(\mathbb{R}) \quad \text{s.t.} \quad T(A) = A^T$$


* **Example 7:**

$$T : M_2(\mathbb{R}) \longrightarrow M_2(\mathbb{R}) \quad \text{s.t.} \quad T(A) = I + A$$


* **Example 8:**

$$T : M_2(\mathbb{R}) \longrightarrow M_2(\mathbb{R}) \quad \text{s.t.} \quad T(A) = BAB^{-1} \quad \text{where } B \text{ is an invertible matrix.}$$



---

## Counterexample: Proving Non-Linearity

To show that a map is **not linear**, we can find a specific counterexample where the additivity property fails:


$$T(u + v) \neq T(u) + T(v)$$

Given the mapping:


$$T(x_1, x_2) = (x_1 - x_2, \; 2x_1^2 - x_2^2)$$

Consider the vectors $(1,1)$ and $(2,2)$ in $\mathbb{R}^2$:

### 1. Individual Transformations

* $$T(1,1) = (1 - 1, \; 2(1)^2 - 1^2) = (0, 1)$$


* $$T(2,2) = (2 - 2, \; 2(2)^2 - 2^2) = (0, 4)$$



### 2. Transformation of the Sum

Adding the input vectors first: $(1,1) + (2,2) = (3,3)$

* $$T(3,3) = (3 - 3, \; 2(3)^2 - 3^2) = (0, 9)$$



### 3. Verification of Additivity Failure

Now, compare $T(u+v)$ with $T(u) + T(v)$:

* $$T(1,1) + T(2,2) = (0,1) + (0,4) = (0, 5)$$


* $$T(1,1) + (2,2)) = (0, 9)$$



Since $(0,9) \neq (0,5)$, we conclude:

$$T((1,1) + (2,2)) \neq T(1,1) + T(2,2)$$

Hence, the transformation is **not a linear map**.



---

## The Matrix of a Linear Map

Suppose $V(F)$ and $W(F)$ are finite dimensional vector spaces with bases $\{v_1, v_2, \dots, v_n\}$ and $\{w_1, w_2, \dots, w_m\}$ respectively. Let $T : V \longrightarrow W$ be a linear map.

Then the matrix of $T$, with entries $a_{ij} \in F$, is defined by:

$$T(v_j) = a_{1j}w_1 + a_{2j}w_2 + \dots + a_{mj}w_m$$

$$\text{for } j = 1, 2, 3, \dots, n$$

### Key Insight

It shows that the $j^{\text{th}}$ column of the matrix $A$ of linear map $T$ consists of the coordinates of $T(v_j)$ in the chosen basis for $W$.

### Converse Property

Conversely, every matrix $A \in \mathbb{R}^{m \times n}$ induces a linear map $T : \mathbb{R}^n \longrightarrow \mathbb{R}^m$ given by:

$$T(v) = Av$$





---

## Examples of Matrix of a Linear Map

### Problem

Consider a linear map $T : \mathbb{R}^2 \longrightarrow \mathbb{R}^2$ defined by:


$$T(x_1, x_2) = (2x_1 - 7x_2, \; 4x_1 + 3x_2)$$

Find the matrix representation of $T$ relative to the basis $B = \{(1,3), (2,5)\}$.

---

### Solution Breakdown

To find the matrix representation relative to a non-standard basis $B = \{v_1, v_2\}$, we must follow three primary steps:

1. Compute the image of each basis vector under $T$.
2. Express these image vectors as a linear combination of the original basis vectors in $B$.
3. Arrange the resulting coefficients into the columns of our coordinate matrix $A$.

#### Step 1: Compute $T(v_1)$ and $T(v_2)$

Substitute the components of the basis vectors into the transformation formula:

* **For $v_1 = (1,3)$:**

$$T(1,3) = (2(1) - 7(3), \; 4(1) + 3(3)) = (2 - 21, \; 4 + 9) = (-19, 13)$$


* **For $v_2 = (2,5)$:**

$$T(2,5) = (2(2) - 7(5), \; 4(2) + 3(5)) = (4 - 35, \; 8 + 15) = (-31, 23)$$



---

#### Step 2: Set up the Coordinate Systems

We express these transformations as combinations of our basis vectors using scalar unknowns $a_{ij}$:

$$\begin{aligned}
T(1,3) &= (-19,13) = a_{11}(1,3) + a_{21}(2,5) \\
T(2,5) &= (-31,23) = a_{12}(1,3) + a_{22}(2,5)
\end{aligned}$$

---

### Step-by-Step Calculation & Verification

Let's break down the system of equations to show exactly where the final numerical matrix values come from.

#### Solving for Column 1 ($a_{11}$ and $a_{21}$)

From the vector equation $(-19, 13) = a_{11}(1, 3) + a_{21}(2, 5)$, we get two linear equations:

1. $\quad a_{11} + 2a_{21} = -19 \implies a_{11} = -19 - 2a_{21}$
2. $\quad 3a_{11} + 5a_{21} = 13$

Substitute the expression for $a_{11}$ into equation (2):


$$\begin{aligned}
3(-19 - 2a_{21}) + 5a_{21} &= 13 \\
-57 - 6a_{21} + 5a_{21} &= 13 \\
-57 - a_{21} &= 13 \\
-a_{21} &= 70 \implies \mathbf{a_{21} = -70}
\end{aligned}$$

Now substitute $a_{21} = -70$ back to find $a_{11}$:


$$a_{11} = -19 - 2(-70) = -19 + 140 \implies \mathbf{a_{11} = 121}$$

---

#### Solving for Column 2 ($a_{12}$ and $a_{22}$)

From the vector equation $(-31, 23) = a_{12}(1, 3) + a_{22}(2, 5)$, we form another system:
3) $\quad a_{12} + 2a_{22} = -31 \implies a_{12} = -31 - 2a_{22}$
4) $\quad 3a_{12} + 5a_{22} = 23$

Substitute the expression for $a_{12}$ into equation (4):


$$\begin{aligned}
3(-31 - 2a_{22}) + 5a_{22} &= 23 \\
-93 - 6a_{22} + 5a_{22} &= 23 \\
-93 - a_{22} &= 23 \\
-a_{22} &= 116 \implies \mathbf{a_{22} = -116}
\end{aligned}$$

Now substitute $a_{22} = -116$ back to find $a_{12}$:


$$a_{12} = -31 - 2(-116) = -31 + 232 \implies \mathbf{a_{12} = 201}$$

---

### Final Representation

Arranging the coefficients into columns ($a_{11}, a_{21}$ as column 1, and $a_{12}, a_{22}$ as column 2):

$$A = \begin{pmatrix} a_{11} & a_{12} \\ a_{21} & a_{22} \end{pmatrix} = \begin{pmatrix} 121 & 201 \\ -70 & -116 \end{pmatrix}$$



Here is the content of the image formatted using clean Markdown and LaTeX, along with a clearly framed question, step-by-step simplification, and a detailed conceptual explanation.

---

## Matrix Transformation from $\mathbb{R}^n$ to $\mathbb{R}^m$

### Problem Statement

Given the matrix:


$$A = \begin{bmatrix} 2 & 1 \\ 4 & 3 \end{bmatrix}$$

1. Find the explicit formula for the linear transformation $T(x_1, x_2) = Ax$ induced by this matrix.
2. Determine the domain and codomain spaces, and explain the relationship between the dimensions of the vector spaces and the size of the matrix.

---

### Step-by-Step Simplification & Solution

#### 1. Computing the Transformation Formula

To find the algebraic formula for $T(x_1, x_2)$, we multiply the matrix $A$ by a generic column vector $x = \begin{bmatrix} x_1 \\ x_2 \end{bmatrix}$ using standard matrix multiplication:

$$T(x_1, x_2) = \begin{bmatrix} 2 & 1 \\ 4 & 3 \end{bmatrix} \begin{bmatrix} x_1 \\ x_2 \end{bmatrix}$$

Multiply the rows of the matrix by the column vector:

* **First component (Row 1):** 
$$(2 \cdot x_1) + (1 \cdot x_2) = 2x_1 + x_2$$


* **Second component (Row 2):** 
$$(4 \cdot x_1) + (3 \cdot x_2) = 4x_1 + 3x_2$$



Putting it together as a coordinate vector:


$$T(x_1, x_2) = (2x_1 + x_2, \; 4x_1 + 3x_2)$$

---

### Detailed Conceptual Explanation

#### The General Mapping Rule

As indicated by the handwritten notes at the bottom of the image, there is a fundamental link between linear maps and matrix dimensions:

$$T: \mathbb{R}^n \longrightarrow \mathbb{R}^m \implies [\text{Matrix Representation}]_{m \times n}$$

* **$n$ (Number of columns):** Represents the dimension of the **domain** ($\mathbb{R}^n$). It tells you how many input variables your transformation expects.
* **$m$ (Number of rows):** Represents the dimension of the **codomain** ($\mathbb{R}^m$). It tells you how many output coordinates your transformation produces.

#### Applying the Rule to this Example

In your specific problem, the handwritten arrow highlights the mapping $T: \mathbb{R}^2 \longrightarrow \mathbb{R}^2$:

* The input vector $(x_1, x_2)$ belongs to $\mathbb{R}^2$ ($n = 2$ variables $\implies 2$ matrix columns).
* The output vector $(2x_1 + x_2, \; 4x_1 + 3x_2)$ also belongs to $\mathbb{R}^2$ ($m = 2$ output components $\implies 2$ matrix rows).

Because $m = 2$ and $n = 2$, the resulting transformation matrix is a square matrix of size $2 \times 2$.


---

## Nullspace and Range of a Linear Map

Let $T : V \longrightarrow W$ be a linear map.

* **Nullspace (Kernel):** The set of all vectors in the domain $V$ that map to the zero vector in $W$.

$$\text{null}(T) = \{v \in V \mid T(v) = 0\}$$


* **Range (Image):** The set of all vectors in the codomain $W$ that are hit by at least one vector from $V$.

$$\text{range}(T) = \{w \in W \mid \exists v \in V \text{ s.t. } T(v) = w\}$$



### Remarks

* The nullspace of $T$ is also called the **kernel** of $T$, denoted by $\text{ker}(T)$.
* $\text{null}(T)$ is a subspace of the domain $V$.
* $\text{range}(T)$ is a subspace of the codomain $W$.
* The dimension of $\text{null}(T)$ is called the **nullity** of $T$.
* The dimension of $\text{range}(T)$ is called the **rank** of $T$.

---

## Practical Example with Step-by-Step Solving

Let's find the basis and dimension for both the nullspace and range of a specific linear map.

### Problem

Consider the linear transformation $T : \mathbb{R}^3 \longrightarrow \mathbb{R}^2$ represented by the standard matrix:


$$A = \begin{bmatrix} 1 & 2 & 3 \\ 2 & 4 & 6 \end{bmatrix}$$

---

### Part 1: Finding the Nullspace, Basis, and Nullity

#### Step 1: Set up the homogeneous system

By definition, the nullspace consists of all vectors $x = \begin{bmatrix} x_1 \\ x_2 \\ x_3 \end{bmatrix}$ such that $Ax = 0$:

$$\begin{bmatrix} 1 & 2 & 3 \\ 2 & 4 & 6 \end{bmatrix} \begin{bmatrix} x_1 \\ x_2 \\ x_3 \end{bmatrix} = \begin{bmatrix} 0 \\ 0 \end{bmatrix}$$

#### Step 2: Row reduce the matrix (RREF)

Apply the row operation $R_2 \to R_2 - 2R_1$:

$$\begin{bmatrix} 1 & 2 & 3 \\ 0 & 0 & 0 \end{bmatrix}$$

#### Step 3: Identify pivot and free variables

* **Pivot variable:** $x_1$ (column 1 has the leading 1).
* **Free variables:** $x_2$ and $x_3$ (columns 2 and 3 do not have pivots).

Let $x_2 = s$ and $x_3 = t$, where $s, t \in \mathbb{R}$.

#### Step 4: Write the general solution in vector form

From the first row: $x_1 + 2x_2 + 3x_3 = 0 \implies x_1 = -2s - 3t$.

$$\begin{bmatrix} x_1 \\ x_2 \\ x_3 \end{bmatrix} = \begin{bmatrix} -2s - 3t \\ s \\ t \end{bmatrix} = s \begin{bmatrix} -2 \\ 1 \\ 0 \end{bmatrix} + t \begin{bmatrix} -3 \\ 0 \\ 1 \end{bmatrix}$$

#### Step 5: Conclude Basis and Nullity

* **Basis for $\text{null}(T)$:** $\left\{ \begin{bmatrix} -2 \\ 1 \\ 0 \end{bmatrix}, \begin{bmatrix} -3 \\ 0 \\ 1 \end{bmatrix} \right\}$
* **Nullity (Dimension):** $2$

---

### Part 2: Finding the Range, Basis, and Rank

#### Step 1: Use the column space concept

The range of a linear transformation is exactly equal to the span of the columns of its standard matrix $A$:

$$\text{range}(T) = \text{span} \left\{ \begin{bmatrix} 1 \\ 2 \end{bmatrix}, \begin{bmatrix} 2 \\ 4 \end{bmatrix}, \begin{bmatrix} 3 \\ 6 \end{bmatrix} \right\}$$

#### Step 2: Identify linearly independent columns

Look back at the row reduced matrix from Part 1:


$$\begin{bmatrix} \mathbf{1} & 2 & 3 \\ \mathbf{0} & 0 & 0 \end{bmatrix}$$

Only the **first column** contains a pivot. This means only the first column of the *original* matrix is needed to form a basis; the other columns are just multiples of it ($2 \cdot \text{Col 1}$ and $3 \cdot \text{Col 1}$).

#### Step 3: Conclude Basis and Rank

* **Basis for $\text{range}(T)$:** $\left\{ \begin{bmatrix} 1 \\ 2 \end{bmatrix} \right\}$
* **Rank (Dimension):** $1$

---

### Quick Verification: The Rank-Nullity Theorem

A great way to check your work is to verify that your dimensions sum up correctly to the dimension of the domain space ($\mathbb{R}^3$):

$$\text{Rank}(T) + \text{Nullity}(T) = \text{Dimension of Domain}$$

$$1 + 2 = 3 \quad \checkmark$$



---

## Rank-Nullity Theorem

For a linear map $T : V \longrightarrow W$, we have:

$$\dim(\text{range}(T)) + \dim(\text{null}(T)) = \dim(V)$$

In other terms:


$$\text{Rank}(T) + \text{Nullity}(T) = \text{Dimension of Domain}$$

---

## Example Problem

**Determine the basis for the range and nullspace of the linear map $T : \mathbb{R}^3 \longrightarrow \mathbb{R}^4$ defined by:**


$$T(x_1, x_2, x_3) = (x_1 - x_2 + x_3, \; x_2 - x_3, \; x_1, \; 2x_1 - 5x_2 + 5x_3)$$

---

## Step-by-Step Solution

### Step 1: Construct the Standard Matrix $A$

To easily solve for both spaces, we express the transformation as a matrix $A$ such that $T(x) = Ax$. We extract the coefficients of $x_1, x_2,$ and $x_3$ for each row:

$$A = \begin{bmatrix} 1 & -1 & 1 \\ 0 & 1 & -1 \\ 1 & 0 & 0 \\ 2 & -5 & 5 \end{bmatrix}$$

---

### Step 2: Reduce to Row Echelon Form (REF)

We perform elementary row operations to find the pivot positions:

1. Eliminate the leading entry in Row 3 ($R_3 \to R_3 - R_1$) and Row 4 ($R_4 \to R_4 - 2R_1$):

$$\begin{bmatrix} 1 & -1 & 1 \\ 0 & 1 & -1 \\ 0 & 1 & -1 \\ 0 & -3 & 3 \end{bmatrix}$$


2. Eliminate the entries in Column 2 below the second row pivot ($R_3 \to R_3 - R_2$) and ($R_4 \to R_4 + 3R_2$):

$$\begin{bmatrix} \mathbf{1} & -1 & 1 \\ 0 & \mathbf{1} & -1 \\ 0 & 0 & 0 \\ 0 & 0 & 0 \end{bmatrix}$$



This is the Row Echelon Form of our matrix.

---

### Step 3: Finding the Basis for $\text{Range}(T)$

The range (column space) is spanned by the columns of the **original matrix** that correspond to the pivot columns in the row-reduced matrix.

* Looking at the reduced matrix, the pivots are in **Column 1** and **Column 2**.
* We select Column 1 and Column 2 from the *original* matrix $A$:

$$\text{Basis for Range}(T) = \left\{ \begin{bmatrix} 1 \\ 0 \\ 1 \\ 2 \end{bmatrix}, \begin{bmatrix} -1 \\ 1 \\ 0 \\ -5 \end{bmatrix} \right\}$$

*(Note: Written in horizontal vector notation as in your snippet: $\text{Range}(T) = \{(1,0,1,2), (1,-1,0,5)\}$, multiplying the second vector by $-1$ preserves the exact same span line).*

* **$\dim(\text{range}(T)) = 2$**

---

### Step 4: Finding the Basis for $\text{Nullspace}(T)$

To find the nullspace, we solve the homogeneous system $Ax = 0$ using our reduced matrix:

$$\begin{aligned}
1x_1 - 1x_2 + 1x_3 &= 0 \\
1x_2 - 1x_3 &= 0
\end{aligned}$$

1. **Identify Variables:**
* $x_1, x_2$ are pivot variables.
* $x_3$ is a free variable. Let $x_3 = t$.


2. **Solve Backwards:**
* From Row 2: $x_2 - t = 0 \implies x_2 = t$
* From Row 1: $x_1 - (t) + t = 0 \implies x_1 = 0$


3. **Vector Form:**

$$\begin{bmatrix} x_1 \\ x_2 \\ x_3 \end{bmatrix} = \begin{bmatrix} 0 \\ t \\ t \end{bmatrix} = t \begin{bmatrix} 0 \\ 1 \\ 1 \end{bmatrix}$$



$$\text{Basis for Nullspace}(T) = \left\{ \begin{bmatrix} 0 \\ 1 \\ 1 \end{bmatrix} \right\}$$

In coordinate form: $\text{Nullspace}(T) = \{(0,1,1)\}$

* **$\dim(\text{null}(T)) = 1$**

---

### Step 5: Verify via the Rank-Nullity Theorem

$$\begin{aligned}
\dim(\text{range}(T)) + \dim(\text{null}(T)) &= \dim(V) \\
2 + 1 &= 3
\end{aligned}$$

Since $\dim(\mathbb{R}^3) = 3$, the calculations perfectly satisfy the theorem!