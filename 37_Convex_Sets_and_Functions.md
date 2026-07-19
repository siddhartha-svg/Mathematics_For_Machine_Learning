# Lecture 37: Convex Sets and Functions

## 1. Introduction to Convexity
Convexity plays a foundational role in modern computation, specifically in:
* **Machine Learning Algorithms:** Optimization routines (like gradient descent) rely heavily on convex properties to guarantee convergence to global minima.
* **Optimization Theory:** A massive framework of mathematical results has been established specifically around convex spaces because they avoid the traps of local optima.

---

## 2. Mathematical Definition: Convex Set

### 💡 Simple Meaning
A set is considered **convex** if you can take *any* two points inside the set, draw a straight line segment directly between them, and every single point on that line segment remains completely inside the set. If the line exits the set at any point, the set is **non-convex**.

### 📐 Formal Definition
A set $S \subseteq \mathbb{R}^n$ is called **convex** if for all $x_1, x_2 \in S$ and a scalar $\lambda \in [0, 1]$, the following holds true:

$$\lambda x_1 + (1 - \lambda)x_2 \in S$$

### 🔍 Understanding the Variables
* $x_1, x_2$: Two independent points chosen from the set $S$.
* $\lambda$ (Lambda): A mixing coefficient between $0$ and $1$ that represents a percentage/ratio.
* $\lambda x_1 + (1 - \lambda)x_2$: The mathematical equation representing a point on the line segment connecting $x_1$ and $x_2$.

---

## 3. Step-by-Step Derivation & Geometric Logic

Let's break down why this formula represents a line segment between two points $A(x_1)$ and $C(x_2)$, with an intermediate point $B(x)$:

### Step 1: Ratio of Line Segments
Imagine a point $x$ dividing the line segment between $x_1$ and $x_2$ in the ratio of $(1 - \lambda) : \lambda$. 
* The distance from $x_1$ to $x$ is proportional to $(1 - \lambda)$.
* The distance from $x$ to $x_2$ is proportional to $\lambda$.

### Step 2: Section Formula Derivation
Using the mathematical internal section formula to find point $x$:

$$x = \frac{\lambda x_1 + (1 - \lambda)x_2}{\lambda + (1 - \lambda)}$$

Since the denominator simplifies to $\lambda + 1 - \lambda = 1$, we get our core convex combination formula:

$$x = \lambda x_1 + (1 - \lambda)x_2$$

### Step 3: Proving the Bounds of $\lambda$
For the point $x$ to lie strictly *between* $x_1$ and $x_2$ (and not outside them), the ratios must be non-negative:
1. $\lambda \geq 0$
2. $1 - \lambda \geq 0 \implies \lambda \leq 1$

Combining these constraints yields the essential boundary: 

$$0 \leq \lambda \leq 1$$

---

## 4. Visualized Representation (Graph)

Below is a geometric visualization of a convex set (a filled unit disk) where the line segment between any two internal points remains bounded within the circle.

```text
       Y-Axis
          ^
          |      *** Convex Set S ***
          |    .---------.
          |  /   * x1     \
          | /     \        \
          | |      \        |
----------+---------\-------+------> X-Axis
          | \        \      /
          |  \        * x2 /
          |    '--------'-'
          |   x² + y² ≤ 1
          |

```

---

## 5. Practical Problems with Solutions

### Problem 1: Proving a Unit Disk is Convex

**Concept:** Prove that the set $S = \{(x, y) \mid x^2 + y^2 \leq 1\}$ is a convex set.

#### Step-by-Step Solution:

* **Step 1:** Select two arbitrary points inside the set $S$. Let $u = (x_1, y_1)$ and $v = (x_2, y_2)$.
Because they belong to $S$, they must satisfy the boundary condition:

$$x_1^2 + y_1^2 \leq 1 \quad \text{and} \quad x_2^2 + y_2^2 \leq 1$$


* **Step 2:** Set up a convex combination point $w$ using scalar $\lambda \in [0, 1]$:

$$w = \lambda u + (1 - \lambda)v = (\lambda x_1 + (1 - \lambda)x_2, \, \lambda y_1 + (1 - \lambda)y_2)$$


* **Step 3:** Evaluate if $w$ satisfies the set criteria $x^2 + y^2 \leq 1$:

$$\left(\lambda x_1 + (1 - \lambda)x_2\right)^2 + \left(\lambda y_1 + (1 - \lambda)y_2\right)^2$$


* **Step 4:** Expand the terms:

$$= \lambda^2(x_1^2 + y_1^2) + (1-\lambda)^2(x_2^2 + y_2^2) + 2\lambda(1-\lambda)(x_1 x_2 + y_1 y_2)$$


* **Step 5:** Apply Cauchy-Schwarz inequality ($x_1 x_2 + y_1 y_2 \leq \sqrt{x_1^2+y_1^2}\sqrt{x_2^2+y_2^2} \leq 1 \cdot 1$):

