# Chapter 14: Advanced Etchback — FinFET, GAA Inner Spacers & SADP/SAQP

## Overview

The previous chapters treated spacer etchback on a planar step: one vertical wall, one floor, one film. Modern devices and patterning schemes break this picture in three ways:

1. **FinFETs** add a second, shorter set of vertical walls (the fins) that cross under the gate. The spacer must stay on the gate and leave the fins.
2. **GAA nanosheets** need spacers *inside* lateral recesses between sheets, formed by isotropic rather than anisotropic etchback.
3. **SADP/SAQP** turns the spacer into a patterning mask, where its width is the line CD and its symmetry sets pitch walking.

This chapter takes each case in turn, then introduces atomic layer etching (ALE) and quasi-ALE as tools for the most demanding steps.

**Learning Objectives:**
- Calculate the overetch needed to remove fin-sidewall spacers while keeping gate spacers, and the resulting budgets
- Describe the GAA inner-spacer sequence and the failure modes of inner-spacer etchback
- Model pitch walking in SADP and SAQP from spacer width and symmetry errors
- Explain the principles of ALE and quasi-ALE for SiN and SiO₂ spacers
- Choose between continuous, pulsed, and ALE approaches for a given step

---

## 14.1 FinFET Gate Spacer With Fin-Spacer Removal

### 14.1.1 The Geometric Conflict

```
Perspective (simplified), after conformal spacer deposition:

            gate (tall)
          ┌─────────┐
          │   HM    │
          │─────────│
     ▓▓▓▓▓│  gate   │▓▓▓▓▓      ← gate spacer: KEEP
     ▓▓▓▓▓│         │▓▓▓▓▓
  ────▓▓▓▓│         │▓▓▓▓────
  fin ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓ fin  ← fin-sidewall spacer: REMOVE
  ════▓▓▓▓══════════════▓▓▓▓════ STI

Heights above STI (illustrative, 7 nm-class):
  Fin height H_fin ≈ 50 nm
  Gate (electrode + HM) above STI ≈ 50 + 100 = 150 nm
  Spacer film t ≈ 7 nm
```

To an anisotropic etch, the fin-sidewall spacer is just like the gate spacer, only shorter. It is thick in the vertical direction (≈ H_fin + t). Removing it means etching vertically through ~H_fin of nitride after the field has cleared:

```
Field clears after removing t = 7 nm
Fin spacer clears after removing ≈ H_fin + t = 57 nm

Required overetch ≈ H_fin / t ≈ 50 / 7 ≈ 710%
```

During that overetch:

- The **gate spacer top** pulls down by about the same 50 nm (it is the same film, Chapter 10.3.1). The gate is tall enough to keep most of its spacer, but the hard mask must be thick enough that the spacer top stays above the gate electrode.
- The **fin top** is exposed to plasma for most of the step and must survive with under ~1 nm loss.
- The **STI oxide** between fins is exposed and recessed by the SiN:SiO₂ selectivity.

### 14.1.2 Budgets for the Long Overetch

```
Overetch exposure of fin top: from field clear (t = 7 nm removed) to fin
spacer clear (≈ 57 nm removed) → equivalent to 50 nm of SiN etching.

Required selectivities for budgets (illustrative):

Budget                          Allowed loss   Required selectivity
─────────────────────────────────────────────────────────────────────
Fin top (direct Si etch)        0.5 nm         S(SiN:Si) ≥ 100
STI oxide recess                5 nm           S(SiN:SiO₂) ≥ 10
Gate HM (oxide cap)             8 nm           S(SiN:SiO₂) ≥ 6
Gate spacer top vs. electrode   Spacer top     HM thickness above
                                drop ~50 nm    electrode ≥ 50 nm + margin
```

A selectivity of 100 to silicon for a 50 nm-equivalent overetch is far beyond what a continuous-bias CH₃F/O₂ process gives (10–30). FinFET fin-spacer removal therefore uses one or more of:

### 14.1.3 Strategies

