# Concept Name: Duality Theory in Mathematical Optimization

Duality is a foundational mathematical principle that establishes a formal connection between two distinct optimization problems: the **Primal Problem** and the **Dual Problem**. 

---

## 1. Core Mathematical Concept & Principles

* **The Duality Principle**: Every constrained optimization problem (the Primal) can be systematically converted into a mirror problem (the Dual). If the Primal aims to minimize an objective function, the Dual aims to maximize a related function (and vice versa).
* **Optimal Value Theorem**: Under appropriate conditions, if an optimal solution exists for either problem, an optimal solution exists for both, and their final optimal objective values are mathematically equal.
* **Application**: Duality theory provides powerful structural insights used to design efficient numerical algorithms for complex operations research, economics, and management science scenarios.

---

## 2. Mathematical Formulation: Primal to Dual Conversion

### The Primal Problem (P)
The general standard form of a constrained optimization minimization problem is written as:
$$(P) \quad \min_{x} f(x)$$
$$\text{subject to } g_i(x) \le 0, \quad i = 1, 2, \dots, m$$
Where $f: \mathbb{R}^n \longrightarrow \mathbb{R}$ represents the objective cost function, and $g_i: \mathbb{R}^n \longrightarrow \mathbb{R}$ represents the $m$ inequality constraints.

### The Lagrangian Function
To incorporate the structural constraints into the objective function, we form the **Lagrangian function** $L(x, \lambda)$ by multiplying each constraint vector by a non-negative weight called a **Lagrangian Multiplier** ($\lambda_i$):
$$L(x, \lambda) = f(x) + \sum_{i=1}^m \lambda_i g_i(x) = f(x) + \lambda^T g(x)$$
Where $x \in \mathbb{R}^n$, $\lambda \in \mathbb{R}^m$, and $g(x) = (g_1(x), g_2(x), \dots, g_m(x))^T$.

### The Dual Problem (D)
The dual configuration maximizes the Lagrangian function under the requirement that its gradient with respect to $x$ equals zero:
$$(D) \quad \max_{x, \lambda} L(x, \lambda)$$
$$\text{subject to } \nabla_x L(x, \lambda) = 0$$
$$\lambda \geq 0$$

Expanding $L(x, \lambda)$ and its gradient yields the complete mathematical rewritten formulation:
$$(D) \quad \max_{x, \lambda} \left[ f(x) + \sum_{i=1}^m \lambda_i g_i(x) \right]$$
$$\text{subject to } \nabla f(x) + \sum_{i=1}^m \lambda_i \nabla g_i(x) = 0$$
$$\lambda_i \geq 0, \quad i = 1, 2, \dots, m$$

---

## 3. Geometric Optimization Intuition

The Dual problem bounds the Primal problem from below. The structural optimization point occurs where the maximum lower bound meets the minimum upper constraint limit.

```text
 Objective Value
       ▲
       │       \       /   ◄--- Primal Minimization Space f(x)
       │        \     /
       │─────────\.  /──────── Optimal Solution Target: Min P = Max D
       │          ·
       │        /───\      ◄--- Dual Maximization Space L(x, λ)
       │       /     \
       └────────────────────────► Variable Domain Space (x)

```

---

## 4. Step-by-Step Practice Problems with Complete Calculations

### Problem 1: Explicit Form Formulation

**Scenario:** Given the following non-linear constrained minimization problem:


$$\min f(x_1, x_2) = x_1^2 + x_2^2$$

$$\text{subject to } 2 - x_1 - x_2 \le 0$$

Formulate the explicit Lagrangian function and derive the exact constraints governing the Dual problem.

#### **Step-by-Step Calculation:**

1. **Convert Constraints to Standard $g_i(x) \le 0$ Form:**

$$g_1(x_1, x_2) = 2 - x_1 - x_2 \le 0$$


2. **Construct the Lagrangian Function $L(x, \lambda)$:**