$$\leq \lambda^2(1) + (1-\lambda)^2(1) + 2\lambda(1-\lambda)(1)$$


$$= (\lambda + 1 - \lambda)^2 = 1^2 = 1$$


* **Conclusion:** Since the result $\leq 1$, the combined point $w \in S$. Thus, **$S$ is a convex set**.

---

### Problem 2: Identifying a Non-Convex Set

**Concept:** Determine if the ring/annulus set $S = \{(x, y) \mid 1 \leq x^2 + y^2 \leq 4\}$ is convex.

#### Step-by-Step Solution:

* **Step 1:** Pick two points that explicitly lie within the boundary conditions of $S$.
* Let $x_1 = (2, 0) \implies 2^2 + 0^2 = 4 \in S$
* Let $x_2 = (-2, 0) \implies (-2)^2 + 0^2 = 4 \in S$


* **Step 2:** Pick a midpoint value for $\lambda$. Let $\lambda = 0.5$.
* **Step 3:** Calculate the intermediate point $x$:

$$x = 0.5(2, 0) + (1 - 0.5)(-2, 0)$$


$$x = (1, 0) + (-1, 0) = (0, 0)$$


* **Step 4:** Check if the resulting point $(0,0)$ belongs to set $S$:

$$0^2 + 0^2 = 0$$



However, the set requires $x^2 + y^2 \geq 1$. Since $0 < 1$, the point $(0,0) \notin S$.
* **Conclusion:** The straight line passing through the center leaves the ring structure. Therefore, **$S$ is NOT a convex set**.



# Optimization Theory: Convex Sets (Visual Analysis & Proofs)

---

## 1. Visual Geometry of Convex vs. Non-Convex Sets

### 💡 Simple Meaning
* **Convex Set:** If you pick *any* two points inside a shape, the entire straight line connecting them must lie completely inside the shape.
* **Non-Convex Set:** If a shape has an inward dent, a cutout, or a non-convex boundary, you can pick two points inside it where the connecting line segment leaves the boundary of the shape.

```text
       CONVEX SET                             NON-CONVEX SET
   (Line stays inside)                     (Line escapes shape)
      .----------.                            .----------.
     /   x        \                          /   x        \
    /     \        \                        /     \        \
   |       \        |                      |       \        |
   |        \       |                      |        \____   |
    \        y     /                        \       /    \ /
     '----------'                            '-----*y----'
                                                   ^
                                             Escaped Area

```

---

## 2. Concept Breakdown & Worked Examples

### Example 1: The Elliptic Region (Convex)

**Concept Name:** Elliptic Disk Parameterization

**Given Set:** $S = \{(x, y) \in \mathbb{R}^2 : x^2 + 2y^2 \leq 4\}$

#### Step-by-Step Explanation & Calculations:

1. **Understand the Shape:** Divide the inequality by 4 to find the standard form:

$$\frac{x^2}{4} + \frac{y^2}{2} \leq 1$$



This describes the solid region inside an ellipse centered at $(0,0)$ with horizontal intercepts at $(\pm 2, 0)$ and vertical intercepts at $(0, \pm\sqrt{2})$.
2. **Mathematical Proof Structure:**
Let $z_1 = (x_1, y_1) \in S$ and $z_2 = (x_2, y_2) \in S$. Therefore:

$$x_1^2 + 2y_1^2 \leq 4 \quad \text{and} \quad x_2^2 + 2y_2^2 \leq 4$$



Take any point $z_3$ on the line segment connecting them using $\lambda \in [0, 1]$:

$$z_3 = \lambda z_1 + (1-\lambda)z_2 = (\lambda x_1 + (1-\lambda)x_2, \lambda y_1 + (1-\lambda)y_2)$$


3. **Verify Inequality Verification:**
Substitute the components of $z_3$ back into the original expression:

$$(\lambda x_1 + (1-\lambda)x_2)^2 + 2(\lambda y_1 + (1-\lambda)y_2)^2$$



Expanding out both quadratic polynomials and separating by $\lambda$ coefficients yields a result $\leq 4$. Since the condition holds for all valid coordinate inputs, **the set is convex**.

---

### Example 2: The Parabolic Region (Non-Convex)

**Concept Name:** Exterior Region of a Parabola

**Given Set:** $S = \{(x, y) \in \mathbb{R}^2 : y^2 \geq 4x\}$

#### Step-by-Step Explanation & Calculations:

1. **Find Counterexample Points:** To prove a set is non-convex, you only need to find *one* line segment that breaks the rule. Let's pick two points that lie on the parabola curve itself:
* Point $A = (1, 2) \implies (2)^2 \geq 4(1) \implies 4 \geq 4$ (True, so $A \in S$)
* Point $B = (1, -2) \implies (-2)^2 \geq 4(1) \implies 4 \geq 4$ (True, so $B \in S$)


