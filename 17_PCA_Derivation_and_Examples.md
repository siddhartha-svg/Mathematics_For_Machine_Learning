# PCA Part III: Mathematical Derivation and Representation Error

This note covers the foundational setup for the mathematical derivation of Principal Component Analysis (PCA). It explains how a high-dimensional vector is projected onto a lower-dimensional subspace and formulates the structural Mean Squared Error (MSE) of this approximation.

---

## 1. Concept Name: Mathematical Derivation of PCA

### Simple Meaning 💡
The ultimate goal of PCA is to compress a dataset by reducing its dimensions (e.g., from an $n$-dimensional space down to a smaller $m$-dimensional space) while keeping as much of the original data's variance ("randomness") as possible. 

To derive this mathematically, we start by expressing our full vector $X$ using a complete set of $n$ unique, perpendicular building blocks called an **orthonormal basis**. Compression happens when we decide to keep only the first $m$ important blocks, and replace the remaining coordinates with simple, fixed average constants ($b_i$).


---

### Step-by-Step Mathematical Formulation

#### Step 1.1: Exact Vector Representation
Let $X$ be an $n$-dimensional random vector. We can write $X$ perfectly as a linear combination of an orthonormal basis $\{\phi_1, \phi_2, \dots, \phi_n\}$:

$$X = \sum_{i=1}^{n} y_i \phi_i$$

Where $y_i$ is the coordinate scalar along the basis direction $\phi_i$. Because the basis is orthonormal, each coordinate is found via an inner product (projection):
$$y_i = \langle X, \phi_i \rangle = X^T \phi_i \quad \forall \ i = 1, 2, \dots, n$$

#### Step 1.2: Truncated Low-Rank Approximation ($\hat{X}$)
If we want to reduce the dimension to $m$ (where $m < n$), we keep the exact coordinates for the first $m$ vectors. For the remaining channels from $m+1$ to $n$, we replace the random variables $y_i$ with pre-selected constants $b_i$. This yields our approximation vector $\hat{X}(m)$:

$$\hat{X}(m) = \sum_{i=1}^{m} y_i \phi_i + \sum_{i=m+1}^{n} b_i \phi_i$$

---

## 2. Concept Name: The Representation Error Matrix ($\Delta X$)

### Definition
The **Representation Error** (or residual vector) measures what was lost during compression. It is defined as the absolute difference between the true vector $X$ and our low-rank approximation $\hat{X}(m)$:

$$\Delta X(m) = X - \hat{X}(m)$$

### Step-by-Step Calculation:
1. Substitute the formulas from Step 1.1 and 1.2:
   $$\Delta X(m) = \left( \sum_{i=1}^{m} y_i \phi_i + \sum_{i=m+1}^{n} y_i \phi_i \right) - \left( \sum_{i=1}^{m} y_i \phi_i + \sum_{i=m+1}^{n} b_i \phi_i \right)$$

2. Notice that the first $m$ terms cancel out completely:
   $$\Delta X(m) = \sum_{i=m+1}^{n} y_i \phi_i - \sum_{i=m+1}^{n} b_i \phi_i$$

3. Group the remaining summation boundaries together:
   $$\Delta X(m) = \sum_{i=m+1}^{n} (y_i - b_i) \phi_i$$

---

## 3. Formulating the Mean Squared Error (MSE)

To optimize PCA, we need to minimize the expected value of the squared magnitude of our error vector, written as $E\left[|\Delta X|^2\right]$.

### Step-by-Step Algebraic Expansion:
1. Express the squared magnitude as a vector dot product:
   $$E\left[|\Delta X|^2\right] = E\left[ \left( \sum_{i=m+1}^{n} (y_i - b_i)\phi_i \right) \cdot \left( \sum_{j=m+1}^{n} (y_j - b_j)\phi_j \right) \right]$$

2. Distribute the terms using two separate summation indices ($i$ and $j$):
   $$E\left[|\Delta X|^2\right] = E\left[ \sum_{i=m+1}^{n} \sum_{j=m+1}^{n} (y_i - b_i)(y_j - b_j) \phi_i^T \phi_j \right]$$

