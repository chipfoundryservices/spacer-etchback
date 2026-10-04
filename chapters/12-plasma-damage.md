# Chapter 12: Plasma-Induced Damage

## Overview

Recess (Chapter 11) is the silicon that **leaves**. Damage is what happens to the silicon and the spacer that **stay**. Spacer etchback exposes three sensitive surfaces to plasma: the source/drain silicon (or fin), the spacer sidewall itself, and in some flows the gate dielectric through charging. Each can be modified a few nanometers deep in ways a cross-section TEM barely shows, but which later appear as poor epitaxy, higher contact resistance, junction leakage, a higher spacer k-value, or excessive spacer loss in wet cleans.

This chapter covers the mechanisms (hydrogen implantation and diffusion, displacement damage, carbon depletion of low-k spacers, charging, and VUV), how to measure them, and how to reduce them.

**Learning Objectives:**
- Estimate hydrogen projected range and affected depth in silicon versus ion energy
- Explain how hydrogen damage degrades epitaxy, dopant activation, and contacts
- Describe displacement damage and amorphous-layer formation by heavy ions
- Quantify low-k spacer carbon depletion and its effect on k and wet-etch rate
- Assess charging and VUV risks in spacer etch
- Select measurement techniques and mitigation strategies

---

## 12.1 Hydrogen in Silicon

### 12.1.1 Sources of Energetic Hydrogen

Hydrofluorocarbon plasmas (CH₃F, CH₂F₂, CHF₃) produce hydrogen ions, H⁺, H₂⁺, and H₃⁺, as well as atomic H. As Chapter 6 showed:

- Light hydrogen ions cross the sheath fastest and see the **full voltage swing**, so their energy reaches the peak sheath voltage.
- Hydrogen bound in heavy molecular ions carries only a small share of the energy (a few eV).
- Atomic H radicals have thermal energies but diffuse easily into silicon.

### 12.1.2 Implantation Range

```
Hydrogen in crystalline Si (illustrative, binary-collision estimates):

H⁺ energy (eV)   Projected range R_p (nm)   Straggle ΔR_p (nm)   Max depth ~R_p + 2ΔR_p
────────────────────────────────────────────────────────────────────────────────────
  30             ~1.0                       ~0.8                 ~2.5
  50             ~1.5                       ~1.0                 ~3.5
 100             ~2.5                       ~1.5                 ~5.5
 150             ~3.5                       ~2.0                 ~7.5
 200             ~4.5                       ~2.5                 ~9.5

For comparison, heavy ions at 100 eV (F, C, Ar): R_p ≈ 0.5–1.0 nm
```

### 12.1.3 Diffusion Beyond the Range

Hydrogen diffuses quickly in silicon even near room temperature, and the wafer is warmer under plasma. It gets trapped at defects, at dopants, and in platelet-like clusters. The **hydrogen-affected depth** is therefore typically 2–3× the implantation depth:

```
H-affected layer (SIMS, illustrative):

  100 eV peak H⁺ energy, 10 s exposure, wafer at 40°C:
    Implanted region:      ~0–5 nm
    H diffusion tail:      to ~10–15 nm at >10¹⁹ cm⁻³

  30 eV peak, narrow IED:
    Implanted region:      ~0–2.5 nm
    Diffusion tail:        to ~5–7 nm
```

### 12.1.4 Consequences

```
Effect                           Mechanism                         Device impact
──────────────────────────────────────────────────────────────────────────────────
Dopant passivation (B)           H forms neutral B–H complexes     Higher R_ext
                                 → acceptors deactivated           in pFET extension
Platelet/defect formation        H clusters into {111} platelets   Epi stacking faults;
                                 and extended defects              junction leakage
Surface disorder                 Si–H bonds, broken lattice        Poor epi nucleation;
                                                                   rough interface
Enhanced etch in cleans          Damaged Si etches faster          Extra recess
                                                                   (Δ_damage, Ch. 11)
```

### 12.1.5 Recovery

```
Treatment                         Removes H?   Repairs lattice?   Thermal budget
───────────────────────────────────────────────────────────────────────────────
Pre-epi H₂ bake (750–850°C)       Yes          Partially          Moderate–High
Spike/RTA anneal                  Yes          Yes (shallow)      High
Low-T anneal (400–500°C)          Partially    No                 Low
Remove damaged layer (clean/      Yes          n/a (removed)      Low; costs recess
  short etch)
```

GAA superlattices and SiGe channels limit the thermal budget available for recovery. **Prevention through low energy and low H⁺ flux is preferred** over cure.

---

## 12.2 Displacement Damage by Heavy Ions

### 12.2.1 Amorphous Layer Formation

Heavy ions (C, F, O, Ar fragments) above ~15–20 eV displace Si atoms (Chapter 6.6). At high doses, displaced atoms overlap into a continuous amorphous layer:

```
Amorphous layer thickness on exposed Si (TEM, illustrative):

Peak heavy-ion energy   Polymer on Si   a-Si thickness
──────────────────────────────────────────────────────
  40 eV                 ~3 nm           Not detectable
  80 eV                 ~2.5 nm         ~0.5–1.0 nm
 150 eV                 ~2 nm           ~1.5–2.5 nm
 300 eV                 ~1 nm           ~3–4 nm
```

