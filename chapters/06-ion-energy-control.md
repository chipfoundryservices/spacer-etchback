# Chapter 6: Ion Energy & Bias Control

## Overview

Ion energy is the most important single parameter in spacer etchback. It sets anisotropy, etch rate, selectivity, faceting, footing, hydrogen implantation depth, and lattice damage. Chapter 3 placed the useful range at roughly 30–150 eV. Chapter 5 showed that the reactor puts a floor of 15–25 eV under it. This chapter covers how bias hardware shapes the **ion energy distribution (IED)** inside that window, and why the **width** of the distribution matters as much as its mean.

A spacer etch with a mean ion energy of 80 eV and a bimodal IED spanning 30–130 eV behaves very differently from one with all ions at 80 ± 5 eV. The low-energy peak deposits polymer and leaves feet. The high-energy peak implants hydrogen and cuts facets. Narrowing the IED is one of the most effective hardware improvements for spacer etch.

**Learning Objectives:**
- Calculate sheath thickness and ion transit time for typical spacer-etch conditions
- Explain how bias frequency and sheath transit time set IED width
- Describe pulsed bias and calculate time-averaged ion energy and net etch rate
- Explain tailored-waveform bias and why it gives narrow IEDs
- Describe synchronous source/bias pulsing and the afterglow regime
- Relate ion energy to hydrogen implantation and silicon displacement thresholds

---

## 6.1 The Sheath at Low Bias

### 6.1.1 Sheath Thickness

For a high-voltage sheath, the Child-law thickness is:

```
s ≈ (√2 / 3) · λ_D · (2V_s / T_e)^(3/4)

λ_D = Debye length = 7430 · √(T_e[eV] / n[m⁻³])  meters

Example: n = 1 × 10¹⁷ m⁻³ (10¹¹ cm⁻³), T_e = 3 eV, V_s = 100 V
  λ_D = 7430 × √(3 / 10¹⁷) = 7430 × 5.48 × 10⁻⁹ ≈ 4.1 × 10⁻⁵ m = 41 µm
  (2V_s/T_e)^(3/4) = (66.7)^0.75 ≈ 23.3
  s ≈ 0.471 × 41 µm × 23.3 ≈ 0.45 mm
```

### 6.1.2 Ion Transit Time

```
τ_ion ≈ 3s · √(M / (2eV_s))

Example: Ar⁺ (M = 40 amu), s = 0.45 mm, V_s = 100 V
  √(M/(2eV_s)) = √(6.64 × 10⁻²⁶ / 3.2 × 10⁻¹⁷) ≈ 4.56 × 10⁻⁵ s/m
  τ_ion ≈ 3 × 4.5 × 10⁻⁴ × 4.56 × 10⁻⁵ ≈ 62 ns
```

---

## 6.2 Bias Frequency and IED Width

### 6.2.1 The Two Limits

The IED shape depends on how the ion transit time compares with the RF period τ_rf = 1/f:

```
τ_ion ≪ τ_rf (low frequency):
  Ions cross the sheath "instantly" and see the instantaneous voltage.
  IED is broad and bimodal, spanning nearly the full voltage swing:
     ΔE → 2 · e · V_rf   (V_rf = RF amplitude; the full peak-to-peak swing)

τ_ion ≫ τ_rf (high frequency):
  Ions respond to the time-averaged voltage.
  IED is narrow and centered on e·V̄_s:
     ΔE ≈ C · e · V_rf · (τ_rf / τ_ion),  C of order 1
```

### 6.2.2 The Spacer-Etch Problem

In high-density spacer etch plasmas, sheaths are thin and voltages are low, so **ions cross quickly**:

```
Bias frequency   τ_rf (ns)   τ_rf/τ_ion (τ_ion = 62 ns)   IED character
─────────────────────────────────────────────────────────────────────────
 400 kHz         2500        40                          Fully bimodal, ΔE ≈ 2eV_rf
 2 MHz            500         8                          Bimodal, very broad
13.56 MHz          74         1.2                        Bimodal, broad
 27 MHz            37         0.6                        Partially narrowed
 60 MHz            17         0.27                       Narrow-ish (but source-like)
```

Even at 13.56 MHz the IED is broad under typical spacer-etch conditions. Raising the bias frequency narrows it, but a high-frequency bias also starts to generate plasma itself, which couples ion energy back to flux.

