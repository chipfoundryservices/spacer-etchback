# Appendix C: Standard Operating Procedures

Representative procedures for running and qualifying a spacer-etch chamber. Limits are illustrative. Each fab sets its own from baseline data, typically mean ± 3σ of a stable reference period.

---

## C.1 Daily Chamber Check

```
Time required: ~20 minutes (plus monitor wafer run time)
Performed by: Equipment technician; reviewed by process engineer

1. Vacuum and leak (3 min)
   ☐ Base pressure ≤ spec (e.g., < 0.5 mTorr after 5 min pump)
   ☐ Rate-of-rise ≤ spec (e.g., < 1 mTorr/min, valves closed)
     Fail → leak check before any production

2. Pressure gauge zero (2 min)
   ☐ Zero capacitance manometer at base pressure
   ☐ Record zero offset; trend it. A jump > 0.2 mTorr → investigate

3. Gas delivery (3 min)
   ☐ MFC zero readings at no-flow (all within ±0.5% FS)
   ☐ Critical low-flow MFC (O₂, edge tuning gas) rate-of-rise check
     if available

4. RF and match (3 min)
   ☐ Run standard Ar plasma check step (fixed power, pressure)
   ☐ Record bias voltage, reflected power, match positions
   ☐ Compare to baseline: bias voltage within ±3%; reflected < spec

5. ESC and thermal (3 min)
   ☐ ESC zone temperatures at set point ±0.5°C (idle)
   ☐ He leak rate with test wafer ≤ spec (e.g., < 1 sccm)
   ☐ Chiller flow and temperature normal

6. OES baseline (2 min)
   ☐ Ar 750 nm intensity in standard step vs. last clean
   ☐ 388/750 ratio in standard step (window transmission tracking)

7. Monitor wafers (run time)
   ☐ Blanket SiN rate (49 sites): mean, range
   ☐ SOI recess monitor (Appendix C.4)
   ☐ Particle adders on bare Si (> 32–45 nm)

Result: Log all values to SPC. Any out-of-control point → hold chamber.
```

---

## C.2 Recipe Qualification (New or Modified Recipe)

```
Time required: 1–3 days including TEM

Step 1: Blanket rates (½ day)
  Wafers: blanket SiN (or spacer film), Si (or SOI), SiO₂, HM film
  Run each recipe step separately for a fixed time
  Measure: rate maps (49 sites), selectivities per step

Step 2: Patterned short loop (1 day)
  Wafers: product or test-reticle wafers through spacer deposition
  Run full recipe at nominal and at ±20% overetch
  Measure: OCD (w_base, w_mid, w_top, h_sp, HM, foot, recess) at
           9–17 sites; CD-SEM for SADP
  Inspect: post-etch defect scan

Step 3: Cross-section (½–1 day)
  TEM at center, mid-radius, edge; dense and isolated; for nominal and
  +20% OE
  Confirm: profile metrics, recess, a-Si layer, residue

Step 4: Clean compatibility
  Run production post-etch clean and pre-epi clean on qualified wafers
  Re-measure spacer width (low-k skin check via width loss)

Step 5: Downstream check (if new film or major change)
  Short loop through S/D epitaxy; post-epi defect inspection

Release criteria (illustrative):
  ☐ All profile metrics within spec at nominal and ±20% OE
  ☐ Recess ≤ budget at +20% OE
  ☐ WIW range within spec
  ☐ No new defect types
  ☐ OCD model χ² within limits (model valid for this profile)
```

---

## C.3 Post-PM Recovery

```
1. Mechanical completion
   ☐ Parts replaced logged (liner, window, edge ring, ESC, etc.)
   ☐ Torque and alignment checks per tool manual

2. Pump-down and leak check
   ☐ Base pressure and rate-of-rise within spec

3. Bake-out
   ☐ Liners/window at maximum service temperature 1–4 h under vacuum
   ☐ Monitor water peak (RGA, if available) until stable

4. Plasma conditioning (30–60 min)
   ☐ Alternating O₂ and NF₃-based plasmas (waferless or cover wafer)

5. Seasoning
   ☐ Run production recipe (with WAC) on seasoning wafers
   ☐ Track seasoning monitor (OES ratio, bias V) per wafer
   ☐ Stop when monitor is within ±2% of seasoned baseline for
     3 consecutive wafers (typically 25–100 wafers)

6. Qualification
   ☐ Particles: adders within spec on 2 consecutive bare-Si wafers
   ☐ Metals: VPD-ICPMS or TXRF on bare Si within spec (Y, Al, Fe, Ni,
     Cu, etc.)
   ☐ Rates: blanket SiN, Si, SiO₂ within ±2–3% of fleet reference
   ☐ SOI recess within ±0.1 nm of fleet reference
   ☐ Patterned OCD within spec; TEM for major PM (ESC, edge ring
     design change)

7. APC
   ☐ Reset or re-initialize chamber offset (â) using qualification
     results; widen λ temporarily if the controller supports it

8. Release to production; flag first 2 production lots for extra
   sampling
```

---

## C.4 SOI Recess Monitor

```
Purpose: Daily measurement of total Si recess (direct + oxidation)
Wafers:  SOI with top Si 10–20 nm, coated with spacer film of nominal
         thickness (or bare SOI for overetch-step-only monitor)

1. Pre-measure top-Si thickness (spectroscopic ellipsometry, 49 sites)
2. Run full spacer recipe (or the overetch step alone, fixed time)
3. Measure top-Si thickness again (with surface-oxide layer in model)
   → Δ_direct (and oxide thickness d_ox)
4. Apply production dHF clean
5. Measure top-Si thickness again → total recess (Δ_direct + Δ_oxidation)

Report: mean recess, range, radial profile, d_ox
Limits: chamber-specific; e.g., 0.70 ± 0.10 nm total
Trend: recess rising with RF-hours → wall/edge-ring drift
```

---

## C.5 Edge-Ring Replacement or Adjustment

```
Trigger: RF-hours limit, or extreme-edge metric out of control
         (edge spacer asymmetry, edge recess, edge width)

1. Record pre-change extreme-edge OCD (r = 140–148 mm) and asymmetry
2. Replace or raise ring per procedure
3. Short season (10–25 wafers or equivalent RF time)
4. Re-measure extreme-edge OCD; verify asymmetry ≤ spec
5. Reset edge-specific APC offsets
```

---

## C.6 OCD–TEM Correlation

```
Frequency: Each OCD model release; after recipe or film changes;
           quarterly for stable processes

1. Select 3 wafers spanning the process range (e.g., OE −20%, 0, +20%)
2. Measure OCD at selected sites (dense, isolated; center, edge)
3. Prepare TEM lamellae at the same sites
4. Measure TEM: w_base, w_mid, w_top, h_sp, HM, foot, recess
5. Regress OCD vs. TEM per parameter:
   ☐ Slope 0.9–1.1, offset < 0.2 nm, R² > 0.9 (illustrative)
6. If failing: add or float parameters (foot, facet, recess), refit
   optical constants on actual films, re-validate
```

---

**Appendix C Version:** 1.0  
**Last Updated:** 2026-10-04
