# Probability Theory: Mathematical Expectation and its Properties

---

## 1. Concept: Mathematical Expectation

### Simple Meaning
The **Expectation** (or Expected Value) of a random variable is the long-run average value you would get if you repeated an experiment infinitely many times. Instead of a simple average, it is a **probability-weighted average**, where values that are more likely to occur contribute more heavily to the final value. It represents the center of mass (mean) of a distribution.

### Mathematical Definition
The expectation of a random variable $X$, denoted as $E[X]$ or $\mu$, is defined as:

$$\mu = E[X] = \begin{cases} \sum_{x} x f(x), & \text{if } X \text{ is discrete} \\ \int_{-\infty}^{\infty} x f(x) \, dx, & \text{if } X \text{ is continuous} \end{cases}$$

Where $f(x)$ represents the **Probability Mass Function (pmf)** if $X$ is discrete, or the **Probability Density Function (pdf)** if $X$ is continuous.

---

## 2. Concept: Linearity Properties of Expectation

### Simple Meaning
Expectation behaves linearly. If you multiply a random variable by a constant scale $a$ and shift it by a constant value $b$, the expected value changes by that exact same scale and shift. 

### The Linearity Formula
For any random variable $X$ and constants $a$ and $b$:
$$E[aX + b] = aE[X] + b$$

---

### 📝 Step-by-Step Proofs of Linearity

#### A. Proof for a Discrete Random Variable
1. Start with the discrete definition of expectation applied to the expression $(ax + b)$:
   $$E(aX + b) = \sum_{x} (ax + b) f(x)$$
2. Distribute the probability function $f(x)$ inside the parentheses:
   $$= \sum_{x} (ax f(x) + b f(x))$$
3. Split the expression into two separate summation structures:
   $$= \sum_{x} ax f(x) + \sum_{x} b f(x)$$
4. Factor the constants $a$ and $b$ outside their respective summations:
   $$= a \sum_{x} x f(x) + b \sum_{x} f(x)$$
5. Substitute known definitions: $\sum_{x} x f(x) = E(X)$, and the sum of all probabilities $\sum_{x} f(x) = 1$:
   $$= a E(X) + b \times 1 = a E(X) + b$$

#### B. Proof for a Continuous Random Variable
1. Set up the definitive integral equation from $-\infty$ to $\infty$:
   $$E(aX + b) = \int_{-\infty}^{\infty} (ax + b) f(x) \, dx$$
2. Distribute $f(x)$ across the integrand terms:
   $$= \int_{-\infty}^{\infty} \left( ax f(x) + b f(x) \right) \, dx$$
3. Separate the singular integral into two distinct integral regions:
   $$= \int_{-\infty}^{\infty} ax f(x) \, dx + \int_{-\infty}^{\infty} b f(x) \, dx$$
4. Extract the scalar factors $a$ and $b$ outside the integration operations:
   $$= a \int_{-\infty}^{\infty} x f(x) \, dx + b \int_{-\infty}^{\infty} f(x) \, dx$$
5. Recognize the operational components: $\int_{-\infty}^{\infty} x f(x) \, dx = E(X)$ and the total density area $\int_{-\infty}^{\infty} f(x) \, dx = 1$:
   $$= a E(X) + b \times 1 = a E(X) + b$$

---

## 3. 📝 Solved Problems with Step-by-Step Calculations

### Problem 1: Discrete Expectation Calculation
Find the expected value of the random variable $Y$ whose pmf is given by:
$$f(y) = \frac{y + 2}{25}; \quad y = 1, 2, 3, 4, 5$$

#### Step-by-Step Calculation:
1. **Set up the summation rule:**
   $$E[Y] = \sum_{y=1}^{5} y \cdot f(y) = \sum_{y=1}^{5} y \left( \frac{y + 2}{25} \right)$$
