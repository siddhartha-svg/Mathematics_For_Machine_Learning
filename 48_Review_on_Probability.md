# Fundamentals of Probability: Definitions, Rules, and Applications

---

## 1. Introduction to Probability Concepts

### Concept Name: Random Experiment
* **Simple Meaning:** A process or action where we know all the possible results that could happen ahead of time, but we cannot predict exactly which specific outcome will occur on any single trial.
* **Examples:** Tossing a coin (could be Heads or Tails), rolling a six-sided die (could be 1, 2, 3, 4, 5, or 6).
* **Definition:** Probability serves as the **mathematical measure of uncertainty** for a random experiment.

### Concept Name: Classical Approach to Probability
* **Simple Meaning:** The simplest way to calculate the chance of something happening when all individual outcomes are equally likely. You divide the number of ways your specific event can happen by the total number of things that could possibly happen.
* **Formula:**
  $$\text{Probability} = \frac{\text{Number of favourable outcomes}}{\text{Total number of outcomes}}$$

---

## 2. Key Terminology and Types of Events

### Standard Definitions
1. **Sample Space ($S$):** The complete set containing absolutely all possible outcomes of a random experiment.
2. **Event ($E$):** Any collection of outcomes from the experiment. Mathematically, it is a subset of the sample space ($E \subseteq S$).

### Types of Events

| Event Type | Simple Meaning | Mathematical Notation |
| :--- | :--- | :--- |
| **Sure Event** | An event that is absolutely certain to happen every time. | $P(E) = 1$ |
| **Impossible Event** | An event that can never happen under any circumstance. | $P(E) = 0$ |
| **Mutually Exclusive Events** | Events that cannot happen at the same time (no overlap). | $E \cap F = \phi$ |
| **Exhaustive Events** | A group of events that together cover every outcome in the sample space. | $E \cup F = S$ |

---

### 📝 Step-by-Step Concept Verification Problem

**Problem:** Consider a sample space containing integers from 1 to 100: $S = \{1, 2, \dots, 100\}$. Let $E_1$ be the event of choosing an odd number, and $E_2$ be the event of choosing an even number. Verify if they are mutually exclusive and exhaustive.

**Step-by-Step Calculation:**
1. **List the events:**
   * $E_1 = \{1, 3, 5, \dots, 99\}$
   * $E_2 = \{2, 4, 6, \dots, 100\}$
2. **Check for Mutual Exclusivity (Intersection $\cap$):**
   Find any elements present in both sets. Since a number cannot be both odd and even:
   $$E_1 \cap E_2 = \phi \implies \text{They are Mutually Exclusive.}$$
3. **Check for Exhaustive Property (Union $\cup$):**
   Combine both sets together:
   $$E_1 \cup E_2 = \{1, 2, 3, 4, \dots, 100\} = S \implies \text{They are Exhaustive.}$$

---

## 3. The Addition Rule of Probability

### Concept Name: Probability Addition Formula Derivation
By taking the cardinality rule of sets and dividing every term by the total number of items in the sample space ($n(S)$), we transform counting numbers into probabilities:

$$\frac{n(A \cup B)}{n(S)} = \frac{n(A)}{n(S)} + \frac{n(B)}{n(S)} - \frac{n(A \cap B)}{n(S)}$$

This yields the fundamental **Addition Rule for Two Events**:
$$P(A \cup B) = P(A) + P(B) - P(A \cap B)$$

For **Three Events**, the rule expands to adjust for overlapping segments:
$$P(A \cup B \cup C) = P(A) + P(B) + P(C) - P(A \cap B) - P(B \cap C) - P(C \cap A) + P(A \cap B \cap C)$$

---

### 📝 Practical Application Word Problem

**Problem Statement:** One integer is chosen at random from the integers $1, 2, \dots, 100$. What is the probability that the chosen integer is divisible by 6 or 8?

**Step-by-Step Calculation:**

1. **Find total sample size:**  
   $$n(S) = 100$$

2. **Calculate favorable outcomes for Event $A$ (Divisible by 6):**  
   Divide 100 by 6 to find how many full multiples fit inside 100:
   $$\lfloor 100 / 6 \rfloor = 16 \implies n(A) = 16$$
   $$P(A) = \frac{16}{100}$$

3. **Calculate favorable outcomes for Event $B$ (Divisible by 8):**  
   Divide 100 by 8:
   $$\lfloor 100 / 8 \rfloor = 12 \implies n(B) = 12$$
   $$P(B) = \frac{12}{100}$$

