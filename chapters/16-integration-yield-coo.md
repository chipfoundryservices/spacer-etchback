# Chapter 16: Integration, Yield & Cost of Ownership

## Overview

A spacer etch is judged by what happens after it. The epitaxy has to nucleate cleanly, the silicide has to stay off the channel, and the self-aligned contact must not short to the gate. Replacement-gate processing needs the spacer to hold its shape while the dummy gate is pulled out from beside it. All of this has to happen at a cost the fab can sustain across hundreds of thousands of wafer passes a year.

This final chapter connects spacer etchback to its neighbors in the flow, catalogs the defect and yield signatures that trace back to it, and builds a cost-of-ownership model that puts recipe and hardware decisions in economic terms. It closes with the principles that run through the whole book.

**Learning Objectives:**
- Design post-etch treatments and cleans compatible with nitride and low-k spacers
- Trace interactions between spacer etch and epitaxy, silicide, contact etch, and RMG
- Map defect types and electrical signatures to spacer-etch root causes
- Build a throughput and cost-of-ownership model for a spacer-etch platform
- Compare the economic weight of throughput changes against yield changes

---

## 16.1 Post-Etch Treatment and Clean

### 16.1.1 What Remains After Etch

```
Residue / modification             Location               Risk if not removed
──────────────────────────────────────────────────────────────────────────────
Hydrofluorocarbon polymer          Spacer sidewalls,      Blocks epi nucleation;
  (1–4 nm CₓHᵧF_z)                 Si surface, gap floor  F outgassing; residue
Plasma oxide (SiOₓ, 1–3 nm)        Exposed Si             Removed by dHF → recess
                                                          (Ch. 11)
Fluorine adsorbed/incorporated     All surfaces           Moisture reaction after
                                                          air exposure → HF, haze
C-rich mixed layer                 Si surface             Epi defects
Damaged Si / H-rich layer          Si surface             Epi defects, R_ext
Low-k damaged skin                 Spacer sidewall        Width loss in dHF
```

### 16.1.2 In-Situ Post-Etch Treatment

A short treatment before the wafer leaves vacuum (Chapter 5.7) removes most polymer and fluorine:

```
Treatment                  Removes            Risk                     Fit
─────────────────────────────────────────────────────────────────────────────
O₂ plasma (low bias)       Polymer, F         Si oxidation, low-k      SiN spacers
                                              carbon depletion
N₂/H₂ plasma               Polymer, F         H into Si (keep bias     Low-k spacers
                                              ~0)
Remote O₂/N₂ or H₂/N₂      Polymer, F         Minimal ion damage       Damage-critical
H₂O vapor / thermal        Loose F            Limited polymer removal  Supplementary
```

### 16.1.3 Wet Clean

```
Clean           Purpose                     Spacer effect                Notes
──────────────────────────────────────────────────────────────────────────────────
dHF (100–1000:1) Oxide removal, pre-epi     SiN: ~0; SiOCN: some;        Sets final
                                            damaged skins: fast           recess
SC1 (NH₄OH/H₂O₂) Particles, organics        Slight SiN/SiOCN etch; Si    Low T, dilute
                                            oxidation/etch                for advanced
SPM (H₂SO₄/H₂O₂) Heavy organics             Oxidizes surfaces            Rarely needed
                                                                          after good
                                                                          in-situ strip
```

### 16.1.4 Queue Time

Fluorine left on surfaces reacts with ambient moisture over hours. Defined **queue-time limits** between spacer etch and clean (e.g., ≤ 4–8 h, product-specific) prevent haze, residue growth, and corrosion of any exposed metals.

---

## 16.2 Interactions With Downstream Steps

### 16.2.1 Source/Drain Epitaxy

```
Spacer-etch output           Epi consequence
──────────────────────────────────────────────────────────────────────
Spacer width (base + foot)   Epi-to-channel proximity → strain, R_ext,
                             short-channel effects
Si recess                    Epi starts lower → strain transfer and
                             junction depth shift
Surface C/F residue          Nucleation delay, faceting, stacking faults
H/displacement damage        Defects at epi interface
Fin-spacer remnant height    Epi lateral growth and merge control
Exposed gate corner          Mushroom (parasitic epi on gate)
Inner spacer flushness       GAA: epi nucleation on sheet ends; voids
                             if indented, blocked growth if protruding
```

### 16.2.2 Silicide (Planar and Some FinFET Flows)

The spacer sets the silicide-to-gate offset. Spacer thinning or a missing foot lets silicide encroach toward the channel, raising leakage. Spacer residues on the S/D surface give silicide voids and high contact resistance.

### 16.2.3 Self-Aligned Contact (SAC) Etch

SAC etch removes oxide (ILD) selectively to the spacer and gate cap. The spacer's **top width and height**, not its mid-height width, set the isolation margin:

```
SAC short risk factors from spacer etch:
  • Faceted spacer top (thin at the corner)          Ch. 10.3.3
  • Spacer top pull-down below the gate cap           Ch. 10.3.1
  • Low-k damaged skin (etched faster by SAC
    chemistry than bulk SiOCN)                        Ch. 12.3
  • Notched top in stacked spacers                    Ch. 10.5
```

