# Unconstrained Optimization: Iterative Schemes and Convergence Properties

## 1. Concept Name: Iterative Search Schemes & Convergence Analysis

### Simple Meaning
When an optimization problem cannot be solved analytically (by setting the derivative to zero and solving directly), we use **numerical search techniques** to find a point $\bar{x}$ that solves (or approximately solves) the problem. 

Numerical search methods start at an initial guess and continuously update the solution step-by-step until they reach the bottom of the function curve. To ensure the strategy actually works, we look for two critical characteristics:
1. **Descent Property:** Every step must successfully lower the objective value ($f(x_{k+1}) < f(x_k)$).
2. **Order of Convergence ($p$):** A measure of the mathematical speed at which the algorithm eliminates error with each new iteration.

---

## 2. Mathematical Framework

### A. General Iterative Scheme
The core equation to find the next point in a sequence is written as:
$$x_{k+1} = x_k + \alpha_k d_k$$

Where:
* $x_k$: The current position or solution at iteration $k$.
* $d_k$: The chosen direction vector to travel away from $x_k$.
* $\alpha_k > 0$: The **step size** or distance multiplier telling us how far to move along direction $d_k$.

### B. Mathematical Speed (Order of Convergence)
Let a sequence $\{x_k\}$ converge to an optimal target point $\bar{x}$. The absolute distance to the target, given by the vector norm $\Vert{}x_k - \bar{x}\Vert{}$, is called the **error of the $k$-th iteration**.

If there exists an asymptotic constant $\alpha$ ($0 < \alpha < \infty$) and a power value $p$ such that:
$$\lim_{k \to \infty} \frac{\Vert{}x_{k+1} - \bar{x}\Vert{}}{\Vert{}x_k - \bar{x}\Vert{}^p} = \alpha$$

Then **$p$** is called the **order of convergence** of the sequence.
* **Linear Convergence ($p = 1$):** The error drops at a constant fractional rate.
* **Quadratic Convergence ($p = 2$):** The number of correct decimal places roughly doubles at each iteration step.

> 💡 **Rule:** The larger the value of $p$, the fewer iterations the algorithm requires to find the optimal solution.

---

## 3. Step-by-Step Calculations and Convergence Problems

### 📝 Problem 1: Determining the Order of Convergence ($p$) from an Error Sequence
An optimization algorithm produces a sequence of errors $e_k = \Vert{}x_k - \bar{x}\Vert{}$ across successive iterations:
* $e_0 = 0.1$
* $e_1 = 0.02$
* $e_2 = 0.0008$

Show that this sequence exhibits **Quadratic Convergence ($p = 2$)** and find the asymptotic error constant $\alpha$.

#### **Step 1: Write out the Ratio Equation for $p = 1$ and $p = 2$**
We must test which integer value of $p$ yields a constant ratio $\alpha$ where $\frac{e_{k+1}}{e_k^p} \approx \alpha$.

#### **Step 2: Test Linear Convergence ($p = 1$)**
Calculate the ratio for consecutive steps:
* **Ratio 1:** $\frac{e_1}{e_0^1} = \frac{0.02}{0.1} = 0.2$
* **Ratio 2:** $\frac{e_2}{e_1^1} = \frac{0.0008}{0.02} = 0.04$

Since $0.2 \neq 0.04$, the ratio is changing dramatically. The convergence is **not linear** ($p \neq 1$).

#### **Step 3: Test Quadratic Convergence ($p = 2$)**
Calculate the ratio using a squared denominator term ($e_k^2$):
* **Ratio 1:** $\frac{e_1}{e_0^2} = \frac{0.02}{(0.1)^2} = \frac{0.02}{0.01} = 2$
* **Ratio 2:** $\frac{e_2}{e_1^2} = \frac{0.0008}{(0.02)^2} = \frac{0.0008}{0.0004} = 2$

#### **Conclusion:**
Because the ratio remains exactly constant ($\alpha = 2$) when the denominator is squared, the sequence exhibits an **order of convergence $p = 2$ (Quadratic Convergence)**.

---

### 📝 Problem 2: Tracking an Iterative Step Calculation
Let an optimization function be given. Suppose at iteration $k$, the current point is $x_k = \begin{pmatrix} 1 \\ 2 \end{pmatrix}$. The optimization algorithm computes the descent direction vector as $d_k = \begin{pmatrix} -1 \\ 4 \end{pmatrix}$ and determines an optimal line step size of $\alpha_k = 0.5$. Calculate the coordinate point for the next iteration $x_{k+1}$.

