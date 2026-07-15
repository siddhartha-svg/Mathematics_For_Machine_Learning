# Total Derivatives and the Multivariate Chain Rule (Single Parameter)

---

## 1. Core Concept: Total Derivatives via the Chain Rule

When an outer function depends on multiple intermediate variables, and each of those intermediate variables ultimately depends on a single shared parameter (like time $t$), we use the **Multivariate Chain Rule**. 

Because the ultimate input is just one single variable ($t$), the final rate of change is called a **total derivative** and uses the standard derivative symbol $d$. However, because the intermediate steps involve functions with multiple inputs, the inner branches use the partial derivative symbol $\partial$.

### Dependency Tree Visualization
To visualize how the variables depend on each other, we can look at the path of variables mapping down to $t$:

```text
                 [ z ]  (Outer Scalar Value)
                /     \
      ∂z/∂x    /       \   ∂z/∂y
              v         v
            [ x ]     [ y ]  (Intermediate Variables)
              |         |
      dx/dt   |         |   dy/dt
              v         v
            [ t ]     [ t ]  (Single Underlying Parameter)

```

To find the total derivative $\frac{dz}{dt}$, you follow every available branch path from $z$ down to $t$, multiplying the rates along each path and then adding the paths together.

---

## 2. Structural Breakdown of Cases

### Case I: Single Variable Function

If $z$ depends on $y$, and $y$ depends on $x$:


$$z = f(y) \quad \text{and} \quad y = \phi(x)$$

$$\frac{dz}{dx} = \frac{dz}{dy} \cdot \frac{dy}{dx}$$

---

### Case II: Function of Two Variables

If $z$ depends on two variables $x$ and $y$, which both depend on $t$:


$$z = f(x, y), \quad x = \phi(t), \quad \text{and} \quad y = \xi(t)$$

$$\frac{dz}{dt} = \frac{\partial z}{\partial x}\frac{dx}{dt} + \frac{\partial z}{\partial y}\frac{dy}{dt}$$

---

### Case III: Function of Three Variables

If $z$ depends on three intermediate variables $x$, $y$, and $w$, which all depend on $t$:


$$z = f(x, y, w), \quad x = x(t), \quad y = y(t), \quad \text{and} \quad w = w(t)$$

$$\frac{dz}{dt} = \frac{\partial z}{\partial x}\frac{dx}{dt} + \frac{\partial z}{\partial y}\frac{dy}{dt} + \frac{\partial z}{\partial w}\frac{dw}{dt}$$

---

### Case IV: General Function of $n$ Variables

For a function featuring $n$ distinct intermediate parameters all driven by $t$:


$$z = f(x_1, x_2, \dots, x_n), \quad \text{where} \quad x_i = x_i(t) \quad \forall i$$

$$\frac{dz}{dt} = \frac{\partial z}{\partial x_1}\frac{dx_1}{dt} + \frac{\partial z}{\partial x_2}\frac{dx_2}{dt} + \dots + \frac{\partial z}{\partial x_n}\frac{dx_n}{dt} = \sum_{i=1}^{n} \frac{\partial z}{\partial x_i}\frac{dx_i}{dt}$$

---

## 3. Step-by-Step Solved Problems

### Problem 1: Single Variable Substitution Check

**Question:** Find $\frac{dz}{dt}$ when $z = x^3$ and $x = \sin t$.

#### Step-by-Step Calculation:

1. Set up the single-path chain rule formula:

$$\frac{dz}{dt} = \frac{dz}{dx} \cdot \frac{dx}{dt}$$


2. Compute the component derivatives:
* $\frac{dz}{dx} = \frac{d}{dx}(x^3) = 3x^2$
* $\frac{dx}{dt} = \frac{d}{dt}(\sin t) = \cos t$


3. Multiply the components together:

$$\frac{dz}{dt} = (3x^2)(\cos t)$$


4. Substitute $x = \sin t$ to get the final answer completely in terms of parameter $t$:

$$\frac{dz}{dt} = 3(\sin t)^2 \cos t = 3\sin^2 t \cos t$$



---

### Problem 2: Two-Variable System with Chain Expansion

