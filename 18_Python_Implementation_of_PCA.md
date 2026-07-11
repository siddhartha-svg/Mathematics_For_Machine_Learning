# Python Tutorial: Dataset Creation and Mean-Centering for Dimensionality Reduction

This note details the initial data engineering pipeline using **NumPy** and **Matplotlib**. It covers array initialization, dimensional transposition, visual scatter inspection, and programmatic column-wise mean-centering (the first critical step in methods like PCA).

---

## 1. Concept Name: Dataset Transposition and Data Structuring

### Simple Meaning 💡
When you enter a list of vectors directly into an array, Python treats each sub-list as a horizontal row. However, in statistics and data science pipelines, it is standard practice for **columns to represent features** and **rows to represent observations (samples)**.
* We initialize our features horizontally to avoid long vertical code typing.
* We then immediately apply a **Transpose operation ($X^T$)** to flip the matrix on its side, converting our horizontal tracks into structured vertical columns.

### Code Walkthrough & Visual Matrix Re-shaping

```python
import numpy as np

# Step 1: Initialize raw horizontal feature vectors
X = np.array([
    [1, 3, 5, 7, 9, 13, 20, 20, 21, 24, 26],  # Feature 1 (horizontal)
    [5, 7, 11, 14, 15, 17, 18, 19, 21, 22, 26] # Feature 2 (horizontal)
])

# Step 2: Transpose to flip the dimensions (Rows <-> Columns)
X = X.T

# Step 3: Inspect the properly structured matrix
print(X)

```

#### Manual Geometric Translation:

Before Transposition ($2 \times 11$):


$$X_{\text{raw}} = \begin{bmatrix} 1 & 3 & 5 & \dots & 26 \\ 5 & 7 & 11 & \dots & 26 \end{bmatrix}$$

After Transposition ($11 \times 2$):


$$X = \begin{bmatrix} 1 & 5 \\ 3 & 7 \\ 5 & 11 \\ 7 & 14 \\ 9 & 15 \\ 13 & 17 \\ 20 & 18 \\ 20 & 19 \\ 21 & 21 \\ 24 & 22 \\ 26 & 26 \end{bmatrix}$$

Now, we have $m = 11$ independent spatial observations tracking $n = 2$ unique features.

---

## 2. Concept Name: Exploratory Data Visualization

Before transforming data numerically, engineers use scatter plots to check for existing clusters, directional trends, or baseline distributions.

```python
import matplotlib.pyplot as plt

# Plot Feature 1 (Column 0) on the X-axis vs. Feature 2 (Column 1) on the Y-axis
plt.scatter(X[:, 0], X[:, 1])
plt.xlabel('Feature 1')
plt.ylabel('Feature 2')
plt.title('Raw Exploratory Scatter Plot')
plt.show()

```

---

## 3. Concept Name: Column-Wise Mean-Centering

### Simple Meaning 💡

Real-world measurements come with arbitrary baseline biases (e.g., temperatures sitting around $70^\circ\text{F}$ instead of $0$).

* **Mean-centering** computes the exact average center of your data cloud and subtracts it from every data point.
* This shifts the entire data cloud across the coordinate system until its balancing center sits perfectly at the origin point $(0,0)$.
* This operation is mandatory before running algorithms like Principal Component Analysis (PCA) or Singular Value Decomposition (SVD) because it allows the models to measure pure variance without being thrown off by coordinate offsets.

---

### Step-by-Step Mathematical Calculations

To center the matrix programmatically, we call `np.mean(X, axis=0)`. The `axis=0` argument tells NumPy to calculate the average by scanning down each column independently.

#### Step 1: Calculate the Column Means manually

Sum the entries in each column and divide by the total number of items ($m = 11$):

$$\mu_{\text{col0}} = \frac{1+3+5+7+9+13+20+20+21+24+26}{11} = \frac{149}{11} \approx 13.54545455$$

$$\mu_{\text{col1}} = \frac{5+7+11+14+15+17+18+19+21+22+26}{11} = \frac{175}{11} \approx 15.90909091$$

NumPy stores these as a mean vector: `[13.5455, 15.9091]`.

#### Step 2: Execute Broadcasting Subtraction ($X - \mu$)

We subtract this mean vector from every single row in our matrix:

```python
X_meaned = X - np.mean(X, axis=0)
print(X_meaned)

```

