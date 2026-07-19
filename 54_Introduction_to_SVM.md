# Machine Learning Foundations & Support Vector Machines (SVM)

---

## 1. Concept: Introduction to Machine Learning
### **Simple Meaning**
Machine Learning is all about algorithms discovering hidden rules from existing data (like photos, test metrics, or records) to make smart, automated decisions in the future. Instead of explicitly coding a rule, the computer finds it by itself.

### **Core Definitions**
* **Machine Learning:** Deals with learning from data (images, measurements, observations, patterns, or records).
* **Primary Objective:** Perform well on the provided **training data** and generalize effectively to ensure accurate results on unseen future data.
* **The Three Main Problem Domains:** Classification, Clustering, and Regression.

---

## 2. Concept: Mathematical Programming Approach in ML
### **Simple Meaning**
When we train a machine learning model, we want to find the parameter settings that make the fewest mistakes. We translate this goal into math equations called **Optimization Problems**. We want to minimize error or maximize accuracy.

### **Mathematical Paradigms**
Many approaches tackle machine learning problems through optimization frameworks introduced by Mangasarian:
* **Linear Programming Problem (LPP):** Equations and constraints use flat lines ($x_1 + x_2$).
* **Quadratic Programming Problem (QPP):** The goal has squared terms ($x^2$), creating a curved bowl shape.
* **Convex Programming Problem (CPP):** A broader category where any local minimum point is guaranteed to be the absolute lowest, most optimal point (global minimum).

> **Key Theory Tools:** Karush-Kuhn-Tucker (**KKT**) conditions and **Duality Theory** are foundational tools utilized to calculate and verify exact solutions for these convex programming problems.

---

## 3. Concept: Supervised vs. Unsupervised Learning

Machine learning problems split cleanly based on whether the training data comes with an explicit "answer key" label:


```
                     ┌─────────────────────────────┐
                     │  Machine Learning Problems  │
                     └──────────────┬──────────────┘
                                    │
            ┌───────────────────────┴───────────────────────┐
            ▼                                               ▼
┌───────────────────────┐                       ┌───────────────────────┐
│  Supervised Learning  │                       │ Unsupervised Learning │
└───────────┬───────────┘                       └───────────┬───────────┘
            │                                               │
     ┌──────┴──────┐                                        │
     ▼             ▼                                        ▼
┌──────────────┐ ┌────────────┐                       ┌────────────┐
│Classification│ │ Regression │                       │ Clustering │
└──────────────┘ └────────────┘                       └────────────┘

```

### **The Dichotomy Split**
* **Supervised Learning:** The dataset contains input features paired with target output labels. 
  * *Classification:* Predicting a discrete category label (e.g., "Spam" vs. "Not Spam").
  * *Regression:* Predicting a continuous value (e.g., housing prices).
* **Unsupervised Learning:** The dataset contains unlabeled inputs.
  * *Clustering:* Grouping data points together by natural similarity alone (e.g., customer segmentation).

---

## 4. Concept: Support Vector Machines (SVM)
### **Simple Meaning**
Developed by Vapnik, SVM is a highly effective classifier. If you have two groups of mixed data points on a graph, SVM draws a decision line directly between them with the widest possible empty safety zone (margin) on both sides.


```

```
   ▲ y
   │          ═══════════  (Upper Boundary)
   │    o    o    o
   │ ───────────────────  (Optimal Decision Line / Hyperplane)
   │    x    x    x
   │          ═══════════  (Lower Boundary)
   └────────────────────────► x

```

```

### **Mathematical Advantage**
* **Global Optimality:** Because SVM formulates its optimization structure as a **convex programming problem**, algorithms are mathematically guaranteed to reach the true **global optimal solution** rather than getting stuck in false localized low points.
* **KKT Sufficiency:** Under convex constraints, satisfying the first-order derivative KKT conditions is completely **sufficient** to confirm you have found the perfect optimal model parameters.

---

## 5. Mathematical Problems with Step-by-Step Solutions

### **Problem 1: Categorizing ML Tasks**
**Scenario:** A clinic gathers a collection of patient measurements (blood pressure, age) and wants to build two systems:
1. System A predicts whether a patient's tumor is benign or malignant.
2. System B automatically groups similar general patient profiles together to identify new unclassified syndromes.