2. **Find the Midpoint ($\lambda = 0.5$):**

$$x_{mid} = 0.5(1) + 0.5(1) = 1$$


$$y_{mid} = 0.5(2) + 0.5(-2) = 0$$



Our midpoint is $(1, 0)$.
3. **Test the Condition:** Check if $(1,0)$ satisfies $y^2 \geq 4x$:

$$(0)^2 \geq 4(1) \implies 0 \geq 4 \quad \text{(False!)}$$



Because the midpoint drops completely outside the allowable area, **the set is not convex**.

---

## 3. Practice Problem with Solution

**Problem:** Check whether the set $S = \{(x, y) \in \mathbb{R}^2 : x + 3y \geq 6\}$ is convex or not.

### Step-by-Step Calculation:

* **Step 1: Pick two arbitrary target points**
Let $u = (x_1, y_1) \in S$ and $v = (x_2, y_2) \in S$. This means:

$$x_1 + 3y_1 \geq 6 \quad \text{and} \quad x_2 + 3y_2 \geq 6$$


* **Step 2: Construct the linear blending point ($w$)**
For any $\lambda \in [0, 1]$, let:

$$w = \lambda u + (1-\lambda)v = (\lambda x_1 + (1-\lambda)x_2, \, \lambda y_1 + (1-\lambda)y_2)$$


* **Step 3: Test $w$ against the set's constraint equation**
Substitute the combined values into $x + 3y$:

$$\text{Value} = [\lambda x_1 + (1-\lambda)x_2] + 3[\lambda y_1 + (1-\lambda)y_2]$$


* **Step 4: Group like terms by their common weights ($\lambda$)**
$$\text{Value} = \lambda(x_1 + 3y_1) + (1-\lambda)(x_2 + 3y_2)$$


* **Step 5: Use inequalities to verify bounds**
Since $(x_1 + 3y_1) \geq 6$ and $(x_2 + 3y_2) \geq 6$:

$$\text{Value} \geq \lambda(6) + (1-\lambda)(6)$$


$$\text{Value} \geq 6\lambda + 6 - 6\lambda = 6$$



### Final Conclusion:

Since the resulting test shows that the linear combination strictly satisfies $\geq 6$, the point $w$ will always remain in the set. Therefore, **the half-plane set $S$ is convex**.



# Optimization Theory: Proving Convexity of Sets

This module provides algebraic proofs and geometric intuitions to determine whether a given mathematical set in $\mathbb{R}^2$ is convex or non-convex.

---

## 1. Concept Recap: Convex Set Criterion
A set $S \subseteq \mathbb{R}^n$ is **convex** if for any two points inside the set, the entire line segment connecting them also lies completely within the set. 
Mathematically, for all $u, v \in S$ and $\lambda \in [0, 1]$, the convex combination must satisfy:
$$\lambda u + (1 - \lambda)v \in S$$

---

## 2. Worked Problems & Verification Steps

### Concept 1: Parabolic Region (Non-Convex Set)
**Problem Statement:** Analyze the set $S = \{(x, y) \in \mathbb{R}^2 : y^2 \geq 4x\}$ to determine if it is convex.

#### 💡 Simple Meaning
The equation $y^2 = 4x$ represents a horizontal parabola opening to the right. The inequality $y^2 \geq 4x$ defines the region *outside* the bowl of the parabola. If you pick one point on the top branch and another on the bottom branch, the straight line connecting them passes through the empty space inside the curve, breaking the convexity rule.

#### 📈 Geometric Representation
```text
          X-Axis
            ^          y² = 4x
     \      |      /
      \     |     /  
-------\----+----/------> Y-Axis
        \   |   /     
   (1,0) *  |  /      Note: The point (1,0) lies 
          \ | /       inside the curve, which is 
            v         outside the defined set S.

```

#### Step-by-Step Proof by Counterexample:

* **Step 1: Choose two test points on the boundary**
Let point $u = (1, 2)$ and point $v = (1, -2)$.
Check if $u \in S$: $(2)^2 \geq 4(1) \implies 4 \geq 4$ (True)
Check if $v \in S$: $(-2)^2 \geq 4(1) \implies 4 \geq 4$ (True)
* **Step 2: Find the midpoint ($\lambda = 0.5$)**

$$w = 0.5(1, 2) + 0.5(1, -2)$$


$$w = (0.5 + 0.5, \, 1 - 1) = (1, 0)$$


* **Step 3: Test the intermediate point against the set definition**
For $w=(1,0)$ to belong to $S$, it must satisfy $y^2 \geq 4x$:

$$0^2 \geq 4(1) \implies 0 \geq 4 \quad \text{(False!)}$$