$$L(x_1, x_2, \lambda_1) = f(x_1, x_2) + \lambda_1 g_1(x_1, x_2)$$


$$L(x_1, x_2, \lambda_1) = x_1^2 + x_2^2 + \lambda_1(2 - x_1 - x_2)$$


3. **Compute the Gradient Components with respect to $x$ ($\nabla_x L = 0$):**
* Partial with respect to $x_1$:

$$\frac{\partial L}{\partial x_1} = 2x_1 - \lambda_1 = 0 \implies 2x_1 = \lambda_1$$


* Partial with respect to $x_2$:

$$\frac{\partial L}{\partial x_2} = 2x_2 - \lambda_1 = 0 \implies 2x_2 = \lambda_1$$




4. **State the Complete Dual Problem Setup:**

$$\max_{x_1, x_2, \lambda_1} \left[ x_1^2 + x_2^2 + \lambda_1(2 - x_1 - x_2) \right]$$


$$\text{subject to } 2x_1 - \lambda_1 = 0$$


$$2x_2 - \lambda_1 = 0$$


$$\lambda_1 \geq 0$$



---

### Problem 2: Finding the Analytic Solution via the Dual

Using the expressions derived in Problem 1, calculate the explicit analytical optimal value for the primal variable $x^*$, dual multiplier $\lambda^*$, and verify that the minimum primal equals the maximum dual value.

#### **Step-by-Step Calculation:**

1. **Express Primal Variables in Terms of Dual Variable $\lambda_1$:**
From the gradient conditions:

$$x_1 = \frac{\lambda_1}{2}$$


$$x_2 = \frac{\lambda_1}{2}$$


2. **Substitute $x_1$ and $x_2$ back into the Lagrangian function to eliminate $x$:**

$$L(\lambda_1) = \left(\frac{\lambda_1}{2}\right)^2 + \left(\frac{\lambda_1}{2}\right)^2 + \lambda_1\left(2 - \frac{\lambda_1}{2} - \frac{\lambda_1}{2}\right)$$


$$L(\lambda_1) = \frac{\lambda_1^2}{4} + \frac{\lambda_1^2}{4} + \lambda_1(2 - \lambda_1)$$


$$L(\lambda_1) = \frac{\lambda_1^2}{2} + 2\lambda_1 - \lambda_1^2$$


$$L(\lambda_1) = 2\lambda_1 - \frac{\lambda_1^2}{2}$$


3. **Maximize the Dual Function with respect to $\lambda_1$:**
Take the derivative and set to zero:

$$\frac{d L(\lambda_1)}{d \lambda_1} = 2 - \lambda_1 = 0 \implies \lambda^* = 2$$


4. **Verify the Non-negativity Constraint:**

$$\lambda^* = 2 \geq 0 \quad \text{(Valid entry)}$$


5. **Calculate the Optimal Spatial Points ($x_1^*, x_2^*$):**

$$x_1^* = \frac{2}{2} = 1$$


$$x_2^* = \frac{2}{2} = 1$$


6. **Verify the Duality Value Balance Equation:**
* Primal Target: $f(1, 1) = 1^2 + 1^2 = 2$
* Dual Target: $L(2) = 2(2) - \frac{(2)^2}{2} = 4 - 2 = 2$



**Final Conclusion Verification:** Since $\min f(x) = 2$ matches $\max L(\lambda) = 2$, the duality relationship is computationally verified.


# Concept Name: Weak Duality Theorem in Convex Programming

When the objective function $f$ and all constraint functions $g_i$ ($i = 1, 2, \dots, m$) are convex and differentiable, the standard optimization problem transforms into a **Convex Programming Problem (CP)**. 

The **Weak Duality Theorem** establishes a fundamental bound between any feasible solution of the primal convex problem and any feasible solution of its dual counterpart.

---

## 1. Mathematical Definitions and Framework

