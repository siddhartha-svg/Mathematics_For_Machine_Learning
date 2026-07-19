# Probability Theory: Random Vectors & Joint Distributions

---

## 1. Concept: Random Vectors
### **Simple Meaning**
When we track more than one outcome at the same time (like measuring both the height *and* weight of a person, or counting red *and* blue balls drawn from a box), we group these individual random variables together into a single column format. This ordered list or column group is called a **Random Vector**.

### **Mathematical Formulation**
Let $X_1, X_2, \dots, X_n$ be $n$ random variables. Then, the random vector $X$ is defined as a column vector by taking the transpose ($T$) of a row row vector:

$$X = \begin{bmatrix} X_1 & X_2 & \dots & X_n \end{bmatrix}^T = \begin{bmatrix} X_1 \\ X_2 \\ \vdots \\ X_n \end{bmatrix}$$

---

## 2. Concept: Joint Probability Distributions
### **Simple Meaning**
Instead of looking at the probability of an event happening for just one variable, a **Joint Distribution** calculates the probability that multiple random variables simultaneously take on specific values. 

### **Mathematical Formulation**
The joint distribution of the random vector $X$ is defined as:

$$f_X(x_1, x_2, \dots, x_n) = P[X_1 = x_1, X_2 = x_2, \dots, X_n = x_n]$$

*   **Joint PMF (Probability Mass Function):** Used when the random variables are **discrete** (countable values like integers).
*   **Joint PDF (Probability Density Function):** Used when the random variables are **continuous** (infinite measurable values like time, height).

---

## 3. Core Example Breakdown (From Images)

### **Problem Statement**
An urn contains **6 Red balls**, **5 Blue balls**, and **3 Green balls**. 
* Total balls = $6 + 5 + 3 = 14$.
* Total balls drawn at random = **4 balls**.
* Let $X$ = number of Red balls drawn.
* Let $Y$ = number of Blue balls drawn.

**Goal:** Determine the marginal PMF of $X$, the marginal PMF of $Y$, and the joint PMF of $(X, Y)$.

---

### **Step-by-Step Calculations**

#### **Step 3.1: Total Possible Outcomes (Denominator)**
No matter which balls we choose, the total number of ways to pick 4 balls out of 14 is given by combinations:
$$\text{Total Ways} = \binom{14}{4} = \frac{14 \times 13 \times 12 \times 11}{4 \times 3 \times 2 \times 1} = 1001$$

#### **Step 3.2: Marginal PMF of $X$ (Red Balls)**
* $X$ can take values from $0$ to $4$.
* For a given $X = x$, we choose $x$ balls from the 6 Red balls, and the remaining $(4 - x)$ balls from the other 8 non-red balls (5 Blue + 3 Green).

| $X$ Value ($x$) | Combination Formula | Calculation | Probability $P(X = x)$ |
| :---: | :---: | :---: | :---: |
| **0** | $\frac{\binom{6}{0}\binom{8}{4}}{\binom{14}{4}}$ | $\frac{1 \times 70}{1001}$ | $\frac{70}{1001} \approx 0.0699$ |
| **1** | $\frac{\binom{6}{1}\binom{8}{3}}{\binom{14}{4}}$ | $\frac{6 \times 56}{1001}$ | $\frac{336}{1001} \approx 0.3357$ |
| **2** | $\frac{\binom{6}{2}\binom{8}{2}}{\binom{14}{4}}$ | $\frac{15 \times 28}{1001}$ | $\frac{420}{1001} \approx 0.4196$ |
| **3** | $\frac{\binom{6}{3}\binom{8}{1}}{\binom{14}{4}}$ | $\frac{20 \times 8}{1001}$ | $\frac{160}{1001} \approx 0.1598$ |
| **4** | $\frac{\binom{6}{4}\binom{8}{0}}{\binom{14}{4}}$ | $\frac{15 \times 1}{1001}$ | $\frac{15}{1001} \approx 0.0150$ |

#### **Step 3.3: Marginal PMF of $Y$ (Blue Balls)**
* $Y$ can take values from $0$ to $4$.
* For a given $Y = y$, we choose $y$ balls from the 5 Blue balls, and the remaining $(4 - y)$ balls from the other 9 non-blue balls (6 Red + 3 Green).

| $Y$ Value ($y$) | Combination Formula | Calculation | Probability $P(Y = y)$ |
| :---: | :---: | :---: | :---: |
| **0** | $\frac{\binom{5}{0}\binom{9}{4}}{\binom{14}{4}}$ | $\frac{1 \times 126}{1001}$ | $\frac{126}{1001} \approx 0.1259$ |
| **1** | $\frac{\binom{5}{1}\binom{9}{3}}{\binom{14}{4}}$ | $\frac{5 \times 84}{1001}$ | $\frac{420}{1001} \approx 0.4196$ |
| **2** | $\frac{\binom{5}{2}\binom{9}{2}}{\binom{14}{4}}$ | $\frac{10 \times 36}{1001}$ | $\frac{360}{1001} \approx 0.3596$ |
| **3** | $\frac{\binom{5}{3}\binom{9}{1}}{\binom{14}{4}}$ | $\frac{10 \times 9}{1001}$ | $\frac{90}{1001} \approx 0.0899$ |
| **4** | $\frac{\binom{5}{4}\binom{9}{0}}{\binom{14}{4}}$ | $\frac{5 \times 1}{1001}$ | $\frac{5}{1001} \approx 0.0050$ |

