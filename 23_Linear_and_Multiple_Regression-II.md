# Data Science & Machine Learning Notes: Exploratory Data Analysis (EDA) for Simple Linear Regression

This note provides a step-by-step walkthrough of performing initial **Exploratory Data Analysis (EDA)** on a student performance dataset using Python, Pandas, and NumPy before training a Simple Linear Regression model.

---

## 1. Concept Name: Simple Linear Regression & Data Loading

### Simple Meaning 💡
**Simple Linear Regression** models the relationship between a single independent input variable ($x$) and a single dependent continuous numeric output variable ($y$). 
* In this example, we try to model how the number of **Hours** a student spends studying ($x$) impacts their final exam **Scores** ($y$).
* The standard mathematical straight-line equation we want to fit is:
  $$Y = a_0 + a_1X$$
  Where $a_0$ is the y-intercept bias and $a_1$ is the slope coefficient.


---

### Step-by-Step Python Environment Setup

First, we load the required open-source data manipulation and visualization libraries into our Python environment:

```python
import numpy as np         # Used for rapid vector matrix math operations
import pandas as pd        # Used to structure our tabular CSV files into DataFrames
import matplotlib.pyplot as plt  # Used to render plots and trend lines

```

In a Jupyter or Google Colab notebook environment, we load a raw spreadsheet file named `student_scores.csv` directly into a DataFrame object:

```python
from google.colab import files

# 1. Trigger the interactive file upload prompt window
uploaded = files.upload()

# 2. Read the binary stream of the target uploaded spreadsheet into a DataFrame
score = pd.read_csv("student_scores.csv")

```

---

## 2. Concept Name: Structural Dimension & Inspection Checking

Once a dataset is parsed into memory, the first step in EDA is to check the baseline dimensional footprint and confirm that the columns loaded correctly.

```python
# Check table matrix rows and columns
print("DataFrame Dimensional Shape:", score.shape)
# Output: (25, 2)

```

#### Meaning of the Shape Dimension 💡

The output `(25, 2)` states that our spreadsheet contains exactly $m = 25$ independent row observations (individual student records) and $n = 2$ feature column tracks (`Hours` and `Scores`).

---

### Step 2.1: Inspecting Top Rows using `.head()`

We call `score.head()` to render a preview table tracking the first 5 records of our student cohort matrix:

```python
# Render the top 5 observation data rows
print(score.head())

```

**DataFrame Preview Output Matrix:**

| Index | Hours ($x$) | Scores ($y$) |
| --- | --- | --- |
| **0** | 2.5 | 21 |
| **1** | 5.1 | 47 |
| **2** | 3.2 | 27 |
| **3** | 8.5 | 75 |
| **4** | 3.5 | 50 |

---

## 3. Concept Name: Descriptive Statistical Summary Check

### Simple Meaning 💡

Before fitting a regression model, it's essential to understand the distribution of the features. We use the `.describe()` method to calculate the central tendency, spread, and range boundaries across all numerical columns.

```python
# Generate structural summary statistic distributions
print(score.describe())

```

---

### Step-by-Step Statistical Analysis and Calculations

The table summary output maps the following explicit distribution values:

| Metric | Hours Column ($x$) | Scores Column ($y$) |
| --- | --- | --- |
| **count** | 25.000000 | 25.000000 |
| **mean** | 5.012000 | 53.560000 |
| **std** | 2.525094 | 27.071018 |
| **min** | 1.100000 | 4.000000 |
| **25%** | 2.700000 | 30.000000 |
| **50%** | 4.800000 | 50.000000 |
| **75%** | 7.400000 | 76.000000 |
| **max** | 9.200000 | 95.000000 |

#### Breaking Down the Metrics:

* **`mean` (Average Position Center):** The balancing center of our data features. The average student in this group studied for $\approx 5.01$ hours and scored an exam grade of $\approx 53.56$.
* **`std` (Standard Deviation Spread):** Measures the spread or dispersion of the data points from their mean. A standard deviation of $27.07$ for scores indicates that individual test results vary significantly across the cohort.
* **`50%` (Median Value):** The middle value of the dataset. Exactly half of the students studied less than $4.8$ hours, and half studied more.

