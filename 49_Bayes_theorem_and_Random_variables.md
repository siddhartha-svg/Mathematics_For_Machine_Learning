# Probability Theory: Bayes' Theorem

---

## 1. Concept Introduction: Bayes' Theorem

### Simple Meaning
**Bayes' Theorem** is a method used to find the probability of a specific cause or background scenario ($E_i$), given that a particular result or event ($A$) has already occurred. It allows us to work backward from an observed outcome to find the most likely starting point. It is often referred to as finding the **posterior probability** (reverse probability).

### The Mathematical Formula
If the events $\{E_1, E_2, \dots, E_n\}$ form a complete partition of a sample space $S$ (meaning they are mutually exclusive and collectively cover all possibilities), and $A$ is an observed event with a non-zero probability, then:

$$P(E_i \mid A) = \frac{P(E_i \cap A)}{P(A)} = \frac{P(E_i)P(A \mid E_i)}{\sum_{j=1}^{n} P(E_j)P(A \mid E_j)}$$

* **Numerator:** The probability of picking a specific pathway $E_i$ and the event $A$ happening along that path.
* **Denominator:** The **Total Probability** of event $A$ happening across all possible paths combined.

---

## 2. 📝 Step-by-Step Textbook Problem

### Problem Statement
Given 3 identical boxes (I, II, and III), each containing 3 coins:
* **Box I** contains 3 gold coins ($3G$).
* **Box II** contains 2 gold coins and 1 silver coin ($2G + 1S$).
* **Box III** contains 1 gold coin and 2 silver coins ($1G + 2S$).

A person chooses a box at random and takes out a coin. If the drawn coin turns out to be **gold**, what is the probability that it was drawn specifically from **Box III**?

---

## 3. Step-by-Step Explanation & Calculations

### Step 1: Define the Events
Let's name our pathways and outcomes clearly:
* $E_1$: The event of choosing **Box I**.
* $E_2$: The event of choosing **Box II**.
* $E_3$: The event of choosing **Box III**.
* $A$: The observed event of drawing a **gold coin**.

### Step 2: Calculate the Prior Box Selection Probabilities
Since all three boxes are identical and one is chosen purely at random, each box has an equal chance of being picked:
$$P(E_1) = \frac{1}{3}, \quad P(E_2) = \frac{1}{3}, \quad P(E_3) = \frac{1}{3}$$

### Step 3: Find the Conditional Probabilities of Getting a Gold Coin from Each Box
Now look inside each box individually and calculate the probability of picking a gold coin:
* **From Box I ($3G$ out of 3 total coins):**  
  $$P(A \mid E_1) = \frac{3}{3} = 1$$
* **From Box II ($2G$ out of 3 total coins):**  
  $$P(A \mid E_2) = \frac{2}{3}$$
* **From Box III ($1G$ out of 3 total coins):**  
  $$P(A \mid E_3) = \frac{1}{3}$$

### Step 4: Apply Bayes' Theorem Formula
We want to find $P(E_3 \mid A)$, the probability that we chose Box III given that the coin is gold:
$$P(E_3 \mid A) = \frac{P(E_3)P(A \mid E_3)}{P(E_1)P(A \mid E_1) + P(E_2)P(A \mid E_2) + P(E_3)P(A \mid E_3)}$$

### Step 5: Substitute the Values & Solve

* **Calculate the Numerator (Path III):**
  $$\text{Numerator} = P(E_3) \times P(A \mid E_3) = \frac{1}{3} \times \frac{1}{3} = \frac{1}{9}$$

* **Calculate the Denominator (Total Probability of getting a Gold Coin):**
  $$\text{Denominator} = \left(\frac{1}{3} \times 1\right) + \left(\frac{1}{3} \times \frac{2}{3}\right) + \left(\frac{1}{3} \times \frac{1}{3}\right)$$
  $$\text{Denominator} = \frac{1}{3} + \frac{2}{9} + \frac{1}{9}$$
  Convert $\frac{1}{3}$ to have a common denominator of 9:
  $$\text{Denominator} = \frac{3}{9} + \frac{2}{9} + \frac{1}{9} = \frac{6}{9}$$

* **Perform Final Division:**
  $$P(E_3 \mid A) = \frac{\frac{1}{9}}{\frac{6}{9}}$$
  Cancel out the identical denominators (9):
  $$P(E_3 \mid A) = \frac{1}{6}$$

