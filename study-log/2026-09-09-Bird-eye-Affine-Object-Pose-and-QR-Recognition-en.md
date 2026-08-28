# Lecture 27 · Bird's-Eye Affine / Object Pose / QR Recognition

> **Lecture info**
> - Date: 2026-09-09 (Tue)
> - Lecture #: 27 (Study Plan Day 27, P7 Computer Vision / OpenCV)
> - Plan ref: `study-plan-60d.md` → **P7 Computer Vision / OpenCV**, episodes **109–111**
> - Goal: Three practical vision tricks — **bird’s-eye affine** straightens a tilted shot into a top-down view; **object pose angle** gives rotation + center (gripper must align to angle to grasp firmly); **QR recognition** reads info via a ready API (gives the object an “ID card”).

---

## 0. One-line summary

> **Bird’s-eye affine = four-point transform that flattens a tilted image to top-down; pose angle = object center + rotation (gripper must align to grab firmly); QR recognition = ready API gives the object an identity with zero training.** Three practical tools that let the arm “see clearly and recognize”.

---

## 1. Core concepts (eps 109–111)

### 1.1 109 Bird’s-eye affine transform
- **Four-point affine** (`getPerspectiveTransform` + `warpPerspective`) straightens a tilted table shot into top-down, easier to measure coords / distances (links Day 23 scale).
- **Wrong point order → distorted image**; must map top-left → top-right → bottom-right → bottom-left.

### 1.2 110 Grasped object pose angle
- From the contour’s **minimum bounding rectangle** get “center + rotation angle”; rotate the gripper to the same angle to grab firmly.
- **Rotation-angle definition (which axis) must be consistent** or pose is wrong and the grip is crooked.

### 1.3 111 OpenCV QR-code recognition
- Ready API (e.g. `cv2.QRCodeDetector` or `pyzbar`) decodes directly to a string (URL / id).
- Like giving the object an “ID card”; the arm sorts / grasps by code — **zero training, works out of the box**.

---

## 2. Principles (grab these)

1. **Affine = line-preserving transform** used for perspective correction (tilt → flat).
2. **Pose = center + angle**; gripper must align to angle or it slips.
3. **QR = ready decode**; no model training needed to give the object an identity.

---

## 3. One diagram: see clearly and recognize

```mermaid
flowchart LR
    IMG[tilted shot] --> AFF[four-point→bird eye]
    AFF --> POSE[contour→center+angle]
    POSE --> QR[QR decode→identity]
    QR --> GRASP[align angle, grasp]
```

---

## 4. Today’s steps

1. **Watch 109–111** (1.0–1.5×), focus on 109 (point order) and 110 (how rotation angle is taken).
2. **Write bird’s-eye affine**: four points flatten the tilt.
3. **Get center + rotation angle** from contour (min bounding rect).
4. **Run QR recognition**: decode the string and print it.
5. **Mirror test (3 min):** *“What is bird’s-eye affine for ___; why align to pose angle ___; why QR needs no training ___.”*

> ✅ **Done today when:** all three trick demos run + mirror test passed.

---

## 5. Common pitfalls

| # | Myth | Truth |
|---|---|---|
| 1 | Affine points in any order | Wrong order → distorted image |
| 2 | Unclear rotation-angle definition | Wrong pose, crooked/slipping grip |
| 3 | Build your own QR recognizer | Ready API exists; don’t reinvent the wheel |
| 4 | Measure distance on tilted image | No affine correction → perspective distortion, wrong distance |

---

## 6. DEA cross-link (light, not main thread)

- Soft hands grasp **deformable objects**; pose angle helps align the gripper; **QR gives material an identity** for sorting different soft parts on a line by code.
- Link: bird’s-eye affine + pose + Day 23 scale together answer “where is it, which way, who is it” even from a tilt — rigid or soft arm alike.

---

## 7. Next / checkpoint

- **Checkpoint passed =** three trick demos run + explain use & pitfalls + mirror test.
- **Next (Day 28, P7 wrap):** face detection / emotion recognition / part counting / limits of traditional CV (112–115).

---

### References (not required today)
- Episodes 109–111 (B 站《黑马程序员 · 具身智能》).
- Reuse: Day 23 (scale), Day 25 (contour / geometry).

*This lecture strictly follows 《60-Day Plan》 Day 27 (P7): 109–111. Zero military content.*
