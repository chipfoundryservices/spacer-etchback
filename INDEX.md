# Index: Book #22 Navigation Guide

## Quick Navigation

**Total Content:** 16 chapters + 7 appendices + glossary  
**Estimated Read Time:** 22–30 hours for the complete book; 6–10 hours for a focused reading path

| Part | Chapters | Theme |
|------|----------|-------|
| I | 1–4 | Fundamentals: architecture, films, physics, chemistry |
| II | 5–9 | Hardware: reactor, ion energy, gas, chuck, walls |
| III | 10–14 | Phenomena: profile, selectivity, damage, loading, advanced cases |
| IV | 15–16 | Production: endpoint, metrology, APC, integration, cost |

---

## Part I: Fundamentals (Chapters 1–4)

### Chapter 1: [Spacer Architecture & the Role of Etchback](./chapters/01-spacer-architecture.md)
**Estimated Time:** 60 min | **Difficulty:** Foundation | **Reading Level:** All roles  
**Focus:** Why do spacers exist, and what must the etchback deliver?

**Key Topics:**
- LDD spacers and the origin of the self-aligned sidewall
- Offset spacers, main spacers, and multi-layer spacer stacks
- FinFET gate spacers and GAA inner spacers
- SADP/SAQP: the spacer as a patterning hard mask
- Specification sheet for a modern spacer etch

**Prerequisites:** None (foundational)  
**Cross-References:** Book #18 (gate stack); Book #21 (STI and fin formation)  
**Critical Equations:** Junction offset vs. spacer width; overlap capacitance scaling  
**Study Questions:** 5 calculations on spacer function and specification

---

### Chapter 2: [Spacer Films — Materials & Deposition](./chapters/02-spacer-films.md)
**Estimated Time:** 70 min | **Difficulty:** Intermediate | **Reading Level:** Process/Integration roles  
**Focus:** What is the spacer made of, and how does deposition set up the etch?

**Key Topics:**
- SiO₂, Si₃N₄, SiCN, SiOCN, SiBCN: structure and properties
- Dielectric constant vs. etch and wet-clean resistance
- ALD, PEALD, PECVD, and LPCVD: conformality and hydrogen content
- Pattern-loading in deposition: the hidden input to etchback
- Bilayer and trilayer spacer stacks

**Prerequisites:** Chapter 1  
**Cross-References:** Silicon Nitride Etch companion volume; Books #6–10  
**Critical Equations:** Step coverage; conformality ratio; density–etch rate correlation  
**Data Tables:** Film property comparison (Appendix A)  
**Study Questions:** 5 calculations on conformality and thickness budgets

---

### Chapter 3: [Etchback Physics — Anisotropic Removal of Conformal Films](./chapters/03-etchback-physics.md)
**Estimated Time:** 90 min | **Difficulty:** Advanced | **Reading Level:** Process/Research roles  
**Focus:** How does a directional etch turn a film into a spacer?

**Key Topics:**
- Vertical-thickness geometry and spacer width
- Ion-enhanced etching: ion–neutral synergy
- Threshold energies and the √E yield law
- Angular yield dependence and faceting
- Overetch sizing from conformality and uniformity

**Prerequisites:** Chapters 1–2; Books #1–5 (sheath physics)  
**Cross-References:** Books #3, #5 (ion-surface interactions)  
**Critical Equations:** Y(E) = A(√E − √E_th); overetch fraction; facet angle  
**Study Questions:** 6 calculations on geometry, yield, and overetch

---

### Chapter 4: [Etch Chemistries for Spacer Materials](./chapters/04-etch-chemistries.md)
**Estimated Time:** 80 min | **Difficulty:** Advanced | **Reading Level:** Process/Research roles  
**Focus:** Which gases etch which spacer, and why are they selective?

**Key Topics:**
- CH₃F/O₂/Ar, CH₂F₂/O₂, CHF₃/O₂ chemistries for Si₃N₄
- Steady-state polymer thickness and selectivity
- C₄F₆/C₄F₈/O₂/Ar chemistries for SiO₂ spacers
- Low-k spacer etch and carbon preservation
- Isotropic chemistries: NF₃/O₂ remote plasma, HF/NH₃ vapor

**Prerequisites:** Chapter 3; Books #6–10 (fluorocarbon chemistry)  
**Cross-References:** Silicon Nitride Etch companion volume; Book #20 (O₂ plasma)  
**Critical Equations:** Etch rate vs. polymer thickness; effective F/C ratio  
**Data Tables:** Reaction products and volatility (Appendix B)  
**Study Questions:** 5 calculations on chemistry selection and selectivity

