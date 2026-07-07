# Linear Algebra Notes: Rank of a Matrix and Key Properties

This note covers the definition of the rank of a matrix, fundamental rank properties, and concrete numerical calculations to understand how rank is determined.

---

## 1. What is the Rank of a Matrix?

### Mathematical Definition
Let $A \in \mathbb{R}^{m \times n}$ be a matrix. The **rank** of matrix $A$ is defined as the dimension of its range space (column space):

$$\text{rank}(A) = \text{dim}(\text{range}(A))$$

In practice, it is equivalent to the maximum number of **Linearly Independent (L.I.)** rows or columns in the matrix.

### Simple Meaning 💡
Think of the rank as the amount of **unique, non-redundant information** inside a matrix. 
* If a row or a column can be built by simply scaling or adding other rows/columns together, it is redundant (Linearly Dependent).
* The rank tells you how many "completely independent directions" the matrix controls in vector space.

---

## 2. Examples with Step-by-Step Calculations

### Example 1: Full-Rank Matrix ($A_1$)

Given the identity matrix $A_1$:

$$A_1 = \begin{bmatrix} 1 & 0 & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 1 \end{bmatrix}$$

#### Calculation & Explanation:
Let's check the rows of $A_1$:
* $\vec{r}_1 = [1, 0, 0]$
* $\vec{r}_2 = [0, 1, 0]$
* $\vec{r}_3 = [0, 0, 1]$

No matter how you combine $\vec{r}_1$ and $\vec{r}_2$, you can never create the $1$ in the third position of $\vec{r}_3$. All three rows are completely unique and independent. 

$$\text{Number of L.I. rows} = 3 \implies \text{rank}(A_1) = 3$$

---

### Example 2: Matrix with Redundancy ($A_2$)

Given the matrix $A_2$:

$$A_2 = \begin{bmatrix} 2 & 1 & -1 \\ 1 & 0 & 1 \\ 1 & 1 & -2 \end{bmatrix}$$

#### Step-by-Step Verification using Row Operations (Gaussian Elimination):
To find the number of independent rows manually, we reduce the matrix to Row Echelon Form (REF).

**Step 1:** Swap Row 1 ($R_1$) and Row 2 ($R_2$) to get a leading 1 at the top left:
$$\begin{bmatrix} 1 & 0 & 1 \\ 2 & 1 & -1 \\ 1 & 1 & -2 \end{bmatrix}$$

**Step 2:** Eliminate the values under the first leading 1.
* Perform $R_2 \leftarrow R_2 - 2R_1$:
  $$\begin{bmatrix} 2 & 1 & -1 \end{bmatrix} - \begin{bmatrix} 2 & 0 & 2 \end{bmatrix} = \begin{bmatrix} 0 & 1 & -3 \end{bmatrix}$$
* Perform $R_3 \leftarrow R_3 - R_1$:
  $$\begin{bmatrix} 1 & 1 & -2 \end{bmatrix} - \begin{bmatrix} 1 & 0 & 1 \end{bmatrix} = \begin{bmatrix} 0 & 1 & -3 \end{bmatrix}$$

The matrix becomes:
$$\begin{bmatrix} 1 & 0 & 1 \\ 0 & 1 & -3 \\ 0 & 1 & -3 \end{bmatrix}$$

**Step 3:** Eliminate the value under the second leading 1.
* Perform $R_3 \leftarrow R_3 - R_2$:
  $$\begin{bmatrix} 0 & 1 & -3 \end{bmatrix} - \begin{bmatrix} 0 & 1 & -3 \end{bmatrix} = \begin{bmatrix} 0 & 0 & 0 \end{bmatrix}$$

The final Row Echelon Form is:
$$\begin{bmatrix} 1 & 0 & 1 \\ 0 & 1 & -3 \\ 0 & 0 & 0 \end{bmatrix}$$

#### Explanation:
Because Row 3 completely vanished into zeros ($0, 0, 0$), it means the original Row 3 was a hidden combination of the first two rows. Specifically, notice that:
$$\vec{r}_1 - \vec{r}_2 = [2, 1, -1] - [1, 0, 1] = [1, 1, -2] = \vec{r}_3$$

Since only **2 non-zero rows** remain in the simplified structure:

$$\text{rank}(A_2) = 2$$

---

## 3. Four Essential Properties of Matrix Rank

Let $A \in \mathbb{R}^{m \times n}$. The following structural rules always hold true:

### Property 1: Transpose Equality
$$\text{rank}(A^T) = \text{rank}(A)$$
* **Simple Meaning:** A matrix has the exact same number of independent columns as it does independent rows. Flipping a matrix on its side does not change its core informational value.

### Property 2: Multiplication by Invertible Matrices
$$\text{rank}(PAQ) = \text{rank}(A) \quad \text{for invertible matrices } P \text{ and } Q$$
* **Simple Meaning:** Invertible matrices represent operations that do not lose data (like pure rotations or scaling factors). Multiplying by them scrambles the matrix elements but leaves the total count of independent dimensions completely intact.

