# Classification and Structure of Constrained Optimization Problems

## 1. Concept Name: Constrained Optimization Framework

### Simple Meaning
A **Constrained Optimization Problem** involves maximizing or minimizing a primary target equation (the objective function) while adhering to a strict set of boundary rules or limits (inequality or equality constraints). 

The general core math structure is written as:
$$\begin{array}{rl} \text{Minimize} & f(x) \\ \text{subject to (s/t)} & g_i(x) \le 0, \quad i = 1, 2, \dots, m \end{array}$$
where $f : \mathbb{R}^n \longrightarrow \mathbb{R}$ and $g_i : \mathbb{R}^n \longrightarrow \mathbb{R}$.

---

## 2. Classification of Problems

Constrained problems are classified based on the functional structure of $f(x)$ and $g_i(x)$:

| Problem Type | Objective Function ($f$) | Constraint Functions ($g_i$) |
| :--- | :--- | :--- |
| **Linear Programming Problem (LPP)** | Linear | All are Linear |
| **Non-Linear Programming Problem (NLPP)** | Nonlinear *OR* at least one constraint is Nonlinear |
| **Quadratic Programming Problem (QPP)** | Quadratic | All are Linear |

> 💡 *Note:* A Quadratic Programming Problem (QPP) is a specialized class belonging to the broader family of non-linear programming problems.

---

## 3. Convex Programming Problems (CPP)

A **Convex Programming Problem (CPP)** is a highly desirable class of optimization problems because any local minimum found is guaranteed to be a global minimum. 

### Core Definition
If the objective function $f$ and all constraint functions $g_i$ are mathematically **convex**, the problem is structurally a Convex Programming Problem.

### Formats & Equivalence Conditions for CPP
Depending on how the optimization goal and the inequality direction are stated, the conditions required to be a valid CPP vary:

| Optimization Goal | Constraint Direction | Required Property for $f(x)$ | Required Property for $g_i(x)$ |
| :--- | :--- | :--- | :--- |
| **Minimize** | $g_i(x) \le 0$ | **Convex** | **Convex** |
| **Maximize** | $g_i(x) \le 0$ | **Concave** | **Convex** |
| **Minimize** | $g_i(x) \ge 0$ | **Convex** | **Concave** |
| **Maximize** | $g_i(x) \ge 0$ | **Concave** | **Concave** |

---

## 4. Solved Problems with Step-by-Step Calculations

### 📝 Problem 1: Structural Classification Analysis
Classify the following optimization problem and determine if it fits the requirements for a Convex Programming Problem (CPP):
$$\text{Minimize } f(x, y) = x^2 + y^2$$
$$\text{subject to } x + y - 2 \le 0$$

#### **Step 1: Check Linearity**
* Objective: $f(x, y) = x^2 + y^2$ contains quadratic terms. It is non-linear.
* Constraint: $g_1(x, y) = x + y - 2$ is linear.
* **Classification:** Since the objective is quadratic and constraints are linear, this is a **Quadratic Programming Problem (QPP)**.

#### **Step 2: Check Curvature (Convexity) of the Objective Function**
Compute the Hessian matrix ($\nabla^2 f$) to verify convexity:
* $\frac{\partial f}{\partial x} = 2x \implies f_{xx} = 2$
* $\frac{\partial f}{\partial y} = 2y \implies f_{yy} = 2$
* $f_{xy} = f_{yx} = 0$
$$\nabla^2 f = \begin{pmatrix} 2 & 0 \\ 0 & 2 \end{pmatrix}$$
Both eigenvalues are positive ($\lambda = 2, 2$), meaning the Hessian is **positive definite**. Therefore, $f(x,y)$ is strictly **convex**.

#### **Step 3: Check Curvature of Constraints**
Since $g_1(x, y) = x + y - 2$ is a linear line expression, its second derivatives are all $0$, making its Hessian a zero matrix (positive semi-definite). Therefore, $g_1$ is **convex**.

#### **Step 4: Cross-reference CPP Conditions Matrix**
Looking at the matrix rules: We are **minimizing** a **convex** function subject to a $\le 0$ **convex** constraint. 
* **Conclusion:** This problem is verified as a **Convex Programming Problem (CPP)**.

---

### 📝 Problem 2: Checking CPP via the "Maximize $\le 0$" Format rule
Analyze the optimization properties of the following problem:
$$\text{Maximize } f(x) = -x^2$$
$$\text{subject to } x^2 - 4 \le 0$$

#### **Step 1: Evaluate the Curvature of $f(x)$**
* $f'(x) = -2x \implies f''(x) = -2$.
* Since the second derivative is strictly negative everywhere, $f(x)$ is **concave**.

#### **Step 2: Evaluate the Curvature of $g_1(x)$**
* $g_1(x) = x^2 - 4$
* $g_1'(x) = 2x \implies g_1''(x) = 2$.
* Since the second derivative is strictly positive, $g_1(x)$ is **convex**.

#### **Step 3: Evaluate against the Target Formats**
The problem asks us to **maximize** a **concave** function subject to a $g_i(x) \le 0$ condition where $g_i(x)$ is **convex**. This perfectly aligns with the second format row rules.
* **Conclusion:** This is a structurally valid **Convex Programming Problem (CPP)**.

---

## 5. Visualizing the Convex Programming Problem Concept

The ASCII plot below shows the interaction in a CPP. Minimizing a bowl-shaped convex function over a convex region prevents local trap hazards, guaranteeing that the lowest point in the allowed shaded zone is globally optimal:

```text
       ▲ f(x) (Objective Curvature)
       │
       │     *                           *
       │      *                         *
       │       *                       *
       │        *                     *
───────┼─────────*───────────────────*───────────► Variable Domain Space
       │          *   [Feasible Zone]*
       │           *================*  ◄── Constraints restrict variables
       │            \░░░░░░░░░░░░░░/       to this convex subset domain.
       │             \░░░░░░░░░░░░/
       │              \░░░░░░░░░░/
       │               ▼────────┘
       │         Global Optimum 
       │         (Unique Valley Bottom)
```

# Convex Programming Problems (CPP) & Convex Feasible Sets

## 1. Concept Name: Identification and Validation of a Convex Programming Problem (CPP)

### Simple Meaning
A **Convex Programming Problem (CPP)** is a special class of optimization problems where finding any single localized valley (a local minimum) guarantees that you have found the absolute lowest point across the entire allowable space (the global minimum). 

To ensure that an optimization problem is structured as a valid CPP, its mathematical pieces must interact correctly based on the problem formatting:
* If your goal is to **Minimize** under standard $\le 0$ constraints, the objective function and all constraints must be **convex** (curving upward like a bowl).
* If your constraints use a greater-than inequality ($\ge 0$), the constraints must be **concave** (curving downward like an inverted bowl) to keep the allowed subset region completely convex.

> 📋 **Theorem (Convex Feasible Region):** Let $g_i(x)$ for each $i = 1, 2, \dots, m$ be a convex function. Then, the resulting feasible set $S = \{x \in \mathbb{R}^n \mid g_i(x) \le 0; \ i = 1, 2, \dots, m\}$ is guaranteed to be a **convex set**.

---

## 2. Core Formats for Convex Programming Problems

A problem is structurally a CPP if and only if it aligns with one of these explicit formats:

| Problem Formulation | Objective Function Type ($f$) | Constraint Functions Type ($g_i$) |
| :--- | :--- | :--- |
| $\text{Min } f(x) \text{ s/t } g_i(x) \le 0$ | **Convex** | **Convex** |
| $\text{Max } f(x) \text{ s/t } g_i(x) \le 0$ | **Concave** | **Convex** |
| $\text{Min } f(x) \text{ s/t } g_i(x) \ge 0$ | **Convex** | **Concave** |
| $\text{Max } f(x) \text{ s/t } g_i(x) \ge 0$ | **Concave** | **Concave** |

---

## 3. Step-by-Step Problem Calculations (From Images)

### 📝 Problem 1: Full Curvature Analysis of Problem (P1)
Analyze the following constrained optimization problem to determine if it is a valid CPP:
$$\text{Minimize } f(x_1, x_2) = x_1 + x_2$$
$$\text{subject to: } \begin{cases} x_1^2 + x_2^2 \le 4 \\ x_1^2 \le x_2 \\ x_1, x_2 \ge 0 \end{cases}$$

#### **Step 1: Standardize the Constraints to the $g_i(x) \le 0$ Format**
*   Constraint 1: $x_1^2 + x_2^2 \le 4 \implies g_1(x_1, x_2) = x_1^2 + x_2^2 - 4 \le 0$
*   Constraint 2: $x_1^2 \le x_2 \implies g_2(x_1, x_2) = x_1^2 - x_2 \le 0$
*   Constraint 3 (Sign): $x_1 \ge 0 \implies g_3(x_1, x_2) = -x_1 \le 0$
*   Constraint 4 (Sign): $x_2 \ge 0 \implies g_4(x_1, x_2) = -x_2 \le 0$

#### **Step 2: Check Curvature of Objective Function ($f$)**
Calculate the partial derivatives of $f(x_1, x_2) = x_1 + x_2$:
*   $\frac{\partial f}{\partial x_1} = 1 \implies \frac{\partial^2 f}{\partial x_1^2} = 0, \quad \frac{\partial^2 f}{\partial x_1 \partial x_2} = 0$
*   $\frac{\partial f}{\partial x_2} = 1 \implies \frac{\partial^2 f}{\partial x_2^2} = 0, \quad \frac{\partial^2 f}{\partial x_2 \partial x_1} = 0$

Construct the Hessian matrix:
$$\nabla^2 f = \begin{pmatrix} 0 & 0 \\ 0 & 0 \end{pmatrix}$$
Because a zero matrix is positive semi-definite, the linear objective function $f$ is **convex**.

#### **Step 3: Check Curvature of Constraint $g_1$**
Calculate second-order derivatives for $g_1 = x_1^2 + x_2^2 - 4$:
*   $\frac{\partial g_1}{\partial x_1} = 2x_1 \implies \frac{\partial^2 g_1}{\partial x_1^2} = 2, \quad \frac{\partial^2 g_1}{\partial x_1 \partial x_2} = 0$
*   $\frac{\partial g_1}{\partial x_2} = 2x_2 \implies \frac{\partial^2 g_1}{\partial x_2^2} = 2, \quad \frac{\partial^2 g_1}{\partial x_2 \partial x_1} = 0$

Construct the Hessian matrix:
$$\nabla^2 g_1 = \begin{pmatrix} 2 & 0 \\ 0 & 2 \end{pmatrix}$$
*   *Order $1 \times 1$ minors:* $2, 2 > 0$
*   *Order $2 \times 2$ minor (Determinant):* $(2 \times 2) - 0 = 4 > 0$

Since all principal minors are strictly positive, $\nabla^2 g_1$ is positive definite, making $g_1$ strictly **convex**.

