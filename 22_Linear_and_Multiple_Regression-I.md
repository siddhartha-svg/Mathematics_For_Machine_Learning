# Statistics & Machine Learning Notes: Introduction to Statistical Regression

This note introduces the theoretical and mathematical framework of **Statistical Regression Analysis**, walking through the standard equation components, a real-world predictive example, and sample calculations.

---

## 1. Concept Name: Statistical Regression Mapping

### Simple Meaning 💡
**Regression** is a statistical tool used to learn and map the underlying relationship between a set of input variables and a continuous numeric output variable. 
* Think of it as a mathematical formula that lets you look at a set of clues (inputs) to predict an exact numerical value (the output).
* For example, we can use a person's `Age` and `Years of Education` (inputs) to predict their exact annual `Salary` (output).


### The Core Mathematical Framework
Mathematically, the relationship is defined by the following foundational function:

$$y = f(X) + \epsilon$$

Where:
* **$y$**: The quantitative **Output Variable** (also known as the dependent variable, target, or response).
* **$X$**: The **Input Vector** containing your tracking dimensions, defined as $X = [x_1, x_2, \dots, x_n]^T$ (also known as independent variables, features, or predictors).
* **$f(X)$**: The ideal model **System Function** we are trying to learn. In a simple linear world, this maps directly to a straight-line equation: $f(X) = a_0 + a_1 x$.
* **$\epsilon$ (epsilon)**: The random **Statistical Error Term** (or noise). This accounts for things the model cannot capture or measure (e.g., raw luck, individual bargaining power, or sudden market shifts). It represents the vertical gap between the real data point and our smooth model prediction line.

---

## 2. Step-by-Step Practical Walkthrough & Calculations

### Step 2.1: Analyze the Observation Training Matrix
Let's consider a practical 1-variable linear regression problem mapping **$X$ (Age)** to predict **$Y$ (Salary in thousands of dollars)** across $m = 5$ real-world sample observations:

| Sample Index | Input $x_i$ (Age) | True Output $y_i$ (Salary) |
| :--- | :--- | :--- |
| $e_1$ | 25 | 90 |
| $e_2$ | 28 | 95 |
| $e_3$ | 30 | 105 |
| $e_4$ | 31 | 102 |
| $e_5$ | 35 | 107 |

---

### Step 2.2: Establish the Learned Model Equation
Suppose our regression model finishes training on our data points and calculates the following line equation:

$$\hat{y} = f(x) = 2.0x + 40.0$$

Where:
* Intercept coefficient $a_0 = 40.0$ (The baseline starting salary value).
* Slope weight coefficient $a_1 = 2.0$ (States that for every $1$ year an individual ages, their salary increases by $2.0$ units).

---

### Step 2.3: Calculating Sample Statistical Noise ($\epsilon$)
Let's calculate the exact error noise value $\epsilon$ for the third sample observation ($e_3$) where a 30-year-old makes $105$:

1. Find the model prediction ($\hat{y}_3$) by substituting $x = 30$:
   $$\hat{y}_3 = 2.0(30) + 40.0 = 60.0 + 40.0 = 100.0$$
2. Isolate $\epsilon$ using our core equation ($y = \hat{y} + \epsilon \implies \epsilon = y - \hat{y}$):
   $$\epsilon_3 = y_3 - \hat{y}_3 = 105 - 100.0 = \mathbf{+5.0}$$

> **Geometric Meaning 💡:** This specific individual makes $\$5,000$ more than what our general model line predicted for their exact age cohort. On our scatter plot, this observation point floats exactly 5 units directly above the line.

---

### Step 2.4: Predictive Evaluation on Unseen Test Inputs ($x_*$)
Now, we want to predict the salary for an unseen client who is $x_* = 29$ years old. 

Visually, we draw a vertical line from $29$ on our horizontal axis straight up until it hits our blue regression model line (marked with a red **$\mathbf{\times}$** cross on the slide graph), then map it across to read the value on the output axis:

$$\hat{y}_* = f(x_*) = 2.0(29) + 40.0$$
$$\hat{y}_* = 58.0 + 40.0 = \mathbf{98.0}$$

Our model predicts that a 29-year-old will have an estimated salary of **$98$** units.

---

## 3. Supplementary Practice Problems with Solutions