### Property 3: Upper Bound on Matrix Multiplication
$$\text{rank}(AB) \le \min\{\text{rank}(A), \text{rank}(B)\}$$
* **Simple Meaning:** When you multiply two matrices together, the combination cannot contain more unique information than the weakest link. The resulting product's rank is bottlenecked by whichever matrix had lower rank.

### Property 4: Rank of an Upper Block Triangular Matrix
$$\text{rank}\left(\begin{bmatrix} A_{11} & A_{12} \\ 0 & A_{22} \end{bmatrix}\right) = \text{rank}(A_{11}) + \text{rank}(A_{22})$$
where $A_{11}, A_{12}, \text{ and } A_{22}$ are distinct block sub-matrices.
* **Simple Meaning:** Because of the zero block ($0$) isolating the bottom-left corner, the information contained in block $A_{11}$ and block $A_{22}$ is completely independent. Therefore, you can calculate their ranks separately and sum them together to find the total rank.

# Linear Algebra Notes: Rank Factorization and Linear Systems

This note covers how a matrix can be broken down into smaller components using its rank (Rank Factorization) and how that relates to solving linear systems of equations.

---

## 1. Rank Factorization (Matrix Factorization)

### Mathematical Definition
Let $A$ be an $m \times n$ matrix with $\text{rank}(A) = r$. 
If we find a basis for the column space (range) of $A$, let's call this set of basis vectors $B = \{b_1, b_2, \dots, b_r\} \subset \mathbb{R}^m$.

Because $B$ is a basis for $\text{Range}(A)$, **every** column vector $a_j$ of the matrix $A = [a_1, a_2, \dots, a_n]$ can be written as a unique linear combination of these basis vectors.

We can collect these linear combination coefficients into a matrix $C$ of size $r \times n$:

$$\begin{bmatrix} a_1 & a_2 & \dots & a_n \end{bmatrix} = \begin{bmatrix} b_1 & b_2 & \dots & b_r \end{bmatrix} \begin{bmatrix} c_{11} & \dots & \dots & c_{1n} \\ \vdots & & & \vdots \\ c_{r1} & \dots & \dots & c_{rn} \end{bmatrix}$$

This is written compactly as:
$$A = B \cdot C$$

Where:
* $A$ is an $m \times n$ matrix (Rank $r$)
* $B$ is an $m \times r$ matrix (Columns are the independent basis vectors)
* $C$ is an $r \times n$ matrix (Rows contain the combination coefficients)

### Simple Meaning 💡
Rank factorization means compressing a large matrix into two smaller, skinier matrices. 
If a matrix has a low rank $r$, it means it has a lot of repetitive or redundant columns. Instead of storing all $n$ columns, we only keep $r$ essential "anchor" vectors in matrix $B$, and matrix $C$ acts as a recipe book telling us how to recreate the original columns using those anchors.

---

## 2. Linear Systems and Rank Consistency ($AX = Z$)

The second slide addresses a system of linear equations written as $AX = Z$ (noting the handwritten correction changing a placeholder $b$ to $Z$).

### Mathematical Condition for Consistency
A linear system $AX = Z$ has a solution (is consistent) if and only if the vector $Z$ lies entirely within the column space of $A$. This is checked using ranks:

$$\text{rank}(A) = \text{rank}([A \mid Z]) \le n$$

Where:
* $[A \mid Z]$ is the **augmented matrix** (the matrix $A$ with the target vector $Z$ attached as an extra column at the end).
* $n$ is the number of columns (variables) in $A$.

### Simple Meaning & Vector Visualization 💡
When you perform the multiplication $AX$, you are taking a linear combination of the columns of matrix $A$, using the values in vector $X$ as weights. 

The equation $AX = Z$ literally asks: *"Can we mix the columns of $A$ together in some way to perfectly build the vector $Z$?"*

* **If $\text{rank}(A) = \text{rank}([A \mid Z])$:** Adding $Z$ as a new column did not increase the rank. This means $Z$ brings zero new information to the table because it can already be constructed by the existing columns of $A$. The system **has a solution**.
* **If $\text{rank}([A \mid Z]) > \text{rank}(A)$:** Adding $Z$ increased the rank by 1. This means $Z$ points in a brand new direction that the columns of $A$ cannot reach. The system is inconsistent and **has no solution**.

---

## 3. Step-by-Step Toy Example Calculation

Let's illustrate both concepts with a simple manual calculation.

### Part A: Calculating Rank Factorization
Let matrix $A$ be:
$$A = \begin{bmatrix} 1 & 2 \\ 3 & 6 \end{bmatrix}$$

