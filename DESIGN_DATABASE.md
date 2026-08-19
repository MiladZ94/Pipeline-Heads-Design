# DESIGN DATABASE — مرجع طراحی از پایه (Pipeline / Subsea / Offshore)

> راهنما: هر استاندارد = کجا + چه زمانی + فرمول/مقدار کلیدی. برای طراحی خودت استفاده کن.

---

## 1️⃣ SUBSEA PIPELINE SYSTEMS

### DNV-ST-F101 (Submarine Pipeline Systems)
- **کی استفاده:** طراحی خط لوله زیر دریا (ضخامت، فشار، buckle، fatigue)
- **حالت طراحی:** LRFD / Limit-state (نه ASD!) — ضرایب γm, γSC, γC
- **کلیدی:**
  - Hoop stress / collapse / buckling از limit-state معادلات
  - SMYS/SMTS لوله از Table 7-5 (DNV 450: SMYS=450, SMTS=535)
  - ⚠️ 0.72 وجود ندارد در ST-F101 — مال DNV-RP-F101 (خوردگی) است
- **کاربرد در Heads:** فقط ارجاع (weld-end validation)

### DNV-RP-F101 (Corroded Pipelines)
- **کی استفاده:** ارزیابی لوله خورده (remaining strength)
- **کلیدی:** معیار 0.72 × SMYS برای hoop در حالت خوردگی

---

## 2️⃣ MARINE OPERATIONS (نصب، بالابری، A&R)

### DNV-ST-N001 (Marine Operations & Marine Warranty) ⭐ برای Heads
- **کی استفاده:** طراحی تجهیزات نصب: heads، padeyes، shackles، A&R، shroud
- **روش:** LRFD — بار طراحی Fd = F_SD × γc × γf
- **ضرایب:**
  | γc (consequence) | γf (load) | γm (material) | γmw (weld) |
  |---|---|---|---|
  | 1.30 | 1.30 | 1.15 | 1.30 |
- **DAF:** §16.2.5 Table 16-1 (≈1.4 کشش؛ بالابری 2.44)
- **زوایا:** 5° in-plane + 5° out-of-plane (§7.9.9)
- **فرمولها:**
  - Bearing: σy/γm ≥ 0.18·√[Fd(1/Dp−1/Dh)·E·β/t] (اگر Dp/Dh<0.94) یا 0.045·√[Fd·E·β/(Dh·t)] (اگر ≥0.94)
  - Tear-out: σy/γm ≥ 1.7·Fd/[(2R_pad−Dh)·t]
  - Pin gap: GAP ≥ max(2mm, 3%D_pin)
  - Shackle: WLL ≥ F_SD
  - Bolt slip: Rd = (1/γm)·μ·Tb ، Tb = 0.70·fub·As

### DNV-ST-N002 (Offshore Structures) / N003 (Marine operations analysis)
- Fatigue و تحلیل دینامیک نصب — برای تحلیل pipelay (نه طراحی head)

---

## 3️⃣ STEEL STRUCTURES (صفحات، مقاطع، جوش)

### EN 1993 Eurocode 3 (Design of Steel Structures) ⭐
- **کی استفاده:** چک مقاطع، ستونها، صفحات، جوشها
- **ضرایب:** γm0=1.0، γm1=1.1، γm2=1.25 (EC3) — ولی در ترکیب با DNV از γm=1.15 استفاده میشود
- **فرمولهای کلیدی:**
  - Section check: σy/γm ≥ √[(σax+σbend)² + 3τ²] (§6.2)
  - Weld directional: √[σ⊥²+3(τ⊥²+τ∥²)] ≤ fu/(βw·γm2)
- **مواد:** S355J0: SMYS 355/345/335 (t≤16/40/63)، SMTS 470

### Roark's Formulas (7th ed.) ⭐
- **کی استفاده:** صفحات خمشی با هندسه خاص (closure plate، clamp wings)
- **کلیدی:**
  - Table 11.2: نیمدایره گیردار تحت فشار یکنواخت: σA=−0.42·P·a²/t²، σB=−0.36، σC=+0.21
  - Table 11.4: صفحات مستطیلی با بار موضعی (clamp wings)

---

## 4️⃣ FLANGES & FITTINGS

### ASME B16.5 (Pipe Flanges & Flanged Fittings)
- **کی استفاده:** فلنجهای استاندارد تا 24" (Classes 150–2500)
- **کلیدی:** ابعاد، فشار-دما ratings، RTJ facing
- **Head example:** 8" NPS Weldneck Class 900# RTJ