#### **Step 3.4: Joint PMF Formula of $(X, Y)$**
To find the probability that *simultaneously* $X=x$ and $Y=y$, the remaining selection must consist of Green balls: $4 - (x + y)$.

$$f_{XY}(x,y) = P(X=x, Y=y) = \frac{\binom{6}{x} \binom{5}{y} \binom{3}{4-(x+y)}}{\binom{14}{4}}$$

**Domain Constraints:**
*   $0 \le x \le 4$, $0 \le y \le 4$
*   Total balls selected cannot exceed 4: $x + y \le 4$
*   Because there are only 3 Green balls, the remaining number of balls cannot exceed 3:  
    $$4 - (x + y) \le 3 \implies x + y \ge 1$$

---

### **Visualizing the Distribution Spaces**

Below is a representation of the sample distribution layout where structural constraints apply.


```
   Y (Blue Balls)
   [4]   [•]   [x]   [x]   [x]
   [3]   [•]   [•]   [x]   [x]
   [2]   [•]   [•]   [•]   [x]
   [1]   [•]   [•]   [•]   [•]
   [0]   [x]   [•]   [•]   [•]   [•]
         [0]   [1]   [2]   [3]   [4]   X (Red Balls)

```

Legend:
[•] Valid Joint Probability Combinations
[x] Invalid Combinations (Breaks constraints like x+y > 4 or x+y < 1)



---

## 4. Practice Problem with Solution

### **Problem Statement**
A committee of **3 people** is to be selected from a pool of **4 Mathematicians, 3 Statisticians, and 2 Computer Scientists**.
* Let $X$ = number of Mathematicians chosen.
* Let $Y$ = number of Statisticians chosen.
* Total Group size = $4 + 3 + 2 = 9$.

Find the explicit Joint PMF value for $P(X=1, Y=1)$.

### **Step-by-Step Calculation**

**Step 1: Calculate total possible committee combinations**
$$\text{Total Ways} = \binom{9}{3} = \frac{9 \times 8 \times 7}{3 \times 2 \times 1} = 84$$

**Step 2: Calculate the required remaining members**
If 1 Mathematician ($X=1$) and 1 Statistician ($Y=1$) are selected, the remaining $3 - (1 + 1) = 1$ member must be a Computer Scientist.

**Step 3: Compute the joint combination ways**
* Ways to choose Mathematicians: $\binom{4}{1} = 4$
* Ways to choose Statisticians: $\binom{3}{1} = 3$
* Ways to choose Computer Scientists: $\binom{2}{1} = 2$

$$\text{Favorable Outcomes} = \binom{4}{1} \times \binom{3}{1} \times \binom{2}{1} = 4 \times 3 \times 2 = 24$$

**Step 4: Compute the final joint probability**
$$P(X=1, Y=1) = \frac{24}{84} = \frac{2}{7} \approx 0.2857$$


# Probability Theory: Marginal Distributions

---

## 1. Concept: Marginal Distributions

### **Simple Meaning**
When you have a joint probability distribution tracking two variables ($X$ and $Y$) simultaneously, the **Marginal Distribution** allows you to look at just *one* of those variables in isolation. 

Think of it as looking at a two-way data table: if you want the total probability of just $X$, you collapse or "sum out" all the rows for $Y$. 

### **Mathematical Formulation**
For a bi-variate random vector $W = (X, Y)$ with joint probability distribution $f(x, y)$, the marginal distribution of $X$ is obtained by eliminating $Y$:

$$f_X(x) = \begin{cases} \sum_{Y} f(x, y) & \text{if } (X, Y) \text{ is discrete} \\ \int_{Y} f(x, y) \, dy & \text{if } (X, Y) \text{ is continuous} \end{cases}$$

Similarly, the marginal distribution of $Y$ is obtained by eliminating $X$:

$$f_Y(y) = \begin{cases} \sum_{X} f(x, y) & \text{if } (X, Y) \text{ is discrete} \\ \int_{X} f(x, y) \, dx & \text{if } (X, Y) \text{ is continuous} \end{cases}$$

---

## 2. Core Example Breakdown (From Images)

### **Problem Statement**
Consider the continuous joint probability density function (pdf) of a bi-variate random vector $(X, Y)$ defined as:

$$f(x, y) = \begin{cases} 6xy^2, & 0 < x < 1, \; 0 < y < 1 \\ 0, & \text{elsewhere} \end{cases}$$

