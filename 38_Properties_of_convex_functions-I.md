# Concept Name: Optimization Properties of Convex Functions

---

## 1. Core Definitions

To understand the core theorems, we first need to define the difference between a **Local Minimum** and a **Global Minimum**.

### Local Minimum
A point $\bar{x}$ is a **local minimum** of a function $f$ on a set $S$ if it has the lowest value within its immediate neighborhood.
$$\bar{x} \text{ is a local minimum} \implies f(\bar{x}) \le f(x), \quad \forall x \in N_{\delta}(\bar{x}) \cap S, \text{ for some } \delta > 0$$

> **Simple Meaning:** If you look at a tiny zone (neighborhood of radius $\delta$) around $\bar{x}$, no other point gives a smaller value than $\bar{x}$.

### Global Minimum
A point $\bar{x}$ is a **global minimum** of a function $f$ on a set $S$ if it has the lowest value over the entire set.
$$\bar{x} \text{ is a global minimum} \implies f(\bar{x}) \le f(x), \quad \forall x \in S$$

> **Simple Meaning:** Out of all possible points in the entire domain $S$, $\bar{x}$ gives the absolute smallest value.

---

## 2. Main Theorems

### Theorem 1: Local Minimum vs. Global Minimum
Let $S \subseteq \mathbb{R}^n$ be a convex set. If $f : S \to \mathbb{R}$ is a **convex function**, then **any local minimum of $f$ in $S$ is also a global minimum on $S$**.

### Theorem 2: Uniqueness of Minima
Let $S \subseteq \mathbb{R}^n$ be a convex set. If $f : S \to \mathbb{R}$ is **strictly convex**, then there exists a **unique minimizing point** of $f$ over $S$.

---

## 3. Mathematical Proof of Theorem 1

**Objective:** Prove that if $\bar{x}$ is a local minimum of a convex function $f$, it must be a global minimum.

### Step-by-Step Breakdown & Explanation:

1. **Set up the Local Minimum condition:**
   Let $\bar{x}$ be a local minimum point. By definition, there exists a neighborhood radius $\delta > 0$ such that:
   $$f(\bar{x}) \le f(x) \quad \forall x \in N_{\delta}(\bar{x}) \cap S \quad \text{--- (Equation 1)}$$

2. **Proof by Contradiction:**
   Suppose $\bar{x}$ is **not** a global minimum. This means there must exist some other point $\hat{x} \in S$ that is even smaller than $\bar{x}$:
   $$f(\hat{x}) < f(\bar{x}) \quad \text{--- (Equation 2)}$$

3. **Construct a Line Segment:**
   Because $S$ is a convex set, any point along the line segment connecting $\hat{x}$ and $\bar{x}$ is also in $S$. Let's define an intermediate point $\tilde{x}$ using a scaling factor $\bar{\lambda}$ (where $0 < \bar{\lambda} < 1$):
   $$\tilde{x} = \bar{\lambda}\hat{x} + (1 - \bar{\lambda})\bar{x}$$
   By choosing a very small value for $\bar{\lambda}$, we can pull $\tilde{x}$ close enough to $\bar{x}$ so that it falls inside the local neighborhood: $\tilde{x} \in N_{\delta}(\bar{x}) \cap S$.

4. **Apply the Definition of Convexity:**
   Since $f$ is a convex function, the function value at the mixture point $\tilde{x}$ is less than or equal to the mixture of the function values:
   $$f(\tilde{x}) = f(\bar{\lambda}\hat{x} + (1 - \bar{\lambda})\bar{x}) \le \bar{\lambda} f(\hat{x}) + (1 - \bar{\lambda}) f(\bar{x})$$

5. **Substitute Equation 2 into the inequality:**
   Since $f(\hat{x}) < f(\bar{x})$, replacing $f(\hat{x})$ with $f(\bar{x})$ makes the right side strictly larger:
   $$f(\tilde{x}) < \bar{\lambda} f(\bar{x}) + (1 - \bar{\lambda}) f(\bar{x})$$