### Solution
The probability that the gold coin came from Box III is **$\frac{1}{6}$** (or approx. **$16.67\%$**).

---

## 4. 📊 Conceptual Tree Graph Diagram

This text-based branch chart shows how the choice breaks down sequentially from picking a box down to drawing the target gold coin:

```text
                      [ Start Selection ]
                               |
         +---------------------+---------------------+
         | (Choose Box)        | (Choose Box)        | (Choose Box)
         v                     v                     v
    [ Box I ]             [ Box II ]            [ Box III ]
    P(E1) = 1/3           P(E2) = 1/3           P(E3) = 1/3
         |                     |                     |
         | (Draw Coin)         | (Draw Coin)         | (Draw Coin)
         v                     v                     v
   Gold Coin (G)         Gold Coin (G)         Gold Coin (G)  <-- (Observed Event A)
   P(A|E1) = 3/3 = 1     P(A|E2) = 2/3         P(A|E3) = 1/3
         |                     |                     |
         v                     v                     v
   Path 1 Product        Path 2 Product        Path 3 Product [TARGET]
    1/3 * 1 = 3/9         1/3 * 2/3 = 2/9       1/3 * 1/3 = 1/9
         |                     |                     |
         +---------------------+---------------------+
                               |
                               v
                     Sum of All Gold Paths
                  3/9 + 2/9 + 1/9 = 6/9 (Total A)
                               |
                               v
                 Bayes' Reverse Ratio Result:
                   Target Path / Total Area
                     (1/9) / (6/9) = 1/6
```

# Probability Theory: Random Variables & Distribution Functions

---

## 1. Concept: Introduction to Random Variables

### Simple Meaning
A **Random Variable** is not a regular single-value variable, but a mathematical rule (a function) that maps every real-world outcome of a random experiment to a real number. 
* It assigns a clear numeric value to situations full of uncertainty.
* **Formal Definition:** A random variable is a function $X : S \longrightarrow \mathbb{R}$, where $S$ is the sample space and $\mathbb{R}$ represents the set of real numbers.
* **Notation:** $P(X = x) = P(\{s \in S : X(s) = x\})$  
  *(Read as: The probability that the variable $X$ equals a specific value $x$ is the probability of all outcomes in the sample space that map to $x$.)*

---

### 📝 Step-by-Step Practical Problem: Tossing Two Coins

**Concept Name: Discrete Probability Distribution Mapping**

**Problem:** Two fair coins are tossed simultaneously. Let the random variable $X$ represent the **number of heads obtained**. Construct the probability distribution table for $X$.

**Step-by-Step Calculation:**
1. **Find the full Sample Space ($S$):** 
   Tossing two coins yields 4 possible outcomes:
   $$S = \{HH, HT, TH, TT\}$$
   Total number of elements: $n(S) = 4$.

2. **Map out the values that $X$ can take (Range):**
   * Outcome $TT$: 0 heads $\implies X = 0$
   * Outcome $HT$: 1 head $\implies X = 1$
   * Outcome $TH$: 1 head $\implies X = 1$
   * Outcome $HH$: 2 heads $\implies X = 2$
   Therefore, the range of $X$ is $X(S) = \{0, 1, 2\}$.

3. **Calculate the Probability for each $X = x$:**
   * **For $X = 0$:** Only 1 outcome $\{TT\}$.
     $$P(X = 0) = \frac{1}{4}$$
   * **For $X = 1$:** There are 2 outcomes $\{HT, TH\}$.
     $$P(X = 1) = \frac{2}{4}$$
   * **For $X = 2$:** Only 1 outcome $\{HH\}$.
     $$P(X = 2) = \frac{1}{4}$$

**Solution Table:**
| $X$ | 0 | 1 | 2 |
| :--- | :---: | :---: | :---: |
| **$P(X)$** | $\frac{1}{4}$ | $\frac{2}{4}$ | $\frac{1}{4}$ |

---

## 2. Concept: Advanced Discrete Variable - Rolling Two Dice

**Concept Name: Sum Distribution of Independent Variables**

**Problem:** Two six-sided fair dice are rolled simultaneously. Let the random variable $X$ represent the **sum of the values obtained** on the two dice faces. Derive the probability mass function.

**Step-by-Step Calculation:**
1. **Determine the total outcomes:** Each die has 6 faces, so $6 \times 6 = 36$ total outcomes. $n(S) = 36$.
2. **Find the range of $X$:** The lowest possible sum is $1+1 = 2$. The highest sum is $6+6 = 12$. 
   $$X(S) = \{2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12\}$$
