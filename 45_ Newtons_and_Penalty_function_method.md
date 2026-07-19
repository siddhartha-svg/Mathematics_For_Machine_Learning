# Unconstrained Optimization: Newton's Method

---

## 1. Concept Overview & Core Schemes

### A. Basic Root-Finding Scheme
Newton's method is classically an iterative numerical algorithm used to find the real roots of a single-variable nonlinear equation:
$$g(y) = 0, \quad y \in \mathbb{R} \text{}$$

#### **The Iterative Formula:**
$$y_{k+1} = y_k - \frac{g(y_k)}{g'(y_k)} \text{}$$
where $y_k$ is the current approximation (iterate) and $g'(y_k)$ represents the first derivative evaluated at $y_k$.

---

### B. Multi-Variable Unconstrained Optimization Scheme
In unconstrained minimization, our target is to minimize a differentiable function $f(x)$ over a multi-dimensional space:
$$\min_{x \in \mathbb{R}^n} f(x)$$

To find the minimum point $\bar{x}$, we look for a coordinate vector where the first-order gradient drops to zero ($\nabla f(\bar{x}) = 0$). By applying the basic Newton scheme to this gradient system, the multi-variable iteration rule becomes:

$$\begin{array}{|c|}
\hline
x_{k+1} = x_k - (H_f(x_k))^{-1} \nabla f(x_k) \\
\hline
\end{array}$$

Where:
*   $x_k \in \mathbb{R}^n$: The current position vector at iteration $k$.
*   $\nabla f(x_k) \in \mathbb{R}^n$: The gradient vector evaluated at $x_k$.
*   $H_f(x_k) \in \mathbb{R}^{n \times n}$: The **Hessian Matrix** containing second-order partial derivatives, which **must be invertible** at $x = x_k$.

---

## 2. Derivation & Mathematical Proof

The multi-variable optimization variant of Newton's method is derived directly from a second-order Taylor series expansion.

### Step-by-Step Derivation:
1.  **Quadratic Approximation:** Approximate the objective function $f(x)$ around the local neighborhood of the current point $x_k$ using its Taylor expansion:
    $$f(x) \approx f(x_k) + (x - x_k)^T \nabla f(x_k) + \frac{1}{2}(x - x_k)^T H_f(x_k)(x - x_k) \text{}$$

2.  **Optimality Condition:** To minimize this quadratic approximation model, find its flat critical point by taking the gradient with respect to $x$ and setting it to zero:
    $$\nabla f(x) \approx \nabla f(x_k) + H_f(x_k)(x - x_k) = 0 \text{}$$

3.  **Isolate the Step Segment:** Rearrange the terms to group the displacement vector:
    $$H_f(x_k)(x - x_k) = -\nabla f(x_k) \text{}$$

4.  **Invert the Hessian Matrix:** Assuming the Hessian matrix is non-singular and invertible, multiply both sides from the left by $(H_f(x_k))^{-1}$:
    $$x - x_k = -(H_f(x_k))^{-1} \nabla f(x_k) \text{}$$

5.  **Establish Next Iteration Step:** Labeling the newly updated target vector position as $x_{k+1}$ completes the derivation:
    $$x_{k+1} = x_k - (H_f(x_k))^{-1} \nabla f(x_k) \text{}$$

---

## 3. Algorithmic Properties

*   **Quadratic Convergence ($p = 2$):** Newton's method converges extremely fast when initialized close to the true minimum. The number of correct decimal places roughly doubles with every step.
*   **Descent Property:** It inherently possesses a descent property under proper local conditions, systematically driving down function values.
*   **One-Step Solution for Quadratic Forms:** If the objective function $f(x)$ is a pure quadratic form involving a positive definite matrix, **Newton's method will find the exact global minimum in exactly one single iteration**.

---

## 4. Solved Step-by-Step Problems

### 📝 Problem 1: Basic Root Finding ($1\text{D}$)
Find the first update step ($y_1$) to locate a root of $g(y) = y^2 - 5 = 0$, starting from an initial guess of $y_0 = 3$.

#### **Step 1: Find the first derivative**
$$g'(y) = \frac{d}{dy}(y^2 - 5) = 2y$$

#### **Step 2: Apply the single-variable iteration formula**
$$y_1 = y_0 - \frac{g(y_0)}{g'(y_0)} = 3 - \frac{3^2 - 5}{2(3)}$$

#### **Step 3: Calculate the numeric updates**
$$y_1 = 3 - \frac{9 - 5}{6} = 3 - \frac{4}{6} = 3 - 0.6667 = 2.3333$$

---

### 📝 Problem 2: Multi-Variable Optimization ($2\text{D}$)
Perform one full iteration step of Newton's method to minimize the quadratic function:
$$f(x_1, x_2) = x_1^2 + 3x_2^2 - 2x_1x_2 - 4x_1$$
Starting from the initial coordinate origin guess: $x_0 = \begin{pmatrix} 0 \\ 0 \end{pmatrix}$.

#### **Step 1: Compute the Gradient Vector ($\nabla f$)**
Calculate first-order partial derivatives:
*   $\frac{\partial f}{\partial x_1} = 2x_1 - 2x_2 - 4$
*   $\frac{\partial f}{\partial x_2} = 6x_2 - 2x_1$

$$\nabla f(x) = \begin{pmatrix} 2x_1 - 2x_2 - 4 \\ -2x_1 + 6x_2 \end{pmatrix} \implies \nabla f(x_0) = \begin{pmatrix} 2(0) - 2(0) - 4 \\ -2(0) + 6(0) \end{pmatrix} = \begin{pmatrix} -4 \\ 0 \end{pmatrix}$$

#### **Step 2: Construct the Hessian Matrix ($H_f$)**
Calculate second-order partial derivatives:
*   $f_{xx} = \frac{\partial^2 f}{\partial x_1^2} = 2$
*   $f_{yy} = \frac{\partial^2 f}{\partial x_2^2} = 6$
*   $f_{xy} = f_{yx} = \frac{\partial^2 f}{\partial x_1 \partial x_2} = -2$

$$H_f(x) = \begin{pmatrix} 2 & -2 \\ -2 & 6 \end{pmatrix}$$

#### **Step 3: Invert the $2 \times 2$ Hessian Matrix**
Using the standard matrix inversion formula $\begin{pmatrix}a & b \\ c & d\end{pmatrix}^{-1} = \frac{1}{ad-bc}\begin{pmatrix}d & -b \\ -c & a\end{pmatrix}$:
$$\text{Determinant} = (2 \times 6) - (-2 \times -2) = 12 - 4 = 8$$
$$(H_f)^{-1} = \frac{1}{8}\begin{pmatrix} 6 & 2 \\ 2 & 2 \end{pmatrix} = \begin{pmatrix} 0.75 & 0.25 \\ 0.25 & 0.25 \end{pmatrix}$$

#### **Step 4: Compute the Next Position Vector ($x_1$)**
$$x_1 = x_0 - (H_f)^{-1}\nabla f(x_0)$$
$$x_1 = \begin{pmatrix} 0 \\ 0 \end{pmatrix} - \begin{pmatrix} 0.75 & 0.25 \\ 0.25 & 0.25 \end{pmatrix} \begin{pmatrix} -4 \\ 0 \end{pmatrix}$$
$$x_1 = \begin{pmatrix} 0 \\ 0 \end{pmatrix} - \begin{pmatrix} (0.75 \times -4) + 0 \\ (0.25 \times -4) + 0 \end{pmatrix} = \begin{pmatrix} 0 \\ 0 \end{pmatrix} - \begin{pmatrix} -3 \\ -1 \end{pmatrix} = \begin{pmatrix} 3 \\ 1 \end{pmatrix}$$

#### **Conclusion:**
The next point is $x_1 = \begin{pmatrix} 3 \\ 1 \end{pmatrix}$. Because the underlying function is quadratic, this single step successfully reaches the exact global minimum.

---

## 5. Geometric Visualization

The ASCII graph below visualizes how Newton's optimization method uses a local second-order Taylor series parabola to approximate the original function curve and leap directly to its estimated bottom vertex:

```text
       ▲ f(x)
       │         *                        *
       │        *  .                    .  *     ◄── Original Non-Quadratic Curve
       │       *    .                  .    *
       │      *      .                .      *
───────┼─────*────────●──────────────●────────*──► Variable Axis (x)
       │    *        / .            . \        *
       │            /   .          .   \
       │  Current ─┘     .        .     └─ Target Next Iteration
       │  Point (x_k)     .      .         Point (x_k+1)
       │                   \____/
       │            Quadratic Taylor Model Fit
       │            (Vertex points straight to x_k+1)
```

# Unconstrained Optimization: Multi-Variable Newton's Method Optimization

## 1. Concept Name: Multi-Variable Newton's Method (Exact Quadratic Optimization)

### Simple Meaning
**Newton's Method** is a powerful iterative search technique used to find the minimum of an unconstrained function. Unlike gradient descent, which only uses slope steepness (first derivatives), Newton's method calculates both the slope and the surface curvature using the second derivatives (organized into a matrix called the **Hessian Matrix**). 

Because it maps out the local curvature, if the function is a pure quadratic polynomial form, Newton's method will find the absolute exact global minimum in **exactly one iteration step** from any starting guess.

---

## 2. The Multi-Variable Iteration Scheme

The next point in the search sequence is updated according to the formula:
$$x_{k+1} = x_k - \left(H_f(x_k)\right)^{-1} \nabla f(x_k)$$

Where:
*   $x_k$: The current coordinate vector position.
*   $\nabla f(x_k)$: The first-order gradient column vector at the current point.
*   $H_f(x_k)$: The second-order partial derivative Hessian matrix.
*   $\left(H_f(x_k)\right)^{-1}$: The inverse of the Hessian matrix (which must be non-singular, meaning $\vert{}H_f\vert{} \neq 0$).

---

## 3. Solved Slide Problem with Step-by-Step Calculations

### 📝 Problem 1 (From Slides)
Use Newton's method to minimize the following function:
$$f(x_1, x_2) = x_1^2 - x_1 x_2 + 3x_2^2$$
*   **Initial Guess Approximation Point:** $x_1 = (1, 2)^T$.

---

### 🔎 Step-by-Step Calculation Workflow

#### **Step 1: Compute the First-Order Gradient Vector ($\nabla f$)**
Find the first-order partial derivatives with respect to each variable:
*   $\frac{\partial f}{\partial x_1} = \frac{\partial}{\partial x_1}(x_1^2 - x_1 x_2) = 2x_1 - x_2$
*   $\frac{\partial f}{\partial x_2} = \frac{\partial}{\partial x_2}(-x_1 x_2 + 3x_2^2) = -x_1 + 6x_2$

Assemble them into a gradient vector:
$$\nabla f(x) = \begin{bmatrix} 2x_1 - x_2 \\ -x_1 + 6x_2 \end{bmatrix} \quad \text{}$$

#### **Step 2: Evaluate the Gradient Vector at the Starting Point ($x_1$)**
Substitute the values from $x_1 = \begin{bmatrix} 1 \\ 2 \end{bmatrix}$ into our newly found gradient function:
$$\nabla f(x_1) = \begin{bmatrix} 2(1) - 2 \\ -1 + 6(2) \end{bmatrix} = \begin{bmatrix} 0 \\ 11 \end{bmatrix} \quad \text{}$$

#### **Step 3: Construct the Hessian Matrix ($H_f$)**
Differentiate a second time to determine the second-order partial rates of change:
*   $f_{11} = \frac{\partial^2 f}{\partial x_1^2} = \frac{\partial}{\partial x_1}(2x_1 - x_2) = 2$
*   $f_{22} = \frac{\partial^2 f}{\partial x_2^2} = \frac{\partial}{\partial x_2}(-x_1 + 6x_2) = 6$
*   $f_{12} = f_{21} = \frac{\partial^2 f}{\partial x_1 \partial x_2} = -1$

Assemble the Hessian matrix:
$$H_f(x) = \begin{bmatrix} 2 & -1 \\ -1 & 6 \end{bmatrix} \quad \text{}$$

#### **Step 4: Invert the $2 \times 2$ Hessian Matrix**
First, evaluate the matrix determinant to ensure it is invertible ($\vert{}H_f\vert{} \neq 0$):
$$\text{Determinant } \vert{}H_f\vert{} = (2 \times 6) - (-1 \times -1) = 12 - 1 = 11 \quad \text{}$$

Now, apply the standard $2 \times 2$ inversion formula:
$$\left(H_f(x)\right)^{-1} = \frac{1}{11} \begin{bmatrix} 6 & 1 \\ 1 & 2 \end{bmatrix} \quad \text{}$$

#### **Step 5: Compute the Next Position Vector ($x_2$)**
Apply Newton's iterative scheme using our values:
$$x_2 = x_1 - \left(H_f(x_1)\right)^{-1} \nabla f(x_1) \quad \text{}$$
$$x_2 = \begin{bmatrix} 1 \\ 2 \end{bmatrix} - \frac{1}{11} \begin{bmatrix} 6 & 1 \\ 1 & 2 \end{bmatrix} \begin{bmatrix} 0 \\ 11 \end{bmatrix} \quad \text{}$$

Perform the matrix-vector multiplication first:
$$\begin{bmatrix} 6 & 1 \\ 1 & 2 \end{bmatrix} \begin{bmatrix} 0 \\ 11 \end{bmatrix} = \begin{bmatrix} (6 \times 0) + (1 \times 11) \\ (1 \times 0) + (2 \times 11) \end{bmatrix} = \begin{bmatrix} 11 \\ 22 \end{bmatrix} \quad \text{}$$

Scale the product vector by the fraction multiplier $\frac{1}{11}$:
$$\frac{1}{11} \begin{bmatrix} 11 \\ 22 \end{bmatrix} = \begin{bmatrix} 1 \\ 2 \end{bmatrix} \quad \text{}$$

Complete the vector subtraction to find $x_2$:
$$x_2 = \begin{bmatrix} 1 \\ 2 \end{bmatrix} - \begin{bmatrix} 1 \\ 2 \end{bmatrix} = \begin{bmatrix} 0 \\ 0 \end{bmatrix} \quad \text{}$$

#### **Step 6: Evaluate the Stopping Condition ($x_3$)**
Evaluate the function's gradient at our new position $x_2 = \begin{bmatrix} 0 \\ 0 \end{bmatrix}$:
$$\nabla f(x_2) = \begin{bmatrix} 2(0) - 0 \\ -0 + 6(0) \end{bmatrix} = \begin{bmatrix} 0 \\ 0 \end{bmatrix} \quad \text{}$$

Because the gradient is exactly zero, the update step cancels out, confirming convergence:
$$x_3 = x_2 - \left(H_f(x_2)\right)^{-1} \nabla f(x_2) = \begin{bmatrix} 0 \\ 0 \end{bmatrix} - \begin{bmatrix} 0 \\ 0 \end{bmatrix} = \begin{bmatrix} 0 \\ 0 \end{bmatrix} \quad \text{}$$

#### **Conclusion:**
The exact structural **point of minima** is located globally at $(0, 0)^T$.

---

## 4. Additional Solved Problem for Practice

### 📝 Problem 2
Minimize the quadratic function $f(x_1, x_2) = 2x_1^2 + 4x_2^2 - 4x_1$ using Newton's method from the starting point $x_1 = \begin{bmatrix} 3 \\ 3 \end{bmatrix}$.

#### **Step 1: Find the Gradient Vector ($\nabla f$)**
*   $\frac{\partial f}{\partial x_1} = 4x_1 - 4$
*   $\frac{\partial f}{\partial x_2} = 8x_2$
$$\nabla f(x) = \begin{bmatrix} 4x_1 - 4 \\ 8x_2 \end{bmatrix} \implies \nabla f(x_1) = \begin{bmatrix} 4(3) - 4 \\ 8(3) \end{bmatrix} = \begin{bmatrix} 8 \\ 24 \end{bmatrix}$$

#### **Step 2: Construct the Hessian Matrix ($H_f$)**
*   $f_{11} = 4, \quad f_{22} = 8, \quad f_{12} = f_{21} = 0$
$$H_f = \begin{bmatrix} 4 & 0 \\ 0 & 8 \end{bmatrix}$$

#### **Step 3: Invert the Hessian Matrix**
$$\text{Determinant } \vert{}H_f\vert{} = (4 \times 8) - 0 = 32$$
$$\left(H_f\right)^{-1} = \frac{1}{32} \begin{bmatrix} 8 & 0 \\ 0 & 4 \end{bmatrix} = \begin{bmatrix} \frac{1}{4} & 0 \\ 0 & \frac{1}{8} \end{bmatrix}$$

#### **Step 4: Calculate the Newton Step ($x_2$)**
$$x_2 = x_1 - \left(H_f\right)^{-1} \nabla f(x_1)$$
$$x_2 = \begin{bmatrix} 3 \\ 3 \end{bmatrix} - \begin{bmatrix} \frac{1}{4} & 0 \\ 0 & \frac{1}{8} \end{bmatrix} \begin{bmatrix} 8 \\ 24 \end{bmatrix}$$
$$x_2 = \begin{bmatrix} 3 \\ 3 \end{bmatrix} - \begin{bmatrix} \frac{1}{4}(8) \\ \frac{1}{8}(24) \end{bmatrix} = \begin{bmatrix} 3 \\ 3 \end{bmatrix} - \begin{bmatrix} 2 \\ 3 \end{bmatrix} = \begin{bmatrix} 1 \\ 0 \end{bmatrix}$$

#### **Conclusion:**
The exact global minimum is reached in one iteration at $x_2 = (1, 0)^T$.

---

## 5. Geometric Optimization Trajectory Graph

This ASCII chart models how Newton's method uses localized second-order curvature mapping to jump across contour boundaries straight to the valley floor basin center in a single stride:

```text
       x₂ ▲
          │      (Concentric oval contour rings of equal elevation)
          │       .─────────.
          │      /   .───.   \
        2 ┼─────●───/─────\───\    ◄── Initial Guess Point x₁ (1, 2)
          │     │  /       \   \
          │     │ (    ●    )   )  ◄── Global Minimum Point x₂ (0, 0)
          │     │  \       /   /       reaches center in exactly 1 step!
          │     └───\─────/───/
   ───────┼──────────┼────────┴───────► x₁
         0           1
```

# Numerical Optimization: Penalty Function Method for Constrained NLP

## 1. Core Concept: Penalty Function Method
The **Penalty Function Method** is a classical numerical optimization technique designed to convert a **Non-Linear Constrained Optimization Problem (NLP)** into a sequence of equivalent **Unconstrained Optimization Problems**. This allows us to use robust unconstrained optimization algorithms (like gradient descent or Newton's method) to find solutions for complex constrained spaces.

Consider a general non-linear constrained programming problem (NLP):
$$\begin{array}{rl} \text{Minimize} & f(x) \\ \text{subject to (s/t)} & g_i(x) \le 0, \quad i = 1, 2, \dots, m \end{array}$$
where $f: \mathbb{R}^n \longrightarrow \mathbb{R}$ and $g_i: \mathbb{R}^n \longrightarrow \mathbb{R}$ are differentiable convex functions.

---

## 2. Motivation & Mathematical Framework

### Ideal Penalty Definition
To eliminate the constraints, we can theoretically add an ideal penalty term $\tilde{P}(x)$ directly to the objective function:
$$\tilde{P}(x) = \begin{cases} 0, & x \in S \\ +\infty, & x \notin S \end{cases}$$
where $S = \{x \in \mathbb{R}^n \mid g_i(x) \le 0 \text{ for } i = 1, \dots, m\}$ is the feasible set. Minimizing $f(x) + \tilde{P}(x)$ makes any point outside the feasible zone unviable due to the infinite penalty cost.

### The Smooth Quadratic Loss Function
Because an infinite jump is numerically impossible to optimize using derivatives, we approximate $\tilde{P}(x)$ using a smooth penalty function $P(x)$, commonly called the **quadratic loss function**:

$$P(x) = \sum_{i=1}^{m} \left[\max(g_i(x), 0)\right]^2$$

*   **If a point is feasible:** $g_i(x) \le 0 \implies \max(g_i(x),0) = 0 \implies$ No penalty is added.
*   **If a point is infeasible:** $g_i(x) > 0 \implies \max(g_i(x),0) = g_i(x) \implies$ A squared positive penalty is added proportional to the violation.

### The Unconstrained Sequential Problem (UMP)
We construct a sequential Unconstrained Minimization Problem (UMP) scaled by a penalty parameter $\alpha > 0$:
$$\text{(UMP)}_\alpha : \min_{x \in \mathbb{R}^n} q(x, \alpha) = f(x) + \alpha P(x)$$

---

## 3. Step-by-Step Penalty Function Algorithm

*   **Step 1:** Choose the quadratic loss penalty function $P(x) = \sum_{i=1}^{m} [\max(g_i(x), 0)]^2$.
*   **Step 2:** Define an increasing sequence of positive real numbers $\{\alpha_k\}_{k=1}^{\infty}$ that tends toward $+\infty$ (e.g., $\alpha_1 = 1$, $\alpha_2 = 10$, $\alpha_3 = 100$, $\alpha_4 = 1000$).
*   **Step 3:** Select an initial starting point $x_0 \in \mathbb{R}^n$. Solve the first problem $\text{(UMP)}_{\alpha_1}$ to find its optimal unconstrained solution, $x_1$. Set $k = 1$.
*   **Step 4:** Construct the next iteration problem using $\alpha_{k+1}$:
    $$\text{(UMP)}_{\alpha_{k+1}} : \min_{x \in \mathbb{R}^n} q(x, \alpha_{k+1}) = f(x) + \alpha_{k+1}P(x)$$
    Solve it using an unconstrained minimization technique starting from the previous solution $x_k$ to find the new optimal point $x_{k+1}$.
*   **Step 5:** **Stopping Criteria:** Terminate the iterations when the penalty footprint or function divergence drops below a specified tolerance level $\epsilon > 0$:
    $$\alpha_k P(x_k) < \epsilon \quad \text{or} \quad q(x_k, \alpha_k) - f(x_k) < \epsilon$$

---

## 4. Solved Problems with Step-by-Step Calculations

### 📝 Problem 1: Constructing and Evaluating a 1D Penalty Function
Convert the following constrained optimization problem into its unconstrained penalty format and calculate the value of the function $q(x, \alpha)$ at the point $x = 3$ for a penalty parameter $\alpha = 100$.
$$\begin{array}{rl} \text{Minimize} & f(x) = x^2 \\ \text{subject to} & g_1(x) = 2 - x \le 0 \end{array}$$

#### **Step 1: Construct the Quadratic Loss Penalty Function $P(x)$**
Using the constraint function $g_1(x) = 2 - x$:
$$P(x) = \left[\max(2 - x, 0)\right]^2$$

#### **Step 2: Assemble the Unconstrained Minimization Function $q(x, \alpha)$**
$$q(x, \alpha) = f(x) + \alpha P(x) = x^2 + \alpha \left[\max(2 - x, 0)\right]^2$$

#### **Step 3: Calculate the Function Value at $x = 3$**
1. Evaluate the inner constraint: $g_1(3) = 2 - 3 = -1$.
2. Compute the max term: $\max(-1, 0) = 0$. (The point is feasible, so the penalty drops to zero).
3. Compute total value:
   $$q(3, 100) = 3^2 + 100 \cdot (0)^2 = 9 + 0 = 9$$

---

### 📝 Problem 2: Penalty Calculation at an Infeasible Point
Using the same problem framework, calculate the function value $q(x, \alpha)$ if the search algorithm evaluates the **infeasible point** $x = 1$ with a penalty parameter $\alpha = 100$.

#### **Step 1: Evaluate the Inner Constraint**
$$g_1(1) = 2 - 1 = 1$$

#### **Step 2: Compute the Max Term and Square It**
Since $1 > 0$, the constraint is actively violated:
$$\max(1, 0) = 1 \implies [1]^2 = 1$$

#### **Step 3: Calculate Total Cost $q(1, 100)$**
$$q(1, 100) = f(1) + 100 \cdot P(1)$$
$$q(1, 100) = 1^2 + 100 \cdot (1) = 1 + 100 = 101$$

---

## 5. Visualizing the Penalty Function Barrier Concept

The text graph below demonstrates how increasing the penalty parameter $\alpha$ dynamically morphs the smooth objective function, building a sharp artificial wall at the feasible boundary line ($g(x) = 0$):

```text
       ▲ Total Cost: q(x, α)
       │
       │                 / ─── High Penalty α₃ = 100 (Creates a steep wall)
       │                /
       │               /  ─── Med Penalty α₂ = 10
       │              /*
       │             /  * ─── Low Penalty α₁ = 1
       │            /  *
       │           / *
───────┼──────────●────────────────────────► Variable Axis (x)
       │         x̄ (Feasible Boundary: g(x) = 0)
       │
       │  [ Feasible Region ] │ [ Infeasible Region ]
       │   Penalty P(x) = 0   │  Penalty P(x) grows quadratically
```



# Convergence Analysis of the Penalty Function Method

## 1. Concept Name: Convergence Criteria for Penalty Methods

### Simple Meaning
When converting a constrained Non-Linear Programming (NLP) problem into an unconstrained problem using a **Penalty Function Method**, we solve a sequence of problems with an increasing penalty scalar parameter ($\alpha_k$). 

As the penalty grows larger ($\alpha_k \to +\infty$), it penalizes constraint violations much more severely. This forces the optimal solutions of the unconstrained sequential steps ($\bar{x}_k$) closer to the true constrained boundary, making sure the algorithm converges perfectly to the exact optimal answer of the original problem ($\bar{x}$).

---

## 2. Core Lemmas for Convergence Theory

Let $\bar{x}_k$ denote the optimal solution of the Unconstrained Minimization Problem at iteration $k$ ($\text{UMP}_{\alpha_k}$), which minimizes the function:
$$q(x, \alpha_k) = f(x) + \alpha_k P(x), \quad \alpha_k > 0$$

### 📘 Lemma 1: Monotonicity Behaviors
As the penalty parameter sequence increases ($\alpha_{k+1} > \alpha_k$), the following structural properties hold true:
1.  **Total Value Lower Bound:** $q(\bar{x}_k, \alpha_k) \le q(\bar{x}_{k+1}, \alpha_{k+1})$ (The total minimum cost increases as constraints are tightened).
2.  **Violation Reduction:** $P(\bar{x}_k) \ge P(\bar{x}_{k+1})$ (The amount of constraint violation drops closer to zero).
3.  **Objective Value Growth:** $f(\bar{x}_k) \le f(\bar{x}_{k+1})$ (The true function value increases toward the constrained floor boundary).

### 📘 Lemma 2: Boundary Sandwiching
Let $\bar{x}$ be the absolute optimal constrained solution of the original NLP problem. Then, for each iteration step $k$:
$$f(\bar{x}) \ge q(\bar{x}_k, \alpha_k) \ge f(\bar{x}_k)$$

---

## 3. Solved Problem with Complete Step-by-Step Calculations

### 📝 Problem Specification (From Slides)
Solve the following constrained NLP using the Penalty Function Method:
$$\begin{array}{rl} \text{Minimize} & f(x_1, x_2) = 3x_1^2 + 2x_2^2 + 2x_1x_2 - 20x_1 - 16x_2 \\ \text{subject to (s/t)} & x_1 + x_2 = 5 \end{array}$$
*   **Starting Point:** $X_0 = (2, 2)^T$
*   **Termination Tolerance Boundary:** $\epsilon = 0.001$

---

### 🔎 Step-by-Step Calculation Curation

#### **Step 1: Convert Equality Constraint to Standard Inequalities**
An equality constraint $x_1 + x_2 = 5$ can be modeled as two overlapping inequalities:
1.  $x_1 + x_2 \le 5 \implies x_1 + x_2 - 5 \le 0$
2.  $x_1 + x_2 \ge 5 \implies -x_1 - x_2 + 5 \le 0$

#### **Step 2: Construct the Smooth Penalty Function $P(x)$**
Using the quadratic loss function format:
$$P(x_1, x_2) = \left[\max(x_1 + x_2 - 5, 0)\right]^2 + \left[\max(-x_1 - x_2 + 5, 0)\right]^2$$
Because any deviation from $5$ will make exactly one of these terms positive and the other zero, the absolute expression simplifies directly to:
$$P(x_1, x_2) = (x_1 + x_2 - 5)^2$$

#### **Step 3: Build the Total Sequential Unconstrained Optimization Function $g(x)$**
For iteration $k = 1$, choose our first penalty parameter value as $\alpha_1 = 1$:
$$g(x) = f(x) + \alpha_1 (x_1 + x_2 - 5)^2$$
$$g(x) = \left(3x_1^2 + 2x_2^2 + 2x_1x_2 - 20x_1 - 16x_2\right) + 1\left(x_1^2 + x_2^2 + 25 + 2x_1x_2 - 10x_1 - 10x_2\right)$$

Combine like algebraic variables to simplify the equation:
$$g(x) = 4x_1^2 + 3x_2^2 + 4x_1x_2 - 30x_1 - 26x_2 + 25$$

#### **Step 4: Execute Gradient Search at Initial Point $X_0 = (2, 2)^T$**
Compute the partial derivatives of $g(x)$ to check the direction of travel:
$$\nabla g(x) = \begin{pmatrix} \frac{\partial g}{\partial x_1} \\ \frac{\partial g}{\partial x_2} \end{pmatrix} = \begin{pmatrix} 8x_1 + 4x_2 - 30 \\ 6x_2 + 4x_1 - 26 \end{pmatrix}$$

Substitute the coordinate parameters from our starting point $X_0 = (2, 2)^T$:
$$\nabla g(2,2) = \begin{pmatrix} 8(2) + 4(2) - 30 \\ 6(2) + 4(2) - 26 \end{pmatrix} = \begin{pmatrix} 16 + 8 - 30 \\ 12 + 8 - 26 \end{pmatrix} = \begin{pmatrix} -6 \\ -6 \end{pmatrix}$$

We search iteratively using line step size $\alpha_0$ along the direction vector opposite the gradient:
$$X_1 = X_0 + \alpha_0 \begin{pmatrix} 6 \\ 6 \end{pmatrix} = \begin{pmatrix} 2 + 6\alpha_0 \\ 2 + 6\alpha_0 \end{pmatrix}$$

---

### 📊 Complete Iterations Summary Table

Solving the unconstrained minimizations sequentially across an increasing sequence of penalty variables ($\alpha_k = 1, 10, 100$) yields the following tracking values:

| $k$ | Penalty Parameter $\alpha_k$ | Solution Coordinate $x_k$ | Objective $f(x_k)$ | Total Value $q(x_k, \alpha_k)$ | Constraint Violation $P(x_k)$ | Stopping Metric $\alpha_k P(x_k)$ |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **1** | $1$ | $(2.375, 2.75)$ | $-46.3906$ | $-46.3750$ | $0.0156$ | $0.0156$ |
| **2** | $10$ | $(2.343, 2.686)$ | $-46.3512$ | $-46.3429$ | $0.00083$ | $0.0083$ |
| **3** | $100$ | $(2.334, 2.669)$ | $-46.3353$ | $-46.3344$ | $0.000009$ | $\mathbf{0.0009}$ |

#### **Step 5: Stopping Criteria Verification**
Evaluate the error difference at iteration $k = 3$:
$$q(x_3, \alpha_3) - f(x_3) = -46.3344 - (-46.3353) = 0.0009$$

Since $0.0009 < 0.001$ ($\epsilon$), the convergence threshold is achieved.

#### **Final Answer Conclusion:**
*   **Optimal Solution Point Vector:** $(x_1, x_2) = (2.334, 2.669)$
*   **Constrained Optimal Objective Value:** $-46.3353$

---

## 4. Visualizing Interval Convergence Trajectory

This text graph visualizes how increasing the penalty multiplier $\alpha_k$ effectively drives the unconstrained sequential solutions toward the valid boundary line segment:

```text
       x₂ ▲
          │                      Line Constraint: x₁ + x₂ = 5
        5 ┼                     /
          │                    /    UMP Solution Path
          │                   /         ● x₁ (α₁=1) [Highly violated]
          │                  /         /
          │                 /         ● x₂ (α₂=10) [Slightly violated]
          │                /        /
   ───────┼───────────────●────────► x₁
          0               5 \ 
                             \─── Optimal Constraint Point Target x₃ (α₃=100)
                                  Sticks tightly to the linear boundary limit wall.
```                                                   
