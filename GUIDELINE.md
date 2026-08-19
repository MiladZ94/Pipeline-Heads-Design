# GUIDELINE — طراحی Head از صفر تا گزارش (گامبهگام)

> هدف: راهنمای کامل برای اینکه خودت محاسبهگر باشی — از دریافت ورودی تا تحویل گزارش نهایی.

---

## 🟢 PHASE 0 — ورودیها را جمع کن (قبل از هر چیزی)

### از Client / Pipelay Analysis بگیر:
| # | ورودی | نماد | چرا مهمه |
|---|---|---|---|
| 1 | قطر خط لوله | DN [in] | تعیین سایز head |
| 2 | گرید و ضخامت لوله | API 5L grade, t | جنس head pipe |
| 3 | **بار اسمی کشش** | F_nom [kN] | بار اصلی طراحی |
| 4 | **Dynamic Load / DAF** | F_DL, DAF | از تحلیل pipelay |
| 5 | فشار هیدروتست | P_hydro [MPa] | closure plate / threadolet |
| 6 | وزن head (تخمینی) | W [t] | lifting padeye |
| 7 | نوع head ها | A/B/C یا SU/LD، A&R، WBR | تعیین قطعات |
| 8 | زوایای sling | θ_in, θ_out | بار خارج صفحه |
| 9 | نوع shackle موجود | — | ابعاد pin |

### از پروژه بگیر:
- استانداردهای الزامی (شرکت معمولاً مشخص میکنه: DNV / API / ASME)
- دمای طراحی (برای انتخاب جنس)
- محیط (offshore → PTFE coating، SS316)

---

## 🟡 PHASE 1 — مواد را انتخاب کن (Decision Table)

```
لوله       → API 5L X52/X60/X65 (مطابق گرید خط)
صفحات      → EN 10025 S355J0/J2  (J2 برای دمای پایین)
فلنج       → ASTM A694 F52/F60/F65 (هماهنگ با لوله)
استاد بولت → ASTM A193 B7 (PTFE)
مهره       → ASTM A194 2H (PTFE)
گسکت       → KaMOS RTJ (SS316) یا معادل
```

**خواصی که لازم داری (از دیتابیس):**
- SMYS، SMTS هر ماده
- E=210 GPa، ν=0.3، ρ=7850 kg/m³
- جدول S355: 355 (t≤16) / 345 (16<t≤40) / 335 (40<t≤63)

---

## 🟠 PHASE 2 — بار طراحی (LRFD) را حساب کن

```
F_SD = max( F_nom × DAF , F_DL )       ← از Pipelay Analysis
F_d  = F_SD × γc × γf                  ← γc=1.30، γf=1.30 (DNV-ST-N001)
```

**نکات:**
- DAF از DNV-ST-N001 Table 16-1 (≈1.4)
- زوایا: 5° داخل صفحه + 5° خارج صفحه (باید در F_d اعمال شود — اجزای افقی/عمودی)
- اگر بار تکرارشونده/خستگی داره → fatigue check جدا (DNV-RP-C203)

**خروجی این مرحله:** F_d نهایی [kN] برای هر head

---

## 🔵 PHASE 3 — ابعاد اولیه (Sizing)

### Padeye اصلی:
```
D_pin   ← از shackle catalog (مثلاً 57mm برای 55t)
D_hole  = D_pin + GAP          (GAP ≥ max(2mm, 3%D_pin))
t_main  ← اولین حدس: t = F_d / (σ_allow × D_pin)
R_pad   ≈ 1.5 × D_hole
t_cheek ≈ 0.5 × t_main
```

### بقیه قطعات:
- Closure plate: t بر اساس P_hydro و Roark فرمول
- Lifting padeye: بر اساس وزن head
- Shroud: بر اساس R_v (بار roller) و L
- Weldolet/Nipple: طبق نیاز pig/vent

---

## 🔴 PHASE 4 — چکهای طراحی (محاسبات اصلی)

