# Linear Algebra Notes: SVD Overview and Structural Foundations

This note covers the core learning outcomes of Singular Value Decomposition (SVD), its stability compared to other techniques, and a breakdown of its basic matrix dimensions.

---

## 1. Learning Outcomes & Real-World Value

Singular Value Decomposition (SVD) is one of the most popular, widely used factorization methods in modern linear algebra and data science.

### Why Use SVD Over Eigendecomposition?

* **Universal Applicability:** Eigendecomposition ($A = X \Lambda X^{-1}$) requires a matrix to be strictly **square** ($n \times n$). SVD can be applied to **any** matrix of any shape (rectangular, tall, wide, or square).
* **Numerical Stability:** SVD uses orthogonal transformations, which prevents rounding errors from blowing up. It is computationally more stable, dependable, and less sensitive to minor data alterations than traditional eigenvalue methods.

### Core Big-Data Applications 💡

* **Compressing:** Reducing file sizes (like images or large database structures) while preserving the core informational content.
* **Denoising:** Stripping out weak singular value channels to clean background white noise from signals or datasets.
* **Data Reduction:** Dropping redundant parameters to feed cleaner, smaller arrays into machine learning pipelines (e.g., Principal Component Analysis, or PCA).

---

## 2. Core Structure: What is SVD?

SVD states that any real $m \times n$ matrix $A$ can be broken down into three distinct, specialized matrices:

$$A = U S V^T$$

*(Note: In your handwritten slide, $S$ is used as a common placeholder variable for the singular matrix $\Sigma$.)*

### Dimension Slicing Breakdown

When you multiply these three matrices together, their inner dimensions must perfectly align following classic matrix multiplication rules:

$$\underbrace{A}_{m \times n} = \underbrace{U}_{m \times m} \cdot \underbrace{S}_{m \times n} \cdot \underbrace{V^T}_{n \times n}$$

---

## 3. Explaining the Components in Simple Terms 💡

* **Matrix $A$ ($m \times n$):** Your raw data matrix. For example, $m$ rows could represent users and $n$ columns could represent movie ratings.
* **Matrix $U$ ($m \times m$):** An orthogonal matrix containing the **left singular vectors**. Geometrically, this handles spatial rotations and links your row entries to their latent, hidden concepts.
* **Matrix $S$ ($m \times n$):** A rectangular diagonal matrix. It contains the **singular values** sorted from largest to smallest along its diagonal. These values act as scaling dials, measuring the relative strength and importance of each hidden concept.
* **Matrix $V^T$ ($n \times n$):** The transpose of an orthogonal matrix containing the **right singular vectors**. This handles the secondary structural rotation and links your column items to those same latent concepts.

---

## 4. Analytical Dimensional Calculations

To ensure your code blocks or manual matrix assemblies are structurally valid, you must verify that the dimension chains collapse properly.

### Step-by-Step Dimensional Reduction Calculation:

Given:

* $\text{Dim}(U) = m \times m$
* $\text{Dim}(S) = m \times n$
* $\text{Dim}(V^T) = n \times n$

#### Step 4.1: Multiply the First Two Matrices ($U \cdot S$)

When multiplying an $(m \times \color{blue}m)$ matrix by an $(\color{blue}m \times n)$ matrix, the inner dimensions ($\color{blue}m$) must match. The resulting intermediate matrix takes the outer boundaries:

$$\text{Dim}(US) = m \times n$$

#### Step 4.2: Multiply the Intermediate Result by the Last Matrix ($(US) \cdot V^T$)

Now, multiply our intermediate $(m \times \color{red}n)$ matrix by the final $(\color{red}n \times n)$ matrix $V^T$. The inner dimensions ($\color{red}n$) match perfectly. The final dimensions take the outer bounds:

$$\text{Dim}(A) = m \times n$$

This verifies that the algebraic structure $U S V^T$ accurately returns a matrix of size $m \times n$.

---

## 5. What is Reconstruction?

The final heading **"Reconstruction"** on your slide refers to multiplying these components back together.

