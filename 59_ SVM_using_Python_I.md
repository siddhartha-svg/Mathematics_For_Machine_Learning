# Concept Name: Introduction to SVM Classification Boundaries and Margin Mechanics in Python

This notebook introduces the practical implementation of binary Support Vector Machine (SVM) classifiers using Python. It demonstrates how synthetic data is generated and explores the geometry behind choosing the optimal separating hyperplane among multiple candidate boundaries.

---

## 1. Python Practical Framework & Environment Setup

To analyze classification boundaries, we generate a synthetic dataset and evaluate custom linear separators.

### Step 1: Import Core Utilities
We leverage standard data management and visualization libraries:
```python
import numpy as np
import matplotlib.pyplot as plt
from scipy import stats

```

### Step 2: Generate Synthetic Binary Data

Using `scikit-learn`, we generate two distinct isotropic Gaussian clusters (blobs) that are perfectly linearly separable:

```python
from sklearn.datasets import make_blobs

# Generate 100 samples distributed across 2 classes
X, y = make_blobs(n_samples=100, centers=2, random_state=0, cluster_std=0.65)

# Plot the points using a color map to separate labels visually
plt.scatter(X[:, 0], X[:, 1], c=y, s=60, cmap='autumn')

```

---

## 2. Mathematical Conception of Candidate Hyperplanes and Margins

When data is linearly separable, an infinite number of straight lines can perfectly segregate the classes. To evaluate these lines, we define candidate boundaries using standard slope-intercept forms along with a margin offset buffer.

### The Linear Separator Equation

Each candidate line is defined by three parameters $(m, b, d)$:


$$y = mx + b$$

Where:

* **$m$**: The slope of the line.
* **$b$**: The $y$-intercept.
* **$d$**: The margin parameter (half-width of the margin corridor).

### Bounding Corridor Equations

The upper and lower boundaries that encapsulate the "dead zone" or margin around the decision line are calculated as:


$$\text{Upper Boundary Line} = mx + b + d$$

$$\text{Lower Boundary Line} = mx + b - d$$

### Code Implementation for Multiple Candidates

We test three arbitrary linear equations to see how they fit between the clusters:

```python
xfit = np.linspace(-1, 3.5)
plt.scatter(X[:, 0], X[:, 1], c=y, s=50, cmap='autumn')

# Loop through three custom parameter sets (slope m, intercept b, margin d)
for m, b, d in [(1, 0.65, 0.33), (0.5, 1.6, 0.55), (-0.2, 2.9, 0.2)]:
    yfit = m * xfit + b
    plt.plot(xfit, yfit, '-k') # Plot the main decision line
    
    # Fill the margin corridor surrounding the line
    plt.fill_between(xfit, yfit - d, yfit + d, edgecolor='none', color='#AAAAAA', alpha=0.4)

plt.xlim(-1, 3.5)

```

---

## 3. Geometric Space Visualization

Below is the text-based ASCII representation of the generated data clusters and the intersection of the candidate classification boundaries.

```text
    y ^
      |           [Class 1: Red Blobs]
  5.0 +             ●    ●    ●   \ Candidate Line 3 (Negative Slope)
      |            ●   ●   ●   ●   \
  4.0 +              ●   ●   ●      \___________ Upper Margin Band 2
      |               \              \         /
  3.0 + ────────────────\─────────────\───────/─── Candidate Line 2 (Slope 0.5)
      |                  \             \     /
  2.0 +                   \    ○   ○    \   /_____ Lower Margin Band 2
      |                    \ ○   ○   ○   \ /
  1.0 +                     \  ○   ○      /
      |                      \           / Candidate Line 1 (Slope 1.0)
  0.0 +---+───+───+───+───+───+───+───+───+───> x
     -1.0 0.0 1.0 2.0 3.0       [Class 2: Yellow Blobs]

```

---

## 4. Computational Practice Problems

### Problem 1: Point Verification Relative to a Margin Corridor

Consider a candidate classification line defined by parameters $(m = 1, b = 0.65, d = 0.33)$. Determine whether the data coordinate point $P(1.5, 2.0)$ falls inside the shaded margin corridor, safely in the upper class zone, or safely in the lower class zone.

#### **Step-by-Step Calculation:**