**Goal:** Determine the marginal distributions of $X$ and $Y$.

---

### **Step-by-Step Calculations**

#### **Step 2.1: Verification of Joint PDF (Optional Verification)**
To check if the function is a valid total probability distribution, we integrate over the complete space to see if it equals $1$:

$$\int_{-\infty}^{\infty} \int_{-\infty}^{\infty} f(x,y) \, dy \, dx = \int_{x=0}^{1} \int_{y=0}^{1} 6xy^2 \, dy \, dx$$

1. **Integrate with respect to $y$ first:**
   $$\int_{0}^{1} 6xy^2 \, dy = \left[ 6x \left( \frac{y^3}{3} \right) \right]_{0}^{1} = 6x \left( \frac{1}{3} - 0 \right) = 2x$$

2. **Integrate the result with respect to $x$:**
   $$\int_{0}^{1} 2x \, dx = \left[ 2 \left( \frac{x^2}{2} \right) \right]_{0}^{1} = \left[ x^2 \right]_{0}^{1} = 1 - 0 = 1$$

---

#### **Step 2.2: Finding the Marginal Distribution of $X$**
To isolate $X$, integrate out $y$ over its defined limits ($0$ to $1$):

$$f_X(x) = \int_{y=0}^{1} f(x, y) \, dy = \int_{0}^{1} 6xy^2 \, dy$$

1. **Perform Integration:**
   $$f_X(x) = \left[ 6x \left(\frac{y^3}{3}\right) \right]_{0}^{1}$$

2. **Substitute Boundaries ($y=1$ and $y=0$):**
   $$f_X(x) = 6x \left( \frac{1^3}{3} - \frac{0^3}{3} \right) = 6x \left(\frac{1}{3}\right) = 2x$$

**Final Marginal PDF for $X$:**
$$f_X(x) = 2x, \quad 0 < x < 1$$

---

#### **Step 2.3: Finding the Marginal Distribution of $Y$**
To isolate $Y$, integrate out $x$ over its defined limits ($0$ to $1$):

$$f_Y(y) = \int_{x=0}^{1} f(x, y) \, dx = \int_{0}^{1} 6xy^2 \, dx$$

1. **Perform Integration:**
   $$f_Y(y) = \left[ 6\left(\frac{x^2}{2}\right)y^2 \right]_{0}^{1}$$

2. **Substitute Boundaries ($x=1$ and $x=0$):**
   $$f_Y(y) = 6\left(\frac{1^2}{2}\right)y^2 - 0 = 3y^2$$

**Final Marginal PDF for $Y$:**
$$f_Y(y) = 3y^2, \quad 0 < y < 1$$

---

## 3. Practice Problem with Solution

### **Problem Statement**
Let a joint PDF of continuous variables $X$ and $Y$ be defined as:
$$f(x, y) = \begin{cases} 2x + 2y, & 0 < x < 1, \; 0 < y < 0.5 \\ 0, & \text{elsewhere} \end{cases}$$

Find the marginal PDF $f_X(x)$.

### **Step-by-Step Calculation**

**Step 1: Set up the marginal integral bounds for $y$**
$$f_X(x) = \int_{0}^{0.5} (2x + 2y) \, dy$$

**Step 2: Integrate term-by-term with respect to $y$**
$$f_X(x) = \left[ 2xy + y^2 \right]_{0}^{0.5}$$

**Step 3: Evaluate at upper bound ($y = 0.5$) and lower bound ($y = 0$)**
$$f_X(x) = \left( 2x(0.5) + (0.5)^2 \right) - \left( 2x(0) + (0)^2 \right)$$
$$f_X(x) = 1x + 0.25$$

**Final Answer:**
$$f_X(x) = x + 0.25, \quad 0 < x < 1$$

---

## 4. Visualizing Bounds (Integration Region Graph)

The integration domain for the core example ($0 < x < 1$ and $0 < y < 1$) forms a perfectly bound square workspace region:


```

y
▲
1 ┼───────────────┐ ◄─── Integrating along this horizontal slice
│               │      yields the marginal distribution of Y: f_Y(y)
│   f(x,y)      │
│   = 6xy²      │
│               │ ◄─── Integrating along this vertical slice
│               │      yields the marginal distribution of X: f_X(x)
0 └───────────────┴───► x
0               1

```


# Probability Theory: Covariance and its Properties

---

## 1. Concept: Covariance

### **Simple Meaning**
**Covariance** measures how two random variables change together. 
* If one variable goes up when the other goes up, they have a **positive relationship**.
* If one variable goes down when the other goes up, they have a **negative relationship**.
* If there is no consistent relationship, the covariance is close to **zero**.

In simple terms, it tracks the joint linear trend of two variables relative to their respective averages.

### **Mathematical Formulation**
For two random variables $X$ and $Y$:
$$\text{Cov}(X, Y) = E[(X - E[X])(Y - E[Y])] = E[XY] - E[X]E[Y]$$

