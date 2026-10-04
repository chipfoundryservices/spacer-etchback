# Chapter 1: Spacer Architecture & the Role of Etchback

## Overview

A **spacer** is a dielectric sidewall formed on a vertical feature (a gate, a mandrel, a fin, or the wall of a recess) by depositing a conformal film and etching it back anisotropically. The spacer is **self-aligned**. Its position is set by the feature it wraps, and its width is set by the deposited film thickness. No lithography step is involved.

This chapter explains why spacers exist, how their role has grown from a junction-engineering trick into a structural element of every advanced transistor and every multipatterned layer, and what specification a modern spacer etchback must meet. It sets the vocabulary and the requirements that the rest of the book works toward.

**Learning Objectives:**
- Explain the self-aligned spacer concept and why it removes lithography from the critical dimension
- Trace the historical development: LDD spacers → offset spacers → multi-spacer stacks → inner spacers
- Identify the device functions of a spacer: junction offset, isolation, epitaxy confinement, capacitance control, pitch splitting
- Locate spacer etchback steps in FinFET, GAA, DRAM, and SADP/SAQP flows
- Write a specification sheet for a modern spacer etch and explain the origin of each line

---

## 1.1 The Self-Aligned Spacer Concept

### 1.1.1 From Conformal Film to Sidewall

Consider a gate line of height *H* and width *L* standing on a silicon substrate. A film of thickness *t* is deposited conformally, with the same thickness on the gate top, the sidewalls, and the substrate.

```
After conformal deposition:            After anisotropic etchback:

      ┌──────────────┐                        ┌──────┐
      │   film (t)   │                      ┌─┤      ├─┐
    ┌─┤ ┌──────────┐ ├─┐                    │ │ gate │ │
    │ │ │   gate   │ │ │                    │ │      │ │
    │ │ │  (H, L)  │ │ │                    │ │      │ │
────┘ │ │          │ │ └────            ────┘ │      │ └────
 film │ │          │ │ film              Si  └──────┘   Si
══════╧═╧══════════╧═╧══════          ══════════════════════
          silicon substrate                 spacer width ≈ t
```

Measured vertically, the film is *t* thick on horizontal surfaces and about *H + t* thick right next to the sidewall. A perfectly anisotropic etch that removes thickness *t* in the vertical direction clears the horizontal surfaces and leaves a sidewall spacer about *t* wide at its base.

The width is set by a deposition thickness, which ALD controls to a fraction of a nanometer. It is not set by a lithographic dimension, which carries exposure, focus, and overlay errors. This is why spacers became the basis of sub-lithographic patterning.

### 1.1.2 Three Things Lithography Cannot Do

| Capability | Lithography | Self-aligned spacer |
|------------|-------------|---------------------|
| Dimension control | CD ± 1–2 nm (3σ), dose/focus-limited | Width ± 0.3–0.5 nm (3σ), deposition-limited |
| Alignment to feature | Overlay ± 2–4 nm (3σ) | Zero by construction |
| Minimum dimension | ~38 nm half-pitch (193i single exposure) | Few nm (limited only by film continuity) |

The trade-off is that a spacer can only **follow** existing topography. It cannot create a new shape. Every spacer process is about turning an existing edge into a new, precisely offset edge.

---

## 1.2 Historical Development

### 1.2.1 The Lightly Doped Drain (Early 1980s)

As MOSFET channel lengths dropped toward 1 µm, the peak lateral electric field at the drain end of the channel grew strong enough to inject hot carriers into the gate oxide. Threshold voltages drifted and transconductance degraded over the device's life. The **lightly doped drain (LDD)** structure, described by Ogura and co-workers at IBM in 1980, addressed this with a two-step implant:

```
LDD process sequence:

1. Pattern gate
2. Light implant (n⁻), self-aligned to gate edge
3. Deposit conformal CVD SiO₂ (~150–300 nm at the time)
4. Anisotropic etchback → oxide spacers
5. Heavy implant (n⁺), self-aligned to spacer edge
6. Anneal

Result:
   gate
  ┌────┐
 ┌┤    ├┐
 │└────┘│
─┴──────┴─
n⁺ │n⁻│  channel  │n⁻│ n⁺
   └──┘           └──┘
   spacer sets the n⁻ extension length
```

The spacer width directly set the length of the n⁻ extension, and therefore the peak field. This was the first production use of reactive ion etching to form a self-aligned dielectric feature. Etch engineers immediately ran into the problems this book addresses: footing at the spacer base, silicon damage in the source/drain region, and width variation across the wafer.