#### **Step 1: State the Iterative Update Rule**
$$x_{k+1} = x_k + \alpha_k d_k$$

#### **Step 2: Substitute the Parameter Coordinates**
$$x_{k+1} = \begin{pmatrix} 1 \\ 2 \end{pmatrix} + 0.5 \begin{pmatrix} -1 \\ 4 \end{pmatrix}$$

#### **Step 3: Perform Vector Scalar Multiplication**
$$0.5 \begin{pmatrix} -1 \\ 4 \end{pmatrix} = \begin{pmatrix} 0.5 \times (-1) \\ 0.5 \times 4 \end{pmatrix} = \begin{pmatrix} -0.5 \\ 2 \end{pmatrix}$$

#### **Step 4: Vector Addition**
$$x_{k+1} = \begin{pmatrix} 1 \\ 2 \end{pmatrix} + \begin{pmatrix} -0.5 \\ 2 \end{pmatrix} = \begin{pmatrix} 1 + (-0.5) \\ 2 + 2 \end{pmatrix} = \begin{pmatrix} 0.5 \\ 4 \end{pmatrix}$$

#### **Conclusion:**
The next iterative step coordinate vector location is $x_{k+1} = \begin{pmatrix} 0.5 \\ 4 \end{pmatrix}$.

---

## 4. Visualizing Order of Convergence Speed

This ASCII graph compares how error decays across successive iterations for Linear ($p=1$) versus Quadratic ($p=2$) algorithms:

```text
       ▲ Absolute Vector Error: ||x_k - x̄||
       │
   0.5 ┼  *
       │   \  
   0.2 ┼    * . . . . . . . . . . . . . 
       │     \                          . ─── Linear Convergence (p=1)
   0.1 ┼      *                          .    Steady, gradual error decrease.
       │       \                          .
  0.01 ┼        ●                          .
       │         \                          .
 0.001 ┼──────────●───────────────────────────.───────► Iteration Count (k)
       │           \
       ▼            \___ Quadratic Convergence (p=2)
                         Dramatically accelerates down to 0 error.
```

# One-Dimensional Search Optimization: Unimodal Functions & Interval Reduction

## 1. Concept Name: Unimodal Functions & Interval Elimination

### Simple Meaning
A function $f: [a, b] \longrightarrow \mathbb{R}$ is said to be **unimodal** if it has exactly **one peak** (maximum or minimum) inside the given range $[a, b]$. 

For a unimodal minimization problem, this means that if you move towards the minimum point $x_{\text{min}}$, the function values constantly decrease, and once you pass it, the values constantly increase. By evaluating the function at two distinct test points ($x_1$ and $x_2$), we can safely throw away a portion of the interval where the minimum definitely cannot exist.

---

## 2. The Three Fundamental Elimination Rules (Interval Reduction)

Let $f(x)$ be a unimodal minimization function on an **interval of uncertainty** $[a, b]$. Take two distinct experimental points $x_1$ and $x_2$ such that $a < x_1 < x_2 < b$. Three main cases can occur to shrink the search space:

### Case I: $f(x_1) > f(x_2)$
*   **Simple Meaning:** The function value at $x_1$ is higher than at $x_2$. Since we are minimizing, the valley must be to the right of $x_1$.
*   **Elimination Strategy:** Discard the region $[a, x_1)$.
*   **New Interval of Uncertainty:** $x_{\text{min}} \in [x_1, b]$.

### Case II: $f(x_1) < f(x_2)$
*   **Simple Meaning:** The function value at $x_1$ is lower than at $x_2$. The valley must be to the left of $x_2$.
*   **Elimination Strategy:** Discard the region $(x_2, b]$.
*   **New Interval of Uncertainty:** $x_{\text{min}} \in [a, x_2]$.

### Case III: $f(x_1) = f(x_2)$
*   **Simple Meaning:** Both points yield identical values. The true minimum valley must lie exactly between them.
*   **Elimination Strategy:** Discard both $[a, x_1)$ and $(x_2, b]$.
*   **New Interval of Uncertainty:** $x_{\text{min}} \in [x_1, x_2]$.

---

## 3. Measure of Effectiveness ($\alpha$)

The efficiency or **measure of effectiveness** of any sequential search technique is quantified by the ratio $\alpha$:

$$\alpha = \frac{L_n}{L_0}$$

Where:
*   $L_0 = b - a$: The initial width of uncertainty before testing.
*   $L_n$: The remaining width of the interval of uncertainty after performing $n$ experiments.
*   **Goal:** A smaller $\alpha$ value means a highly effective search algorithm.

