# Lecture 24: Logistic Regression - I

## 1. Introduction to Logistic Regression
Despite its name containing "regression," **Logistic Regression** is primarily used as a **supervised classification algorithm**. 

* **The Core Paradox:** It is fundamentally a regression model because it builds a mathematical function to predict a continuous value: the **probability** ($P$) that a given data entry belongs to a specific category (usually labeled as "1").
* **Linear vs. Logistic:** Where Linear Regression assumes data follows a straight line, Logistic Regression models the probability using an S-shaped curve called the **Sigmoid function**.

### Mathematical Setup
Given a dataset $\{x_i, y_i\}_{i=1}^n$ where $x_i \in \mathbb{R}^p$ represents the input features, we try to map the linear combination of inputs:

$$\beta_0 + \beta_1 x_1 + \dots + \beta_p x_p = \beta^T x$$

Instead of predicting the discrete target $y \in \{0, 1\}$ directly using a straight line (which could yield values like 1.5 or -3), we squeeze the linear equation through a bounding function.

---

## 2. The Sigmoid Function
To map any real-valued number into a valid probability range between 0 and 1, we use a **Sigmoid Function** ($S: \mathbb{R} \rightarrow (0, 1)$).

### Key Characteristics:
* **Asymptotes:** As $x \rightarrow -\infty$, $S(x) \rightarrow 0$. As $x \rightarrow +\infty$, $S(x) \rightarrow 1$.
* **S-shape:** It smoothly transitions around $x = 0$, where $S(0) = 0.5$.

### Standard Logistic Function Formula:
$$S(x) = \frac{1}{1 + e^{-x}}$$

Common variants of sigmoid curves include the *Logistic function*, *Hyperbolic tangent (tanh)*, and *Arctangent*. For standard binary classification, the Logistic function is preferred.

---

## 3. Logistic Regression-Based Classification
A regression model outputs probabilities. To turn it into a **classifier**, we must introduce a **Decision Threshold** (often denoted as $Th$).

$$\text{Predicted Class} = \begin{cases} 1 & \text{if } P(y=1|x) \ge Th \\ 0 & \text{if } P(y=1|x) < Th \end{cases}$$

> 💡 **Note:** The threshold defaults to `0.5`, but it can be adjusted depending on the specific problem context (e.g., setting a lower threshold to catch rare diseases).

### Types of Logistic Regression
1. **Binomial:** The target variable has exactly 2 outcomes (e.g., Win vs. Loss, Pass vs. Fail, 0 vs. 1).
2. **Multinomial:** The target variable has 3 or more unordered categories (e.g., Disease A vs. Disease B vs. Disease C).

---

## 4. Step-by-Step Calculation Example

Let's look at how the model computes a prediction for a single data point.

### Problem Scenario
Suppose we trained a model to predict whether a student passes an exam ($y=1$) based on two features: $x_1$ (Hours Studied) and $x_2$ (Attendance Rate between 0 and 1).

* **Learned Weights:** $\beta_0 = -5$, $\beta_1 = 0.8$, $\beta_2 = 3$
* **New Student Data:** Studied for $6$ hours ($x_1 = 6$), Attendance is $80\%$ ($x_2 = 0.8$)
* **Decision Threshold:** $0.5$

### Step 1: Calculate the Linear Combination ($z$)
$$z = \beta_0 + \beta_1 x_1 + \beta_2 x_2$$
$$z = -5 + (0.8 \times 6) + (3 \times 0.8)$$
$$z = -5 + 4.8 + 2.4 = 2.2$$

### Step 2: Pass $z$ through the Sigmoid Function
$$P(y=1|x) = \frac{1}{1 + e^{-2.2}}$$

Knowing $e^{-2.2} \approx 0.1108$:
$$P(y=1|x) = \frac{1}{1 + 0.1108} = \frac{1}{1.1108} \approx 0.9002 \text{ (or } 90.02\%)$$

### Step 3: Apply Decision Threshold
Since $0.9002 \ge 0.5$, the model classifies this student as **1 (Pass)**.

