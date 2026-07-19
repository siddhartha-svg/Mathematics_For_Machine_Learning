# Foundations of Mathematical Optimization

## 1. Concept Name: Mathematical Programming & Optimization Basics

### Simple Meaning
* **Optimization** is simply the process of making the best possible choice from a set of available options based on a specific goal. 
* A **Mathematical Programming Problem** translates real-world goals (like maximizing corporate profits or minimizing transport costs) into equations containing an objective function and structural constraints.

---

## 2. Terminology Breakdown

* **Objective Function ($f(x)$):** The main mathematical expression that you want to either maximize or minimize.
* **Constraints ($g_j(x) \le 0$):** Rules or limitations that restrict the choices you can make.
* **Decision Variables ($x = (x_1, x_2, \dots, x_n)^T$):** The unknown variables or parameters you adjust to get the best outcome.
* **Feasible Set / Feasible Region ($S$):** The collection of all possible coordinate points that satisfy every single constraint simultaneously.
  $$S = \{x \in \mathbb{R}^n : g_j(x) \le 0, \ j=1, 2, \dots, m\}$$
* **Feasible Point ($\hat{x}$):** Any single individual point that lives inside the feasible set $S$.
* **Optimal Point / Solution:** A special feasible point that successfully achieves the highest possible value (for maximization) or lowest possible value (for minimization) of the objective function $f$.

---

## 3. Local vs. Global Maxima

* **Local Maxima:** A point $x = \alpha_1$ is a local maximum if its output value $f(\alpha_1)$ is greater than or equal to any nearby point $f(x)$ within a small surrounding neighborhood region $N_\delta(\alpha_1)$.
  $$f(\alpha_1) \ge f(x) \quad \forall x \in N_\delta(\alpha_1)$$
* **Global Maxima:** A point $x = \beta_1$ is a global maximum if its output value $f(\beta_1)$ is absolute peak value across the entire feasible set $S$.
  $$f(\beta_1) \ge f(x) \quad \forall x \in S$$

---

## 4. Solved Problems with Step-by-Step Calculations

### 📝 Problem 1: Finding Feasible Set & Solutions
An objective function is given by $f(x) = 5x$. It is subject to the single boundary constraint:
$$g(x) = x - 4 \le 0 \quad \text{where } x \ge 0$$
Find the Feasible Set, the Local Maxima, and the Global Maxima.

#### **Step 1: Determine the Feasible Set ($S$)**
1. Rewrite the inequality constraint:
   $$x - 4 \le 0 \implies x \le 4$$
2. Combine this with the non-negativity constraint ($x \ge 0$):
   $$S = \{x \in \mathbb{R} : 0 \le x \le 4\} \implies S = [0, 4]$$

#### **Step 2: Evaluate the Function Behavior**
The objective function $f(x) = 5x$ is a strictly increasing linear function. As $x$ increases, $f(x)$ increases.

#### **Step 3: Calculate Boundary Constraints Outposts**
* At the lower bound ($x = 0$): $f(0) = 5(0) = 0$
* At the upper bound ($x = 4$): $f(4) = 5(4) = 20$

#### **Conclusion:**
* **Feasible Set:** $S = [0, 4]$
* **Optimal Solution Point:** $x = 4$
* **Global Maximum Value:** $20$ (Since there are no other peaks, $x = 4$ serves as both the local and global maximum point).

---

### 📝 Problem 2: Identifying Multiple Extrema
Let $f(x) = -x^2 + 6x$ over the entire real domain $S = \mathbb{R}$. Find the optimal point.

#### **Step 1: Take the First Derivative to find Critical Points**
$$f'(x) = -2x + 6$$
Set the derivative equal to zero:
$$-2x + 6 = 0 \implies 2x = 6 \implies x = 3$$

#### **Step 2: Test the Critical Point via the Second Derivative**
$$f''(x) = -2$$
Since $f''(3) = -2 < 0$, the function curves downward (concave), confirming that $x = 3$ is a maximum point.

#### **Step 3: Calculate the Maximum Value**
$$f(3) = -(3)^2 + 6(3) = -9 + 18 = 9$$

#### **Conclusion:**
Since this parabola opens downwards indefinitely, the point $x = 3$ yields the absolute highest point on the curve. Thus, $x = 3$ is the **Global Maximum** with an optimal value of $9$.

---

## 5. Visualizing Optimization Landscapes

The ASCII graph below models the visual concept presented in the slides, illustrating how local peaks contrast with the global peak:

```text
       ▲ f(x) (Objective Value)
       │
       │              Global Peak 
       │               (x = β₁)
       │                 ▲
       │   Local Peak    │
       │    (x = α₁)     │            Local Peak
       │       ▲         │                ▲
       │      * *        *               * *
       │     *   *      * *             *   *
───────┼────*─────*────*───*───────────*─────*─────► Domain Space (x)
       │   *       *  *     *         *
       │  *         **       *       *
       │ *                    *******
       └──────────────────────────────────────────

```

# Optimization Models & Linear Programming Problems (LPP)

## 1. Core Terminology & Concepts

An optimization problem aims to find the best possible solution from a set of choices according to a defined quantitative objective.

*   **Decision Variables:** $x = (x_1, x_2, \dots, x_n) \in \mathbb{R}^n$ are the unknown independent quantities that you choose or control to optimize your problem. These can be continuous, discrete, or sets.
*   **Objective Function:** The mathematical function $f : \mathbb{R}^n \to \mathbb{R}$ that evaluates the performance criterion to be maximized or minimized.
*   **Constraints:** Conditions or physical limits that the decision variables must satisfy.
    *   *Inequality constraints:* $g(x) \le 0$
    *   *Equality constraints:* $h(x) = 0$
    *   *Integer constraints:* $x \in I$, where $I$ is the set of integers
*   **Feasible Set ($S$):** The set or region containing all points that satisfy every single constraint. 
    $$S = \{x \in \mathbb{R}^n \mid x \text{ satisfies all constraints}\}$$
    Any single valid point $x \in S$ is a **feasible point**. The feasible region can be **bounded** or **unbounded**.

---

## 2. Classification of Optimization Models

Optimization models are broadly split based on the nature of their functions:

```text
               ┌─────────────────────────┐
               │   Optimization Model    │
               └────────────┬────────────┘
                            │
            ┌───────────────┴───────────────┐
            ▼                               ▼
 ┌──────────────────────┐       ┌────────────────────────┐
 │ Linear Programming   │       │ Nonlinear Programming  │
 │    Problem (LPP)     │       │         (NLP)          │
 └──────────────────────┘       └────────────────────────┘

```

* **LPP:** Both the objective function and all constraints are purely linear functions.
* **NLP:** The objective function or any of the constraints contains nonlinear terms (e.g., $x_1 x_2 \le 4$, $x_1^2$, etc.).

---

## 3. Standard Matrix Representation of an LPP

When dealing with large numbers of decision variables, we condense the system of equations into matrix notation.

### Linear System to Matrix Conversion Step-by-Step

Given the LPP problem from the slide:


$$\text{Maximize } Z = 3x_1 + 6x_2 + 2x_3$$

$$\text{subject to } \begin{cases} x_1 + x_2 + x_3 \le 1 \\ 2x_1 + x_2 + 3x_3 \le 2 \end{cases}$$

$$x_1, x_2, x_3 \ge 0$$

#### **Step 1: Construct the Objective Vector ($c^T$)**

Extract the coefficients from $Z$ into a row vector:


$$c^T = \begin{pmatrix} 3 & 6 & 2 \end{pmatrix}, \quad x = \begin{pmatrix} x_1 \\ x_2 \\ x_3 \end{pmatrix}$$


So, $Z = c^T x$.

#### **Step 2: Construct the Coefficient Matrix ($A$)**

Extract the variable coefficients from the left side of the inequality constraints:

* Row 1: $1x_1 + 1x_2 + 1x_3 \implies \begin{pmatrix} 1 & 1 & 1 \end{pmatrix}$
* Row 2: $2x_1 + 1x_2 + 3x_3 \implies \begin{pmatrix} 2 & 1 & 3 \end{pmatrix}$

$$A = \begin{pmatrix} 1 & 1 & 1 \\ 2 & 1 & 3 \end{pmatrix}$$

#### **Step 3: Construct the Right-Hand Side Vector ($b$)**

Collect the resource limits from the right side of the constraints:


$$b = \begin{pmatrix} 1 \\ 2 \end{pmatrix}$$

#### **Generalized Formula Matrix Block**

$$\begin{array}{|c|}
\hline
\text{Maximize / Minimize } Z = c^T x \\
\text{subject to } A x \le b \\
x \ge 0 \\
\hline
\end{array}$$

---

## 4. Problems with Step-by-Step Graphical Solutions

### 📝 Problem 1: Graphical Optimization of a Linear Function (Bounded LPP)

Find the optimal solution for:


$$\text{Maximize } Z = x_1 + 2x_2$$

$$\text{subject to } x_1 + x_2 \le 1$$

$$x_1, x_2 \ge 0$$

#### **Step 1: Identify the Feasible Region Boundaries**

Find where the boundary line $x_1 + x_2 = 1$ cuts the coordinate axes:

* If $x_1 = 0 \implies x_2 = 1 \implies \text{Point } (0, 1)$
* If $x_2 = 0 \implies x_1 = 1 \implies \text{Point } (1, 0)$

#### **Step 2: Plot the Feasible Bounded Space**

Since $x_1 \ge 0$ and $x_2 \ge 0$, the region lies entirely in the first quadrant. Testing the origin $(0,0)$ in $0 + 0 \le 1$ holds true, so the area points toward the origin.

```text
     x₂ ▲
        │
   (0,1)●────────┐ Boundary line: x₁ + x₂ = 1
        │▒▒▒▒▒▒▒  \
        │▒▒▒▒▒▒▒   \
        │▒▒▒▒▒▒▒    \
  ──────●───────────●───────► x₁
      (0,0)       (1,0)

```

#### **Step 3: Evaluate $Z$ at each Corner Vertex**

Evaluate the objective function $Z = x_1 + 2x_2$ at all three corners:

1. **At Point $(0, 0)$:**

$$Z = 0 + 2(0) = 0 \quad \text{}$$


2. **At Point $(1, 0)$:**

$$Z = 1 + 2(0) = 1 \quad \text{}$$


3. **At Point $(0, 1)$:**

$$Z = 0 + 2(1) = 2 \quad \text{}$$



#### **Conclusion:**

The maximum value of $Z$ is $2$, occurring at the optimal coordinate point $x_1 = 0, x_2 = 1$.

---

### 📝 Problem 2: Nonlinear Unbounded Region Visualization

Sketch the feasible region defined by the nonlinear constraints:


$$S = \{(x_1, x_2) \mid x_1 x_2 \le 4, \ x_1, x_2 \ge 0\}$$

#### **Step 1: Understand the Boundary Curve**

The constraint equation is $x_1 x_2 = 4 \implies x_2 = \frac{4}{x_1}$. This forms a classic non-linear hyperbola branch in the first quadrant.

#### **Step 2: Analyze Boundedness**

* As $x_1 \to 0$, $x_2 \to \infty$.
* As $x_2 \to 0$, $x_1 \to \infty$.
Because there is no upper capping limit on either axis individually, the region stretches infinitely along the axes, forming an **unbounded feasible region**.

#### **Graphical Representation:**

```text
     x₂ ▲
        │*
        │  *  ◄── Boundary Curve: x₁x₂ = 4
        │▒▒▒ *
        │▒▒▒▒▒  *
        │▒▒▒▒▒▒▒▒  *
  ──────┴───────────────────► x₁

```

*(The shaded region below the hyperbolic arc continuing infinitely to the right and top represents the feasible set $S$).*





# Optimization Theory: Classification, Techniques, and Nonlinear Problems

## 1. Classification of Optimization Problems

Mathematical programming problems are broadly categorized into two fundamental types based on the mathematical structure of their objective function and constraints:

### A. Linear Programming Problem (LPP)
* **Definition:** A programming problem where **both** the objective function and the constraints are strictly linear functions of the decision variables.
* **Example:** 
  $$\text{Minimize } x + y$$
  $$\text{subject to } x \ge 2, \ y \ge 4$$
  This is an LPP because all expressions are first-degree polynomials.

### B. Non-Linear Programming Problem (NLP)
* **Definition:** A programming problem where **either** the objective function, one or more constraints, or both are non-linear functions of the decision variables.
* **Example:** 
  $$\text{Maximize } x^2 + y^2$$
  $$\text{subject to } x + y \le 10$$
  $$x, y \ge 0$$
  This is classified as an NLP because the objective function contains second-degree quadratic terms ($x^2 + y^2$).

---

## 2. Overview of Optimization Techniques

Depending on the geometric structure and dimensionality of the problem, various techniques are used to find solutions:

* **Mathematical Programming Techniques:** Algorithms heavily rooted in the exact geometric properties of the problem space.
  * *Examples:* Simplex algorithm, interior point method, cutting plane algorithm, branch and bound method.
* **Meta-Heuristic Techniques:** Stochastic, nature-inspired global search algorithms useful for complex, non-convex fields where derivatives might not exist.
  * *Examples:* Genetic algorithm, Particle Swarm Optimization (PSO), Grey wolf optimization.
* **Numerical Optimization Techniques:** Iterative calculus-based algorithms that use gradients or second-order derivatives to walk toward optimal points.
  * *Examples:* Steepest descent method, Newton's method, Conjugate gradient method, Penalty function method.

---

## 3. Advanced Formulation: Multi-Objective Optimization
When a system requires balancing multiple goals simultaneously, it is formulated as a multi-objective optimization problem:

$$\text{Maximize / Minimize } f = \{f_1(x), f_2(x), \dots, f_p(x)\}$$
$$\text{subject to } g_j(x) \le 0, \quad j = 1, 2, \dots, m$$

---

## 4. Solved Nonlinear Problems (With Graphical Step-by-Step Breakdown)

### 📝 Problem 1: Maximizing a Circle Objective Over a Linear Feasible Set
Solve the following optimization problem graphically:
$$\text{Maximize } Z = x_1^2 + x_2^2$$
$$\text{subject to } 2x_1 + x_2 \le 2$$
$$x_1, x_2 \ge 0$$

#### **Step 1: Parse the Feasible Set Geometry**
1. Identify the boundary line $2x_1 + x_2 = 2$ by finding its axis intercepts:
   * Set $x_1 = 0 \implies x_2 = 2 \implies \text{Intercept: } (0, 2)$
   * Set $x_2 = 0 \implies 2x_1 = 2 \implies x_1 = 1 \implies \text{Intercept: } (1, 0)$
2. Because the constraint is a "less than or equal to" ($\le 2$) inequality and non-negativity applies ($x_1, x_2 \ge 0$), the feasible region is a closed triangular region in the first quadrant bounded by $(0,0)$, $(1,0)$, and $(0,2)$.

#### **Step 2: Parse the Objective Function Geometry**
The expression $Z = x_1^2 + x_2^2$ represents the equation of a circle centered at the origin $(0,0)$ with a radius $r = \sqrt{Z}$. Maximizing $Z$ means expanding this circle outward from the origin until it hits the furthest reachable point in the feasible triangle.

#### **Step 3: Calculate Corner Values**
Evaluate $Z$ at the vertex points of the triangular region:
1. **At point $(0, 0)$:** 
   $$Z = 0^2 + 0^2 = 0$$
2. **At point $(1, 0)$:** 
   $$Z = 1^2 + 0^2 = 1$$
3. **At point $(0, 2)$:** 
   $$Z = 0^2 + 2^2 = 4$$

#### **Conclusion:**
The maximum value of the objective function is $Z = 4$, which occurs at the optimal boundary point $(0, 2)$.

```text
       x₂ ▲
          │
    (0,2) ● 
          │▒\ 
          │▒▒\      ◄── Shaded Feasible Triangle
     ((●))│▒▒▒\     ◄── Outward growing objective contour circles
   ((  •  ))   \
  ────────┴─────●─────► x₁
              (1,0)

```

---

### 📝 Problem 2: Minimizing Distance to a Point Over an Unbounded Half-Space

Solve the following optimization problem graphically:


$$\text{Minimize } Z = (x_1 - 2)^2 + (x_2 - 3)^2$$

$$\text{subject to } x_1 + x_2 \ge 1$$

$$x_1, x_2 \ge 0$$

#### **Step 1: Parse the Feasible Region**

1. Draw the boundary line $x_1 + x_2 = 1$:
* Intercepts occur at $(0, 1)$ and $(1, 0)$.


2. The inequality is $\ge 1$, meaning the feasible region lies **above and to the right** of the line. Since there is no upper limit parameter, the region is **unbounded**.

#### **Step 2: Parse the Objective Function Geometry**

The equation $Z = (x_1 - 2)^2 + (x_2 - 3)^2$ represents a family of concentric circles centered at the target point $(2, 3)$ with a radius squared equal to $Z$. Minimizing $Z$ is equivalent to finding the point in the feasible region closest to this center point $(2,3)$.

#### **Step 3: Check Location of Target Center Point**

Let's see if the center point $(2, 3)$ satisfies the structural constraints:


$$x_1 + x_2 \ge 1 \implies 2 + 3 = 5 \ge 1 \quad (\text{True!})$$

Since the unconstrained global minimum point $(2,3)$ satisfies the constraints, it lies entirely inside the allowed open feasible region.

#### **Step 4: Calculate Minimum Value**

Substituting the point $(2, 3)$ directly into the objective function:


$$Z_{\text{min}} = (2 - 2)^2 + (3 - 3)^2 = 0 + 0 = 0$$

#### **Conclusion:**

The minimum value is $Z = 0$, occurring at the optimal coordinate point $(2, 3)$.

```text
       x₂ ▲              
          │        * (2,3) [Center Target]
          │       / \
    (0,1) ┼──────/───\─────┐ Feasible Region extends 
          │    / ▒▒▒▒ \    │ infinitely up and right
          │  / ▒▒▒▒▒▒▒ \   │
  ────────┴─●───────────┴──► x₁
          (1,0)

```
