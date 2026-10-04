# Chapter 9: Chamber Wall Conditioning & Seasoning

## Overview

A spacer-etch chamber has a large internal surface area. Liners, window, showerhead or injector, and edge-ring hardware together can exceed the wafer area by a factor of ten or more. In polymerizing CH₃F/O₂ chemistry, all of these surfaces take part in the process. They adsorb radicals, deposit polymer, release carbon and fluorine when that polymer is etched, and recombine O atoms at rates that depend on their state.

The wafer sees a plasma whose chemistry is partly set by **the walls' history**. A spacer recipe that is perfectly centered on a seasoned chamber can produce feet on the first wafer after a clean, or excess recess after a long idle. This chapter covers how walls affect the polymer balance, how waferless autoclean (WAC) and seasoning reset and stabilize them, and how to recover a chamber after preventive maintenance.

**Learning Objectives:**
- Explain how wall polymer acts as a radical sink and source
- Quantify the effect of wall recombination probability on O-atom density
- Design a waferless autoclean (WAC) and seasoning strategy for spacer chemistry
- Identify first-wafer and post-idle effects and their signatures
- Plan PM recovery and chamber qualification
- Manage particle risk from wall deposits and coatings

---

## 9.1 The Walls as a Process Participant

### 9.1.1 Area Ratio

```
Surface                      Approximate area (cm²)
──────────────────────────────────────────────────────
Wafer (300 mm)               707
Chamber liner                3000–5000
Dielectric window / lid      1000–1500
Edge ring and hardware       300–600
Pumping baffle               500–1500
────────────────────────────────────────────────────
Total non-wafer area         ~5000–8500 (7–12× wafer)
```

### 9.1.2 Radical Loss at Walls

In the low-pressure regime, radicals diffuse to the walls and are lost with probability γ per collision. The steady-state radical density is set by the balance of generation and loss:

```
n_rad ≈ G / (k_wall + k_pump)

k_wall ≈ (γ v̄ / 4) · (A_wall / V)     (for small γ, well-mixed)
k_pump = 1 / τ_res

Example: O atoms
  V = 40 L, A_wall = 6000 cm², v̄ = 6.3 × 10⁴ cm/s
  A/V = 6000 / 40000 = 0.15 cm⁻¹

  γ_O = 0.01 (clean, fluorinated Y₂O₃):
    k_wall = 0.01 × 6.3 × 10⁴ / 4 × 0.15 ≈ 24 s⁻¹
  γ_O = 0.05 (polymer-coated wall):
    k_wall ≈ 118 s⁻¹
  k_pump (τ_res = 0.16 s) ≈ 6 s⁻¹

  n_O ratio (polymer-coated / clean) ≈ (24 + 6) / (118 + 6) ≈ 0.24
```

**Polymer-coated walls consume O atoms** about 4× faster in this example. The wafer sees much less oxygen and much more net polymer than on a clean chamber with the same recipe. The difference between "just cleaned" and "seasoned" can be larger than any recipe knob in the selectivity window.

### 9.1.3 Wall as a Source

When wall polymer is attacked by O atoms and ions, it releases carbon, fluorine, and hydrogen back into the plasma. A wall that has accumulated polymer during a CH₃F/O₂ etch acts as a hidden CH₃F source during a following O₂-rich step. This couples recipe steps and wafers to each other.

---

## 9.2 Signatures of Wall-State Variation

```
Wall state                  Wafer signature (CH₃F/O₂ spacer etch)
──────────────────────────────────────────────────────────────────────────
Freshly cleaned (bare,      Higher O density → thinner polymer
  oxide/fluoride surface)   → higher SiN rate, higher Si recess,
                            more lateral loss, lower foot
Heavily polymer-coated      Lower O density, extra C source
                            → thicker polymer, lower recess, more feet,
                            residues, possible etch stop
Post-long-idle              Wall cooled, adsorbed H₂O → first wafer
                            sees extra H/O → recess and rate spike
Mixed (after a different    Previous chemistry's residues (e.g., Cl, Br
  product's recipe)         from a gate etch on a shared chamber)
                            → unpredictable first-wafer behavior
```

### 9.2.1 First-Wafer Effect

```
Illustrative Si recess vs. wafer number after WAC + no seasoning:

  Wafer #     1     2     3     4     5     10    25
  Recess (nm) 1.15  0.98  0.90  0.86  0.84  0.82  0.82

The first wafer recesses ~40% more than steady state.
After ~5 wafers the walls approach steady state.
```

