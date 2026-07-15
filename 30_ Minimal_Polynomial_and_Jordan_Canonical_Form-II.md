# Linear Algebra: Jordan Canonical Form (JCF) & Generalized Eigenvectors

When an $n \times n$ matrix does not have enough linearly independent eigenvectors, it cannot be diagonalized. In such cases, we find its **Jordan Canonical Form (JCF)**, which is the closest thing to a diagonal matrix. To do this, we use **generalized eigenvectors**.

---

## 1. Core Concepts & Definitions

### What is a Generalized Eigenvector?
For a standard eigenvector, we solve $(A - \lambda I)x = 0$. If a matrix is defective (meaning the geometric multiplicity of an eigenvalue is strictly less than its algebraic multiplicity), we cannot find enough standard eigenvectors to span the space. 

Instead, we look for a non-zero vector $x$ that satisfies:
$$(A - \lambda I)^p x = 0$$
for some positive integer $p$, while ensuring that $(A - \lambda I)^{p-1} x \neq 0$. Mathematically, this means $x \in \text{Ker}(A - \lambda I)^p$.

### The JCF Transformation Theorem
Every $n \times n$ matrix $A$ is similar to a Jordan Canonical Form $J$:
$$A = SJS^{-1}$$

* **$J$ (Jordan Matrix):** A block diagonal matrix where the diagonal blocks are Jordan blocks. A Jordan block has the eigenvalue $\lambda$ on the main diagonal and $1$s on the superdiagonal directly above it.
* **$S$ (Transition Matrix):** The matrix whose columns are formed by regular eigenvectors and generalized eigenvectors, carefully ordered into **Jordan chains**.

---

## 2. Step-by-Step Breakdown of the Lecture Example

Let's dissect the example presented in the final two images.

### Given Matrix
$$A = \begin{bmatrix} 1 & 1 & 0 \\ 0 & 1 & 2 \\ 0 & 0 & 3 \end{bmatrix}$$

### Step 1: Find the Eigenvalues
Since $A$ is an upper-triangular matrix, its eigenvalues are simply the elements on its main diagonal:
* $\lambda_1 = 3$ (Algebraic Multiplicity, $\text{AM} = 1$)
* $\lambda_2 = 1$ (Algebraic Multiplicity, $\text{AM} = 2$)

### Step 2: Find the Regular Eigenvectors
We calculate the eigenvectors by finding the null space ($\text{Ker}(A - \lambda I)$) for each distinct eigenvalue.

#### For $\lambda = 3$:
$$A - 3I = \begin{bmatrix} -2 & 1 & 0 \\ 0 & -2 & 2 \\ 0 & 0 & 0 \end{bmatrix}$$
Solving $(A - 3I)X_1 = 0$ yields the regular eigenvector:
$$X_1 = \begin{bmatrix} 1 \\ 2 \\ 2 \end{bmatrix}$$

#### For $\lambda = 1$:
$$A - I = \begin{bmatrix} 0 & 1 & 0 \\ 0 & 0 & 2 \\ 0 & 0 & 2 \end{bmatrix}$$
Solving $(A - I)X_2 = 0$ gives:
$$X_2 = \begin{bmatrix} 1 \\ 0 \\ 0 \end{bmatrix}$$
Since $\text{AM} = 2$ for $\lambda = 1$ but we only found **one** independent regular eigenvector ($\text{GM} = 1$), the matrix $A$ is defective and cannot be diagonalized. We must find a generalized eigenvector.

### Step 3: Find the Generalized Eigenvector for $\lambda = 1$
We look for a vector $X_3$ such that $(A - I)^2 X_3 = 0$ but $(A - I)X_3 \neq 0$.
Let's compute $(A - I)^2$:
$$(A - I)^2 = \begin{bmatrix} 0 & 1 & 0 \\ 0 & 0 & 2 \\ 0 & 0 & 2 \end{bmatrix} \begin{bmatrix} 0 & 1 & 0 \\ 0 & 0 & 2 \\ 0 & 0 & 2 \end{bmatrix} = \begin{bmatrix} 0 & 0 & 2 \\ 0 & 0 & 4 \\ 0 & 0 & 4 \end{bmatrix}$$