```
Illustrative 13.56 MHz IED at 100 V mean sheath voltage, ~70 V RF amplitude:

  ion count
     │   ▄                       ▄
     │  ███                     ███
     │  ███▄                   ▄███
     │  █████▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄█████
     └──┴─────────────────────────┴──── energy (eV)
       ~40                       ~160
      low peak                 high peak

  Low peak (≈ E_th + small):  deposits polymer, slow etch → feet
  High peak (≈ 1.6 × mean):   implants H, sputters corners → facets
```

### 6.2.3 Mass Dependence

Lighter ions cross the sheath faster and see a broader IED. In a CH₃F/O₂/Ar plasma the ion mix includes H⁺, H₂⁺, H₃⁺, O⁺, O₂⁺, CHₓFᵧ⁺, and Ar⁺:

```
Ion      M (amu)   Relative τ_ion   IED width (relative)
──────────────────────────────────────────────────────────
H⁺       1         0.16             Very broad (nearly full swing)
H₂⁺      2         0.22             Very broad
O⁺       16        0.63             Broad
CH₂F⁺    33        0.91             Medium
Ar⁺      40        1.00             Medium (reference)
```

**Hydrogen ions get the full voltage swing.** Even if the mean ion energy is moderate, the H⁺ population reaches the peak sheath voltage. That is the energy that sets hydrogen implantation depth (Section 6.6, Chapter 12).

---

## 6.3 Pulsed Bias

### 6.3.1 Concept

Bias is switched on and off at kHz frequencies (typically 0.5–10 kHz) with duty cycle D:

```
Bias power
   │ ┌──┐     ┌──┐     ┌──┐
   │ │on│     │on│     │on│
   │ │  │ off │  │ off │  │
   └─┴──┴─────┴──┴─────┴──┴──→ time
     ←D·T→
     ←── T ──→

During ON:   ions at E_on (e.g., 100 eV) → etching
During OFF:  ions at E_floor (~15–20 eV) → below SiN threshold
             → polymer deposition, surface passivation
```

### 6.3.2 Time-Averaged Behavior

```
Mean ion energy (flux-weighted, constant flux):
  Ē = D · E_on + (1 − D) · E_floor

Net etch rate (simplified):
  R_net = D · R_on − (1 − D) · R_dep

Example:
  E_on = 120 eV, E_floor = 18 eV, D = 0.4
  Ē = 0.4 × 120 + 0.6 × 18 = 58.8 eV

  R_on (SiN) = 60 nm/min during ON, R_dep = 3 nm/min during OFF
  R_net (SiN) = 0.4 × 60 − 0.6 × 3 = 22.2 nm/min

  For Si (heavier polymer, lower R_on = 6 nm/min):
  R_net (Si) = 0.4 × 6 − 0.6 × 3 = 0.6 nm/min

  Selectivity S(SiN:Si) = 22.2 / 0.6 = 37
  (vs. continuous bias at equivalent mean energy: typically ~15)
```

The OFF phase deposits polymer on all surfaces. The ON phase removes it from nitride (where nitrogen helps consume it) faster than from silicon. Pulsing **amplifies** the polymer-thickness difference that drives selectivity. This is why pulsed bias is standard for spacer overetch steps.

### 6.3.3 Choosing Pulse Parameters

```
Parameter         Effect of increasing
─────────────────────────────────────────────────────────────────────────
Duty cycle D      Higher rate; less selectivity; behaves more like CW
Pulse frequency   Thinner polymer per cycle; smoother; less "ALE-like"
E_on              Faster etch per ON phase; more damage and faceting
OFF duration      More polymer per cycle; risk of net deposition on SiN

Guidance (illustrative):
  Polymer deposited per OFF phase should be ≈ 0.3–1 nm on Si and
  removed from SiN within the ON phase. If OFF deposition exceeds what
  ON removes on SiN, the etch stops (etch stop / "polymer runaway").
```

---

## 6.4 Tailored-Waveform Bias

### 6.4.1 Why Sinusoidal Bias Gives Broad IEDs

With a sinusoidal bias on a wafer that sits on a dielectric (the ESC), the wafer surface potential follows the sinusoid, and ions arriving at different phases see different voltages.

### 6.4.2 Pulse-Shaped Bias

A tailored waveform applies, for most of each period, a **negative voltage ramp** that compensates the charging of the wafer/ESC capacitance by the arriving ion current. The surface potential stays nearly constant, and all ions see the same sheath voltage. A short positive excursion at the end of each period lets electrons neutralize the accumulated charge:

```
Applied waveform (one period, ~2.5 µs at 400 kHz):

 V │
   │ ┐                                ┌┐
 0 │─┼────────────────────────────────┼┼───
   │ │╲                               ││
   │ │  ╲  ← ramp compensates          ││ ← short positive pulse:
   │ │    ╲   ion charging             ││   electrons neutralize
   │ │      ╲                          ││
   │ └────────╲────────────────────────┘│
   └──────────────────────────────────────→ t

Resulting wafer surface potential: ~flat → narrow IED

IED:   ion count
          │         █
          │        ███
          │        ███
          └────────┴┴┴──── energy
                  E_set ± a few eV
```

### 6.4.3 Benefits for Spacer Etch

```
Metric                    Sinusoidal 13.56 MHz     Tailored waveform
──────────────────────────────────────────────────────────────────────────
IED FWHM at 80 eV mean    ~60–100 eV (bimodal)     ~5–15 eV
Max H⁺ energy             ~140–160 eV              ~85–95 eV
Low-energy population     Large (feet)             Small
Selectivity at given rate Baseline                 Higher (fewer ions at
                                                   energies that etch Si
                                                   but barely etch SiN)
Faceting                  Baseline                 Reduced (no high tail)
```

A narrow IED lets the engineer place **all** ions in the window between the nitride threshold and the onset of damage, instead of placing the mean there and accepting tails on both sides.

---

## 6.5 Source Pulsing and the Afterglow

### 6.5.1 What Happens When the Source Turns Off

```
Time after source OFF     Electron temperature    Radical density   Ion flux
──────────────────────────────────────────────────────────────────────────────
0–5 µs                    Falls from ~3 eV → <1 eV   Unchanged       Falls
5–50 µs                   ~0.3–0.7 eV              Unchanged        Falls (τ ~ tens µs)
50 µs – 1 ms              Near thermal              Slowly decays   Low
(radical lifetimes are ms-scale; ion/electron loss is µs-scale)
```

### 6.5.2 Consequences

- **Lower T_e in the afterglow** reduces the plasma potential, so the ion energy floor drops from ~16 eV to a few eV.
- **Radicals persist**, so surface chemistry (polymer deposition, F adsorption) continues without ion bombardment.
- **Less dissociation on average.** With a lower duty-averaged T_e, CH₃F fragments less, which changes the polymer chemistry, often toward more selective, less fluorinated films.
- **Charging relief.** During the afterglow, electrons and negative ions can reach feature bottoms and neutralize positive charge built up during the ON phase (Chapter 12).
- **Less VUV.** VUV photon flux, which can damage low-k films and gate dielectrics, falls during the OFF phase.

### 6.5.3 Synchronous Source and Bias Pulsing

```
Mode                        Source        Bias          Character
──────────────────────────────────────────────────────────────────────────
Bias pulsing only           CW            Pulsed        Etch/deposit cycling
Synchronous (in phase)      Pulsed        Pulsed same   Low average damage,
                                                        afterglow passivation
Asynchronous / offset       Pulsed        Pulsed,       Bias during afterglow:
                                          delayed       low-T_e, low-flux,
                                                        controlled energy
                                                        (quasi-ALE behavior)
```

Bias applied in the afterglow, when the source is off, gives a regime of **low ion flux, controlled energy, and radical-saturated surfaces**. It is close to the conditions of an atomic layer etch removal step (Chapter 14). It is slow, and it is typically used only for the final soft-landing or overetch portion of a spacer etch.

---

## 6.6 Ion Energy and Substrate Damage Thresholds

### 6.6.1 Maximum Energy Transfer

In a binary collision, the maximum energy an ion of mass m transfers to a target atom of mass M is:

```
T_max = E · 4mM / (m + M)²

Silicon displacement threshold: E_d ≈ 13–20 eV (use ~15 eV)

Ion     m (amu)   4mM/(m+M)² (M = 28)   E needed to displace Si
─────────────────────────────────────────────────────────────────
H       1         0.133                  ~110 eV
He      4         0.438                  ~34 eV
C       12        0.840                  ~18 eV
O       16        0.926                  ~16 eV
F       19        0.963                  ~16 eV
Ar      40        0.969                  ~15 eV
```

### 6.6.2 Molecular Ion Break-Up