If the specification is 0.8 ± 0.1 nm, the first three wafers of every lot are out of spec. Seasoning exists to absorb this transient on non-product wafers or in waferless steps.

---

## 9.3 Waferless Autoclean (WAC)

### 9.3.1 Purpose

WAC runs a cleaning plasma with **no wafer** in the chamber (the ESC is sometimes protected by a cover wafer) between production wafers or lots. It removes accumulated wall polymer and resets the wall to a reproducible state.

### 9.3.2 WAC Chemistry

```
Chemistry          Removes                       Leaves wall
──────────────────────────────────────────────────────────────────────────
O₂                 Carbon-based polymer          Oxidized; fluorine-depleted
NF₃ or SF₆         Si-containing deposits        Fluorinated
                   (SiOₓFᵧ from SiF₄ redep.)
O₂ + NF₃ (or SF₆)  Both                          Fluorinated, oxidized
Followed by:
  short CH₃F/He    Deposits a thin, controlled   Lightly polymer-coated
  "season" step    polymer layer                 (closer to steady state)
```

### 9.3.3 WAC Frequency

```
Strategy              Description                  Trade-off
─────────────────────────────────────────────────────────────────────────
Every wafer           WAC after each wafer         Best W2W stability; costs
                      (10–30 s)                    throughput (10–30%)
Every N wafers        WAC after N = 5–25 wafers    Saw-tooth drift within
                                                   each N; less throughput cost
Per lot               WAC at lot start             Lot-to-lot reset; first-wafer
                                                   effect inside each lot
Condition-based       WAC triggered by OES or      Efficient; needs reliable
                      RF sensor drift              wall-state sensor
```

For spacer etch, **WAC-every-wafer plus a short season step** is common at leading-edge nodes. The throughput cost is accepted because wafer-to-wafer recess and width stability matters more.

### 9.3.4 Clean-Then-Season Logic

A pure clean (O₂/NF₃) leaves the walls in the "freshly cleaned" state of Section 9.2, which produces a first-wafer effect. Adding a short polymer-depositing season step returns the walls toward steady state:

```
WAC sequence (illustrative, between every wafer):

Step 1  O₂/NF₃ clean      12 s   Remove C and Si deposits
Step 2  O₂ clean          5 s    Remove residual F from walls
Step 3  CH₃F/He season    6 s    Deposit ~1–3 nm controlled polymer
Total                     23 s   (+ pump/purge ~5 s)

Result: wall state at start of each wafer ≈ reproducible,
        lightly polymerized; first-wafer effect largely eliminated
```

---

## 9.4 Seasoning After Maintenance or Idle

### 9.4.1 Post-PM Seasoning

After a wet clean or part replacement (preventive maintenance, PM), the walls are bare and may contain adsorbed water and cleaning residues. Recovery takes several steps:

```
Post-PM recovery sequence (illustrative):

1. Pump-down and leak check
   Base pressure < spec; rate-of-rise < spec (e.g., < 1 mTorr/min)
2. Bake-out (heated liners at max T, 1–4 h) to desorb H₂O
3. Plasma conditioning: alternating O₂ and NF₃ plasmas (30–60 min)
4. Seasoning: 25–100 bare-Si or blanket-SiN wafers through the
   production recipe (or equivalent RF-hours)
5. Particle check (adders on bare Si)
6. Etch-rate qualification (blanket SiN, Si, SiO₂)
7. Patterned-wafer qualification (spacer width, foot, recess)
8. Release to production
```

### 9.4.2 Seasoning Endpoint

How many seasoning wafers are enough? Use a monitor that tracks wall state:

```
Candidate monitors:
  • OES ratio (e.g., O 777 nm / Ar 750 nm) → O density proxy
  • CO or CN emission during a standard test step
  • RF match position / bias voltage at fixed power (wall impedance)
  • Blanket Si etch rate on a monitor wafer

Criterion: monitor within ±2% of the established seasoned baseline
           for 3 consecutive wafers
```

### 9.4.3 Post-Idle Recovery

```
Idle duration          Recommended action (illustrative)
─────────────────────────────────────────────────────────────
< 15 min               None
15 min – 2 h           WAC + 1 dummy wafer
2 h – 24 h             WAC + 3 dummy wafers or extended season
> 24 h / after vent    Treat as mini-PM: bake + condition + season
```

Idle chambers cool and adsorb residual moisture. Both shift the first wafer toward higher O and H. Many fabs keep spacer chambers in an **idle-plasma** or periodic-season mode to avoid long idle states.

---

## 9.5 Wall Materials and Particle Control

### 9.5.1 Coating Behavior in Spacer Chemistry