---

## 4. Solved Problems with Step-by-Step Calculations

### 📝 Problem 1: Interval Elimination Calculation (Case I)
Let a unimodal function be defined on the initial interval $L_0 = [1, 9]$. You place two experimental points at $x_1 = 3$ and $x_2 = 6$. The evaluated function outputs are $f(3) = 15$ and $f(6) = 8$. 
1. Determine the new interval of uncertainty.
2. Calculate the measure of effectiveness ($\alpha$) for this step.

#### **Step 1: Compare the Function Outputs**
*   $f(x_1) = f(3) = 15$
*   $f(x_2) = f(6) = 8$
*   Since $15 > 8$, we find that $f(x_1) > f(x_2)$. This corresponds to **Case I**.

#### **Step 2: Apply the Elimination Rule**
*   Because $f(3) > f(6)$, the minimum cannot be in the range $[a, x_1) = [1, 3)$.
*   The new reduced interval of uncertainty is:
    $$[x_1, b] = [3, 9]$$

#### **Step 3: Calculate Interval Widths**
*   Initial width: $L_0 = 9 - 1 = 8$
*   Remaining width after 2 experiments: $L_2 = 9 - 3 = 6$

#### **Step 4: Compute Effectiveness Measure ($\alpha$)**
$$\alpha = \frac{L_2}{L_0} = \frac{6}{8} = 0.75$$

#### **Conclusion:**
The new interval of uncertainty is $[3, 9]$ and the algorithm eliminated $25\%$ of the search space ($\alpha = 0.75$).

---

### 📝 Problem 2: Interval Elimination Calculation (Case II)
Using the same function on the same interval $[1, 9]$, let's change the test locations to $x_1 = 4$ and $x_2 = 7$. Suppose the outputs are $f(4) = 5$ and $f(7) = 12$. Find the new interval.

#### **Step 1: Compare the Function Outputs**
*   $f(x_1) = f(4) = 5$
*   $f(x_2) = f(7) = 12$
*   Since $5 < 12$, we find that $f(x_1) < f(x_2)$. This corresponds to **Case II**.

#### **Step 2: Apply the Elimination Rule**
*   The minimum cannot be in the rightmost range $(x_2, b] = (7, 9]$.
*   The new reduced interval of uncertainty is:
    $$[a, x_2] = [1, 7]$$

---

## 5. Visualizing Interval Elimination States

Below are ASCII charts mapping how checking two points filters out dead zones inside an uncertainty domain:

```text
CASE I Matrix: f(x₁) > f(x₂)
      ▲ f(x)
      │*
      │ \             
      │  * ◄── f(x₁)  * ◄── f(b)
      │   \          /
      │    \        * ◄── f(x₂)
      │     \      /
──────┴──────●─────●───────●──────► x
      a      x₁    x₂      b
      └──────┘
     DEAD ZONE (Discarded!) ──► New Range is [x₁, b]
```

```
CASE II Matrix: f(x₁) < f(x₂)
      ▲ f(x)
      │* ◄── f(a)      * ◄── f(x₂)
      │ \             /
      │  * ◄── f(x₁) /
      │   \         /
      │    *_______/
──────┴────●────────●──────●──────► x
      a    x₁       x₂     b
                    └──────┘
                    DEAD ZONE (Discarded!) ──► New Range is [a, x₂]
```

# Unconstrained Optimization: The Steepest Descent Method

## 1. Concept Name: The Steepest Descent (Gradient Descent) Method

### Simple Meaning
The **Steepest Descent Method** is an iterative numerical algorithm used to find the minimum point of an unconstrained function. It works on a simple principle: from your current position, look in all directions, find the path that goes down the steepest (which is the direction opposite to the gradient vector), and take a step. 

The algorithm determines the ideal step distance dynamically using an optimization sub-step, ensuring you descend efficiently until the function's slope becomes completely flat.

---

## 2. The Algorithmic Scheme

Given a function $f(x)$ with continuous first-order partial derivatives, the algorithm proceeds as follows:

1.  **Select a starting guess point:** $X_1$.
2.  **Compute the search direction ($d_k$):** Move in the direction of the negative gradient:
    $$d_k = -\nabla f(X_k)$$
3.  **Find the optimal step size ($\lambda_k$):** Determine a step length $\lambda_k > 0$ that minimizes the function value along the line of descent:
    $$\min_{\lambda_k} f(X_k + \lambda_k d_k)$$
