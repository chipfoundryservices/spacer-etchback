# Chapter 3: Etchback Physics — Anisotropic Removal of Conformal Films

## Overview

Spacer etchback depends on one physical fact: **ions arrive at the wafer moving almost vertically, while neutrals arrive from all directions.** A process that removes material only where ions strike, with neutrals supplying the chemistry and ions supplying the energy, etches downward and not sideways. Applied to a conformal film over a step, such a process leaves material only where the film is thickest in the vertical direction, along the sidewalls.

This chapter develops the geometry of conformal-film etchback, the ion-enhanced etching mechanism that makes it anisotropic, the angular dependence of ion yields that causes faceting, and the logic of overetch. These are the physical foundations for the rest of the book.

**Learning Objectives:**
- Derive the ideal spacer shape from the deposited film geometry
- Explain ion–neutral synergy and why it gives anisotropy
- Apply the threshold-energy yield model Y(E) = A(√E − √E_th)
- Relate angular yield dependence to facet formation at the spacer top
- Identify the sources of stringers and feet at the spacer base
- Size an overetch from deposition and etch non-uniformity and estimate its cost

---

## 3.1 Geometry of Conformal-Film Etchback

### 3.1.1 The Deposited Surface

Place a gate with a vertical sidewall at x = 0 (gate occupying x < 0) and height H. A perfectly conformal film of thickness t covers it. The outer surface of the film consists of:

```
Segment                      Location                         Shape
───────────────────────────────────────────────────────────────────────────
Gate top film                x < 0,  y = H + t                Flat
Convex corner (top)          0 ≤ x ≤ t, y = H + √(t² − x²)    Quarter circle, radius t
Sidewall film                x = t,  t ≤ y ≤ H                Vertical
Concave corner (bottom)      (x, y) = (t, t)                  Sharp (ideal film)
Field film                   x > t,  y = t                    Flat
```

### 3.1.2 Ideal Anisotropic Etch

An ideal anisotropic etch moves every surface point straight down at the same rate. After removing thickness *t* vertically, the surface is the original surface translated down by *t*:

```
After etching exactly t (zero overetch):

          gate          spacer
       ┌────────┐╮
       │        │ ╲        ← rounded top: y = H − t + √(t² − x²)
       │        │  │         reaches gate top (y = H) at x = 0
       │        │  │
       │        │  │       ← vertical outer face at x = t,
       │        │  │         from y = 0 to y = H − t
───────┘        └──┴────── ← field cleared at x > t
                  ←t→

Spacer width at base:        w₀ = t
Height of vertical portion:  H − t
Top shape:                   quarter circle of radius t
```

The ideal spacer has a **rounded top**, not a square one. The rounding is inherent in conformal-film geometry, not an etch artifact. Its height equals the film thickness. For SADP spacers, where the top shape matters for downstream pattern transfer, this rounding is one reason spacers are often formed on mandrels much taller than the spacer width.

### 3.1.3 Effect of Overetch

With overetch Δ (additional vertical removal), the surface translates down a further Δ. The field film is gone, so the substrate is now being etched at a rate set by selectivity:

```
After overetch Δ:

  Spacer height at gate edge:  H − Δ (if gate/HM etches at the same rate)
                               H − Δ/S_HM (if hard mask has selectivity S_HM)
  Spacer width at base:        t (unchanged, ideal anisotropic)
  Substrate recess:            Δ / S_sub
```

In an ideal anisotropic process, overetch costs spacer height and substrate, but not spacer width. In real processes, width is lost through lateral etch (Section 3.3).

### 3.1.4 Non-Ideal Deposition Geometry

Real films depart from the ideal in ways that matter for the etch:

```
Non-ideality                         Effect on etchback
──────────────────────────────────────────────────────────────────────────
Conformality c < 1                   Spacer width = c·t, not t
Bottom fillet (concave corner        Extra vertical thickness near base
  rounded, radius r_f)               → foot unless overetch ≥ r_f(1 − 1/√2)-ish
Tapered gate sidewall (angle α      Vertical film thickness on the taper is
  from vertical)                     t / sin(α) ≫ t, so the film survives;
                                     base width ≈ t / cos(α) and the spacer
                                     profile follows the taper
Re-entrant (undercut) gate           Film under overhang is shadowed from
                                     ions → stringer left at base
Overhang at gate top (breadloafing)  Shadows lower sidewall → thicker
                                     spacer base, foot
```