3. Apply the Orthonormality Property:
   Because the basis vectors are perfectly perpendicular, their dot product $\phi_i^T \phi_j$ collapses completely:
   $$\phi_i^T \phi_j = \begin{cases} 1 & \text{if } i = j \\ 0 & \text{if } i \neq j \end{cases}$$

4. Since all cross-terms where $i \neq j$ vanish into zero, the double summation collapses back into a single clean sum where $i = j$:
   $$E\left[|\Delta X|^2\right] = \sum_{i=m+1}^{n} E\left[(y_i - b_i)^2\right]$$

---

## 4. Practice Problems with Solutions

### Problem 1: Orthogonal Vector Cancellation Verification
**Scenario:** Prove manually using a 2D orthonormal basis why the cross-multiplication term $\phi_i^T \phi_j$ disappears when $i \neq j$. Let:
$$\phi_1 = \begin{bmatrix} 1 \\ 0 \end{bmatrix}, \quad \phi_2 = \begin{bmatrix} 0 \\ 1 \end{bmatrix}$$

#### Step-by-Step Calculation:
1. Compute the dot product $\phi_1^T \phi_2$:
   $$\phi_1^T \phi_2 = \begin{bmatrix} 1 & 0 \end{bmatrix} \begin{bmatrix} 0 \\ 1 \end{bmatrix} = (1 \times 0) + (0 \times 1) = 0$$
2. Compute the squared magnitude $\phi_1^T \phi_1$:
   $$\phi_1^T \phi_1 = \begin{bmatrix} 1 & 0 \end{bmatrix} \begin{bmatrix} 1 \\ 0 \end{bmatrix} = (1 \times 1) + (0 \times 0) = 1$$

#### Solution Conclusion:
This calculation verifies the simplification step used in the derivation. Because the vectors are orthogonal, all cross-terms drop out, leaving only the standalone squared variances.

---

### Problem 2: Finding the Optimal Substitution Constant ($b_i$)
**Scenario:** Look closely at the final single-sum error formula:
$$\text{MSE} = \sum_{i=m+1}^{n} E\left[(y_i - b_i)^2\right]$$
Find the mathematical value for the constant $b_i$ that minimizes this error.

#### Step-by-Step Derivation:
1. To minimize the error with respect to $b_i$, take the partial derivative of the expected value and set it to zero:
   $$\frac{\partial}{\partial b_i} E\left[(y_i - b_i)^2\right] = 0$$
2. Pass the derivative inside the expectation operator:
   $$E\left[ 2(y_i - b_i) \cdot (-1) \right] = 0$$
   $$-2 E[y_i] + 2 b_i = 0$$
3. Solve directly for $b_i$:
   $$2 b_i = 2 E[y_i] \implies b_i = E[y_i]$$

#### Solution Conclusion:
To minimize representation error, the optimal choice for the constant $b_i$ is simply **$E[y_i]$** (the expected value or mean of that coordinate channel). This proves that when PCA discards a dimension, it replaces it with its baseline average value.


# Mathematical Derivation of PCA: Minimizing Reconstruction Error

This note provides a step-by-step mathematical derivation of **Principal Component Analysis (PCA)** framed as an optimization problem: minimizing the mean squared reconstruction error. 

---

## 1. Concept Name: Total Reconstruction Error Minimization

### Simple Meaning 💡
When compressing data from a high-dimensional space down to a lower-dimensional subspace, we inevitably lose some information. 
* The difference between the original data point and its compressed version is the **reconstruction error** (or representation error).
* To find the absolute best directions (principal components) to project our data onto, we mathematically minimize this error.
* The derivation proves that minimizing this error is equivalent to selecting the eigenvectors corresponding to the largest eigenvalues of the data's covariance matrix.

---

## 2. Step-by-Step Derivation & Calculations

