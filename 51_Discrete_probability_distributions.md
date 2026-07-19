# Probability & Statistics: Discrete Probability Distributions

---

## 1. Fundamental Concepts: Expected Value & Variance

### What is Expected Value $E(X)$?
The **Expected Value** represents the long-term average or mean value of a random variable if we were to repeat an experiment infinitely many times. It acts as the "center of mass" of the distribution.

Depending on the type of random variable, it is calculated in two ways:

1. **For Discrete Random Variables:** Sum of all possible values multiplied by their respective probabilities.
   $$E(X) = \sum_{x} x \cdot f(x)$$

2. **For Continuous Random Variables:** The integral over all possible values.
   $$E(X) = \int_{-\infty}^{\infty} x \cdot f(x) \, dx$$

### What is Variance $V(X)$?
**Variance** measures the spread of the random variable's values around its mean (Expected Value). A higher variance means data points are spread further out.

* **Formula:**
  $$V(X) = E(X^2) - [E(X)]^2$$

---

## 2. Bernoulli Trials

A series of experiments or trials are called **Bernoulli Trials** if they satisfy these 4 strict assumptions:
1. **Two Outcomes:** Each trial has exactly two possible outcomes: **Success** ($p$) or **Failure** ($q = 1 - p$).
2. **Constant Probability:** The probability of success ($p$) remains the same for every single trial.
3. **Independence:** The outcome of one trial does not affect the outcome of another.
4. **Finite Trials:** There is a fixed, countable number of trials ($n$).

---

## 3. Binomial Distribution

If you perform $n$ independent Bernoulli trials, the random variable $X$ (which counts the total number of successes) follows a **Binomial Distribution**: 
$$X \sim b(n, p)$$

### Probability Mass Function (PMF)
The probability of getting exactly $x$ successes in $n$ trials is given by:
$$f(x) = P(X = x) = \binom{n}{x} p^x q^{n-x}$$

Where:
* $\binom{n}{x} = \frac{n!}{x!(n-x)!}$ (Number of ways to arrange $x$ successes in $n$ trials)
* $p$ = Probability of success
* $q = 1 - p$ = Probability of failure
* $x = 0, 1, 2, \dots, n$

### Key Properties
1. $f(x) \geq 0$ for all $x$.
2. Total probability sums to 1: 
   $$\sum_{x=0}^{n} \binom{n}{x} p^x q^{n-x} = (p + q)^n = (1)^n = 1$$

### Derived Metrics
* **Mean (Expected Value):** $E(X) = np$
* **Variance:** $V(X) = np(1 - p) = npq$

---

## 4. Mathematical Proof: Mean of a Binomial Distribution

We can derive $E(X) = np$ using the algebraic trick of differentiation on the Binomial Theorem identity.

### Step-by-Step Proof:

1. **Start with the Binomial Identity:**
   $$(p + q)^n = \sum_{x=0}^{n} \binom{n}{x} p^x q^{n-x}$$

2. **Differentiate both sides with respect to $p$:**
   $$\frac{d}{dp} \left[ (p + q)^n \right] = \frac{d}{dp} \left[ \sum_{x=0}^{n} \binom{n}{x} p^x q^{n-x} \right]$$
   $$n(p + q)^{n-1} = \sum_{x=0}^{n} x \cdot \binom{n}{x} p^{x-1} q^{n-x}$$

3. **Multiply both sides by $p$ to balance the exponent:**
   $$np(p + q)^{n-1} = \sum_{x=0}^{n} x \cdot \binom{n}{x} p^x q^{n-x}$$

4. **Simplify using $p + q = 1$:**
   Since $p + q = 1$, the left side becomes $np(1)^{n-1} = np$. 
   The right side matches the definition of $E(X) = \sum x \cdot f(x)$.
   $$np = E(X)$$

---

## 5. Visualizing the Binomial Distribution (Text Graph)

