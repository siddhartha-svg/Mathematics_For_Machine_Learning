# Linear Algebra Notes: Overdetermined and Underdetermined Systems

This note covers the definition, structural characteristics, and solution types of **Overdetermined** and **Underdetermined** systems of linear equations.

---

## 1. Core Framework: Matrix Notation of Linear Systems

Any system of linear equations can be compactly represented using the standard matrix framework:

$$AX = b$$

Where:
* **$A_{m \times n}$**: The **Coefficient Matrix** containing the numerical scaling weights.
* **$X \in \mathbb{R}^n$**: The **Unknown Vector** ($n \times 1$) containing the variables we want to solve for.
* **$b \in \mathbb{R}^m$**: The **Right-Hand Vector** ($m \times 1$) containing the target constraint values.

Here, **$m$** represents the number of equations (or observations) and **$n$** represents the number of unknown variables.

---

## 2. Overdetermined Systems ($m \gg n$)

### Simple Meaning 💡
An overdetermined system has **more equations (observations) than unknown variables**. Think of it as having too many constraints. Because you have more rules than variables, it is usually impossible to satisfy every single equation perfectly. Therefore, these systems typically have **no exact solution**. Instead, data scientists look for an **approximate solution** (like a least-squares fit) that comes as close as possible.


### Visualized Numerical Example
Consider the system from the slide:
$$x_1 + 2x_2 = 5$$
$$x_1 - x_2 = 1$$
$$3x_1 + 4x_2 = 7$$
$$x_1 + 5x_2 = 9$$

Here, we have $m = 4$ equations and $n = 2$ unknowns ($x_1, x_2$). Since $4 > 2$, the system is overdetermined.

#### Setting up the Matrices:
$$A = \begin{bmatrix} 1 & 2 \\ 1 & -1 \\ 3 & 4 \\ 1 & 5 \end{bmatrix}_{4 \times 2}, \quad X = \begin{bmatrix} x_1 \\ x_2 \end{bmatrix}_{2 \times 1}, \quad b = \begin{bmatrix} 5 \\ 1 \\ 7 \\ 9 \end{bmatrix}_{4 \times 1}$$

#### Testing for an Exact Solution:
Let's see if an exact solution exists by solving the first two equations:
1. $x_1 - x_2 = 1 \implies x_1 = x_2 + 1$
2. Substitute into the first equation: $(x_2 + 1) + 2x_2 = 5 \implies 3x_2 = 4 \implies x_2 = \frac{4}{3}$
3. Find $x_1$: $x_1 = \frac{4}{3} + 1 = \frac{7}{3}$

Now, test if this candidate solution $\left(\frac{7}{3}, \frac{4}{3}\right)$ satisfies the third equation:
$$3\left(\frac{7}{3}\right) + 4\left(\frac{4}{3}\right) = 7 + \frac{16}{3} = \frac{37}{3} \neq 7$$

Because the third equation fails, there is **no exact solution**. We must settle for an **approximate solution** that minimizes the overall error across all four lines.

---

## 3. Underdetermined Systems ($m \ll n$)

### Simple Meaning 💡
An underdetermined system has **fewer equations (observations) than unknown variables**. Think of it as not having enough constraints or clues. Because you have more freedom than restrictions, if the equations don't contradict each other, you will end up with **infinitely many solutions**. You can choose arbitrary values for some variables (free variables) and compute the others based on that choice.


### Visualized Numerical Example
*(Note: The handwritten header on the third slide says "Undetermined", which is a common alternative shorthand for **Underdetermined**).*

Consider the system from the slide:
$$x_1 + x_2 - x_3 = 2$$
$$2x_1 + x_2 + x_3 = 4$$

Here, we have $m = 2$ equations and $n = 3$ unknowns ($x_1, x_2, x_3$). Since $2 < 3$, the system is underdetermined.

#### Setting up the Matrices:
$$A = \begin{bmatrix} 1 & 1 & -1 \\ 2 & 1 & 1 \end{bmatrix}_{2 \times 3}, \quad X = \begin{bmatrix} x_1 \\ x_2 \\ x_3 \end{bmatrix}_{3 \times 1}, \quad b = \begin{bmatrix} 2 \\ 4 \end{bmatrix}_{2 \times 1}$$

