# Understanding the Limit of a Function

---

## 1. Core Concept: Limit at a Point

A **limit** describes the behavior of a function $f(x)$ as the input $x$ gets infinitely close to a specific value $a$. Instead of asking what the function *is* exactly at $x = a$, a limit asks what value the function is *approaching*.

### Left-Hand and Right-Hand Limits
For a general limit to exist at a point, the function must approach the exact same value from both sides of that point:
1. **Left-Hand Limit (LHL):** The value $f(x)$ approaches as $x$ nears $a$ from values smaller than $a$ (from the left). Denoted as:
   $$\lim_{x \to a^-} f(x)$$
2. **Right-Hand Limit (RHL):** The value $f(x)$ approaches as $x$ nears $a$ from values larger than $a$ (from the right). Denoted as:
   $$\lim_{x \to a^+} f(x)$$

> **The Fundamental Rule of Existence:**
> The overall limit exists and equals $L$ if and only if both the one-sided limits exist and are equal to $L$:
> $$\lim_{x \to a} f(x) = L \iff \lim_{x \to a^-} f(x) = \lim_{x \to a^+} f(x) = L$$


---

## 2. Graphical Examples of Non-Existence

Limits fail to exist at points where there is a break or a "jump" in the graph, causing the LHL and RHL to point to different values.

### Example A: The Signum-like Function
Consider the piece-wise function:
$$f(x) = \begin{cases} \frac{\vert{}x\vert{}}{x}, & x \neq 0 \\ 0, & x = 0 \end{cases} \implies f(x) = \begin{cases} 1, & x > 0 \\ -1, & x < 0 \\ 0, & x = 0 \end{cases}$$

#### Graph Analysis
```text
                 Y
                 |   o========= (y = 1)
                 |
-----------------+----------------- X
                 |
    =========o   |   (y = -1)
                 |

```

* **Evaluate LHL at $0$:** As $x \to 0^-$, $f(x) = -1 \implies \lim_{x \to 0^-} f(x) = -1$
* **Evaluate RHL at $0$:** As $x \to 0^+$, $f(x) = 1 \implies \lim_{x \to 0^+} f(x) = 1$
* **Conclusion:** Since $\text{LHL} \neq \text{RHL}$ ($-1 \neq 1$), **$\lim_{x \to 0} f(x)$ does not exist**.

---

### Example B: Greatest Integer Function at an Integer Step

Let $f(x) = [x]$ (the floor function). Let's evaluate the limit as $x \to 1$.

#### Graph Analysis

```text
                 Y
                 |
                 |       *-----o  (y = 1)
                 |
        *-----o  |                (y = 0)
                 |       x=1
-----------+-----+-------+--------- X
                 |       |

```

* **Left-Hand Limit ($x \to 1^-$):** Let $x = 1 - h$ where $h \to 0$ is a tiny positive number (e.g., $x = 0.999$).

$$\lim_{h \to 0} [1 - h] = 0$$


* **Right-Hand Limit ($x \to 1^+$):** Let $x = 1 + h$ where $h \to 0$ (e.g., $x = 1.001$).

$$\lim_{h \to 0} [1 + h] = 1$$


* **Conclusion:** Since $\text{LHL} = 0$ and $\text{RHL} = 1$, the values don't match. **$\lim_{x \to 1} [x]$ does not exist**.

---

## 3. Step-by-Step Problem Solving

When directly substituting $x = a$ results in an indeterminate form like $\frac{0}{0}$, we use algebraic manipulation (factoring or trigonometric identities) to simplify the expression before evaluating.

### Problem 1: Factoring Algebraic Polynomials

Evaluate:


$$\lim_{x \to 2} \frac{x^2 - 4}{x^3 - 8}$$

#### Step-by-Step Calculation:

1. **Test Direct Substitution:**
Substituting $x = 2$ gives $\frac{2^2 - 4}{2^3 - 8} = \frac{0}{0}$ (Indeterminate Form). We must factor.
2. **Factor the Numerator (Difference of Squares):**

$$x^2 - 4 = (x - 2)(x + 2)$$


3. **Factor the Denominator (Difference of Cubes):**

$$x^3 - 8 = x^3 - 2^3 = (x - 2)(x^2 + 2x + 4)$$


4. **Rewrite the Limit Equation and Cancel the Common Factor $(x - 2)$:**