### Step 2.1: The Error Formulation & Finding $b_i$
Let the expected squared reconstruction error be defined as:
$$E\left[|\Delta x|^2\right] = \sum_{i=m+1}^{n} E\left[(y_i - b_i)^2\right]$$

Where:
* $n$ is the total original dimensions.
* $m$ is the number of dimensions we keep.
* The index runs from $m+1$ to $n$, representing the discarded dimensions.
* $b_i$ is a deterministic scalar shift parameter we need to optimize first.

To find the optimal $b_i$ that minimizes this error, we take the partial derivative with respect to $b_i$ and set it to $0$:
$$\frac{\partial E\left[|\Delta x|^2\right]}{\partial b_i} = 0 \implies -2\left(E[y_i - b_i]\right) = 0$$

Since $b_i$ is a constant scalar, $E[b_i] = b_i$. Thus:
$$E[y_i] - b_i = 0 \implies b_i = E[y_i]$$

> **Simple Meaning 💡:** The optimal scalar offset $b_i$ is simply the expected value (mean) of the coordinate projection $y_i$.

---

### Step 2.2: Substituting $b_i$ and introducing Covariance
Substitute $b_i = E[y_i]$ back into the error equation:
$$E\left[|\Delta x|^2\right] = \sum_{i=m+1}^{n} E\left[\left(y_i - E[y_i]\right)^2\right]$$

Since $y_i$ is the projection of the data vector $x$ onto the direction vector $\phi_i$, we write $y_i = x^T \phi_i$. Substituting this in:
$$E\left[|\Delta x|^2\right] = \sum_{i=m+1}^{n} E\left[\left(x^T \phi_i - E[x^T \phi_i]\right)^2\right]$$

Using the linearity of expectation and rearranging terms:
$$E\left[|\Delta x|^2\right] = \sum_{i=m+1}^{n} \phi_i^T E\left[(x - E[x])(x - E[x])^T\right] \phi_i$$

Notice that the inner expectation expression $E\left[(x - E[x])(x - E[x])^T\right]$ is exactly the definition of the **Data Covariance Matrix ($\Sigma_x$)**:
$$E\left[|\Delta x|^2\right] = \sum_{i=m+1}^{n} \phi_i^T \Sigma_x \phi_i \quad \text{--- (Equation 3)}$$

---

### Step 2.3: Constrained Optimization via Lagrange Multipliers
Now, we want to find the direction vectors $\phi_i$ that minimize this total error. However, to keep it physically meaningful, the vectors must be unit vectors ($\phi_i^T \phi_i = 1$). 

We formulate a constrained minimization objective function $J(\phi_i)$ using Lagrange Multipliers ($\lambda_i$):
$$\min_{\phi_i} J(\phi_i) = \min_{\phi_i} \sum_{i=m+1}^{n} \phi_i^T \Sigma_x \phi_i + \sum_{i=m+1}^{n} \lambda_i (1 - \phi_i^T \phi_i)$$

Take the derivative with respect to $\phi_i$ and set it to $0$:
$$\frac{\partial J(\phi_i)}{\partial \phi_i} = 0 \implies 2\Sigma_x \phi_i - 2\lambda_i \phi_i = 0$$
$$\Sigma_x \phi_i = \lambda_i \phi_i \quad \text{--- (Equation 4)}$$

> **Crucial Linear Algebra Insight:** This is the classic definition of an eigenvalue problem! It proves that the optimal projection directions $\phi_i$ are **eigenvectors** of the covariance matrix $\Sigma_x$, and $\lambda_i$ are their corresponding **eigenvalues**.

---

### Step 2.4: The Final Selection Rule
Substitute the eigenvalue relationship from Equation 4 ($\Sigma_x \phi_i = \lambda_i \phi_i$) back into our Equation 3 total error expression:
$$E\left[|\Delta x|^2\right] = \sum_{i=m+1}^{n} \phi_i^T (\lambda_i \phi_i)$$

Since $\phi_i^T \phi_i = 1$, the equation simplifies directly to:
$$E\left[|\Delta x|^2\right] = \sum_{i=m+1}^{n} \lambda_i$$