```
Strategy                              Mechanism                          Trade-off
──────────────────────────────────────────────────────────────────────────────────────
Pulsed-bias, polymer-rich pull-down   Selectivity 50–100+ through        Slow; foot/residue
                                      dep/etch cycling (Ch. 6.3)         at fin base
Fin-top protection                    Oxide/nitride cap on fin top       Extra layer; must be
                                      survives the spacer etch           removed later
Partial fin-spacer retention          Pull fin spacer down only to       Fin spacer remnant
                                      a target height (e.g., 10–20 nm)   shapes epi (can be
                                                                         intentional)
Two-step: anisotropic + isotropic     Thin fin spacer with a short       Gate spacer thinned
                                      selective isotropic etch           equally
Quasi-ALE pull-down                   Self-limited removal; very high    Throughput
                                      selectivity (Section 14.4)
```

**Intentional fin-spacer remnants.** Many FinFET flows leave a short fin-sidewall spacer on purpose. It confines lateral epitaxial growth, controls epi merge between adjacent fins, and sets the epi shape. The pull-down then becomes a **height-controlled** etch with its own uniformity specification (e.g., remnant 15 ± 3 nm), rather than a "clear-all" etch.

### 14.1.4 Fin Corner Damage

The fin top corners are convex and exposed for the whole pull-down. Ion-angle effects (Chapter 3.4) and damage (Chapter 12) concentrate there. Fin-top rounding and corner amorphization directly affect the epitaxial interface. Low-energy, narrow-IED bias is especially valuable here.

---

## 14.2 GAA Inner Spacers

### 14.2.1 Process Sequence

```
Step 1: S/D cavity etch (anisotropic) through Si/SiGe superlattice
        alongside the dummy gate + gate spacer

        │gate│        │      cavity      │
        │spcr│ Si ════│                  │
        │    │ SiGe ──│                  │
        │    │ Si ════│                  │
        │    │ SiGe ──│                  │
        │    │ Si ════│                  │

Step 2: Lateral SiGe recess (isotropic, SiGe:Si selectivity ≥ 50:1)
        recess depth d_r ≈ 5–8 nm

        │    │ Si ════│
        │    │ SiGe ┐ │  ← recessed
        │    │ Si ════│

Step 3: Conformal inner-spacer film (ALD SiN, SiOCN, SiCO)
        thickness t_f > h_SiGe / 2 to pinch off the recess

        │    │ Si ════▓▓▓
        │    │ SiGe▓▓▓▓▓▓   ← recess filled (seam at mid-plane)
        │    │ Si ════▓▓▓

Step 4: Isotropic etchback: remove t_f from sheet ends and cavity walls,
        leaving plugs in recesses, flush with Si sheet ends

        │    │ Si ════│
        │    │ SiGe▓▓▓│    ← inner spacer
        │    │ Si ════│

Step 5: S/D epitaxy nucleates on clean Si sheet ends
```

### 14.2.2 Why the Etchback Is Isotropic

The film must be removed from **vertical** surfaces (Si sheet ends, which face the cavity) and kept inside **horizontal** recesses. An anisotropic etch would do the opposite: it would keep the film on vertical surfaces. The inner-spacer etchback uses the **pinch-off geometry**: inside the recess the film is thick in the lateral direction (d_r + t_f), while on the sheet ends it is only t_f thick. An isotropic etch of t_f leaves the recess plug and clears the sheet ends.

### 14.2.3 Key Metrics and Failure Modes

```
Metric / failure              Description                        Cause
───────────────────────────────────────────────────────────────────────────────────
Inner spacer thickness        Lateral plug width (target d_r)    Recess depth, etch
                                                                 overetch
Flushness (indent/protrude)   Plug face vs. Si sheet-end plane   Over/under etchback
Top-to-bottom variation       Upper sheets vs. lower sheets      Etchant transport
                                                                 in deep cavity
Seam opening                  Etchant penetrates pinch-off seam  Overetch; low film
                              → V-notch or void                  density at seam
Si sheet-end loss             Si consumed by etchback            Selectivity
Residue on sheet ends         Film or reaction residue left      Under-etch; by-
                              → blocks epi nucleation            products
SiGe exposure                 Plug too thin; SiGe exposed to     Recess non-uniformity
                              epi → defects, gate-S/D leakage    + overetch
```

### 14.2.4 Etch Amount and Tolerance