---

### **Step-by-Step Algebraic Derivation**
Let us use the shorthand notation $\bar{X} = E[X]$ and $\bar{Y} = E[Y]$ where means behave as constant numbers.

1. **Start with the definition:**
   $$\text{Cov}(X,Y) = E[(X - \bar{X})(Y - \bar{Y})]$$

2. **Expand the binomial terms inside the expectation:**
   $$(X - \bar{X})(Y - \bar{Y}) = XY - \bar{Y}X - \bar{X}Y + \bar{X}\bar{Y}$$

3. **Apply the Linearity of Expectation property ($E[A+B] = E[A] + E[B]$):**
   $$E[XY - \bar{Y}X - \bar{X}Y + \bar{X}\bar{Y}] = E[XY] - \bar{Y}E[X] - \bar{X}E[Y] + \bar{X}\bar{Y}E[1]$$
   *(Note: $\bar{X}$ and $\bar{Y}$ factor out of expectations because they are constants, and $E[1] = 1$)*.

4. **Substitute $E[X] = \bar{X}$ and $E[Y] = \bar{Y}$ back in:**
   $$\text{Cov}(X,Y) = E[XY] - \bar{Y}\bar{X} - \bar{X}\bar{Y} + \bar{X}\bar{Y}$$

5. **Cancel out opposing terms:**
   $$\text{Cov}(X,Y) = E[XY] - \bar{X}\bar{Y}$$

6. **Final Form:**
   $$\text{Cov}(X, Y) = E[XY] - E[X]E[Y]$$

---

## 2. Concept: Properties of Covariance

### **Property 1: Relationship to Variance**
The covariance of a variable with itself is its variance:
$$V[X] = \text{Cov}(X, X)$$

### **Property 2: Bilinearity**
Covariance scales and splits linearly across sums for any random variables $X, Y, Z$ and constants $a, b$:
*   $\text{Cov}(aX + bY, Z) = a\text{Cov}(X, Z) + b\text{Cov}(Y, Z)$
*   $\text{Cov}(X, aY + bZ) = a\text{Cov}(X, Y) + b\text{Cov}(X, Z)$

---

### **Step-by-Step Proof of Bilinearity**
Let $\bar{X} = E[X]$, $\bar{Y} = E[Y]$, and $\bar{Z} = E[Z]$.

1. **Write out the definition:**
   $$\text{Cov}(aX + bY, Z) = E\left[ \Big((aX + bY) - (a\bar{X} + b\bar{Y})\Big)(Z - \bar{Z}) \right]$$

2. **Group matching constant coefficients ($a$ and $b$):**
   $$= E\left[ \Big(a(X - \bar{X}) + b(Y - \bar{Y})\Big)(Z - \bar{Z}) \right]$$

3. **Distribute the $(Z - \bar{Z})$ term:**
   $$= E\left[ a(X - \bar{X})(Z - \bar{Z}) + b(Y - \bar{Y})(Z - \bar{Z}) \right]$$

4. **Apply linearity of expectation:**
   $$= aE[(X - \bar{X})(Z - \bar{Z})] + bE[(Y - \bar{Y})(Z - \bar{Z})]$$

5. **Convert back into covariance definitions:**
   $$= a\text{Cov}(X, Z) + b\text{Cov}(Y, Z)$$

---

## 3. Different Problems with Solutions

### **Problem 1: Calculating Covariance from Discrete Joint Events**
Two fair coins are flipped. Let $X = 1$ if the first coin is heads (else $0$), and let $Y$ equal the total number of heads across both coins. Find $\text{Cov}(X, Y)$.

#### **Step-by-Step Solution:**
*   **Sample space:** $\{HH, HT, TH, TT\}$ (each with probability $0.25$).
*   Values map as:
    *   $HH \implies X=1, Y=2 \implies XY = 2$
    *   $HT \implies X=1, Y=1 \implies XY = 1$
    *   $TH \implies X=0, Y=1 \implies XY = 0$
    *   $TT \implies X=0, Y=0 \implies XY = 0$

1. **Calculate $E[X]$:**
   $$E[X] = (1 \times 0.25) + (1 \times 0.25) + (0 \times 0.25) + (0 \times 0.25) = 0.5$$

2. **Calculate $E[Y]$:**
   $$E[Y] = (2 \times 0.25) + (1 \times 0.25) + (1 \times 0.25) + (0 \times 0.25) = 1.0$$

3. **Calculate $E[XY]$:**
   $$E[XY] = (2 \times 0.25) + (1 \times 0.25) + (0 \times 0.25) + (0 \times 0.25) = 0.75$$

4. **Apply the Covariance formula:**
   $$\text{Cov}(X, Y) = E[XY] - E[X]E[Y] = 0.75 - (0.5 \times 1.0) = 0.25$$

---