* **Full Reconstruction:** If you multiply the complete matrices $U$, $S$, and $V^T$ together using their full dimensions, you perfectly recreate the exact original matrix $A$ without changing a single value.
* **Partial/Low-Rank Reconstruction:** If you truncate $S$ to only use its top $k$ diagonal elements and slice $U$ and $V^T$ accordingly, the multiplication generates a smoothed, compressed approximation matrix ($A_k$). This forms the basis for the python implementations discussed in the upcoming lecture.




# Python Implementation of SVD using NumPy

This note provides a comprehensive walkthrough of computing Singular Value Decomposition (SVD) programmatically in Python using NumPy, matching the structure of the provided Jupyter Notebook slides.

---

## 1. Mathematical Concept Recap

Any real rectangular matrix $A \in \mathbb{R}^{m \times n}$ can be factored using SVD into three constituent matrices:

$$A = U \Sigma V^T$$

Where:
* $U$ is an $m \times m$ **orthogonal (orthonormal) matrix** containing the left singular vectors.
* $\Sigma$ is an $m \times n$ **diagonal matrix** containing sorted singular values ($\sigma_1 \ge \sigma_2 \ge \dots \ge \sigma_k \ge 0$).
* $V^T$ is an $n \times n$ **orthogonal (orthonormal) matrix** containing the right singular vectors.

---

## 2. Step-by-Step Python Implementation Breakdown

### Step 2.1: Initialization and Printing Setup
We first configure NumPy to print arrays with an easy-to-read precision format and suppress small values near zero from appearing in scientific notation.

```python
import numpy as np

# Set formatting options for clear printing
np.set_printoptions(precision=4, suppress=True)

```

---

### Step 2.2: Define the Rectangular Matrix

We initialize a simple $3 \times 4$ rectangular matrix ($m = 3$ rows, $n = 4$ columns):

```python
a = np.array([[1, 2, 3, 4], 
              [1, 1, 2, 3], 
              [0, 1, 1, 0]])
print(a)

```

**Output:**

```text
[[1 2 3 4]
 [1 1 2 3]
 [0 1 1 0]]

```

---

### Step 2.3: Structural Dimensional Target

Our $3 \times 4$ matrix will decompose into the following precise geometric dimension blocks:

$$\underbrace{\begin{bmatrix} 1 & 2 & 3 & 4 \\ 1 & 1 & 2 & 3 \\ 0 & 1 & 1 & 0 \end{bmatrix}}_{A \; (3 \times 4)} = \underbrace{\begin{bmatrix} \cdot & \cdot & \cdot \\ \cdot & \cdot & \cdot \\ \cdot & \cdot & \cdot \end{bmatrix}}_{U \; (3 \times 3)} \cdot \underbrace{\begin{bmatrix} \sigma_1 & 0 & 0 & 0 \\ 0 & \sigma_2 & 0 & 0 \\ 0 & 0 & \sigma_3 & 0 \end{bmatrix}}_{\Sigma \; (3 \times 4)} \cdot \underbrace{\begin{bmatrix} \cdot & \cdot & \cdot & \cdot \\ \cdot & \cdot & \cdot & \cdot \\ \cdot & \cdot & \cdot & \cdot \\ \cdot & \cdot & \cdot & \cdot \end{bmatrix}}_{V^T \; (4 \times 4)}$$

Because the rank of matrix $A$ can be at most $\min(m, n) = \min(3, 4) = 3$, there are at most **3 non-zero singular values ($\sigma$)**.

---

### Step 2.4: Execute SVD in NumPy

We use NumPy's linear algebra module (`np.linalg.svd`) to compute the factors. Setting `full_matrices=True` ensures we get the uncropped, full-sized $U$ and $V^T$ arrays.

```python
u, s, vh = np.linalg.svd(a, full_matrices=True)

# Inspect shapes
print("u shape:", u.shape)
print("s shape:", s.shape)
print("vh shape:", vh.shape)

```

**Output Shapes Explanation 💡**

