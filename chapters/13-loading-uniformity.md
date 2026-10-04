# Chapter 13: Loading, Pattern Dependence & Uniformity

## Overview

A spacer etch must deliver the same width, profile, and recess on an isolated gate and on a gate buried in a 48 nm-pitch array, at the wafer center and 2 mm from the edge, today and after 500 RF-hours. Each of these differences has a physical cause. Each cause gives a **systematic** error, which means it can be predicted and, at least partly, corrected.

This chapter separates pattern-scale effects (microloading, iso-dense bias, aspect-ratio dependence), die- and wafer-scale effects (macroloading, radial and azimuthal non-uniformity, extreme edge), and their compensation.

**Learning Objectives:**
- Identify the physical sources of iso-dense spacer width bias
- Model gap-floor clearing delay in dense arrays from ion and neutral transport
- Distinguish microloading from macroloading and assess each for spacer etch
- Build a combined deposition + etch uniformity budget
- Apply compensation strategies at the design, deposition, etch, and APC levels

---

## 13.1 Iso-Dense Spacer Width Bias

### 13.1.1 Definition

```
Iso-dense bias (IDB) = w_spacer(isolated) − w_spacer(dense)

Typical uncompensated values (illustrative): +0.3 to +1.0 nm
(isolated spacers wider in most hydrofluorocarbon processes)
```

### 13.1.2 Contributing Mechanisms

```
Mechanism                          Sign of IDB     Typical size    Controlled by
──────────────────────────────────────────────────────────────────────────────────
Deposition conformality            + (dense       0.1–0.5 nm      ALD purge/dose,
  (thinner sidewall in dense)        thinner)                     PEALD plasma step
Sidewall polymer supply            + (iso         0.1–0.4 nm      Polymer precursor
  (iso sidewalls see more           thicker                       sticking, pressure
  polymer precursors)               passivation)
Redeposition of sputtered/         − or +          0.0–0.3 nm      Ion energy, Ar
  etched species from neighbors                                   fraction
Lateral etch by radicals           + or −          0.1–0.3 nm      O₂, temperature
  (radical flux differs)
Ion reflection from neighbors      − (dense       0.0–0.2 nm      IED, profile
  (dense sidewalls receive           thinner)
  reflected ions)
```

### 13.1.3 Neutral Shadowing on Sidewalls

A sidewall in a dense array "sees" only the part of the plasma visible through the gap above it. An isolated sidewall sees a full half-space. For an isotropic neutral flux, the flux to a point on the sidewall at depth z below the top of a gap of width g is approximately proportional to the solid angle of the opening:

```
View factor F(z) for a sidewall point in a long trench of width g
(2D approximation):

  F(z) ≈ ½ · (1 − z / √(z² + g²))

  Isolated sidewall: F = ½ (sees full half-space; 2D normalization)

Example: g = 20 nm
  z = 10 nm:  F ≈ ½ (1 − 10/22.4) ≈ 0.28 → 55% of isolated
  z = 50 nm:  F ≈ ½ (1 − 50/53.9) ≈ 0.036 → 7% of isolated
  z = 90 nm:  F ≈ ½ (1 − 90/92.2) ≈ 0.012 → 2% of isolated
```

Dense-array sidewalls are strongly shielded from both passivating and etching radicals, except near the top. Whether the net effect is wider or narrower dense spacers depends on which radical (polymer precursor or O/F etchant) dominates sidewall evolution in that chemistry. This is why the sign and size of IDB **change with the CH₃F:O₂ ratio**, which gives a tuning knob:

```
Illustrative IDB vs. O₂/CH₃F ratio:

  O₂/CH₃F     IDB (nm)
  0.15        +0.8   (polymer-dominated: iso sidewalls over-passivated)
  0.30        +0.3
  0.45        −0.1   (balanced)
  0.60        −0.5   (O-dominated: iso sidewalls laterally etched more)
```

The zero crossing is rarely at the same ratio that optimizes Si recess and foot, so IDB tuning is a compromise.

---

## 13.2 Gap-Floor Clearing in Dense Arrays

### 13.2.1 Geometry

```
Gap width before etch (between deposited films):
  g₀ = CPP − L_g − 2t

Example: CPP = 48 nm, L_g = 16 nm, t = 7 nm (spacer film), H = 100 nm
  g₀ = 48 − 16 − 14 = 18 nm
  Aspect ratio AR = H / g₀ ≈ 5.6
```

### 13.2.2 Ion Transport to the Floor