2. **Expand the sum term-by-term for each $y$ value:**
   * For $y = 1$: $1 \cdot \left(\frac{1+2}{25}\right) = \frac{3}{25}$
   * For $y = 2$: $2 \cdot \left(\frac{2+2}{25}\right) = 2 \cdot \frac{4}{25} = \frac{8}{25}$
   * For $y = 3$: $3 \cdot \left(\frac{3+2}{25}\right) = 3 \cdot \frac{5}{25} = \frac{15}{25}$
   * For $y = 4$: $4 \cdot \left(\frac{4+2}{25}\right) = 4 \cdot \frac{6}{25} = \frac{24}{25}$
   * For $y = 5$: $5 \cdot \left(\frac{5+2}{25}\right) = 5 \cdot \frac{7}{25} = \frac{35}{25}$
3. **Add all terms together over the common denominator:**
   $$E[Y] = \frac{3 + 8 + 15 + 24 + 35}{25}$$
   $$E[Y] = \frac{85}{25} = \frac{17}{5} = 3.4$$

**Solution:** $E[Y] = 3.4$

---

### Problem 2: Continuous Expectation Calculation
Find the expectation of a continuous random variable $X$ whose pdf is given by:
$$g(x) = \begin{cases} x, & 0 < x < 1 \\ 2 - x, & 1 \le x < 2 \\ 0, & \text{elsewhere} \end{cases}$$

#### Step-by-Step Calculation:
1. **Set up the piecewise integral definition:**
   $$E[X] = \int_{0}^{1} x(x) \, dx + \int_{1}^{2} x(2 - x) \, dx$$
   $$E[X] = \int_{0}^{1} x^2 \, dx + \int_{1}^{2} (2x - x^2) \, dx$$
2. **Integrate the first section ($0$ to $1$):**
   $$\int_{0}^{1} x^2 \, dx = \left[ \frac{x^3}{3} \right]_{0}^{1} = \frac{1}{3} - 0 = \frac{1}{3}$$
3. **Integrate the second section ($1$ to $2$):**
   $$\int_{1}^{2} (2x - x^2) \, dx = \left[ x^2 - \frac{x^3}{3} \right]_{1}^{2}$$
   * Evaluate at upper limit ($x=2$): $(2)^2 - \frac{2^3}{3} = 4 - \frac{8}{3} = \frac{4}{3}$
   * Evaluate at lower limit ($x=1$): $(1)^2 - \frac{1^3}{3} = 1 - \frac{1}{3} = \frac{2}{3}$
   * Subtract (Upper - Lower): $\frac{4}{3} - \frac{2}{3} = \frac{2}{3}$
4. **Sum the integrated pieces together:**
   $$E[X] = \frac{1}{3} + \frac{2}{3} = \frac{3}{3} = 1$$

**Solution:** $E[X] = 1$

---

### Problem 3: Linearity System of Equations
If $E[2X] = 10$ and $E[Y + 3X] = 25$, find the expected value of $W = 4X - Y$.

#### Step-by-Step Calculation:
1. **Isolate $E[X]$ from the first equation using linearity:**
   $$E[2X] = 10 \implies 2E[X] = 10 \implies E[X] = 5$$
2. **Expand the second equation to find $E[Y]$:**
   $$E[Y + 3X] = 25 \implies E[Y] + 3E[X] = 25$$
   Substitute $E[X] = 5$:
   $$E[Y] + 3(5) = 25 \implies E[Y] + 15 = 25 \implies E[Y] = 10$$
3. **Evaluate the target expression $E[W] = E[4X - Y]$:**
   $$E[4X - Y] = 4E[X] - E[Y]$$
   Substitute $E[X] = 5$ and $E[Y] = 10$:
   $$E[W] = 4(5) - 10 = 20 - 10 = 10$$

**Solution:** $E[W] = 10$

---

## 4. 📊 Graphical Representations

### Symmetric Continuous Triangular Distribution Graph (Problem 2)
The expected value acts as a balance point. For the continuous piecewise function $g(x)$ evaluated in Problem 2, the graph forms a perfect symmetric triangle. The center of gravity rests exactly at the peak, verifying why our calculated value equals $1$:

```text
  Density g(x)
   1.0 |         *  (Peak at x=1)
       |        / \
       |       /   \
       |      /     \
   0.0 +-----+-------+-----+-------> x Axis
       0     1       2
             ^
       Balance Center (Mean / Expectation) = 1
```

