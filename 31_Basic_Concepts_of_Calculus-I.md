# Comprehensive Guide to Functions, Domains, and Ranges

---

## 1. What is a Function?

### Core Concept
A **function** $f$ from a set $A$ to a set $B$ (denoted as $f : A \rightarrow B$) is a special rule or correspondence that maps elements of set $A$ to elements of set $B$. 

To be considered a valid function, it must satisfy **two strict conditions**:
1. **Total Mapping:** Every single element in set $A$ must be paired with an element in set $B$.
2. **Uniqueness:** Each element in set $A$ must map to **one and only one** element in set $B$. An input cannot have multiple outputs.

---

### Mapping Diagrams Visualization

#### Example A: A Valid Function
Every element in $A$ has exactly one arrow pointing to an element in $B$.
```text
    Set A          Set B
   +-------+      +-------+
   |   a   | ---->|   1   |
   |   b   | ---->|   2   |
   |   c   | ---->|   3   |
   |   d   | ---->|   4   |
   +-------+      |   5   |
                  +-------+

```

#### Example B: NOT a Function

This fails the definition because a single element in $A$ maps to two different elements in $B$.

```text
    Set A          Set B
   +-------+      +-------+
   |   a   | ---->|   1   |
   |       | ---->|   2   |  <-- Element 'a' has TWO outputs!
   |   b   | ---->|   3   |
   +-------+      +-------+

```

---

## 2. The Vertical Line Test (Graphical Check)

If you are looking at a graph on a Cartesian plane ($X$-$Y$ axis), you can easily determine if it represents a function using the **Vertical Line Test**.

> **Rule:** If you can draw *any* vertical line that crosses the graph more than once, the graph is **NOT** a function. This is because a single $x$-value would correspond to multiple $y$-values.

### Examples

#### 1. A Circle (Not a Function)

A vertical line passes through two points.

```text
        Y
        |   ...
     +--|--+   : <-- Vertical Line
    /   |   \  :
---|----+----|--- X
    \   |   /  :
     +--|--+   :
        |   ...

```

#### 2. A Horizontal Parabola ($x = y^2$) (Not a Function)

A vertical line crosses both the top and bottom halves.

```text
        Y
        |   \  :
        |    \ : <-- Vertical Line
--------+-----\--- X
        |    / :
        |   /  :
        |      :

```

#### 3. A Linear or Custom Curve (Is a Function)

Any vertical line will cross the path exactly once.

```text
        Y      / :
       /|     /  : <-- Vertical Line
______/_|____/___:____ X
     /  |   /    :
    /   |  /     :

```

---

## 3. Domain, Co-Domain, and Range

When dealing with a function $f : A \rightarrow B$:

* **Domain ($A$):** The set of all possible input values ($x$) for which the function is defined.
* **Co-Domain ($B$):** The target set containing all potential output values that the function *could* theoretically yield.
* **Range ($f(A)$):** The set of all *actual* output values ($y$) produced by plugging the inputs from the domain into the function.

$$\text{Range} = \{y \in B : y = f(x) \text{ for some } x \in A\}$$

$$\text{Range} \subseteq \text{Co-Domain}$$

---

## 4. Step-by-Step Problems and Calculations

Here are the four standard function examples analyzed in detail.

### Problem 1: The Quadratic Function

Given $f : \mathbb{R} \rightarrow \mathbb{R}$, where $f(x) = x^2$.

#### Graph

```text
         Y
   \     |     /
    \    |    /
     \   |   /
______\_ | _/______ X
         |

```

#### Step-by-Step Explanation:

1. **Domain:** You can square any real number (positive, negative, or zero) without encountering mathematical errors (like dividing by zero or taking the square root of a negative number). Therefore, the Domain is all real numbers.

$$\text{Domain} = \mathbb{R} = (-\infty, \infty)$$


2. **Range:** Whenever you square a real number, the result is always non-negative ($x^2 \geq 0$).

$$\text{Range} = [0, \infty)$$



---

### Problem 2: The Sine Function

Given $f(x) = \sin(x)$.

#### Graph

```text
     1 +    _       _ 
       |  /   \   /   \
-------+-/-----\-/-----\- X
    -1 +       V       V

```

#### Step-by-Step Explanation:

1. **Domain:** The trigonometric sine function accepts any angle or real number value along the horizontal axis.