**Manual Check for Row 1:**

* Entry (1,1): $1 - 13.54545455 = \mathbf{-12.54545455}$
* Entry (1,2): $5 - 15.90909091 = \mathbf{-10.90909091}$

**Manual Check for Row 11:**

* Entry (11,1): $26 - 13.54545455 = \mathbf{12.45454545}$
* Entry (11,2): $26 - 15.90909091 = \mathbf{10.09090909}$

This matches the precise matrix output shown in the final lecture slide:

```text
[[-12.5455 -10.9091]
 [-10.5455  -8.9091]
 [ -8.5455  -4.9091]
 [ -6.5455  -1.9091]
 [ -4.5455  -0.9091]
 [ -0.5455   1.0909]
 [  6.4545   2.0909]
 [  6.4545   3.0909]
 [  7.4545   5.0909]
 [ 10.4545   6.0909]
 [ 12.4545  10.0909]]

```

---

## 4. Practice Problems with Solutions

### Problem 1: Dealing with Multi-Dimensional Axis Mapping

**Scenario:** A data array $Z$ tracks measurements across 3 different sensors (columns) for 4 experimental trials (rows).

```python
Z = np.array([[10, 20, 30],
              [40, 50, 60],
              [70, 80, 90],
              [100, 110, 120]])

```

Calculate the output of `np.mean(Z, axis=0)` manually, and explain what would happen if you mistakenly specified `axis=1`.

#### Step-by-Step Calculation:

1. **`axis=0` (Column-wise extraction):**
* Sensor 1 Mean: $\frac{10+40+70+100}{4} = \frac{220}{4} = 55$
* Sensor 2 Mean: $\frac{20+50+80+110}{4} = \frac{260}{4} = 65$
* Sensor 3 Mean: $\frac{30+60+90+120}{4} = \frac{300}{4} = 75$
* **Output Vector:** `[55, 65, 75]`


2. **`axis=1` (Row-wise error extraction):**
If you use `axis=1`, Python calculates the average across the horizontal rows (averaging different sensors together for a single trial), which is completely incorrect for preprocessing features. For example, row 1 would yield $\frac{10+20+30}{3} = 20$.

---

### Problem 2: Center-Verification Check Code

**Concept:** Write a short validation script to mathematically prove that a matrix has been successfully centered at the spatial origin.

#### Solution Code:

```python
# If a dataset is perfectly centered around the origin, 
# the sum or mean of all elements along the columns must equal 0.

post_transformation_check = np.mean(X_meaned, axis=0)
print("Post-centered Column Means:", post_transformation_check)

# Check if values are close to absolute zero within floating point tolerances
print("Is data perfectly centered?", np.allclose(post_transformation_check, [0, 0]))
# Output: Is data perfectly centered? True

```




# Python Implementation of PCA: Eigen-Analysis and Feature Selection

This note provides a step-by-step programmatic breakdown of executing Principal Component Analysis (PCA) using NumPy, from plotting centered distributions to performing an Eigendecomposition on the data covariance matrix.

---

## 1. Concept Name: Visualizing Mean-Centering Shifts

### Simple Meaning 💡
When you plot the raw dataset and the mean-centered dataset on the same coordinate axes, you notice they are completely identical in shape, tilt, and distribution width. The only difference is their spatial location.
* The original raw data points (shown in orange) sit far away in the upper-right quadrant.
* The mean-centered data points (shown in blue) have been shifted down and to the left, positioning the exact balancing center of the cloud right on top of the origin point $(0,0)$.

```python
import matplotlib.pyplot as plt

# Compute mean-centered matrix
X_meaned = X - np.mean(X, axis=0)

plt.figure(figsize=(6,6))
# Plot mean-centered points in blue
plt.scatter(X_meaned[:, 0], X_meaned[:, 1], label="Centered Data")
# Plot original points in orange
plt.scatter(X[:, 0], X[:, 1], label="Original Data")
plt.axhline(0, color='grey', linestyle='--', linewidth=0.8)
plt.axvline(0, color='grey', linestyle='--', linewidth=0.8)
plt.legend()
plt.show()

```

---

## 2. Concept Name: Generating the Covariance Matrix (`np.cov`)

To find how our features interact with each other across our 11 experimental observations, we construct a sample covariance matrix.