#### Calculating an Infinite Solution Family:
Let's find the general solution by treating $x_3$ as a free parameter ($x_3 = t$):
1. $x_1 + x_2 = 2 + t$
2. $2x_1 + x_2 = 4 - t$

Subtract the first equation from the second equation to eliminate $x_2$:
$$(2x_1 + x_2) - (x_1 + x_2) = (4 - t) - (2 + t)$$
$$x_1 = 2 - 2t$$

Now, substitute $x_1$ back to isolate $x_2$:
$$(2 - 2t) + x_2 = 2 + t \implies x_2 = 3t$$

#### The Final Parametric Solution Vector:
$$X = \begin{bmatrix} 2 - 2t \\ 3t \\ t \end{bmatrix} \quad \text{for any real number } t$$

* If $t = 0 \implies X = \begin{bmatrix} 2 \\ 0 \\ 0 \end{bmatrix}$ (Valid Solution)
* If $t = 1 \implies X = \begin{bmatrix} 0 \\ 3 \\ 1 \end{bmatrix}$ (Another Valid Solution)

This confirms that the system has infinitely many valid solutions along a continuous line in 3D space.

---

## 4. Supplementary Practice Problems with Solutions

### Problem 1: Structural System Classification
**Scenario:** Determine whether the following linear systems are overdetermined or underdetermined based on their dimensions:
1. A system tracking 5 features across 100 data observations.
2. A sensor network where 8 positional coordinates must be solved using 3 receiver equations.

#### Solution Calculation & Logic:
1. Observations ($m = 100$), Variables ($n = 5$). Since $m > n$, this is an **Overdetermined System**.
2. Observations ($m = 3$), Variables ($n = 8$). Since $m < n$, this is an **Underdetermined System**.

---

### Problem 2: Finding the Exact Solvability Criterion for an Overdetermined System
**Scenario:** For what specific value of $k$ does the following overdetermined system have an **exact solution**?
$$x_1 = 2$$
$$x_2 = 3$$
$$2x_1 + 2x_2 = k$$

#### Step-by-Step Calculation:
1. The first two equations give an immediate candidate solution: $x_1 = 2, x_2 = 3$.
2. Substitute these values into the third constraint equation to find the value of $k$ that prevents a contradiction:
   $$2(2) + 2(3) = k$$
   $$4 + 6 = k \implies k = 10$$

#### Solution Conclusion:
* If **$k = 10$**, the system is consistent and yields exactly **1 unique solution**.
* If **$k \neq 10$** (e.g., $k=12$), the equations contradict each other, resulting in **no exact solution**.

# Linear Algebra & Statistics Notes: Least Squares Approximation (Linear Regression)

This note covers the geometrical concept of line fitting, the definition of residues, and the optimization math used to solve overdetermined systems via Least Squares Approximation.

---

## 1. Concept Name: Linear Regression (Line Fitting)