1. **Calculate the $y$-value of the decision line at $x = 1.5$:**

$$y_{\text{line}} = mx + b = (1 \times 1.5) + 0.65 = 1.5 + 0.65 = 2.15$$


2. **Compute the Upper and Lower Margin Bounds at $x = 1.5$:**

$$y_{\text{upper}} = y_{\text{line}} + d = 2.15 + 0.33 = 2.48$$


$$y_{\text{lower}} = y_{\text{line}} - d = 2.15 - 0.33 = 1.82$$


3. **Compare the point's actual $y$-coordinate ($y_P = 2.0$) against the boundaries:**
* Is $y_P$ between $y_{\text{lower}}$ and $y_{\text{upper}}$?
* Checking the inequality: $1.82 \le 2.0 \le 2.48$



**Conclusion:** Because $2.0$ falls within the structural interval $[1.82, 2.48]$, the point $P(1.5, 2.0)$ sits **inside the margin corridor (dead zone)**.

---

### Problem 2: Calculating Margin Interval Widths

Evaluate the second candidate configuration sequence $(m = 0.5, b = 1.6, d = 0.55)$. Find the complete vertical span (thickness) of the margin corridor, and compute the exact vertical coordinate range of the corridor at the slice position $x = 2.0$.

#### **Step-by-Step Calculation:**

1. **Calculate the total vertical span of the corridor:**

$$\text{Total Vertical Span} = (mx + b + d) - (mx + b - d) = 2d$$


$$\text{Total Vertical Span} = 2 \times 0.55 = 1.10 \text{ units}$$


2. **Find the baseline midpoint coordinate on the line at $x = 2.0$:**

$$y_{\text{line}} = mx + b = (0.5 \times 2.0) + 1.6 = 1.0 + 1.6 = 2.6$$


3. **Compute the boundary limits at this specific slice:**

$$y_{\text{upper}} = 2.6 + 0.55 = 3.15$$


$$y_{\text{lower}} = 2.6 - 0.55 = 2.05$$



**Conclusion:** The total vertical span thickness is **1.10 units**, and at the $x = 2.0$ coordinate slice, the margin corridor spans the exact vertical interval of **$[2.05, 3.15]$**.


# Concept Name: Programming Support Vector Classifiers (SVC) and Spatial Mapping with Scikit-Learn

This notebook outlines the implementation of a Support Vector Classifier (SVC) in Python using Scikit-Learn. It details hyperparameter tuning parameters ($C$, kernels, and gamma), provides a comprehensive custom script to dynamically map spatial decision boundaries, and explores the core property of margin stability governed strictly by support vectors.

---

## 1. Core Model Construction and Hyperparameters

To program an SVM, we instantiate a `Support vector classifier` (SVC) object from the `sklearn.svm` library.

### Initialization Syntax
```python
from sklearn.svm import SVC

# Instantiating a hard margin classifier configuration
model = SVC(kernel='linear', C=10000000)
model.fit(X, y)

```

### Key Parameter Definitions

* **$C$ (Regularization Parameter)**: A positive floating-point parameter controls the trade-off between maximizing the margin thickness and minimizing classification errors. The penalty strength scales **inversely** with $C$ using a squared $\ell_2$ penalty:
* **Large $C$ ($10^7$)**: Behaves like a **Hard Margin**, severely penalizing any margin violations or misclassifications.
* **Small $C$ ($1.0$)**: Behaves like a **Soft Margin**, allowing a wider corridor while tolerating occasional cluster overlaps.


* **kernel**: Selects the mathematical mapping algorithm to compute decision spaces. Built-in choices include `'linear'`, `'poly'`, `'rbf'`, and `'sigmoid'` (default is `'rbf'`).
* **degree**: Specifies the degree for a polynomial (`'poly'`) kernel function, ignored by other functions.
* **gamma**: The structural coefficient parameter utilized by the `'rbf'`, `'poly'`, and `'sigmoid'` kernels. If `gamma='scale'` is chosen, it assigns the inverse variance scale:

$$\gamma = \frac{1}{n_{\text{features}} \cdot \text{Var}(X)}$$



If `gamma='auto'`, it assigns $\frac{1}{n_{\text{features}}}$.

---