---

## 4. Practice Problems with Solutions

### Problem 1: Manual Calculation of the Coordinate Feature Range

**Scenario:** Using the summary matrix output from Section 3, calculate the exact **Range** for both the `Hours` input variable and the `Scores` target variable. The statistical range is defined as:


$$\text{Range} = \text{Maximum Value} - \text{Minimum Value}$$

#### Step-by-Step Calculation:

1. **Find Range for Hours ($x$):** Extract `max` and `min` values from the table.

$$\text{Range}_x = 9.200000 - 1.100000 = \mathbf{8.100000 \text{ hours}}$$


2. **Find Range for Scores ($y$):** Extract `max` and `min` values from the table.

$$\text{Range}_y = 95.000000 - 4.000000 = \mathbf{91.000000 \text{ score points}}$$



#### Solution Conclusion:

The study times span a range of **$8.1$ hours**, while the test results span a wide range of **$91$ points**.

---

### Problem 2: Detecting Outliers using the Interquartile Range (IQR)

**Scenario:** Calculate the Interquartile Range ($IQR = Q3 - Q1$) for the `Scores` feature using the values from the 75th percentile ($Q3$) and 25th percentile ($Q1$) to evaluate the spread of the middle 50% of the dataset.

#### Step-by-Step Calculation:

1. Identify the quartiles for the `Scores` feature from the descriptive summary table:
* $Q1$ (25th percentile) = $30.0$
* $Q3$ (75th percentile) = $76.0$


2. Compute the difference:

$$IQR = Q3 - Q1 = 76.0 - 30.0 = \mathbf{46.0}$$



#### Solution Conclusion:

The Interquartile Range for the exam results is **$46.0$ points**. This indicates that the middle 50% of the students scored within a relatively tight 46-point range, which helps reveal the overall structure of the data distribution before fitting a linear model.




# Python Code Walkthrough: Simple Linear Regression with Scikit-Learn

This note tracks a complete programmatic walkthrough for implementing **Simple Linear Regression** on a dataset of student study hours vs. exam scores. It covers feature slicing, model fitting, parameter extraction, and evaluation metrics.

---

## 1. Concept Name: Feature Slicing and Extraction

### Simple Meaning 💡
Before passing a dataset into a machine learning algorithm, you must separate your features into two distinct structures:
* **$X$ (Independent Variables Matrix):** The input signals or clues (must be structured as a 2D matrix shape, even if it contains only one column).
* **$y$ (Dependent Target Vector):** The continuous numeric output value we are trying to predict (structured as a flat 1D array).

```python
# Extract the features matrix (all rows, all columns except the last one)
X = score.iloc[:, :-1].values

# Extract the target vector (all rows, column index 1)
y = score.iloc[:, 1].values

```

---

## 2. Concept Name: Model Fitting and Training

We import the `LinearRegression` class from `sklearn.linear_model`. Calling `.fit(X, y)` runs an optimization algorithm behind the scenes to find the straight-line equation that minimizes the sum of squared errors for our data points.

```python
from sklearn.linear_model import LinearRegression

# 1. Initialize the model object
reg = LinearRegression()

# 2. Fit the model to find the best-fitting line coefficients
reg.fit(X, y)

```

---

## 3. Concept Name: Parameter Extraction & Equation Mapping

Once training completes, we extract the learned straight-line parameters using the `.intercept_` and `.coef_` attributes:

```python
print("Intercept (a_0):", reg.intercept_)  # Output: 4.702020043600342
print("Slope (a_1):", reg.coef_)          # Output: [9.74820031]

```

### Building the Final Model Equation 💡

Substituting these extracted parameters into our straight-line framework ($Y = a_0 + a_1X$) yields our final predictive model equation:

$$\text{Predicted Exam Score} = 4.7020 + 9.7482 \times (\text{Study Hours})$$

* **The Intercept ($4.7020$):** Represents the baseline score. If a student studies for 0 hours ($X=0$), the model expects them to score approximately $4.70$ points on the exam.
* **The Slope ($9.7482$):** Represents the marginal gain. For every $1$ additional hour a student studies, their predicted exam score increases by approximately $9.75$ points.

---

## 4. Concept Name: Inference and Model Evaluation

### Step 4.1: Generate Predictions Array (`y_pred`)

We pass the input column matrix `X` into `.predict()` to calculate our model's estimated score outputs (`y_pred`) for every student row.

```python
# Compute model predictions
y_pred = reg.predict(X)

# Compare actual vs. predicted values in a DataFrame
df_comparison = pd.DataFrame({'Actual': y, 'Predicted': y_pred})
print(df_comparison.head(3))

```

**Actual vs. Predicted Comparison Preview Table:**

| Index | Actual Score ($y$) | Predicted Score ($\hat{y}$) |
| --- | --- | --- |
| **0** | 21 | 29.072521 |
| **1** | 47 | 54.417842 |
| **2** | 27 | 35.896261 |

---

### Step 4.2: Compute Performance Evaluation Metrics (MSE & $R^2$)

We import evaluation metrics from `sklearn.metrics` to measure the accuracy of our model fit.

```python
from sklearn.metrics import mean_squared_error, r2_score

print('Mean Squared Error (MSE):', mean_squared_error(y, y_pred)) # Output: 121.86
print('R2 Score (Goodness of Fit):', r2_score(y, y_pred))          # Output: 0.83

```

#### Meaning of the Performance Metrics 💡

* **$MSE = 121.86$:** On average, the squared deviation between our model predictions and the actual test results is 121.86 score points squared. Taking the square root gives an average error of $\sqrt{121.86} \approx 11.04$ points.
* **$R^2 = 0.83$:** Our model explains **$83.00\%$** of the variance in exam scores based on study hours alone. The remaining $17.00\%$ of variation is due to unexplained random noise (e.g., student focus, exam difficulty, or luck).

---

### Step 4.3: Visualizing the Regression Line

We create a final scatter plot to visualize our regression model. We plot the raw data points as black dots and overlay our learned straight-line model equation in blue:

```python
# Plot actual data points as a black scatter plot
plt.scatter(X, y, color='black', label="Actual Data Rows")

# Overlay the calculated regression line in blue
plt.plot(X, y_pred, color='blue', linewidth=2, label="Fitted Regression Line")

plt.xlabel('Hours Studied')
plt.ylabel('Exam Scores')
plt.title('Exam Scores vs. Study Hours')
plt.legend()
plt.grid(True, linestyle='--', alpha=0.5)
plt.show()

```

---

## 5. Practice Problems with Solutions

### Problem 1: Manual Prediction Calculation

**Scenario:** A student is planning their final exam preparation and decides they can dedicate exactly $X = 7.0$ hours to studying this subject. Using our trained regression model parameters, calculate their predicted exam score manually.

#### Step-by-Step Calculation:

1. State the trained model linear equation:

$$\text{Score} = 4.702020 + 9.748200 \times \text{Hours}$$


2. Substitute the student's study time ($X = 7.0$):

$$\text{Score} = 4.702020 + 9.748200 \times (7.0)$$


3. Compute the product:

$$9.748200 \times 7 = 68.2374$$


4. Complete the final addition:

$$\text{Score} = 4.702020 + 68.2374 = \mathbf{72.93942}$$



#### Solution Conclusion:

The model predicts that a student who studies for 7 hours will achieve an exam score of approximately **$72.94$ points**.

---

### Problem 2: Tracking the Sample Residual Difference

**Scenario:** Take the first student entry from our DataFrame preview ($y = 21$ points achieved after studying for $X = 2.5$ hours).

1. Calculate their predicted model line coordinate value ($\hat{y}$) manually.
2. Calculate the exact residual error value ($e = y - \hat{y}$) for this sample.

