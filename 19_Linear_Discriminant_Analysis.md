# Linear Algebra & Machine Learning Notes: Linear Discriminant Analysis (LDA)

This note introduces the theoretical foundations of **Linear Discriminant Analysis (LDA)**, contrasts its classification optimization objectives with PCA, and derives its core optimization metric based on class separation and internal variance.

---

## 1. Concept Name: Why Use LDA Instead of PCA?

### Simple Meaning 💡
* **PCA (Unsupervised):** Focuses strictly on finding directions that maximize the **total spread (variance)** of the data points, completely ignoring what group or "class" those data points belong to.
* **LDA (Supervised):** Focuses explicitly on finding directions that **maximize class separability**. It uses class labels to project data onto a lower-dimensional line where different groups stay as far apart as possible.

As shown in the initial visual sequence:
* We have two distinct, cleanly separated data classes (Green Squares vs. Red Circles).
* If we blindly apply PCA, it picks the direction of maximum variance (the horizontal layout axis). 
* Projecting both groups onto this horizontal axis squashes them together into an overlapping, blended mess (**not separable**), ruining our classification model.


---

## 2. Concept Name: The Main Objective of LDA

The core intention of LDA is to find a line represented by a projection direction vector $\vec{w}$ such that when multi-dimensional samples are projected onto it, the classes remain well separated.


* **Poor Projection Axis (Left Diagram):** Projecting onto this steep blue line causes the green and red points to overlap heavily on the line, creating high classification error.
* **Optimal Projection Axis (Right Diagram):** Projecting onto this flatter tilted blue line maps the green cluster and red cluster to completely disjoint regions on the line, allowing a classifier to draw a perfect boundary line between them.

---

## 3. Mathematical Optimization Formulation: Step-by-Step

Let our dataset have two classes with original multi-dimensional column means $\vec{\mu}_1$ and $\vec{\mu}_2$. 
When projected onto a lower 1D line space via a projection vector $\vec{w}$, the new scalar coordinates have projected class means denoted as:

$$\tilde{\mu}_1 = \vec{w}^T \vec{\mu}_1 \quad \text{and} \quad \tilde{\mu}_2 = \vec{w}^T \vec{\mu}_2$$

---

### Step 3.1: Attempt 1 — Maximizing Mean Distance
The simplest intuitive distance metric to maximize is the absolute distance between the two projected means:

$$\text{Separation Distance Metric} = |\tilde{\mu}_1 - \tilde{\mu}_2|$$

#### The Limitation 💡
The problem with relying *only* on $|\tilde{\mu}_1 - \tilde{\mu}_2|$ is that it completely ignores the **internal variance (spread)** of the individual classes. 

As illustrated in the final two graphs:
* **Horizontal Axis Projection (Large Variance):** Even though the horizontal means $\hat{\mu}_1$ and $\hat{\mu}_2$ are far apart, the classes themselves have a very wide horizontal spread. Projecting onto this axis causes the tails of the distributions to overlap completely, making clean classification impossible.
* **Vertical Axis Projection (Small Variance):** Even though the vertical projected means $\tilde{\mu}_1$ and $\tilde{\mu}_2$ are closer together, the internal variance along the vertical axis is extremely small. Because the clusters are tightly packed, they remain **perfectly separated** without any overlap.

---

### Step 3.2: Attempt 2 — The Fisher Discriminant Criterion (Calculations)
To balance maximizing mean distance with minimizing individual class spread, we introduce the **Within-Class Scatter (Variance)**.

Let the variance of the projected points for each class be $\tilde{s}_1^2$ and $\tilde{s}_2^2$, calculated as the sum of squared differences:
$$\tilde{s}_1^2 = \sum_{y \in \text{Class 1}} (y - \tilde{\mu}_1)^2 \quad \text{and} \quad \tilde{s}_2^2 = \sum_{y \in \text{Class 2}} (y - \tilde{\mu}_2)^2$$

Fisher's ultimate optimization objective function $J(\vec{w})$ is defined as the ratio of the **between-class variance** to the **within-class variance**:

$$J(\vec{w}) = \frac{(\tilde{\mu}_1 - \tilde{\mu}_2)^2}{\tilde{s}_1^2 + \tilde{s}_2^2}$$

