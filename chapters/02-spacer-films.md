# Chapter 2: Spacer Films — Materials & Deposition

## Overview

The spacer etch begins at the deposition step. Everything the etchback must achieve, including final width, profile, selectivity, and damage tolerance, is bounded by what the film is made of and how it was put down. A spacer etch that is perfectly tuned for one nitride will overetch, underetch, or damage a nitride deposited at a different temperature or by a different precursor.

This chapter surveys the spacer materials used in production, explains how their composition and microstructure affect both dry etchback and downstream wet cleans, and shows how deposition conformality and pattern loading turn into requirements on the etch.

**Learning Objectives:**
- Compare SiO₂, Si₃N₄, SiCN, SiOCN, and SiBCN spacers by dielectric constant, density, hydrogen content, and etch resistance
- Explain why low-k spacers are harder to etch back without damage
- Compare ALD, PEALD, PECVD, and LPCVD by conformality, film quality, and thermal budget
- Quantify how conformality and deposition non-uniformity set the etchback's overetch requirement
- Recognize sidewall-versus-field film quality differences in PEALD films and their etch consequences

---

## 2.1 Why Material Choice Matters to the Etch

A spacer material must satisfy requirements set by device performance and by the rest of the process flow:

```
Requirement                         Driven by                      Favors
────────────────────────────────────────────────────────────────────────────────
Low dielectric constant             Gate-to-contact capacitance    SiOCN, SiBCN, SiOC
Wet-etch resistance (dHF, SC1)      Pre-epi and pre-silicide cleans  Si₃N₄, SiCN
Dry-etch resistance                 Contact etch, RMG etches        Si₃N₄, SiCN
Oxidation resistance                Dummy-gate removal, anneals    Si₃N₄, SiCN, SiBCN
Low deposition temperature          SiGe intermixing, junctions    PEALD films
High conformality                   Width uniformity, 3D features  ALD/PEALD
Low hydrogen                        Bias-temperature stability     LPCVD, high-T ALD
```

No single material wins on every line. **Low-k films contain carbon, boron, or oxygen**, which lowers k but also lowers density and makes the film more sensitive to oxygen and fluorine radicals. The etch engineer inherits this compromise: the lower the k, the narrower the etch process window.

---

## 2.2 Spacer Material Families

### 2.2.1 Silicon Dioxide (SiO₂)

**Role:** Liner, offset spacer, and SADP/SAQP spacers (especially over carbon or amorphous-Si mandrels)

```
Properties (representative):

Property                  Thermal SiO₂     PEALD SiO₂ (300°C)    PEALD SiO₂ (50–100°C)
──────────────────────────────────────────────────────────────────────────────────────
Dielectric constant k     3.9              4.0–4.3               4.2–4.8
Density (g/cm³)           2.27             2.15–2.25             2.0–2.15
H content (at%)           <0.1             1–3                   3–8 (as Si–OH)
WERR in dHF*              1.0              1.5–3                 3–8
Conformality              n/a              >95%                  >95%

* WERR = wet etch rate ratio relative to thermal oxide in the same dilute HF bath
```

Low-temperature PEALD oxide is essential for SADP over photoresist or carbon mandrels, which cannot survive higher temperatures. Its higher OH content and lower density make it etch faster in both dry and wet chemistries than thermal oxide. Chapter 4 covers oxide-spacer etch chemistry.

### 2.2.2 Silicon Nitride (Si₃N₄, SiNₓ:H)

**Role:** The workhorse gate spacer from the 0.25 µm node onward; SADP spacers; inner spacers (early GAA)

```
Properties (representative):

Property               LPCVD (DCS/NH₃,    ALD/PEALD          PECVD (SiH₄/NH₃,
                       ~750–780°C)        (350–550°C)        ~400°C)
─────────────────────────────────────────────────────────────────────────────
k                      7.0–7.5            6.8–7.5            6.5–7.5
Density (g/cm³)        2.9–3.1            2.6–2.95           2.4–2.8
H content (at%)        3–8                6–15               15–25
N/Si ratio             ~1.33              1.2–1.4            0.9–1.3
WERR in dHF            0.03–0.1           0.1–1 (top)        0.5–5
                                          (sidewall higher)
Conformality           90–98%             >95%               50–80%
Stress (GPa)           +1.0 to +1.2       −2 to +1.5         −3 to +0.5
                       (tensile)          (tunable)          (tunable)
```