4.  **Update the position:** Move to the next iterative point:
    $$X_{k+1} = X_k + \lambda_k d_k$$
5.  **Evaluate stopping rules:** Terminate the loop when the slope is close to zero or the improvement is negligible:
    $$\Vert{}\nabla f(X_k)\Vert{} < \epsilon \quad \text{or} \quad \Vert{}f(X_{k+1}) - f(X_k)\Vert{} < \epsilon'$$

### 💡 Core Algorithm Properties:
*   **Globally Convergent:** It will converge to a stationary point regardless of where you start in the domain.
*   **Descent Property:** Every single step guarantees a decrease in the objective function value ($f(X_{k+1}) < f(X_k)$).
*   **Order of Convergence:** It features a linear convergence rate (order of convergence equal to unity, $p=1$).

---

## 3. Solved Slide Problem with Step-by-Step Calculations

### 📝 Problem 1 (From Slides)
Minimize the function $f(x_1, x_2) = x_1^2 - x_1 x_2 + x_2^2$ using the steepest descent method.
*   **Starting Point:** $X_1 = \begin{pmatrix} 1 & \frac{1}{2} \end{pmatrix}^T$
*   **Termination Threshold Criterion:** $\vert{}f(X_{k+1}) - f(X_k)\vert{} < 0.05$

---

### 🏃 Iteration 1 Calculations

#### **Step 1: Compute the Gradient Function and Initial Gradient Vector**
$$\nabla f(x_1, x_2) = \begin{pmatrix} \frac{\partial f}{\partial x_1} \\ \frac{\partial f}{\partial x_2} \end{pmatrix} = \begin{pmatrix} 2x_1 - x_2 \\ -x_1 + 2x_2 \end{pmatrix} \quad \text{}$$

Evaluate the gradient at our starting coordinate point $X_1 = \begin{pmatrix} 1 & \frac{1}{2} \end{pmatrix}^T$:
$$\nabla f(X_1) = \begin{pmatrix} 2(1) - \frac{1}{2} \\ -1 + 2\left(\frac{1}{2}\right) \end{pmatrix} = \begin{pmatrix} \frac{3}{2} \\ 0 \end{pmatrix} \quad \text{}$$

#### **Step 2: Determine Iteration Direction ($d_1$)**
$$d_1 = -\nabla f(X_1) = \begin{pmatrix} -\frac{3}{2} \\ 0 \end{pmatrix} \quad \text{}$$

#### **Step 3: Setup New Position Vector $X_2(\lambda_1)$**
$$X_2 = X_1 + \lambda_1 d_1 = \begin{pmatrix} 1 \\ \frac{1}{2} \end{pmatrix} + \lambda_1 \begin{pmatrix} -\frac{3}{2} \\ 0 \end{pmatrix} = \begin{pmatrix} 1 - \frac{3}{2}\lambda_1 \\ \frac{1}{2} \end{pmatrix} \quad \text{}$$

#### **Step 4: Solve for the Optimal Step Size ($\lambda_1$)**
Substitute the vector components of $X_2$ back into the original objective function $f(x_1, x_2) = x_1^2 - x_1 x_2 + x_2^2$:
$$f(X_2) = \left(1 - \frac{3}{2}\lambda_1\right)^2 - \left(1 - \frac{3}{2}\lambda_1\right)\left(\frac{1}{2}\right) + \left(\frac{1}{2}\right)^2 \quad \text{}$$

To find the minimum along this line, take the derivative with respect to $\lambda_1$ and set it to zero ($\frac{df}{d\lambda_1} = 0$):
$$\frac{df}{d\lambda_1} = 2\left(1 - \frac{3}{2}\lambda_1\right)\left(-\frac{3}{2}\right) - \left(-\frac{3}{2}\right)\left(\frac{1}{2}\right) = 0 \quad \text{}$$
$$-3\left(1 - \frac{3}{2}\lambda_1\right) + \frac{3}{4} = 0 \implies -3 + \frac{9}{2}\lambda_1 + \frac{3}{4} = 0 \quad \text{}$$
$$\frac{9}{2}\lambda_1 = 3 - \frac{3}{4} = \frac{9}{4} \implies \lambda_1 = \frac{9}{4} \times \frac{2}{9} = \frac{1}{2} \quad \text{}$$

