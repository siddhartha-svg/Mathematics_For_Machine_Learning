# Comprehensive Math Notes: Set Theory

---

## 1. Introduction to Sets

### What is a Set?
A **set** is a well-defined collection of distinct (unique) objects. 
* **"Well-defined"** means there is no confusion about whether an item belongs to the set or not.
* **Notation:** Sets are usually named using **capital letters** (e.g., $A, B, C$), and the individual items inside them (elements) are written in **lowercase letters** (e.g., $a, b, c$).

---

## 2. Ways to Represent a Set

There are two primary methods to write down a set:

### A. Roster / Tabular Form
* **Simple Meaning:** You explicitly list out every single element, separate them with commas, and enclose them in curly braces `{ }`.
* **Example:** $A = \{1, 2, 3, 4, 5\}$

### B. Set-Builder Form
* **Simple Meaning:** Instead of listing the elements, you write down the common property or rule that describes the elements.
* **Example:** $A = \{x \mid x \text{ is a natural number less than } 6\}$
  *(Read as: "A is the set of all $x$ such that $x$ is a natural number less than 6")*

---

### 📝 Step-by-Step Conversion Problem

**Problem:** Convert the set $P = \{3, 6, 9, 12, \dots\}$ from Roster form to Set-Builder form.

**Step-by-Step Calculation & Explanation:**
1. **Analyze the pattern:** Look at the numbers: $3, 6, 9, 12, \dots$ Notice that they are all multiples of 3.
2. **Express mathematically:** 
   * $3 = 3 \times 1$
   * $6 = 3 \times 2$
   * $9 = 3 \times 3$
   * $12 = 3 \times 4$
   This means every element can be written in the form $3n$, where $n$ is a counting number ($1, 2, 3, 4, \dots$).
3. **Identify the number system:** Counting numbers are called Natural Numbers, denoted by the symbol $\mathbb{N}$. So, $n \in \mathbb{N}$ (meaning $n$ belongs to Natural Numbers).
4. **Write the final rule:** Put it together inside the set-builder syntax.

**Solution:**
$$P = \{x \mid x = 3n, n \in \mathbb{N}\}$$

---

## 3. Types of Sets

| Type of Set | Simple Meaning | Mathematical Example |
| :--- | :--- | :--- |
| **Empty / Void / Null Set** | A set containing absolutely no elements. | $\phi$ or $\{\}$ |
| **Singleton Set** | A set that contains exactly **one** element. | $S = \{5\}$ |
| **Finite Set** | A set where you can finish counting the elements. | $A = \{1, 2, 3\}$ |
| **Infinite Set** | A set where the elements go on forever without stopping. | $B = \{1, 2, 3, \dots\}$ |
| **Equal Sets** | Two sets that contain the exact same elements. | If $A = \{1, 2\}$ and $B = \{2, 1\}$, then $A = B$ |
| **Equivalent Sets** | Two sets that have the **same number** of elements, even if the elements themselves are different. | If $A = \{1, 2, 3\}$ and $B = \{4, 5, 6\}$, both have 3 elements. Thus, $n(A) = n(B)$. |

---

## 4. Subsets and Intervals

### Subsets
* **Simple Meaning:** A set $B$ is a **subset** of set $A$ (written as $B \subseteq A$) if **every single element** in $B$ is also found inside $A$.

#### 📝 Practice Example:
Let:
* $A = \{1, 2, 3, 4, 5\}$
* $B = \{1, 2, 3\}$
* $C = \{2, 3, 6\}$

* **Calculation for B:** Elements of $B$ are $1, 2, 3$. All of these are inside $A$. Therefore, $\mathbf{B \subseteq A}$.
* **Calculation for C:** Elements of $C$ are $2, 3, 6$. The element $6$ is **not** in $A$. Therefore, $\mathbf{C \not\subseteq A}$.

---

### Intervals as Subsets of Real Numbers ($\mathbb{R}$)
When dealing with continuous real numbers between two values $a$ and $b$:

1. **Open Interval $(a, b)$:** Does **not** include the endpoints $a$ and $b$.
   $$(a, b) = \{x \mid a < x < b\}$$
2. **Closed Interval $[a, b]$:** **Includes** both endpoints $a$ and $b$.
   $$[a, b] = \{x \mid a \le x \le b\}$$
