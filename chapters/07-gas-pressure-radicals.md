# Chapter 7: Gas Delivery, Pressure & Radical Control

## Overview

Chapter 4 showed that spacer selectivity is a polymer-thickness difference, and that the polymer balance depends on gas ratios. This chapter treats the hardware and operating variables that set those ratios at the wafer: mass flow control, pressure, residence time, diluents, and the spatial distribution of gas across a 300 mm wafer.

The practical message is that **small flows control large outcomes**. In a CH₃F/O₂ spacer etch, O₂ may be 10–40 sccm out of a total of several hundred. A 1 sccm error in O₂ can shift selectivity by 10–20% and spacer width by a few tenths of a nanometer. Gas delivery for spacer etch has to be designed around that sensitivity.

**Learning Objectives:**
- Calculate neutral-to-ion flux ratios and explain their role in the polymer balance
- Quantify recipe sensitivity to O₂ flow, pressure, and diluent fraction
- Size mass-flow controllers for low-flow, high-sensitivity gases
- Explain how pressure changes sheath collisionality, radical density, and polymer deposition
- Design center/edge gas distribution to tune radial uniformity
- Identify by-product redeposition and gas-purity effects

---

## 7.1 Neutral and Ion Fluxes

### 7.1.1 Neutral Flux

The flux of neutral species to the wafer is:

```
Γ_n = n_n · v̄ / 4,     v̄ = √(8kT_g / (πM))

Example: 10 mTorr, T_g = 300 K
  Total gas density: n = P/kT = 1.33 Pa / (1.38 × 10⁻²³ × 300)
                       ≈ 3.2 × 10²⁰ m⁻³ = 3.2 × 10¹⁴ cm⁻³

  Polymerizing radicals (CHₓFᵧ, CFₓ), assume 5% of gas density:
    n_rad ≈ 1.6 × 10¹³ cm⁻³
    For M ≈ 33 amu: v̄ ≈ 4.4 × 10⁴ cm/s
    Γ_rad ≈ 1.6 × 10¹³ × 4.4 × 10⁴ / 4 ≈ 1.8 × 10¹⁷ cm⁻²s⁻¹

  O atoms, assume 1% of gas density:
    n_O ≈ 3.2 × 10¹² cm⁻³, v̄ ≈ 6.3 × 10⁴ cm/s
    Γ_O ≈ 5 × 10¹⁶ cm⁻²s⁻¹
```

### 7.1.2 Neutral-to-Ion Flux Ratio

With an ion flux of ~10¹⁶ cm⁻²s⁻¹ (Chapter 5), the radical-to-ion flux ratio is ~10–20. This ratio is a key descriptor of the etch regime:

```
Γ_rad / Γ_ion     Regime                           Spacer outcome
─────────────────────────────────────────────────────────────────────────
< 3               Ion-dominated, neutral-starved   Low selectivity, faceting,
                                                   etch rate limited by neutrals
5–30              Balanced (ion-enhanced etch)     Production window
> 50              Neutral/polymer-dominated        High selectivity, feet,
                                                   residue, etch stop risk
```

Most knobs in this chapter act by moving this ratio, and the balance of O atoms against polymer-forming radicals within it.

---

## 7.2 The O₂ Knob and Its Sensitivity

### 7.2.1 Sensitivity Coefficients

Define the normalized sensitivity of an output Y to an input X as:

```
s(Y, X) = (∂Y / Y) / (∂X / X)    (percent change in Y per percent change in X)
```

Representative sensitivities for a CH₃F/O₂/He nitride spacer overetch, near the selectivity peak (Chapter 4.3.1):

```
Output                 Input: O₂ flow   Pressure   Bias power   Wafer T
──────────────────────────────────────────────────────────────────────────
SiN etch rate          +0.5             −0.3       +0.6         −0.2
Si etch rate           +1.8             −0.6       +0.9         −0.8
S(SiN:Si)              −1.3             +0.3       −0.3         +0.6
Lateral spacer loss    +1.2             +0.4       −0.2         +0.4
Foot height            −1.0             +0.5       −0.8         +0.5

(Illustrative; signs are typical, magnitudes vary with operating point.)
```

