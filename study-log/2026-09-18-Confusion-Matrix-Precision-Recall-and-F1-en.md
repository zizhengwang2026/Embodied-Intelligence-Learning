# Lecture 36 · Confusion Matrix / Precision / Recall / F1

> **Lecture info**
> - Date: 2026-09-18 (Fri)
> - Lecture #: 36 (Study Plan Day 36, P8)
> - Plan ref: `study-plan-60d.md` → **P8**, episodes **141–142**
> - Goal: Learn evaluation tools **far more trustworthy than accuracy** — the confusion matrix (where the errors are) plus precision / recall / F1. Mandatory for judging whether a model is actually any good (you’ll stare at these every day when training YOLO).

---

## 0. One-line summary

> **Accuracy lies (with imbalanced classes, always guessing the majority still scores high); the confusion matrix shows *what got confused with what*; Precision = how many reported items are real, Recall = how many real items were found, F1 = their harmonic mean.** In detection/grasping, **misses and false alarms rarely cost the same** — pick the metric that matches your scenario.

---

## 1. Core concepts (eps 141–142)

### 1.1 141 Confusion matrix
For binary classification, four cells:

|  | predicted “positive” | predicted “negative” |
|---|---|---|
| **actually positive** | **TP** (caught it) | **FN** (missed) |
| **actually negative** | **FP** (false alarm) | **TN** (correctly rejected) |

- Why it matters: **at a glance you see whether 3 got read as 8** — in multi-class it’s a “map of mistakes”.

### 1.2 142 Precision / Recall / F1
- **Precision = TP / (TP + FP)**: of everything I reported, how much is real → worries about **false alarms**.
- **Recall = TP / (TP + FN)**: of everything real, how much did I find → worries about **misses**.
- **F1 = 2·P·R / (P + R)**: their **harmonic mean**; if either is low, F1 drops — good as a single combined number.

**Plain analogy**: a claw machine — you pressed grab 10 times and 8 actually caught something → Precision = 80%. There were 20 dolls on the table and you got 8 → Recall = 40%.

---

## 2. Principles (grab these)

1. **Accuracy misleads under class imbalance** (99% negatives → always guessing “negative” scores 99%).
2. **P and R are a seesaw**: lower the threshold → report more, R up, P down; raise it → the reverse.
3. **F1 combines them**; neither side can look terrible.

---

## 3. One diagram: four cells, two metrics

```mermaid
flowchart LR
    T[actually positive] --> TP[TP caught]
    T --> FN[FN missed]
    F[actually negative] --> FP[FP false alarm]
    F --> TN[TN rejected]
    TP --> P[Precision = TP/(TP+FP)]
    FN --> R[Recall = TP/(TP+FN)]
    P --> F1[F1 = 2PR/(P+R)]
    R --> F1
```

---

## 4. Today’s steps

1. **Watch 141–142** (1.0–1.5×); memorize the four cells.
2. **Hand-compute a small case**: 20 samples with TP=8, FP=2, FN=12, TN=8 → compute P / R / F1 / accuracy and feel how they differ.
3. **Print the confusion matrix (10×10)** for your Day-35 digit demo and find the most-confused digit pair.
4. **Compute per-class P/R/F1** (`sklearn.metrics.classification_report`).
5. **Name one “rather miss than be wrong” scenario and one “rather be wrong than miss” scenario**, and say which metric each should watch.
6. **Mirror test (3 min):** *“TP/FP/FN/TN are ___; Precision cares about ___; Recall cares about ___; when is accuracy untrustworthy ___.”*

> ✅ **Done today when:** you can draw the four cells from memory + hand-compute P/R/F1 + mirror test passed.

---

## 5. Common pitfalls

| # | Myth | Truth |
|---|---|---|
| 1 | Look only at accuracy | Badly distorted under class imbalance |
| 2 | Mix up P and R | P = “are my reports correct”, R = “did I find them all” |
| 3 | Try to max both P and R | They’re a seesaw; use F1 or choose by business cost |
| 4 | Use arithmetic mean instead of F1 | F1 is a **harmonic** mean; it punishes one side being terrible |
| 5 | Read only the confusion-matrix diagonal | The off-diagonal is where improvement lives (which class is confused) |

---

## 6. DEA cross-link (light, not main thread)

- Soft grasping evaluation should especially watch **Recall (misses)**: deformable objects have blurry, shifting outlines, so detection boxes easily miss them — a miss means grabbing empty air.
- Conversely, if your soft system triggers high-voltage actuation from a detection, **FP (false alarm) is expensive** (a wasted high-voltage pulse, possibly a wrong squeeze) — then bias toward **Precision**. This trade-off is sharper for soft bodies than for rigid arms.

---

## 7. Next / checkpoint

- **Checkpoint passed =** draw the confusion matrix + hand-compute P/R/F1 + mirror test.
- **Next (Day 37):** YOLO installation / inference demo / usage notes (143–145).

---

### References (not required today)
- Episodes 141–142 (B站《黑马程序员 · 具身智能》).
- Reuse: Day 30 (train/test split — metrics are computed on the test set).

*This lecture strictly follows 《60-Day Plan》 Day 36 (P8): 141–142. Zero military content.*