```python
# Compute the sample covariance matrix
# rowvar=False treats columns as features and rows as observations
C = np.cov(X_meaned, rowvar=False)
print(C)

```

> **NumPy Syntax Tip:** By default, `np.cov` treats each row as a feature. Because our data matrix is arranged with vertical feature columns, we must explicitly set `rowvar=False` to prevent a dimensional computation mismatch.

---

## 3. Concept Name: Spectral Eigendecomposition (`np.linalg.eig`)

### Simple Meaning 💡

We pass the symmetric covariance matrix into `np.linalg.eig(C)` to find its eigenvalues and eigenvectors.

* **Eigenvalues (`eval`):** Tell us the amount of data variance (information power) contained along each new directional track.
* **Eigenvectors (`evec`):** Provide the directional coordinates (unit vectors) of these new tracking tracks.

```python
# Calculate eigenvalues and eigenvectors
evals, evecs = np.linalg.eig(C)

print("Eigenvalues:\n", evals)
print("\nEigenvectors Matrix (Columns are vectors):\n", evecs)

```

**Programmatic Output Analysis:**

```text
Eigenvalues:
 [119.2938    2.2699]

Eigenvectors:
 [[ 0.8196 -0.573 ]
  [ 0.573   0.8196]]

```

#### Mapping the Eigenpairs Explicitly:

NumPy packs the eigenvectors as **vertical columns** matching the order of the eigenvalues array:

* **Component Track 1 ($\lambda_1 = 119.2938$):**

$$\vec{v}_1 = \begin{bmatrix} 0.81956216 \\ 0.57299028 \end{bmatrix}$$


* **Component Track 2 ($\lambda_2 = 2.26988184$):**

$$\vec{v}_2 = \begin{bmatrix} -0.57299028 \\ 0.81956216 \end{bmatrix}$$



---

## 4. Concept Name: Sorting and Selecting the Principal Components

### Simple Meaning 💡

NumPy's `np.linalg.eig` function does not guarantee that the outputs are sorted by size. Because PCA requires selecting components based on descending data power, we must manually sort the eigenvalues and their matching eigenvectors from largest to smallest.

```python
# 1. Get indices that would sort the eigenvalues in descending order
sorted_index = np.argsort(evals)[::-1]

# 2. Re-arrange arrays using these indices
sorted_eval = evals[sorted_index]
sorted_evec = evecs[:, sorted_index]

# 3. Select the top n=1 principal component for dimensionality reduction
n = 1
evec_subset = sorted_evec[:, 0:n]
print("Selected Projection Basis Subspace (PC1):\n", evec_subset)

```

**Output Subspace Basis:**

```text
[[0.81956216]
 [0.57299028]]

```

This skinny column vector acts as our optimal 1D line axis projection anchor.

---

## 5. Practice Problems with Solutions

### Problem 1: Step-by-Step Quality and Retention Check

**Concept:** Calculate the exact total proportion of variance captured by the selected first principal component ($\text{PC1}$) from the programmatic output above.

#### Step-by-Step Calculation:

1. Extract Eigenvalues: $\lambda_1 = 119.29375452$, $\lambda_2 = 2.26988184$
2. Calculate Total Information Sum ($\lambda_1 + \lambda_2$):

$$\text{Total Variance} = 119.29375452 + 2.26988184 = 121.56363636$$


3. Divide the target component value by the total sum:

$$\text{Captured Quality} = \frac{119.29375452}{121.56363636} \approx 0.98132 \implies \mathbf{98.13\%}$$



#### Solution Conclusion:

By projecting the dataset down onto the single 1D column vector `evec_subset`, we preserve an outstanding **$98.13\%$** of the dataset's total geometric variance.

---

### Problem 2: Programmatic Transformation (Projecting to 1D)

**Concept:** Write the final code lines needed to take the mean-centered $11 \times 2$ data matrix `X_meaned` and mathematically project it down to a compressed 1D matrix using our selected `evec_subset`.

#### Solution Code:

```python
# The transformation formula is: Y = X_meaned . dot( evec_subset )
# Dimension analysis: (11 x 2) . dot(2 x 1) -> Outputs a compressed (11 x 1) vector array

compressed_data_1D = np.dot(X_meaned, evec_subset)

print("Compressed 1D Coordinate Representation:\n", compressed_data_1D)
print("\nNew Compact Shape:", compressed_data_1D.shape)
# Output Shape: (11, 1)

```