# Probability Theory: Advanced Solved Problems on Expectation

---

## 1. Concept: Expectation of a Discrete Random Variable

### Simple Meaning
The **expected value** of a discrete random variable is the long-term weighted average value of the outcomes. Instead of adding the numbers up and dividing by the total count, we multiply each possible outcome value by its respective probability and then sum those products together.

### Formula Context
$$E(Y) = \sum_{y} y \cdot f(y)$$

Useful shortcut summation formulas for the first $n$ natural numbers:
* **Sum of numbers:** $\sum_{y=1}^{n} y = \frac{n(n+1)}{2}$
* **Sum of squares:** $\sum_{y=1}^{n} y^2 = \frac{n(n+1)(2n+1)}{6}$

---

### 📝 Problem 1: Step-by-Step Calculation

**Problem Statement:** Find the expectation of the discrete random variable $Y$ whose probability mass function (pmf) is given by $f(y) = \frac{y + 2}{25}$ for $y = 1, 2, 3, 4, 5$.

#### Step-by-Step Mathematical Derivation:
1. **Set up the definition formula:**
   $$E(Y) = \sum_{y=1}^{5} y \cdot \left(\frac{y + 2}{25}\right)$$

2. **Distribute the variable $y$ and split the summation terms:**
   $$E(Y) = \sum_{y=1}^{5} \left(\frac{y^2 + 2y}{25}\right) = \frac{1}{25}\sum_{y=1}^{5} y^2 + \frac{2}{25}\sum_{y=1}^{5} y$$

3. **Apply the shortcut formulas for $n = 5$:**
   * For $\sum_{y=1}^{5} y^2$: $\frac{5(5+1)(2(5)+1)}{6} = \frac{5 \times 6 \times 11}{6} = 55$
   * For $\sum_{y=1}^{5} y$: $\frac{5(5+1)}{2} = \frac{5 \times 6}{2} = 15$

4. **Substitute the calculated sums back into the equation:**
   $$E(Y) = \frac{1}{25}[55] + \frac{2}{25}[15]$$

5. **Simplify the fractions:**
   $$E(Y) = \frac{11}{5} + \frac{6}{5} = \frac{17}{5}$$

**Solution:**  
$$E(Y) = \frac{17}{5} = 3.4$$

---

## 2. Concept: Expectation of a Continuous Random Variable

### Simple Meaning
When a random variable is continuous, the outcomes exist over an unbroken numeric interval rather than discrete points. To find the long-term average, we replace the summation symbol ($\sum$) with a calculus integration symbol ($\int$), integrating the product of the variable and its density curve equation.

### Formula Context
$$E(X) = \int_{-\infty}^{\infty} x \cdot g(x) \, dx$$

---

### 📝 Problem 2: Step-by-Step Calculation

**Problem Statement:** Find the expectation of the continuous random variable $X$ whose probability density function (pdf) is given by:
$$g(x) = \begin{cases} x, & 0 < x < 1 \\ 2 - x, & 1 \le x < 2 \\ 0, & \text{elsewhere} \end{cases}$$

#### Step-by-Step Mathematical Derivation:
1. **Break the integration down into its piecewise intervals:**
   $$E(X) = \int_{0}^{1} x(x) \, dx + \int_{1}^{2} x(2 - x) \, dx$$
   $$E(X) = \int_{0}^{1} x^2 \, dx + \int_{1}^{2} (2x - x^2) \, dx$$

2. **Evaluate the first integral part:**
   $$\int_{0}^{1} x^2 \, dx = \left[ \frac{x^3}{3} \right]_{0}^{1} = \frac{1}{3} - 0 = \frac{1}{3}$$

3. **Evaluate the second integral part using boundaries:**
   $$\int_{1}^{2} (2x - x^2) \, dx = \left[ \frac{2x^2}{2} - \frac{x^3}{3} \right]_{1}^{2} = \left[ x^2 \right]_{1}^{2} - \left[ \frac{x^3}{3} \right]_{1}^{2}$$
   $$= (2^2 - 1^2) - \frac{1}{3}(2^3 - 1^3)$$
   $$= (4 - 1) - \frac{1}{3}(8 - 1) = 3 - \frac{7}{3}$$