4. **Calculate shared outcomes ($A \cap B$ - Divisible by BOTH 6 and 8):**  
   Find the Least Common Multiple (LCM) of 6 and 8. The smallest number divisible by both is 24. Find the multiples of 24 up to 100:
   $$\lfloor 100 / 24 \rfloor = 4 \implies n(A \cap B) = 4 \text{ (Numbers: 24, 48, 72, 96)}$$
   $$P(A \cap B) = \frac{4}{100}$$

5. **Apply the Probability Addition Rule:**  
   $$P(A \cup B) = P(A) + P(B) - P(A \cap B)$$
   $$P(A \cup B) = \frac{16}{100} + \frac{12}{100} - \frac{4}{100}$$
   $$P(A \cup B) = \frac{16 + 12 - 4}{100} = \frac{24}{100} = 0.24$$

**Solution:**  
The probability that the chosen integer is divisible by 6 or 8 is **$\frac{24}{100}$** (or **$24\%$**).

---

### 📊 Venn Diagram Representation

This graph shows the interaction between the two event sets within the sample space:

```
+---------------------------------------------+ S
| Sample Space (Total numbers = 100)          |
|                                             |
|      +---------------+     +---------------+        |
|     /  Event A       \   /  Event B       \       |
|    /  (Divisible)     \_/   (Divisible)    \      |
|   /      by 6    \    / \      by 8     \     |
|  |                |  |   |               |    |
|  |     12 items   |  | 4 |    8 items    |    |
|  |                |  |   |               |    |
|   \              / \_/ \_/              /     |
|    \            /   \   /              /      |
|     +---------------+     +---------------+        |
|                                             |
|               Remaining: 76 items           |
+---------------------------------------------+
```

# Probability Theory: Conditional Probability and Advanced Principles

---

## 1. Concept: Conditional Probability

### Simple Meaning
**Conditional Probability** measures the likelihood of an event occurring, given that another event has already happened. Instead of looking at the entire original sample space, we shrink our focus down exclusively to the outcomes where the known condition is true. 

### Formula
The conditional probability of event $E$ given that event $F$ has occurred is denoted as $P(E\vert{}F)$ and is calculated as:
$$P(E\vert{}F) = \frac{P(E \cap F)}{P(F)}; \quad \text{provided } P(F) \neq 0$$

---

### 📝 Step-by-Step Practical Problem

**Problem Statement:**  
A black and a red die are rolled. What is the conditional probability of obtaining a sum greater than 9 given that the black die resulted in a 5?

**Step-by-Step Calculation & Explanation:**

1. **Find the Condition Event ($F$):**  
   We are given that the black die shows a 5. The red die can show any number from 1 to 6.  
   * Outcomes for $F$: $\{(5,1), (5,2), (5,3), (5,4), (5,5), (5,6)\}$
   * Total number of favorable outcomes for $F$: $n(F) = 6$
   * Total possible outcomes when rolling two dice: $n(S) = 6 \times 6 = 36$
   * Probability of $F$: 
     $$P(F) = \frac{6}{36}$$

2. **Find the Target Overlap Event ($E \cap F$):**  
   We need the outcomes where the black die is a 5 **and** the sum of both dice is strictly greater than 9 (meaning a sum of 10, 11, or 12).  
   * Check $F$'s outcomes:
     * $5 + 1 = 6$ (No)
     * $5 + 2 = 7$ (No)
     * $5 + 3 = 8$ (No)
     * $5 + 4 = 9$ (No, must be *greater* than 9)
     * $5 + 5 = 10$ (Yes!)
     * $5 + 6 = 11$ (Yes!)
   * Shared elements: $\{(5,5), (5,6)\}$
   * Total number of elements: $n(E \cap F) = 2$
   * Probability of overlap: 
     $$P(E \cap F) = \frac{2}{36}$$

3. **Compute the Conditional Probability:**  
   Apply the formula:
   $$P(E\vert{}F) = \frac{P(E \cap F)}{P(F)} = \frac{\frac{2}{36}}{\frac{6}{36}} = \frac{2}{6} = \frac{1}{3}$$

**Solution:**  
The conditional probability is **$\frac{1}{3}$** (or roughly **$33.3\%$**).

### 📊 Reduced Sample Space Graph Diagram