* `u.shape` $\implies$ `(3, 3)` matches $m \times m$.
* `s.shape` $\implies$ `(3,)` **Note:** NumPy returns the singular values as a flat 1D array of length $\min(m,n)$ to save memory, rather than a full $3 \times 4$ matrix.
* `vh.shape` $\implies$ `(4, 4)` matches $n \times n$ (corresponds directly to $V^T$).

---

### Step 2.5: Verifying Orthonormality Programmatically

An orthogonal matrix satisfies $Q \cdot Q^T = I$ (the Identity matrix). Let's verify that the output matrix `vh` ($V^T$) is perfectly orthonormal by taking its dot product with its own transpose:

```python
# Compute V^T * (V^T)^T which equals V^T * V
print(vh.dot(vh.T))

```

**Output:**

```text
[[ 1.  0.  0.  0.]
 [ 0.  1.  0. -0.]
 [ 0.  0.  1. -0.]
 [ 0. -0. -0.  1.]]

```

> **Simple Meaning:** The output is a perfect $4 \times 4$ Identity Matrix (1s on the diagonal, zeros elsewhere), proving that the computed vectors are perfectly normalized and perpendicular to one another.

---

## 3. Supplementary Practice Problems with Solutions

### Problem 1: Reconstructing Matrix A from NumPy Output

**Concept:** Rebuilding the original matrix from the outputs of `np.linalg.svd`. Since `s` is returned as a 1D vector `(3,)`, we must manually build an empty $3 \times 4$ zero matrix and place `s` on its diagonal before multiplying.

#### Python Solution:

```python
import numpy as np

A_orig = np.array([[1, 2, 3, 4], 
                   [1, 1, 2, 3], 
                   [0, 1, 1, 0]])

u, s, vh = np.linalg.svd(A_orig, full_matrices=True)

# Step 1: Create a 3x4 matrix filled with zeros
Sigma = np.zeros((3, 4))

# Step 2: Populate the diagonal with the singular values
Sigma[:3, :3] = np.diag(s)

# Step 3: Perform matrix multiplication U * Sigma * V^T
A_reconstructed = u.dot(Sigma).dot(vh)

print("Original Matrix:\n", A_orig)
print("\nReconstructed Matrix:\n", A_reconstructed)

```

---

### Problem 2: Computing a Rank-1 Approximation

**Concept:** Use the SVD components to find the closest possible rank-1 matrix to our original matrix $A$, discarding the 2nd and 3rd singular value tracks to compress the data.

#### Step-by-Step Calculation Formula:

$$A_1 = \sigma_1 \cdot u_1 \cdot v_1^T$$

#### Python Solution:

```python
# Extract the first column of u, first singular value, and first row of vh
u_1 = u[:, 0].reshape(-1, 1)  # Make it a column vector (3x1)
sigma_1 = s[0]                 # Scalar value
vh_1 = vh[0, :].reshape(1, -1)  # Make it a row vector (1x4)

# Compute outer product
A_rank1 = sigma_1 * np.dot(u_1, vh_1)

print("Rank-1 Approximation Matrix:\n", A_rank1)

```

# Python Implementation: Full Matrix Reconstruction from SVD

This note covers how to programmatically reconstruct an original matrix $A$ from its Singular Value Decomposition (SVD) factors using NumPy. It explicitly details the shape alignment operations required to handle rectangular matrices.

---

## 1. The Core Concept: SVD Reconstruction

When we execute SVD using NumPy's `np.linalg.svd(a, full_matrices=True)`, it factors our matrix into:
* `u` (Left singular matrix, size $m \times m$)
* `s` (Singular values, returned as a **1D array** of length $\min(m, n)$)
* `vh` (Right singular matrix $V^T$, size $n \times n$)

### The SVD Dimension Alignment Challenge 💡
To reconstruct the matrix using the mathematical equation $A = U \Sigma V^T$, we cannot multiply a 1D array `s` directly with matrices. We must build a full 2D matrix $\Sigma$ matching the dimensions of the original matrix ($m \times n$).

If the input is rectangular ($m \neq n$), we must initialize an all-zero matrix of size $m \times n$, populate its main diagonal with the singular values, and then execute back-to-back dot products.

---

## 2. Step-by-Step Code Walkthrough & Calculations