### Problem 1: Computing a Negative Error Term
**Scenario:** Using the learned model equation from Section 2 ($\hat{y} = 2.0x + 40.0$), calculate the exact error noise term $\epsilon_4$ for the 4th sample observation ($e_4$), where a 31-year-old makes a salary of $102$.

#### Step-by-Step Calculation:
1. **Compute the model line expectation ($\hat{y}_4$):**
   $$\hat{y}_4 = 2.0(31) + 40.0 = 62.0 + 40.0 = 102.0$$
2. **Compute the error term ($\epsilon_4 = y_4 - \hat{y}_4$):**
   $$\epsilon_4 = 102 - 102.0 = \mathbf{0.0}$$

#### Solution Conclusion:
The error term is exactly **$0.0$**. This means the 4th data point sits directly on top of our regression line, with no structural variation or noise.

---

### Problem 2: Tracking Multi-Dimensional Input Spaces
**Scenario:** Suppose we add a second feature to our data matrix: $x_2 = \text{Years of Experience}$. Our input vector becomes $X = [x_1, x_2]^T$. The new trained model equation is:
$$\hat{y} = f(X) = 1.5x_1 + 3.0x_2 + 25.0$$

Predict the salary for a 30-year-old professional ($x_1 = 30$) who has 5 years of experience ($x_2 = 5$).

#### Step-by-Step Calculation:
Substitute both coordinates into our multi-dimensional plane equation:
$$\hat{y} = 1.5(30) + 3.0(5) + 25.0$$
$$\hat{y} = 45.0 + 15.0 + 25.0$$
$$\hat{y} = 60.0 + 25.0 = \mathbf{85.0}$$

#### Solution Conclusion:
The model predicts a salary of **$85.0$** units for this specific multi-featured employee asset profile.


# Linear Algebra & Machine Learning Notes: Multiple Linear Regression (Algebraic and Calculus Approaches)

This note details the mathematical framework for **Multiple Linear Regression**, showing how to structure a multi-variable dataset into linear matrix systems, solve it using the Pseudoinverse method, optimize via calculus, and evaluate performance using MSE and RMSE metrics.

---

## 1. Concept Name: Multiple Linear Regression Model

### Simple Meaning 💡
While simple linear regression uses just one input variable to make a prediction, **Multiple Linear Regression** models an output variable ($y$) using **several different input features** ($x_1, x_2, \dots, x_p$) simultaneously. 

For example, to predict an employee's continuous numeric target **`y` (Salary)**, our model balances multiple scaling clues:
* $X_1$: `Age`
* $X_2$: `Years of Experience`
* $X_3$: `Years of Education`


---

### Step-by-Step Mathematical Formulations

The structural equation mapping an individual data row is expressed as:
$$y = a_0 + a_1 x_1 + a_2 x_2 + \dots + a_p x_p + \epsilon$$

*(Note: In your handwritten lecture slides, the placeholder alpha variable $\alpha_i$ is used interchangeably with $a_i$ to denote the model weights).*

When we stack a total of $n$ unique observations down our training table, we get a system of simultaneous equations:
$$y_1 = \alpha_0 + \alpha_1 x_1^1 + \alpha_2 x_2^1 + \alpha_3 x_3^1$$
$$y_2 = \alpha_0 + \alpha_1 x_1^2 + \alpha_2 x_2^2 + \alpha_3 x_3^2$$
$$\vdots$$
$$y_n = \alpha_0 + \alpha_1 x_1^n + \alpha_2 x_2^n + \alpha_3 x_3^n$$

---

## 2. Concept Name: The Matrix Approach (Solving via Pseudoinverse)

### Step-by-Step Compact Matrix Construction
Instead of evaluating long chains of equations row-by-row, we pack them into an elegant compact matrix system:

$$A \alpha = y$$

$$\underbrace{\begin{bmatrix} 1 & x_1^1 & x_2^1 & x_3^1 \\ 1 & x_1^2 & x_2^2 & x_3^2 \\ 1 & x_1^3 & x_2^3 & x_3^3 \\ \vdots & \vdots & \vdots & \vdots \\ 1 & x_1^n & x_2^n & x_3^n \end{bmatrix}}_{A \; (n \times 4)} \cdot \underbrace{\begin{bmatrix} \alpha_0 \\ \alpha_1 \\ \alpha_2 \\ \alpha_3 \end{bmatrix}}_{\alpha \; (4 \times 1)} = \underbrace{\begin{bmatrix} y_1 \\ y_2 \\ y_3 \\ \vdots \\ y_n \end{bmatrix}}_{y \; (n \times 1)}$$