---

## 5. Conceptual Practice Problems

### Problem 1: Interpret the Probability Output
**Question:** If a logistic regression model computes $z = -1.386$ for a loan application, what is the probability that the loan is fraudulent ($y=1$), and what is the classification decision if the threshold is $0.5$?

**Solution:**
1. Compute the Sigmoid activation:
   $$S(-1.386) = \frac{1}{1 + e^{-(-1.386)}} = \frac{1}{1 + e^{1.386}}$$
   Since $e^{1.386} \approx 4$:
   $$P = \frac{1}{1 + 4} = \frac{1}{5} = 0.20 \text{ (20\% probability)}$$
2. Compare to Threshold:
   Since $0.20 < 0.5$, the loan application is classified as **0 (Not Fraudulent)**.

### Problem 2: Tuning Thresholds
**Question:** Imagine you are building a Logistic Regression system to detect a highly contagious virus. Would you set your decision threshold to $0.2$ or $0.8$? Explain why.

**Solution:**
You should set the decision threshold to **0.2**. In medical screening, missing a positive case (False Negative) is dangerous. Lowering the threshold ensures that even patients with a relatively low predicted probability ($20\%$ or higher) are flagged for further testing, prioritizing high sensitivity.


# Lecture 24 (Continuation): Probability Basics, Random Variables & The Log-it Link

## 1. Probability Basics
Before deep-diving into the probabilistic foundations of classification, we must establish the core components of probability theory.

### I. Sample Space ($\Omega$)
The **Sample Space** is the set of all possible outcomes of a random experiment.
* **Example (Tossing 2 Coins):** $$\Omega = \{HH, HT, TH, TT\}$$

### II. Event Space ($\mathcal{A}$)
The **Event Space** is a collection of potential results or combinations of outcomes from the experiment. It is obtained by considering subsets of $\Omega$.
* For a discrete probability distribution, the event space is the power set of the sample space: $\mathcal{A} = \mathcal{P}(\Omega)$.

### III. Probability Function ($P$)
For each event $A \in \mathcal{A}$, we assign a real number $P(A)$ that measures the likelihood or degree to which that event will occur.
* **Axiom 1:** The probability of any event lies between 0 and 1: 
  $$P(A) \in [0, 1]$$
* **Axiom 2:** The sum of probabilities of all mutually exclusive, exhaustive outcomes equals 1: 
  $$\sum_{i} P(A_i) = 1$$

---

## 2. Random Variables
A **Random Variable** $X$ is a function that maps outcomes from the sample space $\Omega$ to a set of real numbers/classes (often denoted as $\mathcal{T}$).

$$X: \Omega \rightarrow \mathcal{T}$$

### Step-by-Step Mapping Example
Let's define our experiment as tossing two fair coins, so $\Omega = \{HH, HT, TH, TT\}$. 
Let $X$ be the random variable that **counts the number of Heads**.

* **Step 1:** Look at outcome $HH \rightarrow$ There are 2 heads $\rightarrow X(HH) = 2$
* **Step 2:** Look at outcome $HT \rightarrow$ There is 1 head $\rightarrow X(HT) = 1$
* **Step 3:** Look at outcome $TH \rightarrow$ There is 1 head $\rightarrow X(TH) = 1$
* **Step 4:** Look at outcome $TT \rightarrow$ There are 0 heads $\rightarrow X(TT) = 0$

Thus, our target set of classes is $\mathcal{T} = \{0, 1, 2\}$.

---

## 3. Deriving the Log-it Link Function (Log-Odds)
In linear regression, we model continuous targets directly via $\alpha^T X$. In logistic classification, we want to predict the **probability** that the target $Y$ belongs to class 1, given a feature vector $X$:

$$p(X) = P(Y = 1 | X)$$

Let's walk through the algebra to understand how standard linear equations connect to probability outputs.

### Step 1: Write the Logistic Function
Instead of standard linear lines, we define the probability using the sigmoid curve:
$$p(X) = \frac{1}{1 + e^{-\alpha^T X}}$$