#### Step-by-Step Calculation:

1. **Find the prediction value ($\hat{y}$):** Substitute $X = 2.5$ hours into our regression equation.

$$\hat{y} = 4.702020 + 9.748200 \times (2.5)$$


$$\hat{y} = 4.702020 + 24.3705 = \mathbf{29.07252 \text{ points}}$$



*(Note: This matches the first row prediction in our comparison table output).*
2. **Compute the residual error value ($e = y - \hat{y}$):**

$$e = 21 - 29.07252 = \mathbf{-8.07252 \text{ points}}$$



#### Solution Conclusion:

The residual error for this student is **$-8.07$ points**. The negative sign indicates that this specific student scored approximately 8.07 points *lower* than what our general model line expected for someone studying 2.5 hours. Geometrically, this data point floats directly underneath our blue model line.


# Python Code Walkthrough: Multiple Linear Regression with Scikit-Learn

This note tracks a complete machine learning workflow to implement **Multiple Linear Regression** on a dataset of 50 startup companies, using financial investments to predict their total operational profit.

---

## 1. Concept Name: Tabular Feature Matrix Engineering

### Simple Meaning 💡
When building a predictive model with multiple inputs, we separate our columns using explicit keys.
* **Features Matrix ($X$):** The input financial signals. We use `.drop()` to isolate everything except our target column.
* **Target Vector ($y$):** The continuous numeric output value we want to predict (`Profit`).

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

# 1. Load the tabular CSV startup dataset into memory
Score = pd.read_csv("startup.csv")

# 2. Separate the dataset into independent features and dependent targets
X = Score.drop('Profit', axis=1) # Drops the output column to leave features
y = Score['Profit']              # Selects only the target profit vector

```

---

### Step 1.1: Training and Validation Data Partitions

To evaluate our model's performance on unseen data, we split our 50 companies into a **80% training set** (to learn parameters) and a **20% testing set** (for validation testing).

```python
from sklearn.model_selection import train_test_split

# Partition the arrays randomly into train and test subsets
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

```

---

## 2. Concept Name: Multi-Variable Fitting & Parameter Mapping

We initialize the `LinearRegression` engine. Calling `.fit(X_train, y_train)` calculates the multi-dimensional plane that minimizes the global sum of squared residual errors.

```python
from sklearn.linear_model import LinearRegression

# 1. Initialize the regressor object
regressor = LinearRegression()

# 2. Train the model using the training datasets
regressor.fit(X_train, y_train)

```

---

### Step 2.1: Parameter Key Extraction

Once training completes, we extract our intercept constant ($\alpha_0$) and our independent sloped weights ($\alpha_1, \alpha_2, \alpha_3$):

```python
print("Intercept Value:", regressor.intercept_)
# Output: 42989.00816508665

print("Coefficient Weights Vector:", regressor.coef_)
# Output: [0.77884104,  0.0293919,   0.03471025]

```

### Building the Final Model Prediction Equation 💡

Substituting these extracted coefficients back into our multiple linear model framework yields our completed prediction function:

$$\hat{y} = 42989.0082 + 0.7788 \times (x_{\text{R\&D Spend}}) + 0.0294 \times (x_{\text{Administration}}) + 0.0347 \times (x_{\text{Marketing Spend}})$$

#### Understanding the Financial Weights:

* **The Intercept ($42,989.01$):** The baseline profit floor. If a company spends $\$0$ on R&D, Administration, and Marketing, its predicted profit is roughly $\$42,989.01$.
* **R&D Spend Weight ($0.7788$):** The strongest financial driver. For every extra dollar a startup invests in R&D, its profit is expected to increase by approximately $\$0.78$.

---

## 3. Concept Name: Validation Inference and Analysis Plots

### Step 3.1: Generate Predictions Array (`y_pred`)

We pass our unseen test observations (`X_test`) into `.predict()` to evaluate model accuracy against the true results (`y_test`).

```python
# Compute validation estimates
y_pred = regressor.predict(X_test)