#### **Step 5: Compute New Coordinate $X_2$ and Evaluate Termination Condition**
Substitute $\lambda_1 = \frac{1}{2}$ into our $X_2$ equation:
$$X_2 = \begin{pmatrix} 1 - \frac{3}{2}\left(\frac{1}{2}\right) \\ \frac{1}{2} \end{pmatrix} = \begin{pmatrix} 1 - \frac{3}{4} \\ \frac{1}{2} \end{pmatrix} = \begin{pmatrix} \frac{1}{4} \\ \frac{1}{2} \end{pmatrix} \quad \text{}$$

Evaluate the termination metric:
*   $f(X_1) = 1^2 - (1)\left(\frac{1}{2}\right) + \left(\frac{1}{2}\right)^2 = 1 - 0.5 + 0.25 = \frac{3}{4} = 0.75$
*   $f(X_2) = \left(\frac{1}{4}\right)^2 - \left(\frac{1}{4}\right)\left(\frac{1}{2}\right) + \left(\frac{1}{2}\right)^2 = \frac{1}{16} - \frac{1}{8} + \frac{1}{4} = \frac{3}{16} = 0.1875$
*   Check condition difference: $\vert{}f(X_2) - f(X_1)\vert{} = \vert{}0.1875 - 0.75\vert{} = 0.5625 \not< 0.05$

Since $0.5625 > 0.05$, the criterion fails. **Proceed to Iteration 2.**

---

### 🏃 Iteration 2 Calculations

#### **Step 1: Compute Gradient at New Position Vector $X_2$**
$$\nabla f(X_2) = \begin{pmatrix} 2\left(\frac{1}{4}\right) - \frac{1}{2} \\ -\frac{1}{4} + 2\left(\frac{1}{2}\right) \end{pmatrix} = \begin{pmatrix} \frac{1}{2} - \frac{1}{2} \\ -\frac{1}{4} + 1 \end{pmatrix} = \begin{pmatrix} 0 \\ \frac{3}{4} \end{pmatrix} \quad \text{}$$

#### **Step 2: Determine New Iteration Direction ($d_2$)**
$$d_2 = -\nabla f(X_2) = \begin{pmatrix} 0 \\ -\frac{3}{4} \end{pmatrix} \quad \text{}$$

#### **Step 3: Setup New Position Vector $X_3(\lambda_2)$**
$$X_3 = X_2 + \lambda_2 d_2 = \begin{pmatrix} \frac{1}{4} \\ \frac{1}{2} \end{pmatrix} + \lambda_2 \begin{pmatrix} 0 \\ -\frac{3}{4} \end{pmatrix} = \begin{pmatrix} \frac{1}{4} \\ \frac{1}{2} - \frac{3}{4}\lambda_2 \end{pmatrix} \quad \text{}$$

#### **Step 4: Solve for the Optimal Step Size ($\lambda_2$)**
Substitute $X_3$ back into our main objective function:
$$f(X_3) = \left(\frac{1}{4}\right)^2 - \left(\frac{1}{4}\right)\left(\frac{1}{2} - \frac{3}{4}\lambda_2\right) + \left(\frac{1}{2} - \frac{3}{4}\lambda_2\right)^2 \quad \text{}$$

Differentiate with respect to $\lambda_2$ and solve for zero ($\frac{df}{d\lambda_2} = 0$):
$$\frac{df}{d\lambda_2} = -\left(\frac{1}{4}\right)\left(-\frac{3}{4}\right) + 2\left(\frac{1}{2} - \frac{3}{4}\lambda_2\right)\left(-\frac{3}{4}\right) = 0 \quad \text{}$$
$$\frac{3}{16} - \frac{3}{4} + \frac{9}{8}\lambda_2 = 0 \implies \frac{9}{8}\lambda_2 = \frac{9}{16} \implies \lambda_2 = \frac{1}{2} \quad \text{}$$

#### **Step 5: Compute Final Coordinate Point $X_3$ and Evaluate Termination Condition**
$$X_3 = \begin{pmatrix} \frac{1}{4} \\ \frac{1}{2} - \frac{3}{4}\left(\frac{1}{2}\right) \end{pmatrix} = \begin{pmatrix} \frac{1}{4} \\ \frac{1}{2} - \frac{3}{8} \end{pmatrix} = \begin{pmatrix} \frac{1}{4} \\ \frac{1}{8} \end{pmatrix} \quad \text{}$$

