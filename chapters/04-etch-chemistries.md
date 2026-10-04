# Chapter 4: Etch Chemistries for Spacer Materials

## Overview

Chapter 3 showed that anisotropy comes from directional ions acting on a chemically prepared surface. This chapter covers the chemistry: which gases etch which spacer materials, and why some chemistries etch nitride twenty times faster than the silicon beneath it.

The central idea is the **steady-state polymer layer**. In fluorocarbon and hydrofluorocarbon plasmas, every surface carries a thin CₓHᵧF_z film whose thickness is set by a balance of deposition, ion-driven removal, and consumption by the substrate's own atoms. Different substrates consume this film at different rates, so each develops a different steady-state thickness, and the film's thickness controls the etch rate beneath it. **Selectivity is the difference in polymer thickness, translated into an etch-rate difference.**

**Learning Objectives:**
- Apply the effective F/C ratio, including hydrogen scavenging, to rank chemistries by polymerizing tendency
- Explain why nitride, oxide, and silicon develop different steady-state polymer thicknesses
- Describe the role of O₂ as a polymer-balance knob and why selectivity peaks at intermediate O₂
- Select chemistries for SiN, SiO₂, and low-k spacer etchback
- Describe isotropic chemistries used for lateral recess and inner-spacer etchback

---

## 4.1 Chemistry Building Blocks

### 4.1.1 Feed Gases

```
Gas        Role in spacer etch                    Polymerizing tendency
─────────────────────────────────────────────────────────────────────────
CF₄        F source, fast main etch               Low
CHF₃       F + CFₓ, main etch                     Medium
CH₂F₂      Selective nitride etch                 Medium–High
CH₃F       Highly selective nitride etch          High
C₄F₈       Oxide etch, polymer former             High
C₄F₆       Oxide etch, very selective             Very high
O₂         Polymer removal, oxidizer              (removes polymer)
CO₂ / CO   Milder oxidizer / C source             (mild removal)
N₂         Polymer modifier, CN former            (modifies)
H₂         F scavenger, polymer modifier          (raises effective C/F)
Ar / He    Diluent, ion source, cooling           —
NF₃        Isotropic F source (remote)            None
```

### 4.1.2 Effective F/C Ratio

The fluorine-to-carbon ratio of the feed predicts whether a plasma etches or deposits. Hydrogen scavenges fluorine as HF, lowering the effective ratio:

```
(F/C)_eff = (n_F − n_H) / n_C

Gas        n_F   n_H   n_C   (F/C)_eff
─────────────────────────────────────────
CF₄        4     0     1     4.0       → etching, low polymer
CHF₃       3     1     1     2.0       → balanced
C₄F₈       8     0     4     2.0       → balanced, polymer-rich radicals
C₄F₆       6     0     4     1.5       → polymerizing
CH₂F₂      2     2     1     0.0       → strongly polymerizing
CH₃F       1     3     1     −2.0      → very strongly polymerizing

Rule of thumb (no O₂):
  (F/C)_eff > ~3   etching dominates
  (F/C)_eff ~ 2    balanced; substrate-dependent
  (F/C)_eff < ~1.5 deposition dominates unless ions or O₂ remove polymer
```

CH₃F alone, at low bias, would coat the wafer with polymer. **O₂ is added to burn off the excess**, and the CH₃F:O₂ ratio becomes the main knob that sets polymer thickness.

---

## 4.2 The Steady-State Polymer Model

### 4.2.1 Polymer Balance on Each Surface

On each surface the polymer thickness δ settles where deposition equals removal:

```
dδ/dt = Γ_dep − R_ion(δ) − R_O − R_sub(δ) = 0

Γ_dep      polymer deposition from CFₓ, CHₓFᵧ radicals
R_ion      ion-driven sputtering/densification of polymer
R_O        oxidative removal by O atoms (→ CO, CO₂, COF₂)
R_sub      consumption by substrate atoms reaching the polymer:
             SiO₂ supplies O  → C removed as CO, CO₂
             Si₃N₄ supplies N → C removed as CN, HCN, FCN
             Si supplies none → polymer is not consumed by the substrate
```

### 4.2.2 Etch Rate Through a Polymer Layer

Fluorine and ion energy must cross the polymer to reach the substrate. A useful phenomenological model treats the polymer as an attenuating layer:

```
R_sub = R₀ · exp(−δ / λ)

R₀  = etch rate with no polymer at the same ion and neutral flux
λ   = attenuation length for energy/F transport (~0.7–1.2 nm)

Example (λ = 1.0 nm, R₀ = 60 nm/min for both SiN and Si):

Surface    δ (nm)     exp(−δ/λ)    Etch rate (nm/min)
─────────────────────────────────────────────────────
Si₃N₄      0.8        0.449        27
SiO₂       1.6        0.202        12
Si         3.0        0.050        3.0

S(SiN:SiO₂) = 27/12 ≈ 2.2
S(SiN:Si)   = 27/3  = 9
```