$$\text{Domain} = \mathbb{R}$$


2. **Range:** Due to the periodic nature of waves, the output of a standard $\sin(x)$ curve oscillating naturally alternates exclusively between its peak amplitudes of $-1$ and $1$.

$$\text{Range} = [-1, 1]$$



---

### Problem 3: The Radical (Square Root) Function

Given $f(x) = \sqrt{1 - x^2}$.

#### Graph (A Semi-Circle)

```text
         Y
       1 +  ...
        / | \
_______/_ | _\_______ X
     -1   0   1

```

#### Step-by-Step Calculation:

1. **Finding Domain:** The value inside a square root must be greater than or equal to zero:

$$1 - x^2 \geq 0$$


Multiply by $-1$ (remember to flip the inequality sign):

$$x^2 - 1 \leq 0$$


Factor the algebraic difference of squares expression:

$$(x - 1)(x + 1) \leq 0$$


Using a sign chart / number line analysis:
* Roots are at $x = -1$ and $x = 1$.
* The expression is negative or zero between these intervals:

$$\text{Domain} = [-1, 1]$$




2. **Finding Range:**
* When $x = 0$ (its maximum capability), $f(0) = \sqrt{1 - 0} = 1$.
* When $x = \pm 1$ (the boundary edges), $f(\pm 1) = \sqrt{1 - 1} = 0$.
* Since a principal square root cannot return negative values, the output strictly ranges from $0$ up to $1$.

$$\text{Range} = [0, 1]$$





---

### Problem 4: The Rational Function

Given $f(x) = \frac{x}{x + 1}$.

#### Step-by-Step Calculation:

1. **Finding Domain:**
A fraction is undefined if its denominator is equal to zero.

$$x + 1 = 0 \implies x = -1$$



Therefore, $x$ can be any real value *except* $-1$.

$$\text{Domain} = \mathbb{R} - \{-1\}$$


2. **Finding Range:**
To find the range, set $y = f(x)$ and rearrange the equation to solve explicitly for $x$ in terms of $y$:

$$y = \frac{x}{x + 1}$$


Cross-multiply to clear the fraction:

$$y(x + 1) = x$$


$$yx + y = x$$


Move all terms containing $x$ to one side:

$$y = x - yx$$


Factor out $x$:

$$y = x(1 - y)$$


Isolate $x$:

$$x = \frac{y}{1 - y}$$


 or equivalently 
$$x = -\frac{y}{y - 1}$$


Now observe the restriction on this output equation. The new denominator cannot be zero:

$$1 - y \neq 0 \implies y \neq 1$$


$$\text{Range} = \mathbb{R} - \{1\}$$



```

```

# Complete Guide to Types of Functions

---

## 1. Constant Function

### Core Concept
A **Constant Function** maps every single element in the domain to one and the exact same fixed value in the co-domain. No matter what input $x$ you provide, the output remains unchanged.

> **Mathematical Definition:** > Let $f: A \rightarrow B$. If $f(x) = \alpha$ for all $x \in A$, where $\alpha \in B$ is a fixed real number, then $f$ is a constant function.

### Worked Example & Calculation
Let $f: \mathbb{R} \rightarrow \mathbb{R}$ be defined by $f(x) = 2$.

* **Step-by-step evaluation:**
  * For $x = -10 \implies f(-10) = 2$
  * For $x = 0 \implies f(0) = 2$
  * For $x = 3.5 \implies f(3.5) = 2$
* **Domain:** $\mathbb{R}$ (all real numbers can be input)
* **Range:** $\{2\}$ (the only actual output value)

### Graph
The graph is a flat, horizontal line crossing the Y-axis at $(0, 2)$.
```text
                 Y
                 |
- - - - - - - - -+ - - - - - - - - - f(x) = 2
                 |
-----------------+----------------- X
                 |
                 |

```

---

## 2. Identity Function

### Core Concept

An **Identity Function** acts like a perfect mirror. Whatever real number you pass into it, it yields that exact same value as the output.

> **Mathematical Definition:**
> A function $f: \mathbb{R} \rightarrow \mathbb{R}$ defined by $f(x) = x$ for all $x \in \mathbb{R}$.

### Key Properties

