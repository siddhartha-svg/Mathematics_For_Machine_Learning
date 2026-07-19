# Concept Name: Hard Margin Support Vector Machine (SVM) Classifier

This notebook details the primal mathematical formulation of a **Hard Margin Classifier** (Support Vector Machine) for linearly separable data, its transition into a Convex Quadratic Programming Problem (QPP), and its Lagrangian optimization setup.

---

## 1. Core Mathematical Concept & Formulation

### Problem Setup
Let $\{x_i \in \mathbb{R}^n, i = 1,2,\dots,m\}$ be a finite set of patterns (data points) that is perfectly **linearly separable**. 
* Each point $x_i$ belongs to one of two classes, labeled as $d_i \in \{-1, +1\}$.
* $d_i$ is the target label for the $i^{th}$ data point.

### Step-by-Step Constraint Consolidation

#### **Step 1: Strict Separation Inequalities**
For a separating hyperplane defined by weights $w \in \mathbb{R}^n$ and bias $b \in \mathbb{R}$:
* $w^Tx_i - b > 0, \quad \forall i \text{ where } d_i = +1$
* $w^Tx_i - b < 0, \quad \forall i \text{ where } d_i = -1$

#### **Step 2: Canonical Scaling for a Hard Margin**
By scaling $w$ and $b$ appropriately, we establish a functional margin corridor of width 1 on each side:
* $w^Tx_i - b \geq +1, \quad \forall i \text{ where } d_i = +1$
* $w^Tx_i - b \le -1, \quad \forall i \text{ where } d_i = -1$

#### **Step 3: Unifying the Constraints**
Multiplying each inequality by its respective class label $d_i$ consolidates the two conditions into a single elegant expression:
$$d_i(w^Tx_i - b) \geq 1, \quad \forall i = 1, 2, \dots, m$$

---

## 2. Primal Optimization Framework (QPP)

The total geometric margin width between the bounding hyperplanes is $\frac{2}{\Vert{}w\Vert{}}$. To maximize safety, we want the hyperplane that makes this margin as large as possible:
$$\max \frac{2}{\Vert{}w\Vert{}} \iff \min \frac{\Vert{}w\Vert{}}{2} \iff \min \frac{1}{2}\Vert{}w\Vert{}^2$$

This gives us the **Primal Quadratic Programming Problem (P1)**:
$$(P1) \quad \min_{w,b} \quad \frac{1}{2}w^Tw$$
$$\text{subject to } d_i(w^Tx_i - b) \geq 1, \quad i = 1, 2, \dots, m$$

> **Note:** Because the objective function is quadratic and the constraints are entirely linear, this is classified as a **Convex Quadratic Programming Problem (QPP)**.

---

## 3. Lagrangian Duality Setup

To solve this constrained optimization problem, we introduce non-negative Lagrange multipliers $\alpha_i \geq 0$ for each constraint.

### The Lagrangian Function $L(w, b, \alpha_i)$
First, rewrite the constraints in standard form as $1 - d_i(w^Tx_i - b) \le 0$. The Lagrangian function is constructed as:
$$L(w, b, \alpha_i) = \frac{1}{2}w^Tw + \sum_{i=1}^m \alpha_i \Big(1 - d_i(w^Tx_i - b)\Big)$$

### Finding the Stationary Conditions
To minimize the primal parameters, we take the partial derivatives of $L$ with respect to $w$ and $b$ and set them to zero:

1. **Gradient with respect to weights ($\nabla_w L = 0$):**
   $$\nabla_w L = w - \sum_{i=1}^m \alpha_i d_i x_i = 0 \implies w = \sum_{i=1}^m \alpha_i d_i x_i$$
   *Meaning:* The optimal weight vector $w$ is a linear combination of the input data points.

2. **Partial derivative with respect to bias ($\frac{\partial L}{\partial b} = 0$):**
   $$\frac{\partial L}{\partial b} = 0 \implies \sum_{i=1}^m \alpha_i d_i = 0$$
   *Meaning:* The sum of the signed Lagrange multipliers must perfectly balance out to zero.