We want to solve $(A - I)^2 X_3 = 0$:
$$\begin{bmatrix} 0 & 0 & 2 \\ 0 & 0 & 4 \\ 0 & 0 & 4 \end{bmatrix} \begin{bmatrix} x \\ y \\ z \end{bmatrix} = \begin{bmatrix} 0 \\ 0 \\ 0 \end{bmatrix} \implies 2z = 0 \implies z = 0$$
Here, $x$ and $y$ are free variables. To construct a valid Jordan chain, we pick a vector that maps back to our standard eigenvector $X_2$ under the action of $(A - I)$, meaning $(A - I)X_3 = X_2$.
$$\begin{bmatrix} 0 & 1 & 0 \\ 0 & 0 & 2 \\ 0 & 0 & 2 \end{bmatrix} \begin{bmatrix} x \\ y \\ 0 \end{bmatrix} = \begin{bmatrix} 1 \\ 0 \\ 0 \end{bmatrix} \implies y = 1$$
Choosing $x = 0$ for simplicity, we get our generalized eigenvector:
$$X_3 = \begin{bmatrix} 0 \\ 1 \\ 0 \end{bmatrix}$$

### Step 4: Construct Matrices $S$ and $J$
We arrange the columns of $S$ such that the Jordan chain vectors are placed side-by-side: $S = [X_1 \mid X_2 \mid X_3]$.

$$S = \begin{bmatrix} 1 & 1 & 0 \\ 2 & 0 & 1 \\ 2 & 0 & 0 \end{bmatrix}$$

The corresponding Jordan Canonical Form $J$ places a $1 \times 1$ block for $\lambda = 3$ and a $2 \times 2$ Jordan block for $\lambda = 1$:

$$J = \begin{bmatrix} \begin{array}{c|cc} 3 & 0 & 0 \\\hline 0 & 1 & 1 \\ 0 & 0 & 1 \end{array} \end{bmatrix}$$

Thus, the final transformation identity is:
$$A = SJS^{-1} = \begin{bmatrix} 1 & 1 & 0 \\ 2 & 0 & 1 \\ 2 & 0 & 0 \end{bmatrix} \begin{bmatrix} 3 & 0 & 0 \\ 0 & 1 & 1 \\ 0 & 0 & 1 \end{bmatrix} \begin{bmatrix} 1 & 1 & 0 \\ 2 & 0 & 1 \\ 2 & 0 & 0 \end{bmatrix}^{-1}$$

---

## 3. Additional Practice Problem

### Problem
Find the Jordan Canonical Form $J$ and the transformation matrix $S$ for the matrix:
$$B = \begin{bmatrix} 2 & 1 \\ 0 & 2 \end{bmatrix}$$

### Solution

#### Step 1: Eigenvalues
The matrix is upper-triangular, so the eigenvalue is $\lambda = 2$ with $\text{AM} = 2$.

#### Step 2: Regular Eigenvector
$$(B - 2I)X_1 = 0 \implies \begin{bmatrix} 0 & 1 \\ 0 & 0 \end{bmatrix} \begin{bmatrix} x \\ y \end{bmatrix} = \begin{bmatrix} 0 \\ 0 \end{bmatrix} \implies y = 0$$
Choosing $x = 1$, our regular eigenvector is:
$$X_1 = \begin{bmatrix} 1 \\ 0 \end{bmatrix}$$
Since $\text{GM} = 1$, we need one generalized eigenvector.

#### Step 3: Generalized Eigenvector
We need a vector $X_2$ such that $(B - 2I)X_2 = X_1$:
$$\begin{bmatrix} 0 & 1 \\ 0 & 0 \end{bmatrix} \begin{bmatrix} x \\ y \end{bmatrix} = \begin{bmatrix} 1 \\ 0 \end{bmatrix} \implies y = 1$$
Choosing $x = 0$, we get:
$$X_2 = \begin{bmatrix} 0 \\ 1 \end{bmatrix}$$

#### Step 4: Constructing $S$ and $J$
$$S = [X_1 \mid X_2] = \begin{bmatrix} 1 & 0 \\ 0 & 1 \end{bmatrix}$$
$$J = \begin{bmatrix} 2 & 1 \\ 0 & 2 \end{bmatrix}$$

---

## 4. Visual Concept Mapping (Chain Structure Graph)