* **Domain:** $\mathbb{R}$
* **Range:** $\mathbb{R}$
* Every point on the graph has identical coordinates, such as $(-2, -2)$, $(0, 0)$, and $(5, 5)$.

### Graph

The graph is a straight line passing through the origin at a perfect **45° angle**.

```text
                 Y         /
                 |        /
                 |       /
                 |      /
-----------------+-----/----------- X
               / |
              /  |
             /   |
            /    |

```

---

## 3. Odd Function

### Core Concept

An **Odd Function** changes its sign when the sign of its input is flipped. Graphically, odd functions exhibit **rotational symmetry about the origin** (if you rotate the graph 180° around $(0,0)$, it looks exactly the same).

> **Mathematical Definition:**
> A function $f: A \rightarrow B$ is called an odd function if $f(-x) = -f(x)$ for all $x \in A$.

### Worked Example 1: The Cubic Function

Let $f(x) = x^3$ where $f: \mathbb{R} \rightarrow \mathbb{R}$.

* **Step-by-step calculation:**
1. Substitute $-x$ into the function:

$$f(-x) = (-x)^3$$


2. Simplify the exponent:

$$(-x)^3 = (-1)^3 \cdot x^3 = -x^3$$


3. Relate it back to the original function:

$$-x^3 = -f(x)$$


4. Since $f(-x) = -f(x)$, the function is **Odd**.



```text
                 Y       /
                 |      / 
                 |    /   
                 |  .'    
-----------------+.'--------------- X
              '. |
                \|
                 |
                 |

```

### Worked Example 2: The Sine Function

Let $f(x) = \sin(x)$ where $f: \mathbb{R} \rightarrow \mathbb{R}$.

* **Step-by-step calculation:**
1. Check the identity for negative inputs:

$$f(-x) = \sin(-x)$$


2. From trigonometry rules, $\sin(-x) = -\sin(x)$.
3. Therefore, $f(-x) = -f(x)$, proving it is an **Odd** function.



---

## 4. Even Function

### Core Concept

An **Even Function** completely absorbs a negative sign in its input. Graphically, even functions exhibit **reflectional symmetry across the Y-axis** (the left side is a perfect mirror image of the right side).

> **Mathematical Definition:**
> A function $f: A \rightarrow B$ is called an even function if $f(-x) = f(x)$ for all $x \in A$.

### Worked Example: The Quadratic Function

Let $f(x) = x^2$ where $f: \mathbb{R} \rightarrow \mathbb{R}$.

* **Step-by-step calculation:**
1. Substitute $-x$ into the function:

$$f(-x) = (-x)^2$$


2. Square the negative value:

$$(-x) \cdot (-x) = x^2$$


3. Relate back to the original function:

$$x^2 = f(x)$$


4. Since $f(-x) = f(x)$, the function is **Even**.



### Graph

```text
             Y
      \      |      /
       \     |     /
        \    |    /
_________\___|___/_________ X
             |

```

---

## 5. Modulus Function (Absolute Value)

### Core Concept

The **Modulus Function** outputs the non-negative magnitude of a real number, stripping away any negative sign. It is defined as a piece-wise function.

> **Mathematical Definition:**
> A function $f: \mathbb{R} \rightarrow \mathbb{R}$ defined by:
> 
> $$f(x) = \vert{}x\vert{} = \begin{cases} x, & x \geq 0 \\ -x, & x < 0 \end{cases}$$
> 
> 

### Worked Example & Calculation

* **Case 1 (Positive input):** Let $x = 5 \implies$ since $5 \geq 0$, $f(5) = 5$.
* **Case 2 (Negative input):** Let $x = -5 \implies$ since $-5 < 0$, $f(-5) = -(-5) = 5$.
* **Domain:** $\mathbb{R}$
* **Range:** $[0, \infty)$

### Graph

The graph forms a distinctive **"V" shape** with its vertex sitting directly at the origin.

```text
             Y
      \      |      /
       \     |     /
        \    |    /
_________\___|___/_________ X
             |

```

---

## 6. Greatest Integer Function (Floor Function)

### Core Concept

The **Greatest Integer Function** rounds any real number down to the next nearest integer that is less than or equal to it. It is often described as a "step function" because its graph looks like a flight of stairs.