## 2. Dynamic Decision Boundary Visualization Function

To accurately map out the separating hyperplane ($w^Tx - b = 0$) and its margin boundaries ($w^Tx - b = \pm 1$), we use a custom visualization script that generates a mesh grid across the feature coordinates.

```python
def plot_svc_decision_function(model, ax=None, plot_support=True):
    """Plot the decision function for a 2D SVC"""
    if ax is None:
        ax = plt.gca()
    
    # Extract current structural axis bounds from the active figure
    xlim = ax.get_xlim()
    ylim = ax.get_ylim()
    
    # Step 1: Generate a 30x30 coordinate sampling grid over space
    x = np.linspace(xlim[0], xlim[1], 30)
    y = np.linspace(ylim[0], ylim[1], 30)
    Y, X = np.meshgrid(y, x)
    
    # Step 2: Flatten and stack grid matrices into a 2D coordinate array
    xy = np.vstack([X.ravel(), Y.ravel()]).T
    
    # Step 3: Compute raw signed distance output from the separating plane
    P = model.decision_function(xy).reshape(X.shape)
    
    # Step 4: Plot decision boundaries and margin corridors using contours
    ax.contour(X, Y, P, colors='k',
               levels=[-1, 0, 1], alpha=0.5,
               linestyles=['--', '-', '--'])
    
    # Step 5: Highlight the critical Support Vectors visually
    if plot_support:
        ax.scatter(model.support_vectors_[:, 0],
                   model.support_vectors_[:, 1],
                   s=300, linewidth=1, facecolors='none', edgecolors='k')
                   
    ax.set_xlim(xlim)
    ax.set_ylim(ylim)

```

---

## 3. Core Geometric Property: Support Vector Dominance

A fundamental key to an SVM classifier's success is that the optimal separating boundary is determined **exclusively** by the position of the support vectors.

* Any regular data points located safely outside the margin corridor on the correct side do not alter or contribute to the final mathematical fit.
* **Technical Explanation**: These safe points do not contribute to the loss function optimization. Therefore, adding or moving data points far outside the margin corridor has no impact on the hyperplane parameters, so long as they do not cross into the margin zone.

```python
# To inspect the exact support vector coordinates computed by the solver:
print(model.support_vectors_)

```

---

## 4. Text-Based 2D Grid Representation

The layout below illustrates how the decision contours isolate data clusters. The coordinate points enclosed in large brackets represent the **Support Vectors** identified by `model.support_vectors_`.

```text
  Feature 2 (y)
     ▲
 5.0 │         ●  ●  ●  ●
     │       ●   ●  ●  ●
 4.0 │──────[●]──────────────────────────  Upper Margin Corridor line (P = 1)
     │       \
 3.0 │────────\──────────────────────────  Main Hyperplane Separator (P = 0)
     │         \
 2.0 │──────────[○]──────────────────────  Lower Margin Corridor line (P = -1)
     │            ○   ○   ○  ○
 1.0 │          ○   ○   ○
     │
     └───────────┴───────────┴───────────► Feature 1 (x)
                1.0         2.0         3.0

```

---

## 5. Practice Problems with Step-by-Step Calculations

### Problem 1: Manual Evaluation of Gamma Coefficients

A 2D feature dataset containing 2 features ($n_{\text{features}} = 2$) undergoes an RBF kernel SVM training pass with `gamma='scale'`. A variance check yields an explicit dataset variance value of $\text{Var}(X) = 0.25$. Calculate the exact value assigned to the gamma parameter.

#### **Step-by-Step Calculation:**

1. **Recall the definition for the scaling rule coefficient:**

$$\gamma = \frac{1}{n_{\text{features}} \cdot \text{Var}(X)}$$


2. **Substitute the known structural problem parameters ($n_{\text{features}} = 2$ and $\text{Var}(X) = 0.25$):**

$$\gamma = \frac{1}{2 \cdot 0.25}$$


3. **Calculate the denominator score:**

$$\text{Denominator} = 2 \times 0.25 = 0.50$$


4. **Compute the final inversion result:**

$$\gamma = \frac{1}{0.50} = 2.0$$



**Conclusion:** The exact functional value calculated for gamma under the scale framework is **2.0**.

---

### Problem 2: Mapping Grid Array Flattening Transformations

