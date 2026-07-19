# Unconstrained Optimization & First-Order Optimality Conditions

## 1. Core Concept Names & Definitions

### Basic Optimization Problem Formulation
The standard mathematical programming problem $(P)$ is formulated as:
$$\text{Minimize } f(x)$$
$$\text{subject to } x \in C$$
Where $f : \mathbb{R}^n \longrightarrow \mathbb{R}$ and $C \subseteq \mathbb{R}^n$.

* **Objective Function ($f$):** The quantitative criteria expression you want to maximize or minimize.
* **Constraint / Feasible Set ($C$):** The set containing all allowable points for $x$.
* **Feasible Point ($\bar{x}$):** Any point $\bar{x}$ that belongs to the constraint set $C$ ($\bar{x} \in C$).
* **Optimal Solution / Point:** The specific feasible point where the function hits its absolute highest or lowest value.
* **Infeasible Problem:** Occurs when the constraint set is completely empty ($C = \emptyset$).

---

### Unconstrained vs. Constrained Optimization
* **Unconstrained Optimization:** Occurs when there are no artificial boundaries placed on the choices, meaning the variable can take any value in space ($C = \mathbb{R}^n$).
  $$\min_{x \in \mathbb{R}^n} / \max_{x \in \mathbb{R}^n} f(x)$$
* **Constrained Optimization:** Occurs when the variable is trapped inside a restricted subset area ($C \subset \mathbb{R}^n$).

---

### First-Order Optimality Condition & Stationary Points
* **First-Order Optimality Condition:** Let $f: U \rightarrow \mathbb{R}$ be defined on a set $U \subseteq \mathbb{R}^n$. If $\bar{x} \in \text{int}(U)$ is a local optimal point and all partial derivatives exist at $\bar{x}$, then the gradient vector must equal zero:
  $$\nabla f(\bar{x}) = 0$$
* **Stationary Point:** Any point $\bar{x}$ where the gradient vector drops to exactly zero ($\nabla f(\bar{x}) = 0$). This is where the slope of the function is completely flat.

---

## 2. Step-by-Step Procedure to Find Stationary Points
1. Find all first-order partial derivatives of the function $f(x_1, x_2, \dots, x_n)$.
2. Construct the gradient vector:
   $$\nabla f(x) = \begin{pmatrix} \frac{\partial f}{\partial x_1} \\ \frac{\partial f}{\partial x_2} \\ \vdots \\ \frac{\partial f}{\partial x_n} \end{pmatrix}$$
3. Set each individual partial derivative equation equal to zero ($0$).
4. Solve the resulting system of equations simultaneously to discover the coordinate positions of the stationary points.

---

## 3. Solved Problems with Complete Calculations

### 📝 Problem 1: Unconstrained 1D Function
Find the stationary points of the function $f(x) = x^3 - 3x$.

#### **Step 1: Compute the first derivative**
$$f'(x) = \frac{d}{dx}(x^3 - 3x) = 3x^2 - 3$$

#### **Step 2: Apply the optimality condition ($f'(x) = 0$)**
$$3x^2 - 3 = 0$$

#### **Step 3: Solve for $x$**
$$3x^2 = 3 \implies x^2 = 1 \implies x = 1 \quad \text{and} \quad x = -1$$

#### **Conclusion:**
The function has two stationary points located at $x = 1$ and $x = -1$.

---

### 📝 Problem 2: Unconstrained 2D Function
Find the stationary points of the function $f(x, y) = 2x^2 + y^2 - 4x - 4y$.

#### **Step 1: Compute the partial derivatives**
*   With respect to $x$: $\frac{\partial f}{\partial x} = \frac{\partial}{\partial x}(2x^2 - 4x) = 4x - 4$
*   With respect to $y$: $\frac{\partial f}{\partial y} = \frac{\partial}{\partial y}(y^2 - 4y) = 2y - 4$

#### **Step 2: Formulate the gradient vector system**
$$\nabla f(x, y) = \begin{pmatrix} 4x - 4 \\ 2y - 4 \end{pmatrix} = \begin{pmatrix} 0 \\ 0 \end{pmatrix}$$

#### **Step 3: Solve the equations independently**
1.  $$4x - 4 = 0 \implies 4x = 4 \implies x = 1$$
2.  $$2y - 4 = 0 \implies 2y = 4 \implies y = 2$$

#### **Conclusion:**
The function has a unique stationary point located at the coordinate $(1, 2)$.

