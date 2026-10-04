# Chapter 10: Spacer Profile Control — Footing, Faceting & Shoulder

## Overview

A spacer is more than a width. Downstream steps react to its whole cross-section: the foot at the base, the straightness of the outer face, the height of the top, the facet at the top corner, and how much gate hard mask survives above it. Source/drain epitaxy sees the foot. Contact etch sees the outer face. Replacement-gate CMP sees the hard mask. Epitaxial mushroom defects find any exposed gate corner.

This chapter defines profile metrics, explains the mechanisms behind each profile defect, and develops recipe strategies that control them without trading one defect for another.

**Learning Objectives:**
- Define and measure spacer profile metrics: base, mid, and top width, foot, facet, shoulder height, hard-mask loss
- Explain footing and microtrenching as opposite outcomes of the same ion–polymer balance at the spacer base
- Quantify spacer-top pull-down and hard-mask erosion during overetch
- Diagnose profile defects in multi-layer spacer stacks
- Design multi-step recipes that separate profile objectives

---

## 10.1 Profile Metrics

### 10.1.1 Definitions

```
                 ┌──────────┐  ← HM top (reference, after etch)
                 │    HM    │
         facet ─╲│          │
                 │──────────│  ← gate electrode top
       h_sp ─────┤   gate   │
      (spacer    │          │
       top       │          │
       height)   │          │
              ▓▓▓│          │▓▓▓
         w_top▓▓▓│          │▓▓▓  ← measured at 90% of spacer height
         w_mid▓▓▓│          │▓▓▓  ← measured at 50%
        w_base▓▓▓│          │▓▓▓  ← measured at 5% (just above foot)
         foot ▓▓▓▓──────────▓▓▓▓
  ────────────┴──┴──────────┴──┴────────── substrate (recess below)

Metric             Definition
──────────────────────────────────────────────────────────────────────
w_base, w_mid,     Horizontal spacer width at 5%, 50%, 90% of h_sp
  w_top
Foot width/height  Extra width at the base beyond w_base, and its height
Taper              (w_base − w_top) / (h at 5% − h at 90%) → angle
Facet angle        Angle of the inclined surface at the spacer top
                   corner, relative to horizontal
h_sp               Spacer top height above substrate (at gate side)
Shoulder margin    Gate-electrode top height − spacer top height on the
                   gate side (must stay negative: spacer above electrode)
HM remaining       Hard-mask thickness at center and at corner
Recess             Substrate surface drop next to spacer vs. original
```

### 10.1.2 Measurement

```
Method          What it measures                    Throughput   Notes
───────────────────────────────────────────────────────────────────────────
TEM (lamella)   All metrics, atomic resolution      Very low     Reference
CD-SEM (top)    Footprint width (≈ w_base + foot)   High         Misses shape
CD-SEM (tilt)   Rough profile, foot visibility      Medium       Semi-quant.
OCD             Model-based: w_mid, h_sp, HM,       High         Needs TEM-
                foot, recess                                     anchored model
AFM (CD-AFM)    Sidewall profile (limited in        Low          Tip-limited
                tight gaps)
```

OCD (scatterometry) is the production workhorse, but only for parameters its model includes. A foot that is not in the model will appear as an error in other parameters, such as an apparently wider w_mid. When a new profile defect appears, update the OCD model against TEM (Chapter 15).

---

## 10.2 The Spacer Base: Footing vs. Microtrenching

### 10.2.1 One Balance, Two Failure Modes

At the spacer base, two effects compete:

1. **Corner polymer accumulation.** The spacer shadows part of the ion flux in the corner, so polymer builds up there and slows the etch. Too much gives a **foot**.

2. **Ion reflection from the spacer face.** Ions arriving at grazing incidence on the spacer's outer face can reflect specularly and land just beside the base, adding to the ion flux there. Too much gives a **microtrench**: a narrow groove in the substrate at the spacer edge.

