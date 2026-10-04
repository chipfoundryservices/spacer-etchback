# Appendix G: Troubleshooting Guide

Symptom-driven guide for spacer-etch excursions. For each symptom: likely causes ranked from most to least common, checks to separate them, and corrective actions. Chapter references point to the underlying physics.

---

## G.1 Spacer Too Narrow

```
Likely causes                              Checks                              Actions
─────────────────────────────────────────────────────────────────────────────────────────────
1. Thin incoming film / low conformality   Pre-etch film metrology; TEM of     Feed-forward; fix
   (Ch. 2)                                 sidewall vs. field                  deposition
2. Lateral etch increase (O₂ high, T       O₂ MFC check; ESC zone temps;      Reduce O₂ or T in OE;
   high, wall freshly cleaned)             wafer # after WAC/PM               season walls
   (Ch. 7, 8, 9)
3. Excess overetch (endpoint late, APC     Endpoint trace t₅₀, Δt_EP; APC     Correct EP algorithm;
   overcorrecting)                         log                                 check OCD model
4. Low-k damage + clean (width lost        dHF-decoration test; compare        Reduce O; CO₂; lower T;
   in post-etch clean)                     pre/post-clean width                 N₂/H₂ post-treatment
   (Ch. 12.3)
```

## G.2 Spacer Too Wide / Feet

```
Likely causes                              Checks                              Actions
─────────────────────────────────────────────────────────────────────────────────────────────
1. Too much polymer (O₂ low, T low,        O₂ MFC; ESC temps; liner T;         Raise O₂ slightly or T;
   heavy wall polymer)                     WAC history                         restore WAC
2. Insufficient overetch / early EP        Endpoint trace; film thickness      Adjust OE; check film
3. Low-energy IED tail (bias drift,        Bias voltage trend; match           Fix RF; tailored bias;
   match issue)                            positions                           foot-trim step
4. Deposition fillet / breadloafing        TEM of as-deposited film            Deposition tuning
5. OCD model artifact (unmodeled foot)     OCD χ²; TEM correlation             Update OCD model
```

## G.3 Excess Si Recess

```
Likely causes                              Checks                              Actions
─────────────────────────────────────────────────────────────────────────────────────────────
1. Oxidation component high (O₂ high,      SOI monitor before/after dHF;       Earlier soft landing;
   energy high at first exposure)          XPS d_ox                            lower energy/O in OE
   (Ch. 11.2.2)
2. Fresh walls (post-WAC/PM, first         Recess vs. wafer # after clean      Add season step;
   wafer)                                                                      seasoning criteria
3. Overetch longer (EP drift, APC)         t_EP trend; APC log                 Fix EP/APC
4. Temperature high (He leak, zone drift)  He leak trend; zone temps           ESC/He check
5. Damaged layer removal (H energy up)     Epi defects; SIMS on monitor        Lower bias; narrow IED;
                                                                               avoid H₂
```

## G.4 Spacer Top / HM Loss, Mushroom Defects

```
Likely causes                              Checks                              Actions
─────────────────────────────────────────────────────────────────────────────────────────────
1. Thin HM from upstream gate etch         HM thickness pre-spacer (OCD)       Module budget; gate
   (Ch. 10.3.4)                                                                etch correction
2. Overetch too long (pull-down)           OE time, t_EP trend                 Reduce needed OE
                                                                               (uniformity)
3. Faceting increased (bias up, Ar         Bias V; Ar MFC; IED settings        Lower energy; He
   fraction up)                                                                instead of Ar
4. Edge-only: edge-ring wear (tilt)        Edge OCD vs. ring hours             Ring adjust/replace
```

## G.5 Wafer-Edge Excursions

```
Symptom                         Likely cause                 Check                     Action
──────────────────────────────────────────────────────────────────────────────────────────────
Edge spacer asymmetry (L/R)     Edge-ring wear (ion tilt)    Ring RF-hours; edge OCD   Raise/replace ring
Edge recess high                He leak → edge hot;          He leak; zone temps       ESC check; edge
                                edge clears early                                      tuning gas
Edge foot / residue             Edge polymer high; edge      Edge rate map; tuning     Edge O₂ tuning gas;
                                rate low                     gas flow                  zone T
Edge width drift over PM        Ring wear + wall state       Trend vs. RF-hours        APC edge offset;
  cycle                                                                                PM interval
```

