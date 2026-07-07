# Lecture 13: Geometric Interpretation and Fundamental Properties of SVD

This note combines the step-by-step geometric walkthrough of Singular Value Decomposition (SVD) with its corresponding fundamental subspace properties.

---

## 1. Geometric Interpretation: Step-by-Step Mapping

The SVD factors any linear transformation $A \in \mathbb{R}^{m \times n}$ into a sequence of three basic geometric operations: a rotation/reflection, a standalone diagonal scaling, and a final rotation/reflection.

$$A = U \Sigma V^T \quad \text{(or } U \Sigma V^* \text{ in complex spaces)}$$

To understand how $A$ maps a unit circle into an ellipse, we follow the matrix multiplication chain from right to left ($V^T \rightarrow \Sigma \rightarrow U$):

```text
       Direct Path Matrix Transformation (A)
      ┌────────────────────────────────────┐
      │                                    ▼
┌───────────┐                        ┌───────────┐
│           │                        │   ████    │
│   Unit    │                        │ ████████  │ Turned Ellipse
│  Circle   │                        │   ████    │ (Basis: u_i)
└───────────┘                        └───────────┘
      │                                    ▲
      │ 1. Rotate/Reflect                  │ 3. Rotate/Reflect
      │    (Matrix Vᵀ)                     │    (Matrix U)
      ▼                                    │
┌───────────┐      2. Scale Axes           │
│           │      (Matrix Σ)        ┌───────────┐
│ Aligned   │───────────────────────►│  Aligned  │
│  Circle   │    σ_1, σ_2, ..., σ_r  │  Ellipse  │
└───────────┘                        └───────────┘

```

### 1️⃣ Step 1: Base Rotation ($V^T$ or $V^*$)

* **Action:** The transformation begins by applying $V^T$ to the input space.
* **Geometric Effect:** Since $V$ is an orthogonal matrix, multiplying by $V^T$ represents a rigid rotation or reflection. It takes the standard basis vectors and aligns them with the principal directional axes of the upcoming transformation without changing the circular shape.

### 2️⃣ Step 2: Singular Value Scaling ($\Sigma$)

* **Action:** The aligned vectors are multiplied by the rectangular diagonal matrix $\Sigma$.
* **Geometric Effect:** This operation applies straight scalar stretching or compression along the coordinate axes.
* The radii are scaled by the singular values ($\sigma_1, \sigma_2, \dots, \sigma_r$).
* The unit circle is deformed into an **aligned ellipse** whose semi-axes lengths match the singular values exactly. Any dimensions associated with zero singular values are crushed completely to the origin.



### 3️⃣ Step 3: Final Output Rotation ($U$)

* **Action:** The scaled ellipse is multiplied by the final orthogonal matrix $U$.
* **Geometric Effect:** This performs a final rigid rotation or reflection in the output space. It takes the cleanly aligned ellipse and tilts its principal axes to point along the directional tracking paths of the **left singular vectors** ($u_i$).

---

## 2. Fundamental Subspace Properties of SVD

Let $A \in \mathbb{R}^{m \times n}$ be a matrix with $\text{rank}(A) = r$, and let its SVD be $A = U \Sigma V^T$. The columns of $U$ and $V$ provide orthonormal bases for the four fundamental subspaces of linear algebra:

| Subspace | Dimension | Described By | Orthonormal Basis Columns |
| --- | --- | --- | --- |
| **Range / Column Space:** $\text{range}(A)$ | $r$ | First $r$ non-zero singular value outputs | First $r$ columns of $U$ ($\{u_1, \dots, u_r\}$) |
| **Left Nullspace:** $\text{null}(A^T)$ | $m - r$ | Output dimensions crushed to zero | Last $m - r$ columns of $U$ ($\{u_{r+1}, \dots, u_m\}$) |
| **Row Space:** $\text{range}(A^T)$ | $r$ | Input directions that survive mapping | First $r$ columns of $V$ ($\{v_1, \dots, v_r\}$) |
| **Nullspace / Kernel:** $\text{null}(A)$ | $n - r$ | Input directions squashed to zero ($AX=\mathbf{0}$) | Last $n - r$ columns of $V$ ($\{v_{r+1}, \dots, v_n\}$) |

---

## 3. Comprehensive Verification Example

Let's look at a concrete example using the SVD of a $2 \times 2$ matrix to see both the geometric mappings and the subspaces explicitly:

$$A = \begin{bmatrix} 1 & 1 \\ -1 & 1 \end{bmatrix} = \begin{bmatrix} \frac{1}{\sqrt{2}} & -\frac{1}{\sqrt{2}} \\ \frac{1}{\sqrt{2}} & \frac{1}{\sqrt{2}} \end{bmatrix} \begin{bmatrix} \sqrt{2} & 0 \\ 0 & \sqrt{2} \end{bmatrix} \begin{bmatrix} 0 & -1 \\ 1 & 0 \end{bmatrix}$$

### 🧭 Geometric Step Verification:

1. **$V^T = \begin{bmatrix} 0 & -1 \\ 1 & 0 \end{bmatrix}$:** This rotates any input vector by exactly $90^\circ$ clockwise. A unit circle remains a unit circle.
2. **$\Sigma = \begin{bmatrix} \sqrt{2} & 0 \\ 0 & \sqrt{2} \end{bmatrix}$:** Since $\sigma_1 = \sigma_2 = \sqrt{2}$, this scales all directions uniformly by $\sqrt{2}$. The circle expands evenly into a larger circle of radius $\sqrt{2}$.
3. **$U = \begin{bmatrix} \frac{1}{\sqrt{2}} & -\frac{1}{\sqrt{2}} \\ \frac{1}{\sqrt{2}} & \frac{1}{\sqrt{2}} \end{bmatrix}$:** This applies a $45^\circ$ counter-clockwise rotation to the expanded circle to yield the final transformation state.

### 📂 Subspace Extraction Verification:

* **Rank Analysis:** Both singular values are non-zero ($\sigma_1 = \sqrt{2}, \sigma_2 = \sqrt{2}$), meaning $\text{rank}(A) = r = 2$.
* **$\text{range}(A)$:** Spanned by the first $r=2$ columns of $U$. Since it includes all columns, $\text{range}(A) = \mathbb{R}^2$ (The column space fills the entire 2D plane).
* **$\text{null}(A)$:** Spanned by the last $n - r = 2 - 2 = 0$ columns of $V$. The nullspace contains only the trivial zero vector ($\{\mathbf{0}\}$), confirming that no non-zero input vectors are squashed.


#  Fundamental Subspaces and Proofs via SVD

This section connects the **Singular Value Decomposition (SVD)** of an $m \times n$ matrix $A$ directly to the bases of the four fundamental subspaces. It includes algebraic proofs for identifying the basis vectors of nullspaces using the factorized components.

---

## 1. Summary of SVD Subspace Properties

Let $A \in \mathbb{R}^{m \times n}$ with $\text{rank}(A) = r$, and let its singular value decomposition be $A = U\Sigma V^T$.

1. **Singular Value Constraint:** Only the first $r$ diagonal entries of $\Sigma$ are strictly non-zero ($\sigma_1 \ge \sigma_2 \ge \dots \ge \sigma_r > 0$). All subsequent values are zero.
2. **The Column Space / Range ($A$):** An orthonormal basis for $\text{range}(A)$ is given by the **first $r$ columns of $U$**.
3. **The Nullspace ($A$):** An orthonormal basis for $\text{null}(A)$ is given by the **last $n - r$ columns of $V$**.
4. **The Row Space / Range ($A^T$):** An orthonormal basis for $\text{range}(A^T)$ is given by the **first $r$ columns of $V$**.
5. **The Left Nullspace ($A^T$):** An orthonormal basis for $\text{null}(A^T)$ is given by the **last $m - r$ columns of $U$**.

---

## 2. Algebraic Proofs & Derivations

### Part A: Deriving the Basis for $\text{null}(A)$

To find the nullspace of $A$, we analyze the homogeneous equation system $AX = \mathbf{0}$.

#### Step 1: Substitute the SVD factorized form into the equation

$$(U\Sigma V^T)X = \mathbf{0}$$

#### Step 2: Premultiply by $U^T$

Since $U$ is an orthogonal matrix ($U^T U = I$), premultiplying both sides by $U^T$ eliminates $U$ without altering the zero vector on the right side:


$$U^T(U\Sigma V^T)X = U^T\mathbf{0}$$

$$\Sigma (V^T X) = \mathbf{0}$$

#### Step 3: Analyze the tracking behavior of $\Sigma$

The diagonal matrix $\Sigma$ only contains non-zero entries up to row $r$. For the product to equal zero, the vector product $V^T X$ must yield zeros in its first $r$ entries. This means that $X$ must be orthogonal to the first $r$ rows of $V^T$ (which are the first $r$ columns of $V$).

#### Conclusion:

Therefore, the vector $X$ must line up exclusively within the subspace spanned by the remaining columns of $V$.

$$\implies \text{The last } n - r \text{ columns of } V \text{ form the orthonormal basis for } \text{null}(A).$$

---

### Part B: Deriving the Basis for $\text{null}(A^T)$

To analyze the left nullspace, we look at the system mapping for the transpose matrix $A^T: \mathbb{R}^m \to \mathbb{R}^n$.

#### Step 1: Construct the Transpose of the SVD

Using the matrix transpose identity property $(ABC)^T = C^T B^T A^T$:


$$A^T = (U\Sigma V^T)^T = (V^T)^T \Sigma^T U^T$$

$$A^T = V \Sigma^T U^T$$

#### Step 2: Set up the homogeneous system $A^T Y = \mathbf{0}$

$$(V \Sigma^T U^T)Y = \mathbf{0}$$

#### Step 3: Premultiply by $V^T$

Since $V$ is an orthogonal matrix ($V^T V = I$):


$$V^T(V \Sigma^T U^T)Y = V^T\mathbf{0}$$

$$\Sigma^T (U^T Y) = \mathbf{0}$$

#### Conclusion:

By matching the layout logic from Part A, the diagonal constraint of $\Sigma^T$ zeroes out the first $r$ channels. For the product to vanish completely, the vector $Y$ must align exclusively with the remaining vector directions.

$$\implies \text{The last } m - r \text{ columns of } U \text{ form the orthonormal basis for } \text{null}(A^T).$$

---

## 3. Concrete Verification Example

Let's look at a quick, intuitive numerical example using a rank-1 outer product matrix to trace these columns directly:

$$A = \begin{bmatrix} 1 & 0 \\ 0 & 0 \end{bmatrix}_{2 \times 2}$$

This matrix has a size of $2 \times 2$ ($m=2, n=2$) and a rank of $r=1$. Its SVD components align as follows:

$$U = \begin{bmatrix} \mathbf{1} & \mathbf{0} \\ \mathbf{0} & \mathbf{1} \end{bmatrix}, \quad \Sigma = \begin{bmatrix} 1 & 0 \\ 0 & 0 \end{bmatrix}, \quad V^T = \begin{bmatrix} \mathbf{1} & \mathbf{0} \\ \mathbf{0} & \mathbf{1} \end{bmatrix}$$

Let's test our rules using these components:

* **$\text{null}(A)$:** According to our theorem, this space is given by the last $n - r = 2 - 1 = 1$ column of $V$. Look at the second column of $V$: $\begin{bmatrix} 0 \\ 1 \end{bmatrix}$.
* *Verification check:* $A \begin{bmatrix} 0 \\ 1 \end{bmatrix} = \begin{bmatrix} 1 & 0 \\ 0 & 0 \end{bmatrix}\begin{bmatrix} 0 \\ 1 \end{bmatrix} = \begin{bmatrix} 0 \\ 0 \end{bmatrix}$. This matches perfectly.


