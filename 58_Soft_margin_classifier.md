
# Concept Name: Soft Margin Support Vector Machine (SVM) Classifier

When a dataset is **not linearly separable**, it is impossible to find a hyperplane that separates the positive and negative classes perfectly without errors. The **Soft Margin Classifier** introduces non-negative slack variables (error variables) to allow a controlled amount of misclassification or margin violation, trading off margin width with error reduction.

---

## 1. Core Mathematical Setup

### Given Variables:
*   **Patterns**: Let $\{x_i \in \mathbb{R}^n, i = 1, 2, \dots, m\}$ be the set of finite input data points.
*   **Target Labels**: $d_i \in \{+1, -1\}$ denotes the target classification label for the $i^{th}$ data pattern.
*   **Slack / Error Variables**: $\xi_i \geq 0$ represents the deviation or error for the $i^{th}$ data point.

### The Primal Optimization Problem (SP)
To optimize a soft margin classifier, we want to maximize the margin width $\frac{2}{\Vert{}w\Vert{}}$ (which corresponds to minimizing $\frac{1}{2}w^Tw$) while simultaneously minimizing the total classification error $\sum_{i=1}^m \xi_i$. 

Mathematically, this is modeled as the following Primal problem:
$$(SP) \quad \min_{(w,b,\xi)} \quad \frac{1}{2}w^Tw + C\sum_{i=1}^m \xi_i$$
$$\text{subject to } d_i(w^Tx_i - b) + \xi_i \geq 1, \quad (i = 1, 2, \dots, m)$$
$$\xi_i \geq 0, \quad (i = 1, 2, \dots, m)$$

*Here, $C > 0$ is a regularization parameter that determines the trade-off penalty cost between a larger margin and smaller training error.*

---

## 2. Step-by-Step Optimization and Lagrangian Formulation

To find the optimal hyperparameters using duality theory, we convert the constrained optimization problem into an unconstrained function by adding Lagrange multipliers.

### Step 1: Construct the Lagrangian Function
We associate multipliers $\alpha_i \geq 0$ with the classification constraints and $\beta_i \geq 0$ with the slack non-negativity constraints:
$$L(w, b, \xi, \alpha, \beta) = \frac{1}{2}w^Tw + C\sum_{i=1}^m \xi_i + \sum_{i=1}^m \alpha_i \Big(1 - \xi_i - d_i(w^Tx_i - b)\Big) - \sum_{i=1}^m \beta_i\xi_i$$

### Step 2: Compute Stationary Conditions (Optimality Criteria)
We take the partial derivatives of $L$ with respect to the primal variables ($w, b, \xi_i$) and set them to zero:

1.  **With respect to weights ($\nabla_w L = 0$):**
    $$w - \sum_{i=1}^m \alpha_i d_i x_i = 0 \implies w = \sum_{i=1}^m \alpha_i d_i x_i$$
2.  **With respect to bias ($\frac{\partial L}{\partial b} = 0$):**
    $$\sum_{i=1}^m \alpha_i d_i = 0$$
3.  **With respect to errors ($\frac{\partial L}{\partial \xi_i} = 0$):**
    $$C - \alpha_i - \beta_i = 0 \implies \alpha_i + \beta_i = C$$

### Step 3: Complementary Slackness (KKT Conditions)
For the solution to be globally optimal, it must satisfy the complementary slackness criteria:
*   $\alpha_i \Big(1 - d_i(w^Tx_i - b) - \xi_i\Big) = 0$
*   $\beta_i \xi_i = 0$

---

## 3. Geometric Visualization Graph

Below is the ASCII geometric view of a Soft Margin boundary separating non-linear data. Points inside or on the wrong side of the margin corridor possess non-zero slack penalties ($\xi_i > 0$).

```text
      x2 ^
         |         (o Class +1)
         |       o       o
   ======|========================== wᵀx - b = +1   (Positive Margin Border)
         |      .   /   o [ξi = 0]
         |     o   /
         | [ξi > 0]/ ◄── Bounded Support Vector (Violates Margin Corridor)
   ──────|────────/───────────────── wᵀx - b = 0    (Optimal Hyperplane Classifier)
         |       /  * [ξi > 0] ◄── Misclassified Negative Point (Severe Violation)
         |      /
         |     /   
   ======|====/===================== wᵀx - b = -1   (Negative Margin Border)
         |   *      *
         |        *     *  (* Class -1)
   ──────┴─────────────────────────► x1

```