4. **Combine the parts to find the total expected value:**
   $$E(X) = \frac{1}{3} + 3 - \frac{7}{3}$$
   Group the fractions together over a common denominator:
   $$E(X) = \frac{10}{3} - \frac{7}{3} = \frac{3}{3} = 1$$

**Solution:**  
$$E(X) = 1$$

---

## 3. Concept: Linearity Properties of Expectation

### Simple Meaning
The expectation operator is linear. This means if you are looking for the expected value of scales and additions, you can evaluate the individual components separately.
* Rule 1: $E(cX) = c \cdot E(X)$ (where $c$ is a constant multiplier)
* Rule 2: $E(X \pm Y) = E(X) \pm E(Y)$

---

### 📝 Problem 3: Step-by-Step Calculation

**Problem Statement:** If $E[2X] = 10$ and $E[Y + 3X] = 25$, find the expectation of $W = 4X - Y$.

#### Step-by-Step Calculation:
1. **Isolate $E(X)$ using linearity:**
   $$E(2X) = 10 \implies 2E(X) = 10$$
   $$E(X) = \frac{10}{2} = 5$$

2. **Expand the second equation to solve for $E(Y)$:**
   $$E(Y + 3X) = 25 \implies E(Y) + 3E(X) = 25$$
   Substitute our known value $E(X) = 5$:
   $$E(Y) + 3(5) = 25 \implies E(Y) + 15 = 25$$
   $$E(Y) = 25 - 15 = 10$$

3. **Expand and solve the target expression $E(4X - Y)$:**
   $$E(4X - Y) = 4E(X) - E(Y)$$
   Substitute $E(X) = 5$ and $E(Y) = 10$:
   $$E(4X - Y) = 4(5) - 10$$
   $$E(4X - Y) = 20 - 10 = 10$$

**Solution:**  
$$E(4X - Y) = 10$$

---

## 4. 📊 Discrete Probability Mass Function Graph

Below is the visual distribution chart for the discrete variable $Y$ from Problem 1, showcasing how the probabilities scale up linearly as $y$ increases:

```text
 Probability f(y)
  7/25 |                                      *
  6/25 |                              *
  5/25 |                      *
  4/25 |              *
  3/25 |      *
       +------+------+------+------+------+---------> y Axis
              1      2      3      4      5
```


# Probability Theory: Variance and its Algebraic Properties

---

## 1. Concept Introduction: Variance ($V[X]$)

### Simple Meaning
While the **Expectation ($E[X]$)** tells us the balance center (mean) of a random variable, **Variance ($V[X]$)** measures how much the values of the random variable are spread out or scattered around that mean. 
* A **low variance** means the data values are tightly clustered close to the average.
* A **high variance** means the data values are highly spread out far away from the average.

### Mathematical Formulation
Formally, variance is defined as the average squared deviation of the values of $X$ from its mean:
$$V[X] = E\left[(X - E[X])^2\right] = E[X^2] - (E[X])^2$$

---

## 2. 📝 Step-by-Step Proofs and Algebraic Derivations

### Proof 1: Alternate Computational Formula for Variance
**Goal:** Prove that $E[(X - E[X])^2] = E[X^2] - (E[X])^2$.

Let $\mu = E[X]$, where $\mu$ is a constant value.

1. **Expand the squared term inside the expectation:**
   Using the algebraic identity $(a-b)^2 = a^2 - 2ab + b^2$:
   $$V(X) = E\left[(X - \mu)^2\right] = E\left[X^2 - 2X\mu + \mu^2\right]$$

2. **Apply the linearity property of expectation:**
   Separate the singular expectation operator into individual parts:
   $$= E[X^2] + E[-2X\mu] + E[\mu^2]$$