---

## 4. Visualizing Stationary Points

The ASCII graph below maps out the geometric reality of what happens when a function's slope flattens out to fulfill $\nabla f(x) = 0$:

```text
       ▲ f(x)
       │
       │       Local Max (Slope = 0)
       │             ┌───┐
       │            *     *
       │           *       *
       │          *         *             Inflection Point (Slope = 0)
───────┼─────────*───────────*─────────────┌───┐──────────► Domain Space (x)
       │        *             *           *     *
       │       *               *         *       *
       │                        *       *         *
       │                         ┌─────┐
       │                        Local Min (Slope = 0)

```


# Second-Order Optimality Conditions in Optimization

## 1. Concept Name: Second-Order Optimality Conditions

### Simple Meaning
When seeking a local minimum of a multi-variable function, first-order derivative tests (setting the gradient vector $\nabla f(\bar{x}) = 0$) help us locate flat regions called stationary points. However, a flat slope can mean a peak, a valley, or a saddle point. 

**Second-Order Conditions** evaluate the curvature of the function using the **Hessian Matrix** ($\nabla^2 f(\bar{x})$) to determine if a point is truly a valley (local minimum).
* **Necessary Condition:** If a point is a local minimum, the matrix cannot curve downward anywhere; it must be **positive semi-definite**.
* **Sufficient Condition:** If a point is flat ($\nabla f(\bar{x}) = 0$) and curves strictly upward in all directions (**positive definite**), it is guaranteed to be a **strict local minimum**.

---

## 2. Core Theorems & Mathematical Proofs

### A. First-Order Optimality Condition Proof
Let $f : U \to \mathbb{R}$, where $U \subseteq \mathbb{R}^n$ and $\bar{x} \in \text{int}(U)$ is a local minimum point.

1. **Definition of Local Minimum:** There exists a neighborhood radius $\delta > 0$ such that:
   $$f(\bar{x}) \le f(x), \quad \forall x \in N_\delta(\bar{x}) \quad \text{--- (1)}$$

2. **Perturbation Direction:** For any vector $v \in \mathbb{R}^n$, we can scale it by a tiny scalar step $\lambda > 0$ such that $0 < \lambda < \delta$, ensuring the point $(\bar{x} + \lambda v)$ stays inside the neighborhood $N_\delta(\bar{x})$:
   $$\bar{x} + \lambda v \in N_\delta(\bar{x}) \quad \text{--- (2)}$$

3. **Inequality Combination:** Combining equations (1) and (2) gives:
   $$f(\bar{x}) \le f(\bar{x} + \lambda v) \quad \text{--- (3)}$$

4. **First-Order Taylor Expansion:**
   $$f(\bar{x} + \lambda v) = f(\bar{x}) + (\lambda v)^T \nabla f(\bar{x}) + \alpha(\bar{x}, \lambda v)\Vert{}\lambda v\Vert{} \quad \text{--- (4)}$$
   where the error term $\alpha(\bar{x}, \lambda v) \to 0$ as $\lambda \to 0$.

5. **Simplification Steps:**
   Substituting expansion (4) into inequality (3) and subtracting $f(\bar{x})$ from both sides:
   $$\lambda v^T \nabla f(\bar{x}) + \alpha(\bar{x}, \lambda v)\Vert{}\lambda v\Vert{} \ge 0$$
   Since $\Vert{}\lambda v\Vert{} = \lambda \Vert{}v\Vert{}$ for a positive scalar $\lambda$:
   $$\lambda v^T \nabla f(\bar{x}) + \lambda \alpha(\bar{x}, \lambda v)\Vert{}v\Vert{} \ge 0$$
   Divide the entire inequality by $\lambda$:
   $$v^T \nabla f(\bar{x}) + \alpha(\bar{x}, \lambda v)\Vert{}v\Vert{} \ge 0$$

6. **Taking the Limit:** As $\lambda \to 0^+$, the error term disappears:
   $$v^T \nabla f(\bar{x}) \ge 0, \quad \forall v \in \mathbb{R}^n$$
   For this condition to hold true for *both* any vector $v$ and its exact negative direction $-v$, the gradient vector must drop to zero:
   $$\nabla f(\bar{x}) = 0$$

---

### B. Second-Order Necessary Condition Proof
Let $f : U \to \mathbb{R}$ be a twice-differentiable function on an open set $U \subseteq \mathbb{R}^n$ with a local minimum at $\bar{x} \in \text{int}(U)$. 