The bottom fillet is the most common source of **footing**. Even ALD films round the concave corner a little, and PEALD and PECVD films can show a noticeable fillet. Removing the fillet takes overetch, which comes back as substrate recess.

---

## 3.2 Ion-Enhanced Etching: Why the Etch Is Anisotropic

### 3.2.1 Ion–Neutral Synergy

The classic demonstration of ion-enhanced etching (Coburn and Winters, 1979) exposed silicon to a XeF₂ beam, an Ar⁺ beam, and both together:

```
Silicon etch rate (relative units, classic beam experiment):

XeF₂ only (spontaneous chemical etch):   ~1
Ar⁺ only (physical sputtering):          ~1
XeF₂ + Ar⁺ together:                     ~10

The combined rate is about 5× the sum of the individual rates.
```

The ion does not mainly remove material by itself. It **activates** a surface that neutrals have already fluorinated: it breaks bonds, mixes the reactive layer, and promotes desorption of etch products. Where ions strike, etching is fast. Where they do not, as on vertical sidewalls, etching proceeds only at the slow spontaneous rate.

### 3.2.2 Anisotropy From Directional Ions

Ions accelerate across the sheath and arrive nearly normal to the wafer. The ion angular distribution is characterized by the ratio of ion transverse temperature to sheath voltage:

```
Ion angular spread (approximate):

θ_rms ≈ √(kT_i / (2 · e·V_s))   (radians)

Example: T_i ≈ 0.05 eV (cold ions, collisionless sheath), V_s = 100 V
  θ_rms ≈ √(0.05 / 200) = 0.016 rad ≈ 0.9°

Example: collisional sheath (higher pressure), effective T_i ≈ 0.5 eV, V_s = 50 V
  θ_rms ≈ √(0.5 / 100) = 0.071 rad ≈ 4°
```

On a vertical sidewall, the ion flux is reduced by the factor sin(θ) for ions arriving at angle θ from normal. That is near zero for a 1° spread. The **anisotropy** A of the etch is:

```
A = 1 − (R_lateral / R_vertical)

R_vertical = R_spont + R_ion
R_lateral  ≈ R_spont + R_ion × f_off-normal

For a spacer etch:
  R_ion ≈ 30 nm/min, R_spont ≈ 0.3 nm/min, f_off-normal ≈ 0.01
  R_lateral ≈ 0.3 + 0.3 = 0.6 nm/min
  A ≈ 1 − 0.6/30.3 ≈ 0.98
```

An anisotropy of 0.98 sounds very high. Over a 60 s etch, though, it is 0.6 nm of lateral loss per side, which is a large fraction of a 7 nm spacer's tolerance. **Spacer etch chemistry is designed to suppress spontaneous etching**, mainly through sidewall passivation by polymer (Chapter 4), so that lateral loss approaches zero.

### 3.2.3 Sidewall Passivation

In fluorocarbon and hydrofluorocarbon chemistries, a thin polymer film deposits on all surfaces. On horizontal surfaces, ion bombardment removes it continuously and keeps the surface etching. On vertical surfaces, ion flux is negligible, the polymer persists, and it blocks spontaneous etching:

```
Steady-state polymer thickness (representative):

Surface                      Ion flux    Polymer thickness   Etching?
───────────────────────────────────────────────────────────────────────
Field SiN (horizontal)       Full        0.5–1.5 nm          Yes
Spacer sidewall SiN          ~0          2–5 nm              No (blocked)
Exposed Si (horizontal)      Full        2–4 nm              Slowly
```

The passivation layer is what makes the etch anisotropic in practice. It is also what makes it selective (Chapter 4). Too little polymer brings lateral etch. Too much brings footing and residue.

---

## 3.3 Ion Energy Dependence: Threshold and Yield

### 3.3.1 The Yield Model

Ion-enhanced etch yields (atoms removed per incident ion) follow a threshold law over the energy range relevant to spacer etch:

```
Y(E) = A · (√E − √E_th)    for E > E_th
Y(E) = 0                   for E ≤ E_th

where:
  E     = ion energy (eV)
  E_th  = threshold energy (eV)
  A     = material- and chemistry-dependent constant (atoms/ion/√eV)
```