3. **Pull out constants:**
   Since $\mu$ is a constant, values like $-2\mu$ and $\mu^2$ can be factored outside the operators:
   $$= E[X^2] - 2\mu E[X] + \mu^2 E[1]$$

4. **Simplify using fundamental identities:**
   Recall that $E[1] = 1$ and $E[X] = \mu$:
   $$= E[X^2] - 2\mu(\mu) + \mu^2(1)$$
   $$= E[X^2] - 2\mu^2 + \mu^2$$

5. **Combine like terms:**
   $$= E[X^2] - \mu^2$$
   $$= E[X^2] - (E[X])^2$$

> **Important Logical Consequence:**
> Because variance averages squared distances, it can never be negative: $V(X) \ge 0$.
> This mathematically proves that:
> $$E[X^2] - (E[X])^2 \ge 0 \implies E[X^2] \ge (E[X])^2$$

---

### Proof 2: Linearity Property under Scaling and Shifting ($V[aX + b]$)
**Goal:** Prove that $V[aX + b] = a^2 V[X]$ for constants $a$ and $b$.

1. **Set up the base definition equation:**
   $$V(aX + b) = E\left[ \Big( (aX + b) - E(aX + b) \Big)^2 \right]$$

2. **Expand the inner expectation using $E[aX + b] = aE[X] + b$:**
   $$= E\left[ \Big( ax + b - (aE[X] + b) \Big)^2 \right]$$

3. **Simplify terms inside the bracket:**
   The constant shifting factors $+b$ and $-b$ cancel each other out entirely:
   $$= E\left[ \Big( ax + \cancel{b} - aE[X] - \cancel{b} \Big)^2 \right]$$
   $$= E\left[ \Big( ax - aE[X] \Big)^2 \right]$$

4. **Factor out the scalar value $a$:**
   $$= E\left[ \Big( a(X - E[X]) \Big)^2 \right]$$
   $$= E\left[ a^2 (X - E[X])^2 \right]$$

5. **Extract the squared constant outside the expectation operator:**
   $$= a^2 E\left[ (X - E[X])^2 \right]$$
   $$= a^2 V(X)$$

---

### Core Shortcut Summary Rules
* **Scaling Rule:** Shifting has no effect on dispersion, but scaling scales by its square.
  $$V(\alpha X) = \alpha^2 V(X)$$
* **Shifting Rule:** Adding or subtracting a flat value shifts the location of data but leaves its spacing completely unaltered.
  $$V(X - a) = V(X)$$

---

## 3. 📝 Solved Problems with Step-by-Step Calculations

### Problem 1: Variance of a Discrete Distribution Table
A discrete random variable $X$ has the following probability distribution setup:

| $X$ | 1 | 2 | 3 |
| :--- | :---: | :---: | :---: |
| **$P(X)$** | $0.2$ | $0.5$ | $0.3$ |

Calculate the Variance $V[X]$.

#### Step-by-Step Calculation:
1. **Calculate the Expected Value $E[X]$:**
   $$E[X] = \sum x \cdot P(X)$$
   $$E[X] = (1 \times 0.2) + (2 \times 0.5) + (3 \times 0.3)$$
   $$E[X] = 0.2 + 1.0 + 0.9 = 2.1$$

2. **Calculate the Expected Value of Squares $E[X^2]$:**
   $$E[X^2] = \sum x^2 \cdot P(X)$$
   $$E[X^2] = (1^2 \times 0.2) + (2^2 \times 0.5) + (3^2 \times 0.3)$$
   $$E[X^2] = (1 \times 0.2) + (4 \times 0.5) + (9 \times 0.3)$$
   $$E[X^2] = 0.2 + 2.0 + 2.7 = 4.9$$

3. **Compute the final Variance using the formula:**
   $$V[X] = E[X^2] - (E[X])^2$$
   $$V[X] = 4.9 - (2.1)^2$$
   $$V[X] = 4.9 - 4.41 = 0.49$$

**Solution:** $V[X] = 0.49$

---

### Problem 2: Linear Transformation Systems
Suppose a random variable $X$ has an expected value $E[X] = 4$ and a variance $V[X] = 3$. 
Find the variance of a new transformed variable $W = -5X + 7$.