### Complementary Slackness (KKT Condition)
$$\alpha_i \big[1 - d_i(w^Tx_i - b)\big] = 0, \quad \forall i$$
*   If a point lies strictly outside the margin boundary ($d_i(w^Tx_i - b) > 1$), its multiplier drops to zero ($\alpha_i = 0$).
*   If a point sits exactly on the margin border ($d_i(w^Tx_i - b) = 1$), it is allowed to have a non-zero multiplier ($\alpha_i > 0$). These critical boundary points are called **Support Vectors**.

---

## 4. Geometric Margin Visualization Graph

Below is the geometric space layout of a Hard Margin Classifier separating a 2D dataset.

```text
      x2 ^
         |         (● Class +1)
         |       ●       ●
   ======|========================== wᵀx - b = +1   (Positive Margin Border)
         |     .   /
         |Support /
         | Vector/ ◄── Margin Corridor Width = 2 / ||w||
   ──────|──────/─────────────────── wᵀx - b = 0    (Separating Hyperplane)
         |     /
         |    /  Support
         |   / ◄─ Vector
   ======|==/======================= wᵀx - b = -1   (Negative Margin Border)
         | /      X
         |      X       X  (X Class -1)
   ──────┴─────────────────────────► x1

```

---

## 5. Step-by-Step Practice Problems with Calculations

### Problem 1: Unifying Class Constraints

Given a 2D classification challenge containing two points:

* Point 1: $x_1 = [2, 3]^T$ with label $d_1 = +1$
* Point 2: $x_2 = [1, 1]^T$ with label $d_2 = -1$

For the candidate parameters $w = [2, 2]^T$ and $b = 5$, evaluate whether both points satisfy the unified hard margin constraint $d_i(w^Tx_i - b) \geq 1$.

#### **Step-by-Step Calculations:**

1. **Evaluate Point 1 ($i = 1$):**
* Compute inner product $w^Tx_1$:

$$w^Tx_1 = (2 \times 2) + (2 \times 3) = 4 + 6 = 10$$


* Apply bias subtraction:

$$w^Tx_1 - b = 10 - 5 = 5$$


* Multiply by label $d_1 = +1$:

$$d_1(w^Tx_1 - b) = +1 \times 5 = 5$$


* Check constraint: Is $5 \geq 1$? **Yes** (Point 1 satisfies the margin constraint safely).


2. **Evaluate Point 2 ($i = 2$):**
* Compute inner product $w^Tx_2$:

$$w^Tx_2 = (2 \times 1) + (2 \times 1) = 2 + 2 = 4$$


* Apply bias subtraction:

$$w^Tx_2 - b = 4 - 5 = -1$$


* Multiply by label $d_2 = -1$:

$$d_2(w^Tx_2 - b) = -1 \times (-1) = 1$$


* Check constraint: Is $1 \geq 1$? **Yes** (Point 2 sits exactly on the margin boundary).



**Conclusion:** Both points satisfy the unified hard margin constraint framework.

---

### Problem 2: Determining the Optimal Weights from Multipliers

An optimization solver successfully identifies the support vectors for a binary problem and yields the following active non-zero Lagrange multipliers:

* $\alpha_1 = 1.5$ for point $x_1 = [1, 2]^T$ labeled $d_1 = +1$
* $\alpha_2 = 1.5$ for point $x_2 = [2, 1]^T$ labeled $d_2 = -1$
All other multipliers are zero.

1. Check if the dual stationary constraint $\sum \alpha_i d_i = 0$ is preserved.
2. Compute the exact weight vector $w$.

#### **Step-by-Step Calculations:**

1. **Verify the Dual Multiplier Balance Constraint:**

$$\sum_{i=1}^2 \alpha_i d_i = (\alpha_1 \times d_1) + (\alpha_2 \times d_2)$$