#### **Step 4: Check Curvature of Constraint $g_2$**
Calculate second-order derivatives for $g_2 = x_1^2 - x_2$:
*   $\frac{\partial g_2}{\partial x_1} = 2x_1 \implies \frac{\partial^2 g_2}{\partial x_1^2} = 2, \quad \frac{\partial^2 g_2}{\partial x_1 \partial x_2} = 0$
*   $\frac{\partial g_2}{\partial x_2} = -1 \implies \frac{\partial^2 g_2}{\partial x_2^2} = 0, \quad \frac{\partial^2 g_2}{\partial x_2 \partial x_1} = 0$

Construct the Hessian matrix:
$$\nabla^2 g_2 = \begin{pmatrix} 2 & 0 \\ 0 & 0 \end{pmatrix}$$
*   *Order $1 \times 1$ minors:* $2 \ge 0$ and $0 \ge 0$
*   *Order $2 \times 2$ minor:* $(2 \times 0) - 0 = 0 \ge 0$

Since the minors are non-negative, $\nabla^2 g_2$ is positive semi-definite, making $g_2$ a valid **convex** function.

#### **Step 5: Check Linear Boundary Cutes ($g_3, g_4$)**
Since $g_3 = -x_1$ and $g_4 = -x_2$ are purely linear functions, their Hessians are completely zero, classifying them as **convex**.

#### **Conclusion (P1):**
We are **minimizing** a **convex** objective function over a set of entirely **convex** functions under $\le 0$ formats. Therefore, **(P1) is completely a Convex Programming Problem (CPP)**.

---

### 📝 Problem 2: Counter-Example Analysis of Problem (P2)
Determine if the following optimization problem is a valid CPP:
$$\text{Maximize } f(x_1, x_2) = 2x_1 - x_2$$
$$\text{subject to: } \begin{cases} x_1 + x_2 \le 3 \\ x_1 x_2 \le 1 \\ x_1, x_2 \ge 0 \end{cases}$$

#### **Step 1: Check the Non-Linear Constraint Curvature ($g_2 = x_1 x_2 - 1 \le 0$)**
Let's find the Hessian matrix of $g_2(x_1, x_2) = x_1 x_2 - 1$:
*   $\frac{\partial g_2}{\partial x_1} = x_2 \implies \frac{\partial^2 g_2}{\partial x_1^2} = 0$
*   $\frac{\partial g_2}{\partial x_2} = x_1 \implies \frac{\partial^2 g_2}{\partial x_2^2} = 0$
*   Cross terms: $\frac{\partial^2 g_2}{\partial x_1 \partial x_2} = 1$

Construct the Hessian matrix:
$$\nabla^2 g_2 = \begin{pmatrix} 0 & 1 \\ 1 & 0 \end{pmatrix}$$

#### **Step 2: Evaluate Minors for Definiteness**
*   Order $1 \times 1$ minors: $0$
*   Order $2 \times 2$ minor (Determinant): $\begin{vmatrix} 0 & 1 \\ 1 & 0 \end{vmatrix} = (0 \times 0) - (1 \times 1) = -1$

#### **Conclusion (P2):**
Because the determinant minor is strictly negative ($-1$), the matrix is **indefinite**. This means the function $g_2(x_1, x_2) = x_1 x_2 - 1$ is **not convex**. Consequently, the space inside this boundary constraint forms a non-convex region, proving that **(P2) is NOT a Convex Programming Problem**.

---

## 4. Visualizing a Convex vs. Non-Convex Feasible Set

The graphic below displays why convex constraint functions ($g_i \le 0$) are vital for keeping optimization algorithms running reliably without getting stuck:

```text
    [ CONVEX FEASIBLE REGION ]              [ NON-CONVEX FEASIBLE REGION ]
       (Valid CPP Space)                       (Invalid CPP Space)
       
          ┌───────────┐                            * * * * *
         /             \                         *           *
        /   Feasible    \                       *   Feasible  *
       │     Valid       │                      *    Region    *
        \   Region      /                        *            *
         \             /                           *   ┌────┐*  ◄── [Trapping Dent]
          └───────────┘                             * *     *
                                                    
  Straight lines connecting any two           A line connecting two interior 
  points stay entirely inside the set.       points passes completely outside the set!

```

# Convex Optimization: Characterization of Convex Programming Problems (CPP)

## 1. Concept Name: Convex Programming Problem (CPP) Validation

### Simple Meaning
A **Convex Programming Problem (CPP)** is a structured optimization format where any local optimum is guaranteed to be a global optimum. To determine if a problem is a CPP, we must test the mathematical curvature (convexity/concavity) of its objective function and all structural constraints. 

For a standard format maximizing a function subject to lower-bounded inequality constraints ($\le 0$), the rules require that:
1. The **Objective Function** must be **Concave** (or both convex & concave, such as linear functions).
2. All **Constraint Functions** must be strictly **Convex** to ensure the entire feasible space remains a valid convex set.

> 📋 **Fundamental Theorem:** Let $g_i$ for each $i = 1, 2, \dots, m$ be a convex function. Then the set:
> $$S = \{x \in \mathbb{R}^n : g_i(x) \le 0; \ i = 1, 2, \dots, m\}$$
> is mathematically guaranteed to be a **convex set**.

---

## 2. Standard Formats and Rules Matrix for CPP

An optimization problem fits the requirements of a CPP if it strictly complies with one of the following setups:

| Optimization Goal | Constraint Formats | Objective Function ($f$) Property | Constraint Functions ($g_i$) Property |
| :--- | :--- | :--- | :--- |
| **Minimize** | $g_i(x) \le 0$ | Convex | Convex |
| **Maximize** | $g_i(x) \le 0$ | **Concave** | **Convex** |

---

## 3. Step-by-Step Problem Calculations (From Images)

### 📝 Problem 1: Full Dissection of Problem (P2)
Determine whether the following optimization problem is a valid Convex Programming Problem (CPP):
$$\text{Maximize } f(x_1, x_2) = 2x_1 - x_2$$
$$\text{subject to: } \begin{cases} x_1 + x_2 \le 3 \\ x_1 x_2 \le 1 \\ x_1, x_2 \ge 0 \end{cases}$$

#### **Step 1: Rewrite Constraints into Standard Inequality Format ($g_i(x) \le 0$)**
*   Constraint 1 ($g_1$): $x_1 + x_2 \le 3 \implies x_1 + x_2 - 3 \le 0$
*   Constraint 2 ($g_2$): $x_1 x_2 \le 1 \implies x_1 x_2 - 1 \le 0$
*   Constraint 3 ($g_3$): $x_1 \ge 0 \implies -x_1 \le 0$
*   Constraint 4 ($g_4$): $x_2 \ge 0 \implies -x_2 \le 0$

#### **Step 2: Check Curvature of the Objective Function ($f$)**
The objective function is $f(x_1, x_2) = 2x_1 - x_2$.
*   Since it is a first-degree polynomial expression (linear), its rate of change is constant. Linear functions have zero second derivatives, meaning they are simultaneously **convex and concave**.
*   This satisfies the structural maximization requirement (requiring a concave objective).

#### **Step 3: Check Curvature of Linear Constraints ($g_1, g_3, g_4$)**
*   $g_1(x_1, x_2) = x_1 + x_2 - 3 \implies$ Purely Linear $\implies$ **Convex**
*   $g_3(x_1, x_2) = -x_1 \implies$ Purely Linear $\implies$ **Convex**
*   $g_4(x_1, x_2) = -x_2 \implies$ Purely Linear $\implies$ **Convex**

#### **Step 4: Check Curvature of Nonlinear Constraint ($g_2$)**
Calculate the second-order partial derivatives of $g_2(x_1, x_2) = x_1 x_2 - 1$:
*   $\frac{\partial g_2}{\partial x_1} = x_2 \implies \frac{\partial^2 g_2}{\partial x_1^2} = 0$
*   $\frac{\partial g_2}{\partial x_2} = x_1 \implies \frac{\partial^2 g_2}{\partial x_2^2} = 0$
*   Cross partials: $\frac{\partial^2 g_2}{\partial x_1 \partial x_2} = \frac{\partial^2 g_2}{\partial x_2 \partial x_1} = 1$

Construct the Hessian Matrix ($\nabla^2 g_2$):
$$\nabla^2 g_2 = \begin{pmatrix} 0 & 1 \\ 1 & 0 \end{pmatrix}$$

#### **Step 5: Evaluate Hessian Definiteness via Minors**
*   **Order $1 \times 1$ minors:** The diagonal elements are $0, 0 \ge 0$.
*   **Order $2 \times 2$ minor (Full Determinant):**
    $$\text{det}(\nabla^2 g_2) = (0 \times 0) - (1 \times 1) = 0 - 1 = -1$$

#### **Conclusion for Problem (P2):**
Because the $2 \times 2$ principal minor determinant is strictly negative ($-1$), the Hessian matrix $\nabla^2 g_2$ is **indefinite**. This proves that $g_2$ is **NOT a convex function**. Because one of the inner constraints forms a non-convex space boundary, **Problem (P2) is NOT a Convex Programming Problem**.

---

## 4. Textual Graph: Convex vs. Non-Convex Sets Geometry

The ASCII visualization below details why a non-convex boundary function like $g_2 = x_1 x_2 - 1 \le 0$ disrupts optimization algorithms by bending the allowed domain shape inward, creating local traps:

```text
    [ CONVEX FEASIBLE REGION (P1) ]           [ NON-CONVEX FEASIBLE REGION (P2) ]
          
          ┌─────────────────┐                           * * * * * *
         /                   \                        *             *
        /     All internal    \                      *   Feasible    *
       │     points connect    │                     *    Region     *
        \    inside the set.  /                       *             *
         \                   /                         *   ┌───┐   * ◄── [Non-Convex
          └─────────────────┘                            * *   * *      Bending Trap]
```
# Convex Optimization: Convex Feasible Sets & Problem Geometry


## 1. Concept Name: Convex Feasible Sets from Convex Constraints

### Simple Meaning
A **Feasible Set** is the collection of all coordinate points that satisfy every constraint of an optimization problem simultaneously. A **Convex Set** is a region where, if you pick any two internal points, the straight line connecting them stays completely inside the region.

The main theorem tells us that if every single constraint boundary function $g_i(x)$ is **convex** (curves upward), then the resulting intersection space where all $g_i(x) \le 0$ are satisfied is guaranteed to be a perfectly **convex set**. This structural property prevents the shape from bending inward and creating multiple local trap scenarios.

---

## 2. Mathematical Theorem & Proof Breakdown

### Theorem Statement
Let $g_i$ for each $i = 1, 2, \dots, m$ be a convex function. Then, the feasible region defined by:
$$S = \{x \in \mathbb{R}^n : g_i(x) \le 0; \ i = 1, 2, \dots, m\}$$
is a **convex set**.