### The Convex Primal Problem (CP)
$$\min_{x} f(x)$$
$$\text{subject to } g_j(x) \le 0, \quad j = 1, 2, \dots, m$$
Where $f$ and $g_j$ are convex, differentiable functions mapping from $\mathbb{R}^n \longrightarrow \mathbb{R}$.

### The Dual Problem (D)
$$\max_{u, \lambda} \left[ f(u) + \sum_{j=1}^m \lambda_j g_j(u) \right]$$
$$\text{subject to } \nabla f(u) + \sum_{j=1}^m \lambda_j \nabla g_j(u) = 0$$
$$\lambda_j \geq 0, \quad j = 1, 2, \dots, m$$
Where $u$ represents the dual optimization variable corresponding to space domain values.

---

## 2. Weak Duality Theorem & Step-by-Step Proof

> **Theorem Statement:** Let $x$ be a feasible solution for the Primal Problem (CP), and let $(u, \lambda)$ be a feasible solution for the Dual Problem (D). Then:
> $$f(x) \geq f(u) + \sum_{i=1}^m \lambda_i g_i(u)$$

### Step-by-Step Proof Explanation

1. **Leverage Primal Objective Convexity:**
   By the first-order condition of convexity for the differentiable function $f$ at the point $u$:
   $$f(x) - f(u) \geq (x - u)^T \nabla f(u)$$

2. **Substitute the Dual Stationary Constraint:**
   Since $(u, \lambda)$ is dual-feasible, it must satisfy $\nabla f(u) + \sum_{j=1}^m \lambda_j \nabla g_j(u) = 0$, meaning $\nabla f(u) = -\sum_{j=1}^m \lambda_j \nabla g_j(u)$. Substituting this into the first equation yields:
   $$f(x) - f(u) \geq -(x - u)^T \sum_{j=1}^m \lambda_j \nabla g_j(u) \quad \text{--- (Equation 1)}$$

3. **Leverage Constraint Function Convexity:**
   Similarly, apply the first-order condition of convexity to each constraint function $g_j$ at point $u$:
   $$g_j(x) - g_j(u) \geq (x - u)^T \nabla g_j(u)$$

4. **Apply Non-negative Multipliers:**
   Multiply both sides of the inequality by the dual multiplier $\lambda_j$ (since $\lambda_j \geq 0$, the inequality direction is preserved) and sum across all $m$ constraints:
   $$\sum_{j=1}^m \lambda_j g_j(x) - \sum_{j=1}^m \lambda_j g_j(u) \geq (x - u)^T \sum_{j=1}^m \lambda_j \nabla g_j(u) \quad \text{--- (Equation 2)}$$

5. **Combine Equation 1 and Equation 2:**
   Notice that the right side of Equation 2 is exactly the negative of the right side term in Equation 1. Adding the two inequalities together yields:
   $$f(x) - f(u) \geq \sum_{j=1}^m \lambda_j g_j(u) - \sum_{j=1}^m \lambda_j g_j(x)$$

6. **Utilize Primal Feasibility to Finalize:**
   Because $x$ is primal feasible, $g_j(x) \le 0$. Given $\lambda_j \geq 0$, their product must be non-positive ($\lambda_j g_j(x) \le 0$), meaning $-\sum \lambda_j g_j(x) \geq 0$. Removing this non-negative term simplifies the relationship to:
   $$f(x) - f(u) \geq \sum_{j=1}^m \lambda_j g_j(u) + 0$$
   $$\implies f(x) \geq f(u) + \sum_{j=1}^m \lambda_j g_j(u)$$
   **$\blacksquare$ Proof Complete**

### Corollary (Optimality Condition)
If you discover a specific primal feasible point $\bar{x}$ and a dual feasible point $(\bar{u}, \bar{\lambda})$ where their values match exactly:
$$f(\bar{x}) = f(\bar{u}) + \sum_{i=1}^m \bar{\lambda}_i g_i(\bar{u})$$
Then **$\bar{x}$ is guaranteed to be globally optimal for (CP)**, and **$(\bar{u}, \bar{\lambda})$ is guaranteed to be optimal for (D)**.