1. From the first-order condition, we know $\nabla f(\bar{x}) = 0$.
2. Set up the second-order Taylor expansion for a valid directional step $(\bar{x} + \lambda v)$:
   $$f(\bar{x} + \lambda v) = f(\bar{x}) + (\lambda v)^T \nabla f(\bar{x}) + \frac{1}{2}(\lambda v)^T \nabla^2 f(\bar{x})\lambda v + \beta(\bar{x}, \lambda v)\Vert{}\lambda v\Vert{}^2 \quad \text{--- (3)}$$
3. Because $f(\bar{x})$ is a local minimum, $f(\bar{x} + \lambda v) - f(\bar{x}) \ge 0$. Substituting $\nabla f(\bar{x}) = 0$ removes the linear term:
   $$\frac{1}{2}\lambda^2 v^T \nabla^2 f(\bar{x})v + \lambda^2 \beta(\bar{x}, \lambda v)\Vert{}v\Vert{}^2 \ge 0 \quad \text{}$$
4. Dividing the expression by $\lambda^2$ yields:
   $$\frac{1}{2}v^T \nabla^2 f(\bar{x})v + \beta(\bar{x}, \lambda v)\Vert{}v\Vert{}^2 \ge 0$$
5. Taking the limit as $\lambda \to 0^+$, the error term $\beta \to 0$, leaving:
   $$v^T \nabla^2 f(\bar{x})v \ge 0, \quad \forall v \in \mathbb{R}^n$$

Therefore, the Hessian matrix $\nabla^2 f(\bar{x})$ is **positive semi-definite**.

---

## 3. Solved Problems with Step-by-Step Calculations

### 📝 Problem 1: Minimization Analysis on a 2D Function
Find all local minima for the function:
$$f(x, y) = x^2 + 2y^2 - 4x + 8y$$

#### **Step 1: Find Stationary Points (First-Order Condition)**
Calculate the first partial derivatives and set them to zero:
$$\frac{\partial f}{\partial x} = 2x - 4 = 0 \implies 2x = 4 \implies x = 2$$
$$\frac{\partial f}{\partial y} = 4y + 8 = 0 \implies 4y = -8 \implies y = -2$$

Our candidate stationary point is $(\bar{x}, \bar{y}) = (2, -2)$.

#### **Step 2: Construct the Hessian Matrix (Second-Order Condition)**
Calculate the second-order partial derivatives:
* $f_{xx} = \frac{\partial^2 f}{\partial x^2} = 2$
* $f_{yy} = \frac{\partial^2 f}{\partial y^2} = 4$
* $f_{xy} = f_{yx} = \frac{\partial^2 f}{\partial x \partial y} = 0$

Assemble the Hessian matrix $\nabla^2 f$:
$$\nabla^2 f(2, -2) = \begin{pmatrix} 2 & 0 \\ 0 & 4 \end{pmatrix}$$

#### **Step 3: Test Definiteness via Principal Minors**
* Order $1 \times 1$ minor: $D_1 = 2 > 0$
* Order $2 \times 2$ minor (Determinant): $D_2 = (2 \times 4) - (0 \times 0) = 8 > 0$

#### **Conclusion:**
Since all principal minors are strictly positive ($>0$), the Hessian matrix is **positive definite**. According to the sufficient condition, the point $(2, -2)$ is a **strict local minimum**.

---

### 📝 Problem 2: Checking a Saddle Point
Analyze the stationary points of the function $f(x, y) = x^2 - y^2$.

#### **Step 1: First-Order Test**
$$\frac{\partial f}{\partial x} = 2x = 0 \implies x = 0$$
$$\frac{\partial f}{\partial y} = -2y = 0 \implies y = 0$$
Stationary point at $(0,0)$.

#### **Step 2: Second-Order Test**
Calculate second derivatives:
$f_{xx} = 2$, $f_{yy} = -2$, $f_{xy} = 0$.
$$\nabla^2 f(0, 0) = \begin{pmatrix} 2 & 0 \\ 0 & -2 \end{pmatrix}$$

#### **Conclusion:**
The eigenvalues are $\lambda_1 = 2$ and $\lambda_2 = -2$. Because we have a mix of positive and negative values, the Hessian is **indefinite**. The point $(0,0)$ fails the minimum check and is classified as a saddle point.

---