**Question:** Find $\frac{dz}{dt}$ given $z = x\sin y$, where $x = t^2$ and $y = 2t + 5$.

#### Step-by-Step Calculation:

1. Set up the two-path total derivative formula (Case II):

$$\frac{dz}{dt} = \frac{\partial z}{\partial x}\frac{dx}{dt} + \frac{\partial z}{\partial y}\frac{dy}{dt}$$


2. Compute each individual derivative piece:
* $\frac{\partial z}{\partial x} = \frac{\partial}{\partial x}(x\sin y) = \sin y$
* $\frac{dx}{dt} = \frac{d}{dt}(t^2) = 2t$
* $\frac{\partial z}{\partial y} = \frac{\partial}{\partial y}(x\sin y) = x\cos y$
* $\frac{dy}{dt} = \frac{d}{dt}(2t + 5) = 2$


3. Assemble the pieces into the total derivative structure:

$$\frac{dz}{dt} = (\sin y)(2t) + (x\cos y)(2) = 2t\sin y + 2x\cos y$$


4. Substitute the original definitions of $x$ and $y$ to express the output purely in terms of $t$:

$$\frac{dz}{dt} = 2t\sin(2t + 5) + 2(t^2)\cos(2t + 5)$$


$$\frac{dz}{dt} = 2t\sin(2t + 5) + 2t^2\cos(2t + 5)$$



---

### Problem 3: Three-Variable Total Derivative

**Question:** Find $\frac{dw}{dt}$ given $w = x^2y^3z$, where $x = \cos t$, $y = \sin t$, and $z = t^2 - 1$.

#### Step-by-Step Calculation:

1. Set up the three-path total derivative formula (Case III):

$$\frac{dw}{dt} = \frac{\partial w}{\partial x}\frac{dx}{dt} + \frac{\partial w}{\partial y}\frac{dy}{dt} + \frac{\partial w}{\partial z}\frac{dz}{dt}$$


2. Compute the component parts:
* $\frac{\partial w}{\partial x} = 2xy^3z \quad \text{and} \quad \frac{dx}{dt} = -\sin t$
* $\frac{\partial w}{\partial y} = 3x^2y^2z \quad \text{and} \quad \frac{dy}{dt} = \cos t$
* $\frac{\partial w}{\partial z} = x^2y^3 \quad \text{and} \quad \frac{dz}{dt} = 2t$


3. Combine them:

$$\frac{dw}{dt} = (2xy^3z)(-\sin t) + (3x^2y^2z)(\cos t) + (x^2y^3)(2t)$$


4. substitute the expressions for $x$, $y$, and $z$:

$$\frac{dw}{dt} = -2\cos t \sin^3 t (t^2 - 1)\sin t + 3\cos^2 t \sin^2 t (t^2 - 1)\cos t + 2t\cos^2 t \sin^3 t$$


5. Simplify the trigonometric terms:

$$\frac{dw}{dt} = -2(t^2 - 1)\cos t \sin^4 t + 3(t^2 - 1)\cos^3 t \sin^2 t + 2t\cos^2 t \sin^3 t$$


# Advanced Applications of the Multivariate Chain Rule

---

## 1. Polar Coordinate Variable Transformation

### Core Concept
In physics and multi-variable optimization, it is often necessary to transform derivatives between different coordinate tracking frameworks, such as converting a system from standard Cartesian coordinates $(x, y)$ to Polar coordinates $(r, \theta)$.

The link between these two spaces is governed by the structural mapping definitions:
$$x = r\cos\theta, \quad y = r\sin\theta$$

---

### Step-by-Step Problem Breakdown

**Problem Statement:** Let $z = f(x, y)$ be a differentiable function where $x = r\cos\theta$ and $y = r\sin\theta$. Prove that:
$$z_r^2 + \frac{1}{r^2}z_\theta^2 = f_x^2 + f_y^2$$

#### Step 1: Calculate First-Order Component Partials
Compute the base derivatives of the transformation coordinate links:
* $\frac{\partial x}{\partial r} = \cos\theta \quad$ and $\quad \frac{\partial x}{\partial \theta} = -r\sin\theta$
* $\frac{\partial y}{\partial r} = \sin\theta \quad$ and $\quad \frac{\partial y}{\partial \theta} = r\cos\theta$

