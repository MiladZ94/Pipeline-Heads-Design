# PIPELINE HEADS DESIGN — جمعبندی کامل اطلاعات (Task جدید)

## 📋 پروژه
- **نام:** IRENA 3 Platform & Sealine — Pipeline Heads Design
- **شرکت:** EDINA d.o.o. (کرواسی) — منطقه Izabela Concession
- **داکیومنت:** IRE-I-SEA-CS-46031 (C01 — Issued for Construction, 26/05/2026)
- **خط لوله:** 8" — از Irena 3 تا Tie-in نزدیک Izabela N (خط 10" Izabela N→S)
- **هدف:** طراحی سرپوشهای نصب خط لوله (pipeline heads) برای نصب 8"

---

## 📚 استانداردها (References)
| کد | استاندارد | کاربرد |
|---|---|---|
| [A1] | **DNV-ST-F101** | Submarine Pipeline Systems |
| [A2] | **DNV-ST-N001** | Marine Operations & Marine Warranty (بارها، DAF، padeye) |
| [A3] | **EN 1993 Eurocode 3** | Design of Steel Structures (مقاطع، جوش) |
| [A4] | **ASME B16.5** | Pipe Flanges |
| [A5] | ASME B31.7 | Nuclear Piping |
| [D1] | **Roark's Formulas** (7th ed.) | صفحات خمشی (Closure Plate Table 11.2, Clamp Table 11.4) |

- اولویت: قوانین کرواسی → Project Docs → COMPANY Specs → استانداردهای بینالمللی

---