Below is a structural ASCII chart representing how standard eigenvectors and generalized eigenvectors link together linearly to form the columns of transition matrix $S$.


```

[ Generalized Eigenvector: X3 ]  ---(Action of A - λI)--->  [ Standard Eigenvector: X2 ]
│                                                          │
└─────────────────── Ordered together into ────────────────┴───► Placed into Matrix S

```





# Linear Algebra: Advanced Jordan Canonical Form (JCF) & Minimal Polynomials

This set of comprehensive notes covers the construction of the Jordan Canonical Form (JCF), the transition matrix $S$ built via generalized eigenvector chains, and its fundamental relationship with characteristic and minimal polynomials.

---

## 1. Core Mathematical Foundations

### Multiplicities & Jordan Blocks
When a matrix $A_{n \times n}$ has repeated eigenvalues and lacks a complete set of linearly independent standard eigenvectors, it cannot be diagonalized. Instead, we decompose it into its Jordan Canonical Form $J = S^{-1}AS$.

* **Algebraic Multiplicity (AM):** The number of times an eigenvalue $\lambda$ appears as a root of the characteristic polynomial $\chi_A(\lambda)$.
  $$\text{AM of } \lambda = \text{Sum of the sizes of all Jordan blocks corresponding to } \lambda$$
* **Geometric Multiplicity (GM):** The number of linearly independent standard eigenvectors corresponding to $\lambda$.
  $$\text{GM of } \lambda = \text{Total number of distinct Jordan blocks corresponding to } \lambda$$


---

## 2. JCF and the Minimal Polynomial Relationship

Given a matrix $A$ represented in its Jordan Canonical Form $J$:

1. **Eigenvalues:** The eigenvalues are the exact entries along the main diagonal.
2. **Characteristic Polynomial $\chi_A(\lambda)$:**
   $$\chi_A(\lambda) = (\lambda - \lambda_1)^{r_1}(\lambda - \lambda_2)^{r_2}\dots(\lambda - \lambda_k)^{r_k}$$
   where $r_i$ is the **Algebraic Multiplicity** (total occurrences of $\lambda_i$ on the main diagonal).
3. **Minimal Polynomial $m_A(\lambda)$:**
   $$m_A(\lambda) = (\lambda - \lambda_1)^{s_1}(\lambda - \lambda_2)^{s_2}\dots(\lambda - \lambda_k)^{s_k}$$
   where $s_i$ represents the **size of the largest single Jordan block** corresponding to $\lambda_i$.

---

## 3. Step-by-Step Lecture Examples Explained

### Example 1: Finding JCF for a Upper-Triangular System
**Problem:** Find the JCF ($J$) and transition matrix ($S$) for:
$$A = \begin{bmatrix} 2 & 2 & 1 \\ 0 & 2 & -1 \\ 0 & 0 & 3 \end{bmatrix}$$

#### Step 1: Find Eigenvalues & Multiplicities
Since $A$ is upper-triangular, its eigenvalues sit on the diagonal:
* $\lambda = 3$ with $\text{AM} = 1$
* $\lambda = 2$ with $\text{AM} = 2$

#### Step 2: Compute Regular Eigenvectors
* **For $\lambda = 3$:** Solve $(A - 3I)X_1 = 0$
  $$\begin{bmatrix} -1 & 2 & 1 \\ 0 & -1 & -1 \\ 0 & 0 & 0 \end{bmatrix} \begin{bmatrix} x \\ y \\ z \end{bmatrix} = \begin{bmatrix} 0 \\ 0 \\ 0 \end{bmatrix} \implies X_1 = \begin{bmatrix} -1 \\ -1 \\ 1 \end{bmatrix}$$
* **For $\lambda = 2$:** Solve $(A - 2I)X_2 = 0$
  $$\begin{bmatrix} 0 & 2 & 1 \\ 0 & 0 & -1 \\ 0 & 0 & 1 \end{bmatrix} \begin{bmatrix} x \\ y \\ z \end{bmatrix} = \begin{bmatrix} 0 \\ 0 \\ 0 \end{bmatrix} \implies z=0, y=0 \implies X_2 = \begin{bmatrix} 1 \\ 0 \\ 0 \end{bmatrix}$$
  Since we only found $1$ regular eigenvector for $\lambda=2$, its $\text{GM} = 1$. Because $\text{GM} (1) < \text{AM} (2)$, we need a generalized eigenvector.