#### Step-by-Step Calculation:
1. **Set up the transformation equation:**
   $$V[W] = V[-5X + 7]$$
2. **Apply the properties of variance:**
   * Shifting constants ($+7$) have zero impact on variance: $V[-5X + 7] = V[-5X]$
   * Scaling coefficients are pulled out squared: $V[-5X] = (-5)^2 \cdot V[X]$
3. **Compute numerical solution:**
   $$V[W] = 25 \cdot V[X]$$
   Substitute $V[X] = 3$:
   $$V[W] = 25 \times 3 = 75$$

**Solution:** $V[W] = 75$

---

## 4. 📊 Graphical Variance Spread Comparisons

The text-graphs below display how variance scales visually while maintaining the same mean ($\mu = 0$):

### Distribution A: Low Variance (Tightly Packed around Center)
```text
  Probability density f(x)
             *
            ***
           * | *
          *  |  *
        *    |    *
   -----+----+----+-----x Axis
           Mean (0)

```

### Distribution B: High Variance (Widely Dispersed from Center)

```text
  Probability density f(x)
          
             *
         *   |   *
       *     |     *
     *       |       *
   *         |         *
  -----------+-----------x Axis
           Mean (0)

```


# Probability & Statistics: Practice Problems on Variance and Expectation

---

## 1. Concept: Variance of a Discrete Random Variable

### Simple Meaning
For a discrete random variable, the **variance** ($V(X)$) measures how far the discrete points spread out around their center (mean). To find it, we calculate the expected value of the squares ($E(X^2)$) and subtract the square of the standard expectation ($(E(X))^2$).

### Mathematical Formula
$$V(X) = E(X^2) - (E(X))^2$$
* Shortcut for sum of consecutive squares: $\sum_{x=1}^{n} x^2 = \frac{n(n+1)(2n+1)}{6}$
* Shortcut for sum of consecutive cubes: $\sum_{x=1}^{n} x^3 = \left[\frac{n(n+1)}{2}\right]^2$

---

### 📝 Problem 1(a): Step-by-Step Solution

**Problem Statement:** Find the variance of the random variable $X$ whose pmf is given as $f(x) = \frac{x}{15}$ for $x = 1, 2, 3, 4, 5$.

#### Step 1: Calculate the Expectation $E(X)$
$$E(X) = \sum_{x=1}^{5} x \cdot f(x) = \sum_{x=1}^{5} x \left(\frac{x}{15}\right) = \frac{1}{15}\sum_{x=1}^{5} x^2$$
Apply the sum of squares formula for $n=5$:
$$E(X) = \frac{1}{15} \left[ \frac{5 \times (5+1) \times (2(5)+1)}{6} \right] = \frac{1}{15} \left[ \frac{5 \times 6 \times 11}{6} \right] = \frac{1}{15} [55] = \frac{11}{3}$$

#### Step 2: Calculate the Expectation of Squares $E(X^2)$
$$E(X^2) = \sum_{x=1}^{5} x^2 \cdot f(x) = \sum_{x=1}^{5} x^2 \left(\frac{x}{15}\right) = \frac{1}{15}\sum_{x=1}^{5} x^3$$
Apply the sum of cubes formula for $n=5$:
$$E(X^2) = \frac{1}{15} \left[ \frac{5 \times 6}{2} \right]^2 = \frac{1}{15} [15]^2 = \frac{225}{15} = 15$$

#### Step 3: Compute the Final Variance $V(X)$
$$V(X) = E(X^2) - (E(X))^2 = 15 - \left(\frac{11}{3}\right)^2 = 15 - \frac{121}{9}$$
Convert to a common denominator:
$$V(X) = \frac{135 - 121}{9} = \frac{14}{9} \approx 1.556$$

---

## 2. Concept: Variance of a Continuous Random Variable

### Simple Meaning
When a random variable is continuous, its values change smoothly across an unbroken span rather than jumping to specific integers. To calculate the average and spread, we swap discrete sums ($\sum$) for calculus integrals ($\int$). If an integration spans toward infinity ($\infty$), we use limits to find where the values settle.