By multiplying the numerator and denominator by $e^{\alpha^T X}$, we get the equivalent form:
$$p(X) = \frac{e^{\alpha^T X}}{1 + e^{\alpha^T X}}$$

### Step 2: Compute the Probability of the Complement ($1 - p(X)$)
The probability of the event *not* happening ($Y=0$) is:
$$1 - p(X) = 1 - \frac{e^{\alpha^T X}}{1 + e^{\alpha^T X}} = \frac{(1 + e^{\alpha^T X}) - e^{\alpha^T X}}{1 + e^{\alpha^T X}} = \frac{1}{1 + e^{\alpha^T X}}$$

### Step 3: Compute the Odds Ratio
The **Odds Ratio** is the ratio of the probability of success to the probability of failure:
$$\text{Odds} = \frac{p(X)}{1 - p(X)} = \frac{\frac{e^{\alpha^T X}}{1 + e^{\alpha^T X}}}{\frac{1}{1 + e^{\alpha^T X}}} = e^{\alpha^T X}$$

### Step 4: Take the Natural Logarithm (The Log-it Transformation)
Taking the natural log ($\ln$) of both sides isolates our linear combination parameters:
$$\log\left(\frac{p(X)}{1 - p(X)}\right) = \log\left(e^{\alpha^T X}\right) = \alpha^T X$$

$$\log\left(\frac{p(X)}{1 - p(X)}\right) = \alpha_0 + \alpha_1 x_1 + \alpha_2 x_2 + \dots + \alpha_p x_p$$

> 📌 **Core Definition:** The term $\log\left(\frac{p(X)}{1 - p(X)}\right)$ is known as the **Log-it** of $p(X)$, or simply the **Log-Odds**. This shows that logistic regression is simply a linear regression model operating in the log-odds space!

---

## 4. Conceptual Practice Problems

### Problem 1: Converting Probabilities to Odds and Log-Odds
**Question:** Suppose a well-trained model predicts that a customer has an $80\%$ probability ($p(X) = 0.8$) of renewing their subscription. 
1. What are the **Odds** of renewal?
2. What is the value of the **Log-Odds** (Log-it)? 

**Solution & Calculation:**
1. **Find Odds:**
   $$\text{Odds} = \frac{p(X)}{1 - p(X)} = \frac{0.8}{1 - 0.8} = \frac{0.8}{0.2} = 4$$
   *Meaning: The customer is 4 times more likely to renew than not renew.*

2. **Find Log-Odds:**
   $$\text{Log-Odds} = \log(4) \approx 1.3863$$

### Problem 2: Reversing Log-Odds to Probability
**Question:** A logistic regression model outputs a final linear decision value ($\alpha^T X$) of $-0.693$ for an email instance. Find its log-odds, odds, and final probability of being spam.

**Solution & Calculation:**
1. **Log-Odds:** By definition, the linear output equals the log-odds:
   $$\text{Log-Odds} = -0.693$$
2. **Odds:** Eliminate the logarithm by applying base $e$ exponentiation:
   $$\text{Odds} = e^{-0.693} \approx 0.5 = \frac{1}{2}$$
3. **Probability:** Solve for $p(X)$:
   $$\text{Odds} = \frac{p(X)}{1 - p(X)} \rightarrow 0.5 = \frac{p(X)}{1 - p(X)}$$
   $$0.5 - 0.5p(X) = p(X) \rightarrow 0.5 = 1.5p(X)$$
   $$p(X) = \frac{0.5}{1.5} = \frac{1}{3} \approx 0.3333 \text{ (or } 33.33\%)$$


# Lecture 24 (Continuation): Parameter Estimation via Maximum Likelihood Estimation (MLE)

## 1. Problem Formulation
Given a set of training samples $\{x_i, y_i\}_{i=1}^n$ where:
* $x_i \in \mathbb{R}^p$ represents the input feature vectors.
* $y_i \in \{0, 1\}$ represents the binary class targets.

