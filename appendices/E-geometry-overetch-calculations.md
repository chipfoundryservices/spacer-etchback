# Appendix E: Geometry & Overetch Calculations

Derivations and worked calculations used throughout the book, collected in one place.

---

## E.1 Ideal Spacer Shape

**Setup.** Gate sidewall at x = 0 (gate at x < 0), height H. Conformal film thickness t.

**Deposited outer surface:**

```
y_dep(x) = H + t                    for x < 0
         = H + √(t² − x²)           for 0 ≤ x ≤ t
         = t                        for x > t   (with vertical face at x = t
                                                 from y = t to y = H)
```

**After vertical removal of thickness D = t + Δ (Δ = overetch depth):**

```
Ideal anisotropic etch translates the surface down by D, clipped at the
substrate (y = 0) and at the gate top.

Spacer region (0 ≤ x ≤ t):
  y_sp(x) = min(H − Δ_gate, H + √(t² − x²) − D)

  where Δ_gate = HM loss at the gate edge.

Spacer base width:  w₀ = t  (unchanged by Δ in the ideal case)
Vertical-face height: y = H − t − Δ  (where the rounded top meets x = t)
Spacer top at x = 0: y = H − Δ (or H − Δ_gate if the HM erodes more slowly
                     than the spacer top)
```

**With conformality c and lateral loss rate r_lat over total time T:**

```
w₀ = c · t − r_lat · T
```

---

## E.2 Overetch Requirement

**Clearing time at location i:**

```
t_clear,i = t_film,i / R_i

Worst case: t_clear,max = t_film,nom (1 + u_d) / (R_nom (1 − u_e'))
           ≈ t_ME,nom (1 + u_d)(1 + u_e)        with u_e ≈ u_e'/(1 − u_e')
```

**Including pattern slow-down (u_p), endpoint uncertainty (u_t), and foot time:**

```
OE_fraction ≥ (1 + u_d)(1 + u_e)(1 + u_p) − 1 + u_t + t_foot / t_ME
```

**Exposure time of the fastest-clearing location:**

```
t_exposed,max = t_ME (1 + OE_fraction) − t_clear,min
             ≈ t_ME (1 + OE_fraction) − t_ME (1 − u_d')(1 − u_e'')

where primes denote the fast-side deviations.
```

**Worked example (Ch. 3.6.2):** t_ME = 16 s, OE = 45% → total 23.2 s. If the fastest location clears 7% early (14.9 s), it is exposed for 8.3 s.

---

## E.3 Recess Model

```
Recess = Δ_direct + Δ_oxidation + Δ_damage

Δ_direct    = (R_film / S) · t_exposed
Δ_oxidation = 0.44 · d_∞ · (1 − e^(−t_exposed/τ_ox))
Δ_damage    = f_rem · d_dam(E)

Worked example:
  R_film = 24 nm/min, S = 25, t_exposed = 10 s
    Δ_direct = 0.96 × (10/60) = 0.16 nm
  d_∞ = 2.2 nm, τ_ox = 3 s
    Δ_oxidation = 0.44 × 2.2 × (1 − e^(−3.33)) = 0.968 × 0.964 = 0.93 nm
  d_dam = 2.0 nm, f_rem = 0.3
    Δ_damage = 0.60 nm
  Total ≈ 1.69 nm
```

---

## E.4 Facet Recession

```
Vertical recession of a surface inclined at θ to the substrate plane,
under vertical ion flux Γ:

  Flux per unit inclined area = Γ cos θ
  Normal recession rate       = Y(θ) Γ cos θ / n
  Vertical recession rate     = (normal rate) / cos θ = Y(θ) Γ / n

  → v_vert(θ) / v_vert(0) = Y(θ) / Y(0)

At convex corners, the orientation with maximum Y(θ) grows into a facet.
```

---

## E.5 Gap Geometry in Dense Arrays