**Hydrogen is the key variable.** Hydrogen in SiNₓ:H sits in Si–H and N–H bonds and terminates network defects. More hydrogen means a less connected network, lower density, faster dry etch, and lower wet-etch resistance. A film with 20 at% H can etch 1.5–2× faster in a CH₃F/O₂ plasma than a 5 at% H LPCVD nitride.

### 2.2.3 Silicon Carbonitride (SiCN)

**Role:** Offset spacer, etch-stop layer, and moderate-k gate spacer

```
k ≈ 4.5–5.5, density 2.0–2.5 g/cm³, H 10–25 at%

Carbon replaces some nitrogen, lowering polarizability (lower k)
while keeping good wet-etch resistance in dHF.
Vulnerable to O₂ plasma: carbon oxidizes to CO/CO₂, leaving a
nitrogen- and oxygen-rich, higher-k, wet-etch-sensitive skin.
```

### 2.2.4 Silicon Oxycarbonitride (SiOCN)

**Role:** Mainstream low-k gate spacer from the 10 nm/7 nm generation onward

```
k ≈ 4.2–5.0, density 1.9–2.3 g/cm³
Typical composition (at%): Si 30–35, O 25–40, C 5–15, N 15–25

Oxygen lowers k further; carbon and nitrogen keep dHF resistance.
Composition is tuned for a balance:
  More O and C → lower k, but faster dHF etch and more plasma damage
  More N       → better wet and dry resistance, but higher k
```

### 2.2.5 Silicon Borocarbonitride (SiBCN)

**Role:** Low-k gate spacer alternative to SiOCN in some flows

```
k ≈ 4.0–5.0
Boron lowers k and keeps high oxidation resistance.
Fluorine chemistries form volatile BF₃. Boron-rich skins can
change etch behavior relative to SiN-tuned recipes.
```

### 2.2.6 Silicon Oxycarbide (SiOC) and Air-Gap Spacers

Below k ≈ 4, solid films become too soft and too sensitive to plasma for most gate-spacer applications. Approaches include:

- **SiOC spacers** (k ≈ 3.5–4.0), mainly in combination with a protective SiN liner
- **Air-gap spacers** (effective k → 1–2), made by removing a sacrificial layer after contact formation and sealing the gap; used mainly in DRAM bit-line spacers

Air-gap spacers bring their own etch steps: sacrificial-layer removal by isotropic etch and a sealing deposition. They are covered here only as context.

### 2.2.7 Summary Table

```
Material  k        Density   O₂-plasma     dHF          Dry etch     Typical
                   (g/cm³)   sensitivity   resistance   difficulty   use
──────────────────────────────────────────────────────────────────────────────
SiO₂      3.9–4.8  2.0–2.27  Low           Low          Low          SADP, liner
Si₃N₄     6.5–7.5  2.4–3.1   Low           High         Low–Med      Gate spacer
SiCN      4.5–5.5  2.0–2.5   High          High         Medium       Offset spacer
SiOCN     4.2–5.0  1.9–2.3   High          Medium       High         Low-k spacer
SiBCN     4.0–5.0  1.9–2.3   Medium        Medium–High  High         Low-k spacer
SiOC      3.5–4.0  1.6–2.0   Very high     Low          Very high    With SiN liner
```

---

## 2.3 Deposition Methods and Their Etch Consequences

### 2.3.1 Conformality and Step Coverage

Define **conformality** *c* as the ratio of sidewall thickness to top (field) thickness:

```
c = t_sidewall / t_field

Spacer width (ideal anisotropic etch) ≈ t_sidewall = c × t_field
```

Conformality depends on the method and on local geometry:

```
Method       Mechanism                     c (typical)    Sensitivity to AR
──────────────────────────────────────────────────────────────────────────────
Thermal ALD  Self-limiting surface rxn     0.97–1.00      Low (needs long purges)
PEALD        Self-limiting + radicals      0.92–0.99      Medium (radical recombination)
LPCVD        Surface-reaction-limited      0.90–0.98      Low–Medium
PECVD        Flux-limited, directional     0.50–0.80      High
```