The polymer layer on silicon (Chapter 4.2) **absorbs much of the heavy-ion energy** at low bias. This is an underappreciated benefit of polymer-rich overetch chemistry: the same layer that gives selectivity also shields the lattice.

### 12.2.2 Mixed Layer

Between the polymer and crystalline silicon, a thin mixed layer of Si, C, F, O, and H forms. Carbon left in the silicon surface is a known epi-nucleation inhibitor. Post-etch cleans must remove it (Chapter 16).

---

## 12.3 Low-k Spacer Damage

### 12.3.1 Carbon Depletion

In SiOCN, SiCN, and SiBCN spacers, O atoms and to a lesser extent H atoms and ions remove carbon from the exposed sidewall:

```
Mechanism:
  Si–CH₃ + O → Si–O· + CO/CO₂/H₂O        (O radical attack)
  Si–C   + O → Si–O + CO                 (network carbon)
  Si–CH₃ + H → Si· + CH₄                 (H attack, slower)
  then Si· + H₂O (air exposure) → Si–OH  (moisture uptake → k rises)

The damaged skin:
  composition → SiOₓNᵧ(C-poor), sometimes with Si–OH
  k → 5.5–7 (vs. 4.2–5 bulk)
  dHF wet-etch rate → 5–50× bulk
```

### 12.3.2 Depth Growth

Carbon depletion is diffusion-limited: O must diffuse in through the already-depleted layer. Depth grows approximately as √t:

```
d_dep(t) ≈ K · √t

K depends on O flux, wafer temperature, film porosity/density, and
whether a polymer shield is present on the sidewall:

Condition                              K (nm/s^½, illustrative)
───────────────────────────────────────────────────────────────
CH₃F/O₂ (high O), 40°C, no shield      0.30
CH₃F/O₂ (balanced), 20°C, thin shield   0.15
CH₃F/CO₂, 20°C, polymer shield          0.06
O₂-free, 20°C                           0.03 (H-driven)

Example: 25 s total sidewall exposure
  K = 0.30 → d_dep ≈ 1.5 nm
  K = 0.06 → d_dep ≈ 0.3 nm
```

### 12.3.3 Impact on Spacer Width and k

```
Spacer: 6.0 nm SiOCN, k_bulk = 4.6
Damaged skin d_dep = 1.5 nm, k_skin = 6.2, dHF rate 20× bulk

(1) Effective k (series model, skin on one face):
    1/k_eff = (4.5/6)/4.6 + (1.5/6)/6.2 = 0.1630 + 0.0403 = 0.2033
    k_eff ≈ 4.92 (+7%)

(2) After a pre-epi dHF clean that removes 0.3 nm of bulk SiOCN
    equivalent time:
    Skin removal: the 1.5 nm skin uses only 1.5/20 = 0.075 nm of the
    bulk-equivalent clean budget, so the whole skin is removed
    Remaining budget removes 0.3 − 0.075 = 0.225 nm of bulk SiOCN
    Spacer width loss ≈ 1.5 + 0.225 ≈ 1.7 nm
    vs. 0.3 nm expected from bulk-film data

    Final spacer ≈ 4.3 nm instead of 5.7 nm → ~1.4 nm unplanned CD loss
```

Low-k damage often shows up first as **spacer loss in the next clean**, not as a k measurement. If spacer width after pre-epi clean is lower than expected, suspect carbon depletion in the etch.

### 12.3.4 Measuring Low-k Damage

```
Method                        Sensitivity                  Notes
──────────────────────────────────────────────────────────────────────────
dHF decoration                Excellent for depth          Dip patterned wafer,
                                                           measure width loss
                                                           by OCD/TEM
XPS (blanket, angle-resolved) Composition of top ~5 nm     Blanket proxy
FTIR (blanket)                Si–CH₃, Si–C, Si–OH bonds    Needs thicker films
EELS/EDS in TEM               C profile across spacer      Direct, slow
Blanket k (MIS capacitor)     Effective k                  Blanket only
```

---

## 12.4 Charging Damage

### 12.4.1 Mechanism

In dense gate arrays, electrons arriving with an isotropic velocity distribution are partly shadowed by the gate stack tops. Ions arrive vertically and reach the gap floor. The gap floor charges positive, and the gate tops charge negative (**electron shading**). If the gate electrode is connected to a large antenna, current can be driven through the gate dielectric.

### 12.4.2 Relevance to Spacer Etch

```
Flow type             Gate dielectric present        Charging risk
                      during spacer etch?
──────────────────────────────────────────────────────────────────────
Planar / gate-first   Yes (final dielectric)         Moderate: antenna rules
HKMG                                                 and test structures needed
RMG (FinFET, GAA)     Dummy oxide only (replaced     Low for final gate;
                      later)                         I/O oxide may be at risk
                                                     in some flows
```

In replacement-metal-gate flows, the final gate dielectric is deposited after spacer etch, so charging damage to it is not possible. Charging can still deflect ions at the gap floor, which affects footing and microtrenching asymmetrically.