---

## 3. Geometric Visualization Graph

The Weak Duality Theorem ensures that the objective value of any primal feasible minimization solution always sits above or equal to the value of any dual maximization solution. The gap between them is called the **Duality Gap**.

```text
Primal Objective Value f(x) ──►  ▲  (Higher values: x is just feasible)
                                 │      │
                                 │      ▼  Decreases during minimization
      ===========================│===================================
      Optimal Bound Reached     │  f(x*) = Dual(u*, λ*)  [Duality Gap = 0]
      ===========================│===================================
                                 │      ▲  Increases during maximization
                                 │      │
Dual Objective Value L(u,λ) ──►  ┴  (Lower bounds: derived from multipliers)

```

---

## 4. Problems with Step-by-Step Calculations

### Problem 1: Verifying Weak Duality Bounds

Consider a 1D convex optimization problem:


$$\min f(x) = x^2 \quad \text{s.t.} \quad g(x) = 2 - x \le 0$$

Let's pick a random primal feasible point $x = 3$ and a dual point with parameters $u = 1$, $\lambda = 2$.

1. Verify if the chosen points are feasible for their respective environments.
2. Calculate both sides of the Weak Duality inequality to verify the bound holds.

#### **Step-by-Step Calculation:**

1. **Check Primal Feasibility of $x = 3$:**

$$g(3) = 2 - 3 = -1 \le 0 \quad \text{(Primal Feasible!)}$$


2. **Check Dual Feasibility of $(u=1, \lambda=2)$:**
* Multiplier check: $\lambda = 2 \geq 0$ (Valid)
* Stationary gradient condition check ($\nabla f(u) + \lambda \nabla g(u) = 0$):

$$\nabla f(u) = \frac{d}{du}(u^2) = 2u$$


$$\nabla g(u) = \frac{d}{du}(2 - u) = -1$$


$$\text{Condition: } 2u + \lambda(-1) = 2(1) - 2 = 0 \quad \text{(Dual Feasible!)}$$




3. **Compute the Primal Value $f(x)$:**

$$f(3) = 3^2 = 9$$


4. **Compute the Dual Objective Value $L(u, \lambda)$:**

$$L(u, \lambda) = f(u) + \lambda g(u)$$


$$L(1, 2) = 1^2 + 2(2 - 1) = 1 + 2(1) = 3$$


5. **Verify Inequality Bound:**

$$f(3) \geq L(1, 2) \implies 9 \geq 3 \quad \text{(True! Weak Duality holds value check.)}$$



---

### Problem 2: Proving Optimality via the Corollary

Using the same problem framework as Problem 1, test the target values $\bar{x} = 2$, $\bar{u} = 2$, and $\bar{\lambda} = 4$. Use the corollary to prove if these values represent the absolute global optimal setup.

#### **Step-by-Step Calculation:**

1. **Verify Primal Feasibility for $\bar{x} = 2$:**

$$g(2) = 2 - 2 = 0 \le 0 \quad \text{(Feasible, sits exactly on the active boundary constraint)}$$


2. **Verify Dual Feasibility for $(\bar{u}=2, \bar{\lambda}=4)$:**
* Multiplier check: $\bar{\lambda} = 4 \geq 0$ (Valid)
* Stationary gradient equation check ($2\bar{u} - \bar{\lambda} = 0$):

$$2(2) - 4 = 4 - 4 = 0 \quad \text{(Feasible!)}$$




3. **Calculate Primal Objective Value:**

$$f(\bar{x}) = f(2) = 2^2 = 4$$


4. **Calculate Dual Objective Value:**

$$L(\bar{u}, \bar{\lambda}) = \bar{u}^2 + \bar{\lambda}(2 - \bar{u})$$


$$L(2, 4) = 2^2 + 4(2 - 2) = 4 + 4(0) = 4$$