From our previous log-it relationship, we model the probability $p(x_i) = P(y_i = 1 | x_i)$ using:
$$\log\left(\frac{p(x_i)}{1 - p(x_i)}\right) = \alpha^T x_i$$

Our goal is to estimate the parameter weights vector $\hat{\alpha} = \{\alpha_0, \alpha_1, \dots, \alpha_p\}$. Unlike linear regression, which uses Ordinary Least Squares (OLS), logistic regression parameters are estimated using **Maximum Likelihood Estimation (MLE)**.

---

## 2. Deriving the Likelihood Function $L(\alpha)$
The likelihood function measures how likely we are to observe our actual target labels given our model parameters $\alpha$. 

### Step 1: Combine the Outcomes
For data points where the true class is $y_i = 1$, the probability of that event occurring is $p(x_i)$.  
For data points where the true class is $y_i = 0$, the probability is $1 - p(x_i)$.

Assuming all data points are independent, the total likelihood is the product of these probabilities:
$$L(\alpha) = \prod_{i, y_i=1} p(x_i) \cdot \prod_{i, y_i=0} (1 - p(x_i))$$

### Step 2: Write as a Single Unified Product
Using the algebraic trick of putting indicators in exponents ($y_i$ and $1-y_i$), we can consolidate this into a single expression valid for any $y_i \in \{0,1\}$:
$$L(\alpha) = \prod_{i=1}^n \left(p(x_i)\right)^{y_i} \left(1 - p(x_i)\right)^{1 - y_i}$$

* If $y_i = 1$: $(p(x_i))^1 \cdot (1 - p(x_i))^0 = p(x_i)$
* If $y_i = 0$: $(p(x_i))^0 \cdot (1 - p(x_i))^1 = 1 - p(x_i)$

Our objective is to find $\alpha$ that maximizes this total likelihood: $\max_{\alpha} L(\alpha)$.

---

## 3. Deriving the Log-Likelihood Function $l(\alpha)$
Multiplying many small probabilities can lead to numerical underflow. To make optimization easier, we take the natural logarithm ($\ln$) of the likelihood function to convert products into sums.

$$l(\alpha) = \log L(\alpha)$$
$$l(\alpha) = \log \left[ \prod_{i=1}^n \left(p(x_i)\right)^{y_i} \left(1 - p(x_i)\right)^{1 - y_i} \right]$$

Using log rules ($\log(A \cdot B) = \log A + \log B$ and $\log(A^B) = B \log A$):
$$l(\alpha) = \sum_{i=1}^n \left[ y_i \log(p(x_i)) + (1 - y_i) \log(1 - p(x_i)) \right]$$

### Step 3: Simplifying Using the Log-it Relationship
Let's group the terms to substitute our known log-odds function:
$$l(\alpha) = \sum_{i=1}^n \left[ y_i \log(p(x_i)) + \log(1 - p(x_i)) - y_i \log(1 - p(x_i)) \right]$$
$$l(\alpha) = \sum_{i=1}^n \left[ y_i \left( \log(p(x_i)) - \log(1 - p(x_i)) \right) + \log(1 - p(x_i)) \right]$$
$$l(\alpha) = \sum_{i=1}^n \left[ y_i \log\left(\frac{p(x_i)}{1 - p(x_i)}\right) + \log(1 - p(x_i)) \right]$$

Since we know $\log\left(\frac{p(x_i)}{1 - p(x_i)}\right) = \alpha^T x_i$, we substitute it in:
$$l(\alpha) = \sum_{i=1}^n \left[ y_i (\alpha^T x_i) + \log(1 - p(x_i)) \right]$$

> 💡 **Optimization Note:** To maximize this expression, we want to take the partial derivative with respect to $\alpha$ and set it to zero:
> $$\frac{\partial l(\alpha)}{\partial \alpha} = 0$$
> Because this equation has no closed-form analytical solution, we must use **Numerical Optimization** techniques like **Gradient Descent** or Newton-Raphson to iteratively find the optimal weights.