### 16.2.4 Replacement Metal Gate (RMG)

```
RMG step                    Spacer requirement
──────────────────────────────────────────────────────────────────
ILD CMP to gate top         Spacer height uniform; HM/spacer top
                            does not dish or erode unevenly
Dummy gate removal          Spacer inner face resists the poly-Si
  (poly-Si etch)            etch (HBr/Cl-based, or TMAH wet)
Dummy oxide removal (dHF)   Spacer inner face resists dHF (low-k
                            inner surface must not be damaged)
GAA channel release         Inner spacers resist SiGe release etch
  (SiGe removal)            → defines gate-to-S/D isolation
High-k / metal deposition   Spacer inner faces define gate length
```

The inner face of the spacer, next to the dummy gate, is protected during spacer etch. The outer face is exposed. Damage on the outer face affects SAC and contacts. Damage on the inner face (from the gate etch upstream) affects RMG.

---

## 16.3 Defects and Yield Signatures

### 16.3.1 Defect Catalog

```
Defect                       Detection                   Spacer-etch root cause
───────────────────────────────────────────────────────────────────────────────────
Mushroom (epi on gate)       Post-epi inspection;         HM/spacer-top loss, facet
                             gate-S/D short               exposing gate corner
Epi stacking faults/voids    Post-epi inspection, TEM     Residue, C/F contamination,
                                                          H damage
Stringers / spacer residue   Post-etch inspection,        Re-entrant gate profile,
                             SEM review                   underetch
Missing/lifted spacer        Inspection; SEM              Adhesion, undercut in
                                                          cleans, damaged interface
Spacer collapse/leaning      CD-SEM (SADP)                High AR thin spacers;
  (SADP)                                                  capillary forces in wet
                                                          clean; stress
Particles                    Post-etch inspection         Wall flaking, ESC, handling
SAC short                    Electrical (gate-contact     Faceted/thinned spacer top
                             leakage)
```

### 16.3.2 Electrical Signatures

```
Electrical symptom                       Likely spacer-etch contribution
──────────────────────────────────────────────────────────────────────────
I_on low, R_ext high                     Excess recess; B passivation by H;
                                         wide spacer/foot
I_off / DIBL high                        Narrow spacer; epi too close
Junction leakage high                    Lattice/H damage; metal contamination
C_gc (gate-contact cap) high             Low-k damage (higher k); thin spacer
Gate-to-contact leakage/shorts           Faceted top, low-k skin attacked in SAC
V_t shift at array edges                 Array-edge spacer asymmetry (Ch. 13.5.2)
Fin-to-fin variation in I_on             Fin-spacer remnant height variation;
                                         fin-top recess variation
```

### 16.3.3 Yield Correlation Practice

```
1. Tag every wafer with chamber, PM-cycle position (RF-hours since PM,
   edge-ring hours), WAC history, and APC adjustments
2. Join with inline metrology (OCD width, recess), FDC features
   (Δt_EP, bias V, He leak), and downstream inspection
3. Correlate with electrical test (WAT) and sort yield by chamber
   and by PM-cycle position
4. Typical findings:
   • Yield or R_ext trend with edge-ring hours → edge ring management
   • Epi defect excursions after PM → seasoning criteria
   • C_gc shift with O₂-flow APC adjustments → low-k damage coupling
```

---

## 16.4 Throughput Model

### 16.4.1 Chamber Cycle Time

```
t_cycle = t_transfer + t_pump/stabilize + t_process + t_WAC + t_dechuck

Example (illustrative):
  Transfer in/out:          12 s
  Pump/gas stabilize:        6 s
  Process (5 steps):        45 s
  WAC + season:             23 s
  Dechuck/He purge:          4 s
  ────────────────────────────
  t_cycle                   90 s → 40 wph per chamber

Without WAC-every-wafer: 67 s → 54 wph per chamber (+35%)
```

### 16.4.2 Platform Throughput

```
Platform wph = min(N_chambers × chamber wph, transfer-robot limit)

  4 etch chambers × 40 wph = 160 wph
  Robot/load-lock limit: ~180–250 wph → not limiting

Effective annual wafer passes:
  W = wph × 8760 h × availability × utilization
    = 160 × 8760 × 0.85 × 0.75
    ≈ 893,000 passes/year
```

---

## 16.5 Cost of Ownership

### 16.5.1 Annual Cost Components

```
Component (illustrative)                         $/year
──────────────────────────────────────────────────────────
Depreciation ($10M platform, 5 years)          2,000,000
Service contract + spares                        450,000
Consumables (edge rings, liners, windows,        350,000
  ESC refurbishment)
Gases and utilities (RF power, chillers,         150,000
  N₂, exhaust abatement)
Clean-room floor space                           200,000
Labor (allocated)                                150,000
──────────────────────────────────────────────────────────
Total                                          3,300,000
```

### 16.5.2 Cost per Wafer Pass

```
Cost per pass = Annual cost / W

  = 3,300,000 / 893,000 ≈ $3.70 per pass (WAC every wafer)

Without WAC-every-wafer (+35% throughput):
  W ≈ 1,205,000 → ≈ $2.74 per pass (saves ~$0.96)
```