* **$\text{range}(A)$:** This space is given by the first $r = 1$ column of $U$: $\begin{bmatrix} 1 \\ 0 \end{bmatrix}$. This matches the output space generated by the columns of matrix $A$.


# SVD and the Moore-Penrose Pseudo-Inverse

This section details how to calculate the **Moore-Penrose Pseudo-Inverse** (denoted as $A^+$) of any matrix using its Singular Value Decomposition (SVD). This tool extends the concept of a matrix inverse to rectangular or singular matrices.

---

## 1. Mathematical Framework and Formulation

Let $A \in \mathbb{R}^{m \times n}$ be a general real matrix with a mathematical rank of $\text{rank}(A) = r$. The Singular Value Decomposition of $A$ factorizes the matrix into:

$$A = U \Sigma V^T$$

Where the non-zero singular values are ordered hierarchically along the diagonal: $\sigma_1 \ge \sigma_2 \ge \dots \ge \sigma_r > 0$.

### Step-by-Step Derivation of $A^+$

To find the pseudo-inverse, we apply the matrix inversion property $(ABC)^+ = C^+ B^+ A^+$ to our singular value decomposition factors:

$$A^+ = (U \Sigma V^T)^+$$

1. **Expand using the reverse-order rule:**

$$A^+ = (V^T)^+ \Sigma^+ U^+$$


2. **Simplify the orthogonal components:**
Because $U$ and $V$ are orthogonal matrices ($U^T U = I$ and $V^T V = I$), their pseudo-inverses are identical to their standard inverses, which equal their transposes:
* $(V^T)^+ = (V^T)^{-1} = V$
* $U^+ = U^{-1} = U^T$


3. **Assemble the final structural equation:**
Substituting these simplified components back into the formula gives the foundational calculation rule for the pseudo-inverse:

$$A^+ = V \Sigma^+ U^T$$

---

## 2. Constructing the Pseudo-Inverse Diagonal Matrix ($\Sigma^+$)

The matrix $\Sigma^+$ is an $n \times m$ rectangular matrix (the transposed shape of $\Sigma$). It is constructed using a simple arithmetic recipe:

* **Reciprocal Rule:** Take the reciprocal ($\frac{1}{\sigma_i}$) of every non-zero singular value sitting on the main diagonal.
* **Keep Zeros Clean:** Leave all original zero entries as exactly zero ($0 \to 0$).

### 📝 Clear Structural Case Study: $3 \times 3$ Matrix with Rank 2

Let $A$ be a $3 \times 3$ matrix whose singular values are $\sigma_1$, $\sigma_2$, and a third singular value that drops cleanly to $0$ ($\sigma_3 = 0$).

#### Step 1: Write down the original diagonal matrix $\Sigma$

$$\Sigma = \begin{bmatrix} \sigma_1 & 0 & 0 \\ 0 & \sigma_2 & 0 \\ 0 & 0 & 0 \end{bmatrix}_{3 \times 3}$$

#### Step 2: Apply the arithmetic rules to construct $\Sigma^+$

Invert the non-zero singular values along the main diagonal, keeping the zero entry intact:

$$\Sigma^+ = \begin{bmatrix} \frac{1}{\sigma_1} & 0 & 0 \\ 0 & \frac{1}{\sigma_2} & 0 \\ 0 & 0 & 0 \end{bmatrix}_{3 \times 3}$$

---

## 3. Walkthrough Calculation Example

Let's compute the pseudo-inverse for a non-invertible, singular diagonal matrix to trace this math in action:

$$A = \begin{bmatrix} 2 & 0 \\ 0 & 0 \end{bmatrix}$$

Since this matrix is already diagonal, symmetric, and positive semi-definite, its SVD matrices are trivial to identify:


$$U = \begin{bmatrix} 1 & 0 \\ 0 & 1 \end{bmatrix}, \quad \Sigma = \begin{bmatrix} 2 & 0 \\ 0 & 0 \end{bmatrix}, \quad V^T = \begin{bmatrix} 1 & 0 \\ 0 & 1 \end{bmatrix}$$

### Step 1: Calculate $\Sigma^+$

Take the reciprocal of the non-zero entry ($2 \to \frac{1}{2}$) and preserve the zero:


$$\Sigma^+ = \begin{bmatrix} \frac{1}{2} & 0 \\ 0 & 0 \end{bmatrix}$$

### Step 2: Compute $A^+ = V \Sigma^+ U^T$

Multiply the components back together:


$$A^+ = \begin{bmatrix} 1 & 0 \\ 0 & 1 \end{bmatrix} \begin{bmatrix} \frac{1}{2} & 0 \\ 0 & 0 \end{bmatrix} \begin{bmatrix} 1 & 0 \\ 0 & 1 \end{bmatrix} = \begin{bmatrix} \frac{1}{2} & 0 \\ 0 & 0 \end{bmatrix}$$

### Conclusion

The pseudo-inverse is $A^+ = \begin{bmatrix} 0.5 & 0 \\ 0 & 0 \end{bmatrix}$.

> **💡 Verification Check:** While a pseudo-inverse doesn't satisfy the strict definition of a standard matrix inverse ($A A^{-1} = I$), it satisfies the weaker Moore-Penrose criteria:
> 
> $$A A^+ A = \begin{bmatrix} 2 & 0 \\ 0 & 0 \end{bmatrix} \begin{bmatrix} 0.5 & 0 \\ 0 & 0 \end{bmatrix} \begin{bmatrix} 2 & 0 \\ 0 & 0 \end{bmatrix} = \begin{bmatrix} 1 & 0 \\ 0 & 0 \end{bmatrix} \begin{bmatrix} 2 & 0 \\ 0 & 0 \end{bmatrix} = \begin{bmatrix} 2 & 0 \\ 0 & 0 \end{bmatrix} = A$$
> 
> 
> 
> The verification condition holds true.