Instead of searching through all 36 options, conditional probability focuses purely on the condition row:

```
Black Die = 5 (Our entire universe now)
+-------------------------------------------------------+
|  (5,1)  |  (5,2)  |  (5,3)  |  (5,4)  |  (5,5)* |  (5,6)* |
+-------------------------------------------------------+
                                         \_____ _____/
                                               V
                                     Sum > 9 (2 out of 6)

```

---

## 2. Properties of Conditional Probability

Conditional probability follows algebraic rules similar to standard probability, adapted to a given background context ($F$):

| Property Rule | Simple Meaning |
| --- | --- |
| **1. $P(E\Vert{}E) = P(S\Vert{}E) = 1$** | The probability of an event happening, given that it already happened, is 100%. |
| **2. $P((A \cup B)\Vert{}F) = P(A\Vert{}F) + P(B\Vert{}F) - P((A \cap B)\Vert{}F)$** | The addition rule holds true when evaluating everything under a condition $F$. |
| **3. $P(A^C\Vert{}F) = 1 - P(A\Vert{}F)$** | The probability of an event *not* happening under condition $F$ is 1 minus the probability that it does happen. |

---

## 3. Advanced Problem: System of Equations with Conditional Complements

### 📝 Step-by-Step Algebraic Problem

**Problem Statement:**

A problem is given to two students: A and B.

* The probability that A can solve it given that B can solve it is $\frac{3}{7}$.
* The probability that B can solve it given that A cannot solve it is $\frac{1}{7}$.
* The probability that B can solve it is $\frac{1}{10}$.

What is the probability that A can solve it ($P(A)$)?

**Step-by-Step Calculation & Explanation:**

1. **Translate the Word Problem into Notation:**
* $P(B) = \frac{1}{10} \implies P(B^C) = 1 - \frac{1}{10} = \frac{9}{10}$
* $P(A\vert{}B) = \frac{3}{7}$
* $P(B\vert{}A^C) = \frac{1}{7}$


2. **Expand the Second Condition Statement:**
Using the definition of conditional probability:

$$P(B\vert{}A^C) = \frac{P(B \cap A^C)}{P(A^C)} = \frac{1}{7}$$


Recall that $P(B \cap A^C)$ means "elements in B that are not in A", which can be calculated as $P(B) - P(A \cap B)$.

$$\frac{P(B) - P(A \cap B)}{1 - P(A)} = \frac{1}{7} \quad \text{--- (Equation 1)}$$


3. **Expand the First Condition Statement to find $P(A \cap B)$:**
$$P(A\vert{}B) = \frac{P(A \cap B)}{P(B)} = \frac{3}{7}$$



Substitute $P(B) = \frac{1}{10}$:

$$\frac{P(A \cap B)}{\frac{1}{10}} = \frac{3}{7} \implies P(A \cap B) = \frac{3}{7} \times \frac{1}{10} = \frac{3}{70}$$


4. **Substitute values back into Equation 1 to isolate $P(A)$:**
$$\frac{\frac{1}{10} - \frac{3}{70}}{1 - P(A)} = \frac{1}{7}$$


Simplify the top fraction by finding a common denominator (70):

$$\frac{1}{10} - \frac{3}{70} = \frac{7}{70} - \frac{3}{70} = \frac{4}{70}$$


Now substitute this back:

$$\frac{\frac{4}{70}}{1 - P(A)} = \frac{1}{7}$$


Cross-multiply to clear fractions:

$$7 \times \frac{4}{70} = 1 - P(A)$$


$$\frac{28}{70} = 1 - P(A)$$


Reduce $\frac{28}{70}$ by dividing the numerator and denominator by 14:

$$\frac{2}{5} = 1 - P(A)$$


$$P(A) = 1 - \frac{2}{5} = \frac{3}{5}$$



**Solution:**

The probability that student A can solve the problem is **$\frac{3}{5}$** (or **$0.6$ / $60\%$**).

---

### 📊 Probability Breakdown Graph

Visual mapping of how the total workspace sample space values are split across the variables:

```text
Total Universal Area
+-------------------------------------------------------+
|  Student A Area                    Student B Area     |
|  +-----------------------+        +------------+      |
|  | Exclusive to A        | Share  | Exclusive  |      |
|  |                       |  AnB   | to B       |      |
|  |         39/70         |  3/70  |    4/70    |      |
|  +-----------------------+        +------------+      |
|                                                       |
|   Outside Area (Neither can solve): 24/70             |
+-------------------------------------------------------+
Summary Totals Verified:
* P(B) = 3/70 + 4/70 = 7/70 = 1/10
* P(A) = 39/70 + 3/70 = 42/70 = 3/5

```





