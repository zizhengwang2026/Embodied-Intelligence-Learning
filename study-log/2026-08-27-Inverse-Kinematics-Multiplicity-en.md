# Lecture 14 — Inverse Kinematics: Multiplicity & Other Difficulties

> **Meta**
> - Date: 2026-08-27 (Thursday)
> - Lecture / Day: Lecture 14 — Day 14 of the study plan
> - Plan anchor: `study-plan-60d.md` → **P5 Kinematics (IK)**, course episodes **057–059**
> - Goal of today: IK = given end target pose, solve joint angles; focus on WHY IK is **multi-solution**, plus singularities / joint limits / no-solution pitfalls. Builds on Day 13 FK matrices.

---

## 0. One-line summary

> **FK is unique (angles → one end); IK is multi-solution (end → several angle sets)**; IK's trouble isn't only multiplicity — there are also singularities (Jacobian degenerates, can't move), joint limits (solution out of range), and no-solution (unreachable). The hardest lesson I learned: **I assumed IK, like FK, has one answer — but the same target can be reached by several poses**.

---

## 1. Core knowledge (against 057–059)

### 1.1 057 Verify rotation-translation matrix in code
- Verify Day 13's FK matrix actually computes coordinates right (confirm FK before IK).
- What I did: wrote a Python function taking θ1,θ2 → (x,y), then cross-checked against the §2.2 closed form; only trusted it once both agreed.

### 1.2 058 IK multiplicity
- IK = given end target pose, solve joint angles.
- **Usually multi-solution**: same end, arm can reach with "elbow up" / "elbow down" etc. (see §2.2).
- Source of multiplicity: redundant DOF, symmetric configurations.

### 1.3 059 Other IK difficulties
- **Singularity**: Jacobian degenerates, one direction suddenly "can't move" (typical: fully stretched arm can't push radially).
- **Joint limit**: solved angle exceeds hardware range (servos often only ±120° etc.).
- **No solution**: target is simply out of reach (outside workspace).

---

## 2. Principles: closed-form IK for a planar two-link arm (geometric)

### 2.1 Why IK is multi-solution: circle–circle intersection
"The end lies on a circle of radius r around the base" and "the elbow lies on a circle of radius L1 around the base and L2 around the end" — their intersection generally gives two elbow points → two solutions (elbow up / down). That's the source of multiplicity.

### 2.2 Analytic two-link IK (I derived by hand + verified in code)
Target (x, y), link lengths L1, L2, base at origin. Let `r² = x² + y²`.
- **Reachability check**: must satisfy `|L1−L2| ≤ r ≤ L1+L2`; otherwise no solution (unreachable) or degenerate.
- By the law of cosines, solve θ2:
  `cosθ2 = (x² + y² − L1² − L2²) / (2·L1·L2)`
  `θ2 = atan2( ±√(1 − cos²θ2), cosθ2 )`
  The **± picks elbow-up / elbow-down** (the two solutions).
- Then θ1 (β = direction of target from base, γ = the back-bend caused by the second link):
  `β = atan2(y, x)`
  `γ = atan2(L2·sinθ2, L1 + L2·cosθ2)`
  `θ1 = β − γ`

> Intuition: first fix "which way the end points from the base (β)", then subtract "the angle the second link bends the end back (γ)" — that's how much the first link must rotate. atan2 handles quadrants automatically, no manual sign checks.

This diagram shows "one target → two solutions" and "workspace boundary → singular / no-solution", rendered directly on GitHub:

![Inverse Kinematics IK: multiplicity & singularity](assets/ik_solutions.svg)

---

## 3. Today's operation steps

1. **Verify FK matrix in code** (confirm Day 13 is right).
2. **Derive the two-link IK above by hand**, and implement in Python: (x,y) → two sets of (θ1,θ2); feed back into FK to confirm you return to (x,y).
3. **Explain out loud**: FK vs IK, why IK multi-solves, singularity / limit / no-solution.
4. **(Later)** run an IK solver and see which solution it picks by default (usually the one "closest to the current pose").
5. **Mirror test (3 min):** *"FK vs IK ___; why is IK multi-solution ___; what are singularity / limit / no-solution ___; how to solve θ2 in two-link IK ___"*

> ✅ **Definition of "done today":** explain FK/IK difference + IK multiplicity cause + three hard cases + recite two-link IK + pass mirror test.

---

## 4. Common misconceptions & easy mistakes

| # | Misconception | Reality |
|---|---|---|
| 1 | IK has one solution | Usually multi (elbow up/down); must choose |
| 2 | Greedily take first solution | May pose weirdly or hit itself / exceed limits |
| 3 | Ignore joint limits | Solved angle may exceed hardware range (±120° servos) |
| 4 | Compute without reachability | If r is outside [|L1−L2|, L1+L2] there is no solution; check first |

---

## 5. DEA cross-link (light, not the main line)

- Rigid-arm IK solves multiplicity in "discrete angle space"; **soft / DEA arm IK solution space is a continuous deformation function space**, harder to enumerate "multi-solutions" — usually an optimizer / data-driven method finds one feasible shape (ties to Day 17 soft modeling). So soft arm's "IK" is essentially a shape-optimization problem.

---

## 6. Next steps / checkpoint

- **Checkpoint passed if:** explain FK/IK difference + IK multiplicity cause + three hard cases + recite two-link IK + pass mirror test.
- **Next lecture (Day 15):** IK solving methods — geometric vs numerical, episodes 060–062.

---

### References (for later, not required today)
- Course episodes 057–059 (B 站《黑马程序员 · 具身智能》).
- (Later) Day 15 geometric/numerical IK, Day 16 keyboard control build on this.