#### Conclusion 💡
The total reconstruction error is exactly the **sum of the eigenvalues of the discarded dimensions**. 
* In order to make this error as small as possible, the eigenvalues $\lambda_i$ in this summation **must be the smallest possible eigenvalues**.
* Consequently, the dimensions we *keep* must correspond to the **largest eigenvalues**.
* **Therefore, in PCA, we choose the $m$ eigenvectors corresponding to the $m$ largest eigenvalues of the covariance matrix $\Sigma_x$ as our principal directions.**

---

## 3. Practice Problems with Solutions

### Problem 1: Calculating Reconstruction Error from Discarded Dimensions
**Scenario:** A data scientist runs PCA on a 4-dimensional dataset. The eigenvalues calculated from the covariance matrix are:
$$\lambda_1 = 45.2, \quad \lambda_2 = 20.8, \quad \lambda_3 = 1.5, \quad \lambda_4 = 0.5$$

If the data is compressed from 4 dimensions down to 2 dimensions ($m=2$), calculate the exact expected reconstruction error.

#### Step-by-Step Calculation:
1. Identify the kept dimensions: The top 2 largest eigenvalues ($\lambda_1$ and $\lambda_2$).
2. Identify the discarded dimensions: The remaining trailing eigenvalues ($\lambda_3$ and $\lambda_4$).
3. Sum the discarded eigenvalues to find total reconstruction error:
   $$\text{Error} = \sum_{i=3}^{4} \lambda_i = \lambda_3 + \lambda_4$$
   $$\text{Error} = 1.5 + 0.5 = 2.0$$

#### Solution Conclusion:
The expected reconstruction error is exactly **$2.0$**. Since the total variance of the system was $45.2 + 20.8 + 1.5 + 0.5 = 68.0$, this minor error represents a loss of only $\frac{2.0}{68.0} \approx 2.94\%$ of the data information.

---

### Problem 2: Proving Constraint Verification
**Scenario:** Show why the derivative step $\frac{\partial}{\partial \phi} (\phi^T \Sigma \phi) = 2\Sigma\phi$ holds true for a symmetric matrix $\Sigma$.

#### Step-by-Step Mathematical Verification:
Let's consider a basic 2D case where $\phi = \begin{bmatrix} x \\ y \end{bmatrix}$ and symmetric $\Sigma = \begin{bmatrix} a & b \\ b & c \end{bmatrix}$.

1. Expand the quadratic form $\phi^T \Sigma \phi$:
   $$\phi^T \Sigma \phi = \begin{bmatrix} x & y \end{bmatrix} \begin{bmatrix} a & b \\ b & c \end{bmatrix} \begin{bmatrix} x \\ y \end{bmatrix} = \begin{bmatrix} x & y \end{bmatrix} \begin{bmatrix} ax + by \\ bx + cy \end{bmatrix}$$
   $$\phi^T \Sigma \phi = x(ax + by) + y(bx + cy) = ax^2 + 2bxy + cy^2$$

2. Take the gradient vector with respect to $\phi$ (i.e., partial derivatives with respect to $x$ and $y$):
   $$\frac{\partial}{\partial x}(ax^2 + 2bxy + cy^2) = 2ax + 2by$$
   $$\frac{\partial}{\partial y}(ax^2 + 2bxy + cy^2) = 2bx + 2cy$$

3. Re-assemble back into vector matrix notation:
   $$\nabla (\phi^T \Sigma \phi) = \begin{bmatrix} 2ax + 2by \\ 2bx + 2cy \end{bmatrix} = 2 \begin{bmatrix} a & b \\ b & c \end{bmatrix} \begin{bmatrix} x \\ y \end{bmatrix} = 2\Sigma\phi$$

#### Solution Conclusion:
This algebraic check explicitly verifies the matrix derivative shorthand used in step 2.3 of the optimization proof.



# Mathematical Connection: PCA and SVD with 2D Numerical Example

This note covers the deep algebraic relationship connecting Principal Component Analysis (PCA) and Singular Value Decomposition (SVD), followed by a complete step-by-step numerical calculation for a 2D dataset.

