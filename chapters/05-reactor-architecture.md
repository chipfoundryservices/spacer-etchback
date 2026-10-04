# Chapter 5: Etch Reactor Architecture for Spacer Etchback

## Overview

Part I established what spacer etchback needs: directional ions at **low, well-controlled energy**, a **tunable polymer balance**, and **uniformity** good enough that overetch can stay small. This chapter turns those needs into reactor requirements and compares the reactor architectures used to meet them.

Spacer etch is usually run on conductor-etch-class reactors: inductively coupled sources with independent low-frequency bias. These are the same tools used for gate and fin etch, not the high-energy capacitively coupled tools used for high-aspect-ratio contact etch. The reason is ion energy. Spacer etch lives at 30–150 eV, and the reactor must deliver high ion flux at that energy without the source power raising it.

**Learning Objectives:**
- Translate spacer-etch process requirements into reactor specifications
- Compare ICP, dual-frequency CCP, and microwave/surface-wave sources for spacer etch
- Calculate ion flux from plasma density using the Bohm criterion, and the floor on ion energy without bias
- Estimate gas residence time and its effect on radical and by-product balance
- Describe chamber features that matter most for spacer etch: symmetry, wall temperature, gas switching, and in-situ treatment

---

## 5.1 From Process Needs to Reactor Specifications

```
Process need (Part I)                      Reactor specification
─────────────────────────────────────────────────────────────────────────────
Ion energy 30–150 eV, narrow IED           Independent bias; low minimum bias;
                                           low plasma potential; pulsing
High ion flux at low energy (rate)         High-density source (≥10¹¹ cm⁻³)
Polymer balance tunable                    Precise MFCs; low-flow capability
                                           for O₂ (few sccm resolution)
Uniformity ≤ 2% (range) on rate            Symmetric chamber; tunable source
                                           (multi-coil, multi-zone gas)
Wafer temperature control ±0.5°C           Multi-zone ESC; high He-cooling
                                           capacity
Multi-step recipes                         Fast gas switching; plasma
                                           stability across transitions
Low damage                                 Low electron temperature near
                                           wafer; no unintended high-energy
                                           tails in the IED
Low defectivity                            Y₂O₃/YOF wall coatings; controlled
                                           wall polymer; WAC capability
```

---

## 5.2 Source Architectures

### 5.2.1 Inductively Coupled Plasma (ICP/TCP)

```
              RF coil (13.56 MHz, 300–3000 W)
         ════════════════════════════════
         ┌──────── dielectric window ──────┐
         │                                 │
         │   plasma (n_e ≈ 10¹¹–10¹² cm⁻³) │  ← gas in (center/edge)
         │                                 │
         │ ─ ─ ─ ─ ─ sheath ─ ─ ─ ─ ─ ─ ─ │
         │  ███████ wafer on ESC ███████   │
         └────────────┬────────────────────┘
                      │ bias RF (0–500 W; 13.56 MHz or lower)
                    pump (symmetric, below wafer)
```

**Strengths for spacer etch:**
- Ion flux set mainly by source (coil) power, ion energy by bias power. The two are largely decoupled.
- High density at low pressure (3–30 mTorr) gives collisionless sheaths and narrow ion angular distributions.
- Bias can be reduced to zero, leaving only the plasma potential to accelerate ions (Section 5.3).

**Weaknesses:**
- Electron temperature of 2–4 eV in the bulk gives a floor on ion energy (~15–25 eV) and high dissociation. CH₃F breaks up more completely, which changes polymer chemistry relative to lower-density sources.
- Coil-induced azimuthal non-uniformity must be corrected with multi-coil or phase-controlled designs.
- Window and wall erosion are possible at high source power.

### 5.2.2 Dual-Frequency Capacitively Coupled Plasma (DF-CCP)

```
   upper electrode (showerhead) ← HF source (27–100 MHz)
   ═════════════════════════════
          plasma (n_e ≈ 10¹⁰–10¹¹ cm⁻³), gap 20–40 mm
   ═════════════════════════════
   lower electrode (ESC + wafer) ← LF bias (0.4–13.56 MHz)
```

