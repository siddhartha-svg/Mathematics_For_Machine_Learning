# Linear Algebra & Data Science Notes: PCA v/s LDA

This note explores the core geometric and functional differences between **Principal Component Analysis (PCA)** and **Linear Discriminant Analysis (LDA)**, accompanied by a structured overview table and Python initialization code.

---

## 1. Concept Name: Visualizing PCA v/s LDA

### Simple Meaning 💡
* **PCA** is blind to class categories. It looks at a cloud of data points and finds the longest axis of stretching (maximum variance). If your classes happen to lie parallel to this axis, projecting onto it squashes the distinct groups together, making them impossible to separate.
* **LDA** leverages group labels explicitly. It searches for an optimized angle to project the data so that the class clusters are compressed tightly while their group centers remain far apart.


---

### Visual Case Study Analysis
Looking at the 2D scatter plots in the slide:
* **The Data Structure:** We have a blue cluster of points and a red cluster of points distributed along a diagonal trend.
* **PCA Projection (Left):** Follows the main diagonal axis because that is where the overall variance stretches longest. When projected onto this line, the red and blue points mix completely together. They become **linearly inseparable**.
* **LDA Projection (Right):** Projects onto a line tilted perpendicular to the data trend (the green line). Even though this line has less overall variance, it successfully groups the blue dots on one side and the red dots on the other, ensuring a clean classification boundary.

---

## 2. Structural Comparison Table

The core differences between these two dimensionality reduction techniques are summarized below:

| Functional Property | Principal Component Analysis (PCA) | Linear Discriminant Analysis (LDA) |
| :--- | :--- | :--- |
| **Learning Paradigm** | **Unsupervised Learning** (Operates purely on features; completely ignores class labels). | **Supervised Learning** (Requires explicit class target labels for optimization). |
| **Mathematical Goal** | Projects data in the direction of **maximum total variation**. | Projects data in a direction providing **maximum inter-class separability** while minimizing internal scatter. |
| **Primary Use-Case** | Feature representation, data reduction, compression, and denoising. | Class-discriminant dimensionality reduction for classification tasks. |
| **Dimensional Constraint** | Can reduce data dimensions down to any integer $k$ where $1 \le k \le d$. | Can reduce data dimensions to at most **$c - 1$**, where $c$ is the number of unique classes. |

---

## 3. Python Implementation: Dataset Initialization

The final notebook image illustrates how to initialize a custom 2D classification dataset for exploring these concepts in Python.

### Code Walkthrough & Setup

```python
import numpy as np
import matplotlib.pyplot as plt

# 1. Define the 2D feature coordinates horizontally
X = np.array([
    [0, 1, 2, 3, 4, 5, 1, 2, 3, 3, 5, 6, 7, 8],  # Feature 1 (X-axis tracks)
    [1, 2, 3, 3, 5, 5, 0, 1, 1, 2, 3, 5, 6, 6]   # Feature 2 (Y-axis tracks)
])

# 2. Define the supervised target class labels (0 = Purple, 1 = Yellow)
y = np.array([0, 0, 0, 0, 0, 0, 1, 1, 1, 1, 1, 1, 1, 1])

# 3. Transpose X to get the standard data shapes (Samples x Features)
X = X.T

print("Data Matrix Dimensions (Samples x Features):", X.shape)
# Output: (14, 2)

# 4. Generate the exploratory supervised scatter plot
# c=y automatically splits colors by their category label
plt.scatter(X[:, 0], X[:, 1], c=y, cmap='viridis')
plt.xlabel('Feature 1')
plt.ylabel('Feature 2')
plt.title('Custom 2D Supervised Dataset')
plt.grid(True, linestyle='--', alpha=0.5)
plt.show()

```

### Visual Distribution Layout 💡

When you run this script, it builds an intermediate data cloud containing 14 points split into two classes across a 2D plane:

```text
  Feature 2 (Y)
   ^
 6 +                             🟡   🟡
 5 +                   🟣   🟣        🟡
 4 +
 3 +              🟣   🟣             🟡
 2 +         🟣        🟡
 1 +    🟣        🟡   🟡
 0 +         🟡
   +----+----+----+----+----+----+----+----+----> Feature 1 (X)
        0    1    2    3    4    5    6    7    8

```

---

## 4. Supplementary Practice Problems with Solutions

### Problem 1: Calculating the LDA Subspace Boundary Limit

**Scenario:** A genomic dataset tracks expressions across 20,000 genes for patient groups categorized into $c = 3$ different cancer mutation classes.

1. If you run PCA, what is the maximum number of dimensions you can compress the features into?
2. If you run LDA, what is the absolute highest number of compressed dimensions allowed?

#### Step-by-Step Calculation:

1. **PCA Bound:** PCA is bounded only by the number of independent features ($d$) or samples ($m$). Since $d = 20,000$, PCA can map components down to any rank $k \le 20,000$.
2. **LDA Bound:** LDA relies on the cross-product ranking of between-class scatter matrices, which has a maximum rank limit of $c - 1$:

$$\text{Maximum LDA Subspace Components} = c - 1 = 3 - 1 = 2 \text{ dimensions}$$



#### Solution Conclusion:

While PCA can scale flexibly to any dimension, LDA can compress this specific medical dataset down to a maximum of **2 dimensions** because the informational focus is strictly restricted to separating 3 distinct class centers.

---

### Problem 2: Preserved Information Ratio Under PCA

**Scenario:** After calculating the covariance matrix for the custom dataset defined in Section 3, the eigenvalues are computed as:


$$\lambda_1 = 18.5, \quad \lambda_2 = 1.5$$

Calculate the exact percentage of total information (variance) preserved if you reduce this 2D coordinate system down to a 1D line using PCA.

#### Step-by-Step Calculation:

1. Find Total Dataset Variance ($\sum \lambda_i$):

$$\text{Total Variance} = \lambda_1 + \lambda_2 = 18.5 + 1.5 = 20.0$$


2. Divide the first dominant principal component value by the total variance sum:

$$\text{Preserved Variance Ratio} = \frac{\lambda_1}{\text{Total Variance}} = \frac{18.5}{20.0}$$


$$\text{Preserved Variance Ratio} = 0.925 \implies \mathbf{92.5\%}$$



#### Solution Conclusion:

By compressing this custom dataset down to a 1D line using PCA, we preserve an excellent **$92.5\%$** of the overall data variance. However, as noted in the geometric lessons above, whether this high-variance axis remains useful for separating our classes depends entirely on the spatial orientation of the class labels.




# Python Code Comparison: 1D Dimensionality Reduction via PCA vs. LDA

This note provides a step-by-step programmatic breakdown of executing **Principal Component Analysis (PCA)** and **Linear Discriminant Analysis (LDA)** on a custom classification dataset using `scikit-learn`. It highlights why LDA succeeds at separating classes in lower dimensions where PCA fails.

---

## 1. Concept Name: Preprocessing and Pre-transformed Arrays

We evaluate a dataset containing two labeled classes (represented as yellow and purple dots) across a 2D coordinate system. Our objective is to apply dimensionality reduction to project this dataset from 2D down into a simple 1D line space.

---

## 2. Step-by-Step Code Execution & Graphical Breakdown

### Step 2.1: Execute 1D PCA Reduction
We call the unsupervised `PCA` class with `n_components=1`. It scales the total combined data cloud to identify the single axis carrying the longest directional variation, regardless of class membership.

```python
from sklearn.decomposition import PCA
import matplotlib.pyplot as plt

# 1. Initialize PCA model for 1 component
pca = PCA(n_components=1)

# 2. Fit and transform the dataset features matrix X
Xr = pca.fit_transform(X)

# 3. Print the array values
print("PCA 1D Coordinates:\n", Xr)

```

**Output Array Values:**

