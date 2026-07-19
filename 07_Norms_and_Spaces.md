## 7. Norms and Spaces

### Introduction

In this lecture, we will discuss about Metric spaces, Normed spaces and Inner product spaces. These spaces are really needed to make in depth analysis of some of the ML algorithms.



### Metric Spaces

It is a generalization of the notion of distance from Euclidean space.

#### Definition

A metric on a set $S$ is a function

$$d : S \times S \longrightarrow \mathbb{R}$$

such that:

1. $d(x, y) \geqslant 0 \quad \forall x, y \in S$ and $d(x, y) = 0 \iff x = y$
2. $d(x, y) = d(y, x) \quad \forall x, y \in S$
3. $d(x, z) \leqslant d(x, y) + d(y, z) \quad \forall x, y, z \in S$

#### Example

Take $S \subseteq \mathbb{R}$ and define

$$d(x, y) = |x - y|$$

then $(S, d)$ forms a metric space.



---

## Metric Spaces

### Definition

A **metric** on a set $S$ is a function:

$$d : S \times S \longrightarrow \mathbb{R}$$

that assigns a real number as the distance between any two elements in $S$. The pair $(S, d)$ is called a **metric space**. To be considered a valid metric, the function must satisfy three fundamental properties:

---

### Property 1: Non-Negativity & Identity of Indiscernibles

#### Statement

$$d(x, y) \geqslant 0 \quad \forall x, y \in S \quad \text{and} \quad d(x, y) = 0 \iff x = y$$

#### The Intuition: Why is it defined like this?

* **Non-Negativity ($d(x, y) \geqslant 0$):** Real-world distance can never be negative. It makes no physical or logical sense to say that two objects are $-5$ meters apart.
* **Identity of Indiscernibles ($d(x,y) = 0 \iff x = y$):** * If you do not move, your travel distance is exactly zero ($x = y \implies d=0$).
* Conversely, if the distance between two points is absolutely zero, those two points must actually be the exact same point ($d=0 \implies x = y$). They cannot occupy different locations in space.



---

### Property 2: Symmetry

#### Statement

$$d(x, y) = d(y, x) \quad \forall x, y \in S$$

#### The Intuition: Why is it defined like this?

Distance is a two-way street. The distance from point $A$ to point $B$ must be exactly equal to the distance from point $B$ back to point $A$. A valid mathematical metric rules out "one-way paths" or directional biases where going forward measures differently than coming backward.

---

### Property 3: Triangle Inequality

#### Statement

$$d(x, z) \leqslant d(x, y) + d(y, z) \quad \forall x, y, z \in S$$

#### The Intuition: Why is it defined like this?

This rule establishes that **a straight line is always the shortest distance between two points**.

If you want to travel from $x$ to $z$, taking a detour through a third stop $y$ will always take just as long ($=$ if $y$ lies perfectly on the line segment between $x$ and $z$) or longer ($>$ if $y$ forces you out of your way). It prevents shortcuts through indirect routes from breaking the structure of space.

---

## Practical Examples of Metric Spaces

### Example 1: The Absolute Difference Metric (From your notes)

Take a subset of the real numbers $S \subseteq \mathbb{R}$ and define the function as:

$$d(x, y) = |x - y|$$

#### Verification Check:

1. **Property 1:** Absolute values are always greater than or equal to $0$. $|x - y| = 0$ is only possible if $x - y = 0$, which means $x = y$.
2. **Property 2:** $|x - y| = |-(y - x)| = |y - x|$. Symmetry holds perfectly.
3. **Property 3:** By the algebraic properties of absolute values, $|x - z| = |(x - y) + (y - z)| \leqslant |x - y| + |y - z|$. Triangle inequality holds.

Therefore, $(S, d)$ is a valid metric space.

---

### Example 2: The Discrete Metric (A different way to think about space)

Metrics don't just have to be geometric. For any non-empty set $S$, define:

$$d(x, y) = \begin{cases} 0 & \text{if } x = y \\ 1 & \text{if } x \neq y \end{cases}$$

#### Why it works:

Even though it sounds strange (everything that isn't itself is exactly distance $1$ away), it fully satisfies all three conditions:

* It is never negative, and only zero when items are identical.
* It is symmetric.
* If you check three distinct points $x, y, z$, the triangle inequality simplifies to $1 \leqslant 1 + 1$, which is absolutely true!

Here is the transcription of the handwritten text from the image using standard Markdown and LaTeX for the mathematical expressions.

---

## **Norm**

A norm on a real vector space $V$ is a function


$$\|\cdot\| : V \longrightarrow \mathbb{R}$$

such that:

1. $\|x\| \ge 0 \quad \forall x \in V \text{ and } \|x\| = 0 \iff x = \vec{0}$
2. $\|\alpha x\| = |\alpha| \|x\| \quad \forall x \in V \text{ and } \alpha \in \mathbb{R}$
3. $\|x + Y\| \le \|x\| + \|Y\| \quad \forall x, Y \in V$

$(V, \|\cdot\|)$ is called a **normed space**.



---

## **Relation:**

```
┌─────────────────────────────────┐
│           Metric Space          │
│                                 │
│      ┌──────────────────┐       │
│      │   Normed Space   │       │
│      └──────────────────┘       │
└─────────────────────────────────┘

```

* **Every normed space is a metric space**
* **Converse is not true**

**Ex:** Let $X = \{0, 1\}$

$$d(x, y) = \begin{cases} 1 & \text{if } x \neq y \\ 0 & \text{otherwise} \end{cases}$$

$(X, d)$ is a **metric space**, but **not a normed space**.



---

### **Examples of some norms on $\mathbb{R}^n$**

* $\|X\|_1 = \sum_{i=1}^{n} |x_i|$
* $\|X\|_2 = \left( \sum_{i=1}^{n} x_i^2 \right)^{1/2}$
* $\|X\|_p = \left( \sum_{i=1}^{n} |x_i|^p \right)^{1/p}$
* $\|X\|_\infty = \max_{1 \le i \le n} |x_i|$


## **Examples:** Let $V = \mathbb{R}^3(\mathbb{R})$

$$X = (1, 0, -2)$$

* **Manhattan norm:**

$$\|X\|_1 = 1 + 0 + |-2| = 3$$


* $$\|X\|_2 = \left(1^2 + 0^2 + (-2)^2\right)^{1/2} = \sqrt{5}$$


* $$\|X\|_\infty = 2$$



---

### **Geometric Representation (Unit Balls)**

Here is a text-based visualization representing the unit balls for the different norms shown in your diagram:

```
               ▲
               │      ┌─────────┐ ◄─── ∞-norm (Square)
               │   ───│───      │
               │ ╱    │    ╲    │
               ╱      │      ╲  │
              ╱│      │      │╲ │
 ────────────‡─┼──────┼──────┼─‡────────►
            ╱  │      │      │  ╲
           ╱   │      │      │   ╲
          ╱    │   ───│───   │    ╲ ◄─ 2-norm (Circle)
         ◄─────┴──────┴──────┴────► 1-norm (Diamond)
               │      └─────────┘
               │
               │

```




## **Convex function:**

A function $f : S \subseteq \mathbb{R}^n \longrightarrow \mathbb{R}$ is said to be **convex**, if for $x_1, x_2 \in S$, we have:

$$f(\lambda x_1 + (1-\lambda)x_2) \le \lambda f(x_1) + (1-\lambda)f(x_2)$$

where, $0 \le \lambda \le 1$

---

## **Convex set:**

A set is said to be **convex**, if the line joining any two points of the set lies entirely in the set $S$.

$$x_1, x_2 \in S \implies \lambda x_1 + (1-\lambda)x_2 \in S$$

---

### **Geometric Representation**

Here is a text-based visualization of the diagram provided in your notes, showing both the function curve and the chord connecting $f(x_1)$ and $f(x_2)$:

```text
         │                 
  \      │      /    ◄─── f(x) (Convex Curve)
   •═════┼═════•     ◄─── Chord connecting f(x₁) and f(x₂) 
   │\    │    /│          (lies above the curve)
   │ \   │   / │             
───‡──└──┼──┘──‡─────────►
  x₁   \ │ /   x₂            
        ─┴─          ◄─── Line segment between x₁ and x₂ on the axis

```


## **Inner Product Spaces**

An inner product on a real vector space $V$ is a function

$$\langle \cdot, \cdot \rangle : V \times V \longrightarrow \mathbb{R}$$

satisfying:

1. $\langle X, X \rangle \ge 0 \quad \forall X \in V \text{ and } \langle X, X \rangle = 0 \iff X = 0$
2. $\langle X + Y, Z \rangle = \langle X, Z \rangle + \langle Y, Z \rangle \text{ and } \langle \alpha X, Y \rangle = \alpha \langle X, Y \rangle \quad \forall X, Y, Z \in V \text{ and } \alpha \in \mathbb{R}$
3. $\langle X, Y \rangle = \langle Y, X \rangle \quad \forall X, Y \in V$

A vector space together with an inner product is called an **inner product space**.



## **Examples of inner product spaces:**

### **Euclidean Inner Product on $\mathbb{R}^n$**

Let $V = \mathbb{R}^n(\mathbb{R})$

$$\langle X, Y \rangle = \sum_{i=1}^{n} x_i y_i = x_1 y_1 + x_2 y_2 + \cdots + x_n y_n$$

Where,

* $X = (x_1, x_2, \dots, x_n)$
* $Y = (y_1, y_2, \dots, y_n)$

---

### **Geometric Interpretation**

This is also known as the **dot product**:

$$X \cdot Y$$

$$\langle X, Y \rangle = \|X\| \|Y\| \cos \theta$$


### **Examples of inner product on $\mathbb{R}^n$**

1. Let $V = \mathbb{R}^n$, let $\mathbf{x} = (x_1, x_2, \dots, x_n), \mathbf{y} = (y_1, y_2, \dots, y_n) \in \mathbb{R}^n$. Then the **standard inner product** on $\mathbb{R}^n$ is given as follows:

$$\langle \mathbf{x}, \mathbf{y} \rangle = \sum_{i=1}^{n} x_i y_i$$


2. Let $V = \mathbb{R}^2$, $\mathbf{u} = (u_1, u_2), \mathbf{v} = (v_1, v_2) \in \mathbb{R}^2$. Then an inner product is defined as:

$$\langle \mathbf{u}, \mathbf{v} \rangle = 2u_1 v_1 - u_1 v_2 - v_1 u_2 + u_2 v_2$$



## **$l_0$-norm:**

$\|X\|_0$ is the number of nonzero elements of $X$.

$$X = (1, 2, 0, 0, 3, 0, 0, 4) \in \mathbb{R}^8$$

then $\|X\|_0 = 4$  $\qquad \text{[Compressed Sensing]}$

---

### **Property Counterexample:**

2. $\| \alpha X \|_0 \neq |\alpha| \|X\|_0$ for $\alpha \neq 1$
Let $\alpha = 2$:
* **$\text{L.H.S.}$** $= 4$
* **$\text{R.H.S.}$** $= 2 \cdot 4 = 8$



---

## **Mathematical Example**

Let's pick a vector $X$ in $\mathbb{R}^3$ and a scalar $\alpha$:

* **Vector:** $X = (5, 0, -7)$
* **Scalar:** $\alpha = 3$

### **1. Calculate the Left-Hand Side (L.H.S.): $\| \alpha X \|_0$**

First, multiply the vector by the scalar:


$$\alpha X = 3 \cdot (5, 0, -7) = (15, 0, -21)$$

Now, count the number of non-zero elements in $\alpha X$:

* $15$ is non-zero.
* $0$ is zero.
* $-21$ is non-zero.

$$\|\alpha X\|_0 = 2$$

### **2. Calculate the Right-Hand Side (R.H.S.): $|\alpha| \cdot \|X\|_0$**

First, find the number of non-zero elements in the original vector $X = (5, 0, -7)$:


$$\|X\|_0 = 2 \quad \text{(since 5 and -7 are non-zero)}$$

Now, multiply by the absolute value of the scalar $|\alpha|$:


$$|\alpha| \cdot \|X\|_0 = |3| \cdot 2 = 3 \cdot 2 = 6$$

### **Conclusion**

$$\text{L.H.S.} \neq \text{R.H.S.} \quad (2 \neq 6)$$

Because scaling a vector changes the *values* of its components but **does not change whether they are zero or non-zero**, the absolute value multiplication rule breaks down. This is why mathematicians refer to it as a **pseudo-norm** rather than a true norm.

---

## **Application: Compressed Sensing**

Even though it isn't a strict mathematical norm, the $l_0$-norm is incredibly useful in **Compressed Sensing** and data compression.

When transmitting huge amounts of data (like medical MRI images or audio signals), we want the data to be **sparse** (having as many zeros as possible) so it takes up less storage.

* **Optimization Problem:** Algorithms try to minimize $\|X\|_0$ to find the absolute sharpest, most data-efficient representation of a signal without losing its core information.



---

### **Geometric Interpretation (Unit Balls)**

Here are the text-based visualizations for the geometric shapes drawn in your notes, analyzing whether they meet the criteria to define a norm:

#### **1. Oval / Ellipse (Valid Norm)**

* **Symmetric:** Yes (balanced across both axes)
* **Convex:** Yes (no inward curves)
* **Verdict:** ✅ Defines a norm (closely related to the 2-norm / Euclidean distance).

```text
       ▲
     ╱ │ ╲
   ─┼──┼──┼─►
     ╲ │ ╱
       ▼

```

#### **2. Hourglass-like / Concave Box (Invalid Norm)**

* **Symmetric:** Yes
* **Convex:** ❌ **No**. The left and right sides curve inward. If you connect two points near the edges, the line leaves the shape.
* **Verdict:** ❌ Does **not** define a norm.

```text
       ▲
    │╲ │ ╱│
    │ ─┼─ │►
    │╱ │ ╲│
       ▼

```

#### **3. Curved Cylinder / Capsule Shape (Valid Norm)**

* **Symmetric:** Yes
* **Convex:** Yes (the sides bow outward smoothly)
* **Verdict:** ✅ Defines a norm.

```text
       ▲
     ╭─┼─╮
     │ │ │
    ─┼─┼─┼─►
     │ │ │
     ╰─┼─╯
       ▼

```

#### **4. Regular Polygon / Octagon (Valid Norm)**

* **Symmetric:** Yes
* **Convex:** Yes (straight geometric edges bowing outward)
* **Verdict:** ✅ Defines a norm.

```text
       ▲
     ╱─┼─╲
    │  │  │
   ─┼──┼──┼─►
    │  │  │
     ╲─┼─╱
       ▼

```