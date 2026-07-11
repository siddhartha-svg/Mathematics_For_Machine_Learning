# Linear Algebra & Data Science Notes: Introduction to Principal Component Analysis (PCA)

This note covers the motivational concepts of Principal Component Analysis (PCA) for dimensionality reduction, followed by the fundamental statistical metrics (Mean, Standard Deviation, and Covariance) needed to perform it.

---

## 1. Concept Name: Principal Component Analysis (PCA) & Dimensionality Reduction

### Simple Meaning 💡
Imagine you are evaluating 5 different cities ($C_1$ to $C_5$) using 4 distinct feature parameters:
* $X_1$: Quality of Education
* $X_2$: Public Transportation Availability (Notice all cities score a flat $7$; this feature has zero variance!)
* $X_3$: Entertainment Venues
* $X_4$: Public Safety Indices

Instead of dealing with a 4-dimensional data space ($\mathbb{R}^4$) for every city, you want to compress this data down into fewer parameters (e.g., $Y_1, Y_2, Y_3 \in \mathbb{R}^3$) without losing meaningful information. 

PCA accomplishes this by looking for **Principal Components ($Y_i$)**, which are linear combinations of your original features ($X_j$). 
* A **"Good"** component captures high variation/spread in the data.
* A **"Not Good"** component shows very little variation (like column $X_2$ where every city scores a $7$) and can be safely discarded.


---

### Step-by-Step Mathematical Structure

#### Step 1.1: Representing a Data Point
Every row in our dataset is a vector in a 4-dimensional real coordinate space ($\mathbb{R}^4$). For city $C_1$:
$$C_1 = \begin{bmatrix} 8 \\ 7 \\ 9 \\ 7 \end{bmatrix} \in \mathbb{R}^4$$

#### Step 1.2: Forming Linear Transformations
We construct a new coordinate system by setting up linear combinations:
$$Y_1 = a_{11}X_1 + a_{12}X_2 + a_{13}X_3 + a_{14}X_4$$
$$Y_2 = a_{21}X_1 + a_{22}X_2 + a_{23}X_3 + a_{24}X_4$$
$$Y_3 = a_{31}X_1 + a_{32}X_2 + a_{33}X_3 + a_{34}X_4$$

#### Step 1.3: Matrix Dimensional Mapping ($\mathbb{R}^4 \longrightarrow \mathbb{R}^3$)
We can stack these transformations into a single matrix system to map our 4 features down to 3 compressed indicators:

$$\underbrace{\begin{bmatrix} Y_1 \\ Y_2 \\ Y_3 \end{bmatrix}}_{3 \times 1} = \underbrace{\begin{bmatrix} a_{11} & a_{12} & a_{13} & a_{14} \\ a_{21} & a_{22} & a_{23} & a_{24} \\ a_{31} & a_{32} & a_{33} & a_{34} \end{bmatrix}}_{3 \times 4} \cdot \underbrace{\begin{bmatrix} X_1 \\ X_2 \\ X_3 \\ X_4 \end{bmatrix}}_{4 \times 1}$$

---

## 2. Statistical Prerequisites for PCA

To find which directions contain the most information, we must measure data distribution using three fundamental formulas.

### 2.1. Mean ($\mu$)
* **Formula:** $$\mu = \frac{1}{n} \sum_{i=1}^{n} x_i$$
* **Simple Meaning 💡:** The baseline average value of a feature column.

### 2.2. Standard Deviation ($\sigma$)
* **Formula:** $$\sigma = \sqrt{\frac{1}{n} \sum_{i=1}^{n} (x_i - \mu)^2}$$
* **Simple Meaning 💡:** Measures how spread out the data points are from their baseline average. High standard deviation means a feature carries a high amount of distinct informational variance.

### 2.3. Covariance ($\Sigma_{XY}$)
* **Formula:** $$\Sigma_{XY} = \frac{1}{n} \sum_{i=1}^{n} (x_i - \mu_X)(y_i - \mu_Y)^T$$
* **Simple Meaning 💡:** A measure of how two different variables change together. 
  * If it's **positive**, both variables tend to increase at the same time.
  * If it's **zero**, the variables change completely independently of each other.