```text
[[-4.0714], [-2.6633], [-1.2552], [-0.4855], [1.5610], [2.3307],
 [-3.9400], [-2.5319], [-1.7621], [-1.1238], [1.0541], [3.1005],
 [ 4.5086], [ 5.2783]]

```

#### Visualizing the PCA Error Drop 💡

To see this 1D data line plotted on a 2D canvas, we duplicate the coordinates: `plt.scatter(Xr[:, 0], Xr[:, 0], c=y)`.

```python
plt.scatter(Xr[:, 0], Xr[:, 0], c=y, cmap='viridis')
plt.title("Jupyter Output: 1D PCA Projection")
plt.xlabel("Component 1 Axis")
plt.ylabel("Dummy Symmetrical Axis")
plt.show()

```

**Graphical Problem Analysis:** Look closely at the purple and yellow dot sequence on the resulting line. Because PCA only cares about overall data width, it projects along the diagonal trend. This forces the yellow dots and purple dots to **overlap completely on top of each other** around the center of the line (between coordinates `-3` and `2`), making linear classification impossible.

---

### Step 2.2: Execute 1D LDA Reduction

We switch to `LinearDiscriminantAnalysis` from `sklearn.discriminant_analysis`. Since LDA is a supervised algorithm, we must provide the class target vector `y` during fitting so the model can maximize class separability.

```python
from sklearn.discriminant_analysis import LinearDiscriminantAnalysis

# 1. Initialize LDA model
lda = LinearDiscriminantAnalysis()

# 2. Fit and transform by passing both features (X) and class labels (y)
X_lda = lda.fit_transform(X, y)

# 3. Print the array values
print("LDA 1D Coordinates:\n", X_lda)

```

#### Visualizing the LDA Success 💡

We plot the LDA line representation using: `plt.scatter(X_lda[:, 0], X_lda[:, 0], c=y)`.

```python
plt.scatter(X_lda[:, 0], X_lda[:, 0], c=y, cmap='viridis')
plt.title("Jupyter Output: 1D LDA Projection")
plt.xlabel("Discriminant 1 Axis")
plt.ylabel("Dummy Symmetrical Axis")
plt.show()

```

**Graphical Success Analysis:** Look at the massive structural improvement! LDA successfully splits the dataset into two clean, disjoint blocks on the line:

* All **purple dots** are tightly packed on the bottom left (spanning between coordinate values `-3.5` and `-1.0`).
* All **yellow dots** are pushed away to the right side (spanning between coordinate values `0.5` and `3.5`).
* There is a clear gap around coordinate `0.0`. A classification model can now separate these two classes with zero error using a simple threshold.

---

## 3. Practice Problems with Solutions

### Problem 1: Manual Calculation of File Storage Footprints

**Scenario:** A machine learning pipeline processes $m = 10,000$ images categorized into $c = 2$ classes. Each image has $d = 500$ pixel features. Calculate the exact array elements stored on disk if the data is compressed using:

1. PCA down to a 1D vector.
2. LDA down to its maximum allowed subspace dimensions.

#### Step-by-Step Calculation:

1. **PCA 1D Output Shape:**

$$\text{Elements} = m \times k = 10,000 \times 1 = 10,000 \text{ float values}$$


2. **LDA Maximum Output Shape:**
The maximum number of dimensions for LDA is bounded by $c - 1$:

$$\text{Max LDA dimensions} = c - 1 = 2 - 1 = 1 \text{ dimension}$$


$$\text{Elements} = m \times (c - 1) = 10,000 \times 1 = 10,000 \text{ float values}$$



#### Solution Conclusion:

Both methods produce an output array of identical size ($10,000 \times 1$). However, as demonstrated by the graphs, only the LDA array keeps the classes separated for downstream classification.

---

### Problem 2: Programmatic Classification Error Verification

**Concept:** Write a validation script using a `KNeighborsClassifier` to prove that the LDA compressed matrix `X_lda` yields better classification accuracy than the PCA compressed matrix `Xr`.

#### Solution Code:

```python
from sklearn.neighbors import KNeighborsClassifier
from sklearn.metrics import accuracy_score

# Initialize a standard 1-Nearest Neighbor classifier
knn = KNeighborsClassifier(n_neighbors=1)

# Test 1: PCA Classification Performance
knn.fit(Xr, y)
pca_preds = knn.predict(Xr)
pca_acc = accuracy_score(y, pca_preds)

# Test 2: LDA Classification Performance
knn.fit(X_lda, y)
lda_preds = knn.predict(X_lda)
lda_acc = accuracy_score(y, lda_preds)

print(f"PCA 1D Subspace Accuracy: {pca_acc * 100:.2f}%")
print(f"LDA 1D Subspace Accuracy: {lda_acc * 100:.2f}%")

```

#### Expected Output Performance:

* `PCA 1D Subspace Accuracy` will be low (e.g., $\approx 60\%-70\%$) due to the severe group overlaps in the center of the line.
* `LDA 1D Subspace Accuracy` will be a perfect **$100.00\%$**, verifying that LDA successfully preserved the underlying class structure during dimensionality reduction.



# PCA Pipeline: Unsupervised Dimensionality Reduction on the UCI Wine Dataset

This note walks through a complete end-to-end data analysis pipeline using `scikit-learn` to process the multi-attribute **UCI Wine Recognition Dataset** via Principal Component Analysis (PCA).

---

## 1. Concept Name: The Wine Recognition Dataset

### Simple Meaning 💡
The Wine dataset is a classic multivariate classification dataset in machine learning. It contains the results of a chemical analysis of wines grown in the same region in Italy, but derived from **three different cultivars (cultivated varieties)**. 

The analytical goal is to classify any unknown wine bottle into one of these three parent varieties based on its internal chemical signature.

---

### Dataset Dimensions and Features Checklist
* **Data Set Characteristics:** Multivariate
* **Total Number of Instances (Samples, $m$):** 178 rows
* **Total Number of Attributes (Features, $d$):** 13 column variables
* **Missing Values?:** No (clean dataset)
* **Associated Tasks:** Multiclass Classification / Compression

#### The 13 Chemical Features:
1. `alcohol`
2. `malic_acid`
3. `ash`
4. `alcalinity_of_ash`
5. `magnesium`
6. `total_phenols`
7. `flavanoids`
8. `nonflavanoid_phenols`
9. `proanthocyanins`
10. `color_intensity`
11. `hue`
12. `od280/od315_of_diluted_wines`
13. `proline`

#### Target Classes ($c = 3$):
* `class_0` (Mapped as integer `0`)
* `class_1` (Mapped as integer `1`)
* `class_2` (Mapped as integer `2`)

---

## 2. Programmatic Python Pipeline (`scikit-learn`)

### Step 2.1: Loading the Dataset
We load the dataset using `load_wine()` from `sklearn.datasets`. This returns a dictionary-like object containing our data split into a features matrix `X` ($178 \times 13$) and a categorical target vector `y` ($178 \times 1$).

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from sklearn.datasets import load_wine

# 1. Load the core dataset object
wine = load_wine()

# 2. Extract arrays
X = np.array(wine.data)
y = np.array(wine.target)

print("Features Matrix Shape (Samples x Attributes):", X.shape) 
# Output: (178, 13)
print("Target Classes Shape:", y.shape)                          
# Output: (178,)

```

---

### Step 2.2: Compute 2D PCA Compression ($13\text{D} \to 2\text{D}$)

Since working in a 13-dimensional space is impossible to visualize on a flat screen, we apply unsupervised PCA with `n_components=2`. The model computes a $13 \times 13$ covariance matrix and projects our $178 \times 13$ data matrix onto the eigenvectors matching the top two largest eigenvalues.

```python
from sklearn.decomposition import PCA

# 1. Initialize PCA model for 2 target dimensions
pca = PCA(n_components=2)

# 2. Fit the covariance matrix and transform the data matrix
Z = pca.fit_transform(X)

