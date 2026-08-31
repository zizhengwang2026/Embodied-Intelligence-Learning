# Lecture 32 · sklearn Linear Regression / The XOR Problem / Parsing OX*R Data

> **Lecture info**
> - Date: 2026-09-14 (Mon)
> - Lecture #: 32 (Study Plan Day 32, P8)
> - Plan ref: `study-plan-60d.md` → **P8**, episodes **129–131**
> - Goal: Run a linear regression with sklearn by hand; then hit the **XOR problem** — no single line can separate it — and understand **why we need nonlinearity (neural networks)**. This is the leap from “linear models” to “deep learning”.

---

## 0. One-line summary

> **Linear regression can only draw one straight line (or hyperplane); in XOR the two classes sit on *diagonals*, so no single line can split them — that’s not bad data, it’s insufficient model capacity.** The fix is adding **nonlinearity** (activations / multiple layers / kernels), which is exactly why neural networks show up.

---

## 1. Core concepts (eps 129–131)

### 1.1 129 sklearn linear regression demo
- Three lines: `model = LinearRegression()` → `model.fit(X, y)` → `model.predict(X_new)`.
- Form: `y = w₁x₁ + w₂x₂ + ... + b`; geometrically **a line / a plane**.
- sklearn wraps Day 31’s “MSE + gradient descent” for you (it actually solves the least-squares problem).

### 1.2 130 A linear model cannot solve XOR
- XOR truth table: `(0,0)→0`, `(0,1)→1`, `(1,0)→1`, `(1,1)→0`.
- Plotted in 2D: **the two 0s are on one diagonal, the two 1s on the other** — no straight line can separate 0 from 1.
- Conclusion: **not linearly separable**.

### 1.3 131 Parsing the OX*R data
- Load the XOR data (often with noise / continuous values) and confirm a linear model scores about chance (~50%) on it.
- Leads to: you need a **nonlinear transform** (bend the space) to make the data separable.

---

## 2. Principles (grab these)

1. **A linear model’s ceiling = cut the space in half with one line.**
2. **Not linearly separable ≠ bad data; it means the model lacks expressive power.**
3. **Nonlinearity = capacity**: activations, stacked layers, or lifting to higher dimensions (kernel trick).

---

## 3. One diagram: why no line can split XOR

```mermaid
flowchart LR
    subgraph GRID[XOR plane]
        A[(0,0) → 0]
        B[(1,1) → 0]
        C[(0,1) → 1]
        D[(1,0) → 1]
    end
    GRID --> LINE[one straight line?]
    LINE --> NO[impossible: diagonals share class]
    NO --> FIX[add nonlinearity<br>layers / activations]
    FIX --> OK[now separable]
```

---

## 4. Today’s steps

1. **Watch 129–131** (1.0–1.5×), focus on 130 (no matter how you draw it, the line fails).
2. **Run sklearn linear regression**: generate `y = 2x + 1 + noise`, check whether fitted w/b land near 2/1.
3. **Apply the same model to XOR data**: print accuracy, confirm ≈50%.
4. **Name two ways to make it separable** (hint: hidden layer + activation / hand-built cross feature x₁x₂).
5. **Mirror test (3 min):** *“Geometrically, linear regression is ___; why XOR can’t be split ___; linear inseparability indicates whose fault ___; how to fix ___.”*

> ✅ **Done today when:** linear regression runs + you verified it fails on XOR + you can name the fix + mirror test passed.

---

## 5. Common pitfalls

| # | Myth | Truth |
|---|---|---|
| 1 | Can’t separate = bad data | It’s insufficient model capacity, not bad data |
| 2 | Linear regression handles only 1-D | It handles many dims — geometrically a hyperplane |
| 3 | 50% accuracy means buggy code | Random guessing on binary = 50%; that *is* the symptom |
| 4 | Stack more linear layers to fix it | Linear∘linear is still linear — you need a **nonlinear activation** |

---

## 6. DEA cross-link (light, not main thread)

- The DEA “voltage → displacement” curve has a **hysteresis loop** (loading and unloading follow different paths) — a classic **nonlinear + memory** relation. A linear model will fail here for the same reason as XOR: **not bad data, too simple a model**.
- That is the hard reason soft robotics genuinely benefits from **neural / data-driven models** — not because it’s fashionable.

---

## 7. Next / checkpoint

- **Checkpoint passed =** linear regression runs + XOR shown non-separable + mirror test.
- **Next (Day 33):** feature engineering + assembling complex neural nets, MNIST dataset intro & loading (132–134).

---

### References (not required today)
- Episodes 129–131 (B站《黑马程序员 · 具身智能》).
- Reuse: Day 31 (MSE / gradient descent — sklearn wraps them).

*This lecture strictly follows 《60-Day Plan》 Day 32 (P8): 129–131. Zero military content.*
