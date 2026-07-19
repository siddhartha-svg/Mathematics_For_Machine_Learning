# Probability & Statistics: Continuous Uniform Distribution

---

## 1. Concept Introduction: Continuous Uniform Distribution

A **Continuous Uniform Distribution** describes a situation where a continuous random variable $X$ can take any value within a specific interval $[a, b]$, and the probability density is **equally spread out (flat)** across that entire range. It is written as:
$$X \sim U[a, b]$$

### Probability Density Function (PDF)
Because the total area under a probability curve must equal 1, the height of a flat distribution spanning a width of $b - a$ must be exactly equal to $\frac{1}{b - a}$.
$$u(x; a, b) = \begin{cases} \frac{1}{b - a}, & a < x < b \\ 0, & \text{elsewhere} \end{cases}$$

### Fundamental Properties
*   **Mean (Expected Value):** $E[X] = \frac{a + b}{2}$ (The exact midpoint of the interval)
*   **Variance:** $V[X] = \frac{1}{12}(b - a)^2$ (A measure of the distribution spread)

---

## 2. Mathematical Proofs & Derivations

### Proof 1: Verifying Total Probability Equals 1
To verify the PDF is valid, integrating it across all real numbers must yield exactly 1:
$$\int_{-\infty}^{\infty} u(x; a, b) \, dx = \int_{a}^{b} \frac{1}{b - a} \, dx$$

#### Step-by-Step Calculation:
1. **Factor out the constant:**
   $$\frac{1}{b - a} \int_{a}^{b} 1 \, dx$$
2. **Integrate $1$ with respect to $x$:**
   $$\frac{1}{b - a} \Big[ x \Big]_{a}^{b}$$
3. **Evaluate the limits ($b - a$):**
   $$\frac{1}{b - a} (b - a) = 1$$

---

### Proof 2: Deriving the Mean $E(X) = \frac{a + b}{2}$
The expected value for a continuous distribution is found by integrating $x \cdot PDF$:
$$E(X) = \int_{a}^{b} x \left( \frac{1}{b - a} \right) \, dx$$

#### Step-by-Step Calculation:
1. **Factor out the constant:**
   $$\frac{1}{b - a} \int_{a}^{b} x \, dx$$
2. **Apply the power rule for integration ($\int x \, dx = \frac{x^2}{2}$):**
   $$\frac{1}{b - a} \left[ \frac{x^2}{2} \right]_{a}^{b} = \frac{1}{2(b - a)} (b^2 - a^2)$$
3. **Factor the difference of squares ($b^2 - a^2 = (b - a)(b + a)$):**
   $$E(X) = \frac{(b - a)(b + a)}{2(b - a)}$$
4. **Cancel the common term $(b - a)$:**
   $$E(X) = \frac{a + b}{2}$$

---

### Proof 3: Deriving the Variance $V(X) = \frac{(b - a)^2}{12}$
Using the identity $V(X) = E(X^2) - (E(X))^2$, we first compute $E(X^2)$:
$$E(X^2) = \int_{a}^{b} x^2 \left( \frac{1}{b - a} \right) \, dx$$

#### Step-by-Step Calculation:
1. **Integrate $x^2$:**
   $$\frac{1}{b - a} \left[ \frac{x^3}{3} \right]_{a}^{b} = \frac{b^3 - a^3}{3(b - a)}$$
2. **Factor the difference of cubes ($b^3 - a^3 = (b - a)(b^2 + a^2 + ab)$):**
   $$E(X^2) = \frac{(b - a)(b^2 + a^2 + ab)}{3(b - a)} = \frac{b^2 + a^2 + ab}{3}$$
3. **Substitute $E(X^2)$ and $E(X)$ into the variance formula:**
   $$V(X) = \frac{b^2 + a^2 + ab}{3} - \left(\frac{a + b}{2}\right)^2$$
   $$V(X) = \frac{b^2 + a^2 + ab}{3} - \frac{a^2 + b^2 + 2ab}{4}$$