### ترتیب چکها (همان ترتیب گزارش):
| # | چک | فرمول | استاندارد |
|---|---|---|---|
| 1 | Bearing | σy/γm ≥ 0.18·√[Fd(1/Dp−1/Dh)·E·β/t] یا 0.045·√[Fd·E·β/(Dh·t)] | DNV-N001 §P2.7 |
| 2 | Tear-out | σy/γm ≥ 1.7·Fd/[(2R_pad−Dh)·t] | DNV-N001 |
| 3 | Cheek weld | σy/γmw ≥ Fd·tch·δ/(1.5·t·Dch·a) | DNV-N001 |
| 4 | Main weld | √[σ⊥²+3(τ⊥²+τ∥²)] ≤ fu/γmw | DNV-N001 |
| 5 | Sections 0-0..3-3 | σy/γm ≥ √[(σax+σbend)²+3τ²] | EC3 §6.2 |
| 6 | Closure plate | σA/B/C = Roark 11.2، UC≤1 | Roark |
| 7 | Pig stopper | σ = Fd/Area ≤ σy/γm | — |
| 8 | Threadolet | P·γQ·Ahole/Aweld ≤ σu/(0.9γmw√3) | EC3 |
| 9 | Lifting padeye | bearing/shearout/weld | DNV |
| 10 | Shroud | bending + bolts + torque | DNV/EC3 |

### فاکتورهای ایمنی (یکجا):
γc=1.30 · γf=1.30 · γm=1.15 · γmw=1.30 · γQ=1.50 · DAF_lift=2.44

### شرط قبولی:
**هر چک: Stress ≤ Allowable → UC = Stress/Allowable ≤ 1.0**
(بهترین حالت: همه UC < 0.9 — جا برای عدمقطعیت)

---

## 🟣 PHASE 5 — خروجیها

### 1. Drawing (برای drafter):
- Assembly view (head کامل روی لوله)
- Detail: Main Padeye (با ابعاد pin/hole/شعاعها)
- Detail: Cheek plates، Lifting padeye، Closure plate، Shroud
- جدول مواد (Bill of Materials) با ابعاد

### 2. Design Report (ساختار استاندارد):
```
1. INTRODUCTION
2. DEFINITIONS & ABBREVIATIONS
3. REFERENCES (استانداردها)
4. SCOPE
5. SUMMARY & CONCLUSION (جدول UC ها — اول!)
6. DESIGN DATA (مواد، بارها، فلنجها)
7. DESIGN METHODOLOGY (فرمولها)
   7.1-7.4 چکهای هر head
8. RESULTS (جدول کامل UC)
9. APPENDICES (محاسبات کامل)
```

### 3. چک نهایی قبل از تحویل:
- [ ] همه ورودیها مستند شده (از کجا اومدن)
- [ ] همه فرمولها با مرجع استاندارد
- [ ] همه UC ≤ 1.0
- [ ] واحدها یکدست (MPa, kN, mm)
- [ ] جدول خلاصه در ابتدا (بخش 5) برای مدیر

---

## ✅ CHECKLIST نهایی (قبل از ارسال)
```
□ ورودیها از Pipelay Analysis گرفتم؟ (بار، DAF، دما، فشار)
□ مواد از دیتابیس انتخاب کردم؟ (با مرجع)
□ F_d با γc×γf محاسبه شد؟
□ همه ۱۰ چک انجام شد؟
□ همه UC ≤ 1.0؟
□ ابعاد به drafter داده شد؟
□ گزارش با ساختار بالا نوشته شد؟
□ جدول خلاصه در بخش 5 هست؟
```

---

## 📌 اشتباهات رایج (Pitfalls)
1. **فراموش کردن زوایای 5°** — بار خارج صفحه واقعی است، نه صفر
2. **DAF اشتباه** — DAF بالابری (2.44) ≠ DAF کشش (1.4)
3. **γm جوش** — γmw=1.30 جدا از γm=1.15
4. **GAP سوراخ** — حداقل max(2mm, 3%D_pin) — اگر کمتر → تماس گوشهای
5. **واحدها** — kN vs N، mm vs m (خطای رایج 1000×)
6. **S355 بر اساس ضخامت** — SMYS با t عوض میشه (355→335)
7. **مقاطع 0-0 تا 3-3** — همه را چک کن، بحرانی همیشه 3-3 (پای padeye) نیست
8. **Hertz check برای Head C** — تماس pin-pipe (بحرانیترین 0.88 در نمونه)

---

## 📚 منابع (همه محلی)
- دیتابیس: `/opt/data/heads_design/DESIGN_DATABASE.md`
- روش کامل + مثال 8": `/opt/data/heads_design/SUMMARY.md`
- متن ریپورت نمونه: `/opt/data/heads_design/design_report.txt`
- Skill: `pipeline-heads-design`