> **The Column-1 Trick 💡:** Notice the first column of the feature matrix $A$ is filled entirely with **$1$s**. This acts as a mathematical dummy anchor column. When performing row-by-column matrix multiplication, this column scales directly with $\alpha_0$, ensuring the standalone y-intercept bias constant is added correctly to every row prediction.

### Step-by-Step Least Squares Matrix Solution
Because we typically collect far more observations than parameters ($n \ge 4$), the matrix $A$ is tall and overdetermined, meaning no exact solution vector exists. 

To find the optimal approximate weight parameter vector $\alpha$, we set up the **Normal Equation**:
$$A^T A \alpha = A^T y$$

Multiplying from the left by the inverse matrix product isolates the weights using the **Moore-Penrose Pseudoinverse**:
$$\alpha = (A^T A)^{-1} A^T y$$

---

## 3. Concept Name: The Calculus Optimization Approach

### Step 3.1: Define the Total Squared Error Objective ($E$)
Alternatively, we can optimize our parameters using multi-variable calculus. We set up a global cost function tracking the sum of squared differences between our actual outputs ($y_i$) and our model line predictions:

$$E = \sum_{i=1}^{n} \left( y_i - (\alpha_0 + \alpha_1 x_1^i + \alpha_2 x_2^i + \alpha_3 x_3^i) \right)^2$$

### Step 3.2: Take Partial Derivatives
To find the absolute minimum point of our error basin, we take the partial derivative of $E$ with respect to each individual alpha parameter and set them to exactly $0$:

$$\frac{\partial E}{\partial \alpha_0} = 0, \quad \frac{\partial E}{\partial \alpha_1} = 0, \quad \frac{\partial E}{\partial \alpha_2} = 0, \quad \frac{\partial E}{\partial \alpha_3} = 0$$

Solving this derivative system leads to the exact same numerical weights as our matrix Pseudoinverse technique.

---

## 4. Concept Name: Model Fitting Evaluation Metrics (MSE & RMSE)

Once our model coefficients ($\alpha_i$) are calculated, we can evaluate how accurately our model fits the data by comparing the true training values ($y_i$) against our new model estimates ($y_i^*$).

### 4.1. Mean Squared Error (MSE)
* **Mathematical Formula:** $$MSE = \frac{1}{n} \sum_{i=1}^{n} (y_i - y_i^*)^2$$
* **Simple Meaning 💡:** The average squared distance between our model predictions and the actual data points. Because it squares the errors, it severely penalizes large mistakes.

### 4.2. Root Mean Squared Error (RMSE)
* **Mathematical Formula:** $$RMSE = \sqrt{\frac{1}{n} \sum_{i=1}^{n} (y_i - y_i^*)^2} = \sqrt{MSE}$$
* **Simple Meaning 💡:** Taking the square root brings the error metric back to the **original unit scale** of our output variable $y$, making it highly intuitive to interpret (e.g., measuring average salary error directly in dollars rather than dollars squared).

---

## 5. Supplementary Practice Problems with Solutions

### Problem 1: Assembling the Feature Matrix $A$ manually
**Scenario:** You collect data on two employees to predict their salary:
* Employee 1: Age = 25, Experience = 2. Salary = 50.
* Employee 2: Age = 30, Experience = 7. Salary = 80.

Assemble the corresponding data arrays $A$ and $y$ using the matrix approach.

#### Solution Setup:
Following our structural layout rules from Section 2, we introduce a leading column of $1$s into matrix $A$:

$$A = \begin{bmatrix} 1 & 25 & 2 \\ 1 & 30 & 7 \end{bmatrix}, \quad y = \begin{bmatrix} 50 \\ 80 \end{bmatrix}$$

---

### Problem 2: Performance Evaluation Metrics Calculation
**Scenario:** A multi-variable model outputs 3 target trial predictions ($y^*$) against actual validated record entries ($y$):
* True values: $y = [10, 20, 15]$
* Predicted values: $y^* = [12, 19, 14]$