```
Ions arriving at angle θ reach the floor center only if:
  tan θ < (g₀/2) / H   →   θ_max = arctan(9/100) ≈ 5.1°

With θ_rms ≈ 1–2° (collisionless sheath): >99% of ions reach the floor
With θ_rms ≈ 4° (collisional sheath, Ch. 7): ~80% reach the floor center

Charging-induced deflection (Ch. 12.4) can bend low-energy ions toward
sidewalls, reducing floor flux further for the slowest ions.
```

### 13.2.3 Neutral Transport to the Floor

For neutrals entering a long trench with reaction (sticking) probability s on the walls, the flux reaching the floor falls with AR. A simple approximation for the floor-to-top flux ratio in a 2D trench is:

```
Γ_floor / Γ_top ≈ 1 / (1 + (s · AR) / (2(1 − s/2)))    (approximate)

For AR = 5.6:
  s = 0.01 (O atoms on passivated surfaces): ratio ≈ 0.97
  s = 0.1  (polymer precursors):             ratio ≈ 0.78
  s = 0.5  (high-sticking CFₓ fragments):    ratio ≈ 0.35
```

High-sticking polymer precursors are depleted toward the floor, while low-sticking etchants (O, F) reach it nearly undepleted. In a CH₃F/O₂ process, the gap floor tends to see **less polymer** than open areas. That partly offsets the ion-flux deficit.

### 13.2.4 Net Clearing Delay

```
Combined effect (illustrative, CH₃F/O₂, AR ≈ 5.6):

  Ion flux factor at floor:      0.95
  Etchant flux factor:           0.97
  Polymer flux factor:           0.80 (less polymer → faster)
  Net floor etch rate vs. open:  ≈ 0.90–1.00

At AR ≈ 10 (taller gates or tighter pitch):
  Ion flux factor:               0.85
  Net floor etch rate vs. open:  ≈ 0.80–0.90
```

The clearing delay feeds directly into the overetch requirement (Chapter 3.6, factor u_p). For tight-pitch arrays, **dense-array floor clearing often sets the overetch time**, and open areas pay for it in recess.

---

## 13.3 Macroloading

### 13.3.1 Definition and Relevance

Macroloading is the dependence of etch rate on the **total amount of etchable material** on the wafer. More exposed film consumes more etchant and produces more by-products.

```
Spacer etch exposed-film fraction:
  Blanket spacer film (most steps):   ~100% of wafer area + sidewall area
  → Little product-to-product variation

  Masked/partial spacer steps (e.g., S/D cavity spacer opened only on
  nFET or pFET): 30–70% exposed, product-dependent
  → Product-to-product rate variation of a few %
```

### 13.3.2 Sidewall Area Contribution

For dense gate products, the conformal film's total area includes the sidewalls, which can exceed the planar area:

```
Area ratio for a gate array (per unit planar area):
  A_total / A_planar ≈ 1 + 2H / CPP × (gate density fraction)

  H = 100 nm, CPP = 48 nm, 60% of die area covered by gate arrays:
  A_total / A_planar ≈ 1 + (200/48) × 0.6 ≈ 3.5

The sidewall film is mostly NOT removed (it becomes spacer), but the
gate-top and field film is. The etched volume is dominated by planar
area; the by-product load is similar across products. The polymer
SINK, however, scales with total area, which can shift polymer balance
modestly between high-density and low-density products.
```

---

## 13.4 Within-Wafer Uniformity

### 13.4.1 Combined Budget

Spacer width and recess non-uniformity at wafer scale combine deposition and etch:

```
w(r) = c(r) · t(r) − Δw_lat(r)

Var(w) ≈ Var(c·t) + Var(Δw_lat)     (if independent)

Example (3σ, nm):
  Deposition sidewall thickness:   0.25
  Etch lateral loss variation:     0.20
  Combined:                        √(0.25² + 0.20²) ≈ 0.32

Field clearing time variation sets overetch; recess variation then
follows overetch exposure variation:
  Recess(r) ∝ t_exposed(r) = t_total − t_clear(r)
  Regions that clear first (thin film, fast etch) recess most
```

### 13.4.2 Deposition–Etch Matching

If deposition is systematically thicker at the edge, an etch tuned to be **faster at the edge** clears everywhere at the same time. That minimizes overetch and evens out silicon exposure:

```
Deposition profile:   t(r) = t₀ (1 + a·(r/R)²),   a = 0.02 (2% edge-thick)
Ideal etch profile:   R(r) = R₀ (1 + a·(r/R)²)    (2% edge-fast)

Clearing time: t_clear(r) = t(r)/R(r) = t₀/R₀ (uniform)

Tools to shape R(r): edge tuning gas, coil ratio, ESC zones (Ch. 7–8)
```