**O₂ has the largest sensitivities on the outputs that matter most** (Si rate, selectivity, lateral loss). A 5% O₂ error gives a ~9% change in Si recess rate and ~6–7% change in selectivity.

### 7.2.2 Sizing the O₂ Mass-Flow Controller

MFC accuracy is often specified as a percentage of full scale (FS) at low set points:

```
O₂ set point = 20 sccm

MFC range    Accuracy spec        Absolute error   % of set point
───────────────────────────────────────────────────────────────────
500 sccm     ±1% FS               ±5.0 sccm        ±25%   ✗
100 sccm     ±1% FS               ±1.0 sccm        ±5%    marginal
 50 sccm     ±1% of set point     ±0.2 sccm        ±1%    ✓
 50 sccm     ±0.5% of set point   ±0.1 sccm        ±0.5%  ✓✓

Rule: for gases with |s| > 1 on a critical output, size the MFC so the
set point lies in the upper half of its range and specify accuracy as
% of set point.
```

Chamber-to-chamber matching depends heavily on this. Two chambers whose O₂ MFCs differ by 1 sccm at a 20 sccm set point can differ in Si recess by ~10% and look like a "chamber signature" that no recipe offset fully removes.

### 7.2.3 CH₃F:O₂ Ratio vs. Absolute Flows

Holding the **ratio** constant while changing total flow changes residence time and dilution but keeps the polymer balance roughly fixed. Recipe tuning is therefore best done on the ratio first, and on total flow second:

```
Recipe sweep design (illustrative):
  Fix total flow (e.g., 300 sccm) and pressure.
  Vary R = O₂/CH₃F from 0.15 to 0.60 in 0.05 steps.
  Measure SiN rate, Si rate (blanket), spacer width and foot (patterned).
  Identify R window where S(SiN:Si) ≥ target and foot ≤ spec.
  Then adjust total flow ±20% to confirm window stability.
```

---

## 7.3 Pressure

### 7.3.1 Sheath Collisionality

```
Mean free path (approximate, for ion–neutral charge exchange in Ar):
  λ_i (cm) ≈ 3 × 10⁻³ / P (Torr)

  P = 5 mTorr  → λ_i ≈ 0.6 cm
  P = 20 mTorr → λ_i ≈ 0.15 cm
  P = 80 mTorr → λ_i ≈ 0.04 cm

Sheath thickness at low bias (Chapter 6): ~0.3–0.6 mm

  P ≤ 20 mTorr:  λ_i ≫ s → collisionless sheath → narrow angular spread
  P ≈ 80 mTorr:  λ_i ≈ s → collisional sheath → broader angles, lower mean energy
```

Collisional sheaths send ions in at larger angles. That raises lateral etch on spacer sidewalls and lowers the mean energy at fixed bias. Spacer etch generally runs at **5–30 mTorr** to keep ion trajectories near-vertical.

### 7.3.2 Pressure and the Polymer Balance

```
Effect of raising pressure (fixed flows and powers):

  ↑ radical density (more gas, longer residence)  → more polymer
  ↓ electron temperature                          → less dissociation per molecule
  ↓ ion flux fraction (more energy to neutrals)   → higher Γ_rad/Γ_ion
  ↑ by-product partial pressure                   → more redeposition

Net: higher pressure → more polymer, more selectivity, more footing,
     slower SiN rate, more sensitivity to wall state
```

### 7.3.3 Pressure Measurement and Control

```
Error source                        Typical magnitude    Effect
──────────────────────────────────────────────────────────────────────────
Capacitance manometer zero drift    ±0.1–0.3 mTorr       At 10 mTorr: ±1–3%
Gauge thermal transpiration         Systematic           Chamber-to-chamber offset
Throttle valve resolution           ±0.1–0.2 mTorr       Step-to-step variation
Gauge location vs. wafer            Systematic           Pressure at wafer ≠ gauge
```

Regular gauge zeroing under base vacuum (Appendix C) is one of the simplest and most effective chamber-matching practices.

---

## 7.4 Diluents

### 7.4.1 Argon vs. Helium