# Probability Theory: Multiplication Theorem & Sequential Events

---

## 1. Concept Name: Multiplication Theorem on Probability

### Simple Meaning
The **Multiplication Theorem** calculates the probability of multiple dependent events happening one after another (simultaneously or successively). Instead of assuming the conditions remain static, it adjusts the probability of subsequent stages based on what already happened in the previous stages.

### Mathematical Formulations
* **For Two Successive Events ($E$ and $F$):**
  $$P(E \cap F) = P(E) \cdot P(F \mid E) = P(F) \cdot P(E \mid F)$$

* **For Three Successive Events ($E$, $F$, and $G$):**
  $$P(E \cap F \cap G) = P(E) \cdot P(F \mid E) \cdot P(G \mid E \cap F)$$

---

## 2. 📝 Problem 1: Dependent Sequential Card Selection

### Problem Statement
Three cards are drawn successively **without replacement** from a standard well-shuffled deck of 52 cards. What is the probability that the first two cards drawn are kings and the third card drawn is a queen?

### Step-by-Step Explanation & Calculation

1. **Define the Individual Stage Events:**
   * $E_1$: Event that the 1st card drawn is a King.
   * $E_2$: Event that the 2nd card drawn is a King.
   * $E_3$: Event that the 3rd card drawn is a Queen.

2. **Step 1: Calculate the Probability of the First King ($P(E_1)$):**
   * Total Kings in a deck = 4
   * Total cards in the deck = 52
   $$P(E_1) = \frac{4}{52}$$

3. **Step 2: Calculate the Probability of the Second King given the First King ($P(E_2 \mid E_1)$):**
   * Since there is **no replacement**, the total pool shrinks.
   * Remaining Kings = $4 - 1 = 3$
   * Remaining total cards = $52 - 1 = 51$
   $$P(E_2 \mid E_1) = \frac{3}{51}$$

4. **Step 3: Calculate the Probability of the Third Card being a Queen ($P(E_3 \mid E_1 \cap E_2)$):**
   * Total Queens in a deck remains untouched = 4
   * Remaining total cards = $51 - 1 = 50$
   $$P(E_3 \mid E_1 \cap E_2) = \frac{4}{50}$$

5. **Step 4: Apply the Multiplication Theorem for Three Events:**
   $$P(E_1 \cap E_2 \cap E_3) = P(E_1) \cdot P(E_2 \mid E_1) \cdot P(E_3 \mid E_1 \cap E_2)$$
   $$P(E_1 \cap E_2 \cap E_3) = \frac{4}{52} \times \frac{3}{51} \times \frac{4}{50}$$

6. **Step 5: Simplify the Fraction Product:**
   * Simplify $\frac{4}{52} \rightarrow \frac{1}{13}$
   * Simplify $\frac{3}{51} \rightarrow \frac{1}{17}$
   * Simplify $\frac{4}{50} \rightarrow \frac{2}{25}$
   $$\text{Final Fraction} = \frac{1 \times 1 \times 2}{13 \times 17 \times 25} = \frac{2}{5525}$$

### Final Solution
The probability is **$\frac{2}{5525}$** (or approximately **$0.000362$ / $0.036\%$**).

---

## 3. 📝 Problem 2: System of Advanced Conditional Equations