* **Conclusion:** Because the line segment exits the valid region, **$S$ is not a convex set**.

---

### Concept 2: Linear Half-Plane (Convex Set)

**Problem Statement:** Check whether the set $S = \{(x, y) \in \mathbb{R}^2 : x + 3y \geq 6\}$ is convex or not.

#### 💡 Simple Meaning

The equation $x + 3y = 6$ forms a straight line on a graph. The inequality $x + 3y \geq 6$ represents all the space on one side of that line (a half-plane). Since it's flat and extends infinitely without bending inwards, any line segment between two internal points will stay inside the region.

#### 📈 Geometric Representation

```text
        Y-Axis
          ^
          |      / Shaded Region (Satisfies x + 3y ≥ 6)
          |     /   /   /
        2 +----/---/---/--->
          |   /   /   /
----------+--/---/---/------> X-Axis
          | /   6
          v
        x + 3y = 6

```

#### Step-by-Step Algebraic Proof:

* **Step 1: Pick two arbitrary points in the set**
Let $(x_1, y_1) \in S$ and $(x_2, y_2) \in S$. By definition, they satisfy:

$$x_1 + 3y_1 \geq 6 \quad \text{and} \quad x_2 + 3y_2 \geq 6$$


* **Step 2: Set up the components of the combined target point ($z_1, z_2$)**
Let the target point be $(z_1, z_2) = \lambda(x_1, y_1) + (1-\lambda)(x_2, y_2)$ where $0 \leq \lambda \leq 1$.
Splitting into coordinate components:

$$z_1 = \lambda x_1 + (1-\lambda)x_2$$


$$z_2 = \lambda y_1 + (1-\lambda)y_2$$


* **Step 3: Substitute the new components into the constraint equation**
We must test if $z_1 + 3z_2 \geq 6$:

$$z_1 + 3z_2 = [\lambda x_1 + (1-\lambda)x_2] + 3[\lambda y_1 + (1-\lambda)y_2]$$


* **Step 4: Distribute and regroup by common factors ($\lambda$ and $1-\lambda$)**

$$z_1 + 3z_2 = \lambda x_1 + (1-\lambda)x_2 + \lambda(3y_1) + (1-\lambda)(3y_2)$$


$$z_1 + 3z_2 = \lambda(x_1 + 3y_1) + (1-\lambda)(x_2 + 3y_2)$$


* **Step 5: Apply the step 1 inequalities to establish bounds**
Since $(x_1 + 3y_1) \geq 6$ and $(x_2 + 3y_2) \geq 6$, and both scaling parameters ($\lambda$) are non-negative:

$$z_1 + 3z_2 \geq \lambda(6) + (1-\lambda)(6)$$


$$z_1 + 3z_2 \geq 6\lambda + 6 - 6\lambda$$


$$z_1 + 3z_2 \geq 6$$


* **Conclusion:** Since the inequality holds true for any coordinates matching our framework, $(z_1, z_2) \in S$. Therefore, **$S$ is a convex set in $\mathbb{R}^2$**.


# Properties of Convex Sets

This document breaks down the fundamental properties of convex sets, providing algebraic proofs, simplified meanings, worked problems, and visualizations.

---

## 🏛️ Overview of Core Properties
1. **Intersection:** The intersection of any arbitrary collection of convex sets is always convex.
2. **Union:** The union of two convex sets does **not** need to be convex.
3. **Vector Sum:** The vector sum $C_1 + C_2$ of two convex sets $C_1$ and $C_2$ is convex.
4. **Scalar Multiplication:** The set $\alpha C$ is convex for any convex set $C$ and scalar $\alpha$.

---

## 1. Property 1: Intersection of Convex Sets

### 💡 Simple Meaning
If you have multiple shapes that are all convex, the region where they **all overlap** (their intersection) will always be a convex shape. No matter how many shapes you overlay, the shared space won't suddenly develop an inward dent.

### 📐 Step-by-Step Formal Proof
Let $\{C_i\}_{i \in I}$ be a collection of convex sets in $\mathbb{R}^n$, where $I$ is an index set. We want to show that $\bigcap_{i \in I} C_i$ is convex.

* **Step 1:** Select two arbitrary points $x$ and $y$ that lie inside the intersection:
  $$let \quad x, y \in \bigcap_{i \in I} C_i$$
* **Step 2:** By definition of set intersection, if the points are in the intersection, they must be members of *every single individual set* $C_i$:
  $$\implies x, y \in C_i \quad \forall i \in I$$
* **Step 3:** Since every individual set $C_i$ is given to be convex, any line segment between $x$ and $y$ must stay completely inside each set $C_i$ for any $\lambda \in [0,1]$:
  $$\implies \lambda x + (1-\lambda)y \in C_i \quad \forall i \in I$$
