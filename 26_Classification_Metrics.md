# Machine Learning Notes: Classification and Confusion Matrix Performance Evaluation

This note introduces the theoretical foundations of **Machine Learning Classification**, explores the core quadrant structure of a **Confusion Matrix**, and provides complete step-by-step performance metric calculations.

---

## 1. Concept Name: Machine Learning Classification Foundations

### Simple Meaning 💡
Unlike regression, which predicts a continuous numerical value (like house prices or temperatures), **Classification** is a form of supervised learning focused on predicting a discrete categorical category or label.
* **Binary Classification:** Separating data into exactly two categories (e.g., Email is either `Spam` or `Not Spam`, a medical test is `Positive` or `Negative`).
* **Multi-Class Classification:** Separating data into three or more distinct categorical families (e.g., identifying handwritten digits `0` through `9`, categorizing Youtube videos into `Sports`, `Music`, or `Gaming`).


### Common Real-World Applications
* **Face Recognition & Image Tagging**
* **Content Moderation & Video Categorization**
* **Medical Diagnostic Screening Systems**
* **Hate Speech & Toxicity Detection on Social Media Text**

### Baseline Algorithmic Models
Common models used to solve classification problems include: Logistic Regression, Support Vector Machines (SVM), Decision Trees, Random Forests, Convolutional Neural Networks (CNN), and Recurrent Neural Networks (RNN).

---

## 2. Concept Name: Performance Evaluation — The Confusion Matrix

### Simple Meaning 💡
When evaluating a classification model, simply checking overall accuracy can be misleading, especially if the dataset is imbalanced. A **Confusion Matrix** is a square summary table that cross-references the model's categorical predictions against the actual ground-truth labels. 


### The 4 Core Quadrant Quad Definitions
In a binary classification system, the table organizes outcomes into four distinct quadrants:

1. **True Positive (TP):** The model predicted a positive class, and the actual label was indeed **Positive**. *(Correct Prediction)*
2. **True Negative (TN):** The model predicted a negative class, and the actual label was indeed **Negative**. *(Correct Prediction)*
3. **False Positive (FP):** The model predicted a positive class, but the actual label was **Negative**. *(Type I Error / False Alarm)*
4. **False Negative (FN):** The model predicted a negative class, but the actual label was **Positive**. *(Type II Error / Missed Target)*

---

## 3. Step-by-Step Case Study Walkthrough & Calculations

### Medical Screening Scenario (Slide 3 & 4)
Consider a diagnostic algorithm evaluating chest X-rays to detect a disease across $1,100$ total patients:
* **The Ground Truth:** Out of the $1,100$ total patients, exactly **$100$ are truly Positive** and **$1,000$ are truly Negative**.
* **The Model Output:** * The algorithm correctly identifies $90$ out of the $100$ positive patients as positive.
  * The algorithm correctly identifies $940$ out of the $1,000$ negative patients as negative.

### Step 3.1: Derive the Quadrant Counts
Let's calculate the values for each quadrant:
* **True Positive ($TP$):** **$90$** (Truly sick patients correctly flagged as positive).
* **True Negative ($TN$):** **$940$** (Healthy patients correctly flagged as negative).
* **False Negative ($FN$):** Out of $100$ positive cases, $90$ were caught $\implies 100 - 90 = \mathbf{10}$ sick patients missed by the model.
* **False Positive ($FP$):** Out of $1,000$ negative cases, $940$ were caught $\implies 1,000 - 940 = \mathbf{60}$ healthy patients incorrectly flagged as positive.

#### Assembling the Asymmetric Validation Matrix:
| | Predicted Positive | Predicted Negative | Total Actual Rows |
| :---: | :---: | :---: | :---: |
| **Actual Positive** | $TP = \mathbf{90}$ | $FN = \mathbf{10}$ | $\mathbf{100}$ |
| **Actual Negative** | $FP = \mathbf{60}$ | $TN = \mathbf{940}$ | $\mathbf{1,000}$ |
| **Total Predicted Columns** | $\mathbf{150}$ | $\mathbf{950}$ | **Total Sample Sum = 1,100** |

