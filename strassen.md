# Strassen's Matrix Multiplication

## 1. Normal Matrix Multiplication lo em jaruguthundi?

**Input:** Rendu matrices $A$ mariyu $B$ (Size: $n \times n$)

### Basic Logic
Oka output cell value ravali ante:
- Row lo unde $n$ values ni...
- Column lo unde $n$ values tho multiply chesi, add cheyali

### Calculation
- Prati cell ki $n$ multiplications kavali
- Total cells $n^2$ untayi
- **Total Multiplications** = $n^2 \times n = n^3$

👉 **Time Complexity:** $O(n^3)$ _(Idi mana school method. Pani jaruguthundi kani time ekkuva paduthundi)_

---

## 2. Mari Strassen's Matrix Multiplication enti?

Strassen simple ga **"Divide and Conquer"** strategy vadathadu.

### Core Idea
- Oka pedda matrix ni 4 chinna sub-matrices ga divide chesthadu
- $A \rightarrow A_{11}, A_{12}, A_{21}, A_{22}$
- $B \rightarrow B_{11}, B_{12}, B_{21}, B_{22}$

---

## 3. Normal Method lo Problem enti?

Mamuluga 2x2 matrix ni multiply cheyalante manaki **8 Multiplications** avasaram:

$$C_{11} = A_{11}B_{11} + A_{12}B_{21}$$
$$C_{12} = A_{11}B_{12} + A_{12}B_{22}$$
$$C_{21} = A_{21}B_{11} + A_{22}B_{21}$$
$$C_{22} = A_{21}B_{12} + A_{22}B_{22}$$

_(Total 4 equations, prati daanilo 2 multiplications untayi)_

👉 **Total: 8 Multiplications** ❌

---

## 4. Strassen Magic ekkada undi? ✨

Ikkade Strassen oka dialogue vesadu:
> "Enduku ra 8 multiplications? 7 chaalu, nenu manage chestha!" 😏

Strassen 7 intermediate products ($P_1$ nunchi $P_7$) create chesthadu.

**Key Insight:**
- Direct ga multiply cheyakunda
- $A$ & $B$ sub-matrices ni add/subtract chesi
- Aa values ni multiply chesthadu

Trick To Remember: https://youtu.be/HO7tEhH_Dlg

## Strassen formulas:
$$
\begin{aligned}
P_1 &= A_{11}(B_{12} - B_{22}) \\
P_2 &= B_{22}(A_{11} + A_{12}) \\
P_3 &= B_{11}(A_{21} + A_{22}) \\
P_4 &= A_{22}(B_{21} - B_{11}) \\
P_5 &= (A_{11} + A_{22})(B_{11} + B_{22}) \\
P_6 &= (A_{12} - A_{22})(B_{21} + B_{22}) \\
P_7 &= (A_{11} - A_{21})(B_{11} + B_{12})
\end{aligned}
$$
### Final Combination
$$
\begin{aligned}
C_{11} &= P_5 + P_4 - P_2 + P_6 \\
C_{12} &= P_1 + P_2 \\
C_{21} &= P_3 + P_4 \\
C_{22} &= P_5 + P_1 - P_3 - P_7
\end{aligned}
$$



**Result:** 8 Multiplications → 7 Multiplications ✅

### Twist enti ante:
- Additions perigayi ⬆️
- Kani computer ki Addition chala cheap, **Multiplication eh costly**
- So, multiplications taggithe speed periginatte! 🚀

---

## 5. Asalu Strassen em skip chesthadu?

| ❌ Skip | ✅ Do |
|---------|------|
| Direct row-column multiplication | Smart ga regroup chesi, prathi level lo okka multiplication avoid chesthadu |

**Simple ga:**
- Multiplication count 📉
- Addition count 📈
- **Overall performance jump avuthundi!**

---

## 6. Recursion lo em avuthundhi?

Ee logic ni **recursive** ga (malli malli) apply chestham.

- Prathi step lo matrix size sagam ($n/2$) avthundi
- Multiplications 7/8 th part available avuthayi

### Recurrence Relation
$$T(n) = 7T(n/2) + O(n^2)$$

---

## 7. Time Complexity Comparison 📊

| Method | Complexity |
|--------|-----------|
| **Normal Method** | $O(n^3)$ |
| **Strassen Method** | $O(n^{\log_2 7}) \approx O(n^{2.807})$ |

🔥 **Difference:** $n$ value peddaga unnapudu, ee difference chala huge ga untundi!

---

## 8. Space Complexity (Chinna Disadvantage) ⚠️

| Method | Space |
|--------|-------|
| **Normal** | $O(1)$ - Extra space peddaga akkarledu |
| **Strassen** | $O(n^2)$ - Sub-matrices store + recursion stack |

**Tradeoff:** Speed kavali ante space sacrifice cheyali ⚖️

---

## 9. Logic Summary (Okka Mukka Lo) 🧠

**Multiplication** ante CPU ki baruvu. **Addition** ante CPU ki aata.

**Strassen em chesadante:**
> "Costly ga unde oka Multiplication ni lepesi, cheap ga unde konni Additions ni add chesadu."

👉 **Less Multiplications = Faster Algorithm** 🚀

---

## 10. Practical Reality Check 😈

