# Concept Name: Error Minimizing Linear Programming Problem (LPP) for Linear Separability

This markdown note outlines the formulation of an optimization framework used to find a separating hyperplane between two datasets ($A^+$ and $A^-$) while minimizing classification errors.

---

## 1. Core Mathematical Foundations

### Strict Linear Separability
We want to separate two sets of points, $A^+$ (positive class) and $A^-$ (negative class), using a hyperplane defined by weights $w$ and a bias $b$:
*   For $A^+$ points: $A^+ w > eb$
*   For $A^-$ points: $A^- w < eb$

*Note: $e$ is a vector of ones ($[1, 1, \dots, 1]^T$) matching the dimensions of the datasets to properly scale the scalar bias $b$.*

### Scaling and Margin Formulation
By applying a suitable scaling factor to the weights $w$ and bias $b$, strict inequalities can be converted into standard classification margins:
$$A^+ w \geq eb + e$$
$$A^- w \le eb - e$$

### The Plus-Function $(\cdot)_+$ (ReLU/Hinge Loss Operator)
To measure how much a point violates these margins, we define the positive part operator for any scalar $a$:
$$a_+ = \max\{a, 0\}$$

For a vector $x \in \mathbb{R}^n$:
$$x_+ = \begin{pmatrix} (x_1)_+ \\ (x_2)_+ \\ \vdots \\ (x_n)_+ \end{pmatrix}$$

### $L_1$ Norm
The $L_1$ norm sums the absolute values of the elements of a vector:
$$\Vert{}x\Vert{}_1 = \sum_{i=1}^n \vert{}x_i\vert{}$$

---

## 2. Step-by-Step Optimization Formulation

When datasets are **not** perfectly linearly separable, we want to minimize the total classification error.

### Step 1: Rewrite Constraints as Error Terms
If a point is classified correctly and lies on the correct side of the margin, its error should be $0$. If it violates the margin, the error is positive.

*   **For the positive class ($A^+$):** 
    We want $A^+ w - eb - e \geq 0$, which means $-A^+ w + eb + e \le 0$. 
    The violation (error vector) is:
    $$(-A^+ w + eb + e)_+$$

*   **For the negative class ($A^-$):** 
    We want $A^- w - eb + e \le 0$. 
    The violation (error vector) is:
    $$(A^- w - eb + e)_+$$

### Step 2: Formulate the Objective Function
We compute the average error for both classes by taking the $L_1$ norm of the violation vectors and dividing them by the respective number of samples ($m_1$ samples in $A^+$, and $m_2$ samples in $A^-$):

$$\min_{(w,b)} \frac{1}{m_1} \Vert{}(-A^+ w + eb + e)_+\Vert{}_1 + \frac{1}{m_2} \Vert{}(A^- w - eb + e)_+\Vert{}_1$$

### Fundamental Theorem of Separability
> **Theorem:** If $A^+$ and $A^-$ are linearly separable, the minimum error value of the optimization problem is exactly **0**. Conversely, if the minimum value is **0**, the sets are perfectly linearly separable.

---

## 3. Visual Concept Representation

Below is a geometric view of how the margins ($eb+e$ and $eb-e$) penalize misclassified or poorly separated points.

```text
       Class A+ (+)          |        Class A- (-)
                             |
         +      +            |              -
              +              |          -       -
-----------------------------|----------------------------- Hyperplane (w·x = b)
                             |              
    Error = 0                |          Error > 0 
   (Correct Side)            |       (Misclassified (-) point 
                             |        trespassing into A+ zone!)
                             |              * [Penalty applied]

```

---

## 4. Practical Problems & Step-by-Step Calculations

### Problem 1: Evaluating the Plus-Function and $L_1$ Norm

Given an error vector calculated from a test weight setup:


$$x = \begin{pmatrix} -2.5 \\ 4.0 \\ 0.0 \\ -1.2 \end{pmatrix}$$