5. **Evaluate Equality Condition:**

$$f(\bar{x}) = 4, \quad L(\bar{u}, \bar{\lambda}) = 4 \implies f(\bar{x}) = L(\bar{u}, \bar{\lambda})$$



**Conclusion:** Because the primal value matches the dual value exactly, the duality gap is zero. According to the corollary, $\bar{x} = 2$ is mathematically verified as the global optimal solution.

# Concept Name: Strong Duality and the Dual of a Quadratic Programming Problem (QPP)

This note covers the complete proofs for the Optimality Conditions of Convex Programming using Strong Duality and walks step-by-step through setting up the Dual problem for a standard Quadratic Programming Problem (QPP).

---

## 1. Strong Duality & Optimality Proofs

### Strong Duality Theorem
> **Theorem Statement:** Let $\bar{x}$ be a feasible solution to the Convex Programming problem (CP) and let the basic constraint qualification hold at $\bar{x}$. Then there exists a dual multiplier vector $\bar{\lambda}$ such that $(\bar{x}, \bar{\lambda})$ is optimal to the Dual problem (D). Further, the optimal values of the two objective functions coincide:
> $$f(\bar{x}) = f(\bar{u}) + \sum_{j} \bar{\lambda}_j g_j(\bar{u})$$

---

### Step-by-Step Proofs for the Optimality Criteria

#### **Part A: Proof that $\bar{x}$ is the Optimal Solution of (CP)**
We are given the equality of primal and dual values at the candidate optimal point:
$$f(\bar{x}) = f(\bar{u}) + \sum_{j} \bar{\lambda}_j g_j(\bar{u})$$

1. **Introduce an Arbitrary Primal Feasible Point:** Let $y$ be any feasible point belonging to the problem (CP). To prove $\bar{x}$ is the absolute minimum, we must show that:
   $$f(\bar{x}) \le f(y)$$
2. **Apply the Weak Duality Boundary:** By the Weak Duality theorem, the objective value of any primal feasible point $y$ is bounded from below by the dual function at the dual point $(\bar{u}, \bar{\lambda})$:
   $$f(y) \geq f(\bar{u}) + \sum_{j} \bar{\lambda}_j g_j(\bar{u})$$
3. **Substitute the Given Value Match:** Since the right-hand side is exactly equal to $f(\bar{x})$ by our initial condition, we substitute it directly:
   $$f(y) \geq f(\bar{x}) \implies f(\bar{x}) \le f(y)$$
4. **Conclusion:** Because $f(\bar{x})$ is less than or equal to any other feasible objective value $f(y)$, $\bar{x}$ is mathematically proven to be the **optimal solution of (CP)**.

$\blacksquare$

#### **Part B: Proof that $(\bar{u}, \bar{\lambda})$ is the Optimal Solution of (D)**
1. **Introduce an Arbitrary Dual Feasible Point:** Let $(u, \lambda)$ be any feasible point belonging to the Dual problem (D). We must show that the objective value at our candidate dual point is the absolute maximum:
   $$f(\bar{u}) + \sum_{j} \bar{\lambda}_j g_j(\bar{u}) \geq f(u) + \sum_{j} \lambda_j g_j(u)$$
2. **Apply the Weak Duality Boundary:** From Weak Duality, we know the primal value at $\bar{x}$ bounds any general dual value from above:
   $$f(\bar{x}) \geq f(u) + \sum_{j} \lambda_j g_j(u)$$
3. **Substitute the Given Value Match:** Swap $f(\bar{x})$ with its dual value expression:
   $$f(\bar{u}) + \sum_{j} \bar{\lambda}_j g_j(\bar{u}) \geq f(u) + \sum_{j} \lambda_j g_j(u)$$
4. **Conclusion:** Since the value at $(\bar{u}, \bar{\lambda})$ is greater than or equal to the function evaluation at any arbitrary dual point, **$(\bar{u}, \bar{\lambda})$ is the optimal solution of (D)**.