### Step-by-Step Proof
1. **Setup:** Let $x_1, x_2 \in S$ be any two points belonging to the feasible region. By definition of the set $S$, this implies:
   $$g_i(x_1) \le 0 \quad \forall i \quad \text{and} \quad g_i(x_2) \le 0 \quad \forall i \quad \text{---}$$

2. **Construct the Line Segment Point ($z$):** Pick a point $z$ lying on the straight line segment between $x_1$ and $x_2$ using a weight scalar $\lambda \in [0, 1]$:
   $$z = \lambda x_1 + (1 - \lambda) x_2 \quad \text{---}$$

3. **Apply the Property of Convex Functions:** Evaluate the constraint functions at this new point $z$. Because $g_i$ is a convex function, it must satisfy the definition of convexity:
   $$g_i(z) = g_i(\lambda x_1 + (1 - \lambda) x_2) \le \lambda g_i(x_1) + (1 - \lambda) g_i(x_2) \quad \text{---}$$

4. **Substitute the Boundary Limits:** Since $g_i(x_1) \le 0$ and $g_i(x_2) \le 0$, we can substitute their upper limits ($0$) to check the maximum possible value for $g_i(z)$:
   $$g_i(z) \le \lambda \times 0 + (1 - \lambda) \times 0 = 0 \quad \text{---}$$
   $$g_i(z) \le 0 \quad \text{for any index } i \quad \text{---}$$

5. **Conclusion:** Since $z$ satisfies all structural boundary constraints ($g_i(z) \le 0$), it must belong to the feasible region ($z \in S$). Therefore, **$S$ is a convex set on $\mathbb{R}^n$**.

---

## 3. Solved Problems with Step-by-Step Calculations

### 📝 Problem 1: Analyzing Optimization Problem (P2)
Determine whether the following problem is a Convex Programming Problem (CPP) and evaluate its structural parts:
$$\text{Maximize } f(x_1, x_2) = 2x_1 - x_2 \quad \text{---}$$
$$\text{subject to: } \begin{cases} x_1 + x_2 \le 3 \\ x_1 x_2 \le 1 \\ x_1, x_2 \ge 0 \end{cases} \quad \text{---}$$

#### **Step 1: Convert to Standard $\le 0$ Inequality Form**
*   Objective function: $f(x_1, x_2) = 2x_1 - x_2$ (Linear, meaning it acts as both **convex & concave**)
*   Constraint 1: $x_1 + x_2 - 3 \le 0 \implies g_1(x_1, x_2) = x_1 + x_2 - 3$ (Linear $\implies$ **Convex**)
*   Constraint 2: $x_1 x_2 - 1 \le 0 \implies g_2(x_1, x_2) = x_1 x_2 - 1$
*   Boundary signs: $-x_1 \le 0$ ($g_3$ is **convex**) and $-x_2 \le 0$ ($g_4$ is **convex**).

#### **Step 2: Calculate Curvature of the Nonlinear Constraint ($g_2$)**
Compute the Hessian matrix of $g_2(x_1, x_2) = x_1 x_2 - 1$ using partial derivatives:
*   $\frac{\partial g_2}{\partial x_1} = x_2 \implies \frac{\partial^2 g_2}{\partial x_1^2} = 0 \quad \text{---}$
*   $\frac{\partial g_2}{\partial x_2} = x_1 \implies \frac{\partial^2 g_2}{\partial x_2^2} = 0 \quad \text{---}$
*   Cross derivatives: $\frac{\partial^2 g_2}{\partial x_1 \partial x_2} = \frac{\partial^2 g_2}{\partial x_2 \partial x_1} = 1 \quad \text{---}$

Assemble the Hessian Matrix ($\nabla^2 g_2$):
$$\nabla^2 g_2 = \begin{pmatrix} 0 & 1 \\ 1 & 0 \end{pmatrix} \quad \text{---}$$

#### **Step 3: Test Definiteness via Minors**
*   **Order $1 \times 1$ minors (Diagonal elements):** $0, 0 \ge 0 \quad \text{---}$
*   **Order $2 \times 2$ minor (Full Determinant):**
    $$\text{det}(\nabla^2 g_2) = (0 \times 0) - (1 \times 1) = 0 - 1 = -1 \quad \text{---}$$

#### **Conclusion:**
Because the order $2 \times 2$ minor evaluates to a negative value ($-1$), the Hessian is **indefinite**. Therefore, $g_2$ is **NOT convex**. Since one of the constraint functions bounding the space fails the convexity requirement, the region is not a convex set, confirming that **Problem (P2) is NOT a Convex Programming Problem**.

---

### 📝 Problem 2: Verifying a Convex Set
Show that the constraint set $S = \{x \in \mathbb{R} : x^2 - 9 \le 0\}$ forms a convex set.

#### **Step 1: Check the Curvature of $g(x)$**
The constraint function is $g(x) = x^2 - 9$. Let's take its derivatives:
*   $g'(x) = 2x$
*   $g''(x) = 2$

#### **Step 2: Evaluate the Sign of the Second Derivative**
Since $g''(x) = 2 > 0$ for all real values of $x$, the function is strictly **convex**.

#### **Conclusion:**
According to our theorem, because the inequality is written in the form $g(x) \le 0$ and $g(x)$ is a proven convex function, the resulting set $S = [-3, 3]$ is fundamentally a **convex set**.

---

## 4. Visualizing Feasible Region Geometry

The text graph below shows how a convex constraint boundary forms an orderly, easy-to-solve set, while a non-convex constraint boundary warps the region into an irregular shape:

```text
    [ CONVEX REGION SET ]               [ NON-CONVEX BOUNDARY SET ]
      (Valid CPP Shape)                       (Invalid CPP Shape)
      
         ┌──────────┐                            * * * * *
        /            \                         *           *
       /   Feasible   \                       *   Feasible  *
      │     Valid      │                      *    Region    *
       \    Region    /                        *            *
        \            /                           *   ┌────┐*  ◄── [Inward Dent Trap]
         └──────────┘                             * *     *
                                                  
 Straight lines between any two internal    A line connecting two valid inside points 
 points stay completely inside the set.     cuts outside the set due to the bent wall!

```

# Convex Optimization: Quadratic Programming Problems (QPP)

## 1. Concept Name: Quadratic Programming Problem (QPP) Formulation

### Simple Meaning
A **Quadratic Programming Problem (QPP)** is a special kind of optimization problem where the target goal (the objective function) contains squared variables or variables multiplied by each other (quadratic terms), while all the rules or boundaries (the constraints) are purely linear equations (straight lines or planes).

---

## 2. Standard Mathematical Representation

The general form of a Quadratic Programming Problem is represented in vector-matrix notation as follows:

$$\begin{array}{|c|}
\hline
\text{Minimize } f(x) = c^T x + \frac{1}{2}x^T Qx \\
\text{subject to (s/t) } Ax \le b \\
x \ge 0 \\
\hline
\end{array}$$

### Component Breakdown:
*   $x \in \mathbb{R}^n$: The column vector containing our $n$ decision variables.
*   $c \in \mathbb{R}^n$: A vector of linear coefficients, making $c^T x$ the linear part of our objective function.
*   $Q \in \mathbb{R}^{n \times n}$: A **symmetric matrix** ($Q = Q^T$) containing the quadratic coefficients.
*   $A \in \mathbb{R}^{m \times n}$: The structural coefficient matrix for the linear constraints.
*   $b \in \mathbb{R}^m$: The right-hand side limit vector for the linear constraints.

---

## 3. Step-by-Step Problem Breakdown & Matrix Extraction

### 📝 Problem 1 (From Slide)
Convert the following algebraic formulation of a QPP into its standard matrix representation:
$$\text{Minimize } f(x_1, x_2) = 2x_1^2 - x_1 x_2 + 4x_2^2 + 6x_1 + 8x_2$$
$$\text{subject to } 3x_1 + 2x_2 \le 6$$
$$x_1, x_2 \ge 0$$

---

### 🔎 Step-by-Step Matrix Calculation Workflow

#### **Step 1: Set up the Decision Vector ($x$)**
We group our independent variables into a column vector:
$$x = \begin{pmatrix} x_1 \\ x_2 \end{pmatrix} \implies x^T = \begin{pmatrix} x_1 & x_2 \end{pmatrix}$$

#### **Step 2: Extract the Linear Coefficient Vector ($c^T$)**
Isolate the purely linear terms from the objective function ($6x_1 + 8x_2$):
$$c^T = \begin{pmatrix} 6 & 8 \end{pmatrix}$$

#### **Step 3: Construct the Symmetric Quadratic Matrix ($Q$)**
The objective function contains the quadratic terms $2x_1^2 - x_1 x_2 + 4x_2^2$. In the standard formula, this part equals $\frac{1}{2}x^T Qx$. To reverse-engineer $Q$, we use these rules:
1.  **Diagonal Elements ($Q_{ii}$):** Multiply the squared term coefficients by **2** to cancel out the $\frac{1}{2}$ multiplier in the formula:
    *   $Q_{11} = 2 \times 2 = 4$
    *   $Q_{22} = 4 \times 2 = 8$
2.  **Off-Diagonal Elements ($Q_{ij}$):** Split the interaction coefficient ($-1$ from $-x_1x_2$) equally across the symmetric slots ($Q_{12}$ and $Q_{21}$):
    *   $Q_{12} = Q_{21} = \frac{-1}{2} \times 2 = -1$

$$Q = \begin{pmatrix} 4 & -1 \\ -1 & 8 \end{pmatrix}$$

*Verification:*
$$\frac{1}{2} \begin{pmatrix} x_1 & x_2 \end{pmatrix} \begin{pmatrix} 4 & -1 \\ -1 & 8 \end{pmatrix} \begin{pmatrix} x_1 \\ x_2 \end{pmatrix} = \frac{1}{2} \begin{pmatrix} x_1 & x_2 \end{pmatrix} \begin{pmatrix} 4x_1 - x_2 \\ -x_1 + 8x_2 \end{pmatrix}$$
$$= \frac{1}{2} (4x_1^2 - x_1 x_2 - x_2 x_1 + 8x_2^2) = 2x_1^2 - x_1 x_2 + 4x_2^2 \quad \text{(Correct! Validates ✅)}$$

#### **Step 4: Extract Constraint Matrix ($A$) and Boundary Vector ($b$)**
Extract the parameters from the constraint inequality $3x_1 + 2x_2 \le 6$:
$$A = \begin{pmatrix} 3 & 2 \end{pmatrix}, \quad b = \begin{pmatrix} 6 \end{pmatrix}$$

