# Optimality Conditions for Constrained Optimization (KKT Conditions)

## 1. Concept Name: Karush-Kuhn-Tucker (KKT) Conditions

### Simple Meaning
When trying to minimize a function that has limitations or boundaries (constraints), we can no longer simply look for where the gradient is zero ($\nabla f(x) = 0$). Instead, we use the **KKT Conditions**. 

Think of KKT conditions as a balancing act: they look for points where the slope pushing you to a lower value of the objective function is perfectly canceled out by the forces pushing back from the constraint boundaries. 

The standard formulation of the problem is:
$$\begin{array}{rl} \text{Minimize} & f(x) \\ \text{subject to (s/t)} & g_i(x) \le 0, \quad i = 1, 2, \dots, m \end{array}$$
where $f$ and $g_i$ are continuously differentiable functions mapping $\mathbb{R}^n \rightarrow \mathbb{R}$.

---

## 2. The Necessary and Sufficient Conditions

### A. First-Order Necessary Conditions
If $\bar{x}$ is a local minimum point of the problem and a basic constraint qualification holds, then there **must** exist a set of scaling multipliers $\bar{\lambda}_i$ (called **KKT multipliers**) that satisfy the following four conditions:

1.  **Stationarity:** $\nabla f(\bar{x}) + \sum_{i=1}^{m} \bar{\lambda}_i \nabla g_i(\bar{x}) = 0$
2.  **Primal Feasibility:** $g_i(\bar{x}) \le 0, \quad i = 1, 2, \dots, m$
3.  **Complementary Slackness:** $\bar{\lambda}_i g_i(\bar{x}) = 0, \quad i = 1, 2, \dots, m$
4.  **Dual Feasibility:** $\bar{\lambda}_i \ge 0 \quad \forall i$

### B. Sufficient Conditions
If you find a candidate point $\bar{x}$ and a set of multipliers $(\bar{\lambda}_1, \bar{\lambda}_2, \dots, \bar{\lambda}_m)$ that pass all four KKT conditions **AND** both $f$ and all $g_i$ are **convex functions**, then $\bar{x}$ is guaranteed to be an absolute **global minimum point**.

---

## 3. Solved Problems with Step-by-Step Calculations

### 📝 Problem 1: Verifying Optimality via KKT Conditions
Consider the following optimization problem:
$$\text{Minimize } f(x, y) = x^2 + y^2$$
$$\text{subject to } g_1(x, y) = 1 - x - y \le 0$$

Test whether the candidate point $(\bar{x}, \bar{y}) = (0.5, 0.5)$ satisfies the KKT conditions, and find the corresponding multiplier $\bar{\lambda}_1$.

#### **Step 1: Compute Gradients**
*   Objective gradient:
    $$\nabla f(x, y) = \begin{pmatrix} 2x \\ 2y \end{pmatrix} \implies \nabla f(0.5, 0.5) = \begin{pmatrix} 1 \\ 1 \end{pmatrix}$$
*   Constraint gradient:
    $$\nabla g_1(x, y) = \begin{pmatrix} -1 \\ -1 \end{pmatrix}$$

#### **Step 2: Test Feasibility (Condition 2)**
Check if the point satisfies the boundary constraint:
$$g_1(0.5, 0.5) = 1 - 0.5 - 0.5 = 0 \le 0 \quad (\text{Feasible! } \checkmark)$$
*(Since it equals exactly 0, the constraint is **active**).*

#### **Step 3: Solve the Stationarity Equation for $\bar{\lambda}_1$ (Condition 1)**
$$\nabla f(\bar{x}) + \bar{\lambda}_1 \nabla g_1(\bar{x}) = 0$$
$$\begin{pmatrix} 1 \\ 1 \end{pmatrix} + \bar{\lambda}_1 \begin{pmatrix} -1 \\ -1 \end{pmatrix} = \begin{pmatrix} 0 \\ 0 \end{pmatrix}$$
Looking at either row:
$$1 - \bar{\lambda}_1 = 0 \implies \bar{\lambda}_1 = 1$$

#### **Step 4: Verify Dual Feasibility & Complementary Slackness (Conditions 3 & 4)**
*   **Dual Feasibility:** $\bar{\lambda}_1 = 1 \ge 0 \quad (\text{True! } \checkmark)$
*   **Complementary Slackness:** $\bar{\lambda}_1 g_1(\bar{x}) = 1 \times 0 = 0 \quad (\text{True! } \checkmark)$

