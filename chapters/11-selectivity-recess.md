# Chapter 11: Selectivity & Substrate Recess

## Overview

Substrate recess is the silicon lost from the source/drain region next to the spacer during and after spacer etchback. It looks minor. A nanometer or two is hard to see in a cross-section. But it accumulates over several spacer passes, it moves the top of the source/drain below the channel, it removes extension doping, and it changes the starting surface for epitaxy. At advanced nodes, a recess budget of **under 1 nm per pass** is typical. Some flows set it near 0.3 nm.

A common surprise is that recess often far exceeds what blanket selectivity predicts. A process with S(SiN:Si) = 30 and 8 s of overetch "should" lose 0.1 nm of silicon. TEM shows 1.2 nm. This chapter explains the gap. Recess has three components (direct etch, oxidation and removal, and damaged-layer removal), and only one of them is governed by selectivity.

**Learning Objectives:**
- Build a recess budget across a multi-pass logic flow
- Separate recess into direct-etch, oxidation–removal, and damaged-layer components
- Calculate silicon consumed by oxidation and removed by subsequent cleans
- Design main etch / soft landing / overetch sequences for minimum recess
- Evaluate selectivity to SiO₂ liners, SiGe, and hard masks
- Choose measurement methods for sub-nanometer recess

---

## 11.1 Why Recess Matters

### 11.1.1 Device Impact

```
Effect of recess in S/D extension region (illustrative, FinFET/planar):

Recess per pass   Cumulative (4 passes)   Consequences
─────────────────────────────────────────────────────────────────────────
0.3 nm            1.2 nm                  Negligible
0.8 nm            3.2 nm                  Extension dose loss ~5–10%;
                                          R_ext +3–5%
1.5 nm            6.0 nm                  Epi starts below channel top;
                                          R_ext +8–15%; strain transfer
                                          changes; V_t shift
```

### 11.1.2 FinFET Fin-Top Recess

In FinFETs, the fin top in the source/drain region is exposed during the gate spacer overetch, which is long because the spacer must also be cleared from the fin sidewalls (Chapter 14). Fin-top recess shortens effective fin height under the source/drain epitaxy and can change the epitaxial facet shape.

---

## 11.2 Three Components of Recess

```
Total recess = Δ_direct + Δ_oxidation + Δ_damage

Δ_direct     Silicon etched directly during overetch, through its polymer
             (governed by selectivity and overetch time)

Δ_oxidation  Silicon converted to SiOₓ by O atoms/ions during the etch,
             then removed by the next dHF-containing clean
             (governed by O exposure and ion energy)

Δ_damage     Silicon damaged or amorphized by H and heavy ions, then
             removed preferentially in cleans, pre-epi bake, or epi
             pre-treatment (governed by ion energy and H flux)
```

### 11.2.1 Direct Etch

```
Δ_direct = (R_SiN / S) × t_exposed

where t_exposed is the time silicon is uncovered (overetch, plus extra
time for regions that clear early).

Example: R_SiN = 24 nm/min, S = 25, t_exposed = 10 s
  Δ_direct = (24/25) × (10/60) ≈ 0.16 nm
```

### 11.2.2 Oxidation and Removal

O atoms and O-containing ions oxidize exposed silicon. Ion bombardment drives the oxidation deeper than thermal oxidation would at the same temperature (ion-enhanced oxidation). The oxide does not etch quickly in a nitride-selective chemistry, so it survives the spacer etch. The next dilute-HF clean removes it.

```
Silicon consumed by oxidation:
  1 nm of SiO₂ contains the Si from ≈ 0.44 nm of crystalline Si

Oxidized thickness during overetch (illustrative):
  d_ox(t) ≈ d_∞ · (1 − exp(−t/τ_ox))

  d_∞ depends on ion energy (penetration) and O flux:
    E_ion = 30 eV  → d_∞ ≈ 1.0–1.5 nm
    E_ion = 80 eV  → d_∞ ≈ 2.0–2.5 nm
    E_ion = 150 eV → d_∞ ≈ 3.0–3.5 nm
  τ_ox ≈ 2–5 s (fast; saturates early in the overetch)

Δ_oxidation ≈ 0.44 × d_ox

Example: E_ion = 80 eV, d_ox ≈ 2.2 nm → Δ_oxidation ≈ 0.97 nm
```

**This is usually the largest component.** It saturates within a few seconds, so it depends mainly on **ion energy and O availability**, and only weakly on overetch time. Shortening the overetch helps less than expected. Lowering the energy or the oxygen during overetch helps more.

### 11.2.3 Damaged-Layer Removal

Hydrogen and heavy-ion bombardment create a disordered or hydrogenated silicon layer (Chapter 12). Later steps remove this layer faster than crystalline silicon:

```
Damaged layer thickness (illustrative): 1–4 nm depending on energy and H flux
Fraction removed by later cleans/pre-epi treatments: 20–80%

Δ_damage ≈ f_rem × d_dam

Example: d_dam = 2.0 nm, f_rem = 0.3 → Δ_damage ≈ 0.6 nm
```

### 11.2.4 Combined Example

```
Overetch: CH₃F/O₂/He, 80 eV peak energy, 10 s exposure, S(SiN:Si) = 25

Component       Value (nm)   Share
─────────────────────────────────────
Δ_direct        0.16          9%
Δ_oxidation     0.97         56%
Δ_damage        0.60         35%
─────────────────────────────────────
Total           1.73

"Selectivity predicts 0.16 nm; TEM after clean shows ~1.7 nm."
```

### 11.2.5 The Same Process at Lower Energy and Oxygen

```
Overetch: CH₃F/CO₂/He, 35 eV peak (narrow IED, pulsed), 12 s

Component       Value (nm)
───────────────────────────────
Δ_direct        0.12  (S higher, rate lower; longer exposure)
Δ_oxidation     0.50  (d_ox ≈ 1.1 nm; CO₂ gives fewer O atoms)
Δ_damage        0.15  (d_dam ≈ 0.8 nm, f_rem ≈ 0.2)
───────────────────────────────
Total           0.77  (−55%)
```

---

## 11.3 Selectivity to Other Materials

### 11.3.1 SiO₂ Liners and Etch-Stop Layers

Landing a nitride etch on an oxide liner (Chapter 2.4.2) moves the recess problem from silicon to the liner:

```
Liner budget:
  Liner consumed during nitride OE = (R_SiN / S(SiN:SiO₂)) × t_OE

  R_SiN = 24 nm/min, S = 6, t_OE = 10 s → 0.67 nm consumed
  Liner 2.5 nm → 1.8 nm left ✓

The remaining liner is removed in a separate step:
  dHF (S(SiO₂:Si) > 100) → Si loss ≈ 0 from the etch itself
  Oxidation component is avoided because Si was never exposed to plasma
```

The liner approach removes most of Δ_oxidation and Δ_damage, because the plasma never touches the silicon. Its costs are width, an extra deposition, and an extra clean.

### 11.3.2 SiGe

In pFET regions and GAA superlattices, SiGe may be exposed:

```
SiGe vs. Si in spacer overetch (illustrative):

  Direct etch:  SiGe etches 1.5–3× faster than Si in fluorine-containing
                chemistry (weaker Si–Ge and Ge–Ge bonds, volatile GeF₄)
  Oxidation:    SiGe oxidizes faster; Ge-oxide is water-soluble and
                removed by DI water and cleans → larger Δ_oxidation
  Ge segregation: oxidation can pile up Ge at the interface

Implication: SiGe recess often 1.5–2× Si recess under the same recipe
```

### 11.3.3 Gate Hard Mask

Covered in Chapter 10. The hard-mask budget is consumed through flat erosion (selectivity-limited) and corner faceting (angular-yield-limited).

---

## 11.4 Recipe Design for Minimum Recess

### 11.4.1 Endpoint-Triggered Soft Landing

The silicon should be exposed to plasma for as short a time and at as low an energy as possible. That means switching from the main etch to a gentle landing step **before** the field clears anywhere, using endpoint or calculated time:

```
Recipe flow:

Main etch ──(OES endpoint start detected: CN signal begins to drop,
             i.e., first areas clearing)──▶ Soft landing / Overetch
             low energy, low O, pulsed

Timing:
  Endpoint "onset" ≈ when the thinnest/fastest regions clear
  Switch at onset (or onset − margin) → Si sees only low-energy steps

Risk: switching too early leaves more film for the slow step → longer
      overetch time → more spacer top pull-down
```

### 11.4.2 Overetch Chemistry Options

```
Option                      Δ_direct   Δ_oxid.   Δ_damage   Feet/residue
──────────────────────────────────────────────────────────────────────────
CH₃F/O₂/Ar, CW, 80 eV       Low        High      High       Low
CH₃F/O₂/He, pulsed, 50 eV   Low        Medium    Medium     Medium
CH₃F/CO₂/He, pulsed, 35 eV  Low        Low       Low        Medium–High
CH₃F/He (no oxidizer)       Very low   Very low  Low–Med    High (polymer)
                                                            → needs post-strip
Quasi-ALE (Chapter 14)      ~0         Low       Very low   Low, but slow
```

### 11.4.3 Overetch Time Optimization

Because Δ_oxidation saturates quickly, and Δ_direct grows linearly, the recess–overetch curve has a characteristic shape:

```
Recess (nm)
  2.0 │                                       ___----
      │                          ___----‾‾‾‾‾
  1.5 │               ___---‾‾‾‾
      │         _--‾‾          ← slope = direct etch + damage growth
  1.0 │      _-‾
      │    /      ← steep initial rise: oxidation saturating (τ_ox)
  0.5 │  /
      │ /
  0.0 └┴─────┴─────┴─────┴─────┴─────┴──── overetch time (s)
       0     4     8     12    16    20

  First few seconds of exposure "cost" the most recess.
  Additional seconds are relatively cheap (slope is small).
```

The practical conclusion runs against intuition. **Once silicon has been exposed, shaving a few seconds off the overetch saves little recess.** The big savings come from avoiding exposure at higher energy (switching to the soft landing earlier), from lowering energy and oxygen in the step where silicon first appears, and from protecting silicon with a liner.

---

## 11.5 Measuring Sub-Nanometer Recess

```
Method                     Resolution     Notes
───────────────────────────────────────────────────────────────────────────
TEM cross-section          ~0.2 nm        Needs reference (unetched region
                                          or marker layer); local
SOI blanket monitors       ~0.05 nm       Ellipsometry of top-Si thickness
  (ellipsometry)                          before/after; captures direct +
                                          oxidation (after dHF) + some damage
OCD on patterned           ~0.2–0.3 nm    Recess as a model parameter;
  structures                              correlates with TEM
AFM step height            ~0.1 nm        Needs a protected reference area
  (masked test area)
XPS (oxide thickness)      ~0.1 nm        Measures d_ox before clean →
                                          Δ_oxidation estimate
```

### 11.5.1 SOI Recess Monitor Protocol

```
1. Measure SOI top-Si thickness (spectroscopic ellipsometry), 49 sites
2. Run the spacer overetch step alone (or full recipe on blanket Si
   with a nitride film of known thickness)
3. Apply the production post-etch clean (including dHF)
4. Re-measure top-Si thickness
5. Recess map = before − after

Also measure after etch but before clean to separate:
  Δ_direct (thickness loss before clean, corrected for oxide)
  Δ_oxidation (additional loss after dHF)
```

This monitor is cheap, fast, and sensitive to every component except some damage removal that happens only in epi pre-treatment. It is the standard daily or weekly recess control.

---

## 11.6 Summary & Key Takeaways

1. **Recess accumulates.** Several spacer passes in the same source/drain region add up, so per-pass budgets are often well under 1 nm.

2. **Recess has three parts.** Direct etch (set by selectivity), oxidation and removal (set by O and energy), and damaged-layer removal (set by H and energy).

3. **Oxidation usually dominates.** About 0.44 nm of silicon is lost per nanometer of plasma oxide removed by the next dHF clean. It saturates within seconds.

4. **Selectivity alone underestimates recess.** Blanket S(SiN:Si) predicts only the direct component, often less than 20% of the total.

5. **Lower energy and lower oxygen at first exposure give the biggest savings.** Switch to a soft landing before silicon appears, and use pulsed, narrow-IED, CO₂-based or O₂-lean overetch.

6. **Liners remove the problem at a cost.** Landing on oxide keeps plasma off silicon. Width and extra steps are the price.

7. **SiGe recesses more than Si.** Faster fluorination and oxidation, and soluble Ge oxide, give 1.5–2× the Si recess.

8. **Monitor with SOI.** Ellipsometry on SOI before and after etch and clean resolves recess to ~0.05 nm.

---

## Study Questions

1. A process has R_SiN = 30 nm/min, S(SiN:Si) = 20, t_exposed = 12 s, d_ox = 1.8 nm, d_dam = 1.5 nm, f_rem = 0.4. Calculate each recess component and the total.

2. With d_ox(t) = d_∞(1 − e^(−t/τ)), d_∞ = 2.2 nm, τ = 3 s, compute Δ_oxidation after 3, 6, and 12 s. By how much does reducing overetch from 12 s to 6 s reduce Δ_oxidation?

3. A liner of 2.0 nm SiO₂ sits under the SiN. With S(SiN:SiO₂) = 5 and R_SiN = 28 nm/min, what is the maximum overetch time that leaves at least 0.8 nm of liner?

4. If SiGe direct-etch rate is 2.2× and oxidation consumption is 1.6× that of Si, recalculate the Section 11.2.4 example for SiGe.

5. An SOI monitor shows 0.25 nm thickness loss after etch (before clean) and 0.95 nm after the dHF clean. Separate the direct and oxidation components. What d_ox does this imply?

6. Explain, using the recess–overetch curve, why switching from main etch to soft landing 2 s earlier can save more recess than cutting overetch by 4 s.

---

**Previous Chapter:** [Chapter 10: Spacer Profile Control — Footing, Faceting & Shoulder](./10-profile-control.md)  
**Next Chapter:** [Chapter 12: Plasma-Induced Damage](./12-plasma-damage.md)

---

**Chapter 11 Development Status:** Complete  
**Version:** 1.0