---

## 3. Practice Problems with Solutions

### Problem 1: Manual Calculation of Variance & Information Retention
**Scenario:** Let's look at feature column $X_2$ (Transportation) from the first image, where all 5 data observations are exactly $7$: 
$$X_2 = \{7, 7, 7, 7, 7\}$$

#### Step-by-Step Calculation:
1. **Find the Mean ($\mu$):**
   $$\mu = \frac{7 + 7 + 7 + 7 + 7}{5} = \frac{35}{5} = 7$$

2. **Find the Variance ($\sigma^2$):**
   $$\sigma^2 = \frac{1}{5} \sum_{i=1}^{5} (x_i - 7)^2$$
   $$\sigma^2 = \frac{(7-7)^2 + (7-7)^2 + (7-7)^2 + (7-7)^2 + (7-7)^2}{5} = \frac{0}{5} = 0$$

#### Solution Conclusion:
Because the variance is exactly **$0$**, this feature contains no unique informational value. In a real PCA pipeline, this component would be classified as **"Not Good"** and dropped immediately, reducing your dimensions effortlessly.

---

### Problem 2: Computing Covariance Between Two Features
**Scenario:** Given observations for two features $X$ and $Y$ across 3 samples:
* $X = \{2, 4, 6\}$
* $Y = \{1, 3, 8\}$

#### Step-by-Step Calculation:
1. **Compute Means:**
   $$\mu_X = \frac{2 + 4 + 6}{3} = 4$$
   $$\mu_Y = \frac{1 + 3 + 8}{3} = 4$$

2. **Compute Deviations ($x_i - \mu_X$) and ($y_i - \mu_Y$):**
   * Sample 1: $(2 - 4) = -2$ and $(1 - 4) = -3 \implies (-2) \times (-3) = 6$
   * Sample 2: $(4 - 4) = 0$ and $(3 - 4) = -1 \implies (0) \times (-1) = 0$
   * Sample 3: $(6 - 4) = 2$ and $(8 - 4) = 4 \implies (2) \times (4) = 8$

3. **Sum and Divide by $n=3$:**
   $$\Sigma_{XY} = \frac{6 + 0 + 8}{3} = \frac{14}{3} \approx 4.67$$

#### Solution Conclusion:
The covariance is **$+4.67$**. Because this value is positive, it proves that features $X$ and $Y$ move together in the same direction. PCA will exploit this relationship to combine them into a single, shared principal component variable.


# PCA Part II: Covariance Matrices and Principal Component Selection

This note details the structure of a covariance matrix and explains how its eigenvalues and eigenvectors are mathematically used to identify principal components for dimensionality reduction.

---

## 1. Concept Name: The Covariance Matrix ($\bar{\Sigma}$)

### Simple Meaning 💡
When evaluating a multi-featured dataset, measuring variance column-by-column isn't enough; we need to see how every feature interacts with every other feature. 

The **Covariance Matrix** organizes all these relationships into a structured grid. 
* The entries down the **main diagonal** show the standalone variance of each separate feature.
* The entries **off the diagonal** measure the cross-covariance between two different features. 

### Mathematical Structure
For a $k$-dimensional dataset consisting of features $\{X_1, X_2, \dots, X_k\}$, the covariance matrix $\bar{\Sigma}$ is a square matrix of size $k \times k$:

$$\bar{\Sigma} = \begin{bmatrix} 
\sigma_{X_1}^2 & \Sigma_{X_1, X_2} & \Sigma_{X_1, X_3} & \dots & \Sigma_{X_1, X_k} \\ 
\Sigma_{X_1, X_2} & \sigma_{X_2}^2 & \dots & \dots & \Sigma_{X_2, X_k} \\ 
\vdots & \vdots & \ddots & & \vdots \\ 
\Sigma_{X_k, X_1} & \dots & \dots & \dots & \sigma_{X_k}^2 
\end{bmatrix}$$

> **Core Geometric Properties:** The covariance matrix is always a **Symmetric Matrix**. This means the top-right half is a mirror image of the bottom-left half ($\Sigma_{X_i, X_j} = \Sigma_{X_j, X_i}$). Because it is symmetric, it can always be broken down into clean, real eigenvalues and mutually perpendicular eigenvectors.