$$\sum_{i=1}^2 \alpha_i d_i = (1.5 \times +1) + (1.5 \times -1) = 1.5 - 1.5 = 0 \quad \text{(Constraint is valid!)}$$


2. **Calculate the Weight Vector $w$ using the Stationary Equation:**

$$w = \sum_{i=1}^2 \alpha_i d_i x_i$$


$$w = \alpha_1 d_1 x_1 + \alpha_2 d_2 x_2$$


$$w = 1.5 \times (+1) \times \begin{pmatrix} 1 \\ 2 \end{pmatrix} + 1.5 \times (-1) \times \begin{pmatrix} 2 \\ 1 \end{pmatrix}$$


$$w = \begin{pmatrix} 1.5 \\ 3.0 \end{pmatrix} + \begin{pmatrix} -3.0 \\ -1.5 \end{pmatrix}$$


$$w = \begin{pmatrix} 1.5 - 3.0 \\ 3.0 - 1.5 \end{pmatrix} = \begin{pmatrix} -1.5 \\ 1.5 \end{pmatrix}$$



**Conclusion:** The optimal weight vector derived from the support vector parameters is $w = [-1.5, 1.5]^T$.


# Concept Name: Dual Formulation of Hard Margin Support Vector Machine (SVM) Classifier

This notebook details the step-by-step derivation of the **Dual Optimization Problem** from the Primal Hard Margin SVM using **Karush-Kuhn-Tucker (KKT)** conditions. Transforming the problem into its dual form yields a concave maximization objective that depends only on the inner products of the data points, making it significantly easier to solve computationally.

---

## 1. The Lagrangian Function

To solve the constrained primal optimization problem, we combine the objective function ($\frac{1}{2}w^Tw$) and its inequality constraints into a single unconstrained function using non-negative weights called **Lagrange Multipliers** ($\alpha_i$):

$$L(w, b, \alpha) = \frac{1}{2}w^Tw + \sum_{i=1}^m \alpha_i\Big(1 - d_i(w^Tx_i - b)\Big) \quad \text{--- (1)}$$

### Simple Explanation of Components:
*   **$\frac{1}{2}w^Tw$**: The primal objective term related to minimizing the weight norm (which maximizes the margin boundary thickness).
*   **$\alpha_i$**: The Lagrange multiplier for the $i$-th data point ($x_i$). It acts as a penalty scale; $\alpha_i > 0$ only for points resting exactly on the margin borders (**Support Vectors**).
*   **$1 - d_i(w^Tx_i - b)$**: The structural classification constraint rewritten into a standard format where values $\le 0$ mean correct separation.

---

## 2. The KKT (Karush-Kuhn-Tucker) Conditions

For the primal problem to reach its global optimum, the Lagrangian function must satisfy the following fundamental KKT conditions:

1.  **Stationarity with respect to weights ($w$):**
    $$\nabla_w L = 0 \implies w - \sum_{i=1}^m \alpha_i d_i x_i = 0 \implies w = \sum_{i=1}^m \alpha_i d_i x_i \quad \text{--- (2)}$$
2.  **Stationarity with respect to bias ($b$):**
    $$\frac{\partial L}{\partial b} = 0 \implies \sum_{i=1}^m \alpha_i d_i = 0 \quad \text{--- (3)}$$
3.  **Primal Feasibility:**
    $$1 - d_i(w^Tx_i - b) \leq 0, \quad \forall i = 1, 2, \dots, m \quad \text{--- (4)}$$
4.  **Complementary Slackness:**
    $$\alpha_i\Big(1 - d_i(w^Tx_i - b)\Big) = 0, \quad \forall i = 1, 2, \dots, m \quad \text{--- (5)}$$
5.  **Dual Feasibility:**
    $$\alpha_i \geq 0, \quad \forall i = 1, 2, \dots, m \quad \text{--- (6)}$$

---

## 3. Step-by-Step Mathematical Derivation of the Dual

To obtain the dual problem, we substitute the expressions for $w$ (Equation 2) and the condition on $b$ (Equation 3) back into the primary Lagrangian equation to completely eliminate the primal parameters.