### 1.2.2 Offset and Multi-Spacer Stacks (0.25 µm – 28 nm)

As junctions became shallower and gate lengths shrank, a single spacer could no longer set all the lateral offsets needed:

```
Typical planar 45 nm-era spacer stack:

        ┌──────┐
     ┌──┤      ├──┐
   ┌─┤ ┌┤ gate ├┐ ├─┐
   │ │ ││      ││ │ │
   │ │ ││      ││ │ │
───┘ └─┴┴──────┴┴─┘ └───
   │ │ │        │ │ │
   │ │ └ offset spacer (SiN or SiO₂, 3–8 nm): sets extension/halo offset
   │ └── liner oxide (2–5 nm): etch stop and stress buffer
   └──── main spacer (SiN, 20–40 nm): sets deep S/D and silicide offset
```

- **Offset spacer (spacer 0):** thin, sets the offset of the extension and halo implants from the gate edge to control overlap capacitance and short-channel effects.
- **Liner:** thin oxide under the main nitride, providing an etch stop for the nitride etchback and a stress buffer.
- **Main spacer:** sets the offset of the deep source/drain implant and keeps silicide away from the channel.

With strained-silicon technologies came **disposable spacers**. They were formed to set the position of an embedded SiGe recess or a stress liner and then stripped. Each added another etchback, and each etchback added another increment of silicon recess.

### 1.2.3 FinFET Gate Spacers (22/16 nm – 5 nm)

FinFETs made the spacer etch three-dimensional. The spacer film now coats both the gate (tall) and the fins (shorter, crossing under the gate). The etch must:

- **Keep** the spacer on the gate sidewalls, full height
- **Remove** the spacer from the fin sidewalls in the source/drain region so epitaxy can grow on the full fin
- **Not** recess the fin top or damage it

These goals pull in different directions. Chapter 14 treats them in depth. They make FinFET spacer etch one of the most demanding dielectric etches in the flow.

### 1.2.4 GAA Inner Spacers (3 nm and Below)

In nanosheet (GAA) transistors, the gate wraps each silicon sheet. During replacement-gate processing the sacrificial SiGe layers between the sheets are removed and replaced with metal gate. Without isolation, that metal gate would sit right next to the source/drain epitaxy. The **inner spacer** is a dielectric plug a few nanometers thick that fills a lateral recess at the end of each SiGe layer:

```
Cross-section along the channel (one side shown):

   gate spacer  │ S/D epi
   ┌───────┐    │
   │ dummy │    │
   │ gate  │    │
═══╪═══════╪════╡  Si sheet 3
   │ SiGe  │▓▓▓▓│  ← inner spacer (SiN/SiOCN), 5–8 nm lateral
═══╪═══════╪════╡  Si sheet 2
   │ SiGe  │▓▓▓▓│  ← inner spacer
═══╪═══════╪════╡  Si sheet 1
   │ SiGe  │▓▓▓▓│  ← inner spacer
───┴───────┴────┴──────────
          substrate
```

Inner-spacer etchback is usually **isotropic**, not anisotropic. Conformal film fills the recesses and is then removed everywhere except inside them. This reverses the usual spacer logic, and Chapter 14 covers it separately.

### 1.2.5 Spacer-Based Patterning (SADP/SAQP)

In self-aligned double patterning, a sacrificial **mandrel** is patterned at twice the target pitch. A spacer is formed on both sides of every mandrel, the mandrel is removed, and the spacers become the hard mask for the next etch:

```
SADP sequence:

1. Mandrels at pitch 2P:      ██      ██      ██
2. Conformal spacer film:    ▓██▓    ▓██▓    ▓██▓
3. Spacer etchback:          ▓██▓    ▓██▓    ▓██▓  (tops and floors cleared)
4. Mandrel pull:             ▓  ▓    ▓  ▓    ▓  ▓
5. Result: lines at pitch P, line width = spacer width
```

Here the spacer width **is** the final line CD. SAQP repeats the process to reach pitch P/2. Fins at 7 nm and below, and the tightest metal layers, are typically defined this way. The spacer etch has to deliver symmetric, square profiles. Any left/right asymmetry turns into **pitch walking**, an alternating error in the spaces between lines (Chapter 14).

---

## 1.3 Device Functions of a Spacer

### 1.3.1 Junction Offset

The spacer sets how far the heavily doped source/drain sits from the channel. For a raised or embedded epitaxial source/drain, it sets how close the epitaxy grows to the gate.

