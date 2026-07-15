# Functions of Several Variables: Foundations, Domain, and Range

---

## 1. Introduction to Functions of Several Variables

### Core Concept
Up until now, you have likely worked primarily with single-variable functions like $y = f(x)$, where one single input maps to one single output. However, many real-world phenomena depend on multiple independent factors. 

A **Function of Several Variables** maps a collection of multiple inputs (ordered pairs, triplets, or $n$-tuples) to a single real number.

> **Mathematical Definition:**
> Let $S \subseteq \mathbb{R}^n$. A real-valued function $f$ on $S$ is a rule that assigns a single real number $w$ to every element of $S$. It is written as:
> 
> $$w = f(x_1, x_2, \dots, x_n) \quad \forall (x_1, x_2, \dots, x_n) \in S$$
> 
> Here, the variables $x_1, x_2, \dots, x_n$ are the **independent variables**, and $w$ is the **dependent variable**.

### Visualizing the Coordinate Spaces
* **$\mathbb{R}^n$ Space:** The set of all ordered $n$-tuples of real numbers.
  $$\mathbb{R}^n = \{(x_1, x_2, \dots, x_n) : x_i \in \mathbb{R} \text{ for all } i\}$$
* **$\mathbb{R}^2$ Space (2-Variables):** The standard flat Cartesian plane where inputs are pairs $(x, y)$.
  $$\mathbb{R}^2 = \{(x, y) : x, y \in \mathbb{R}\}$$

---

## 2. Domain and Range of Multi-Variable Functions

When transitioning to multiple variables, the core definitions of domain and range remain exactly the same structurally, but the geometry changes.

* **Domain ($D(f)$ or $\text{Dom}(f)$):** The set of all input points $(x_1, x_2, \dots, x_n) \in \mathbb{R}^n$ for which the mathematical rule produces a valid real number output. *Instead of an interval on a line, the domain is now a region in a 2D plane, a 3D space, or higher dimensions.*
  
  $$D(f) = \{(x_1, x_2, \dots, x_n) \in \mathbb{R}^n \mid f(x_1, x_2, \dots, x_n) \text{ is defined}\}$$

* **Range ($R(f)$ or $\text{Range}(f)$):** The set of all *actual* real number outputs generated when you map every possible input point from the domain through the function. The range remains a 1D subset of real numbers ($\mathbb{R}$).
  
  $$R(f) = \{f(x_1, x_2, \dots, x_n) \mid (x_1, x_2, \dots, x_n) \in D(f)\}$$

### Multi-Variable Mapping Diagram
```text
      Domain Region                    Target Set
     in 2D Space (R²)               Real Line (R)
     +--------------+               +------------+
     |   (x₁, x₂)   | ------------> |     w      |
     |   (p, q)     | ------------> |            |
     +--------------+               +------------+

```

---

## 3. Step-by-Step Problems and Calculations

### Problem 1: The Paraboloid Surface Function

**Question:** Find the domain and range of the function $f : \mathbb{R}^2 \rightarrow \mathbb{R}$ defined by $f(x, y) = x^2 + y^2$.

#### Step-by-Step Explanation & Calculations:

1. **Finding the Domain:**
Look for operations that cause mathematical errors (like division by zero or square roots of negative numbers). The expression $x^2 + y^2$ only uses basic arithmetic multiplication and addition. You can square and add any real numbers $x$ and $y$ without restrictions.

$$\text{Domain}(f) = \mathbb{R}^2$$


2. **Finding the Range:**
Analyze the behavior of the terms:
* For any real number $x$, $x^2 \geq 0$.
* For any real number $y$, $y^2 \geq 0$.


Adding two non-negative values together will always produce a non-negative value:

$$x^2 + y^2 \geq 0$$


* Minimum value occurs at the origin: $f(0, 0) = 0^2 + 0^2 = 0$.
* As $x$ or $y$ goes towards infinity, the value grows without bound ($\infty$).


$$\text{Range}(f) = [0, \infty)$$



#### Geometric Graph Visualization

This function forms a circular bowl shape known as a **paraboloid**.

```text
                 Z (Output Axis)
                 |       /
          \      |      /
           \     |     /  <-- Paraboloid Bowled Surface
            \____|____/
                 +---------------- Y
                /
               /
              X (Input Planes)

```

---

### Problem 2: Rational Multi-Variable Function

**Question:** Determine the domain of the function $g(x, y) = \frac{1}{x - y}$.

#### Step-by-Step Explanation & Calculations:

1. Identify constraints: A denominator cannot equal zero.

$$x - y \neq 0$$


2. Isolate the algebraic relationship:

$$x \neq y$$


3. State the domain: The domain contains all coordinates in the 2D plane *except* for the points lying directly on the diagonal line where $y = x$.

$$\text{Domain}(g) = \{(x, y) \in \mathbb{R}^2 \mid x \neq y\}$$



#### Domain Graph Representation

The domain is the entire plane excluding the dashed boundary line $y = x$.

```text
                 Y
                 |     . / (Excluded Line: y = x)
                 |     . /
                 |   .  /
-----------------+----.------------ X
               . |  /
             .   | /
           .     |

```

---

### Problem 3: Square Root Multi-Variable Function

**Question:** Find the domain of the function $h(x, y) = \sqrt{9 - x^2 - y^2}$.