---

### 📝 Problem 1(b): Step-by-Step Solution

**Problem Statement:** Find the variance of the random variable $Z$ whose pdf is given as $h(z) = 2e^{-2z}$ for $z > 0$.

#### Step 1: Calculate the Expectation $E(Z)$
Using Integration by Parts ($\int u \, dv = uv - \int v \, du$):
$$E(Z) = \int_{0}^{\infty} z \cdot (2e^{-2z}) \, dz = 2 \int_{0}^{\infty} z e^{-2z} \, dz$$
$$= 2 \left[ z\left(\frac{e^{-2z}}{-2}\right) - 1\left(\frac{e^{-2z}}{4}\right) \right]_{0}^{\infty}$$
* Evaluating the upper limit ($\infty$): As $z \to \infty$, the term $\frac{z}{-2e^{2z}} \to 0$ and $\frac{1}{4e^{2z}} \to 0$ due to L'Hôpital's Rule.
* Evaluating the lower limit ($z = 0$): $2 \left[ 0 - \frac{1}{4} \right] = -\frac{1}{2}$.
Subtracting lower limit from upper limit: $0 - \left(-\frac{1}{2}\right) = \frac{1}{2}$.
$$E(Z) = \frac{1}{2}$$

#### Step 2: Calculate the Expectation of Squares $E(Z^2)$
Integrating by parts twice:
$$E(Z^2) = \int_{0}^{\infty} z^2 \cdot (2e^{-2z}) \, dz = 2 \left[ z^2\left(\frac{e^{-2z}}{-2}\right) - (2z)\left(\frac{e^{-2z}}{4}\right) + 2\left(\frac{e^{-2z}}{-8}\right) \right]_{0}^{\infty}$$
* The upper limit ($\infty$) evaluates to $0$.
* The lower limit ($z=0$) evaluates to $2 \left[ 0 - 0 - \frac{2}{8} \right] = -\frac{1}{2}$.
Subtracting: $0 - \left(-\frac{1}{2}\right) = \frac{1}{2}$.
$$E(Z^2) = \frac{1}{2}$$

#### Step 3: Compute the Final Variance $V(Z)$
$$V(Z) = E(Z^2) - (E(Z))^2 = \frac{1}{2} - \left(\frac{1}{2}\right)^2 = \frac{1}{2} - \frac{1}{4} = \frac{1}{4} = 0.25$$

---

## 3. Concept: Linear Properties of Variance

### Simple Meaning
* **Shifting Rule:** Adding or subtracting a flat number to a variable shifts the entire dataset but leaves the spacing between points completely unchanged. Therefore, constants added or subtracted drop out: $V(X + c) = V(X)$.
* **Scaling Rule:** Multiplying a variable stretches or compresses the dataset. The variance changes by the **square** of that multiplier: $V(cX) = c^2 \cdot V(X)$.

---

### 📝 Problem 2: Step-by-Step Solution

**Problem Statement:** If $V[X] = 4$ and $V[4Y] = 32$, determine the variance of $Z = 2X - 8$ and $U = Y + 2$.

#### Step 1: Find the Variance of $Z$
$$V(Z) = V(2X - 8)$$
* Drop the shifting constant ($-8$): $V(2X - 8) = V(2X)$
* Pull out the multiplier squared: $V(2X) = 2^2 \cdot V(X) = 4 \cdot V(X)$
* Substitute $V[X] = 4$:
$$V(Z) = 4 \times 4 = 16$$

#### Step 2: Find the Base Variance of $Y$ and the Variance of $U$
* First decode $V[4Y] = 32$:
  $$V(4Y) = 4^2 \cdot V(Y) = 16 \cdot V(Y) = 32 \implies V(Y) = \frac{32}{16} = 2$$
* Now compute $V(U)$:
  $$V(U) = V(Y + 2)$$
* Drop the shifting constant ($+2$):
  $$V(U) = V(Y) = 2$$

---