### **Problem 2: Applying Covariance Properties**
Given that $\text{Cov}(X, Z) = 3$ and $\text{Cov}(Y, Z) = -2$, compute the value of $\text{Cov}(4X - 2Y, Z)$.

#### **Step-by-Step Solution:**
1. **Apply the bilinearity property to separate the expression:**
   $$\text{Cov}(4X - 2Y, Z) = 4\text{Cov}(X, Z) - 2\text{Cov}(Y, Z)$$

2. **Substitute the given baseline values:**
   $$= 4(3) - 2(-2)$$

3. **Calculate the final arithmetic result:**
   $$= 12 + 4 = 16$$

---

## 4. Visualizing Linear Relationships (Graph Concept)

This text diagram reflects how the direction of covariance relates visually to the layout of points on an axis system:

```
Positive Covariance (>0)          Negative Covariance (<0)
      y                                 y
      ▲                                 ▲
      │       *                         │  *
      │     *                           │    *
      │   *                             │      *
      │ *                               │        *
      └───────────► x                   └───────────► x
Variables move together           Variables move inversely
```



# Probability Theory: Continuous Covariance & Marginal Integration

---

## 1. Concept: Continuous Covariance over a Bounded Region

### **Simple Meaning**
When random variables $X$ and $Y$ are continuous, finding their relationship (covariance) requires multi-variable integration instead of simple summations. If their values depend on a constraint like $x + y < 1$, the region forms a triangle rather than a perfect square. This boundary links the variables together, meaning their limits change depending on each other during integration steps.

### **Mathematical Formulation**
To calculate the covariance of continuous random variables $X$ and $Y$:
$$\text{Cov}(X, Y) = E[XY] - E[X]E[Y]$$

Where the expected values are computed via calculus integrations:
*   $$E[XY] = \int_{-\infty}^{\infty} \int_{-\infty}^{\infty} xy \cdot f(x,y) \, dx \, dy$$
*   $$E[X] = \int_{-\infty}^{\infty} x \cdot f_X(x) \, dx$$
*   $$E[Y] = \int_{-\infty}^{\infty} y \cdot f_Y(y) \, dy$$

---

## 2. Core Example Breakdown (From Images)

### **Problem Statement**
Find the covariance of the random variables $X$ and $Y$ whose joint PDF is given by:
$$f(x,y) = \begin{cases} 2; & x > 0, \; y > 0, \; x + y < 1 \\ 0; & \text{elsewhere} \end{cases}$$

---

### **Step-by-Step Calculations**

#### **Step 2.1: Finding the Expected Value $E[XY]$**
Because $x + y < 1$, the inner integration limits for $x$ run from $0$ up to $1 - y$, while the outer limits for $y$ run from $0$ to $1$:

$$E[XY] = \int_{y=0}^{1} \int_{x=0}^{1-y} 2xy \, dx \, dy$$

1. **Integrate with respect to $x$ first**:
   $$\int_{0}^{1-y} 2xy \, dx = 2y \left[ \frac{x^2}{2} \right]_{0}^{1-y} = y(1-y)^2$$

2. **Expand the expression before integrating with respect to $y$**:
   $$y(1 - 2y + y^2) = y - 2y^2 + y^3$$

3. **Integrate with respect to $y$ from 0 to 1**:
   $$\int_{0}^{1} (y - 2y^2 + y^3) \, dy = \left[ \frac{y^2}{2} - \frac{2y^3}{3} + \frac{y^4}{4} \right]_{0}^{1} = \frac{1}{2} - \frac{2}{3} + \frac{1}{4}$$

4. **Find a common denominator (12) to calculate the fraction**:
   $$E[XY] = \frac{6 - 8 + 3}{12} = \frac{1}{12}$$

---

#### **Step 2.2: Finding Marginal Distributions $f_X(x)$ and $f_Y(y)$**
To find the individual profiles for each variable, integrate out the opposing variable over the triangle boundary.

*   **Marginal PDF of $X$** ($y$ ranges from $0$ to $1-x$):
    $$f_X(x) = \int_{0}^{1-x} 2 \, dy = 2(1-x), \quad 0 < x < 1$$

*   **Marginal PDF of $Y$** ($x$ ranges from $0$ to $1-y$):
    $$f_Y(y) = \int_{0}^{1-y} 2 \, dx = 2(1-y), \quad 0 < y < 1$$

---

#### **Step 2.3: Finding the Individual Expectations $E[X]$ and $E[Y]$**
1. **Compute $E[X]$**:
   $$E[X] = \int_{0}^{1} x \cdot 2(1-x) \, dx = \int_{0}^{1} (2x - 2x^2) \, dx$$
   $$E[X] = \left[ x^2 - \frac{2x^3}{3} \right]_{0}^{1} = 1 - \frac{2}{3} = \frac{1}{3}$$

2. **Compute $E[Y]$** (by symmetry of the matching PDFs, $E[Y]$ is identical to $E[X]$):
   $$E[Y] = \frac{1}{3}$$

