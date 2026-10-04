# Chapter 15: Endpoint, Metrology & Advanced Process Control

## Overview

The previous fourteen chapters described what a spacer etch should do. This chapter covers how a production line knows it did it, wafer after wafer and chamber after chamber. Three tools carry that load:

1. **Endpoint detection**, which decides in real time when the field film has cleared, so the recipe can switch to its soft-landing and overetch steps.
2. **Metrology**, which measures spacer width, profile, and recess on sampled wafers and feeds models with ground truth.
3. **Advanced process control (APC)**, which uses deposition data, endpoint traces, and metrology to adjust each run and keep the fleet centered.

Spacer etch is an unusually good fit for APC. The input film thickness is measured on every lot, the etch is short and repeatable, and the outputs (width, recess) respond almost linearly to a few knobs (time, O₂, temperature).

**Learning Objectives:**
- Select OES lines for nitride and oxide spacer endpoint and interpret their transitions
- Use endpoint transition width as a wafer-scale clearing-uniformity monitor
- Apply real-time reflectometry to switch steps at a set remaining thickness
- Compare OCD, CD-SEM, TEM, and AFM for spacer metrology and plan sampling
- Design feed-forward and EWMA feedback controllers for spacer etch
- Use FDC and virtual metrology on chamber sensor data

---

## 15.1 Optical Emission Endpoint

### 15.1.1 Useful Emission Lines

```
Species   Wavelength (nm)          Behavior at SiN clear      Use
────────────────────────────────────────────────────────────────────────
CN        388.3 (violet band head) ↓ sharply                  Primary SiN EP
N₂        337.1 (2nd positive)     ↓                          SiN EP (N₂-free
                                                              feed only)
SiF       ~440 (band)              ↓                          SiN/SiO₂ EP
CO        451.1, 483.5, 519.8      ↑ or ↓ (polymer/O balance) Oxide EP; polymer
                                                              indicator
F         703.7                    ↑ (less consumption)       Generic clearing
O         777.4, 844.6             ↑ (less consumption)       O balance monitor
H (Hα)    656.3                    ~ / ↑                      H chemistry monitor
Ar        750.4, 811.5             Reference (actinometry)    Normalization
C₂        516.5 (Swan)             Polymer-rich indicator     Residue risk
```

For SiN spacers in CH₃F/O₂, **CN at 388 nm** is the standard endpoint line. It comes directly from nitrogen leaving the film combined with carbon from the polymer. When the nitride clears, its source disappears.

### 15.1.2 Normalization

Ratioing to a reference line removes the effect of plasma intensity drift and window clouding:

```
Signal S(t) = I_CN(388) / I_Ar(750)

Using a ratio of two lines also partly cancels window transmission
drift, though not completely, because transmission is wavelength-
dependent. Window clouding from polymer deposition affects UV/blue
lines (388 nm) more than red lines (750 nm), so the ratio still
drifts slowly over a PM cycle. Track baseline S(0) over time.
```

### 15.1.3 The Endpoint Trace

Because the spacer film is nearly blanket, the CN signal is strong and its drop is large. The drop is **not** instantaneous. It spans the time from first clearing to last clearing across the wafer:

```
S(t)
1.0 ┤────────────────╮
    │                 ╲
    │                  ╲       ← transition: regions clearing
    │                   ╲         across the wafer
0.5 ┤                    ╲
    │                     ╲
    │                      ╲___
0.2 ┤                          ‾‾‾‾‾‾────── (residual: sidewalls,
    │                                         spacer tops still
    └─────────────────┬─────┬──────────       etching)
                     t₁₀   t₉₀            time

t₁₀: signal has dropped 10% of the total drop → first regions cleared
t₉₀: signal has dropped 90% → most of the wafer cleared
Δt_EP = t₉₀ − t₁₀ → wafer-scale clearing spread
```

### 15.1.4 Transition Width as a Uniformity Monitor