print("Compressed Matrix Shape:", Z.shape)
# Output: (178, 2)

```

---

### Step 2.3: Visualize the Lower Subspace Scatter Plot

We plot the two compressed columns of `Z` using `matplotlib`. Setting `c=y` automatically maps distinct cluster colors to our three wine classes.

```python
plt.figure(figsize=(8, 6))

# Column 0 maps to PC1 (X-axis), Column 1 maps to PC2 (Y-axis)
plt.scatter(Z[:, 0], Z[:, 1], c=y, cmap='viridis', s=40)

plt.xlabel('Principal Component 1 (PC1)', fontsize=12)
plt.ylabel('Principal Component 2 (PC2)', fontsize=12)
plt.title('UCI Wine Dataset: 2D Projection Subspace via PCA', fontsize=14)
plt.colorbar(ticks=[0, 1, 2], label='Wine Cultivar Classes')
plt.grid(True, linestyle='--', alpha=0.5)
plt.show()

```

#### Visual Subspace Interpretation 💡

The resulting graph displays the distribution of the compressed components:

```text
  PC2 (Secondary Variance Axis)
   ^
60 +                 ● (Class_1 / Green)
   |                ●● ●
40 +               ● ●●● ●  ●
   |             ●●●●●●●●●
20 +          ●●●●●●●●●●●●●●
   |         ●●●●●●●●●●●●●●●
 0 +        ●●●●●●●●●●●●●●●●●●
   |          ●●●●●●●●●●●●●●● (Class_0 / Purple)
-20+            ●●●●●●●●●●
   |
   +----+----+----+----+----+----+----+----+----> PC1 (Dominant Variance Axis)
       -4   -2    0   20   40   60   80

```

* **Class Clustering Separation:** The three distinct varieties of wine cluster into separate regions in the 2D plane.
* **The Overlap Notice:** Notice that while `Class_0` (Purple) and `Class_1` (Green) show clean separation, there is minor overlap along the bottom boundary. This is because unsupervised PCA only focuses on maximizing variance (spread) rather than class separation. To achieve a cleaner separation, we can apply a supervised technique like Linear Discriminant Analysis (LDA).

---

## 3. Practice Problems with Solutions

### Problem 1: Calculating Storage Savings and Compression Ratio

**Scenario:** Evaluate the data storage footprint reduction when compressing the UCI Wine dataset from its original 13 features down to 2 principal components.

#### Step-by-Step Calculation:

1. Calculate uncompressed value counts required:

$$\text{Elements}_{\text{orig}} = m \times d = 178 \text{ samples} \times 13 \text{ features} = 2,314 \text{ float entries}$$


2. Calculate compressed value counts required:

$$\text{Elements}_{\text{comp}} = m \times k = 178 \text{ samples} \times 2 \text{ features} = 356 \text{ float entries}$$


3. Compute the file compression space ratio:

$$\text{Ratio} = \frac{356}{2,314} \approx 0.1538 \implies \mathbf{15.38\%}$$



#### Solution Conclusion:

By projecting the dataset down into a 2D space, the matrix size is reduced to just **$15.38\%$** of its original footprint, resulting in a **$84.62\%$ saving** in disk space.

---

### Problem 2: Tracking Matrix Multiplication Alignment

**Scenario:** Given that our wine feature matrix $X$ has size $150 \times 13$, and we select a PCA projection matrix $W$ containing the top 2 eigenvectors.

1. State the exact required dimension shape for matrix $W$.
2. Prove that the matrix multiplication $X \cdot W$ yields our target shape of $150 \times 2$.

#### Step-by-Step Dimensional Analysis:

1. **Find shape of $W$:** The projection matrix maps data from our original feature dimension ($d = 13$) down to our compressed dimension ($k = 2$). Therefore:

$$\text{Shape of } W = 13 \times 2$$


2. **Verify Product Dimensions ($X \cdot W$):**
When multiplying a $(150 \times \color{blue}{13})$ matrix by a $(\color{blue}{13} \times 2)$ matrix, the inner dimensions ($\color{blue}{13}$) match perfectly. The final dimensions take the outer boundaries:

$$\text{Shape of Product} = 150 \times 2$$



This confirms that the transformation dimensions align properly.


# Linear Discriminant Analysis (LDA): Dimensionality Reduction & Predictive Modeling

This note covers the programmatic implementation of **Linear Discriminant Analysis (LDA)** for multi-class dimensionality reduction and classification using `scikit-learn`.

---

## 1. Concept Name: Supervised Dimensionality Reduction & Classification

### Simple Meaning 💡
While Principal Component Analysis (PCA) reduces dimensions by looking purely at where the data spans widest, **Linear Discriminant Analysis (LDA)** reduces dimensions by keeping your classes cleanly separated. 
* For a dataset with $c$ unique classes, LDA can project the data down to a maximum of $c - 1$ dimensions.
* By using class labels during training, LDA acts both as a **dimensionality reduction technique** and a **supervised classifier**.

---

## 2. Step-by-Step Code Execution & Graphical Breakdown

### Step 2.1: Multi-Class Projection via `fit_transform`
Using the Wine dataset (which contains $c = 3$ distinct classes), LDA maps the 13 original chemical features down to a maximum of $c - 1 = 2$ dimensions.

```python
import matplotlib.pyplot as plt
from sklearn.discriminant_analysis import LinearDiscriminantAnalysis