4. **Find a common denominator (12):**
   $$V(X) = \frac{4(b^2 + a^2 + ab) - 3(a^2 + b^2 + 2ab)}{12}$$
   $$V(X) = \frac{4b^2 + 4a^2 + 4ab - 3a^2 - 3b^2 - 6ab}{12}$$
   $$V(X) = \frac{a^2 + b^2 - 2ab}{12}$$
5. **Simplify using the perfect square trinomial identity:**
   $$V(X) = \frac{(a - b)^2}{12} = \frac{(b - a)^2}{12}$$

---

## 3. Text-Based Graph Visualization

A continuous uniform distribution forms a perfect rectangle over the interval $[a, b]$. The area inside this box equals exactly $1.0$.

```text
 Probability Density f(x)
   ^
   |
1/(b-a) |       +-----------------------+
   |       |                       |
   |       |      Total Area = 1   |
   |       |                       |
 0 +-------+-----------------------+-------+-----> Value of X
           a                       b

```

---

## 4. Practice Problems with Solutions

### Problem 1: Bus Waiting Time

A commuter bus arrives at a station uniformly between 8:00 AM and 8:20 AM. Let $X$ represent the waiting time in minutes for a passenger who arrives exactly at 8:00 AM.

1. Find the probability that the passenger waits between 5 and 15 minutes.
2. Find the mean and variance of the waiting time.

#### Step-by-Step Solution:

1. **Identify parameters:**
* $a = 0$ minutes, $b = 20$ minutes.
* Constant height of PDF $= \frac{1}{b - a} = \frac{1}{20 - 0} = \frac{1}{20}$


2. **Calculate Probability $P(5 < X < 15)$:**

$$P(5 < X < 15) = \int_{5}^{15} \frac{1}{20} \, dx = \frac{1}{20} \Big[ x \Big]_{5}^{15}$$


$$P(5 < X < 15) = \frac{1}{20} (15 - 5) = \frac{10}{20} = 0.5$$



*(There is a **50%** chance of waiting between 5 and 15 minutes.)*
3. **Calculate Mean:**

$$E(X) = \frac{a + b}{2} = \frac{0 + 20}{2} = 10 \text{ minutes}$$


4. **Calculate Variance:**

$$V(X) = \frac{(b - a)^2}{12} = \frac{(20 - 0)^2}{12} = \frac{400}{12} \approx 33.33 \text{ minutes}^2$$



---

### Problem 2: Industrial Cable Cutting

An automated industrial machine cuts electrical wires to lengths that are uniformly distributed between 98 cm and 102 cm. What is the probability that a randomly chosen wire length is greater than 101 cm?

#### Step-by-Step Solution:

1. **Identify parameters:**
* Lower bound $a = 98$, Upper bound $b = 102$
* PDF value within range $= \frac{1}{102 - 98} = \frac{1}{4} = 0.25$


2. **Set up the target condition:**
* We want the probability of lengths greater than 101 cm up to the maximum limit of 102 cm: $P(101 < X < 102)$


3. **Calculate the Probability:**

$$P(101 < X < 102) = \int_{101}^{102} 0.25 \, dx = 0.25 \Big[ x \Big]_{101}^{102}$$


$$P(101 < X < 102) = 0.25 \times (102 - 101) = 0.25 \times 1 = 0.25$$



**Answer:** There is a **25%** probability that a randomly selected wire is longer than 101 cm.


# Probability Distributions: Uniform & Exponential (Continuous)

---

## 1. Concept: Continuous Uniform Distribution Problems

The Probability Density Function (PDF) of a continuous uniform random variable $X \sim U[a, b]$ is given by $f(x) = \frac{1}{b - a}$ for $a < x < b$, and $0$ elsewhere. The probability that $X$ falls within a sub-interval is computed by integrating the PDF over that specific region, which visually corresponds to finding the area of a rectangle.

---

### Problem 1: Solving for a Parameter Given a Probability
**Statement:** Suppose $X \sim U[-a, a]$, with $a > 0$. Determine the value of $a$ such that:
$$P\left[X < -\frac{1}{2}\right] = \frac{3}{10}$$