The √E dependence reflects energy deposition into a collision cascade near the surface. The threshold reflects the minimum energy needed to break surface bonds and desorb etch products.

```
Representative thresholds and yields (fluorocarbon/hydrofluorocarbon,
neutral-to-ion flux ratio high enough to saturate the surface):

Material   E_th (eV)    A (atoms/ion/√eV)    Y at 100 eV
────────────────────────────────────────────────────────
SiO₂       ~20–40       ~0.10–0.14          ~0.4–0.7
Si₃N₄      ~15–30       ~0.10–0.15          ~0.5–0.9
Si         ~10–25       ~0.08–0.12          ~0.3–0.6 (strongly reduced by polymer)

Values are illustrative and depend on surface passivation and chemistry.
```

### 3.3.2 Etch Rate From Yield

```
R = Y(E) · Γ_ion / n

where Γ_ion = ion flux (ions/cm²·s), n = atom density of the film

Example: Si₃N₄ (n ≈ 1.0 × 10²³ atoms/cm³ for ρ ≈ 3.0 g/cm³)
  E = 80 eV, E_th = 20 eV, A = 0.12
  Y = 0.12 × (√80 − √20) = 0.12 × (8.94 − 4.47) = 0.54
  Γ_ion = 1.0 × 10¹⁵ ions/cm²·s
  R = 0.54 × 10¹⁵ / 10²³ = 5.4 × 10⁻⁹ cm/s = 0.054 nm/s ≈ 3.2 nm/min

This is too slow for production. Real spacer etches reach 20–60 nm/min because:
  (1) Ion flux in high-density sources is 5–20 × 10¹⁵ ions/cm²·s
  (2) Neutral-assisted yield exceeds this estimate under high radical flux
```

### 3.3.3 Why the Energy Window Is Narrow

```
Ion energy        Effect on spacer etch
─────────────────────────────────────────────────────────────────────────
< E_th (≈20 eV)   Polymer accumulates; etch stops (useful for soft landing)
20–50 eV          Slow, highly selective etch; risk of incomplete clearing
50–150 eV         Production window: good rate, acceptable selectivity
150–300 eV        Faster, but more Si damage, H implantation, faceting
> 300 eV          Physical sputtering significant; facets, poor selectivity
```

Spacer etch generally works in the lower half of the range that a typical dielectric etch uses. This is why low-bias capability and narrow ion energy distributions matter so much for spacer reactors (Chapters 5 and 6).

---

## 3.4 Angular Yield and Faceting

### 3.4.1 Angular Dependence

The ion yield depends on angle of incidence θ (measured from the surface normal):

```
Physical sputtering (e.g., Ar⁺ on oxide):
  Y(θ) rises from θ = 0, peaks at θ ≈ 55–70°, then falls to 0 at 90°
  Y(θ_max) / Y(0) ≈ 2–4

Chemically assisted (ion-enhanced) etching:
  Y(θ) roughly constant or decreasing with θ up to ~40–50°,
  then falls; peak enhancement is weaker or absent
```

### 3.4.2 Facet Formation at Convex Corners

A surface tilted at angle θ to the incoming ions recedes vertically at a rate proportional to Y(θ). At a convex corner, such as the spacer top or the gate hard-mask corner, the surface orientation with the **fastest vertical recession** takes over and spreads as a facet:

```
Facet development at the spacer top:

  t = 0               t = main etch end      t = end of overetch
     ╮                    ╲                        ╲
  ┌──┤                 ┌───╲                    ┌───────╲
  │HM│ ╲               │HM │╲                   │HM     ╱│╲
  │  │  │              │   │ │                  │  ____╱  │
  │  │  │              │   │ │                  │ │gate   │
  └──┴──┘              └───┴─┘                  └─┴───────┘

Facet angle θ_f ≈ θ at which Y(θ) is maximum

  Sputter-dominated (high E, Ar-rich):  θ_f ≈ 55–70° → strong faceting
  Chemistry-dominated (low E):          θ_f small → rounded top, weak faceting
```

**Faceting erodes spacer height and gate hard mask together.** When the facet cuts down to the gate electrode, the gate is exposed and the result is the mushroom defect described in Chapter 1. Facet control is covered in Chapter 10. The physical rule is simple: **lower ion energy and less sputter-dominated chemistry give less faceting.**

