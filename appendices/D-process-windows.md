# Appendix D: Process Windows & Lookup Tables

Starting points for design of experiments (DOE). These are **not** qualified recipes. Absolute values depend strongly on reactor design, chamber condition, and film. Use the trends and ranges to frame the DOE, then establish the window on your own hardware.

---

## D.1 Starting Recipes

### D.1.1 SiN Gate Spacer (ICP, Planar or Main FinFET Spacer)

```
Step           Gases (sccm)                    P        Source   Bias       Time
                                               (mTorr)  (W)      (W / eV)
──────────────────────────────────────────────────────────────────────────────────
Breakthrough   CF₄ 100 / Ar 100                5        500      50 / ~60   3 s
Main etch      CH₂F₂ 60 / O₂ 25 / Ar 200       15       700      70 / ~80   EP-onset
               (or CHF₃ 80 / O₂ 15 / Ar 150)
Soft landing   CH₃F 100 / O₂ 35 / He 200       30       500      40 / ~50   EP t₉₀
Overetch       CH₃F 100 / O₂ 25 / CO₂ 20 /     40       400      pulsed     30–60%
               He 300                                            D=0.3,     of ME
                                                                 ~45 peak
ESC: center 40°C / edge 45°C; liners 80–120°C
```

### D.1.2 SiOCN Low-k Gate Spacer

```
Differences from D.1.1:
  • Replace O₂ with CO₂ (or reduce O₂ by 50–70%) in soft landing and OE
  • Lower ESC temperature (20–30°C) to slow carbon depletion
  • Prefer pulsed source + bias in OE (lower O-atom density, less VUV)
  • In-situ post-treatment: N₂/H₂ remote or zero-bias, not O₂
  • Verify with dHF-decoration OCD (width loss after a fixed dHF dip)
```

### D.1.3 SiO₂ SADP Spacer on a-Si Mandrel

```
Main etch:   C₄F₈ 15 / Ar 300 / O₂ 8        20 mTorr, moderate bias
Overetch:    C₄F₆ 10 / Ar 300 / O₂ 6        20 mTorr, low bias, pulsed
Notes: polymer-rich for selectivity to a-Si mandrel top and
       underlying layer; watch footing (spacer CD = line CD)
```

### D.1.4 SiO₂ SADP Spacer on Carbon Mandrel

```
Main etch:   CF₄ 50 / CHF₃ 50 / Ar 200       10 mTorr, moderate bias
Overetch:    CHF₃ 60 / Ar 200 (no O₂)        15 mTorr, low bias
Notes: O₂-free once the mandrel top is exposed (Ch. 4.4.2)
```

### D.1.5 FinFET Fin-Spacer Pull-Down

```
After main gate-spacer etch (D.1.1 through soft landing):
Pull-down:   CH₃F 120 / O₂ 30 / He 300       40 mTorr, pulsed bias
             D = 0.2–0.3, peak ~40–60 eV; time set for remnant height
Optional:    quasi-ALE cycles for the last 5–10 nm of pull-down
Monitor:     fin-spacer remnant height (OCD/TEM), fin-top recess,
             STI recess, gate HM remaining
```

### D.1.6 GAA Inner-Spacer Etchback (Remote Plasma)

```
Remote source: NF₃ 20 / O₂ 200 / N₂ 100 / Ar 500, 0.5–2 Torr
Wafer: 10–30°C (lower T → more reaction-limited, better
       top-to-bottom uniformity)
Etch rate: target 2–5 nm/min (time-controlled, or cycled with pauses)
Monitor: inner-spacer indent (TEM top/middle/bottom sheet),
         sheet-end residue (TEM/EDS), Si sheet loss
```

---

## D.2 Sensitivity Lookup Table

Normalized sensitivities s = (%ΔY)/(%ΔX) around a centered CH₃F/O₂ SiN overetch. Positive means the output rises when the input rises.

```
Output \ Input       O₂     CH₃F   Pressure  Bias   Source  Wafer T  He/Ar
                                             power  power            fraction
─────────────────────────────────────────────────────────────────────────────
SiN rate             +0.5   −0.2   −0.3      +0.6   +0.4    +0.2     +0.1
Si rate              +1.8   −0.8   −0.6      +0.9   +0.5    +0.8     +0.2
S(SiN:Si)            −1.3   +0.6   +0.3      −0.3   −0.1    −0.6     −0.1
S(SiN:SiO₂)          −0.6   +0.4   +0.2      −0.4   −0.1    −0.3     ~0
Lateral loss         +1.2   −0.5   +0.4      −0.2   +0.3    +0.4     ~0
Foot height          −1.0   +0.7   +0.5      −0.8   −0.2    −0.5     −0.1
Facet rate           +0.2   −0.2   −0.2      +1.2   +0.3    +0.1     +0.4 (Ar)
Low-k depletion      +1.0   −0.3   +0.2      +0.2   +0.5    +0.5     ~0

(Illustrative magnitudes; establish your own with a DOE.)
```

---

## D.3 Specification Windows (Illustrative)

### D.3.1 By Application

```
Application            Width        Recess     HM loss   Foot     Other
                       tol. (3σ)    (max)      (max)     (max)
───────────────────────────────────────────────────────────────────────────────
Planar 28 nm main      ±1.0 nm      1.5 nm     10 nm     2 nm     —
  spacer
FinFET gate spacer     ±0.4 nm      1.0 nm     5 nm      0.5 nm   fin residue
  (7 nm class)                                                    ≤ spec
GAA gate spacer        ±0.3 nm      0.5 nm     5 nm      0.5 nm   Δk ≤ 0.2
GAA inner spacer       ±0.5 nm      0.2 nm     —         —        indent ≤ 1 nm,
                       (indent)     (sheet)                       no residue
SADP spacer (fin)      ±0.3 nm      —          —         0.3 nm   pitch walk
                                                                  ≤ 1 nm
```

### D.3.2 Overetch Sizing Quick Table

From OE ≥ (1+u_d)(1+u_e)(1+u_p) − 1 + u_t + t_foot/t_ME, with u_t = 0.03 and t_foot/t_ME = 0.15:

```
u_d    u_e    u_p=0.05   u_p=0.10   u_p=0.20   u_p=0.30
──────────────────────────────────────────────────────────
0.01   0.02   26%        31%        42%        52%
0.02   0.03   28%        34%        44%        55%
0.02   0.05   30%        36%        47%        57%
0.03   0.05   32%        37%        48%        59%
```

---

## D.4 DOE Templates

### D.4.1 Selectivity Window Mapping

```
Factors: O₂/CH₃F ratio (5 levels), wafer T (3 levels)
Fixed:   pressure, powers, total flow
Responses (blanket): SiN rate, Si rate, SiO₂ rate
Responses (patterned): w_mid, foot, recess (SOI), IDB
Runs: 15 + 3 center replicates
Output: contour plots of S(SiN:Si) and foot vs. ratio and T;
        window = overlap of S ≥ target and foot ≤ spec
```

### D.4.2 Overetch Robustness

```
Factors: OE time (−30%, 0, +30%), bias in OE (3 levels), pulse duty
         (2 levels)
Responses: recess, h_sp, HM loss, foot, w_mid
Runs: 18 (full factorial) or 9 (fractional) + replicates
Output: recess–OE curve slope and intercept (Ch. 11.4.3); choose the
        energy/duty with the lowest intercept (oxidation component)
```

---

**Appendix D Version:** 1.0  
**Last Updated:** 2026-10-04