### Step 1: Expand the Lagrangian Function
$$L(w, b, \alpha) = \frac{1}{2}w^Tw + \sum_{i=1}^m \alpha_i - \sum_{i=1}^m \alpha_i d_i w^Tx_i + b\sum_{i=1}^m \alpha_i d_i \quad \text{--- (7)}$$

### Step 2: Apply Bias Stationarity Condition
From Equation (3), we know that $\sum_{i=1}^m \alpha_i d_i = 0$. Therefore, the final term involving $b$ completely vanishes:
$$b\sum_{i=1}^m \alpha_i d_i = b(0) = 0$$

### Step 3: Substitute $w = \sum_{i=1}^m \alpha_i d_i x_i$ into the Remaining Terms
Let's substitute the optimal representation of $w$ into the quadratic term and the linear interaction term:

*   **For the $\frac{1}{2}w^Tw$ term:**
    $$\frac{1}{2}w^Tw = \frac{1}{2}\left(\sum_{i=1}^m \alpha_i d_i x_i\right)^T\left(\sum_{j=1}^m \alpha_j d_j x_j\right) = \frac{1}{2}\sum_{i=1}^m\sum_{j=1}^m \alpha_i \alpha_j d_i d_j x_i^T x_j$$

*   **For the $-\sum_{i=1}^m \alpha_i d_i w^Tx_i$ term:**
    $$-\sum_{i=1}^m \alpha_i d_i \left(\sum_{j=1}^m \alpha_j d_j x_j\right)^Tx_i = -\sum_{i=1}^m\sum_{j=1}^m \alpha_i \alpha_j d_i d_j x_j^T x_i$$
    *(Note: Since $x_j^T x_i = x_i^T x_j$, this matches the quadratic double sum exactly but has a negative coefficient of $-1$.)*

### Step 4: Combine the Simplified Terms
Now, add these modified components back together into Equation (7):
$$L = \frac{1}{2}\sum_{i=1}^m\sum_{j=1}^m \alpha_i \alpha_j d_i d_j x_i^T x_j + \sum_{i=1}^m \alpha_i - \sum_{i=1}^m\sum_{j=1}^m \alpha_i \alpha_j d_i d_j x_i^T x_j$$

Combine the identical double sum terms ($\frac{1}{2} - 1 = -\frac{1}{2}$):
$$L(\alpha) = \sum_{i=1}^m \alpha_i - \frac{1}{2}\sum_{i=1}^m\sum_{j=1}^m \alpha_i \alpha_j d_i d_j x_i^T x_j$$

---

## 4. The Final Dual Optimization Problem (P3)

This leaves us with the standalone **Wolfe Dual Optimization Problem (P3)**:

$$\text{(P3)} \quad \max_{\alpha} \quad \sum_{i=1}^m \alpha_i - \frac{1}{2}\sum_{i=1}^m\sum_{j=1}^m \alpha_i \alpha_j d_i d_j x_i^T x_j$$
$$\text{subject to } \sum_{i=1}^m \alpha_i d_i = 0$$
$$\alpha_i \geq 0, \quad \forall i = 1, 2, \dots, m$$

> **Why is this preferred?** The objective function is concave, meaning any local maximum is a guaranteed global maximum. Additionally, it contains only a single equality constraint instead of many structural geometric bounds, making it far more efficient to solve computationally.

---

## 5. Geometric Mapping Graph

The following ASCII map illustrates how data coordinates dictate the boundary selection, where non-zero multipliers ($\alpha_i > 0$) highlight the boundary-defining Support Vectors.

```text
  x2 ^
     |          (● Class +1)
     |        ● 
     |       / 
  1.0+      ● [α1 = 2.0]  ◄── Support Vector (Helps define the margin)
     |     /
     |    / 
  0.5+   /   ☼ [α = 0.0]  ◄── Regular Point (Has no effect on the boundary)
     |  /
     | /  
  0.0+─●─────────────────────────► x1
     | [α2 = 2.0] ◄── Support Vector (Class -1)
     |

```

