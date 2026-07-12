# Lecture 25: Logistic Regression - II (Practical Implementation)

## 1. Case Study Overview: Company Dataset Problem
We explore a practical binary classification problem using a real-world company dataset named `User_Data.csv`. 

### Problem Statement
A company wants to predict whether a specific user will purchase their newly launched product or not based on database characteristics. This allows targeted marketing.

### Dataset Feature Structure
The raw data matrix consists of 5 columns:
1. `User ID`: Unique identifier for each customer (Numerical descriptor).
2. `Gender`: Gender classification (Categorical text: Male/Female).
3. `Age`: The user's age in years (Numerical continuous).
4. `EstimatedSalary`: The estimated annual income of the user (Numerical continuous).
5. `Purchased`: Target tracking indicator (Binary indicator: `0` = No purchase, `1` = Purchased).

### Feature Selection Insights
To optimize training speed and predictive performance, we isolate the independent features that affect purchasing patterns.
* **Important Predictors:** `Age` and `EstimatedSalary` show direct statistical correlation with purchases.
* **Irrelevant Redundancies:** `User ID` and `Gender` are skipped here because unique IDs have no predictive power, and gender is excluded to simplify this basic multi-variable model setup.

---

## 2. Step-by-Step Code Walkthrough

### Step 1: Environmental Library Imports
We load the core computing stack required for matrix mutations and tracking:
```python
import pandas as pd           # For high-level data frame analysis and loading
import numpy as np            # For multi-dimensional vector array mathematics
import matplotlib.pyplot as plt # For rendering data curves and scatter visualizations

```

### Step 2: Ingesting Data Source via Colab Environment

To read local computer files within remote cloud notebook nodes, use the runtime upload wrapper:

```python
from google.colab import files
uploaded = files.upload() # Prompt to browse and choose 'User_Data.csv'

```

### Step 3: Parsing Data and Shape Auditing

Once uploaded, we map the CSV stream into a structured tabular data frame using Pandas and inspect its dimensions:

```python
dataset = pd.read_csv("User_Data.csv")
print(dataset.shape)
# Output: (400, 5)

```

> 📊 **Data Dimensions Note:** The output `(400, 5)` tells us the dataset contains exactly **400 rows** (individual customer records) and **5 columns** (features and target).

### Step 4: Previewing Head Structures

Let's look at the first 5 rows to verify columns match expectations:

```python
dataset.head()

```

|  | User ID | Gender | Age | EstimatedSalary | Purchased |
| --- | --- | --- | --- | --- | --- |
| **0** | 15624510 | Male | 19 | 19000 | 0 |
| **1** | 15810944 | Male | 35 | 20000 | 0 |
| **2** | 15668575 | Female | 26 | 43000 | 0 |
| **3** | 15603246 | Female | 27 | 57000 | 0 |
| **4** | 15804002 | Male | 19 | 76000 | 0 |

### Step 5: Slicing Target Arrays and Input Matrices

We use integer location slicing (`.iloc`) to separate our features from our labels. Remember that Python indexing starts at **0**:

* Index 0: `User ID`
* Index 1: `Gender`
* Index 2: `Age`
* Index 3: `EstimatedSalary`
* Index 4: `Purchased`

```python
# Input Matrix X: Extract all rows, only keep columns 2 and 3 (Age, EstimatedSalary)
X = dataset.iloc[:, [2, 3]].values

# Target Vector y: Extract all rows, only keep column index 4 (Purchased status)
y = dataset.iloc[:, 4].values
print(y)
# Output Array: [0 0 0 0 0 0 0 1 0 0 ... 1 0 0 0 0]

```

---

## 3. Index Calculation Mechanics

Let's walk through how Python's multi-dimensional slice command `[ : , [2, 3] ]` extracts data under the hood.

### Slicing Extraction Matrix

Given row 0 from our dataset array:


$$\text{Row}_0 = [15624510, \text{"Male"}, 19, 19000, 0]$$

Applying the filter mappings:

* `dataset.iloc[0, 2]` $\rightarrow 19$
* `dataset.iloc[0, 3]` $\rightarrow 19000$

This collapses the row down into an input matrix slice:


$$X_0 = [19, 19000]$$

---

## 4. Conceptual Practice Problems

### Problem 1: Column Array Restructuring

**Question:** If we want to update our model to include `Gender` (index 1) along with `Age` and `EstimatedSalary` as inputs, how should we modify the `.iloc` index code expression?

**Solution:**
We can pass the required list of index positions into the column slot of the `.iloc` function:

```python
X_updated = dataset.iloc[:, [1, 2, 3]].values

```

### Problem 2: Slicing Matrix Dimensions

**Question:** If a dataset has shape `(1000, 10)` and we slice it using `X = dataset.iloc[0:250, [4, 7]].values`, what will be the exact matrix dimensions of the resulting array `X`?

**Solution:**

* The row index selection `0:250` selects rows from 0 up to (but not including) 250, which gives exactly **250 rows**.
* The column index selection `[4, 7]` explicitly extracts **2 columns**.
* Therefore, the dimensions of matrix `X` will be exactly **(250, 2)**.


# Lecture 25: Logistic Regression - II (Practical Implementation)

## 1. Case Study Overview: Company Dataset Problem
We explore a practical binary classification problem using a real-world company dataset named `User_Data.csv`. 

### Problem Statement
A company wants to predict whether a specific user will purchase their newly launched product or not based on database characteristics. This allows targeted marketing.

### Dataset Feature Structure
The raw data matrix consists of 5 columns:
1. `User ID`: Unique identifier for each customer (Numerical descriptor).
2. `Gender`: Gender classification (Categorical text: Male/Female).
3. `Age`: The user's age in years (Numerical continuous).
4. `EstimatedSalary`: The estimated annual income of the user (Numerical continuous).
5. `Purchased`: Target tracking indicator (Binary indicator: `0` = No purchase, `1` = Purchased).

### Feature Selection Insights
To optimize training speed and predictive performance, we isolate the independent features that affect purchasing patterns.
* **Important Predictors:** `Age` and `EstimatedSalary` show direct statistical correlation with purchases.
* **Irrelevant Redundancies:** `User ID` and `Gender` are skipped here because unique IDs have no predictive power, and gender is excluded to simplify this basic multi-variable model setup.

---

## 2. Step-by-Step Code Walkthrough

### Step 1: Environmental Library Imports
We load the core computing stack required for matrix mutations and tracking:
```python
import pandas as pd           # For high-level data frame analysis and loading
import numpy as np            # For multi-dimensional vector array mathematics
import matplotlib.pyplot as plt # For rendering data curves and scatter visualizations

```

### Step 2: Ingesting Data Source via Colab Environment

To read local computer files within remote cloud notebook nodes, use the runtime upload wrapper:

```python
from google.colab import files
uploaded = files.upload() # Prompt to browse and choose 'User_Data.csv'

```

### Step 3: Parsing Data and Shape Auditing

Once uploaded, we map the CSV stream into a structured tabular data frame using Pandas and inspect its dimensions:

```python
dataset = pd.read_csv("User_Data.csv")
print(dataset.shape)
# Output: (400, 5)

```

> 📊 **Data Dimensions Note:** The output `(400, 5)` tells us the dataset contains exactly **400 rows** (individual customer records) and **5 columns** (features and target).

### Step 4: Previewing Head Structures

Let's look at the first 5 rows to verify columns match expectations:

```python
dataset.head()

```

|  | User ID | Gender | Age | EstimatedSalary | Purchased |
| --- | --- | --- | --- | --- | --- |
| **0** | 15624510 | Male | 19 | 19000 | 0 |
| **1** | 15810944 | Male | 35 | 20000 | 0 |
| **2** | 15668575 | Female | 26 | 43000 | 0 |
| **3** | 15603246 | Female | 27 | 57000 | 0 |
| **4** | 15804002 | Male | 19 | 76000 | 0 |

### Step 5: Slicing Target Arrays and Input Matrices

We use integer location slicing (`.iloc`) to separate our features from our labels. Remember that Python indexing starts at **0**:

* Index 0: `User ID`
* Index 1: `Gender`
* Index 2: `Age`
* Index 3: `EstimatedSalary`
* Index 4: `Purchased`

