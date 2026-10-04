# Appendix A: Spacer Material Properties

Representative properties of spacer films and the materials they are etched against. Values vary with deposition method, temperature, and precursor. Use them for estimates and screening, and replace them with measured data from your own films for process work.

---

## A.1 Spacer Dielectrics

### A.1.1 Electrical and Physical Properties

```
Material          k          Density     H content   Refractive     Breakdown
                             (g/cm³)     (at%)       index (633nm)  (MV/cm)
───────────────────────────────────────────────────────────────────────────────
SiO₂ (thermal)    3.9        2.27        <0.1        1.46           10–12
SiO₂ (PEALD,      4.0–4.3    2.15–2.25   1–3         1.45–1.47      8–10
  ~300°C)
SiO₂ (PEALD,      4.2–4.8    2.0–2.15    3–8         1.44–1.46      6–9
  50–100°C)
Si₃N₄ (LPCVD)     7.0–7.5    2.9–3.1     3–8         1.98–2.02      8–10
SiN (ALD/PEALD)   6.8–7.5    2.6–2.95    6–15        1.90–2.00      6–9
SiN (PECVD)       6.5–7.5    2.4–2.8     15–25       1.85–2.00      4–7
SiCN              4.5–5.5    2.0–2.5     10–25       1.85–2.10      4–7
SiOCN             4.2–5.0    1.9–2.3     5–15        1.60–1.80      5–8
SiBCN             4.0–5.0    1.9–2.3     5–15        1.75–1.90      5–8
SiOC              3.5–4.0    1.6–2.0     10–20       1.45–1.55      4–6
```

### A.1.2 Mechanical and Thermal Properties

```
Material          Young's modulus   Film stress            Thermal conductivity
                  (GPa)             (GPa, typical)         (W/m·K)
────────────────────────────────────────────────────────────────────────────────
SiO₂ (thermal)    70                −0.3 (compressive)     1.4
SiO₂ (PEALD)      55–70             −0.2 to +0.1           1.0–1.3
Si₃N₄ (LPCVD)     250–300           +1.0 to +1.2 (tens.)   ~3 (thin film)
SiN (PEALD)       150–250           −2 to +1.5 (tunable)   1.5–3
SiN (PECVD)       100–200           −3 to +0.5 (tunable)   1–2
SiCN              100–200           −0.5 to +0.5           1–2
SiOCN             60–120            −0.3 to +0.3           0.8–1.5
SiBCN             80–150            −0.5 to +0.5           0.8–1.5
```

### A.1.3 Wet-Etch Resistance

Wet etch rate ratio (WERR) relative to thermal SiO₂ in the same dilute HF bath:

```
Material                 WERR in dHF       Hot H₃PO₄ (~160°C)    SC1 (dilute, ~50°C)
───────────────────────────────────────────────────────────────────────────────────────
SiO₂ (thermal)           1.0               Very slow             Very slow
SiO₂ (PEALD, 300°C)      1.5–3             Very slow             Slow
SiO₂ (PEALD, low T)      3–8               Slow                  Slow
Si₃N₄ (LPCVD)            0.03–0.1          Fast (~4–6 nm/min)    Very slow
SiN (PEALD, top)         0.1–1             Fast                  Slow
SiN (PEALD, sidewall)    0.3–3             Fast                  Slow
SiN (PECVD)              0.5–5             Fast                  Slow
SiCN                     0.05–0.3          Slow–moderate         Very slow
SiOCN                    0.2–1.5           Moderate              Slow
SiBCN                    0.1–0.8           Slow–moderate         Slow
Plasma-damaged low-k     5–50              —                     Moderate
  skin
```

### A.1.4 Atom Densities (for Etch-Rate Calculations)

```
Material         Formula unit    Density (g/cm³)   Atoms/cm³        Si atoms/cm³
──────────────────────────────────────────────────────────────────────────────────
SiO₂             60.08 g/mol     2.27              6.8 × 10²²       2.3 × 10²²
Si₃N₄            140.28 g/mol    3.00              9.0 × 10²²       3.9 × 10²²
Si               28.09 g/mol     2.33              5.0 × 10²²       5.0 × 10²²
Si₀.₇Ge₀.₃       41.5 g/mol avg  ~3.3              4.85 × 10²²      3.4 × 10²²

Conversion: atoms/cm³ = (ρ / M) × N_A × (atoms per formula unit)
```

---

## A.2 Substrate and Mandrel Materials

```
Material         Role in spacer etch           Key etch behavior
─────────────────────────────────────────────────────────────────────────────
Crystalline Si   S/D region, fin, sheet ends   Polymer-protected; oxidizes in O₂;
                                               H-sensitive
SiGe (20–40% Ge) pFET S/D, GAA sacrificial     Etches 1.5–3× faster than Si in F;
                                               Ge-oxide water-soluble
Poly-Si / a-Si   Dummy gate, SADP mandrel      Similar to Si; a-Si slightly faster
Amorphous carbon SADP mandrel, hard mask       O-sensitive: avoid O₂ when exposed
Spin-on carbon   SADP mandrel                  O-sensitive; low thermal budget
SiO₂ (STI)       Isolation between fins        Exposed during fin-spacer pull-down
Gate HM (SiO₂/   Gate cap                      Facet-sensitive at corners
  SiN)
```

---

## A.3 Material Selection Checklist for a New Spacer

```
☐ k target and its effect on C_gc (Ch. 1.3.2)
☐ Deposition temperature vs. thermal budget (Ch. 2.3.4)
☐ Conformality on the tightest pattern (Ch. 2.3.1)
☐ Sidewall vs. top film quality (PEALD) (Ch. 2.3.3)
☐ dHF WERR (top and sidewall) vs. pre-epi clean budget
☐ Dry-etch rate and selectivity in candidate chemistry (Ch. 4)
☐ O₂-plasma sensitivity (carbon depletion rate K) (Ch. 12.3)
☐ Resistance to SAC etch and RMG chemistries (Ch. 16.2)
☐ Stress and adhesion (lifting, collapse in SADP)
☐ Metrology: OCD optical constants measured on the actual film
```

---

**Appendix A Version:** 1.0  
**Last Updated:** 2026-10-04