During the execution of `plot_svc_decision_function`, the sampling limits yield short coordinate vectors $x = [0, 1, 2]$ and $y = [10, 20]$. Show the step-by-step matrix changes that occur when building the grid array using `meshgrid`, `ravel`, and `vstack`.

#### **Step-by-Step Matrix Generation Steps:**

1. **Generate the initial 2D coordinate grid using `meshgrid(y, x)`:**

$$X = \begin{pmatrix} 0 & 0 \\ 1 & 1 \\ 2 & 2 \end{pmatrix}, \quad Y = \begin{pmatrix} 10 & 20 \\ 10 & 20 \\ 10 & 20 \end{pmatrix}$$


2. **Flatten the matrices into 1D arrays using `ravel()`:**

$$X.\text{ravel}() = [0, 0, 1, 1, 2, 2]$$


$$Y.\text{ravel}() = [10, 20, 10, 20, 10, 20]$$


3. **Stack them vertically and transpose using `np.vstack([...]).T`:**

$$\text{vstack} = \begin{pmatrix} 0 & 0 & 1 & 1 & 2 & 2 \\ 10 & 20 & 10 & 20 & 10 & 20 \end{pmatrix}$$


$$\text{Transpose Matrix (xy)} = \begin{pmatrix} 0 & 10 \\ 0 & 20 \\ 1 & 10 \\ 1 & 20 \\ 2 & 10 \\ 2 & 20 \end{pmatrix}$$



**Conclusion:** The operations successfully compile the coordinate grids into a structured matrix of size $6 \times 2$, ready to evaluate the decision boundary distance function.


# Support Vector Machines (SVM) & Kernel Tricks

This notebook covers the fundamental concepts of Support Vector Machines (SVM), including linear decision boundaries, support vectors, and dealing with non-linearly separable data using the RBF (Radial Basis Function) Kernel Trick.

---

## 1. Linear Support Vector Machine (Linear SVM)

### Concept Name
**Maximal Margin Classifier & Linear Support Vector Classifier**

### Simple Explanation
Imagine you have red dots and yellow dots on a sheet of paper. You want to draw a straight line to perfectly separate them. 
* A **Linear SVM** finds the **best possible straight line** (called a *Decision Boundary* or *Hyperplane*).
* The "best" line is the one that stays as far away as possible from the closest dots of both groups. 
* This empty space around the line is called the **Margin**. 
* The special data points right on the edge of the margin are called **Support Vectors**. If you move them, the boundary line moves.

### Text-Art Visualization (Graph)
```text
  Feature Y 
     ^
     |    (Red)    (Red)
     |       (Red)    \
  5 -|                 \  <-- Upper Margin Line
     |==================\=============
     |                   \  <-- Main Decision Boundary (Hyperplane)
  3 -|====================\===========
     |                     \ <-- Lower Margin Line
     |      (Yellow)        \
  1 -|          (Yellow)
     |
     +----------------------------------> Feature X
            1         2         3

```

### Numerical Calculation Example

The mathematical formulation for the decision boundary hyperplane is:


$$w \cdot x + b = 0$$

Let's assume a 1D problem to make calculations easy:

* Class 1 (Red) has a point at $x_1 = 4$
* Class 2 (Yellow) has a point at $x_2 = 2$

**Step 1: Calculate the middle point (Decision Boundary)**


$$x_{boundary} = \frac{x_1 + x_2}{2} = \frac{4 + 2}{2} = 3$$

**Step 2: Calculate the Margin ($M$)**
The distance from the boundary to the closest point:


$$M = \vert{}x_1 - x_{boundary}\vert{} = \vert{}4 - 3\vert{} = 1$$


Total width of the corridor is $2M = 2$.

---

## 2. Implementing Linear SVM in Python

Here is how we generate a clean blob dataset and fit a linear Support Vector Classifier.