### ASME B16.47 (Large Diameter Flanges) / B16.21 (Gaskets)
- B16.47: فلنج > 24" (Series A/B)
- B16.21: گسکتهای غیرفلزی

### ASME B31.7 / B31.8 (Nuclear / Gas Pipelines)
- B31.7: هستهای (در ref اومده ولی برای heads کاربردی ندارد)
- B31.8: خطوط گاز

---

## 5️⃣ MATERIALS

### API 5L (Line Pipe) ⭐
- **کی استفاده:** انتخاب گرید لوله
- **گریدها (SMYS/SMTS MPa):**
  | Grade | SMYS | SMTS |
  |---|---|---|
  | X52 | 360 | 460 |
  | X60 | 415 | 520 |
  | X65 | 450 | 535 |
  | X70 | 485 | 570 |
- **نسبت Sy/Su ≈ 0.80-0.85** (بالا — در ASME VIII-2 cap میشود)

### ASTM A694 (Carbon Steel Flanges for High-Pressure Pipe)
- **کی استفاده:** فلنجهای آهنگری خط لوله
- **گریدها:** F52 (360/485)، F60 (415/520)، F65 (450/530)
- ⚠️ A694 در ASME II-D نیست (ماده vessel نیست) — از ASTM خودش

### EN 10025 (Structural Steel Plates) ⭐
- S355J0/J2: SMYS 355/345/335، SMTS 470
- J2 = دمای پایین (−20°C) — برای offshore ترجیح

### ASTM A193/A194 (Bolts & Nuts)
- B7: SMYS 725، SMTS 860 (سیال کروم-مولی)
- 2H nuts
- PTFE-coated برای offshore (ضد خوردگی)

### Gasket
- KaMOS RTJ Octagonal (SS316) — فشار بالا offshore
- Pikotek VCS — gasket عایق/فشرده

---

## 6️⃣ PRESSURE VESSEL (اگر head فشار داخلی هم دارد)

### ASME VIII Div.2 Part 5 (Design by Analysis) ⭐
- **کی استفاده:** تحلیل تنش FEM فلنج/head با فشار
- **Allowables (von Mises):**
  - Pm ≤ S = min(Su/2.4, Sy/1.5)
  - PL, PL+Pb ≤ S_PL = max(1.5S, Sy) — اگر Sy/Su>0.70، Sy سقف به S → SPL=1.5S
  - P+Q ≤ S_PS = max(3S, 2Sy)
- **SCL/Linearization:** Annex 5-A (Stress Integration)
- **Local region:** اگر تنش >1.1S در جهت مریدینال کمتر از √(R·t) → PL (حد SPL)
- **Weld toe:** Peak (F) برای plastic collapse DISREGARD — Structural Stress Method (Annex 5-A.6)

---

## 7️⃣ ضریبهای ایمنی — خلاصه سریع
| فاکتور | مقدار | استاندارد |
|---|---|---|
| γc consequence | 1.30 | DNV-ST-N001 |
| γf load | 1.30 | DNV-ST-N001 |
| γm material | 1.15 | DNV/EC3 |
| γmw weld | 1.30 | DNV/EC3 |
| γQ variable | 1.50 | EC3 |
| DAF pull | ≈1.40 | DNV Table 16-1 |
| DAF lifting | 2.44 | DNV |
| WLL shackle | ≥ F_SD | DNV |

---

## 8️⃣ دستورالعمل انتخاب (Decision Guide)
```
سوال: چی طراحی میکنم؟
├─ خط لوله زیر دریا → DNV-ST-F101
├─ تجهیز نصب (head/padeye/A&R/shroud) → DNV-ST-N001 + EC3
├─ فلنج/اتصال → ASME B16.5/B16.47 + ASTM A694 + A193/A194
├─ فشار داخلی → ASME VIII-2 Part 5 (یا B31.8 برای گاز)
├─ صفحه خمشی غیراستاندارد → Roark Tables
├─ جوش → EC3 directional method
└─ خستگی → DNV-RP-C203 (S-N curves)
```

---

## 📁 منابع محلی
- `/opt/data/heads_design/SUMMARY.md` — روش کامل heads + مثال 8"
- `/opt/data/asme_repo/docs/Standards/` — PDF استانداردها (DNV-F101، PCC-1، II-D، B16.5/47/21، API 601)
- `/opt/data/asme_repo/extracted_part5_snippets.txt` — متن رسمی ASME VIII-2 Part 5
- Skill: `pipeline-heads-design` — روش پارامتریک heads