#### Expanding in Terms of the Original Feature Spaces:
Substitute $\tilde{\mu}_i = \vec{w}^T \vec{\mu}_i$:
$$\text{Numerator} = (\vec{w}^T \vec{\mu}_1 - \vec{w}^T \vec{\mu}_2)^2 = \left(\vec{w}^T(\vec{\mu}_1 - \vec{\mu}_2)\right)^2 = \vec{w}^T (\vec{\mu}_1 - \vec{\mu}_2)(\vec{\mu}_1 - \vec{\mu}_2)^T \vec{w}$$
$$\text{Numerator} = \vec{w}^T S_B \vec{w} \quad \text{(where } S_B \text{ is the Between-Class Scatter Matrix)}$$

Similarly, expanding the denominator yields:
$$\text{Denominator} = \vec{w}^T S_1 \vec{w} + \vec{w}^T S_2 \vec{w} = \vec{w}^T (S_1 + S_2) \vec{w} = \vec{w}^T S_W \vec{w}$$
$$\text{Denominator} = \vec{w}^T S_W \vec{w} \quad \text{(where } S_W \text{ is the Within-Class Scatter Matrix)}$$

This yields the complete LDA optimization objective:
$$J(\vec{w}) = \frac{\vec{w}^T S_B \vec{w}}{\vec{w}^T S_W \vec{w}}$$

> **Core Optimization Rule:** To find the optimal direction vector $\vec{w}$ that maximizes this ratio, we compute the derivative with respect to $\vec{w}$ and set it to 0. This reduces to a generalized eigenvalue problem: $S_W^{-1} S_B \vec{w} = \lambda \vec{w}$. The optimal line direction is the eigenvector matching the largest eigenvalue!

---

## 4. Practice Problems with Solutions

### Problem 1: Comparing Fisher Criterion Scores
**Scenario:** A data scientist tests two different projection lines ($\vec{w}_A$ and $\vec{w}_B$) to separate two classes. The projected parameters are:
* **Line A:** Projected means distance $(\tilde{\mu}_1 - \tilde{\mu}_2) = 6.0$; Class variances $\tilde{s}_1^2 = 4.0, \; \tilde{s}_2^2 = 5.0$.
* **Line B:** Projected means distance $(\tilde{\mu}_1 - \tilde{\mu}_2) = 4.0$; Class variances $\tilde{s}_1^2 = 0.5, \; \tilde{s}_2^2 = 0.5$.

Calculate the Fisher Criterion score $J(\vec{w})$ for both lines, and determine which line is better for classification.

#### Step-by-Step Calculation:
1. **Compute Score for Line A ($J_A$):**
   $$J_A = \frac{(\tilde{\mu}_1 - \tilde{\mu}_2)^2}{\tilde{s}_1^2 + \tilde{s}_2^2} = \frac{(6.0)^2}{4.0 + 5.0} = \frac{36.0}{9.0} = 4.0$$

2. **Compute Score for Line B ($J_B$):**
   $$J_B = \frac{(\tilde{\mu}_1 - \tilde{\mu}_2)^2}{\tilde{s}_1^2 + \tilde{s}_2^2} = \frac{(4.0)^2}{0.5 + 0.5} = \frac{16.0}{1.0} = 16.0$$

#### Solution Conclusion:
**Line B is significantly better.** Even though Line A has a wider distance between its means ($6.0 > 4.0$), its internal class variances are large and messy. Line B has a much higher Fisher score ($16.0 > 4.0$) because its classes are highly compact ($\tilde{s}_1^2 + \tilde{s}_2^2 = 1.0$), ensuring perfect class separation with zero overlap.

---

### Problem 2: Conceptual SVD-PCA-LDA Synthesis Matrix
**Concept:** Summarize the core operational and structural differences between PCA and LDA for reference in competitive machine learning pipelines.