3. **Semi-Open / Semi-Closed Intervals:** Includes only one endpoint.
   * $[a, b) = \{x \mid a \le x < b\}$ (Includes $a$, excludes $b$)
   * $(a, b] = \{x \mid a < x \le b\}$ (Excludes $a$, includes $b$)

---

## 5. Power Set and Universal Set

### Power Set
* **Simple Meaning:** The collection of **all possible subsets** that you can create from a given set $A$. It is denoted by $P(A)$.
* **Formula for total number of elements:** If a set has $m$ elements, its power set will have $2^m$ elements.

#### 📝 Step-by-Step Calculation Problem
**Problem:** Find the Power Set of $A = \{1, 2\}$.

**Step-by-Step Calculation:**
1. **Count elements:** Set $A$ has $2$ elements ($m = 2$).
2. **Determine size:** The power set must contain $2^2 = 4$ subsets.
3. **List subsets systematically:**
   * The empty set is a subset of every set: $\phi$
   * Subsets with 1 element: $\{1\}$, $\{2\}$
   * Subsets with 2 elements (the set itself): $\{1, 2\}$
4. **Group them together:** Put all listed subsets into one large set.

**Solution:**
$$P(A) = \{\phi, \{1\}, \{2\}, \{1, 2\}\}$$

---

### Universal Set
* **Simple Meaning:** The mother of all sets in a specific problem. It contains all the elements under consideration and is denoted by $\mathbf{U}$.

---

## 6. Venn Diagram Representation

A **Venn Diagram** is a visual way to show relationships between sets. 
* The **Universal Set ($U$)** is drawn as a large **Rectangle**.
* **Subsets** (like Set $A$ and Set $B$) are drawn as **Circles** inside that rectangle.

```text
+------------------------------------------+
| Universal Set (U)                        |
|                                          |
|    +------------+      +------------+    |
|   /              \    /              \   |
|  /   Set A        \  /   Set B        \  |
| |                  ||                  | |
| |    Elements      ||    Elements      | |
|  \                /  \                /  |
|   \              /    \              /   |
|    +------------+      +------------+    |
|                                          |
+------------------------------------------+
```


# Advanced Set Theory: Power Sets, Venn Diagrams, and Operations

---

## 1. Power Set Cardinality

### Concept Name: Power Set Calculation
The **Power Set** of a set $A$, denoted as $P(A)$, is the set containing all possible subsets of $A$. If a set $A$ contains $n$ elements, the total number of elements in its power set is calculated using the formula:
$$n(P(A)) = 2^n$$

---

### 📝 Step-by-Step Calculation Problem

**Problem:** 
Let $A = \{1, 2, 3\}$. Find its power set $P(A)$ and verify the total number of subsets.

**Step-by-Step Explanation & Calculations:**
1. **Count the elements of set A:** 
   The given set is $A = \{1, 2, 3\}$. It contains 3 distinct elements.
   $$n = 3$$
2. **Calculate the expected number of subsets:** 
   Apply the formula $2^n$:
   $$n(P(A)) = 2^3 = 2 \times 2 \times 2 = 8 \text{ elements}$$
3. **List all subsets systematically:**
   * **Empty set (0 elements):** $\phi$
   * **Singletons (1 element each):** $\{1\}, \{2\}, \{3\}$
   * **Pairs (2 elements each):** $\{1, 2\}, \{2, 3\}, \{1, 3\}$
   * **The full set itself (3 elements):** $A$ (which is $\{1, 2, 3\}$)
4. **Group into the final Power Set:**

**Solution:**
$$P(A) = \{\phi, A, \{1\}, \{2\}, \{3\}, \{1, 2\}, \{2, 3\}, \{1, 3\}\}$$
$$n(P(A)) = 8$$

---

## 2. Venn Diagrams

### Concept Name: Visualizing Sets with Venn Diagrams
A **Venn Diagram** uses a large bounding rectangle to represent the **Universal Set ($U$)** and overlapping or distinct circles inside it to represent individual sets and their shared elements.

```
+-------------------------------------------------+
| U (Universal Set)                               |
|   7 .                                           |
|        +-----------------+   +-----------------+  |
|       /   A              \ /   B              \ |
|      /     . 1            X     . 5            \|
|     |                    | |                    | |
|     |      . 2           | |    . 6             | |
|     |                    |4|                    | |
|      \     . 3            X                    /  |
|       \                  / \                  /   |
|        +-----------------+   +-----------------+  |
|                                             . 8 |
+-------------------------------------------------+
```