---

### Step 3.2: Compute Overall Classification Accuracy (%)
Classification Accuracy is defined as the total number of correct predictions divided by the total number of predictions, multiplied by 100 to yield a percentage score:

$$\text{Classification Accuracy} = \frac{TP + TN}{TP + TN + FP + FN} \times 100$$

$$\text{Classification Accuracy} = \frac{90 + 940}{90 + 940 + 60 + 10} \times 100$$

$$\text{Classification Accuracy} = \left( \frac{1030}{1100} \right) \times 100 \approx 0.93636 \times 100 = \mathbf{93.6\%}$$

The diagnostic screening model achieves an overall classification accuracy of **$93.6\%$**.

---

## 4. Supplementary Practice Problems with Solutions

### Problem 1: Advanced Metrics Evaluation (Sensitivity and Specificity)
**Scenario:** Using the medical confusion matrix calculated in Section 3 ($TP=90, TN=940, FP=60, FN=10$), calculate two vital medical screening metrics:
1. **Sensitivity (Recall):** The proportion of actual positive cases correctly identified ($\frac{TP}{TP + FN}$).
2. **Specificity:** The proportion of actual negative cases correctly identified ($\frac{TN}{TN + FP}$).

#### Step-by-Step Calculation:
1. **Compute Sensitivity (True Positive Rate):**
   $$\text{Sensitivity} = \frac{90}{90 + 10} = \frac{90}{100} = 0.90 \implies \mathbf{90.00\%}$$

2. **Compute Specificity (True Negative Rate):**
   $$\text{Specificity} = \frac{940}{940 + 60} = \frac{940}{1000} = 0.94 \implies \mathbf{94.00\%}$$

#### Solution Conclusion:
The model achieves a **Sensitivity of $90.00\%$** (it catches 90% of the sick patients but misses 10%) and a **Specificity of $94.00\%$** (it correctly identifies 94% of the healthy patients but generates false alarms for 6%).

---

### Problem 2: Analyzing the Danger of Accuracy Alone
**Scenario:** A data scientist builds a fraud-detection model where the test matrix contains $9,900$ legitimate transactions and $100$ fraudulent transactions. A baseline model simply flags *every single transaction* as legitimate.
1. State the confusion matrix quadrant values ($TP, TN, FP, FN$) for this simple model.
2. Calculate its classification accuracy, and explain why this model is completely useless despite its high score.

#### Step-by-Step Calculation:
1. **Determine the Quadrant Counts:**
   Since the baseline model flags everything as negative (legitimate):
   * It makes no positive predictions $\implies TP = \mathbf{0}, \; FP = \mathbf{0}$
   * It identifies all legitimate cases correctly $\implies TN = \mathbf{9,900}$
   * It misses all fraudulent cases $\implies FN = \mathbf{100}$

2. **Calculate Classification Accuracy:**
   $$\text{Accuracy} = \frac{TP + TN}{\text{Total}} = \frac{0 + 9900}{10000} = \frac{9900}{10000} = 0.99 \implies \mathbf{99.00\%}$$

#### Solution Conclusion:
The model achieves a very high classification accuracy of **$99.00\%$**. However, its **Sensitivity is $0.00\%$** ($\frac{0}{0+100}$), meaning it fails to catch a single fraudulent transaction. This problem demonstrates why monitoring additional confusion matrix metrics like Sensitivity, Specificity, and F1-score is essential for evaluating classification models, especially on imbalanced datasets.


# Machine Learning Notes: Advanced Classification Evaluation Metrics

This note breaks down the critical metrics used to evaluate classification performance beyond basic accuracy, focusing on **Precision**, **Recall (Sensitivity)**, and the **F1-Score**.

---

## 1. Concept Name: The Problem with Classification Accuracy

### Simple Meaning 💡
While overall classification accuracy is simple to understand, it is often a misleading metric when dealing with an **imbalanced dataset** (where one class occurs much more frequently than another). 

