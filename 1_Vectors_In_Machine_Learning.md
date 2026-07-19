# Linear Algebra Notes: Vectors

## What is a Vector?
A **vector** is a mathematical object that encodes a length and direction. 

More formally, they are elements of a **vector space**: a collection of objects that is closed under an addition rule and a rule for multiplication by scalars.

---

## Representations of Vectors

### 1. Computer Science / Numerical Representation
A vector is often represented as a **1-dimensional array of numbers**, referred to as components, and is displayed either in column form or row form.

### 2. Geometric Representation
Represented geometrically, vectors typically represent coordinates within an **$n$-dimensional space**, where $n$ is the number of dimensions.

> **Simplistic Representation:** > A simplistic representation of a vector might be an arrow in a vector space, with an origin, direction, and magnitude (length). 
>
# Linear Algebra Notes: Vectors in $\mathbb{R}^n$

## Geometric Examples ($n = 2$ and $n = 3$)

### Case 1: Take $n = 2 \implies \mathbb{R}^2$ ($\mathbb{R} \times \mathbb{R}$)
A vector in 2D space represents a point or a directed arrow on a Cartesian plane.

* **Vector:** $v = (1, 2)$
* **Visual Representation:** An arrow starting at the origin and pointing to the coordinates $(1,2)$ at an angle $\theta$ relative to the x-axis.

### Case 2: Take $n = 3 \implies \mathbb{R}^3$
A vector in 3D space introduces a third depth axis ($z$-axis).

* **Vector:** $v = (1, 2, 3)$
* **Visual Representation:** Points in a three-dimensional coordinate system with $x$, $y$, and $z$ axes.

---

## Formal Definition of $\mathbb{R}^n$

An $n$-dimensional vector consists of $n$ components where each component belongs to the set of real numbers ($\mathbb{R}$).

### Row Vector Notation
$$v = [v_1, v_2, \dots, v_n] \in \mathbb{R}^n \quad \text{where } v_i \in \mathbb{R}$$

### Column Vector Notation
$$v = \begin{bmatrix} v_1 \\ v_2 \\ \vdots \\ v_n \end{bmatrix} \in \mathbb{R}^n$$

# Linear Algebra Notes: Vector Algebra

## Key Operations Covered
* Addition / Subtraction
* Dot Product
* Length / Magnitude
* Angle between two vectors

---

## Example in $\mathbb{R}^2$

Given two vectors:
$$v_1 = (1, 3) \quad \text{and} \quad v_2 = (1, 1)$$

### Vector Addition
$$v_1 + v_2 = (1 + 1, 3 + 1) = (2, 4)$$

* **Geometric Interpretation:** In the coordinate system, adding $v_2$ to the tip of $v_1$ results in a new vector pointing directly to the coordinates $(2, 4)$.

### Vector Subtraction
$$v_1 - v_2 = (1 - 1, 3 - 1) = (0, 2)$$

---

## Generalization to $\mathbb{R}^n$

For any two vectors in an $n$-dimensional space:
$$v_1 = (x_1, x_2, \dots, x_n)$$
$$v_2 = (y_1, y_2, \dots, y_n)$$

### Component-wise Addition and Subtraction
$$v_1 \pm v_2 = (x_1 \pm y_1, x_2 \pm y_2, \dots, x_n \pm y_n)$$

# Linear Algebra Notes: Vector Algebra (Part 2)

## 1. Dot Product (Inner Product)

For two vectors in $\mathbb{R}^n$:
$$v_1 = (x_1, x_2, \dots, x_n) \in \mathbb{R}^n$$
$$v_2 = (y_1, y_2, \dots, y_n) \in \mathbb{R}^n$$

The dot product is the sum of the products of their corresponding components:
$$v_1 \cdot v_2 = x_1 y_1 + x_2 y_2 + \dots + x_n y_n = \sum_{i=1}^{n} x_i y_i$$

### Example in $\mathbb{R}^3$
Given:
$$v_1 = (1, 1, -1) \quad \text{and} \quad v_2 = (2, 3, 1)$$

$$v_1 \cdot v_2 = (1 \times 2) + (1 \times 3) + (-1 \times 1) = 2 + 3 - 1 = 4$$

---

## 2. Length / Magnitude of a Vector

The length (norm) of a vector $\vec{v} = (x_1, x_2, \dots, x_n)$ is defined as the square root of the dot product of the vector with itself:

$$|\vec{v}| = v = \sqrt{\vec{v} \cdot \vec{v}} = \sqrt{x_1^2 + x_2^2 + \dots + x_n^2}$$

### Example
Given $\vec{v} = (1, -1, 2)$:
$$|\vec{v}| = \sqrt{1^2 + (-1)^2 + 2^2} = \sqrt{1 + 1 + 4} = \sqrt{6}$$

---

## 3. Angle Between Two Vectors

For any two non-zero vectors $\vec{v}_1, \vec{v}_2 \in \mathbb{R}^n$, the angle $\theta$ between them is calculated using the formula:

$$\theta = \cos^{-1} \left( \frac{\vec{v}_1 \cdot \vec{v}_2}{|\vec{v}_1| |\vec{v}_2|} \right)$$


# Linear Algebra Notes: Linear Combination of Vectors

## Definition

Consider a set of vectors $S = \{v_1, v_2, \dots, v_k\}$. A new vector $v$ defined by:

$$v = \alpha_1 v_1 + \alpha_2 v_2 + \dots + \alpha_k v_k$$

is called a **linear combination** of $v_1, v_2, \dots, v_k$, where $\alpha_1, \alpha_2, \dots, \alpha_k$ are **scalars**.

---

## Example

Given the following vectors in $\mathbb{R}^3$:
$$v_1 = (1, 2, -1), \quad v_2 = (1, 1, 0), \quad v_3 = (0, 1, -1)$$

We can set up their linear combination as:
$$\alpha_1 v_1 + \alpha_2 v_2 + \alpha_3 v_3 = \alpha_1(1, 2, -1) + \alpha_2(1, 1, 0) + \alpha_3(0, 1, -1)$$

### Component-wise Expansion
By distributing the scalars and adding the components together, we get the final combined vector:

$$\implies \big(\alpha_1 + \alpha_2, \; 2\alpha_1 + \alpha_2 + \alpha_3, \; -\alpha_1 - \alpha_3\big)$$


# Linear Algebra Notes: Linearly Independent and Dependent Vectors

## Definitions

### Linearly Independent (LI)
A set of vectors $S = \{v_1, v_2, \dots, v_n\}$ is **linearly independent** if the vector equation:

$$\alpha_1 v_1 + \alpha_2 v_2 + \dots + \alpha_n v_n = \vec{0}$$

holds **only** when all scalars are zero:
$$\alpha_1 = \alpha_2 = \dots = \alpha_n = 0$$

### Linearly Dependent (LD)
Else (if there exists at least one non-zero scalar $\alpha_i$ that satisfies the equation), the set $S$ is **linearly dependent**.

---

## Examples in $\mathbb{R}^2$

### Example 1: Linearly Independent Set

Let $S = \{(1, 0), (1, 1)\}$

Set up the vector equation:
$$\alpha_1 (1, 0) + \alpha_2 (1, 1) = (0, 0)$$

This creates the following system of linear equations:
$$\begin{aligned}
\alpha_1 + \alpha_2 &= 0 \\
\alpha_2 &= 0
\end{aligned}$$

Substituting $\alpha_2 = 0$ into the first equation yields $\alpha_1 = 0$.

* Since $\alpha_1 = 0$ and $\alpha_2 = 0$, the set $S$ contains **Linearly Independent (LI)** vectors.

### Example 2: Linearly Dependent Set
Let $S' = \{(1, 1), (3, 3)\}$

We can find a non-trivial combination where the scalars are not all zero:
$$(-3)(1, 1) + (1)(3, 3) = (-3, -3) + (3, 3) = (0, 0)$$

Here, $\alpha_1 = -3$ and $\alpha_2 = 1$. 
* Since non-zero scalars satisfy the zero vector equation, **$S'$ contains LD vectors.**

# Linear Algebra Notes: Linear Independence and Dependence (Examples in $\mathbb{R}^3$)

## Example 1: Linearly Dependent (LD) Set

Consider the set of vectors $S \in \mathbb{R}^3$:
$$S = \{v_1, v_2, v_3\} = \{(1, -1, 0), \; (1, 0, 1), \; (0, 1, 1)\}$$

Let's test if non-zero scalars can satisfy the vector dependency equation. Take the scalars:
$$\alpha_1 = 1, \quad \alpha_2 = -1, \quad \alpha_3 = 1$$

Substitute them into the linear combination:
$$\begin{aligned}
\alpha_1 (1, -1, 0) + \alpha_2 (1, 0, 1) + \alpha_3 (0, 1, 1) &= 1(1, -1, 0) + (-1)(1, 0, 1) + 1(0, 1, 1) \\
&= (1 - 1 + 0, \; -1 + 0 + 1, \; 0 - 1 + 1) \\
&= (0, 0, 0)
\end{aligned}$$

* Since a non-trivial solution (where scalars are not all zero) yields the zero vector, **$S$ is a Linearly Dependent (LD) set of vectors.**

### Algebraic Dependency Proof
A set is dependent because at least one vector can be written as a combination of the others:
$$v_2 = v_1 + v_3$$
$$(1, -1, 0) + (0, 1, 1) = (1, 0, 1) = v_2$$

---

## Example 2: Standard Basis Vectors in $\mathbb{R}^3$

Consider the standard unit vectors:
$$\{(1, 0, 0), \; (0, 1, 0), \; (0, 0, 1)\}$$

> *Note: This is a classic example of a **linearly independent** set since no vector can be created using any combination of the other two.*