Below is an abstract representation of a symmetric Binomial Distribution ($n=6, p=0.5$). The distribution peaks precisely at its mean $E(X) = np = 6 \times 0.5 = 3$.

```text
Probability P(X=x)
   ^
0.35 |              [x=3]
0.30 |             | --- |
0.25 |      [x=2]  |     |  [x=4]
0.20 |     | --- | |     | | --- |
0.15 |     |     | |     | |     |
0.10 | [x=1]     | |     | |     | [x=5]
0.05 | |---|     | |     | |     | |---|
0.00 +-+-----+-----+-----+-----+-----+-----> Number of Successes (x)
       0     1     2     3     4     5

```

---

## 6. Practice Problems with Solutions

### Problem 1: Discrete Expectation & Variance

A biased coin is flipped. Let $X = 1$ if heads appears, and $X = 0$ if tails appears. The probability of getting heads is $0.6$. Find $E(X)$ and $V(X)$.

**Solution:**

* **Step 1: Identify distribution values**
* $f(1) = P(X=1) = 0.6$
* $f(0) = P(X=0) = 1 - 0.6 = 0.4$


* **Step 2: Calculate $E(X)$**

$$E(X) = \sum x \cdot f(x) = (0 \times 0.4) + (1 \times 0.6) = 0.6$$


* **Step 3: Calculate $E(X^2)$**

$$E(X^2) = \sum x^2 \cdot f(x) = (0^2 \times 0.4) + (1^2 \times 0.6) = 0.6$$


* **Step 4: Compute Variance $V(X)$**

$$V(X) = E(X^2) - [E(X)]^2 = 0.6 - (0.6)^2 = 0.6 - 0.36 = 0.24$$



---

### Problem 2: Binomial Word Problem

A student takes a multiple-choice quiz with $5$ questions. Each question has $4$ options (only one is correct). If the student guesses completely at random, what is the probability of passing the quiz by getting exactly $3$ questions correct? Also, find the expected number of correct answers.

**Solution:**

* **Step 1: Identify parameters**
* Number of trials $n = 5$
* Probability of success $p = \frac{1}{4} = 0.25$
* Probability of failure $q = 1 - 0.25 = 0.75$
* Target successes $x = 3$


* **Step 2: Apply the Binomial PMF formula**

$$P(X = 3) = \binom{5}{3} (0.25)^3 (0.75)^{5-3}$$


$$\binom{5}{3} = \frac{5 \times 4}{2 \times 1} = 10$$


$$P(X = 3) = 10 \times 0.015625 \times 0.5625 = 0.08789$$



*(There is roughly an 8.79% chance of getting exactly 3 right.)*
* **Step 3: Calculate Expected Value**

$$E(X) = np = 5 \times 0.25 = 1.25$$



*(On average, a student guessing randomly will get 1.25 answers correct.)*



# Discrete Probability Distributions: Variance Proof & Applications

---

## 1. Concept Introduction: Variance of a Random Variable

In statistics, **Variance** measures how far a set of numbers are spread out from their average value. For any random variable $X$, the formula for variance $V(X)$ is defined as:

$$V(X) = E(X^2) - (E(X))^2$$

Where:
* $E(X)$ is the expected value (mean) of $X$.
* $E(X^2)$ is the expected value of the squared variable $X^2$.

For a **Binomial Distribution**, our goal is to show how this expression simplifies to the classic formula: 

$$V(X) = npq$$

---

## 2. Mathematical Proof: Variance of a Binomial Distribution

Here is the step-by-step mathematical derivation using the method of successive differentiation on the Binomial Theorem.

### Step 1: Set up the Expected Value for $X^2$
By definition, the expected value of $X^2$ under a binomial probability mass function is:
$$E(X^2) = \sum_{x=0}^{n} x^2 \cdot \binom{n}{x} p^x q^{n-x}$$

### Step 2: Use the Binomial Theorem Identity
We begin with the standard algebraic binomial expansion:
$$(p + q)^n = \sum_{x=0}^{n} \binom{n}{x} p^x q^{n-x}$$