#### Simple Meaning:
We are told that the variable is completely flat between a negative number $-a$ and a positive number $a$. The total width of this range is $a - (-a) = 2a$, making the constant height of the probability block $\frac{1}{2a}$. We need to find the specific boundary width $a$ so that the left side of the block up to $-\frac{1}{2}$ holds exactly $30\%$ ($\frac{3}{10}$) of the total probability area.

#### Step-by-Step Calculation:
1. **Identify the PDF parameters:**
   * Lower bound $= -a$, Upper bound $= a$.
   * The height of the function is: $f(x) = \frac{1}{a - (-a)} = \frac{1}{2a}$.

2. **Set up the definite integral for the given probability region:**
   Since $X$ cannot go below $-a$, the probability area accumulates from $-a$ up to $-\frac{1}{2}$:
   $$\int_{-a}^{-1/2} \frac{1}{2a} \, dx = \frac{3}{10}$$

3. **Perform the integration:**
   $$\frac{1}{2a} \Big[ x \Big]_{-a}^{-1/2} = \frac{3}{10}$$
   $$\frac{1}{2a} \left( -\frac{1}{2} - (-a) \right) = \frac{3}{10}$$
   $$\frac{1}{2a} \left( -\frac{1}{2} + a \right) = \frac{3}{10}$$

4. **Expand and simplify the algebraic equation:**
   $$-\frac{1}{4a} + \frac{a}{2a} = \frac{3}{10}$$
   $$-\frac{1}{4a} + \frac{1}{2} = \frac{3}{10}$$

5. **Isolate the variable fraction:**
   $$-\frac{1}{4a} = \frac{3}{10} - \frac{1}{2}$$
   $$-\frac{1}{4a} = \frac{3 - 5}{10} = -\frac{2}{10}$$
   $$-\frac{1}{4a} = -\frac{1}{5}$$

6. **Cross-multiply to find $a$:**
   $$4a = 5 \implies a = \frac{5}{4} = 1.25$$

---

### Problem 2: Finding a Probability Over a Sub-Interval
**Statement:** Let $X \sim U[-2, 3]$. Find $P[X > 1]$.

#### Simple Meaning:
The variable is uniformly spread across an interval starting at $-2$ and ending at $3$. We want to know the chances that a randomly selected value from this distribution is strictly greater than $1$.

#### Step-by-Step Calculation:
1. **Determine the constant PDF value:**
   * Lower bound $a = -2$, Upper bound $b = 3$.
   * Total interval width $= 3 - (-2) = 5$.
   * Constant height $f(x) = \frac{1}{5}$.

2. **Set up the integral boundaries:**
   We want the area where $X > 1$, which starts at $1$ and goes up to the absolute upper distribution limit of $3$:
   $$P(X > 1) = \int_{1}^{3} \frac{1}{5} \, dx$$

3. **Evaluate the integration:**
   $$P(X > 1) = \frac{1}{5} \Big[ x \Big]_{1}^{3}$$
   $$P(X > 1) = \frac{1}{5} (3 - 1) = \frac{2}{5} = 0.4$$

**Answer:** The probability is **0.4** (or **40%**).

---

### Text Graph: Uniform Distribution $U[-2, 3]$ Area for $P(X > 1)$

```text
  f(x)
   ^
0.2|   +-----------------------+  <- Height = 1/5 = 0.2
   |   |///////|               |
   |   |///////|  Target Area  |
   |   |///////|   (2/5 = 0.4) |
 0 +---+-------+---------------+---> x
      -2       1               3

```

---

## 2. Concept: Exponential Distribution

The **Exponential Distribution** models the continuous time intervals between independent Poisson events occurring at a constant average rate. It is widely used to study item lifespans, waiting times, or operational durations before a component fails.

### Probability Density Function (PDF)

A continuous random variable $X$ follows an exponential distribution, written as $X \sim \text{Exp}(\lambda)$, if its probability density is defined by:


$$\text{exp}(x; \lambda) = \begin{cases} \frac{1}{\lambda} e^{-x/\lambda}, & x > 0 \\ 0, & x \le 0 \end{cases}$$