```
Polymer-dominated (low energy,       Ion-dominated (high energy,
high polymer, cold):                 low polymer, tapered face):

   ▓▓▓│                                 ▓▓▓│
   ▓▓▓│                                 ▓▓▓│
   ▓▓▓▓▓ ← foot                         ▓▓▓│
───────┴──────                       ───┐▓▓┴──────
                                         └─ microtrench in Si
```

### 10.2.2 When Each Dominates

```
Condition                        Foot      Microtrench
──────────────────────────────────────────────────────────
High polymer (low O₂, cold)      ↑         ↓
High ion energy                  ↓         ↑
Tapered spacer face (sloped)     ↓         ↑ (more reflection
                                            toward base)
Narrow IED (tailored waveform)   ↓ (fewer  ↓ (fewer high-energy
                                 low-E     reflecting ions)
                                 ions)
Pulsed bias, low duty            ↑ slightly ↓
```

A narrow IED helps on both sides, which is one reason tailored-waveform bias (Chapter 6.4) is valued for spacer etch.

### 10.2.3 Foot Removal Strategies

```
Strategy                          Mechanism                 Risk
─────────────────────────────────────────────────────────────────────────
Extend overetch                   More time at the corner   Recess, spacer top
                                                            pull-down, HM loss
Raise O₂ slightly in overetch     Thinner corner polymer    Si oxidation recess,
                                                            lateral loss
Raise wafer T                     Less polymer              Lateral loss, recess
Short higher-bias "foot trim"     Ion-driven removal at     Microtrench, H damage
  step before overetch            the corner
Post-etch isotropic trim          Uniform thinning (incl.   Thins whole spacer;
                                  foot)                     needs width offset
```

A common sequence is a short foot-trim step (2–4 s at moderately higher bias) right after main-etch endpoint, followed by the low-energy, high-selectivity overetch. The foot is removed while the corner is still covered by a thin layer of film, so the higher energy does not land directly on silicon.

---

## 10.3 The Spacer Top: Pull-Down, Facet, and Shoulder

### 10.3.1 Spacer Top Pull-Down

The spacer top is **made of the film being etched**, and it faces the ion flux directly. Once the field film clears, the spacer top keeps receding at about the full film etch rate:

```
Spacer top pull-down during overetch:

  Δh_sp ≈ R_film × t_OE × (Y(θ_top)/Y(0))

Example: SiN spacer, R = 26 nm/min during OE, t_OE = 8 s,
         rounded top with effective angle factor ≈ 1.1
  Δh_sp ≈ 26 × (8/60) × 1.1 ≈ 3.8 nm
```

This is often the largest single height loss in the process. Selectivity does not protect the spacer from itself. Only shorter overetch, lower rate during overetch, or a taller initial structure (more hard mask) helps.

### 10.3.2 Hard-Mask Erosion

The gate hard mask is usually an oxide-capped nitride or an oxide/nitride bilayer, so that a nitride-selective spacer etch slows down on it:

```
HM configuration     HM loss rate during SiN OE    Comment
──────────────────────────────────────────────────────────────────────
SiN only             ≈ R_SiN (no selectivity)      Rapid loss; HM must be thick
SiO₂ cap on SiN      ≈ R_SiN / S(SiN:SiO₂)         Cap protects flat top;
                                                   corner still facets
SiN cap on SiO₂      ≈ R_SiN initially, then slow  Cap lost early; oxide
                                                   then protects
```

### 10.3.3 Faceting at the HM/Spacer Corner

The HM corner and the spacer top together form a convex corner that facets (Chapter 3.4). The facet propagates down and inward:

```
Facet propagation (illustrative):

  Facet vertical rate = R_flat × Y(θ_f)/Y(0)

  Oxide HM cap, flat loss rate 4 nm/min, Y(55°)/Y(0) = 2.0 (Ar-rich)
    → facet descends at 8 nm/min
  Same with He diluent, Y(55°)/Y(0) = 1.3
    → facet descends at 5.2 nm/min

  Over a 30 s total exposure after the HM is uncovered:
    Ar-rich: 4 nm facet descent
    He:      2.6 nm facet descent
```

### 10.3.4 Shoulder Margin and Mushroom Risk