* **Step 4:** Since the line segment $\lambda x + (1-\lambda)y$ belongs to every single set $C_i$, it must also belong to their collective overlapping intersection:
  $$\implies \lambda x + (1-\lambda)y \in \bigcap_{i \in I} C_i$$

**Conclusion:** Therefore, the intersection $\bigcap_{i \in I} C_i$ is also convex.

---

## 2. Property 2: Union of Convex Sets (Counterexample Proof)

### 💡 Simple Meaning
Just because two individual shapes are convex doesn't mean combining them together into a single master shape (union) preserves convexity. For instance, if you cross two thin straight lines (which are individually convex), you create a giant 'X' shape. If you pick a point on one arm of the 'X' and a point on another arm, the straight line connecting them flies right out into the empty space between the arms.

### 📈 Geometric Representation
Below is a visual of two perpendicular lines in $\mathbb{R}^2$ ($S_1$ along the X-axis and $S_2$ along the Y-axis). Their combination is a non-convex cross structure.

```text
               Y-Axis
                 ^
                 |   * (0,1) ∈ S₂
                 |   |
                 |   |  Line segment exits the axes!
                 |   |
-----------------+---+------------> X-Axis
               (0,0) |    * (1,0) ∈ S₁
                 |
                 v

```

### 📐 Step-by-Step Calculation / Counterexample

Let's mathematically define two sets representing the X and Y coordinate axes in $\mathbb{R}^2$:

* $S_1 = \{(x, 0) : x \in \mathbb{R}\}$ (The horizontal line/X-axis—convex)
* $S_2 = \{(0, y) : y \in \mathbb{R}\}$ (The vertical line/Y-axis—convex)

Now let's test if their union $S_1 \cup S_2$ is convex:

* **Step 1: Pick two points within the union set**
Let $u = (1, 0) \in S_1 \implies u \in S_1 \cup S_2$
Let $v = (0, 1) \in S_2 \implies v \in S_1 \cup S_2$
* **Step 2: Find the midpoint between them ($\lambda = 0.5$)**

$$\text{Midpoint} = 0.5(1, 0) + (1 - 0.5)(0, 1)$$


$$\text{Midpoint} = (0.5, 0) + (0, 0.5) = \left(\frac{1}{2}, \frac{1}{2}\right)$$


* **Step 3: Test if the midpoint belongs to the union**
For $\left(\frac{1}{2}, \frac{1}{2}\right)$ to be in $S_1 \cup S_2$, it must have *either* a $y$-value of $0$ (to be in $S_1$) or an $x$-value of $0$ (to be in $S_2$).
Since neither coordinate is zero:

$$\left(\frac{1}{2}, \frac{1}{2}\right) \notin S_1 \cup S_2$$



**Conclusion:** The line segment leaves the set space. Thus, $S_1 \cup S_2$ is **not** a convex set.

---

## 3. Property 3: Scalar Multiplication ($\alpha C$)

### 💡 Simple Meaning

If you take a convex shape and multiply every coordinate inside it by a constant scale factor $\alpha$ (which effectively expands, shrinks, mirrors, or shifts the shape), the resulting resized shape remains perfectly convex.

### 📐 Step-by-Step Formal Proof

Let $C$ be a convex set in $\mathbb{R}^n$ and $\alpha$ be a real scalar value. The scaled set is defined as:


$$\alpha C = \{\alpha c : c \in C\}$$

* **Step 1: Choose two random points $x$ and $y$ from the newly scaled set**

$$let \quad x, y \in \alpha C$$


* **Step 2: Relate them back to original source elements**
Since $x$ and $y$ belong to $\alpha C$, there must exist two original points $c_1, c_2 \in C$ such that:

$$x = \alpha c_1 \quad \text{and} \quad y = \alpha c_2$$


* **Step 3: Build a convex combination line segment using parameter $\lambda \in [0, 1]$**

$$\lambda x + (1-\lambda)y = \lambda(\alpha c_1) + (1-\lambda)(\alpha c_2)$$


* **Step 4: Algebraically factor out the common scalar value $\alpha$**

$$\lambda x + (1-\lambda)y = \alpha \left[ \lambda c_1 + (1-\lambda)c_2 \right]$$


* **Step 5: Check structural membership**
Because the base set $C$ is fundamentally convex, the inner term $\lambda c_1 + (1-\lambda)c_2$ is guaranteed to belong to $C$. Therefore, $\alpha$ times that internal element must belong to $\alpha C$:

$$\implies \alpha \left[ \lambda c_1 + (1-\lambda)c_2 \right] \in \alpha C$$



**Conclusion:** Since the blend stays inside the scaled boundary, the set $\alpha C$ is convex.


# Mathematical Optimization: Convex and Concave Functions

---

## 1. Concept: Convex Functions

