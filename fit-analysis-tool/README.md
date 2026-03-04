# Fit Analysis & Driver Interface

**Phenomenological stress-testing of the BH-vacuum ansatz**

*Part of the [Recursive Black Hole Cosmology](https://doi.org/10.5281/zenodo.18783687) framework · Andrii Zlotnikov*

---

## Role in the Repository

This tool is an exploratory computational interface developed to test what classes of Λ(t) dynamics are structurally compatible with FRW observables — before the minimal single-parameter geometric formulation was identified.

The central result of the project — that a narrow parent-mass window (log₁₀ M/M☉ ≈ 22–23) produces ΛCDM-compatible late-time expansion from the geometric ansatz Λ_geom = 1/Rs² — is established in the Evolution Sandbox (`/evolution-sandbox/`), not here.

This interface is retained for methodological transparency and as a diagnostic companion to the main sandbox.

---

## What It Does

Starting from the geometric seed Λ_geom = 1/Rs², the tool numerically integrates the FRW equations and computes the resulting effective equation of state w(z). To map the accretion-coupling parameter space, a phenomenological driver is superimposed on the geometric baseline:

> **V1 (additive):** Λ(t) = 1 + η · F(t)  
> **V2 (exponential):** Λ(t) = exp( η · [F(t) − F(t₀)] )

where F(t) = (dℋ/dv)·(dv/dt) / Ṽ(t)^β encodes the coupling between black hole accretion capacity and the effective vacuum energy.

A CPL fit w(z) ≈ w₀ + wₐ(1−a) is computed post-hoc from the integration output for comparison with observational references. The w(z) trajectory itself is not assumed CPL — it is integrated directly.

---

## Engine Versions

**V1 — Additive driver** (archived)

The built-in floor Λ ≥ 1 structurally biases the model toward wₐ > 0, making the thawing regime (w₀ > −1, wₐ < 0) inaccessible without inflating Ω_Λ. Retained for historical comparison.

**V2 — Exponential driver** (current default)

The floor constraint is removed. Λ(t₀) = 1 is guaranteed analytically. Λ(t) < 1 is possible in the past, enabling genuine thawing behavior. The ΛCDM limit is exact: η → 0 gives w₀ = −1, wₐ = 0 identically.

---

## Observed Behavior

Three representative runs across both engine versions:

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

t₀ = 12.57 Gyr · w₀ within 1σ DESI DR2 · wₐ > 0 (wrong sign)

**Run C — V2 exponential driver:**

| z | w(z) | Ω_Λ(z) |
|---|------|---------|
| 5.0 | −1.124 | 0.007 |
| 1.0 | −1.118 | 0.236 |
| 0.5 | −1.000 | 0.435 |
| 0.0 | −0.840 | 0.701 |

t₀ = 13.33 Gyr · phantom crossing at z ≈ 0.50 · w₀ = −0.840 · wₐ ≈ −0.34

Reference trajectory for Run C is available in `/data/`.

---

## Structural Observation

> At modest coupling strengths (η ≈ 1.0–1.5, q ≈ 2.0, τ ≈ 0.5–0.7) the V2 exponential driver produces a dynamical equation of state (w₀ ≈ −0.84, effective wₐ < 0, phantom crossing at z ≈ 0.5) that lies within the parameter space currently reported by DESI DR2 2025 and combined BAO+CMB+SN analyses, while maintaining Ω_Λ,eff ≈ 0.70 and t₀ ≈ 13.3 Gyr.

This is a structural observation only. No claim is made that this constitutes a statistical fit, a prediction, or a physical explanation of the data. The exponential driver is a phenomenological ansatz external to the core geometric framework.

---

## Parameters

| Parameter | Symbol | Role |
|-----------|--------|------|
| Parent BH mass | log₁₀(M/M☉) | Sets geometric capacity scale Ṽ — the primary inherited parameter |
| Coupling amplitude | η | Controls accretion–Λ coupling strength; η = 0 → exact ΛCDM |
| Capacity exponent | q | Shape of v(t) = t^q slicing ansatz |
| Accretion timescale | τ | Decay/growth rate of the accretion driver |
| Suppression exponent | β | Modifies driver suppression; β = 1 reproduces V1 exactly |
| Ω_m, Ω_r | — | Standard FRW background priors |

**Note:** η, q, τ, and β are exploration parameters of this interface only. In the core framework, FRW evolution is driven solely by parent mass M via the geometric ansatz. These parameters serve to map the sensitivity of the background dynamics to various accretion scenarios — they are not free parameters of the theory.

---

## Relationship to the Evolution Sandbox

| | Fit Analysis Tool | Evolution Sandbox |
|-|-------------------|-------------------|
| Λ source | Phenomenological driver (η, τ, β, q) | Geometric: Λ = 1/Rs² |
| w(z) shape | Dynamic — thawing or phantom crossing | Effectively near −1 |
| Free parameters | η, τ, β, q (exploration only) | logM only (Ω_m, Ω_r as priors) |
| DESI DR2 region | V2 engine: w₀ and wₐ within bounds | Not the target — geometric consistency |
| Bounce | Not implemented | LQC-inspired phase boundary |
| Purpose | Stress-test dynamical DE regime | Test geometric inheritance ansatz |

---

## Scope and Limitations

- **Phenomenological Λ sector.** Λ_eff(t) is prescribed by ansatz, not derived from a Lagrangian or action principle. No new dynamical degrees of freedom are introduced.
- **Background evolution only.** Homogeneous FRW equations. No perturbations, CMB spectra, or structure formation.
- **Static parent mass.** M enters only through the fixed capacity Ṽ(t). No dynamical mass evolution M(t) is modelled.
- **Minimal slicing ansatz.** v(t) = t^q has no derivation from loop quantum gravity or spin-foam structures. Placeholder for future work.
- **UV regulator.** The +0.5 floor (or 1e-8 when disabled) prevents singular coupling at t → 0. Not derived from LQC microphysics.
- **Auto-fit.** Rescales the phenomenological coupling η by S = 0.69/Ω_Λ,model in a single pass. Exact convergence to Ω_Λ = 0.69 is not guaranteed due to nonlinearity.
- **F₀ normalization.** The reference value F(t₀) is computed analytically at t₀ = 977.8/H₀, scaling correctly with the current H₀ slider value. The V2 normalization condition Λ(t₀) = 1 is guaranteed by construction across the full H₀ range.

---

## Relation to the Preprint

The preprint (*Recursive Black Hole Cosmology: An Interpretive Framework*, v1, February 2026) is an interpretive synthesis. It does not introduce new dynamical equations and does not perform observational fitting. This interface was developed in parallel to test the phenomenological consequences of the geometric seed Λ = 1/Rs².

Any transition from interpretive framework to predictive model — as discussed in Section 7 of the preprint — would require explicit interior metrics, collapse invariants, and derivation of effective parameters. That step is not taken here.

For the motivation behind the Λ = 1/Rs² ansatz, see the [main README](../README.md#motivation-for-the--1rs-ansatz).