---

## 4. Practice Problems with Complete Step-by-Step Calculations

### Problem 1: Evaluating Slack Violations ($\xi_i$)

Given an operational 1D hyperplane classifier configuration with parameters $w = [2]$ and $b = 3$. Determine the explicit error/slack variable value ($\xi_i$) for a data sample positioned at $x_1 = [1]$ labeled with class target $d_1 = +1$.

#### **Step-by-Step Calculation:**

1. **State the standard constraint form requirement:**

$$d_i(w^Tx_i - b) + \xi_i \geq 1 \implies \xi_i \geq 1 - d_i(w^Tx_i - b)$$


2. **Calculate the inner functional boundary value ($w^Tx_1 - b$):**

$$w^Tx_1 - b = (2 \times 1) - 3 = 2 - 3 = -1$$


3. **Multiply by the target label ($d_1 = +1$):**

$$d_1(w^Tx_1 - b) = +1 \times (-1) = -1$$


4. **Solve for the minimum required slack value ($\xi_1$):**

$$\xi_1 = \max\{0, 1 - (-1)\} = \max\{0, 1 + 1\} = 2$$



**Conclusion:** Because the positive point falls deeply into the negative territory, it incurs a slack margin error penalty of **2.0**.

---

### Problem 2: Deducing Bound Constraints on Lagrange Multipliers

Suppose a soft margin SVM optimization model uses a penalty cost constant $C = 5$. During computation, an optimal bounded support vector point yields a slack value of $\xi_k = 1.5$. Calculate the precise values or bounds for the corresponding Lagrange multipliers $\alpha_k$ and $\beta_k$.

#### **Step-by-Step Calculation:**

1. **Apply Bounded Error Complementary Slackness:**
From KKT conditions, we know $\beta_i \xi_i = 0$. Since $\xi_k = 1.5 > 0$, its multiplier must be zero:

$$\beta_k = 0$$


2. **Utilize the Stationary Parameter Balance condition:**
From the derivative condition with respect to $\xi_i$, we have:

$$C - \alpha_i - \beta_i = 0 \implies \alpha_i + \beta_i = C$$


3. **Substitute the known constants ($C = 5$ and $\beta_k = 0$) into the equation:**

$$\alpha_k + 0 = 5 \implies \alpha_k = 5$$



**Conclusion:** For any support vector point actively violating the margin corridor ($\xi_i > 0$), the Lagrange multiplier locks exactly to the upper penalty value limit, yielding **$\alpha_k = 5$** and **$\beta_k = 0$**.


# Concept Name: KKT Case Analysis for Soft Margin SVM (Free vs. Bounded Support Vectors)

This markdown note outlines the comprehensive analysis of Karush-Kuhn-Tucker (KKT) conditions for a **Soft Margin Support Vector Machine (SVM)**, exploring how the values of Lagrange multipliers determine whether data points are correctly classified, lie on the margin bounds, or violate the corridor.

---

## 1. Summary of KKT Optimality Conditions

For a soft margin SVM with a cost tuning penalty factor $c$, the system parameters must meet the following baseline conditions at the optimal point:

*   **Weight Stationarity:** $w = \sum_{i=1}^{m} \alpha_i d_i x_i$ \hfill ---(1)
*   **Bias Stationarity:** $\sum_{i=1}^{m} \alpha_i d_i = 0$ \hfill ---(2)
*   **Slack Multiplier Stationarity:** $c - \alpha_i - \beta_i = 0 \implies \beta_i = c - \alpha_i$ \hfill ---(3)
*   **Primal Feasibility:** $\xi_i - d_i(w^Tx_i - b) \geq 1 \implies d_i(w^Tx_i - b) \geq 1 - \xi_i$ \hfill ---(4)
*   **Complementary Slackness (Margin):** $\alpha_i(1 - \xi_i - d_i(w^Tx_i - b)) = 0$ \hfill ---(5)
*   **Complementary Slackness (Slack):** $\beta_i \xi_i = 0$ \hfill ---(6)
*   **Dual Feasibility:** $\xi_i, \alpha_i, \beta_i \geq 0$ \hfill ---(7)