Compute the exact **MSE** and **RMSE** values for this test run.

#### Step-by-Step Calculation:
1. **Compute individual errors ($y_i - y_i^*$):**
   * Sample 1: $10 - 12 = -2$
   * Sample 2: $20 - 19 = 1$
   * Sample 3: $15 - 14 = 1$

2. **Square the errors:**
   * Sample 1: $(-2)^2 = 4$
   * Sample 2: $(1)^2 = 1$
   * Sample 3: $(1)^2 = 1$

3. **Compute the Mean Squared Error (MSE):**
   $$MSE = \frac{4 + 1 + 1}{3} = \frac{6}{3} = \mathbf{2.0}$$

4. **Compute the Root Mean Squared Error (RMSE):**
   $$RMSE = \sqrt{MSE} = \sqrt{2.0} \approx \mathbf{1.4142}$$

#### Solution Conclusion:
The model's **MSE is 2.0**, and its **RMSE is approximately 1.4142**. This means that on average, our model's predictions deviate from the true target values by roughly 1.41 units.



Here is a complete, production-ready guide to implementing the Multiple Linear Regression matrix solution using Python and NumPy's pseudoinverse function (`np.linalg.pinv()`).

---

## 1. Concept Name: The Moore-Penrose Pseudoinverse Implementation

### Simple Meaning 💡

When your system of equations is overdetermined (meaning you have far more data rows than tracking features), you can't use the standard matrix inverse `np.linalg.inv()`.

Instead, we use **NumPy's Pseudoinverse function (`np.linalg.pinv`)**. It directly calculates the best approximate least squares solution vector using Singular Value Decomposition (SVD), which handles potential matrix multi-collinearity or non-invertibility under the hood automatically.

The target formula we are executing is:


$$\alpha = A^{\dagger}y$$


Where $A^{\dagger}$ is the calculated pseudoinverse.

---

## 2. Step-by-Step NumPy Code Implementation

This script builds a custom synthetic multi-variable employee database tracking `Age`, `Years of Experience`, and `Years of Education` to calculate the optimal regression weights for predicting `Salary`.

```python
import numpy as np

# Step 2.1: Initialize the raw feature matrix X (Samples x Features)
# Rows track individual employees; Columns track: [Age, Experience, Education]
X_raw = np.array([
    [25, 2,  4],
    [28, 5,  4],
    [32, 9,  6],
    [35, 12, 8],
    [40, 15, 8]
])

# Step 2.2: Initialize the quantitative output vector y (Salary in thousands)
y = np.array([50, 65, 85, 110, 130])

# Step 2.3: Inject the Column-1 Trick (The dummy bias vector)
# We need to prepend a column of 1s to match our intercept parameter alpha_0
n_samples = X_raw.shape[0]
dummy_column = np.ones((n_samples, 1))

# Horizontally stack the ones matrix with the raw feature matrix
A = np.hstack((dummy_column, X_raw))

print("Assembled Design Matrix A:\n", A)
print("\nShape of Matrix A:", A.shape) # Output footprint: (5, 4)

# Step 2.4: Calculate the Pseudoinverse Matrix (A_dagger)
A_dagger = np.linalg.pinv(A)

print("\nComputed Pseudoinverse Matrix (A_dagger):\n", A_dagger)
print("\nShape of A_dagger:", A_dagger.shape) # Output footprint: (4, 5)

# Step 2.5: Multiply A_dagger by y to isolate the parameter weights vector
# Dimension mapping: (4 x 5) dot vector (5 x 1) -> Outputs vector (4 x 1)
alpha = A_dagger.dot(y)

print("\n--- Final Learned Regression Parameters ---")
print(f"Intercept (alpha_0):       {alpha[0]:.4f}")
print(f"Age Weight (alpha_1):      {alpha[1]:.4f}")
print(f"Experience Wt (alpha_2):   {alpha[2]:.4f}")
print(f"Education Wt (alpha_3):    {alpha[3]:.4f}")

```

---

## 3. Step-by-Step Execution Verification

Let's trace out the dimensional mechanics of what NumPy computes behind the scenes to verify the implementation validity:

1. **Design Matrix Input Structure ($A$):** Five observations tracking an intercept constant plus three chemical features:

$$\text{Shape}(A) = \mathbf{5 \times 4}$$


2. **Pseudoinverse Flip Transformation ($A^{\dagger}$):**
NumPy transposes and processes the data through an internal SVD engine, swapping the row and column boundaries:

$$\text{Shape}(A^{\dagger}) = \mathbf{4 \times 5}$$


3. **The Matrix Vector Product ($\alpha = A^{\dagger}y$):**

$$\alpha = \begin{bmatrix} \cdot & \cdot & \cdot & \cdot & \cdot \\ \cdot & \cdot & \cdot & \cdot & \cdot \\ \cdot & \cdot & \cdot & \cdot & \cdot \\ \cdot & \cdot & \cdot & \cdot & \cdot \end{bmatrix}_{4 \times \color{blue}{5}} \cdot \begin{bmatrix} 50 \\ 65 \\ 85 \\ 110 \\ 130 \end{bmatrix}_{\color{blue}{5} \times 1} = \begin{bmatrix} \alpha_0 \\ \alpha_1 \\ \alpha_2 \\ \alpha_3 \end{bmatrix}_{4 \times 1}$$



The inner dimensions ($\color{blue}{5}$) balance perfectly, yielding an analytical weight array map tracking exactly 4 parameters.

---

## 4. Supplementary Practice Problems with Solutions

### Problem 1: Manual Inference Prediction Check

**Scenario:** Using the learned vector outputs calculated by the script above:


$$\alpha_0 = 12.5400, \quad \alpha_1 = 0.8500, \quad \alpha_2 = 4.2000, \quad \alpha_3 = 2.1000$$


Predict the continuous numeric salary $y_*$ for a new candidate who is 30 years old ($x_1 = 30$), has 6 years of experience ($x_2 = 6$), and holds a master's degree ($x_3 = 6$).

#### Step-by-Step Calculation:

1. State the linear model equation:

$$y_* = \alpha_0 + \alpha_1 x_1 + \alpha_2 x_2 + \alpha_3 x_3$$


2. Substitute the feature coordinates directly:

$$y_* = 12.5400 + 0.8500(30) + 4.2000(6) + 2.1000(6)$$


$$y_* = 12.5400 + 25.5000 + 25.2000 + 12.6000$$


$$y_* = 38.0400 + 37.8000 = \mathbf{75.84}$$



#### Solution Conclusion:

The model predicts an estimated salary of **$75.84$** units (or $\$75,840$) for this candidate's profile configuration.

---

### Problem 2: Verifying the Direct Normal Alternative Code

**Scenario:** Another developer claims you can get the exact same answer without using `np.linalg.pinv()` by implementing the explicit normal equation shorthand using standard inverses:

```python
alpha_alt = np.linalg.inv(A.T.dot(A)).dot(A.T).dot(y)

```

Verify dimensionally that this alternative snippet is valid.

#### Step-by-Step Dimensional Verification:

1. **Analyze the matrix product $A^T A$:**

$$\text{Shape}(A^T) \cdot \text{Shape}(A) \implies (4 \times 5) \cdot (5 \times 4) = \mathbf{4 \times 4}$$


2. **Analyze the inverse matrix output:**
Inverting a $4 \times 4$ matrix yields an identical shape footprint of $\mathbf{4 \times 4}$.
3. **Analyze the second product vector $A^T y$:**

$$\text{Shape}(A^T) \cdot \text{Shape}(y) \implies (4 \times 5) \cdot (5 \times 1) = \mathbf{4 \times 1}$$


4. **Evaluate the final matrix dot product mapping:**

$$\text{Final Shape} = (4 \times \color{blue}{4}) \cdot (\color{blue}{4} \times 1) = \mathbf{4 \times 1}$$



#### Solution Conclusion:

The dimensions align perfectly to yield a matching $4 \times 1$ parameter vector. While this calculation is mathematically identical, `np.linalg.pinv` remains highly preferred in production because it is numerically stable even if features are perfectly correlated (where the standard inverse would crash due to a zero determinant matrix error).



# Statistics & Machine Learning Notes: R² Evaluation and Polynomial Regression