**Question:** Identify the class of machine learning techniques required for System A and System B based on the core pillars.

#### **Step-by-Step Solution:**
* **Step 1 (Analyze System A):** The goal requires choosing between two discrete categories ("benign" vs "malignant"). This is a targeted decision process relying on existing medical labels. Therefore, it is a **Classification** problem belonging to **Supervised Learning**.
* **Step 2 (Analyze System B):** The goal requires grouping patient data by patterns without using pre-existing labels. Therefore, it is a **Clustering** task belonging to **Unsupervised Learning**.

---

### **Problem 2: Linear Optimization Problem Formulation**
**Scenario:** Let a simplified linear model have a single parameter weight $w$. We want to minimize a cost function $J(w) = 4w$, subject to the linear constraint that $w \ge 3$. 

**Question:** Calculate the optimal solution $w^*$ and determine if it forms a Convex Programming Problem.

#### **Step-by-Step Calculation:**
* **Step 1 (Check Convexity):** The objective function $J(w) = 4w$ is linear, and the constraint domain $w \ge 3$ is a convex set. Since any linear function is convex, this is a **Convex Programming Problem (CPP)**.
* **Step 2 (Apply Constraints):** The objective function $J(w) = 4w$ increases as $w$ increases. To make $J(w)$ as small as possible, we must choose the absolute smallest value allowed by the constraint domain.
* **Step 3 (Solve):** Given $w \ge 3$, the absolute smallest feasible value is:
  $$w^* = 3$$
* **Step 4 (Compute Optimal Cost):** 
  $$J(3) = 4(3) = 12$$
Because it is a convex problem, this localized edge point is mathematically guaranteed to be the **global optimal solution**.


# Support Vector Machines: Linear Separability & Binary Pattern Classification

---

## 1. Concept: Binary Pattern Classification

### **Simple Meaning**
In machine learning, a **pattern** is simply a data point represented as a list of numbers (a vector). **Binary Classification** is the process of separating these data points into exactly two distinct groups, typically tagged with target labels like $+1$ (positive class) and $-1$ (negative class).

### **Mathematical Formulation**
* A pattern is an element belonging to the real coordinate space $\mathbb{R}^n$, where $n$ represents the number of measurable features.
* Let $m_1$ be the number of patterns belonging to the positive class (label $+1$).
* Let $m_2$ be the number of patterns belonging to the negative class (label $-1$).

We stack these individual patterns into data matrices:
* $[A^+]_{m_1 \times n}$: The collection matrix of all $m_1$ patterns with label $+1$.
* $[A^-]_{m_2 \times n}$: The collection matrix of all $m_2$ patterns with label $-1$.

---

## 2. Concept: Linear vs. Non-Linear Separability

### **Simple Meaning**
* **Linearly Separable:** Two groups of data points are linearly separable if you can draw a perfectly straight line (in 2D), a flat plane (in 3D), or a flat surface called a **hyperplane** (in higher dimensions) that completely cuts between them without a single mistake.
* **Non-Linearly Separable:** If the data points are mixed together or wrapped around each other such that no straight line can cleanly divide them, they require a curved decision boundary ($f(x) = 0$).

### **Mathematical Conditions**
Two sets $A^+$ and $A^-$ are **linearly separable** if there exists a hyperplane defined by a weight vector $w \in \mathbb{R}^n$ and a scalar bias $b \in \mathbb{R}$ such that:

$$A^+ w > eb \quad \text{and} \quad A^- w < eb$$

Where $e$ is a column vector consisting entirely of ones ($[1, 1, \dots, 1]^T$), which scales the scalar bias $b$ to match the matrix dimensions.

---

## 3. Core Example Breakdown (From Hand-written Notes)

### **Problem Statement**
Consider a dataset in a 2D space ($\mathbb{R}^2$, meaning $n=2$ features):
* Positive Class: $A^+ = \{(1,1), (1,2), (2,1), (3,2), (4,1)\}$
* Negative Class: $A^- = \{(6,2), (2,6), (7,1), (7,3)\}$

**Goal:** Test if the separating line $x + y = 6$ successfully separates these two sets.

---

### **Step-by-Step Matrix Calculation**