### Core Derivation: The Error Binding Formula
By substituting the expression for $\beta_i$ from condition (3) ($\beta_i = c - \alpha_i$) directly into condition (6) ($\beta_i\xi_i = 0$), we get the fundamental relationship:
$$(c - \alpha_i)\xi_i = 0 \quad \text{--- (9)}$$

---

## 2. In-Depth Case Analysis & Simple Explanations

Based on formula (9), the status of any data pattern $x_i$ can be completely determined by examining its Lagrange multiplier $\alpha_i$:

### Case 1: $0 < \alpha_i < c$ (Free Support Vectors)
*   **Simple Meaning:** These are the ideal benchmark points that sit perfectly right on the margin lines.
*   **Mathematical Steps:**
    1. Since $\alpha_i < c$, the term $(c - \alpha_i) \neq 0$.
    2. To satisfy condition (9), we must have $\xi_i = 0$. This means there is **zero margin error violation**.
    3. Since $\alpha_i > 0$, condition (5) requires the interior bracket to vanish: $1 - 0 - d_i(w^Tx_i - b) = 0 \implies d_i(w^Tx_i - b) = 1$.
*   **Status:** The pattern is **correctly classified** and lies exactly on one of the outer bounding planes ($w^Tx = b \pm 1$). It is called a **free support vector**.

### Case 2: $\alpha_i = 0$ (Non-Support Vectors / Safe Zone Points)
*   **Simple Meaning:** These points are safely placed deep within their correct class territories and have no influence on where the boundary line is drawn.
*   **Mathematical Steps:**
    1. If $\alpha_i = 0$, then $(c - \alpha_i) = c \neq 0$.
    2. From condition (9), this forces $\xi_i = 0$.
    3. Because $\alpha_i = 0$, condition (5) is satisfied automatically without forcing the margin bracket to zero. Instead, checking condition (4) with $\xi_i = 0$ yields:
       $$d_i(w^Tx_i - b) \geq 1$$
*   **Status:** The point is **correctly classified** and is comfortably far away from the active decision boundaries.

### Case 3: $\alpha_i = c$ (Bounded Support Vectors / Corridor Violators)
*   **Simple Meaning:** These points are "troublemakers" that either cross into the margin dead zone corridor or end up entirely misclassified on the wrong side of the wall.
*   **Mathematical Steps:**
    1. If $\alpha_i = c$, then $(c - \alpha_i) = 0$.
    2. This satisfies condition (9) even if the slack error variable is positive ($\xi_i > 0$).
    3. From condition (3), $\beta_i = c - c = 0$.
    4. Since $\alpha_i = c > 0$, condition (5) dictates: $1 - \xi_i - d_i(w^Tx_i - b) = 0 \implies d_i(w^Tx_i - b) = 1 - \xi_i$.

This case splits into two distinct sub-behaviors based on the severity of the violation:
*   **Sub-Case 3a: $\xi_i \in (0, 1)$**
    *   Since $\xi_i < 1$, the expression $1 - \xi_i > 0$, which means $d_i(w^Tx_i - b) > 0$.
    *   *Status:* The point is **correctly classified** but has penetrated past its margin border, landing inside the **dead zone**.
*   **Sub-Case 3b: $\xi_i \in [1, \infty)$**
    *   Since $\xi_i \geq 1$, the expression $1 - \xi_i \le 0$, which means $d_i(w^Tx_i - b) \le 0$.
    *   *Status:* The point is **not correctly classified**; it has completely crossed the decision boundary line ($w^Tx = b$) into enemy territory.

---

## 3. Visual Layout Map

Below is a text-based ASCII classification map that illustrates how the various points are grouped under their KKT cases.