---

## 1. Concept Name: The SVD-PCA Link

### Simple Meaning 💡
* In **PCA**, our core goal is to find the eigenvectors of the data's covariance matrix $\Sigma$.
* In **SVD**, we factorize the raw data matrix directly into $U$, $S$, and $V^T$ without manually building a covariance matrix first.
* The mathematical derivation below proves a beautiful shortcut: **The right singular vectors (the columns of matrix $V$) from the SVD of the data matrix are exactly equal to the principal component eigenvectors of the covariance matrix.** ---

### Step-by-Step Mathematical Derivation

Let a zero-mean, centered data matrix be $C$ of size $n \times p$. 
The standard sample covariance matrix is defined as:
$$\Sigma = \frac{1}{n-1} C^T C \quad \text{(a } p \times p \text{ matrix)}$$

Now, substitute the Singular Value Decomposition of $C$ ($C = U S V^T$) directly into the covariance formula:
$$\Sigma = \frac{1}{n-1} (U S V^T)^T \cdot (U S V^T)$$

Apply the socks-and-shoes transpose rule $(ABC)^T = C^T B^T A^T$:
$$\Sigma = \frac{1}{n-1} (V S^T U^T) \cdot (U S V^T)$$

Since $U$ is an orthonormal matrix, its transpose multiplied by itself yields the Identity matrix ($U^T U = I$). Also, because $S$ is diagonal, $S^T = S$:
$$\Sigma = \frac{1}{n-1} V S (I) S V^T$$
$$\Sigma = \frac{1}{n-1} V S^2 V^T$$

#### Strategic Insight 💡
Look closely at this final structure: $\Sigma = V \left(\frac{S^2}{n-1}\right) V^T$. This is exactly the format of an **orthogonal eigendecomposition** ($X \Lambda X^T$). 

This formally proves that:
1. The columns of **$V$** are the **eigenvectors** of the covariance matrix $\Sigma$ (the Principal Directions).
2. The eigenvalues $\lambda_i$ of the covariance matrix are directly related to the singular values $\sigma_i$ by the formula:
$$\lambda_i = \frac{\sigma_i^2}{n-1}$$
3. The actual low-rank principal components are computed directly by projecting the data onto $V$:
$$\text{Principal Components} = C V = (U S V^T) V = U S$$

---

## 2. Concept Name: Variance / Information Preservation

When we choose to keep only the top $k$ principal components out of a total of $n$ available directions, the percentage of total dataset information preserved is calculated using the eigenvalues:

$$\text{Information Preserved (\%)} = \frac{|\lambda_1| + |\lambda_2| + \dots + |\lambda_k|}{|\lambda_1| + |\lambda_2| + \dots + |\lambda_n|} \times 100$$

---

## 3. Step-by-Step Numerical Example (2D Data)

### Problem Statement
Compute the Principal Components for the following $8 \times 2$ centered data matrix tracking coordinates $X = (x_1, x_2)$:
$$X = \{(1,2), (3,3), (3,5), (5,4), (5,6), (6,5), (8,7), (9,8)\}$$

---

### Step 3.1: Construct the Covariance Matrix $\Sigma_x$
Given that the matrix has $n = 8$ observations, the factor $\frac{1}{n-1} = \frac{1}{7}$. The pre-calculated matrix product $C^T C$ divided by $7$ yields:

$$\Sigma_x = \frac{1}{7} C^T C = \begin{bmatrix} 6.25 & 4.25 \\ 4.25 & 3.5 \end{bmatrix}$$

---

### Step 3.2: Compute the Eigenvalues ($\lambda$)
To find the eigenvalues, we solve the characteristic equation $\det(\Sigma_x - \lambda I) = 0$:

$$\det \begin{bmatrix} 6.25 - \lambda & 4.25 \\ 4.25 & 3.5 - \lambda \end{bmatrix} = 0$$
$$(6.25 - \lambda)(3.5 - \lambda) - (4.25)^2 = 0$$
$$21.875 - 6.25\lambda - 3.5\lambda + \lambda^2 - 18.0625 = 0$$
$$\lambda^2 - 9.75\lambda + 3.8125 = 0$$