$$\lim_{x \to 2} \frac{(x - 2)(x + 2)}{(x - 2)(x^2 + 2x + 4)} = \lim_{x \to 2} \frac{x + 2}{x^2 + 2x + 4}$$


5. **Substitute $x = 2$ safely into the simplified expression:**

$$\frac{2 + 2}{2^2 + 2(2) + 4} = \frac{4}{4 + 4 + 4} = \frac{4}{12} = \frac{1}{3}$$



---

### Problem 2: Using Trigonometric Identities

Evaluate:


$$\lim_{x \to 0} \frac{1 - \cos 2x}{1 - \cos x}$$

#### Step-by-Step Calculation:

1. **Identify Trigonometric Identities:**
Recall the half-angle formulas:
* $1 - \cos 2x = 2\sin^2 x$
* $1 - \cos x = 2\sin^2\left(\frac{x}{2}\right)$


2. **Substitute these identities into the limit:**

$$\lim_{x \to 0} \frac{2\sin^2 x}{2\sin^2\left(\frac{x}{2}\right)} = \lim_{x \to 0} \frac{\sin^2 x}{\sin^2\left(\frac{x}{2}\right)}$$


3. **Apply the Standard Trigonometric Limit Rule:**
We know that $\lim_{\theta \to 0} \frac{\sin \theta}{\theta} = 1$. Let's manipulate our expression to match this form:

$$\lim_{x \to 0} \frac{\left(\frac{\sin x}{x}\right)^2 \cdot x^2}{\left(\frac{\sin(x/2)}{x/2}\right)^2 \cdot \left(\frac{x}{2}\right)^2}$$


4. **Simplify the algebraic constants:**

$$\lim_{x \to 0} \frac{\left(\frac{\sin x}{x}\right)^2 \cdot x^2}{\left(\frac{\sin(x/2)}{x/2}\right)^2 \cdot \frac{x^2}{4}} = \lim_{x \to 0} \frac{\left(\frac{\sin x}{x}\right)^2}{\left(\frac{\sin(x/2)}{x/2}\right)^2 \cdot \frac{1}{4}}$$


5. **Evaluate the limits:**
Since both $\frac{\sin x}{x} \to 1$ and $\frac{\sin(x/2)}{x/2} \to 1$:

$$\frac{1^2}{1^2 \cdot \frac{1}{4}} = \frac{1}{\frac{1}{4}} = 4$$



---

### Problem 3: Factoring Quadratic Expressions

Evaluate:


$$\lim_{x \to 1} \frac{x^2 - 3x + 2}{x^2 - 6x + 5}$$

#### Step-by-Step Calculation:

1. **Test Direct Substitution:**
Substituting $x = 1$ gives $\frac{1 - 3 + 2}{1 - 6 + 5} = \frac{0}{0}$. We need to factor.
2. **Factor the Numerator:**
Find numbers that multiply to $2$ and add to $-3$: $(-2)$ and $(-1)$.

$$x^2 - 3x + 2 = (x - 1)(x - 2)$$


3. **Factor the Denominator:**
Find numbers that multiply to $5$ and add to $-6$: $(-5)$ and $(-1)$.

$$x^2 - 6x + 5 = (x - 1)(x - 5)$$


4. **Cancel out the zero-causing factor $(x - 1)$:**

$$\lim_{x \to 1} \frac{(x - 1)(x - 2)}{(x - 1)(x - 5)} = \lim_{x \to 1} \frac{x - 2}{x - 5}$$


5. **Substitute $x = 1$:**

$$\frac{1 - 2}{1 - 5} = \frac{-1}{-4} = \frac{1}{4}$$



```

```


# Continuity and Differentiability of Functions

---

## 1. Continuity of a Function at a Point

### Core Concept
Intuitively, a function is **continuous** at a point if you can draw its graph through that point without lifting your pencil from the paper. There are no holes, jumps, or vertical asymptotes at that location.

> **Mathematical Definition:**
> A function $f : X \rightarrow Y$ is said to be continuous at a point $x = a$ if and only if:
> $$\lim_{x \to a} f(x) = f(a)$$

This single equation implies **three strict conditions** must be met simultaneously:
1. $f(a)$ must be defined (the point actually exists on the graph).
2. The overall limit $\lim_{x \to a} f(x)$ must exist, meaning the Left-Hand Limit (LHL) matches the Right-Hand Limit (RHL):
   $$\lim_{x \to a^-} f(x) = \lim_{x \to a^+} f(x)$$