3. **Calculate specific frequencies systematically:**
   * **Sum = 2:** $\{(1,1)\} \implies 1$ way $\implies P(X=2) = \frac{1}{36}$
   * **Sum = 3:** $\{(1,2), (2,1)\} \implies 2$ ways $\implies P(X=3) = \frac{2}{36}$
   * **Sum = 4:** $\{(1,3), (2,2), (3,1)\} \implies 3$ ways $\implies P(X=4) = \frac{3}{36}$
   * **Sum = 7:** $\{(1,6), (2,5), (3,4), (4,3), (5,2), (6,1)\} \implies 6$ ways $\implies P(X=7) = \frac{6}{36}$
   * **Sum = 12:** $\{(6,6)\} \implies 1$ way $\implies P(X=12) = \frac{1}{36}$

### 📊 Probability Mass Function (pmf) Line Plot
Below is a text graph showing the symmetrical rise and fall of probabilities based on the sum value:

```text
Probability
  6/36 |              *
  5/36 |            *   *
  4/36 |          *       *
  3/36 |        *           *
  2/36 |      *               *
  1/36 |    *                   *
       +----------------------------
  X =       2 3 4 5 6 7 8 9 10 11 12 (Sum Value)

```

---

## 3. Types of Random Variables

Random variables are classified into two broad categories depending on the nature of their numerical range:

### A. Discrete Random Variables

* **Simple Meaning:** A random variable where you can count the possible values individually (like steps on a ladder, e.g., number of cars, coin flips).
* **Specified by:** **Probability Mass Function (pmf)**, denoted as $f_X(x)$.
* **Core Rules:**
1. The probability of any value must never be negative:

$$f_X(x) \ge 0, \quad \forall x \in X(S)$$


2. The sum of all individual probabilities must equal exactly 1:

$$\sum_{x \in X(S)} f_X(x) = 1$$





### B. Continuous Random Variables

* **Simple Meaning:** A random variable that can take any value within a continuous range or interval (like measurements, e.g., temperature, height, precise time duration). You cannot list the individual values because they are infinite and uncountable.
* **Specified by:** **Probability Density Function (pdf)**, denoted as $f_X(x)$.
* **Core Rules:**
1. The density function line must stay above or on the x-axis:

$$f_X(x) \ge 0, \quad \forall x \in X(S)$$


2. The total area underneath the continuous density curve must equal exactly 1:

$$\int_{-\infty}^{\infty} f_X(x) \, dx = 1$$





---

## 4. 📝 Practice Problems with Solutions

### Problem 1: Verifying a Discrete pmf Function

A discrete random variable $X$ has a probability mass function given by $f_X(x) = kx$ for $X = \{1, 2, 3, 4\}$. Find the value of the constant $k$.

**Step-by-Step Calculation:**

1. **Apply the total probability rule:** The sum of all probabilities must equal 1.

$$\sum f_X(x) = f_X(1) + f_X(2) + f_X(3) + f_X(4) = 1$$


2. **Substitute the function rule ($kx$):**

$$k(1) + k(2) + k(3) + k(4) = 1$$


3. **Factor out $k$ and add the integers:**

$$k(1 + 2 + 3 + 4) = 1$$


$$10k = 1$$


4. **Isolate $k$:**

$$k = \frac{1}{10}$$



**Solution:**

$$k = 0.1$$

---

### Problem 2: Verifying a Continuous pdf Curve

A continuous random variable $X$ has a probability density function defined by $f_X(x) = c(2x)$ over the interval $x \in [0, 2]$, and $f_X(x) = 0$ everywhere else. Find the constant value $c$.

**Step-by-Step Calculation:**

1. **Apply the continuous area rule:** The definite integral across the boundaries must equal 1.

$$\int_{0}^{2} c(2x) \, dx = 1$$


2. **Move the constants outside and perform integration:**
Recall the basic rule $\int x \, dx = \frac{x^2}{2}$.

$$2c \left[ \frac{x^2}{2} \right]_{0}^{2} = 1 \implies c \left[ x^2 \right]_{0}^{2} = 1$$


3. **Evaluate the limits (Upper - Lower):**

$$c(2^2 - 0^2) = 1$$


$$4c = 1$$


4. **Solve for $c$:**