# Map true values vs predictions side-by-side inside a DataFrame
df_eval = pd.DataFrame({'Actual': y_test, 'Predicted': y_pred})
print(df_eval.head(4))

```

**Actual vs. Predicted Validation Comparison Table:**

| Row Index | Actual Profit ($y$) | Predicted Profit ($\hat{y}$) |
| --- | --- | --- |
| **28** | 103282.38 | 103901.896970 |
| **11** | 144259.40 | 132763.059931 |
| **10** | 146121.95 | 133567.903700 |
| **41** | 77798.83 | 72911.789767 |

---

### Step 3.2: Plotting Residual Visualizations

To evaluate the fit across a single feature column (such as `Administration`), we create a validation scatter plot. We map the true testing samples as black dots and the corresponding model predictions as blue dots:

```python
# Plot true observations as black markers
plt.scatter(X_test['Administration'], y_test, color='black', label='Actual Data Points')

# Plot corresponding predictions as blue markers
plt.scatter(X_test['Administration'], y_pred, color='blue', label='Model Predictions')

# Clear tick mark boundaries for generic relative trend viewing
plt.xticks(())
plt.yticks(())
plt.xlabel('Administration Expenditures')
plt.ylabel('Company Profits')
plt.title('Validation Residual Analysis: Administration')
plt.legend()
plt.show()

```

#### Graphical Residual Analysis 💡

On the resulting plot, the vertical gap between any matching black dot (actual) and blue dot (prediction) represents that company's specific **residual error**.

* If a blue dot sits close to its black partner, the model successfully captured that startup's financial profile.
* If the dots are far apart, it indicates a larger error caused by unexplained market factors or variance.

---

## 4. Practice Problems with Solutions

### Problem 1: Manual Prediction from a Financial Profile Vector

**Scenario:** A new startup company registers the following asset expenditure metrics:

* R&D Spend ($x_1$) = $\$100,000$
* Administration Spend ($x_2$) = $\$50,000$
* Marketing Spend ($x_3$) = $\$200,000$

Calculate this company's predicted profit manually using the regression model equation.

#### Step-by-Step Calculation:

1. State the completed linear regression model equation:

$$\hat{y} = 42989.0082 + 0.778841(x_1) + 0.029392(x_2) + 0.034710(x_3)$$


2. Substitute the expenditure values:

$$\hat{y} = 42989.0082 + 0.778841(100000) + 0.029392(50000) + 0.034710(200000)$$


3. Compute the products:
* R&D: $0.778841 \times 100000 = 77884.10$
* Administration: $0.029392 \times 50000 = 1469.60$
* Marketing: $0.034710 \times 200000 = 6942.00$


4. Sum all terms together to find total estimated profit:

$$\hat{y} = 42989.0082 + 77884.10 + 1469.60 + 6942.00$$


$$\hat{y} = 120873.1082 + 8411.60 = \mathbf{129284.7082}$$



#### Solution Conclusion:

The model predicts a final profit of **$\$129,284.71$** for this startup's expenditure configuration.

---

### Problem 2: Calculating Validation Residual Errors

**Scenario:** Using the comparison table output from Row Index 28, the company recorded an actual profit of $y = 103282.38$, while our model estimated a profit of $\hat{y} = 103901.896970$. Calculate the exact residual value for this company.

#### Step-by-Step Calculation:

1. State the residual definition formula:

$$e_i = y_i - \hat{y}_i$$


2. Substitute the values from the validation table:

$$e_{28} = 103282.38 - 103901.896970$$


3. Perform the subtraction:

$$e_{28} = \mathbf{-619.516970 \text{ dollars}}$$



#### Solution Conclusion:

The residual error value for this validation company is **$-\$619.52$**. The negative sign indicates that this company made roughly $\$619.52$ *less* profit than what our model expected based on its expenditures.


# Python Code Walkthrough: Polynomial Regression Analysis and Model Degree Selection

This note provides a step-by-step programmatic walkthrough using **NumPy** and **Scikit-Learn** to fit different degrees of polynomial curves to a non-linear dataset, tracking how performance metrics change at each stage.

---

## 1. Concept Name: The Polynomial Regression Fitting Architecture

### Simple Meaning 💡
When data points follow a curve instead of a straight line, we can use NumPy's `np.polyfit()` function to add higher-power terms (like $x^2, x^3, \dots$) to our model. This lets us control the complexity of the curve by adjusting the **degree** parameter:
* **Degree 1 (Linear Line):** A rigid straight line that cannot bend.
* **Degree 2 (Quadratic Curve):** Can bend once, forming a smooth parabola.
* **Degree 3 (Cubic Curve):** Can bend twice, forming an S-shape.
* **Higher Degrees:** Can bend multiple times, fitting more complex shapes but increasing the risk of overfitting.

---

### Step-by-Step Code Walkthrough

We use the onion bulb growth dataset (15 data points matching time $x$ to dry weight $y$). We use `np.linspace(1, 15, 100)` to generate 100 evenly spaced points along the x-axis, creating a smooth line for plotting our model's predictions.

```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn.metrics import r2_score, mean_squared_error