---

## 6. Practice Problems with Complete Calculations

### Problem 1: Computing the Dual Objective Value

Given a small dataset with $m=2$ samples:

* $x_1 = \begin{pmatrix} 1 \\ 1 \end{pmatrix}, d_1 = +1$
* $x_2 = \begin{pmatrix} 0 \\ 0 \end{pmatrix}, d_2 = -1$

Evaluate the dual objective function value for the candidate multipliers $\alpha_1 = 2$ and $\alpha_2 = 2$.

#### **Step-by-Step Calculation:**

1. **Verify the Equality Constraint Compliance:**

$$\sum_{i=1}^2 \alpha_i d_i = \alpha_1 d_1 + \alpha_2 d_2 = (2)(1) + (2)(-1) = 2 - 2 = 0 \quad \text{(Valid!)}$$


2. **Compute Inner Vector Matrix Products ($x_i^T x_j$):**
* $x_1^T x_1 = 1^2 + 1^2 = 2$
* $x_2^T x_2 = 0^2 + 0^2 = 0$
* $x_1^T x_2 = (1)(0) + (1)(0) = 0$
* $x_2^T x_1 = 0$


3. **Calculate the Linear Sum Vector ($\sum \alpha_i$):**

$$\sum_{i=1}^2 \alpha_i = \alpha_1 + \alpha_2 = 2 + 2 = 4$$


4. **Calculate the Double Sum Term:**
Expand the nested matrix components for $i, j \in \{1, 2\}$:

$$\text{Sum} = \alpha_1^2 d_1^2 (x_1^T x_1) + \alpha_2^2 d_2^2 (x_2^T x_2) + 2\alpha_1\alpha_2 d_1 d_2 (x_1^T x_2)$$


$$\text{Sum} = (2)^2(1)^2(2) + (2)^2(-1)^2(0) + 2(2)(2)(1)(-1)(0)$$


$$\text{Sum} = (4)(1)(2) + 0 + 0 = 8$$


5. **Compute the Final Objective Value:**

$$\text{Dual Objective Value} = 4 - \frac{1}{2}(8) = 4 - 4 = 0$$



---

### Problem 2: Hyperplane Recovery from Optimal Multipliers

Using the optimal dual parameters calculated in Problem 1 ($\bar{\alpha}_1 = 2, \bar{\alpha}_2 = 2$), recover the explicit parameter weights ($\bar{w}$) and the separating hyperplane bias value ($\bar{b}$).

#### **Step-by-Step Calculation:**

1. **Reconstruct the Weight Vector ($\bar{w}$) via Equation (2):**

$$\bar{w} = \sum_{i=1}^2 \bar{\alpha}_i d_i x_i = \bar{\alpha}_1 d_1 x_1 + \bar{\alpha}_2 d_2 x_2$$


$$\bar{w} = (2)(1)\begin{pmatrix} 1 \\ 1 \end{pmatrix} + (2)(-1)\begin{pmatrix} 0 \\ 0 \end{pmatrix} = \begin{pmatrix} 2 \\ 2 \end{pmatrix} + \begin{pmatrix} 0 \\ 0 \end{pmatrix} = \begin{pmatrix} 2 \\ 2 \end{pmatrix}$$


2. **Calculate the Separation Bias ($\bar{b}$) using Complementary Slackness:**
Since $\bar{\alpha}_1 = 2 > 0$, the first point is a support vector resting exactly on the margin boundary:

$$d_1(\bar{w}^Tx_1 - \bar{b}) = 1 \implies \bar{w}^Tx_1 - \bar{b} = \frac{1}{d_1}$$



Substitute $\bar{w} = \begin{pmatrix} 2 \\ 2 \end{pmatrix}$, $x_1 = \begin{pmatrix} 1 \\ 1 \end{pmatrix}$, and $d_1 = 1$:

$$\begin{pmatrix} 2 \\ 2 \end{pmatrix}^T \begin{pmatrix} 1 \\ 1 \end{pmatrix} - \bar{b} = 1$$


$$(2 \times 1) + (2 \times 1) - \bar{b} = 1 \implies 4 - \bar{b} = 1 \implies \bar{b} = 3$$


3. **Verify Consistency with Second Support Vector ($x_2$):**

$$\bar{w}^Tx_2 - \bar{b} = \frac{1}{d_2} \implies \begin{pmatrix} 2 \\ 2 \end{pmatrix}^T \begin{pmatrix} 0 \\ 0 \end{pmatrix} - 3 = -1 \implies -3 = -3 \quad \text{(Consistent!)}$$



**Final Conclusion:** The recovered separating hyperplane equation is $2x_1 + 2x_2 = 3$.


# Concept Name: Hard Margin Support Vector Machine (SVM) Formulations & Complete Geometric Solver Example

This note outlines a full numerical problem demonstrating how to translate a 2D linearly separable classification dataset into a **Primal Quadratic Programming Problem (QPP)**, interpret the optimization solution, and reconstruct the final geometric classifier line.

---

## 1. Step-by-Step Mathematical Formulation Rules

### Step 1: Establish the Raw Coordinate Sets
We are given a 2D space containing two distinct finite coordinate sets:
*   **Negative Class ($A^-$ / Label $d_i = -1$):** $\{(1, 2), (2, 1), (3, 2), (2, 3)\}$
*   **Positive Class ($A^+$ / Label $d_i = +1$):** $\{(5, 4), (4, 5), (5, 6), (6, 5)\}$

### Step 2: Set up the Primal Objective Function
Since the variable domain lies in 2D space, the weight vector is defined as $w = (w_1, w_2)^T$. The task aims to minimize the structural weight norm:
$$\min \frac{1}{2}\Vert{}w\Vert{}^2 = \min \frac{1}{2}(w_1^2 + w_2^2)$$

### Step 3: Expand the Hard Margin Classifier Conditions
We apply the unified canonical boundary condition $d_i(w^Tx_i - b) \geq 1$ individually to every pattern point in the space:

#### For the Negative Class Points ($d_i = -1$):
The constraint $-(w_1x_{i1} + w_2x_{i2} - b) \geq 1$ yields:
1.  **Point $(1,2)$:** $-(w_1 + 2w_2 - b) \geq 1 \implies -w_1 - 2w_2 + b \geq 1$
2.  **Point $(2,1)$:** $-(2w_1 + w_2 - b) \geq 1 \implies -2w_1 - w_2 + b \geq 1$
3.  **Point $(3,2)$:** $-(3w_1 + 2w_2 - b) \geq 1 \implies -3w_1 - 2w_2 + b \geq 1$
4.  **Point $(2,3)$:** $-(2w_1 + 3w_2 - b) \geq 1 \implies -2w_1 - 3w_2 + b \geq 1$

#### For the Positive Class Points ($d_i = +1$):
The constraint $+(w_1x_{i1} + w_2x_{i2} - b) \geq 1$ yields:
5.  **Point $(5,4)$:** $5w_1 + 4w_2 - b \geq 1$
6.  **Point $(4,5)$:** $4w_1 + 5w_2 - b \geq 1$
7.  **Point $(5,6)$:** $5w_1 + 6w_2 - b \geq 1$
8.  **Point $(6,5)$:** $6w_1 + 5w_2 - b \geq 1$

*The optimization variables $w_1, w_2,$ and $b$ are completely unrestricted in sign.*

---

## 2. Quantitative Optimization Solution & Line Recovery

After implementing the eight constraint inequality structures into a standard numerical solver, we arrive at the absolute optimal spatial parameters:
$$w_1 = 0.5, \quad w_2 = 0.5, \quad b = 3.5$$

### Reconstructing the Separating Hyperplane Plane Equation
The general dividing hyperplane path follows $w^Tx = b$:
$$w_1x_1 + w_2x_2 = b \implies 0.5x_1 + 0.5x_2 = 3.5$$