### Step 3: First Differentiation (Finding $E(X)$)
Differentiating both sides with respect to $p$:
$$n(p+q)^{n-1} = \sum_{x=0}^{n} x \cdot \binom{n}{x} p^{x-1} q^{n-x}$$

Multiply both sides by $p$ to return the exponent to $p^x$:
$$np(p+q)^{n-1} = \sum_{x=0}^{n} x \cdot \binom{n}{x} p^x q^{n-x}$$

### Step 4: Second Differentiation (Finding $E(X^2)$)
Now, differentiate this entire expression with respect to $p$ once more using the **product rule** ($d(uv) = u\,dv + v\,du$) on the left side:
$$n \left[ p \cdot (n-1)(p+q)^{n-2} + (p+q)^{n-1} \cdot 1 \right] = \sum_{x=0}^{n} x^2 \cdot \binom{n}{x} p^{x-1} q^{n-x}$$

Since we know that in total probability $p + q = 1$, we can simplify the terms inside the brackets:
$$n \left[ p(n-1)(1) + (1) \right] = \sum_{x=0}^{n} x^2 \cdot \binom{n}{x} p^{x-1} q^{n-x}$$
$$n [np - p + 1] = \sum_{x=0}^{n} x^2 \cdot \binom{n}{x} p^{x-1} q^{n-x}$$

### Step 5: Finalizing $E(X^2)$
Multiply both sides by $p$ to balance out the $p^{x-1}$ term on the right hand side:
$$np(np + 1 - p) = \sum_{x=0}^{n} x^2 \cdot \binom{n}{x} p^x q^{n-x}$$

Thus, we have successfully isolated our definition for $E(X^2)$:
$$E(X^2) = np(np + 1 - p)$$

### Step 6: Substitute back into the Variance Formula
Now replace $E(X^2)$ and $E(X) = np$ into the original variance equation:
$$V(X) = np(np + 1 - p) - (np)^2$$

Expand the expression:
$$V(X) = n^2p^2 + np - np^2 - n^2p^2$$

Cancel out the opposing $n^2p^2$ terms:
$$V(X) = np - np^2$$

Factor out $np$:
$$V(X) = np(1 - p)$$

Since the probability of failure is defined as $q = 1 - p$, we arrive at our final result:
$$V(X) = npq$$

---

## 3. Visual Representation (Probability Distribution Graph)

Below is an ASCII visualization showing how the probability behaves across the sample size when $n=4$ and $p=0.25$ (matching the practical problem below).

```
 Probability P(X=x)
   ^
0.40 |          [x=0] (0.316)
0.35 |         +-----+  [x=1] (0.422)
0.30 |         |     | +-----+
0.25 |         |     | |     |
0.20 |         |     | |     |  [x=2] (0.211)
0.15 |         |     | |     | +-----+
0.10 |         |     | |     | |     |  [x=3] (0.047)
0.05 |         |     | |     | |     | +-----+  [x=4] (0.004)
0.00 +---------+-----+-----+-----+-----+-----+-----> Number of Successes (x)
                  0      1      2      3      4

```

---

## 4. Practice Problems with Solutions

### Problem 1: Building Code Violations (From Lecture Slides)

The probability that a new building violates the building code is $\frac{1}{4}$. What is the probability that a building inspector who randomly selects $4$ of the new buildings for inspection will catch **none** of the buildings that violate the code?

#### Step-by-Step Calculation:

1. **Identify the Given Values:**
* Total number of trials ($n$) = $4$
* Probability of success/violation ($p$) = $\frac{1}{4}$
* Probability of failure/no violation ($q$) = $1 - p = 1 - \frac{1}{4} = \frac{3}{4}$
* Target number of successes ($x$) = $0$ (finding *none*)


2. **Apply the Binomial PMF Formula:**

$$P(X = x) = \binom{n}{x} p^x q^{n-x}$$


$$P(X = 0) = \binom{4}{0} \left(\frac{1}{4}\right)^0 \left(\frac{3}{4}\right)^4$$