#### Step-by-Step Explanation & Calculations:

1. Identify constraints: The values residing beneath a radical principal root index must be greater than or equal to zero.

$$9 - x^2 - y^2 \geq 0$$


2. Rearrange terms to reveal the geometric structure:

$$9 \geq x^2 + y^2 \implies x^2 + y^2 \leq 9$$


3. **Conclusion:** The expression $x^2 + y^2 = 9$ is a circle of radius $3$ centered at $(0,0)$. The inequality $\leq$ indicates all points inside or on that circle.

$$\text{Domain}(h) = \{(x, y) \in \mathbb{R}^2 \mid x^2 + y^2 \leq 3^2\}$$



#### Domain Graph Representation

The shaded region represents the allowed inputs (a filled solid disk of radius 3).

```text
                 Y
                 |   3
              .-*-.
            /  |  \
-----------+---+---+----------- X
         -3 \  |  / 3
              '-*-'
                |-3

```

```

```

# Foundations of Multi-Variable Functions and Partial Derivatives

---

## 1. Multi-Variable Domain Analysis (Example Case)

Before diving into derivatives, let us analyze how restrictions function when dealing with more than one independent input variable.

### Problem: Radical Multi-Variable Domain & Range
Given $f : \mathbb{R}^2 \rightarrow \mathbb{R}$ defined by:
$$f(x, y) = \sqrt{y - x^2}$$

#### Step-by-Step Calculation:
1. **Identify Constraints:** The values under a square root radical must be non-negative.
   $$y - x^2 \geq 0$$
2. **Isolate Variables:** $$y \geq x^2$$
3. **Determine Domain ($D(f)$):** The domain consists of all ordered pairs $(x, y)$ in the 2D Cartesian plane that lie on or above the parabola $y = x^2$.
   $$D(f) = \{(x, y) \in \mathbb{R}^2 \mid y - x^2 \geq 0\}$$
4. **Determine Range ($R(f)$):** A principal square root yields any value from $0$ up to infinity.
   $$R(f) = [0, \infty)$$

#### Domain Region Graph
The shaded region above and including the solid line boundary represents the allowed inputs:
```text
                 Y
                 |     / (Boundary Line: y = x²)
              \  |  /  
               \ | /   <- Shaded region INSIDE the bowl
-----------------+----------------- X
                 |

```

---

## 2. Transitioning from Single Variable to Partial Derivatives

To understand partial derivatives, let's first review ordinary single-variable derivatives.

### Single Variable Derivative Review

For a function $y = f(x)$ mapping $\mathbb{R} \rightarrow \mathbb{R}$, the derivative represents the instantaneous rate of change (the exact slope of the tangent line) at a point:

$$\frac{dy}{dx} = \lim_{h \to 0} \frac{f(x + h) - f(x)}{h}$$

Evaluated at a specific constant coordinate $x = a$:


$$\left(\frac{dy}{dx}\right)_{x=a} = \lim_{h \to 0} \frac{f(a + h) - f(a)}{h}$$

---

### What is a Partial Derivative?

When a function depends on multiple variables, say $z = f(x_1, x_2, \dots, x_n)$, you cannot change all inputs simultaneously along a single line. Instead, we look at the rate of change **with respect to one variable at a time, while holding all other variables completely constant**.

> **Mathematical Definition (General Case):**
> The partial derivative of $f$ with respect to an independent variable $x_i$ is denoted as $f_{x_i}$ or $\frac{\partial f}{\partial x_i}$, defined by the limit:
> $$f_{x_i} = \frac{\partial f}{\partial x_i} = \lim_{\Delta x_i \to 0} \frac{f(x_1, x_2, \dots, x_i + \Delta x_i, \dots, x_n) - f(x_1, x_2, \dots, x_n)}{\Delta x_i}$$
> 
> 

---

## 3. First-Order Partial Derivatives (2-Variable Systems)

For a two-variable system where $w = f(x_1, x_2)$ mapping $\mathbb{R}^2 \rightarrow \mathbb{R}$:

### 1. Partial Derivative with respect to $x_1$

We vary $x_1$ by a tiny increment $h$ while keeping $x_2$ completely locked.


$$\frac{\partial f}{\partial x_1} = \lim_{h \to 0} \frac{f(x_1 + h, x_2) - f(x_1, x_2)}{h}$$

### 2. Partial Derivative with respect to $x_2$

We vary $x_2$ by a tiny increment $k$ while keeping $x_1$ completely locked.


$$\frac{\partial f}{\partial x_2} = \lim_{k \to 0} \frac{f(x_1, x_2 + k) - f(x_1, x_2)}{k}$$

---

## 4. Practical Worked Problems (Calculations)

### Problem 1: Basic Polynomial Expression

Let $f(x, y) = 3x^2y + 5x + 2y^3$. Find $\frac{\partial f}{\partial x}$ and $\frac{\partial f}{\partial y}$.

#### Step-by-Step Calculation for $\frac{\partial f}{\partial x}$:

1. Treat $y$ as a fixed constant number.
2. Differentiate each term with respect to $x$:
* Derivative of $3x^2y \implies 3y \cdot (2x) = 6xy$
* Derivative of $5x \implies 5$
* Derivative of $2y^3 \implies 0$ (since it contains no $x$ variables, it behaves like a constant)