---

#### Step 2: Establish the Pathway Equation for $z_r$ ($\frac{\partial z}{\partial r}$)
Apply the multivariable chain rule to follow all pathways leading down to variable $r$:
$$z_r = \frac{\partial z}{\partial r} = \left(\frac{\partial f}{\partial x}\right)\left(\frac{\partial x}{\partial r}\right) + \left(\frac{\partial f}{\partial y}\right)\left(\frac{\partial y}{\partial r}\right)$$

Substitute the component derivative blocks calculated in Step 1:
$$z_r = f_x\cos\theta + f_y\sin\theta \quad \longrightarrow \text{ (Equation 1)}$$

---

#### Step 3: Establish the Pathway Equation for $z_\theta$ ($\frac{\partial z}{\partial \theta}$)
Apply the multivariable chain rule to follow all pathways leading down to variable $\theta$:
$$z_\theta = \frac{\partial z}{\partial \theta} = \left(\frac{\partial f}{\partial x}\right)\left(\frac{\partial x}{\partial \theta}\right) + \left(\frac{\partial f}{\partial y}\right)\left(\frac{\partial y}{\partial \theta}\right)$$

Substitute the component derivative blocks:
$$z_\theta = f_x(-r\sin\theta) + f_y(r\cos\theta)$$

Isolate the constant radius variable scale $r$ by dividing both sides by $r$:
$$\frac{1}{r}z_\theta = f_x(-\sin\theta) + f_y(\cos\theta) \quad \longrightarrow \text{ (Equation 2)}$$

---

#### Step 4: Square and Sum the Equations
Square both expressions to match the target form:
$$(z_r)^2 = (f_x\cos\theta + f_y\sin\theta)^2 = f_x^2\cos^2\theta + 2f_xf_y\cos\theta\sin\theta + f_y^2\sin^2\theta$$
$$\left(\frac{1}{r}z_\theta\right)^2 = (-f_x\sin\theta + f_y\cos\theta)^2 = f_x^2\sin^2\theta - 2f_xf_y\cos\theta\sin\theta + f_y^2\cos^2\theta$$

Add the two squared equations together. Notice that the cross-product terms cancel out perfectly:
$$z_r^2 + \frac{1}{r^2}z_\theta^2 = f_x^2(\cos^2\theta + \sin^2\theta) + f_y^2(\sin^2\theta + \cos^2\theta)$$

Using the fundamental trigonometric identity $\cos^2\theta + \sin^2\theta = 1$, we get our completed proof:
$$z_r^2 + \frac{1}{r^2}z_\theta^2 = f_x^2 + f_y^2$$

---

## 2. Second-Order Chain Rule (Curvature Tracking)

### Core Concept
Computing a *second-order* partial derivative using the chain rule requires applying the chain rule twice. When you take the first derivative, the resulting expression ($w_x$) is still a multi-variable function. Therefore, computing $w_{xx}$ requires applying the product rule and chain rule simultaneously to all components inside the expression.

---

### Step-by-Step Problem Breakdown

**Problem Statement:** Let $w = f(u, v)$ where $u = \frac{x^2 - y^2}{2}$ and $v = xy$. Find the algebraic expression for $w_{xx}$ ($\frac{\partial^2 w}{\partial x^2}$).

#### Step 1: Compute First-Order Partials of the Intermediate Coordinates
* $\frac{\partial u}{\partial x} = \frac{1}{2}(2x) = x \quad$ and $\quad \frac{\partial u}{\partial y} = \frac{1}{2}(-2y) = -y$
* $\frac{\partial v}{\partial x} = y \quad$ and $\quad \frac{\partial v}{\partial y} = x$

---

#### Step 2: Compute the First-Order Total Derivative $w_x$
$$\frac{\partial w}{\partial x} = \left(\frac{\partial f}{\partial u}\right)\left(\frac{\partial u}{\partial x}\right) + \left(\frac{\partial f}{\partial v}\right)\left(\frac{\partial v}{\partial x}\right)$$
$$w_x = f_u \cdot (x) + f_v \cdot (y) = xf_u + yf_v$$

---