```text
       Class (-1) Stars [☆]         │       Class (+1) Circles [●]
                                    │
    ☆ 1                             │               ● 7
 (α=0, ξ=0)                         │           (α=c, ξ>1) [Misclassified!]
 [Safe Zone]                        │          
                                    │                 ● 6
 ------------- Bounding Plane ──────│─────────  (α=c, 0<ξ<1) [In Dead Zone]
             \                      │        /
              ☆ 2                   │       /
         (0<α<c, ξ=0)               │      /    ● 4
        [Free Support               │     /  (α=0, ξ=0) [Safe Zone]
           Vector]                  │    /
                                    │   /
 ──────────────────────── Hyperplane Classifier Line (wᵀx = b) ────────────────
                                    │ /
                            ☆ 5     │/
                        (α=c, 0<ξ<1)│          ● 3
                       [In Dead Zone]         (0<α<c, ξ=0) [Free Support Vector]
                                    │
 ------------- Bounding Plane ──────│──────────────────────────────────────────
                                    │
                                    │           ☆ 8
                                    │       (α=c, ξ>1) [Misclassified!]

```

---

## 4. Practice Problems with Step-by-Step Calculations

### Problem 1: Categorizing Point Status via Alpha Values

A soft margin SVM optimization model is trained with an upper bound penalty constant $c = 4.0$. The solver returns the following Lagrange multiplier values for four specific points. Categorize each point's positional profile status using the KKT conditions.

* Point A: $\alpha_A = 0.0$
* Point B: $\alpha_B = 2.5$
* Point C: $\alpha_C = 4.0$ with $\xi_C = 0.4$
* Point D: $\alpha_D = 4.0$ with $\xi_D = 1.2$

#### **Step-by-Step Explanation and Categorization:**

1. **Evaluate Point A:**
* $\alpha_A = 0.0 \implies$ Matches **Case 2** ($\alpha_i = 0$).
* *Calculation:* From condition (9), $(4.0 - 0)\xi_A = 0 \implies \xi_A = 0$.
* *Status:* The point is **correctly classified** and sits safely inside its class territory away from the margin corridor.


2. **Evaluate Point B:**
* $\alpha_B = 2.5 \implies$ Matches **Case 1** ($0 < \alpha_i < 4.0$).
* *Calculation:* From condition (9), $(4.0 - 2.5)\xi_B = 0 \implies 1.5\xi_B = 0 \implies \xi_B = 0$.
* *Functional Value:* $d_B(w^Tx_B - b) = 1$.
* *Status:* It is a **free support vector** resting exactly on the margin boundary line.


3. **Evaluate Point C:**
* $\alpha_C = 4.0 \implies$ Matches **Case 3** ($\alpha_i = c$).
* *Calculation:* Given $\xi_C = 0.4$, we look at its range: $0.4 \in (0, 1)$.
* *Functional Value:* $d_C(w^Tx_C - b) = 1 - 0.4 = 0.6 > 0$.
* *Status:* It is a **bounded support vector** that is correctly classified but violates the margin corridor, landing inside the **dead zone**.


4. **Evaluate Point D:**
* $\alpha_D = 4.0 \implies$ Matches **Case 3** ($\alpha_i = c$).
* *Calculation:* Given $\xi_D = 1.2$, we check its range: $1.2 \in [1, \infty)$.
* *Functional Value:* $d_D(w^Tx_D - b) = 1 - 1.2 = -0.2 < 0$.
* *Status:* It is a **bounded support vector** that is **misclassified**, having crossed over onto the wrong side of the separating line.



---

### Problem 2: Calculating Slack from Functional Margin Values

A point $x_k$ belonging to the positive class ($d_k = +1$) yields a raw classification output score of $w^Tx_k - b = 0.35$. If the model was trained with a margin penalty of $c = 2.0$ and its optimal multiplier was found to be bounded at $\alpha_k = 2.0$, find the value of its slack multiplier $\beta_k$ and calculate its exact structural margin violation error $\xi_k$.

#### **Step-by-Step Calculation Steps:**

1. **Determine the Slack Multiplier ($\beta_k$) using Condition (3):**

$$c - \alpha_k - \beta_k = 0 \implies \beta_k = c - \alpha_k$$