3. The value the function approaches must exactly equal the actual value at the point: $\text{LHL} = \text{RHL} = f(a)$.


### Graphical Comparison
#### Continuous at $x = a$
The path is unbroken. The limit target matches the solid dot.
```text
                 Y
                 |       /
                 |      / 
                 |     * (a, f(a))
                 |    /
-----------------+---/------------- X
                 |  a

```

#### Discontinuous at $x = a$ (Removable Discontinuity)

The path approaches a value, but the actual point is defined somewhere else.

```text
                 Y        • (a, f(a))
                 |       /
                 |      / 
                 |     o <-- Hole at the limit path
                 |    /
-----------------+---/------------- X
                 |  a

```

---

## 2. Properties of Continuous Functions

If two functions $f$ and $g$ are both confirmed to be continuous at a specific point $x = a$, and $\alpha$ is a constant scalar value, the following structural combinations are also guaranteed to remain continuous at $x = a$:

1. **Sum and Difference:** $f \pm g$
2. **Scalar Multiplication:** $\alpha f$
3. **Product:** $fg$
4. **Quotient:** $\frac{f}{g}$ (provided that $g(a) \neq 0$)

---

## 3. Worked Continuity Problem

### Problem Statement

Show that the piecewise function $f : [0, 2] \rightarrow \mathbb{R}$ defined below is continuous at $x = 1$:


$$f(x) = \begin{cases} 1 + x, & 0 \leq x < 1 \\ 2, & x = 1 \\ 2x, & 1 < x \leq 2 \end{cases}$$

---

### Step-by-Step Verification

#### Step 1: Find the actual value at the point $f(1)$

Look at the rule given specifically for $x = 1$:


$$f(1) = 2$$

#### Step 2: Calculate the Left-Hand Limit (LHL) as $x \to 1^-$

For values slightly less than $1$, use the first piece of the function $f(x) = 1 + x$:


$$\text{LHL} = \lim_{x \to 1^-} (1 + x)$$

Let $x = 1 - h$, where $h$ is a tiny positive value approaching $0$:


$$\text{LHL} = \lim_{h \to 0} (1 + (1 - h)) = \lim_{h \to 0} (2 - h) = 2 - 0 = 2$$

#### Step 3: Calculate the Right-Hand Limit (RHL) as $x \to 1^+$

For values slightly greater than $1$, use the third piece of the function $f(x) = 2x$:


$$\text{RHL} = \lim_{x \to 1^+} (2x)$$

Let $x = 1 + h$, where $h$ is a tiny positive value approaching $0$:


$$\text{RHL} = \lim_{h \to 0} 2(1 + h) = \lim_{h \to 0} (2 + 2h) = 2 + 0 = 2$$

#### Step 4: Compare LHL, RHL, and $f(1)$

$$\text{LHL} = 2, \quad \text{RHL} = 2, \quad f(1) = 2$$

$$\text{LHL} = \text{RHL} = f(1)$$

**Conclusion:** Because the limits from both sides match the defined point exactly, the function is **continuous at $x = 1$**.

---

## 4. Differentiability of a Function at a Point

### Core Concept

A function is **differentiable** at a point if it has a well-defined derivative (slope) at that location. Geometrically, this means the graph is completely smooth at that point, allowing you to draw a **single, unique tangent line**.

If a graph contains sharp corners, spikes, cusps, or vertical drops, it is not differentiable at those points.

> **Mathematical Definition:**
> Let $f$ be a real-valued function defined on an open interval $(a, b)$. Then, $f$ is differentiable at a point $c \in (a, b)$ if and only if the following limit exists:
> 
> $$f'(c) = \lim_{x \to c} \frac{f(x) - f(c)}{x - c}$$
> 
> 

---

### Left-Hand and Right-Hand Derivatives

Just like limits, the slopes must match when approaching from the left and right sides.

1. **Left-Hand Derivative (LHD):** The slope approaching from the left.

$$\text{LHD} = \lim_{x \to c^-} \frac{f(x) - f(c)}{x - c} = \lim_{h \to 0} \frac{f(c - h) - f(c)}{-h}$$


2. **Right-Hand Derivative (RHD):** The slope approaching from the right.