```
Clearing spread (fraction) ≈ Δt_EP / t₅₀

Example:
  t₁₀ = 18.5 s, t₅₀ = 20.0 s, t₉₀ = 21.6 s
  Δt_EP = 3.1 s → spread ≈ 15.5% of main-etch time

  Tracked over lots: a rise from 15% to 20% means uniformity has
  degraded (edge ring wear, ESC zone drift, film non-uniformity),
  even before metrology shows a width or recess change.
```

### 15.1.5 Endpoint Algorithms

```
Algorithm                   Trigger                         Robustness
────────────────────────────────────────────────────────────────────────
Threshold on S(t)           S falls below fixed level       Sensitive to baseline
                                                            drift
Threshold on normalized     S(t)/S(t_ref) < k               Better; t_ref early
  signal                                                    in main etch
First derivative            dS/dt minimum (steepest drop)   Good; noise-sensitive
                                                            → smoothing needed
Multivariate (PCA/PLS on    Score crosses threshold         Best SNR; needs
  full spectrum)                                            training data
```

Common practice for spacer etch:

- Detect **t₁₀ (onset)** to switch from main etch to soft landing (Chapter 11.4.1)
- Detect **t₉₀** (or a derivative-based "end") to start a **fixed or proportional** overetch: t_OE = k × t_ME or t_OE = constant
- Set **timeouts**: if endpoint is not detected within t_nominal × (1 ± 25%), stop and alarm

### 15.1.6 Signal-to-Noise Considerations

```
SNR ≈ ΔS / σ_noise

ΔS for blanket SiN spacer etch: large (50–80% drop) → SNR > 50 typical
Problems arise when:
  • Exposed area is small (masked/partial spacer steps)
  • Step transitions coincide with endpoint (signal disturbed)
  • Pulsed plasma: sample synchronously with the pulse or average over
    many periods
```

---

## 15.2 Reflectometry and Interferometry

### 15.2.1 Thin-Film Case

For a few-nanometer film, interferometric fringes do not appear (one fringe requires a thickness change of λ/2n ≈ 100+ nm). Spectral reflectometry still works: the reflectance spectrum changes measurably with thickness and is fitted to a thin-film model in real time:

```
Broadband reflectometry endpoint:

  Measure R(λ) every 100–200 ms on a blanket-like area (or the
  wafer average for a blanket-dominated pattern)
  Fit remaining film thickness d(t) with a stack model
  Trigger: d(t) ≤ d_switch (e.g., 1.5 nm) → switch to soft landing

Advantages over OES:
  • Triggers BEFORE clearing (OES only sees clearing after it starts)
  • Directly measures remaining thickness at a known location

Limitations:
  • Measures one spot (or an average), not wafer extremes
  • Patterned areas need effective-medium or RCWA models
```

### 15.2.2 Combining Reflectometry and OES

```
Hybrid scheme:
  Main etch → stop on reflectometry d ≤ 1.5 nm
  Soft landing → stop on OES t₉₀
  Overetch → fixed time (or proportional to Δt_EP)

Using Δt_EP to size overetch:
  t_OE = t_OE,base + α × (Δt_EP − Δt_EP,ref)
  → wafers with wider clearing spread get more overetch automatically
```

---

## 15.3 Spacer Metrology

### 15.3.1 Techniques

```
Technique       Parameters                     Precision   Throughput   Role
──────────────────────────────────────────────────────────────────────────────
OCD             w (base/mid/top), h_sp, HM,    0.1–0.2 nm  High         Production
(scatterometry) foot, recess (model params)                             control
CD-SEM          Footprint width, LER           0.2–0.4 nm  High         Production;
                                                                        SADP lines
Tilt-SEM        Qualitative profile, foot      —           Medium       Excursion
TEM             Everything (local)             ~0.2 nm     Very low     Reference,
                                                                        model anchor
CD-AFM          Sidewall profile (open areas)  0.3–0.5 nm  Low          Reference
XPS             Surface composition (blanket)  —           Medium       Damage
SOI ellipsometry Recess (blanket)              0.05 nm     High         Recess
                                                                        monitor
```

### 15.3.2 OCD Model Maintenance

OCD reports the parameters its model contains. When the profile changes in a way the model does not capture, the error moves into other parameters:

```
Example: foot appears (1.5 nm) but model has no foot parameter
  → fitted w_mid increases by ~0.3 nm, h_sp shifts
  → APC "sees" wider spacers and lengthens overetch
  → recess increases, while the true w_mid has not changed

Mitigation:
  • TEM correlation every model release and after major recipe changes
  • Include foot, facet, and recess as floating parameters
  • Monitor goodness-of-fit (χ²) as an SPC parameter; a χ² rise flags
    unmodeled profile change
```

### 15.3.3 Sampling Plan

```
Measurement            Frequency (illustrative)
────────────────────────────────────────────────────────────────
Pre-etch film (field)  Every wafer or every lot (feed-forward)
OCD post-etch          2–5 wafers/lot × 9–17 sites
CD-SEM (SADP)          1–2 wafers/lot × 5–9 sites
SOI recess monitor     Daily per chamber
Blanket rate monitors  Daily per chamber (SiN, Si, SiO₂)
TEM                    Weekly per product/chamber group, and on excursion
```

---

## 15.4 Advanced Process Control

### 15.4.1 Control Structure

```
            ┌───────────────┐
 film t ───▶│ Feed-forward  │──┐
 (dep tool) │ model         │  │
            └───────────────┘  ▼
                         ┌──────────────┐     ┌────────────┐
 previous runs ─────────▶│ Recipe       │────▶│ Etch       │──▶ wafer
 (feedback, EWMA)        │ adjustment   │     │ chamber    │
                         └──────────────┘     └─────┬──────┘
                                ▲                   │ OES, RF, sensors
                                │                   ▼
                         ┌──────┴───────┐     ┌────────────┐
                         │ Feedback     │◀────│ Metrology  │
                         │ controller   │     │ (OCD, SOI) │
                         └──────────────┘     └────────────┘
```

### 15.4.2 Feed-Forward on Film Thickness

```
Main-etch time (if not endpointed):
  t_ME = t_film / R̂

where R̂ is the controller's current estimate of the etch rate.

If endpointed, feed-forward adjusts:
  • Endpoint timeout window (expected t₅₀ ± margin)
  • Overetch, if film thickness non-uniformity is measured:
    t_OE = t_OE,base × (1 + β × (u_film − u_film,ref))
```

### 15.4.3 EWMA Feedback

```
Model:  y_k = a + b · u_k + noise
  y = measured output (e.g., spacer width), u = knob (e.g., O₂ flow or
  overetch time), a = drifting offset, b = gain (from DOE)

EWMA estimate of offset:
  â_k = λ (y_k − b·u_k) + (1 − λ) â_{k−1}

Next run:
  u_{k+1} = (y_target − â_k) / b

λ: 0.2–0.5 typical. Larger λ responds faster but passes more noise.

Example (spacer width via overetch time):
  b = −0.03 nm/s (width falls 0.03 nm per second of overetch)
  target y = 7.00 nm, current u = 8.0 s, measured y = 7.12 nm
  â_prev = 7.25 nm
  y − b·u = 7.12 + 0.24 = 7.36
  â = 0.3 × 7.36 + 0.7 × 7.25 = 7.283
  u_next = (7.00 − 7.283) / (−0.03) = 9.4 s
```

### 15.4.4 Choosing the Control Knob

```
Output to control       Preferred knob             Why
────────────────────────────────────────────────────────────────────────
Spacer width            O₂ flow (soft landing) or   Linear; small side
                        ESC temperature             effects on recess
Recess                  Overetch time or energy     Direct; check width
                                                    side effect
Clearing uniformity     Edge tuning gas, ESC zones  Spatial knobs
Edge width/asymmetry    Edge-ring height/bias       Edge-specific
```

Avoid using **overetch time** to control width if recess is near its limit. Width gains from longer overetch come at a recess cost (Chapter 11). Use a knob that is "orthogonal" to the most constrained output.

### 15.4.5 Multi-Chamber Matching

```
Chamber offsets: each chamber gets its own â (offset), sharing b (gain)
Fleet target:    all chambers centered on y_target

Matching checks (illustrative):
  Blanket SiN rate:     ±2% chamber-to-chamber
  Blanket Si rate:      ±5%
  OCD spacer width:     ±0.15 nm after APC
  SOI recess:           ±0.1 nm

Hardware-level matching first (MFC, gauge, ESC calibration, Ch. 7–8),
APC offsets second. APC should not hide a hardware problem.
```