## 🧱 مواد (Materials)
### 8" Head Pipe:
| پارامتر | مقدار |
|---|---|
| جنس | **API 5L X60** |
| SMYS | **415 MPa** |
| SMTS | **520 MPa** |
| E | 210,000 MPa |
| ν | 0.3 |
| ρ | 7.85 t/m³ |
| OD | **219.1 mm** (8") |
| ضخامت (padeye) | 12.7 mm |
| ضخامت (pig) | 12.7 mm |

### Steel Plates:
| پارامتر | مقدار |
|---|---|
| جنس | **EN 10025 S355J0** |
| SMYS | 355 MPa (t≤16) / 345 (16<t≤40) / 335 (40<t≤63) |
| SMTS | 470 MPa |
| E | 207,000 MPa |

### فلنج/بولت/گسکت:
- فلنج: **ASTM A694 F60Q**
- استاد بولت: **ASTM A193 B7 (PTFE-coated)**
- مهره: **ASTM A194 2H (PTFE)**
- گسکت: **KaMOS RTJ Octagonal R49 SS316**

---

## ⚙️ بارها (Loads)
### بارهای اسمی (از Pipelay Analysis [C2]):
| Head | Nominal [kN] | DAF | F_SD [kN] | γc | γf | **F_d [kN]** | زاویه |
|---|---|---|---|---|---|---|---|
| Start-up/Lay-down (A) | 375 | 1.40 | 527 | 1.30 | 1.30 | **887** | 5° in + 5° out |
| A&R (B) | 352 | 1.42 | 499 | 1.30 | 1.30 | **840** | 5° + 5° |
| Wet Buckle Recovery (C) | 350 | 1.42 | 496 | 1.30 | 1.30 | **836** | 5° + 5° |

### فرمول طراحی (LRFD):
```
F_d = F_SD × γc × γf     (DNV-ST-N001 §P.2.6)
γc = 1.30 (consequence), γf = 1.30 (load)
F_SD = max(SHL×DAF, DL) از Pipelay Analysis
DAF از DNV-ST-N001 §16.2.5 Table 16-1
زوایا: 5° in-plane + 5° out-of-plane (DNV §7.9.9)
```

### Shackle: **Wide Body 55t P-6013** (WLL = 55 mT = 540 kN ≥ F_SD = 527 kN)

---

## 🔧 چکهای طراحی (Design Criteria)

### 1. Bearing/Contact Stress (DNV-ST-N001 §P2.7):
```
اگر D_pin/D_H < 0.94:  σy/γm ≥ 0.18·√[Fd·(1/Dpin − 1/DH)·E·β/t]
اگر D_pin/D_H ≥ 0.94:  σy/γm ≥ 0.045·√[Fd·E·β/(DH·t)]
γm = 1.15
```

### 2. Tear Out (Shear Out):
```
σy/γm ≥ 1.7·Fd / [(2·R_pad − DH)·t]
```

### 3. Cheek Plate Weld:
```
σy/γmw ≥ Fd·tch·δ / (1.5·t·Dch·a)
δ = 4·tan(v)·h/t + 1
γmw = 1.30
```

### 4. Main Plate-to-Pipe Weld (دایرکشنال):
```
√[σ⊥² + 3(τ⊥² + τ∥²)] ≤ fu/γmw
```

### 5. Sectional (Eurocode 3 §6.2):
```
σy/γm ≥ √[(σaxial + σbend)² + 3·τshear²]
```

### 6. Closure Plate (Roark Table 11.2):
```
σA = −0.42·PLD·a²/t²   (semicircular, fixed edges, hydrotest P)
σB = −0.36·PLD·a²/t²
σC = +0.21·PLD·a²/t²
UC = max(|σA|,|σB|,|σC|)/fyd ≤ 1
γQ = 1.50, γm = 1.15
```

### 7. Threadolet Weld:
```
P·γQ·Area_hole / WeldArea ≤ σu / (0.9·γmw·√3)
```

### 8. Lifting Padeye (γQ=1.50, γm=1.15, γmw=1.30, DAF=2.44):
```
Bearing:  fp = Fd/(Dph·t) ≤ σy/γm
ShearOut: τEd = Fd/Area_shear ≤ σy/(γm·√3)
Weld:     σ = Fd/A_weld ≤ fu/(0.9·γmw·√3)
Fd = γQ·DAF·Weight_max
```

### 9. Shroud (Start-up/Laydown):
```
Bending:  M_MAX = γQ·Rv·L/4,  σBend = M/W ≤ σy/γm
Bolt:     F_AX = γQ·Rv·(tan θ + μroller-shroud)
          Rd = (1/γm)·μpipe-clamp·Tb,  Tb = 0.70·fu_bolt
          n·Rd ≥ F_AX
Torque:   M_Torque = k·d·T_Select  (k = 0.2)
```

---

## 📊 نتایج (همه PASS — نسبتهای بهرهبرداری)

### Head A (Start-up/Laydown) — Fd=887 kN:
| چک | Stress [MPa] | Allowable [MPa] | Ratio |
|---|---|---|---|
| Padeye Bearing | 262 | 300 | 0.87 |
| Tear Out | 82 | 300 | 0.27 |
| Cheek Plate Weld | 114 | 265 | 0.43 |
| Main Plate-Pipe Weld | 132 | 346 | 0.38 |
| Section 0-0 | 129 | 300 | 0.43 |
| Section 1-1 | 136 | 300 | 0.45 |
| Section 2-2 | 66 | 300 | 0.22 |
| **Section 3-3** | **225** | 300 | **0.75** |
| Closure Plate | max 66 | 300 | 0.22 |
| Pig Stopper | 109 | 291 | 0.37 |
| Weldolet | 17 | 232 | 0.07 |

### Head B (A&R) — Fd=840 kN: (مشابه، max ratio 0.85 bearing)
### Head C (WBR) — Fd=836 kN:
- Bearing Pin-Pipe: Fb,Ed=836 kN ≤ Fb,Rd=981 (0.85)
- **Hertz: σh,Ed=790 MPa ≤ fh,Rd=902 (0.88)** ← بحرانیترین
- Lateral Plates Section 2-2: 246/300 (0.82)

### Lifting Padeye (همه):
- Bearing: 192/300 (0.64) · Shear Out: 96/173 (0.55) · Weld: 84/232 (0.36)

### Pin Geometry (DNV): GAP = max(2mm, 3%Dpin)
- Padeye: Dpin 57 / Dhole 59 (gap 2.0 ≤ 2.0) ✓
- Pipe pin: Dpin 107 / Dhole 110 (gap 3.0 ≤ 3.2) ✓

### Shroud: Bolts M24 ×8 (fub=800, As=353mm², Tb=198kN, Tsel=90kN, ratio 0.23) · Bending 36/309 (0.12)

---

## 📐 DXFها (Drawings)
- **DW-46036**: Start-up Head Assembly & Details
- **DW-46037**: A&R Head Assembly & Details
- **DW-46039**: Laydown Head Assembly & Details
- **DW-46040**: Shroud for Start-up-Laydown Head
- (DW-46038: Wet Buckle Recovery Frame — توی پوشه نیست)

## 📁 فایلهای دانلودشده
- `/opt/data/heads_design/` — ۵ PDF (ریپورت + ۴ DXF)
- متن کامل ریپورت: `design_report.txt` (56 صفحه)

## 🎯 برای طراحی از صفر (نیازمندیها)
1. مدل 3D: Head (صفحات + padeye + cheek plates) روی 8" pipe X60
2. ابعاد اصلی: از DW-46036/37/39 (باید از PDF ها استخراج بشه)
3. تحلیل: LRFD با DNV-ST-N001 + EC3 (فرمولهای بالا)
4. چکها: Bearing, Tear-out, Welds, Sections, Closure Plate, Pig Stopper, Lifting Padeye, Shroud

---

## ⚠️ یادداشت مهم (از کاربر)
**این drawing ها و report فقط یک نمونه (example) از پروژههای آینده هستند.**
این فایلها فقط **مرجع یادگیری** هستن — برای سایزهای دیگه (قطر، فشار، بار) باید **از صفر طراحی** بشه.
→ کل بخشهای بالا دادههای نمونه 8" است؛ روش طراحی پایین **پارامتریک** است و برای هر سایزی کار میکند.

---

# 🎓 روش طراحی از صفر (PARAMETRIC — برای هر سایز)

## STEP 0 — ورودیهای طراحی (از Pipelay Analysis / Client)
| ورودی | نماد | منبع |
|---|---|---|
| قطر اسمی خط | DN [in] | پروژه |
| ضخامت لوله | t_pipe [mm] | Pipeline Design Report |
| جنس لوله | API 5L grade | پروژه |
| بار اسمی کشش | F_nom [kN] | Pipelay Analysis |
| Dynamic Load / DAF | F_DL, DAF | Pipelay Analysis |
| فشار هیدروتست | P_hydro [MPa] | پروژه |
| وزن head (برای lifting) | W [t] | مدل 3D |

## STEP 1 — انتخاب مواد (بر اساس سایز/بار)
| جزء | انتخاب استاندارد |
|---|---|
| لوله | **API 5L** (X52/X60/X65 — طبق پروژه) |
| صفحات | **EN 10025 S355J0** (یا S355J2 برای دمای پایین) |
| فلنج | **ASTM A694** (F52/F60/F65 — هماهنگ با لوله) |
| بولت | **ASTM A193 B7** (PTFE-coated برای offshore) |
| مهره | **ASTM A194 2H** |
| گسکت | **KaMOS RTJ** (جنس طبق سرویس) |

### خواص مواد (الگو):
- لوله: SMYS از جدول API 5L، SMTS = SMYS + ~100-120 MPa
- صفحات S355: SMYS=355 (t≤16) / 345 (16<t≤40) / 335 (40<t≤63)، SMTS=470
- E = 210 GPa (فولاد)، ν = 0.3، ρ = 7850 kg/m³

## STEP 2 — بار طراحی (LRFD — DNV-ST-N001)
```
F_SD = max( F_nom × DAF , F_DL )      ← از Pipelay Analysis
F_d  = F_SD × γc × γf                  ← γc=1.30 (consequence), γf=1.30 (load)
زوایا: 5° in-plane + 5° out-of-plane   ← DNV §7.9.9
DAF:  از DNV-ST-N001 §16.2.5 Table 16-1 (≈1.4 برای کشش)
```

### انتخاب Shackle:
```
WLL ≥ F_SD      (مثل: 55t → 540 kN ≥ 527 kN ✓)
ابعاد shackle: از کاتالوگ سازنده (Pin Ø برای چک bearing)
```

## STEP 3 — هندسه Padeye (sizing اولیه)
| پارامتر | رابطه |
|---|---|
| قطر سوراخ | D_H ≈ D_pin + 2mm (GAP ≥ max(2mm, 3%D_pin)) |
| ضخامت صفحه اصلی | t ≈ F_d / (σ_allow × D_pin) (اولیه) |
| شعاع padeye | R_pad ≈ 1.5 × D_H (اولیه) |
| ضخامت cheek plates | t_ch ≈ 0.5 × t (اولیه) |
| گوشه پین (pin) | از shackle catalog |

## STEP 4 — چکهای طراحی (فرمولهای کامل — برای هر سایز)

### 4.1 Bearing / Contact Stress (DNV-ST-N001 §P2.7)
```
if D_pin/D_H < 0.94:   σy/γm ≥ 0.18·√[Fd·(1/Dpin − 1/DH)·E·β/t]
if D_pin/D_H ≥ 0.94:   σy/γm ≥ 0.045·√[Fd·E·β/(DH·t)]
β = 1 (ضریب تماس)، γm = 1.15
```

### 4.2 Tear Out (Shear Out) — DNV-ST-N001
```
σy/γm ≥ 1.7·Fd / [(2·R_pad − D_H)·t]
```

### 4.3 Cheek Plate Weld
```
σy/γmw ≥ Fd·t_ch·δ / (1.5·t·D_ch·a)
δ = 4·tan(45°)·h/t + 1,   γmw = 1.30
```

### 4.4 Main Plate → Pipe Weld (روش دایرکشنال)
```
√[σ⊥² + 3(τ⊥² + τ∥²)] ≤ f_u/γmw        ← نیرو + ممان درون/برون صفحه
```

### 4.5 Sections (Eurocode 3 §6.2.9)
```
σy/γm ≥ √[(σ_axial + σ_bend)² + 3·τ_shear²]    در مقاطع بحرانی 0-0 تا 3-3
```

### 4.6 Closure Plate (Roark Table 11.2 — نیمدایره، لبههای گیردار، فشار هیدروتست)
```
σ_A = −0.42·P_LD·a²/t²
σ_B = −0.36·P_LD·a²/t²
σ_C = +0.21·P_LD·a²/t²
P_LD = γQ·P_hydro (γQ=1.50),  f_yd = f_y/γm (γm=1.15)
UC = max|σ|/f_yd ≤ 1.0
```

### 4.7 Pig Stopper (جلوگیری از عبور pig)
```
σ = F_d / A_effective ≤ σy/γm        (جوش/اتصال طبق هندسه)
```

### 4.8 Threadolet Weld
```
P·γQ·Area_hole / Weld_Area ≤ σu / (0.9·γmw·√3)
```

### 4.9 Lifting Padeye (همه heads)
```
F_d = γQ × DAF × W_max          (γQ=1.50، DAF=2.44)
Bearing:  f_p = F_d/(D_ph·t) ≤ σy/γm
ShearOut: τ = F_d/Area_shear ≤ σy/(γm·√3)
Weld:     σ = F_d/A_weld ≤ f_u/(0.9·γmw·√3)
```

### 4.10 Shroud (برای Start-up/Laydown)
```
Bending:  M_MAX = γQ·R_v·L/4 → σ_bend = M/W ≤ σy/γm
Bolt:     F_AX = γQ·R_v·(tanθ + μ_roller)   (θ=14°, μ=0.3)
          R_d = (1/γm)·μ_clamp·T_b,   T_b = 0.70·f_ub·A_s
          n·R_d ≥ F_AX
Torque:   M_T = k·d·T_sel   (k=0.2)
```

## STEP 5 — فاکتورهای ایمنی (خلاصه)
| پارامتر | مقدار | استاندارد |
|---|---|---|
| γc (consequence) | 1.30 | DNV-ST-N001 |
| γf (load) | 1.30 | DNV-ST-N001 |
| γm (material) | 1.15 | EC3 / DNV |
| γmw (weld) | 1.30 | EC3 / DNV |
| γQ (variable load) | 1.50 | EC3 |
| DAF (درون صفحه) | ≈1.40 | DNV Table 16-1 |
| DAF (lifting) | 2.44 | DNV |
| دما/محیط | PTFE coating، SS316 | offshore |

## STEP 6 — خروجیها
1. **Drawing**: Assembly + Detail (Main Padeye، Cheek Plates، Lifting Padeye، Closure Plate، Shroud)
2. **Design Report**: Inputs → Loads → Checks → Results (Table با UC)
3. **چک نهایی**: همه UC ≤ 1.0 (طبق DNV-ST-N001 + EC3)

---

## 📌 نکات کلیدی از نمونه
- **بحرانیترین چکها**: Padeye Bearing (0.87) و **Hertz Pin-Pipe (0.88)** و Section 3-3 (0.75)
- **GAP سوراخ-پین**: DNV حد = max(2mm, 3%D_pin) — برای پین 57mm → 2mm
- ۳ نوع head: A (Start-up/Laydown)، B (A&R)، C (WBR — با lateral plates + pin اتصال)
- همه چکها با **spreadsheet داخلی** (نه FEM) انجام شده — فرمولهای بالا کافیان