#### Step 3: Compute the Generalized Eigenvector
We set up a Jordan chain where $(A - 2I)X_3 = X_2$:
$$\begin{bmatrix} 0 & 2 & 1 \\ 0 & 0 & -1 \\ 0 & 0 & 1 \end{bmatrix} \begin{bmatrix} x \\ y \\ z \end{bmatrix} = \begin{bmatrix} 1 \\ 0 \\ 0 \end{bmatrix} \implies 2y + z = 1, -z = 0 \implies z = 0, y = \frac{1}{2}$$
Choosing free variable $x = 0$:
$$X_3 = \begin{bmatrix} 0 \\ \frac{1}{2} \\ 0 \end{bmatrix}$$

#### Step 4: Construct $S$, $J$, and Minimal Polynomial
Assemble $S = [X_1 \mid X_2 \mid X_3]$ and group $J$ into blocks:
$$S = \begin{bmatrix} -1 & 1 & 0 \\ -1 & 0 & \frac{1}{2} \\ 1 & 0 & 0 \end{bmatrix}, \quad J = \begin{bmatrix} 3 & 0 & 0 \\ 0 & 2 & 1 \\ 0 & 0 & 2 \end{bmatrix}$$

* The largest block for $\lambda=3$ is size $1$.
* The largest block for $\lambda=2$ is size $2$.
* **Minimal Polynomial:** $m_A(\lambda) = (\lambda - 3)^1(\lambda - 2)^2$

---

### Example 2: Full 3x3 Jordan Chain Block
**Problem:** Find $J$ and $S$ for:
$$A = \begin{bmatrix} 3 & 0 & 1 \\ -1 & 3.5 & 2.5 \\ 1 & -0.5 & 2.5 \end{bmatrix}$$

#### Step 1: Eigenvalues
Solving $\det(A - \lambda I) = 0$ yields a single repeated root:
* $\lambda = 3$ with $\text{AM} = 3$.

#### Step 2: Regular Eigenvector
Solving $(A - 3I)X_1 = 0$:
$$\begin{bmatrix} 0 & 0 & 1 \\ -1 & 0.5 & 2.5 \\ 1 & -0.5 & -0.5 \end{bmatrix} \begin{bmatrix} x \\ y \\ z \end{bmatrix} = \begin{bmatrix} 0 \\ 0 \\ 0 \end{bmatrix} \implies X_1 = \begin{bmatrix} 1 \\ 2 \\ 0 \end{bmatrix}$$
Since $\text{GM} = 1$, all $3$ dimensions are packed into a single Jordan block. We need to construct a chain of length 3: $X_3 \xrightarrow{A-3I} X_2 \xrightarrow{A-3I} X_1$.

#### Step 3: Generalized Eigenvectors Chain
* **Find $X_2$** via $(A - 3I)X_2 = X_1$:
  $$\begin{bmatrix} 0 & 0 & 1 \\ -1 & 0.5 & 2.5 \\ 1 & -0.5 & -0.5 \end{bmatrix} \begin{bmatrix} x \\ y \\ z \end{bmatrix} = \begin{bmatrix} 1 \\ 2 \\ 0 \end{bmatrix} \implies X_2 = \begin{bmatrix} 1 \\ 1 \\ 1 \end{bmatrix}$$
* **Find $X_3$** via $(A - 3I)X_3 = X_2$:
  $$\begin{bmatrix} 0 & 0 & 1 \\ -1 & 0.5 & 2.5 \\ 1 & -0.5 & -0.5 \end{bmatrix} \begin{bmatrix} x \\ y \\ z \end{bmatrix} = \begin{bmatrix} 1 \\ 1 \\ 1 \end{bmatrix} \implies X_3 = \begin{bmatrix} 1 \\ -1 \\ 1 \end{bmatrix}$$

#### Step 4: Final Canonical Structures
$$S = \begin{bmatrix} 1 & 1 & 1 \\ 2 & 1 & -1 \\ 0 & 1 & 1 \end{bmatrix}, \quad J = \begin{bmatrix} 3 & 1 & 0 \\ 0 & 3 & 1 \\ 0 & 0 & 3 \end{bmatrix}$$