### Step 2.1: Extract Singular Values
From the computation on our input $3 \times 4$ matrix, `s` returns three singular values:
```python
print(s)
# Output: [6.7509, 1.1734, 0.2186]

```

### Step 2.2: Convert 1D Array to a Square Diagonal Matrix

We use `np.diag(s)` to convert the flat vector into a square $3 \times 3$ matrix:

```python
sd = np.diag(s)
print(sd)

```

**Output:**

```text
[[6.7509 0.     0.    ]
 [0.     1.1734 0.    ]
 [0.     0.     0.2186]]

```

### Step 2.3: Pad to Match Original Dimensions ($3 \times 4$)

Since our original matrix has 4 columns, a $3 \times 3$ diagonal matrix cannot be multiplied by the $4 \times 4$ matrix $V^T$. We initialize a $3 \times 4$ matrix of zeros and fill its left-hand $3 \times 3$ partition with our diagonal matrix `sd`:

```python
# Create an empty 3x4 canvas
b = np.zeros((3, 4))

# Copy the 3x3 diagonal matrix into the first 3 columns
b[:, :-1] = sd
sigma = b
print(sigma)

```

**Output:**

```text
[[6.7509 0.     0.     0.    ]
 [0.     1.1734 0.     0.    ]
 [0.     0.     0.2186 0.    ]]

```

### Step 2.4: Perform Back-to-Back Matrix Multiplication

Now that the dimensions match perfectly, we calculate the product $U \cdot \Sigma \cdot V^T$:

```python
reconstructed_a = np.dot(np.dot(u, sigma), vh)
print(reconstructed_a)

```

**Output Matrix:**

```text
[[ 1.0959  1.9567  3.0526  3.9542]
 [ 0.8764  1.0558  1.9322  3.0589]
 [-0.0559  1.0252  0.9693  0.0267]]

```

*(Note: These outputs correspond to the original matrix data with minor floating-point variations due to truncated display precisions in the lecture slides).*

---

## 3. Practice Problems with Solutions

### Problem 1: Manual Verification of Dimensional Sufficiency

**Concept:** Verify if a tall rectangular matrix $A$ of size $5 \times 3$ can be reconstructed using NumPy shapes without running into dimension mismatch errors.

#### Step-by-Step Calculation:

1. Shape of $U = 5 \times 5$
2. Shape of flat array $s = (3,)$
3. Shape of $V^T = 3 \times 3$

To build the appropriate $\Sigma$ matrix, we must establish an empty target array matching $A$'s original dimensions ($5 \times 3$).

#### Solution Code:

```python
import numpy as np

# Simulate components for a 5x3 tall matrix
u = np.random.randn(5, 5)
s = np.array([10.5, 4.2, 1.1])
vh = np.random.randn(3, 3)

# Step 1: Create a 5x3 canvas of zeros
sigma = np.zeros((5, 3))

# Step 2: Place the 3x3 diagonal matrix into the top block
sigma[:3, :3] = np.diag(s)

# Step 3: Compute product
A_reconstructed = np.dot(np.dot(u, sigma), vh)
print("Reconstructed Shape:", A_reconstructed.shape)
# Output: Reconstructed Shape: (5, 3)

```

---

### Problem 2: Tracking Approximation Energy Loss (Quality Metric)

**Concept:** Calculate the percentage of data variance (energy) retained if we drop the smallest singular value ($\sigma_3 = 0.2186$) from our reconstruction matrix, creating a rank-2 approximation.

#### Step-by-Step Mathematical Formula:

$$\text{Quality Ratio} = \frac{\sigma_1^2 + \sigma_2^2}{\sigma_1^2 + \sigma_2^2 + \sigma_3^2}$$

#### Step-by-Step Calculation:

1. Squares of singular values:
* $\sigma_1^2 = (6.7509)^2 = 45.5747$
* $\sigma_2^2 = (1.1734)^2 = 1.3769$
* $\sigma_3^2 = (0.2186)^2 = 0.0478$


2. Compute Sums:
* Numerator (Rank-2): $45.5747 + 1.3769 = 46.9516$
* Denominator (Total): $46.9516 + 0.0478 = 46.9994$