### Problem Statement
Given the conditional probability system below, solve for the unknown parameter $P(A)$:
* $P(A \mid B) = \frac{3}{7}$
* $P(B \mid A') = \frac{1}{7}$
* $P(B) = \frac{1}{10}$

### Step-by-Step Explanation & Calculation

1. **Deconstruct Equation 1 using the Conditional Identity:**
   $$P(A \mid B) = \frac{P(A \cap B)}{P(B)} = \frac{3}{7}$$
   Substitute $P(B) = \frac{1}{10}$:
   $$\frac{P(A \cap B)}{\frac{1}{10}} = \frac{3}{7} \implies P(A \cap B) = \frac{3}{7} \times \frac{1}{10} = \frac{3}{70}$$

2. **Deconstruct Equation 2 using Complements:**
   Notice that $P(B \cap A') = P(B) - P(A \cap B)$ (this represents elements purely exclusive to $B$, excluding $A$).
   $$P(B \mid A') = \frac{P(B \cap A')}{P(A')} = \frac{P(B) - P(A \cap B)}{1 - P(A)} = \frac{1}{7}$$

3. **Substitute Known Values into Equation 2:**
   Substitute $P(B) = \frac{1}{10}$ and $P(A \cap B) = \frac{3}{70}$:
   $$\frac{\frac{1}{10} - \frac{3}{70}}{1 - P(A)} = \frac{1}{7}$$

4. **Simplify the Numerator:**
   Find a common denominator of 70:
   $$\frac{1}{10} - \frac{3}{70} = \frac{7}{70} - \frac{3}{70} = \frac{4}{70}$$

5. **Solve the Resulting Proportional Equation:**
   $$\frac{\frac{4}{70}}{1 - P(A)} = \frac{1}{7} \implies \frac{4}{70} \times \frac{7}{1} = 1 - P(A)$$
   $$\frac{4 \times 7}{70} = 1 - P(A) \implies \frac{28}{70} = 1 - P(A)$$
   Divide by 14 to reduce the fraction:
   $$\frac{4}{10} = \frac{2}{5} = 1 - P(A)$$
   $$P(A) = 1 - \frac{2}{5} = \frac{3}{5}$$

### Final Solution
$$P(A) = \frac{3}{5}$$

---

## 4. 📊 Probability Distribution Graphs

### A. Dependent Selection Tree Diagram (Problem 1)
```text
                  [ Deck of 52 Cards ]
                           |
                           v Draw 1 (King)
                       [ 4 / 52 ]
                           |
                           v Draw 2 (King given 1st King)
                       [ 3 / 51 ]
                           |
                           v Draw 3 (Queen given 2 Kings)
                       [ 4 / 50 ]

```

### B. Venn Diagram Mapping Space (Problem 2)

The universal space layout when mapped using fractions over a common base value denominator of 70:

```text
+-------------------------------------------------------+ U
| Universal Workspace                                   |
|                                                       |
|       +-------------------+   +-------------------+   |
|      /  Set A             \ /  Set B             \  |
|     /                      X                      \ |
|    |   Exclusive to A     | |    Exclusive to B    | |
|    |                      | |     P(B ∩ A')        | |
|    |      39 / 70         | |                      | |
|    |                      |3|        4 / 70        | |
|     \                     |7|                     /  |
|      \                    |0|                    /   |
|       +-------------------+   +-------------------+   |
|                            \ /                        |
|                             V                         |
|                       Intersection                    |
|                         (3 / 70)                      |
+-------------------------------------------------------+

```


# Probability Theory: Independent Events & Total Probability

---

## 1. Concept Name: Independent Events

### Simple Meaning
Two events are **independent** if the occurrence or non-occurrence of one event has absolutely no effect on the chance of the other event happening. In other words, knowing that one event occurred gives you zero new information about the other.

### Mathematical Condition
Two events $E$ and $F$ are independent if and only if:
$$P(E \cap F) = P(E) \cdot P(F)$$

**Alternative Form via Conditional Probability:**
$$P(E \mid F) = P(E); \quad \text{where } P(F) \neq 0$$
$$P(F \mid E) = P(F); \quad \text{where } P(E) \neq 0$$
*(This literally says: The probability of $E$ given that $F$ happened is still just the baseline probability of $E$.)*

---

### 📝 Independent Events Practice Problem

**Problem:** A fair coin is tossed and a fair six-sided die is rolled. Let event $E$ be "getting heads on the coin" and event $F$ be "rolling a 6 on the die". Determine if these two events are mathematically independent.

**Step-by-Step Calculation:**
1. **Find individual probabilities:**
   * Coin outcomes: $\{\text{Heads}, \text{Tails}\} \implies P(E) = \frac{1}{2}$
   * Die outcomes: $\{1, 2, 3, 4, 5, 6\} \implies P(F) = \frac{1}{6}$
2. **Find the probability of both happening together ($P(E \cap F)$):**
   * Total shared outcome combinations: $2 \times 6 = 12$ total outcomes.
   * Only 1 combination is exactly $(\text{Heads}, 6) \implies P(E \cap F) = \frac{1}{12}$
3. **Verify via multiplication rule:**
   $$P(E) \cdot P(F) = \frac{1}{2} \times \frac{1}{6} = \frac{1}{12}$$
4. **Compare values:** Since $P(E \cap F) = P(E) \cdot P(F)$, the events are **Independent**.

---

## 2. Concept Name: Partition of a Sample Space

### Simple Meaning
A **partition** means cutting up the entire Sample Space ($S$) into a group of sub-events $\{E_1, E_2, \dots, E_n\}$ like pieces of a puzzle. To be a valid partition, the sub-events must follow two strict rules:
1. **Exhaustive:** Together, all the pieces must add up to cover the entire space ($E_1 \cup E_2 \cup \dots \cup E_n = S$). No gaps allowed.
2. **Mutually Exclusive:** None of the pieces can overlap with each other ($E_i \cap E_j = \phi$ for any $i \neq j$). 

---

## 3. Concept Name: Theorem of Total Probability

### Simple Meaning
If an event $A$ can happen through several different pathways (where each pathway is a part of a sample space partition), the total probability of $A$ is found by calculating the probability of going down each specific path, and adding all those path probabilities together.

### Mathematical Formula
$$P(A) = P(E_1)P(A \mid E_1) + P(E_2)P(A \mid E_2) + \dots + P(E_n)P(A \mid E_n) = \sum_{j=1}^{n} P(E_j)P(A \mid E_j)$$

### Mathematical Derivation
1. Start with the fact that $A$ is entirely inside the sample space: $P(A) = P(A \cap S)$.
2. Substitute the partition components for $S$: $P(A) = P(A \cap (E_1 \cup E_2 \cup \dots \cup E_n))$.
3. Distribute $A$ across the union: $P(A) = P((A \cap E_1) \cup (A \cap E_2) \cup \dots \cup (A \cap E_n))$.
4. Convert to a summation of independent pathways: $\sum_{i=1}^{n} P(A \cap E_i)$.
5. Apply the conditional probability multiplication rule ($P(A \cap E_i) = P(E_i)P(A \mid E_i)$) to get the final form.

---

### 📝 Total Probability Worked Example

**Problem Statement:**  
A person has undertaken a construction job. The probabilities are:
* **$0.6$** that there will be a strike.
* **$0.8$** that the construction job will be completed on time if there is **no strike**.
* **$0.3$** that the construction work will be completed on time if there **is a strike**.

Determine the probability that the construction job will be completed on time.

### Step-by-Step Calculation & Explanation:

1. **Define the Events:**
   * Let $A$ = Required probability that the job is completed on time.
   * Let $E_1$ = There is a strike.
   * Let $E_1'$ = There is no strike (the complement event).

2. **Extract Given Probabilities:**
   * Probability of strike: $P(E_1) = 0.6$
   * Probability of no strike: $P(E_1') = 1 - 0.6 = 0.4$
   * Probability of on-time completion given a strike: $P(A \mid E_1) = 0.3$
   * Probability of on-time completion given no strike: $P(A \mid E_1') = 0.8$

3. **Set up the Total Probability Equation:**
   $$P(A) = P(E_1) \cdot P(A \mid E_1) + P(E_1') \cdot P(A \mid E_1')$$

4. **Substitute and Calculate:**
   * Path 1 (Completion during strike): $0.6 \times 0.3 = 0.18$
   * Path 2 (Completion without strike): $0.4 \times 0.8 = 0.32$
   * Sum both pathways: 
     $$P(A) = 0.18 + 0.32 = 0.50$$

**Solution:**  
The total probability that the construction job will be completed on time is **$0.50$** (or **$50\%$**).

---

## 4. 📊 Sample Space Partition Diagram

The text-graph below visualizes how the target event $A$ cuts across different parts of a partitioned sample space $S$:

```text
+-------------------------------------------------------+ S
| Sample Space Partition Map                            |
|                                                       |
|   +-----------+-----------+-----------+-----------+   |
|   |    E1     |    E2     |    E3     |    En     |   |
|   |           |           |   ///     |           |   |
|   |           |        +--+---\\\     |           |   |
|   |           |       /   |    \\\    |           |   |
|   |           |      |  Event A \\\   |           |   |
|   |           |       \   |    ///    |           |   |
|   |           |        +--+---///     |           |   |
|   |           |           |   \\\     |           |   |
|   +-----------+-----------+-----------+-----------+   |
|                                                       |
+-------------------------------------------------------+
Note: The total area of circle A is found by summing its intersections
      with all separate areas (like the shaded region inside E3).
```      