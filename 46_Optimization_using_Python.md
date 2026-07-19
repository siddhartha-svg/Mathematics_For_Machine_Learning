# Linear Programming Formulation and Computational Solution via CVXOPT

## 1. Concept Name: Linear Programming Problem (LPP) Vectorization & Computational Solution via CVXOPT

### Simple Meaning
A **Linear Programming Problem (LPP)** is an optimization problem where both the objective function and the constraints are purely linear expressions. To solve an LPP computationally using advanced Python libraries like **CVXOPT** (a library tailored for convex optimization), the problem must be converted from standard algebraic equations into standard matrix-vector structures. 

The CVXOPT standard library solver requires inequality constraints to be in a less-than-or-equal-to form ($Ax \le b$). Therefore, any greater-than-or-equal-to constraint ($\ge$) must be multiplied by $-1$ to flip its inequality sign before loading it into the program.

---

## 2. Standard Mathematical and Computational Matrix Formats

The canonical standard matrix format expected by the CVXOPT linear programming solver `solvers.lp(c, A, b)` is structured as follows:

$$\begin{array}{|c|}
\hline
\text{Minimize } Z = c^T x \\
\text{subject to (s/t) } Ax \le b \\
\hline
\end{array}$$


### Critical Python Syntax Note:
When defining standard matrices in CVXOPT using `matrix([[...], [...]])`, the list of values inside the brackets represents **columns**, not rows. 
*   `matrix([[row1_col1, row2_col1], [row1_col2, row2_col2]])` converts directly to an entry pattern where each sub-list populates a single vertical matrix column.

---

## 3. Detailed Step-by-Step Problem Calculations and Vectorization

### 📝 Problem 1 (From Slides)
Convert the following algebraic LPP into vectorized matrices and program it via CVXOPT to find the optimal solution:
$$\text{Minimize } Z = 2x_1 + 3x_2$$
$$\text{subject to: } \begin{cases} x_1 + x_2 \ge 2 \\ 2x_1 + 3x_2 \le 12 \\ x_1 \ge 0 \\ x_2 \ge 0 \end{cases}$$

#### **Step 1: Convert all inequalities to the standard $\le$ form**
*   Constraint 1: $x_1 + x_2 \ge 2 \implies \mathbf{-x_1 - x_2 \le -2}$
*   Constraint 2: $2x_1 + 3x_2 \le 12 \implies \mathbf{2x_1 + 3x_2 \le 12}$
*   Constraint 3 (Sign Bound): $x_1 \ge 0 \implies \mathbf{-x_1 \le 0}$
*   Constraint 4 (Sign Bound): $x_2 \ge 0 \implies \mathbf{-x_2 \le 0}$

#### **Step 2: Isolate the Objective Coefficient Vector ($c$)**
$$Z = \begin{pmatrix} 2 & 3 \end{pmatrix} \begin{pmatrix} x_1 \\ x_2 \end{pmatrix} \implies c = \begin{pmatrix} 2 \\ 3 \end{pmatrix}$$

#### **Step 3: Extract the Structural Matrix $A$ and Resource Vector $b$**
Group the coefficients left over from Step 1 into row alignments:
$$A = \begin{pmatrix} -1 & -1 \\ 2 & 3 \\ -1 & 0 \\ 0 & -1 \end{pmatrix}, \quad b = \begin{pmatrix} -2 \\ 12 \\ 0 \\ 0 \end{pmatrix}$$

#### **Step 4: Transpose Matrix $A$ into Column Layouts for Python Coding**
To construct $A$ properly using CVXOPT column definitions, we transpose it:
*   Column 1 values (for $x_1$ entries): `[-1.0, 2.0, -1.0, 0.0]`
*   Column 2 values (for $x_2$ entries): `[-1.0, 3.0, 0.0, -1.0]`

---

### 💻 Python Code Script for Problem 1

```python
from cvxopt import matrix, solvers

# Define the coefficients of the objective function (c)
c = matrix([2.0, 3.0])

# Define the constraint matrix A (Pass as columns)
A = matrix([[-1.0, 2.0, -1.0, 0.0], 
            [-1.0, 3.0, 0.0, -1.0]])

# Define the right hand side vector b
b = matrix([-2.0, 12.0, 0.0, 0.0])

# Execute the linear programming solver
sol = solvers.lp(c, A, b)

# Display the optimal coordinate vector point
print("Optimal Solution Point:")
print(sol['x'])

```