*(Note: Here, $\lambda$ acts as the scale parameter representing the average waiting time).*

### Key Properties

* **Mean ($E[X]$):** $\lambda$
* **Variance ($V[X]$):** $\lambda^2$

---

## 3. Mathematical Proofs for the Exponential Distribution

### Proof 1: Verifying Total Probability Area Equals 1

An integration across its entire positive domain must sum up to exactly $1.0$ to satisfy probability axioms:

$$\int_{0}^{\infty} \frac{1}{\lambda} e^{-x/\lambda} \, dx = 1$$

#### Step-by-Step Derivation:

1. **Factor out the constant value:**

$$\frac{1}{\lambda} \int_{0}^{\infty} e^{-x/\lambda} \, dx$$


2. **Integrate the exponential term using substitution rules:**

$$\frac{1}{\lambda} \left[ \frac{e^{-x/\lambda}}{-1/\lambda} \right]_{0}^{\infty} = \frac{1}{\lambda} \cdot (-\lambda) \Big[ e^{-x/\lambda} \Big]_{0}^{\infty} = - \Big[ e^{-x/\lambda} \Big]_{0}^{\infty}$$


3. **Evaluate the limits from $0$ to $\infty$:**

$$- \left( \lim_{x \to \infty} e^{-x/\lambda} - e^{-0/\lambda} \right) = - (0 - 1) = 1$$



---

### Proof 2: Deriving the Mean Expected Value $E(X) = \lambda$

By expected value definitions for continuous variables, $E(X) = \int_{0}^{\infty} x \cdot f(x) \, dx$:

$$E(X) = \int_{0}^{\infty} x \left( \frac{1}{\lambda} e^{-x/\lambda} \right) \, dx = \frac{1}{\lambda} \int_{0}^{\infty} x e^{-x/\lambda} \, dx$$

#### Step-by-Step Derivation:

1. **Apply Integration by Parts ($\int u \, dv = u v - \int v \, du$):**
* Let $u = x \implies du = dx$.
* Let $dv = e^{-x/\lambda} \, dx \implies v = -\lambda e^{-x/\lambda}$.


2. **Set up the expanded terms:**

$$\frac{1}{\lambda} \left( \Big[ x \cdot (-\lambda e^{-x/\lambda}) \Big]_{0}^{\infty} - \int_{0}^{\infty} (-\lambda e^{-x/\lambda}) \, dx \right)$$


$$\frac{1}{\lambda} \left( \Big[ -\lambda x e^{-x/\lambda} \Big]_{0}^{\infty} + \lambda \int_{0}^{\infty} e^{-x/\lambda} \, dx \right)$$


3. **Evaluate the boundary calculations:**
* For the first bracket: Using L'Hôpital's rule, $\lim_{x\to\infty} \frac{x}{e^{x/\lambda}} = 0$. At the lower limit $x=0$, the term evaluates to $0$. Thus, the entire first block disappears ($0$).
* For the second block: From our previous proof, we already know that $\int_{0}^{\infty} \frac{1}{\lambda} e^{-x/\lambda} \, dx = 1$, which means $\int_{0}^{\infty} e^{-x/\lambda} \, dx = \lambda$.


4. **Combine the results:**

$$E(X) = \frac{1}{\lambda} \left( 0 + \lambda \cdot \lambda \right) = \frac{\lambda^2}{\lambda} = \lambda$$



---

## 4. Text Graph: Exponential Decay Curve

The continuous exponential distribution exhibits a maximum value at $x=0$ and decays rapidly toward zero as $x$ increases toward infinity.

```text
 f(x)
   ^
1/λ|*
   |  *
   |    *
   |      * 
   |         *
 0 +------------*-----------------> x
   0

```

# Advanced Probability Distributions: Exponential & Normal Models

---

## 1. Concept: Exponential Distribution Variance & Application

The **Exponential Distribution** represents the continuous time intervals between independent Poisson events occurring at a constant average rate.

### Variance Formula
To find the variance $V(X)$ of an exponential distribution, we utilize the identity:
$$V(X) = E(X^2) - (E(X))^2$$