Imagine a dataset where **99%** of transactions are legitimate and only **1%** are fraudulent. If a model blindly predicts "legitimate" for every single transaction without actually looking at the data, it achieves a stellar **99% accuracy**. However, the model has learned absolutely nothing and is completely useless because it failed to catch a single fraudulent event. To evaluate such models properly, we rely on advanced metrics derived from the confusion matrix.

---

## 2. Step-by-Step Advanced Metrics & Calculations

We will use the matrix quantities established in the medical screening case study to calculate our metrics:
* **True Positives ($TP$):** 90
* **False Positives ($FP$):** 60
* **False Negatives ($FN$):** 10
* **True Negatives ($TN$):** 940


### Step 2.1: Precision
* **Simple Meaning 💡:** Out of all the instances that the model *predicted* as positive, what fraction was actually correct? It measures quality and helps evaluate the cost of false alarms.
* **Mathematical Formula:**
  $$\text{Precision} = \frac{TP}{TP + FP}$$
* **Calculation Walkthrough:**
  $$\text{Precision} = \frac{90}{90 + 60} = \frac{90}{150} = \frac{3}{5} = \mathbf{0.60 \quad (60.0\%)}$$

---

### Step 2.2: Recall (Sensitivity)
* **Simple Meaning 💡:** Out of all the *actual* positive instances in the real world, what fraction did the model successfully catch? It measures completeness and helps evaluate missed targets.
* **Mathematical Formula:**
  $$\text{Recall} = \frac{TP}{TP + FN}$$
* **Calculation Walkthrough:**
  $$\text{Recall} = \frac{90}{90 + 10} = \frac{90}{100} = \frac{9}{10} = \mathbf{0.90 \quad (90.0\%)}$$

---

### Step 2.3: F1-Score
* **Simple Meaning 💡:** It is often hard to compare two models if one has high precision and low recall, while the other has low precision and high recall. The **F1-Score** combines both into a single metric by computing their **harmonic mean**.

* **Mathematical Formula:**
  $$\text{F1-Score} = 2 \times \frac{\text{Precision} \times \text{Recall}}{\text{Precision} + \text{Recall}}$$

* **Calculation Walkthrough:**
  $$\text{F1-Score} = 2 \times \frac{0.6 \times 0.9}{0.6 + 0.9} = 2 \times \frac{0.54}{1.5} = \frac{1.08}{1.50} = \mathbf{0.72 \quad (72.0\%)}$$$$\text{F1-Score} = \frac{1.08}{1.50} = \mathbf{0.72 \quad (72.0\%)}$$

#### Why use the Harmonic Mean instead of a simple average? 💡
The harmonic mean is highly sensitive to unbalanced values. For example, if a model has a perfect Precision of $1$ but a Recall of $0$, a simple average gives a misleading score of $0.5$. The harmonic mean, however, yields a more accurate **F1-Score of 0**. The F1-score aggressively punishes models where one metric is critically low, favoring classifiers that achieve a healthy balance between Precision and Recall.

---

## 3. Performance Summary Matrix

| Metric | Formula | Value | What It Answers |
| :--- | :--- | :---: | :--- |
| **Accuracy** | $\frac{TP + TN}{\text{Total}}$ | $93.6\%$ | Out of all samples, what fraction did we predict correctly? |
| **Precision** | $\frac{TP}{TP + FP}$ | $60.0\%$ | When the model flags a positive result, how reliable is it? |
| **Recall** | $\frac{TP}{TP + FN}$ | $90.0\%$ | What percentage of truly positive cases did we find? |
| **F1-Score** | $2 \times \frac{\text{Precision} \times \text{Recall}}{\text{Precision} + \text{Recall}}$ | $72.0\%$ | What is the overall balanced health of the classifier? |

---

## 4. Practice Problems with Solutions

### Problem 1: Evaluating a Spam Filter Classifier
**Scenario:** A spam filter classifier scans a batch of user emails and generates the following confusion matrix parameters:
* Truly spam emails caught ($TP$) = $80$
* Legitimate emails accidentally blocked ($FP$) = $5$
* Spam emails missed ($FN$) = $20$

