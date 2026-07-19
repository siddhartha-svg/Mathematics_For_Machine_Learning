
# Comprehensive Notes: Calculus using Python (SymPy)

This guide covers how to use the **SymPy** library in Python to perform mathematical differentiation (finding derivatives). It includes simple explanations, step-by-step code analysis, mathematical calculations, extra practice problems, and illustrative text-based graphs.

---

## 1. Concept Introduction: Calculus & SymPy

*   **What is a Derivative?** In simple terms, a derivative measures how fast something is changing at a specific moment. For a graph, it represents the slope (steepness) of the curve at any given point.
*   **What is SymPy?** It is a Python library used for **symbolic mathematics**. Instead of calculating approximate decimal answers, it solves math problems exactly with algebraic symbols (like $x, y, z$).

---

## 2. Basic Differentiation (First-Order Derivative)

### Concept Name: Simple Derivative
Finding the derivative of a single trigonometric function with respect to $x$.

### Python Implementation
```python
import sympy as sym

# Define 'x' as a mathematical symbol
x = sym.symbols('x')

# Calculate the first derivative of sin(x)
derivative1 = sym.diff(sym.sin(x), x)
print(derivative1)
# Output: cos(x)

```

### Step-by-Step Explanation & Calculation

1. **`import sympy as sym`**: Loads the SymPy library.
2. **`x = sym.symbols('x')`**: Tells Python to treat the letter `x` as an algebraic variable rather than a standard programming string or number.
3. **`sym.diff(sym.sin(x), x)`**: The `diff(function, variable)` syntax tells Python to differentiate $\sin(x)$ with respect to $x$.

**Mathematical Proof:**


$$\frac{d}{dx}[\sin(x)] = \cos(x)$$

---

## 3. Applying the Chain Rule

### Concept Name: Composite Function Differentiation

When a function sits inside another function (e.g., $x^2$ inside a $\sin$ function), we must apply the **Chain Rule**.

### Python Implementation

```python
import sympy as sym

x = sym.symbols('x')

# Differentiate sin(x^2) with respect to x
derivative1 = sym.diff(sym.sin(x**2), x)
print(derivative1)
# Output: 2*x*cos(x**2)

```

### Step-by-Step Explanation & Calculation

* **Outside Function:** $\sin(u)$ where $u = x^2$. Its derivative is $\cos(u)$.
* **Inside Function:** $x^2$. Its derivative is $2x$.

**Mathematical Calculation:**


$$\text{Chain Rule Formula: } \frac{d}{dx}[f(g(x))] = f'(g(x)) \cdot g'(x)$$

$$\frac{d}{dx}[\sin(x^2)] = \cos(x^2) \cdot \frac{d}{dx}[x^2]$$

$$\frac{d}{dx}[\sin(x^2)] = \cos(x^2) \cdot 2x = 2x\cos(x^2)$$

---

## 4. Combinations of Functions (Sum Rule)

### Concept Name: Sum Rule & Exponential Differentiation

Differentiating an expression containing a sum of two different functions: a trigonometric power function and an exponential function.

### Python Implementation

```python
import sympy as sym

x = sym.symbols('x')

# Define the complex function
func = sym.sin(x)**2 + sym.exp(x**2)

# Differentiate the function
derivative1 = sym.diff(func, x)
print(derivative1)
# Output: 2*x*exp(x**2) + 2*sin(x)*cos(x)

```

### Step-by-Step Explanation & Calculation

We break the expression into two parts and differentiate them individually:

* **Part 1: $\sin^2(x)$**

$$\frac{d}{dx}[(\sin(x))^2] = 2\sin(x) \cdot \frac{d}{dx}[\sin(x)] = 2\sin(x)\cos(x)$$


* **Part 2: $e^{x^2}$**

$$\frac{d}{dx}[e^{x^2}] = e^{x^2} \cdot \frac{d}{dx}[x^2] = e^{x^2} \cdot 2x = 2xe^{x^2}$$



**Total Sum Calculation:**


$$\frac{d}{dx}[\sin^2(x) + e^{x^2}] = 2\sin(x)\cos(x) + 2xe^{x^2}$$

---

## 5. Higher-Order Derivatives

### Concept Name: Second Derivative

Finding the derivative of a derivative. This represents acceleration if the original function measures position.

### Python Implementation