```
Example:
  SiGe layer thickness h = 10 nm, recess d_r = 6 nm
  Film t_f = 6 nm (> h/2 = 5 nm ✓ pinch-off)
  Target removal: 6 nm from sheet ends (flush)

  Overetch Δ (isotropic):
    Plug face indents by ≈ Δ
    Seam opens to a depth that grows faster than Δ (seam etch
    enhancement factor f_seam ≈ 2–5)

  Spec: indent ≤ 1.0 nm, seam ≤ 1.5 nm
    → Δ ≤ 1.0 nm and Δ × f_seam ≤ 1.5 → Δ ≤ 0.3–0.75 nm (f_seam = 2–5)

  Underetch: film left on Si sheet end → no epi nucleation
    → need Δ ≥ 0 everywhere (including bottom sheet)

  Window: 0 ≤ Δ ≤ ~0.5 nm across all sheets and the wafer
    → total etch-amount uniformity of ~±4% (3σ) on 6 nm
```

### 14.2.5 Top-to-Bottom Uniformity

In a narrow S/D cavity (width 20–30 nm, depth 60–80 nm), an isotropic etchant with non-negligible reaction probability is depleted with depth. Lower sheets see less etchant:

```
Etchant flux to sheet n (top = 1) in a cavity of AR ≈ 3:
  s = 0.01 → bottom/top ratio ≈ 0.98  (reaction-limited, uniform)
  s = 0.1  → bottom/top ratio ≈ 0.85
  s = 0.3  → bottom/top ratio ≈ 0.65

Strategy: operate in a reaction-limited regime (low reaction probability,
lower temperature, lower etchant reactivity) or use cyclic/self-limiting
removal so each cycle saturates on every sheet (Section 14.4).
```

### 14.2.6 Chemistry Choices

```
Approach                         Selectivity to Si/SiGe    Uniformity    Notes
───────────────────────────────────────────────────────────────────────────────
Remote NF₃/O₂/N₂ radical etch    SiN:Si 10–40             Good if       Continuous;
                                                          reaction-     timing-critical
                                                          limited
Hot H₃PO₄ (wet)                  SiN:Si high               Moderate      Seam attack,
                                                                         capillary/stiction
Cyclic surface modification      Very high                 Excellent     Slow; best
  + removal (quasi-ALE)                                                  control
HF-based vapor (for SiCO/        Film-dependent            Good          Low-k plugs
  oxide-like plugs)
```

---

## 14.3 SADP/SAQP Spacer Etch

### 14.3.1 SADP Geometry and Pitch Walking

```
After spacer etch and mandrel pull (SADP):

  mandrel CD = m, mandrel pitch = 2P, spacer width = w

  │▓│  core  │▓│  gap   │▓│  core  │▓│  gap
  ←w→←─ m ─→←w→←─ g ─→

  Core space:  s_core = m
  Gap space:   s_gap  = 2P − m − 2w
  Line CD:     w
  Average pitch: P

Pitch walking = s_gap − s_core = 2P − 2m − 2w

Ideal: s_core = s_gap → m = P − w
```

### 14.3.2 Sensitivities

```
∂(pitch walk)/∂m = −2
∂(pitch walk)/∂w = −2

Example: P = 32 nm (target), w = 16 nm, m = 16 nm → walk = 0
  Mandrel CD +0.5 nm → walk = −1.0 nm
  Spacer width −0.4 nm → walk = +0.8 nm

A 0.4 nm spacer width error gives 0.8 nm of pitch walking.
Spacer width control therefore needs to be about twice as tight as the
pitch-walk specification.
```

### 14.3.3 Spacer Shape and Mask Asymmetry

The ideal spacer has a rounded top on its **outer** side (Chapter 3.1). After mandrel pull, each spacer line is asymmetric: flat on the former mandrel side, rounded on the outer side:

```
After mandrel pull:

     ┌╮        ╭┐         ← each spacer: vertical inner face,
     │ ╲      ╱ │            rounded outer shoulder
     │  │    │  │
  ───┴──┴────┴──┴───

During pattern transfer, the rounded shoulder erodes faster (faceting),
so the mask edge on the outer side retreats → transferred line shifts
toward the core side and its CD shrinks.

Consequence: pitch walking appears after pattern transfer even when
             spacer widths measured at mid-height are perfect.
```