$$c = \frac{1}{4}$$



**Solution:**

$$c = 0.25$$


# Advanced Probability Theory: Discrete pmf and Cumulative Distribution Functions (CDF)

---

## 1. Concept: Discrete Random Variables and Probability Mass Function (pmf)

### Simple Meaning
A **Discrete Random Variable** is a variable that takes on separate, countable values (like $0, 1, 2, \dots$) with a specific probability assigned to each. The rule that gives the probability for each individual value is called the **Probability Mass Function (pmf)**.

### Rules a pmf Must Follow:
1. All individual probabilities must be greater than or equal to zero (no negative probabilities):
   $$f_X(x) \geq 0, \quad \forall x \in X(S)$$
2. The sum of all probabilities across the entire range must equal exactly 1 (100% total probability):
   $$\sum_{x \in X(S)} f_X(x) = 1$$

---

## 2. Concept: Cumulative Distribution Function (CDF)

### Simple Meaning
The **Cumulative Distribution Function (CDF)**, written as $F_X(x)$, computes the total accumulated probability from the very beginning up to a specific point $x$. Instead of asking "What is the probability of getting exactly $x$?", it answers "What is the probability of getting a value less than or equal to $x$?".

### Fundamental Formulas

Depending on whether the random variable is continuous or discrete, the CDF is calculated differently:

$$F_X(x) = P(X \leq x) = \begin{cases} \int_{-\infty}^{x} f_X(t)dt, & \text{if } X \text{ is continuous} \\ \sum_{y \leq x} f_X(y), & \text{if } X \text{ is discrete} \end{cases}$$

### Key Mathematical Relationships
* **Finding Interval Probabilities:** To find the probability between two values $a$ and $b$, subtract the CDF value at $a$ from the CDF value at $b$:
  $$P(a \leq X \leq b) = F_X(b) - F_X(a)$$
* **Finding individual pmf from CDF (Discrete):** 
  $$f_X(x) = F_X(x) - F_X(x^-)$$
* **Finding density function from CDF (Continuous):** The derivative of the cumulative function gives back the baseline probability density function:
  $$f_X(x) = \frac{d}{dx}F_X(x)$$

---

## 3. 📝 Step-by-Step Problems with Solutions

### Problem 1: Discrete CDF & Interval Calculations
A discrete random variable $X$ has the following probability mass function (pmf):
* $f_X(1) = 0.2$
* $f_X(2) = 0.3$
* $f_X(3) = 0.5$

1. Find the cumulative distribution function $F_X(x)$ for all values.
2. Calculate the probability $P(1 < X \leq 3)$.

#### Step-by-Step Calculation:
1. **Find $F_X(x)$ by accumulating probabilities:**
   * For $x = 1$: 
     $$F_X(1) = P(X \leq 1) = f_X(1) = 0.2$$
   * For $x = 2$: 
     $$F_X(2) = P(X \leq 2) = f_X(1) + f_X(2) = 0.2 + 0.3 = 0.5$$
   * For $x = 3$: 
     $$F_X(3) = P(X \leq 3) = F_X(2) + f_X(3) = 0.5 + 0.5 = 1.0$$

2. **Calculate the interval probability $P(1 < X \leq 3)$:**
   Using the formula $P(a < X \leq b) = F_X(b) - F_X(a)$:
   $$P(1 < X \leq 3) = F_X(3) - F_X(1)$$
   $$P(1 < X \leq 3) = 1.0 - 0.2 = 0.8$$

**Solution:**
* $F_X(x) = 0.2$ for $1 \leq x < 2$; $0.5$ for $2 \leq x < 3$; $1.0$ for $x \geq 3$.
* $P(1 < X \leq 3) = 0.8$

---

### Problem 2: Continuous CDF and Derivation
A continuous random variable $X$ has a CDF defined as:
$$F_X(x) = \begin{cases} 0, & x < 0 \\ \frac{x^2}{4}, & 0 \leq x \leq 2 \\ 1, & x > 2 \end{cases}$$

Find the probability density function $f_X(x)$ within the interval $[0, 2]$.

#### Step-by-Step Calculation:
1. **Apply the derivative rule:** For continuous variables, $f_X(x) = \frac{d}{dx}F_X(x)$.
2. **Differentiate the function:**
   $$\frac{d}{dx}\left(\frac{x^2}{4}\right) = \frac{1}{4} \cdot \frac{d}{dx}(x^2) = \frac{1}{4} \cdot 2x = \frac{x}{2}$$