## Pseudo-Inverse Dimensions and Concrete Rectangular Walkthrough

This section provides a clear framework for constructing the pseudo-inverse singular value matrix $\Sigma^+$ across different matrix dimensions, followed by a complete step-by-step example for calculating the pseudo-inverse $A^+$ of a rectangular matrix.

---

## 1. Dimensional Behavior of $\Sigma^+$

When computing the Moore-Penrose pseudo-inverse matrix using SVD ($A^+ = V \Sigma^+ U^T$), the structural layout of the singular value matrix $\Sigma^+$ changes dynamically based on the dimensions of the original matrix $A$.

> ### 📌 The Core Transpose Rule
> 
> 
> If the original singular matrix $\Sigma$ has a size of **$m \times n$**, then its pseudo-inverse matrix $\Sigma^+$ **must** have a flipped size of **$n \times m$**.

---

### Case A: Tall Matrices ($m > n$)

Let $A$ be a $5 \times 3$ matrix ($m=5, n=3$) with a rank of $r=2$ ($\sigma_1 \ge \sigma_2 > 0$ and $\sigma_3 = 0$).

* **Original Matrix $\Sigma$ ($5 \times 3$):** Holds singular values on the main diagonal up to row 3.
* **Pseudo-Inverse Matrix $\Sigma^+$ ($3 \times 5$):** The layout rotates horizontally. We invert the non-zero singular values ($\frac{1}{\sigma_i}$) along the diagonal entries, leaving all original zeros intact.

$$\Sigma = \begin{bmatrix} \sigma_1 & 0 & 0 \\ 0 & \sigma_2 & 0 \\ 0 & 0 & 0 \\ 0 & 0 & 0 \\ 0 & 0 & 0 \end{bmatrix}_{5 \times 3} \implies \Sigma^+ = \begin{bmatrix} \frac{1}{\sigma_1} & 0 & 0 & 0 & 0 \\ 0 & \frac{1}{\sigma_2} & 0 & 0 & 0 \\ 0 & 0 & 0 & 0 & 0 \end{bmatrix}_{3 \times 5}$$

---

### Case B: Wide Matrices ($m < n$)

Let $A$ be a $3 \times 5$ matrix ($m=3, n=5$) with a full row rank of $r=3$ ($\sigma_1 \ge \sigma_2 \ge \sigma_3 > 0$).

* **Original Matrix $\Sigma$ ($3 \times 5$):** Holds singular values on the main diagonal up to column 3.
* **Pseudo-Inverse Matrix $\Sigma^+$ ($5 \times 3$):** The layout rotates vertically. We invert the non-zero singular values along the diagonal entries, and add extra padding rows of zeros at the bottom.

$$\Sigma = \begin{bmatrix} \sigma_1 & 0 & 0 & 0 & 0 \\ 0 & \sigma_2 & 0 & 0 & 0 \\ 0 & 0 & \sigma_3 & 0 & 0 \end{bmatrix}_{3 \times 5} \implies \Sigma^+ = \begin{bmatrix} \frac{1}{\sigma_1} & 0 & 0 \\ 0 & \frac{1}{\sigma_2} & 0 \\ 0 & 0 & \frac{1}{\sigma_3} \\ 0 & 0 & 0 \\ 0 & 0 & 0 \end{bmatrix}_{5 \times 3}$$

---

## 2. Complete Walkthrough Problem

**Task:** Find the Moore-Penrose Pseudo-Inverse ($A^+$) of the following rectangular $2 \times 3$ matrix:

$$A = \begin{bmatrix} 4 & 11 & 14 \\ 8 & 7 & -2 \end{bmatrix}$$

### Step 1: Obtain the SVD of Matrix $A$

From our prior SVD calculations, the singular value decomposition components ($A = U \Sigma V^T$) are given as:

* **Left Singular Vectors ($U_{2 \times 2}$):**

$$U = \begin{bmatrix} -\frac{3}{\sqrt{10}} & \frac{1}{\sqrt{10}} \\ -\frac{1}{\sqrt{10}} & -\frac{3}{\sqrt{10}} \end{bmatrix}$$


* **Singular Values ($\Sigma_{2 \times 3}$):**

$$\Sigma = \begin{bmatrix} 6\sqrt{10} & 0 & 0 \\ 0 & 3\sqrt{10} & 0 \end{bmatrix}$$


* **Right Singular Vectors ($V^T_{3 \times 3}$):**

$$V^T = \begin{bmatrix} -\frac{1}{3} & -\frac{2}{3} & -\frac{2}{3} \\ -\frac{2}{3} & -\frac{1}{3} & \frac{2}{3} \\ \frac{2}{3} & -\frac{2}{3} & \frac{1}{3} \end{bmatrix}^T \implies V = \begin{bmatrix} -\frac{1}{3} & -\frac{2}{3} & \frac{2}{3} \\ -\frac{2}{3} & -\frac{1}{3} & -\frac{2}{3} \\ -\frac{2}{3} & \frac{2}{3} & \frac{1}{3} \end{bmatrix}$$



---

### Step 2: Compute the Pseudo-Inverse Diagonal Matrix ($\Sigma^+$)

Our original matrix $\Sigma$ has a size of $2 \times 3$. Therefore, our pseudo-inverse matrix $\Sigma^+$ must be a **$3 \times 2$** matrix.

We invert the non-zero elements along the main diagonal path:

* $\sigma_1 = 6\sqrt{10} \implies \frac{1}{\sigma_1} = \frac{1}{6\sqrt{10}}$
* $\sigma_2 = 3\sqrt{10} \implies \frac{1}{\sigma_2} = \frac{1}{3\sqrt{10}}$

$$\Sigma^+ = \begin{bmatrix} \frac{1}{6\sqrt{10}} & 0 \\ 0 & \frac{1}{3\sqrt{10}} \\ 0 & 0 \end{bmatrix}_{3 \times 2}$$

---

