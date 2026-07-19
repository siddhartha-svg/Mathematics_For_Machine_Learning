## **Orthogonal Vectors**

In an inner product space $(V, \langle \cdot, \cdot \rangle)$, two vectors $v_i$ and $v_j$ are said to be **orthogonal** if

$$\langle v_i, v_j \rangle = 0$$

For example, vectors $(1,0,0)$ and $(0,1,0)$ are orthogonal in $\mathbb{R}^3(\mathbb{R})$ with the inner product taken as the usual dot product of vectors.


## **Orthogonal Complement**

If $W \subseteq V$, where $V$ is an inner product space, then the **orthogonal complement** of $W$, denoted by $W^\perp$, is the set of vectors in $V$ that are orthogonal to every element of $W$:

$$W^\perp = \{v \in V \mid v \perp w \quad \forall w \in W\}$$

---

### **Example**

In $\mathbb{R}^3$ with the inner product taken as the usual dot product of vectors in $\mathbb{R}^3$, if we take:

$$W = L[(1, 0, 0)] = \{(x_1, x_2, x_3) \in \mathbb{R}^3 \mid x_2 = 0 = x_3\}$$

then,

$$W^\perp = L[(0, 1, 0), (0, 0, 1)] = \{(x_1, x_2, x_3) \in \mathbb{R}^3 \mid x_1 = 0\}$$


## **Example:**

Let $V = \mathbb{R}^3(\mathbb{R})$, with $\langle \cdot, \cdot \rangle = \text{usual dot product}$.

If we have the set:


$$W = \{(1, 0, 0), (0, 1, 0)\}$$

Then its orthogonal complement is the linear span:


$$W^\perp = L\{(0, 0, 1)\}$$

---

### **Important Property:**

> $W^\perp$ is always a **subspace** of $V$.

---

### **Geometric Representation**

Geometrically, in 3D space ($\mathbb{R}^3$), the set $W$ spans the horizontal $xy$-plane. Its orthogonal complement, $W^\perp$, represents all vectors perpendicular to that plane, which forms the vertical $z$-axis.

```text
               z (W┴ : z-axis)
               ▲
               │
               │
               │   ╱ y
               │ ╱
               ┼──────────► x
             ╱ │
           ╱   │
  (W : xy-plane)

```



## **Important Remarks**

1. There is no requirement on $W$ to be a subspace of $V$. However, $W^\perp$ is always a subspace of $V$.
2. If $W$ is also a subspace of $V$, then

$$V = W \oplus W^\perp$$


Means, every vector $v \in V$ can be written uniquely as

$$v = v_W + v_{W^\perp}$$



where $v_W \in W$ and $v_{W^\perp} \in W^\perp$

---

### **Geometric Interpretation**

This is known as the **orthogonal decomposition theorem**. It means you can break down any vector into a component that lies perfectly inside the subspace $W$ and a component completely perpendicular to it.

```text
          v_W┴  (Component perpendicular to W)
           ▲       _ ──► v (Original vector)
           │     ╱   
           │   ╱     
           │ ╱       
           ┼──────────► v_W (Component in W)
         ╱
       ╱  
     W (Subspace plane)

```