Substitute the known values ($c = 2.0, \alpha_k = 2.0$):

$$\beta_k = 2.0 - 2.0 = 0$$


2. **Calculate the Slack Variable ($\xi_k$) using the Core Case 3 Condition:**
Since $\alpha_k = c = 2.0$, we employ the structural equation derived from condition (5):

$$d_k(w^Tx_k - b) = 1 - \xi_k$$



Substitute the given functional margin score ($0.35$) and label ($d_k = +1$):

$$(+1)(0.35) = 1 - \xi_k \implies 0.35 = 1 - \xi_k$$



Rearrange the equation to isolate $\xi_k$:

$$\xi_k = 1 - 0.35 = 0.65$$


3. **Cross-Verify and Categorize the Point Profile:**
* Is $\xi_k \geq 0$? Yes ($0.65 \geq 0$, which honors condition 7).
* Is the slack condition satisfied? $\beta_k \xi_k = (0)(0.65) = 0$ (Honors condition 6).
* Since $\xi_k = 0.65 \in (0, 1)$, this point matches Sub-case 3a.



**Final Conclusion:** The point's associated slack multiplier values are **$\beta_k = 0$** and **$\xi_k = 0.65$**, indicating it is a correctly classified point that lies inside the margin dead zone corridor.


# Concept Name: Bounding Hyperplanes and Bias Recovery in Soft Margin SVM

This note covers the strategic execution of a **Soft Margin Support Vector Machine (SVM)** Dual formulation, details the explicit mathematical recovery of the decision boundary parameters ($\bar{w}, \bar{b}$) from optimal Lagrange multipliers ($\alpha_i$), and provides a comprehensive numerical classification example with step-by-step constraint modeling.

---

## 1. Dual Framework & Optimization Parameter Recovery