```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn.datasets import make_blobs
from sklearn.svm import SVC

# Step 1: Generate 100 random datapoints clustered in 2 distinct groups
X, y = make_blobs(n_samples=100, centers=2, random_state=0, cluster_std=0.95)

# Step 2: Plot the generated raw data points
plt.scatter(X[:, 0], X[:, 1], c=y, s=60, cmap='autumn')
plt.title("Linearly Separable Data Blobs")
plt.xlabel("Feature 1")
plt.ylabel("Feature 2")
plt.show()

# Step 3: Train a Linear Support Vector Machine
model = SVC(kernel='linear', C=1E6)
model.fit(X, y)

# Step 4: Identify the critical points (Support Vectors)
print("Coordinates of Support Vectors:\n", model.support_vectors_)

```

---

## 3. The Problem of Non-Linearity & The Kernel Trick

### Concept Name

**Kernel Trick using Radial Basis Function (RBF)**

### Simple Explanation

Sometimes, data points are arranged in a ring or circle where one class is completely surrounded by another class. If you draw a straight line anywhere through it, you will fail to separate them cleanly.

To fix this, we use a **Kernel Trick (RBF)**. It calculates a "projection score" based on how close data points are to a central reference. This creates a new **3rd dimension** ($Z$-axis), lifting the inner circle points up into a mountain shape, while leaving the outer ring points down in the valley. Now, you can easily slide a flat sheet of paper (a linear plane) right between the mountain and the valley to separate them perfectly!

### Mathematical Formula (RBF Kernel)

The radial basis function score ($r$) between a point and the origin can be represented simplistically as:


$$r = e^{-\sum (X^2)}$$

### Practice Problem: Mapping to 3D Space

Let's manually compute the new $Z$-axis coordinate ($r$) for two data points using the exact code equation: `r = np.exp(-(X ** 2).sum(1))`

#### Point A (Inner Circle):

* Coordinates: $X_A = [0.1, 0.2]$
* **Step 1:** Square the features: $0.1^2 = 0.01$, $0.2^2 = 0.04$
* **Step 2:** Sum them up: $0.01 + 0.04 = 0.05$
* **Step 3:** Apply exponential negative power: $r_A = e^{-0.05} \approx 0.951$ *(High value, lifted up)*

#### Point B (Outer Ring):

* Coordinates: $X_B = [1.0, 1.0]$
* **Step 1:** Square the features: $1.0^2 = 1.0$, $1.0^2 = 1.0$
* **Step 2:** Sum them up: $1.0 + 1.0 = 2.0$
* **Step 3:** Apply exponential negative power: $r_B = e^{-2.0} \approx 0.135$ *(Low value, stays down)*

---

## 4. Implementing RBF Kernel SVM in Python

When we apply the RBF kernel, `Scikit-Learn` handles this higher-dimensional transformation automatically behind the scenes.

```python
from sklearn.datasets import make_circles

# Step 1: Generate concentric circular data (Non-linearly separable)
X, y = make_circles(n_samples=100, factor=0.1, noise=0.1, random_state=0)

# Step 2: Train the SVM using the 'rbf' kernel trick
clf = SVC(kernel='rbf', C=1E6)
clf.fit(X, y)

# Step 3: Define a helpful function to plot boundaries and support vectors

def plot_svc_decision_function(model, ax=None, plot_support=True):
    if ax is None:
        ax = plt.gca()
    xlim = ax.get_xlim()
    ylim = ax.get_ylim()
    
    # Create evaluation grid
    x = np.linspace(xlim[0], xlim[1], 30)
    y = np.linspace(ylim[0], ylim[1], 30)
    Y, X = np.meshgrid(y, x)
    xy = np.vstack([X.ravel(), Y.ravel()]).T
    P = model.decision_function(xy).reshape(X.shape)
    
    # Plot decision boundary and margins
    ax.contour(X, Y, P, colors='k',
               levels=[-1, 0, 1], alpha=0.5,
               linestyles=['--', '-', '--'])
    
    # Highlight support vectors with a large outer circle ring
    if plot_support:
        ax.scatter(model.support_vectors_[:, 0],
                   model.support_vectors_[:, 1],
                   s=300, linewidth=1, facecolors='none', edgecolors='black')
    ax.set_xlim(xlim)
    ax.set_ylim(ylim)

# Step 4: Render the final non-linear classification graph
plt.scatter(X[:, 0], X[:, 1], c=y, s=50, cmap='autumn')
plot_svc_decision_function(clf, plot_support=True)
plt.title("RBF Kernel Successfully Separating Circular Boundaries")
plt.show()