---

## 4. Step-by-Step Mathematical Calculation

### Problem Scenario
Let's calculate the Log-Likelihood value $l(\alpha)$ manually for a tiny dataset of $2$ samples to see how a model evaluates its current parameters.

* **Sample 1:** Features $x_1$, Label $y_1 = 1$. The model currently predicts $p(x_1) = 0.90$.
* **Sample 2:** Features $x_2$, Label $y_2 = 0$. The model currently predicts $p(x_2) = 0.40$.

### Step 1: Compute the individual components for each sample
* **For Sample 1 ($y_1 = 1$):**
  $$\text{Term}_1 = y_1 \log(p(x_1)) + (1 - y_1) \log(1 - p(x_1))$$
  $$\text{Term}_1 = 1 \cdot \log(0.90) + 0 \cdot \log(0.10) = \log(0.90) \approx -0.1054$$

* **For Sample 2 ($y_0 = 0$):**
  $$\text{Term}_2 = y_2 \log(p(x_2)) + (1 - y_2) \log(1 - p(x_2))$$
  $$\text{Term}_2 = 0 \cdot \log(0.40) + (1 - 0) \cdot \log(1 - 0.40) = \log(0.60) \approx -0.5108$$

### Step 2: Sum the terms to get Total Log-Likelihood
$$l(\alpha) = \sum_{i=1}^2 \text{Term}_i = (-0.1054) + (-0.5108) = -0.6162$$

---

## 5. Conceptual Practice Problems

### Problem 1: Analyzing the Ideal Likelihood Limits
**Question:** What is the maximum possible value that a Log-Likelihood function $l(\alpha)$ can reach for a binary classification problem, and when does it happen?

**Solution:**
The maximum possible value is **0**. 
This happens in the case of a theoretically "perfect" model. If a model predicts $p(x_i) = 1$ for every true $y_i = 1$ sample, and $p(x_i) = 0$ for every true $y_i = 0$ sample, then all probability terms evaluated inside the log are exactly $1$. Since $\log(1) = 0$, the sum equals $0$. Because probabilities are bound between $0$ and $1$, their logarithms are always negative numbers; hence, a value closer to $0$ represents a better fit.

### Problem 2: Link to Cost Functions
**Question:** In machine learning libraries, we often *minimize* a loss function instead of *maximizing* a likelihood. How is the cost function **Binary Cross-Entropy Loss** related to the Log-Likelihood function $l(\alpha)$ derived above?

**Solution:**
Binary Cross-Entropy (BCE) Loss is simply the **Negative Log-Likelihood** divided by the total number of samples ($n$). Maximizing a function $l(\alpha)$ is mathematically identical to minimizing its negative version:

$$\text{BCE Loss} = -\frac{1}{n} \sum_{i=1}^n \left[ y_i \log(p(x_i)) + (1 - y_i) \log(1 - p(x_i)) \right]$$



#  Making Predictions on New Test Instances

## 1. Concept Overview: Inference / Prediction Stage
Once our logistic regression model has optimized its parameter weights $\alpha = \{\alpha_0, \alpha_1, \dots, \alpha_p\}$ using Maximum Likelihood Estimation (MLE), we use these weights to predict the class of a completely new, unseen test sample $x_i^*$.

### The Test Instance Structure
Let a new test data point be represented as a vector of $p$ features:
$$x_i^* = (x_{i_1}^*, x_{i_2}^*, \dots, x_{i_p}^*)$$

Our objective is to determine whether its true hidden label $y_i^*$ is more likely to be **0** or **1**.

---

## 2. Step-by-Step Prediction Workflow

### Step 1: Compute the Linear Score ($m$)
We first pass our test features through the learned linear boundary equation to calculate an intermediate linear score, which we will call $m$:
$$m = \alpha_0 + \alpha_1 x_{i_1}^* + \alpha_2 x_{i_2}^* + \dots + \alpha_p x_{i_p}^*$$