### The Dual Optimization Problem (SP')
When accounting for slack errors $\xi_i$ controlled by a capacity penalty factor $c$, the system transforms into a dual form matching the hard margin framework but introducing a strict upper bound restriction on the Lagrange multipliers:
$$(\text{SP'}) \quad \max_{\alpha} \quad \sum_{i=1}^{m} \alpha_i - \frac{1}{2}\sum_{i=1}^{m}\sum_{j=1}^{m} \alpha_i \alpha_j d_i d_j x_i^T x_j$$
$$\text{subject to } \sum_{i=1}^{m} \alpha_i d_i = 0$$
$$0 \leq \alpha_i \leq c, \quad \forall i = 1, 2, \dots, m$$

### Hyperplane Parameter Recovery Calculations
Once a solver calculates the optimal values for the multipliers ($\alpha$), the weight vector $\bar{w}$ and scalar bias $\bar{b}$ are recovered step-by-step:

1. **Weight Vector ($\bar{w}$):** Derived as a weighted combination of the training points:
   $$\bar{w} = \sum_{i=1}^{m} \alpha_i d_i x_i$$
2. **Bias Scalar ($\bar{b}$):** Found using any **free support vector** (a point where $0 < \alpha_i < c$, forcing its slack error to $\xi_i = 0$). By applying the KKT complementary slackness constraint:
   $$\alpha_i \big[ 1 - \xi_i - d_i(\bar{w}^Tx_i - \bar{b}) \big] = 0$$
   Since $0 < \alpha_i < c$, the expression inside the bracket must equal $0$:
   $$1 - 0 - d_i(\bar{w}^Tx_i - \bar{b}) = 0 \implies d_i(\bar{w}^Tx_i - \bar{b}) = 1$$
   Multiplying both sides by $d_i$ (recalling that $d_i^2 = 1$ because $d_i \in \{-1, +1\}$):
   $$d_i^2(\bar{w}^Tx_i - \bar{b}) = d_i \implies \bar{w}^Tx_i - \bar{b} = d_i$$
   $$\bar{b} = \bar{w}^Tx_i - d_i$$

---

## 2. Quantitative Classification Problem Example

### Problem Scenario
Let's construct a non-linearly separable 2D environment containing two overlapping classes:
*   **Negative Class ($A^-$ / $d_i = -1$):** $\{(2,1), (1,2), (2,3), (3,2), \mathbf{(5,5)}\}$
*   **Positive Class ($A^+$ / $d_i = +1$):** $\{(5,4), (4,5), (5,6), (6,5), \mathbf{(2,2)}\}$
*Notice: Point $(5,5)$ has crossed deep into the positive territory, and point $(2,2)$ has crossed into the negative cluster.*

### Step-by-Step Constraint Formulation
Assuming a capacity penalty parameter value of $c=1$, the objective function targets minimizing structural weights alongside aggregated error variables:
$$\min \quad \frac{1}{2}(w_1^2 + w_2^2) + \sum_{i=1}^{10} \xi_i$$

We expand the primal boundary constraint equation $d_i(w^Tx_i - b) + \xi_i \geq 1 \implies -d_i w^Tx_i + d_i b + \xi_i \geq 1$ step-by-step for each of the 10 data patterns:

#### Negative Class Points ($d_i = -1$):
1.  **Point $(2,1)$:** $-(2w_1 + w_2 - b) + \xi_1 \geq 1 \implies -2w_1 - w_2 + b + \xi_1 \geq 1$
2.  **Point $(1,2)$:** $-(w_1 + 2w_2 - b) + \xi_2 \geq 1 \implies -w_1 - 2w_2 + b + \xi_2 \geq 1$
3.  **Point $(2,3)$:** $-(2w_1 + 3w_2 - b) + \xi_3 \geq 1 \implies -2w_1 - 3w_2 + b + \xi_3 \geq 1$
4.  **Point $(3,2)$:** $-(3w_1 + 2w_2 - b) + \xi_4 \geq 1 \implies -3w_1 - 2w_2 + b + \xi_4 \geq 1$
5.  **Point $(5,5)$:** $-(5w_1 + 5w_2 - b) + \xi_5 \geq 1 \implies -5w_1 - 5w_2 + b + \xi_5 \geq 1 \quad \text{[Overlapping Violator]}$

#### Positive Class Points ($d_i = +1$):
6.  **Point $(5,4)$:** $+(5w_1 + 4w_2 - b) + \xi_6 \geq 1 \implies 5w_1 + 4w_2 - b + \xi_6 \geq 1$
7.  **Point $(4,5)$:** $+(4w_1 + 5w_2 - b) + \xi_7 \geq 1 \implies 4w_1 + 5w_2 - b + \xi_7 \geq 1$
8.  **Point $(5,6)$:** $+(5w_1 + 6w_2 - b) + \xi_8 \geq 1 \implies 5w_1 + 6w_2 - b + \xi_8 \geq 1$
9.  **Point $(6,5)$:** $+(6w_1 + 5w_2 - b) + \xi_9 \geq 1 \implies 6w_1 + 5w_2 - b + \xi_9 \geq 1$
10. **Point $(2,2)$:** $+(2w_1 + 2w_2 - b) + \xi_{10} \geq 1 \implies 2w_1 + 2w_2 - b + \xi_{10} \geq 1 \quad \text{[Overlapping Violator]}$

*Bounds: All variables satisfy $\xi_i \geq 0$, and $w_1, w_2, b$ remain unrestricted in sign.*

### Optimization Results & Analysis
Solving this system yields the following optimal metrics:
$$w_1 = 0.5, \quad w_2 = 0.5, \quad b = 3.5$$

Substituting these back into the classification boundary configurations gives our system of hyperplanes:
*   **Main Separating Hyperplane ($w^Tx = b$):** $0.5x_1 + 0.5x_2 = 3.5 \implies x_1 + x_2 = 7$
*   **Lower Bounding Plane ($w^Tx = b - 1$):** $0.5x_1 + 0.5x_2 = 2.5 \implies x_1 + x_2 = 5$
*   **Upper Bounding Plane ($w^Tx = b + 1$):** $0.5x_1 + 0.5x_2 = 4.5 \implies x_1 + x_2 = 9$

---

## 3. Comprehensive Sample Nature Log Table

Evaluating the final optimal variables reveals the physical distribution and nature of each sample point in relation to the boundary system:

| Pattern | Slack Value ($\xi_i$) | Multiplier ($\alpha_i$) | Nature / Structural Location |
| :---: | :---: | :---: | :--- |
| **1** | $\xi_1 = 0$ | $\alpha_1 = 0$ | Correctly classified (Safe Zone point) |
| **2** | $\xi_2 = 0$ | $0 < \alpha_2 < c$ | Free support vector (Sits exactly on lower plane $x_1+x_2=5$) |
| **3** | $\xi_3 > 1$ | $\alpha_3 = c$ | Bounded support vector (Not correctly classified / Misclassified) |
| **4** | $0 < \xi_4 < 1$ | $\alpha_4 = c$ | Bounded support vector (Correctly classified but inside Dead Zone corridor) |
| **5** | $0 < \xi_5 < 1$ | $\alpha_5 = c$ | Bounded support vector (Correctly classified but inside Dead Zone corridor) |
| **6** | $\xi_6 = 0$ | $0 < \alpha_6 < c$ | Free support vector (Sits exactly on upper plane $x_1+x_2=9$) |
| **7** | $\xi_7 = 0$ | $\alpha_7 = 0$ | Correctly classified (Safe Zone point) |
| **8** | $\xi_8 > 1$ | $\alpha_8 = c$ | Bounded support vector (Not correctly classified / Misclassified) |

---

## 4. Text-Based Visual Space Map

The graph below visualizes the data space layout. Notice how the two outlier points create non-zero slack penalties inside the margin corridor.

```text
  x2 ^
     |
 6.0 +           o (5,6)
     |         /   \
 5.0 +       o       # (5,5) [Misclassified # Outlier! ξ > 1]
     |     /   \   /
 4.0 +   /       o (5,4)      ────── Upper Bounding Plane (x1 + x2 = 9)
     |  /      /
 3.0 + /     # (2,3)          ────── Main Separating Hyperplane (x1 + x2 = 7)
     |/    /   \
 2.0 +   o       # (3,2)      ────── Lower Bounding Plane (x1 + x2 = 5)
     | [Misclassified o]
 1.0 +       # (2,1)
     |
 0.0 +---+---+---+---+---+---+───► x1
    0.0 1.0 2.0 3.0 4.0 5.0 6.0

```

---

## 5. Practice Problem with Step-by-Step Calculations

### Problem

Using the final optimal parameters ($w_1 = 0.5, w_2 = 0.5, b = 3.5$), calculate the explicit margin error value ($\xi_5$) and verify the specific categorization profile for the negative outlier point $x_5 = (5,5)^T$ ($d_5 = -1$).

#### **Step-by-Step Calculation:**

1. **State the structural constraint inequality rule:**

$$d_5(w_1x_{51} + w_2x_{52} - b) + \xi_5 \geq 1 \implies \xi_5 \geq 1 - d_5(w_1x_{51} + w_2x_{52} - b)$$


2. **Compute the inner product score for $x_5$:**

$$w^Tx_5 = (0.5 \times 5) + (0.5 \times 5) = 2.5 + 2.5 = 5.0$$


3. **Incorporate the scalar separation bias ($b = 3.5$):**

$$w^Tx_5 - b = 5.0 - 3.5 = 1.5$$


4. **Multiply by the target label value ($d_5 = -1$):**

$$d_5(w^Tx_5 - b) = (-1) \times (1.5) = -1.5$$


5. **Solve for the necessary slack variable parameter value ($\xi_5$):**

$$\xi_5 = 1 - (-1.5) = 1 + 1.5 = 2.5$$


6. **Profile Status Verification:**
* Since $\xi_5 = 2.5$, it perfectly honors the dual condition $\xi_5 > 0$.
* Because $\xi_5 = 2.5 \geq 1$, it matches the criteria for a severe violation.
* Checking its classification sign confirms that $d_5(w^Tx_5 - b) = -1.5 < 0$.



**Conclusion:** The point has an explicit margin error value of **$\xi_5 = 2.5$**. Because its slack penalty is greater than or equal to $1$, it is mathematically classified as a **misclassified bounded support vector**, matching its designation in the log table.

