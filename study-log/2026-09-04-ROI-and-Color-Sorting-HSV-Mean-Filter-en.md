# Lecture 22 — ROI & Color Sorting: HSV Extraction + Mean Filter

> **Plan slot**: Day 22 (P7) | Episodes 087 ROI / 088 Color-sorter requirements / 089 Color-sorter code / 090 A gray HSV-range extractor / 091 Add a mean filter for stability
> **Series**: Heima《Embodied Intelligence》223-lecture study notes · Day 22

## 1. Where this sits
The second P7 hands-on case: sort objects by color. Core tools: ROI, the HSV color space, mean filtering.

## 2. Core knowledge

### 2.1 ROI (087)
- Region of Interest: crop/process only the **rectangular patch you care about** — saves compute and rejects distraction.
- `roi = img[y1:y2, x1:x2]`.

### 2.2 Color-sorter requirement (088)
- Goal: find "a block of some color" in the frame, output its position / bounding box for the arm to grasp or classify.

### 2.3 HSV color extraction (089–090)
- **HSV** (Hue / Saturation / Value) suits color segmentation better than RGB: H directly says "what color", and it's less sensitive to light intensity.
- Method: `cvtColor(BGR→HSV)` → `inRange` with `[Hmin,Smin,Vmin]`~`[Hmax,Smax,Vmax]` to get a binary mask → find contours.
- "Gray HSV-range extractor" = a small slider tool to set thresholds live (avoid hard-coding).

### 2.4 Mean filter (091)
- `blur` / `medianBlur`: smooth with neighborhood average / median to **remove noise** so the detection box doesn't jitter.
- Mean blur is simple; median blur is better against "salt-and-pepper" noise.

## 3. Hands-on
Write a color sorter: open camera → to HSV → inRange for a color → find the largest contour → draw box + center; add medianBlur to stabilize; use the slider tool to set HSV ranges live.

## 4. Common pitfalls (IMPORTANT!)
- **Lighting changes → hard-coded HSV thresholds fail** → calibrate live / adapt, don't hard-code.
- No filtering → jittery box, false detections.
- In OpenCV H is 0–179 (not 0–360), S/V are 0–255 — don't mix up the ranges.
- Reversed inRange bounds → mask all black / all white.

## 5. Checkpoint
Independently build a "detect and locate a colored block" program; understand why HSV over RGB.

## 6. DEA cross-link (light, not the main thread)
- Color/vision sorting is very useful for soft grasping: when a soft hand grabs deformable objects, locating by "the object's color block" is steadier than a fixed gripper.
- The soft body's own color/markers can also serve as a proprioception cue (estimate deformation from film appearance).
- Link: after Day 24, send the "seen color block's physical coords" through IK to the arm — the loop closes, rigid or soft arm alike.

```mermaid
flowchart LR
    CAM[Camera frame BGR] --> HSV[cvtColor to HSV]
    HSV --> BLUR[medianBlur denoise]
    BLUR --> MASK[inRange color mask]
    MASK --> CNT[find contour / largest blob]
    CNT --> BOX[draw box + center]
    style MASK fill:#fff0d0
```

---
*Strictly follows the 60-day plan Day 22 (P7): episodes 087–091. Zero military content. Note: calibrate HSV live, don't hard-code.*