### 💡 Simple Meaning
Geometrically, a function is **convex** if you pick any two points on its curve and draw a straight line (a chord) between them, the actual curve of the function always sits **below or touches** that straight line. Think of it as a bowl that opens upward.

### 📐 Formal Mathematical Definition
Let $S \subseteq \mathbb{R}^n$ be a convex set. A function $f: S \to \mathbb{R}$ is said to be **convex** over $S$ if for all $x_1, x_2 \in S$, and for all $\lambda$ with $0 \leq \lambda \leq 1$:

$$f(\lambda x_1 + (1 - \lambda)x_2) \leq \lambda f(x_1) + (1 - \lambda)f(x_2)$$

* **Strict Convexity:** If the inequality strictly holds ($<$) for distinct points $x_1 \neq x_2$ and $\lambda \in (0, 1)$, the function is called **strictly convex**.

### 🔍 Understanding the Algebraic Sides
* **Left-Hand Side ($f(\lambda x_1 + (1 - \lambda)x_2)$):** The height/value of the function at a weighted average position between $x_1$ and $x_2$.
* **Right-Hand Side ($\lambda f(x_1) + (1 - \lambda)f(x_2)$):** The height/value of the straight chord connecting the two points $(x_1, f(x_1))$ and $(x_2, f(x_2))$.

---

## 2. Geometrical Interpretation Graph

Below is a visual mapping of the mathematical variables onto an upward-opening curve:

```text
       y = f(x)
          \                                /
           \   A [x1, f(x1)]              / B [x2, f(x2)]
            \    *-----------------------*
             \    \        Chord        /
              \    \                   /
               \    \      D          /
                \    \     |         /
                 \    \    |        /
                  \    \   |       /
                   \    '--*------'
                    \      C [x, f(x)]
                     '-------------'
  -------------------------|-------------------------> X-Axis
                          x = λx1 + (1-λ)x2

```

### Key Position Mappings:

* **Point A:** $(x_1, f(x_1))$ — The first boundary coordinate on the function.
* **Point B:** $(x_2, f(x_2))$ — The second boundary coordinate on the function.
* **Point C:** Represents the actual curve position: $(x, f(\lambda x_1 + (1 - \lambda)x_2))$.
* **Point D:** Represents the chord line position: $(x, \lambda f(x_1) + (1 - \lambda)f(x_2))$.
* **Geometric Rule:** For a convex function, the segment $PC$ (height to curve) must always be less than or equal to $PD$ (height to chord).

---

## 3. Concept: Concave Functions

### 💡 Simple Meaning

A function is **concave** if it behaves exactly opposite to a convex function. If you connect any two points on its curve with a straight line chord, the actual curve of the function always sits **above or touches** that line. Think of it as a dome that opens downward.

### 📐 Formal Mathematical Definition

Let $S \subseteq \mathbb{R}^n$ be a convex set. A function $f: S \to \mathbb{R}$ is said to be **concave** over $S$ if for all $x_1, x_2 \in S$, and for all $\lambda$ with $0 \leq \lambda \leq 1$:

$$f(\lambda x_1 + (1 - \lambda)x_2) \geq \lambda f(x_1) + (1 - \lambda)f(x_2)$$

### 🔄 Duality Rule

A function $f$ is concave if and only if its negative image $-f$ is a convex function.

---

## 4. Worked Problems with Step-by-Step Calculations

### Problem 1: Proving $f(x) = x^2$ is Convex using Definition

**Concept:** Verifying convexity through basic algebraic definition over the domain $\mathbb{R}$.

#### Step-by-Step Calculations:

* **Step 1: Set up the expansion equation**
Let $x_1$ and $x_2$ be two real numbers, and $\lambda \in [0, 1]$. We must evaluate:

$$f(\lambda x_1 + (1-\lambda)x_2) = (\lambda x_1 + (1-\lambda)x_2)^2$$


* **Step 2: Expand the quadratic expression**

$$= \lambda^2 x_1^2 + 2\lambda(1-\lambda)x_1 x_2 + (1-\lambda)^2 x_2^2$$


* **Step 3: Set up the target chord equation (RHS)**

$$\lambda f(x_1) + (1-\lambda)f(x_2) = \lambda x_1^2 + (1-\lambda)x_2^2$$


* **Step 4: Analyze the difference (Chord minus Curve)**

$$\text{Difference} = [\lambda x_1^2 + (1-\lambda)x_2^2] - [\lambda^2 x_1^2 + 2\lambda(1-\lambda)x_1 x_2 + (1-\lambda)^2 x_2^2]$$



Group the $x_1^2$ and $x_2^2$ terms:

$$= (\lambda - \lambda^2)x_1^2 - 2\lambda(1-\lambda)x_1 x_2 + ((1-\lambda) - (1-\lambda)^2)x_2^2$$



Factor out $\lambda(1-\lambda)$:

$$= \lambda(1-\lambda)x_1^2 - 2\lambda(1-\lambda)x_1 x_2 + \lambda(1-\lambda)x_2^2$$


$$= \lambda(1-\lambda)[x_1^2 - 2\times_1 x_2 + x_2^2]$$


$$= \lambda(1-\lambda)(x_1 - x_2)^2$$


* **Step 5: Verify the sign of the result**
* Since $\lambda \in [0, 1]$, the term $\lambda(1-\lambda) \geq 0$.
* The term $(x_1 - x_2)^2$ is a squared real number, so it is always $\geq 0$.
* Therefore, $\text{Difference} \geq 0$, which mathematically translates to:

$$\lambda f(x_1) + (1-\lambda)f(x_2) \geq f(\lambda x_1 + (1-\lambda)x_2)$$





**Conclusion:** The chord is always above or equal to the function curve. Hence, $f(x) = x^2$ is a **convex function**.

---

### Problem 2: Proving $f(x) = 2x + 5$ is both Convex and Concave (Linear)

**Concept:** Linear functions have straight curves where chords lay exactly on top of the function values.

#### Step-by-Step Calculations:

* **Step 1: Evaluate the function over a blended position**

$$f(\lambda x_1 + (1-\lambda)x_2) = 2(\lambda x_1 + (1-\lambda)x_2) + 5$$


$$= 2\lambda x_1 + 2(1-\lambda)x_2 + 5$$


* **Step 2: Distribute the constant '5' using the identity $\lambda + (1-\lambda) = 1$**

$$= 2\lambda x_1 + 2(1-\lambda)x_2 + 5(\lambda + (1-\lambda))$$


$$= 2\lambda x_1 + 2(1-\lambda)x_2 + 5\lambda + 5(1-\lambda)$$


* **Step 3: Group the terms by their parameter scaling weights**

$$= \lambda(2x_1 + 5) + (1-\lambda)(2x_2 + 5)$$


$$= \lambda f(x_1) + (1-\lambda)f(x_2)$$



**Conclusion:** Because $f(\lambda x_1 + (1-\lambda)x_2) = \lambda f(x_1) + (1-\lambda)f(x_2)$, it satisfies both the convex ($\leq$) and concave ($\geq$) constraints simultaneously. Linear functions are always **both convex and concave**.



# Lecture 37: Examples & Properties of Convex and Concave Functions

---

## 1. Core Definitions & Example Analyses

### 💡 Simple Meaning Recap
* **Convex Function:** The function curve curves upward like a bowl. Geometrically, if you draw a straight line (chord) between any two points on the graph, the function curve sits **on or below** that line.
* **Concave Function:** The function curve caps downward like a dome. A straight line chord connecting two points on the graph sits **on or above** the curve.
* **Neither:** The function changes its curving behavior across its domain (e.g., bends upward in one region and downward in another).

---

### Example 1: Absolute Value Function (Convex)
* **Concept Name:** Absolute Value Convexity
* **Function:** $f : \mathbb{R} \to \mathbb{R}$, $f(x) = \vert{}x\vert{}$

#### 📈 Geometric Graph
```text
          Y-Axis
            ^
     \      |      /
      \     |     /   <-- f(x) = |x|
       \    |    /
________\___|___/________> X-Axis
            |

```

#### Step-by-Step Proof & Calculations:

1. **Choose Definition Inequality:** A function is convex if $f(\lambda x_1 + (1-\lambda)x_2) \leq \lambda f(x_1) + (1-\lambda)f(x_2)$.
2. **Substitute $f(x) = \vert{}x\vert{}$:**

$$\vert{}\lambda x_1 + (1-\lambda)x_2\vert{}$$


3. **Apply Triangle Inequality Property ($\vert{}a + b\vert{} \leq \vert{}a\vert{} + \vert{}b\vert{}$):**

$$\vert{}\lambda x_1 + (1-\lambda)x_2\vert{} \leq \vert{}\lambda x_1\vert{} + \vert{}(1-\lambda)x_2\vert{}$$


4. **Factor out $\lambda$** (Since $0 \leq \lambda \leq 1$, $\vert{}\lambda\vert{} = \lambda$ and $\vert{}1-\lambda\vert{} = 1-\lambda$):

$$\leq \lambda \vert{}x_1\vert{} + (1-\lambda)\vert{}x_2\vert{}$$


5. **Conclusion:** Because the step-by-step math yields a true inequality statement, $f(x) = \vert{}x\vert{}$ is **convex**.

---

### Example 2: Negative Monomial Function (Concave)

* **Concept Name:** Polynomial Curvature Inversion
* **Function:** $f : \mathbb{R} \to \mathbb{R}$, $f(x) = -x^4$

#### Step-by-Step Explanation & Calculations:

1. **Use Second Derivative Test for Concavity:** If $f''(x) \leq 0$ for all $x$, the function is concave.
2. **First Derivative ($f'(x)$):**

$$f'(x) = \frac{d}{dx}(-x^4) = -4x^3$$


3. **Second Derivative ($f''(x)$):**

$$f''(x) = \frac{d}{dx}(-4x^3) = -12x^2$$


4. **Analyze the Sign:** Since $x^2 \geq 0$ for all real numbers, multiplying by $-12$ guarantees that $-12x^2 \leq 0$.
5. **Conclusion:** Since $f''(x) \leq 0$ everywhere, $f(x) = -x^4$ is strictly a **concave function**.

---

### Example 3: Linear Function (Both Convex and Concave)

* **Concept Name:** Affine Duality
* **Function:** $f : \mathbb{R} \to \mathbb{R}$, $f(x) = 4x + 1$

#### Step-by-Step Explanation & Calculations:

1. **Evaluate Curve Expression:**

$$f(\lambda x_1 + (1-\lambda)x_2) = 4(\lambda x_1 + (1-\lambda)x_2) + 1$$


$$= 4\lambda x_1 + 4(1-\lambda)x_2 + 1(\lambda + (1-\lambda))$$


$$= \lambda(4x_1 + 1) + (1-\lambda)(4x_2 + 1)$$


2. **Compare to Chord Expression:**

$$\lambda f(x_1) + (1-\lambda)f(x_2) = \lambda(4x_1 + 1) + (1-\lambda)(4x_2 + 1)$$


3. **Conclusion:** Both sides are exactly identical ($=$). Because it satisfies both $\leq$ (convexity condition) and $\geq$ (concavity condition) at the same time, it is **both a convex and a concave function**.

---

### Example 4: Cubic Function (Neither Convex nor Concave)

* **Concept Name:** Inflection Points
* **Function:** $f : \mathbb{R} \to \mathbb{R}$, $f(x) = x^3$

#### 📈 Geometric Graph

```text
            Y-Axis
              ^       /
              |      /   <-- Convex here (x > 0)
              |    .'
______________|__.'________> X-Axis
            .'|
           /  |   <-- Concave here (x < 0)
          /   v

```

#### Step-by-Step Explanation & Calculations:

1. **Find Second Derivative ($f''(x)$):**

$$f'(x) = 3x^2 \implies f''(x) = 6x$$


2. **Evaluate the Output Signs across Domain:**
* When $x > 0$, $f''(x) > 0 \implies$ The function behaves **convexly**.
* When $x < 0$, $f''(x) < 0 \implies$ The function behaves **concavely**.


3. **Conclusion:** Since the entire global domain $\mathbb{R}$ contains conflicting shapes, the function as a whole is **neither convex nor concave**.

---

### Example 5: Exponential Function (Convex)

* **Concept Name:** Strict Monotone Convex Growth
* **Function:** $f : \mathbb{R} \to \mathbb{R}$, $f(x) = e^x$

#### 📈 Geometric Graph

```text
          Y-Axis
            ^         / <-- f(x) = e^x
            |       .'
            |   _.-'
____________|_-'___________> X-Axis
            |

```

* **Explanation:** The second derivative is $f''(x) = e^x$. Since $e^x > 0$ for all real values of $x$, the curve is strictly opening upward, making it a **convex function**.

---

### Example 6: Trigonometric Sine Function (Concave over Interval)

* **Concept Name:** Restricted Bounded Domain Concavity
* **Function:** $f : [0, \pi] \to \mathbb{R}$, $f(x) = \sin x$

#### 📈 Geometric Graph

```text
          Y-Axis
            ^      _.-._
            |    .'     '.  <-- Chord line sits below curve
            |   /         \
____________|__/___________\____> X-Axis
          (0,0)             π

```

* **Explanation:** Over the restricted domain interval from $0$ to $\pi$, the second derivative is $f''(x) = -\sin x$. Because $\sin x \geq 0$ within this region, $f''(x) \leq 0$. This confirms it functions as a **concave function** on $[0, \pi]$.

---

## 2. Mathematical Properties of Convex Functions

### Property 1: Sum of Two Convex Functions

If $f : \mathbb{R}^n \to \mathbb{R}$ and $g : \mathbb{R}^n \to \mathbb{R}$ are both individual convex functions, then their combined added sum $(f + g)(x) = f(x) + g(x)$ is guaranteed to be a **convex function**.

### Property 2: Scalar Multiples

If $f : \mathbb{R}^n \to \mathbb{R}$ is a validated convex function, multiplying it by a scalar constant $\alpha$ changes the dynamic behavior depending on the sign of $\alpha$:

* **$\alpha f$ remains a convex function** if $\alpha > 0$ (Positive scaling).
* **$\alpha f$ transforms into a concave function** if $\alpha < 0$ (Negative scaling flips the curve downside up).