---

## 15.5 FDC and Virtual Metrology

### 15.5.1 Fault Detection and Classification (FDC)

```
Sensor                      Typical fault indicated
──────────────────────────────────────────────────────────────────
Bias voltage / RF match     Wall state change, edge-ring wear,
  positions                 arcing
He backside leak            Wafer bow, particles, ESC wear
ESC zone heater power       Thermal drift, coolant issues
Throttle valve position     Pump degradation, leak, flow error
OES baseline (S at t_ref)   Window clouding, chemistry drift
Endpoint time t₅₀           Film thickness or rate change
Endpoint spread Δt_EP       Uniformity degradation
```

FDC limits are set on run-level summaries (mean, slope, max) of each sensor trace, using SPC rules. A run out of limits holds the wafer for metrology before it proceeds.

### 15.5.2 Virtual Metrology (VM)

VM predicts metrology outputs from sensor data on wafers that are not measured:

```
ŷ_VM = f(OES features, RF features, t_EP, Δt_EP, ESC temps, film t)

Uses:
  • Fill in unmeasured wafers for APC (more frequent feedback)
  • Flag wafers for measurement when ŷ_VM is near limits
  • Track chamber health between PMs

Validation:
  • VM residual (ŷ_VM − y_measured) monitored on sampled wafers
  • Retrain after PM, hardware change, or recipe change
```

---

## 15.6 Summary & Key Takeaways

1. **CN at 388 nm is the standard SiN spacer endpoint.** Normalize to an Ar line and track the baseline over the PM cycle.

2. **The endpoint transition width measures uniformity.** Δt_EP grows when wafer-scale clearing spreads, often before metrology sees it.

3. **Reflectometry can trigger before clearing.** Switching at a measured remaining thickness keeps silicon away from main-etch conditions.

4. **OCD needs its model maintained.** Unmodeled feet or facets move error into reported widths. Anchor to TEM and watch goodness-of-fit.

5. **Spacer etch suits APC.** Measured input thickness, short repeatable etches, and nearly linear responses make feed-forward and EWMA feedback effective.

6. **Choose control knobs orthogonal to the tightest constraint.** Do not buy width with overetch when recess is near its limit.

7. **FDC and VM extend control between measurements.** Bias voltage, He leak, endpoint time and spread, and OES baselines are the key sensor features.

---

## Study Questions

1. A CN/Ar endpoint trace has t₁₀ = 16.2 s, t₅₀ = 17.5 s, t₉₀ = 19.4 s. Calculate the clearing spread. If the reference spread is 14%, what overetch adjustment would you make using t_OE = t_OE,base + α(Δt_EP − Δt_EP,ref) with α = 1.5 and t_OE,base = 8 s?

2. Window clouding reduces 388 nm transmission by 0.4% per wafer and 750 nm by 0.1% per wafer. After 300 wafers, by how much has the CN/Ar baseline ratio drifted? What fixed threshold would fail first, and how would a normalized-to-t_ref algorithm behave?

3. Using the EWMA controller of Section 15.4.3 with λ = 0.4 and b = −0.025 nm/s, compute the next overetch time if â_prev = 7.18 nm, u = 9.0 s, and y = 7.05 nm (target 7.00 nm).

4. OCD reports w_mid rising by 0.25 nm over a week while TEM shows constant w_mid and a growing foot. Explain how APC would respond if it controls width with overetch time, and what would happen to recess.

5. Propose a VM model for Si recess using available sensor features. Which three features do you expect to carry the most information, and why?

---

**Previous Chapter:** [Chapter 14: Advanced Etchback — FinFET, GAA Inner Spacers & SADP/SAQP](./14-advanced-etchback.md)  
**Next Chapter:** [Chapter 16: Integration, Yield & Cost of Ownership](./16-integration-yield-coo.md)

---

**Chapter 15 Development Status:** Complete  
**Version:** 1.0