```python
import sympy as sym

# Syntax guide: sym.diff(function, variable, order)
x = sym.symbols('x')
func = sym.sin(x)**2 + sym.exp(x**2)

# Calculate the 2nd derivative by passing '2' as the third argument
derivative2 = sym.diff(func, x, 2)
print(derivative2)
# Output: 2*(2*x**2*exp(x**2) + exp(x**2) - sin(x)**2 + cos(x)**2)

```

### Step-by-Step Explanation & Calculation

We take our previous first derivative result and differentiate it a second time.


$$\text{First Derivative } (f') = 2\sin(x)\cos(x) + 2xe^{x^2}$$

* **Differentiating $2\sin(x)\cos(x)$ using Product Rule:**

$$\frac{d}{dx}[2\sin(x)\cos(x)] = 2\cos(x)\cos(x) + 2\sin(x)(-\sin(x)) = 2\cos^2(x) - 2\sin^2(x)$$


* **Differentiating $2xe^{x^2}$ using Product Rule:**

$$\frac{d}{dx}[2x \cdot e^{x^2}] = 2(e^{x^2}) + 2x(2xe^{x^2}) = 2e^{x^2} + 4x^2e^{x^2}$$



**Combining and Factoring Out 2:**


$$f'' = 2\cos^2(x) - 2\sin^2(x) + 2e^{x^2} + 4x^2e^{x^2}$$

$$f'' = 2(2x^2e^{x^2} + e^{x^2} - \sin^2(x) + \cos^2(x))$$

---

## 6. Multi-Variable Functions (Partial Derivatives)

### Concept Name: Partial Differentiation

When an equation contains multiple variables ($x, y, z$), a **partial derivative** finds how the expression changes with respect to *one* chosen variable while treating all other variables like static numbers (constants).

### Python Implementation

```python
import sympy as sym

# Define multiple symbols at once
x, y, z = sym.symbols('x,y,z')

func = x**3 * y + y**2 + z**3

# Partially differentiate with respect to x only
deriv1_x = sym.diff(func, x)
print(deriv1_x)
# Output: 3*x**2*y

```

### Step-by-Step Explanation & Calculation

We are differentiating $f(x,y,z) = x^3y + y^2 + z^3$ strictly with respect to $x$. Therefore, $y$ and $z$ are treated as constant numbers.

* **Term 1 ($x^3y$):** $y$ is a constant multiplier. $\frac{d}{dx}[x^3 \cdot y] = 3x^2 \cdot y$.
* **Term 2 ($y^2$):** Contains no $x$, so its derivative is $0$.
* **Term 3 ($z^3$):** Contains no $x$, so its derivative is $0$.

**Final Calculation:**


$$\frac{\partial}{\partial x}[x^3y + y^2 + z^3] = 3x^2y + 0 + 0 = 3x^2y$$

---

## 7. Additional Practice Problems

### Problem 1: Quotient Rule

**Find the derivative of:** $f(x) = \frac{\ln(x)}{x}$

```python
# Code snippet to test:
func = sym.log(x) / x
print(sym.diff(func, x))
# Output: -log(x)/x**2 + 1/x**2  ==>  (1 - log(x)) / x**2

```

**Manual Calculation Steps:**


$$\text{Formula: } \frac{u'v - uv'}{v^2}$$

$$u = \ln(x) \rightarrow u' = \frac{1}{x}$$

$$v = x \rightarrow v' = 1$$

$$f'(x) = \frac{(\frac{1}{x} \cdot x) - (\ln(x) \cdot 1)}{x^2} = \frac{1 - \ln(x)}{x^2}$$

### Problem 2: Partial Derivative with respect to $y$

**Using the same function from Section 6:** $f(x,y,z) = x^3y + y^2 + z^3$, find $\frac{\partial f}{\partial y}$.

```python
# Code snippet to test:
print(sym.diff(x**3*y + y**2 + z**3, y))
# Output: x**3 + 2*y

```

**Manual Calculation Steps:**

* Treat $x$ and $z$ as constants.
* $\frac{\partial}{\partial y}[x^3y] = x^3$
* $\frac{\partial}{\partial y}[y^2] = 2y$
* $\frac{\partial}{\partial y}[z^3] = 0$
* **Result:** $x^3 + 2y$

---

## 8. Visualizing Derivatives (Concept Graph)

Below is a conceptual text-based graph showing a function $f(x) = x^2$ alongside its derivative line (slope) at a given point.

```text
Value of y 
    ^
    |          / [f(x) = x^2 Curve]
16  |         *  
    |        / \ 
    |       /   \  <-- Tangent Line showing Slope at x=2
4   |------*     \     (Slope / Derivative at this point is 2*x = 4)
    |     /|      \
0   +----+---------+--------> Value of x
         0 2       4

```

```

```




# Advanced Calculus Notes using Python (SymPy)

This guide covers advanced symbolic calculus operations using **SymPy**, focusing on **Partial Derivatives**, **Higher-Order Partial Derivatives**, and **Integration**.

---

## 1. Concept Name: First-Order Partial Derivatives

### Simple Meaning
When a function contains multiple independent variables (like $x, y, z$), a **partial derivative** finds the rate of change with respect to *one* variable while treating all other variables as fixed constants.

### Python Implementation
```python
import sympy as sym

# Step 1: Define multiple mathematical symbols
x, y, z = sym.symbols('x,y,z')

# Step 2: Write out the multivariable function
func = x**3 * y + y**2 + z**3

# Step 3: Differentiate with respect to y only
deriv1_y = sym.diff(func, y)
print(deriv1_y)
# Output: x**3 + 2*y

```

### Step-by-Step Mathematical Calculation

Given the function:


$$f(x, y, z) = x^3y + y^2 + z^3$$

To find the partial derivative with respect to $y$ ($\frac{\partial f}{\partial y}$), treat $x$ and $z$ as constant values:

1. **Differentiate Term 1 ($x^3y$):** Since $x^3$ is a constant multiplier, $\frac{\partial}{\partial y}(x^3y) = x^3 \cdot 1 = x^3$.
2. **Differentiate Term 2 ($y^2$):** Using the standard power rule, $\frac{\partial}{\partial y}(y^2) = 2y$.
3. **Differentiate Term 3 ($z^3$):** Since $z^3$ contains no $y$, its rate of change is $0$.

**Combining the calculations:**


$$\frac{\partial f}{\partial y} = x^3 + 2y + 0 = x^3 + 2y$$

---

## 2. Concept Name: Higher-Order Partial Derivatives (Same Variable)

### Simple Meaning

This means performing partial differentiation with respect to the same variable multiple times in a row. It measures the acceleration or curvature along that specific variable's axis.

### Python Implementation

```python
import sympy as sym

x, y, z = sym.symbols('x,y,z')
func = x**3 * y + y**2 + z**3

# Calculate the second partial derivative with respect to x twice
deriv2_x = sym.diff(func, x, x)
print(deriv2_x)
# Output: 6*x*y

```

### Step-by-Step Mathematical Calculation

Given the function:


$$f(x, y, z) = x^3y + y^2 + z^3$$

1. **Find the first partial derivative with respect to $x$:**

$$\frac{\partial f}{\partial x} = \frac{\partial}{\partial x}(x^3y) + \frac{\partial}{\partial x}(y^2) + \frac{\partial}{\partial x}(z^3)$$


$$\frac{\partial f}{\partial x} = 3x^2y + 0 + 0 = 3x^2y$$


2. **Differentiate the result with respect to $x$ again:**

$$\frac{\partial^2 f}{\partial x^2} = \frac{\partial}{\partial x}(3x^2y)$$


$$\frac{\partial^2 f}{\partial x^2} = 3 \cdot (2x) \cdot y = 6xy$$



---

## 3. Concept Name: Mixed Partial Derivatives

### Simple Meaning

A mixed partial derivative involves differentiating a multivariable function with respect to one variable first, and then differentiating that result with respect to a *different* variable.

### Python Implementation

```python
import sympy as sym

x, y, z = sym.symbols('x,y,z')
func = x**3 * y + y**2 + z**3

# Differentiate with respect to x first, then with respect to y
deriv2_xy = sym.diff(func, x, y)
print(deriv2_xy)
# Output: 3*x**2

```

### Step-by-Step Mathematical Calculation

Given the function:


$$f(x, y, z) = x^3y + y^2 + z^3$$

1. **First, calculate $\frac{\partial f}{\partial x}$ (treating $y$ and $z$ as constants):**

$$\frac{\partial f}{\partial x} = 3x^2y$$


2. **Next, differentiate $3x^2y$ with respect to $y$ (treating $x$ as a constant):**

$$\frac{\partial^2 f}{\partial y \partial x} = \frac{\partial}{\partial y}(3x^2y)$$


$$\frac{\partial^2 f}{\partial y \partial x} = 3x^2 \cdot (1) = 3x^2$$



---

## 4. Concept Name: Symbolic Integration (Indefinite Integral)

### Simple Meaning

Integration is the reverse process of differentiation. An **indefinite integral** finds the original function (antiderivative) whose derivative matches the given expression.

### Python Implementation

```python
# Syntax Overview:
# Indefinite: sym.integrate(func, var)
# Definite:   sym.integrate(func, (var, lower_limit, upper_limit))

import sympy as sym

x = sym.symbols('x')

# Find the indefinite integral of sin(x)
integ = sym.integrate(sym.sin(x), x)
print(integ)
# Output: -cos(x)

```

### Step-by-Step Mathematical Calculation

We are looking for a function whose derivative is $\sin(x)$.
Since we know that:


$$\frac{d}{dx}[\cos(x)] = -\sin(x)$$

Multiplying by $-1$ gives the exact match:


$$\frac{d}{dx}[-\cos(x)] = \sin(x)$$

Therefore, the indefinite integral is:


$$\int \sin(x) \, dx = -\cos(x) + C$$


*(Note: SymPy leaves out the arbitrary integration constant $+ C$ by default).*

---

## 5. Extra Practice Problems

### Problem 1: Mixed Partial Derivative

**Problem:** Find $\frac{\partial^2 f}{\partial z^2}$ for the function $f(x,y,z) = x^3y + y^2 + z^3$.

**Python Verification:**

```python
print(sym.diff(x**3*y + y**2 + z**3, z, z))
# Output: 6*z

```

**Calculation:**

* First derivative: $\frac{\partial f}{\partial z} = 3z^2$
* Second derivative: $\frac{\partial^2 f}{\partial z^2} = \frac{d}{dz}(3z^2) = 6z$

### Problem 2: Definite Integration

**Problem:** Evaluate the definite integral of $f(x) = \sin(x)$ from $0$ to $\pi$.

**Python Verification:**

```python
print(sym.integrate(sym.sin(x), (x, 0, sym.pi)))
# Output: 2

```

**Calculation:**


$$\int_{0}^{\pi} \sin(x) \, dx = \left[ -\cos(x) \right]_{0}^{\pi}$$

$$= (-\cos(\pi)) - (-\cos(0))$$

$$= (-(-1)) - (-1) = 1 + 1 = 2$$

---

## 6. Conceptual Visualization Graph

Below is a text graph showing the relationship between $\sin(x)$ and its integral $-\cos(x)$. The area under the curve of $\sin(x)$ from $0$ to $\pi$ equals the value changes computed during integration.

```text
 Value 
   ^
 1 |     *** [sin(x) Curve]
   |   *     *
 0 +-*-------*-------*-----> x
   |0        pi      2*pi
-1 | *               *  [ -cos(x) Curve]
   |   *           *
   v     *********

```

```

```


.


# Symbolic Calculus with Python (SymPy): Definite Integrals & Limits

This guide covers advanced integration techniques (definite, improper, and double integrals) and evaluating mathematical limits using **SymPy**.

---

## 1. Definite Integrals

### Concept Name: Single Variable Definite Integration
A **Definite Integral** calculates the total accumulated value (like the exact net area) of a function between two specific boundary points (a lower limit and an upper limit).

### Python Implementation
```python
import sympy as sym

# Set up the symbolic variable
x = sym.symbols('x')

# Syntax: sym.integrate(function, (variable, lower_limit, upper_limit))
integ = sym.integrate(sym.sin(x), (x, 0, 1))
print(integ)
# Output: 1 - cos(1)

```

### Step-by-Step Explanation & Calculation

1. **`sym.integrate(sym.sin(x), (x, 0, 1))`**: Tells SymPy to integrate $\sin(x)$ over the specific interval from $x = 0$ to $x = 1$.
2. **Find the Antiderivative**: The indefinite integral of $\sin(x)$ is $-\cos(x)$.
3. **Apply the Fundamental Theorem of Calculus**: Substitute the upper boundary, then subtract the substitution of the lower boundary:

$$\int_{0}^{1} \sin(x) \, dx = \left[ -\cos(x) \right]_{0}^{1}$$

$$\text{Calculation: } (-\cos(1)) - (-\cos(0))$$

$$\text{Since } \cos(0) = 1: \implies -\cos(1) + 1 = 1 - \cos(1)$$

---

## 2. Improper Integrals & Limits to Infinity

### Concept Name: Integrals with Infinite Boundaries

An improper integral has one or both of its limits extending to infinity ($\infty$). SymPy uses `sym.oo` to represent infinity.

### Python Implementation

```python
import sympy as sym

x = sym.symbols('x')

# Integrating e^(-x) from 0 to positive infinity (sym.oo)
integ1 = sym.integrate(sym.exp(-x), (x, 0, sym.oo))
print(integ1)
# Output: 1

# Integrating e^(-x) from 0 to pi
integ2 = sym.integrate(sym.exp(-x), (x, 0, sym.pi))
print(integ2)
# Output: 1 - exp(-pi)

```

### Step-by-Step Explanation & Calculation

For the infinite boundary problem:

1. **Find the Antiderivative**: $\int e^{-x} \, dx = -e^{-x}$.
2. **Evaluate at boundaries**: Take the limit as $x \to \infty$ for the upper bound:

$$\int_{0}^{\infty} e^{-x} \, dx = \lim_{t \to \infty} \left[ -e^{-x} \right]_{0}^{t}$$

$$\text{Calculation: } \left( \lim_{t \to \infty} -e^{-t} \right) - \left( -e^{-0} \right)$$

$$\text{Since } \lim_{t \to \infty} e^{-t} = 0 \text{ and } e^0 = 1: \implies (0) - (-1) = 1$$

---

## 3. Double Integrals

### Concept Name: Multivariable Volume Integration

A **Double Integral** integrates an expression over two different variables sequentially, computing the geometric volume under a 3D surface surface.

### Python Implementation

```python
# Concept Name: Double Integral over Infinite Space
import sympy as sym

x, y = sym.symbols('x y')

# Syntax: sym.integrate(function, (var1, lower1, upper1), (var2, lower2, upper2))
dinteg = sym.integrate(sym.exp(-x**2 - y**2), (x, -sym.oo, sym.oo), (y, -sym.oo, sym.oo))
print(dinteg)
# Output: pi

```

### Step-by-Step Explanation & Calculation

The expression can be broken down into product components because $e^{-x^2-y^2} = e^{-x^2} \cdot e^{-y^2}$:

$$\int_{-\infty}^{\infty} \int_{-\infty}^{\infty} e^{-x^2 - y^2} \, dx \, dy = \left( \int_{-\infty}^{\infty} e^{-x^2} \, dx \right) \cdot \left( \int_{-\infty}^{\infty} e^{-y^2} \, dy \right)$$

Knowing the standard Gaussian integral value $\int_{-\infty}^{\infty} e^{-t^2} \, dt = \sqrt{\pi}$:


$$\text{Calculation: } \sqrt{\pi} \cdot \sqrt{\pi} = \pi$$

---

## 4. Evaluating Limits

### Concept Name: Function Tendency at a Point

A **Limit** checks what value a function approaches as its input variable gets closer and closer to a targeted specific number or infinity.

### Python Implementation

```python
import sympy as sym

x = sym.symbols('x')

# Syntax: sym.limit(function, variable, target_point)
limit1 = sym.limit(sym.exp(-x), x, 0)
print(limit1)
# Output: 1

# Evaluating a limit approaching infinity
limit2 = sym.limit(sym.exp(-x)/x, x, sym.oo)
print(limit2)
# Output: 0

```

### Step-by-Step Explanation & Calculation

* **Case 1: $x \to 0$**
Direct substitution gives:

$$\lim_{x \to 0} e^{-x} = e^{-0} = 1$$


* **Case 2: $x \to \infty$**
Both components change as $x$ gets larger:

$$\lim_{x \to \infty} \frac{e^{-x}}{x} = \frac{0}{\infty} = 0$$



---

## 5. Extra Practice Problems

### Problem 1: Definite Polynomial Integration

**Problem:** Find the area under the curve $f(x) = x^3$ from $x=1$ to $x=2$.

```python
# Code snippet to verify
print(sym.integrate(x**3, (x, 1, 2))) 
# Output: 15/4

```

**Calculation Steps:**


$$\int_{1}^{2} x^3 \, dx = \left[ \frac{x^4}{4} \right]_{1}^{2} = \frac{2^4}{4} - \frac{1^4}{4} = \frac{16}{4} - \frac{1}{4} = \frac{15}{4}$$

### Problem 2: Fundamental Trignometric Limit

**Problem:** Find $\lim_{x \to 0} \frac{\sin(x)}{x}$.

```python
# Code snippet to verify
print(sym.limit(sym.sin(x)/x, x, 0)) 
# Output: 1

```

**Calculation Steps:**
Substituting $0$ results in the indeterminate form $\frac{0}{0}$. Applying L'Hôpital's Rule (differentiating numerator and denominator):


$$\lim_{x \to 0} \frac{\frac{d}{dx}[\sin(x)]}{\frac{d}{dx}[x]} = \lim_{x \to 0} \frac{\cos(x)}{1} = \frac{1}{1} = 1$$

---

## 6. Mathematical Visualizations

### Graph A: Definite Integral Area ($\sin(x)$ from $0$ to $1$)

The area under the curve filled with `##` represents the numeric region calculated by `sym.integrate(sym.sin(x), (x, 0, 1))`.

```text
 y Axis
   ^
 1 |         ******
   |       **######**
   |     *#########  *   <-- sin(x) curve
 0 +----*----------|--*----> x Axis
        0          1  pi

```

### Graph B: Limit Behaviour ($e^{-x}$ as $x \to \infty$)

As the plot advances to the right along the $x$-axis, the function height levels off to asymptotically approach $0$.

```text
 y Axis
   ^
 1 |*
   | \
   |  \
   |   *__
 0 +------****-------======> x Axis (Approaches 0 as x goes to Infinity)
   0

```

```

```


# Taylor and Maclaurin Series Expansions using Python (SymPy)

This note focuses on generating series expansions of functions using the **SymPy** library. Series expansions are used to approximate complex functions as infinite sums of simpler polynomial terms.

---

## 1. Concept Name: Maclaurin Series Expansion

### Simple Meaning
A **Maclaurin Series** is a specific type of Taylor series that expands a function around the central point $x = 0$. It creates a polynomial approximation that is highly accurate near zero.

### Python Implementation
```python
import sympy as sym

# Set up the symbolic variable
x = sym.symbols('x')

# Syntax: sym.series(function, variable)
# By default, SymPy expands around x=0 up to the 6th order term.
exp = sym.series(sym.cos(x), x)
print(exp)
# Output: 1 - x**2/2 + x**4/24 + O(x**6)

```

### Step-by-Step Explanation & Calculation

The general formula for a Maclaurin series of a function $f(x)$ is:


$$f(x) = f(0) + f'(0)x + \frac{f''(0)}{2!}x^2 + \frac{f'''(0)}{3!}x^3 + \dots$$