```
Property                    Ar                        He
──────────────────────────────────────────────────────────────────────────
Ion mass                    40 amu                    4 amu
Sputter contribution        High                      Low
Faceting                    More                      Less
Plasma density (ICP)        Higher (low E_iz,         Lower (high E_iz =
                            metastables)              24.6 eV)
Heat transfer in gas        Lower                     Higher
H-like damage risk          No                        He⁺ implants several nm
                                                      at >50 eV
Typical use                 Main etch                 Overetch, soft landing
```

### 7.4.2 Dilution Fraction

Dilution affects both chemistry and physics:

```
Increasing diluent fraction (fixed total flow, pressure):

  ↓ radical density → less polymer, thinner passivation
  ↑ or ↓ density (Ar ↑, He ↓)
  Changes IED via ion mass mix (Chapter 6.2.3)

Example (illustrative):
  CH₃F : O₂ : Ar = 100 : 30 : 200  → baseline
  CH₃F : O₂ : Ar = 100 : 30 : 400  → SiN rate +10%, S(SiN:Si) −15%,
                                      faceting +20%
```

### 7.4.3 N₂ and H₂ Additions

```
N₂:  Incorporates N into polymer (CN-rich film); changes polymer
     removal on SiN; can be used to tune foot without raising O₂.
     Side effect: raises N₂ background in OES (endpoint).

H₂:  Lowers effective F/C, increases polymer on Si, raises H⁺
     fraction → more implantation damage (Chapter 12). Usually
     avoided in overetch of damage-critical spacers.
```

---

## 7.5 Spatial Gas Distribution

### 7.5.1 Center/Edge Injection

Modern spacer-etch chambers inject gas through two or more independently controlled zones:

```
            ┌─── center injector ───┐
            │                       │
    edge ───┤     dielectric        ├─── edge
  injectors │     window            │  injectors
            └───────────────────────┘
                    plasma
            ═══════ wafer ═══════════

Split ratio: f_c = Q_center / (Q_center + Q_edge)
```

### 7.5.2 Radial Profile Tuning

Radical density at the wafer is a balance of local generation, transport, and loss at walls and at the wafer. In ICP chambers, wall loss makes radical density lower near the wafer edge, while ion flux depends on coil design and can be center- or edge-peaked:

```
Typical uncompensated profiles (illustrative):

  Radius (mm)     0      50     100    130    145
  Ion flux (rel)  1.00   1.01   0.99   0.96   0.92
  Polymer (rel)   1.00   1.00   0.98   0.95   0.90
  SiN rate (rel)  1.00   1.01   1.00   0.98   0.95

Tuning tools:
  ↑ center split → more polymer/center, lower center rate
  Edge "tuning gas" (e.g., extra O₂ or CH₃F at edge only)
  Coil current ratio (inner/outer coil) for ion flux
  ESC zone temperatures (Chapter 8)
```

### 7.5.3 Tuning-Gas Strategy

A small, separately metered flow of a single gas injected only at the edge is a powerful uniformity knob:

```
Edge O₂ tuning gas: 0–5 sccm
  Effect: thins edge polymer → raises edge SiN rate, edge Si rate
  Use: compensate edge rate deficit without disturbing center

Edge CH₃F tuning gas: 0–10 sccm
  Effect: thickens edge polymer → protects edge Si, reduces edge
          lateral loss
  Use: compensate edge spacer thinning
```

Because the edge zone sets the overetch requirement (Chapter 3.6), improving edge uniformity directly reduces the overetch needed and, with it, the recess at the center.

---

## 7.6 By-Products and Redeposition

### 7.6.1 By-Product Partial Pressures

```
Etching 8 nm SiN over 300 mm wafer at 30 nm/min:
  Volume removed rate ≈ π × (15 cm)² × 30 × 10⁻⁷ cm/min
                     ≈ 2.1 × 10⁻³ cm³/min ≈ 3.5 × 10⁻⁵ cm³/s
  Si atoms (n_Si ≈ 3.9 × 10²² cm⁻³ in Si₃N₄)
    ≈ 1.4 × 10¹⁸ Si atoms/s → SiF₄ ≈ 1.4 × 10¹⁸ molecules/s
  1 sccm ≈ 4.5 × 10¹⁷ molecules/s → SiF₄ generation ≈ 3 sccm

  With 300 sccm total flow, SiF₄ ≈ 1% of gas; HCN, FCN, N₂ similar.
```