3. **Compute the Arithmetic:**
* $\binom{4}{0} = 1$
* $\left(\frac{1}{4}\right)^0 = 1$
* $\left(\frac{3}{4}\right)^4 = \frac{3^4}{4^4} = \frac{81}{256}$


4. **Final Answer:**

$$P(X = 0) = \frac{81}{256} \approx 0.3164 \text{ (or } 31.64\%)$$



---

### Problem 2: Finding Mean and Variance

Using the same building inspection scenario ($n = 4, p = \frac{1}{4}$), calculate the expected number of code-violating buildings found and its variance.

#### Step-by-Step Calculation:

1. **Calculate Expected Value (Mean):**

$$E(X) = np = 4 \times \frac{1}{4} = 1$$



*Meaning:* On average, out of every 4 buildings inspected, the inspector can expect to find exactly 1 building violating code.
2. **Calculate Variance:**

$$V(X) = npq = 4 \times \frac{1}{4} \times \frac{3}{4} = \frac{3}{4} = 0.75$$



*Meaning:* The spread/variability of the distribution around our mean of 1 is 0.75.


# Probability & Statistics: Poisson Distribution

---

## 1. Concept Introduction: Poisson Distribution

The **Poisson Distribution** is a discrete probability distribution that models the number of times an event occurs within a specified, fixed interval of time or space. 

It serves as an excellent model for experiments and real-world phenomena involving the waiting time or frequency of occurrences, such as the number of customers arriving at a retail shop during a given hour.

### Notation
A random variable $X$ following a Poisson distribution is denoted as:
$$X \sim P(\lambda)$$

Where $\lambda$ (Lambda) is the **average rate** (mean number) of occurrences in the given interval.

### Probability Mass Function (P.M.F.)
The probability of experiencing exactly $x$ occurrences over the interval is given by:
$$f(x) = P[X = x] = \frac{\lambda^x e^{-\lambda}}{x!}$$

*   **$x$**: The number of occurrences ($x = 0, 1, 2, \dots$)
*   **$\lambda$**: The average occurrence rate ($\lambda > 0$)
*   **$e$**: Euler's constant ($\approx 2.71828$)
*   **$x!$**: The factorial of $x$

### Key Properties
*   **Mean ($E[X]$):** $\lambda$
*   **Variance ($V[X]$):** $\lambda$

> **Note:** In a Poisson distribution, the Mean and Variance are always equal to each other ($\lambda$).

---

## 2. Mathematical Proofs

### Proof 1: Deriving the Mean $E(X) = \lambda$

We calculate the expected value by summing all possible outcomes multiplied by their respective probabilities:

$$E(X) = \sum_{x=0}^{\infty} x \cdot P(x) = \sum_{x=0}^{\infty} x \cdot \frac{\lambda^x e^{-\lambda}}{x!}$$

#### Step-by-Step Derivation:
1. **Drop the $x=0$ term:** When $x=0$, the entire term becomes $0$. Thus, shift the summation base to $x=1$:
   $$E(X) = \sum_{x=1}^{\infty} x \cdot \frac{\lambda^x e^{-\lambda}}{x!}$$

2. **Simplify the factorial ($x! = x \cdot (x-1)!$):** The $x$ in the numerator cancels out the $x$ factor in the denominator:
   $$E(X) = \sum_{x=1}^{\infty} \frac{\lambda^x e^{-\lambda}}{(x-1)!}$$

3. **Factor out constants ($\lambda$ and $e^{-\lambda}$):** Extract one $\lambda$ out of $\lambda^x$, making it $\lambda \cdot \lambda^{x-1}$:
   $$E(X) = \lambda \sum_{x=1}^{\infty} \left( \frac{\lambda^{x-1}}{(x-1)!} \right) e^{-\lambda}$$
   $$E(X) = \lambda e^{-\lambda} \sum_{x=1}^{\infty} \frac{\lambda^{x-1}}{(x-1)!}$$