### 16.5.3 Yield Changes Dominate

```
Value of a leading-edge logic wafer at end of line: ~$15,000–20,000
(illustrative)

A 0.1% yield change is worth $15–20 per wafer.
A spacer etch pass costs ~$3–4.

If WAC-every-wafer reduces epi defects enough to gain even 0.05% yield
(~$8–10 per wafer), it pays for itself more than eight times over
compared with the ~$0.96 throughput saving from removing it.
```

This is the main economic lesson of spacer etch. **The cost of the step is small compared with the value it controls.** Hardware and recipe decisions that improve control, such as narrow-IED bias, high-zone ESCs, WAC-every-wafer, ALE landings, and tight metrology sampling, are usually justified by yield and parametric gains, even when they cut throughput or add capital cost.

### 16.5.4 Where Cost Reduction Does Make Sense

```
Lever                                 Saves                    Condition
──────────────────────────────────────────────────────────────────────────
Longer edge-ring life (movable ring,  Consumables, downtime    Edge metrics stay
  SiC)                                                         in spec
Shorter transitions between steps     Throughput (5–10%)       No effect on result
Condition-based WAC                   Throughput               Reliable wall-state
                                                               sensor proven
VM-reduced metrology sampling         Metrology cost, cycle    VM residuals within
                                      time                     limits
Fewer seasoning wafers after PM       Wafers, downtime         Seasoning endpoint
                                                               monitored (Ch. 9)
```

---

## 16.6 The Principles of Spacer Etchback

The whole book can be condensed into a short list:

1. **Geometry does the patterning.** A conformal film and a directional etch draw the spacer. Deposition sets width and the etch must preserve it.

2. **Polymer does the selecting.** Selectivity is a difference in steady-state polymer thickness. Every knob that moves polymer (O₂, temperature, wall state, pulsing) moves selectivity.

3. **Overetch decides the outcome.** It clears feet, fin spacers, and gap floors, and it costs recess, spacer height, hard mask, and width. Reduce the overetch needed through uniformity, and make what remains as gentle as possible.

4. **Recess is mostly not selectivity.** Oxidation and damage removal usually dominate. Lower energy and less oxygen at first silicon exposure save the most.

5. **Ion energy must be narrow, not just low.** The window between nitride threshold and damage is tens of eV. The IED tails decide feet, facets, and hydrogen depth.

6. **The chamber is part of the recipe.** Walls, ESC zones, edge ring, and MFC accuracy set the process as much as the recipe text.

7. **Spacers are CDs.** In SADP/SAQP they become lines, and in logic they set junctions and capacitance. Control them with CD-grade metrology and APC.

8. **Value lives downstream.** The step is cheap and its consequences are expensive. Spend on control.

---

## 16.7 Summary & Key Takeaways

1. **Post-etch treatment and clean finish the job.** Remove polymer and fluorine in situ. Choose cleans that do not attack low-k skins or add recess. Enforce queue times.

2. **Each downstream step reads a different part of the spacer.** Epi reads base, foot, recess, and surface. SAC reads the top. RMG reads height and inner faces.

3. **Defects and electrical signatures map to spacer-etch causes.** Mushrooms come from top loss, epi faults from residue and damage, C_gc from low-k damage, and R_ext from recess and H.

4. **Throughput follows cycle time.** WAC-every-wafer costs ~25–35% throughput.

5. **Cost per pass is a few dollars.** At about $3–4 per pass versus $15–20 per 0.1% yield, control improvements usually pay for themselves.

6. **Cut cost where results do not suffer.** Consumable life, transitions, condition-based WAC, VM sampling, and seasoning efficiency.

---

## Study Questions

1. A spacer-etch process cycle is 38 s process + 10 s transfer + 5 s stabilize + 3 s dechuck. Adding WAC-every-wafer adds 20 s. Compute chamber wph with and without WAC, and the percentage throughput loss.

2. Using the cost model of Section 16.5, compute the cost per pass for a $12M platform with 5 chambers at 36 wph each, availability 0.88, utilization 0.80, and other annual costs of $1.4M.

3. A recipe change lowers Si recess by 0.4 nm and is estimated to raise yield by 0.08%. It adds 6 s to process time on a 90 s cycle. With a wafer value of $17,000, calculate the net value per wafer of the change.

4. Post-epi inspection shows a 3× rise in mushroom defects on wafers from one chamber in the last third of its PM cycle. List the spacer-etch mechanisms that could explain this and the data you would pull to confirm each.

5. Write a one-page "spacer etch control plan" for a new SiOCN gate spacer: list the inline measurements, FDC parameters, APC loops, and qualification checks you would put in place, with a reason for each.

---

**Previous Chapter:** [Chapter 15: Endpoint, Metrology & Advanced Process Control](./15-endpoint-metrology-apc.md)  
**Back Matter:** [Appendices](../appendices/) · [Glossary](../GLOSSARY.md)

---

**Chapter 16 Development Status:** Complete  
**Version:** 1.0

**Book #22 main text complete.**