3. Divide:

$$\text{Quality} = \frac{46.9516}{46.9994} \approx 0.99898$$



#### Solution Code:

```python
s_values = np.array([6.7509, 1.1734, 0.2186])

# Calculate squared energy
energy_squared = s_values ** 2

# Percentage captured by first two singular values
quality = np.sum(energy_squared[:2]) / np.sum(energy_squared)
print(f"Captured Energy Quality: {quality * 100:.3f}%")
# Output: Captured Energy Quality: 99.898%

```




# Python Implementation: Full vs. Reduced SVD with Tall Matrices

This note explores Singular Value Decomposition (SVD) applied to a **tall rectangular matrix** ($m > n$) using NumPy. It compares the structural differences between **Full SVD** (`full_matrices=True`) and **Reduced/Thin SVD** (`full_matrices=False`).

---

## 1. Concept: Full SVD vs. Reduced (Thin) SVD

When processing an $m \times n$ tall matrix where $m > n$, computing the complete decomposition yields extra padding dimensions containing only zeros. We use the parameter `full_matrices` to toggle between saving memory and generating complete basis dimensions.

### Concept Parameters:
* **Full SVD (`full_matrices=True`):** Computes $U$ as a full square $m \times m$ matrix. Since the matrix can only have at most $n$ non-zero singular values, the final $(m - n)$ columns of $U$ correspond to zero singular values and map to the left null space.
* **Reduced SVD (`full_matrices=False`):** Crops out the extra geometric dimensions. It calculates $U$ with size $m \times n$ and $\Sigma$ with size $n \times n$. This saves massive amounts of memory in big-data applications while retaining 100% of the non-zero dataset information.


---

## 2. Step-by-Step Code Walkthrough

### Step 2.1: Define a Tall Rectangular Matrix ($5 \times 4$)
We construct a matrix $A$ containing $m = 5$ rows and $n = 4$ columns:

```python
import numpy as np
np.set_printoptions(precision=4, suppress=True)

a = np.array([[1, 2, 3, 4], 
              [1, 1, 2, 3], 
              [0, 1, 1, 0], 
              [0, 2, 2, 0], 
              [0, 5, 5, 0]])
print(a)

```

---

### Step 2.2: Compute Full SVD (`full_matrices=True` by default)

When calling `np.linalg.svd(a)` without toggling options, full-dimensional bases are generated:

```python
u, s, vh = np.linalg.svd(a)
print("U Matrix Dimensions:", u.shape)
print("Singular Values:", s)

```

#### Dimensional Output Analysis:

* `u.shape` $\implies$ `(5, 5)` ($m \times m$)
* `s` vector array $\implies$ `[9.2296, 4.4454, 0.2312, 0.]`

**Important Observation:** Notice that the 4th singular value is exactly **$0.$**. This implies that the matrix does not have full column rank; its true rank $r = 3$.

---

### Step 2.3: Compute Reduced / Thin SVD (`full_matrices=False`)

Now, let's optimize our memory space by trimming the columns that multiply with trailing zeroes:

```python
u_red, s_red, vh_red = np.linalg.svd(a, full_matrices=False)
print("Reduced U Shape:", u_red.shape)
print("Reduced s Shape:", s_red.shape)
print("Reduced V^T Shape:", vh_red.shape)

```

#### Verification of Structural Transformation:

Let's see how the matrix dimensions change from Full to Reduced form:

| Matrix component | Full SVD Dimensions | Reduced SVD Dimensions | Change Behavior |
| --- | --- | --- | --- |
| **`u`** (Left Singular) | $5 \times 5$ | $5 \times 4$ | Dropped the final column |
| **`s`** (Singular Array) | `(4,)` | `(4,)` | Remains the same vector length |
| **`vh`** (Right Singular) | $4 \times 4$ | $4 \times 4$ | Unchanged since columns are already bounded by $n$ |

---

## 3. Practice Problems with Solutions

### Problem 1: Manual Verification of Dimensional Savings