4. **Change the summation index:** Let $k = x - 1$. As $x$ goes from $1$ to $\infty$, $k$ goes from $0$ to $\infty$:
   $$E(X) = \lambda e^{-\lambda} \sum_{k=0}^{\infty} \frac{\lambda^k}{k!}$$

5. **Apply Taylor Series expansion:** The infinite sum $\sum_{k=0}^{\infty} \frac{\lambda^k}{k!}$ matches the exact Taylor expansion for $e^\lambda$:
   $$E(X) = \lambda e^{-\lambda} \cdot e^\lambda$$

6. **Final Simplification:**
   $$E(X) = \lambda \cdot e^0 = \lambda$$

---

### Proof 2: Deriving the Variance $V(X) = \lambda$

Using the variance identity formula:
$$V(X) = E(X^2) - (E(X))^2$$

First, we must solve for $E(X^2)$:
$$E(X^2) = \sum_{x=0}^{\infty} x^2 \frac{\lambda^x e^{-\lambda}}{x!}$$

#### Step-by-Step Derivation:
1. **Rewrite $x^2$ algebraically:** Express $x^2$ as $x(x-1) + x$ to facilitate factorial cancellation:
   $$E(X^2) = \sum_{x=0}^{\infty} \big( x(x-1) + x \big) \frac{\lambda^x e^{-\lambda}}{x!}$$

2. **Split into two separate series:**
   $$E(X^2) = \sum_{x=0}^{\infty} x(x-1) \frac{\lambda^x e^{-\lambda}}{x!} + \sum_{x=0}^{\infty} x \frac{\lambda^x e^{-\lambda}}{x!}$$

3. **Simplify the denominators:** 
   * In the first term, drop $x=0$ and $x=1$ (since they yield zero) and expand $x! = x(x-1)(x-2)!$.
   * The second term is exactly our definition for $E(X) = \lambda$.
   $$E(X^2) = \sum_{x=2}^{\infty} \frac{\lambda^x e^{-\lambda}}{(x-2)!} + \lambda$$

4. **Factor out $\lambda^2$ from the first series:**
   $$E(X^2) = \lambda^2 e^{-\lambda} \sum_{x=2}^{\infty} \frac{\lambda^{x-2}}{(x-2)!} + \lambda$$

5. **Substitute Taylor Series values:** The remaining infinite sum evaluates to $e^\lambda$:
   $$E(X^2) = \lambda^2 e^{-\lambda} \cdot e^\lambda + \lambda$$
   $$E(X^2) = \lambda^2 + \lambda$$

6. **Compute final Variance $V(X)$:**
   $$V(X) = (\lambda^2 + \lambda) - (\lambda)^2$$
   $$V(X) = \lambda$$

---

## 3. Distribution Graph Visualization

Below is an abstract text-based distribution graph demonstrating a Poisson Distribution where $\lambda = 2$. Notice how the distribution peaks around its mean values ($x = 1$ and $x = 2$).

```text
 Probability P(X=x)
   ^
0.30 |          [x=1]      [x=2]
0.25 |         +-----+    +-----+
0.20 |         |     |    |     |
0.15 |  [x=0]  |     |    |     |    [x=3]
0.10 | +-----+ |     |    |     |   +-----+
0.05 | |     | |     |    |     |   |     |    [x=4]
0.00 +-+-----+-----+------+-----+---+-----+---+-----+-----> Number of Events (x)
          0       1          2         3         4

```

---

## 4. Practice Problems with Solutions

### Problem 1: Customer Arrivals

On average, a small coffee shop receives $\lambda = 3$ customers per 10-minute interval. What is the probability that exactly 2 customers will arrive in a randomly selected 10-minute window?

#### Step-by-Step Calculation:

1. **Identify parameters:**
* Average rate ($\lambda$) = $3$
* Number of target events ($x$) = $2$


2. **Apply P.M.F Formula:**