3. Combine terms:

$$\frac{\partial f}{\partial x} = 6xy + 5$$



#### Step-by-Step Calculation for $\frac{\partial f}{\partial y}$:

1. Treat $x$ as a fixed constant number.
2. Differentiate each term with respect to $y$:
* Derivative of $3x^2y \implies 3x^2 \cdot (1) = 3x^2$
* Derivative of $5x \implies 0$ (behaves completely like a constant)
* Derivative of $2y^3 \implies 2 \cdot (3y^2) = 6y^2$


3. Combine terms:

$$\frac{\partial f}{\partial y} = 3x^2 + 6y^2$$



---

### Problem 2: Using the Chain Rule Partials

Let $z = \sin(xy^2)$. Find $\frac{\partial z}{\partial x}$.

#### Step-by-Step Calculation:

1. Treat $y$ as a constant.
2. Apply the outer derivative formula for sine, which is cosine:

$$\frac{\partial}{\partial x}[\sin(xy^2)] = \cos(xy^2) \cdot \frac{\partial}{\partial x}(xy^2)$$


3. Compute the inner derivative with respect to $x$ (keeping $y$ constant):

$$\frac{\partial}{\partial x}(xy^2) = y^2 \cdot (1) = y^2$$


4. Assemble the final solution structural parts:

$$\frac{\partial z}{\partial x} = y^2\cos(xy^2)$$



```

```


# Higher-Order and Mixed Partial Derivatives

---

## 1. Core Concept: Higher-Order Partial Derivatives

Just as you can differentiate a single-variable function multiple times to find its second or third derivatives, you can take successive derivatives of multi-variable functions. These are called **higher-order partial derivatives**.

When dealing with a function of two variables $w = f(x_1, x_2)$, its first-order partial derivatives $f_{x_1}$ and $f_{x_2}$ are also functions of $x_1$ and $x_2$. Therefore, we can differentiate them again.

### Notation Guide
For a standard two-variable system, there are four possible second-order partial derivatives:

| Concept Name | Subscript Notation | Operator Notation | Simple Meaning |
| :--- | :--- | :--- | :--- |
| **Second Partial w.r.t $x_1$** | $f_{x_1x_1}$ | $\frac{\partial^2 f}{\partial x_1^2} = \frac{\partial}{\partial x_1}\left(\frac{\partial f}{\partial x_1}\right)$ | Differentiate with respect to $x_1$ twice. |
| **Second Partial w.r.t $x_2$** | $f_{x_2x_2}$ | $\frac{\partial^2 f}{\partial x_2^2} = \frac{\partial}{\partial x_2}\left(\frac{\partial f}{\partial x_2}\right)$ | Differentiate with respect to $x_2$ twice. |
| **Mixed Partial ($x_1$ then $x_2$)** | $f_{x_1x_2}$ | $\frac{\partial^2 f}{\partial x_2 \partial x_1} = \frac{\partial}{\partial x_2}\left(\frac{\partial f}{\partial x_1}\right)$ | Differentiate first with respect to $x_1$, then take that result and differentiate it with respect to $x_2$. |
| **Mixed Partial ($x_2$ then $x_1$)** | $f_{x_2x_1}$ | $\frac{\partial^2 f}{\partial x_1 \partial x_2} = \frac{\partial}{\partial x_1}\left(\frac{\partial f}{\partial x_2}\right)$ | Differentiate first with respect to $x_2$, then take that result and differentiate it with respect to $x_1$. |

> **Clairaut's Theorem Note:** For almost all smooth, continuous functions encountered in calculus, the order of differentiation for mixed partials does not matter. That means $f_{x_1x_2} = f_{x_2x_1}$.

---

## 2. Step-by-Step Comprehensive Problem

### Problem Statement
Given the function $f : \mathbb{R}^2 \rightarrow \mathbb{R}$ defined by:
$$f(x, y) = x^4 - x^2y^2 + y^4$$

Find the values of $f_x$, $f_y$, $f_{xx}$, $f_{yy}$, and $f_{xy}$ evaluated at the point $(-1, 1)$.

---

### Step-by-Step Calculation Breakdown

#### Step 1: Find the First-Order Partial Derivatives
* **To find $f_x$ (treat $y$ as a constant):**
  $$f_x = \frac{\partial f}{\partial x} = \frac{\partial}{\partial x}(x^4) - \frac{\partial}{\partial x}(x^2y^2) + \frac{\partial}{\partial x}(y^4)$$
  $$f_x = 4x^3 - (2x \cdot y^2) + 0 = 4x^3 - 2xy^2$$

* **To find $f_y$ (treat $x$ as a constant):**
  $$f_y = \frac{\partial f}{\partial y} = \frac{\partial}{\partial y}(x^4) - \frac{\partial}{\partial y}(x^2y^2) + \frac{\partial}{\partial y}(y^4)$$
  $$f_y = 0 - (x^2 \cdot 2y) + 4y^3 = -2x^2y + 4y^3$$

---

#### Step 2: Evaluate First-Order Derivatives at $(-1, 1)$
Substitute $x = -1$ and $y = 1$:
* **For $(f_x)_{(-1,1)}$:**
  $$(f_x)_{(-1,1)} = 4(-1)^3 - 2(-1)(1)^2 = 4(-1) - 2(-1) = -4 + 2 = -2$$