### Step 3: Compute $A^+ = V \Sigma^+ U^T$

Now we chain-multiply our three constituent components together according to the pseudo-inverse formula:

$$A^+ = \begin{bmatrix} -\frac{1}{3} & -\frac{2}{3} & \frac{2}{3} \\ -\frac{2}{3} & -\frac{1}{3} & -\frac{2}{3} \\ -\frac{2}{3} & \frac{2}{3} & \frac{1}{3} \end{bmatrix} \begin{bmatrix} \frac{1}{6\sqrt{10}} & 0 \\ 0 & \frac{1}{3\sqrt{10}} \\ 0 & 0 \end{bmatrix} \begin{bmatrix} -\frac{3}{\sqrt{10}} & \frac{1}{\sqrt{10}} \\ -\frac{1}{\sqrt{10}} & -\frac{3}{\sqrt{10}} \end{bmatrix}^T$$

#### 1. Perform the first multiplication ($V \cdot \Sigma^+$):

Since the third column of $V$ multiplies against the bottom row of zeros in $\Sigma^+$, it drops out of the calculation, reducing the operation to a $3 \times 2$ matrix:

$$V\Sigma^+ = \begin{bmatrix} \left(-\frac{1}{3} \cdot \frac{1}{6\sqrt{10}}\right) & \left(-\frac{2}{3} \cdot \frac{1}{3\sqrt{10}}\right) \\ \left(-\frac{2}{3} \cdot \frac{1}{6\sqrt{10}}\right) & \left(-\frac{1}{3} \cdot \frac{1}{3\sqrt{10}}\right) \\ \left(-\frac{2}{3} \cdot \frac{1}{6\sqrt{10}}\right) & \left(\frac{2}{3} \cdot \frac{1}{3\sqrt{10}}\right) \end{bmatrix} = \begin{bmatrix} -\frac{1}{18\sqrt{10}} & -\frac{2}{9\sqrt{10}} \\ -\frac{2}{18\sqrt{10}} & -\frac{1}{9\sqrt{10}} \\ -\frac{2}{18\sqrt{10}} & \frac{2}{9\sqrt{10}} \end{bmatrix} = \begin{bmatrix} -\frac{1}{18\sqrt{10}} & -\frac{4}{18\sqrt{10}} \\ -\frac{2}{18\sqrt{10}} & -\frac{2}{18\sqrt{10}} \\ -\frac{2}{18\sqrt{10}} & \frac{4}{18\sqrt{10}} \end{bmatrix}$$

#### 2. Transpose the $U$ matrix ($U^T$):

$$U^T = \begin{bmatrix} -\frac{3}{\sqrt{10}} & -\frac{1}{\sqrt{10}} \\ \frac{1}{\sqrt{10}} & -\frac{3}{\sqrt{10}} \end{bmatrix}$$

#### 3. Multiply $(V\Sigma^+)$ by $U^T$:

Factor out common scalar denominators ($\frac{1}{18\sqrt{10}} \cdot \frac{1}{\sqrt{10}} = \frac{1}{180}$) to simplify the calculation:

$$A^+ = \frac{1}{180} \begin{bmatrix} -1 & -4 \\ -2 & -2 \\ -2 & 4 \end{bmatrix} \begin{bmatrix} -3 & -1 \\ 1 & -3 \end{bmatrix}$$

$$A^+ = \frac{1}{180} \begin{bmatrix} (3 - 4) & (1 + 12) \\ (6 - 2) & (2 + 6) \\ (6 + 4) & (2 - 12) \end{bmatrix} = \frac{1}{180} \begin{bmatrix} -1 & 13 \\ 4 & 8 \\ 10 & -10 \end{bmatrix}$$

### Final Evaluated Solution:

Distributing the fractional denominator yields the finalized Moore-Penrose Pseudo-Inverse matrix:

$$A^+ = \begin{bmatrix} -\frac{1}{180} & \frac{13}{180} \\ \frac{1}{45} & \frac{2}{45} \\ \frac{1}{18} & -\frac{1}{18} \end{bmatrix}$$


Here are the complete, step-by-step notes based on the uploaded image. The note is formatted in clean **Markdown** (including LaTeX math syntax) so that it renders perfectly in VS Code when using any Markdown preview extension.

---


# Linear Algebra Notes: Finding Range and Null Space using SVD

This note demonstrates how Singular Value Decomposition (SVD) can be used to find the **Range** (Column Space) and **Null Space** (Kernel) of a given matrix $A$.

---

## 1. Problem Statement

Given a $2 \times 3$ matrix $A$:

$$A = \begin{bmatrix} 4 & 11 & 14 \\ 8 & 7 & -2 \end{bmatrix}$$

Find $\text{Range}(A)$ and $\text{Null}(A)$.

---

## 2. Theory & Concept

The Singular Value Decomposition of an $m \times n$ matrix $A$ of rank $r$ is given by:

$$A = U \Sigma V^T$$

Where:
* **$U$** is an $m \times m$ orthogonal matrix. The first $r$ columns of $U$ form an orthonormal basis for the **Range (Column Space)** of $A$, i.e., $\text{Range}(A)$.
* **$\Sigma$** is an $m \times n$ diagonal matrix containing the singular values $\sigma_1 \ge \sigma_2 \ge \dots \ge \sigma_r > 0$.
* **$V$** is an $n \times n$ orthogonal matrix ($V^T$ is its transpose). The last $(n - r)$ columns of $V$ (corresponding to the zero singular values) form an orthonormal basis for the **Null Space** of $A$, i.e., $\text{Null}(A)$.

---

## 3. Step-by-Step Solution

### Step 3.1: Given SVD Composition

From the given solution, the SVD factorization $A = U \Sigma V^T$ is computed as:

$$A = \begin{bmatrix} -\frac{3}{\sqrt{10}} & \frac{1}{\sqrt{10}} \\ -\frac{1}{\sqrt{10}} & -\frac{3}{\sqrt{10}} \end{bmatrix} \begin{bmatrix} 6\sqrt{10} & 0 & 0 \\ 0 & 3\sqrt{10} & 0 \end{bmatrix} \begin{bmatrix} -\frac{1}{3} & -\frac{2}{3} & -\frac{2}{3} \\ -\frac{2}{3} & -\frac{1}{3} & \frac{2}{3} \\ -\frac{2}{3} & \frac{2}{3} & -\frac{1}{3} \end{bmatrix}^T$$

Here, the rank $r = 2$ because there are 2 non-zero singular values ($\sigma_1 = 6\sqrt{10}$ and $\sigma_2 = 3\sqrt{10}$).

### Step 3.2: Finding Null(A)

The matrix $V$ is the matrix inside the transpose bracket:

$$V = \begin{bmatrix} -\frac{1}{3} & -\frac{2}{3} & -\frac{2}{3} \\ -\frac{2}{3} & -\frac{1}{3} & \frac{2}{3} \\ -\frac{2}{3} & \frac{2}{3} & -\frac{1}{3} \end{bmatrix}$$

Since matrix $A$ has $n = 3$ columns and rank $r = 2$, the dimension of the null space (nullity) is:
$$\text{dim}(\text{Null}(A)) = n - r = 3 - 2 = 1$$

Therefore, the last ($3\text{rd}$) column of $V$ spans the null space:

$$\vec{v}_3 = \begin{bmatrix} -\frac{2}{3} \\ \frac{2}{3} \\ -\frac{1}{3} \end{bmatrix}$$

Multiplying by a scalar factor of $-3$ to clear the fractions and signs gives a clean basis vector:

$$\text{Null}(A) = (-2, 2, -1)$$

---

### Step 3.3: Finding Range(A)

The matrix $U$ provides the basis for the column space (Range):

$$U = \begin{bmatrix} -\frac{3}{\sqrt{10}} & \frac{1}{\sqrt{10}} \\ -\frac{1}{\sqrt{10}} & -\frac{3}{\sqrt{10}} \end{bmatrix}$$

Since the rank $r = 2$, both columns of $U$ form the basis for $\text{Range}(A)$:

$$\vec{u}_1 = \begin{bmatrix} -\frac{3}{\sqrt{10}} \\ -\frac{1}{\sqrt{10}} \end{bmatrix}, \quad \vec{u}_2 = \begin{bmatrix} \frac{1}{\sqrt{10}} \\ -\frac{3}{\sqrt{10}} \end{bmatrix}$$

Clearing the common scaling factor $\frac{1}{\sqrt{10}}$ from each vector yields the simplified spanning vectors:

$$\text{Range}(A) = [(-3, -1), (1, -3)]$$

---

## 4. Final Answer Summary

* **$\text{Null}(A)$ Basis:** $$(-2, 2, -1)$$

* **$\text{Range}(A)$ Basis:** $$[(-3, -1), (1, -3)]$$

# Linear Algebra Notes: Operator and Matrix Norms

This note covers the mathematical definition of operator norms and how they apply to matrices, specifically focusing on the special cases where $p = 1, 2, \text{ and } \infty$.

---

## 1. Operator Norm (General Vector Spaces)

### Mathematical Definition
If $V(F)$ and $W(F)$ are vector spaces over a field $F$, we can define a set $\tau$ of all possible linear mappings from $V$ to $W$:

$$\tau = \{T \mid T : V \longrightarrow W \text{ is a linear map}\}$$

The set $\tau$ itself forms a vector space. The **operator norm** on this space $\tau$ is defined as:

$$\|T\|_{\text{op}} = \max_{X \in V, X \neq 0} \frac{\|TX\|_W}{\|X\|_V}$$

### Simple Explanation 💡
Think of a linear map $T$ as a "stretching machine" that takes a vector $X$ from space $V$ and maps it to a new vector $TX$ in space $W$. 
* The operator norm $\|T\|_{\text{op}}$ measures the **maximum possible amplification** or stretching factor that $T$ can cause to any non-zero vector $X$. 
* It answers the question: *"At most, how many times longer can a vector get after being transformed by $T$?"*

---

## 2. Matrix $p$-Norms

### Mathematical Definition
When working with matrices, a matrix $A \in \mathbb{R}^{m \times n}$ acts as a linear operator. We define the **matrix $p$-norm** as:

$$\|A\|_p = \max_{X \neq 0} \frac{\|AX\|_p}{\|X\|_p}$$

---

## 3. Special Cases for Matrix Norms ($p = 1, 2, \infty$)

When $p$ takes specific values, computing the norm becomes much simpler using structural properties of the matrix rather than optimization.

### 3.1. The 1-Norm ($\|A\|_1$) — Maximum Absolute Column Sum

#### Formula:
$$\|A\|_1 = \max_{1 \le j \le n} \sum_{i=1}^{m} |a_{ij}|$$

#### Simple Explanation 💡
1. Take the absolute value of every entry in the matrix.
2. Sum up the values in each **column** individually.
3. The largest column sum is your 1-norm.
> **Memory Trick:** The number **1** looks like a vertical column. So, $\|A\|_1$ is the **Maximum Column Sum**.

---

### 3.2. The $\infty$-Norm ($\|A\|_\infty$) — Maximum Absolute Row Sum

#### Formula:
$$\|A\|_\infty = \max_{1 \le i \le m} \sum_{j=1}^{n} |a_{ij}|$$

#### Simple Explanation 💡
1. Take the absolute value of every entry in the matrix.
2. Sum up the values in each **row** individually.
3. The largest row sum is your $\infty$-norm.
> **Memory Trick:** The infinity symbol ($\infty$) lies flat horizontally like a row. So, $\|A\|_\infty$ is the **Maximum Row Sum**.

---

### 3.3. The 2-Norm ($\|A\|_2$) — Spectral Norm

#### Formula:
$$\|A\|_2 = \sigma_1(A)$$