# PCA Case Study: Dimensionality Reduction on the Famous Iris Dataset

This note walks through a complete end-to-end Machine Learning pipeline using `scikit-learn` to execute **Principal Component Analysis (PCA)** on the famous **Iris Flower Dataset**. It details the structural dimensionality changes from a 4D space down to a visual 2D scatter plot.

---

## 1. Concept Name: The Iris Dataset (Multivariate Structural Analysis)

### Simple Meaning 💡
The Iris Dataset, compiled by statistician R.A. Fisher, is a classic benchmark dataset in data science. It tracks anatomical measurements of three distinct species of Iris flowers:
1. **Iris Setosa** (Target Class Label: `0`)
2. **Iris Versicolor** (Target Class Label: `1`)
3. **Iris Virginica** (Target Class Label: `2`)

There are exactly $50$ observations for each flower class, resulting in a total dataset size of $150$ samples. 

---

### Step-by-Step Dimensional Framework

Every flower sample is measured across $4$ separate numerical feature coordinates:
* $X_1$: `sepal length (cm)`
* $X_2$: `sepal width (cm)`
* $X_3$: `petal length (cm)`
* $X_4$: `petal width (cm)`

#### 1. Input Dimensions ($D$):
The raw features form a large data matrix of size $150 \times 4$.
$$D = \begin{bmatrix} 6.1 & 3.0 & 4.6 & 1.4 \\ 5.8 & 2.6 & 4.0 & 1.2 \\ \vdots & \vdots & \vdots & \vdots \\ 5.7 & 2.8 & 4.1 & 1.3 \end{bmatrix}_{150 \times 4}$$

#### 2. Covariance Matrix Dimension:
Computing the cross-correlations among the 4 distinct features yields a square symmetric matrix of size $4 \times 4$, which produces 4 unique eigenvalues ($\lambda_1 \ge \lambda_2 \ge \lambda_3 \ge \lambda_4$).

#### 3. PCA Objective (Target Lower Subspace):
Our primary objective is to map this complex 4-dimensional system down into an easily viewable **2-dimensional coordinate plane** ($k = 2$). We establish two optimized linear transformation tracks using the eigenvectors matching our top two largest eigenvalues ($\lambda_1$ and $\lambda_2$):

$$Y_1 = \alpha_1 X_1 + \alpha_2 X_2 + \alpha_3 X_3 + \alpha_4 X_4 \quad \text{(PC1 Axis coefficients Vector } \vec{\alpha}\text{)}$$
$$Y_2 = \beta_1 X_1 + \beta_2 X_2 + \beta_3 X_3 + \beta_4 X_4 \quad \text{(PC2 Axis coefficients Vector } \vec{\beta}\text{)}$$

Multiplying our data matrix by these two tracking directions shrinks our matrix layout directly from **$150 \times 4$** down to a compact **$150 \times 2$**.

---

## 2. Programmatic Python Pipeline (`scikit-learn`)

### Step 2.1: Fetching the Raw Dataset Matrix
We import the pre-bundled dataset module from `sklearn` to load the data matrix arrays.

```python
from sklearn import datasets

# Load the complete dataset dictionary object
iris = datasets.load_iris()

# Inspect feature labels and raw array footprints
print("Feature Column Names:", iris.get("feature_names"))
print("First 3 Data Rows:\n", iris.data[:3])
print("Target Class Categories:\n", iris.target)

```

---

### Step 2.2: Compute PCA Transformation ($4\text{D} \to 2\text{D}$)

We import the `PCA` class from `sklearn.decomposition`. By setting `n_components=2`, the model automatically handles centering the data, calculating the $4 \times 4$ covariance matrix, sorting the eigenvectors, and projecting the coordinates.

```python
import matplotlib.pyplot as plt
from sklearn.decomposition import PCA

# 1. Initialize the PCA transformer with our target dimension
pca = PCA(n_components=2)

# 2. Fit the model and transform the 150x4 matrix down to 150x2
X_transformed = pca.fit_transform(iris.data)

print("Transformed Matrix Shape:", X_transformed.shape)
# Output: (150, 2)

```

---

### Step 2.3: Plot the Visualized Component Subspace