### 2.3.2 The Field-Thickness Problem

The etchback must clear the **field thickness** everywhere, including the thickest spot on the wafer and in tight gaps. The spacer width tracks the **sidewall thickness**. These are not the same thickness. The etch time is set by the field film, while the CD is set by the sidewall film.

```
Example: PEALD SiN, 8.0 nm target

Location               t_field (nm)   t_sidewall (nm)   c
──────────────────────────────────────────────────────────
Isolated gate, center  8.00           7.76              0.97
Dense gate, center     8.00           7.52              0.94
Isolated, wafer edge   8.24           7.99              0.97
Dense, wafer edge      8.24           7.75              0.94

Etch must clear 8.24 nm (thickest field) → time set by edge
Spacer width range: 7.52–7.99 nm → 0.47 nm spread from deposition alone
```

The etch cannot remove deposition variation unless it is compensated (Chapter 13). Whatever the deposition delivers, the etch can at best preserve.

### 2.3.3 PEALD Sidewall Film Quality

In plasma-enhanced ALD, the plasma step (N₂, NH₃, or N₂/H₂ for nitride; O₂ for oxide) densifies the film through ion bombardment and radical exposure. Horizontal surfaces receive directional ion flux. Vertical sidewalls receive mostly radicals. The result is that **sidewall films are less dense and contain more hydrogen** than field films:

```
PEALD SiN, top vs. sidewall (representative):

                   Field (top)     Sidewall
──────────────────────────────────────────────
Density (g/cm³)    2.80            2.55–2.70
H content (at%)    8               12–15
dHF WER (nm/min)   0.5             1.5–4
Dry etch rate      1.0 (ref)       1.1–1.3×

Consequences for etchback:
  1. Sidewall etches faster laterally → more spacer thinning per unit overetch
  2. Spacer top corner (mixed quality) facets faster
  3. Post-etch dHF clean thins the spacer more than blanket data predicts
```

When qualifying a new spacer film, measure etch and wet-etch rates **on sidewalls** using TEM or OCD on patterned structures, not only on blanket wafers.

### 2.3.4 Thermal Budget Constraints

```
Constraint                                      Max deposition T
──────────────────────────────────────────────────────────────────
Planar: LDD/halo dopant diffusion               ~650–700°C (short)
FinFET: dummy poly gate, before S/D             ~600–650°C
GAA: Si/SiGe superlattice intermixing           ~550–600°C
SADP over photoresist mandrel                   ~100°C
SADP over spin-on carbon / a-C mandrel          ~200–400°C
BEOL SADP                                       ~400°C
```

Lower deposition temperature generally means more hydrogen, lower density, and faster, less selective etching. As thermal budgets have tightened, spacer etch processes have had to accept softer films.

---

## 2.4 Multi-Layer Spacer Stacks

### 2.4.1 Why Use Stacks

Combining films gives properties no single film has:

```
Common stacks (inner → outer):

Stack                      Purpose
──────────────────────────────────────────────────────────────────
SiO₂ liner / SiN           Liner is the etch stop for the SiN etchback;
                           buffers SiN stress
SiN / SiOCN                Thin SiN protects low-k from later O₂ and dHF
SiOCN / SiN cap            SiN skin on the outside protects against
                           pre-epi clean and contact etch
SiN / SiO₂ / SiN (N-O-N)   DRAM bit-line; O later removed for air gap
```

### 2.4.2 Etch Implications of Stacks

**A liner as an etch stop.** With an SiO₂ liner under a SiN spacer, the SiN etchback can run a large overetch in a nitride-selective chemistry and land on oxide. The thin oxide is then removed by a short, separate step or by a later dHF clean. The silicon never sees the nitride overetch, and substrate recess falls substantially:

```
Without liner:  SiN OE lands on Si → recess 1.0–2.0 nm (typical)
With 3 nm liner: SiN OE lands on SiO₂ (S ≈ 5–10:1) → liner thinned ~1 nm
                 Liner removed by dHF (oxide-selective to Si) → recess ~0.2–0.4 nm
```

The cost is width. The liner adds to the total spacer width and to the pitch budget.