**Strengths:**
- Excellent radial uniformity through the showerhead and a small gap
- Lower dissociation, so polymer precursors (CFₓ, CHₓFᵧ) survive more intact, which helps oxide selectivity
- Well proven for dielectric etch

**Weaknesses for spacer etch:**
- The HF source itself creates a sheath voltage at the wafer of tens of volts or more. Ion energy cannot go as low as in ICP.
- Coupling between HF and LF is stronger. Changing HF power shifts ion energy.
- Lower density gives lower ion flux at a given energy.

DF-CCP tools are used for oxide-spacer SADP and some nitride spacers where very low energy is not required.

### 5.2.3 Microwave and Surface-Wave Sources

Microwave (2.45 GHz) surface-wave and slot-antenna sources produce dense plasmas with **low electron temperature near the wafer**, about 1–1.5 eV in the diffusion region:

```
Advantages:  Very low plasma potential → ion energy floor ~5–10 eV
             Low UV and low damage; good for damage-sensitive spacers
Trade-offs:  Uniformity tuning differs; dissociation chemistry differs;
             less common installed base
```

### 5.2.4 Remote (Downstream) Plasma Sources

For isotropic etchback (Chapter 4.6, Chapter 14), the plasma is generated upstream and only radicals reach the wafer, often through an ion-filtering grid or showerhead. These are separate chamber types, sometimes integrated on the same platform as the anisotropic spacer chamber.

### 5.2.5 Comparison

```
Parameter               ICP          DF-CCP        Microwave SW    Remote
──────────────────────────────────────────────────────────────────────────────
n_e (cm⁻³)              10¹¹–10¹²    10¹⁰–10¹¹     10¹¹–10¹²       — (at wafer)
Pressure (mTorr)        3–50         15–200        5–100           100–2000
Min ion energy (eV)     ~15–25       ~30–60        ~5–10           ~0
Flux/energy decoupling  Good         Moderate      Good            n/a
Dissociation            High         Low–Med       High            Very high
Radial uniformity       Good (tuned) Excellent     Good (tuned)    Good
Typical spacer use      SiN gate     Oxide SADP    Damage-critical Inner spacer,
                        spacer, fin  spacer        spacers         trim
```

---

## 5.3 Ion Flux and the Ion Energy Floor

### 5.3.1 Ion Flux From the Bohm Criterion

Ions enter the sheath at the Bohm velocity:

```
u_B = √(k T_e / M)

Γ_ion ≈ h · n₀ · u_B      (h ≈ 0.4–0.6, edge-to-center density ratio)

Example: Ar-dominated plasma, T_e = 3 eV, M = 40 amu, n₀ = 1 × 10¹¹ cm⁻³
  u_B = √(3 × 1.6 × 10⁻¹⁹ / (40 × 1.66 × 10⁻²⁷)) ≈ 2.7 × 10³ m/s
      = 2.7 × 10⁵ cm/s
  Γ_ion ≈ 0.5 × 10¹¹ × 2.7 × 10⁵ ≈ 1.3 × 10¹⁶ ions/cm²·s

Equivalent ion current density: J = eΓ ≈ 2.2 mA/cm²
```

At this flux, the etch-rate estimate of Chapter 3.3.2 rises from ~3 nm/min to the 20–60 nm/min production range. This is why high-density ICP is the default for spacer etch.

### 5.3.2 Ion Energy With No Bias

With zero bias power, ions still gain the potential difference between the plasma and the floating wafer:

```
E_ion,min ≈ e(V_p − V_f) ≈ (k T_e / 2) · [1 + ln(M / (2π m_e))]

For Ar (M/m_e ≈ 7.3 × 10⁴):
  ln(7.3 × 10⁴ / 6.28) = ln(1.16 × 10⁴) ≈ 9.36
  E_ion,min ≈ (T_e/2) × 10.36 ≈ 5.2 T_e

T_e = 3.0 eV → E_ion,min ≈ 16 eV
T_e = 1.2 eV → E_ion,min ≈ 6 eV   (microwave diffusion region)
```

