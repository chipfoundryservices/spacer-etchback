# Chapter 8: Wafer Temperature & Electrostatic Chuck Design

## Overview

Wafer temperature is the quiet variable in spacer etch. It is rarely the first knob an engineer reaches for, but it controls polymer sticking and desorption, so it moves selectivity, footing, lateral loss, and low-k damage, often by amounts comparable to an O₂ flow change. Unlike gas flow, it varies **across the wafer** in ways set by hardware: the electrostatic chuck (ESC), the helium backside gap, and the edge ring.

This chapter covers the temperature dependence of spacer-etch outcomes, the heat balance that sets wafer temperature during plasma, the multi-zone ESC as a uniformity tool, and the edge ring's effect on the extreme-edge spacer.

**Learning Objectives:**
- Quantify the temperature sensitivity of polymer deposition, selectivity, and spacer profile
- Compute wafer heat load and temperature rise across the He backside gap
- Explain how multi-zone ESCs compensate radial non-uniformity
- Describe edge-ring wear and its effect on ion angle and spacer symmetry at the extreme edge
- Manage thermal transients at plasma ignition and between wafers

---

## 8.1 Temperature Dependence of Spacer-Etch Outcomes

### 8.1.1 Polymer Sticking and Desorption

The polymer balance (Chapter 4.2) depends on temperature through:

- **Sticking coefficient** of polymer precursors (CFₓ, CHₓFᵧ), which falls as temperature rises
- **Thermal desorption** of weakly bound fragments, which rises with temperature
- **Reaction rates** of O atoms with polymer, which rise with temperature (Arrhenius, E_a of a few kcal/mol)

The net effect: **cooler wafers carry more polymer.**

```
Illustrative polymer thickness on Si vs. wafer temperature
(CH₃F/O₂/He overetch, fixed flows and bias):

T_wafer (°C)   δ_Si (nm)   δ_SiN (nm)   Si rate     SiN rate    S(SiN:Si)
                                         (nm/min)    (nm/min)
───────────────────────────────────────────────────────────────────────────
  0            3.6         1.0          1.2         24          20
 20            3.2         0.9          1.9         26          14
 40            2.8         0.8          2.9         28          9.7
 60            2.4         0.7          4.3         30          7.0
```

### 8.1.2 Temperature Sensitivity of Key Outputs

```
Output                         Sensitivity (per +10°C, illustrative)
─────────────────────────────────────────────────────────────────────
SiN etch rate                  +3 to +5%
Si etch rate (overetch)        +20 to +25%
S(SiN:Si)                      −15 to −20%
Lateral spacer loss            +0.05 to +0.1 nm per side
Foot height                    −0.2 to −0.4 nm
Low-k carbon depletion depth   +10 to +20%
```

At typical overetch conditions, a 2°C difference between two zones of the same wafer gives a 4–5% difference in silicon recess rate. Holding wafer temperature uniformity to ±1°C or better is a real requirement.

### 8.1.3 Using Temperature as a Tuning Knob

Since temperature changes polymer without changing ion energy or gas chemistry, it is a clean knob for local corrections:

```
Problem                            Temperature response
───────────────────────────────────────────────────────────────────
Edge foot higher than center       Raise edge zone T (less polymer)
Center Si recess higher than edge  Lower center zone T (more polymer)
Low-k damage too high              Lower T overall (slower depletion)
Residue after etch                 Raise T (less polymer)
```

---

## 8.2 Wafer Heat Balance

### 8.2.1 Heat Sources

```
Source                          Typical heat flux (W/cm²)
─────────────────────────────────────────────────────────────
Ion bombardment (J × V_s)       0.1–0.5
  e.g. 2.2 mA/cm² × 80 V = 0.18 W/cm²
Ion neutralization/recomb.      0.05–0.1
Radical recombination           0.01–0.05
Exothermic etch reactions       0.01–0.03
Radiation from plasma/window    0.02–0.1
────────────────────────────────────────────────────────────
Total                           ~0.2–0.8 W/cm²

300 mm wafer area ≈ 707 cm² → total heat load ≈ 140–560 W
```

### 8.2.2 Temperature Rise Across the He Gap

The wafer sits on the ESC with helium filling the microscopic gap between them. The gap conductance h_gap depends on He pressure and gap geometry:

```
ΔT = q / h_gap

h_gap (He at 10–20 Torr, typical ESC): ~300–1000 W/m²K (0.03–0.1 W/cm²K)

Example: q = 0.3 W/cm², h_gap = 0.05 W/cm²K
  ΔT = 0.3 / 0.05 = 6 K above ESC surface temperature

If He pressure drops 20% at the edge (He leakage at the seal band):
  h_gap ≈ 0.04 W/cm²K → ΔT = 7.5 K
  Edge is 1.5 K hotter → ~3–4% higher Si recess rate at edge
```