**Solution:**
$$f_X(x) = \begin{cases} \frac{x}{2}, & 0 \leq x \leq 2 \\ 0, & \text{otherwise} \end{cases}$$

---

## 4. 📊 Graphical Representations

### Continuous Distribution Curve & CDF Area
For a continuous function, $F_X(x)$ calculates the total area under the density curve starting from $-\infty$ up to the threshold point $x$:

```text
               Probability Density Function f(x)
                           
                             ***
                          *  |||  *
                        *    |||    *
                      *      |||      *
                    *        |||        *
         ----------*---------|||---------*-----------> x Axis
                             x
         \____________________/
                   |
       Shaded Area (///) = F_X(x) = P(X <= x)

```

### Discrete Step-Function CDF Graph

Because discrete variables update instantly when hitting a new integer, their cumulative graphs form a step-like structure:

```text
Probability F(x)
  1.0 |                               +---------
      |                               |
  0.5 |               +-------o-------+
      |               |
  0.2 |       +-------o
      |       |
      +-------+-------+-------+-------+---------> x Axis
              0       1       2       3

```


# Probability Theory: Discrete and Continuous Distributions

---

## 1. Concept: Discrete Random Variables (Binomial Approach)

### Simple Meaning
When an experiment has separate, distinct outcomes (like counting coin flips), we use a **Discrete Random Variable**. 
* **Probability Mass Function (pmf):** Gives the exact probability for each individual outcome $X = x$.
* **Cumulative Distribution Function (cdf):** Denoted as $F_X(x)$, it accumulates the probabilities up to a certain point ($P(X \le x)$).

---

### 📝 Problem 1: Step-by-Step Solution

**Problem Statement:** A coin is known to come up heads three times as often as tails. This coin is tossed three times. Let $X$ denote the number of tails that appear. Determine the pmf and cdf of $X$. Find $P(1 \le X < 2)$.

#### Step 1: Calculate Individual Probabilities
Let the probability of getting a tail be $P(T) = p$. Since heads appear 3 times as often:
$$P(H) = 3p$$

Because the total probability of all outcomes must equal 1:
$$P(H) + P(T) = 1 \implies 3p + p = 1 \implies 4p = 1 \implies p = \frac{1}{4}$$

Thus, we have:
* **Probability of Tail:** $P(T) = \frac{1}{4}$
* **Probability of Head:** $P(H) = \frac{3}{4}$

#### Step 2: Compute the pmf using the Binomial Formula
The general formula to find the probability of getting $x$ tails in 3 trials is:
$$P(X = x) = \binom{3}{x} \cdot [P(T)]^x \cdot [P(H)]^{3-x}$$

Let's compute the value for each possible number of tails ($x = 0, 1, 2, 3$):

* **For $X = 0$ (Zero Tails):**
  $$x_1 = P(X = 0) = \binom{3}{0}\left(\frac{3}{4}\right)^3\left(\frac{1}{4}\right)^0 = 1 \cdot \frac{27}{64} \cdot 1 = \frac{27}{64}$$

* **For $X = 1$ (One Tail):**
  $$x_2 = P(X = 1) = \binom{3}{1}\left(\frac{3}{4}\right)^2\left(\frac{1}{4}\right)^1 = 3 \cdot \frac{9}{16} \cdot \frac{1}{4} = \frac{27}{64}$$

* **For $X = 2$ (Two Tails):**
  $$x_3 = P(X = 2) = \binom{3}{2}\left(\frac{3}{4}\right)^1\left(\frac{1}{4}\right)^2 = 3 \cdot \frac{3}{4} \cdot \frac{1}{16} = \frac{9}{64}$$

* **For $X = 3$ (Three Tails):**
  $$x_4 = P(X = 3) = \binom{3}{3}\left(\frac{1}{4}\right)^3 = 1 \cdot \frac{1}{64} = \frac{1}{64}$$

*(Self-Check Validation: $x_1 + x_2 + x_3 + x_4 = \frac{27+27+9+1}{64} = \frac{64}{64} = 1$)*