## 4. Concept: Two-Dice Distribution Analysis (Modulus Difference)

### Simple Meaning
When rolling two dice, we analyze the absolute positive gap between the numbers. For example, rolling a 2 and a 5 creates a difference of $\vert{}2 - 5\vert{} = 3$. We count how often each gap size occurs out of the 36 possible outcomes to build a new distribution table.

---

### 📝 Problem 3: Step-by-Step Solution

**Problem Statement:** Consider a random experiment of rolling two dice simultaneously. Find the expectation and variance of the modulus of the difference of the two numbers that come up.

#### Step 1: Construct the Probability Distribution Table
Let $X = \vert{} \text{Die}_1 - \text{Die}_2 \vert{}$. The gaps range from 0 to 5.
* **$X = 0$** (Double outcomes: (1,1) to (6,6)) $\implies 6 \text{ pairs} \implies P(0) = \frac{6}{36}$
* **$X = 1$** (Pairs like (1,2), (2,1), (2,3)...) $\implies 10 \text{ pairs} \implies P(1) = \frac{10}{36}$
* **$X = 2$** (Pairs like (1,3), (3,1), (2,4)...) $\implies 8 \text{ pairs} \implies P(2) = \frac{8}{36}$
* **$X = 3$** (Pairs like (1,4), (4,1), (2,5)...) $\implies 6 \text{ pairs} \implies P(3) = \frac{6}{36}$
* **$X = 4$** (Pairs like (1,5), (5,1), (2,6)...) $\implies 4 \text{ pairs} \implies P(4) = \frac{4}{36}$
* **$X = 5$** (Pairs like (1,6), (6,1)) $\implies 2 \text{ pairs} \implies P(5) = \frac{2}{36}$

| $X$ | 0 | 1 | 2 | 3 | 4 | 5 |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| **$P(X)$** | $\frac{6}{36}$ | $\frac{10}{36}$ | $\frac{8}{36}$ | $\frac{6}{36}$ | $\frac{4}{36}$ | $\frac{2}{36}$ |

#### Step 2: Calculate the Expectation $E(X)$
$$E(X) = \sum x \cdot P(x) = \left(0 \times \frac{6}{36}\right) + \left(1 \times \frac{10}{36}\right) + \left(2 \times \frac{8}{36}\right) + \left(3 \times \frac{6}{36}\right) + \left(4 \times \frac{4}{36}\right) + \left(5 \times \frac{2}{36}\right)$$
$$E(X) = \frac{0 + 10 + 16 + 18 + 16 + 10}{36} = \frac{70}{36} = \frac{35}{18} \approx 1.944$$

#### Step 3: Calculate the Expectation of Squares $E(X^2)$
$$E(X^2) = \sum x^2 \cdot P(x) = \left(0^2 \times \frac{6}{36}\right) + \left(1^2 \times \frac{10}{36}\right) + \left(2^2 \times \frac{8}{36}\right) + \left(3^2 \times \frac{6}{36}\right) + \left(4^2 \times \frac{4}{36}\right) + \left(5^2 \times \frac{2}{36}\right)$$
$$E(X^2) = \frac{0 + 10 + 32 + 54 + 64 + 50}{36} = \frac{210}{36} = \frac{35}{6} \approx 5.833$$

#### Step 4: Calculate Variance $V(X)$
$$V(X) = E(X^2) - (E(X))^2 = \frac{35}{6} - \left(\frac{35}{18}\right)^2 = \frac{35}{6} - \frac{1225}{324}$$
Bring to a common denominator (324):
$$V(X) = \frac{1890 - 1225}{324} = \frac{665}{324} \approx 2.0524$$

---

## 5. 📊 Graphical Representations

### Line Plot: Probability Distribution of Modulus Differences
This graph shows the step-down pattern of probabilities as the modulus gap size increases:

```text
 Probability P(X)
  10/36 |       *
   8/36 |               *
   6/36 |   *                   *
   4/36 |                           *
   2/36 |                                   *
        +-------+-------+-------+-------+-------+---------> X Axis
            0       1       2       3       4       5  (Gap Size)