#### **Step 5: Check Sufficiency**
*   $\nabla^2 f = \begin{pmatrix} 2 & 0 \\ 0 & 2 \end{pmatrix}$ (Positive definite $\implies$ $f$ is convex).
*   $g_1$ is linear ($\implies$ $g_1$ is convex).
*   **Conclusion:** The point $(0.5, 0.5)$ satisfies all KKT conditions and is a **global minimum**.

---

### 📝 Problem 2: Handling an Inactive Constraint Case
Consider the problem:
$$\text{Minimize } f(x) = (x - 3)^2$$
$$\text{subject to } g_1(x) = x - 5 \le 0$$
Test if the point $\bar{x} = 3$ is an optimal solution.

#### **Step 1: Verify Primal Feasibility**
$$g_1(3) = 3 - 5 = -2 \le 0 \quad (\text{Feasible! } \checkmark)$$
*(Since $g_1(3) < 0$, this constraint is **inactive**).*

#### **Step 2: Apply Complementary Slackness**
Because $g_1(3) \neq 0$, condition 3 dictates that the multiplier must be zero:
$$\bar{\lambda}_1 g_1(3) = 0 \implies \bar{\lambda}_1 \times (-2) = 0 \implies \bar{\lambda}_1 = 0$$

#### **Step 3: Evaluate Stationarity**
Calculate derivatives at $\bar{x} = 3$:
$$\nabla f(x) = 2(x - 3) \implies \nabla f(3) = 2(3 - 3) = 0$$
$$\nabla g_1(x) = 1$$
Substitute into the KKT stationarity vector formula:
$$\nabla f(3) + \bar{\lambda}_1 \nabla g_1(3) = 0 + (0 \times 1) = 0 \quad (\text{True! } \checkmark)$$

#### **Conclusion:**
Since $\bar{\lambda}_1 = 0 \ge 0$ (Dual Feasible) and the equations balance out, the point $\bar{x} = 3$ satisfies the KKT conditions. Because the objective function is convex, this point is the **global minimum**.

---

## 4. Visualizing the Geometric Meaning of KKT

The ASCII vector graph below demonstrates how the forces balance at an active boundary constraint during optimization:

```text
                        Objective Function Topography Curls
                              (Lower values inward)
                                    \   │   /
                                     \  │  /
                                      ▼ │ ▼
                                     * * * *
                                   *    │    *
       Active Constraint          *     │     *
       Boundary Line             *      ▼      *
    ────────────────────────────●─────────────────────────────
       Feasible Region Below    │ \    x̄       /
                                │  \          /
                                │   \        /
                                │    ▼
                          ∇f(x̄) │   -∇f(x̄) = λ₁∇g₁(x̄)
  The objective slope vector ───┘   (Opposing constraint force vector
  points outwards, exactly           scaled by multiplier λ₁ ≥ 0)
  balanced by the boundary.
```


# Convex Optimization: KKT Sufficiency Proof & Convexity Necessity Counterexamples

## 1. Concept Name: KKT Conditions Sufficiency Proof & The Necessity of Convexity

### Simple Meaning
The **Karush-Kuhn-Tucker (KKT) Conditions** establish a mathematical system to find candidate minimum valleys in constrained optimization problems. However, passing these conditions on paper does not automatically guarantee a global minimum unless the problem is geometrically **convex**.

This note acts as a two-part masterclass:
1. **The Proof of Sufficiency:** It step-by-step proves how KKT points translate to a true global minimum under explicit convexity rules.
2. **The Counterexample Breakdown:** It calculates a full counterexample illustrating how a point can satisfy all KKT equations but fail to be a minimum when the underlying functions bend non-convexly.

---

## 2. Mathematical Proof: Sufficiency of KKT under Convexity

### Goal
Given a point $\bar{x}$ that satisfies the KKT conditions, prove that $f(\bar{x}) \le f(x)$ for all feasible points $x$, assuming $f$ and $g_i$ are continuously differentiable **convex** functions.

### Step-by-Step Mathematical Derivation

#### **Step 1: Setup from KKT Stationarity (Condition 1)**
The first KKT condition states that the gradient weights must sum to zero:
$$\nabla f(\bar{x}) + \sum_{i=1}^{m} \bar{\lambda}_i \nabla g_i(\bar{x}) = 0 \quad \text{--- (1)}$$