## G.6 Iso-Dense Bias Out of Spec

```
Likely causes                              Checks                              Actions
─────────────────────────────────────────────────────────────────────────────────────────────
1. Polymer balance shifted (O₂/CH₃F        O₂ MFC; wall state                  Retune ratio (Ch. 13.1.3)
   ratio drift)
2. Deposition conformality changed         TEM dense vs. iso sidewall          Deposition fix
3. Pressure drift (sidewall radical        Gauge zero; throttle position       Re-zero gauge
   supply)
4. New product with different array        Product layout                      Product-specific APC
   environment                                                                 offset
```

## G.7 Wafer-to-Wafer / First-Wafer Drift

```
Pattern                         Likely cause                     Action
─────────────────────────────────────────────────────────────────────────────────────
First 1–3 wafers of lot differ  Wall state after idle            Season step; dummy
                                                                 wafers after idle
Saw-tooth every N wafers        WAC every N wafers               WAC every wafer or
                                                                 condition-based WAC
Slow drift over days            Window clouding, liner           Track OES baseline;
                                deposits, edge ring              PM planning; APC
Step change after PM            Incomplete seasoning;            Seasoning endpoint;
                                part mismatch                    re-qualify
Random wafer outliers           He leak, chucking, particles     FDC on He leak;
                                                                 ESC inspection
```

## G.8 Endpoint Problems

```
Symptom                         Likely cause                     Action
─────────────────────────────────────────────────────────────────────────────────────
EP not detected (timeout)       Window clouding; wrong line;     Clean/replace window;
                                small exposed area               normalized algorithm;
                                                                 multivariate EP
EP early                        Signal noise; transition         Smoothing; trigger
                                artifact                         delay after step change
EP time drifting                Film thickness or rate drift     Check deposition;
                                                                 monitor rate
Δt_EP widening                  Uniformity degrading             Edge ring, ESC zones,
                                                                 gas split, film WIW
```

## G.9 Defects and Downstream Signatures

```
Downstream signature            Spacer-etch suspects             First checks
─────────────────────────────────────────────────────────────────────────────────────
Epi stacking faults/voids       C/F residue; H damage;           Post-treatment step;
                                post-PM wall state               bias/IED; PM timing
Mushroom defects                HM/spacer-top loss; facets       HM budget; OE; edge ring
Gate–contact shorts (SAC)       Thin spacer top; low-k skin      w_top (TEM); dHF decor.
C_gc high                       Low-k carbon depletion           XPS/dHF decoration; O₂
R_ext high (pFET especially)    Recess; B passivation by H       SOI recess; H energy
Particles (fall-on pattern)     Wall polymer flaking             WAC; liner condition
Metal contamination             Coating erosion                  VPD-ICPMS; coating
                                                                 inspection
```

## G.10 GAA Inner-Spacer Specific

```
Symptom                           Likely cause                       Action
─────────────────────────────────────────────────────────────────────────────────────
Residue on Si sheet ends (no epi) Underetch; by-product residue      Increase D slightly;
                                                                     post-clean
Plug indent too deep / seam open  Overetch; low-density seam         Reduce D; denser
                                                                     film; cyclic etch
Top sheets indented more than     Transport-limited etchant          Lower T / reactivity;
  bottom                                                             cyclic removal
Si sheet thinning                 Selectivity too low                Adjust NO/O
                                                                     passivation; lower T
Exposed SiGe after etch           Recess non-uniform + overetch      SiGe recess control
```

---

## G.11 Escalation Path

```
1. Hold the chamber; quarantine affected lots
2. Check FDC and SPC: what changed (sensor, consumable hours, PM,
   recipe, incoming film)?
3. Run monitors: blanket rates, SOI recess, particles
4. If unresolved: patterned short loop + TEM
5. Restore: fix root cause → re-qualify (Appendix C.2/C.3) → release
6. Document: root cause, signature, detection lag; update FDC limits or
   this guide
```

---

**Appendix G Version:** 1.0  
**Last Updated:** 2026-10-04