#### **Final Standard Form Result:**
$$\text{Min } f = \frac{1}{2}\begin{pmatrix} x_1 & x_2 \end{pmatrix}\begin{pmatrix} 4 & -1 \\ -1 & 8 \end{pmatrix}\begin{pmatrix} x_1 \\ x_2 \end{pmatrix} + \begin{pmatrix} 6 & 8 \end{pmatrix}\begin{pmatrix} x_1 \\ x_2 \end{pmatrix}$$
$$\text{s/t } \begin{pmatrix} 3 & 2 \end{pmatrix}\begin{pmatrix} x_1 \\ x_2 \end{pmatrix} \le \begin{pmatrix} 6 \end{pmatrix}, \quad \begin{pmatrix} x_1 \\ x_2 \end{pmatrix} \ge \begin{pmatrix} 0 \\ 0 \end{pmatrix}$$

---

## 4. Additional Solved Practice Problem

### 📝 Problem 2
Convert the following formulation into standard QPP matrix form:
$$\text{Minimize } f(x_1, x_2) = x_1^2 + 4x_1 x_2 + 5x_2^2 - 3x_1$$
$$\text{subject to } \begin{cases} 2x_1 + x_2 \le 4 \\ x_1 + 3x_2 \le 9 \end{cases}$$
$$x_1, x_2 \ge 0$$

#### **Step 1: Extract Linear Terms**
The linear term is $-3x_1 + 0x_2$. Thus:
$$c^T = \begin{pmatrix} -3 & 0 \end{pmatrix}$$

#### **Step 2: Construct Quadratic Matrix ($Q$)**
*   Diagonal terms: $Q_{11} = 1 \times 2 = 2$, $Q_{22} = 5 \times 2 = 10$.
*   Off-diagonal terms: The $x_1 x_2$ coefficient is $4$. Split it equally: $Q_{12} = Q_{21} = 2$.
$$Q = \begin{pmatrix} 2 & 2 \\ 2 & 10 \end{pmatrix}$$

#### **Step 3: Extract Constraint Components**
Gather the row parameters from the system of linear inequalities:
$$A = \begin{pmatrix} 2 & 1 \\ 1 & 3 \end{pmatrix}, \quad b = \begin{pmatrix} 4 \\ 9 \end{pmatrix}$$

---

## 5. Visualizing the Geometric Concept of a QPP

This ASCII visualization shows the unique structure of a QPP—optimizing a curved, paraboloid objective space within a flat-sided polygon boundary:

```text
       ▲ f(x) [Objective Value Dimension]
       │
       │         *               *      ◄── Curved Quadratic Surface
       │          *             *           (Shape governed by Matrix Q)
       │           *           *
───────┼────────────*─────────*─────────► Variable Domain Space (x)
       │             *       *
       │            ┌─────────┐
       │            │░░░░░░░░░│         ◄── Flat-Sided Linear Feasible Region
       │            │░░░░░░░░░│             (Boundaries governed by Ax ≤ b)
       │            └─────────┘
```

# Convex Quadratic Programming Problems & Definiteness Proofs

## 1. Concept Name: Convex Quadratic Programming Problem (QPP) Condition

### Simple Meaning
A **Quadratic Programming Problem (QPP)** optimizes a quadratic objective function subject to linear constraints. A QPP is structurally a **Convex Programming Problem** if and only if the matrix $Q$ representing its second-order quadratic terms curves strictly upward or remains flat across the entire space. This requirement translates to $Q$ being a **symmetric positive semi-definite matrix**. When this condition holds, any local minimum found by an optimization algorithm is automatically guaranteed to be the absolute lowest global minimum point.

---

## 2. Core Proofs and Lemmas

### A. Quadratic Inequality Lemma
> **Lemma:** Let $M$ be a symmetric positive semi-definite matrix of order $n$. Then, for any vectors $x, y \in \mathbb{R}^n$:
> $$x^T My \le \frac{1}{2}[x^T Mx + y^T My]$$

#### **Step-by-Step Proof Derivation:**
1. **Apply Definition of Positive Semi-Definiteness:** Because $M$ is positive semi-definite, multiplying it by any vector on both sides must yield a non-negative result. Let's choose the difference vector $(x - y)$:
   $$(x - y)^T M (x - y) \ge 0$$

2. **Expand the Vector Product Expressions:**
   $$(x^T - y^T) M (x - y) \ge 0$$
   $$x^T Mx + y^T My - x^T My - y^T Mx \ge 0$$

3. **Utilize Matrix Scalar Transpose Identity:** Since $y^T Mx$ is a scalar ($1 \times 1$ matrix value), it is equal to its own transpose:
   $$y^T Mx = (y^T Mx)^T = x^T M^T (y^T)^T = x^T M^T y$$
   Because $M$ is explicitly a symmetric matrix ($M = M^T$):
   $$y^T Mx = x^T My$$

4. **Combine the Cross Terms:** Substitute $x^T My$ back into our expanded inequality equation:
   $$x^T Mx + y^T My - x^T My - x^T My \ge 0$$
   $$x^T Mx + y^T My - 2x^T My \ge 0$$

5. **Isolate the Dot Product Term:** Shift the negative term to the opposing side and multiply by $\frac{1}{2}$:
   
   $$x^T Mx + y^T My \ge 2x^T My \implies x^T My \le \frac{1}{2}\left[x^T Mx + y^T My\right] \quad \text{--- Proof Complete!}$$
---

### B. Algebraic Proof Matrix Curation for Convexity
To test a quadratic function $f(x) = c^T x + \frac{1}{2}x^T Qx$ for convexity, evaluate the standard algebraic segment:
$$f(\lambda x_1 + (1-\lambda)x_2) - \lambda f(x_1) - (1-\lambda)f(x_2)$$