### 8.2.3 Thermal Time Constant

```
τ_th = (ρ c_p d) / h_gap

Si wafer: ρ = 2.33 g/cm³, c_p = 0.7 J/gK, d = 0.0775 cm
  ρ c_p d = 2.33 × 0.7 × 0.0775 ≈ 0.126 J/cm²K

h_gap = 0.05 W/cm²K → τ_th ≈ 2.5 s

The wafer reaches 95% of its plasma-on temperature in ~3τ ≈ 7.5 s.
For a 30 s spacer etch, the first ~25% of the process runs at a lower,
changing temperature.
```

This transient is one reason the **first seconds** of a spacer etch (often the breakthrough step) behave differently from the rest of the process.

---

## 8.3 Electrostatic Chuck Design

### 8.3.1 ESC Types

```
Type                 Mechanism                       Clamping     Notes
──────────────────────────────────────────────────────────────────────────
Coulombic            Dielectric (Al₂O₃), field       Moderate     Fast de-chuck;
                     across thin dielectric                       weaker at low V
Johnsen-Rahbek (JR)  Semi-conductive ceramic          High         Strong clamp at
                     (doped AlN/Al₂O₃), charge                     low V; residual
                     at interface                                  charge risk
```

### 8.3.2 Multi-Zone Temperature Control

```
Generation      Zones                 Control
─────────────────────────────────────────────────────────────────────
Legacy          1–2 (coolant only)    Uniform T, no tuning
Dual/quad zone  2–4 radial heaters    Radial tuning (center/mid/edge)
High zone       10–100+ heater pixels Radial + azimuthal tuning
                                      (die-scale correction possible)

Coolant base: typically −20 to +40°C; heaters raise local surface T
Tuning range: ±5–15°C relative between zones
```

### 8.3.3 Radial Compensation Example

```
Measured spacer width map (before tuning), r in mm:

  r:           0     50    100   130   145
  width (nm):  7.00  7.02  7.05  7.12  7.25   (edge wider: more polymer,
                                                lower edge ion flux)

Sensitivity: ∂w/∂T ≈ −0.02 nm/°C (raising T thins the spacer slightly
             by reducing sidewall polymer and adding lateral etch)

Required correction:
  r = 130 mm: −0.12 nm → +6°C
  r = 145 mm: −0.25 nm → +12.5°C (may exceed zone range; combine with
              edge O₂ tuning gas, Chapter 7.5.3)
```

Temperature zones cannot fully correct the extreme edge (r > 140 mm), where the edge ring dominates the geometry.

### 8.3.4 Azimuthal Correction

High-zone-count ESCs can correct azimuthal signatures from:

- The wafer transfer slot (pumping asymmetry)
- Coil feed position (ion-flux asymmetry)
- Gas injector placement

For SADP spacers, azimuthal width variation becomes a direct line-CD variation, so azimuthal correction can be worth the controller complexity.

---

## 8.4 The Edge Ring and the Extreme Edge

### 8.4.1 Sheath Geometry at the Wafer Edge

The edge ring (focus ring) sits around the wafer and is designed so the sheath stays flat across the wafer edge. When the ring's top surface is level with the wafer, ions arrive vertically at the edge. When the ring has eroded (it is exposed to the same plasma as the wafer), the sheath bends:

```
New edge ring (flush):              Eroded edge ring (lower):

  sheath ─────────────────          sheath ──────────╲
          ↓  ↓  ↓  ↓  ↓  ↓                  ↓  ↓  ↓  ↘ ↘
  ═══════════════════╗ ring         ═══════════════════╗
       wafer         ║════             wafer           ╚═ ring (eroded)

  Vertical ions at edge             Ions tilt outward at edge
```

### 8.4.2 Consequences for Spacers

Tilted ions hit one side of each feature more than the other:

```
Ion tilt θ_tilt at r = 147 mm (illustrative):
  New ring:         ~0°
  After 300 RF-hr:  ~0.5–1°
  After 600 RF-hr:  ~1.5–2.5°

Effect on spacer pair (left/right of the same gate):
  The side facing the wafer center is shadowed slightly; the outward-facing
  side receives more grazing ions → more lateral loss and faceting there.

  The outward-facing sidewall intercepts an ion flux fraction of about
  sin(θ_tilt) of the vertical flux: ~1.7% at 1°, ~3.5% at 2°. Over a full
  etch this adds lateral loss on that side only.
  Typical result: 0.1–0.4 nm left/right asymmetry at 1–2° tilt

For SADP, left/right asymmetry → pitch walking at the wafer edge.
```