---

## Part II: Hardware Design (Chapters 5–9)

### Chapter 5: [Etch Reactor Architecture for Spacer Etchback](./chapters/05-reactor-architecture.md)
**Estimated Time:** 70 min | **Difficulty:** Intermediate | **Reading Level:** Equipment/Process roles  
**Focus:** What reactor delivers low-damage, highly controlled etchback?

**Key Topics:**
- ICP vs. CCP vs. hybrid sources
- Plasma density, ion flux, and ion energy decoupling
- Chamber geometry, pumping speed, and residence time
- Platform configuration for spacer modules

**Prerequisites:** Chapters 1–4  
**Cross-References:** Books #11–15 (reactor engineering)  
**Critical Equations:** Residence time; Bohm flux; power balance  
**Study Questions:** 5 calculations on reactor selection

---

### Chapter 6: [Ion Energy & Bias Control](./chapters/06-ion-energy-control.md)
**Estimated Time:** 90 min | **Difficulty:** Advanced | **Reading Level:** Equipment/Research roles  
**Focus:** How do we place ion energy precisely in the spacer-etch window?

**Key Topics:**
- Sheath voltage, bias frequency, and IED width
- Pulsed bias and duty-cycle averaging
- Tailored-waveform bias for narrow IEDs
- Synchronous source/bias pulsing and afterglow chemistry

**Prerequisites:** Chapter 3; Books #1–5  
**Cross-References:** Books #11–15 (RF delivery and pulsing)  
**Critical Equations:** IED splitting ΔE; time-averaged ion energy; ion transit time  
**Study Questions:** 6 calculations on IED design and pulsing

---

### Chapter 7: [Gas Delivery, Pressure & Radical Control](./chapters/07-gas-pressure-radicals.md)
**Estimated Time:** 70 min | **Difficulty:** Intermediate | **Reading Level:** Process/Equipment roles  
**Focus:** How do gas flows and pressure set the polymer balance?

**Key Topics:**
- CH₃F:O₂ ratio as the selectivity knob
- Diluent effects (Ar, He, N₂)
- Multi-zone gas injection and center/edge tuning
- Residence time and by-product redeposition
- MFC accuracy and recipe sensitivity

**Prerequisites:** Chapters 4–5  
**Cross-References:** Book #20 (gas distribution)  
**Critical Equations:** Residence time; sensitivity coefficients  
**Study Questions:** 5 calculations on flow ratio and sensitivity

---

### Chapter 8: [Wafer Temperature & Electrostatic Chuck Design](./chapters/08-wafer-temperature-esc.md)
**Estimated Time:** 70 min | **Difficulty:** Intermediate | **Reading Level:** Equipment/Process roles  
**Focus:** How does wafer temperature drive polymer, selectivity, and CD?

**Key Topics:**
- Temperature dependence of polymer sticking and desorption
- Multi-zone ESC design and tuning
- Helium backside cooling and heat flux
- Edge ring wear and extreme-edge spacer width

**Prerequisites:** Chapters 4–7  
**Cross-References:** Books #19–20 (thermal management)  
**Critical Equations:** Wafer heat balance; ΔT across He gap  
**Study Questions:** 5 calculations on thermal design

---

### Chapter 9: [Chamber Wall Conditioning & Seasoning](./chapters/09-chamber-conditioning.md)
**Estimated Time:** 60 min | **Difficulty:** Intermediate | **Reading Level:** Equipment/Manufacturing roles  
**Focus:** How does the chamber's history change the etch?

**Key Topics:**
- Wall polymer as a radical source and sink
- Waferless autoclean (WAC) strategy
- Seasoning after PM and first-wafer effect
- Wall materials and particle control

**Prerequisites:** Chapters 4, 7  
**Cross-References:** Book #20 Chapter 8 (chamber coatings)  
**Critical Equations:** Wall-loss probability and radical density  
**Study Questions:** 5 calculations on seasoning and drift

---

## Part III: Process Phenomena (Chapters 10–14)

### Chapter 10: [Spacer Profile Control — Footing, Faceting & Shoulder](./chapters/10-profile-control.md)
**Estimated Time:** 80 min | **Difficulty:** Advanced | **Reading Level:** Process/Integration roles  
**Focus:** How do we get a square spacer with the right width and height?