#### **Execution Logs & Solution Output Analysis:**

The algorithm resolves the interior-point method steps inside 5 iterations:

* `Iteration 0`: Primal cost `1.0471e+01`, Dual cost `-7.7647e+00`
* `Iteration 5`: Primal cost `4.0000e+00`, Dual cost `4.0000e+00`

**Output results printed from `sol['x']`:**


$$x_1 = 2.00\text{, } \quad x_2 = 5.38 \times 10^{-7} \approx 0$$

$$\text{Optimal Minimum Value: } Z = 2(2) + 3(0) = 4$$

---

## 4. Alternate Practice Problem with Strict Iteration Limits

### 📝 Problem 2

Formulate and solve a problem where we restrict the interior point engine to stop exactly at 3 iterations using the `options` parameter dictionary flag.


$$\text{Minimize } Z = 5x_1 + 4x_2$$

$$\text{subject to: } \begin{cases} x_1 + 2x_2 \ge 3 \implies -x_1 - 2x_2 \le -3 \\ x_1, x_2 \ge 0 \implies -x_1 \le 0, \ -x_2 \le 0 \end{cases}$$

#### **Vector Extraction:**

$$c = \begin{pmatrix} 5 \\ 4 \end{pmatrix}, \quad A = \begin{pmatrix} -1 & -2 \\ -1 & 0 \\ 0 & -1 \end{pmatrix} \implies A^T = \begin{pmatrix} -1 & -1 & 0 \\ -2 & 0 & -1 \end{pmatrix}, \quad b = \begin{pmatrix} -3 \\ 0 \\ 0 \end{pmatrix}$$

```python
from cvxopt import matrix, solvers

c = matrix([5.0, 4.0])
A = matrix([[-1.0, -1.0, 0.0], 
            [-2.0, 0.0, -1.0]])
b = matrix([-3.0, 0.0, 0.0])

# Enforce loop termination at exactly 3 iterations
solvers.options['maxiters'] = 3
sol = solvers.lp(c, A, b)

print(sol['x'])

```

*Output Log Notice:* Program alerts user with message `Terminated (maximum number of iterations reached)` if it does not find the final minimum point before hitting iteration 3.

---

## 5. Geometric Visualization of the Constrained Search Space

The ASCII chart below maps the valid geometry space for Problem 1, showcasing the corner vector trajectories searched by CVXOPT:

```text
       x₂ ▲
          │   \ Boundary 2: 2x₁ + 3x₂ = 12
        4 ┼────\───.
          │░░░░░\    \
          │░░░░░░\    \
        2 ┼─●░░░░░\    \     ◄── Feasible Domain (Ax ≤ b Area)
          │▒▒\ ░░░░\    \
          │▒▒▒\ ░░░░\    \
   ───────┴────●─────┴────●─────────► x₁
          0    2     4    6
                ▲
                 \ Boundary 1: x₁ + x₂ = 2
                   The optimal solution lands on corner coordinate (2,0)

```
# Quadratic Programming Formulation and Computational Solution via CVXOPT

## 1. Concept Name: Quadratic Programming Problem (QPP) Matrix Vectorization

### Simple Meaning
A **Quadratic Programming Problem (QPP)** is an optimization setup where the target goal (the objective function) contains quadratic terms (variables squared or multiplied together), while all its operational restrictions (the constraints) are strictly linear expressions.

To pass a QPP into Python's computational convex optimization engine (**CVXOPT**), we must extract and translate our algebraic formulas into standard matrices and vectors. 

---

## 2. Canonical CVXOPT Matrix Structure

The CVXOPT quadratic programming module `solvers.qp(P, q, G, h, A, b)` requires all data parameters to perfectly match the following standard matrix framework:

$$\begin{array}{|rl|}
\hline
\text{Minimize} & \frac{1}{2}x^T P x + q^T x \\
\text{subject to} & Gx \le h \\
& Ax = b \\
\hline
\end{array}$$