**Concept:** Calculate the number of structural values saved by switching from a Full SVD profile to a Reduced SVD profile when processing a tall matrix tracking $m = 1000$ data packets across $n = 10$ parameters.

#### Step-by-Step Calculation:

1. **Full SVD Element Elements Required:**
* Elements in $U$ ($m \times m$): $1000 \times 1000 = 1,000,000$
* Elements in $V^T$ ($n \times n$): $10 \times 10 = 100$
* Total Storage $= 1,000,100 \text{ values}$


2. **Reduced SVD Element Elements Required:**
* Elements in $U_{\text{reduced}}$ ($m \times n$): $1000 \times 10 = 10,000$
* Elements in $V^T$ ($n \times n$): $10 \times 10 = 100$
* Total Storage $= 10,100 \text{ values}$


3. **Compute Efficiency Difference Ratio:**

$$\text{Compression Factor} = \frac{10,100}{1,000,100} \approx 0.0101 \implies \approx 1\%$$



#### Solution Code Verification:

```python
m, n = 1000, 10
a_large = np.random.randn(m, n)

u_full, s_full, vh_full = np.linalg.svd(a_large, full_matrices=True)
u_red, s_red, vh_red = np.linalg.svd(a_large, full_matrices=False)

print(f"Full U Elements: {u_full.size}")  # 1000000
print(f"Reduced U Elements: {u_red.size}")  # 1000

```

---

### Problem 2: Reconstructing a Tall Matrix from Reduced Form

**Concept:** Verify that multiplying the cropped elements from `full_matrices=False` yields an identical reconstruction matrix to our original $5 \times 4$ data canvas without losing numerical precision.

#### Step-by-Step Calculation Structure:

Because `u_red` has size $5 \times 4$ and `vh_red` has size $4 \times 4$, the intermediate singular matrix $\Sigma$ must be built as a clean square matrix of size $4 \times 4$:

$$\Sigma_{\text{reduced}} = \text{diag}(s) \in \mathbb{R}^{4 \times 4}$$

#### Solution Code:

```python
import numpy as np

a = np.array([[1, 2, 3, 4], 
              [1, 1, 2, 3], 
              [0, 1, 1, 0], 
              [0, 2, 2, 0], 
              [0, 5, 5, 0]])

# 1. Compute Reduced SVD
u_red, s_red, vh_red = np.linalg.svd(a, full_matrices=False)

# 2. Convert flat singular array straight into a 4x4 square diagonal matrix
sigma_red = np.diag(s_red)

# 3. Multiply matrices together: (5x4) * (4x4) * (4x4) -> Result is 5x4
a_reconstructed = np.dot(np.dot(u_red, sigma_red), vh_red)

print("Are the matrices matching close?")
print(np.allclose(a, a_reconstructed))
# Output: True

```



# Python Implementation: Image Compression and Low-Rank Reconstruction via SVD

This note details the step-by-step programmatic pipeline for loading an image, preprocessing it into a normalized 2D grayscale matrix, executing Singular Value Decomposition (SVD), analyzing its variance decay via a Scree Plot, and reconstructing low-rank approximations.

---

## 1. Concept Overview: Low-Rank Image Approximation

An image can be treated as an $m \times n$ matrix $A$. Real-world images have highly correlated rows and columns, meaning their singular values decay rapidly. By sorting the singular values ($\sigma_1 \ge \sigma_2 \ge \dots \ge \sigma_r > 0$) and keeping only the top $k$ components, we create a rank-$k$ approximation matrix $A_k$:

$$A_k = \sum_{i=1}^{k} \sigma_i u_i v_i^T$$

The total data variance or energy explained by keeping $k$ singular values is measured as:
$$\text{Variance Explained} = \frac{\sum_{i=1}^{k} \sigma_i^2}{\sum_{j=1}^{r} \sigma_j^2}$$

---

## 2. Step-by-Step Code Walkthrough

### Step 2.1: Library Dependencies
We import essential libraries for numeric matrix calculations (`numpy`), data manipulation (`pandas`), computer vision filtering (`cv2`), image input/output fetching (`skimage.io`), and visualization plotting (`matplotlib`, `seaborn`).