**Key Topics:**
- Spacer width definitions and measurement
- Footing and stringer mechanisms
- Faceting and gate-cap erosion
- Shoulder loss and spacer top height
- Multi-step profile recipes

**Prerequisites:** Chapters 3–4, 6  
**Critical Equations:** Facet-limited spacer height; foot clearance time  
**Study Questions:** 6 calculations on profile evolution

---

### Chapter 11: [Selectivity & Substrate Recess](./chapters/11-selectivity-recess.md)
**Estimated Time:** 80 min | **Difficulty:** Advanced | **Reading Level:** Process/Integration roles  
**Focus:** Where does silicon go, and how do we keep it?

**Key Topics:**
- Recess budget across a logic flow
- Oxidation-and-removal recess mechanism
- Selectivity to SiO₂, SiGe, and hard mask
- Main etch / soft landing / overetch design

**Prerequisites:** Chapters 3–4, 10  
**Cross-References:** Book #21 (silicon etch and damage)  
**Critical Equations:** Recess vs. overetch time; cumulative recess  
**Study Questions:** 6 calculations on recess and selectivity

---

### Chapter 12: [Plasma-Induced Damage](./chapters/12-plasma-damage.md)
**Estimated Time:** 80 min | **Difficulty:** Advanced | **Reading Level:** Device/Research roles  
**Focus:** What does the etch do beneath the surface?

**Key Topics:**
- Hydrogen implantation range and diffusion
- Displacement damage and amorphous layer depth
- Low-k spacer carbon depletion
- Charging damage at the gate edge
- Detection: TEM, XPS, SIMS, epitaxy test structures

**Prerequisites:** Chapters 3, 6, 11  
**Cross-References:** Book #18 (gate damage); Book #21 (substrate damage)  
**Critical Equations:** Projected range vs. energy; damaged-layer thickness  
**Study Questions:** 5 calculations on damage depth and mitigation

---

### Chapter 13: [Loading, Pattern Dependence & Uniformity](./chapters/13-loading-uniformity.md)
**Estimated Time:** 75 min | **Difficulty:** Advanced | **Reading Level:** Process/Integration roles  
**Focus:** Why does spacer width depend on where it is?

**Key Topics:**
- Microloading and iso-dense bias
- Aspect-ratio-dependent clearing in tight gaps
- Macroloading and die-level density
- Within-wafer and extreme-edge uniformity
- Compensation strategies

**Prerequisites:** Chapters 3, 7–8, 10  
**Cross-References:** Book #20 Chapter 10 (ARDE)  
**Critical Equations:** Conductance-limited neutral flux; ion angular cutoff  
**Study Questions:** 5 calculations on loading and compensation

---

### Chapter 14: [Advanced Etchback — FinFET, GAA Inner Spacers & SADP/SAQP](./chapters/14-advanced-etchback.md)
**Estimated Time:** 100 min | **Difficulty:** Expert | **Reading Level:** Process/Integration/Research roles  
**Focus:** How do 3D devices and multipatterning change the problem?

**Key Topics:**
- FinFET: gate spacer kept, fin spacer removed
- GAA inner spacer: lateral recess, fill, isotropic etchback
- SADP/SAQP spacer etch and pitch walking
- ALE and quasi-ALE for nitride spacers

**Prerequisites:** Chapters 1–13  
**Cross-References:** Book #19 (mandrels); Book #21 (fins)  
**Critical Equations:** Fin-spacer overetch ratio; pitch-walk error budget; ALE EPC  
**Study Questions:** 6 calculations on advanced architectures

---

## Part IV: Production Scale (Chapters 15–16)

### Chapter 15: [Endpoint, Metrology & Advanced Process Control](./chapters/15-endpoint-metrology-apc.md)
**Estimated Time:** 75 min | **Difficulty:** Intermediate | **Reading Level:** Process/Manufacturing roles  
**Focus:** How do we know the etch is done and done right?

**Key Topics:**
- OES endpoint on CN, N₂, CO, and SiF emission
- Interferometric endpoint on blanket areas
- OCD, CD-SEM, TEM, and AFM for spacer metrology
- Feed-forward and feedback APC

**Prerequisites:** Chapters 3–4, 10–13  
**Cross-References:** Books #11–15 (endpoint)  
**Critical Equations:** EWMA controller; endpoint signal-to-noise  
**Study Questions:** 5 calculations on endpoint and APC

---