### 3.4.3 Facet Erosion Rate

```
Vertical recession of a facet at angle θ_f relative to a flat surface:

  v_facet / v_flat = Y(θ_f) / Y(0)

Example: Y(θ_f)/Y(0) = 1.8 (moderately sputter-dominated)
  Flat HM etches at 3 nm/min during overetch (S_HM ≈ 10)
  Facet recedes vertically at 5.4 nm/min
  20 s overetch → flat HM loss 1.0 nm, facet loss 1.8 nm
```

---

## 3.5 Stringers, Feet, and Residues at the Base

### 3.5.1 Stringers From Re-entrant Topography

If a gate or mandrel has a re-entrant profile, with its base narrower than its top, the film deposited under the overhang is **shadowed** from vertical ions. It survives etchback as a stringer:

```
         ┌────┐
        ╱      ╲        ← overhang
       │        │
  ▓▓▓▓ ╲ gate  ╱ ▓▓▓▓
  ▓stringer▓   ▓stringer▓   (film in shadow, survives anisotropic etch)
──────────────────────────
```

Only an isotropic component can remove a stringer, and that also thins the spacer. The cure is upstream: gates and mandrels must have vertical or slightly tapered (non-re-entrant) profiles.

### 3.5.2 Feet From Fillet and Polymer

A spacer **foot** is extra width at the base. It comes from:

1. **Deposition fillet** at the concave corner (Section 3.1.4)
2. **Polymer accumulation** in the corner, where ion flux is partially shadowed by the spacer itself
3. **Ion flux reduction near the sidewall**, from charging-induced deflection or from ions scattering off the sidewall

```
Foot clearance requirement (simplified):

  Fillet of radius r_f adds vertical thickness up to ~r_f near the base
  A foot of height h_f takes extra overetch time:
     t_foot ≈ h_f / (R_ME × f_corner)

  where f_corner (0.3–0.7) is the reduced etch rate in the corner
  due to ion shadowing and polymer.

Example: h_f = 2 nm, R_ME = 30 nm/min, f_corner = 0.5
  t_foot = 2 / (30 × 0.5) min = 0.133 min = 8 s
```

### 3.5.3 Residue in Narrow Gaps

In dense arrays, the gap between adjacent spacers can be narrower than the gate height. Neutrals and ions reaching the gap floor are reduced, so the field film there clears later. Chapter 13 develops the transport model. The key physical point is that **completion time varies with local geometry** even when the film thickness is uniform.

---

## 3.6 Overetch: Why, How Much, and at What Cost

### 3.6.1 The Overetch Equation

The main etch is timed (or endpointed) to clear the nominal film. Overetch must then cover:

```
1. Deposition non-uniformity     u_d (fractional range, thickest − nominal)
2. Etch-rate non-uniformity      u_e (fractional range, slowest vs. nominal)
3. Pattern-dependent slow-down   u_p (gap floors, fin bases)
4. Foot/fillet clearance         t_foot
5. Endpoint/timing uncertainty   u_t

Required overetch fraction (worst-case stack):

OE ≥ (1 + u_d)(1 + u_e)(1 + u_p) − 1 + u_t + t_foot / t_ME
```

### 3.6.2 Worked Example

```
Film: 8.0 nm SiN, R_ME = 30 nm/min → t_ME = 16 s

  u_d = 0.02 (2% thicker at worst location)
  u_e = 0.04 (4% slower at worst location)
  u_p = 0.10 (dense gate gap floor 10% slower)
  u_t = 0.03 (endpoint detection jitter)
  t_foot = 4 s

OE ≥ (1.02)(1.04)(1.10) − 1 + 0.03 + 4/16
   = 1.1669 − 1 + 0.03 + 0.25
   = 0.447 → 45% overetch → ~7 s

Cost of 7 s overetch (illustrative, S(SiN:Si) = 15, S(SiN:HM) = 8):
  Si recess where field cleared first: 30 nm/min × (7 s/60) / 15 ≈ 0.23 nm
    (plus the extra time those regions see while slower regions clear:
     up to 16 × 0.167 ≈ 2.7 s more → total ≈ 0.32 nm)
  HM loss:                            30 × (9.7/60) / 8 ≈ 0.6 nm
  Lateral spacer loss (A = 0.995):    30 × (23/60) × 0.005 ≈ 0.06 nm per side
```