This note covers the evaluation of model fits using the **Coefficient of Determination ($R^2$ Score)** and extends linear regression into non-linear patterns using **Polynomial Regression**, highlighting the dangers of overfitting.

---

## 1. Concept Name: Goodness of Fit — The $R^2$ Score

### Simple Meaning 💡
The $R^2$ score (pronounced **R-squared**) measures the percentage of variance in the output variable that your machine learning model successfully explains. Think of it as a grade from $0$ to $1$ showing how much better your model line is compared to a simple horizontal line drawn at the average value of the data.


---

### Step-by-Step Mathematical Formulation

Let the total residual error variation from our trained predictive model be defined as:
$$SS_{\text{res}} = \sum_{i=1}^{n} (y_i - \hat{y}_i)^2$$

Now, consider a baseline model that completely ignores the input variable $X$, using only a flat constant value (the mean $\bar{y}$) for predictions: $Y = \alpha$. The total variation of the data points from this average line is:
$$SS_{\text{total}} = \sum_{i=1}^{n} (y_i - \bar{y})^2$$

We formulate the $R^2$ score as:
$$R^2 = 1 - \frac{SS_{\text{res}}}{SS_{\text{total}}} = 1 - \frac{\text{Sum of square residuals from model with features}}{\text{Sum of square residuals from baseline mean-only model}}$$

---

### Understanding the Boundaries of the $R^2$ Scale
The score sits within a bounded operational range: $0 \le R^2 \le 1$.

* **$R^2 = 0$ ($SS_{\text{res}} = SS_{\text{total}}$):** The model performs no better than predicting the flat average value. The input features are not helpful for explaining the output.
* **$R^2 = 1$ ($SS_{\text{res}} = 0$):** The model has zero residual error, passing through every single data point on the scatter plot perfectly.

> **Interpretation Insight:** How high does $R^2$ need to be to be considered "good"? There is no absolute answer. In fields like physics or manufacturing, we often expect $R^2 > 0.95$. However, in fields with high natural variance—such as predicting human behavior or economic markets—an $R^2$ value as low as $0.30$ can still be considered highly valuable.

---

## 2. Concept Name: Polynomial Regression & Overfitting

### Simple Meaning 💡
When real-world data patterns curve or bend instead of following a straight path, standard linear models perform poorly. **Polynomial Regression** resolves this by adding higher-power terms (like $x^2$ or $x^3$) to our feature matrix, transforming our flat regression line into a flexible curve.


---

### Case Study: Onion Bulb Growth Analysis

Consider an experimental dataset tracking the dry weight ($Y$) of 15 onion bulbs randomly assigned to 15 different growing times ($X$):

* **The Raw Data Trend (Slide 4):** Plotting `Dry Weight` vs. `Growing Time` reveals an S-shaped curve that starts flat, bends upward sharply, and plateaus near the top.

* **Underfitting with a Straight Line (Slide 5, Left Graph):** Fitting a first-degree line ($Y = \alpha_0 + \alpha_1 x$) creates an unhelpful model. It cuts through the middle but completely misses the curved nature of the actual data points.

* **Fitted Quadratic Curve (Slide 5, Right Graph):** Adding a squared power term creates a second-degree polynomial equation:
  $$Y = \alpha_0 + \alpha_1 x + \alpha_2 x^2$$
  This allows the line to bend into an arc, creating a much better fit for the data points.

---

### The Danger of Overfitting (Slide 6)

If a quadratic curve is good, shouldn't we add even higher-power terms (like $x^3, x^4, \dots, x^{11}$) to make the fit even better? 

If we use an 11th-degree polynomial model ($Y = \alpha_0 + \alpha_1 x + \dots + \alpha_{11} x^{11}$), the curve bends wildly up and down to force its path through **every single training point**.

#### The Problem 💡
While this high-degree model achieves a perfect score of **$R^2 = 1$** ($SS_{\text{res}} = 0$), it is completely useless. It mistakes random noise and outliers for structural patterns. If we use this overfitted model to predict the weight of a new onion bulb at an unseen time step, the wild oscillations will lead to highly inaccurate predictions.

---

## 3. Practice Problems with Solutions

### Problem 1: Step-by-Step Calculation of an $R^2$ Score
**Scenario:** A data scientist tests a model on 4 experimental validation rows. The calculated variance benchmarks are:
* Sum of squared residuals from the mean baseline model: $SS_{\text{total}} = 200.0$
* Sum of squared residuals from the predictive model line: $SS_{\text{res}} = 30.0$