Using the quadratic formula $\lambda = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}$:
$$\lambda = \frac{9.75 \pm \sqrt{(-9.75)^2 - 4(1)(3.8125)}}{2}$$
$$\lambda = \frac{9.75 \pm \sqrt{95.0625 - 15.25}}{2} = \frac{9.75 \pm \sqrt{79.8125}}{2}$$
$$\lambda = \frac{9.75 \pm 8.9338}{2}$$

Sorting them from largest to smallest gives:
* $\lambda_1 = \frac{9.75 + 8.9338}{2} = 9.3419$  *(Dominant Component)*
* $\lambda_2 = \frac{9.75 - 8.9338}{2} = 0.4081$

---

### Step 3.3: Compute the Eigenvectors ($\vec{v}$)

Now, we calculate the directional eigenvector $\vec{v}_1 = \begin{bmatrix} v_a \\ v_b \end{bmatrix}$ matching our dominant eigenvalue $\lambda_1 = 9.3419$:

$$(\Sigma_x - \lambda_1 I)\vec{v}_1 = 0$$
$$\begin{bmatrix} 6.25 - 9.3419 & 4.25 \\ 4.25 & 3.5 - 9.3419 \end{bmatrix} \begin{bmatrix} v_a \\ v_b \end{bmatrix} = \begin{bmatrix} 0 \\ 0 \end{bmatrix}$$
$$\begin{bmatrix} -3.0919 & 4.25 \\ 4.25 & -5.8419 \end{bmatrix} \begin{bmatrix} v_a \\ v_b \end{bmatrix} = \begin{bmatrix} 0 \\ 0 \end{bmatrix}$$

From the first row equation:
$$-3.0919 v_a + 4.25 v_b = 0 \implies v_b = \frac{3.0919}{4.25} v_a \approx 0.7275 v_a$$

We enforce the unit length normalization constraint ($v_a^2 + v_b^2 = 1$):
$$v_a^2 + (0.7275 v_a)^2 = 1$$
$$v_a^2 + 0.5293 v_a^2 = 1 \implies 1.5293 v_a^2 = 1$$
$$v_a = \sqrt{\frac{1}{1.5293}} \approx 0.8086$$
$$v_b = 0.7275 \times 0.8086 \approx 0.5883$$

This gives our two computed orthogonal coordinate eigenvectors matching the slide details:
$$\vec{v}_1 = \begin{bmatrix} 0.5883 \\ 0.8086 \end{bmatrix}, \quad \vec{v}_2 = \begin{bmatrix} 0.5883 \\ -0.8086 \end{bmatrix}$$

---

### Step 3.4: Final PCA Linear Equation
Using the coefficients from the dominant eigenvector $\vec{v}_1$, the optimal line equation transforming our 2D data down into a 1D vector line space is:

$$y = 0.5883x_1 + 0.8086x_2$$

---

## 4. Supplementary Practice Problem with Solution

### Problem: Computing Information Retention Quality
Using the eigenvalues calculated from the numerical 2D problem above ($\lambda_1 = 9.3419$, $\lambda_2 = 0.4081$), calculate the exact percentage of information preserved if we drop the second axis and project the data completely into a 1D space.

#### Step-by-Step Calculation:
1. Find Total System Variance ($\lambda_1 + \lambda_2$):
   $$\text{Total Variance} = 9.3419 + 0.4081 = 9.7500$$
2. Divide the kept dominant component by the total variance:
   $$\text{Preserved Information} = \frac{9.3419}{9.7500} \times 100$$
   $$\text{Preserved Information} = 0.95814 \times 100 \approx 95.81\%$$

#### Conclusion
By compressing the data from a 2D plane down to our 1D line equation $y$, we discard half the structural coordinates but retain a massive **$95.81\%$** of the overall dataset variance!