Evaluate the final termination metric:
*   $f(X_3) = \left(\frac{1}{4}\right)^2 - \left(\frac{1}{4}\right)\left(\frac{1}{8}\right) + \left(\frac{1}{8}\right)^2 = \frac{1}{16} - \frac{1}{32} + \frac{1}{64} = \frac{3}{64} = 0.046875$
*   Check condition difference: $\vert{}f(X_3) - f(X_2)\vert{} = \left\vert{}\frac{3}{64} - \frac{3}{16}\right\vert{} = \left\vert{}\frac{3 - 12}{64}\right\vert{} = \frac{9}{64} = 0.1406 \not< 0.05$

*(Note: The slides state $\frac{9}{64} < 0.05$ due to a slight typo in the slide copy text, but this step explicitly completes the two iterations matching the handout calculations).*

---

## 4. Additional Solved Problem for Practice

### 📝 Problem 2
Minimize $f(x_1, x_2) = 2x_1^2 + x_2^2$ starting from $X_1 = \begin{pmatrix} 1 & 1 \end{pmatrix}^T$. Compute the first step.

#### **Step 1: Compute Gradient**
$$\nabla f(x_1, x_2) = \begin{pmatrix} 4x_1 \\ 2x_2 \end{pmatrix} \implies \nabla f(X_1) = \begin{pmatrix} 4 \\ 2 \end{pmatrix}$$

#### **Step 2: Determine Search Direction ($d_1$)**
$$d_1 = -\begin{pmatrix} 4 \\ 2 \end{pmatrix} = \begin{pmatrix} -4 \\ -2 \end{pmatrix}$$

#### **Step 3: Construct Point Vector $X_2(\lambda_1)$**
$$X_2 = \begin{pmatrix} 1 \\ 1 \end{pmatrix} + \lambda_1 \begin{pmatrix} -4 \\ -2 \end{pmatrix} = \begin{pmatrix} 1 - 4\lambda_1 \\ 1 - 2\lambda_1 \end{pmatrix}$$

#### **Step 4: Optimize Step Size ($\lambda_1$)**
$$f(X_2) = 2(1 - 4\lambda_1)^2 + (1 - 2\lambda_1)^2$$
$$\frac{df}{d\lambda_1} = 4(1 - 4\lambda_1)(-4) + 2(1 - 2\lambda_1)(-2) = 0$$
$$-16(1 - 4\lambda_1) - 4(1 - 2\lambda_1) = 0 \implies -16 + 64\lambda_1 - 4 + 8\lambda_1 = 0$$
$$72\lambda_1 = 20 \implies \lambda_1 = \frac{20}{72} = \frac{5}{18}$$

---

## 5. Visualizing the Zig-Zag Descent Trajectory

The ASCII graph below models the geometric property of steepest descent. Because each step size $\lambda_k$ optimizes the line trajectory, **successive search directions are always perfectly orthogonal ($90^\circ$) to each other**:

```text
       x₂ ▲
          │      (Contour lines of equal function value)
          │       .───.
          │      /     \
          │     /  .─.  \
     0.5  ┼────●───┐     \     ◄── Start point X₁ (1, 0.5)
          │    │   │      )
          │    │   │     /
     0.125┼────┼───●    /      ◄── Point X₃ (1/4, 1/8)
          │    │   ▲   /
          │    └───┴──*        ◄── Point X₂ (1/4, 1/2)
          └────┼───┼───┼──────► x₁
              0.25 0.5 1.0
```

# Unconstrained Optimization: Detailed Step-by-Step Gradient Descent

## 1. Concept Name: The Steepest Descent Method (Iteration Steps)

### Simple Meaning
The **Steepest Descent Method** finds the lowest point of a bowl-like function by stepping down the steepest path. The direction is determined by taking the negative of the gradient ($d_k = -\nabla f(X_k)$). The optimal step distance ($\lambda_k$) is chosen by treating the line along that direction as a mini one-dimensional minimization problem, solving where its derivative equals zero ($\frac{df}{d\lambda_k} = 0$).

---

## 2. Complete Step-by-Step Problem Calculations (From Slides)

### 📝 Problem Context
We want to minimize the function $f(x_1, x_2) = x_1^2 - x_1 x_2 + x_2^2$.
* **Starting Guess Point:** $X_1 = \left(1, \frac{1}{2}\right)^T$.
* **Termination Check Threshold:** $\vert{}f(X_{k+1}) - f(X_k)\vert{} < 0.05$.

---

### 🏃 Iteration 1 Calculations

#### **Step 1: Compute General Gradient Formula & Find Initial Gradient**
Take partial derivatives of $f(x_1, x_2) = x_1^2 - x_1 x_2 + x_2^2$:
$$\nabla f(x_1, x_2) = \begin{pmatrix} 2x_1 - x_2 \\ -x_1 + 2x_2 \end{pmatrix}^T \text{}$$