To align with the hyperplane equation $w^T x = b$, we rewrite $x + y = 6$ into vector notation:
* Weight vector: $w = \begin{bmatrix} 1 \\ 1 \end{bmatrix}$
* Bias: $b = 6$

#### **Step 3.1: Evaluate the Positive Class $A^+$**
We multiply the data matrix $[A^+]_{5 \times 2}$ by the weight vector $w$:

$$A^+ w = \begin{bmatrix} 1 & 1 \\ 1 & 2 \\ 2 & 1 \\ 3 & 2 \\ 4 & 1 \end{bmatrix} \begin{bmatrix} 1 \\ 1 \end{bmatrix} = \begin{bmatrix} 1(1) + 1(1) \\ 1(1) + 2(1) \\ 2(1) + 1(1) \\ 3(1) + 2(1) \\ 4(1) + 1(1) \end{bmatrix} = \begin{bmatrix} 2 \\ 3 \\ 3 \\ 5 \\ 5 \end{bmatrix}$$

**Verification:** Every calculated value in the resulting vector must be less than or equal to the boundary value $6$. 
$$\begin{bmatrix} 2 \\ 3 \\ 3 \\ 5 \\ 5 \end{bmatrix} \le 6 \begin{bmatrix} 1 \\ 1 \\ 1 \\ 1 \\ 1 \end{bmatrix} \quad \color{green}\checkmark \text{ (True)}$$

#### **Step 3.2: Evaluate the Negative Class $A^-$**
We multiply the data matrix $[A^-]_{4 \times 2}$ by the weight vector $w$:

$$A^- w = \begin{bmatrix} 6 & 2 \\ 2 & 6 \\ 7 & 1 \\ 7 & 3 \end{bmatrix} \begin{bmatrix} 1 \\ 1 \end{bmatrix} = \begin{bmatrix} 6(1) + 2(1) \\ 2(1) + 6(1) \\ 7(1) + 1(1) \\ 7(1) + 3(1) \end{bmatrix} = \begin{bmatrix} 8 \\ 8 \\ 8 \\ 10 \end{bmatrix}$$

**Verification:** Every calculated value in the resulting vector must be greater than or equal to the boundary value $6$.
$$\begin{bmatrix} 8 \\ 8 \\ 8 \\ 10 \end{bmatrix} \ge 6 \begin{bmatrix} 1 \\ 1 \\ 1 \\ 1 \end{bmatrix} \quad \color{green}\checkmark \text{ (True)}$$

**Conclusion:** The boundary line successfully separates the two classes.

---

## 4. Concept: Convex Hulls & Geometric Separability Theorem

### **Theorem (Mangasarian)**
> Two finite sets $A$ and $B$ in $\mathbb{R}^n$ are **linearly separable** if and only if their **convex hulls do not overlap** (i.e., their convex hulls are disjoint).

* **Convex Hull:** Think of stretching a rubber band around the outermost points of a data set. The entire region enclosed inside that rubber band is the convex hull.

### **Counter-Example Breakdown (Non-Separable)**
Let two sets be defined as:
* $A^+ = \{(-1,0), (0,1), (1,0)\}$ (Forms a blue triangle pointing up)
* $A^- = \{(0,0), (1,1), (0,2)\}$ (Forms a purple triangle pointing down)


```

y
▲
2 ┼      (0,2) [A-]
│       ┃  ╲
1 ┼      (0,1)  ╲   (1,1) [A-]
│    ╱  ┃  ╳  ╱ ┃
0 ┼──(1,0)┃────(1,0)───► x
╱     ┃
-1 ┼ (-1,0) [A+]

```

**Why they are NOT separable:** 
As seen in the geometric intersection diagram, the two shapes cross paths. Because the triangular regions wrap inside each other, you cannot slide a straight line between them without slicing through the shapes. Their convex hulls are **not disjoint**, making them completely non-linearly separable.

---

## 5. Visualizing Geometric Separability States (Graph Concepts)

### Linearly Separable vs. Non-Linearly Separable Configurations



```
Linearly Separable                    Non-Linearly Separable
      y                                         y
      ▲                                         ▲
      │   □   □   /                             │   □    ●    □
      │     □    /  ●                           │     ●   □   ●
      │   □     / ●   ●                         │   □    ●    □
      │        /   ●                            │
      └───────────► x                           └───────────► x
 A straight line splits                    Data requires a curve 
   the groups cleanly                         to separate them

```

