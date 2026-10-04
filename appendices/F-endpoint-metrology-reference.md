# Appendix F: Endpoint & Metrology Reference

---

## F.1 OES Line Reference

```
Species   Wavelength (nm)       Transition / system           Use in spacer etch
────────────────────────────────────────────────────────────────────────────────────
CN        388.3 (band head)     B²Σ⁺ → X²Σ⁺ (violet, Δv=0)    SiN endpoint (primary)
CN        421.6                 B → X (Δv = −1)               SiN endpoint (alt.)
N₂        337.1                 C³Πu → B³Πg (2nd positive)    SiN endpoint (N₂-free
                                                              feed only)
N₂⁺       391.4                 B²Σu⁺ → X²Σg⁺ (1st negative)  N₂ plasma monitor
SiF       ~436–442              A²Σ⁺ → X²Π                    Si-containing film EP
CO        451.1, 483.5, 519.8   B¹Σ⁺ → A¹Π (Ångström)         Oxide EP; polymer/O
CF₂       ~250–320 (bands)      A¹B₁ → X¹A₁                   Polymer precursor
C₂        516.5                 d³Πg → a³Πu (Swan)            Polymer-rich indicator
CH        431.4                 A²Δ → X²Π                     H-C chemistry
Hα        656.3                 Balmer n=3→2                  H monitor
F         685.6, 703.7          3p → 3s                       F density (actinometry
                                                              with Ar 750.4)
O         777.4, 844.6          3p → 3s                       O density (actinometry
                                                              with Ar 750.4)
Ar        750.4, 811.5          4p → 4s                       Reference
He        587.6, 706.5          3d → 2p, 3s → 2p              Reference (He diluent)
```

### F.1.1 Actinometry

```
n_X / n_Ar ≈ K · (I_X / I_Ar)

Valid when the emitting states of X and Ar are excited mainly by direct
electron impact from the ground state, with similar threshold energies,
and quenching is negligible. F 703.7 / Ar 750.4 and O 844.6 / Ar 750.4
are common pairs. Use for trends, not absolute densities.
```

### F.1.2 Endpoint Settings Checklist

```
☐ Line(s) chosen: primary + normalization + backup
☐ Integration time / sampling: ≥ 5 points across the expected
  transition; synchronous sampling for pulsed plasmas
☐ Smoothing: moving average or Savitzky–Golay; check lag
☐ Trigger: normalized threshold or derivative; t_ref after plasma
  stabilization
☐ Timeouts: min and max times (e.g., nominal ±25%)
☐ Logging: t₁₀, t₅₀, t₉₀, Δt_EP, baseline S(t_ref) → SPC
```

---

## F.2 Metrology Capability Summary

```
Technique        Parameters                      Precision   Accuracy      Throughput
                                                 (3σ)        notes
──────────────────────────────────────────────────────────────────────────────────────
OCD (spectral    w_base/mid/top, h_sp, HM,       0.1–0.3 nm  Model-        High
  ellipsometry/  foot, recess, sidewall angle                dependent;
  reflectometry)                                             TEM-anchored
CD-SEM (top      Footprint, line width (SADP),   0.2–0.4 nm  Edge-         High
  down)          LER/LWR                                     algorithm
                                                             dependent
CD-SEM (tilt)    Qualitative profile             —           —             Medium
TEM / STEM       All profile metrics, a-Si,      ~0.2 nm     Reference     Very low
                 residue (EDS/EELS)
CD-AFM           Sidewall profile (open areas)   0.3–0.5 nm  Tip-limited   Low
Spectroscopic    Blanket film thickness,         0.02–0.05   Model-        High
  ellipsometry   SOI recess                      nm          dependent
XPS              Surface composition,            ~0.1 nm     Blanket       Medium
                 oxide thickness                 (oxide)     only
SIMS             H, F, C, dopant depth profiles  —           Depth         Very low
                                                             resolution
                                                             ~1 nm
TXRF / VPD-      Metal contamination             —           —             Medium
  ICPMS
```

---

## F.3 OCD Model Parameter Set (Gate Spacer)

```
Parameter               Float / fixed     Notes
───────────────────────────────────────────────────────────────────
Gate CD (L_g)           Float             Upstream variation
Gate height             Float
HM thickness (top)      Float
HM corner facet         Float             Often correlated with h_sp
Spacer w_mid            Float             Primary output
Spacer sidewall angle   Float             Or w_base & w_top separately
Spacer foot (h, w)      Float             Include when TEM shows feet
Spacer top height h_sp  Float
Si recess               Float             Correlates with foot; check
Spacer optical          Fixed (measured)  Refit if film changes
  constants (n, k)
Substrate stack         Fixed             From upstream metrology

Health metrics: χ² (goodness of fit), parameter correlations,
                parameter at limits (bound hits)
```

---

## F.4 Recommended SPC Charts

```
Chart                            Source           Frequency       Reaction
───────────────────────────────────────────────────────────────────────────────
Blanket SiN rate (mean, range)   Monitor wafer    Daily/chamber   Hold if OOC
Blanket Si rate / SOI recess     Monitor wafer    Daily/chamber   Hold if OOC
Particles (adders)               Monitor wafer    Daily/chamber   Hold if OOC
OCD w_mid (APC-corrected)        Production       Every lot       APC; hold on
                                                                  trend rules
OCD recess, h_sp, foot           Production       Every lot       Investigate
OCD χ²                           Production       Every lot       Model review
t₅₀ (endpoint time)              FDC              Every wafer     Investigate
Δt_EP (clearing spread)          FDC              Every wafer     Uniformity
                                                                  review
Bias voltage (standard step)     FDC              Every wafer     Wall/edge ring
He leak rate                     FDC              Every wafer     ESC/wafer check
OES baseline 388/750             FDC              Every wafer     Window/PM plan
Extreme-edge asymmetry           OCD (edge sites) Weekly          Edge ring
Epi defect density (downstream)  Inspection       Every lot       Damage/residue
                                                                  review
```

---

**Appendix F Version:** 1.0  
**Last Updated:** 2026-10-04