$\blacksquare$

---

## 2. Formulating the Dual of a Quadratic Programming Problem (QPP)

### The Primal Quadratic Programming Problem (QP)
Consider a standard QPP minimization setup:
$$(\text{QP}) \quad \min_{x} \quad c^Tx + \frac{1}{2}x^TQx$$
$$\text{subject to } Ax \le b$$
$$x \geq 0$$
Where:
*   $A$ is an $m \times n$ matrix.
*   $c, x \in \mathbb{R}^n$ and $b \in \mathbb{R}^m$.
*   $Q$ is an $n \times n$ symmetric positive semi-definite matrix.

---

### Step-by-Step Derivation of the QPP Lagrangian

#### **Step 1: Convert all constraints to the standard inequality form ($g_i(x) \le 0$)**
*   The system constraints $Ax \le b$ become:
    $$Ax - b \le 0 \quad \longrightarrow \text{Associate with multiplier vector } u \in \mathbb{R}^m$$
*   The non-negativity constraints $x \geq 0$ become:
    $$-x \le 0 \quad \longrightarrow \text{Associate with multiplier vector } v \in \mathbb{R}^n$$

#### **Step 2: Construct the Lagrangian Function $L(x, u, v)$**
We add the weighted constraints directly to the primal objective function:
$$L(x, u, v) = c^Tx + \frac{1}{2}x^TQx + u^T(Ax - b) + v^T(-x)$$

#### **Step 3: Define the Optimization Structure for the Quadratic Dual (QD)**
Following Duality theory, the Dual problem maximizes the Lagrangian subject to its gradient with respect to $x$ equaling zero:
$$(\text{QD}) \quad \max_{x, u, v} L(x, u, v)$$
$$\text{subject to } \nabla_x L(x, u, v) = 0$$
$$u \geq 0, \quad v \geq 0$$

---

## 3. Geometric Boundary Concept Matrix Graph

The Strong Duality theorem guarantees that for convex problems, the primal cost minimizes downward and the dual cost maximizes upward until they meet seamlessly at an identical point, leaving a Duality Gap of exactly 0.

```text
 Objective value Space
          ▲
          │       \       /   ◄--- Primal Minimization Objective: cᵀx + 0.5xᵀQx
          │        \     /
 Optimal  │─────────\.  /──────── Primal Min = Dual Max [Duality Gap = 0]
 Solution │          ·
          │        /───\      ◄--- Dual Maximization Objective L(x, u, v)
          │       /     \
          └────────────────────────► Primal Variable Space Domain (x)

```

---

## 4. Practice Problem with Step-by-Step Calculations

### Problem: Constructing the Matrix Dual for a 2D QPP

Given the following explicit 2D Quadratic Programming problem:


$$\min f(x_1, x_2) = 4x_1 + 3x_2 + x_1^2 + x_2^2$$

$$\text{subject to } x_1 + 2x_2 \le 6$$

$$x_1, x_2 \geq 0$$

Find the explicit gradient system constraint equation ($\nabla_x L = 0$) needed to form its Dual problem.

#### **Step-by-Step Vector-Matrix Form Setup Calculation:**

1. **Extract Matrices and Vectors:**

$$c = \begin{pmatrix} 4 \\ 3 \end{pmatrix}, \quad Q = \begin{pmatrix} 2 & 0 \\ 0 & 2 \end{pmatrix}, \quad A = \begin{pmatrix} 1 & 2 \end{pmatrix}, \quad b = \begin{pmatrix} 6 \end{pmatrix}$$



*(Note: The quadratic term is written as $\frac{1}{2}x^TQx$, so $\frac{1}{2}\begin{pmatrix} x_1 & x_2 \end{pmatrix} \begin{pmatrix} 2 & 0 \\ 0 & 2 \end{pmatrix} \begin{pmatrix} x_1 \\ x_2 \end{pmatrix} = x_1^2 + x_2^2$)*
2. **Write the Expanded Lagrangian Function:**