* **For $(f_y)_{(-1,1)}$:**
  $$(f_y)_{(-1,1)} = -2(-1)^2(1) + 4(1)^3 = -2(1)(1) + 4 = -2 + 4 = 2$$

---

#### Step 3: Find and Evaluate the Second-Order Derivative $f_{xx}$
* **Find the algebraic expression:** Differentiate $f_x = 4x^3 - 2xy^2$ with respect to $x$ again (keeping $y$ constant):
  $$f_{xx} = \frac{\partial^2 f}{\partial x^2} = \frac{\partial}{\partial x}(4x^3 - 2xy^2) = 12x^2 - 2y^2$$

* **Evaluate at $(-1, 1)$:**
  $$(f_{xx})_{(-1,1)} = 12(-1)^2 - 2(1)^2 = 12(1) - 2(1) = 12 - 2 = 10$$

---

#### Step 4: Find and Evaluate the Second-Order Derivative $f_{yy}$
* **Find the algebraic expression:** Differentiate $f_y = -2x^2y + 4y^3$ with respect to $y$ again (keeping $x$ constant):
  $$f_{yy} = \frac{\partial^2 f}{\partial y^2} = \frac{\partial}{\partial y}(-2x^2y + 4y^3) = -2x^2(1) + 12y^2 = -2x^2 + 12y^2$$

* **Evaluate at $(-1, 1)$:**
  $$(f_{yy})_{(-1,1)} = -2(-1)^2 + 12(1)^2 = -2(1) + 12 = -2 + 12 = 10$$

---

#### Step 5: Find and Evaluate the Mixed Partial Derivative $f_{xy}$
* **Find the algebraic expression:** Take the expression for $f_x = 4x^3 - 2xy^2$ and differentiate it with respect to $y$ (keeping $x$ constant):
  $$f_{xy} = \frac{\partial^2 f}{\partial y \partial x} = \frac{\partial}{\partial y}(4x^3 - 2xy^2) = 0 - 2x(2y) = -4xy$$

* **Evaluate at $(-1, 1)$:**
  $$(f_{xy})_{(-1,1)} = -4(-1)(1) = 4$$

---

### Summary of Results
| Derivative | Algebraic Form | Value at $(-1, 1)$ |
| :--- | :--- | :--- |
| $f_x$ | $4x^3 - 2xy^2$ | $-2$ |
| $f_y$ | $-2x^2y + 4y^3$ | $2$ |
| $f_{xx}$ | $12x^2 - 2y^2$ | $10$ |
| $f_{yy}$ | $-2x^2 + 12y^2$ | $10$ |
| $f_{xy}$ | $-4xy$ | $4$ |

---

## 3. Supplementary Practice Problem

**Question:** Given $g(x, y) = x^2 \sin(y) + y e^x$, verify that the mixed partials $g_{xy}$ and $g_{yx}$ are equal.

#### Step 1: Calculate First-Order Partials
* $g_x = 2x\sin(y) + ye^x$
* $g_y = x^2\cos(y) + e^x$

#### Step 2: Compute Mixed Partial $g_{xy}$
Differentiate $g_x$ with respect to $y$:
$$g_{xy} = \frac{\partial}{\partial y}(2x\sin(y) + ye^x) = 2x\cos(y) + e^x$$

#### Step 3: Compute Mixed Partial $g_{yx}$
Differentiate $g_y$ with respect to $x$:
$$g_{yx} = \frac{\partial}{\partial x}(x^2\cos(y) + e^x) = 2x\cos(y) + e^x$$

#### Conclusion:
$$g_{xy} = g_{yx} = 2x\cos(y) + e^x$$
This explicitly verifies Clairaut's Theorem!



# Gradients and Directional Derivatives

---

## 1. The Gradient Vector

### Core Concept
In single-variable calculus, the derivative gives you the rate of change along a single line. In machine learning and optimization, functions depend on thousands or millions of parameters. The **gradient** generalizes the concept of a derivative to functions of several variables. 

Instead of a single scalar slope, the gradient packs all first-order partial derivatives into a single **vector**. 

> **Properties of the Gradient:**
> * The gradient vector points in the direction of the **steepest ascent** (most rapid increase) of the function.
> * The magnitude (length) of the gradient vector indicates the rate of change in that steepest direction.
> * In machine learning, we move in the opposite direction ($-\nabla f$) to minimize cost functions, a core algorithm known as **Gradient Descent**.

> **Mathematical Definition:**
> For a scalar-valued function $f : \mathbb{R}^n \rightarrow \mathbb{R}$, the gradient is denoted by $\nabla f$ (read as "del f" or "grad f") and is defined as the transpose of a row vector containing all $n$ partial derivatives:
> 
> $$\nabla f = \begin{bmatrix} \frac{\partial f}{\partial x_1} & \frac{\partial f}{\partial x_2} & \dots & \frac{\partial f}{\partial x_n} \end{bmatrix}^T = \begin{bmatrix} \frac{\partial f}{\partial x_1} \\ \frac{\partial f}{\partial x_2} \\ \vdots \\ \frac{\partial f}{\partial x_n} \end{bmatrix}$$
> 
> Index-wise, the $i$-th component of the gradient vector is simply the partial derivative with respect to that variable: $[\nabla f]_i = \frac{\partial f}{\partial x_i}$.