Given the probability density function (PDF):
$$f(x) = \frac{1}{\lambda}e^{-x/\lambda}$$

#### Step-by-Step Derivation of Variance:
1. **Set up the Expected Value of $X^2$:**
   $$E(X^2) = \int_{0}^{\infty} x^2 \frac{1}{\lambda} e^{-x/\lambda} \, dx = \frac{1}{\lambda} \int_{0}^{\infty} x^2 e^{-x/\lambda} \, dx$$
2. **Apply Integration by Parts (Successive/Tabular Method):**
   Integrating $x^2 e^{-x/\lambda}$ bounds it to:
   $$\frac{1}{\lambda} \left[ x^2 \frac{e^{-x/\lambda}}{-1/\lambda} - 2x \frac{e^{-x/\lambda}}{(1/\lambda)^2} + 2 \frac{e^{-x/\lambda}}{-(1/\lambda)^3} \right]_{0}^{\infty}$$
3. **Evaluate the Definite Integral Limits:**
   * At $x \to \infty$, the exponential decay forces all terms to $0$.
   * At the lower bound $x = 0$, only the final constant component remains:
   $$-2\lambda^2(0 - 1) = 2\lambda^2$$
4. **Compute Final Variance:**
   Since $E(X) = \lambda$, substitute these values back into the variance identity:
   $$V(X) = 2\lambda^2 - \lambda^2 = \lambda^2$$

---

### Practical Problem: Call Duration
**Statement:** The duration in minutes of a phone call follows the exponential distribution with $\lambda = 5$. Calculate the probability that a phone call exceeds 5 minutes.

#### Step-by-Step Solution:
1. **Identify Parameter:** $\lambda = 5$.
2. **Set Up the Definite Integral for $P(X \ge 5)$:**
   $$P(X \ge 5) = \int_{5}^{\infty} \frac{1}{5} e^{-x/5} \, dx$$
3. **Integrate:**
   $$\frac{1}{5} \left[ \frac{e^{-x/5}}{-1/5} \right]_{5}^{\infty} = - \left[ e^{-x/5} \right]_{5}^{\infty}$$
4. **Evaluate Boundaries:**
   $$- (0 - e^{-5/5}) = -(-e^{-1}) = \frac{1}{e} \approx 0.3679$$

---

## 2. Concept: Normal (Gaussian) Distribution

The **Normal Distribution** is a continuous probability distribution that forms a symmetric, bell-shaped curve around its central parameter. It describes how values of a variable are distributed around its mean.

### Probability Density Function (PDF):
$$f(x) = \frac{1}{\sqrt{2\pi}\sigma} \exp\left[ -\frac{1}{2} \left( \frac{x - \mu}{\sigma} \right)^2 \right]$$
* Domain: $-\infty < x < \infty$, $-\infty < \mu < \infty$, $\sigma > 0$.
* Key Parameters: Mean $E[X] = \mu$, Variance $V[X] = \sigma^2$.

---

### Standardizing a Normal Distribution
To simplify operations, any normal variable $X \sim N(\mu, \sigma^2)$ can be transformed into a **Standard Normal Variable** $Z \sim N(0, 1)$ via the substitution:
$$Z = \frac{X - \mu}{\sigma}$$

This compresses the complex distribution density formula down to:
$$f(z) = \frac{1}{\sqrt{2\pi}} \exp\left( -\frac{z^2}{2} \right)$$

---

## 3. Deriving Properties of the Standard Normal Distribution

### Derivation 1: Expected Value $E(Z) = 0$
$$E(Z) = \int_{-\infty}^{\infty} z f(z) \, dz = \int_{-\infty}^{\infty} z \frac{1}{\sqrt{2\pi}} e^{-z^2/2} \, dz$$
* **Simple Meaning:** Because $z$ is an odd function and $e^{-z^2/2}$ is perfectly symmetric (even), the negative half explicitly cancels out the positive half, leaving a total balance of $0$.

### Derivation 2: Expected Value of $Z^2$ using Gamma Functions
$$E(Z^2) = \int_{-\infty}^{\infty} z^2 \frac{1}{\sqrt{2\pi}} e^{-z^2/2} \, dz$$