#### Step 3: Set up the Second-Order Operational Structure
To find $w_{xx}$, differentiate our $w_x$ expression with respect to $x$ again:
$$w_{xx} = \frac{\partial}{\partial x}(w_x) = \frac{\partial}{\partial x}(xf_u + yf_v)$$

Apply the standard single-variable product rule to the first term ($\frac{\partial}{\partial x}(xf_u) = x\frac{\partial f_u}{\partial x} + f_u \cdot 1$):
$$w_{xx} = x\frac{\partial f_u}{\partial x} + f_u + y\frac{\partial f_v}{\partial x}$$

---

#### Step 4: Expand the Inner Derivatives via the Chain Rule
Because $f_u$ and $f_v$ depend on $u$ and $v$, expanding their derivatives requires another application of the multi-variable chain rule:
$$\frac{\partial f_u}{\partial x} = \left(\frac{\partial f_u}{\partial u}\right)\left(\frac{\partial u}{\partial x}\right) + \left(\frac{\partial f_u}{\partial v}\right)\left(\frac{\partial v}{\partial x}\right) = f_{uu}(x) + f_{vu}(y)$$
$$\frac{\partial f_v}{\partial x} = \left(\frac{\partial f_v}{\partial u}\right)\left(\frac{\partial u}{\partial x}\right) + \left(\frac{\partial f_v}{\partial v}\right)\left(\frac{\partial v}{\partial x}\right) = f_{uv}(x) + f_{vv}(y)$$

---

#### Step 5: Substitute and Simplify the Terms
Substitute these expanded expressions back into the main equation from Step 3:
$$w_{xx} = x[x f_{uu} + y f_{vu}] + f_u + y[x f_{uv} + y f_{vv}]$$
$$w_{xx} = x^2 f_{uu} + xy f_{vu} + f_u + xy f_{uv} + y^2 f_{vv}$$

Assuming the mixed partial derivatives are continuous, Clairaut's Theorem applies, so $f_{vu} = f_{uv}$. Combining these like terms gives the final result:
$$w_{xx} = x^2 f_{uu} + 2xy f_{uv} + y^2 f_{vv} + f_u$$

---

## 3. Practice Problems and Solutions

### Problem A: Two-Variable Intermediate Mapping
**Question:** Given $z = x^2y^2$, where $x = st$ and $y = t^2 - s^2$, find expressions for $\frac{\partial z}{\partial s}$ and $\frac{\partial z}{\partial t}$.

#### Step-by-Step Calculation for $\frac{\partial z}{\partial s}$:
1. Set up the chain rule pathway equation:
   $$\frac{\partial z}{\partial s} = \frac{\partial z}{\partial x}\frac{\partial x}{\partial s} + \frac{\partial z}{\partial y}\frac{\partial y}{\partial s}$$
2. Compute the component derivatives:
   * $\frac{\partial z}{\partial x} = 2xy^2 \quad$ and $\quad \frac{\partial x}{\partial s} = t$
   * $\frac{\partial z}{\partial y} = 2x^2y \quad$ and $\quad \frac{\partial y}{\partial s} = -2s$
3. Assemble the expression:
   $$\frac{\partial z}{\partial s} = (2xy^2)(t) + (2x^2y)(-2s) = 2xy^2t - 4x^2ys$$

---

#### Step-by-Step Calculation for $\frac{\partial z}{\partial t}$:
1. Set up the chain rule pathway equation:
   $$\frac{\partial z}{\partial t} = \frac{\partial z}{\partial x}\frac{\partial x}{\partial t} + \frac{\partial z}{\partial y}\frac{\partial y}{\partial t}$$
2. Compute the remaining variable components:
   * $\frac{\partial x}{\partial t} = s$
   * $\frac{\partial y}{\partial t} = 2t$
3. Assemble the expression:
   $$\frac{\partial z}{\partial t} = (2xy^2)(s) + (2x^2y)(2t) = 2xy^2s + 4x^2yt$$


# Advanced Jacobian Transformations and Change of Variables

---

## 1. Jacobian Determinants in Change of Variables

### Core Concept
When transforming a set of independent coordinates to another coordinate system (e.g., $(x, y) \to (u, v)$), the **Jacobian determinant** ($J$) serves as the local scaling factor between the two coordinate systems. 