```
Coating              Fluorination             Particle mechanism
──────────────────────────────────────────────────────────────────────────
Plasma-spray Y₂O₃    Surface → YOF/YF₃        Porous coating traps polymer,
                     (volume expansion)       flakes at grain boundaries
Dense Y₂O₃ (AD/PVD)  Thin YOF skin            Fewer pores, fewer flakes
YOF / YF₃            Stable                   Low; less first-wafer shift
                                              from fluorination
Anodized Al          AlF₃ formation           AlF₃ flakes, Al contamination
```

### 9.5.2 Polymer Flaking

Wall polymer grows between cleans. Above a critical thickness, stress and thermal cycling cause flakes, which land on wafers as particles, often with the characteristic "fall-on" distribution near the wafer edge or under the window center:

```
Polymer thickness on liner vs. particle adders (illustrative):

  Thickness (µm)   Adders (> 45 nm) per wafer
  < 0.5            < 5
  0.5–1.5          5–15
  1.5–3            15–50   ← schedule WAC/PM before reaching
  > 3              > 50, bursts
```

WAC-every-wafer keeps wall polymer thin enough that flaking is negligible, which is another reason for the throughput trade-off.

### 9.5.3 Metal Contamination

Coating erosion can release Y, Al, and other metals onto wafers. Spacer etch exposes silicon at the source/drain, where metal contamination raises junction leakage. Periodic VPD-ICPMS or TXRF checks of metal levels on bare-Si monitors are part of chamber qualification (Appendix C).

---

## 9.6 Shared Chambers and Recipe Sequencing

When the same chamber runs several recipes (for example, spacer etch and fin-cut or gate-trim steps), each recipe leaves its own wall signature:

```
Previous recipe chemistry     Risk to next spacer etch
──────────────────────────────────────────────────────────────────
HBr/Cl₂ (Si etch)             Br/Cl on walls → Si recess enhancement,
                              memory effect in OES
O₂-rich strip                 Clean walls → first-wafer effect
Heavy C₄F₆ (oxide etch)       Thick CF polymer → feet, etch stop

Mitigation:
  • Dedicated spacer chambers where volume allows
  • Recipe-specific WAC between chemistry changes
  • Sequencing rules in the MES (e.g., spacer after Br-chemistry
    only after a specific WAC)
```

---

## 9.7 Summary & Key Takeaways

1. **The walls are 7–12× the wafer's area.** Their state sets radical densities as much as the recipe does.

2. **Polymer-coated walls consume O atoms.** Higher wall recombination lowers O density, thickens wafer polymer, lowers recess, and raises footing.

3. **First-wafer and post-idle effects are wall effects.** Clean walls give more O and more recess. Moist walls add H and O.

4. **WAC resets, seasoning stabilizes.** Clean-then-season between wafers gives a reproducible, lightly polymerized wall at the start of every wafer.

5. **Post-PM recovery is a defined procedure.** Bake, condition, season to a monitored baseline, then qualify particles, rates, and patterned results.

6. **Coatings matter for particles and drift.** Dense Y₂O₃ and pre-fluorinated YOF reduce flaking and fluorination-driven drift.

7. **Shared chambers need sequencing rules.** Prior chemistries leave wall memory that can affect the next spacer etch.

---

## Study Questions

1. Using the wall-loss model in Section 9.1.2, calculate the ratio of O-atom density for γ_O = 0.02 and γ_O = 0.08, with A/V = 0.12 cm⁻¹ and τ_res = 0.10 s.

2. If Si recess scales as n_O^0.8, and n_O on a freshly cleaned wall is 1.6× the seasoned value, what is the first-wafer recess when the seasoned recess is 0.75 nm?

3. A chamber runs 25-wafer lots with a 20 s WAC per wafer. The production recipe is 50 s plus 20 s transfer overhead. What is the throughput penalty of WAC-every-wafer compared with WAC-per-lot? Express it in wafers per hour.

4. Liner polymer grows by 0.03 µm per wafer without WAC. Using the table in Section 9.5.2, how many wafers can run before particle adders exceed 15 per wafer? How does this compare with typical PM intervals?

5. Propose a seasoning-endpoint criterion using an OES ratio, and explain how you would set its baseline and tolerance.

---

**Previous Chapter:** [Chapter 8: Wafer Temperature & Electrostatic Chuck Design](./08-wafer-temperature-esc.md)  
**Next Chapter:** [Chapter 10: Spacer Profile Control — Footing, Faceting & Shoulder](./10-profile-control.md)

---

**Chapter 9 Development Status:** Complete  
**Version:** 1.0