---

### Worked Gradient Problem
**Question:** Given $f : \mathbb{R}^3 \rightarrow \mathbb{R}$ defined by $f(x, y, z) = x^3 - 3xy^2 + x^2y + y^3 + zy$, find the gradient vector $\nabla f$ at the specific point $(-1, 0, 1)$.

#### Step 1: Compute the First-Order Partial Derivatives
* **For $f_x$ (treat $y$ and $z$ as constants):**
  $$f_x = \frac{\partial}{\partial x}(x^3) - \frac{\partial}{\partial x}(3xy^2) + \frac{\partial}{\partial x}(x^2y) + 0 + 0$$
  $$f_x = 3x^2 - 3y^2 + 2xy$$

* **For $f_y$ (treat $x$ and $z$ as constants):**
  $$f_y = 0 - \frac{\partial}{\partial y}(3xy^2) + \frac{\partial}{\partial y}(x^2y) + \frac{\partial}{\partial y}(y^3) + \frac{\partial}{\partial y}(zy)$$
  $$f_y = -6xy + x^2 + 3y^2 + z$$

* **For $f_z$ (treat $x$ and $y$ as constants):**
  $$f_z = 0 - 0 + 0 + 0 + \frac{\partial}{\partial z}(zy)$$
  $$f_z = y$$

#### Step 2: Evaluate the Partial Derivatives at $P(-1, 0, 1)$
Substitute $x = -1$, $y = 0$, and $z = 1$:
* $(f_x)_{(-1,0,1)} = 3(-1)^2 - 3(0)^2 + 2(-1)(0) = 3(1) - 0 - 0 = 3$
* $(f_y)_{(-1,0,1)} = -6(-1)(0) + (-1)^2 + 3(0)^2 + 1 = 0 + 1 + 0 + 1 = 2$
* $(f_z)_{(-1,0,1)} = 0$

#### Step 3: Construct the Gradient Vector
$$\nabla f_{(-1,0,1)} = \begin{bmatrix} 3 & 2 & 0 \end{bmatrix}^T = \begin{bmatrix} 3 \\ 2 \\ 0 \end{bmatrix}$$

---

## 2. Directional Derivatives

### Core Concept
Partial derivatives $\frac{\partial f}{\partial x}$ and $\frac{\partial f}{\partial y}$ tell you the rate of change of a function exclusively along the standard coordinate axes ($X$ and $Y$). A **Directional Derivative** computes the rate of change along **any** arbitrary path defined by a unit vector $\vec{u}$.


> **Mathematical Limit Definition (2-Variable System):**
> Let $\vec{u} = \langle a_1, a_2 \rangle$ be a unit vector ($\vert{}\vec{u}\vert{} = 1$). The directional derivative of $f(x_1, x_2)$ in the direction of $\vec{u}$ is given by:
> 
> $$D_{\vec{u}}f(x_1, x_2) = \lim_{h \to 0} \frac{f(x_1 + a_1h, x_2 + a_2h) - f(x_1, x_2)}{h}$$

This concept naturally scales up to $n$ independent variables:
$$D_{\vec{u}}f(x_1, x_2, \dots, x_n) = \lim_{h \to 0} \frac{f(x_1 + a_1h, \dots, x_n + a_nh) - f(x_1, x_2, \dots, x_n)}{h}$$

---

## 3. Connecting the Gradient and Directional Derivatives

Calculating the limit from scratch for every direction is tedious. Fortunately, multivariable calculus provides a powerful link using a line paramaterization and the **Multivariate Chain Rule**.

### Mathematical Derivation / Proof

1. Let $P_0(x_0, y_0)$ be our starting point and let $\vec{u} = u_1\hat{i} + u_2\hat{j}$ be the unit vector direction ($\vert{}\vec{u}\vert{} = \sqrt{u_1^2 + u_2^2} = 1$).
2. Parameterize the straight path moving away from $P_0$ in terms of distance $s$:
   $$\frac{x - x_0}{u_1} = \frac{y - y_0}{u_2} = s \implies x = x_0 + su_1, \quad y = y_0 + su_2$$

```text
                 Y
                 |             / u = <u₁, u₂>
                 |            /
                 |           /  (x, y) = (x₀ + su₁, y₀ + su₂)
                 |          * |        /
                 |      * P₀(x₀, y₀)
-----------------+--------------------------- X
                 |

```

3. Rewrite the derivative expression using the Single-Variable notation with step parameter $s$:

$$\left(\frac{df}{ds}\right)_{P_0, \vec{u}} = \lim_{s \to 0} \frac{f(x_0 + su_1, y_0 + su_2) - f(x_0, y_0)}{s}$$


4. Apply the Multivariate Chain Rule:

$$\frac{df}{ds} = \left(\frac{\partial f}{\partial x}\right)\frac{dx}{ds} + \left(\frac{\partial f}{\partial y}\right)\frac{dy}{ds}$$


5. Calculate the component coordinate rates of change from our parameter equations:

$$\frac{dx}{ds} = \frac{d}{ds}(x_0 + su_1) = u_1$$


$$\frac{dy}{ds} = \frac{d}{ds}(y_0 + su_2) = u_2$$


6. Substitute these back into the chain rule equation:

$$\left(\frac{df}{ds}\right)_{P_0, \vec{u}} = \left(\frac{\partial f}{\partial x}\right)_{P_0}u_1 + \left(\frac{\partial f}{\partial y}\right)_{P_0}u_2$$


7. Express this sum as a **Dot Product** of two vectors:

$$\left(\frac{df}{ds}\right)_{P_0, \vec{u}} = \left( \left(\frac{\partial f}{\partial x}\right)_{P_0}\hat{i} + \left(\frac{\partial f}{\partial y}\right)_{P_0}\hat{j} \right) \cdot (u_1\hat{i} + u_2\hat{j})$$



This yields the fundamental formula:


$$D_{\vec{u}}f(P_0) = \nabla f(P_0) \cdot \vec{u}$$

> **Important Condition:** This relationship is only valid if $\vec{u}$ is explicitly configured as a **unit vector** ($|\vec{u}| = 1$). If given a vector of any other length, you must normalize it first by dividing it by its magnitude before computing the dot product.

---

## 4. Worked Directional Derivative Problem

**Question:** Find the directional derivative of $f(x, y) = 2x^2y^3$ at the point $P(1, 2)$ in the direction of the vector $\vec{v} = \langle 3, 4 \rangle$.

### Step-by-Step Calculation:

#### Step 1: Normalize the Direction Vector

Calculate the magnitude of $\vec{v}$:


$$|\vec{v}| = \sqrt{3^2 + 4^2} = \sqrt{9 + 16} = \sqrt{25} = 5$$

Construct the unit vector $\vec{u}$:


$$\vec{u} = \frac{\vec{v}}{|\vec{v}|} = \left\langle \frac{3}{5}, \frac{4}{5} \right\rangle$$

#### Step 2: Calculate the Gradient Vector $\nabla f$

* $f_x = \frac{\partial}{\partial x}(2x^2y^3) = 4xy^3$
* $f_y = \frac{\partial}{\partial y}(2x^2y^3) = 6x^2y^2$

$$\nabla f = \langle 4xy^3, 6x^2y^2 \rangle$$

#### Step 3: Evaluate $\nabla f$ at the Point $(1, 2)$

* $f_x(1, 2) = 4(1)(2)^3 = 4(1)(8) = 32$
* $f_y(1, 2) = 6(1)^2(2)^2 = 6(1)(4) = 24$

$$\nabla f_{(1,2)} = \langle 32, 24 \rangle$$

#### Step 4: Compute the Dot Product

$$D_{\vec{u}}f(1,2) = \nabla f_{(1,2)} \cdot \vec{u}$$

$$D_{\vec{u}}f(1,2) = \langle 32, 24 \rangle \cdot \left\langle \frac{3}{5}, \frac{4}{5} \right\rangle$$

$$D_{\vec{u}}f(1,2) = (32) \cdot \left(\frac{3}{5}\right) + (24) \cdot \left(\frac{4}{5}\right)$$

$$D_{\vec{u}}f(1,2) = \frac{96}{5} + \frac{96}{5} = \frac{192}{5} = 38.4$$

```

```


# Maximizing and Minimizing Rates of Change via the Gradient

---

## 1. Core Concept: Maximum and Minimum Rates of Change

The directional derivative of a function $f$ at a point $P_0$ in the direction of a unit vector $\vec{u}$ measures how fast the function's output changes in that specific direction. We express this rate of change mathematically using the dot product:

$$\left(\frac{df}{ds}\right)_{P_0, \vec{u}} = \nabla f(P_0) \cdot \vec{u}$$

By applying the geometric definition of a vector dot product ($A \cdot B = |A||B|\cos\theta$), we can expand this relationship:

$$\left(\frac{df}{ds}\right)_{P_0, \vec{u}} = |\nabla f(P_0)| \cdot |\vec{u}| \cdot \cos\theta$$

Because $\vec{u}$ is defined strictly as a **unit vector**, its magnitude is always one ($|\vec{u}| = 1$). Substituting this simplifies our calculation down to:

$$\left(\frac{df}{ds}\right)_{P_0, \vec{u}} = |\nabla f(P_0)| \cos\theta$$

Here, $\theta$ represents the spatial angle between the fixed gradient vector $\nabla f(P_0)$ and our chosen direction vector $\vec{u}$. Since the value of $\cos\theta$ is bounded strictly between $-1$ and $+1$, we can deduce the absolute maximum and minimum behaviors of any smooth surface.


---

### Key Properties of Maximum and Minimum Ascents

#### Property 1: Maximum Rate of Change (Steepest Ascent)
* **Condition:** Occurs when $\cos\theta$ hits its maximum value of $1$.
* **Angle:** This happens when $\theta = 0^\circ$, meaning the direction vector $\vec{u}$ points **exactly in the same direction** as the gradient vector $\nabla f(P_0)$.
* **Maximum Magnitude:** $$\text{Maximum Rate} = |\nabla f(P_0)|$$
* **Direction Vector:** $$\vec{u}_{\text{max}} = \frac{\nabla f(P_0)}{|\nabla f(P_0)|}$$