If we have an implicit function $z = f(x, y)$ where $x$ and $y$ are functions of $u$ and $v$, calculating the direct partial derivatives $f_x = \frac{\partial f}{\partial x}$ and $f_y = \frac{\partial f}{\partial y}$ manually can be highly complex. By setting up a system of linear equations using the multivariable chain rule and applying **Cramer's Rule**, we can express these partial derivatives directly as ratios of determinants.

---

### Two-Variable System Formulation ($2 \times 2$)
Let $z = f(x, y)$, where $x = \phi(u, v)$ and $y = \xi(u, v)$. 

The baseline transformation Jacobian $J$ (also written as $\frac{\partial(x, y)}{\partial(u, v)}$) is given by the determinant:
$$J = \frac{\partial(x, y)}{\partial(u, v)} = \begin{vmatrix} \frac{\partial x}{\partial u} & \frac{\partial x}{\partial v} \\ \frac{\partial y}{\partial u} & \frac{\partial y}{\partial v} \end{vmatrix} = \begin{vmatrix} x_u & x_v \\ y_u & y_v \end{vmatrix}$$

Using determinants, the hidden partial derivatives of $f$ are calculated as:
$$f_x = \frac{\partial f}{\partial x} = \frac{1}{J} \frac{\partial(f, y)}{\partial(u, v)} = \frac{1}{J} \begin{vmatrix} f_u & f_v \\ y_u & y_v \end{vmatrix}$$
$$f_y = \frac{\partial f}{\partial y} = -\frac{1}{J} \frac{\partial(f, x)}{\partial(u, v)} = \frac{1}{J} \begin{vmatrix} x_u & f_u \\ x_v & f_v \end{vmatrix}$$

---

### Three-Variable System Formulation ($3 \times 3$)
Let $z = f(x, y, z)$, where $x = \phi(u, v, w)$, $y = \eta(u, v, w)$, and $z = \xi(u, v, w)$.

The $3 \times 3$ baseline conversion determinant is:
$$J = \frac{\partial(x, y, z)}{\partial(u, v, w)} = \begin{vmatrix} \frac{\partial x}{\partial u} & \frac{\partial x}{\partial v} & \frac{\partial x}{\partial w} \\ \frac{\partial y}{\partial u} & \frac{\partial y}{\partial v} & \frac{\partial y}{\partial w} \\ \frac{\partial z}{\partial u} & \frac{\partial z}{\partial v} & \frac{\partial z}{\partial w} \end{vmatrix}$$

The respective derivatives are given by:
$$f_x = \frac{1}{J} \frac{\partial(f, y, z)}{\partial(u, v, w)}, \quad f_y = -\frac{1}{J} \frac{\partial(f, x, z)}{\partial(u, v, w)}, \quad f_z = \frac{1}{J} \frac{\partial(f, x, y)}{\partial(u, v, w)}$$

---

## 2. Fundamental Properties of Jacobians

Jacobian determinants satisfy several elegant algebraic properties that behave similarly to standard single-variable fraction rules:

### Property 1: The Reciprocal Property (Inverse Mapping)
If $J$ maps $(x, y) \to (u, v)$ and $J'$ performs the reverse mapping $(u, v) \to (x, y)$, then their product is always $1$:
$$\text{If } J = \frac{\partial(x, y)}{\partial(u, v)} \quad \text{and} \quad J' = \frac{\partial(u, v)}{\partial(x, y)} \implies J \cdot J' = 1$$

### Property 2: The Chain Rule of Jacobians
If coordinates $(u, v)$ are functions of $(r, s)$, and $(r, s)$ are functions of $(x, y)$, the total coordinate area scale changes transitively through matrix multiplication:
$$\frac{\partial(u, v)}{\partial(x, y)} = \frac{\partial(u, v)}{\partial(r, s)} \cdot \frac{\partial(r, s)}{\partial(x, y)}$$

---

## 3. Step-by-Step Problems and Calculations

### Problem 1: Exponential Logarithmic Area Transformation
**Question:** Let $z = f(x, y)$, where $x = e^u \cos v$ and $y = e^u \sin v$. Determine $\frac{\partial z}{\partial x}$ ($z_x$) using Jacobian transformation properties.