These are small fractions, but in a polymer-sensitive chemistry they matter. SiF₄ dissociated in the plasma can redeposit as SiOₓF_y when O₂ is present, adding to footing and residue.

### 7.6.2 Pattern-Density Coupling

The amount of film removed depends on how much nitride is exposed. For blanket-like spacer etch this is nearly 100% of the wafer, but in some partial-spacer or masked-spacer steps the exposed fraction is much smaller. Then by-product levels and loading change between products (Chapter 13).

### 7.6.3 Gas Purity and Line Conditioning

```
Contaminant                   Source                    Effect
──────────────────────────────────────────────────────────────────────────
H₂O in O₂ or lines            Moisture after line       Extra H and O;
                              opening                   recess and
                                                        selectivity drift
CH₃F impurities (CH₄, CH₂F₂)  Cylinder lot variation    Polymer shift
Air leak (N₂, O₂, H₂O)        Seals, fittings           O₂-like drift
Residual gas from previous    Shared lines, dead legs   Step-to-step
step                                                    contamination
```

After any gas-line maintenance, purge cycles and a chamber seasoning run should precede qualification (Appendix C).

---

## 7.7 Summary & Key Takeaways

1. **Radical-to-ion flux ratio sets the regime.** The production window is roughly 5–30. Higher ratios give polymer-dominated etching with feet. Lower ratios give ion-dominated etching with poor selectivity.

2. **O₂ is the most sensitive knob.** Normalized sensitivities above 1 on Si recess, selectivity, and lateral loss mean that small O₂ errors move key outputs.

3. **Size MFCs for the critical gases.** Low-flow, high-sensitivity gases need MFCs with set points in the upper half of range and accuracy specified as % of set point.

4. **Keep the sheath collisionless.** At 5–30 mTorr ions arrive near-vertical. Higher pressure adds polymer, broadens angles, and slows the etch.

5. **Choose diluents by role.** Ar for rate and density, He for low faceting and gentler overetch, N₂ for polymer tuning. Avoid H₂ in damage-critical steps.

6. **Edge tuning gas is a strong uniformity tool.** Small, edge-only flows of O₂ or CH₃F correct edge rate and edge spacer width without disturbing the center.

7. **By-products and purity matter.** Redeposited SiOₓF_y adds to footing. Moisture and contamination shift the polymer balance.

---

## Study Questions

1. At 15 mTorr and 300 K, compute the total gas density. If 4% are polymerizing radicals with M = 33 amu, calculate Γ_rad. With Γ_ion = 1.2 × 10¹⁶ cm⁻²s⁻¹, what is the flux ratio? Which regime is it in?

2. A recipe uses 18 sccm O₂. Si recess sensitivity to O₂ is s = +1.8, and baseline recess is 0.8 nm. What recess results from a +1 sccm MFC error? What MFC range and accuracy spec would hold the recess error under ±0.03 nm?

3. Using the approximate λ_i formula, at what pressure does λ_i equal a 0.4 mm sheath? What would you expect to happen to lateral spacer loss above that pressure?

4. The edge zone (r > 135 mm) etches SiN 5% slower than the center, which raises the overetch requirement from 40% to 46%. If an edge O₂ tuning gas eliminates the deficit, how much less overetch time is needed for a 20 s main etch, and how much center Si recess is avoided at a Si rate of 2 nm/min?

5. Estimate the SiF₄ generation rate (in sccm) for etching a 10 nm SiN film at 40 nm/min across a 300 mm wafer. What fraction of a 250 sccm total flow is this?

---

**Previous Chapter:** [Chapter 6: Ion Energy & Bias Control](./06-ion-energy-control.md)  
**Next Chapter:** [Chapter 8: Wafer Temperature & Electrostatic Chuck Design](./08-wafer-temperature-esc.md)

---

**Chapter 7 Development Status:** Complete  
**Version:** 1.0