$$P(X = 2) = \frac{3^2 \cdot e^{-3}}{2!}$$


3. **Compute the individual values:**
* $3^2 = 9$
* $e^{-3} \approx 0.049787$
* $2! = 2 \times 1 = 2$


4. **Solve:**

$$P(X = 2) = \frac{9 \times 0.049787}{2} = \frac{0.44808}{2} = 0.22404$$



**Answer:** There is approximately a **22.40%** chance that exactly 2 customers arrive.

---

### Problem 2: Network Server Errors

A web server experiences an average of $\lambda = 0.5$ system drops per day. What is the probability that the server experiences **at least one** system drop tomorrow?

#### Step-by-Step Calculation:

1. **Understand "At least one":**
"At least one" means $X \geq 1$. It is easier to calculate this using the complement rule:

$$P(X \geq 1) = 1 - P(X = 0)$$


2. **Compute $P(X = 0)$:**

$$P(X = 0) = \frac{0.5^0 \cdot e^{-0.5}}{0!}$$


* Since $0.5^0 = 1$ and $0! = 1$:

$$P(X = 0) = e^{-0.5} \approx 0.6065$$




3. **Subtract from 1:**

$$P(X \geq 1) = 1 - 0.6065 = 0.3935$$



**Answer:** There is a **39.35%** probability of experiencing at least one system drop tomorrow.


# Probability & Statistics: Poisson Distribution Applications

---

## 1. Concept Summary: Cumulative Poisson Probability

The **Poisson Distribution** determines the probability of a specific number of independent events occurring within a fixed boundary of time or space. 

When a problem asks for conditions like **"at most $k$ events"** or **"at least $k$ events"**, we calculate the cumulative probabilities:
* **At most $k$ events:** We sum the individual probabilities from 0 up to $k$.
  $$P(X \le k) = \sum_{x=0}^{k} \frac{e^{-\lambda} \lambda^x}{x!}$$
* **At least $k$ events:** We use the complement rule to subtract the unwanted lower values from 1.
  $$P(X \ge k) = 1 - P(X < k) = 1 - \sum_{x=0}^{k-1} \frac{e^{-\lambda} \lambda^x}{x!}$$

---

## 2. Text-Based Probability Curve Visualization

Below is a visualization of a Poisson probability mass distribution when the average rate ($\lambda$) equals 2. The cumulative value $P(X \le 2)$ comprises the bulk area of the curve under $x = 0$, $x = 1$, and $x = 2$.

```text
 Probability P(X=x)
   ^
0.30 |                  [x=1]       [x=2]
0.25 |                 +-----+     +-----+
0.20 |                 |     |     |     |
0.15 |     [x=0]       |     |     |     |     [x=3]
0.10 |    +-----+      |     |     |     |    +-----+
0.05 |    |     |      |     |     |     |    |     |    [x=4]
0.00 +----+-----+------+-----+-----+-----+----+-----+----+-----> Time Event (x)
          0            1           2          3          4
       |_________________________________|
                Sum = P(X <= 2)

```

---

## 3. Lecture Problems & Step-by-Step Solutions

### Problem 1: Checkout Counter Arrivals

At a checkout counter, customers arrive at an average rate of 2 per minute. What is the probability that **at most 2 customers** will arrive in any given minute?

#### Step-by-Step Calculation:

1. **Identify parameters:**
* Average arrival rate ($\lambda$) = 2 customers/minute
* Interval = 1 minute
* Target condition: "At most 2" $\rightarrow P(X \le 2)$


2. **Set up the cumulative calculation:**

$$P(X \le 2) = P(X = 0) + P(X = 1) + P(X = 2)$$


3. **Substitute values into the Poisson formula $\left( \frac{e^{-\lambda} \lambda^x}{x!} \right)$:**

$$P(X \le 2) = \frac{e^{-2} \cdot 2^0}{0!} + \frac{e^{-2} \cdot 2^1}{1!} + \frac{e^{-2} \cdot 2^2}{2!}$$