Find $x_+$ and its $L_1$ norm $\|x_+\|_1$.

#### **Step-by-Step Calculation:**

1. **Apply the max operator to each component:**
* $(x_1)_+ = \max\{-2.5, 0\} = 0$
* $(x_2)_+ = \max\{4.0, 0\} = 4.0$
* $(x_3)_+ = \max\{0.0, 0\} = 0$
* $(x_4)_+ = \max\{-1.2, 0\} = 0$


2. **Assemble the $x_+$ vector:**

$$x_+ = \begin{pmatrix} 0 \\ 4.0 \\ 0 \\ 0 \end{pmatrix}$$


3. **Compute the $L_1$ Norm:**

$$\|x_+\|_1 = |0| + |4.0| + |0| + |0| = 4.0$$



---

### Problem 2: Complete Objective Value Computation

Let's evaluate a simple 1D classification setup to find the total error value.

* **Positive Class ($A^+$):** $m_1 = 2$ points at $x = [3, 4]$
* **Negative Class ($A^-$):** $m_2 = 2$ points at $x = [1, 2.5]$

Let's test the candidate parameters: $w = 2$, $b = 5$.

* Note: Since it's 1D, $e = \begin{pmatrix} 1 \\ 1 \end{pmatrix}$

#### **Step 1: Calculate Error for Class $A^+$**

$$A^+ w = \begin{pmatrix} 3 \\ 4 \end{pmatrix} \cdot 2 = \begin{pmatrix} 6 \\ 8 \end{pmatrix}$$

$$eb + e = \begin{pmatrix} 1 \\ 1 \end{pmatrix}(5) + \begin{pmatrix} 1 \\ 1 \end{pmatrix} = \begin{pmatrix} 6 \\ 6 \end{pmatrix}$$

Compute the violation vector:


$$-A^+ w + eb + e = \begin{pmatrix} -6 \\ -8 \end{pmatrix} + \begin{pmatrix} 6 \\ 6 \end{pmatrix} = \begin{pmatrix} 0 \\ -2 \end{pmatrix}$$

Apply the plus-function:


$$\begin{pmatrix} 0 \\ -2 \end{pmatrix}_+ = \begin{pmatrix} \max\{0,0\} \\ \max\{-2,0\} \end{pmatrix} = \begin{pmatrix} 0 \\ 0 \end{pmatrix}$$

Compute the norm:


$$\|(-A^+w + eb + e)_+\|_1 = 0 + 0 = 0$$

#### **Step 2: Calculate Error for Class $A^-$**

$$A^- w = \begin{pmatrix} 1 \\ 2.5 \end{pmatrix} \cdot 2 = \begin{pmatrix} 2 \\ 5 \end{pmatrix}$$

$$eb - e = \begin{pmatrix} 1 \\ 1 \end{pmatrix}(5) - \begin{pmatrix} 1 \\ 1 \end{pmatrix} = \begin{pmatrix} 4 \\ 4 \end{pmatrix}$$

Compute the violation vector:


$$A^- w - eb + e = \begin{pmatrix} 2 \\ 5 \end{pmatrix} - \begin{pmatrix} 4 \\ 4 \end{pmatrix} = \begin{pmatrix} -2 \\ 1 \end{pmatrix}$$

Apply the plus-function:


$$\begin{pmatrix} -2 \\ 1 \end{pmatrix}_+ = \begin{pmatrix} \max\{-2,0\} \\ \max\{1,0\} \end{pmatrix} = \begin{pmatrix} 0 \\ 1 \end{pmatrix}$$

Compute the norm:


$$\|(A^-w - eb + e)_+\|_1 = 0 + 1 = 1$$

#### **Step 3: Calculate the Total Objective Function Value**

$$\text{Total Error} = \frac{1}{m_1}(0) + \frac{1}{m_2}(1) = \frac{1}{2}(0) + \frac{1}{2}(1) = 0.5$$