| Functional Property | Principal Component Analysis (PCA) | Linear Discriminant Analysis (LDA) |
| :--- | :--- | :--- |
| **Learning Class Profile** | **Unsupervised** (Ignores group target labels completely) | **Supervised** (Requires class target labels explicitly) |
| **Optimization Focus** | Maximizes the **total variance** of the combined points | Maximizes the **separability** between different classes |
| **Core Math Engine** | Solves standard SVD / Eigendecomposition on data matrix | Solves generalized eigenvalue problem on scatter matrices |
| **Vulnerability Note** | Can collapse distinct classification groups if variance runs parallel to the class boundary | Assumes normal distributions and equal covariance structures across classes |

# Mathematical Optimization of LDA: Finding the Fisher Discriminant Vector

This note details the complete step-by-step mathematical derivation of **Linear Discriminant Analysis (LDA)**. It covers how multi-dimensional data components are projectively mapped onto an optimized 1D vector line space to maximize class separability while minimizing internal class scatter.

---

## 1. Concept Name: The Fisher Discriminant Objective Function $J(v)$

### Simple Meaning 💡
Imagine you have two separate groups of data points floating in a high-dimensional space. We want to find a specific line direction, defined by a unit vector $v$, to project all these data points onto. 

To make this projection line perfect for classification, we want two competing behaviors to happen at the same time:
1. **Maximize the distance between the two group means** on the line so they stay far apart.
2. **Minimize the variance (scatter) within each individual group** on the line so the points compress into tightly packed, non-overlapping clusters.


---

### Step-by-Step Derivation & Core Calculations

### Step 1.1: Projecting the Means
Suppose we have a $d$-dimensional dataset containing samples from two distinct classes:
* $n_1$ samples belong to Class 1 ($C_1$), with an original multi-dimensional mean vector $\mu_1$.
* $n_2$ samples belong to Class 2 ($C_2$), with an original multi-dimensional mean vector $\mu_2$.

The mathematical projection of any sample data point $x_i$ onto a line with direction vector $v$ is given by the vector dot product:
$$y_i = v^T x_i$$

Using the linearity of expectations, the projected sample scalar mean $\tilde{\mu}_1$ for Class 1 on our line is calculated as:
$$\tilde{\mu}_1 = \frac{1}{n_1} \sum_{x_i \in C_1} v^T x_i = v^T \left( \frac{1}{n_1} \sum_{x_i \in C_1} x_i \right) = v^T \mu_1$$

Similarly, for Class 2, the projected mean is:
$$\tilde{\mu}_2 = v^T \mu_2$$

---

### Step 1.2: Projecting the Internal Sample Scatter
The scatter (variance) of the projected scalar samples within Class 1 and Class 2 is defined as the sum of squared differences from their respective projected means:

$$\tilde{s}_1^2 = \sum_{y_i \in C_1} (y_i - \tilde{\mu}_1)^2 \quad \text{and} \quad \tilde{s}_2^2 = \sum_{y_i \in C_2} (y_i - \tilde{\mu}_2)^2$$

Our goal is to maximize the **Fisher Criterion Function $J(v)$**, which is the ratio of the squared distance between the projected means to the total within-class scatter:

$$J(v) = \frac{(\tilde{\mu}_1 - \tilde{\mu}_2)^2}{\tilde{s}_1^2 + \tilde{s}_2^2}$$

---

### Step 1.3: Introducing High-Dimensional Scatter Matrices
To solve this optimization problem for the vector $v$, we must express the projected scalar scatters in terms of our original high-dimensional feature spaces.

#### 1. Within-Class Scatter Matrices ($S_1, S_2, S_W$):
We define the standalone multi-dimensional scatter matrices for both classes as:
$$S_1 = \sum_{x_i \in C_1} (x_i - \mu_1)(x_i - \mu_1)^T \quad \text{and} \quad S_2 = \sum_{x_i \in C_2} (x_i - \mu_2)(x_i - \mu_2)^T$$

The total **Within-Class Scatter Matrix ($S_W$)** is the sum of these two matrices:
$$S_W = S_1 + S_2$$