Let's calculate it manually for $f(x) = \cos(x)$:

1. **$n=0$**: $f(x) = \cos(x) \implies f(0) = \cos(0) = 1$
2. **$n=1$**: $f'(x) = -\sin(x) \implies f'(0) = -\sin(0) = 0$
3. **$n=2$**: $f''(x) = -\cos(x) \implies f''(0) = -\cos(0) = -1$
4. **$n=3$**: $f'''(x) = \sin(x) \implies f'''(0) = \sin(0) = 0$
5. **$n=4$**: $f^{(4)}(x) = \cos(x) \implies f^{(4)}(0) = \cos(0) = 1$

**Plugging these into the formula:**


$$\cos(x) = 1 + (0)x + \frac{-1}{2!}x^2 + \frac{0}{3!}x^3 + \frac{1}{4!}x^4 + \dots$$

$$\cos(x) = 1 - \frac{x^2}{2} + \frac{x^4}{24} + \dots$$

The `O(x**6)` in the output represents the "Big O" error term, meaning all following omitted terms contain powers of $x^6$ or higher.

---

## 2. Concept Name: Taylor Series Expansion

### Simple Meaning

A **Taylor Series** allows you to expand a function around *any* specific point (let's call it $x_0$), not just $x=0$. It provides a polynomial approximation centered around that chosen point. You can also dictate how many terms (the order $n$) the expansion should generate.

### Python Implementation

```python
import sympy as sym

x = sym.symbols('x')

# Syntax: sym.series(function, variable, point_of_expansion (x0), order (n))
# Expanding cos^2(x) around x=1, up to the 4th order.
exp1 = sym.series(sym.cos(x)**2, x, 1, 4)
print(exp1)

# Output snippet: cos(1)**2 - 2*(x - 1)*sin(1)*cos(1) + (-1 + sin(1)**2/cos(1)**2)*(x - 1)**2*cos(1)**2 ... + O((x - 1)**4)

```

### Step-by-Step Explanation & Calculation

The general formula for a Taylor series centered at $x=a$ is:


$$f(x) = f(a) + f'(a)(x-a) + \frac{f''(a)}{2!}(x-a)^2 + \frac{f'''(a)}{3!}(x-a)^3 + \dots$$