### Step 2: Convert the Score to a Probability Estimate ($\hat{Y}$)
We map this real-valued score $m$ into a value strictly between 0 and 1 using the standard logistic sigmoid function. This output is our estimated target probability $\hat{Y}$:
$$\hat{Y} = \frac{1}{1 + e^{-m}}$$

### Step 3: Apply the Decision Threshold Criteria
Using the default probability threshold of $0.5$, we assign the sample to its final discrete category:
$$\text{Class Assignment} = \begin{cases} \text{Class 0} & \text{if } \hat{Y} < 0.5 \quad (\text{equivalent to } m < 0) \\ \text{Class 1} & \text{otherwise } (\hat{Y} \ge 0.5 \quad \text{equivalent to } m \ge 0) \end{cases}$$

### Visualizing the Sigmoid Classification Boundary
The threshold boundary can be visualized along the S-shaped sigmoid curve:



Y (Probability)


```

1.0 +                               /-------
|                              /
|                             /
0.5 + - - - - - - - - - - - - - -/ - - - Threshold Line
|                           /|
|                          / |
0.0 +-------------------------/--+-------------> m (Linear Score)
|           Class 0      /   |   Class 1
(m < 0)      (m >= 0)

```

---

## 3. Step-by-Step Numerical Calculation

### Problem Scenario
Assume our binary logistic classifier has finished training and generated the following final parameters:
* $\alpha_0 = -2.0$ (Intercept)
* $\alpha_1 = 0.5$
* $\alpha_2 = 1.5$

We receive a new incoming test profile $x_i^* = (4, 1)$. Let's find its predicted class assignment step-by-step.

### Step 1: Calculate the value of $m$
$$m = \alpha_0 + \alpha_1 x_{i_1}^* + \alpha_2 x_{i_2}^*$$
$$m = -2.0 + (0.5 \times 4) + (1.5 \times 1)$$
$$m = -2.0 + 2.0 + 1.5 = 1.5$$

### Step 2: Calculate the Sigmoid Probability Output $\hat{Y}$
$$\hat{Y} = \frac{1}{1 + e^{-1.5}}$$

Knowing that $e^{-1.5} \approx 0.2231$:
$$\hat{Y} = \frac{1}{1 + 0.2231} = \frac{1}{1.2231} \approx 0.8176 \text{ (or } 81.76\%)$$

### Step 3: Evaluate against the Decision Rule
Since our estimated probability $\hat{Y} = 0.8176$, we check our threshold rule:
$$\text{Is } 0.8176 < 0.5? \rightarrow \text{False.}$$

Therefore, $x_i^*$ is explicitly assigned to **Class 1**.

---

## 4. Conceptual Practice Problems

### Problem 1: Critical Boundary Analysis
**Question:** If a test sample yields an intermediate score of exactly $m = 0$, what will be its calculated probability $\hat{Y}$, and which class will it be assigned to under the rule shown above?

**Solution:**
1. Let's substitute $m = 0$ into our sigmoid converter:
   $$\hat{Y} = \frac{1}{1 + e^{-0}} = \frac{1}{1 + 1} = \frac{1}{2} = 0.5$$
2. Checking our classification threshold logic block:
   The rule says $x_i^* \in \text{Class 0}$ **only if** $\hat{Y} < 0.5$. Since our value is exactly $0.5$, it falls into the **"otherwise"** bucket. Thus, it is classified into **Class 1**.

### Problem 2: Negative Parameter Mechanics
**Question:** Let's say a model outputs a negative score ($m = -3.5$) for an email evaluation test instance. Without running full calculator exponents, can you instantly state which class it belongs to? Explain why.

**Solution:**
Yes, it belongs to **Class 0**. 
The logistic function maps any negative linear input ($m < 0$) to a probability value below $0.5$. Since $m = -3.5$ sits well to the left of the origin line on the coordinate spectrum, its corresponding sigmoid position will safely yield $\hat{Y} < 0.5$, matching the threshold criteria for Class 0.