Where $\sigma_1(A)$ denotes the **largest singular value** of the matrix $A$.

#### Simple Explanation 💡
The 2-norm measures the maximum geometric stretching in the Euclidean space. It is calculated by finding the square root of the largest eigenvalue of the matrix $A^T A$ (which is exactly what the largest singular value $\sigma_1$ means).

---

## 4. Quick Reference Summary Table

| Norm Notation | Common Name | How to Calculate |
| :--- | :--- | :--- |
| **$\|A\|_1$** | 1-Norm / Column Norm | Maximize the sum of absolute values in any **column**. |
| **$\|A\|_\infty$** | $\infty$-Norm / Row Norm | Maximize the sum of absolute values in any **row**. |
| **$\|A\|_2$** | 2-Norm / Spectral Norm | Find the **largest singular value** ($\sigma_1$) of the matrix. |


# Linear Algebra Notes: Spectral Norm, Frobenius Norm, and Unitary Invariance

This note covers the definition of the Spectral and Frobenius norms, their relationship to singular values, and the concept of unitary invariance.

---

## 1. Spectral Norm (2-Norm)

### Mathematical Definition
The matrix 2-norm, denoted as $\|A\|_2$, is defined as:

$$\|A\|_2 = \sigma_1(A) = \max_{\lambda_i} \{|\lambda_i|\}$$

Where:
* $\sigma_1(A)$ is the **largest singular value** of the matrix $A$.
* $\lambda_i$ represents the eigenvalues of the matrix $A^T A$ (or $A A^T$), and $\sigma_i = \sqrt{\lambda_i}$.

Because it relies on the spectrum (eigenvalues/singular values) of the matrix, it is commonly called the **Spectral Norm**.

### Simple Explanation 💡
Imagine a matrix $A$ transforming a perfect geometric sphere into an ellipsoid. 
* The matrix has different scaling factors along different directions.
* The singular values ($\sigma_i$) represent the lengths of the principal axes of this new ellipsoid.
* The **Spectral Norm** is simply the length of the **longest axis** of that ellipsoid. It tells you the absolute maximum amount that any vector can be stretched by the matrix $A$.

---

## 2. Frobenius Norm

### Mathematical Definition
For a matrix $A \in \mathbb{R}^{m \times n}$, the **Frobenius norm** (denoted as $\|A\|_F$) can be computed in multiple equivalent ways:

$$\|A\|_F = \sqrt{\sum_{i=1}^{\min(m,n)} \sigma_i^2(A)} = \sqrt{\text{trace}(A^T A)}$$

*(Note: Another fundamental, direct definition is simply the square root of the sum of the absolute squares of all its elements: $\sqrt{\sum_{i=1}^m \sum_{j=1}^n |a_{ij}|^2}$)*

Where:
* $\sigma_i(A)$ are the singular values of $A$.
* $\text{trace}(A^T A)$ is the sum of the diagonal elements of the matrix $A^T A$.

### Simple Explanation 💡
Think of the Frobenius norm as the standard **Euclidean distance formula** (Pythagorean theorem) applied to a matrix. 
* If you flatten the matrix out into one long straight vector of numbers, the Frobenius norm is just the ordinary length of that long vector.
* Alternatively, it tells us that the total energy/variance of a matrix can be perfectly measured either by looking at its individual grid elements, or by looking at its singular values ($\sigma_i$).

---

## 3. Unitary Invariance

### Mathematical Definition
A matrix norm $\|\cdot\|$ is said to be **unitary invariant** (or orthogonally invariant in real spaces) if multiplying a matrix $A$ by orthogonal/unitary matrices $U$ and $V$ does not change its norm:

$$\|UAV\| = \|A\| = \|\Sigma\|$$

For all orthogonal matrices $U$ and $V$ of appropriate sizes, where $\Sigma$ is the diagonal matrix containing the singular values of $A$.

### Simple Explanation 💡
Orthogonal (or unitary) matrices represent pure **rotations** or **reflections** in space. They change directions, but they never stretch or alter lengths.
* Unitary invariance means that if you rotate a matrix from the left ($U$) and rotate it from the right ($V$), its intrinsic "size" or norm remains completely unchanged.
* Because of this property, the norm depends strictly on the matrix's singular values ($\Sigma$), completely ignoring how the matrix is rotated in space.
* Both the **Spectral Norm** ($\|A\|_2$) and the **Frobenius Norm** ($\|A\|_F$) are classical examples of unitary invariant norms.

---

## 4. Quick Comparison Summary Table

| Norm Property | Spectral Norm ($\|A\|_2$) | Frobenius Norm ($\|A\|_F$) |
| :--- | :--- | :--- |
| **Focus** | Measures the **maximum stretching** along a single worst-case direction. | Measures the **total size/energy** contained across all dimensions. |
| **SVD Formula** | $\sigma_{\max}$ (Just the largest singular value) | $\sqrt{\sigma_1^2 + \sigma_2^2 + \dots + \sigma_r^2}$ (Root sum of all squared singular values) |
| **Unitary Invariant?**| **Yes** ($\|UAV\|_2 = \|A\|_2$) | **Yes** ($\|UAV\|_F = \|A\|_F$) |




# Linear Algebra Example: Computing Matrix Norms

This practical note walks through computing the **1-norm**, **$\infty$-norm**, **2-norm (Spectral norm)**, and **Frobenius norm** for a specific $3 \times 3$ matrix.

---

## 1. Problem Statement

Given the matrix $A$:

$$A = \begin{bmatrix} 0 & 1 & 1 \\ \sqrt{2} & 2 & 0 \\ 0 & 1 & 1 \end{bmatrix}$$

Calculate the following norms:
1. $\|A\|_1$ (Maximum Absolute Column Sum)
2. $\|A\|_\infty$ (Maximum Absolute Row Sum)
3. $\|A\|_2$ (Spectral Norm / Largest Singular Value)
4. $\|A\|_F$ (Frobenius Norm)