Let's look at the first few terms for $f(x) = \cos^2(x)$ around $a=1$:

1. **Zero-th Order Term ($n=0$):**

$$f(1) = \cos^2(1)$$


2. **First Order Term ($n=1$):**

$$f'(x) = 2\cos(x)(-\sin(x)) = -2\sin(x)\cos(x)$$


$$f'(1) = -2\sin(1)\cos(1)$$



The term is: $-2\sin(1)\cos(1) \cdot (x-1)$
3. **Second Order Term ($n=2$):**
Requires differentiating $-2\sin(x)\cos(x)$ (which equals $-\sin(2x)$) again:

$$f''(x) = -2\cos(2x)$$


$$f''(1) = -2\cos(2)$$



The term is: $\frac{-2\cos(2)}{2!} (x-1)^2 = -\cos(2)(x-1)^2$
*(Note: The SymPy output uses an expanded trigonometric identity form for this term).*

---

## 3. Extra Practice Problems

### Problem 1: Maclaurin Series of Exponential Function

**Problem:** Find the Maclaurin series expansion of $e^x$ up to the $x^3$ term.

```python
# Code snippet to verify:
print(sym.series(sym.exp(x), x, 0, 4))
# Output: 1 + x + x**2/2 + x**3/6 + O(x**4)

```