#### Property 2: Minimum Rate of Change (Steepest Descent)
* **Condition:** Occurs when $\cos\theta$ drops to its minimum value of $-1$.
* **Angle:** This happens when $\theta = \pi$ ($180^\circ$), meaning the direction vector $\vec{u}$ points **directly opposite** to the gradient vector (in the direction of $-\nabla f(P_0)$).
* **Minimum Magnitude:** $$\text{Minimum Rate} = -|\nabla f(P_0)|$$
* **Direction Vector:** $$\vec{u}_{\text{min}} = -\frac{\nabla f(P_0)}{|\nabla f(P_0)|}$$

---

## 2. Step-by-Step Problem and Calculation

### Problem Statement
Given a 3-variable function $f : \mathbb{R}^3 \rightarrow \mathbb{R}$ defined by:
$$f(x, y, z) = x^2y + y^2z + z^2x$$

Find the unique unit vector directions where $f$ **increases most rapidly** and **decreases most rapidly** at the point $P_0(1, 0, 1)$.

---

### Step-by-Step Calculation Breakdown

#### Step 1: Compute the Partial Derivatives
To construct our gradient vector, evaluate the partial derivative equations one by one:
* **For $f_x$ (treat $y$ and $z$ as constants):**
  $$f_x = \frac{\partial}{\partial x}(x^2y) + 0 + \frac{\partial}{\partial x}(z^2x) = 2xy + z^2$$

* **For $f_y$ (treat $x$ and $z$ as constants):**
  $$f_y = \frac{\partial}{\partial y}(x^2y) + \frac{\partial}{\partial y}(y^2z) + 0 = x^2 + 2yz$$

* **For $f_z$ (treat $x$ and $y$ as constants):**
  $$f_z = 0 + \frac{\partial}{\partial z}(y^2z) + \frac{\partial}{\partial z}(z^2x) = y^2 + 2zx$$

---

#### Step 2: Evaluate Partials at the point $P_0(1, 0, 1)$
Substitute the coordinates $x = 1$, $y = 0$, and $z = 1$:
* $(f_x)_{(1,0,1)} = 2(1)(0) + (1)^2 = 0 + 1 = 1$
* $(f_y)_{(1,0,1)} = (1)^2 + 2(0)(1) = 1 + 0 = 1$
* $(f_z)_{(1,0,1)} = (0)^2 + 2(1)(1) = 0 + 2 = 2$

Combining these vectors into standard component column format:
$$\nabla f(P_0) = \begin{bmatrix} 1 & 1 & 2 \end{bmatrix}^T = 1\hat{i} + 1\hat{j} + 2\hat{k}$$

---

#### Step 3: Compute the Vector Magnitude
Calculate the geometric length of the gradient vector at this point:
$$|\nabla f(P_0)| = \sqrt{(1)^2 + (1)^2 + (2)^2} = \sqrt{1 + 1 + 4} = \sqrt{6}$$

---

#### Step 4: Find Direction of Most Rapid Increase (Steepest Ascent)
As proven by our rules, the function increases fastest along the exact vector path of the gradient. To get the directional path unit vector, normalize the gradient:
$$\vec{u}_{\text{increase}} = \frac{\hat{i} + \hat{j} + 2\hat{k}}{\sqrt{6}}$$

* **Maximum Slope Value:** $\sqrt{6} \approx 2.45$

---

#### Step 5: Find Direction of Most Rapid Decrease (Steepest Descent)
The function decreases fastest in the exact opposite direction ($-\nabla f(P_0)$):
$$\vec{u}_{\text{decrease}} = \frac{-\hat{i} - \hat{j} - 2\hat{k}}{\sqrt{6}}$$

* **Minimum Slope Value:** $-\sqrt{6} \approx -2.45$

---

## 3. Directional Derivative Generalization

As reviewed in previous chapters, if you want to evaluate the rate of change in *any general* direction, you can use the multi-variable limit definition:

$$D_{\vec{u}}f(x_1, x_2, \dots, x_n) = \lim_{h \to 0} \frac{f(x_1 + a_1h, \dots, x_n + a_nh) - f(x_1, x_2, \dots, x_n)}{h}$$

### Verification Using Dot Product Example
Let's verify that the directional derivative at $P_0(1,0,1)$ in the direction of maximum increase yields exactly its magnitude $|\nabla f| = \sqrt{6}$.

$$D_{\vec{u}}f = \nabla f \cdot \vec{u}_{\text{increase}}$$
$$D_{\vec{u}}f = \langle 1, 1, 2 \rangle \cdot \left\langle \frac{1}{\sqrt{6}}, \frac{1}{\sqrt{6}}, \frac{2}{\sqrt{6}} \right\rangle$$
$$D_{\vec{u}}f = \frac{1}{\sqrt{6}} + \frac{1}{\sqrt{6}} + \frac{4}{\sqrt{6}} = \frac{6}{\sqrt{6}} = \sqrt{6}$$


# Advanced Gradient Vector Properties and Sigma Notation

---

## 1. Sigma ($\sum$) Notation for Directional Derivatives

### Core Concept
The directional derivative measures the rate of change of a function in the direction of a unit vector $\vec{u} = \langle a_1, a_2, \dots, a_n \rangle$. Rather than writing out the dot product longhand, we can use **Sigma ($\sum$) Notation** to compactly represent this sum across any arbitrary number of dimensions ($n$).