# Support Vector Machines: Canonical Scaling of Separating Hyperplanes

---

## 1. Concept: Scaling of Hyperplane Inequalities

### **Simple Meaning**
When we want to separate two groups of points using a straight boundary (a hyperplane), the basic math states that one group must evaluate to a value greater than a threshold, and the other group must evaluate to a value less than that threshold. 

However, because you can multiply both sides of a strict inequality by any positive number, there are infinite ways to write the exact same boundary line. To fix this and make optimization calculations easier, we "scale" the equations so that the closest points to the boundary evaluate to exactly $+1$ and $-1$. This standard form is known as the **Canonical Representation** of the hyperplane.

### **Mathematical Formulation**
The strict geometric separation inequalities:
$$A^+ w > eb \quad \text{and} \quad A^- w < eb$$

Can be rewritten through suitable scaling into canonical form as:
$$A^+ w^* \ge b^*e + e$$
$$A^- w^* \le b^*e - e$$

Where $e$ is a vector of ones ($[1, 1, \dots, 1]^T$) used to ensure matrix dimensions match.

---

## 2. Step-by-Step Mathematical Derivation

Let us walk through how strict inequalities translate into the scaled canonical version using the minimum margin variables.

### **Step 2.1: Introduce Margin Slack Variables ($\alpha_i, \beta_j$)**
Since the inequalities are strict ($>$ and $<$), there must be some positive gap between the data points and the boundary. We can define the individual distances for each point:
* For the positive class: $A^+ w \ge eb + \alpha_i e \quad (\alpha_i > 0 \text{ for all } i)$
* For the negative class: $A^- w \le eb - \beta_j e \quad (\beta_j > 0 \text{ for all } j)$

### **Step 2.2: Find the Minimum Distances ($\alpha^*, \beta^*$)**
To find a single scaling value that safely satisfies all points at once, we find the closest positive and negative points to the boundary:
$$\alpha^* = \min_i \{\alpha_i\} \implies \alpha^* \le \alpha_i \quad \forall i$$
$$\beta^* = \min_j \{\beta_j\} \implies \beta^* \le \beta_j \quad \forall j$$

Substituting these minimum constraints transforms our inequalities into:
$$A^+ w \ge eb + \alpha^* e \implies A^+ w \ge (b + \alpha^*)e$$
$$A^- w \le eb - \beta^* e \implies A^- w \le (b - \beta^*)e$$

### **Step 2.3: Scale Using the Universal Margin ($\gamma$)**
Let $\gamma$ be the absolute minimum distance among all points from both classes:
$$\gamma = \min\{\alpha^*, \beta^*\} \implies \gamma \le \alpha^* \text{ and } \gamma \le \beta^*$$

This gives us the standard margin bounded inequalities:
$$A^+ w \ge be + \gamma e$$
$$A^- w \le be - \gamma e$$

### **Step 2.4: Divide by $\gamma$ to Normalise**
Divide every term in both inequalities by $\gamma$ (since $\gamma > 0$, the inequality directions do not change):
$$\frac{A^+ w}{\gamma} \ge \frac{be}{\gamma} + e \implies A^+\left(\frac{w}{\gamma}\right) \ge \left(\frac{b}{\gamma}\right)e + e$$
$$\frac{A^- w}{\gamma} \le \frac{be}{\gamma} - e \implies A^-\left(\frac{w}{\gamma}\right) \le \left(\frac{b}{\gamma}\right)e - e$$

By defining our newly scaled canonical weights and biases as $w^* = \frac{w}{\gamma}$ and $b^* = \frac{b}{\gamma}$, we achieve the final canonical form:
$$A^+ w^* \ge b^*e + e$$
$$A^- w^* \le b^*e - e$$

---

## 3. Practical Core Problems with Solutions

### **Problem 1: Verifying Non-Linear Separability Geometric Bounds**
**Scenario:** Consider the dataset shown in the image:
* Positive Class: $A^+ = \{(-1, 0), (1, 0), (0, 1)\}$
* Negative Class: $A^- = \{(0, 0), (1, 1), (0, 2)\}$