$$\text{RHD} = \lim_{x \to c^+} \frac{f(x) - f(c)}{x - c} = \lim_{h \to 0} \frac{f(c + h) - f(c)}{h}$$



$$\text{Function is Differentiable at } c \iff \text{LHD} = \text{RHD}$$

---

## 5. Worked Differentiability Problem

### Problem Statement

Analyze whether the classic modulus function $f(x) = \vert{}x\vert{}$ is differentiable at the origin ($x = 0$).

#### Visualizing the Corner (Graph)

```text
             Y
      \      |      /
       \     |     /
        \    |    /  Graph has a sharp corner at (0,0)!
_________\___|___/_________ X
             |

```

---

### Step-by-Step Verification

#### Step 1: Write down the component forms

$$f(x) = \begin{cases} x, & x \geq 0 \\ -x, & x < 0 \end{cases}$$


Here, the target point is $c = 0$, and $f(0) = |0| = 0$.

#### Step 2: Calculate the Left-Hand Derivative (LHD) at $0$

Using the LHD formula:


$$\text{LHD} = \lim_{h \to 0} \frac{f(0 - h) - f(0)}{-h}$$

$$\text{LHD} = \lim_{h \to 0} \frac{|-h| - 0}{-h}$$

Since $h > 0$, the value inside the absolute bounds is negative, meaning $|-h| = h$:


$$\text{LHD} = \lim_{h \to 0} \frac{h}{-h} = -1$$

#### Step 3: Calculate the Right-Hand Derivative (RHD) at $0$

Using the RHD formula:


$$\text{RHD} = \lim_{h \to 0} \frac{f(0 + h) - f(0)}{h}$$

$$\text{RHD} = \lim_{h \to 0} \frac{|h| - 0}{h}$$

Since $h > 0$, $|h| = h$:


$$\text{RHD} = \lim_{h \to 0} \frac{h}{h} = 1$$

#### Step 4: Compare LHD and RHD

$$\text{LHD} = -1 \quad \neq \quad \text{RHD} = 1$$

**Conclusion:** Because the slope abruptly changes from $-1$ to $+1$ at the origin, the limit does not exist. The function $f(x) = |x|$ is **not differentiable at $x = 0$**.

```

```


# Advanced Differentiability and Rules of Differentiation

---

## 1. Differentiability of Piecewise Functions

### Core Concept
For a piecewise function to be **differentiable** at a boundary value $x = c$ where the function changes its definition, the slope approaching from the left must perfectly match the slope approaching from the right. 

$$\text{Function is Differentiable at } c \iff \text{Left-Hand Derivative (LHD)} = \text{Right-Hand Derivative (RHD)}$$

* **LHD Formula:** $$\text{LHD} = \lim_{h \to 0} \frac{f(c - h) - f(c)}{-h}$$
* **RHD Formula:** $$\text{RHD} = \lim_{h \to 0} \frac{f(c + h) - f(c)}{h}$$

---

## 2. Worked Differentiability Problem

### Problem Statement
Determine if the piecewise function $f(x)$ defined below is differentiable at $x = 1$. If it is, find $f'(1)$.
$$f(x) = \begin{cases} 2x, & x \leq 1 \\ x^2, & x > 1 \end{cases}$$

### Step-by-Step Calculation

#### Step 1: Find the value of the function at the boundary point
Look at the component that includes equality ($x \leq 1$):
$$f(1) = 2(1) = 2$$

#### Step 2: Compute the Left-Hand Derivative (LHD)
For values strictly less than $1$ ($x = 1 - h$), the function definition is $f(x) = 2x$.
$$\text{LHD} = \lim_{h \to 0} \frac{f(1 - h) - f(1)}{-h}$$

Substitute the function rule into the limit:
$$\text{LHD} = \lim_{h \to 0} \frac{2(1 - h) - 2}{-h}$$
$$\text{LHD} = \lim_{h \to 0} \frac{2 - 2h - 2}{-h}$$
$$\text{LHD} = \lim_{h \to 0} \frac{-2h}{-h} = 2$$

#### Step 3: Compute the Right-Hand Derivative (RHD)
For values strictly greater than $1$ ($x = 1 + h$), the function definition is $f(x) = x^2$.
$$\text{RHD} = \lim_{h \to 0} \frac{f(1 + h) - f(1)}{h}$$