6. **Simplify the Calculation:**
   Factoring out $f(\bar{x})$:
   $$f(\tilde{x}) < (\bar{\lambda} + 1 - \bar{\lambda}) f(\bar{x})$$
   $$f(\tilde{x}) < f(\bar{x})$$

7. **Conclusion:**
   This result ($f(\tilde{x}) < f(\bar{x})$) directly **contradicts** Equation 1, which states that $f(\bar{x})$ must be the smallest value in its local neighborhood. Thus, our assumption was wrong: $\bar{x}$ **must** be a global minimum.

---

## 4. Visualizing the Concepts

### Non-Convex Function (Multiple Local Minima)
In a non-convex function, a local minimum is not necessarily the lowest point overall.
```text
  y ^
    |       _--_
    |      /    \      _--_
    |     /      \    /    \
    |____/        \__/      \____
    |             (Local)
    +-----------------------------> x

```

### Convex Function (Local Min = Global Min)

In a convex function, there is only one "bowl", ensuring any local low point is the absolute lowest point.

```text
  y ^
    |  \                    /
    |   \                  /
    |    \                /
    |     \____      ____/
    |          \____/ 
    |         (Global Min)
    +-----------------------------> x

```

---

## 5. Practice Problems with Solutions

### Problem 1: Verifying Local to Global Properties

**Question:** Given the function $f(x) = x^2 - 4x + 4$ defined on the convex set $S = \mathbb{R}$, find its local minimum and show it is a global minimum.

**Solution:**

1. **Find the critical point:** Take the first derivative and set it to 0.

$$f'(x) = 2x - 4 = 0 \implies x = 2$$


2. **Check convexity:** Take the second derivative.

$$f''(x) = 2 > 0$$



Since $f''(x) > 0$ for all $x$, the function is strictly convex.
3. **Conclusion:** According to Theorem 1, since $f(x)$ is convex, the local minimum at $x = 2$ is automatically the **global minimum**.

---

### Problem 2: Uniqueness of Minima

**Question:** Show that the function $f(x) = e^x - x$ has a unique minimizing point on $\mathbb{R}$.

**Solution:**

1. **Find the critical point:**

$$f'(x) = e^x - 1 = 0 \implies e^x = 1 \implies x = 0$$


2. **Check strict convexity:**

$$f''(x) = e^x$$



Since $e^x > 0$ for all real numbers $x$, the function is **strictly convex**.
3. **Conclusion:** According to Theorem 2, a strictly convex function contains a **unique minimizing point**. Therefore, $x = 0$ is the unique global minimum.

Here are the complete notes compiled into a structured, clean Markdown document ready to copy and paste directly into VS Code.


# Optimization and Convexity Properties of Differentiable Functions

---

## 1. Concept: Uniqueness of Global Minimum for Strictly Convex Functions

### Simple Meaning
If a function is **strictly convex** (it curves upwards sharply like a perfect U-shape bowl without any flat parts), it cannot have multiple lowest points. If a global minimum exists, it must be completely unique. 

### Proof by Contradiction
Let $f$ be a strictly convex function on a convex set $S$. 
Suppose $\bar{x} \in S$ is a global minimum point of $f$. Let's assume $\bar{x}$ is **not** unique.

* **Step 1:** If it's not unique, there must exist another point $\hat{x} \in S$ such that $\bar{x} \neq \hat{x}$ and their function values are equal:
  $$f(\bar{x}) = f(\hat{x})$$

* **Step 2:** Define a new point $z$ as a weighted combination (line segment) between $\bar{x}$ and $\hat{x}$ with $0 < \lambda < 1$:
  $$z = \lambda \bar{x} + (1 - \lambda) \hat{x}, \quad \text{where } z \in S$$

* **Step 3:** Calculate the function value at $z$ using the definition of **strict convexity**:
  $$f(z) = f(\lambda \bar{x} + (1 - \lambda) \hat{x}) < \lambda f(\bar{x}) + (1 - \lambda) f(\hat{x})$$