**Question:** Prove mathematically that a single linear hyperplane cannot separate these two datasets (i.e., they are not linearly separable).

#### **Step-by-Step Proof Calculation:**
1. **Set up the Linear Separation Conditions:**
   For a line to separate these two groups, there must exist a weight vector $w = \begin{bmatrix} w_1 \\ w_2 \end{bmatrix}$ and a bias $b$ such that:
   * For all $x \in A^+$: $w_1x_1 + w_2x_2 > b$
   * For all $x \in A^-$: $w_1x_1 + w_2x_2 < b$

2. **Evaluate the conditions for the Positive Points ($A^+$):**
   * Point $(-1, 0) \implies -w_1 + 0 > b \implies -w_1 > b$
   * Point $(1, 0) \implies w_1 + 0 > b \implies w_1 > b$
   * Point $(0, 1) \implies 0 + w_2 > b \implies w_2 > b$

3. **Evaluate the conditions for the Negative Points ($A^-$):**
   * Point $(0, 0) \implies 0 + 0 < b \implies b > 0$
   * Point $(1, 1) \implies w_1 + w_2 < b$
   * Point $(0, 2) \implies 2w_2 < b$

4. **Identify the Contradiction:**
   From the positive class evaluation, we have $-w_1 > b$ and $w_1 > b$.
   If we add these two inequalities together:
   $$(-w_1) + (w_1) > b + b \implies 0 > 2b \implies b < 0$$
   
   However, from the negative class evaluation point $(0,0)$, we established that:
   $$b > 0$$

5. **Conclusion:**
   A value for $b$ cannot be simultaneously greater than 0 and less than 0 ($0 < b < 0$ is impossible). Because this system of linear equations yields a logical contradiction, no such separating line exists. Therefore, the datasets are **not linearly separable**.

---

### **Problem 2: Canonical Rescaling Calculation**
**Scenario:** A separating line between two 1D clusters is given by $2x > 8$ for class $+1$ and $2x < 8$ for class $-1$. The closest point in the positive class is at $x = 6$, and the closest point in the negative class is at $x = 2$. Find the canonical weights $w^*$ and bias $b^*$.

#### **Step-by-Step Solution:**
1. **Identify parameters from standard inequality format ($w \cdot x - b > 0$):**
   $$2x - 8 > 0 \implies w = 2, \quad b = 8$$

2. **Calculate the margin slacks ($\alpha^*, \beta^*$) using the closest boundary points:**
   * Positive slack: $\alpha^* = w(x_{pos}) - b = 2(6) - 8 = 12 - 8 = 4$
   * Negative slack: $\beta^* = b - w(x_{neg}) = 8 - 2(2) = 8 - 4 = 4$

3. **Identify the universal margin value ($\gamma$):**
   $$\gamma = \min\{\alpha^*, \beta^*\} = \min\{4, 4\} = 4$$

4. **Calculate canonical scaled parameters ($w^*, b^*$):**
   * $$w^* = \frac{w}{\gamma} = \frac{2}{4} = 0.5$$
   * $$b^* = \frac{b}{\gamma} = \frac{8}{4} = 2$$

**Final Canonical Form:** $0.5x \ge 2 + 1$ (for positive class closest point: $0.5(6) = 3 \ge 3$) and $0.5x \le 2 - 1$ (for negative class closest point: $0.5(2) = 1 \le 1$).

---

## 4. Visualizing Overlapping Convex Hulls (Graph Concept)

This graph visualizes the non-linearly separable example from the image. Notice the shaded conflict zone where the two triangles cross paths, which makes straight-line separation impossible:


```
y
  ▲
2.0 ┼ (0,2) [A-]
    │  ┃ ╲
1.5 ┼  ┃   ╲
    │  ┃     ╲
1.0 ┼ (0,1)───(1,1) [A-]
    │  ┃▒▒▒▒╱  ┃
0.5 ┼  ┃▒▒╱    ┃  ◀─── [▒▒] Shaded area is the overlapping 
    │  ┃╱      ┃       convex hull conflict zone.
0.0 ┼─(0,0)───(1,0)──► x
   ╱  [A-]     [A+]
-1.0  (-1,0) [A+]

```