### Chapter 16: [Integration, Yield & Cost of Ownership](./chapters/16-integration-yield-coo.md)
**Estimated Time:** 75 min | **Difficulty:** Intermediate | **Reading Level:** All roles  
**Focus:** How does spacer etch affect the rest of the flow and the bottom line?

**Key Topics:**
- Post-etch clean and residue removal
- Interactions with epitaxy, silicide, contact, and RMG
- Defect signatures and yield correlation
- Throughput and cost-of-ownership model

**Prerequisites:** Chapters 1–15  
**Cross-References:** Book #20 (residue); Book #18 (gate integrity)  
**Critical Equations:** Cost per wafer pass; throughput model  
**Study Questions:** 5 calculations on integration and cost

---

## Appendices

| Appendix | Title | Use |
|----------|-------|-----|
| [A](./appendices/A-spacer-material-properties.md) | Spacer Material Properties | k, density, H content, wet-etch rates |
| [B](./appendices/B-chemistry-reaction-data.md) | Chemistry & Reaction Data | Bond energies, product volatility, gas properties |
| [C](./appendices/C-standard-procedures.md) | Standard Operating Procedures | Daily checks, qualification, PM recovery |
| [D](./appendices/D-process-windows.md) | Process Windows & Lookup Tables | Starting recipes, sensitivities |
| [E](./appendices/E-geometry-overetch-calculations.md) | Geometry & Overetch Calculations | Worked derivations |
| [F](./appendices/F-endpoint-metrology-reference.md) | Endpoint & Metrology Reference | OES lines, metrology capabilities |
| [G](./appendices/G-troubleshooting-guide.md) | Troubleshooting Guide | Symptom → cause → action |

Glossary: [GLOSSARY.md](./GLOSSARY.md)

---

## Suggested Reading Paths

### Process Engineer (≈10 hours)
1 → 3 → 4 → 10 → 11 → 13 → 14 → Appendix D, E, G

### Equipment Engineer (≈9 hours)
1 → 3 → 5 → 6 → 7 → 8 → 9 → 15 → Appendix C, F

### Integration Engineer (≈8 hours)
1 → 2 → 10 → 11 → 14 → 16 → Appendix A, G

### Device Engineer (≈6 hours)
1 → 2 → 11 → 12 → 16

### Researcher (≈10 hours)
3 → 4 → 6 → 12 → 14 → Appendix B

---

## Cross-Reference Map to Other Books

| Book | Topic | Relevant Chapters |
|------|-------|-------------------|
| Books #1–5 | Plasma Physics Fundamentals | Ch. 3, 5, 6 |
| Books #6–10 | Dielectric & Fluorocarbon Etch | Ch. 4, 7, 11 |
| Books #11–15 | Advanced Plasma Engineering | Ch. 5, 6, 15 |
| Book #18 | Gate Oxide Etch | Ch. 1, 12, 16 |
| Book #19 | Carbon Hard Mask Etch | Ch. 14 (SADP/SAQP) |
| Book #20 | Photoresist Ashing | Ch. 9, 16 |
| Book #21 | Shallow Trench Isolation Etch | Ch. 11, 12, 14 |
| Companion | Silicon Nitride Etch | Ch. 2, 4, 14 |

---

## Study Questions Summary

**Total Study Questions:** 5–6 per chapter × 16 chapters ≈ 86 questions  
**Nature:** Mostly calculation-based  
**Topics:** Geometry, overetch sizing, selectivity, ion energy design, loading compensation, APC tuning, cost analysis

Examples:
- Compute final spacer width from deposited thickness, conformality, and lateral etch rate
- Size overetch for a given deposition and etch non-uniformity
- Estimate silicon recess from overetch time and selectivity
- Design a pulsed-bias duty cycle for a target average ion energy
- Predict pitch walking from mandrel CD error and spacer width error
- Compute cost per wafer pass from throughput, consumables, and depreciation

---

## How to Use This Index

1. **First time?** Read PREFACE.md, then this INDEX, then Chapter 1.
2. **Focused reading?** Pick your role from the reading paths above.
3. **Reference mode?** Jump to the chapter. Use Appendix G for symptoms.
4. **Deep dive?** Read Chapters 1–16 in order and work the study questions.

---

**Index Version:** 1.0  
**Last Updated:** 2026-10-04  
**Next:** Begin [Chapter 1: Spacer Architecture & the Role of Etchback](./chapters/01-spacer-architecture.md)