Multiply both sides by the directional displacement row vector $(x - \bar{x})^T$:
$$\left(\nabla f(\bar{x}) + \sum_{i=1}^{m} \bar{\lambda}_i \nabla g_i(\bar{x})\right)^T (x - \bar{x}) = 0$$
$$\implies (\nabla f(\bar{x}))^T (x - \bar{x}) + \left(\sum_{i=1}^{m} \bar{\lambda}_i \nabla g_i(\bar{x})\right)^T (x - \bar{x}) = 0 \quad \text{--- (1b)}$$

#### **Step 2: Leverage the First-Order Condition for Convex Functions**
Because $f$ and $g_i$ are convex functions, their curves lie entirely above their first-order tangent planes:
$$f(x) - f(\bar{x}) \ge (\nabla f(\bar{x}))^T (x - \bar{x}) \quad \text{--- (2)}$$
$$g_i(x) - g_i(\bar{x}) \ge (\nabla g_i(\bar{x}))^T (x - \bar{x}) \quad \forall i$$

Since KKT multipliers are non-negative ($\bar{\lambda}_i \ge 0$), multiplying the $g_i$ equations preserves the inequality direction. Summing across all $m$ constraints yields:
$$\sum_{i=1}^{m} \bar{\lambda}_i g_i(x) - \sum_{i=1}^{m} \bar{\lambda}_i g_i(\bar{x}) \ge \left(\sum_{i=1}^{m} \bar{\lambda}_i \nabla g_i(\bar{x})\right)^T (x - \bar{x}) \quad \text{--- (3)}$$

#### **Step 3: Combine and Reduce via KKT Conditions**
Add inequality (2) and inequality (3) together:
$$f(x) - f(\bar{x}) + \sum_{i=1}^{m} \bar{\lambda}_i g_i(x) - \sum_{i=1}^{m} \bar{\lambda}_i g_i(\bar{x}) \ge \underbrace{(\nabla f(\bar{x}))^T (x - \bar{x}) + \left(\sum_{i=1}^{m} \bar{\lambda}_i \nabla g_i(\bar{x})\right)^T (x - \bar{x})}_{\text{From Equation (1b), this equals } 0}$$
$$\implies f(x) - f(\bar{x}) + \sum_{i=1}^{m} \bar{\lambda}_i g_i(x) - \sum_{i=1}^{m} \bar{\lambda}_i g_i(\bar{x}) \ge 0$$

#### **Step 4: Isolate the Objective Function Term**
By KKT Complementary Slackness, the multiplier product at $\bar{x}$ is exactly zero: $\sum_{i=1}^{m} \bar{\lambda}_i g_i(\bar{x}) = 0$. This reduces our expression to:
$$f(x) - f(\bar{x}) + \sum_{i=1}^{m} \bar{\lambda}_i g_i(x) \ge 0 \implies f(x) - f(\bar{x}) \ge -\sum_{i=1}^{m} \bar{\lambda}_i g_i(x)$$

#### **Step 5: Conclude the Global Property**
Evaluate the remaining terms for any valid feasible point $x$:
*   $g_i(x) \le 0$ (Feasibility requirement)
*   $\bar{\lambda}_i \ge 0$ (Dual feasibility)
*   Therefore, their product must be non-positive: $\sum_{i=1}^{m} \bar{\lambda}_i g_i(x) \le 0$.
*   Negating a non-positive value makes it non-negative: $-\sum_{i=1}^{m} \bar{\lambda}_i g_i(x) \ge 0$.

$$f(x) - f(\bar{x}) \ge -\sum_{i=1}^{m} \bar{\lambda}_i g_i(x) \ge 0 \implies f(x) \ge f(\bar{x})$$

**Proof Complete!** Under explicit convexity conditions, any point satisfying the KKT parameters is guaranteed to be a global minimum.

---

## 3. The Necessity of Convexity (Counterexample Dissection)

> ⚠️ **Remark:** Without strict convexity assumptions on $f$ and $g_i$, the KKT conditions are **not** sufficient for a point $\bar{x}$ to be a local or global minimum.

### 📝 Counterexample Problem Analysis
Consider the non-convex optimization problem from the slide:
$$\text{Minimize } f(x_1, x_2) = -x_2$$
$$\text{subject to: } \begin{cases} g_1(x_1, x_2) = x_1^2 + x_2^2 - 4 \le 0 \\ g_2(x_1, x_2) = -x_1^2 + x_2 \le 0 \end{cases}$$

Let's rigorously calculate if the origin point **$(0,0)$** satisfies all KKT conditions, and if it functions as a minimum.