---

#### **Step 2.4: Calculate Final Covariance**
Using the values computed above ($E[XY] = \frac{1}{12}$, $E[X] = \frac{1}{3}$, $E[Y] = \frac{1}{3}$):

$$\text{Cov}(X, Y) = \frac{1}{12} - \left(\frac{1}{3} \times \frac{1}{3}\right) = \frac{1}{12} - \frac{1}{9}$$

Factoring out $\frac{1}{3}$ to simplify:
$$\text{Cov}(X, Y) = \frac{1}{3}\left(\frac{1}{4} - \frac{1}{3}\right) = \frac{1}{3}\left(-\frac{1}{12}\right) = -\frac{1}{36}$$

---

## 3. Practice Problem with Solution

### **Problem Statement**
Let a joint PDF over a symmetric triangular domain be defined as:
$$f(x,y) = \begin{cases} 8xy, & 0 < x < 1, \; 0 < y < 1, \; x+y < 1 \\ 0, & \text{elsewhere} \end{cases}$$
*(Note: Assume the normalized expected value parameters yield $E[X] = \frac{2}{5}$, $E[Y] = \frac{2}{5}$).*

Find $E[XY]$ and determine the final covariance.

### **Step-by-Step Calculation**

**Step 1: Set up the integral for $E[XY]$**
$$E[XY] = \int_{0}^{1} \int_{0}^{1-y} (xy) \cdot (8xy) \, dx \, dy = \int_{0}^{1} \int_{0}^{1-y} 8x^2y^2 \, dx \, dy$$

**Step 2: Integrate with respect to $x$**
$$\int_{0}^{1-y} 8x^2y^2 \, dx = \left[ \frac{8}{3}x^3y^2 \right]_{0}^{1-y} = \frac{8}{3}y^2(1-y)^3$$

**Step 3: Expand the cubic term and integrate with respect to $y$**
Expanding $(1-y)^3 = 1 - 3y + 3y^2 - y^3$, then distributing $y^2$:
$$\frac{8}{3} \int_{0}^{1} (y^2 - 3y^3 + 3y^4 - y^5) \, dy = \frac{8}{3} \left[ \frac{1}{3} - \frac{3}{4} + \frac{3}{5} - \frac{1}{6} \right]$$
Calculating the bracket sum yields $\frac{1}{60}$.
$$E[XY] = \frac{8}{3} \times \frac{1}{60} = \frac{2}{45}$$

**Step 4: Compute final covariance**
$$\text{Cov}(X, Y) = E[XY] - E[X]E[Y] = \frac{2}{45} - \left(\frac{2}{5} \times \frac{2}{5}\right)$$
$$\text{Cov}(X, Y) = \frac{2}{45} - \frac{4}{25} = \frac{10 - 36}{225} = -\frac{26}{225}$$

---

## 4. Visualizing Bounds (Triangular Integration Region Graph)

The domain conditions $x > 0$, $y > 0$, and $x + y < 1$ form a right-triangle boundary space:


```

y
▲
1 ┼

│  ╲    ◀─── The boundary line equation is x + y = 1 (or x = 1 - y)
│   ╲

│█████╲     ◀─── The shaded area represents the valid domain region
│███████╲       where probability density function f(x,y) = 2
└─────────┴───► x
0         1

```

# Probability & Linear Algebra: Correlation, Vector Expectations, and Covariance Matrices

---

## 1. Concept: Correlation Coefficient & Independence

### **Simple Meaning**
While **Covariance** tells us the direction of a relationship between two variables, its value depends on the scale of the data (like inches vs. centimeters). The **Correlation Coefficient** ($\rho$) scales covariance down to a universal range between **-1 and +1**. 
* **+1**: Perfect positive linear relationship.
* **-1**: Perfect negative linear relationship.
* **0**: No linear relationship (**Uncorrelated**).

### **Mathematical Formulation**
$$\rho(X, Y) = \frac{\text{Cov}(X, Y)}{\sqrt{V[X]V[Y]}}$$

> **Important Rule:** If two random variables are independent, they are automatically uncorrelated ($\text{Cov}(X,Y) = 0$). However, **the converse is NOT true**—variables can be completely dependent on one another but still have a correlation of 0.

---

### **Proof: Uncorrelated but Dependent Variables**
Let $X$ be a continuous random variable distributed uniformly between -1 and 1:
$$f(x) = \begin{cases} \frac{1}{2}, & -1 \le x \le 1 \\ 0, & \text{elsewhere} \end{cases}$$
Let $Y = X^2$ (clearly, $Y$ depends entirely on $X$). Let us show they are uncorrelated:

1. **Calculate $E[X]$:**
   $$E[X] = \int_{-1}^{1} x \cdot \frac{1}{2} \, dx = \left[ \frac{x^2}{4} \right]_{-1}^{1} = \frac{1}{4} - \frac{1}{4} = 0$$