| Scenario | Method | Why? |
|----------|--------|------|
| **Small Matrices** | Normal Method | Overhead ekkuva |
| **Large Matrices** | Strassen ✅ | Super fast |
| **Real World** | Hybrid Approach | NumPy-style: Small → Normal, Large → Strassen |

---

## One-Line Intuition 💡

Strassen be like:
> "Oka multiplication ni teesyadam kosam, ekkuva additions ichina parledhu!" 😎

---
Example:
## Multiply these 2 matrices using Strassen's Method:
$$
A =
\begin{bmatrix}
1 & 2 \\
3 & 4
\end{bmatrix},
\quad
B =
\begin{bmatrix}
5 & 6 \\
7 & 8
\end{bmatrix}
$$
**Step 1:** Calculate $P_1$ to $P_7$:
$$P_1 = 1(6 - 8) = 1(-2) = -2$$
$$P_2 = 8(1 + 2) = 8 \times 3 = 24$$
$$P_3 = 5(3 + 4) = 5 \times 7 = 35$$
$$P_4 = 4(7 - 5) = 4 \times 2 = 8$$
$$P_5 = (1 + 4)(5 + 8) = 5 \times 13 = 65$$
$$P_6 = (2 - 4)(7 + 8) = (-2) \times 15 = -30$$
$$P_7 = (1 - 3)(5 + 6) = (-2) \times 11 = -22$$
**Step 2:** Calculate $C_{11}$, $C_{12}$, $C_{21}$, $C_{22}$:
$$C_{11} = P_5 + P_4 - P_2 + P_6 = 65 + 8 - 24 - 30 = 19$$
$$C_{12} = P_1 + P_2 = -2 + 24 = 22$$
$$C_{21} = P_3 + P_4 = 35 + 8 = 43$$
$$C_{22} = P_5 + P_1 - P_3 - P_7 = 65 - 2 - 35 + 22 = 50$$
**Final Result:**
$$
C =
\begin{bmatrix}
19 & 22 \\
43 & 50
\end{bmatrix}
$$


Python Implementation:
```python
import numpy as np

def split(matrix):
    """
    Matrix ni 4 quadrants ga divide chesthundi.
    Like cutting a cake into 4 pieces! 🍰
    """
    row, col = matrix.shape
    row2, col2 = row // 2, col // 2
    return (matrix[:row2, :col2], matrix[:row2, col2:],
            matrix[row2:, :col2], matrix[row2:, col2:])

def strassen(A, B):
    """
    Main Strassen Function.
    Recursion use chesi 7 products calculate chesthundi.
    """
    # Step 1: Base Case (Recursion aapadaniki)
    # Matrix size 1 unte, just direct multiply chesey.
    if len(A) == 1:
        return A * B

    # Step 2: Divide (Matrix ni 4 parts ga vidagodatham)
    # A -> a11, a12, a21, a22
    # B -> b11, b12, b21, b22
    a11, a12, a21, a22 = split(A)
    b11, b12, b21, b22 = split(B)

    # Step 3: The 7 Magic Products (P1 to P7) ✨
    # Ikkade asalaina Strassen intelligence undi.
    
    # p1 = a11 * (b12 - b22)
    p1 = strassen(a11, b12 - b22)
    
    # p2 = (a11 + a12) * b22
    p2 = strassen(a11 + a12, b22)
    
    # p3 = (a21 + a22) * b11
    p3 = strassen(a21 + a22, b11)
    
    # p4 = a22 * (b21 - b11)
    p4 = strassen(a22, b21 - b11)
    
    # p5 = (a11 + a22) * (b11 + b22) -> Idi main diagonal sum product
    p5 = strassen(a11 + a22, b11 + b22)
    
    # p6 = (a12 - a22) * (b21 + b22)
    p6 = strassen(a12 - a22, b21 + b22)
    
    # p7 = (a11 - a21) * (b11 + b12)
    p7 = strassen(a11 - a21, b11 + b12)

    # Step 4: Conquer (Recombine P values to get C)
    # Formulas konchem complex ga untayi, but simple math.
    
    # c11 = p5 + p4 - p2 + p6
    c11 = p5 + p4 - p2 + p6
    
    # c12 = p1 + p2
    c12 = p1 + p2
    
    # c21 = p3 + p4
    c21 = p3 + p4
    
    # c22 = p5 + p1 - p3 - p7
    c22 = p5 + p1 - p3 - p7

    # Step 5: Merge (4 parts ni malli oka matrix la join cheyadam)
    # numpy.vstack and hstack vadutham
    top = np.hstack((c11, c12))
    bottom = np.hstack((c21, c22))
    
    return np.vstack((top, bottom))

# --- Testing the Cinema ---

# Rendu 4x4 Matrices teesukundam
A = np.array([[1, 2, 3, 4],
              [5, 6, 7, 8],
              [9, 1, 2, 3],
              [4, 5, 6, 7]])

B = np.array([[8, 7, 6, 5],
              [4, 3, 2, 1],
              [1, 9, 8, 7],
              [6, 5, 4, 3]])

print("Strassen's Result:\n")
result = strassen(A, B)
print(result)

# Verification check (Direct numpy multiplication tho compare cheddam)
print("\n Verification (Numpy Standard):\n")
print(np.dot(A, B))
```

<img width="366" height="319" alt="output" src="https://github.com/user-attachments/assets/f0d64d4e-adcb-4ab1-9dc1-ef343b7f3038" />