Calculate the filter's **Precision**, **Recall**, and **F1-Score**.

#### Step-by-Step Calculation:
1. **Compute Precision:**
   $$\text{Precision} = \frac{TP}{TP + FP} = \frac{80}{80 + 5} = \frac{80}{85} \approx \mathbf{0.9412 \quad (94.12\%)}$$

2. **Compute Recall:**
   $$\text{Recall} = \frac{TP}{TP + FN} = \frac{80}{80 + 20} = \frac{80}{100} = \mathbf{0.8000 \quad (80.00\%)}$$

3. **Compute F1-Score:**
   $$\text{F1-Score} = 2 \times \frac{0.9412 \times 0.8000}{0.9412 + 0.8000} = 2 \times \frac{0.7530}{1.7412} = \frac{1.5060}{1.7412} \approx \mathbf{0.8649 \quad (86.49\%)}$$

#### Solution Conclusion:
The spam filter exhibits high reliability with a **94.12% Precision** (few false alarms blocking clean emails), catches **80.00% of all spam (Recall)**, and retains a solid overall **F1-Score of 86.49%**.

---

### Problem 2: Navigating Trade-offs in a Security Alarm Network
**Scenario:** You change the sensitivity setting on a building security motion sensor. This adjustment causes the system to generate zero False Positives ($FP = 0$) but results in several missed break-ins ($FN > 0$).
1. State the exact value of the resulting **Precision** score.
2. Explain what happens to the **Recall** score.

#### Step-by-Step Calculation:
1. Substitute $FP = 0$ directly into the precision equation:
   $$\text{Precision} = \frac{TP}{TP + 0} = \frac{TP}{TP} = \mathbf{1.0 \quad (100.0\%)}$$
2. Look at the recall equation with a growing $FN$:
   $$\text{Recall} = \frac{TP}{TP + \text{increasing value}} \implies \mathbf{\text{Recall decreases}}$$

#### Solution Conclusion:
The sensor achieves a perfect **Precision of 100%**, meaning every single alarm triggered is guaranteed to be a real break-in. However, because it misses a significant number of actual break-ins ($FN > 0$), its **Recall will drop**. This problem highlights the classic **Precision-Recall Trade-off** found in nearly all machine learning classification tasks.



# Data Science & Machine Learning Notes: Multi-Class Confusion Matrix & Performance Metrics

This note breaks down the implementation and mathematical mechanics of a **Multi-Class Confusion Matrix** and its accompanying **Classification Report** using Scikit-Learn.

---

## 1. Concept Name: Multi-Class Confusion Matrix Evaluation

### Simple Meaning 💡
When your machine learning model has to choose between more than two categories (e.g., classifying an image as a **c**at, **h**orse, or **f**ox), we look at a multi-class evaluation framework. 
* A **Multi-Class Confusion Matrix** grids these categories into a square layout.
* The rows track what the target classes **actually** were.
* The columns track what the model **predicted** them to be.
* The main diagonal cells running from top-left to bottom-right show where the model was right. Any number off this diagonal shows a specific misclassification error.


---

## 2. Step-by-Step Data Evaluation & Matrix Mapping

Let's look at the custom 3-class target tracking lists provided in the lecture slides:
* True labels: `y_actual = ["c", "h", "f", "c", "h", "f", "c", "h", "h"]`
* Predictions: `y_pred   = ["c", "c", "f", "h", "h", "c", "c", "f", "f"]`

By specifying `labels=["c", "h", "f"]`, Scikit-Learn maps out the row/column tracking grids in that exact order.