Substitute the function rule into the limit:
$$\text{RHD} = \lim_{h \to 0} \frac{(1 + h)^2 - 2}{h}$$

Expand the binomial term $(1 + h)^2 = 1 + 2h + h^2$:
$$\text{RHD} = \lim_{h \to 0} \frac{1 + 2h + h^2 - 2}{h}$$


> **Wait, let's double-check our continuity status first!** > If we compute the RHL of the function value itself: $\lim_{x \to 1^+} x^2 = 1^2 = 1$.  
> But $f(1) = 2$. Because the Left-Hand side ends at $2$ and the Right-Hand side starts at $1$, the function has a sudden **jump discontinuity** at $x=1$! 
>
> Let's look at how the calculation handles this discontinuity:
> $$\text{RHD} = \lim_{h \to 0} \frac{h^2 + 2h - 1}{h} = \lim_{h \to 0} \left(h + 2 - \frac{1}{h}\right) = -\infty$$
>
> Since the limit does not yield a finite matching real number, **$\text{LHD} \neq \text{RHD}$**. 

*Correction Note:* In order for a function to be differentiable at a point, it **must** be continuous there first. Since $\lim_{x \to 1^-} f(x) = 2$ but $\lim_{x \to 1^+} f(x) = 1$, the function breaks at $x=1$ and is **not differentiable**.

---

## 3. Basic Rules of Differentiation

When a function is continuous and smooth, we don't need to use the limit definitions every time. Instead, we rely on standard derivative properties. Let $f(x)$ and $g(x)$ be differentiable functions, and let $\alpha \in \mathbb{R}$ be a constant.

### 1. Scalar Product Rule
A constant factor can be factored out of a derivative.
$$\frac{d}{dx}(\alpha f(x)) = \alpha \frac{d}{dx}f(x)$$

### 2. Sum and Difference Rule
The derivative of a sum or difference is the sum or difference of their individual derivatives.
$$\frac{d}{dx}(f(x) \pm g(x)) = \frac{d}{dx}f(x) \pm \frac{d}{dx}g(x)$$

### 3. Product Rule
To find the derivative of two functions multiplied together, use the template: *first times derivative of the second + second times derivative of the first*.
$$\frac{d}{dx}(f(x)g(x)) = f(x)g'(x) + g(x)f'(x)$$

### 4. Quotient Rule
To find the derivative of a fraction of two functions, use the template: *(bottom times derivative of top - top times derivative of bottom) divided by bottom squared*.
$$\frac{d}{dx}\left(\frac{f(x)}{g(x)}\right) = \frac{f'(x)g(x) - f(x)g'(x)}{(g(x))^2}, \quad \text{where } g(x) \neq 0$$

---

## 4. Practice Problems Using Differentiation Rules

### Problem A: Applying the Product Rule
**Question:** Find the derivative of $y = x^2 \cdot \sin(x)$.

#### Step-by-Step Calculation:
1. Identify the components: $f(x) = x^2$ and $g(x) = \sin(x)$.
2. Compute their individual derivatives:
   * $f'(x) = 2x$
   * $g'(x) = \cos(x)$
3. Apply the Product Rule formula:
   $$\frac{dy}{dx} = f(x)g'(x) + g(x)f'(x)$$
   $$\frac{dy}{dx} = (x^2)(\cos x) + (\sin x)(2x)$$
4. Simplify the final expression:
   $$\frac{dy}{dx} = x^2\cos x + 2x\sin x$$

---

### Problem B: Applying the Quotient Rule
**Question:** Find the derivative of $y = \frac{x^2}{x + 1}$.

#### Step-by-Step Calculation:
1. Identify the numerator and denominator: $f(x) = x^2$ and $g(x) = x + 1$.
2. Compute their individual derivatives:
   * $f'(x) = 2x$
   * $g'(x) = 1$
3. Apply the Quotient Rule formula:
   $$\frac{dy}{dx} = \frac{f'(x)g(x) - f(x)g'(x)}{(g(x))^2}$$
   $$\frac{dy}{dx} = \frac{(2x)(x + 1) - (x^2)(1)}{(x + 1)^2}$$
4. Expand the numerator:
   $$\frac{dy}{dx} = \frac{2x^2 + 2x - x^2}{(x + 1)^2}$$
5. Combine like terms:
   $$\frac{dy}{dx} = \frac{x^2 + 2x}{(x + 1)^2}$$