* **Minimal Polynomial:** Since the largest (and only) block for $\lambda=3$ is of size 3:
  $$m_A(\lambda) = (\lambda - 3)^3$$

---

## 4. Visualizing Vector Action Chains

The flowchart below displays how generalized eigenvectors map down to regular standard eigenvectors through repeated multiplication by the shifted matrix $(A - \lambda I)$.


```

[ Generalized Gen-2: X3 ]
│
▼ Matrix Action: (A - λI)
[ Generalized Gen-1: X2 ]
│
▼ Matrix Action: (A - λI)
[ Standard Eigenvector: X1 ]
│
▼ Matrix Action: (A - λI)
[ Zero Vector: 0 ]

```





# Linear Algebra: Constructing Jordan Forms from Polynomials & Matrix Applications

This module details how to determine all possible structures for a matrix's **Jordan Canonical Form (JCF)** using its characteristic and minimal polynomials. It also introduces critical applications of JCF, such as computing high matrix powers and matrix exponentials.

---

## 1. Concept: Determining JCF from Characteristic and Minimal Polynomials

When constructing a Jordan Canonical Form matrix $J$ for a given matrix $A_{n \times n}$, we follow two mathematical restrictions determined by the roots of its polynomials:

1. **Total Size (From Characteristic Polynomial $c_A(\lambda)$):** The exponent of the factor $(\lambda - \lambda_i)$ represents the **Algebraic Multiplicity (AM)** of $\lambda_i$. This tells us the *total number of times* $\lambda_i$ must appear along the diagonal of $J$.
2. **Largest Block Size (From Minimal Polynomial $m_A(\lambda)$):** The exponent of the factor $(\lambda - \lambda_i)$ in the minimal polynomial indicates the size of the **largest single Jordan block** associated with $\lambda_i$.
3. **Partition Combinations:** Any remaining allocations for that eigenvalue must be distributed into smaller or equal-sized Jordan blocks such that the sum of all block sizes equals the AM.

---

## 2. Step-by-Step Breakdown of the Lecture Examples

### Given Parameters
Consider a $6 \times 6$ matrix $A$ with the characteristic polynomial:
$$c_A(\lambda) = (\lambda - 3)^4(\lambda - 4)^2$$

* For $\lambda = 3$: Total diagonal entries ($\text{AM}$) = $4$.
* For $\lambda = 4$: Total diagonal entries ($\text{AM}$) = $2$.

---

### Case 1: When $m_A(\lambda) = (\lambda - 3)^3(\lambda - 4)^2$

#### Step 1: Analyze $\lambda = 3$
* Total elements required = $4$.
* The largest single Jordan block must be of size **3**.
* The remaining allocation ($4 - 3 = 1$) must form a block of size **1**.
* The unique integer partition for the blocks is: $4 = 3 + 1$.

#### Step 2: Analyze $\lambda = 4$
* Total elements required = $2$.
* The largest single Jordan block must be of size **2**.
* The unique integer partition for the blocks is: $2 = 2$.

#### Step 3: Construct the Final JCF Matrix ($J$)
Combining a $3 \times 3$ and a $1 \times 1$ block for $\lambda=3$, alongside a $2 \times 2$ block for $\lambda=4$:

$$J = \begin{bmatrix} 
\begin{array}{ccc|c|cc} 
3 & 1 & 0 & 0 & 0 & 0 \\ 
0 & 3 & 1 & 0 & 0 & 0 \\ 
0 & 0 & 3 & 0 & 0 & 0 \\ \hline
0 & 0 & 0 & 3 & 0 & 0 \\ \hline
0 & 0 & 0 & 0 & 4 & 1 \\ 
0 & 0 & 0 & 0 & 0 & 4 
\end{array} 
\end{bmatrix}$$

---

### Case 2: When $m_A(\lambda) = (\lambda - 3)^2(\lambda - 4)^2$

#### Step 1: Analyze $\lambda = 3$
* Total elements required = $4$.
* The largest single Jordan block must be of size **2**.
* The remaining slots ($4 - 2 = 2$) can be partitioned into sizes less than or equal to 2. This yields two valid possibilities:
  * **Option A:** Two blocks of size 2 $\implies 4 = 2 + 2$
  * **Option B:** One block of size 2, and two blocks of size 1 $\implies 4 = 2 + 1 + 1$