# 1. Define the raw dataset vectors
x = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15]
y = [16.08, 33.83, 65.8, 97.2, 191.55, 326.20, 386.87, 520.53, 590.03, 651.92, 724.93, 699.56, 689.96, 637.56, 717.41]

# 2. Generate a dense array of x-coordinates for smooth plotting
myline = np.linspace(1, 15, 100)

```

---

## 2. Model Performance Tracking Across Different Degrees

We evaluate how changing the polynomial degree affects the model's fit by monitoring the $R^2$ score and Mean Squared Error (MSE).

### Step 2.1: Fitting a Degree-1 Model (Linear Underfitting)

We fit a straight line by setting the degree parameter to `1`.

```python
# Train a 1st-degree linear model: Y = a_0 + a_1*x
mymodel_1 = np.poly1d(np.polyfit(x, y, 1))

print(f"Degree-1 R2 Score:         {r2_score(y, mymodel_1(x)):.2f}")
print(f"Degree-1 MSE Error:        {mean_squared_error(y, mymodel_1(x)):.2f}")

```

#### Output Metrics & Visual Inspection:

* **$R^2$ Score:** $0.91$
* **MSE Error:** $6811.63$

> **Analysis 💡:** While an $R^2$ of $0.91$ seems high, the plot reveals a systematic issue. The straight line consistently cuts across the curve, underestimating the data in the middle and overestimating it at both ends. The high MSE ($6811.63$) confirms a poor fit to the underlying pattern.

---

### Step 2.2: Fitting a Degree-2 Model (Quadratic Fit)

We increase the degree to `2` to allow the model to bend once.

```python
# Train a 2nd-degree quadratic model: Y = a_0 + a_1*x + a_2*x^2
mymodel_2 = np.poly1d(np.polyfit(x, y, 2))

print(f"Degree-2 R2 Score:         {r2_score(y, mymodel_2(x)):.2f}")
print(f"Degree-2 MSE Error:        {mean_squared_error(y, mymodel_2(x)):.2f}")

```

#### Output Metrics & Visual Inspection:

* **$R^2$ Score:** $0.95$
* **MSE Error:** $3808.64$

---

### Step 2.3: Fitting a Degree-3 Model (Cubic Fit)

We increase the degree to `3` to allow the line to bend twice, forming an S-shape.

```python
# Train a 3rd-degree cubic model: Y = a_0 + a_1*x + a_2*x^2 + a_3*x^3
mymodel_3 = np.poly1d(np.polyfit(x, y, 3))

print(f"Degree-3 R2 Score:         {r2_score(y, mymodel_3(x)):.2f}")
print(f"Degree-3 MSE Error:        {mean_squared_error(y, mymodel_3(x)):.2f}")