Let's substitute the projection properties to see how they relate to the scalar projected scatters $\tilde{s}_i^2$:
$$\tilde{s}_1^2 = \sum_{x_i \in C_1} (v^T x_i - v^T \mu_1)^2 = \sum_{x_i \in C_1} \left( v^T (x_i - \mu_1) \right)^2$$
$$\tilde{s}_1^2 = \sum_{x_i \in C_1} v^T (x_i - \mu_1)(x_i - \mu_1)^T v = v^T \left[ \sum_{x_i \in C_1} (x_i - \mu_1)(x_i - \mu_1)^T \right] v = v^T S_1 v$$

Following this exact same steps for Class 2 yields $\tilde{s}_2^2 = v^T S_2 v$. Summing them together gives our denominator expression:
$$\tilde{s}_1^2 + \tilde{s}_2^2 = v^T S_1 v + v^T S_2 v = v^T (S_1 + S_2) v = v^T S_W v \quad \text{--- (Expression *健全)}$$

#### 2. Between-Class Scatter Matrix ($S_B$):
We define the structural data separation matrix between the two groups as:
$$S_B = (\mu_1 - \mu_2)(\mu_1 - \mu_2)^T$$

Let's expand our numerator expression using this definition:
$$(\tilde{\mu}_1 - \tilde{\mu}_2)^2 = (v^T \mu_1 - v^T \mu_2)^2 = \left( v^T (\mu_1 - \mu_2) \right)^2$$
$$(\tilde{\mu}_1 - \tilde{\mu}_2)^2 = v^T (\mu_1 - \mu_2)(\mu_1 - \mu_2)^T v = v^T S_B v \quad \text{--- (Expression **)}$$

---

### Step 1.4: Maximizing $J(v)$ via the Rayleigh Quotient
Substituting Expression $*$ and Expression $**$ back into our objective function gives:

$$J(v) = \frac{v^T S_B v}{v^T S_W v}$$

To find the vector $v$ that maximizes this ratio, we take the derivative with respect to $v$ using the matrix quotient rule and set it to $0$:
$$\frac{d}{dv} J(v) = 0 \implies \frac{2 S_B v \cdot (v^T S_W v) - 2 S_W v \cdot (v^T S_B v)}{(v^T S_W v)^2} = 0$$

Simplifying the numerator gives:
$$S_B v - \left( \frac{v^T S_B v}{v^T S_W v} \right) S_W v = 0$$

Notice that the scalar term inside the parenthesis is exactly our original objective function $J(v)$, which resolves to a constant scalar eigenvalue $\lambda$:
$$S_B v - \lambda S_W v = 0 \implies S_B v = \lambda S_W v$$

Assuming $S_W$ is invertible, we multiply both sides from the left by $S_W^{-1}$:
$$S_W^{-1} S_B v = \lambda v$$

> **The Eigenvalue Insight:** The optimal projection direction $v$ is an **eigenvector** of the matrix $S_W^{-1} S_B$, corresponding to its **largest eigenvalue** $\lambda$.

---

### Step 1.5: The Algebraic Shortcut Solution
We can simplify this calculation significantly by examining the structure of $S_B v$:
$$S_B v = (\mu_1 - \mu_2)(\mu_1 - \mu_2)^T v$$