### 📝 Step-by-Step Verification Problem

**Problem:**
Given $U = \{1, 2, 3, 4, 5, 6, 7, 8\}$, $A = \{1, 2, 3, 4\}$, and $B = \{4, 5, 6\}$. Verify how the numbers are arranged inside the diagram.

**Step-by-Step Explanation:**

1. **Find the intersection (shared numbers):** Look for elements present in both $A$ and $B$. The number $4$ belongs to both. Place it in the overlapping region.
2. **Find elements exclusive to A:** Remove the shared elements from $A$: $\{1, 2, 3, 4\} \setminus \{4\} = \{1, 2, 3\}$. Place these inside circle $A$ only.
3. **Find elements exclusive to B:** Remove the shared elements from $B$: $\{4, 5, 6\} \setminus \{4\} = \{5, 6\}$. Place these inside circle $B$ only.
4. **Find outside elements:** Identify elements in $U$ that are neither in $A$ nor in $B$: $\{7, 8\}$. Place these outside the circles but inside the rectangle.

---

## 3. Operations on Sets

### Concept 1: Union of Sets ($A \cup B$)

* **Simple Meaning:** Combining all elements from both sets together into one big set without repeating any duplicates.
* **Formula:** $A \cup B = \{x \mid x \in A \text{ or } x \in B\}$

### Concept 2: Intersection of Sets ($A \cap B$)

* **Simple Meaning:** Collecting only the common elements that show up in both sets simultaneously.
* **Formula:** $A \cap B = \{x \mid x \in A \text{ and } x \in B\}$
* **Note:** If $A \cap B = \phi$, the sets are called **disjoint sets** (they share nothing).

### Concept 3: Difference of Sets ($A \setminus B$ or $A - B$)

* **Simple Meaning:** Starting with set $A$ and cutting away any elements that also happen to belong to set $B$.
* **Formula:** $A \setminus B = \{x \mid x \in A \text{ and } x \notin B\}$

### Concept 4: Complement of a Set ($A'$)

* **Simple Meaning:** Everything in the universal set ($U$) that is **not** inside set $A$.
* **Formula:** $A' = U \setminus A = \{x \mid x \in U \text{ and } x \notin A\}$

---

### 📝 Operations Practice Problems

Let's use the sets:

* $U = \{1, 2, 3, 4, 5, 6, 7, 8\}$
* $A = \{1, 2, 3, 4\}$
* $B = \{4, 5, 6\}$

#### Problem A: Calculate $A \cup B$

* **Calculation:** Combine all items from $A$ and $B$: $1, 2, 3, 4$ and $4, 5, 6$. Write $4$ only once.
* **Solution:** $A \cup B = \{1, 2, 3, 4, 5, 6\}$

#### Problem B: Calculate $A \cap B$

* **Calculation:** Find what is common between $\{1, 2, 3, 4\}$ and $\{4, 5, 6\}$.
* **Solution:** $A \cap B = \{4\}$

#### Problem C: Calculate $A \setminus B$

* **Calculation:** Take $A = \{1, 2, 3, 4\}$ and drop the element $4$ because it appears in $B$.
* **Solution:** $A \setminus B = \{1, 2, 3\}$

#### Problem D: Calculate the complement of $A$ ($U \setminus A$)

* **Calculation:** Take everything from $U$ except the elements $1, 2, 3, 4$.
* **Solution:** $A' = \{5, 6, 7, 8\}$

---

## 4. Visualizing Set Operations via Text-Graphs

Below are text-based diagrams illustrating how regions are shaded (represented by `///`) for different operations inside the Universal set environment.

### Disjoint Sets ($A \cap B = \phi$)

```
+-----------------------+
| U                     |
|   +---+       +---+   |
|  /     \     /     \  |
| |   A   |   |   B   | |
|  \     /     /     \  |
|   +---+       +---+   |
+-----------------------+

```

### Union ($A \cup B$)

```
+-----------------------+
| U                     |
|   +-----------+       |
|  / /////////   \      |
| | // A ///// B  |     |
|  \ /////////   /      |
|   +-----------+       |
|  Both circles filled  |
+-----------------------+

```

### Difference ($A \setminus B$)

```
+-----------------------+
| U                     |
|   +-----------+       |
|  / /////       \      |
| | / A //    B   |     |
|  \ /////       /      |
|   +-----------+       |
| Only left crescent    |
+-----------------------+

```