2. **Calculate $E[XY]$:**
   Since $Y = X^2$, then $XY = X \cdot X^2 = X^3$:
   $$E[XY] = E[X^3] = \int_{-1}^{1} x^3 \cdot \frac{1}{2} \, dx = \left[ \frac{x^4}{8} \right]_{-1}^{1} = \frac{1}{8} - \frac{1}{8} = 0$$

3. **Calculate Covariance:**
   $$\text{Cov}(X,Y) = E[XY] - E[X]E[Y] = 0 - (0 \cdot E[Y]) = 0$$

Because $\text{Cov}(X,Y) = 0$, they are **uncorrelated**, even though $Y = X^2$ makes them completely **dependent**.

---

## 2. Concept: Expectation and Variance of a Random Vector

### **Simple Meaning**
When we group multiple random variables together into a column list (a **Random Vector**), finding its "mean" or "variance" requires matrix operations. 
* The **Expectation** of a vector is simply a column vector filled with the individual expected values.
* The **Variance** of a vector expands into a grid called a **Covariance Matrix** ($\Sigma$), tracking how every variable interacts with every other variable.

### **Mathematical Formulation**
For a random vector $X = [X_1 \quad X_2 \quad \dots \quad X_n]^T$:

$$E[X] = \begin{bmatrix} E[X_1] \\ E[X_2] \\ \vdots \\ E[X_n] \end{bmatrix}$$

$$\Sigma = E[(X - E[X])(X - E[X])^T] = \begin{bmatrix} V[X_1] & \text{Cov}(X_1, X_2) & \dots & \text{Cov}(X_1, X_n) \\ \text{Cov}(X_2, X_1) & V[X_2] & \dots & \text{Cov}(X_2, X_n) \\ \vdots & \vdots & \ddots & \vdots \\ \text{Cov}(X_n, X_1) & \text{Cov}(X_n, X_2) & \dots & V[X_n] \end{bmatrix}$$

### **Properties of the Covariance Matrix ($\Sigma$)**
1. **Symmetric**: $\Sigma^T = \Sigma$ because $\text{Cov}(X_i, X_j) = \text{Cov}(X_j, X_i)$.
2. **Positive Semi-Definite**: For any constant vector $z$, $z^T \Sigma z \ge 0$.

---

### **Proof: Positive Semi-Definiteness**
Let $z$ be any constant column vector in $\mathbb{R}^n$, and let $\bar{X} = E[X]$:
1. $$z^T \Sigma z = z^T E[(X - \bar{X})(X - \bar{X})^T] z$$
2. Since $z$ is a constant vector, move it inside the expectation:
   $$= E[z^T (X - \bar{X})(X - \bar{X})^T z]$$
3. Notice that $z^T(X - \bar{X})$ is the transpose of $(X - \bar{X})^T z$. Let $\xi = z^T(X - \bar{X})$, which is a single scalar value:
   $$= E[\xi \cdot \xi^T] = E[\|\xi\|^2]$$
4. Since the expected value of a squared norm value cannot be negative:
   $$E[\|\xi\|^2] \ge 0 \implies z^T \Sigma z \ge 0$$

---

## 3. Step-by-Step Comprehensive Vector Example

### **Problem Statement**
Determine the variance (covariance matrix) of the random vector $W = \begin{bmatrix} X \\ Y \end{bmatrix}$ where the discrete joint PMF of $X$ and $Y$ is:
$$f(x,y) = \frac{x+y}{15}; \quad x \in \{0, 1, 2\}, \quad y \in \{1, 2\}$$

---

### **Step-by-Step Calculations**

#### **Step 3.1: Construct the Joint Probability Distribution Table**
We evaluate $f(x,y) = \frac{x+y}{15}$ for all combinations:

| $X \downarrow$ \ $Y \rightarrow$ | $Y = 1$ | $Y = 2$ | **Marginal $P(X=x)$** |
| :---: | :---: | :---: | :---: |
| **$X = 0$** | $\frac{0+1}{15} = \frac{1}{15}$ | $\frac{0+2}{15} = \frac{2}{15}$ | **$\frac{3}{15}$** |
| **$X = 1$** | $\frac{1+1}{15} = \frac{2}{15}$ | $\frac{1+2}{15} = \frac{3}{15}$ | **$\frac{5}{15}$** |
| **$X = 2$** | $\frac{2+1}{15} = \frac{3}{15}$ | $\frac{2+2}{15} = \frac{4}{15}$ | **$\frac{7}{15}$** |
| **Marginal $P(Y=y)$** | **$\frac{6}{15}$** | **$\frac{9}{15}$** | **Total = $\frac{15}{15} = 1$** |

#### **Step 3.2: Calculate Expectations and Variance for $X$**
1. **$E[X]$**:
   $$E[X] = \left(0 \cdot \frac{3}{15}\right) + \left(1 \cdot \frac{5}{15}\right) + \left(2 \cdot \frac{7}{15}\right) = \frac{19}{15}$$