```
Gap between deposited films:   g₀ = CPP − L_g − 2t
Gap aspect ratio:              AR = H / g₀
Max ion angle to reach floor center: θ_max = arctan(g₀ / 2H)

Sidewall view factor (2D trench, point at depth z, gap width g):
  F(z) = ½ (1 − z / √(z² + g²))

Floor neutral flux (2D trench, sticking s, approximate):
  Γ_floor / Γ_top ≈ 1 / (1 + s·AR / (2(1 − s/2)))
```

---

## E.6 FinFET Fin-Spacer Overetch

```
Vertical thickness on fin sidewall ≈ H_fin + t

Overetch to clear completely (as fraction of the field film t):
  OE = H_fin / t

Overetch to leave remnant of height h_r:
  OE = (H_fin − h_r) / t

Gate spacer pull-down ≈ (H_fin − h_r) + (field-clearing component)
Fin-top exposure ≈ equivalent SiN removal of (H_fin − h_r)
Fin-top direct loss ≈ (H_fin − h_r) / S(SiN:Si)

Example: H_fin = 50, t = 7, h_r = 15
  OE = 35/7 = 500%
  Fin-top direct loss at S = 60: 35/60 ≈ 0.58 nm
```

---

## E.7 GAA Inner-Spacer Pinch-Off and Etchback

```
Pinch-off condition: t_f ≥ h_SiGe / 2

Isotropic etchback amount for flush plugs: D = t_f (film on sheet ends)

Plug indent after overetch Δ:  ≈ Δ
Seam depth after overetch Δ:   ≈ f_seam · Δ    (f_seam ≈ 2–5)

Allowed window: 0 ≤ Δ ≤ min(indent_max, seam_max / f_seam)

Required etch-amount uniformity (3σ):
  σ_D ≤ (window width) / 6
  e.g., window 0.5 nm → σ_D ≤ 0.083 nm → ±1.4% (1σ) on 6 nm
```

---

## E.8 SADP and SAQP Spaces

**SADP:**

```
Mandrel CD m, mandrel pitch 2P, spacer width w

s_core = m
s_gap  = 2P − m − 2w
Pitch walk = s_gap − s_core = 2P − 2m − 2w
Zero walk:  m = P − w
Sensitivities: ∂walk/∂m = −2,  ∂walk/∂w = −2
```

**SAQP (first mandrel m₁ at pitch 4P, first spacer w₁, second spacer w₂):**

```
After first spacer + mandrel pull: second-stage mandrels of width w₁ at
alternating spaces m₁ (core) and 4P − m₁ − 2w₁ (gap).

Final spaces (repeat unit of four lines of width w₂):
  α = w₁                               (where first spacer is removed)
  β = m₁ − 2w₂                         (former first core)
  γ = 4P − m₁ − 2w₁ − 2w₂              (former first gap)

Target: α = β = γ = P − w₂
  → w₁ = P − w₂,  m₁ = P + w₂,  check γ: 4P − (P + w₂) − 2(P − w₂) − 2w₂
                                         = P − w₂ ✓
```

---

## E.9 Thermal Calculations

```
Wafer temperature rise:   ΔT = q / h_gap
Wafer thermal time const: τ_th = ρ c_p d / h_gap
  Si 300 mm: ρ c_p d ≈ 2.33 × 0.70 × 0.0775 ≈ 0.126 J/cm²K

Ion heat flux: q_ion = J_ion · V_s
  2.2 mA/cm² × 80 V = 0.176 W/cm²
```

---

## E.10 Cost of Ownership

```
Chamber wph = 3600 / t_cycle
Platform wph = min(N × chamber wph, transfer limit)
Annual passes W = wph × 8760 × availability × utilization
Cost per pass = annual cost / W

Break-even for a control improvement that costs Δt seconds per wafer:
  Value gained per wafer ≥ Cost per pass × (Δt / t_cycle)
  vs. yield gain ΔY × wafer value
```

---

**Appendix E Version:** 1.0  
**Last Updated:** 2026-10-04