Plug in our initial guess $X_1 = \left(1, \frac{1}{2}\right)^T$:
$$\nabla f(X_1) = \begin{pmatrix} 2(1) - \frac{1}{2} \\ -1 + 2(\frac{1}{2}) \end{pmatrix}^T = \begin{pmatrix} \frac{3}{2} \\ 0 \end{pmatrix}^T \text{}$$

#### **Step 2: Assign Descent Direction**
$$d_1 = -\nabla f(X_1) = \begin{pmatrix} -\frac{3}{2} \\ 0 \end{pmatrix}^T \text{}$$

#### **Step 3: Setup the Linear Line Path $X_2(\lambda_1)$**
$$X_2 = X_1 + \lambda_1 d_1 = \begin{pmatrix} 1 \\ \frac{1}{2} \end{pmatrix}^T + \lambda_1 \begin{pmatrix} -\frac{3}{2} \\ 0 \end{pmatrix}^T = \begin{pmatrix} 1 - \frac{3}{2}\lambda_1 \\ \frac{1}{2} \end{pmatrix}^T \text{}$$

#### **Step 4: Find the Optimal Step Size ($\lambda_1$)**
Substitute the components into $f(x_1, x_2)$:
$$f(X_2) = \left(1 - \frac{3}{2}\lambda_1\right)^2 - \left(1 - \frac{3}{2}\lambda_1\right)\left(\frac{1}{2}\right) + \left(\frac{1}{2}\right)^2 \text{}$$
$$f(X_2) = \left(\frac{2 - 3\lambda_1}{2}\right)^2 - \left(\frac{2 - 3\lambda_1}{4}\right) + \frac{1}{4} \text{}$$

Minimize with respect to $\lambda_1$ by setting the line derivative to zero:
$$\frac{df(X_2)}{d\lambda_1} = 0 \implies \lambda_1 = \frac{1}{2} \text{}$$

#### **Step 5: Compute New Coordinate $X_2$ & Verify Stopping Condition**
$$\text{Therefore, } X_2 = \begin{pmatrix} 1 - \frac{3}{2}\left(\frac{1}{2}\right) \\ \frac{1}{2} \end{pmatrix}^T = \begin{pmatrix} \frac{1}{4} \\ \frac{1}{2} \end{pmatrix}^T \text{}$$

Evaluate functional drop:
* $f(X_1) = 1^2 - (1)(\frac{1}{2}) + (\frac{1}{2})^2 = \frac{3}{4} = 0.75$
* $f(X_2) = (\frac{1}{4})^2 - (\frac{1}{4})(\frac{1}{2}) + (\frac{1}{2})^2 = \frac{1}{16} - \frac{1}{8} + \frac{1}{4} = \frac{3}{16} = 0.1875$
* Check absolute change: $\vert{}f(X_2) - f(X_1)\vert{} = \vert{}0.1875 - 0.75\vert{} = 0.5625$
* Since $0.5625 \not< 0.05$, the stop check fails. **Proceed to Iteration 2.**

---

### 🏃 Iteration 2 Calculations

#### **Step 1: Compute Gradient at $X_2$ & Assign Next Direction ($d_2$)**
$$\nabla f(X_2) = \begin{pmatrix} 2\left(\frac{1}{4}\right) - \frac{1}{2} \\ -\frac{1}{4} + 2\left(\frac{1}{2}\right) \end{pmatrix}^T = \begin{pmatrix} 0 \\ \frac{3}{4} \end{pmatrix}^T$$
$$d_2 = -\nabla f(X_2) = \begin{pmatrix} 0 \\ -\frac{3}{4} \end{pmatrix}^T \text{}$$

#### **Step 2: Setup Next Line Path $X_3(\lambda_2)$**
$$X_3 = X_2 + \lambda_2 d_2 = \begin{pmatrix} \frac{1}{4} \\ \frac{1}{2} \end{pmatrix}^T + \lambda_2 \begin{pmatrix} 0 \\ -\frac{3}{4} \end{pmatrix}^T = \begin{pmatrix} \frac{1}{4} \\ \frac{1}{2} - \frac{3}{4}\lambda_2 \end{pmatrix}^T \text{}$$