# 1. Initialize the LDA model
lda = LinearDiscriminantAnalysis()

# 2. Fit and transform the data matrix X using class labels y
X_lda = lda.fit_transform(X, y)

# 3. Create a 2D scatter plot of the transformed components
plt.figure(figsize=(8, 5))
plt.scatter(X_lda[:, 0], X_lda[:, 1], c=y, cmap='viridis', edgecolor='k', alpha=0.9)
plt.xlabel('Linear Discriminant 1 (LD1)')
plt.ylabel('Linear Discriminant 2 (LD2)')
plt.title('Wine Dataset: 2D Projection Subspace via LDA')
plt.show()

```

#### Visualizing the LDA Projection Subspace 💡

The resulting scatter plot shows how LDA organizes the 3 classes into highly distinct, isolated clusters:

```text
   Linear Discriminant 2 (LD2)
    ^
  4 +            🟣  🟣🟣
    |          🟣🟣🟣 🟣🟣     (Purple Cluster: Class 0)
  2 +           🟣🟣🟣🟣
    |                                   🟡 🟡🟡
  0 +                                 🟡🟡🟡🟡🟡   (Yellow Cluster: Class 2)
    |                                  🟡🟡🟡🟡
 -2 +                🟢 🟢🟢🟢
    |              🟢🟢🟢🟢🟢🟢     (Green Cluster: Class 1)
 -4 +               🟢🟢🟢🟢
    +----+----+----+----+----+----+----+----> Linear Discriminant 1 (LD1)
        -6   -4   -2    0    2    4    6

```

> **Key Takeaway:** Unlike the un-supervised PCA projection where the classes bleed slightly into each other, the supervised LDA projection separates the three clusters completely with obvious, wide gaps between them.

---

### Step 2.2: Cross-Validation Modeling (Train/Test Split)

To evaluate the predictive accuracy of the model, we split our data into a **70% training set** and a **30% testing set**.

```python
from sklearn.model_selection import train_test_split

# Split the dataset into random train and test partitions
xtrain, xtest, ytrain, ytest = train_test_split(X, y, test_size=0.3, random_state=42)

```

---

### Step 2.3: Training and Predicting

We train the LDA model on the training features (`xtrain`, `ytrain`) and predict the classifications for our unseen test array (`xtest`).

```python
# 1. Fit the model on the training data
lda.fit(xtrain, ytrain)

# 2. Predict the class labels for the test set
yn = lda.predict(xtest)