The critical quantity is the **shoulder margin**: how far the spacer top on the gate side stays above the top of the gate electrode (polysilicon or amorphous silicon in a dummy gate):

```
Shoulder margin = h_sp(gate side) − h_electrode

Budget (illustrative):
  HM thickness as deposited:              40 nm
  HM loss in gate etch (upstream):        −12 nm
  HM at start of spacer etch:             28 nm
  Spacer top pull-down + facet:           −8 nm (at corner)
  Later etches/cleans before epitaxy:     −6 nm
  Remaining spacer above electrode:       14 nm   ✓ (> 5 nm minimum)

If upstream gate etch loses 8 nm more HM, the margin falls to 6 nm,
and a further 2 nm of faceting would bring it to the 5 nm minimum.
```

The spacer etch inherits whatever hard mask the gate etch leaves. Shoulder margin should be tracked as a **module-level budget**, not as a spacer-etch-only specification.

---

## 10.4 The Outer Face: Straightness and Taper

### 10.4.1 Sources of Taper

```
Source                               Effect
────────────────────────────────────────────────────────────────────
Gate sidewall taper (upstream)       Spacer follows; outer face tapers
Lateral etch decreasing with depth   Top thinner than base (taper)
  (more radicals at top)
Sidewall polymer thicker at base     Base protected more → taper
Faceting reaching into the spacer    Top rounded/thinned
```

### 10.4.2 Effect on Downstream Steps

```
Downstream step          Sensitive to
────────────────────────────────────────────────────────────────────
Contact etch (SAC)       w_top: thin spacer top → contact-to-gate
                         short through the spacer corner
S/D epitaxy              w_base + foot: epi proximity to channel
Silicide                 w_base: silicide encroachment
Gate-cut and RMG         h_sp, HM: CMP stop and gate-height control
```

For self-aligned contacts (SAC), **w_top** at the height of the contact etch's most aggressive point matters most. A spacer can meet w_mid specs and still fail SAC isolation if its top is faceted thin.

---

## 10.5 Multi-Layer Spacer Profiles

### 10.5.1 Different Layers, Different Rates

With stacked spacers, each layer etches at its own rate in each recipe step:

```
Example: SiO₂ liner (2 nm) / SiOCN (5 nm) / SiN cap (2 nm)
CH₃F/O₂ overetch rates (illustrative):
  SiN    26 nm/min
  SiOCN  32 nm/min  (O and C lower density; etches faster)
  SiO₂    5 nm/min

Top view of the spacer top after overetch:

    gate │ SiO₂│ SiOCN │SiN│
         │  ▲  │       │ ▲ │
         │ ┃liner│ ╲    │ ┃ cap
         │  stands    recessed
         │  proud    (notched top)

SiOCN recedes faster than the SiN cap and SiO₂ liner, so the spacer
top develops a groove ("notch"). The groove can trap residues and
weakens SAC isolation at the top.
```

### 10.5.2 Mitigations

```
• Select chemistries whose rates for the stacked materials are closer
  in the overetch step (rate matching), even at some cost in selectivity
• Order layers so the faster-etching material is protected (cap on top)
• Shorten overetch with better uniformity (Chapter 13)
• Accept the notch and fill it in a later liner deposition
```

---

## 10.6 Profile-Oriented Recipe Design

### 10.6.1 Separating Objectives by Step

```
Step            Primary profile objective       Typical settings
──────────────────────────────────────────────────────────────────────────
Breakthrough    Uniform start                   CF₄, short, moderate bias
Main etch       Vertical face, no lateral loss  CH₂F₂/O₂/Ar, medium bias,
                                                sidewall passivation
Foot trim       Remove base foot while film      Slightly higher bias, short,
                still covers the substrate      moderate polymer
Soft landing    Clear field uniformly; endpoint CH₃F/O₂/He, low bias
Overetch        Clear residues; minimum top     CH₃F/O₂(/CO₂)/He, very low
                pull-down and recess            energy, pulsed bias
```

### 10.6.2 Worked Example: Profile Budget