Remedies include taller mandrels (rounding is a smaller fraction of mask height), squarer spacer tops (thicker films relative to their final height, then trimmed), and transfer etches with low faceting.

### 14.3.4 SAQP: Three Spaces

In SAQP, the first-generation spacers become mandrels for a second spacer. Any asymmetry of the first spacers is inherited:

```
SAQP spaces (repeat unit of 4 lines):
  α: space left where a first-generation spacer (the second-stage
     mandrel) is pulled; equals w₁, the first spacer width
  β: between 2nd spacers across a former core (set by m₁, w₁, w₂)
  γ: between 2nd spacers across a former gap (set by P, m₁, w₁, w₂)

Each space depends on different combinations of m₁, w₁, w₂ → three
independent error sources → "pitch walking" with three space values.
Spec for 7 nm-class fins: all three within ~±1 nm of target.
```

### 14.3.5 Materials

```
Spacer material     Mandrel            Spacer etch chemistry        Notes
──────────────────────────────────────────────────────────────────────────────
SiO₂ (PEALD)        a-Si               C₄F₈/Ar or CF₄/CHF₃          Selectivity to a-Si
                                                                    mandrel top
SiO₂ (low-T ALD)    Carbon / SOC       O₂-free fluorocarbon         Protect mandrel
                                                                    (Ch. 4.4.2)
SiN                 a-Si or carbon     CH₃F/O₂ (low O₂ on carbon)   High etch
                                                                    resistance in
                                                                    transfer
TiO₂ / TiN (ALD)    Carbon / a-Si      Cl₂/BCl₃-based               BEOL SADP/SAQP;
                                                                    high selectivity
                                                                    to dielectrics
```

---

## 14.4 Atomic Layer Etching and Quasi-ALE

### 14.4.1 Principle

ALE splits etching into two **self-limiting** half-steps, repeated in cycles:

```
Step A (modification):  Change the top ~0.5–2 nm of the surface so it
                        becomes removable (e.g., fluorinate, hydrogenate,
                        deposit a thin reactant film)
Step B (removal):       Remove only the modified layer, with energy or
                        chemistry too weak to etch unmodified material

EPC (etch per cycle) is set by the modification depth, not by time.
```

Because each half-step saturates, ALE is **insensitive to flux variations**: across the wafer, between dense and isolated, and from top to bottom of a nanosheet stack. That is exactly the problem spacer etch has at its tightest steps.

### 14.4.2 Fluorocarbon-Based ALE (SiO₂, SiN)

```
Cycle:
  A: Deposit 0.3–1 nm CₓF_y film (e.g., C₄F₈ pulse, no bias)
  B: Low-energy Ar⁺ bombardment (E just above the threshold for removing
     the mixed CₓF_y/substrate layer, below the sputter threshold of the
     substrate)

EPC: ~0.3–1 nm (tuned by deposited film thickness and ion energy)
Selectivity: very high to materials that do not form volatile products
             with the deposited film at that energy (e.g., Si under
             SiO₂-ALE conditions)
Non-ideal: not perfectly self-limited; "quasi-ALE"
```

### 14.4.3 Hydrogen-Modification Quasi-ALE for SiN

```
Cycle:
  A: Low-energy H₂ (or H₂/He) plasma: H implants a few nm into SiN,
     breaking Si–N bonds and forming a modified, H-rich layer
     (depth set by H ion energy, Ch. 12.1.2)
  B: Selective removal of the modified layer only:
     - Remote fluorine radicals (NF₃-based), or
     - Dilute HF (wet), which etches modified SiN much faster than
       unmodified SiN

EPC: ~1–3 nm (set by H energy)
Strength: very high selectivity to Si and SiO₂ in step B; anisotropy
          from step A (only surfaces hit by ions are modified)
Weakness: H also reaches Si if exposed in step A → keep step A energy
          low once Si is uncovered
```

### 14.4.4 Throughput Cost