---

### 🔎 Step-by-Step KKT Verification Calculations

#### **Step 1: Compute All Gradient Vectors**
*   $\nabla f(x_1, x_2) = \left( \frac{\partial f}{\partial x_1}, \frac{\partial f}{\partial x_2} \right) = (0, -1)$
*   $\nabla g_1(x_1, x_2) = (2x_1, 2x_2)$
*   $\nabla g_2(x_1, x_2) = (-2x_1, 1)$

#### **Step 2: Test Primal Feasibility at $(0,0)$**
*   $g_1(0, 0) = 0^2 + 0^2 - 4 = -4 \le 0 \quad (\text{Feasible! } \checkmark)$
*   $g_2(0, 0) = -0^2 + 0 = 0 \le 0 \quad (\text{Feasible! } \checkmark)$

*Analysis:* Since $g_1(0,0) = -4 < 0$, constraint 1 is **inactive**. Since $g_2(0,0) = 0$, constraint 2 is **active**.

#### **Step 3: Apply Complementary Slackness**
Because constraint $g_1$ is inactive at the origin, its multiplier must equal zero:
$$\lambda_1 g_1(0,0) = 0 \implies \lambda_1 \times (-4) = 0 \implies \lambda_1 = 0$$

#### **Step 4: Solve the Stationarity Vector Equation**
$$\nabla f(0,0) + \lambda_1 \nabla g_1(0,0) + \lambda_2 \nabla g_2(0,0) = (0,0)$$
$$\begin{pmatrix} 0 \\ -1 \end{pmatrix} + \lambda_1 \begin{pmatrix} 2(0) \\ 2(0) \end{pmatrix} + \lambda_2 \begin{pmatrix} -2(0) \\ 1 \end{pmatrix} = \begin{pmatrix} 0 \\ 0 \end{pmatrix}$$
$$\begin{pmatrix} 0 \\ -1 \end{pmatrix} + \lambda_1 \begin{pmatrix} 0 \\ 0 \end{pmatrix} + \lambda_2 \begin{pmatrix} 0 \\ 1 \end{pmatrix} = \begin{pmatrix} 0 \\ 0 \end{pmatrix}$$

Let's separate this vector statement into independent rows:
1.  **Row 1:** $0 + 0\lambda_1 - 0\lambda_2 = 0 \implies 0 = 0 \quad (\text{Valid } \checkmark)$
2.  **Row 2:** $-1 + 0\lambda_1 + 1\lambda_2 = 0 \implies -1 + \lambda_2 = 0 \implies \lambda_2 = 1$

#### **Step 5: Evaluate Dual Feasibility**
Check the values of the calculated multipliers:
*   $\lambda_1 = 0 \ge 0 \quad (\text{Valid } \checkmark)$
*   $\lambda_2 = 1 \ge 0 \quad (\text{Valid } \checkmark)$

#### **Conclusion:**
The origin point $(0,0)$ with multipliers $(\lambda_1, \lambda_2) = (0, 1)$ **perfectly satisfies every KKT condition**. 

However, looking closely at the domain: if you take a tiny step forward along the positive y-axis (e.g., the point $(0, 1)$), let's evaluate its feasibility and performance:
*   $g_1(0, 1) = 0^2 + 1^2 - 4 = -3 \le 0 \quad (\text{Feasible!})$
*   $g_2(0, 1) = -0^2 + 1 = 1 \not\le 0 \quad (\text{Infeasible, cannot move directly up})$.
*   Instead, let's step along the parabola boundary: consider the point $(1, 1)$.
    *   $g_1(1, 1) = 1^2 + 1^2 - 4 = -2 \le 0 \quad (\text{Feasible!})$
    *   $g_2(1, 1) = -1^2 + 1 = 0 \le 0 \quad (\text{Feasible!})$
    *   Objective value: $f(1, 1) = -1$.

Since $f(1, 1) = -1 < f(0,0) = 0$, the origin point is **not** a local minimum, despite cleanly passing the KKT test! The constraint function $g_2 = -x_1^2 + x_2$ has an indefinite Hessian ($\nabla^2 g_2 = \left(\begin{smallmatrix}-2&0\\0&0\end{smallmatrix}\right)$), meaning it is non-convex and warps the space to invalidate standard KKT sufficiency.

---

## 4. Textual Optimization Landscape Visualization

This graph details why non-convex structures prevent KKT conditions from acting as a global guarantee:

```text
       ▲ f(x)
       │
       │     *   *              * * *               ◄── Non-Convex Objective Space
       │    *     *           *       *                 (Bends down irregularly)
       │   *       *         *         *
───────┼──*─────────*───────*───────────*────────► Domain Space (x)
       │ *           *     *             *
       │              *   *               *
       │               ▼                    ▼
                KKT Point (0,0)      True Deep Valley Minimum
               Slope is flat (=0),    (Lower than candidate point!)
               but it's a trap peak.
```

# Application of KKT Conditions to Convex Constrained Optimization Problems

## 1. Concept Name: Verifying Global Optimality using Karush-Kuhn-Tucker (KKT) Conditions

### Simple Meaning
For constrained optimization problems, the **KKT conditions** serve as a first-order necessary test to find optimal candidate points. However, if the objective function $f(x)$ is strictly **convex** ( bowl-shaped curving upwards) and the feasible region is a **convex set** (enclosed by convex constraint boundaries), the KKT conditions become **sufficient**. This means any point satisfying the KKT system is mathematically guaranteed to be the absolute **unique global optimal solution**.

---

## 2. Step-by-Step Verification Procedure
To prove a given candidate point $\bar{x} = (\bar{x}_1, \bar{y}_2)^T$ is the unique global minimum:
*   **Step 1:** Formulate all constraints into the standard inequality format: $g_i(x) \le 0$.
*   **Step 2:** Check the convexity of the objective function $f(x)$ and constraint functions $g_i(x)$ using Hessian matrices ($\nabla^2 f \succeq 0$).
*   **Step 3:** Evaluate which constraints are **active** ($g_i(\bar{x}) = 0$) and **inactive** ($g_i(\bar{x}) < 0$) at the given point. Set $\lambda_i = 0$ for all inactive constraints (Complementary Slackness).
*   **Step 4:** Set up the KKT stationarity vector equation: $\nabla f(\bar{x}) + \sum \lambda_i \nabla g_i(\bar{x}) = 0$.
*   **Step 5:** Solve for the remaining unknown Lagrange multipliers ($\lambda_i$) and confirm they are non-negative ($\lambda_i \ge 0$).

---

## 3. Detailed Step-by-Step Problem Calculations

### 📝 Problem 1 (From Slide)
Show that $\bar{x} = (3/2, 9/4)^T$ is the unique global optimal solution for the following problem:
$$\begin{array}{rl} \text{Minimize} & f(x) = \left(x_1 - \frac{9}{4}\right)^2 + (x_2 - 2)^2 \\ \text{subject to} & x_1^2 \le x_2 \\ & x_1 + x_2 \le 6 \\ & x_1, x_2 \ge 0 \end{array}$$

#### **Step 1: Standardize the Constraints**
$$g_1(x) = x_1^2 - x_2 \le 0$$
$$g_2(x) = x_1 + x_2 - 6 \le 0$$
$$g_3(x) = -x_1 \le 0$$
$$g_4(x) = -x_2 \le 0$$

#### **Step 2: Verify Global Convexity**
*   **Objective Function Curvature:**
    $$\nabla^2 f(x) = \begin{pmatrix} 2 & 0 \\ 0 & 2 \end{pmatrix} \implies \text{Positive Definite } (\succ 0) \implies f \text{ is strictly convex.}$$
*   **Constraint 1 Curvature:**
    $$\nabla^2 g_1(x) = \begin{pmatrix} 2 & 0 \\ 0 & 0 \end{pmatrix} \implies \text{Positive Semi-Definite } (\succeq 0) \implies g_1 \text{ is convex.}$$
*   Since $g_2, g_3, g_4$ are purely linear, they are globally convex. The sufficiency theorem holds!

#### **Step 3: Analyze Constraint Activity at $\bar{x} = (3/2, 9/4)^T$**
*   $g_1(3/2, 9/4) = (3/2)^2 - 9/4 = 9/4 - 9/4 = 0 \implies \mathbf{\text{Active!}}$
*   $g_2(3/2, 9/4) = 3/2 + 9/4 - 6 = 15/4 - 6 = -9/4 < 0 \implies \text{Inactive} \implies \mathbf{\lambda_2 = 0}$
*   $\bar{x}_1 = 3/2 > 0 \implies \text{Inactive} \implies \mathbf{\lambda_3 = 0}$
*   $\bar{x}_2 = 9/4 > 0 \implies \text{Inactive} \implies \mathbf{\lambda_4 = 0}$