#### Step 2: Analyze $\lambda = 4$
* Total elements required = $2$.
* The largest block size is **2** $\implies$ a single block of size 2.

#### Step 3: Construct the Potential JCF Matrices
Depending on the partition option chosen for $\lambda = 3$, $J$ can take one of two structures:

**For Option A ($2 + 2$ block structure):**
$$J = \begin{bmatrix} 
\begin{array}{cc|cc|cc} 
3 & 1 & 0 & 0 & 0 & 0 \\ 
0 & 3 & 0 & 0 & 0 & 0 \\ \hline
0 & 0 & 3 & 1 & 0 & 0 \\ 
0 & 0 & 0 & 3 & 0 & 0 \\ \hline
0 & 0 & 0 & 0 & 4 & 1 \\ 
0 & 0 & 0 & 0 & 0 & 4 
\end{array} 
\end{bmatrix}$$

**For Option B ($2 + 1 + 1$ block structure):**
$$J = \begin{bmatrix} 
\begin{array}{cc|c|c|cc} 
3 & 1 & 0 & 0 & 0 & 0 \\ 
0 & 3 & 0 & 0 & 0 & 0 \\ \hline
0 & 0 & 3 & 0 & 0 & 0 \\ \hline
0 & 0 & 0 & 3 & 0 & 0 \\ \hline
0 & 0 & 0 & 0 & 4 & 1 \\ 
0 & 0 & 0 & 0 & 0 & 4 
\end{array} 
\end{bmatrix}$$

---

## 3. Core Matrix Applications of JCF

Because any square matrix can be rewritten via similarity transformation as $A = SJS^{-1}$, computing matrix functions becomes significantly simpler.

### High Matrix Powers
Multiplying $A$ by itself $k$ times causes internal $S^{-1}S$ terms to cancel out:
$$A^k = (SJS^{-1})(SJS^{-1})\dots(SJS^{-1}) = SJ^kS^{-1}$$
> **Example:** To compute a massive matrix power like $A^{100}$, you only need to calculate:
> $$A^{100} = S J^{100} S^{-1}$$

### Matrix Exponentials
Using the Taylor series expansion for the matrix exponential function $e^A$:
$$e^A = \sum_{n=0}^{\infty} \frac{A^n}{n!} = S \left( \sum_{n=0}^{\infty} \frac{J^n}{n!} \right) S^{-1} = S e^J S^{-1}$$

---

## 4. Additional Practice Problem

**Problem:** A $4 \times 4$ matrix $A$ has $c_A(\lambda) = (\lambda - 5)^4$ and $m_A(\lambda) = (\lambda - 5)^2$. Find all possible structures for its Jordan Canonical Form $J$.

### Solution Step-by-Step

1. **Extract Constraints:** The eigenvalue is $\lambda = 5$ with a total dimension ($\text{AM}$) of $4$. The largest single block can only be of size $2$.
2. **Find Partitions:** We need to find all unique ways to add positive integers up to $4$, where the maximum integer in the partition is exactly $2$:
   * **Possibility 1:** $4 = 2 + 2$ (Two blocks of size $2$)
   * **Possibility 2:** $4 = 2 + 1 + 1$ (One block of size $2$, two blocks of size $1$)
3. **Write Matrices:**
   $$J_1 = \begin{bmatrix} 5 & 1 & 0 & 0 \\ 0 & 5 & 0 & 0 \\ 0 & 0 & 5 & 1 \\ 0 & 0 & 0 & 5 \end{bmatrix} \quad \text{or} \quad J_2 = \begin{bmatrix} 5 & 1 & 0 & 0 \\ 0 & 5 & 0 & 0 \\ 0 & 0 & 5 & 0 \\ 0 & 0 & 0 & 5 \end{bmatrix}$$

---

## 5. Visual Concept Map (JCF Derivation Pipeline)

The flowchart below shows how the characteristic and minimal polynomials dictate the layout of a Jordan Canonical Form matrix.


```

[ Characteristic Polynomial ] ───► Determines TOTAL occurrences of λ (Total Size)
│
▼
[   Minimal Polynomial    ] ───► Determines LARGEST single Block Size
│
▼
[  Partition Combinations ] ───► Determines all valid JCF block structures

```

```