### 12.4.3 Mitigation

- Low bias voltage (smaller charging potentials)
- Source pulsing: electrons and negative ions reach feature bottoms in the afterglow (Chapter 6.5)
- Antenna-ratio design rules and protection diodes in gate-first flows

---

## 12.5 VUV Photon Damage

Hydrofluorocarbon and O₂ plasmas emit vacuum-ultraviolet photons (wavelengths below ~200 nm). VUV photons:

- Break Si–CH₃ bonds in low-k films. The resulting dangling bonds are then attacked by radicals, which speeds carbon depletion.
- Create trapped charge and interface states in oxide layers.
- Penetrate tens of nanometers into some dielectrics, much deeper than ions.

```
Mitigation:
  • Source pulsing (VUV falls in the afterglow)
  • Lower T_e sources (less high-energy excitation)
  • Diluent choice: Ar resonance lines (104.8, 106.7 nm) and He resonance
    line (58.4 nm) contribute VUV; their relative impact depends on
    absorption depth in the exposed film
```

---

## 12.6 Detecting Damage in Production

```
Damage type             Inline-capable method               Offline reference
──────────────────────────────────────────────────────────────────────────────
H in Si                 —                                   SIMS (D-labeled
                                                            studies), TEM
a-Si layer              OCD (sometimes), ellipsometry on    TEM, RBS-channeling
                        blanket Si
Epi impact              Post-epi defect inspection          TEM of epi
                        (stacking faults), epi thickness    interface
                        variation by OCD
Dopant passivation      Sheet resistance on test pads       SRP, SIMS
Low-k carbon depletion  dHF-decoration OCD on patterned     EELS, XPS
                        monitors
Charging                Antenna test structures (gate       —
                        leakage, V_t shift) at WAT
```

The most informative **production** damage monitor is often downstream: **epitaxy defect density and epi thickness uniformity**. A change in the spacer etch's damage profile usually appears as an epi defect excursion before any direct damage measurement flags it.

---

## 12.7 Mitigation Summary

```
Lever                              Reduces                         Watch out for
──────────────────────────────────────────────────────────────────────────────────
Lower peak ion energy              H depth, a-Si, faceting         Feet, slower etch
Narrow IED (tailored waveform)     High-energy tail (H depth)      Hardware cost
Reduce H⁺ fraction (no H₂,         H implantation                  Polymer balance
  less dissociation, pulsing)                                      changes
Polymer-rich overetch              a-Si, recess (shielding)        Residue, feet
O₂ → CO₂/CO in overetch            Low-k depletion, oxidation      More polymer
Lower wafer T                      Low-k depletion, H diffusion    Feet
Liner landing                      Si never sees plasma            Width budget
Source pulsing                     VUV, charging, H⁺ fraction      Lower rate
Post-etch damaged-layer removal    Removes damaged Si              Adds recess
```

---

## 12.8 Summary & Key Takeaways

1. **Damage stays behind.** Recess is silicon removed. Damage is silicon and spacer modified a few nanometers deep that then cause downstream failures.

2. **Hydrogen goes deepest.** H⁺ at 100 eV implants ~2.5 nm, reaches ~5 nm, and diffuses to 10–15 nm. It passivates boron, forms defects, and spoils epitaxy.

3. **Polymer shields the lattice.** Heavy-ion displacement damage is limited at low bias because surface polymer absorbs much of the energy.

4. **Low-k damage shows up as spacer loss in the next clean.** Carbon-depleted skins etch 5–50× faster in dHF and raise effective k.

5. **Depletion grows as √t.** Reduce O flux, use polymer shields, and keep wafers cool to slow it.

6. **Charging matters mainly in gate-first flows.** RMG flows deposit the final gate dielectric after spacer etch.

7. **Epi defectivity is the best production damage monitor.** Spacer-etch damage changes usually appear first as epi excursions.

---

## Study Questions

1. Using the H⁺ range table, compare the maximum H depth for a sinusoidal-bias process with mean ion energy 70 eV and a ±60 eV swing, and a tailored-waveform process at 70 ± 5 eV.

2. A SiOCN spacer is exposed for 30 s with K = 0.20 nm/s^½. Calculate the depletion depth. If the spacer is 5.5 nm wide (k_bulk = 4.5, k_skin = 6.0), what is k_eff with skin on one face?

3. A pre-epi dHF clean removes 0.4 nm of bulk SiOCN. The damaged skin etches 15× faster. If the skin is 1.2 nm, what total spacer width loss results?

4. Explain why switching overetch diluent from Ar to He might reduce displacement damage but increase hydrogen-like implantation concerns. Use T_max from Chapter 6.

5. Epi stacking-fault density rose from 0.05 to 0.4 cm⁻² after a spacer-etch chamber PM. List three plausible damage-related causes and the measurements that would separate them.

---

**Previous Chapter:** [Chapter 11: Selectivity & Substrate Recess](./11-selectivity-recess.md)  
**Next Chapter:** [Chapter 13: Loading, Pattern Dependence & Uniformity](./13-loading-uniformity.md)

---

**Chapter 12 Development Status:** Complete  
**Version:** 1.0