#### **Step 3: Solve for Optimal Step Size ($\lambda_2$)**
Plug the path components back into the objective function $f(x_1, x_2)$:
$$f(X_3) = \frac{1}{16} - \left(\frac{1}{2} - \frac{3}{4}\lambda_2\right)\left(\frac{1}{4}\right) + \left(\frac{1}{2} - \frac{3}{4}\lambda_2\right)^2 \text{}$$

Take the derivative with respect to $\lambda_2$ and set it equal to zero:
$$\frac{df(X_3)}{d\lambda_2} = 0 \implies \lambda_2 = \frac{1}{2} \text{}$$

#### **Step 4: Compute Final Coordinate Point $X_3$ & Verify Stopping Condition**
$$X_3 = \begin{pmatrix} \frac{1}{4} \\ \frac{1}{2} - \frac{3}{4}\left(\frac{1}{2}\right) \end{pmatrix}^T = \begin{pmatrix} \frac{1}{4} \\ \frac{1}{8} \end{pmatrix}^T \text{}$$

Evaluate convergence:
* $f(X_3) = \frac{1}{16} - (\frac{1}{8})(\frac{1}{4}) + (\frac{1}{8})^2 = \frac{1}{16} - \frac{1}{32} + \frac{1}{64} = \frac{3}{64} \approx 0.046875$
* Check absolute change: $\vert{}f(X_3) - f(X_2)\vert{} = \vert{}\frac{3}{64} - \frac{3}{16}\vert{} = \frac{9}{64} \approx 0.1406$

*(Note: Although $\frac{9}{64} \approx 0.1406$ is not strictly less than $0.05$, the slide treats this step as the final illustrative milestone iteration).*

---

## 4. Alternative Problem with Solution

### 📝 Problem 2
Find the first update step ($X_2$) to minimize $f(x, y) = x^2 + 2y^2$ using the steepest descent method starting from $X_1 = \begin{pmatrix} 2 & 1 \end{pmatrix}^T$.

#### **Step 1: Compute Initial Gradient Vector**
$$\nabla f(x, y) = \begin{pmatrix} 2x \\ 4y \end{pmatrix} \implies \nabla f(X_1) = \begin{pmatrix} 2(2) \\ 4(1) \end{pmatrix} = \begin{pmatrix} 4 \\ 4 \end{pmatrix}$$

#### **Step 2: Establish Direction Vector ($d_1$)**
$$d_1 = -\nabla f(X_1) = \begin{pmatrix} -4 \\ -4 \end{pmatrix}$$

#### **Step 3: Formulate Path Update Equation**
$$X_2(\lambda_1) = \begin{pmatrix} 2 \\ 1 \end{pmatrix} + \lambda_1 \begin{pmatrix} -4 \\ -4 \end{pmatrix} = \begin{pmatrix} 2 - 4\lambda_1 \\ 1 - 4\lambda_1 \end{pmatrix}$$

#### **Step 4: Solve for the Step Size ($\lambda_1$)**
Substitute path values into our objective function:
$$f(X_2) = (2 - 4\lambda_1)^2 + 2(1 - 4\lambda_1)^2$$
$$\frac{df}{d\lambda_1} = 2(2 - 4\lambda_1)(-4) + 4(1 - 4\lambda_1)(-4) = 0$$
$$-8(2 - 4\lambda_1) - 16(1 - 4\lambda_1) = 0 \implies -16 + 32\lambda_1 - 16 + 64\lambda_1 = 0$$
$$96\lambda_1 = 32 \implies \lambda_1 = \frac{32}{96} = \frac{1}{3}$$

#### **Step 5: Compute Coordinate Point $X_2$**
$$X_2 = \begin{pmatrix} 2 - 4(\frac{1}{3}) \\ 1 - 4(\frac{1}{3}) \end{pmatrix} = \begin{pmatrix} \frac{2}{3} \\ -\frac{1}{3} \end{pmatrix}$$

---

## 5. Visualizing the Descent Curvature Trajectory

The ASCII graph below tracks our calculated optimization trajectory. Notice how the update steps make sharp $90^\circ$ turns relative to the contour lines:

```text
       x₂ ▲
          │      (Contour rings of equal elevation)
          │       .───.
          │      /     \
     0.5  ┼────●───┐     \     ◄── Initial Guess Point X₁ (1, 0.5)
          │    │   │      )
     0.125┼────┼───●     /      ◄── Final Solved Iteration Point X₃ (1/4, 1/8)
          │    │   ▲    /
          │    └───┴───*       ◄── First Step Turning Point X₂ (1/4, 1/2)
          └────┼───┼───┼──────► x₁
              0.25 0.5 1.0
```                                                                         