```

#### Output Metrics & Visual Inspection:

* **$R^2$ Score:** $0.98$
* **MSE Error:** $1247.22$

---

### Step 2.4: Fitting a Degree-5 Model (High-Degree Overfitting)

Finally, we test a complex 5th-degree polynomial curve.

```python
# Train a high-degree 5th-degree model
mymodel_5 = np.poly1d(np.polyfit(x, y, 5))

print(f"Degree-5 R2 Score:         {r2_score(y, mymodel_5(x)):.2f}")
print(f"Degree-5 MSE Error:        {mean_squared_error(y, mymodel_5(x)):.2f}")

```

#### Output Metrics & Visual Inspection:

* **$R^2$ Score:** $1.00$
* **MSE Error:** $268.74$

> **Critical Overfitting Warning 💡:** The 5th-degree model achieves a perfect **$R^2 = 1.00$** and cuts the MSE down to a tiny **$268.74$**. However, look closely at the right end of the curve (near $x=12$ to $15$). The line begins to weave up and down dramatically just to touch every single point. This model has overfit the data—it is learning random noise rather than the true underlying growth trend, which will lead to poor predictions on new data.

---

## 3. Performance Summary Matrix

| Polynomial Degree | Model Complexity Status | $R^2$ Goodness Score | Mean Squared Error (MSE) |
| --- | --- | --- | --- |
| **Degree 1** | Underfitting (Too Rigid) | $0.91$ | $6,811.63$ |
| **Degree 2** | Moderately Underfitting | $0.95$ | $3,808.64$ |
| **Degree 3** | **Optimal Balanced Fit** | $0.98$ | $1,247.22$ |
| **Degree 5** | Overfitting (Too Wild) | $1.00$ | $268.74$ |

---

## 4. Practice Problems with Solutions

### Problem 1: Calculating Root Mean Squared Error (RMSE) Improvement

**Scenario:** Using the performance metrics from our summary table, calculate the exact change in the **Root Mean Squared Error (RMSE)** when moving from the rigid Degree-1 model to the well-balanced Degree-3 model. Recall that $RMSE = \sqrt{MSE}$.

#### Step-by-Step Calculation:

1. **Compute RMSE for the Degree-1 Model:**

$$RMSE_1 = \sqrt{6811.63} \approx \mathbf{82.5326}$$


2. **Compute RMSE for the Degree-3 Model:**

$$RMSE_3 = \sqrt{1247.22} \approx \mathbf{35.3159}$$


3. **Calculate the net reduction in error value:**

$$\text{Error Reduction} = RMSE_1 - RMSE_3 = 82.5326 - 35.3159 = \mathbf{47.2167 \text{ units}}$$



#### Solution Conclusion:

Upgrading from a simple linear line to a 3rd-degree polynomial curve reduces our average prediction error by **$47.22$ units**, a substantial improvement in model performance.

---

### Problem 2: Tracking Polynomial Equation Parameters

**Scenario:** When you run `print(mymodel_2)` in your workspace, the output displays the following parameter coefficients:

```text
-4.25 x^2 + 73.12 x - 85.40

```

Use this quadratic equation to calculate the predicted onion dry weight ($\hat{y}$) for a growth time of $x = 10$.

#### Step-by-Step Calculation:

1. Write down the quadratic equation:

$$\hat{y} = -4.25x^2 + 73.12x - 85.40$$


2. Substitute $x = 10$ into the formula:

$$\hat{y} = -4.25(10)^2 + 73.12(10) - 85.40$$


3. Simplify the terms step-by-step:
* Term 1: $-4.25 \times 100 = -425.0$
* Term 2: $73.12 \times 10 = 731.2$


4. Complete the arithmetic addition and subtraction:

$$\hat{y} = -425.0 + 731.2 - 85.40$$


$$\hat{y} = 306.2 - 85.40 = \mathbf{220.80}$$



#### Solution Conclusion:

The 2nd-degree polynomial model predicts a dry weight of **$220.80$ units** at a growing time step of 10.