```
Cycle time (illustrative): A = 3 s, B = 4 s, purge/transition 2 × 1.5 s
                            → 10 s per cycle
EPC = 1.0 nm → 6 nm/min effective rate

For a 7 nm film:
  Full ALE:             ~7–8 cycles → ~75 s
  Hybrid:               Continuous main etch to ~1.5 nm remaining (15 s)
                        + 3 ALE cycles (30 s) → ~45 s

Hybrid "continuous main etch + ALE landing" is the common production
compromise.
```

### 14.4.5 When to Use What

```
Need                                      Approach
───────────────────────────────────────────────────────────────────────
Planar/simple gate spacer, ≥ 0.8 nm       Continuous multi-step (Ch. 4, 11)
  recess allowed
Recess ≤ 0.5 nm, moderate overetch        Pulsed bias, narrow IED overetch
FinFET fin-spacer pull-down, S ≥ 100      Pulsed/afterglow bias or quasi-ALE
GAA inner-spacer etchback, ±0.5 nm        Cyclic/self-limited isotropic removal
  across sheets
SADP/SAQP with < 1 nm pitch walk          Continuous with tight IED and
                                          temperature control; ALE for
                                          landing on sensitive mandrel/
                                          underlayers
```

---

## 14.5 Summary & Key Takeaways

1. **FinFET fin-spacer removal is a ~700% overetch.** The fin spacer is the same film as the gate spacer, only shorter. Removing it pulls down the gate spacer by the fin height and exposes the fin top for a long time.

2. **Fin-spacer pull-down needs very high selectivity.** S(SiN:Si) ≈ 100 or a protective fin cap. Many flows keep a fin-spacer remnant on purpose to shape epitaxy.

3. **GAA inner-spacer etchback is isotropic and uses pinch-off geometry.** The film is thick laterally inside recesses and thin on sheet ends. The window is roughly ±0.5 nm.

4. **Inner-spacer failures are seams, indents, residues, and top-to-bottom variation.** Reaction-limited or self-limiting removal keeps all sheets the same.

5. **In SADP, pitch walking responds at twice the spacer width error.** Spacer width control must be about twice as tight as the pitch-walk specification.

6. **Spacer-top asymmetry causes pitch walking after transfer.** Rounded outer shoulders erode faster and shift transferred lines.

7. **ALE trades speed for control.** Self-limited half-steps make removal insensitive to flux variations. Production usually uses a continuous main etch with an ALE landing.

---

## Study Questions

1. A FinFET has H_fin = 46 nm and spacer film t = 6.5 nm. What overetch percentage is needed to clear the fin-sidewall spacer completely? If the intended fin-spacer remnant is 12 nm, what overetch is needed instead?

2. For the overetch in Q1 (full clear) with an equivalent of 46 nm of SiN etching, compute fin-top loss for S(SiN:Si) = 25, 60, and 120. Which approach from Section 14.1.3 would you choose to meet 0.5 nm?

3. In a GAA stack with h_SiGe = 9 nm and d_r = 7 nm, what minimum film thickness pinches off the recess? If the etchback removes 5.5 ± 0.4 nm (3σ) and the film is 5.0 nm, what fraction of sites are underetched (residue) and what is the maximum indent?

4. In SADP with P = 28 nm, m = 15 nm, w = 13.5 nm, calculate s_core, s_gap, and the pitch walk. What spacer width gives zero pitch walk at this mandrel CD?

5. A hybrid recipe uses a continuous main etch at 30 nm/min to 1.5 nm remaining, then quasi-ALE cycles with EPC = 0.8 nm and 9 s per cycle. For an 8 nm film, how many cycles and what total etch time are needed (ignoring transitions)? Compare to a full-ALE approach.

6. Explain why ALE is less sensitive to iso-dense loading than continuous etching, and identify one way in which real quasi-ALE departs from ideal self-limitation.

---

**Previous Chapter:** [Chapter 13: Loading, Pattern Dependence & Uniformity](./13-loading-uniformity.md)  
**Next Chapter:** [Chapter 15: Endpoint, Metrology & Advanced Process Control](./15-endpoint-metrology-apc.md)

---

**Chapter 14 Development Status:** Complete  
**Version:** 1.0