### 3.6.3 The Overetch Trade Curve

Plotting outcomes against overetch fraction shows the window:

```
Overetch    Foot height   Fin residue   Si recess   HM loss   Spacer width
 (%)          (nm)          (nm)          (nm)        (nm)      (nm)
──────────────────────────────────────────────────────────────────────────
  10          2.5           5.0           0.08        0.2       7.35
  25          1.4           2.5           0.18        0.4       7.20
  45          0.4           0.8           0.32        0.6       7.05
  70          0.0           0.0           0.55        1.0       6.85
 100          0.0           0.0           0.85        1.4       6.60

(Illustrative; foot and residue fall steeply at first, while recess, HM loss,
and width loss rise roughly linearly. The window is where foot and residue
reach spec before recess and HM loss exceed theirs.)
```

The engineer's main tools for widening this window are:

1. **Raise selectivity** during overetch, so recess and HM loss rise more slowly (Chapters 4, 11)
2. **Reduce non-uniformity**, which lowers the overetch needed (Chapters 7, 8, 13)
3. **Reduce lateral etch**, so width holds as overetch increases (Chapters 4, 10)
4. **Use multi-step recipes**: aggressive main etch, then a highly selective soft-landing/overetch step (Chapter 11)

---

## 3.7 Summary & Key Takeaways

1. **Geometry makes the spacer.** An ideal anisotropic etch of thickness t leaves a spacer of base width c·t with a quarter-round top of radius t.

2. **Anisotropy comes from ion–neutral synergy.** Directional ions activate surfaces that neutrals have prepared. Where ions do not reach, etching nearly stops.

3. **Sidewall passivation is essential.** Even 98% anisotropy loses too much width over a production etch. Polymer on sidewalls brings lateral loss near zero.

4. **Yield follows Y = A(√E − √E_th).** Spacer etch runs in a low-energy window, roughly 50–150 eV, just above threshold.

5. **Faceting follows angular yield.** Sputter-dominated conditions (high energy, Ar-rich) form steep facets that consume spacer height and gate hard mask.

6. **Feet and stringers come from geometry and polymer.** Fillets, shadowing, and corner polymer leave material at the base. Re-entrant profiles leave stringers that anisotropic etch cannot remove.

7. **Overetch is a calculated quantity.** It is set by deposition, etch, and pattern non-uniformity, and every percent costs recess, hard mask, and width.

---

## Study Questions

1. A gate of height 90 nm is coated with a conformal 10 nm film (c = 1). After an ideal anisotropic etch with 30% overetch and a hard-mask selectivity of 8:1, what is the spacer height at the gate edge relative to the original gate top? What is the height at which the spacer's rounded top meets its vertical face?

2. Using Y(E) = A(√E − √E_th) with A = 0.12 and E_th = 20 eV, compute the ratio of yields at 60 eV and 120 eV. If silicon has A = 0.05 and E_th = 15 eV under the same conditions (polymer-suppressed), compute S(SiN:Si) at each energy, assuming equal atom densities. What does this suggest about energy choice for overetch?

3. An etch has R_vertical = 40 nm/min and an anisotropy of 0.990. How much lateral spacer loss per side occurs during a 45 s etch? What anisotropy is needed to hold lateral loss below 0.1 nm per side?

4. Sputtering yield of the gate hard mask at θ = 60° is 2.5× its normal-incidence yield. If the flat hard mask loses 1.2 nm during the etch, how much vertical height does the facet lose? If the gate electrode lies 6 nm below the hard-mask top at its corner, is the gate exposed?

5. Recalculate the overetch in Section 3.6.2 for a FinFET case where u_p = 0.30 (spacer on fin sidewalls must be cleared, Chapter 14) and t_foot = 6 s. What overetch percentage is needed? With S(SiN:Si) = 15, estimate the worst-case fin-top recess.

6. Explain qualitatively why adding Ar to a CH₃F/O₂ spacer etch increases faceting even if the bias voltage is kept constant.

---

**Previous Chapter:** [Chapter 2: Spacer Films — Materials & Deposition](./02-spacer-films.md)  
**Next Chapter:** [Chapter 4: Etch Chemistries for Spacer Materials](./04-etch-chemistries.md)

---

**Chapter 3 Development Status:** Complete  
**Version:** 1.0