---

## 2. Step-by-Step Calculations

### Step 2.1: Finding the 1-Norm ($\|A\|_1$)
The 1-norm requires summing up the absolute values of the entries in each **column** and choosing the maximum sum.

* **Column 1 Sum:** $|0| + |\sqrt{2}| + |0| = \sqrt{2} \approx 1.414$
* **Column 2 Sum:** $|1| + |2| + |1| = 4$
* **Column 3 Sum:** $|1| + |0| + |1| = 2$

$$\|A\|_1 = \max \{\sqrt{2}, 4, 2\} = 4$$

> **Simple Meaning:** Look down each vertical column, add up the magnitudes, and pick the largest total. Column 2 has the highest value of 4.

---

### Step 2.2: Finding the $\infty$-Norm ($\|A\|_\infty$)
The $\infty$-norm requires summing up the absolute values of the entries in each **row** and choosing the maximum sum.

* **Row 1 Sum:** $|0| + |1| + |1| = 2$
* **Row 2 Sum:** $|\sqrt{2}| + |2| + |0| = 2 + \sqrt{2} \approx 3.414$
* **Row 3 Sum:** $|0| + |1| + |1| = 2$

$$\|A\|_\infty = \max \{2, 2 + \sqrt{2}, 2\} = 2 + \sqrt{2}$$

> **Simple Meaning:** Scan across each horizontal row, add up the magnitudes, and pick the largest total. Row 2 yields the maximum value of $2 + \sqrt{2}$.

---

### Step 2.3: Finding the Frobenius Norm ($\|A\|_F$)
The Frobenius norm can be calculated directly by taking the square root of the sum of all squared entries, which is mathematically equivalent to $\sqrt{\text{trace}(A^T A)}$. Let's do both to see why they match.

#### Method A: Direct Entry Summation
Square every entry in matrix $A$ and add them together:

$$\sum |a_{ij}|^2 = (0)^2 + (1)^2 + (1)^2 + (\sqrt{2})^2 + (2)^2 + (0)^2 + (0)^2 + (1)^2 + (1)^2$$
$$\sum |a_{ij}|^2 = 0 + 1 + 1 + 2 + 4 + 0 + 0 + 1 + 1 = 10$$

Now, take the square root:
$$\|A\|_F = \sqrt{10}$$

#### Method B: Trace Method (As shown in handwritten notes)
1. First, find $A^T$:
   $$A^T = \begin{bmatrix} 0 & \sqrt{2} & 0 \\ 1 & 2 & 1 \\ 1 & 0 & 1 \end{bmatrix}$$

2. Multiply $A^T$ by $A$:
   $$A^T A = \begin{bmatrix} 0 & \sqrt{2} & 0 \\ 1 & 2 & 1 \\ 1 & 0 & 1 \end{bmatrix} \begin{bmatrix} 0 & 1 & 1 \\ \sqrt{2} & 2 & 0 \\ 0 & 1 & 1 \end{bmatrix} = \begin{bmatrix} 2 & 2\sqrt{2} & 0 \\ 2\sqrt{2} & 6 & 2 \\ 0 & 2 & 2 \end{bmatrix}$$

3. Find the **Trace** (the sum of the main diagonal elements of $A^T A$):
   $$\text{Trace}(A^T A) = 2 + 6 + 2 = 10$$

4. Take the square root:
   $$\|A\|_F = \sqrt{\text{Trace}(A^T A)} = \sqrt{10}$$

---

### Step 2.4: Finding the 2-Norm / Spectral Norm ($\|A\|_2$)
The 2-norm is equal to the largest singular value ($\sigma_1$) of $A$, which is the square root of the largest eigenvalue ($\lambda_{\max}$) of the matrix $A^T A$ we calculated above.

#### 1. Set up the Characteristic Equation for $A^T A$:
$$\det(A^T A - \lambda I) = 0$$

$$\det \begin{bmatrix} 2-\lambda & 2\sqrt{2} & 0 \\ 2\sqrt{2} & 6-\lambda & 2 \\ 0 & 2 & 2-\lambda \end{bmatrix} = 0$$

#### 2. Solve for Eigenvalues ($\lambda$):
Expanding along the first row:
$$(2-\lambda) \cdot \left[ (6-\lambda)(2-\lambda) - 4 \right] - 2\sqrt{2} \cdot \left[ 2\sqrt{2}(2-\lambda) - 0 \right] = 0$$

$$(2-\lambda) \cdot [\lambda^2 - 8\lambda + 12 - 4] - 8(2-\lambda) = 0$$

Factor out the common term $(2-\lambda)$:
$$(2-\lambda) \cdot [(\lambda^2 - 8\lambda + 8) - 8] = 0$$
$$(2-\lambda) \cdot (\lambda^2 - 8\lambda) = 0$$
$$\lambda(2-\lambda)(\lambda-8) = 0$$

The eigenvalues are:
$$\lambda_1 = 8, \quad \lambda_2 = 2, \quad \lambda_3 = 0$$

#### 3. Calculate Singular Values ($\sigma_i = \sqrt{\lambda_i}$):
* $\sigma_1 = \sqrt{8} = 2\sqrt{2}$ (Largest)
* $\sigma_2 = \sqrt{2}$
* $\sigma_3 = 0$

$$\|A\|_2 = \sigma_1(A) = 2\sqrt{2}$$

---

## 3. Final Summary Table

| Norm Type | Exact Solution | Approximate Decimal |
| :--- | :--- | :--- |
| **1-Norm ($\|A\|_1$)** | $4$ | $4.000$ |
| **$\infty$-Norm ($\|A\|_\infty$)** | $2 + \sqrt{2}$ | $3.414$ |
| **2-Norm ($\|A\|_2$)** | $2\sqrt{2}$ | $2.828$ |
| **Frobenius Norm ($\|A\|_F$)** | $\sqrt{10}$ | $3.162$ |