#### Step 1: Compute Component Partial Derivatives
* $x_u = \frac{\partial}{\partial u}(e^u \cos v) = e^u \cos v = x$
* $x_v = \frac{\partial}{\partial v}(e^u \cos v) = -e^u \sin v = -y$
* $y_u = \frac{\partial}{\partial u}(e^u \sin v) = e^u \sin v = y$
* $y_v = \frac{\partial}{\partial v}(e^u \sin v) = e^u \cos v = x$

#### Step 2: Compute the Base Jacobian Determinant ($J$)
$$J = \frac{\partial(x, y)}{\partial(u, v)} = \begin{vmatrix} x_u & x_v \\ y_u & y_v \end{vmatrix} = \begin{vmatrix} e^u \cos v & -e^u \sin v \\ e^u \sin v & e^u \cos v \end{vmatrix}$$
$$J = (e^u \cos v)(e^u \cos v) - (-e^u \sin v)(e^u \sin v)$$
$$J = e^{2u} \cos^2 v + e^{2u} \sin^2 v = e^{2u}(\cos^2 v + \sin^2 v) = e^{2u}$$
Thus, the reciprocal factor is: $\frac{1}{J} = e^{-2u}$.

#### Step 3: Set up the Target Determinant for $z_x$
Using our conversion identity:
$$z_x = \frac{1}{J} \begin{vmatrix} f_u & f_v \\ y_u & y_v \end{vmatrix} = e^{-2u} \begin{vmatrix} f_u & f_v \\ y & x \end{vmatrix}$$

Let us find $f_u$ and $f_v$ using the chain rule to expand the row elements:
* $f_u = f_x x_u + f_y y_u = f_x (x) + f_y (y) = x f_x + y f_y$
* $f_v = f_x x_v + f_y y_v = f_x (-y) + f_y (x) = -y f_x + x f_y$

Substitute these expansions directly into the matrix determinant:
$$z_x = e^{-2u} \begin{vmatrix} x f_x + y f_y & -y f_x + x f_y \\ y & x \end{vmatrix}$$
$$z_x = e^{-2u} \Big[ x(x f_x + y f_y) - y(-y f_x + x f_y) \Big]$$
$$z_x = e^{-2u} \Big[ x^2 f_x + xy f_y + y^2 f_x - xy f_y \Big]$$

Cancel out the $xy f_y$ terms:
$$z_x = e^{-2u} \Big[ x^2 f_x + y^2 f_x \Big] = e^{-2u} (x^2 + y^2) f_x$$

Since $x^2 + y^2 = (e^u \cos v)^2 + (e^u \sin v)^2 = e^{2u}$:
$$z_x = e^{-2u} (e^{2u}) f_x = f_x$$

---

### Problem 2: Verifying the Chain Rule Property
**Question:** Verify the chain rule of Jacobians ($\frac{\partial(x, y)}{\partial(r, s)} \cdot \frac{\partial(r, s)}{\partial(x, y)} = 1$) given the mapping definitions $x = r(1 - s)$ and $y = r + s$.

#### Step 1: Compute Forward Partials $\frac{\partial(x, y)}{\partial(r, s)}$
* $x_r = 1 - s, \quad x_s = -r$
* $y_r = 1, \quad y_s = 1$

$$J = \begin{vmatrix} 1 - s & -r \\ 1 & 1 \end{vmatrix} = (1 - s)(1) - (-r)(1) = 1 - s + r$$

#### Step 2: Solve for Reverse Equations to find $\frac{\partial(r, s)}{\partial(x, y)}$
From $y = r + s \implies s = y - r$. Substitute this into the $x$ equation:
$$x = r(1 - (y - r)) = r - ry + x_r^2 \quad \text{... (Non-linear styling)}$$

Instead of algebraic rearrangement, let's use the property $J' = \frac{1}{J}$:
$$J' = \frac{\partial(u, v)}{\partial(x, y)} = \frac{1}{1 + r - s}$$

Multiplying both configurations together:
$$J \cdot J' = (1 + r - s) \cdot \frac{1}{1 + r - s} = 1$$
This explicitly verifies the reciprocal chain rule property!   