4. **Factor out $e^{-2}$ to simplify:**

$$P(X \le 2) = e^{-2} \left[ \frac{1}{1} + \frac{2}{1} + \frac{4}{2} \right]$$


$$P(X \le 2) = e^{-2} [1 + 2 + 2]$$


5. **Final result expression:**

$$P(X \le 2) = 5e^{-2}$$



*(Numerically, $5 \times 0.135335 \approx 0.6767$ or **67.67%**)*

---

### Problem 2: Office Switchboard Phone Calls

An office switchboard receives phone calls at a rate of 3 calls per minute. Find the probability of:

1. Receiving no calls in a one-minute interval.
2. Receiving at least 4 calls in a 3-minute interval.

#### Part (i) Calculation: No calls in 1 minute

1. **Identify parameters:**
* Average rate ($\lambda$) = 3 calls/minute
* Target number ($x$) = 0


2. **Calculate:**

$$P(X = 0) = \frac{e^{-3} \cdot 3^0}{0!} = e^{-3}$$



*(Numerically, $e^{-3} \approx 0.0498$ or **4.98%**)*

#### Part (ii) Calculation: At least 4 calls in 3 minutes

1. **Adjust the rate for a 3-minute interval:**
* If $\lambda = 3$ calls for 1 minute, then for 3 minutes:

$$\lambda' = 3 \times 3 = 9 \text{ calls}$$




2. **Set up the complement rule for "at least 4" ($P(X \ge 4)$):**

$$P(X \ge 4) = 1 - [P(X=0) + P(X=1) + P(X=2) + P(X=3)]$$


3. **Substitute formula terms with $\lambda' = 9$:**

$$P(X \ge 4) = 1 - \left[ \frac{e^{-9} 9^0}{0!} + \frac{e^{-9} 9^1}{1!} + \frac{e^{-9} 9^2}{2!} + \frac{e^{-9} 9^3}{3!} \right]$$


4. **Factor out $e^{-9}$ and simplify terms:**

$$P(X \ge 4) = 1 - e^{-9} \left[ 1 + 9 + \frac{81}{2} + \frac{729}{6} \right]$$


$$P(X \ge 4) = 1 - e^{-9} \left[ 10 + \frac{81}{2} + \frac{243}{2} \right]$$


$$P(X \ge 4) = 1 - e^{-9} \left[ 10 + \frac{324}{2} \right] = 1 - e^{-9} [10 + 162]$$


$$P(X \ge 4) = 1 - 172e^{-9}$$



*(Numerically, $1 - (172 \times 0.0001234) \approx 0.9788$ or **97.88%**)*

---

### Problem 3: Book Proofreading Errors

After correcting 60 pages of the proof of a book, a reader finds that there are on average 4 errors per 10 pages. Find the number of pages one would expect to find 2 errors in 1000 pages of the first print of the book.

#### Step-by-Step Calculation:

1. **Determine the rate per single page ($\lambda$):**

$$\lambda = \frac{4 \text{ errors}}{10 \text{ pages}} = 0.4 \text{ error/page}$$


2. **Find the probability of getting exactly 2 errors on a single page:**

$$P(X = 2) = \frac{e^{-0.4} \cdot (0.4)^2}{2!}$$


$$P(X = 2) = \frac{e^{-0.4} \cdot 0.16}{2} = 0.08 e^{-0.4}$$


3. **Calculate expected number of pages out of 1000 total pages:**
To find total expected pages matching this condition, multiply total pages ($N = 1000$) by the single-page probability:

$$\text{Expected Pages} = 1000 \times 0.08 e^{-0.4}$$


$$\text{Expected Pages} = 80 e^{-0.4}$$


4. **Convert to numerical value:**
* Given $e^{-0.4} \approx 0.67032$

$$\text{Expected Pages} = 80 \times 0.67032 \approx 53.63 \text{ pages}$$


**Answer:** One would expect to find approximately **54 pages** that contain exactly 2 errors out of a 1000-page printing run.
