# SVM Classifiers: Benchmarking Datasets & Image Flattening

This document covers the execution setup for implementing Hard and Soft margin Support Vector Machine (SVM) classifiers, data transformation pipelines for dimensional flattening, and standard computer vision evaluation benchmarks using benchmark datasets.

---

## 1. Concept Name: Image Flattening & Feature Vector Transformation

### Simple Meaning
Computer vision models cannot natively interpret a grid-like 2D image matrix directly in basic algorithms like standard SVMs. 

**Image Flattening** is the process of unrolling a 2D image matrix row-by-row into a long 1D array (a **feature vector**). For instance, an $8 \times 8$ pixel grayscale image is stripped of its spatial square shape and stretched into a single line of 64 sequential values, where each value represents the numerical intensity of a specific pixel (e.g., from 0 for pure white to 16 or 255 for deep black).

### Text-Art Visualization (Graph/Matrix Transition)

```text
2D Image Matrix (8x8)                1D Feature Vector (Length 64)
  Col 0  Col 1 ... Col 7
  +----+----+     ----+              +----+----+----+----+     ----+
  | P0 | P1 | ... | P7 |  --Row 0--> | P0 | P1 | .. | P7 | P8 | ... | P63|
  +----+----+     ----+              +----+----+----+----+     ----+
  | P8 | P9 | ... | P15|  --Row 1--^   |    |    |
  +----+----+     ----+                [0]  [1]  ..           [63]
  |... |... | ... |... |
  +----+----+     ----+
  |P56 |P57 | ... | P63|  --Row 7--^
  +----+----+     ----+

```

### Step-by-Step Numerical Calculations

Let's assume a tiny $3 \times 3$ thumbnail image matrix to visually map out index calculation before executing on the benchmark standard $8 \times 8$ set.

#### Problem 1: Flattening Index Formula

To calculate where a pixel located at Row index $i$ and Column index $j$ will land inside a 1D vector derived from an image of width $W$, we use the formula:


$$\text{Vector Index} = (i \times W) + j$$

Given a pixel at Row $i = 4$, Column $j = 3$ inside an standard $8 \times 8$ image grid ($W = 8$):

* **Step 1:** Multiply the current row index by the total pixel width of the row matrix.

$$4 \times 8 = 32$$


* **Step 2:** Add the column index shift.

$$32 + 3 = 35$$


* **Result:** The element sits exactly at index position **35** inside the 64-length array.

---

## 2. Benchmark Datasets Overview

When verifying the generalization properties of an SVM classifier, modern machine learning relies on standardized data environments:

### A. The Optical Handwritten Digits Dataset

* **Composition:** Contains 1,797 total image samples.
* **Dimensions:** Each data point is stored as a low-resolution $8 \times 8$ grid matrix.
* **Transformation Step:** Prior to training the machine learning pipeline, each matrix is flattened into a 64-length linear array.

### B. Labelled Faces in the Wild (LFW) Dataset

* **Core Application:** Designed extensively for unconstrained face verification and recognition studies.
* **Data Scale:** Encompasses over 13,000 distinct facial photographs scraped and compiled from public web links.
* **Storage Footprint:** Approximately 173MB overall.

---

## 3. Python Implementation: Data Loading & Vectorization Pipeline

Below is the complete, runnable code to pull down standard handwritten digit samples, display the spatial representation, and mathematically verify the unrolling process.

```python
import matplotlib.pyplot as plt
from sklearn import datasets
from sklearn.model_selection import train_test_split
from sklearn.svm import SVC
from sklearn.metrics import classification_report, confusion_matrix

# Step 1: Initialize the dataset collection
digits = datasets.load_digits()

# Step 2: Inspect structural dimensions before and after spatial unrolling
raw_shape = digits.images.shape  # Structurally (1797, 8, 8)
flattened_shape = digits.data.shape  # Structurally (1797, 64)

print(f"Original matrix geometry: {raw_shape[1]}x{raw_shape[2]}")
print(f"Flattened 1D array feature length: {flattened_shape[1]}")

# Step 3: Plot a sample instance for qualitative verification
plt.figure(1, figsize=(3, 3))
plt.imshow(digits.images[0], cmap=plt.cm.gray_r, interpolation='nearest')
plt.title(f"Target Label: {digits.target[0]}")
plt.show()

# Step 4: Split data into training sets and testing subsets
X_train, X_test, y_train, y_test = train_test_split(
    digits.data, digits.target, test_size=0.3, random_state=42
)

# Step 5: Fit an SVM classifier to perform structural classification
# Instantiating a Soft-Margin classifier with standard parameters
clf = SVC(kernel='rbf', C=1.0, gamma='scale')
clf.fit(X_train, y_train)

# Step 6: Evaluate structural performance metrics
y_pred = clf.predict(X_test)
print("\n--- Evaluation Metrics Classification Report ---")
print(classification_report(y_test, y_pred))

```