```python
import numpy as np
import pandas as pd
import cv2 as cv
from google.colab.patches import cv2_imshow # Used if rendering images raw inside Google Colab
from skimage import io
from PIL import Image
import matplotlib.pylab as plt
import seaborn as sns

# Set clean visualization parameters
np.set_printoptions(precision=4, suppress=True)

```

---

### Step 2.2: Load and Preprocess the Image Matrix

We fetch a remote image via its URL, convert its color profile from 3-channel BGR to a single-channel grayscale matrix, and map it as a 2D floating-point NumPy array.

```python
# 1. Fetch image from URL
url = "[https://channeli.in/api/django_filemanager/media_files/12069/](https://channeli.in/api/django_filemanager/media_files/12069/)"
myImg = io.imread(url)

# 2. Convert to Grayscale
gray_image = cv.cvtColor(myImg, cv.COLOR_BGR2GRAY)

# 3. Form standard 2D float NumPy matrix
img_mat = np.array(list(gray_image), float)

print("Matrix Sample:\n", img_mat)
print("\nImage Dimensions (m x n):", img_mat.shape)

```

**Dimensional Output:**

```text
[[207. 207. 207. ... 244. 244. 244.]
 [207. 207. 208. ... 244. 244. 244.]
 [208. 208. 208. ... 244. 244. 244.]
 ...
 [201. 206. 210. ... 120. 120. 120.]
 [199. 204. 209. ... 121. 121. 120.]
 [191. 197. 202. ... 122. 121. 120.]]

(720, 960)

```

> **Simple Meaning 💡:** The image acts as a matrix containing $m = 720$ horizontal rows and $n = 960$ vertical columns. The entries correspond to individual pixel brightness levels ranging theoretically between `0.0` (black) and `255.0` (white).

---

### Step 2.3: Scale/Standardize the Data Matrix

Before performing SVD, it is standard practice to normalize the data matrix by subtracting its global mean and dividing by its standard deviation. This sets the dataset center to $0$ and ensures numeric stability.

$$A_{\text{scaled}} = \frac{A - \mu}{\sigma}$$

```python
img_mat_scaled = (img_mat - img_mat.mean()) / img_mat.std()

```

---

### Step 2.4: Execute SVD and Analyze Variance (Scree Plot)

We run SVD on our normalized $720 \times 960$ matrix, which outputs `U` $(720 \times 720)$, a 1D vector `s` of length $720$, and `V` $(960 \times 960)$. Note that in this specific script's line `U, s, V = np.linalg.svd(...)`, the third output variable represents $V^T$ directly.

We calculate the relative variance explained by each individual tracking channel by squaring the values ($\sigma_i^2$) and dividing by the total sum of squares.

```python
# Compute SVD factors
U, s, V = np.linalg.svd(img_mat_scaled)

# Compute variance ratio per singular vector component
var_explained = np.round(s**2 / np.sum(s**2), decimals=3)

# Plot a Scree Bar Chart tracking the top 10 most dominant components
sns.barplot(x=list(range(1, 11)), y=var_explained[0:10], color="dodgerblue")
plt.xlabel('Singular Vector', fontsize=16)
plt.ylabel('Variance Explained', fontsize=16)
plt.tight_layout()
plt.savefig('svd_scree_plot.png', dpi=150)
plt.show()

```

---

### Step 2.5: Low-Rank Reconstructions ($k = 5, 50, 100$)

To compress the image, we truncate the matrices to keep only the first `num_components` tracks, discarding everything else as noise.

```python
def reconstruct_image(U, s, V, num_components):
    # Slice columns of U, diagonalize sliced s vector, slice rows of V^T
    U_k = U[:, :num_components]
    Sigma_k = np.diag(s[:num_components])
    V_k = V[:num_components, :]
    
    # Perform double dot product multiplication
    return np.dot(U_k.dot(Sigma_k), V_k)

reconst_img_5 = reconstruct_image(U, s, V, num_components=5)
reconst_img_50 = reconstruct_image(U, s, V, num_components=50)
reconst_img_100 = reconstruct_image(U, s, V, num_components=100)
reconst_img_650 = reconstruct_image(U, s, V, num_components=650)

```