**Calculation:**
Because $\frac{d}{dx}[e^x] = e^x$, all derivatives evaluated at $x=0$ are $e^0 = 1$.


$$e^x = 1 + 1\cdot x + \frac{1}{2!}x^2 + \frac{1}{3!}x^3 = 1 + x + \frac{x^2}{2} + \frac{x^3}{6}$$

### Problem 2: Taylor Series of Natural Logarithm

**Problem:** Expand $\ln(x)$ around the point $x=1$, up to order 3.

```python
# Code snippet to verify:
print(sym.series(sym.log(x), x, 1, 3))
# Output: (x - 1) - (x - 1)**2/2 + O((x - 1)**3)

```

**Calculation:**

1. $f(x) = \ln(x) \implies f(1) = 0$
2. $f'(x) = x^{-1} \implies f'(1) = 1$
3. $f''(x) = -x^{-2} \implies f''(1) = -1$

**Result:**


$$0 + 1\cdot(x-1) + \frac{-1}{2!}(x-1)^2 = (x-1) - \frac{(x-1)^2}{2}$$

---

## 4. Visualizing Series Approximations

Below is a conceptual graph illustrating how adding terms to a Taylor series improves its accuracy. The target function is $\cos(x)$.

```
 y Axis
   ^
 1 |----*-----------*----  <-- T0: First term approx (y = 1)
   |     \         /       <-- T2: Two term approx (y = 1 - x^2/2) 
   |      *-------*        
   |      |       |        
 0 +------|-------|-----> x Axis
         -pi/2   pi/2
-1|      /         \
  |     *   Actual  *      <-- The actual cos(x) curve continues downward
  |         cos(x) 

```

* **T0:** The simplest approximation $y=1$ is only accurate exactly at $x=0$.
* **T2:** The parabola $y = 1 - \frac{x^2}{2}$ fits the curve nicely near $x=0$ but fails as you move further away towards $\pm \frac{\pi}{2}$.
* Adding more terms (like $+ \frac{x^4}{24}$) bends the approximation to "hug" the true curve for a wider range.