#### Step-by-Step Calculation:
1. **Convert to a single-sided interval using symmetry:**
   $$E(Z^2) = \frac{2}{\sqrt{2\pi}} \int_{0}^{\infty} z^2 e^{-z^2/2} \, dz$$
2. **Apply variable substitution:** Let $t = \frac{z^2}{2} \implies z = \sqrt{2t}$ and $dz = \sqrt{2} \cdot \frac{1}{2} t^{-1/2} \, dt$.
3. **Substitute values into the integral expression:**
   $$E(Z^2) = \frac{\sqrt{2}}{\sqrt{\pi}} \int_{0}^{\infty} 2t e^{-t} \frac{1}{\sqrt{2}} t^{-1/2} \, dt = \frac{1}{\sqrt{\pi}} \times 2 \int_{0}^{\infty} t^{1/2} e^{-t} \, dt$$
4. **Identify the Gamma Function relationship ($\Gamma(n) = \int_{0}^{\infty} t^{n-1}e^{-t}dt$):**
   $$E(Z^2) = \frac{2}{\sqrt{\pi}} \Gamma\left(\frac{3}{2}\right)$$
5. **Evaluate using the property $\Gamma(n+1) = n\Gamma(n)$ where $\Gamma(\frac{1}{2}) = \sqrt{\pi}$:**
   $$E(Z^2) = \frac{2}{\sqrt{\pi}} \cdot \left(\frac{1}{2}\sqrt{\pi}\right) = 1$$
6. **Calculate Variance:**
   $$V(X) = E(Z^2) - (E(Z))^2 = 1 - 0 = 1$$

---

## 4. Text-Based Graph: Standard Normal Curve $N(0, 1)$

The standard normal curve is perfectly symmetrical, peaking precisely at its mean ($Z=0$).

```text
 Probability Density f(z)
   ^
0.4|          .---.            <- Peak at Z = 0
   |         /     \
0.2|        /       \
   |       /         \
0.0 +----+----+----+----+----+---> Z Value
        -2   -1    0    1    2

```

---

## 5. Additional Practice Problem

### Problem: Calculating Lifespan Proportions

A critical component in a network router has a functional lifetime that is normally distributed with a mean $\mu = 1000$ hours and standard deviation $\sigma = 100$ hours. Find the $Z$-score for a component that lasts exactly 1150 hours.

#### Step-by-Step Calculation:

1. **Identify Parameters:**
* Mean ($\mu$) = 1000
* Standard Deviation ($\sigma$) = 100
* Target value ($X$) = 1150


2. **Apply the Transformation Formula:**

$$Z = \frac{X - \mu}{\sigma}$$


3. **Compute Value:**

$$Z = \frac{1150 - 1000}{100} = \frac{150}{100} = 1.5$$



**Answer:** The component's lifetime sits exactly $1.5$ standard deviations above the average population mean.


# Probability & Statistics: Normal (Gaussian) Distribution Notes

---

## 1. Concept Introduction: Normal (Gaussian) Distribution

The **Normal Distribution** (also known as the **Gaussian Distribution**) is the most crucial continuous probability distribution in statistics. It models real-world variables that cluster symmetrically around a central value, tapering off gradually in both directions to form a distinct **bell-shaped curve**.

### Formal Definition
A continuous random variable $X$ follows a normal distribution, denoted as $X \sim N(\mu, \sigma^2)$, if its probability density function (pdf) is given by:

$$f(x) = \frac{1}{\sqrt{2\pi}\sigma} \exp\left[ -\frac{1}{2}\left(\frac{x - \mu}{\sigma}\right)^2 \right]$$

Where the constraints and parameters are defined as:
*   $\sigma > 0$ (Standard Deviation)
*   $-\infty < x < \infty$ (Domain of the variable)
*   $-\infty < \mu < \infty$ (Mean or center location)

### Fundamental Metrics
*   **Mean (Expected Value):** $E[X] = \mu$
*   **Variance:** $V[X] = \sigma^2$

---