* **Step 4:** Substitute $f(\bar{x}) = f(\hat{x})$ into the right side of the inequality:
  $$f(z) < \lambda f(\hat{x}) + (1 - \lambda) f(\hat{x})$$
  $$f(z) < (\lambda + 1 - \lambda) f(\hat{x})$$
  $$f(z) < f(\hat{x})$$

* **Step 5 Conclusion:** This implies $f(z) < f(\hat{x})$ (and thus $f(z) < f(\bar{x})$). This contradicts the initial condition that $\bar{x}$ and $\hat{x}$ are global minimum points. Thus, **$\bar{x}$ must be a unique global minimum point of $f$ on $S$**.

---

## 2. Concept: Differentiable and Twice Differentiable Multi-Variable Functions

### Simple Meaning
When approximating a smooth curve mathematically near a specific point $\bar{x}$, we can use Taylor series approximations. For a single derivative, it maps a linear tangent plane. For a second derivative, it maps a quadratic curvature.

### Mathematical Definitions
1. **First-order Differentiability:** Let $f: S \to \mathbb{R}$ be differentiable at $\bar{x} \in S$, where $S \subseteq \mathbb{R}^n$ is an open subset. For any point $x + \bar{x} \in S$:
   $$f(x + \bar{x}) = f(\bar{x}) + x^T(\nabla f(\bar{x})) + \alpha(\bar{x}, x) \Vert{}x\Vert{}$$
   where the error term satisfies $\lim_{x \to 0} \alpha(\bar{x}, x) = 0$.

2. **Second-order Differentiability:** Let $f: S \to \mathbb{R}$ be twice differentiable at $\bar{x} \in S$:
   $$f(x + \bar{x}) = f(\bar{x}) + x^T(\nabla f(\bar{x})) + \frac{1}{2}x^T \nabla^2 f(\bar{x})x + \beta(\bar{x}, x) \Vert{}x\Vert{}^2$$
   where the error term satisfies $\lim_{x \to 0} \beta(\bar{x}, x) = 0$.

---

## 3. Concept: First-Order Characterization of Convexity

### Simple Meaning
A differentiable function is convex if and only if its entire graph sits **on or above** its tangent line (or tangent plane) at any given point. The tangent line always under-estimates the function values.

### The First-Order Convexity Theorem
Let $f : S \longrightarrow \mathbb{R}$ be a differentiable function on an open convex subset $S$ of $\mathbb{R}^n$. Then $f$ is a convex function if and only if:
$$f(x_1) - f(x_2) \geq (x_1 - x_2)^T \nabla f(x_2) \quad \forall x_1, x_2 \in S$$

> **Alternative Form:** Rearranging terms yields $f(x_1) \geq f(x_2) + \nabla f(x_2)^T (x_1 - x_2)$, where the right side represents the linear tangent approximation at $x_2$.

### Visual Graph Representation
Below is a text-based layout showing that the actual curve $f(x)$ stays completely above the tangent line drawn at point $x_2$:

```text
  f(x) ^
       |                     . B (x1, f(x1))
       |                    /|
       |     A (x2, f(x2)) / |
       |          .-------*--|------- Tangent Line
       |         /       . M | (Tangent Value at x1)
       |        /        .   |
       |_______/_________.___|________> x
                        x2   x1

```

* **Point A ($x_2, f(x_2)$)** is where the tangent line touches the function curve.
* **Point B ($x_1, f(x_1)$)** is the actual function value at $x_1$.
* **Point M** represents the height of the tangent line at $x_1$.
* Since the function is convex, the distance $BN \geq MN$, meaning $f(x_1) \geq f(x_2) + f'(x_2)(x_1 - x_2)$.

---

## 4. Analytical Step-by-Step Calculation Example

Let's algebraically verify this first-order condition using the basic convex function:


$$f(x) = x^2, \quad \text{where } f'(x) = 2x$$

### Objective

Prove that $f(x_1) - f(x_2) - (x_1 - x_2)f'(x_2) \geq 0$ for any real values $x_1, x_2 \in \mathbb{R}$.