A source with high T_e cannot give ions energies below this floor. For a soft-landing or ALE step that needs ions just above the nitride threshold but below the silicon damage threshold, a 16 eV floor may already be too close. Pulsing the source to lower the average T_e (Chapter 6) is one way around this.

### 5.3.3 Power Balance and Density

```
n₀ ≈ P_abs / (e · u_B · A_eff · E_T)

E_T = total energy lost per electron–ion pair created
      (collisional loss + kinetic energy carried to walls)
      ≈ 50–150 eV, higher for molecular gases

Molecular gases (CH₃F, O₂) have larger E_T than Ar, because energy
goes into dissociation and vibrational excitation. Expect lower density
at the same coil power when the Ar fraction drops.
```

**Practical implication:** changing the diluent fraction changes density and ion flux, not only the chemistry. Recipe changes that alter Ar:CH₃F ratio need re-checking of rate and selectivity, even at fixed source power.

---

## 5.4 Chamber Geometry, Pumping, and Residence Time

### 5.4.1 Residence Time

```
τ = P · V / Q

Q in Torr·L/s: 1 sccm ≈ 0.0127 Torr·L/s

Example:
  V = 40 L (chamber plasma volume), P = 20 mTorr, Q = 400 sccm
  Q = 400 × 0.0127 = 5.07 Torr·L/s
  τ = (0.020 × 40) / 5.07 ≈ 0.16 s

Effective pumping speed at chamber: S = Q / P = 5.07 / 0.020 ≈ 250 L/s
```

### 5.4.2 Why Residence Time Matters

```
Short τ (< 0.1 s):  Feed-gas-dominated chemistry; less by-product
                    redeposition; less complete dissociation
Long τ (> 0.5 s):   By-products (SiF₄, HCN, CO) accumulate and
                    re-dissociate; more polymer from recycled carbon;
                    endpoint signals smear
```

Spacer etch generally favors short-to-moderate residence times (0.05–0.3 s). This keeps the polymer balance driven by the feed gas and gives clean transitions between recipe steps.

### 5.4.3 Symmetric Pumping

Pumping through a port on one side of the chamber creates an azimuthal pressure and flow asymmetry. Modern spacer-etch chambers pump symmetrically, through an annulus below the wafer to a pump directly underneath. The remaining asymmetries come from the wafer transfer slot, the coil feed, and gas injector placement. Chapter 13 discusses the residual azimuthal signatures these leave in spacer width.

---

## 5.5 Wall Temperature and Materials

### 5.5.1 Heated Liners

Hydrofluorocarbon chemistries deposit polymer on every surface, including chamber walls. Wall polymer:

- Consumes radicals (a sink) when it is growing
- Releases carbon and fluorine (a source) when it is etched
- Flakes into particles when thick

Heating the liners (typically 60–120°C) reduces polymer sticking coefficients and keeps wall deposits thin and stable:

```
Effect of liner temperature (illustrative, CH₃F/O₂ chemistry):

Liner T (°C)   Wall deposit rate    Wafer-to-wafer SiN rate drift
──────────────────────────────────────────────────────────────────
 40            High                 −3% over 25 wafers
 80            Medium               −1% over 25 wafers
120            Low                  < 0.5% over 25 wafers
```

### 5.5.2 Wall Coatings

```
Coating          Fluorine resistance   Particle risk   Notes
───────────────────────────────────────────────────────────────────
Anodized Al      Poor                  High (AlF₃)     Legacy
Y₂O₃ (plasma     Good                  Medium          Standard; converts
  spray)                                               to YOF at surface
Y₂O₃ (dense,     Very good             Low             Aerosol deposition,
  aerosol/PVD)                                         lower porosity
YOF / YF₃        Excellent             Low             Pre-fluorinated;
                                                       less first-wafer
                                                       effect
```

Chapter 9 covers wall conditioning in depth.

---

## 5.6 Gas Switching and Multi-Step Capability

Spacer recipes use 3–5 steps (Chapter 4.3.3). Every step change involves:

```
Transition sequence (typical):

1. Hold plasma on (avoids restrike transients) or turn off between steps
2. Change flows; wait for MFC settle (0.5–2 s)
3. Change pressure set point; throttle valve moves (0.5–2 s)
4. Change source/bias power; match network re-tunes (0.1–1 s)
5. Stabilization interval before the step's "count" begins

Total transition: 1–4 s per step change
```