Since $(\mu_1 - \mu_2)^T v$ is a simple scalar dot product value (let's call it $\alpha$), we can rewrite it as:
$$S_B v = \alpha (\mu_1 - \mu_2)$$

Substitute this back into our eigenvalue equation ($S_B v = \lambda S_W v$):
$$\alpha (\mu_1 - \mu_2) = \lambda S_W v$$

Isolating the vector $v$:
$$v = \left(\frac{\alpha}{\lambda}\right) S_W^{-1} (\mu_1 - \mu_2)$$

Since we only care about the **direction** of the line (magnitudes can be normalized to 1 later), we can drop the scalar scaling factor $\frac{\alpha}{\lambda}$. This gives us the famous, direct LDA solution formula:

$$v = S_W^{-1} (\mu_1 - \mu_2)$$

---

## 2. Practice Problems with Solutions

### Problem 1: Direct Calculation of the Optimal Projection Direction Vector
**Scenario:** A 2-dimensional dataset has two classes with the following pre-computed high-dimensional mean vectors and combined within-class scatter matrix:
$$\mu_1 = \begin{bmatrix} 4 \\ 7 \end{bmatrix}, \quad \mu_2 = \begin{bmatrix} 1 \\ 3 \end{bmatrix}, \quad S_W = \begin{bmatrix} 3 & 1 \\ 1 & 2 \end{bmatrix}$$

Calculate the exact coordinates of the optimal Fisher Discriminant projection vector $v$.

#### Step-by-Step Calculation:
1. **Find the difference between the class means ($\mu_1 - \mu_2$):**
   $$\mu_1 - \mu_2 = \begin{bmatrix} 4 - 1 \\ 7 - 3 \end{bmatrix} = \begin{bmatrix} 3 \\ 4 \end{bmatrix}$$

2. **Compute the matrix inverse $S_W^{-1}$:**
   For a $2 \times 2$ matrix $\begin{bmatrix} a & b \\ c & d \end{bmatrix}$, the inverse is $\frac{1}{ad-bc} \begin{bmatrix} d & -b \\ -c & a \end{bmatrix}$.
   $$\det(S_W) = (3 \times 2) - (1 \times 1) = 6 - 1 = 5$$
   $$S_W^{-1} = \frac{1}{5} \begin{bmatrix} 2 & -1 \\ -1 & 3 \end{bmatrix} = \begin{bmatrix} 0.4 & -0.2 \\ -0.2 & 0.6 \end{bmatrix}$$

3. **Multiply $S_W^{-1}$ by $(\mu_1 - \mu_2)$ to find $v$:**
   $$v = \begin{bmatrix} 0.4 & -0.2 \\ -0.2 & 0.6 \end{bmatrix} \begin{bmatrix} 3 \\ 4 \end{bmatrix} = \begin{bmatrix} (0.4 \times 3) + (-0.2 \times 4) \\ (-0.2 \times 3) + (0.6 \times 4) \end{bmatrix}$$
   $$v = \begin{bmatrix} 1.2 - 0.8 \\ -0.6 + 2.4 \end{bmatrix} = \begin{bmatrix} 0.4 \\ 1.8 \end{bmatrix}$$

#### Solution Conclusion:
The optimal line direction vector is $v = \begin{bmatrix} 0.4 \\ 1.8 \end{bmatrix}$. Projecting the data points onto this line maximizes class separation while minimizing internal class scatter.

---

### Problem 2: Tracking the Dimensionality Rules of Matrix Multiplications
**Scenario:** A dataset contains $m = 500$ sample rows tracking $d = 100$ individual feature parameters across 2 balanced classes. State the exact matrix dimension shapes for matrices $S_W$ and $S_B$, and verify that the product $S_W^{-1} S_B$ maintains valid matrix multiplication dimensions.

#### Step-by-Step Dimensional Analysis:
1. **Determine Scatter Matrix Shape Rules:**
   Both the within-class scatter matrix ($S_W$) and between-class scatter matrix ($S_B$) track correlations between features. Therefore, their dimensions are always determined by the number of features ($d \times d$), completely independent of the sample size $m$.
   $$\text{Shape of } S_W = 100 \times 100$$
   $$\text{Shape of } S_B = 100 \times 100$$

2. **Verify the Inverse Operation Matrix Shape:**
   Inverting a matrix does not alter its dimensional footprint.
   $$\text{Shape of } S_W^{-1} = 100 \times 100$$

3. **Verify the Final Product Dimensions:**
   Multiplying a $(100 \times \color{blue}{100})$ matrix by a $(\color{blue}{100} \times 100)$ matrix is valid because the inner dimensions ($\color{blue}{100}$) match perfectly. The resulting matrix takes the outer boundaries:
   $$\text{Shape of } S_W^{-1} S_B = 100 \times 100$$

#### Solution Conclusion:
The operations are dimensionally sound, resulting in a square matrix of size $100 \times 100$. This matrix produces a single $100 \times 1$ eigenvector $v$, matching the original feature dimensions of our data points.



# Linear Discriminant Analysis (LDA): Comprehensive Example & Multiple Class Generalization

This note walks through a concrete 2D numerical example of **Fisher's Linear Discriminant (FLD)**, compares its projection with PCA, and explains how to generalize the framework to multiple classes.

---

## 1. Concept Name: Fisher Linear Discriminant (2-Class Example)

### Simple Meaning 💡
When classes are distributed diagonally in a 2D plane, PCA can easily fail. PCA picks the direction of highest overall variance (the long diagonal direction of the entire combined data cloud). 
* As shown in the first slide's bottom diagram, projecting points onto the PCA diagonal line blends the classes together into an inseparable line segment.
* **LDA** solves this by finding a different line (the green line in the third slide) where the two groups project onto completely separate regions with an obvious gap between them.

---

### Step-by-Step Numerical Walkthrough

Given a 2D dataset with two distinct classes:
* **Class 1 ($c_1$):** 5 samples $\implies [(1,2), (2,3), (3,3), (4,5), (5,5)]$
* **Class 2 ($c_2$):** 6 samples $\implies [(1,0), (2,1), (3,1), (3,2), (5,3), (6,5)]$

We organize the coordinates into separate data matrices:
$$c_1 = \begin{bmatrix} 1 & 2 \\ 2 & 3 \\ 3 & 3 \\ 4 & 5 \\ 5 & 5 \end{bmatrix}_{5 \times 2} \quad \text{and} \quad c_2 = \begin{bmatrix} 1 & 0 \\ 2 & 1 \\ 3 & 1 \\ 3 & 2 \\ 5 & 3 \\ 6 & 5 \end{bmatrix}_{6 \times 2}$$

---

### Step 1.1: Calculate Mean Vectors ($\mu_1, \mu_2$)
We compute the coordinate centers by averaging the columns for each matrix:

$$\mu_1 = \begin{bmatrix} \frac{1+2+3+4+5}{5} \\ \frac{2+3+3+5+5}{5} \end{bmatrix} = \begin{bmatrix} \frac{15}{5} \\ \frac{18}{5} \end{bmatrix} = \mathbf{\begin{bmatrix} 3 \\ 3.6 \end{bmatrix}}$$

$$\mu_2 = \begin{bmatrix} \frac{1+2+3+3+5+6}{6} \\ \frac{0+1+1+2+3+5}{6} \end{bmatrix} = \begin{bmatrix} \frac{20}{6} \\ \frac{12}{6} \end{bmatrix} = \mathbf{\begin{bmatrix} 3.3333 \\ 2.0 \end{bmatrix}} \approx \begin{bmatrix} 3.3 \\ 2.0 \end{bmatrix}$$

---

### Step 1.2: Compute Within-Class Scatter Matrices ($S_1, S_2, S_W$)
The scatter matrices are unnormalized covariance matrices, calculated as $S_i = (n_i - 1) \times \text{cov}(c_i)$.

1. **Scatter Matrix for Class 1 ($S_1$):**
   $$S_1 = \begin{bmatrix} 10 & 8 \\ 8 & 7.2 \end{bmatrix}$$

2. **Scatter Matrix for Class 2 ($S_2$):**
   $$S_2 = \begin{bmatrix} 17.3 & 16 \\ 16 & 16 \end{bmatrix}$$

3. **Total Within-Class Scatter Matrix ($S_W = S_1 + S_2$):**
   $$S_W = \begin{bmatrix} 10 & 8 \\ 8 & 7.2 \end{bmatrix} + \begin{bmatrix} 17.3 & 16 \\ 16 & 16 \end{bmatrix} = \mathbf{\begin{bmatrix} 27.3 & 24 \\ 24 & 23.2 \end{bmatrix}}$$

---

### Step 1.3: Compute the Inverse Matrix $S_W^{-1}$
Using the $2 \times 2$ matrix inversion formula $\frac{1}{ad-bc}\begin{bmatrix} d & -b \\ -c & a \end{bmatrix}$:

$$\det(S_W) = (27.3 \times 23.2) - (24 \times 24) = 633.36 - 576 = 57.36$$

$$S_W^{-1} = \frac{1}{57.36} \begin{bmatrix} 23.2 & -24 \\ -24 & 27.3 \end{bmatrix} \approx \mathbf{\begin{bmatrix} 0.39 & -0.41 \\ -0.41 & 0.47 \end{bmatrix}}$$

---

### Step 1.4: Calculate the Optimal Discriminant Line Direction Vector ($v$)
Using the analytic Fisher shortcut formula:

$$v = S_W^{-1}(\mu_1 - \mu_2)$$

First, calculate the difference between the mean vectors:
$$\mu_1 - \mu_2 = \begin{bmatrix} 3 - 3.3333 \\ 3.6 - 2.0 \end{bmatrix} = \begin{bmatrix} -0.3333 \\ 1.6 \end{bmatrix}$$

Now, multiply by the inverse scatter matrix:
$$v = \begin{bmatrix} 0.39 & -0.41 \\ -0.41 & 0.47 \end{bmatrix} \begin{bmatrix} -0.3333 \\ 1.6 \end{bmatrix} = \begin{bmatrix} (0.39 \times -0.3333) + (-0.41 \times 1.6) \\ (-0.41 \times -0.3333) + (0.47 \times 1.6) \end{bmatrix}$$
$$v = \begin{bmatrix} -0.1300 - 0.6560 \\ 0.1367 + 0.7520 \end{bmatrix} = \mathbf{\begin{bmatrix} -0.79 \\ 0.89 \end{bmatrix}}$$

> **Geometric Meaning 💡:** This vector defines the tilt of the optimal projection line. It states that for every $0.79$ units we move to the left, we should step $0.89$ units upwards to align the line with perfect cluster separation.

---

## 2. Concept Name: Multiple Discriminant Analysis (Generalization to $c$ Classes)

### Simple Meaning 💡
Fisher's Linear Discriminant is not limited to separating just two groups. If our dataset contains **$c$ separate classes** (e.g., three different flower species or four types of blood cells), we can project the data onto a multi-dimensional subspace instead of a single 1D line.


### Fundamental Rules of Multiple LDA:
* **Subspace Dimension Bound:** If you have $c$ distinct classes, you can project the dataset down to a maximum of **$c - 1$ dimensions**. For instance, if you have 3 classes, your optimal projection space is a 2D plane ($3 - 1 = 2$).
* **Projection Equation:** We compress samples using a projection matrix $V$:
  $$y_i = V^T x_i$$
  Where $V$ is built by stacking the top $(c-1)$ optimal eigenvectors side-by-side.

---

## 3. Practice Problems with Solutions

### Problem 1: Determining Maximum Subspace Dimensions
**Scenario:** A marketing department applies Multiple Discriminant Analysis to customer profiles to segment them into $c = 5$ distinct purchasing categories based on 20 different background features. 
1. Determine the maximum number of dimensions allowed for the LDA projection space.
2. If the data matrix $X$ has size $1000 \times 20$, what will be the shape of the projection matrix $V$?

#### Step-by-Step Explanation & Calculation:
1. **Find Subspace Bound ($c - 1$):**
   $$\text{Max Dimensions} = c - 1 = 5 - 1 = 4 \text{ dimensions}$$
2. **Find Shape of Matrix $V$:**
   The matrix $V$ maps data from the original feature dimension ($d = 20$) down to our new subspace dimension ($k = 4$). Therefore:
   $$\text{Dimension of } V = d \times k = 20 \times 4$$

---

### Problem 2: Mapping a 2D Point to the Optimal Fisher Line
**Scenario:** Take the first sample from Class 1, $x_1 = \begin{bmatrix} 1 \\ 2 \end{bmatrix}$, and project it onto the optimal Fisher vector $v = \begin{bmatrix} -0.79 \\ 0.89 \end{bmatrix}$ calculated in Section 1. Find its 1D scalar coordinate value $y_1$.

#### Step-by-Step Calculation:
Use the vector dot product projection formula:
$$y_1 = v^T x_1$$
$$y_1 = \begin{bmatrix} -0.79 & 0.89 \end{bmatrix} \begin{bmatrix} 1 \\ 2 \end{bmatrix}$$
$$y_1 = (-0.79 \times 1) + (0.89 \times 2)$$
$$y_1 = -0.79 + 1.78 = \mathbf{0.99}$$

#### Solution Conclusion:
The 1D coordinate of the first sample on the optimal discriminant line is **$0.99$**. Repeating this calculation for all points confirms that Class 1 and Class 2 map to non-overlapping regions along the line.