## 2. Standardizing a Normal Distribution (Z-Score)

Because the parameters $\mu$ and $\sigma$ vary from one dataset to another, we convert raw scores into standard units to calculate exact probabilities easily. This process is called **Standardization**.

### The Transformation Formula
Any normal variable $X$ can be transformed into a **Standard Normal Variable** $Z \sim N(0, 1)$ using:

$$Z = \frac{X - \mu}{\sigma}$$

*   **Simple Meaning:** The $Z$-score indicates exactly how many standard deviations a value $X$ lies away from the mean ($\mu$). 
*   If $Z$ is positive, the value is above average. If $Z$ is negative, it is below average.

---

## 3. Text-Based Graph: Standard Normal Curve & Sub-Interval Area

The curve is completely symmetric around $Z = 0$. When calculating a probability between two boundaries like $P(a \le Z \le b)$, we are computing the exact geometric area under the curve between those points.

```text
              Probability Density f(z)
                        ^
                       / \
                      /   \
                     /|   |\
                    / |   | \
                   /  |///|  \        Shaded Area = Target Probability
                  /   |///|   \       Interval: [a, b]
  ---------------+----+---+----+-------+-----> Z-score Value
                -2    a   0    b       2

```

---

## 4. Lecture Problem Walkthrough

### Problem Statement

The time required to assemble a piece of machinery is a random variable having a normal distribution with a mean of 12 minutes and a standard deviation of 2 minutes. What is the probability that the assembly of a piece of machinery of this kind will take anywhere from 11 to 14 minutes?

*(Given data: $P[Z < 1] = 0.8413$ and $P[Z < -1/2] = 0.3805$)*

---

### Step-by-Step Calculation:

#### Step 1: Extract Given Parameters

* Mean ($\mu$) = 12 minutes
* Standard Deviation ($\sigma$) = 2 minutes
* Target Range: $11 \le X < 14$

#### Step 2: Set up the Standardization Equation

Using $Z = \frac{X - 12}{2}$, we transform the raw boundary values ($X = 11$ and $X = 14$) into standardized $Z$-scores.

* **For the Lower Bound ($X = 11$):**

$$Z_{\text{lower}} = \frac{11 - 12}{2} = \frac{-1}{2} = -0.5$$


* **For the Upper Bound ($X = 14$):**

$$Z_{\text{upper}} = \frac{14 - 12}{2} = \frac{2}{2} = 1$$



#### Step 3: Rewrite the Probability in Terms of $Z$

$$P(11 \le X < 14) = P\left(-\frac{1}{2} \le Z < 1\right)$$

#### Step 4: Split Using Cumulative Densities

To find the area between two boundaries, take the total area up to the upper limit and subtract the area below the lower limit:


$$P\left(-\frac{1}{2} \le Z < 1\right) = P(Z < 1) - P\left(Z < -\frac{1}{2}\right)$$

#### Step 5: Substitute Cumulative Values and Evaluate

Substitute the given values into the equation:


$$P(11 \le X < 14) = 0.8413 - 0.3805$$

$$P(11 \le X < 14) = 0.4608$$

**Simple Meaning of Answer:** There is a **46.08%** chance that assembling this piece of machinery will take between 11 and 14 minutes.

---

## 5. Additional Practice Problem

### Problem Statement

An automated bottling plant fills soda bottles. The volume of soda per bottle follows a normal distribution with a mean $\mu = 500$ mL and a standard deviation $\sigma = 5$ mL. Find the probability that a randomly selected bottle contains less than 490 mL of soda.

*(Given standard values: $P[Z < -2] = 0.0228$)*

### Step-by-Step Calculation:

1. **Identify parameters:**
* $\mu = 500$
* $\sigma = 5$
* Target: $P(X < 490)$


2. **Standardize the target value:**

$$Z = \frac{490 - 500}{5} = \frac{-10}{5} = -2$$


3. **Determine cumulative probability:**

$$P(X < 490) = P(Z < -2)$$


$$P(Z < -2) = 0.0228$$



**Answer:** There is a **2.28%** probability that a bottle contains less than 490 mL of soda.