After canceling the linear vector portions ($c^T x$) and expanding the matrices using the lemma above, the expression groups down to:
$$= \frac{\lambda(1-\lambda)}{2} \left[ -x_1^T Q x_1 - x_2^T Q x_2 + 2x_1^T Q x_2 \right]$$
$$= -\frac{\lambda(1-\lambda)}{2} (x_1 - x_2)^T Q (x_1 - x_2)$$

Since $\lambda \in [0, 1]$, the scalar multiplier is positive. If $Q$ is positive semi-definite, the matrix term is $\ge 0$. The overall expression becomes $\le 0$, which mathematically matches the exact definition of a **convex function**.

---

## 3. Solved Problems with Step-by-Step Calculations

### 📝 Problem 1: Dissection and Definiteness Test of Problem (QP1)
Determine if the following QPP is a valid Convex Programming Problem:
$$\text{Minimize } f(x) = x_1^2 + 2x_2^2 + 3x_3^2 + 4x_1 x_3 + 2x_2 x_3 + x_1 - x_2 + 2x_3$$
$$\text{subject to } x_1 + x_2 + x_3 \le 10, \quad x_1, x_2, x_3 \ge 0$$

#### **Step 1: Construct the Quadratic Matrix $Q$**
Extract coefficients from the quadratic portion ($x_1^2 + 2x_2^2 + 3x_3^2 + 4x_1 x_3 + 2x_2 x_3$):
* Diagonal slots ($Q_{ii}$): Multiply squared coefficients by $2$:
  $$Q_{11} = 1 \times 2 = 2, \quad Q_{22} = 2 \times 2 = 4, \quad Q_{33} = 3 \times 2 = 6$$
* Off-diagonal slots ($Q_{ij}$): Split interaction values across symmetric index pairs:
  $$Q_{13} = Q_{31} = 4, \quad Q_{23} = Q_{32} = 2, \quad Q_{12} = Q_{21} = 0$$

$$Q = \begin{pmatrix} 2 & 0 & 4 \\ 0 & 4 & 2 \\ 4 & 2 & 6 \end{pmatrix}$$

#### **Step 2: Calculate Minors of Order $1 \times 1$**
Read the entries sitting along the main diagonal:
$$D_1 = 2, \quad D_1 = 4, \quad D_1 = 6 \quad (\text{All } \ge 0)$$

#### **Step 3: Calculate Minors of Order $2 \times 2$**
Evaluate the three principal $2 \times 2$ determinants along the diagonal:
1. **Top-Left $2 \times 2$ Minor:**
   $$\begin{vmatrix} 2 & 0 \\ 0 & 4 \end{vmatrix} = (2 \times 4) - 0 = 8 \quad (\ge 0)$$
2. **Bottom-Right $2 \times 2$ Minor:**
   $$\begin{vmatrix} 4 & 2 \\ 2 & 6 \end{vmatrix} = (4 \times 6) - (2 \times 2) = 24 - 4 = 20 \quad (\ge 0)$$
3. **Outer Corner $2 \times 2$ Minor:**
   $$\begin{vmatrix} 2 & 4 \\ 4 & 6 \end{vmatrix} = (2 \times 6) - (4 \times 4) = 12 - 16 = -4 \quad (\mathbf{Negative!})$$

#### **Conclusion for (QP1):**
Because one of the $2 \times 2$ principal minors evaluates to a negative value ($-4$), the matrix $Q$ is **indefinite**. Therefore, the objective function is not convex, meaning **(QP1) is NOT a convex QPP**.

---

### 📝 Problem 2: Dissection and Definiteness Test of Problem (QP2)
Evaluate the convexity of the following programming problem:
$$\text{Minimize } f(x) = x_1^2 + 2x_2^2 - 2x_1 x_2 - 6x_1 - 8x_2$$
$$\text{subject to } 2x_1 - x_2 \le 13, \quad x_1, x_2 \ge 0$$

#### **Step 1: Construct Matrix $Q$**
* Diagonal entries: $Q_{11} = 1 \times 2 = 2$, $Q_{22} = 2 \times 2 = 4$
* Off-diagonal entries: The cross coefficient is $-2$, so we split it: $Q_{12} = Q_{21} = -1$
$$Q = \begin{pmatrix} 2 & -1 \\ -1 & 4 \end{pmatrix}$$

#### **Step 2: Test Principal Minors**
* Order $1 \times 1$ minors: $2$ and $4$ (Both are $> 0$)
* Order $2 \times 2$ minor (Determinant):
  $$\text{det}(Q) = \begin{vmatrix} 2 & -1 \\ -1 & 4 \end{vmatrix} = (2 \times 4) - (-1 \times -1) = 8 - 1 = 7 \quad (> 0)$$

#### **Conclusion for (QP2):**
Since every single principal minor is strictly greater than zero ($> 0$), matrix $Q$ is **positive definite** (which forms a subclass of positive semi-definite). Therefore, the objective function is strictly convex, confirming that **(QP2) is a valid Convex QPP**.

---

## 4. Optimization Energy Space Visualization

The text graph below models how matrix definiteness changes the geometry of your optimization problem:

```text
    [ CONVEX QPP (QP2) ]                      [ NON-CONVEX QPP (QP1) ]
     Positive Definite Q Matrix                 Indefinite Q Matrix
     
         ▲ f(x)                                     ▲ f(x)
         │                                          │      *
         │   *           *                          │    *   *     *
         │    *         *                           │   *     *   *
         │     *       *                            │  *       * *
 ────────┴───────*****───────► Variable Space ──────┴───────────*────────► Variable Space
            Global Valley Minimum                      Unstable Saddle Trap Area
            (Easy to Solve!)                           (Hard to Optimize!)