```
Film: 8.0 nm SiN; gate height (electrode + HM) 110 nm; HM: 10 nm SiO₂
      on 18 nm SiN; electrode below.

Step           Time    SiN rate   Effects
──────────────────────────────────────────────────────────────────────────
Breakthrough   3 s     45 nm/min  2.3 nm SiN removed
Main etch      10 s    30 nm/min  5.0 nm removed (field now ~0.7 nm left)
Foot trim      2 s     35 nm/min  0.7 nm field cleared + foot reduced
Overetch       8 s     24 nm/min  (field clear) → top pull-down, recess

The field clears 0.75/1.17 ≈ 64% of the way through the trim step, so
about 0.7 s of trim time counts as overetch.

Spacer top pull-down beyond the ideal (zero-overetch) shape:
  during foot trim:  35 × 0.7/60 × 1.1 ≈ 0.45 nm
  during overetch:   24 × 8/60 × 1.1   ≈ 3.5 nm
  total ≈ 4.0 nm

Oxide HM cap loss (exposed when the gate-top film clears;
S(SiN:SiO₂) = 3 in trim, 6 in OE):
  trim: 35/3 × 0.7/60 ≈ 0.14 nm; OE: 24/6 × 8/60 ≈ 0.53 nm → ~0.7 nm flat
  facet (×1.5): ~1.0 nm at corner → cap survives (10 nm)

Si recess (S(SiN:Si) = 18 in OE; trim lands on ~0 nm Si exposure):
  24/18 × 8/60 ≈ 0.18 nm direct + oxidation–removal component
  (Chapter 11) ≈ 0.3–0.4 nm → total ≈ 0.5 nm
```

---

## 10.7 Summary & Key Takeaways

1. **Profile is multi-dimensional.** Base, mid, and top width, foot, facet, spacer height, HM remaining, and recess each matter to a different downstream step.

2. **Feet and microtrenches come from the same balance.** Too much corner polymer gives feet. Too many reflected high-energy ions give microtrenches. A narrow IED helps with both.

3. **The spacer top etches at the film rate.** Selectivity does not protect the spacer from itself. Overetch time translates directly into spacer pull-down.

4. **Facets descend faster than flat surfaces.** Ar-rich, high-energy conditions accelerate them. Use He and low energy to slow them.

5. **Shoulder margin is a module budget.** Gate-etch HM loss, spacer pull-down, facets, and later cleans all draw on it.

6. **Stacked spacers notch at the top.** Layers with different rates create grooves. Rate-match in the overetch, or order the layers so the cap protects.

7. **Assign each profile goal to its own recipe step.** Main etch, foot trim, soft landing, and overetch each have one primary profile job.

---

## Study Questions

1. A spacer etch has a 10 s overetch at a SiN rate of 28 nm/min with an angle factor of 1.15 at the spacer top. How much does the spacer top pull down? If the shoulder margin before the etch is 12 nm and later steps consume 5 nm, does it meet a 5 nm minimum?

2. Using the facet rates in Section 10.3.3, how long can the oxide HM corner be exposed in Ar-rich chemistry before a 6 nm facet descent is reached? How long with He?

3. Explain why a tapered (sloped) spacer face increases microtrenching at the base. Sketch the ion reflection geometry.

4. In the stacked spacer of Section 10.5.1, compute the notch depth (SiOCN recess relative to the SiN cap) after an 8 s overetch. What rate ratio SiOCN:SiN would keep the notch below 0.5 nm?

5. A process shows feet of 1.8 nm. Option A extends overetch by 4 s (SiN rate 24 nm/min; Si recess rate 1.6 nm/min). Option B adds a 2 s foot trim at 35 nm/min with negligible Si exposure. Compare spacer top pull-down and Si recess for each.

6. An OCD model without a foot parameter reports w_mid 0.3 nm wider than TEM. What is the likely cause, and how would you fix the model?

---

**Previous Chapter:** [Chapter 9: Chamber Wall Conditioning & Seasoning](./09-chamber-conditioning.md)  
**Next Chapter:** [Chapter 11: Selectivity & Substrate Recess](./11-selectivity-recess.md)

---

**Chapter 10 Development Status:** Complete  
**Version:** 1.0