On a 30–60 s process, 2–3 transitions take 5–15% of the plasma time and are not well controlled. Reactor features that shorten them include:

- Gas boxes close to the chamber (short lines, low dead volume)
- Fast-response throttle valves and pressure controllers
- Pre-set match positions per step (pre-tuned capacitor positions)
- Plasma-on transitions with ramped rather than stepped flows

---

## 5.7 Platform Configuration

```
Typical spacer-etch platform (illustrative):

           ┌───────────────┐
           │  Transfer     │
   ┌───────┤  module       ├───────┐
   │ PM1   │  (vacuum)     │  PM4  │
   │ etch  │               │  etch │
   ├───────┤               ├───────┤
   │ PM2   │               │  PM5  │
   │ etch  │               │ strip/│  ← in-situ polymer removal or
   ├───────┤               │ treat │    surface treatment before
   │ PM3   │               ├───────┘    air exposure
   │ etch  │               │
   └───────┴───────┬───────┘
                 Load locks / EFEM
```

**Post-etch treatment chamber.** A short, low-energy H₂/N₂ or O₂-lean plasma (or a remote-plasma treatment) removes residual fluorinated polymer before the wafer leaves vacuum. This lowers queue-time sensitivity: fluorine left on the surface reacts with moisture after air exposure and can form residues or corrode exposed materials. For low-k spacers, the treatment must be chosen to avoid carbon loss (Chapter 16).

---

## 5.8 Summary & Key Takeaways

1. **Spacer etch is a low-energy, high-flux process.** ICP-class reactors with independent low-power bias are the default.

2. **Flux comes from density.** Bohm flux at 10¹¹ cm⁻³ gives about 10¹⁶ ions/cm²·s, enough for 20–60 nm/min at low energy.

3. **There is an ion energy floor.** With zero bias, ions still gain about 5 T_e, roughly 16 eV in a typical ICP. Lower floors need low-T_e sources or pulsing.

4. **DF-CCP has uniformity and lower dissociation, but a higher energy floor.** It suits oxide SADP spacers better than damage-critical nitride spacers.

5. **Residence time shapes chemistry.** Short residence times keep the polymer balance tied to the feed gas and give sharper step transitions.

6. **Walls are part of the process.** Heated liners and Y₂O₃/YOF coatings keep wall polymer thin and stable, which reduces drift and particles.

7. **Multi-step recipes need fast transitions.** Gas, pressure, and match transitions can consume 5–15% of plasma time.

---

## Study Questions

1. Calculate the Bohm ion flux for T_e = 2.5 eV, M = 33 amu (an effective mass for a CH₃F/Ar mixture), n₀ = 6 × 10¹⁰ cm⁻³, and h = 0.5. Using the yield model of Chapter 3 with Y = 0.6 at the chosen energy and n = 9 × 10²² atoms/cm³, what SiN etch rate results?

2. For an O₂/CH₃F-rich plasma with effective mass 25 amu, calculate the zero-bias ion energy floor at T_e = 3.5 eV and at T_e = 1.5 eV.

3. A chamber of 35 L runs at 15 mTorr with 250 sccm total flow. Compute τ. If pressure is raised to 40 mTorr at the same flow, what is the new τ, and what happens to the by-product partial pressure (qualitatively)?

4. A 45 s spacer recipe has 3 step transitions of 2.5 s each. What fraction of plasma time is spent in transitions? If transitions are shortened to 1.0 s, how much does throughput improve for a chamber whose total wafer cycle is 75 s (including transfers)?

5. Explain why a DF-CCP with a 60 MHz source at 500 W cannot easily reach a 25 eV ion energy at the wafer, even with zero LF bias power.

---

**Previous Chapter:** [Chapter 4: Etch Chemistries for Spacer Materials](./04-etch-chemistries.md)  
**Next Chapter:** [Chapter 6: Ion Energy & Bias Control](./06-ion-energy-control.md)

---

**Chapter 5 Development Status:** Complete  
**Version:** 1.0