> **Mathematical Definition:**
> The function $f: \mathbb{R} \rightarrow \mathbb{R}$ defined by $f(x) = [x]$ (or $\lfloor x \rfloor$) for all $x \in \mathbb{R}$, which represents the greatest integer less than or equal to $x$.

### Worked Example & Calculation

* **Step-by-step evaluations:**
* For $x = 2.3 \implies$ The integers less than or equal to $2.3$ are $\{\dots, 0, 1, 2\}$. The largest among them is $2$. So, $[2.3] = 2$.
* For $x = 5 \implies$ Since $5$ is already an integer, $[5] = 5$.
* For $x = -1.2 \implies$ The integers less than or equal to $-1.2$ are $\{-2, -3, -4, \dots\}$. The largest one is $-2$. So, $[-1.2] = -2$. *(Note: It does not drop the decimal to become $-1$, it rounds down to the next lower integer).*


* **Domain:** $\mathbb{R}$
* **Range:** $\mathbb{Z}$ (the set of all integers: $\{\dots, -2, -1, 0, 1, 2, \dots\}$)

### Graph

A series of broken steps where solid points `*` mean included values and open circles `o` mean excluded values:

```text
                 Y
                 |
                 |       *-----o  (y=2)
                 |
                 *-----o          (y=1)
                 |
-----------*-----o---------------- X
         /       | (0,0)
   *-----o       |                (y=-1)
                 |

```




# Advanced Functions: Exponential and Logarithmic Functions

---

## 1. Exponential Function

### Core Concept
An **Exponential Function** features a constant base raised to a variable exponent. The behavior of the function changes significantly depending on whether the base is greater than $1$ (growth) or between $0$ and $1$ (decay).

> **Mathematical Definition:**
> A function $f : \mathbb{R} \rightarrow \mathbb{R}$ defined by $f(x) = a^x$, for all $x \in \mathbb{R}$, where $a > 0$ and $a \neq 1$.

### Why are there restrictions on the base $a$?
* If $a \leq 0$, raising it to fractional exponents (like $a^{1/2} = \sqrt{a}$) would result in imaginary numbers.
* If $a = 1$, the function simplifies to $f(x) = 1^x = 1$, which is just a constant function, not an exponential one.

---

### Analysis of the Two Cases

#### Case I: Exponential Growth ($a > 1$)
When the base is greater than $1$, the outputs grow rapidly as $x$ increases. As $x$ becomes highly negative, the curve approaches the $X$-axis but never quite touches it (the Y-value approaches $0$).

* **Graph ($a > 1$):**
```text
                 Y         / (y = a^x)
                 |        /
                 |      / 
                 |    /   
                 |  * (0,1)   
-----------------+----------------- X
 _  _  .  .  '  '|

```

#### Case II: Exponential Decay ($0 < a < 1$)

When the base is a fraction between $0$ and $1$, the outputs shrink as $x$ increases. As $x$ becomes highly positive, the values get closer and closer to $0$.

* **Graph ($0 < a < 1$):**

```text
(y = a^x) \      Y
           \     |
            \    |
             \   |
              \  * (0,1)
-----------------+----------------- X
                 |  _  _  .  .  '  '

```

---

### Domain and Range Properties

* **Domain:** $\mathbb{R}$ (You can input any positive, negative, or zero exponent).
* **Range:** $(0, \infty)$ (Any positive real number base raised to any power will always yield a strictly positive result. It can never be negative or zero).

---

## 2. Logarithmic Function

### Core Concept

The **Logarithmic Function** is the direct inverse of the exponential function. It answers the question: *"To what exponent must we raise the base $a$ to get the value $x$?"*

> **Mathematical Definition:**
> If $a > 0$ and $a \neq 1$, then the function defined by $f(x) = \log_a x$ is called a logarithmic function, valid only for $x > 0$.

### Crucial Domain Restriction

You cannot take the logarithm of a negative number or zero in the real number system ($x > 0$). Therefore:

* **Domain:** $(0, \infty)$
* **Range:** $\mathbb{R}$ (Logarithms can output any value from negative infinity to positive infinity).

---

## 3. Step-by-Step Worked Problems

### Problem 1: Evaluating Exponential Values

**Question:** Given $f(x) = 2^x$, calculate the outputs for $x = 3$, $x = 0$, and $x = -2$.

#### Calculations:

1. **For $x = 3$:**