```python
# Input Matrix X: Extract all rows, only keep columns 2 and 3 (Age, EstimatedSalary)
X = dataset.iloc[:, [2, 3]].values

# Target Vector y: Extract all rows, only keep column index 4 (Purchased status)
y = dataset.iloc[:, 4].values
print(y)
# Output Array: [0 0 0 0 0 0 0 1 0 0 ... 1 0 0 0 0]

```

---

## 3. Index Calculation Mechanics

Let's walk through how Python's multi-dimensional slice command `[ : , [2, 3] ]` extracts data under the hood.

### Slicing Extraction Matrix

Given row 0 from our dataset array:


$$\text{Row}_0 = [15624510, \text{"Male"}, 19, 19000, 0]$$

Applying the filter mappings:

* `dataset.iloc[0, 2]` $\rightarrow 19$
* `dataset.iloc[0, 3]` $\rightarrow 19000$

This collapses the row down into an input matrix slice:


$$X_0 = [19, 19000]$$

---

## 4. Conceptual Practice Problems

### Problem 1: Column Array Restructuring

**Question:** If we want to update our model to include `Gender` (index 1) along with `Age` and `EstimatedSalary` as inputs, how should we modify the `.iloc` index code expression?

**Solution:**
We can pass the required list of index positions into the column slot of the `.iloc` function:

```python
X_updated = dataset.iloc[:, [1, 2, 3]].values

```

### Problem 2: Slicing Matrix Dimensions

**Question:** If a dataset has shape `(1000, 10)` and we slice it using `X = dataset.iloc[0:250, [4, 7]].values`, what will be the exact matrix dimensions of the resulting array `X`?

**Solution:**

* The row index selection `0:250` selects rows from 0 up to (but not including) 250, which gives exactly **250 rows**.
* The column index selection `[4, 7]` explicitly extracts **2 columns**.
* Therefore, the dimensions of matrix `X` will be exactly **(250, 2)**.

```

```markdown
# Lecture 26: Facial Recognition Pipeline using Logistic Regression

## 1. Environment Setup & Data Ingestion
We build an image classification system to recognize political figures using their facial structures. We use the **Labeled Faces in the Wild (LFW)** dataset.

```python
%matplotlib inline
import numpy as np
import matplotlib.pyplot as plt
from scipy import stats
import seaborn as sns; sns.set() # Apply default aesthetic styling

```

### Fetching the Image Dataset

We import the dataset wrapper from `sklearn` and filter out personalities who have fewer than 60 image samples available to avoid class imbalances.

```python
from sklearn.datasets import fetch_lfw_people
faces = fetch_lfw_people(min_faces_per_person=60)

print(faces.target_names)
print(faces.images.shape)

```

### Dataset Structure & Metadata Output

* **`faces.target_names`**: Contains the target labels: `['Ariel Sharon', 'Colin Powell', 'Donald Rumsfeld', 'George W Bush', 'Gerhard Schroeder', 'Hugo Chavez', 'Junichiro Koizumi', 'Tony Blair']`.
* **`faces.images.shape`**: Returns the shape tuple `(1348, 62, 47)`.

---

## 2. Dimensional Data Mechanics & Grid Plotting

Let's break down the image tensor dimensions to understand what the shape metadata means.

### Dimensions Breakdown

Given the array dimensions $(1348, 62, 47)$:

* **$1348$**: Total number of individual face images in our processed dataset matrix.
* **$62$**: Height of each picture in pixels (number of rows per image).
* **$47$**: Width of each picture in pixels (number of columns per image).

### Total Flattened Features Calculation

When passing images into a standard machine learning classifier like Logistic Regression, the 2D grid pixels must be flattened out into a single 1D feature row vector.


$$\text{Total Input Features per Face} = 62 \times 47 = 2914 \text{ continuous gray values}$$

### Plotting Training Samples

We render a $3 \times 5$ subplot structure to check the source training quality:

```python
fig, ax = plt.subplots(3, 5)
for i, axi in enumerate(ax.flat):
    axi.imshow(faces.images[i], cmap='bone') # Display grayscale tone map
    axi.set(xticks=[], yticks=[]) # Strip index labels off the border axis
    axi.set_ylabel(faces.target_names[faces.target[i]].split()[-1]) # Show last name only

```