---

### Step 2.6: Comparative Multi-Plot Grid Display

We group the final low-rank outputs into a $2 \times 2$ grid layout using `matplotlib.subplots` to visualize the quality progression as the number of singular values increases.

```python
fig, axs = plt.subplots(2, 2, figsize=(10, 10))

# Subplot 1: 5 Singular Values (Very Blurry/Blocky)
axs[0, 0].imshow(reconst_img_5)
axs[0, 0].set_title('Reconstructed Image: 5 SVs', size=16)

# Subplot 2: 50 Singular Values (Features recognizable, slightly soft)
axs[0, 1].imshow(reconst_img_50)
axs[0, 1].set_title('Reconstructed Image: 50 SVs', size=16)

# Subplot 3: 100 Singular Values (Sharp, near-perfect quality)
axs[1, 0].imshow(reconst_img_100)
axs[1, 0].set_title('Reconstructed Image: 100 SVs', size=16)

# Subplot 4: 650 Singular Values (Identical to original image)
axs[1, 1].imshow(reconst_img_650)
axs[1, 1].set_title('Reconstructed Image: 650 SVs', size=16)

plt.tight_layout()
plt.show()

```

---

## 3. Supplementary Practice Problems with Solutions

### Problem 1: Automated Threshold-Based Image Compression

**Concept:** Instead of manually guessing a number of components (like $k=50$), write a function that scans the singular values and automatically finds the minimum number of components needed to retain a specific target percentage of information (e.g., **$95\%$ variance**).

#### Python Solution:

```python
import numpy as np

def find_target_rank_components(s_vector, threshold_ratio=0.95):
    # Calculate squared energy values
    squared_energy = s_vector ** 2
    total_energy = np.sum(squared_energy)
    
    # Calculate cumulative energy sum step-by-step
    cumulative_energy = np.cumsum(squared_energy)
    cumulative_ratio = cumulative_energy / total_energy
    
    # Find the first index where cumulative ratio satisfies our threshold
    optimal_k = np.argmax(cumulative_ratio >= threshold_ratio) + 1
    return optimal_k, cumulative_ratio[optimal_k - 1]

# Example Application
target_k, exact_ratio = find_target_rank_components(s, threshold_ratio=0.95)
print(f"To preserve 95% image quality, keep exactly {target_k} singular values.")
print(f"Exact retained ratio: {exact_ratio * 100:.2f}%")

```

---

### Problem 2: SVD Image File Storage Savings Calculation

**Concept:** Calculate the theoretical memory footprint reduction when compressing a $720 \times 960$ matrix down to its top $k = 50$ structural components.

#### Step-by-Step Manual Calculation:

1. **Uncompressed Array Elements:**

$$\text{Elements}_{\text{orig}} = m \times n = 720 \times 960 = 691,200 \text{ float values}$$


2. **Compressed SVD Components ($U_k, \Sigma_k, V^T_k$):**
* Sliced $U$ columns ($m \times k$): $720 \times 50 = 36,000$
* Sliced $\Sigma$ diagonal vector ($k$): $50$
* Sliced $V^T$ rows ($k \times n$): $50 \times 960 = 48,000$

$$\text{Elements}_{\text{comp}} = 36,000 + 50 + 48,000 = 84,050 \text{ float values}$$




3. **Storage Allocation Ratio Evaluation:**

$$\text{Data Leftover} = \frac{84,050}{691,200} \approx 0.1216 \implies \mathbf{12.16\%}$$



#### Python Verification Code:

```python
m, n = 720, 960
k = 50

original_elements = m * n
compressed_elements = (m * k) + k + (n * k)

savings_percent = (1.0 - (compressed_elements / original_elements)) * 100
print(f"Original Space Needed: {original_elements} elements")
print(f"Compressed Space Needed: {compressed_elements} elements")
print(f"Total Storage Disk Space Saved: {savings_percent:.2f}%")
# Output: Total Storage Disk Space Saved: 87.84%

```

```
_

```