Real R₀ values differ by material too. The model shows the key point: **a 2 nm difference in polymer thickness gives an order of magnitude in selectivity.** Small changes in polymer balance, such as O₂ flow, wafer temperature, or wall condition, swing selectivity considerably.

### 4.2.3 Why Si₃N₄ Keeps Its Polymer Thin

Nitride is unusual among dielectrics in that its etch products include carbon-containing species. Nitrogen leaving the surface combines with carbon in the polymer:

```
N (from film) + C (from polymer) → CN radicals
CN + F → FCN (volatile)
CN + H → HCN (volatile)

With hydrogen-containing gases (CH₃F, CH₂F₂):
  H promotes HCN formation, giving nitrogen an efficient exit route
  that also removes carbon from the polymer.
```

This is a main reason hydrofluorocarbons with high H content are selective for nitride. The nitride effectively "eats" its own polymer. Silicon cannot. Oxide can, through CO formation, but in an H-rich, O₂-balanced CH₃F plasma the nitride's consumption is more efficient.

The CN signal is visible in optical emission (CN violet system near 388 nm). It falls sharply when the nitride clears, which makes it a natural endpoint signal (Chapter 15).

---

## 4.3 Nitride Spacer Chemistry: CH₃F/O₂ and Relatives

### 4.3.1 Role of O₂: The Selectivity Peak

With CH₃F fixed, increasing O₂ thins polymer on every surface:

```
CH₃F/O₂/Ar, 100 sccm CH₃F, 200 sccm Ar, low bias (illustrative)

O₂ (sccm)   SiN rate     Si rate      SiO₂ rate    S(SiN:Si)   S(SiN:SiO₂)
              (nm/min)     (nm/min)     (nm/min)
────────────────────────────────────────────────────────────────────────────
   0         ~0 (dep.)    dep.         dep.          —            —
  25          8           0.3          2.5           27           3.2
  50         22           0.9          4.0           24           5.5
  75         32           2.0          5.5           16           5.8
 100         38           4.5          8.0            8.4         4.8
 150         44          10            14             4.4         3.1
```

Three regimes appear:

1. **Low O₂ (polymer-starved of oxygen):** nitride etches slowly and silicon is buried under thick polymer. Selectivity to Si is high but rate is low, and footing and residue risk is high.
2. **Intermediate O₂ (window):** polymer on SiN is thin and on Si is still thick. This is the selectivity window used in production.
3. **High O₂:** polymer collapses everywhere. Silicon oxidizes into SiOₓ, which then etches, and recess climbs through an **oxidation–removal** mechanism (Chapter 11).

### 4.3.2 Comparison of Hydrofluorocarbons

```
Chemistry           SiN rate   S(SiN:Si)   S(SiN:SiO₂)   Profile       Use
─────────────────────────────────────────────────────────────────────────────────
CF₄/O₂              High       2–4         1–2           Isotropic-ish Breakthrough
CHF₃/O₂/Ar          Medium     4–8         1.5–3         Anisotropic   Main etch
CH₂F₂/O₂/Ar         Medium     8–15        3–6           Anisotropic   Main/OE
CH₃F/O₂/Ar          Med–Low    10–30+      4–10          Anisotropic   Main/OE
CH₃F/CO₂/Ar         Low        15–40       5–15          Anisotropic   Soft landing

(Representative ranges at low bias; they depend strongly on bias,
 pressure, temperature, and wall state.)
```

### 4.3.3 Typical Multi-Step Nitride Spacer Recipe

```
Step              Chemistry               Purpose                       Bias
────────────────────────────────────────────────────────────────────────────────
1. Breakthrough   CF₄ (or CHF₃/CF₄)       Remove surface oxide/oxynitride Low–Med
                                          and any native skin; 2–5 s
2. Main etch      CH₂F₂ or CHF₃ + O₂/Ar   Fast, anisotropic bulk removal  Medium
                                          to ~80–90% of film
3. Soft landing   CH₃F/O₂/Ar              High selectivity; endpoint      Low
                                          on CN/N₂ emission
4. Overetch       CH₃F/O₂(/CO₂)/He        Clear feet and gap floors;      Very low
                                          minimum recess
```

The breakthrough step matters because air-exposed nitride develops a thin oxynitride skin that a highly selective CH₃F chemistry may etch slowly. An unbroken skin gives a delayed and non-uniform start, which looks like a wafer-scale non-uniformity.

### 4.3.4 Diluent Choice