> **Mathematical Formula:**
> For a function of $n$ variables $f(x_1, x_2, \dots, x_n)$, the directional derivative is defined as:
> 
> $$D_{\vec{u}}f(x_1, x_2, \dots, x_n) = \sum_{i=1}^{n} f_{x_i}(x_1, x_2, \dots, x_n)a_i = \nabla f \cdot \vec{u}$$
> 
> Where:
> * $f_{x_i}$ represents the partial derivative with respect to the $i$-th variable ($\frac{\partial f}{\partial x_i}$).
> * $a_i$ represents the $i$-th component of the unit vector $\vec{u}$.

### Breaking Down the Expansion
If you expand this summation for a standard $3$-variable system ($n=3$) with variables $(x, y, z)$ and a unit direction vector $\vec{u} = \langle a_1, a_2, a_3 \rangle$, it directly yields the standard dot product sum:

$$\sum_{i=1}^{3} f_{x_i}a_i = \left(\frac{\partial f}{\partial x}\right)a_1 + \left(\frac{\partial f}{\partial y}\right)a_2 + \left(\frac{\partial f}{\partial z}\right)a_3$$

---

## 2. Core Geometric Properties of the Gradient

The gradient vector $\nabla f(\mathbf{x})$ possesses two fundamental properties that form the absolute bedrock of mathematical optimization and machine learning algorithms (such as neural network training via backpropagation):

### Property 1: Steepest Ascent
The gradient vector $\nabla f(\mathbf{x})$ points directly in the spatial direction where the function's value **increases most rapidly** from the point $\mathbf{x}$. 

### Property 2: Steepest Descent
The negative gradient vector $-\nabla f(\mathbf{x})$ points directly in the spatial direction where the function's value **decreases most rapidly** from the point $\mathbf{x}$.


---

## 3. Step-by-Step Problems and Calculations

### Problem 1: Expanding the Sigma Formula in 4D Space
**Question:** Write out the explicit directional derivative formula using the provided summation notation for a $4$-dimensional function $f(x_1, x_2, x_3, x_4)$ along a unit direction vector $\vec{u} = \langle a_1, a_2, a_3, a_4 \rangle$.

#### Step-by-Step Calculation:
1. Set the upper limit of the summation index to $n = 4$:
   $$D_{\vec{u}}f = \sum_{i=1}^{4} f_{x_i}a_i$$
2. Expand the sum by stepping the index variable $i$ from $1$ up to $4$:
   $$D_{\vec{u}}f = f_{x_1}a_1 + f_{x_2}a_2 + f_{x_3}a_3 + f_{x_4}a_4$$
3. Convert the notation into traditional partial derivative format:
   $$D_{\vec{u}}f = \left(\frac{\partial f}{\partial x_1}\right)a_1 + \left(\frac{\partial f}{\partial x_2}\right)a_2 + \left(\frac{\partial f}{\partial x_3}\right)a_3 + \left(\frac{\partial f}{\partial x_4}\right)a_4$$

---

### Problem 2: Finding the Direction of Steepest Descent
**Question:** Given the cost function $f(x, y) = 4x^2 + 9y^2$, determine the exact direction vector of **steepest descent** at the point $(1, 2)$.

#### Step-by-Step Calculation:
1. **Compute the First-Order Partial Derivatives:**
   * Differentiate with respect to $x$ (treat $y$ as a constant):
     $$f_x = \frac{\partial}{\partial x}(4x^2 + 9y^2) = 8x$$
   * Differentiate with respect to $y$ (treat $x$ as a constant):
     $$f_y = \frac{\partial}{\partial y}(4x^2 + 9y^2) = 18y$$

2. **Construct the general Gradient Vector:**
   $$\nabla f(x, y) = \langle 8x, 18y \rangle$$

3. **Evaluate the Gradient at the specific point $(1, 2)$:**
   $$\nabla f(1, 2) = \langle 8(1), 18(2) \rangle = \langle 8, 36 \rangle$$
   *(Note: This vector $\langle 8, 36 \rangle$ points in the direction of steepest **ascent**).*

4. **Determine the Steepest Descent Direction ($-\nabla f$):**
   Multiply the gradient vector by $-1$:
   $$-\nabla f(1, 2) = -\langle 8, 36 \rangle = \langle -8, -36 \rangle$$

5. **Convert to a Unit Vector (Optional but ideal for finding pure direction):**
   * Find the magnitude: 
     $$\vert{}-\nabla f\vert{} = \sqrt{(-8)^2 + (-36)^2} = \sqrt{64 + 1296} = \sqrt{1360} = 4\sqrt{85}$$
   * Divide the vector by its magnitude:
     $$\vec{u}_{\text{descent}} = \left\langle \frac{-8}{4\sqrt{85}}, \frac{-36}{4\sqrt{85}} \right\rangle = \left\langle \frac{-2}{\sqrt{85}}, \frac{-9}{\sqrt{85}} \right\rangle$$

#### 2D Contour Plot Visualization
The concentric ellipses represent lines of constant output value (contours). The gradient vector points outwards perpendicularly, while the steepest descent path points directly inward toward the minimum at the origin $(0,0)$.

```text
                 Y
                 |       .---.
                 |     /   |   \
                 |    |    |    |
                 |    |  <-* |  <-- Steepest Descent (-∇f) points
                 |     \ (1,2) /       directly toward the center bowl!
-----------------+-------'---'----- X
                 |
                 |