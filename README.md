# Pipeline Heads Design

Design reference for **subsea pipeline installation heads** (start-up/laydown, A&R, wet-buckle recovery) — parametric for **any pipe size**.

> ⚠️ The IRENA3 8" example is a **reference only** — always recalculate for your project.

## 📂 Contents
| File | Description |
|---|---|
| **HEADS_DESIGN_CENTER.html** | 🖥️ Interactive reference center (open in browser — searchable standards, guideline, 10 checks, materials, example) |
| **DESIGN_DATABASE.md** | Standards DB — when to use which standard + key formulas |
| **GUIDELINE.md** | Step-by-step workflow: inputs → materials → load → checks → deliverables |
| **SUMMARY.md** | Full parametric method + 8" IRENA3 example (all PASS) |
| **docs/report/** | Extracted example design report text (56 pages) |

## 🏗️ Design basis
- **Loads:** DNV-ST-N001 (LRFD) — `F_d = F_SD × γc × γf` (1.30 × 1.30), DAF ≈ 1.4, 5°+5° sling angles
- **Structure:** EN 1993 Eurocode 3 + Roark's Formulas
- **Materials:** API 5L pipe · EN 10025 S355J0 plates · ASTM A694 flanges · A193 B7 bolts · KaMOS RTJ gasket
- **Acceptance:** all Unity Checks (UC) ≤ 1.0

## 🧮 10 checks
Bearing · Tear-out · Cheek weld · Main weld · Sections 0-0..3-3 · Closure plate · Pig stopper · Threadolet · Lifting padeye · Shroud