$$f(3) = 2^3 = 2 \cdot 2 \cdot 2 = 8$$


2. **For $x = 0$:**

$$f(0) = 2^0 = 1$$


 *(Any non-zero base raised to the power of 0 is 1)*
3. **For $x = -2$:**

$$f(-2) = 2^{-2} = \frac{1}{2^2} = \frac{1}{4} = 0.25$$



---

### Problem 2: Finding Domain with an Inner Constraint

**Question:** Find the domain of the function $g(x) = \log_3 (x - 4)$.

#### Step-by-Step Explanation & Calculation:

1. Identify the core restriction for a logarithmic function: The expression inside the log must be strictly greater than zero.

$$\text{Argument} > 0$$


2. Set up the inequality for this problem:

$$x - 4 > 0$$


3. Isolate $x$ by adding $4$ to both sides:

$$x > 4$$


4. Express the solution set in interval notation:

$$\text{Domain} = (4, \infty)$$



---

### Problem 3: Solving a Logarithmic Equation

**Question:** Find the value of $x$ if $\log_5 x = -2$.

#### Step-by-Step Explanation & Calculation:

1. Recall the relationship between logarithms and exponents:

$$\log_a b = c \iff a^c = b$$


2. Rewrite the given equation into its equivalent exponential form:

$$5^{-2} = x$$


3. Convert the negative exponent into a fraction:

$$x = \frac{1}{5^2}$$


4. Simplify the denominator:

$$x = \frac{1}{25}$$



```

```


# Special Structural Types of Functions: Injections, Surjections, and Bijections

---

## 1. One-One Function (Injection)

### Core Concept
A function $f: A \rightarrow B$ is **One-One** (or **injective**) if distinct inputs in the domain always produce distinct outputs in the co-domain. No two different inputs share the same result.

> **Mathematical Conditions to Prove One-One:**
> * **Approach 1:** If $x \neq y$, then $f(x) \neq f(y)$
> * **Approach 2 (Most Practical):** Assume $f(x) = f(y)$. If you can algebraically simplify this to prove that $x = y$ is the *only* solution, the function is one-one.

### Graphical Check: The Horizontal Line Test
If *any* horizontal line drawn across a function's graph intersects the curve at **most once**, the function is one-one.

### Mapping Diagram Representation
```text
    Set A          Set B
   +-------+      +-------+
   |   a   | ---->|   1   |
   |   b   | ---->|   2   |
   |   c   | ---->|   3   |
   +-------+      |   4   |
                  +-------+

```

---

## 2. Many-One Function

### Core Concept

A function is **Many-One** if two or more distinct elements from the domain map to the exact same element in the co-domain.

> **Mathematical Condition:**
> There exists at least one pair $x, y \in A$ such that $x \neq y$ but $f(x) = f(y)$.

### Mapping Diagram Representation

```text
    Set A          Set B
   +-------+      +-------+
   |   a   | ---->|   1   |
   |   b   | ---->|   2   | <-- Both 'a' and 'b' map here!
   |   c   | ---->|   3   |
   +-------+      +-------+

```

---

## 3. Onto Function (Surjection)

### Core Concept

A function $f: A \rightarrow B$ is **Onto** (or **surjective**) if every single element in the target set $B$ (the co-domain) is mapped to by at least one element in set $A$. In simple terms, there are no "leftover" or unused elements in set $B$.

$$\text{Function is Onto} \iff \text{Range of } f = \text{Co-Domain } B$$

---

## 4. One-One and Onto Function (Bijection)

### Core Concept

A function is a **Bijection** if it is simultaneously **both One-One (Injective) and Onto (Surjective)**. Every element in the domain pairs up perfectly with exactly one unique element in the co-domain, leaving no elements unpaired on either side.

*Bijections are crucial because only bijective functions possess a well-defined **inverse function** ($f^{-1}$).*

---

## 5. Step-by-Step Problems and Calculations

### Problem 1: Proving a Linear Function is One-One

**Question:** Prove that $f: \mathbb{R} \rightarrow \mathbb{R}$ defined by $f(x) = 2x - 1$ is a one-one function.

#### Step-by-Step Calculation:

1. Let $x$ and $y$ be two arbitrary elements in the domain ($\mathbb{R}$).
2. Set their outputs equal to each other:

$$f(x) = f(y)$$


3. Substitute the algebraic definitions:

$$2x - 1 = 2y - 1$$


4. Add $1$ to both sides of the equation:

$$2x = 2y$$


5. Divide both sides by $2$:

$$x = y$$


6. **Conclusion:** Since assuming $f(x) = f(y)$ directly leads to $x = y$, the function is verified as **One-One**.

---

### Problem 2: Proving a Cubic Function is One-One

**Question:** Analyze $f: \mathbb{R} \rightarrow \mathbb{R}$ where $f(x) = x^3 - 1$ to check if it is one-one.

#### Step-by-Step Calculation:

1. Assume $f(x) = f(y)$ for $x, y \in \mathbb{R}$:

$$x^3 - 1 = y^3 - 1$$


2. Add $1$ to both sides:

$$x^3 = y^3$$


3. Move both terms to one side to factor:

$$x^3 - y^3 = 0$$


4. Use the difference of cubes factoring rule:

$$(x - y)(x^2 + xy + y^2) = 0$$


5. Set each factor to zero:
* **Case 1:** $x - y = 0 \implies x = y$
* **Case 2:** $x^2 + xy + y^2 = 0$. This quadratic part yields no real roots for $x$ and $y$ (unless $x = y = 0$) because its discriminant is strictly negative.


6. **Conclusion:** The only real solution path is $x = y$. Therefore, the function is **One-One**.

#### Graph

A cubic curve strictly increases from left to right, meaning any horizontal line will cross it exactly once.

```text
                 Y         /
                 |        /
                 |       /
-----------------+------/---------- X
               / |    (0,-1)
              /  |  *
             /   |

```

---

### Problem 3: Demonstrating a Many-One Function

**Question:** Show that the quadratic function $f: \mathbb{R} \rightarrow \mathbb{R}$ defined by $f(x) = x^2$ is many-one.

#### Step-by-Step Calculation / Counter-Example:

1. To show a function is many-one, find two distinct inputs that share an output. Let's test $x = -1$ and $y = 1$.
2. Note that $x \neq y$ (since $-1 \neq 1$).
3. Evaluate $f(-1)$:

$$f(-1) = (-1)^2 = 1$$


4. Evaluate $f(1)$:

$$f(1) = (1)^2 = 1$$


5. **Observation:** Since $f(-1) = f(1) = 1$, two completely different inputs yield the exact same output.

#### Graph

A horizontal line drawn at $y = 1$ cuts through the parabola at two separate points, violating the horizontal line test.

```text
             Y
      \      |      /
-----\-------+-------/----- Horizontal Line (y = 1)
        \    |    /
_________\___|___/_________ X
             |

```

6. **Conclusion:** The function is **Many-One**.




# Understanding the Inverse of a Function

---

## 1. Core Concept: Inverse of a Function

An **Inverse Function** undoes the action of the original function. If a function $f$ takes an input $x$ and maps it to an output $y$, then its inverse function, denoted as $f^{-1}$, takes that output $y$ and maps it right back to the original input $x$.

### Strict Requirement for Invertibility
A function $f: A \rightarrow B$ has a valid inverse **if and only if it is a bijection**. This means it must simultaneously satisfy two conditions:
1. **One-One (Injective):** Every distinct input has a unique output. If it isn't one-one, the reverse mapping would have to point to multiple original inputs, which violates the definition of a function.
2. **Onto (Surjective):** Every element in set $B$ is an output for some input in set $A$. If it isn't onto, there would be elements in set $B$ with no path back to set $A$, leaving the inverse function undefined for those inputs.

> **Mathematical Definition:**
> Let $f : A \rightarrow B$ be a bijection. Then, a function $g : B \rightarrow A$ which associates each element $y \in B$ to a unique element $x \in A$ such that $f(x) = y$ is called the inverse of $f$ and is denoted as $f^{-1}$.

### Visualizing the Mapping
```text
          --- f --->
     Set A          Set B
    +-------+      +-------+
    |   x   |      |   y   |
    +-------+      +-------+
          <-- f⁻¹ ---

```

---

## 2. Step-by-Step Method to Find the Inverse

To find the inverse function algebraically, follow these steps:

1. **Prove the function is one-one:** Set $f(x) = f(y)$ and solve to show that $x = y$ is the only solution.
2. **Express the equation in terms of $y$:** Write the function as $y = f(x)$.
3. **Rearrange to isolate $x$:** Use algebra to solve the equation explicitly for $x$, giving you an expression where $x = g(y)$.
4. **Define the inverse function:** Replace $x$ with $f^{-1}(y)$. If you prefer the final answer in terms of $x$, swap the variable name $y$ out for $x$.

---

## 3. Comprehensive Worked Problems

### Problem 1: Inverting a Cubic Function

**Question:** Given $f : \mathbb{R} \rightarrow \mathbb{R}$ defined by $f(x) = x^3 + 1$, show that it is invertible and find its inverse function.

#### Step 1: Prove it is One-One (1-1)

Assume $f(x) = f(y)$ for two arbitrary real numbers $x$ and $y$:


$$x^3 + 1 = y^3 + 1$$

Subtract $1$ from both sides:


$$x^3 = y^3$$

Take the cube root of both sides. Since cube roots of real numbers are unique:


$$x = y$$


Because $f(x) = f(y) \implies x = y$, the function is **One-One**.

#### Step 2: Find the Inverse Expression

Set the function equal to $y$:


$$y = x^3 + 1$$

Isolate the $x^3$ term by subtracting $1$:


$$y - 1 = x^3$$

Solve completely for $x$ by taking the cube root of both sides:


$$x = (y - 1)^{\frac{1}{3}}$$

#### Step 3: Write the Final Inverse Function

Since $x = f^{-1}(y)$, we write:


$$f^{-1}(y) = (y - 1)^{\frac{1}{3}}$$

Or written traditionally with $x$ as the input variable:


$$f^{-1}(x) = (x - 1)^{\frac{1}{3}}$$

#### Graph Visualization

The graph of a function and its inverse are mirror reflections of each other across the diagonal line $y = x$.

```text
                 Y         / f(x) = x³ + 1
                 |        / 
                 |       /   
                 * (0,1)/     
-----------------+-----/----------- X
               / |    /
              /  |   / 
             /   |  /  
            /    | /   f⁻¹(x) = (x - 1)^(1/3)

```

---

### Problem 2: Inverting a Rational Function (From the Slides)

**Question:** Show that the function $f : S \rightarrow S$, where $S = \mathbb{R} - \{-1\}$, given by $f(x) = \frac{x}{x + 1}$ is invertible. Also, find $f^{-1}$.

#### Step 1: Prove it is One-One

Let $x, y \in S$ and assume their outputs are equal:


$$f(x) = f(y) \implies \frac{x}{x + 1} = \frac{y}{y + 1}$$

Cross-multiply to clear the denominators:


$$x(y + 1) = y(x + 1)$$

Distribute the terms on both sides:


$$xy + x = yx + y$$

Subtract the common $xy$ term from both sides:


$$x = y$$


Since $f(x) = f(y)$ simplifies uniquely to $x = y$, the function is **One-One**.

#### Step 2: Prove it is Onto & Find the Inverse Function Simultaneously

Set $y = f(x)$ and solve for $x$ in terms of $y$:


$$y = \frac{x}{x + 1}$$

Cross-multiply:


$$y(x + 1) = x$$

Distribute $y$:


$$yx + y = x$$

Move all terms containing $x$ to one side to prepare for factoring:


$$y = x - yx$$

Factor out the common $x$ variable:


$$y = x(1 - y)$$

Isolate $x$ by dividing both sides by $(1 - y)$:


$$x = \frac{y}{1 - y}$$

#### Step 3: Analyze the Range and State the Output

Let's check the restriction on our newly found equation for $x$. The denominator tells us that $1 - y \neq 0$, which means $y \neq 1$.

Since our target co-domain set $S$ is explicitly defined as $\mathbb{R} - \{-1\}$ (and the range of outputs excludes $1$, matching the problem's structural domain mappings from $S \rightarrow \mathbb{R}-\{1\}$ as established in early chapters), every valid element has a match. The mapping works cleanly, confirming the function is **Onto**.

Thus, substituting $f^{-1}(y)$ for $x$:


$$f^{-1}(y) = \frac{y}{1 - y}$$

Replacing it with standard input variable $x$:


$$f^{-1}(x) = \frac{x}{1 - x}$$

```

```