### Intersection ($A \cap B$)

```
+-----------------------+
| U                     |
|   +-----------+       |
|  /     ///     \      |
| |   A |///| B   |     |
|  \     ///     /      |
|   +-----------+       |
| Only shared center    |
+-----------------------+

```




# Advanced Set Theory: Laws, Properties, and Cardinality

---

## 1. Properties of Complement & Symmetric Difference

### Concept Name: Complement Properties
The complement of a set $A$ (denoted as $A'$) includes all elements in the Universal Set $U$ that do not belong to $A$. The fundamental properties are:
1. **$A \cup A' = U$**: A set combined with its complement yields the entire universal set.
2. **$A \cap A' = \phi$**: A set and its complement share absolutely no elements.
3. **$U' = \phi$**: The complement of everything is nothing.
4. **$\phi' = U$**: The complement of nothing is everything.
5. **$(A')' = A$**: The complement of a complement brings you back to the original set.

### Concept Name: Symmetric Difference ($A \triangle B$)
* **Simple Meaning:** The set of elements that belong to either set $A$ or set $B$, but **not both** at the same time. It cuts out the overlapping intersection.
* **Formula:** 
  $$A \triangle B = (A \setminus B) \cup (B \setminus A) = \{x : x \in A \cup B, x \notin A \cap B\}$$

---

### 📝 Symmetric Difference Step-by-Step Problem

**Problem:** Given $A = \{1, 2, 3, 4\}$ and $B = \{3, 4, 5, 6\}$, calculate the Symmetric Difference $A \triangle B$.

**Step-by-Step Calculation:**
1. **Find $A \setminus B$ (Elements in $A$ but not in $B$):**
   Remove $3$ and $4$ from set $A$.
   $$A \setminus B = \{1, 2\}$$
2. **Find $B \setminus A$ (Elements in $B$ but not in $A$):**
   Remove $3$ and $4$ from set $B$.
   $$B \setminus A = \{5, 6\}$$
3. **Combine the results using Union ($\cup$):**
   $$A \triangle B = \{1, 2\} \cup \{5, 6\} = \{1, 2, 5, 6\}$$

---

## 2. Laws of Algebra of Sets

These rules govern how sets interact algebraically:

| Law Name | Mathematical Expressions | Simple Meaning |
| :--- | :--- | :--- |
| **Idempotent Laws** | $A \cap A = A$ <br> $A \cup A = A$ | Intersecting or uniting a set with itself changes nothing. |
| **Identity Laws** | $A \cap U = A$ <br> $A \cup \phi = A$ | $U$ acts as the identity for intersection; $\phi$ acts as the identity for union. |
| **Commutative Laws** | $A \cup B = B \cup A$ <br> $A \cap B = B \cap A$ | The ordering of the sets does not affect the outcome. |
| **Associative Laws** | $A \cup (B \cup C) = (A \cup B) \cup C$ <br> $A \cap (B \cap C) = (A \cap B) \cap C$ | Grouping order does not matter when operations are identical. |
| **Distributive Laws** | $A \cup (B \cap C) = (A \cup B) \cap (A \cup C)$ <br> $A \cap (B \cup C) = (A \cap B) \cup (A \cap C)$ | Operations distribute over one another, similar to standard algebra. |
| **De Morgan's Laws** | $(A \cup B)' = A' \cap B'$ <br> $(A \cap B)' = A' \cup B'$ | The complement flips a union to an intersection and vice versa. |

---

### 📊 De Morgan's Law Text-Graph Representation

Visualizing $(A \cup B)' = A' \cap B'$ via line patterns:

```text
De Morgan's Shading Graph: Everything outside both circles A and B

+------------------------------------------+ U
|  \\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\    |
|  \\\\   +---+            +---+   \\\\    |
|  \\\\  /     \          /     \  \\\\    |
|  \\\\ |   A   |        |   B   | \\\\    |
|  \\\\  \     /          \     /  \\\\    |
|  \\\\   +---+            +---+   \\\\    |
|  \\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\    |
+------------------------------------------+

```

---

## 3. Results on Cardinality of Sets

### Concept Name: Cardinality Formulas

Cardinality, denoted by $n(A)$, refers to the total count of elements inside a set. Key foundational rules include:

1. **Two-Set Union:**

$$n(A \cup B) = n(A) + n(B) - n(A \cap B)$$



*(We subtract the intersection so we don't double-count elements where the circles overlap)*.
2. **Set Difference / Exclusivity:**

$$n(A \setminus B) = n(A \cap B') = n(A) - n(A \cap B)$$


3. **Three-Set Union:**

$$n(A \cup B \cup C) = n(A) + n(B) + n(C) - n(A \cap B) - n(B \cap C) - n(C \cap A) + n(A \cap B \cap C)$$



---

### 📝 Cardinality Practice Problems

#### Problem 1: Two-Set Union Calculation

In a class, 30 students like Math ($M$), 25 like Science ($S$), and 10 like both subjects. How many students like at least one of the subjects ($M \cup S$)?

**Step-by-Step Calculation:**

* Given values: $n(M) = 30$, $n(S) = 25$, $n(S \cap M) = 10$
* Apply formula: $n(M \cup S) = n(M) + n(S) - n(M \cap S)$
* Substitute values:

$$n(M \cup S) = 30 + 25 - 10$$


$$n(M \cup S) = 55 - 10 = 45$$



**Solution:** 45 students like at least one subject.

---

#### Problem 2: Three-Set Union Calculation

Let:

* $n(A) = 20, n(B) = 25, n(C) = 30$
* $n(A \cap B) = 8, n(B \cap C) = 10, n(C \cap A) = 7$
* $n(A \cap B \cap C) = 3$

Find $n(A \cup B \cup C)$.

**Step-by-Step Calculation:**

1. **Write out the base formula:**

$$n(A \cup B \cup C) = n(A) + n(B) + n(C) - n(A \cap B) - n(B \cap C) - n(C \cap A) + n(A \cap B \cap C)$$


2. **Substitute your values step by step:**

$$n(A \cup B \cup C) = 20 + 25 + 30 - 8 - 10 - 7 + 3$$


3. **Perform additions and subtractions left-to-right:**
* $20 + 25 + 30 = 75$
* $75 - 8 = 67$
* $67 - 10 = 57$
* $57 - 7 = 50$
* $50 + 3 = 53$



**Solution:**


$$n(A \cup B \cup C) = 53$$

---

### 📊 Three-Set Cardinality Graph Diagram

```
         +---------------------------------------+ U
         |           /---------\                 |
         |          /     A     \                |
         |         /   20        \               |
         |        |     /----\    |              |
         |        |    /  3   \   |              |
         |     /--+---+--------+--+---\          |
         |    /   |    \  B   /   |    \         |
         |   /    \     \----/    /     \        |
         |  /  C   \-------------/    25 \       |
         | /   30                         \      |
         | \                              /      |
         |  \----------------------------/       |
         +---------------------------------------+

```




# Set Theory: Word Problems & Practical Applications

---

## 1. Concept: Finding Elements Exclusive to One Set

### Simple Meaning
When we want to find the elements that belong to set $A$ but **do not** belong to set $B$, we are finding the set difference, written as $A \setminus B$ or $A \cap B'$. 

To find the *number* of such elements, we take the total count of elements in $A$ and subtract the elements that $A$ shares with $B$ (the intersection).

### Cardinality Formula
$$n(A \cap B') = n(A \setminus B) = n(A) - n(A \cap B)$$

---

### 📝 Problem 1: Step-by-Step Solution

**Problem Statement:**  
If $n(U) = 200$, $n(A) = 120$, and $n(A \cap B) = 30$, compute $n(A \cap B')$.

**Step-by-Step Calculation:**
1. **Identify Given Data:**  
   * Total elements in Universal set, $n(U) = 200$
   * Total elements in set $A$, $n(A) = 120$
   * Shared elements between $A$ and $B$, $n(A \cap B) = 30$
2. **Apply the Exclusion Formula:**  
   $$n(A \cap B') = n(A) - n(A \cap B)$$
3. **Substitute the numbers and compute:**  
   $$n(A \cap B') = 120 - 30 = 90$$

**Solution:**  
$$n(A \cap B') = 90$$

### 📊 Venn Diagram Representation

```text
+-----------------------------------+ U
|  Universal Set (U = 200)          |
|                                   |
|     +---------+     +---------+   |
|    /  A        \   /        B  \  |
|   /  /////////  \_/             \ |
|  |  //////////  | |              ||
|  |  // 90 ////  |30|             ||
|   \  /////////  / \             / |
|    \  ///////// /   \          /  |
|     +---------+     +---------+   |
|                                   |
+-----------------------------------+
Note: The shaded area (///) represents n(A ∩ B') = 90

```

---

## 2. Concept: Three-Set Union Applications

### Simple Meaning

When tracking items or people divided into three different groups (like three different sports), some items will belong to multiple categories at the same time. To find the total combined number of unique individuals across all three sets without double-counting anyone, we use the Three-Set Union formula.

### Cardinality Formula

$$n(F \cup H \cup C) = n(F) + n(H) + n(C) - n(F \cap H) - n(F \cap C) - n(H \cap C) + n(F \cap H \cap C)$$

---

### 📝 Problem 2: Step-by-Step Solution

**Problem Statement:**

In a group of students, 64 play football ($F$), 45 play hockey ($H$), and 45 play cricket ($C$). 22 play football and hockey, 24 play football and cricket, 15 play hockey and cricket, and 8 play all three games. Assume that each student in the group plays at least one game. Find the total number of students in the group.

**Step-by-Step Calculation:**

1. **Extract and Define Variables:**
* $n(F) = 64$ (Football)
* $n(H) = 45$ (Hockey)
* $n(C) = 45$ (Cricket)
* $n(F \cap H) = 22$ (Football & Hockey)
* $n(F \cap C) = 24$ (Football & Cricket)
* $n(H \cap C) = 15$ (Hockey & Cricket)
* $n(F \cap H \cap C) = 8$ (All three games)


2. **Set up the Three-Set Equation:**
$$n(F \cup H \cup C) = 64 + 45 + 45 - 22 - 24 - 15 + 8$$


3. **Stepwise Computation:**
* Add the individual sets:
$$64 + 45 + 45 = 154$$


* Subtract the two-set intersections:
$$154 - 22 = 132$$


$$132 - 24 = 108$$


$$108 - 15 = 93$$


* Add back the central three-set intersection:
$$93 + 8 = 101$$





**Solution:**

The total number of students in the group is **101**.

### 📊 Three-Set Venn Diagram

```text
                  /---------\
                 /  Football \
                /    (F)      \
               |      26       |
               |   /-----\     |
               |14/   8   \16  |
            /--+--+-------+--+---\
           /   |   \ 101 /   |    \
          /     \   \---/   /      \
         / Hockey\---------/ Cricket\
        /   (H)               (C)    \
       |    16                 14     |
        \                            /
         \--------------------------/

```

---

## 3. Concept: Maximizing/Minimizing Intersections

### Simple Meaning

When we are given total figures but don't know the exact size of the combined union ($n(S \cup T)$), we can bound it. The total union can never be larger than the Universal Set ($U$), and it can never be smaller than the size of the single largest set involved. Re-arranging the formula allows us to analyze the overlap boundaries.

### Bounding Logic Formulas

$$n(S \cup T) = n(S) + n(T) - n(S \cap T)$$

$$\Rightarrow n(S \cap T) = n(S) + n(T) - n(S \cup T)$$

Where the value constraints must satisfy:


$$\text{Largest single set size} \le n(S \cup T) \le n(U)$$

---

### 📝 Problem 3: Step-by-Step Solution

**Problem Statement:**

Given $n(U) = 1000$, $n(S) = 720$, and $n(T) = 450$, establish the equation constraints to evaluate $n(S \cap T)$.

**Step-by-Step Calculation:**

1. **Find Limits for the Union $n(S \cup T)$:**
* **Minimum possible value:** The union must contain at least as many elements as the largest standalone set. Since $n(S) = 720$ is larger than $n(T) = 450$, the union cannot be lower than $720$.
* **Maximum possible value:** The union cannot exceed the total size of the universal set, which is $1000$.
* **Inequality statement:**
$$720 \le n(S \cup T) \le 1000$$




2. **Isolate the Target Variable ($n(S \cap T)$):**
Substitute the known constants into the isolated formula:
$$n(S \cap T) = 720 + 450 - n(S \cup T)$$


$$n(S \cap T) = 1170 - n(S \cup T)$$


3. **Evaluate Boundaries:**
* When the union is at its maximum ($1000$):
$$\text{Minimum Intersection} = 1170 - 1000 = 170$$


* When the union is at its minimum ($720$):
$$\text{Maximum Intersection} = 1170 - 720 = 450$$





**Solution:**

The intersection size is variable depending on the population overlap, bounded by:

$$170 \le n(S \cap T) \le 450$$