---

## 4. Analytical Practice Problems

### Problem 1: Dimension Matrix Volumetrics

**Scenario:** You have a high-resolution sub-collection slice from the LFW face dataset. Instead of low-resolution grids, these inputs are configured as $50 \times 50$ color pixels (RGB channels = 3). Calculate the total feature vector length when this color matrix slice undergoes full unrolling and flattening.

**Solution:**

1. Determine total spatial elements in one channel layer:

$$50 \times 50 = 2,500\text{ pixels}$$


2. Account for the parallel color layers (Red, Green, Blue):

$$2,500 \times 3 = 7,500$$



**Answer:** The resulting flattened feature vector length is **7,500** independent values.

### Problem 2: Classification Error Performance Analysis

**Scenario:** An SVM classifier evaluates a batch of 100 face images from the LFW dataset. The system outputs the predicted names, marking incorrect predictions in red. If the validation yields 88 correct identifications and 12 misclassified labels, calculate the baseline accuracy rate of the trained classifier.

**Solution:**


$$\text{Accuracy} = \frac{\text{Correct Classifications}}{\text{Total Evaluation Universe}} \times 100$$

$$\text{Accuracy} = \frac{88}{100} \times 100 = 88\%$$


**Answer:** The performance metrics reveal a baseline model classification accuracy of **88%**.




# Applications: Hand-written Digit Classification using SVM

This document walks through the step-by-step implementation of an image classification workflow using the standard Scikit-Learn digits dataset and a Support Vector Classifier (SVC).

---

## 1. Concept Name: Data Loading and Matrix Splitting

### Simple Meaning
Before a machine learning model can learn, it needs data formatted correctly:
* **Features Matrix ($X$):** The raw input details. For images, this is the pixel intensity values unrolled into a flat row vector.
* **Target Vector ($y$):** The ground-truth answers or labels (e.g., the number `0`, `1`, `2`, ..., `9`) that match each image.
* **Train/Test Splitting:** We divide our rows into two pools. The **Training Set** acts like a textbook for the model to practice on, while the **Testing Set** acts like an exam with held-out questions to check the model's true accuracy.

---

## 2. Concept Name: Subplot Grid Space Calculation

### Simple Meaning
When plotting multiple tiny images side-by-side in Matplotlib, we construct a grid using `fig.add_subplot(rows, cols, index + 1)`. 
* Columns and rows are 1-indexed (starting at 1).
* Loop variables in code typically start at index 0, meaning we must adjust the plot placement math dynamically inside the loop (`i + 1`).

### Text-Art Visualization (8x8 Subplot Layout)
```text
  +------------- Subplot Figure Grid -------------+
  | [i=0, Box 1]  [i=1, Box 2]  ... [i=7, Box 8]   |
  | [i=8, Box 9]  [i=9, Box 10] ... [i=15, Box 16] |
  |       .             .                 .        |
  |       .             .                 .        |
  | [i=56, Box 57]      ...         [i=63, Box 64] |
  +------------------------------------------------+

```

### Step-by-Step Index Calculation

Let's see how the loop index maps out precisely to coordinate boxes.

#### Problem 1: Grid Coordinates Mapping

Given a loop index $i$, we want to find its exact row and column position in an $8 \times 8$ subplot layout. The formulas are:


$$\text{Row Position} = (i // 8) + 1$$

$$\text{Column Position} = (i \% 8) + 1$$

Let's compute the grid location for index **$i = 19$**:

* **Step 1: Compute Row Placement (Integer Division)**

$$19 // 8 = 2$$



Adding 1 for 1-based index: $2 + 1 = 3$ (Row 3).
* **Step 2: Compute Column Placement (Modulo Division)**

$$19 \% 8 = 3$$



Adding 1 for 1-based index: $3 + 1 = 4$ (Column 4).
* **Result:** Loop index 19 maps directly to the subplot box located at **Row 3, Column 4**, displaying as box number **20** (`i + 1`).

#### Problem 2: Dataset Proportional Split Size

If a dataset has $N = 1,797$ samples and we use `train_test_split(X, y)` without explicitly setting `test_size`, it defaults to a **$75\%$ training / $25\%$ testing** split.

* **Step 1: Calculate Test sample volume**

$$\text{Test Size} = 1797 \times 0.25 = 449.25 \rightarrow 450\text{ samples}$$


* **Step 2: Calculate Train sample volume**

$$\text{Train Size} = 1797 - 450 = 1347\text{ samples}$$



---

## 3. Python Implementation Pipeline

The complete, runnable script based on the shared notebook screens:

```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn import datasets
from sklearn.svm import SVC
from sklearn.model_selection import train_test_split

# Step 1: Import dataset
digits = datasets.load_digits()
X = digits.data
y = digits.target

# Step 2: Visualizing Data Grid (64 sample digits)
fig = plt.figure(figsize=(6, 6)) # Figure size in inches
# Adjust margins tightly to minimize whitespace
fig.subplots_adjust(left=0, right=1, bottom=0, top=1, hspace=0.05, wspace=0.05)

# Plot the digits: each image is 8x8 pixels
for i in range(64):
    ax = fig.add_subplot(8, 8, i + 1, xticks=[], yticks=[])
    ax.imshow(digits.images[i], cmap=plt.cm.binary, interpolation='nearest')
    # Label the image with the target ground truth value at coordinate (0, 7)
    ax.text(0, 7, str(digits.target[i]), color='blue', fontsize=12)

plt.show()

# Step 3: Splitting data into training and validation sets
# random_state=0 ensures reproducible shuffling splits
Xtrain, Xtest, ytrain, ytest = train_test_split(X, y, random_state=0)

# Step 4: Instantiating and fitting the Support Vector Machine (Linear Kernel)
model = SVC(kernel='linear')
model.fit(Xtrain, ytrain)

# Step 5: Generate predictions on evaluation subset
ypred = model.predict(Xtest)

# Print verification check
print(f"Total training points processed: {Xtrain.shape[0]}")
print(f"Total evaluation test points: {Xtest.shape[0]}")
print(f"First 10 Predicted labels: {ypred[:10]}")
print(f"First 10 Actual labels:    {ytest[:10]}")

```

---

## 4. Practice Problems with Solutions

### Problem 1: Pixel Density Rescaling Math

**Scenario:** A flattened digit vector row in `X` contains pixel values bounded between 0 (white) and 16 (black). Write out the basic math step to normalize a single pixel value $v = 12$ to fall within a standard relative range between `0.0` and `1.0`.

**Solution:**


$$\text{Normalized Value} = \frac{v - v_{min}}{v_{max} - v_{min}}$$


Given $v = 12$, $v_{min} = 0$, $v_{max} = 16$:


$$\text{Normalized Value} = \frac{12 - 0}{16 - 0} = \frac{12}{16} = 0.75$$


**Answer:** The rescaled normalized input coordinate value is **0.75**.

### Problem 2: Tracking Mismatches

**Scenario:** You evaluate a testing subset size containing exactly 10 predictions.

* Target array: `ytest = [2, 5, 8, 0, 1, 7, 4, 3, 9, 6]`
* Predicted array: `ypred = [2, 5, 3, 0, 1, 7, 4, 3, 9, 6]`
Calculate the classification accuracy percentage for this localized slice.

**Solution:**

1. Compare index by index to identify mismatches:
At index position 2 (third number), the real value is `8`, but the model predicted `3`. All other 9 elements are identical matches.
2. Apply accuracy rate arithmetic:

$$\text{Accuracy} = \frac{\text{Correct Matches}}{\text{Total Subset Samples}} \times 100 = \frac{9}{10} \times 100 = 90\%$$



**Answer:** The specific subset classification performance yields **90% accuracy**.


# Evaluating Machine Learning Models: Metrics & Confusion Matrices

This document covers how to evaluate the performance of a classification model (like an SVM) using Scikit-Learn's built-in metric functions, specifically focusing on the Classification Report and the Confusion Matrix.

---

## 1. Concept Name: The Confusion Matrix

### Simple Meaning
A **Confusion Matrix** is a table that allows you to visualize the performance of an algorithm. It compares the *actual* target values with the *predicted* values generated by your model. 
* The **diagonal** elements represent points for which the predicted label is equal to the true label (correct predictions).
* Anything **outside the diagonal** represents a misclassification (where the model got "confused").

### Text-Art Visualization
```text
                  PREDICTED CLASS
                +-------+-------+-------+
                |   0   |   1   |   2   |
        +-------+-------+-------+-------+
 ACTUAL |   0   |  TP   |   E   |   E   |
 CLASS  +-------+-------+-------+-------+
        |   1   |   E   |  TP   |   E   |
        +-------+-------+-------+-------+
        |   2   |   E   |   E   |  TP   |
        +-------+-------+-------+-------+
        
        * TP = True Positive (Correct, on diagonal)
        * E = Error / Misclassification (Off diagonal)

```

### Step-by-Step Numerical Calculations

Let's analyze a specific row from the provided 10x10 confusion matrix output. We will look at **Row 1** (Actual Class 1):
`[ 0 42  0  0  0  0  1  0  3  0 ]`

* **Step 1: Identify Correct Predictions (True Positives)**
Look at the diagonal element for Row 1, Column 1. The value is **42**. The model correctly identified the digit '1' forty-two times.
* **Step 2: Identify Errors (False Negatives)**
Look at the non-zero elements outside the diagonal in that row.
The model predicted a '6' one time (Column 6 is 1).
The model predicted an '8' three times (Column 8 is 3).
* **Step 3: Calculate Total Actual Instances (Support)**
Sum the entire row:

$$42 + 1 + 3 = 46$$



There are exactly 46 images of the digit '1' in this test set.

---

## 2. Concept Name: Classification Report (Precision, Recall, F1-Score)

### Simple Meaning

The **Classification Report** gives a detailed breakdown of performance for *each individual class*, moving beyond just overall accuracy.

* **Precision:** When the model guesses a class, how often is it actually correct? (Quality)
* **Recall:** Out of all the true examples of a class, how many did the model successfully find? (Quantity)
* **F1-Score:** A balanced harmonic mean between Precision and Recall.
* **Support:** The actual number of occurrences of the class in the dataset.

### Mathematical Formulas

$$\text{Precision} = \frac{TP}{TP + FP}$$

$$\text{Recall} = \frac{TP}{TP + FN}$$

*(Where TP = True Positives, FP = False Positives, FN = False Negatives)*

### Code Implementation

Here is how you generate these reports in Python using Scikit-Learn:

```python
from sklearn import metrics

# 1. Generate and print the Classification Report
# This shows precision, recall, f1-score, and support per class
print("Classification Report:")
print(metrics.classification_report(ypred, ytest))

# 2. Generate and print the Confusion Matrix
# This shows the raw correct and incorrect prediction counts
print("\nConfusion Matrix:")
print(metrics.confusion_matrix(ypred, ytest))

```

---

## 3. Practice Problems with Solutions

### Problem 1: Calculating Recall from a Confusion Matrix

**Scenario:** Using the provided 97% accuracy model data, we know that for Class 1, $TP = 42$ and $FN = 4$ (1 misclassified as '6', 3 misclassified as '8'). Calculate the Recall for Class 1.

**Solution:**

1. Use the Recall formula:

$$\text{Recall} = \frac{TP}{TP + FN}$$


2. Plug in the numbers:

$$\text{Recall} = \frac{42}{42 + 4}$$


$$\text{Recall} = \frac{42}{46} \approx 0.913$$



**Answer:** The recall is **0.91**. This perfectly matches the `0.91` shown in the actual classification report output for Class 1.

### Problem 2: Model Comparison

**Scenario:** You have run your SVM model twice with different hyperparameters (e.g., changing from a linear kernel to an RBF kernel).
Model A gives an overall accuracy of **0.97**.
Model B gives an overall accuracy of **0.99**.
Looking at Model A, what is the F1-Score for Class 8, and what is the total number of test samples evaluated?

**Solution:**

1. Locate Class 8 in the first classification report (Model A). The F1-score column reads **0.93**.
2. Locate the "Support" column total at the bottom of the report. The total support is **450**.
**Answer:** The F1-Score for Class 8 is **0.93**, and the total evaluation dataset size is **450 samples**.


# Face Recognition with Support Vector Machines (SVM)

This notebook covers data ingestion, dimensional analysis, and visualization subplots using the **Labeled Faces in the Wild (LFW)** dataset.

---

## 1. Concept Name: Dataset Tuple Shape & Dimension Volumetrics

### Simple Meaning
When dealing with an image dataset in machine learning, its structural setup is represented as a tuple: `(samples, height, width)`. 

* **Samples:** The total count of separate photos available in the data array.
* **Height & Width:** The dimensional resolution measured in pixels for each individual photo.
* **Min Faces Per Person:** A filter parameter that forces the system to download images only for individuals who have at least a specified number of unique photos in the source library. This keeps the dataset balanced so the model has enough sample variation to learn from.

### Text-Art Visualization (Structural Mapping)
```text
  Dataset Array Shape: (1348, 62, 47)
  
  +--- Entire Dataset Universe ---------------------------------+
  |                                                             |
  |  [ Image 0 ]      [ Image 1 ]      ...    [ Image 1347 ]     |
  |  +-------+        +-------+               +-------+         |
  |  | 47 px |        | 47 px |               | 47 px |         |
  |  |       | 62 px  |       | 62 px         |       | 62 px   |
  |  +-------+        +-------+               +-------+         |
  |                                                             |
  +-------------------------------------------------------------+

```

### Step-by-Step Numerical Calculations

Let's break down the mathematical scale of the input space dynamically based on the image shape metadata printout `(1348, 62, 47)`.

#### Problem 1: Pixel Content per Matrix Image

Calculate the total number of input features (pixels) contained within a single facial photo in this dataset.

* **Step 1:** Extract individual dimensions from the shape tuple: $\text{Height} = 62$, $\text{Width} = 47$.
* **Step 2:** Multiply height by width to find the total pixel area grid:

$$\text{Total Pixels} = 62 \times 47 = 2,914\text{ pixels}$$


* **Result:** Each unrolled feature vector array fed into the SVM will consist of exactly **2,914** numerical pixel parameters.

#### Problem 2: Complete Dataset Matrix Volume

Calculate the total number of single data points (individual pixel values) the model must parse across the entire training/testing landscape.

* **Step 1:** Extract the total sample count: $\text{Total Samples} = 1,348$.
* **Step 2:** Multiply the absolute number of samples by the pixel count computed in Problem 1:

$$\text{Total Elements} = 1,348 \times 2,914 = 3,928,072\text{ data values}$$



---

## 2. Concept Name: Linearized Subplot Grid Flattening

### Simple Meaning

When preparing a target frame for visualizing images side-by-side using `plt.subplots(rows, cols)`, Matplotlib returns a multi-dimensional array of axes coordinates. Running `.flat` collapses this 2D coordinate grid into a single 1D sequence loop. This allows `enumerate()` to iterate from 0 to 8 smoothly to draw images sequentially into a $3 \times 3$ grid box layout without needing complex nested loops.

---

## 3. Python Implementation Code Pipeline

Below is the execution workflow used to acquire metadata coordinates and map the collection visually.

```python
# Step 1: Initialize operational utilities and default plotting aesthetics
import numpy as np
import matplotlib.pyplot as plt
from scipy import stats
import seaborn as sns; sns.set()

# Step 2: Ingest the LFW data filtered by minimum volume criteria
from sklearn.datasets import fetch_lfw_people
faces = fetch_lfw_people(min_faces_per_person=60)

# Step 3: Print dimensional structural properties
print("Target Class Profiles:\n", faces.target_names)
print("Data Matrix Structural Shape:", faces.images.shape)

# Step 4: Render a 3x3 evaluation grid framework
fig, ax = plt.subplots(3, 3)
for i, axi in enumerate(ax.flat):
    # Display the grayscale facial structure using the 'bone' color space map
    axi.imshow(faces.images[i], cmap='bone')
    
    # Strip boundary tick values and set target names as x-labels
    axi.set(xticks=[], yticks=[],
            xlabel=faces.target_names[faces.target[i]])

plt.tight_layout()
plt.show()

```

---

## 4. Analytical Practice Problems

### Problem 1: Label Verification Logic

**Scenario:** While iterating through the subplot rendering sequence, the loop reaches item index $i = 4$. The class identification integer stored at `faces.target[4]` is `3`. Based on the console log list array: `['Ariel Sharon', 'Colin Powell', 'Donald Rumsfeld', 'George W Bush', 'Gerhard Schroeder', 'Hugo Chavez', 'Junichiro Koizumi', 'Tony Blair']`, which target label will be attached as the subtitle string under this specific face plot?

**Solution:**

1. Match the 0-based index to the label list structure:
* Index 0: `'Ariel Sharon'`
* Index 1: `'Colin Powell'`
* Index 2: `'Donald Rumsfeld'`
* Index 3: `'George W Bush'`


2. The index points directly to item position 3.
**Answer:** The string text drawn below the image will be **'George W Bush'**.

### Problem 2: Downsampling Spatial Adjustments

**Scenario:** Processing thousands of 2,914-pixel dimensions impacts the training speed of a standard SVM. If you configure `fetch_lfw_people` using the parameter `resize=0.5` to cut the height and width in half, what will be the length of the new flattened feature vector?

**Solution:**

1. Calculate the new downscaled dimensions (rounding down to whole integer pixels):

$$\text{New Height} = 62 \times 0.5 = 31\text{ pixels}$$


$$\text{New Width} = 47 \times 0.5 = 23.5 \rightarrow 23\text{ pixels}$$


2. Multiply the updated values to find the new surface pixel length:

$$\text{New Feature Space Length} = 31 \times 23 = 713$$



**Answer:** The compressed flattened feature vector length drops down to **713** inputs.


# Face Recognition: Dimensionality Reduction (PCA) & SVM Pipelines

This document details the machine learning workflow for structural face classification using Principal Component Analysis (PCA) preprocessing packaged seamlessly with a Support Vector Classifier (SVC).

---

## 1. Concept Name: Machine Learning Pipelines & Dimensionality Preprocessing

### Simple Meaning
When processing large raw images containing nearly 3,000 pixels ($62 \times 47$), treating every pixel as an independent feature makes models computationally heavy and prone to noise. 

* **Principal Component Analysis (PCA):** A dimensionality reduction technique that finds the directions of maximum variance in high-dimensional data, extracting the most meaningful fundamental components (e.g., reducing 2,914 features down to 150 or 350).
* **Pipeline (`make_pipeline`):** A wrapper tool that chains data transformation tools (like PCA) and estimators (like SVC) together sequentially. Data flows automatically from preprocessing to modeling, preventing data leakage during validation.
* **Balanced Class Weight:** Automatically adjusts weights inversely proportional to class frequencies in the input data to handle unequal representation across targeted categories.

### Text-Art Visualization (Pipeline Architecture)
```text
  [ Raw Data Matrix ] (1348 samples x 2914 pixels)
          │
          ▼
┌─────────────────── Pipeline ───────────────────┐
│                                                │
│  [ Preprocessor ] Component Analysis (PCA)     │
│                   Reduces features to 150/350  │
│          │                                     │
│          ▼                                     │
│  [ Classifier ]   Support Vector Machine (SVC) │
│                   Finds optimal hyperplanes    │
│                                                │
└────────────────────────────────────────────────┘
          │
          ▼
  [ Final Output Predictions (yfit) ]

```

### Step-by-Step Data Volume & Metric Calculations

#### Problem 1: Training and Testing Splitting Metrics

Based on the classification reports, our total testing subset size is `support = 337`. If the model split targets a standard evaluation balance of **$75\%$ training / $25\%$ testing**, calculate the size of the total dataset universe.

* **Step 1:** Set up the algebraic balance calculation:

$$\text{Total Samples} \times 0.25 = 337$$


* **Step 2:** Isolate and solve for the absolute sample volume:

$$\text{Total Samples} = \frac{337}{0.25} = 1348\text{ total samples}$$



#### Problem 2: Classification Precision Assessment

Let's manually compute the baseline **Precision** performance score for a specific category using the values printed in the final confusion matrix grid layout.

* Formula:

$$\text{Precision} = \frac{\text{True Positives (TP)}}{\text{True Positives (TP)} + \text{False Positives (FP)}}$$



Let's inspect **Class 0 (Ariel Sharon)** from the confusion matrix output:

* True Positives (Row 0, Column 0) = **10**
* False Positives (Sum of Column 0 elements below Row 0): $1 + 0 + 0 + 1 + 1 + 0 + 0 = \mathbf{3}$
* Calculate Precision:

$$\text{Precision} = \frac{10}{10 + 3} = \frac{10}{13} \approx 0.769 \rightarrow 77\%$$


* *Validation Check:* This matches the classification report's precision value of **0.77** for Ariel Sharon.

---

## 2. Python Implementation: The Pipeline Framework

Below is the structured, clean production script implementing the machine learning sequence from transformation to grid validation plots.

```python
import matplotlib.pyplot as plt
from sklearn.svm import SVC
from sklearn.decomposition import PCA
from sklearn.pipeline import make_pipeline
from sklearn.model_selection import train_test_split
from sklearn.metrics import classification_report, confusion_matrix

# Step 1: Initialize sequential pipeline stages
# n_components captures optimal directional variance vectors
pca = PCA(n_components=150, whiten=True, random_state=42)
svc = SVC(kernel='rbf', class_weight='balanced')

# Package preprocessor and estimator into a single pipeline model
model = make_pipeline(pca, svc)

# Step 2: Split data partitions (faces object generated in previous steps)
# Xtrain, Xtest, ytrain, ytest = train_test_split(faces.data, faces.target, random_state=42)

# Step 3: Run optimization fitting across validation arrays
# model.fit(Xtrain, ytrain)
# yfit = model.predict(Xtest)

# Step 4: Construct error tracking plot fields
def plot_prediction_gallery(Xtest, ytest, yfit, target_names):
    fig, ax = plt.subplots(4, 4, figsize=(8, 8))
    for i, axi in enumerate(ax.flat):
        # Reshape the 1D feature vector array back to 2D image coordinates
        axi.imshow(Xtest[i].reshape(62, 47), cmap='bone')
        axi.set(xticks=[], yticks=[])
        
        # Color coding title annotations: Black for correct, Red for misclassifications
        is_correct = yfit[i] == ytest[i]
        color = 'black' if is_correct else 'red'
        
        # Display only the last name for cleanliness (.split()[-1])
        axi.set_ylabel(target_names[yfit[i]].split()[-1], color=color, fontsize=10)
        
    fig.suptitle('Predicted Names; Incorrect Labels in Red', size=14)
    plt.tight_layout()
    plt.show()

# Step 5: Report evaluation scores
# print(classification_report(ytest, yfit, target_names=faces.target_names))
# print(confusion_matrix(ytest, yfit))

```

---

## 3. Analytical Practice Problems

### Problem 1: Model Feature Reduction Ratio

**Scenario:** A feature matrix initially processes an image input size of $62 \times 47$. You pipeline this dataset into a PCA configured to project down to `n_components = 150`. Calculate the percentage reduction in your input feature dimensionality space.

**Solution:**

1. Determine original raw dimensionality volume:

$$\text{Original Space} = 62 \times 47 = 2914\text{ features}$$


2. Calculate the drop in dimensions:

$$\text{Reduction} = 2914 - 150 = 2764\text{ features removed}$$


3. Compute the proportional percentage drop:

$$\text{Percentage Drop} = \left(\frac{2764}{2914}\right) \times 100 \approx 94.85\%$$



**Answer:** The PCA preprocessor successfully eliminates **94.85%** of the feature space while retaining the core variance structure.

### Problem 2: Global Macro Average Computation

**Scenario:** You change your pipeline's target components from 150 to 350 (`n_components=350`), shifting the model's overall tracking accuracy to **0.82**. Looking at the individual recalls for the top three represented target names in the updated output:

* Colin Powell: `0.85`
* Donald Rumsfeld: `0.74`
* George W Bush: `0.86`
Calculate the localized arithmetic macro average recall value for this target subset.

**Solution:**


$$\text{Macro Average Subset Recall} = \frac{\sum(\text{Individual Recalls})}{\text{Count of Evaluated Targets}}$$

$$\text{Macro Average Subset Recall} = \frac{0.85 + 0.74 + 0.86}{3} = \frac{2.45}{3} \approx 0.8166$$


**Answer:** The localized tracking average subset recall is **0.82**.