## 4. Visualizing Curvature Geometries

The ASCII visualization below depicts how second-order properties differentiate a local minimum from other stationary points:

```text
       ▲ f(x,y)
       │
       │     *         *              . . . . .
       │      *       *             .           .
       │       *     *             .             .
       │        *   *               .           .
───────┼─────────***─────────────────────...───────────► Variable Space
       │    Local Minimum              Local Maximum
       │    ∇²f(x) is Positive      ∇²f(x) is Negative
       │     Semi-Definite           Semi-Definite

# Second-Order Sufficient Condition: Mathematical Proof & Applications

## 1. Concept Name: Second-Order Sufficient Condition for Local Minima

### Simple Meaning
The **Second-Order Sufficient Condition** provides a definitive mathematical test to guarantee whether a flat point (a stationary point where the gradient vector $\nabla f(\bar{x}) = 0$) behaves as a strict local minimum valley. 

If a function's gradient drops to zero at a point $\bar{x}$, and its second-order derivative structure (the **Hessian Matrix**) is **Positive Definite** at that point, then the function curves strictly upward in every single direction from $\bar{x}$. This mathematical property acts as sufficient proof that $\bar{x}$ is a **strict local minimum**.

---

## 2. Mathematical Proof by Contradiction

### Goal
Prove that if $\nabla f(\bar{x}) = 0$ and the Hessian matrix $\nabla^2 f(\bar{x})$ is strictly **positive definite**, then $\bar{x}$ must be a point of strict local minimum.

### Step-by-Step Proof Development

#### **Step 1: Set up the Contradiction Assumption**
Assume the opposite is true: Suppose $\bar{x}$ is **not** a point of strict local minimum. 
By definition, this implies there must exist a sequence of points $\{x_k\}$ converging to $\bar{x}$ ($x_k \to \bar{x}$) such that the function values are less than or equal to the value at $\bar{x}$:
$$f(\bar{x}) \ge f(x_k) \quad \text{for all } k \quad \text{--- (1)}$$

#### **Step 2: Second-Order Taylor Expansion**
Expand the function $f(x_k)$ around the point $\bar{x}$:
$$f(x_k) = f(\bar{x}) + (x_k - \bar{x})^T \nabla f(\bar{x}) + \frac{1}{2}(x_k - \bar{x})^T \nabla^2 f(\bar{x})(x_k - \bar{x}) + \beta(\bar{x}, x_k - \bar{x})\Vert{}x_k - \bar{x}\Vert{}^2$$
where the remainder error term satisfies $\beta \to 0$ as $x_k \to \bar{x} \quad \text{--- (2)}$.

#### **Step 3: Apply the Stationary Point Condition**
Since $\bar{x}$ is a stationary point, the first-order gradient term vanishes completely: $\nabla f(\bar{x}) = 0$. 
Substituting this and combining our equations (1) and (2) gives the inequality:
$$\frac{1}{2}(x_k - \bar{x})^T \nabla^2 f(\bar{x})(x_k - \bar{x}) + \beta(\bar{x}, x_k - \bar{x})\Vert{}x_k - \bar{x}\Vert{}^2 \le 0 \quad \text{--- (3)}$$

#### **Step 4: Normalize the Directional Steps**
Divide the entire inequality expression by the squared norm vector length $\Vert{}x_k - \bar{x}\Vert{}^2$:
$$\frac{1}{2}\frac{(x_k - \bar{x})^T}{\Vert{}x_k - \bar{x}\Vert{}} \nabla^2 f(\bar{x}) \frac{(x_k - \bar{x})}{\Vert{}x_k - \bar{x}\Vert{}} + \beta(\bar{x}, x_k - \bar{x}) \le 0$$

Let us define a normalized direction vector sequence $d_k$:
$$d_k = \frac{x_k - \bar{x}}{\Vert{}x_k - \bar{x}\Vert{}} \quad \text{where } \Vert{}d_k\Vert{} = 1$$
Because the sequence $\{d_k\}$ is bounded on a unit sphere, it contains a subsequence converging to a limiting unit vector $d$ as $k \to \infty$.

#### **Step 5: Evaluate the Limit and Uncover the Contradiction**
Taking the mathematical limit as $k \to \infty$, the error term $\beta \to 0$. The inequality reduces to:
$$\frac{1}{2}d^T \nabla^2 f(\bar{x})d \le 0$$

This presents a blatant mathematical contradiction! We were explicitly given that the Hessian matrix $\nabla^2 f(\bar{x})$ is **positive definite**, meaning that by definition, $d^T \nabla^2 f(\bar{x})d > 0$ for all non-zero vectors $d$. 

Because our initial assumption leads to a contradiction, the assumption must be false. Therefore, $\bar{x}$ **must be a point of strict local minimum**.

---

## 3. Solved Problems with Step-by-Step Calculations

### 📝 Problem 1: Full Optimization of a 2D Polynomial Function (From Slide)
Analyze the stationary points and definiteness of:
$$f(x, y) = xy - x^2 - y^2 - 2x - 2y + 4$$

#### **Step 1: Compute First-Order Partial Derivatives**
* $\frac{\partial f}{\partial x} = y - 2x - 2$
* $\frac{\partial f}{\partial y} = x - 2y - 2$

#### **Step 2: Find the Stationary Points ($\nabla f = 0$)**
Set both equations to zero to build a simultaneous linear system:
1) $-2x + y = 2$
2) $x - 2y = 2 \implies x = 2y + 2$

Substitute $x$ into equation (1):
$$-2(2y + 2) + y = 2 \implies -4y - 4 + y = 2$$
$$-3y = 6 \implies y = -2$$

Substitute $y = -2$ back to find $x$:
$$x = 2(-2) + 2 = -4 + 2 = -2$$

The only unique stationary point for this function is **$(-2, -2)$**.

#### **Step 3: Construct the Hessian Matrix ($H_f$)**
Differentiate a second time to determine the matrix entries:
* $f_{xx} = \frac{\partial^2 f}{\partial x^2} = -2$
* $f_{yy} = \frac{\partial^2 f}{\partial y^2} = -2$
* $f_{xy} = f_{yx} = \frac{\partial^2 f}{\partial x \partial y} = 1$

$$H_f = \begin{pmatrix} -2 & 1 \\ 1 & -2 \end{pmatrix}$$

#### **Step 4: Test for Definiteness Using Principal Minors**
* **Minors of Order $1 \times 1$ (Diagonal items):** $-2$ and $-2$. (Both are $< 0$)
* **Minor of Order $2 \times 2$ (Determinant):**
  $$\begin{vmatrix} -2 & 1 \\ 1 & -2 \end{vmatrix} = (-2 \times -2) - (1 \times 1) = 4 - 1 = 3 \quad (\text{Which is } > 0)$$

#### **Conclusion:**
Because the $1 \times 1$ minors are negative and the $2 \times 2$ minor is positive, the matrix is **Negative Definite**. This confirms that the point $(-2, -2)$ forms a **Strict Local Maximum** (an inverted peak rather than a minimum valley).

---

### 📝 Problem 2: Verifying a Strict Local Minimum
Analyze the function $f(x, y) = x^2 + y^2$.

#### **Step 1: First-Order Conditions**
$$\frac{\partial f}{\partial x} = 2x = 0 \implies x = 0$$
$$\frac{\partial f}{\partial y} = 2y = 0 \implies y = 0$$
Stationary point located at **$(0,0)$**.

#### **Step 2: Second-Order Conditions**
Compute second-order partial derivatives: $f_{xx} = 2$, $f_{yy} = 2$, $f_{xy} = 0$.
$$H_f = \begin{pmatrix} 2 & 0 \\ 0 & 2 \end{pmatrix}$$

#### **Step 3: Evaluate Definiteness**
* $D_1 = 2 > 0$
* $D_2 = (2 \times 2) - 0 = 4 > 0$

#### **Conclusion:**
Since all principal minors are strictly positive ($> 0$), the Hessian matrix is **Positive Definite**. By the Second-Order Sufficient Condition, the origin $(0,0)$ is verified as a **Strict Local Minimum**.

---

## 4. Optimization Curvature Visualization

This text graph visualizes how the signs of second-order changes determine whether a flat stationary point is a local minimum valley or maximum peak:

```text
  [ Strict Local Maximum ]                [ Strict Local Minimum ]
     Hessian Matrix ≺ 0                      Hessian Matrix ≻ 0
     (Negative Definite)                     (Positive Definite)

            ***                                     *         *
          *     *                                    *       *
         *       *                                    *     *
───────*───────────*───────► Variable Space ◄───────────***─────────
       ▲                                                 ▲
  Slope = 0                                         Slope = 0
 (Peak Summit)                                     (Valley Basin)              