**Stacks with different etch rates.** If inner and outer layers etch at different rates in the same chemistry, the spacer can develop a step or notch at the interface. Chapter 10 discusses profile control for stacked spacers.

---

## 2.5 Film Variation as an Input to Etch Control

### 2.5.1 Sources of Film Variation

```
Source                                  Typical magnitude
───────────────────────────────────────────────────────────
Wafer-to-wafer thickness (ALD)          ±0.5–1% (1σ)
Within-wafer thickness (ALD)            1–2% range
Chamber-to-chamber (ALD platform)       ±1–2%
Composition drift (precursor aging)     ±2–5% in C or O content
Density drift (plasma step wear)        ±1–3%
```

### 2.5.2 Feed-Forward Opportunity

Because field thickness is measured on every lot (or every wafer) after deposition, the etch can be adjusted for it. This is **feed-forward APC**:

```
t_etch = t_ME,nominal × (t_measured / t_nominal) + t_OE

Example:
  Nominal film 8.0 nm, main-etch time 20 s, overetch 8 s
  Measured film 8.3 nm (+3.75%)
  Adjusted main etch: 20 × 8.3/8.0 = 20.75 s
  Total: 28.75 s

Without feed-forward the 0.3 nm excess is cleared by the
overetch margin, which reduces the margin left for wafer-scale
non-uniformity and can leave residue at the wafer edge.
```

Chapter 15 develops this into a full APC scheme.

---

## 2.6 Summary & Key Takeaways

1. **The film sets the etch's limits.** Composition, density, and hydrogen content determine etch rate, selectivity, and damage sensitivity.

2. **Low-k means fragile.** SiOCN, SiBCN, and SiOC lower capacitance but are carbon- or oxygen-rich and easily damaged by O₂ and fluorine radicals.

3. **Hydrogen content tracks etch rate.** Low-temperature and plasma-deposited films contain more hydrogen, are less dense, and etch faster and less selectively.

4. **Etch time follows the field, width follows the sidewall.** The overetch must clear the thickest field film, while the spacer CD reflects sidewall thickness and conformality.

5. **PEALD sidewalls are softer than tops.** Lower sidewall density means faster lateral loss during overetch and wet cleans than blanket data predicts.

6. **Liners protect the substrate.** An oxide liner under a nitride spacer converts silicon recess into liner consumption, at the cost of pitch budget.

7. **Measured film thickness is a control input.** Feed-forward from deposition metrology reduces the overetch margin needed.

---

## Study Questions

1. A PEALD SiN film has field thickness 10.0 nm and conformality 0.95 on isolated gates and 0.92 on dense gates. What is the iso-dense spacer width bias from deposition alone? If the etch adds a lateral loss of 0.25 nm per side on isolated gates and 0.15 nm on dense gates, what is the total bias?

2. Two SiN films etch at 30 nm/min (LPCVD, 5 at% H) and 48 nm/min (PECVD, 20 at% H) in the same CH₃F/O₂ plasma. For a fixed etch time tuned to the LPCVD film with 30% overetch, how much overetch (in % and nm-equivalent) does an 8 nm PECVD film see?

3. A spacer stack is 2.5 nm SiO₂ liner + 7.0 nm SiN. The SiN etch has S(SiN:SiO₂) = 6:1 and runs with 40% overetch based on SiN thickness. How much liner is consumed? Is any liner left?

4. Field thickness varies 1.8% (range) across the wafer for an 8.0 nm film. Etch rate varies 2.5% (range). If the main etch is timed to clear the nominal film at nominal rate, what is the minimum overetch (in %) that clears the worst-case combination? Treat the errors as worst-case additive.

5. A SiOCN spacer has k = 4.6. After etchback, XPS shows a 1.2 nm carbon-depleted skin on each exposed face, with k ≈ 5.8. For a 6 nm spacer with the skin on one side only, what is the effective k (series model)?

---

**Previous Chapter:** [Chapter 1: Spacer Architecture & the Role of Etchback](./01-spacer-architecture.md)  
**Next Chapter:** [Chapter 3: Etchback Physics — Anisotropic Removal of Conformal Films](./03-etchback-physics.md)

---

**Chapter 2 Development Status:** Complete  
**Version:** 1.0