**Conclusion:** The total normalized classification error for this layout is **0.5**. Since the value is greater than zero, these specific parameters ($w=2, b=5$) do not yield perfect linear separation.


# Concept Name: Recasting Error Minimizing LPP as a Standard Linear Programming Problem

This markdown note outlines how to transform a non-smooth error minimization problem involving $L_1$ norms and plus-functions into a standard Linear Programming Problem (LPP) that can be easily implemented and solved using computational tools like MATLAB or LINGO.

---

## 1. Step-by-Step Explanation of the Formulation

### Step 1: Handling the Objective Function
The original optimization model tries to minimize normalized violation errors:
$$\min \frac{1}{m_1} \Vert{}(-A^+w + eb + e)_+\Vert{}_1 + \frac{1}{m_2} \Vert{}(A^-w - eb + e)_+\Vert{}_1$$

To remove the absolute values inside the $L_1$ norm and the non-differentiable plus-functions, we define non-negative error variables $y$ and $z$ for each dataset point:
*   Let $y = (-A^+w + eb + e)_+ = \max\{-A^+w + eb + e, 0\}$
*   Let $z = (A^-w - eb + e)_+ = \max\{A^-w - eb + e, 0\}$

Because $y$ and $z$ represent the output of a max function against $0$, every component must be greater than or equal to $0$ ($y \geq 0, z \geq 0$). Thus, the absolute value signs drop out ($\vert{}y_i\vert{} = y_i$ and $\vert{}z_j\vert{} = z_j$), letting us write the $L_1$ norm as a simple dot product with a vector of ones ($e^T$):
$$\frac{1}{m_1}\sum_{i=1}^{m_1} y_i + \frac{1}{m_2}\sum_{j=1}^{m_2} z_j = \frac{e^T y}{m_1} + \frac{e^T z}{m_2}$$

### Step 2: Deriving Linear Constraints
From the definitions of $y$ and $z$ as maximum functions, we get two algebraic properties:
1. $y \geq 0$ and $y \geq -A^+w + eb + e \implies A^+w - eb + y \geq e$
2. $z \geq 0$ and $z \geq A^-w - eb + e \implies -A^-w + eb + z \geq e$

### Recasted Standard LPP Form
Bringing the objective function and constraints together yields a standard LPP:
$$\min_{w,b,y,z} \frac{e^Ty}{m_1} + \frac{e^Tz}{m_2}$$
$$\text{subject to } A^+w - eb + y \geq e$$
$$-A^-w + eb + z \geq e$$
$$y, z \geq 0$$
$$w, b \text{ are unrestricted in sign}$$

---

## 2. Practical Application: Solving the "AND" Logic Gate Problem

Let's apply this layout to the logical **AND** problem to check if it is linearly separable.

### Problem Setup
*   **Positive Class ($A^+$):** Contains $m_1 = 1$ point: $(1, 1)$
*   **Negative Class ($A^-$):** Contains $m_2 = 3$ points: $(0, 0), (0, 1), (1, 0)$
*   **Weight vectors:** Since the data has 2 dimensions, $w = (w_1, w_2)$.

### Step-by-Step Setup and Matrix Computations

#### 1. Formulate Objective Function
Since $m_1 = 1$ and $m_2 = 3$:
$$\text{Min } Z = y_1 + \frac{1}{3}(z_1 + z_2 + z_3)$$

#### 2. Expand Constraints for Positive Class ($A^+$)
For the point $(1,1)$, the constraint $A^+w - b + y_1 \geq 1$ evaluates to:
$$(1\cdot w_1 + 1\cdot w_2) - b + y_1 \geq 1 \implies w_1 + w_2 - b + y_1 \geq 1$$

#### 3. Expand Constraints for Negative Class ($A^-$)
The condition is $-A^-w + eb + z \geq e$. Let's compute it step-by-step for each of the three points:
*   **For point $(0,0)$:**
    $$-(0\cdot w_1 + 0\cdot w_2) + b + z_1 \geq 1 \implies b + z_1 \geq 1$$