2. **$E[X^2]$**:
   $$E[X^2] = \left(0^2 \cdot \frac{3}{15}\right) + \left(1^2 \cdot \frac{5}{15}\right) + \left(2^2 \cdot \frac{7}{15}\right) = \frac{5 + 28}{15} = \frac{33}{15}$$
3. **$V[X]$**:
   $$V[X] = E[X^2] - (E[X])^2 = \frac{33}{15} - \left(\frac{19}{15}\right)^2 = \frac{495 - 361}{225} = \frac{134}{225} \approx 0.596$$

#### **Step 3.3: Calculate Expectations and Variance for $Y$**
1. **$E[Y]$**:
   $$E[Y] = \left(1 \cdot \frac{6}{15}\right) + \left(2 \cdot \frac{9}{15}\right) = \frac{24}{15} = \frac{8}{5} = 1.6$$
2. **$E[Y^2]$**:
   $$E[Y^2] = \left(1^2 \cdot \frac{6}{15}\right) + \left(2^2 \cdot \frac{9}{15}\right) = \frac{6 + 36}{15} = \frac{42}{15} = \frac{14}{5} = 2.8$$
3. **$V[Y]$**:
   $$V[Y] = E[Y^2] - (E[Y])^2 = \frac{42}{15} - \left(\frac{24}{15}\right)^2 = \frac{630 - 576}{225} = \frac{54}{225} = \frac{6}{25} = 0.24$$

#### **Step 3.4: Calculate Joint Term $E[XY]$ and $\text{Cov}(X,Y)$**
1. **$E[XY] = \sum \sum xy \cdot f(x,y)$**:
   $$E[XY] = \left(1\cdot1\cdot\frac{2}{15}\right) + \left(1\cdot2\cdot\frac{3}{15}\right) + \left(2\cdot1\cdot\frac{3}{15}\right) + \left(2\cdot2\cdot\frac{4}{15}\right)$$
   *(Note: Terms where $x=0$ evaluate directly to 0)*
   $$E[XY] = \frac{2 + 6 + 6 + 16}{15} = \frac{30}{15} = 2$$
2. **$\text{Cov}(X,Y)$**:
   $$\text{Cov}(X,Y) = E[XY] - E[X]E[Y] = 2 - \left(\frac{19}{15} \cdot \frac{24}{15}\right) = 2 - \frac{456}{225} = \frac{450 - 456}{225} = -\frac{6}{225}$$

#### **Step 3.5: Construct Final Covariance Matrix ($\Sigma$)**
$$\Sigma = \begin{bmatrix} V[X] & \text{Cov}(X,Y) \\ \text{Cov}(Y,X) & V[Y] \end{bmatrix} = \begin{bmatrix} \frac{134}{225} & -\frac{6}{225} \\ -\frac{6}{225} & \frac{54}{225} \end{bmatrix} \approx \begin{bmatrix} 0.596 & -0.027 \\ -0.027 & 0.240 \end{bmatrix}$$

---

## 4. Practice Problem with Solution

### **Problem Statement**
Given a 2D random vector $Z = [X \quad Y]^T$ with variance values $V[X] = 4$, $V[Y] = 9$, and a correlation coefficient $\rho(X,Y) = 0.5$. Find its covariance matrix $\Sigma$.

### **Step-by-Step Calculation**

**Step 1: Identify missing parameter**
We need $\text{Cov}(X,Y)$ to fill out the off-diagonal cells of the matrix structure.

**Step 2: Rearrange the correlation equation to isolate covariance**
$$\rho(X,Y) = \frac{\text{Cov}(X,Y)}{\sqrt{V[X]V[Y]}} \implies \text{Cov}(X,Y) = \rho(X,Y) \cdot \sqrt{V[X]} \cdot \sqrt{V[Y]}$$

**Step 3: Calculate value**
$$\text{Cov}(X,Y) = 0.5 \cdot \sqrt{4} \cdot \sqrt{9} = 0.5 \cdot 2 \cdot 3 = 3$$

**Step 4: Assembly**
$$\Sigma = \begin{bmatrix} 4 & 3 \\ 3 & 9 \end{bmatrix}$$

---

## 5. Visualizing Data Dependency Shapes (Graph Concept)

The text graphs below contrast how independent data structures compare against dependent structures that share a zero-value correlation metric:

```
  Independent Data                          Dependent but Uncorrelated
(e.g., Two Fair Dice)                            (e.g., Y = X² Space)
y                                                y
▲                                                ▲
│  *   *   *                                     │  *         *
│  *   *   *                                     │   *       *
│  *   *   *                                     │    *     *
│                                                │       *
└───────────► x                                  └───────────► x
Uniformly filled grid                             Symmetric Parabola shape
Cov(X,Y) = 0                                      Cov(X,Y) = 0

```