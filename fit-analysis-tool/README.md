# Fit Analysis & Driver Interface

**Exploratory parameter-space mapping for the BH-vacuum ansatz**

*Part of the [Recursive Black Hole Cosmology](https://doi.org/10.5281/zenodo.18783687) framework · Andrii Zlotnikov*

---

## Role in the Repository

This tool is an exploratory computational interface developed to map what classes of accretion-coupled Λ(t) dynamics are structurally accessible within the FRW framework. It was developed in parallel with the core geometric work and is retained for methodological transparency.

**The central result of the project** — that a narrow parent-mass window (log₁₀ M/M☉ ≈ 22–23) produces ΛCDM-compatible late-time expansion from the geometric ansatz Λ_geom = 1/Rs² — is established in the Evolution Sandbox (`/evolution-sandbox/`), not here.

This interface is **not** the source of that result and should not be read as independent evidence for it.

---

## Known Limitation: Mass Scale Incompatibility

This tool has a structural limitation that must be stated explicitly.

The coupling driver F(t) = (dℋ/dv)·(dv/dt) / Ṽ(t)^β is designed as a relative perturbation on the geometric baseline. The capacity scale Ṽ ~ M² means:

- At **low mass** (log₁₀ M ≪ 20): Ṽ is negligibly small, F(t) diverges, and the accretion driver dominates over the geometric baseline entirely. Any w(z) dynamics observed in this regime reflect driver pathology, not physical behavior.
- At **physical mass** (log₁₀ M ≈ 22–23): Ṽ is enormous, F(t) → 0, and the driver contribution vanishes. The model collapses to exact ΛCDM (w = −1, wₐ = 0).

**Consequence:** The exploratory parameter space in which this tool produces non-trivial dynamical dark energy trajectories is the non-physical mass regime. No self-consistent dynamical w(z) result has been demonstrated at the physically motivated mass scale. The representative runs documented below (including Run C) were obtained at log₁₀ M = 6, which is outside the physical range of the framework.

---

## What It Does

Starting from the geometric seed Λ_geom = 1/Rs², the tool numerically integrates the FRW equations and computes the resulting effective equation of state w(z). A phenomenological driver is superimposed on the geometric baseline:

> **V1 (additive):** Λ(t) = 1 + η · F(t)  
> **V2 (exponential):** Λ(t) = exp( η · [F(t) − F(t₀)] )

A CPL fit w(z) ≈ w₀ + wₐ(1−a) is computed post-hoc from the integration output. The w(z) trajectory itself is not assumed CPL — it is integrated directly.

---

## Engine Versions

**V1 — Additive driver** (archived)

The built-in floor Λ ≥ 1 structurally biases the model toward wₐ > 0, making the thawing regime inaccessible without inflating Ω_Λ. Retained for historical comparison only.

**V2 — Exponential driver** (current default)

The floor constraint is removed. Λ(t₀) = 1 is guaranteed analytically. Λ(t) < 1 is possible in the past, enabling genuine thawing behavior. The ΛCDM limit is exact: η → 0 gives w₀ = −1, wₐ = 0 identically.

---

## Representative Runs

The following runs are documented for methodological reference. **All were obtained at log₁₀ M = 6**, which is outside the physically motivated mass range of the framework (log₁₀ M ≈ 22–23). They illustrate the dynamical range of the driver parametrization, not physical predictions.

**Run A — V1 additive, high coupling (η ≈ 3.5):**

| z | w(z) | Ω_Λ(z) |
|---|------|---------|
| 5.0 | −0.611 | 0.108 |
| 1.0 | −0.575 | 0.454 |
| 0.0 | −0.757 | 0.761 |

t₀ = 11.76 Gyr · wₐ > 0 · age tension present

**Run B — V1 additive, moderate coupling (η ≈ 1.8):**

| z | w(z) | Ω_Λ(z) |
|---|------|---------|
| 5.0 | −0.636 | 0.063 |
| 1.0 | −0.674 | 0.354 |
| 0.0 | −0.871 | 0.730 |

t₀ = 12.57 Gyr · w₀ departs from −1 · wₐ > 0

**Run C — V2 exponential driver:**

| z | w(z) | Ω_Λ(z) |
|---|------|---------|
| 5.0 | −1.124 | 0.007 |
| 1.0 | −1.118 | 0.236 |
| 0.5 | −1.000 | 0.435 |
| 0.0 | −0.840 | 0.701 |

t₀ = 13.33 Gyr · phantom crossing at z ≈ 0.50 · w₀ = −0.840 · wₐ ≈ −0.34

Reference trajectory for Run C is available in `/data/`. These numerical values are not presented as observational evidence or as a fit to any survey data.

---

## Parameters

| Parameter | Symbol | Role |
|-----------|--------|------|
| Parent BH mass | log₁₀(M/M☉) | Sets geometric capacity scale Ṽ |
| Coupling amplitude | η | Controls accretion–Λ coupling strength; η = 0 → exact ΛCDM |
| Capacity exponent | q | Shape of v(t) = t^q slicing ansatz |
| Accretion timescale | τ | Decay/growth rate of the accretion driver |
| Suppression exponent | β | Modifies driver suppression; β = 1 reproduces V1 exactly |
| Ω_m, Ω_r | — | Standard FRW background priors |

η, q, τ, and β are exploration parameters of this interface only. They are not free parameters of the theory.

---

## Relationship to the Evolution Sandbox

| | Fit Analysis Tool | Evolution Sandbox |
|-|-------------------|-------------------|
| Λ source | Phenomenological driver (η, τ, β, q) | Geometric: Λ = 1/Rs² |
| w(z) shape | Dynamic in non-physical mass regime only | Effectively near −1 |
| Free parameters | η, τ, β, q (exploration only) | logM only (Ω_m, Ω_r as priors) |
| Physical mass range | Driver degenerates at logM ≈ 22–23 | logM ≈ 22–23 is the target |
| Bounce | Not implemented | LQC-inspired phase boundary |
| Purpose | Map dynamical DE parameter space | Test geometric inheritance ansatz |

---

## Scope and Limitations

- **Non-physical default regime.** Non-trivial w(z) dynamics in this tool are only accessible at mass scales (log₁₀ M ≪ 20) that are inconsistent with the core geometric framework. At the physically motivated mass scale, the driver vanishes and the model is exactly ΛCDM.
- **Phenomenological Λ sector.** Λ_eff(t) is prescribed by ansatz, not derived from a Lagrangian or action principle.
- **Background evolution only.** No perturbations, CMB spectra, or structure formation.
- **Static parent mass.** No dynamical mass evolution M(t) is modelled.
- **Minimal slicing ansatz.** v(t) = t^q has no derivation from LQC or spin-foam structures.
- **UV regulator.** The +0.5 floor is a numerical regularization, not derived from LQC microphysics.
- **Auto-fit.** Single-pass rescaling of η; exact convergence to Ω_Λ = 0.69 is not guaranteed.

---

## Relation to the Preprint

The preprint (*Recursive Black Hole Cosmology: An Interpretive Framework*, v1, February 2026) is an interpretive synthesis. It does not introduce new dynamical equations and does not perform observational fitting. This interface was developed in parallel to explore the phenomenological consequences of the geometric seed Λ = 1/Rs².

Any transition from interpretive framework to predictive model — as discussed in Section 7 of the preprint — would require explicit interior metrics, collapse invariants, and derivation of effective parameters from first principles. That step is not taken here.