---

## 2. Concept Name: Principal Component Extraction

### Definition
The **Principal Components (PCs)** of a dataset are exactly the **eigenvectors** calculated from its covariance matrix. 


If your raw dataset is arranged as a centered matrix $C$ of size $n \times 3$ (where $n$ represents the samples and 3 represents the parameters), the $3 \times 3$ covariance matrix is calculated directly as:

$$\Sigma = \frac{1}{n}(C^T C) = \Sigma_{3 \times 3}$$

### Selection Optimization Rules:
* **First Principal Component (PC1):** The specific eigenvector that corresponds directly to the **largest eigenvalue** ($\lambda_{\max}$) of the covariance matrix. This vector points in the direction of maximum variance (spread) in the data.
* **Dimensionality Reduction Rule ($n \to k$):** If you want to compress an $n$-dimensional dataset down to a lower $k$-dimensional subspace, you calculate the entire spectrum of eigenvectors, sort them based on their matching eigenvalues from largest to smallest, and select only the **first $k$ eigenvectors**.

---

## 3. Practice Problems with Solutions

### Problem 1: Analyzing a $2 \times 2$ Covariance Matrix
**Scenario:** You calculate the following covariance matrix for a two-feature dataset ($X_1$ and $X_2$):
$$\Sigma = \begin{bmatrix} 9 & -4 \\ -4 & 16 \end{bmatrix}$$

Identify the standalone variance of each feature and describe their relationship based on the off-diagonal entries.

#### Step-by-Step Explanation & Calculation:
1. **Find Variances:** Look along the main diagonal.
   * Variance of feature $X_1 \implies \sigma_{X_1}^2 = 9$
   * Variance of feature $X_2 \implies \sigma_{X_2}^2 = 16$
2. **Analyze Covariance:** Look at the off-diagonal element.
   $$\Sigma_{X_1, X_2} = -4$$

#### Solution Conclusion:
The cross-covariance is **$-4$**. Because this value is negative, it indicates an inverse relationship: when feature $X_1$ increases, feature $X_2$ generally tends to decrease.

---

### Problem 2: Selecting the Dominant Principal Component Vector
**Scenario:** A 3-dimensional dataset yields a $3 \times 3$ covariance matrix. Its calculated eigenvalues ($\lambda_i$) and matching normalized eigenvectors ($\vec{v}_i$) are:

$$\lambda_1 = 8.2, \quad \vec{v}_1 = \begin{bmatrix} 0.70 \\ 0.70 \\ 0.00 \end{bmatrix}$$
$$\lambda_2 = 1.5, \quad \vec{v}_2 = \begin{bmatrix} -0.70 \\ 0.70 \\ 0.00 \end{bmatrix}$$
$$\lambda_3 = 0.3, \quad \vec{v}_3 = \begin{bmatrix} 0.00 \\ 0.00 \\ 1.00 \end{bmatrix}$$

Determine which vector represents the **First Principal Component (PC1)** and calculate its information retention quality score.

#### Step-by-Step Calculation:
1. **Identify PC1:** Compare the eigenvalues. 
   Since $\lambda_1 = 8.2$ is the absolute largest value, its matching eigenvector $\vec{v}_1$ is the first principal component.
   $$\text{PC1} = \begin{bmatrix} 0.70 \\ 0.70 \\ 0.00 \end{bmatrix}$$

2. **Compute Total Dataset Variance:** Sum all eigenvalues together.
   $$\text{Total Variance} = \lambda_1 + \lambda_2 + \lambda_3 = 8.2 + 1.5 + 0.3 = 10.0$$

3. **Compute PC1 Retention Quality Ratio:** Divide the target eigenvalue by the total sum.
   $$\text{Quality ratio} = \frac{\lambda_1}{\text{Total Variance}} = \frac{8.2}{10.0} = 0.82 \implies \mathbf{82\%}$$

#### Solution Conclusion:
Vector $\vec{v}_1$ is selected as the first principal component because it tracks the maximum variation direction. Storing only this single component allows us to drop the other two dimensions while retaining **$82\%$** of the dataset's total variance.