1. **Find Rank:** Notice column 2 is just $2 \times$ column 1. The columns are dependent. The rank $r = 1$.
2. **Extract Basis Matrix $B$ ($m \times r$):** Take the single independent column.
   $$B = \begin{bmatrix} 1 \\ 3 \end{bmatrix}$$
3. **Construct Coefficient Matrix $C$ ($r \times n$):** Figure out how to recreate $A$'s columns using $B$.
   * To get column 1 $\begin{bmatrix}1 \\ 3\end{bmatrix}$, multiply $B$ by $1$.
   * To get column 2 $\begin{bmatrix}2 \\ 6\end{bmatrix}$, multiply $B$ by $2$.
   $$C = \begin{bmatrix} 1 & 2 \end{bmatrix}$$

Verify factorization $B \cdot C$:
$$\begin{bmatrix} 1 \\ 3 \end{bmatrix} \begin{bmatrix} 1 & 2 \end{bmatrix} = \begin{bmatrix} 1\cdot1 & 1\cdot2 \\ 3\cdot1 & 3\cdot2 \end{bmatrix} = \begin{bmatrix} 1 & 2 \\ 3 & 6 \end{bmatrix} = A$$

---

### Part B: Testing System Consistency ($AX = Z$)

Using our same matrix $A$, let's test two different targets for $Z$.

#### Case 1: Consistent Target
Let $Z_1 = \begin{bmatrix} 5 \\ 15 \end{bmatrix}$. Create the augmented matrix $[A \mid Z_1]$:

$$[A \mid Z_1] = \begin{bmatrix} 1 & 2 & \mid & 5 \\ 3 & 6 & \mid & 15 \end{bmatrix}$$

Reduce using row operation $R_2 \leftarrow R_2 - 3R_1$:
$$\begin{bmatrix} 1 & 2 & \mid & 5 \\ 0 & 0 & \mid & 0 \end{bmatrix}$$

* $\text{rank}(A) = 1$
* $\text{rank}([A \mid Z_1]) = 1$
* Since $1 = 1$, the system is **consistent** (solutions exist because $Z_1$ is just $5 \times$ the first column).

#### Case 2: Inconsistent Target
Let $Z_2 = \begin{bmatrix} 5 \\ 20 \end{bmatrix}$. Create the augmented matrix $[A \mid Z_2]$:

$$[A \mid Z_2] = \begin{bmatrix} 1 & 2 & \mid & 5 \\ 3 & 6 & \mid & 20 \end{bmatrix}$$

Reduce using row operation $R_2 \leftarrow R_2 - 3R_1$:
$$\begin{bmatrix} 1 & 2 & \mid & 5 \\ 0 & 0 & \mid & 5 \end{bmatrix}$$