---

## 3. Training & Convergence Troubleshooting

We split our datasets into standard partitions and attempt to train the classifier model.

```python
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LogisticRegression

# Target vectors use .data (flattened 2914 vectors) instead of .images
Xtrain, Xtest, ytrain, ytest = train_test_split(faces.data, faces.target, random_state=0)

model = LogisticRegression(random_state=0)
model.fit(Xtrain, ytrain)

```

### The Convergence Warning Exception

When running `model.fit()`, the runtime system displays an error warning message block:

```text
/usr/local/lib/python3.7/dist-packages/sklearn/linear_model/_logistic.py:940: 
ConvergenceWarning: lbfgs failed to converge (status=1):
STOP: TOTAL NO. of ITERATIONS REACHED LIMIT.
Increase the number of iterations (max_iter) or scale the data...

```

### Why Did This Happen?

By default, `LogisticRegression` stops trying to solve the Maximum Likelihood Estimation equations after 100 iterations. Because our input dataset has a high dimensionality ($2914$ features per row), the gradient descent solver gets stuck before finding the absolute global minimum loss score.

To fix this, we should either increase the iteration headroom limit parameter (`max_iter=1000`) or apply feature normalization techniques like `StandardScaler` or Principal Component Analysis (PCA) to shrink the dimensional scope beforehand.

---

## 4. Testing Predictions & Visualizing Error Profiles

Despite the early optimizer cutoff, we pass the test partition matrix into the model to inspect the resulting classifications:

```python
yfit = model.predict(Xtest)

```

### Plotting Prediction Classifications

We generate a $4 \times 5$ verification grid to visually check where our model makes errors. The code displays correctly classified names in black, and incorrect classifications in red.

```python
fig, ax = plt.subplots(4, 5)
for i, axi in enumerate(ax.flat):
    # Reshape the 1D flattened array row back into the original 62x47 square image geometry
    axi.imshow(Xtest[i].reshape(62, 47), cmap='bone')
    axi.set(xticks=[], yticks=[])
    
    # Display the last name predicted by the model
    predicted_name = faces.target_names[yfit[i]].split()[-1]
    actual_name = faces.target_names[ytest[i]].split()[-1]
    
    # Text coloring rule: use black text for correct matches, red text for mistakes
    if yfit[i] == ytest[i]:
        axi.set_ylabel(predicted_name, color='black')
    else:
        axi.set_ylabel(f"{predicted_name}", color='red')

```

---

## 5. Conceptual Practice Problems

### Problem 1: Input Matrix Shape Derivation

**Question:** If the `train_test_split` statement uses the default allocation split configuration (which reserves exactly 75% for training and 25% for testing), what are the exact matrix shapes for `Xtrain` and `Xtest` given our source geometry shape of `(1348, 62, 47)`?

**Solution & Calculation:**

1. Determine the number of rows allocated to each subset:

$$\text{Train Rows} = 1348 \times 0.75 = 1011 \text{ rows}$$


$$\text{Test Rows} = 1348 \times 0.25 = 337 \text{ rows}$$


2. Our training loop uses `faces.data`, which flattens the input pixels down to $62 \times 47 = 2914$ features.
3. Therefore, the resulting matrix dimension shapes are:
* **`Xtrain.shape`**: `(1011, 2914)`
* **`Xtest.shape`**: `(337, 2914)`



### Problem 2: Multiclass Probability Framework

**Question:** Our previous examples only dealt with simple binary classification outcomes (`0` or `1`). Here, we have 8 distinct political figures. How does Logistic Regression calculate probabilities when dealing with more than two target classes?

**Solution:**
When handling multiple classes, Scikit-Learn defaults to using a **One-vs-Rest (OvR)** approach. The model trains 8 separate binary logistic regression classifiers under the hood (e.g., *Classifier 1: Tony Blair vs. Everyone Else*, *Classifier 2: George W. Bush vs. Everyone Else*, and so on). During inference on a test image, all 8 models process the image vector, and the class that outputs the highest probability value is selected as the final predicted label.

```

```



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