### 8.4.3 Edge-Ring Management

```
Strategy                          Benefit                 Cost
─────────────────────────────────────────────────────────────────────────
Scheduled replacement             Simple                  Downtime, consumable
                                                          cost, step change
Movable/liftable ring             Restores sheath height  Mechanism complexity
                                  as it wears
Edge-ring RF bias tuning          Adjusts edge sheath     Additional RF control
                                  electrically
Harder materials (SiC vs. Si)     Slower wear             Particle, cost trade-offs
APC on edge spacer width          Compensates drift       Metrology load
```

Edge-ring wear produces a slow, monotonic drift in extreme-edge spacer width and symmetry. It should be tracked against RF hours and handled with a combination of mechanical adjustment and APC (Chapter 15).

---

## 8.5 Thermal Transients and First-Wafer Effects

### 8.5.1 Sources of Transients

```
Transient                              Time scale       Magnitude
──────────────────────────────────────────────────────────────────────
Wafer heat-up after plasma ignition    3–10 s           +5–15 K
ESC surface heat-up over a lot         5–10 wafers      +1–3 K
Chamber wall/window heat-up            10–25 wafers     Polymer balance shift
Idle cool-down between lots            Minutes–hours    Resets the above
```

### 8.5.2 Mitigation

```
Pre-heat / stabilization step:
  Low-power inert plasma (He or Ar) for 3–5 s before the first etch step
  Brings wafer to near-steady temperature; also stabilizes He pressure

Dummy/conditioning wafers after idle:
  1–3 seasoning wafers after idle > N minutes (N set by data, often 15–60)

Heater feed-forward:
  ESC controller anticipates plasma heat load (reduces heater power at
  plasma-on), lowering the overshoot
```

### 8.5.3 He Backside Monitoring

He flow (leak rate) and pressure are measured for every wafer. Rising He leak indicates:

- Wafer bow or backside particles (poor sealing)
- ESC surface wear
- Incomplete chucking

He leak excursions correlate with edge temperature excursions. Interlocks and SPC on He leak rate are cheap insurance against edge spacer-width and recess excursions.

---

## 8.6 Summary & Key Takeaways

1. **Cooler wafers carry more polymer.** That raises selectivity and foot height and lowers lateral loss and low-k damage.

2. **Si recess is very temperature-sensitive.** Roughly +20–25% per 10°C in overetch, so ±1°C uniformity is a real specification.

3. **The He gap sets wafer temperature rise.** ΔT = q/h_gap, about 5–10 K under plasma. He pressure loss at the edge makes the edge hotter.

4. **Multi-zone ESCs correct radial and azimuthal signatures.** Temperature is a clean knob that does not disturb ion energy or chemistry.

5. **The edge ring controls the extreme edge.** Wear tilts the sheath, which causes left/right spacer asymmetry and SADP pitch walking at the wafer edge.

6. **Transients affect the first seconds and first wafers.** Use pre-heat steps, seasoning after idle, and heater feed-forward.

---

## Study Questions

1. Using the table in Section 8.1.1, estimate the Si recess for a 10 s overetch at 20°C and at 30°C (interpolate). What temperature uniformity (±°C) keeps recess within ±5% of target?

2. Ion current density is 2.5 mA/cm² at 70 V sheath voltage. Other heat sources add 0.12 W/cm². With h_gap = 0.06 W/cm²K, what is the wafer temperature rise above the ESC? What He pressure change (as a % change in h_gap) would shift the rise by 1 K?

3. Calculate the wafer thermal time constant for h_gap = 0.08 W/cm²K. How long until the wafer reaches 95% of its steady temperature? What fraction of a 25 s etch is affected?

4. Edge spacer width is 0.20 nm wider than center at r = 140 mm. With ∂w/∂T = −0.02 nm/°C and a zone tuning range of ±8°C, can the ESC fully correct it? What else could you use?

5. An edge ring wears at 0.05 mm per 100 RF-hours, and ion tilt at the extreme edge grows by about 0.4° per 0.1 mm of wear. If left/right spacer asymmetry is 0.15 nm per degree of tilt and the limit is 0.2 nm, how many RF-hours can the ring run before replacement or adjustment?

---

**Previous Chapter:** [Chapter 7: Gas Delivery, Pressure & Radical Control](./07-gas-pressure-radicals.md)  
**Next Chapter:** [Chapter 9: Chamber Wall Conditioning & Seasoning](./09-chamber-conditioning.md)

---

**Chapter 8 Development Status:** Complete  
**Version:** 1.0