### Structural Definitions:
*   $P$: Symmetric matrix containing the coefficients of the quadratic objective terms.
*   $q$: Vector containing the coefficients of the linear objective terms.
*   $G$: Matrix tracking the coefficients of the **inequality** boundaries ($Gx \le h$).
*   $h$: Right-hand side capacity vector for the **inequality** constraints.
*   $A$: Matrix tracking the coefficients of the **equality** boundaries ($Ax = b$).
*   $b$: Right-hand side target vector for the **equality** constraints.

> ⚠️ **Important Code Syntax Rule:** When creating standard multi-dimensional structures using CVXOPT's `matrix([[...], [...]])` constructor, array entries are parsed **column-by-column**, rather than row-by-row.

---

## 3. Step-by-Step Problem Deconstruction & Calculations

### 📝 Problem 1 (From Slides)
Convert the following algebraic QPP into vectorized matrices and compute its solution via CVXOPT:
$$\text{Minimize } f(x_1, x_2) = x_1^2 + x_1 x_2 + 2x_2^2 + 3x_1 + 4x_2$$
$$\text{subject to: } \begin{cases} 2x_1 + x_2 = 1 \\ x_1 \ge 0 \\ x_2 \ge 0 \end{cases}$$

---

### 🔎 Step-by-Step Parameter Calculations

#### **Step 1: Deconstruct the Quadratic Objective Terms into Matrix $P$**
The quadratic portion is $x_1^2 + x_1 x_2 + 2x_2^2$. In the standard formula, this equates to $\frac{1}{2}x^T P x$. To reverse-engineer $P$, we match indices and scale coefficients by **2** to neutralize the $\frac{1}{2}$ multiplier:
*   **Diagonal elements ($P_{ii}$):** 
    *   $P_{11} = 1 \times 2 = 2$
    *   $P_{22} = 2 \times 2 = 4$
*   **Off-diagonal elements ($P_{ij}$):** Split the interaction coefficient ($1$ from $+1x_1x_2$) evenly across symmetric cells:
    *   $P_{12} = P_{21} = \frac{1}{2} \times 2 = 1$

$$P = \begin{pmatrix} 2 & 1 \\ 1 & 4 \end{pmatrix} \quad \text{}$$

#### **Step 2: Isolate the Linear Objective Vector ($q$)**
Collect the coefficients of the purely first-degree linear variables ($3x_1 + 4x_2$):
$$q^T = \begin{pmatrix} 3 & 4 \end{pmatrix} \implies q = \begin{pmatrix} 3 \\ 4 \end{pmatrix} \quad \text{}$$

#### **Step 3: Convert the Greater-Than Inequalities into Standard $\le$ Format**
CVXOPT strictly requires inequality limits to face a less-than-or-equal-to ($\le$) direction:
*   $x_1 \ge 0 \implies \mathbf{-x_1 \le 0}$
*   $x_2 \ge 0 \implies \mathbf{-x_2 \le 0}$

From this, extract inequality parameters $G$ and $h$:
$$G = \begin{pmatrix} -1 & 0 \\ 0 & -1 \end{pmatrix}, \quad h = \begin{pmatrix} 0 \\ 0 \end{pmatrix} \quad \text{}$$

#### **Step 4: Vectorize the Linear Equality Constraint ($Ax = b$)**
Isolate the structural parameters from $2x_1 + x_2 = 1$:
$$A = \begin{pmatrix} 2 & 1 \end{pmatrix}, \quad b = \begin{pmatrix} 1 \end{pmatrix} \quad \text{}$$

---

### 💻 Python Optimization Script

```python
from cvxopt import matrix, solvers

# 1. Quadratic Objective Terms (Passed column by column)
P = matrix([[2.0, 1.0], 
            [1.0, 4.0]])

# 2. Linear Objective Terms
q = matrix([3.0, 4.0])

# 3. Inequality Constraints (G x <= h)
G = matrix([[-1.0, 0.0], 
            [0.0, -1.0]])
h = matrix([0.0, 0.0])

# 4. Equality Constraints (A x = b)
A = matrix([[2.0], 
            [1.0]])
b = matrix([1.0])

# Execute CVXOPT Quadratic Programming Solver
sol = solvers.qp(P, q, G, h, A, b)

# Print the resulting optimal solution vector
print("Optimal Coordinate Vectors:")
print(sol['x'])