```
Effect of spacer width on drive current (illustrative, planar nMOS):

Spacer width   Extension length   R_ext (Ω·µm)   I_on change
──────────────────────────────────────────────────────────────
  20 nm            ~20 nm            ~180            baseline
  15 nm            ~15 nm            ~140            +5–7%
  10 nm            ~10 nm            ~100            +10–14%
   5 nm             ~5 nm             ~65            +15–20% (but SCE degrades)

Trade-off: narrower spacer → lower series resistance → higher I_on,
           but the junction moves closer to the channel → worse DIBL,
           higher overlap capacitance, and higher leakage.
```

### 1.3.2 Gate-to-Contact Isolation and Capacitance

At a 7 nm-class node, contacted poly pitch (CPP) is about 48–57 nm. The pitch budget looks like this:

```
CPP budget (illustrative, CPP = 48 nm):

  ┌ contact ┐┌sp┐┌ gate ┐┌sp┐┌ contact ┐
  │  18 nm  ││ 7││ 16   ││ 7││  (shared)│
  └─────────┘└──┘└──────┘└──┘└──────────┘

  CPP = L_g + 2 × w_spacer + w_contact
  48  = 16  + 2 × 7         + 18   ✓

A 1 nm loss of spacer width on each side gives 2 nm to the contact
or the gate, but it reduces gate-to-contact isolation from 7 nm to 6 nm.
At ~1 V operation that raises the field across the spacer by ~17%.
```

The gate-to-contact parasitic capacitance scales roughly as:

```
C_gc ≈ ε₀ · k_spacer · (H_overlap × W) / w_spacer

Example (per µm of gate width):
  H_overlap = 40 nm, w_spacer = 7 nm
  k = 7.0 (Si₃N₄):  C_gc ≈ 8.85e-12 × 7.0 × (40e-9 × 1e-6) / 7e-9
                        ≈ 0.354 fF/µm
  k = 5.0 (SiOCN):  C_gc ≈ 0.253 fF/µm  (−29%)
  k = 4.0 (SiBCN):  C_gc ≈ 0.202 fF/µm  (−43%)
```

This is why low-k spacer materials matter, and why an etch that raises the spacer's k by depleting carbon is a real performance loss (Chapter 12).

### 1.3.3 Epitaxy Confinement and Gate Protection

During selective source/drain epitaxy, the spacer and gate hard mask together must completely encapsulate the gate. Any exposed polysilicon or amorphous silicon becomes a nucleation site for **mushroom defects**: parasitic epitaxial nodules that can short gate to source/drain. The spacer etchback must therefore:

- Leave the gate hard mask intact (limit faceting and cap erosion, Chapter 10)
- Leave the spacer full height to the top of the gate
- Leave no thin spots at the gate top corner

### 1.3.4 Pitch Splitting

In SADP/SAQP, the spacer is a patterning material. Its required properties are etch resistance in the downstream pattern transfer, a vertical profile, and symmetric shape. Its device role is indirect, but its CD role is direct.

---

## 1.4 Where Spacer Etchback Appears in Modern Flows

### 1.4.1 FinFET Logic Front End (Illustrative)

```
Front-end spacer-etch passes in a FinFET logic flow:

Step                                   Film               Etch type
────────────────────────────────────────────────────────────────────────
Fin SAQP mandrel spacer (×2)           SiO₂ or SiN        Anisotropic
Dummy gate SADP spacer (if used)       SiO₂               Anisotropic
Gate offset spacer                     SiN / SiCN         Anisotropic
Main gate spacer + fin spacer removal  SiOCN / SiN        Anisotropic, high OE
nFET/pFET S/D cavity spacer (×2)       SiN                Anisotropic
Contact liner / CESL open (some flows) SiN                Anisotropic

Typical total: 6–10 front-end spacer etchbacks
```

### 1.4.2 GAA Additions

```
GAA adds:
  Inner spacer isotropic etchback        SiN / SiOCN        Isotropic, selective
  Possible bottom dielectric isolation   SiN / SiO₂         Mixed
```

### 1.4.3 Back End and Memory

```
BEOL:   SADP/SAQP spacer etch for tight-pitch metal (M0–M2): 1–2 per layer
DRAM:   Bit-line spacer (often air-gap or N/O/N), storage-node contact spacer
3D NAND: Peripheral CMOS gate spacers; SADP for bit lines
```

A leading-edge logic flow can contain **15–30 spacer etchbacks** in total. Even a small improvement per pass, such as 0.2 nm less silicon recess or 0.1 nm tighter width control, adds up across the flow.