*   **For point $(0,1)$:**
    $$-(0\cdot w_1 + 1\cdot w_2) + b + z_2 \geq 1 \implies -w_2 + b + z_2 \geq 1$$
*   **For point $(1,0)$:**
    $$-(1\cdot w_1 + 0\cdot w_2) + b + z_3 \geq 1 \implies -w_1 + b + z_3 \geq 1$$

### Final LPP Layout
$$\text{Min } Z = y_1 + \frac{1}{3}(z_1 + z_2 + z_3)$$
$$\text{s.t. } w_1 + w_2 - b + y_1 \geq 1$$
$$b + z_1 \geq 1$$
$$-w_2 + b + z_2 \geq 1$$
$$-w_1 + b + z_3 \geq 1$$
$$y_1, z_1, z_2, z_3 \geq 0$$

### Optimal Solution Verification
By executing this standard LPP, we obtain the following optimal values:
$$w_1 = 2, \quad w_2 = 2, \quad b = 3$$
$$y_1 = z_1 = z_2 = z_3 = 0 \implies Z = 0$$

Because the minimum error objective value $Z = 0$, **the problem is perfectly linearly separable**.

### Finding the Final Classifier Equation
The separator boundary follows the rule $w^Tx = b$.
$$w_1x_1 + w_2x_2 = b \implies 2x_1 + 2x_2 = 3$$

Dividing the entire equation by 2 gives the final linear classifier line:
$$x_1 + x_2 = 1.5$$

---

## 3. Geometric Visualization Graph

Below is the geometric representation of the **AND** problem space and its separating line.

```text
   x2 ^
      |
  1.0 +   X (0,1)            ● (1,1) [A+]
      |    \
      |     \  Separating Line: x1 + x2 = 1.5
      |      \
--0.0 +---+---X----------+---------> x1
      | (0,0)  \        1.0
      |         \
  1.0 +          X (1,0)
      |

```

* **Legend:**
* `●` represents the positive class $A^+$ point.
* `X` marks the negative class $A^-$ points.
* The diagonal line represents the boundary separating the two classes completely.


# Concept Name: Linear Non-Separability (XOR) and Optimal Separating Hyperplanes

This notebook explores the limits of linear separation using the classical **XOR problem** and introduces the foundational optimization geometric concepts of **Margins**, **Dead Zones**, and **Optimal Separating Hyperplanes**.

---

## 1. The XOR Problem & Proof of Non-Separability

When a classification task cannot achieve zero error using a linear boundary, the datasets are considered **linearly non-separable**. The **XOR (Exclusive OR)** logical gate is the classic example of this phenomenon.

### Dataset Setup
*   **Positive Class ($A^+$):** Contains $m_1 = 2$ points: $(1, 0)$ and $(0, 1)$
*   **Negative Class ($A^-$):** Contains $m_2 = 2$ points: $(0, 0)$ and $(1, 1)$

### Step-by-Step LPP Error Minimization Form
Using our standard error-minimization recasting rule with $m_1=2$ and $m_2=2$:
$$\text{Min } z = \frac{1}{2}(y_1 + y_2) + \frac{1}{2}(z_1 + z_2)$$

#### Expanding the Constraints Step-by-Step:
1.  **For $A^+$ Point 1 $(1,0)$:** 
    $$(1\cdot w_1 + 0\cdot w_2) - b + y_1 \geq 1 \implies w_1 - b + y_1 \geq 1$$
2.  **For $A^+$ Point 2 $(0,1)$:** 
    $$(0\cdot w_1 + 1\cdot w_2) - b + y_2 \geq 1 \implies w_2 - b + y_2 \geq 1$$
3.  **For $A^-$ Point 1 $(0,0)$:** 
    $$-(0\cdot w_1 + 0\cdot w_2) + b + z_1 \geq 1 \implies b + z_1 \geq 1$$
