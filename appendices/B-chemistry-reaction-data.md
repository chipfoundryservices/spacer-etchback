# Appendix B: Chemistry & Reaction Data

Reference data for spacer-etch chemistry. Bond energies are representative averages for bonds in solids or molecules, intended for qualitative comparison. Values from different sources differ by a few percent.

---

## B.1 Feed Gas Properties

```
Gas      MW        (F/C)_eff   Ionization      Global warming    Role
         (g/mol)               energy (eV)     potential (GWP100,
                                               IPCC AR5)
──────────────────────────────────────────────────────────────────────────────
CF₄      88.0      4.0         ~16.2           6,630            Breakthrough,
                                                                fast etch
CHF₃     70.0      2.0         ~13.9           12,400           Main etch
CH₂F₂    52.0      0.0         ~12.7           677              Selective
                                                                main/OE
CH₃F     34.0      −2.0        ~12.5           116              Selective OE
C₄F₈     200.0     2.0         ~11.6–12.3      9,540            Oxide etch
C₄F₆     162.0     1.5         ~10.4           <1               Oxide etch
                                                                (selective)
NF₃      71.0      —           ~12.9           16,100           Remote F, WAC
SF₆      146.1     —           ~15.3           23,500           WAC (some tools)
O₂       32.0      —           12.07           0                Polymer control
CO₂      44.0      —           13.78           1                Mild oxidizer
CO       28.0      —           14.01           —                C source, mild
N₂       28.0      —           15.58           0                Polymer modifier
H₂       2.0       —           15.43           —                F scavenger
Ar       39.9      —           15.76           0                Diluent
He       4.0       —           24.59           0                Diluent
```

**Environmental note:** High-GWP gases (CHF₃, NF₃, SF₆, CF₄, C₄F₈) need point-of-use abatement. CH₃F and CH₂F₂ have far lower GWP, and C₄F₆ is negligible. Gas choice for spacer etch therefore also affects a fab's emissions inventory.

---

## B.2 Representative Bond Energies

```
Bond      Energy (eV)   Energy (kJ/mol)   Relevance
───────────────────────────────────────────────────────────────────────
Si–Si     ~2.3          ~225              Si lattice; easiest Si bond to break
Si–H      ~3.3          ~320              H-terminated Si, SiNₓ:H
Si–C      ~3.3          ~320              SiCN, SiOCN network
Si–N      ~3.5–4.0      ~340–385          Si₃N₄ network
Si–O      ~4.5–4.7      ~440–455          SiO₂ network (strongest Si bond
                                          in the film set)
Si–F      ~5.7–6.0      ~550–580          Driving force for SiF₄ formation
C–H       ~4.3          ~415              Polymer, CH₃F
C–F       ~5.0–5.4      ~485–520          Polymer, fluorocarbons
H–F       ~5.9          ~570              HF formation (F scavenging)
C–N (CN)  ~7.8          ~750              CN radical: stable product
N≡N       ~9.8          ~945              N₂ product
C≡O       ~11.1         ~1,075            CO product: strong sink for C+O
```

The ordering Si–Si < Si–N < Si–O explains the baseline etch-resistance ordering Si < Si₃N₄ < SiO₂ under purely chemical attack. The polymer layer (Ch. 4.2) rearranges the practical selectivities.

---

## B.3 Etch Products

```
Film       Main products                   Notes
──────────────────────────────────────────────────────────────────────
SiO₂       SiF₄, CO, CO₂, COF₂             O consumes polymer carbon
Si₃N₄      SiF₄, N₂, FCN, HCN, NF₃ (minor) N consumes carbon via CN
Si         SiF₄ (SiFₓ radicals)            No C consumption → thick polymer
SiCN       SiF₄, HCN, FCN, CO (if O)       Film C adds to polymer budget
SiOCN      SiF₄, CO, CO₂, HCN, FCN         O and N both consume C
SiBCN      SiF₄, BF₃, HCN, FCN             BF₃ volatile
SiGe       SiF₄, GeF₄                      GeF₄ bp −36.5°C (sublimes)
```

### B.3.1 Product Volatility

```
Product   Boiling / sublimation point (°C)
────────────────────────────────────────────
N₂        −196
CO        −191
NF₃       −129
BF₃       −100
SiF₄      −86 (sublimes)
COF₂      −85
CO₂       −78 (sublimes)
FCN       −46
GeF₄      −36.5 (sublimes)
C₂N₂      −21
HF        +20
HCN       +26
```

---

## B.4 Electron-Impact Processes (Selected)

```
Process                               Threshold (eV, approx.)
────────────────────────────────────────────────────────────────
O₂ + e → O + O + e (via excitation)   ~6–8 (bond energy 5.1)
O₂ + e → O₂⁺ + 2e                     12.1
CH₃F + e → CH₃ + F + e                ~5–6 (C–F bond ~4.9–5.1)
CH₃F + e → CH₂F + H + e               ~4.5–5
CH₃F + e → CH₃F⁺ + 2e                 ~12.5
H₂ + e → H + H + e                    ~8.8 (via b³Σ state)
N₂ + e → N + N + e                    ~10–12 (bond 9.8)
NF₃ + e → NF₂ + F⁻ (attachment)       ~0–2 (dissociative attachment)
Ar + e → Ar* (metastable)             11.5
Ar + e → Ar⁺ + 2e                     15.76
```

---

## B.5 Useful Constants and Conversions

```
1 sccm                   = 4.48 × 10¹⁷ molecules/s = 0.0127 Torr·L/s
1 mTorr at 300 K         = 3.22 × 10¹³ molecules/cm³
1 eV                     = 1.602 × 10⁻¹⁹ J = 96.5 kJ/mol = 23.06 kcal/mol
kT at 300 K              = 0.0259 eV
Mean speed v̄             = √(8kT/πM) → 4.4 × 10⁴ cm/s for M = 33 amu at 300 K
Neutral flux             = n·v̄/4
Si consumed per nm SiO₂  ≈ 0.44 nm
1 mA/cm² ion current     = 6.24 × 10¹⁵ ions/cm²·s
```

---

**Appendix B Version:** 1.0  
**Last Updated:** 2026-10-04