$$L(x_1, x_2, u_1, v_1, v_2) = 4x_1 + 3x_2 + x_1^2 + x_2^2 + u_1(x_1 + 2x_2 - 6) - v_1x_1 - v_2x_2$$


3. **Calculate the Partial Derivatives with respect to Primal Variables ($\nabla_x L = 0$):**
* For variable $x_1$:

$$\frac{\partial L}{\partial x_1} = 4 + 2x_1 + u_1 - v_1 = 0 \implies 2x_1 + u_1 - v_1 = -4$$


* For variable $x_2$:

$$\frac{\partial L}{\partial x_2} = 3 + 2x_2 + 2u_1 - v_2 = 0 \implies 2x_2 + 2u_1 - v_2 = -3$$




4. **Assemble the Final Dual Constraints Form:**

$$\begin{pmatrix} 2 & 0 \\ 0 & 2 \end{pmatrix} \begin{pmatrix} x_1 \\ x_2 \end{pmatrix} + \begin{pmatrix} 1 \\ 2 \end{pmatrix} u_1 - \begin{pmatrix} v_1 \\ v_2 \end{pmatrix} = \begin{pmatrix} -4 \\ -3 \end{pmatrix}$$


$$u_1 \geq 0, \quad v_1 \geq 0, \quad v_2 \geq 0$$



**Conclusion:** The structural framework for the QPP Dual constraints is successfully computed as $Qx + A^Tu - v = -c$.


# Concept Name: Quadratic Programming Problem (QPP) Duality & Verification

This notebook details the systematic formulation of the dual for a Quadratic Programming Problem (QPP) and provides step-by-step verification of optimality using primal-dual objective values.

---

## 1. General Mathematical Formulation of QPP Duality

### The Primal Quadratic Programming Problem (QP)
The standard minimization model for a QPP is defined as:
$$\min_{x} \quad c^Tx + \frac{1}{2}x^TQx$$
$$\text{subject to } Ax \le b$$
$$x \geq 0$$

### The Complete Dual (QD) Formulation
By utilizing the Lagrangian function, the dual configuration can be expressed in two primary equivalent structures:

#### Structure 1 (Explicit Lagrangian Form)
$$(\text{QD}) \quad \max_{x, u, v} \quad c^Tx + \frac{1}{2}x^TQx + u^T(Ax - b) - v^Tx$$
$$\text{subject to } c + Qx + A^Tu - v = 0$$
$$u \geq 0, \quad v \geq 0$$
*Note: The constraint equation stems directly from setting the gradient of the Lagrangian with respect to $x$ to zero ($\nabla_x L = 0$). Multiplying this stationary condition by $x^T$ shows that $x^Tc + x^TQx + x^tA^Tu - x^Tv = 0$, which allows for simplification.*

#### Structure 2 (Simplified Matrix Form)
Substituting the stationary condition back into the objective function allows us to eliminate the linear terms and variable vector $v$, yielding the standard simplified QPP dual matrix form:
$$(\text{QD1}) \quad \max_{x, u} \quad -\frac{1}{2}x^TQx - u^Tb$$
$$\text{subject to } c + Qx + A^Tu \geq 0$$
$$u \geq 0$$

---

## 2. Geometric Solution Space Visualization

Below is the geometric intuition highlighting how the primal minimization space matches the dual maximization space at the optimal point $(\bar{x}, \bar{u})$, closing the duality gap to $0$.

```text
 Objective Value
       ▲
  20.0 │       \       /   ◄── Primal Function f(x)
       │        \     /        Values decrease during minimization
  12.8 │─────────\.  /──────── Primal Min = Dual Max = 12.8 (Optimal Point)
       │          ·
  10.0 │        /───\      ◄── Dual Function g(u)
       │       /     /         Values increase during maximization
   0.0 └────────────────────────► Variable Domain Space (x, u)
```   