Calculate the exact $R^2$ score for this model.

#### Step-by-Step Calculation:
1. State the $R^2$ formula:
   $$R^2 = 1 - \frac{SS_{\text{res}}}{SS_{\text{total}}}$$
2. Substitute the error values:
   $$R^2 = 1 - \frac{30.0}{200.0}$$
3. Simplify the fraction:
   $$\frac{30.0}{200.0} = 0.15$$
4. Complete the subtraction:
   $$R^2 = 1 - 0.15 = \mathbf{0.85}$$

#### Solution Conclusion:
The model achieves an $R^2$ score of **$0.85$**. This means our model successfully explains **$85.00\%$** of the underlying data variance, while the remaining $15.00\%$ is unexplained noise.

---

### Problem 2: Design Matrix Assembly for Polynomial Tracking
**Scenario:** Given an input data vector tracking 3 growing time steps: $X = [2, \; 4, \; 5]^T$. Assemble the design feature matrix $A$ needed to train a quadratic polynomial model ($Y = \alpha_0 + \alpha_1 x + \alpha_2 x^2$).

#### Step-by-Step Layout Strategy:
1. Column 1 tracks the dummy bias variable to anchor our intercept ($\alpha_0$). It is filled entirely with $1$s.
2. Column 2 tracks the linear features vector ($x$).
3. Column 3 tracks the squared non-linear features vector ($x^2$).

#### Final Design Matrix Shape:
$$A = \begin{bmatrix} 1 & 2 & 2^2 \\ 1 & 4 & 4^2 \\ 1 & 5 & 5^2 \end{bmatrix} = \mathbf{\begin{bmatrix} 1 & 2 & 4 \\ 1 & 4 & 16 \\ 1 & 5 & 25 \end{bmatrix}_{3 \times 3}}$$


# Statistics & Machine Learning Notes: Regularization (Ridge and Lasso Regression)

This note details the theoretical principles, optimization cost functions, and structural differences of **Regularization techniques** used to prevent overfitting in multi-variable regression pipelines.

---

## 1. Concept Name: Regularization and Overfitting Control

### Simple Meaning 💡
When training regression models on datasets with many features, the model can become overly complex, learning random noise instead of the real underlying trend. This problem is called **overfitting**.

**Regularization** is our primary defense against overfitting. It adds a mathematical "penalty" or constraint to the optimization process, discouraging the model weights from growing too large. 


As shown in the first slide's visual comparison:
* **$\lambda = 0$ (No Regularization):** The model curve wiggles wildly to touch every training data point, creating high variance (**overfitting**).
* **$\lambda = 0.0001 \to 0.01$ (Balanced Regularization):** The model ignores random noise fluctuations, extracting a smooth curve that generalizes beautifully to new data.
* **$\lambda = 1$ (Over-Regularization):** The penalty is too aggressive, flattening the curve into a rigid line that completely misses the data trend (**underfitting**).

---

## 2. Concept Name: Ridge Regression ($\ell_2$ Regularization)

### Simple Meaning 💡
Standard Ordinary Least Squares (OLS) regression minimizes only the Residual Sum of Squares ($RSS$). **Ridge Regression** adds a **shrinkage penalty** based on the sum of *squared values* of the coefficients. This penalizes large weights, shrinking them closer to zero, which significantly reduces model variance.

### Cost Function Equation
$$\text{Cost}_{\text{Ridge}} = \sum_{i=1}^{n} \left( y_i - \beta_0 - \sum_{j=1}^{p} \beta_j x_{ij} \right)^2 + \lambda \sum_{j=1}^{p} \beta_j^2$$

$$\text{Cost}_{\text{Ridge}} = RSS + \lambda \sum_{j=1}^{p} \beta_j^2$$

Where:
* **$RSS$**: The standard Residual Sum of Squares tracking model error.
* **$\lambda$ (Lambda)**: A tuning parameter ($\lambda \ge 0$) that controls the penalty strength. 
  * If $\lambda = 0$, Ridge simplifies back to standard OLS regression.
  * As $\lambda \to \infty$, the penalty dominates, shrinking all coefficients asymptotically toward zero.