---

## 1.5 Specification of a Modern Spacer Etch

### 1.5.1 Representative Specification Sheet

```
Spacer etchback specification (illustrative FinFET main gate spacer)

Parameter                          Target           Limit (3σ)    Origin
─────────────────────────────────────────────────────────────────────────────
Spacer width at gate mid-height    7.0 nm           ±0.4 nm       CPP budget, C_gc
Spacer width at base (footing)     ≤ 7.5 nm         —             Epi proximity
Spacer top height (below HM top)   ≤ 3 nm loss      —             Mushroom defect
Gate HM loss                       ≤ 5 nm           ±1.5 nm       RMG CMP margin
Fin-sidewall spacer residue        ≤ 2 nm height    —             Epi volume
Fin top recess                     ≤ 1.0 nm         ±0.3 nm       Channel/R_ext
Damaged layer on fin (TEM)         ≤ 2 nm           —             Epi quality
Spacer k after etch (blanket)      Δk ≤ +0.2        —             C_gc
WIW spacer width range             ≤ 0.6 nm         —             Parametric
Iso-dense spacer width bias        ≤ 0.5 nm         —             Design rules
Particles (>32 nm adders)          ≤ 10 per wafer   —             Yield
Throughput                         ≥ 45 wph/chamber —             Cost
```

### 1.5.2 The Competing Demands

Every line on this sheet competes with at least one other:

```
Increase overetch      → ✓ fin residue, ✓ footing   ✗ fin recess, ✗ HM loss
Increase ion energy    → ✓ footing, ✓ anisotropy    ✗ damage, ✗ faceting
Increase polymer       → ✓ selectivity, ✓ recess    ✗ footing, ✗ iso-dense bias
Increase O₂            → ✓ less residue             ✗ Si oxidation/recess, ✗ low-k damage
Lower temperature      → ✓ selectivity              ✗ footing, ✗ polymer residue
```

Spacer etch engineering means finding the point in this multi-dimensional space where every specification is met with margin, and then keeping the process there as the chamber ages.

---

## 1.6 Summary & Key Takeaways

1. **The spacer is self-aligned.** Its position comes from an existing edge and its width from deposited thickness, so lithographic CD and overlay errors drop out.

2. **Spacers grew from a junction trick into structural elements.** LDD → offset/main spacer stacks → FinFET gate spacers → GAA inner spacers → SADP/SAQP masks.

3. **Spacer width is a device parameter.** It sets junction offset, series resistance, gate-to-contact isolation, and in SADP/SAQP the final line CD.

4. **The spacer's k matters.** Moving from Si₃N₄ (k ≈ 7) to SiOCN (k ≈ 5) cuts gate-to-contact capacitance by about 30%, as long as the etch does not degrade the film.

5. **Spacer etches repeat many times.** 15–30 passes per advanced logic flow means small per-pass effects add up.

6. **Every specification competes with another.** Overetch, ion energy, polymer, oxygen, and temperature each improve some metrics and degrade others.

---

## Study Questions

1. A conformal SiN film of 9.0 nm is deposited on a 100 nm tall gate. Conformality (sidewall/top thickness) is 0.95. Assuming a perfectly anisotropic etch with no lateral loss, what is the spacer width at the base? What is it if the etch also has a lateral component of 3% of the vertical rate and runs for a 40% overetch?

2. For CPP = 51 nm, L_g = 18 nm, and a minimum contact width of 19 nm, what is the maximum spacer width? If the spacer width tolerance is ±0.5 nm (3σ), what nominal width keeps the contact at or above minimum at +3σ?

3. Using the C_gc expression in Section 1.3.2, calculate the percentage change in gate-to-contact capacitance if a 7 nm SiOCN spacer (k = 5.0) suffers a 1.5 nm carbon-depleted skin with k = 6.5 on the contact side. Treat the two layers as series capacitors.

4. A logic flow exposes the same source/drain silicon region to four spacer etchbacks, each causing 0.7 ± 0.2 nm (1σ) of recess. Assuming independent passes, what is the mean and 3σ of the cumulative recess?

5. In SADP, mandrel CD is 24 nm at a mandrel pitch of 64 nm, and the spacer width is 16 nm. Calculate the resulting line pitch, the line CD, and the two alternating space widths. What mandrel CD gives equal spaces?

---

**Next Chapter:** [Chapter 2: Spacer Films — Materials & Deposition](./02-spacer-films.md)

---

**Chapter 1 Development Status:** Complete  
**Version:** 1.0