### Step 2.1: Manual Data Coordinate Mapping
Let's pair each entry index-by-index to build the matrix coordinates manually:
1. Index 0: Actual = `c`, Pred = `c` $\implies$ Row `c`, Col `c` (+1)
2. Index 1: Actual = `h`, Pred = `c` $\implies$ Row `h`, Col `c` (+1)
3. Index 2: Actual = `f`, Pred = `f` $\implies$ Row `f`, Col `f` (+1)
4. Index 3: Actual = `c`, Pred = `h` $\implies$ Row `c`, Col `h` (+1)
5. Index 4: Actual = `h`, Pred = `h` $\implies$ Row `h`, Col `h` (+1)
6. Index 5: Actual = `f`, Pred = `c` $\implies$ Row `f`, Col `c` (+1)
7. Index 6: Actual = `c`, Pred = `c` $\implies$ Row `c`, Col `c` (+1)
8. Index 7: Actual = `h`, Pred = `f` $\implies$ Row `h`, Col `f` (+1)
9. Index 8: Actual = `h`, Pred = `f` $\implies$ Row `h`, Col `f` (+1)

### Step 2.2: Re-Assembling the Confusion Matrix Shape
Summing up these intersections produces the matrix printed in the first notebook image:

```text
               Predicted Class
               "c"   "h"   "f"
              +-----+-----+-----+
          "c" |  2  |  1  |  0  |  -> Row Sum (Support c) = 3
              +-----+-----+-----+
 Actual   "h" |  1  |  1  |  2  |  -> Row Sum (Support h) = 4
 Class        +-----+-----+-----+
          "f" |  1  |  0  |  1  |  -> Row Sum (Support f) = 2
              +-----+-----+-----+
                 |     |     |
              Col Sum Col Sum Col Sum
              (Pred c)(Pred h)(Pred f)
                = 4   = 2   = 3

```

---

## 3. Step-by-Step Metric Derivations & Calculations

Using our matrix counts, let's derive every decimal value displayed in the `classification_report` table.

### Step 3.1: Individual Class Precision Calculations

Precision looks down each vertical column. Out of all items predicted as a class, how many were true?

* **Class "c" Precision:** True Positives = $2$. Total Predicted Column Sum = $2 + 1 + 1 = 4$.

$$\text{Precision}_c = \frac{2}{4} = \mathbf{0.50}$$


* **Class "h" Precision:** True Positives = $1$. Total Predicted Column Sum = $1 + 1 + 0 = 2$.

$$\text{Precision}_h = \frac{1}{2} = \mathbf{0.50}$$


* **Class "f" Precision:** True Positives = $1$. Total Predicted Column Sum = $0 + 2 + 1 = 3$.

$$\text{Precision}_f = \frac{1}{3} \approx \mathbf{0.33}$$



---

### Step 3.2: Individual Class Recall Calculations

Recall looks across each horizontal row. Out of all truly actual members of that class, how many did the model find?

* **Class "c" Recall:** True Positives = $2$. Total Actual Row Sum (Support) = $3$.

$$\text{Recall}_c = \frac{2}{3} \approx \mathbf{0.67}$$


* **Class "h" Recall:** True Positives = $1$. Total Actual Row Sum (Support) = $4$.

$$\text{Recall}_h = \frac{1}{4} = \mathbf{0.25}$$


* **Class "f" Recall:** True Positives = $1$. Total Actual Row Sum (Support) = $2$.

$$\text{Recall}_f = \frac{1}{2} = \mathbf{0.50}$$



---

### Step 3.3: Individual Class F1-Score Calculations

The harmonic mean of precision and recall: $2 \times \frac{\text{Precision} \times \text{Recall}}{\text{Precision} + \text{Recall}}$.

* **Class "c" F1-Score:**

$$\text{F1}_c = 2 \times \frac{0.50 \times 0.6667}{0.50 + 0.6667} = 2 \times \frac{0.3333}{1.1667} \approx \mathbf{0.57}$$


* **Class "h" F1-Score:**

$$\text{F1}_h = 2 \times \frac{0.50 \times 0.25}{0.50 + 0.25} = 2 \times \frac{0.125}{0.75} \approx \mathbf{0.33}$$


* **Class "f" F1-Score:**

$$\text{F1}_f = 2 \times \frac{0.3333 \times 0.50}{0.3333 + 0.50} = 2 \times \frac{0.1667}{0.8333} \approx \mathbf{0.40}$$



---

### Step 3.4: Global Macro and Weighted Averaging Calculations

#### 1. Overall System Accuracy:

The sum of correct predictions along the main diagonal divided by the total sample size ($N=9$).


$$\text{Accuracy} = \frac{\text{Diagonal Sum}}{N} = \frac{2 + 1 + 1}{9} = \frac{4}{9} \approx \mathbf{0.44}$$

#### 2. Macro Average (Unweighted Mean):

Computes the arithmetic average of the metrics, giving each class equal weight regardless of sample size.


$$\text{Macro Precision} = \frac{\text{Precision}_c + \text{Precision}_h + \text{Precision}_f}{3} = \frac{0.50 + 0.50 + 0.3333}{3} = \frac{1.3333}{3} \approx \mathbf{0.44}$$

$$\text{Macro Recall} = \frac{\text{Recall}_c + \text{Recall}_h + \text{Recall}_f}{3} = \frac{0.6667 + 0.25 + 0.50}{3} = \frac{1.4167}{3} \approx \mathbf{0.47}$$

#### 3. Weighted Average (Support-Proportioned Mean):

Averages the metrics while weighting each class by its `support` (sample count), making it highly robust for imbalanced classes.


$$\text{Weighted Precision} = \frac{(0.50 \times 3) + (0.50 \times 4) + (0.3333 \times 2)}{9} = \frac{1.5 + 2.0 + 0.6667}{9} = \frac{4.1667}{9} \approx \mathbf{0.46}$$

$$\text{Weighted Recall} = \frac{(0.6667 \times 3) + (0.25 \times 4) + (0.50 \times 2)}{9} = \frac{2.0 + 1.0 + 1.0}{9} = \frac{4.0}{9} \approx \mathbf{0.44}$$

---

## 4. Practice Problems with Solutions

### Problem 1: Evaluating an Imbalanced 3-Class Confusion Matrix

**Scenario:** A multi-class model evaluates text sentiment as `Positive`, `Neutral`, or `Negative`. The confusion matrix yields:

```text
                    Predicted
                Pos   Neu   Neg
          Pos [  10,   2,    0  ]
 Actual   Neu [   3,  15,    2  ]
          Neg [   1,   4,    3  ]

```

Calculate the exact **Precision** and **Recall** metrics for the `Negative` class.

#### Step-by-Step Calculation:

1. **Identify True Positives ($TP$) for the Negative Class:**
Locate the intersection where Actual = Neg and Predicted = Neg $\implies \mathbf{3}$.
2. **Compute Negative Precision (Column perspective):**
Sum the entries down the third column: $\text{Column Sum} = 0 + 2 + 3 = 5$.

$$\text{Precision}_{\text{Neg}} = \frac{TP}{\text{Column Sum}} = \frac{3}{5} = \mathbf{0.60 \quad (60.0\%)}$$


3. **Compute Negative Recall (Row perspective):**
Sum the entries across the third row (Support): $\text{Row Sum} = 1 + 4 + 3 = 8$.

$$\text{Recall}_{\text{Neg}} = \frac{TP}{\text{Row Sum}} = \frac{3}{8} = \mathbf{0.375 \quad (37.5\%)}$$



---

### Problem 2: Reconstructing Global Accuracy from Diagonal Data

**Scenario:** An engineering validation algorithm tests a component tracking tool across 3 structural flags. The confusion matrix contains a main diagonal of `[25, 40, 15]`. If the macro-average `support` count per class is exactly $30$, calculate the overall classification accuracy.

#### Step-by-Step Calculation:

1. **Calculate the total number of correct predictions:**

$$\text{Correct Predictions} = 25 + 40 + 15 = 80$$


2. **Find the total sample size ($N$):**
Since there are 3 classes and the average support (row count) per class is 30:

$$N = 3 \text{ classes} \times 30 = 90 \text{ total samples}$$


3. **Compute the final Accuracy percentage:**

$$\text{Accuracy} = \frac{\text{Correct Predictions}}{N} = \frac{80}{90} \approx 0.8889 \implies \mathbf{88.89\%}$$



#### Solution Conclusion:

The component tracking model achieves an overall classification accuracy of **$88.89\%$**.