This does not make spacer width uniform. Width follows sidewall thickness, which is still 2% thicker at the edge. It does make recess and clearing uniform. Width non-uniformity needs either a uniform deposition or a lateral-loss profile tuned to compensate, which usually costs some recess uniformity. The engineer has to decide which matters more for the product.

### 13.4.3 Azimuthal and Extreme-Edge Signatures

```
Signature                       Typical cause                     Ch.
────────────────────────────────────────────────────────────────────────
One-sided (slot) tilt           Pumping/transfer-slot asymmetry   5
Threefold/fourfold pattern      Coil or gas injector symmetry     5, 7
Edge ring (r > 145 mm)          Sheath bending, ring wear         8
Notch-side asymmetry            Wafer orientation × ESC zones     8
```

---

## 13.5 Compensation Strategies

### 13.5.1 By Level

```
Level          Strategy                                    Fixes
──────────────────────────────────────────────────────────────────────────
Design         Fixed-pitch gate gratings; dummy gates at   IDB, array-edge
               array edges; restricted pitches             effects
Deposition     ALD conformality tuning; dose/purge;        Sidewall thickness
               PEALD plasma power; radial thickness tune   IDB, WIW
Etch recipe    O₂/CH₃F ratio for IDB; edge tuning gas;     IDB, radial, edge
               ESC zones; coil ratio
Etch hardware  Edge-ring height/bias control; symmetric    Edge, azimuthal
               pumping
APC            Feed-forward of measured film profile;      W2W, L2L, drift
               feedback on OCD width/recess
Mask (SADP)    Mandrel CD bias by pattern density          Pitch walking,
                                                           local CD
```

### 13.5.2 Array-Edge Effects

The first and last gate in an array have one "dense" side and one "isolated" side. Their two spacers differ by roughly the IDB:

```
Array:   iso | G1 | G2 | G3 | ... | Gn | iso
Spacers: wide|  narrow ... narrow  |wide

G1 outer spacer ≈ isolated width; inner spacer ≈ dense width
→ G1 left/right asymmetry ≈ IDB
```

Design rules typically add dummy gates at array edges so that active gates always see dense neighbors on both sides.

---

## 13.6 Summary & Key Takeaways

1. **Iso-dense bias has several sources.** Deposition conformality, sidewall polymer supply, radical lateral etch, redeposition, and ion reflection all contribute, with different signs.

2. **Dense sidewalls are shielded.** Neutral view factors fall to a few percent of isolated values within tens of nanometers of the gap top.

3. **The O₂:CH₃F ratio tunes IDB.** Polymer-dominated chemistries make isolated spacers wider. O-dominated ones make them narrower.

4. **Dense-array floors often set overetch.** Ion angle limits, charging, and neutral depletion slow clearing by 0–20% at AR 5–10.

5. **Macroloading is small for blanket spacer etch.** It matters mainly for masked or partial spacer steps.

6. **Deposition–etch matching equalizes clearing.** An etch that is faster where deposition is thicker minimizes overetch and evens out recess, but does not fix width.

7. **Compensate at every level.** Design rules, deposition tuning, etch knobs, hardware, and APC each address different signatures.

---

## Study Questions

1. For CPP = 54 nm, L_g = 18 nm, t = 8 nm, H = 110 nm, calculate g₀ and AR. What ion angle can still reach the floor center?

2. Using the view-factor formula with g = 15 nm, compute the relative neutral flux at z = 5, 20, and 60 nm. At what depth does the sidewall receive less than 10% of the isolated flux?

3. Using the trench-transport approximation, compute Γ_floor/Γ_top at AR = 8 for s = 0.05 and s = 0.3. Which species is depleted more, and what does that imply for floor polymer?

4. Deposition is 1.5% thicker at the wafer edge, and etch is 1% slower at the edge. If the center clears at 20 s, when does the edge clear? How much extra overetch is needed, and what edge rate adjustment would equalize clearing?

5. An array-edge gate shows a 0.6 nm left/right spacer asymmetry. Propose two corrections: one at the design level and one at the etch level.

---

**Previous Chapter:** [Chapter 12: Plasma-Induced Damage](./12-plasma-damage.md)  
**Next Chapter:** [Chapter 14: Advanced Etchback — FinFET, GAA Inner Spacers & SADP/SAQP](./14-advanced-etchback.md)

---

**Chapter 13 Development Status:** Complete  
**Version:** 1.0