### Step-by-Step Computations:

1. Write out the general expression:

$$= f(x_1) - f(x_2) - (x_1 - x_2) f'(x_2)$$


2. Substitute $f(x) = x^2$ and $f'(x) = 2x$ into the equation:

$$= x_1^2 - x_2^2 - (x_1 - x_2)(2x_2)$$


3. Expand the multiplication terms:

$$= x_1^2 - x_2^2 - 2x_1x_2 + 2x_2^2$$


4. Group and simplify like-terms (combining $-x_2^2$ and $+2x_2^2$):

$$= x_1^2 + x_2^2 - 2x_1x_2$$


5. Condense the expression into a perfect square trinomial:

$$= (x_1 - x_2)^2$$



### Final Analysis Result:

Since any real number squared must be greater than or equal to zero:


$$(x_1 - x_2)^2 \geq 0$$


This cleanly proves that $f(x_1) - f(x_2) \geq (x_1 - x_2)f'(x_2)$, verifying first-order convexity.

---

## 5. Additional Practice Problems with Solutions

### Problem 1: First-Order Condition Check

**Question:** Show that the function $f(x) = e^{-x}$ satisfies the first-order convexity condition across its domain.

**Solution:**

1. **Find the first derivative:**

$$f'(x) = -e^{-x}$$


2. **Set up the first-order inequality check:**

$$f(x_1) - f(x_2) - (x_1 - x_2)f'(x_2)$$


$$= e^{-x_1} - e^{-x_2} - (x_1 - x_2)(-e^{-x_2})$$


$$= e^{-x_1} - e^{-x_2} + (x_1 - x_2)e^{-x_2}$$


3. **Analyze using Taylor Series expansion properties:**
Let's rewrite the term by factoring out $e^{-x_2}$:

$$= e^{-x_2} \left( e^{-(x_1 - x_2)} - 1 + (x_1 - x_2) \right)$$



Let $\Delta = x_1 - x_2$. The expression inside becomes $e^{-\Delta} - 1 + \Delta$. Since $e^{-\Delta} \geq 1 - \Delta$ holds true for all real values of $\Delta$, it means $e^{-\Delta} + \Delta - 1 \geq 0$.
4. **Conclusion:** Because $e^{-x_2} > 0$ always, the whole expression remains $\geq 0$. Thus, $f(x) = e^{-x}$ satisfies the first-order convexity theorem.

---

### Problem 2: Checking Multi-Variable Global Minima Uniqueness

**Question:** Consider the multi-variable function $f(x, y) = 3x^2 + 2y^2 - 6x + 8y$. Determine if its stationary point is a unique global minimum.

**Solution:**

1. **Compute the gradient vector ($\nabla f(x, y)$) to locate stationary points:**

$$\frac{\partial f}{\partial x} = 6x - 6 = 0 \implies x = 1$$


$$\frac{\partial f}{\partial y} = 4y + 8 = 0 \implies y = -2$$



The stationary point resides at $(\bar{x}, \bar{y}) = (1, -2)$.
2. **Compute the Hessian Matrix ($\nabla^2 f(x, y)$) to verify the type of convexity:**

$$\nabla^2 f(x, y) = \begin{pmatrix} \frac{\partial^2 f}{\partial x^2} & \frac{\partial^2 f}{\partial x \partial y} \\ \frac{\partial^2 f}{\partial y \partial x} & \frac{\partial^2 f}{\partial y^2} \end{pmatrix} = \begin{pmatrix} 6 & 0 \\ 0 & 4 \end{pmatrix}$$


3. **Check for strict convexity:**
A matrix is positive definite if all its eigenvalues are strictly positive. Here, the eigenvalues are $6$ and $4$. Both are greater than $0$, so the matrix is **positive definite**, meaning $f(x, y)$ is **strictly convex**.
4. **Conclusion:** According to the strict convexity theorem, because the function is strictly convex over its entire domain, the critical point $(1, -2)$ forms a completely **unique global minimum point**.