#### **Step 4: Solve the Stationarity Vector Equation**
$$\nabla f(\bar{x}) + \lambda_1 \nabla g_1(\bar{x}) + \lambda_2 \nabla g_2(\bar{x}) + \lambda_3 \nabla g_3(\bar{x}) + \lambda_4 \nabla g_4(\bar{x}) = \begin{pmatrix} 0 \\ 0 \end{pmatrix}$$

Substitute the gradient formulas at our coordinate point:
$$\nabla f(\bar{x}) = \begin{pmatrix} 2(x_1 - 9/4) \\ 2(x_2 - 2) \end{pmatrix} = \begin{pmatrix} 2(3/2 - 9/4) \\ 2(9/4 - 2) \end{pmatrix} = \begin{pmatrix} -3/2 \\ 1/2 \end{pmatrix}$$
$$\nabla g_1(\bar{x}) = \begin{pmatrix} 2x_1 \\ -1 \end{pmatrix} = \begin{pmatrix} 2(3/2) \\ -1 \end{pmatrix} = \begin{pmatrix} 3 \\ -1 \end{pmatrix}$$

Set up the linear row equations (remembering $\lambda_2 = \lambda_3 = \lambda_4 = 0$):
1.  **Row 1 Equation:** $-\frac{3}{2} + 3\lambda_1 = 0 \implies 3\lambda_1 = \frac{3}{2} \implies \mathbf{\lambda_1 = \frac{1}{2}}$
2.  **Row 2 Verification:** $\frac{1}{2} - \lambda_1 = 0 \implies \frac{1}{2} - \frac{1}{2} = 0 \quad (\text{Perfect Match! } \checkmark)$

#### **Conclusion:**
Since $\lambda_1 = 1/2 \ge 0$, all KKT conditions are perfectly satisfied. Combined with the absolute convexity of the system components, **$\bar{x} = (3/2, 9/4)^T$ is proven to be the unique global optimal minimum solution**.

---

### 📝 Problem 2 (Practice Problem From Slide)
Solve the following constrained optimization problem:
$$\begin{array}{rl} \text{Minimize} & f(x) = x_1^2 + x_2^2 - 6x_1 - 4x_2 + 13 \\ \text{subject to} & x_1^2 + x_2^2 \le 52 \\ & x_1, x_2 \ge 0 \end{array}$$

#### **Step 1: Check Global Unconstrained Minimum First**
Find the flat stationarity point of $f(x)$ assuming constraints are inactive:
$$\frac{\partial f}{\partial x_1} = 2x_1 - 6 = 0 \implies x_1 = 3$$
$$\frac{\partial f}{\partial x_2} = 2x_2 - 4 = 0 \implies x_2 = 2$$
Candidate point: $\bar{x} = (3, 2)^T$.

#### **Step 2: Verify Constraint Bounds Feasibility**
Test our unconstrained candidate point inside the main inequality constraint:
$$g_1(3, 2) = 3^2 + 2^2 - 52 = 9 + 4 - 52 = -39 \le 0 \quad (\text{Feasible! } \checkmark)$$

#### **Conclusion:**
Because the absolute global unconstrained minimum point $(3, 2)^T$ sits cleanly inside the permitted feasible boundaries, the boundary constraint remains completely inactive ($\lambda_1 = 0$). By checking the Hessian matrix $\nabla^2 f = \left(\begin{smallmatrix}2&0\\0&2\end{smallmatrix}\right) \succ 0$, the function is strictly convex, confirming that **$\bar{x} = (3, 2)^T$ is the unique global minimum solution**.

---

## 4. Visualizing the Convex Feasible Boundaries Landscape

Below is an ASCII geometric layout showing the boundaries of Problem 1. The optimal solution occurs exactly at the boundary curve point where the paraboloid objective contour lines rest tangent against the parabolic constraint fence:

```text
       x₂ ▲
          │          \ Line: x₁ + x₂ = 6
        6 ┼           \
          │            \     Parabola Boundary: x₂ ≥ x₁²
          │             \          *
          │   Feasible   \        *
        2 ┼───Region──────●──────* ◄── Tangent Optimal Point (3/2, 9/4)
          │▒▒▒▒▒▒▒▒▒▒▒▒▒▒/ ▒*   *
          │▒▒▒▒▒▒▒▒▒▒▒▒▒/ ▒▒▒* *
   ───────┴────────────┼──────●────────────────► x₁
          0            2      3