A molecular ion breaks apart on impact, and its kinetic energy is shared among the fragments roughly in proportion to their masses:

```
CH₂F⁺ at 100 eV (M = 33):
  C gets  12/33 × 100 ≈ 36 eV
  F gets  19/33 × 100 ≈ 58 eV
  each H gets 1/33 × 100 ≈ 3 eV   → negligible implantation

H⁺ at 100 eV:
  H gets the full 100 eV          → implants several nm into Si
```

**Atomic hydrogen ions are the damage driver**, not the hydrogen carried in heavy molecular ions. The H⁺/H₂⁺/H₃⁺ fraction in the ion flux, which rises with H₂ addition and with high dissociation, matters more than the total hydrogen content of the feed.

### 6.6.3 The Spacer-Etch Energy Window

```
Lower bound: E_th(SiN) ≈ 15–30 eV  (need net etch on nitride)
             plus margin for low-energy tail (feet)

Upper bound: Set by most restrictive of:
  • H⁺ implantation depth into Si (Chapter 12): often ~60–100 eV
  • Si displacement by heavy ions: >~15 eV, but surface polymer
    absorbs much of the energy at low E
  • Faceting of hard mask and spacer top: rises above ~100–150 eV

Practical window (peak ion energy, including the IED tail):
  Main etch:     60–150 eV   (film-covered substrate; damage moot)
  Soft landing:  40–80 eV
  Overetch:      25–60 eV    (substrate exposed; damage critical)
```

The window narrows as the substrate becomes exposed. A narrow-IED bias lets the overetch run close to the threshold without a tail that reaches into the damage regime.

---

## 6.7 Summary & Key Takeaways

1. **IED width matters as much as mean energy.** Low-energy tails cause feet. High-energy tails cause facets and damage.

2. **High-density, low-voltage sheaths are thin.** Ions cross in tens of nanoseconds, so 13.56 MHz bias still gives a broad, bimodal IED.

3. **Light ions see the full swing.** H⁺ reaches the peak sheath voltage regardless of mean energy, and it drives implantation damage.

4. **Pulsed bias amplifies selectivity.** OFF phases deposit polymer and ON phases etch. The cycle magnifies the polymer-thickness difference between nitride and silicon.

5. **Tailored waveforms narrow the IED.** A compensating ramp holds the wafer surface potential nearly constant, giving IED widths of 5–15 eV.

6. **Source pulsing exploits the afterglow.** Low T_e, persistent radicals, charge relief, and less VUV make afterglow-bias regimes suitable for soft-landing and overetch.

7. **Energy transfer limits set the upper bound.** H needs ~110 eV to displace Si but implants deeply at much lower energies. Heavy ions displace Si at ~15–20 eV but are mostly stopped by surface polymer.

---

## Study Questions

1. Calculate the sheath thickness and Ar⁺ transit time for n = 3 × 10¹¹ cm⁻³, T_e = 3 eV, V_s = 60 V. Is the IED at 13.56 MHz bias narrow or broad?

2. A pulsed bias runs at E_on = 100 eV, E_floor = 16 eV, D = 0.3. SiN etches at 55 nm/min and Si at 5 nm/min during ON. Polymer deposits at 2.5 nm/min on both during OFF. Calculate R_net for both and the selectivity. At what duty cycle does SiN net etch rate fall to zero?

3. For a sinusoidal bias with mean sheath voltage 90 V and RF amplitude 60 V in the low-frequency limit, what are the minimum and maximum ion energies for H⁺? Compare with a tailored waveform set to 90 ± 5 eV.

4. Using the T_max formula, what is the minimum He⁺ energy to displace Si (E_d = 15 eV)? Why might He diluent be preferred over Ar for overetch steps, and what is the risk?

5. A CHF₂⁺ ion (M = 51) strikes at 120 eV. Estimate the energy carried by the H atom and by each F atom. Compare with an H₃⁺ ion at 120 eV: what energy does each H atom carry?

6. Explain why bias applied during the source afterglow can reduce charging damage at the base of a tight gate-to-gate gap.

---

**Previous Chapter:** [Chapter 5: Etch Reactor Architecture for Spacer Etchback](./05-reactor-architecture.md)  
**Next Chapter:** [Chapter 7: Gas Delivery, Pressure & Radical Control](./07-gas-pressure-radicals.md)

---

**Chapter 6 Development Status:** Complete  
**Version:** 1.0