### Simple Meaning 💡
Imagine you collect real-world data points (like tracking how a customer's `Monthly Charges` increase the longer their `Tenure` lasts). When you plot these points on a graph, they don't form a perfectly straight line because real-world data contains noise and minor variations. 

Since no single straight line can pass through every point, our goal is to find the **best-fitting line**. This process is called **Linear Regression**, and the resulting line is known as the **regression line** or **least squares line**.


### Core Structural Element: The Residual ($e_i$)
A **residual** is the vertical directed distance between an actual observed data point on your scatter plot and the corresponding predicted point on your model's trend line.

$$\text{Residual } (e_i) = \text{Observed Value } (y_i) - \text{Predicted Value } (\hat{y}_i)$$

* To get the "absolute best" line, we cannot simply minimize the raw sum of residuals because positive and negative errors would cancel each other out.
* Instead, our optimization objective is to **minimize the sum of the squared residuals**. This is why the technique is called the method of least squares.

---

## 2. Concept Name: Least Squares Matrix Approximation

### Mathematical Formulation
When dealing with an overdetermined linear system $AX = b$ where $A \in \mathbb{R}^{m \times n}$ and $m \gg n$ (more constraints/equations than variables), an exact solution does not exist. 

To find the best possible approximate variable vector $X$, we minimize the square of the L2 norm of the residual vector, denoted as:

$$\arg\min_{X} \|AX - b\|_2^2$$

---

### Step-by-Step Optimization Derivation & Calculations

Let's look at an overdetermined system with $m = 3$ equations and $n = 2$ unknown variables ($x_1, x_2$):

$$a_{11}x_1 + a_{12}x_2 = b_1$$
$$a_{21}x_1 + a_{22}x_2 = b_2$$
$$a_{31}x_1 + a_{32}x_2 = b_3$$

#### Step 2.1: Write out the Total Squared Error Function ($E$)
We pull all terms to one side to define our individual residuals, square them, and sum them together to define our total error function $E$:

$$E = \|AX - b\|_2^2$$
$$E = (a_{11}x_1 + a_{12}x_2 - b_1)^2 + (a_{21}x_1 + a_{22}x_2 - b_2)^2 + (a_{31}x_1 + a_{32}x_2 - b_3)^2$$

#### Step 2.2: Optimize via Partial Differentiation
To find the coordinate point $(x_1, x_2)$ that minimizes the total error $E$, we take the partial derivatives with respect to each variable independently and set them to zero:

$$\frac{\partial E}{\partial x_1} = 0 \quad \text{and} \quad \frac{\partial E}{\partial x_2} = 0$$

#### Step 2.3: Compute the Derivatives
Applying the chain rule ($\frac{d}{dx}[g(x)]^2 = 2 \cdot g(x) \cdot g'(x)$) to our error function gives:

$$\frac{\partial E}{\partial x_1} = 2(a_{11}x_1 + a_{12}x_2 - b_1)a_{11} + 2(a_{21}x_1 + a_{22}x_2 - b_2)a_{21} + 2(a_{31}x_1 + a_{32}x_2 - b_3)a_{31} = 0$$

$$\frac{\partial E}{\partial x_2} = 2(a_{11}x_1 + a_{12}x_2 - b_1)a_{12} + 2(a_{21}x_1 + a_{22}x_2 - b_2)a_{22} + 2(a_{31}x_1 + a_{32}x_2 - b_3)a_{32} = 0$$

#### Step 2.4: Expressing the Normal Equation Shorthand
If you rearrange these algebraic terms back into matrix notation, it reduces to a famous system of equations known as the **Normal Equations**:

$$A^T A X = A^T b$$

Assuming $A^T A$ is invertible, we can multiply from the left to isolate our optimal variables vector:

$$X = (A^T A)^{-1} A^T b$$

---

## 3. Practice Problems with Solutions

### Problem 1: Calculating a Single Residual Value
**Scenario:** A linear regression model provides the trend line equation $\hat{y} = 2.5x + 10$. An experimental observation is recorded at the data point $(x, y) = (4, 22)$. Calculate the exact residual value for this sample.

#### Step-by-Step Calculation:
1. **Find the predicted value ($\hat{y}$):** Substitute $x = 4$ into the model equation.
   $$\hat{y} = 2.5(4) + 10 = 10 + 10 = 20$$
2. **Compute the residual ($e$):** Subtract the predicted value from the actual observed value.
   $$e = y - \hat{y} = 22 - 20 = \mathbf{+2}$$

#### Solution Conclusion:
The residual value is **$+2$**. Geometrically, this means the actual observed data point floats exactly 2 units above our fitted model line.

---

### Problem 2: Solving an Overdetermined System via Least Squares
**Scenario:** Find the optimal least squares solution vector $X = \begin{bmatrix} x \end{bmatrix}$ for the following overdetermined 1-variable system:
$$1x = 2$$
$$2x = 5$$

#### Step-by-Step Calculation:
1. **Construct the Matrices:**
   $$A = \begin{bmatrix} 1 \\ 2 \end{bmatrix}, \quad b = \begin{bmatrix} 2 \\ 5 \end{bmatrix}$$

2. **Compute the matrix product $A^T A$:**
   $$A^T A = \begin{bmatrix} 1 & 2 \end{bmatrix} \begin{bmatrix} 1 \\ 2 \end{bmatrix} = [1(1) + 2(2)] = [1 + 4] = [5]$$

3. **Compute the matrix product $A^T b$:**
   $$A^T b = \begin{bmatrix} 1 & 2 \end{bmatrix} \begin{bmatrix} 2 \\ 5 \end{bmatrix} = [1(2) + 2(5)] = [2 + 10] = [12]$$

4. **Solve the Normal Equation ($A^T A X = A^T b$):**
   $$5x = 12 \implies x = \frac{12}{5} = \mathbf{2.4}$$

#### Solution Conclusion:
The optimal least squares approximate solution is $x = 2.4$. 
* If we substitute $x = 2.4$ back into our equations, the predictions are $1(2.4) = 2.4$ and $2(2.4) = 4.8$.
* The residuals are $(2 - 2.4) = -0.4$ and $(5 - 4.8) = +0.2$. 
* The sum of squared residuals is $(-0.4)^2 + (0.2)^2 = 0.16 + 0.04 = 0.20$. Any other value for $x$ will result in a larger total error.


# Linear Algebra Notes: Pseudoinverse and Minimum Normed Solutions

This note covers the calculations for solving non-square systems of linear equations ($AX = b$) using the **Moore-Penrose Pseudoinverse ($A^+$)**. It explicitly distinguishes between **Overdetermined** systems (via Least Squares) and **Underdetermined** systems (via Minimum Normed Solutions).

---

## 1. Concept Name: The Pseudoinverse ($A^+$) and System Types

### Simple Meaning 💡
When a matrix $A$ is square and invertible, we find a single unique solution using $X = A^{-1}b$. However, if a system is rectangular (non-square), a traditional matrix inverse does not exist. 

To bridge this gap, we use a generalized proxy called the **Pseudoinverse ($A^+$)**. Depending on whether your matrix is tall or wide, the pseudoinverse takes on two distinct algebraic structures:

### Case 1: Overdetermined Systems ($m > n$) — Least Squares
* **Scenario:** More equations than variables. Usually has **no exact solution**.
* **Goal:** Find an approximate vector $X$ that minimizes the reconstruction error $\|AX - b\|_2^2$.
* **The Normal Equation Setup:** $$A^T A X = A^T b$$
  $$X = \underbrace{(A^T A)^{-1} A^T}_{A^+} b$$
* **Right Pseudoinverse:** $A^+ = (A^T A)^{-1} A^T$. Since $A$ is $m \times n$, the matrix product $A^T A$ is a smaller, invertible square matrix of size $n \times n$.

---

### Case 2: Underdetermined Systems ($m < n$) — Minimum Normed Solution (MNS)
* **Scenario:** Fewer equations than variables. This leaves you with $n - m$ free variables, yielding **infinitely many valid solutions**.
* **Goal:** Among all infinite solutions that satisfy $AX = b$ perfectly, find the specific unique vector $X$ that has the **shortest overall geometric length** (minimizing the norm $\|X\|_2$).
* **The Optimization Objective:**
  $$\min_{X} \|X\|_2^2 \quad \text{subject to } AX = b$$
* **The Solution Setup:**
  $$X = \underbrace{A^T (A A^T)^{-1}}_{A^+} b$$
* **Left Pseudoinverse:** $A^+ = A^T (A A^T)^{-1}$. Because $A$ is wide, $A^T A$ is a giant $n \times n$ matrix whose standard inverse does not exist due to rank deficiency ($\text{rank}(A^T A) \le m < n$). Instead, we invert the smaller $m \times m$ matrix product $A A^T$.

---

## 2. Step-by-Step 3x2 Overdetermined Numerical Walkthrough

### Problem Statement
Solve the following overdetermined system of $m=3$ equations and $n=2$ unknowns:
$$\begin{bmatrix} 1 & 0 \\ 1 & 1 \\ 1 & 2 \end{bmatrix} \begin{bmatrix} x_1 \\ x_2 \end{bmatrix} = \begin{bmatrix} 6 \\ 0 \\ 0 \end{bmatrix}$$

---

### Step 2.1: Compute $A^T A$
Multiply the transposed $2 \times 3$ matrix by the original $3 \times 2$ matrix:
$$A^T A = \begin{bmatrix} 1 & 1 & 1 \\ 0 & 1 & 2 \end{bmatrix} \begin{bmatrix} 1 & 0 \\ 1 & 1 \\ 1 & 2 \end{bmatrix} = \begin{bmatrix} (1+1+1) & (0+1+2) \\ (0+1+2) & (0+1+4) \end{bmatrix} = \mathbf{\begin{bmatrix} 3 & 3 \\ 3 & 5 \end{bmatrix}}$$

---

### Step 2.2: Compute the Inverse Matrix $(A^T A)^{-1}$
Using the standard $2 \times 2$ inverse formula $\frac{1}{ad-bc}\begin{bmatrix} d & -b \\ -c & a \end{bmatrix}$:
$$\det(A^T A) = (3 \times 5) - (3 \times 3) = 15 - 9 = 6$$
$$(A^T A)^{-1} = \frac{1}{6} \begin{bmatrix} 5 & -3 \\ -3 & 3 \end{bmatrix}$$

---

### Step 2.3: Calculate the Right Pseudoinverse $A^+$
Multiply the inverted matrix by $A^T$:
$$A^+ = (A^T A)^{-1} A^T = \frac{1}{6} \begin{bmatrix} 5 & -3 \\ -3 & 3 \end{bmatrix} \begin{bmatrix} 1 & 1 & 1 \\ 0 & 1 & 2 \end{bmatrix}$$
$$A^+ = \frac{1}{6} \begin{bmatrix} (5+0) & (5-3) & (5-6) \\ (-3+0) & (-3+3) & (-3+6) \end{bmatrix} = \mathbf{\frac{1}{6} \begin{bmatrix} 5 & 2 & -1 \\ -3 & 0 & 3 \end{bmatrix}}$$

---

### Step 2.4: Compute the Final Approximate Solution Vector $X$
Multiply the pseudoinverse by our target constraints vector $b$:
$$X = A^+ b = \frac{1}{6} \begin{bmatrix} 5 & 2 & -1 \\ -3 & 0 & 3 \end{bmatrix} \begin{bmatrix} 6 \\ 0 \\ 0 \end{bmatrix}$$
$$X = \frac{1}{6} \begin{bmatrix} (5 \times 6) + 0 + 0 \\ (-3 \times 6) + 0 + 0 \end{bmatrix} = \frac{1}{6} \begin{bmatrix} 30 \\ -18 \end{bmatrix} = \mathbf{\begin{bmatrix} 5 \\ -3 \end{bmatrix}}$$

#### Final Answer:
$$x_1 = 5, \quad x_2 = -3$$

---

## 3. Supplementary Practice Problems with Solutions

### Problem 1: Structural Verification of Underdetermined Constraints
**Scenario:** A wide sensor array data matrix $A$ has dimensions $2 \times 4$ ($m=2$ rows, $n=4$ columns).
1. State the shape of the matrix products $A^T A$ and $A A^T$.
2. State which product can be inverted to solve the system.

#### Step-by-Step Dimensional Analysis:
1. **Matrix Product Dimensions:**
   * Shape of $A^T A \implies (4 \times 2) \times (2 \times 4) = \mathbf{4 \times 4}$
   * Shape of $A A^T \implies (2 \times 4) \times (4 \times 2) = \mathbf{2 \times 2}$
2. **Invertibility Verification:**
   The true rank of matrix $A$ can be at most $\min(m, n) = \min(2, 4) = 2$. Consequently, the large $4 \times 4$ matrix $A^T A$ is rank-deficient ($\text{rank} \le 2$), meaning its determinant is exactly 0 and it cannot be inverted. 
   Therefore, we must use the smaller $2 \times 2$ matrix **$A A^T$** to compute the left pseudoinverse:
   $$A^+ = A^T(A A^T)^{-1}$$

---

### Problem 2: Finding a Minimum Normed Solution (Underdetermined System)
**Scenario:** Find the unique minimum normed solution vector $X = \begin{bmatrix} x_1 \\ x_2 \end{bmatrix}$ that satisfies the single wide equation ($m=1, n=2$):
$$[ 1 \quad 2 ] \begin{bmatrix} x_1 \\ x_2 \end{bmatrix} = [ 10 ]$$

#### Step-by-Step Calculation:
1. **Identify the Components:**
   $$A = \begin{bmatrix} 1 & 2 \end{bmatrix}, \quad b = \begin{bmatrix} 10 \end{bmatrix}$$

2. **Compute the scalar product $A A^T$:**
   $$A A^T = \begin{bmatrix} 1 & 2 \end{bmatrix} \begin{bmatrix} 1 \\ 2 \end{bmatrix} = [1(1) + 2(2)] = [5]$$

3. **Compute the scalar inverse $(A A^T)^{-1}$:**
   $$(A A^T)^{-1} = \begin{bmatrix} \frac{1}{5} \end{bmatrix} = [0.2]$$

4. **Compute the Left Pseudoinverse $A^+$:**
   $$A^+ = A^T (A A^T)^{-1} = \begin{bmatrix} 1 \\ 2 \end{bmatrix} \begin{bmatrix} \frac{1}{5} \end{bmatrix} = \begin{bmatrix} \frac{1}{5} \\ \frac{2}{5} \end{bmatrix} = \begin{bmatrix} 0.2 \\ 0.4 \end{bmatrix}$$

5. **Calculate the Minimum Normed Solution vector $X = A^+ b$:**
   $$X = \begin{bmatrix} 0.2 \\ 0.4 \end{bmatrix} \begin{bmatrix} 10 \end{bmatrix} = \mathbf{\begin{bmatrix} 2 \\ 4 \end{bmatrix}}$$

#### Verification Check 💡
Let's verify that our solution is valid and find its length:
* **Constraint Check:** Substitute back into our original equation: $1(2) + 2(4) = 2 + 8 = 10$. This satisfies the constraint perfectly.
* **Geometric Length (Norm):** The squared length is $\|X\|_2^2 = 2^2 + 4^2 = 4 + 16 = 20$. 

Any other combination of numbers that equals 10 (such as $x_1=0, x_2=5$) will result in a larger length vector ($\|X\|_2^2 = 0^2 + 5^2 = 25 > 20$). Thus, $\begin{bmatrix} 2 \\ 4 \end{bmatrix}$ is the unique minimum normed solution vector.


# Linear Algebra Notes: Pseudoinverse and Minimum Normed Solutions

This note covers the calculations for solving non-square systems of linear equations ($AX = b$) using the **Moore-Penrose Pseudoinverse ($A^+$)**. It explicitly distinguishes between **Overdetermined** systems (via Least Squares) and **Underdetermined** systems (via Minimum Normed Solutions).

---

## 1. Concept Name: The Pseudoinverse ($A^+$) and System Types

### Simple Meaning 💡
When a matrix $A$ is square and invertible, we find a single unique solution using $X = A^{-1}b$. However, if a system is rectangular (non-square), a traditional matrix inverse does not exist. 

To bridge this gap, we use a generalized proxy called the **Pseudoinverse ($A^+$)**. Depending on whether your matrix is tall or wide, the pseudoinverse takes on two distinct algebraic structures:

### Case 1: Overdetermined Systems ($m > n$) — Least Squares
* **Scenario:** More equations than variables. Usually has **no exact solution**.
* **Goal:** Find an approximate vector $X$ that minimizes the reconstruction error $\|AX - b\|_2^2$.
* **The Normal Equation Setup:** $$A^T A X = A^T b$$
  $$X = \underbrace{(A^T A)^{-1} A^T}_{A^+} b$$
* **Right Pseudoinverse:** $A^+ = (A^T A)^{-1} A^T$. Since $A$ is $m \times n$, the matrix product $A^T A$ is a smaller, invertible square matrix of size $n \times n$.

---

### Case 2: Underdetermined Systems ($m < n$) — Minimum Normed Solution (MNS)
* **Scenario:** Fewer equations than variables. This leaves you with $n - m$ free variables, yielding **infinitely many valid solutions**.
* **Goal:** Among all infinite solutions that satisfy $AX = b$ perfectly, find the specific unique vector $X$ that has the **shortest overall geometric length** (minimizing the norm $\|X\|_2$).
* **The Optimization Objective:**
  $$\min_{X} \|X\|_2^2 \quad \text{subject to } AX = b$$
* **The Solution Setup:**
  $$X = \underbrace{A^T (A A^T)^{-1}}_{A^+} b$$
* **Left Pseudoinverse:** $A^+ = A^T (A A^T)^{-1}$. Because $A$ is wide, $A^T A$ is a giant $n \times n$ matrix whose standard inverse does not exist due to rank deficiency ($\text{rank}(A^T A) \le m < n$). Instead, we invert the smaller $m \times m$ matrix product $A A^T$.

---

## 2. Step-by-Step 3x2 Overdetermined Numerical Walkthrough

### Problem Statement
Solve the following overdetermined system of $m=3$ equations and $n=2$ unknowns:
$$\begin{bmatrix} 1 & 0 \\ 1 & 1 \\ 1 & 2 \end{bmatrix} \begin{bmatrix} x_1 \\ x_2 \end{bmatrix} = \begin{bmatrix} 6 \\ 0 \\ 0 \end{bmatrix}$$

---

### Step 2.1: Compute $A^T A$
Multiply the transposed $2 \times 3$ matrix by the original $3 \times 2$ matrix:
$$A^T A = \begin{bmatrix} 1 & 1 & 1 \\ 0 & 1 & 2 \end{bmatrix} \begin{bmatrix} 1 & 0 \\ 1 & 1 \\ 1 & 2 \end{bmatrix} = \begin{bmatrix} (1+1+1) & (0+1+2) \\ (0+1+2) & (0+1+4) \end{bmatrix} = \mathbf{\begin{bmatrix} 3 & 3 \\ 3 & 5 \end{bmatrix}}$$

---

### Step 2.2: Compute the Inverse Matrix $(A^T A)^{-1}$
Using the standard $2 \times 2$ inverse formula $\frac{1}{ad-bc}\begin{bmatrix} d & -b \\ -c & a \end{bmatrix}$:
$$\det(A^T A) = (3 \times 5) - (3 \times 3) = 15 - 9 = 6$$
$$(A^T A)^{-1} = \frac{1}{6} \begin{bmatrix} 5 & -3 \\ -3 & 3 \end{bmatrix}$$

---

### Step 2.3: Calculate the Right Pseudoinverse $A^+$
Multiply the inverted matrix by $A^T$:
$$A^+ = (A^T A)^{-1} A^T = \frac{1}{6} \begin{bmatrix} 5 & -3 \\ -3 & 3 \end{bmatrix} \begin{bmatrix} 1 & 1 & 1 \\ 0 & 1 & 2 \end{bmatrix}$$
$$A^+ = \frac{1}{6} \begin{bmatrix} (5+0) & (5-3) & (5-6) \\ (-3+0) & (-3+3) & (-3+6) \end{bmatrix} = \mathbf{\frac{1}{6} \begin{bmatrix} 5 & 2 & -1 \\ -3 & 0 & 3 \end{bmatrix}}$$

---

### Step 2.4: Compute the Final Approximate Solution Vector $X$
Multiply the pseudoinverse by our target constraints vector $b$:
$$X = A^+ b = \frac{1}{6} \begin{bmatrix} 5 & 2 & -1 \\ -3 & 0 & 3 \end{bmatrix} \begin{bmatrix} 6 \\ 0 \\ 0 \end{bmatrix}$$
$$X = \frac{1}{6} \begin{bmatrix} (5 \times 6) + 0 + 0 \\ (-3 \times 6) + 0 + 0 \end{bmatrix} = \frac{1}{6} \begin{bmatrix} 30 \\ -18 \end{bmatrix} = \mathbf{\begin{bmatrix} 5 \\ -3 \end{bmatrix}}$$

#### Final Answer:
$$x_1 = 5, \quad x_2 = -3$$

---

## 3. Supplementary Practice Problems with Solutions

### Problem 1: Structural Verification of Underdetermined Constraints
**Scenario:** A wide sensor array data matrix $A$ has dimensions $2 \times 4$ ($m=2$ rows, $n=4$ columns).
1. State the shape of the matrix products $A^T A$ and $A A^T$.
2. State which product can be inverted to solve the system.

#### Step-by-Step Dimensional Analysis:
1. **Matrix Product Dimensions:**
   * Shape of $A^T A \implies (4 \times 2) \times (2 \times 4) = \mathbf{4 \times 4}$
   * Shape of $A A^T \implies (2 \times 4) \times (4 \times 2) = \mathbf{2 \times 2}$
2. **Invertibility Verification:**
   The true rank of matrix $A$ can be at most $\min(m, n) = \min(2, 4) = 2$. Consequently, the large $4 \times 4$ matrix $A^T A$ is rank-deficient ($\text{rank} \le 2$), meaning its determinant is exactly 0 and it cannot be inverted. 
   Therefore, we must use the smaller $2 \times 2$ matrix **$A A^T$** to compute the left pseudoinverse:
   $$A^+ = A^T(A A^T)^{-1}$$

---

### Problem 2: Finding a Minimum Normed Solution (Underdetermined System)
**Scenario:** Find the unique minimum normed solution vector $X = \begin{bmatrix} x_1 \\ x_2 \end{bmatrix}$ that satisfies the single wide equation ($m=1, n=2$):
$$[ 1 \quad 2 ] \begin{bmatrix} x_1 \\ x_2 \end{bmatrix} = [ 10 ]$$

#### Step-by-Step Calculation:
1. **Identify the Components:**
   $$A = \begin{bmatrix} 1 & 2 \end{bmatrix}, \quad b = \begin{bmatrix} 10 \end{bmatrix}$$

2. **Compute the scalar product $A A^T$:**
   $$A A^T = \begin{bmatrix} 1 & 2 \end{bmatrix} \begin{bmatrix} 1 \\ 2 \end{bmatrix} = [1(1) + 2(2)] = [5]$$

3. **Compute the scalar inverse $(A A^T)^{-1}$:**
   $$(A A^T)^{-1} = \begin{bmatrix} \frac{1}{5} \end{bmatrix} = [0.2]$$

4. **Compute the Left Pseudoinverse $A^+$:**
   $$A^+ = A^T (A A^T)^{-1} = \begin{bmatrix} 1 \\ 2 \end{bmatrix} \begin{bmatrix} \frac{1}{5} \end{bmatrix} = \begin{bmatrix} \frac{1}{5} \\ \frac{2}{5} \end{bmatrix} = \begin{bmatrix} 0.2 \\ 0.4 \end{bmatrix}$$

5. **Calculate the Minimum Normed Solution vector $X = A^+ b$:**
   $$X = \begin{bmatrix} 0.2 \\ 0.4 \end{bmatrix} \begin{bmatrix} 10 \end{bmatrix} = \mathbf{\begin{bmatrix} 2 \\ 4 \end{bmatrix}}$$

#### Verification Check 💡
Let's verify that our solution is valid and find its length:
* **Constraint Check:** Substitute back into our original equation: $1(2) + 2(4) = 2 + 8 = 10$. This satisfies the constraint perfectly.
* **Geometric Length (Norm):** The squared length is $\|X\|_2^2 = 2^2 + 4^2 = 4 + 16 = 20$. 

Any other combination of numbers that equals 10 (such as $x_1=0, x_2=5$) will result in a larger length vector ($\|X\|_2^2 = 0^2 + 5^2 = 25 > 20$). Thus, $\begin{bmatrix} 2 \\ 4 \end{bmatrix}$ is the unique minimum normed solution vector.