#### Step 3: Construct the cdf ($F_X(x)$)
The cumulative distribution function builds up step-by-step:
* For $x < 0$: $F_X(x) = 0$
* For $0 \le x < 1$: $F_X(x) = x_1 = \frac{27}{64}$
* For $1 \le x < 2$: $F_X(x) = x_1 + x_2 = \frac{27}{64} + \frac{27}{64} = \frac{54}{64}$
* For $2 \le x < 3$: $F_X(x) = x_1 + x_2 + x_3 = \frac{54}{64} + \frac{9}{64} = \frac{63}{64}$
* For $x \ge 3$: $F_X(x) = 1$

$$F_X(x) = \begin{cases} 0, & x < 0 \\ \frac{27}{64}, & 0 \le x < 1 \\ \frac{27}{32}, & 1 \le x < 2 \\ \frac{63}{64}, & 2 \le x < 3 \\ 1, & x \ge 3 \end{cases}$$

#### Step 4: Calculate $P(1 \le X < 2)$
Because $X$ is a discrete variable, the only integer that satisfies the inequality $1 \le X < 2$ is $X = 1$.
$$P(1 \le X < 2) = P(X = 1) = \frac{27}{64}$$

---

### 📊 Discrete Step Function Graph (cdf)

Discrete cumulative functions present visually as flat steps with jump breaks at individual integer thresholds:

```text
 Probability F(x)
  1.0  |                                       +------
       |                                       |
 63/64 |                       +-------o-------+
       |                       |
 27/32 |       +-------o-------+
       |       |
 27/64 |-------+
       |
       +-------+-------+-------+-------+---------> x Axis
               0       1       2       3

```

---

---

## 2. Concept: Continuous Random Variables

### Simple Meaning

When values are measured continuously along an unbroken interval (like height, distance, or time), we use a **Continuous Random Variable**.

* **Probability Density Function (pdf):** Written as $f(x)$, it defines the shape of the continuous distribution curve.
* **Total Area Property:** The entire area under a valid continuous pdf curve over all possible space **must** equal exactly 1.
* **Finding the cdf:** Calculated by integrating the density function from the absolute lower bound up to variable point $x$.

---

### 📝 Problem 2: Step-by-Step Solution

**Problem Statement:** Suppose a continuous random variable $X$ has pdf:


$$f(x) = \begin{cases} kx^2, & 0 < x < 1 \\ 0, & \text{elsewhere} \end{cases}$$


where $k$ is a suitable constant. Determine the cdf of $X$.

#### Step 1: Solve for the Constant Value $k$

Using the total area rule under the density function curve:


$$\int_{-\infty}^{\infty} f(x) \, dx = 1 \implies \int_{0}^{1} k x^2 \, dx = 1$$

Perform the integration using the power rule ($\int x^2 \, dx = \frac{x^3}{3}$):


$$k \left[ \frac{x^3}{3} \right]_{0}^{1} = 1$$

Apply the integration boundaries (Upper - Lower):


$$k \left( \frac{1^3}{3} - \frac{0^3}{3} \right) = 1 \implies k \left( \frac{1}{3} \right) = 1 \implies k = 3$$

Therefore, the fully updated density function is:


$$f(x) = \begin{cases} 3x^2, & 0 < x < 1 \\ 0, & \text{otherwise} \end{cases}$$

#### Step 2: Integrate to find the cdf ($F_X(x)$)

The cdf is found by accumulating density from the start of the valid domain ($x = 0$) up to our current evaluation coordinate $x$:


$$F_X(x) = \int_{0}^{x} 3t^2 \, dt$$

Perform the definite calculus integration:


$$F_X(x) = 3 \left[ \frac{t^3}{3} \right]_{0}^{x} = 3 \left( \frac{x^3}{3} - 0 \right) = x^3$$

#### Step 3: Write the Final Piecewise cdf Output

Organizing the integration solutions across all possible numeric domains yields the clean piecewise continuous output function:

$$F_X(x) = \begin{cases} 0, & x \le 0 \\ x^3, & 0 < x < 1 \\ 1, & x \ge 1 \end{cases}$$

---

### 📊 Continuous Variable Graph (pdf vs cdf)

This text diagram showcases the behavior comparison of the continuous parabolic density distribution curve against the rising cubic cumulative output profile:

```text
   [ Density Curve f(x) = 3x^2 ]          [ Cumulative Curve F(x) = x^3 ]
  3.0 |          *                         1.0 |              *--------
      |         *                              |            *
      |        *                               |          *
      |       *                                |        *
  0.0 +-------*---------> x Axis           0.0 +-------*---------> x Axis
      0       1                                0       1

```