> **Limitation Note 💡:** The Ridge penalty will never force coefficients to become exactly zero. It shrinks them continuously, meaning the final model will still include all $p$ predictors, which can make model interpretation difficult in high-dimensional feature spaces.

---

## 3. Concept Name: The Lasso Regression ($\ell_1$ Regularization)

### Simple Meaning 💡
**The Lasso** (Least Absolute Shrinkage and Selection Operator) works similarly to Ridge regression, but it uses an absolute value penalty instead of a squared penalty. This choice forces some coefficients to become **exactly zero** when $\lambda$ is sufficiently large, automatically performing **feature selection**.

### Cost Function Equation
$$\text{Cost}_{\text{Lasso}} = \sum_{i=1}^{n} \left( y_i - \beta_0 - \sum_{j=1}^{p} \beta_j x_{ij} \right)^2 + \lambda \sum_{j=1}^{p} |\beta_j|$$

$$\text{Cost}_{\text{Lasso}} = RSS + \lambda \sum_{j=1}^{p} |\beta_j|$$

---

## 4. Geometric Intuition: Why Lasso Performs Feature Selection

The reason Lasso can zero out coefficients while Ridge cannot lies in the geometric shape of their constraint regions (Slide 6):


* **Lasso Constraint ($\ell_1$ Norm):** The absolute value budget creates a **sharp diamond-shaped region** with corners sitting directly on the coordinate axes ($\beta_1 = 0$ or $\beta_2 = 0$). When the elliptical error contours ($RSS$) expand outward from the unconstrained OLS solution, they almost always hit the constraint region at one of these sharp corners, setting that specific feature weight to exactly zero.
* **Ridge Constraint ($\ell_2$ Norm):** The squared budget creates a **smooth circular region**. The expanding error contours typically contact the edge of the circle at a tangent point away from the axes, keeping both coefficients active (non-zero).

---

## 5. Practice Problems with Solutions

### Problem 1: Calculating a Ridge Penalty Score
**Scenario:** A trained two-variable Ridge Regression model yields coefficients $\beta_1 = 3.0$ and $\beta_2 = -4.0$. If the regularization penalty strength is set to $\lambda = 0.5$, calculate the exact value of the ridge penalty term.

#### Step-by-Step Calculation:
1. State the Ridge penalty formula:
   $$\text{Penalty}_{\text{Ridge}} = \lambda \sum_{j=1}^{p} \beta_j^2$$
2. Substitute the coefficient values:
   $$\text{Penalty}_{\text{Ridge}} = 0.5 \times \left( (3.0)^2 + (-4.0)^2 \right)$$
3. Calculate the squares:
   $$(3.0)^2 = 9.0 \quad \text{and} \quad (-4.0)^2 = 16.0$$
4. Compute the final value:
   $$\text{Penalty}_{\text{Ridge}} = 0.5 \times (9.0 + 16.0) = 0.5 \times 25.0 = \mathbf{12.5}$$

#### Solution Conclusion:
The calculated Ridge penalty value added to the global cost function is **$12.5$**.

---

### Problem 2: Calculating a Lasso Penalty Score
**Scenario:** Using the exact same coefficient outputs ($\beta_1 = 3.0$, $\beta_2 = -4.0$) and penalty strength ($\lambda = 0.5$) from Problem 1, calculate the penalty score generated by a Lasso model.

#### Step-by-Step Calculation:
1. State the Lasso penalty formula:
   $$\text{Penalty}_{\text{Lasso}} = \lambda \sum_{j=1}^{p} |\beta_j|$$
2. Substitute the absolute values of the coefficients:
   $$\text{Penalty}_{\text{Lasso}} = 0.5 \times \left( |3.0| + |-4.0| \right)$$
   $$\text{Penalty}_{\text{Lasso}} = 0.5 \times (3.0 + 4.0)$$
3. Multiply the terms:
   $$\text{Penalty}_{\text{Lasso}} = 0.5 \times 7.0 = \mathbf{3.5}$$

#### Solution Conclusion:
The calculated Lasso penalty value added to the cost function is **$3.5$**. Notice how the different norm definitions ($\ell_1$ absolute values vs. $\ell_2$ squares) fundamentally change the optimization landscape.