Multiplying the entire expression by 2 simplifies it to its final recognizable geometric form:
$$x_1 + x_2 = 7 \implies x_2 = -x_1 + 7$$

---

## 3. Geometric Verification of Support Vector Margins

Let's plug our optimal parameters back into the boundary limits to see which specific coordinate points act as the **Support Vectors** (the critical points that sit exactly on the margin boundaries with an error balance of zero).

### Bounding Limit 1: The Lower Negative Margin ($w^Tx - b = -1$)
$$0.5x_1 + 0.5x_2 - 3.5 = -1 \implies 0.5x_1 + 0.5x_2 = 2.5 \implies x_1 + x_2 = 5$$
*   Test point $(3,2)$: $3 + 2 = 5$ (Sits exactly on the boundary line)
*   Test point $(2,3)$: $2 + 3 = 5$ (Sits exactly on the boundary line)
*   *Conclusion:* Points $(3,2)$ and $(2,3)$ are the support vectors for Class $-1$.

### Bounding Limit 2: The Upper Positive Margin ($w^Tx - b = +1$)
$$0.5x_1 + 0.5x_2 - 3.5 = 1 \implies 0.5x_1 + 0.5x_2 = 4.5 \implies x_1 + x_2 = 9$$
*   Test point $(5,4)$: $5 + 4 = 9$ (Sits exactly on the boundary line)
*   Test point $(4,5)$: $4 + 5 = 9$ (Sits exactly on the boundary line)
*   *Conclusion:* Points $(5,4)$ and $(4,5)$ are the support vectors for Class $+1$.

---

## 4. Text-Based Space Visualization Graph

Below is the geometric space visualization of our calculated hyperplane system. The clear corridor between the upper and lower bounds represents the optimal **Dead Zone margin**.

```text
  x2 ^
     |
 6.0 +           o (5,6)
     |         /   \
 5.0 +       o (4,5) o (6,5)     [+] Upper Bound Margin line: x1 + x2 = 9
     |     /   \   /
 4.0 +   /       o (5,4)
     |  /      /
 3.0 + /     # (2,3)             [☼] Separating Optimal Hyperplane: x1 + x2 = 7
     |/    /   \
 2.0 +   # (1,2) # (3,2)         [-] Lower Bound Margin line: x1 + x2 = 5
     |     \   /
 1.0 +       # (2,1)
     |
 0.0 +---+---+---+---+---+---+───► x1
    0.0 1.0 2.0 3.0 4.0 5.0 6.0

```

* **Legend:**
* `o` represents Positive Class points ($A^+$).
* `#` represents Negative Class points ($A^-$).
* The diagonal lines represent the margin corridor limits.


---

## 5. Additional Practice Problem with Solution

### Problem Challenge

Using the final optimal weight vector derived above, $w = (0.5, 0.5)^T$, calculate the exact geometric margin distance separating the two classes.

#### **Step-by-Step Calculation:**

1. **State the Geometric Margin Formula:**

$$\text{Margin Width} = \frac{2}{\|w\|}$$


2. **Calculate the Euclidean Norm of the Weight Vector ($\|w\|$):**

$$\|w\| = \sqrt{w_1^2 + w_2^2} = \sqrt{(0.5)^2 + (0.5)^2}$$


$$\|w\| = \sqrt{0.25 + 0.25} = \sqrt{0.5}$$


3. **Substitute the Norm Value back into the Width Equation:**

$$\text{Margin Width} = \frac{2}{\sqrt{0.5}}$$


4. **Rationalize and Simplify the Expression:**
Since $\sqrt{0.5} = \frac{1}{\sqrt{2}}$:

$$\text{Margin Width} = \frac{2}{\frac{1}{\sqrt{2}}} = 2\sqrt{2} \approx 2.828$$



**Final Conclusion:** The absolute optimal geometric gap separating the parallel margin boundaries is exactly $2\sqrt{2}$ (or approximately **2.828** units).