We map the two columns of `X_transformed` onto a scatter plot. Passing the integer vector `c=iris.target` automatically colors the dots based on their actual flower family classes.

```python
plt.figure(figsize=(8, 6))

# Plot all 150 transformed samples
# Column 0 maps to PC1 (X-axis), Column 1 maps to PC2 (Y-axis)
plt.scatter(X_transformed[:, 0], X_transformed[:, 1], c=iris.target, cmap='viridis', s=50)

# Highlight sample index 10 with a large translucent red marker (as seen in slide)
plt.scatter(X_transformed[10, 0], X_transformed[10, 1], s=300, c='red', alpha=0.5)

plt.xlabel('Principal Component 1 (PC1)', fontsize=14)
plt.ylabel('Principal Component 2 (PC2)', fontsize=14)
plt.title('Iris Dataset: 2D Projection Subspace via PCA', fontsize=16)
plt.grid(True, linestyle='--', alpha=0.5)
plt.show()

```

#### Visual Subspace Interpretation 💡

The resulting graph provides a clear 2D visualization of the data distributions:

```text
  PC2 (Sepal/Petal Secondary Variance Axis)
   ^
1.5+             ● (Virginica)
   |           ●   ●● ●
1.0+          ● ●●● ●●●   ● (Yellow)
   |        ●●●●●●●●●●● ●
0.5+    🔴   ●●●●●●●● ●
   |   ●●●●    ●●●● (Versicolor / Green)
0.0+  ●●●●●
   |  ●●●●
-0.5+  ●●● (Setosa / Purple)
   |
-1.0+
   +----+----+----+----+----+----+----> PC1 (Dominant Structural Tracking Axis)
       -3   -2   -1    0    1    2    3

```

* **Purple Cluster (Left):** The **Iris Setosa** species is completely separated from the others. This indicates that its physical features vary significantly along the PC1 tracking axis.
* **Green and Yellow Clusters (Right):** The **Versicolor** and **Virginica** species show minor overlaps, demonstrating that they share closer physical traits, though they are still distinguishable.

---

## 3. Supplementary Practice Problems with Solutions

### Problem 1: Calculating Storage Savings and Compression Ratio

**Concept:** Evaluate the file compression efficiency achieved by transforming the raw Iris dataset from 4 dimensions to 2 dimensions using SVD/PCA principles.

#### Step-by-Step Calculation:

1. Calculate raw data values required:

$$\text{Elements}_{\text{orig}} = 150 \text{ samples} \times 4 \text{ features} = 600 \text{ float values}$$


2. Calculate transformed low-rank values required:

$$\text{Elements}_{\text{transformed}} = 150 \text{ samples} \times 2 \text{ features} = 300 \text{ float values}$$


3. Compute data compression ratio:

$$\text{Ratio} = \frac{300}{600} = 0.50 \implies \mathbf{50\%}$$



#### Solution Conclusion:

By mapping the dataset to a 2D space, we reduce the file storage size by **$50\%$**. This enables us to visualize the multi-dimensional dataset on a standard flat screen while preserving the maximum possible structural variance.

---

### Problem 2: Analyzing Information Preservation via Code

**Concept:** Write a script to inspect the `explained_variance_ratio_` attribute of the fitted `PCA` class. This calculates the exact percentage of data variance retained by our top two principal components.

#### Solution Code:

```python
# The model stores the individual variance percentages in explained_variance_ratio_
variance_percentages = pca.explained_variance_ratio_

print("Variance captured by PC1:", f"{variance_percentages[0] * 100:.2f}%")
print("Variance captured by PC2:", f"{variance_percentages[1] * 100:.2f}%")

total_preserved = np.sum(variance_percentages) * 100
print(f"\nTotal Information Preserved in 2D Space: {total_preserved:.2f}%")

```

#### Expected Output Analysis:

* PC1 captures approximately **$92.46\%$** of the total variance.
* PC2 captures approximately **$5.31\%$** of the variance.
* Total information preserved: **$\approx 97.77\%$**.

> **Takeaway Summary:** Even though we discarded half the feature columns (dropping Sepal Width and Petal Width as independent tracks), our compressed 2D coordinates still retain a massive **$97.77\%$** of the original physical variance! This explains why the three species clusters remain clearly separated on our plot.

```