```

---

### Step 2.4: Evaluation via Element-Wise Residual Subtraction

A direct way to check for classification mistakes is to print the true labels array (`ytest`) and our predictions array (`yn`) side-by-side, then calculate the element-wise **residual difference matrix ($y_{\text{test}} - y_n$)**.

```python
print("True Test Labels (ytest):      ", ytest)
print("Predicted Test Labels (yn):    ", yn)
print("Residual Difference (ytest-yn):", ytest - yn)

```

**Output Breakdown:**

```text
True Test Labels (ytest):       [1 0 0 2 1 0 2 2 2 1 1 2 1 2 0 1 0 2 2 0 0 0 2 0 2 1 0 0 1 2 1 1 2 2 0 1 1 0 2 0 2 0 1 1 1 0 2 2 2 2 2 1 1 1]
Predicted Test Labels (yn):     [1 0 0 2 1 0 2 2 2 1 1 2 1 2 0 1 0 2 2 0 0 0 2 0 2 1 0 0 1 2 1 1 2 2 0 1 1 0 2 0 2 0 1 1 1 0 2 2 2 2 2 1 1 1]
Residual Difference (ytest-yn): [0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0]

```

#### Meaning of the Calculations 💡

* If the true label matches the predicted label (e.g., $1 - 1$ or $2 - 2$), the residual is exactly **$0$**.
* If the model makes a mistake, the value is non-zero (either $+1, -1, +2,$ or $-2$).
* Since our residual array contains **only zeros**, the model achieved **perfect classification accuracy ($100\%$)** on the test set.

---

## 3. Practice Problems with Solutions

### Problem 1: Quantitative Residual Verification

**Scenario:** Suppose your test set has 5 samples with true labels $y_{\text{test}} = [0, 1, 2, 1, 0]$. Due to real-world noise, the model outputs predictions $y_n = [0, 2, 2, 1, 0]$.

1. Calculate the residual difference vector ($y_{\text{test}} - y_n$).
2. Compute the final classification accuracy percentage.

#### Step-by-Step Calculation:

1. **Subtract vectors element-by-element:**

$$y_{\text{test}} - y_n = [0-0, \; 1-2, \; 2-2, \; 1-1, \; 0-0]$$


$$y_{\text{test}} - y_n = [0, \; -1, \; 0, \; 0, \; 0]$$


2. **Count mistakes:** There is exactly 1 non-zero entry, meaning the model made 1 error out of 5 samples.
3. **Compute accuracy ratio:**

$$\text{Accuracy} = \frac{\text{Correct Predictions}}{\text{Total Samples}} = \frac{4}{5} = 0.80 \implies \mathbf{80.00\%}$$



---

### Problem 2: Tracking Subspace Mapping Dimensions

**Scenario:** A dataset contains $m = 10,000$ consumer records split into $c = 4$ unique loyalty tiers based on $d = 50$ distinct behavioral features.

1. State the exact maximum dimensions permitted for an LDA subspace projection matrix $V$.
2. What will be the dimensional shape of the final matrix output when you run `lda.fit_transform(X, y)`?

#### Step-by-Step Dimensional Analysis:

1. **Find maximum allowed LDA dimensions ($k$):**
The maximum number of dimensions for an LDA projection is bounded by the number of classes minus one:

$$k = c - 1 = 4 - 1 = 3 \text{ dimensions}$$


2. **Find the shape of the transformation matrix $V$:**
The projection matrix maps data from our original feature dimension ($d = 50$) down to our new subspace dimension ($k = 3$). Thus:

$$\text{Shape of } V = d \times k = 50 \times 3$$


3. **Find the shape of the final output matrix:**
Multiplying our input matrix ($10,000 \times \color{blue}{50}$) by the projection matrix ($\color{blue}{50} \times 3$) yields a compressed matrix:

$$\text{Output Shape} = 10,000 \times 3$$



#### Solution Conclusion:

The final output matrix will have a shape of **$10,000 \times 3$**. This compact matrix retains the maximum possible class separability while throwing away 47 redundant feature dimensions.