```
Diluent   Effect
────────────────────────────────────────────────────────────────────────
Ar        Heavier ions → more physical sputtering → faster but more faceting
          (Chapter 3.4); higher plasma density in ICP
He        Light ions → less sputtering; better heat transfer in gas phase;
          lower faceting; slightly lower density
N₂        Modifies polymer (CN incorporation); can raise SiN rate and
          lower SiN:SiO₂ selectivity; sometimes used to tune footing
```

---

## 4.4 Oxide Spacer Chemistry

### 4.4.1 Fluorocarbon Oxide Etch

SiO₂ spacers, used in SADP and as liners, are etched in fluorocarbon chemistries similar to contact etch but at much lower energy:

```
Chemistry             S(SiO₂:Si)   S(SiO₂:SiN)   Notes
─────────────────────────────────────────────────────────────────────
CF₄/CHF₃/Ar           5–10         1–2           Simple, low polymer
C₄F₈/O₂/Ar            10–20        3–8           Standard balance
C₄F₆/O₂/Ar            15–40        5–15          Most selective, polymer-rich
```

Oxide consumes polymer through CO formation, so it etches through layers that stop silicon and, under the right conditions, nitride.

### 4.4.2 SADP Oxide Spacers on Carbon Mandrels

When the mandrel is amorphous carbon or spin-on carbon (Book #19), the spacer etch must **not** use O₂-rich chemistry. Oxygen would attack the exposed mandrel tops once the spacer clears:

```
Issue: Mandrel top is exposed when spacer film clears from it.
       O₂ in the etch erodes the mandrel → mandrel height loss and
       mandrel CD trim → spacer leans or loses support.

Approaches:
  • O₂-free fluorocarbon (CF₄/CHF₃/Ar, C₄F₈/Ar) with polymer control by bias
  • CO instead of O₂ for milder polymer control
  • Accept mandrel top loss if mandrel pull is next (the mandrel is
    removed anyway), but control asymmetry
```

### 4.4.3 SADP Spacers on Amorphous Silicon Mandrels

With a-Si mandrels, an oxide or nitride spacer etch must be selective to silicon on two surfaces: the mandrel top and the underlying layer, which may be another hard mask. The chemistries follow the same polymer logic as the gate-spacer case.

---

## 4.5 Low-k Spacer Chemistry

### 4.5.1 The Problem

SiOCN, SiCN, and SiBCN contain carbon that lowers k. Oxygen atoms in the plasma remove that carbon near the surface:

```
Si–CH₃ / Si–C (in film) + O → CO, CO₂ + Si–O (left behind)

Consequences:
  • Surface skin becomes SiO₂- or SiON-like: k rises toward 4.5–6.5
  • dHF wet-etch rate of the skin rises sharply (oxide-like)
  • Downstream pre-epi clean thins the spacer more than planned
```

### 4.5.2 Mitigation Strategies

```
Strategy                          Mechanism                         Trade-off
─────────────────────────────────────────────────────────────────────────────────
Reduce O₂, replace with CO₂/CO    Lower O-atom density               More polymer, footing
O₂-free (CH₃F/H₂/Ar, CHF₃/N₂)     No O atoms                         H/N damage; polymer
Higher polymer on sidewalls       Polymer shields spacer from O      Residue; needs clean
Pulsed source (lower O density)   Radical density falls in off-time  Lower rate
SiN cap over low-k                Sacrificial outer layer protects   Adds width, k penalty
Low wafer temperature             Slower carbon depletion kinetics   More polymer
```

The low-k spacer's **sidewall** is the critical surface. Field surfaces are etched away, so their damage does not matter. The sidewall, which forms the final spacer face, sees radicals for the whole etch. A passivating polymer on the sidewall is the most effective protection, and it is removed later by a mild ash or clean that is itself low in oxygen (Chapter 16).

---

## 4.6 Isotropic Chemistries

### 4.6.1 When Isotropy Is Wanted

Some spacer-related steps need **lateral** etching:

- GAA inner-spacer etchback: remove nitride everywhere except inside lateral recesses
- Spacer trim: thin a spacer uniformly after anisotropic etch
- Fin-sidewall spacer removal: some flows use a short isotropic step (Chapter 14)
- Removal of sacrificial layers for air-gap spacers

### 4.6.2 Remote-Plasma Fluorine Chemistry

A remote (downstream) plasma delivers F atoms with negligible ion flux to the wafer:

```
NF₃/O₂/N₂ (or CF₄/O₂/N₂) remote plasma:

  NF₃ → NFₓ + F
  O₂ + N₂ → NO (in discharge and afterglow)
  NO enhances Si₃N₄ etching by attacking N-sites; it also forms
  thin oxide on Si, which suppresses Si etching

Representative selectivity (illustrative, optimized):
  S(SiN:SiO₂)   10–50
  S(SiN:Si)     10–40 (O-passivated Si)
  Rate           1–10 nm/min (well-controlled for few-nm recess)
```

### 4.6.3 Other Isotropic Options

```
Method                      Selectivity                   Notes
───────────────────────────────────────────────────────────────────────
Hot H₃PO₄ (wet, ~160°C)     SiN:SiO₂ ~30–100+             Classic nitride strip;
                                                          surface-tension and
                                                          loading issues in 3D
dHF                          SiO₂:SiN high                Oxide-selective
HF/NH₃ (vapor, SiCoNi-like)  SiO₂:SiN, SiO₂:Si high        Self-limiting salt
                                                          formation, sublimation
HF vapor (anhydrous)         SiO₂ selective               Moisture-sensitive
Radical-based SiGe etch      SiGe:Si 50–100+              Lateral SiGe recess
  (e.g., F-based remote)                                  before inner spacer
```

Chapter 14 combines these into the full inner-spacer sequence.

---

## 4.7 Gas-Phase and Surface Products

Volatility of etch products sets the removal pathway:

```
Product     Boiling/sublimation point     Formed from
──────────────────────────────────────────────────────
SiF₄        −86°C (sublimes)              Si + F
CO          −191°C                        C + O
CO₂         −78°C (sublimes)              C + O
HF          +20°C                         H + F
HCN         +26°C                         H + C + N
FCN         −46°C                         F + C + N
C₂N₂        −21°C                         C + N
N₂          −196°C                        N + N
BF₃         −100°C                        B + F
NF₃         −129°C                        N + F
COF₂        −85°C                         C + O + F
```

All of these are volatile at typical wafer temperatures (−10 to +60°C). HF and HCN can condense on very cold surfaces. At low wafer temperatures with heavy hydrogen chemistries, check for condensation-related residues. See Appendix B for more data.

---

## 4.8 Summary & Key Takeaways

1. **Effective F/C ranks chemistries.** Subtract H from F. CH₃F (−2) and CH₂F₂ (0) polymerize strongly. CF₄ (4) etches.

2. **Selectivity is a polymer-thickness difference.** Etch rate falls roughly exponentially with polymer thickness, so a 2 nm difference gives an order of magnitude in selectivity.

3. **Nitride eats its own polymer.** Nitrogen leaves as CN, HCN, and FCN, keeping nitride polymer thin while silicon stays covered. This is the root of SiN:Si selectivity.

4. **O₂ has an optimum.** Too little gives polymer build-up and feet. Too much gives silicon oxidation and recess. Selectivity peaks in between.

5. **Multi-step recipes separate jobs.** Breakthrough, main etch, soft landing, and overetch each use the chemistry suited to their purpose.

6. **Low-k spacers need low oxygen.** O atoms deplete carbon, raising k and wet-etch rate. Use CO₂/CO, polymer shielding, pulsing, or protective caps.

7. **Isotropic chemistries have their place.** Remote NF₃/O₂/N₂, hot phosphoric acid, and vapor-phase HF chemistries handle lateral recess and inner-spacer etchback.

---

## Study Questions

1. Compute (F/C)_eff for a mixture of 60 sccm CH₂F₂ + 40 sccm CHF₃. How does it compare to pure CH₂F₂ and pure CHF₃?

2. Using R = R₀ exp(−δ/λ) with λ = 0.9 nm and equal R₀, what polymer thicknesses on SiN and Si give S(SiN:Si) = 20 if δ_SiN = 0.7 nm? If a wall-condition change adds 0.3 nm of polymer to every surface, what is the new selectivity and SiN rate (relative)?

3. From the table in Section 4.3.1, which O₂ flow would you choose if the specification is S(SiN:Si) ≥ 15 and a SiN rate ≥ 25 nm/min? Which flow maximizes S(SiN:SiO₂)? Can one O₂ flow satisfy both?

4. A SiOCN spacer loses carbon to a depth that grows as d = k√t with k = 0.25 nm/s^½ in a CH₃F/O₂ overetch. How deep is the depleted skin after 16 s? If replacing O₂ with CO₂ reduces k by 60%, what is the new depth?

5. An inner-spacer etchback must remove 6 nm of SiN from the outer surfaces of a nanosheet stack while leaving recesses filled. With remote-plasma S(SiN:Si) = 25 and S(SiN:SiO₂) = 30, how much Si and SiO₂ is lost if the etch runs 30% over? What does this imply about required selectivity if the Si sheet budget is 0.2 nm?

---

**Previous Chapter:** [Chapter 3: Etchback Physics — Anisotropic Removal of Conformal Films](./03-etchback-physics.md)  
**Next Chapter:** [Chapter 5: Etch Reactor Architecture for Spacer Etchback](./05-reactor-architecture.md)

---

**Chapter 4 Development Status:** Complete  
**Version:** 1.0