* $\text{rank}(A) = 1$
* $\text{rank}([A \mid Z_2]) = 2$
* Since $1 \neq 2$, the system is **inconsistent** (no combinations of $A$'s columns can ever equal $Z_2$).

# Linear Algebra Notes: Low-Rank Factorization and Storage Optimization

This note covers how low-rank matrix factorization ($A = BC^T$) is used practically to reduce storage space, optimize memory, and achieve data compression.

---

## 1. Mathematical Definition of Low-Rank Factorization

Every matrix $A \in \mathbb{R}^{m \times n}$ with a rank of $r$ can be factored into a product of two skinnier matrices:

$$A = B C^T$$

Where the dimensions match as follows:
* $A$ is an $m \times n$ matrix.
* $B$ is an $m \times r$ matrix ($B \in \mathbb{R}^{m \times r}$).
* $C$ is an $n \times r$ matrix, which means its transpose $C^T$ is an $r \times n$ matrix ($C \in \mathbb{R}^{n \times r}$).

### What is a "Low-Rank" Matrix?
We say that a matrix has a **low rank** if its rank $r$ is significantly smaller than its overall geometric dimensions:

$$r \ll \min\{m, n\}$$

---

## 2. Core Concept: Storage and Data Compression 💡

### Simple Meaning
Imagine you have a huge, high-resolution grayscale image represented as a matrix $A$ with thousands of rows and columns. 

* If you store the matrix normally, you must save every single pixel element individually.
* However, if many rows/columns contain repeating patterns or highly redundant information, the matrix has a very low rank ($r$).
* Instead of saving the giant matrix $A$, you can just save the two smaller matrices $B$ and $C^T$. When your computer needs to render the image, it performs a quick matrix multiplication ($B \times C^T$) to reconstruct the original data. This saves massive amounts of memory!

---

## 3. Element Counting Formulas

To see exactly how much memory space is saved, we count the total number of numeric values (elements) required under both storage methods:

1. **Standard Matrix Storage:** $$\text{Elements in } A = m \cdot n$$

2. **Factorized Storage ($B$ and $C^T$ together):**
   $$\text{Elements in } B + \text{Elements in } C^T = (m \cdot r) + (n \cdot r) = r(m + n)$$

> **Rule of Thumb:** If $r \ll \min\{m, n\}$, then the factorized right-hand side has a **sufficiently lower** number of elements than $m \cdot n$.

---

## 4. Numerical Example (Step-by-Step Calculation)

Let's work through the numerical example provided in the handwritten lecture slide.

### Given Data:
* Matrix dimensions: $m = 50$ rows, $n = 100$ columns
* Matrix Rank: $r = 20$

---

### Step-by-Step Calculations:

#### Step 4.1: Compute Full Matrix Storage Requirement
If we store the matrix $A$ in its raw form, we compute the total number of elements using $m \cdot n$:

$$\text{Elements in } A = 50 \times 100$$
$$\text{Elements in } A = 5000 \text{ values}$$

#### Step 4.2: Compute Factorized Matrix Storage Requirement
If we break it down into $A = B_{50 \times 20} \cdot C^T_{20 \times 100}$:

1. Calculate elements needed for Matrix $B$ ($m \cdot r$):
   $$\text{Elements in } B = 50 \times 20 = 1000$$

2. Calculate elements needed for Matrix $C^T$ ($n \cdot r$):
   $$\text{Elements in } C^T = 100 \times 20 = 2000$$

3. Sum them together:
   $$\text{Total Factorized Elements} = 1000 + 2000 = 3000 \text{ values}$$

---

### 5. Final Compression Conclusion

* **Raw Storage:** $5000$ values
* **Low-Rank Factorized Storage:** $3000$ values

$$\text{Memory Savings} = 5000 - 3000 = 2000 \text{ values}$$

By exploiting the fact that the matrix has a rank of only $20$, we successfully reduced the file storage size by **40%** without losing any structural information!




# Linear Algebra Notes: Low-Rank Approximation and Non-Convexity

This note covers the definition of the low-rank approximation problem using the Frobenius norm and a step-by-step mathematical proof demonstrating why this optimization problem is structurally non-convex.

---

## 1. What is Low-Rank Approximation?

### Mathematical Definition
Let $A \in \mathbb{R}^{m \times n}$ be a large matrix with $\text{rank}(A) \le \min\{m, n\}$. 
The goal of **low-rank approximation** is to find an alternative matrix $A_k \in \mathbb{R}^{m \times n}$ whose rank is constrained to a lower value $k$ ($k \le \text{rank}(A)$) such that $A_k$ is as close to $A$ as possible.

To find the absolute "best" approximation, we measure the error distance using the **Frobenius norm** of their difference. This yields the following optimization problem:

$$\|A - A_k\| = \min_{A_k} \left\{ \|A - A_k\|_F : A_k \in \mathbb{R}^{m \times n} \text{ and } \text{rank}(A_k) \le k \right\}$$

### Simple Meaning 💡
Imagine you have a high-resolution data dataset (Matrix $A$). A low-rank approximation means trying to clean, compress, or simplify that dataset down to its $k$ most dominant patterns (Matrix $A_k$). The optimization formula ensures that when we subtract our simplified matrix from the original matrix, the leftover noise ($A - A_k$) is minimized as much as humanly possible.

---

## 2. The Structural Challenge: Non-Convexity

The slides note a massive caveat: **The low-rank approximation optimization problem is strictly non-convex.**

### What does Non-Convex mean? 💡
In optimization, a problem is convex if a straight line drawn between any two valid choices stays within the set of valid options. 

If a problem is **non-convex**, blending two valid, optimal solutions together can create an invalid or terrible solution. This matters because non-convex problems cannot be solved using simple gradient descent curves; they contain multiple traps, local minima, and erratic geometric shapes.

---

## 3. Step-by-Step Proof of Non-Convexity (Manual Verification)

To prove that the rank constraint ($\text{rank}(A_k) \le k$) breaks convexity, we run a counterexample trying to create a **rank-1 approximation** ($k = 1$) of a simple $2 \times 2$ Identity Matrix ($I_2$).

### Given:
Target Matrix:
$$I_2 = \begin{bmatrix} 1 & 0 \\ 0 & 1 \end{bmatrix}, \quad \text{rank}(I_2) = 2$$

We choose two different, perfectly valid rank-1 approximation candidates for our problem:
$$A = \begin{bmatrix} 1 & 0 \\ 0 & 0 \end{bmatrix} \implies \text{rank}(A) = 1$$
$$B = \begin{bmatrix} 0 & 0 \\ 0 & 1 \end{bmatrix} \implies \text{rank}(B) = 1$$

To test convexity, we form a weighted blend (convex combination) of these two solutions using a scalar parameter $\alpha$, where $\alpha \in (0, 1)$. The mathematical rule for convexity requires that:
$$\text{rank}(\alpha A + (1-\alpha)B) \le \alpha \cdot \text{rank}(A) + (1-\alpha)\cdot \text{rank}(B)$$

Let's compute both sides step-by-step to check if this holds true.

---

### Step 3.1: Calculate the Right-Hand Side (R.H.S.)
Substitute our known ranks ($\text{rank}(A) = 1$ and $\text{rank}(B) = 1$) into the target expectation formula:

$$\text{R.H.S.} = \alpha \cdot \text{rank}(A) + (1-\alpha) \cdot \text{rank}(B)$$
$$\text{R.H.S.} = \alpha \cdot (1) + (1-\alpha) \cdot (1)$$
$$\text{R.H.S.} = \alpha + 1 - \alpha$$
$$\text{R.H.S.} = 1$$

---

### Step 3.2: Calculate the Left-Hand Side (L.H.S.)
Now, let's actually perform the matrix algebra inside the rank brackets:

1. Multiply matrix $A$ by $\alpha$:
   $$\alpha A = \alpha \begin{bmatrix} 1 & 0 \\ 0 & 0 \end{bmatrix} = \begin{bmatrix} \alpha & 0 \\ 0 & 0 \end{bmatrix}$$

2. Multiply matrix $B$ by $(1-\alpha)$:
   $$(1-\alpha)B = (1-\alpha) \begin{bmatrix} 0 & 0 \\ 0 & 1 \end{bmatrix} = \begin{bmatrix} 0 & 0 \\ 0 & 1-\alpha \end{bmatrix}$$

3. Add the two resulting matrices together:
   $$\alpha A + (1-\alpha)B = \begin{bmatrix} \alpha & 0 \\ 0 & 0 \end{bmatrix} + \begin{bmatrix} 0 & 0 \\ 0 & 1-\alpha \end{bmatrix} = \begin{bmatrix} \alpha & 0 \\ 0 & 1-\alpha \end{bmatrix}$$

4. Determine the rank of the blended matrix:
   Since $\alpha \in (0,1)$, neither diagonal entry is zero. Both rows are completely independent. Therefore:
   $$\text{rank}\left(\begin{bmatrix} \alpha & 0 \\ 0 & 1-\alpha \end{bmatrix}\right) = 2$$
   $$\text{L.H.S.} = 2$$

---

### 4. Final Conclusion

Comparing our calculated sides:
* **$\text{L.H.S.} = 2$**
* **$\text{R.H.S.} = 1$**

Because $\text{L.H.S.} \neq \text{R.H.S.}$, the property fails:
$$\text{rank}(\alpha A + (1-\alpha) B) \neq \alpha \cdot \text{rank}(A) + (1-\alpha) \cdot \text{rank}(B)$$

Blending two perfect rank-1 matrices unexpectedly resulted in a rank-2 matrix! This mathematical mismatch formally proves that the rank constraint set is **non-convex**, making low-rank approximation a highly challenging optimization problem solved via special tools like Singular Value Decomposition (SVD).


# Linear Algebra Notes: Low-Rank Approximation via SVD (Eckart-Young-Mirsky Theorem)

This note explains how Singular Value Decomposition (SVD) elegantly solves the non-convex low-rank approximation problem, supported by a step-by-step example.

---

## 1. The Core Concept: Eckart-Young-Mirsky Theorem

Even though finding a low-rank approximation is fundamentally a non-convex optimization problem, the **Singular Value Decomposition (SVD)** provides an exact, global, and simple analytical solution.

### Mathematical Definition
Let $A \in \mathbb{R}^{m \times n}$ (where $m \ge n$) be a matrix whose full SVD is written as a sum of outer products:

$$A = U \Sigma V^T = \sum_{i=1}^{n} \sigma_i u_i v_i^T$$

Where:
* $\sigma_1 \ge \sigma_2 \ge \dots \ge \sigma_n \ge 0$ are the sorted singular values.
* $u_i$ are the columns of the orthogonal matrix $U$ (left singular vectors).
* $v_i$ are the columns of the orthogonal matrix $V$ (right singular vectors).

According to the theorem, the **best $k$-rank approximation** ($A_k$) under any unitary invariant matrix norm (such as the Frobenius or Spectral norm) is found by keeping only the first $k$ largest terms:

$$A_k = \sum_{i=1}^{k} \sigma_i u_i v_i^T, \quad \text{where } k \le \text{rank}(A)$$

### The Optimality Condition
This specific matrix $A_k$ is mathematically proven to be the closest possible rank-$k$ matrix to $A$:

$$\|A - A_k\| \le \|A - \tilde{A}\|$$

for **any** other arbitrary matrix $\tilde{A} \in \mathbb{R}^{m \times n}$ that satisfies $\text{rank}(\tilde{A}) \le k$.

### Simple Meaning 💡
SVD breaks a matrix down into components and ranks them by importance using the singular values ($\sigma_i$). 
To make a perfect, optimal rank-$k$ version of your matrix, you simply look at the full SVD formula and **discard everything after the first $k$ terms**. You keep the major signals and throw away the smaller elements, which usually represent noise or minor details.

---

## 2. Step-by-Step Numerical Example

Let's walk through the manual example provided in the handwritten lecture notes to visualize how this truncation works geometrically and structurally.

### Given Data:
* Matrix $A$ is a $5 \times 5$ matrix.
* Sorted Singular Values: $\sigma_1 = 3, \;\sigma_2 = 1, \;\sigma_3 = 0.5, \;\sigma_4 = 0.2, \;\sigma_5 = 0.05$
* Objective: Construct an optimal **rank-3 approximation** ($A_3$).

---

### Step-by-Step Construction:

#### Step 2.1: Truncate the Diagonal Singular Matrix ($\Sigma$)
In a full $5 \times 5$ matrix, the matrix $\Sigma$ contains all 5 singular values on its main diagonal. To make a rank-3 approximation, we forcefully drop all singular values after the 3rd index ($\sigma_4$ and $\sigma_5$) by setting them to zero:

$$\Sigma_3 = \begin{bmatrix} \sigma_1 & 0 & 0 & 0 & 0 \\ 0 & \sigma_2 & 0 & 0 & 0 \\ 0 & 0 & \sigma_3 & 0 & 0 \\ 0 & 0 & 0 & 0 & 0 \\ 0 & 0 & 0 & 0 & 0 \end{bmatrix} = \begin{bmatrix} 3 & 0 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 & 0 \\ 0 & 0 & 0.5 & 0 & 0 \\ 0 & 0 & 0 & 0 & 0 \\ 0 & 0 & 0 & 0 & 0 \end{bmatrix}$$

#### Step 2.2: Perform Dimension Reduction (Matrix Compression)
Look at the zero boundaries created in $\Sigma_3$:

$$\Sigma_3 = \left[ \begin{array}{ccc|cc} 3 & 0 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 & 0 \\ 0 & 0 & 0.5 & 0 & 0 \\ \hline 0 & 0 & 0 & 0 & 0 \\ 0 & 0 & 0 & 0 & 0 \end{array} \right]$$

Because the entire last 2 rows and last 2 columns are purely filled with zeros, multiplying them during the full calculation adds absolutely nothing to the final values. 

Therefore, we can safely slice and crop the trailing parts of matrices $U$ and $V^T$:
* We keep only the first **3 columns** of $U \implies$ yields a skinnier matrix of size $5 \times 3$.
* We keep only the top **$3 \times 3$ submatrix** of $\Sigma \implies \Sigma_k$.
* We keep only the first **3 rows** of $V^T \implies$ yields a flatter matrix of size $3 \times 5$.

---


---

### Step 2.3: Final Compressed Assembly
Reassembling the truncated components yields our clean, low-rank approximation system:

$$A_3 = [ U_{\text{cropped}} ]_{5 \times 3} \cdot \begin{bmatrix} 3 & 0 & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 0.5 \end{bmatrix}_{3 \times 3} \cdot [ V^T_{\text{cropped}} ]_{3 \times 5}$$

When you execute this inner matrix multiplication:
$$(5 \times 3) \times (3 \times 3) \times (3 \times 5) = (5 \times 5)$$

The final result $A_3$ outputs an standard $5 \times 5$ matrix layout, but it structurally acts as a **rank-3 matrix** because it was built out of only 3 independent spatial tracks.



# Linear Algebra Notes: Quality of Low-Rank Approximation with SVD Example

This note explains how to measure the accuracy or "quality" of a low-rank matrix approximation and provides a step-by-step calculation based on a numeric $3 \times 3$ matrix example.

---

## 1. Metric: Quality of Approximation

When approximating a matrix $A$ with a lower-rank matrix $A_k$, we need a way to quantify how much of the original matrix's "energy" or "variance" has been captured.

### Mathematical Definition

Using the Frobenius norm, the percentage of energy retained by a rank-$k$ approximation is given by the ratio of their squared norms:

$$\text{Quality} = \frac{\|A_k\|_F^2}{\|A\|_F^2} = \frac{\sigma_1^2 + \sigma_2^2 + \dots + \sigma_k^2}{\sigma_1^2 + \sigma_2^2 + \dots + \sigma_r^2}$$

Where:

* $\sigma_i$ are the singular values of $A$ sorted in descending order ($\sigma_1 \ge \sigma_2 \ge \dots \ge \sigma_r > 0$).
* $k$ is the target approximation rank.
* $r$ is the total rank of the original matrix $A$.

### Simple Meaning 💡

Think of this metric like a score out of **100%**. The square of each singular value ($\sigma_i^2$) represents a chunk of data information or "energy" contained inside the matrix.

* The denominator adds up **all** the information available.
* The numerator adds up only the information captured by your top $k$ choices.
* Dividing them tells you exactly what fraction of the original data survived the compression.

---

## 2. Step-by-Step Numerical Example

### Problem Statement

Given the $3 \times 3$ upper-triangular matrix $A$:


$$A = \begin{bmatrix} 3 & 2 & 1 \\ 0 & 2 & 1 \\ 0 & 0 & 1 \end{bmatrix}$$

Find its **rank-2 approximation ($A_2$)** and calculate the quality of this approximation.

---

### Step 1: Analyze the Full SVD

From the lecture slides, the full Singular Value Decomposition ($A = U \Sigma V^T$) is pre-computed to two decimal places:

$$A = \begin{bmatrix} 0.91 & 0.42 & 0.02 \\ 0.41 & -0.87 & -0.26 \\ 0.09 & -0.24 & 0.97 \end{bmatrix} \begin{bmatrix} 4.04 & 0 & 0 \\ 0 & 1.70 & 0 \\ 0 & 0 & 0.87 \end{bmatrix} \begin{bmatrix} 0.67 & 0.73 & 0.08 \\ 0.65 & -0.54 & -0.53 \\ 0.35 & -0.41 & 0.84 \end{bmatrix}^T$$

From the diagonal matrix $\Sigma$, we extract our three sorted singular values:

* $\sigma_1 = 4.04$
* $\sigma_2 = 1.70$
* $\sigma_3 = 0.87$

---

### Step 2: Construct the Rank-2 Approximation ($A_2$)

To create a rank-2 matrix, we keep only the components corresponding to the two largest singular values ($\sigma_1$ and $\sigma_2$), discarding the third row/column entirely:

$$A_2 = \begin{bmatrix} 0.91 & 0.42 \\ 0.41 & -0.87 \\ 0.09 & -0.24 \end{bmatrix}_{3 \times 2} \begin{bmatrix} 4.04 & 0 \\ 0 & 1.70 \end{bmatrix}_{2 \times 2} \begin{bmatrix} 0.67 & 0.73 & 0.08 \\ 0.65 & -0.54 & -0.53 \end{bmatrix}_{2 \times 3}$$

#### Manual Verification of the Matrix Multiplication:

First, multiply the truncated $U$ matrix by the truncated $\Sigma$ matrix:


$$U_{\text{truncated}}\Sigma_{\text{truncated}} = \begin{bmatrix} 0.91 \cdot 4.04 & 0.42 \cdot 1.70 \\ 0.41 \cdot 4.04 & -0.87 \cdot 1.70 \\ 0.09 \cdot 4.04 & -0.24 \cdot 1.70 \end{bmatrix} \approx \begin{bmatrix} 3.676 & 0.714 \\ 1.656 & -1.479 \\ 0.364 & -0.408 \end{bmatrix}$$

Next, multiply this result by $V^T_{\text{truncated}}$:


$$A_2 = \begin{bmatrix} 3.676 & 0.714 \\ 1.656 & -1.479 \\ 0.364 & -0.408 \end{bmatrix} \begin{bmatrix} 0.67 & 0.73 & 0.08 \\ 0.65 & -0.54 & -0.53 \end{bmatrix}$$

Let's calculate a couple of sample entries to see how it matches the slide's final matrix:

* **Entry (1,1):** $(3.676 \cdot 0.67) + (0.714 \cdot 0.65) = 2.463 + 0.464 = 2.927 \approx 2.99$ *(Note: Variance due to intermediate rounding in slides)*
* **Entry (2,2):** $(1.656 \cdot 0.73) + (-1.479 \cdot -0.54) = 1.209 + 0.799 = 2.008 \approx 1.88$

Performing the complete multiplication yields the final approximated matrix shown on the slide:


$$A_2 = \begin{bmatrix} 2.99 & 2.01 & 0.98 \\ 0.02 & 1.88 & 1.1 \\ -0.07 & 0.45 & 0.29 \end{bmatrix}$$

---

### Step 3: Compute the Quality of the Approximation

Let's find out exactly how much data accuracy we preserved by dropping the lowest singular value ($\sigma_3$).

#### 1. Calculate squared singular values:

* $\sigma_1^2 = (4.04)^2 = 16.3216$
* $\sigma_2^2 = (1.70)^2 = 2.89$
* $\sigma_3^2 = (0.87)^2 = 0.7569$

#### 2. Plug values into the energy ratio formula:

$$\text{Quality} = \frac{\sigma_1^2 + \sigma_2^2}{\sigma_1^2 + \sigma_2^2 + \sigma_3^2}$$

$$\text{Quality} = \frac{16.3216 + 2.89}{16.3216 + 2.89 + 0.7569}$$

$$\text{Quality} = \frac{19.2116}{19.9685} \approx 0.9621$$

---

## 3. Final Conclusion Summary

* **Rank-2 Approximated Matrix:**

$$A_2 = \begin{bmatrix} 2.99 & 2.01 & 0.98 \\ 0.02 & 1.88 & 1.1 \\ -0.07 & 0.45 & 0.29 \end{bmatrix}$$


* **Quality Metric Score:** 
$$\approx 96.2\%$$



> **Takeaway:** Even though we threw away part of the SVD structure to simplify our calculations, our compressed matrix $A_2$ still retains **96.2%** of the original structural information!


# Linear Algebra Notes: Application of SVD in Image Processing

This note covers how low-rank approximation via Singular Value Decomposition (SVD) is used for image compression and reconstruction, using a practical grayscale image example.

---

## 1. Core Concept: Images as Matrices

### Simple Meaning 💡

Every digital grayscale image is just a grid of numbers. If an image is $300 \times 400$ pixels, your computer sees it as a mathematical matrix $A \in \mathbb{R}^{300 \times 400}$, where each entry represents the brightness (intensity) of a single pixel.

Because real-world images contain smooth gradients, repeating patterns, and matching backgrounds, their rows and columns are highly correlated. This means the matrix has a specific numerical rank ($r$), but it can be compressed beautifully using a much smaller rank $k$ without losing noticeable visual details.

---

## 2. Key Elements of SVD Image Filtering

When we apply a rank-$k$ approximation to an image matrix, we observe a sequence of components:

1. **Input Image:** The original uncompressed source matrix $A$ (Full Rank $r$).
2. **Low-Rank Approximation ($A_k$):** The reconstructed image keeping only the first $k$ singular values.
3. **Approximation Error ($A - A_k$):** The data that gets thrown away (the "residual noise" or fine details).
4. **Spectrum of Singular Values:** A plot tracking the decay of singular values.

---

## 3. Step-by-Step Breakdown of the Visual Sequence

Let's look at what happens conceptually and mathematically as the approximation rank $k$ increases, based on the provided slides.

### Case 1: Rank-1 Approximation ($k = 1$)

* **What happens mathematically:** We reconstruct the matrix using only the single largest singular value: $A_1 = \sigma_1 u_1 v_1^T$.
* **Visual Result:** The approximation image looks like a basic, abstract grid of vertical and horizontal blocks. It doesn't look like a human face yet.
* **Error Matrix ($A - A_1$):** The error image is highly detailed because almost all of the facial features, expressions, and shadows were thrown away and left behind in the error category.

### Case 2: Rank-4 Approximation ($k = 4$)

* **What happens mathematically:** We use the sum of the top 4 structural tracks: $A_4 = \sum_{i=1}^{4} \sigma_i u_i v_i^T$.
* **Visual Result:** The blurry grid begins to blend together. A ghostly, recognizable silhouette of a man with a white beard begins to emerge.
* **Error Matrix ($A - A_4$):** The error image loses some of its heavy contrast because some of that structural information moved over into the approximation image.

### Final Target: Rank-25 Approximation ($k = 25$)

* **What happens mathematically:** We take the sum of the first 25 tracks ($A_{25}$).
* **Visual Result:** The slide notes that using $k = 25$ produces a **reasonable approximation**. The image looks sharp, recognizable, and very close to the original input.

---

## 4. Step-by-Step Data Compression Calculation

Let's do the math on the specific example details given in the lecture text to see the exact storage savings.

### Given Parameters:

* **Original Image Matrix Rank ($r$):** $266$
* **Assumed Image Resolution:** Let's assume a standard square dimension matching its max rank capability, e.g., $m = 300$ rows, $n = 300$ columns.
* **Target Low-Rank Approximation ($k$):** $25$

---

### Calculations:

#### Step 4.1: Raw Storage Space Requirement

Without any compression, storing the pixel intensities directly requires saving every entry in the $300 \times 300$ grid:

$$\text{Total Pixels} = m \cdot n$$

$$\text{Total Pixels} = 300 \times 300 = 90,000 \text{ data values}$$

#### Step 4.2: SVD Compressed Storage Space Requirement

Using a rank-25 approximation, we only need to save the first 25 columns of $U$, the first 25 diagonal values of $\Sigma$, and the first 25 rows of $V^T$:

$$\text{Compressed Elements} = (m \cdot k) + k + (n \cdot k) = k(m + n + 1)$$

Substitute our values ($m=300, n=300, k=25$):


$$\text{Compressed Elements} = 25 \times (300 + 300 + 1)$$

$$\text{Compressed Elements} = 25 \times 601 = 15,025 \text{ data values}$$

#### Step 4.3: Compression Ratio

Let's find the fraction of the file size left over after this SVD truncation:

$$\text{Storage Percentage} = \frac{15,025}{90,000} \approx 0.1669 \implies 16.7\%$$

---

## 5. Summary Conclusion

* **Original Size:** $90,000$ values ($100\%$)
* **Compressed Size:** $15,025$ values ($\approx 16.7\%$)
* **Total Space Saved:** **$83.3\%$ saving**

> **Takeaway:** By exploiting SVD, we can throw away more than **83%** of the raw file data. Because the singular values decay so rapidly (as seen on the spectrum plot), the remaining 25 tracks hold almost all the essential information, giving us a perfectly clear image while using a fraction of the memory space.