# Linear Algebra Notes: Key Remarks on Linear Independence and Dependence

> ### 📌 Important Remarks
> 
> 1. In $\mathbb{R}^n$, a set of **more than $n$ vectors** is always Linearly Dependent (LD).
>    * *Example:* Any set containing 3 or more vectors in $\mathbb{R}^2$ is automatically linearly dependent.
> 
> 2. Any set containing the **zero vector** ($\vec{0}$) is always Linearly Dependent (LD).

Here is the clean, structured Markdown code for your lecture notes on **Orthogonal Vectors**. You can copy and paste this directly into your VS Code `.md` file.

---


# Orthogonal Vectors

## Definition

We say that a set of vectors $\{v_1, v_2, \dots, v_n\}$ are **mutually (pairwise) orthogonal** if the dot product of any two distinct vectors is zero:

$$v_i \cdot v_j = 0 \quad \text{for } i \neq j$$

---

## Example in $\mathbb{R}^3$

Consider the following set of three vectors:
$$S = \{ (1, 0, -1), (1, \sqrt{2}, 1), (1, -\sqrt{2}, 1) \}$$

To check if they are mutually orthogonal, we compute the dot product for every unique pair:

1. **Pair 1 & 2:**
   $$(1, 0, -1) \cdot (1, \sqrt{2}, 1) = (1 \times 1) + (0 \times \sqrt{2}) + (-1 \times 1) = 1 + 0 - 1 = 0$$

2. **Pair 1 & 3:**
   $$(1, 0, -1) \cdot (1, -\sqrt{2}, 1) = (1 \times 1) + (0 \times -\sqrt{2}) + (-1 \times 1) = 1 + 0 - 1 = 0$$

3. **Pair 2 & 3:**
   $$(1, \sqrt{2}, 1) \cdot (1, -\sqrt{2}, 1) = (1 \times 1) + (\sqrt{2} \times -\sqrt{2}) + (1 \times 1) = 1 - 2 + 1 = 0$$

* Since all pairwise dot products equal $0$, the set consists of **mutually orthogonal vectors**.

## Orthonormal Vectors

### Definition
A set of orthogonal vectors is **orthonormal** if each individual vector has a length (magnitude) of exactly $1$.

$$\text{Orthonormal} = \text{Orthogonal} + \text{Normalized (Length = 1)}$$

### Example
Consider the set 

$$S = \left\{ \left(\frac{1}{\sqrt{2}}, \frac{1}{\sqrt{2}}\right), \; \left(\frac{1}{\sqrt{2}}, -\frac{1}{\sqrt{2}}\right) \right\}$$

1. **Check Orthogonality (Dot Product = 0):**
   $$\left(\frac{1}{\sqrt{2}}\right)\left(\frac{1}{\sqrt{2}}\right) + \left(\frac{1}{\sqrt{2}}\right)\left(-\frac{1}{\sqrt{2}}\right) = \frac{1}{2} - \frac{1}{2} = 0 \quad \checkmark$$

2. **Check Length (Magnitude = 1):**
   $$\left\|v_1\right\| = \sqrt{\left(\frac{1}{\sqrt{2}}\right)^2 + \left(\frac{1}{\sqrt{2}}\right)^2} = \sqrt{\frac{1}{2} + \frac{1}{2}} = \sqrt{1} = 1 \quad \checkmark$$

> ### 📌 Important Remark
> A set of non-zero orthogonal vectors is always **Linearly Independent (LI)**.

---

## Machine Learning Application: An Example of Feature Vectors

In data science and machine learning, vectors are used to represent data points, where individual components correspond to specific **features** or **attributes**.

### Feature Table Representation

| Entity / Sample | Feature 1: Height | Feature 2: Weight |
| :--- | :---: | :---: |
| $e_1$ | $\alpha_1$ | $\beta_1$ |
| $e_2$ | $\alpha_2$ | $\beta_2$ |
| $\vdots$ | $\vdots$ | $\vdots$ |
| $e_k$ | $\alpha_k$ | $\beta_k$ |

### Feature Vector Formulation
Each row can be extracted as a coordinate point or a vector. For instance, the 20th entity in the dataset would be represented by the feature vector:

$$v_{20} = (\alpha_{20}, \; \beta_{20})$$


### Python Code Executable via NumPy

```python
import numpy as np

# 1. Initialize Vectors
v = np.array([1, -1, 2])
w = np.array([2, 5, 2])

# 2. Vector Addition
# Output: [3 4 4]
print("Addition:", v + w)

# 3. Vector Subtraction
# Output: [-1 -6  0]
print("Subtraction:", v - w)

# 4. Scalar Multiplication
# Output: [ 3 -3  6]
print("Scalar Multiplication:", 3 * v)

# 5. Vector Length / Magnitude (Norm)
# Output: 2.449489742783178
print("L2 Norm / Length:", np.linalg.norm(v))

# 6. Dot Product
# Output: 1
s = np.dot(v, w)
print("Dot Product:", s)