4.  **For $A^-$ Point 2 $(1,1)$:** 
    $$-(1\cdot w_1 + 1\cdot w_2) + b + z_2 \geq 1 \implies -w_1 - w_2 + b + z_2 \geq 1$$

### Optimal Calculations & Solution
When run through an optimization solver, the absolute minimum error parameters are reached at:
$$w_1 = w_2 = b = 0$$
$$y_1 = y_2 = z_1 = z_2 = 1$$

#### Objective Value Evaluation:
$$z = \frac{1}{2}(1 + 1) + \frac{1}{2}(1 + 1) = 1 + 1 = 2$$

> **Conclusion:** Because the minimum error value $z = 2 \neq 0$, the XOR problem is mathematically proven to be **not linearly separable**.

---

## 2. Structural Space Definitions

To prepare for robust classifiers, we rely on core geometric parameters:

### Margin
For any given separating hyperplane $w^Tx = b$, the perpendicular distance separating the two parallel outer bounding boundaries $w^Tx = b - 1$ and $w^Tx = b + 1$ is defined explicitly as the **Margin**.

### Canonical Separating Hyperplane
A hyperplane $w^Tx = b$ is labeled **canonical** if the datasets $A^+$ and $A^-$ are perfectly scaled to clear the margin without any error variables:
$$A^+w \geq eb + e \quad \text{and} \quad A^-w \le eb - e$$

### Dead Zone
The open corridor sandwiched directly between the bounding planes:
$$\{x : (b - 1) < w^Tx < (b + 1)\}$$
For a perfect classifier, this region is completely void of any data points.

---

## 3. Geometric Space Optimization (Maximizing the Margin)

The total geometric width of the dead zone corridor between the bounding planes is computed as:
$$\text{Margin Width} = \frac{2}{\Vert{}w\Vert{}}$$

To get the most robust classifier possible, we want to maximize this distance:
$$\max \frac{2}{\Vert{}w\Vert{}} \iff \min \frac{\Vert{}w\Vert{}}{2}$$

---

## 4. Text-Based Visual Space Graphs

### The XOR Non-Separable Grid Space
Notice how you cannot draw a single straight line to isolate the `●` points from the `X` points without getting something wrong.

```text
   x2 ^
      |
  1.0 +   ● (0,1)            X (1,1)
      |
      |
--0.0 +---X------------------●---------> x1
      | (0,0)               1.0

```

### The Optimal Separating Margin Layout

This shows a perfectly separated dataset where the line sits exactly in the middle of a clear corridor (Dead Zone).

```text
               Class A+ (●)
             ●    ●    ●   
  -------------------------  wᵀx = b + 1  (Upper Bound)
  \                       /
   \  [ DEAD ZONE ]      /   <- Width = 2 / ||w||
    \                   /
  -------------------------  wᵀx = b      (Separating Hyperplane)
      \               /
       \             /       
  -------------------------  wᵀx = b - 1  (Lower Bound)
       X    X    X   
         Class A- (X)

```

---

## 5. Additional Practice Problem

### Problem: Checking Canonical Boundaries

Let a 1D separating hyperplane be defined by $w = [4]$ and $b = 8$. Verify if the point $x = [2.5]$ falls inside the **Dead Zone**.

#### **Step-by-Step Calculation:**

1. **Find the Dead Zone Interval Boundaries:**
* Lower Bound: $b - 1 = 8 - 1 = 7$
* Upper Bound: $b + 1 = 8 + 1 = 9$
* The Dead Zone corridor is defined by: $7 < w^Tx < 9$


2. **Evaluate the Point:**

$$w^Tx = 4 \cdot 2.5 = 10$$


3. **Check Interval Membership:**
Is $7 < 10 < 9$? No, $10 \geq 9$.

**Conclusion:** The value lands outside the dead zone region on the positive side of the bounding margin plane.