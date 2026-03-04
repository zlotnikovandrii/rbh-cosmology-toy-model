# Recursive Black Hole Cosmology — Research Repository

**Andrii Zlotnikov** · Independent Researcher  
[![ORCID](https://img.shields.io/badge/ORCID-0009--0003--2607--0269-a6ce39?logo=orcid&logoColor=white)](https://orcid.org/0009-0003-2607-0269)
[![Preprint](https://img.shields.io/badge/Preprint-Zenodo%2018783687-4fa3d1?logo=zenodo&logoColor=white)](https://doi.org/10.5281/zenodo.18783687)
[![Software](https://img.shields.io/badge/Software-Zenodo%2018822173-4fa3d1?logo=zenodo&logoColor=white)](https://doi.org/10.5281/zenodo.18822173)

---

## Overview

This repository accompanies the preprint *Recursive Black Hole Cosmology: An Interpretive Framework* (v1, February 2026). It investigates the structural implications of a single geometric ansatz:

> **Λ_geom = 1 / Rs²**, where Rs = 2GM / c² is the Schwarzschild radius of a parent black hole.

The framework introduces no new fields, no modified gravitational equations, and no additional dynamical degrees of freedom. All computational tools are structural consistency tests, not predictive cosmological models.

Consistency is evaluated through two complementary lenses: a pure geometric evolution sandbox and a dynamical accretion-driven diagnostic interface.

---

## Relationship between Preprint and Computational Tools

The preprint (v1, February 2026) establishes an interpretive framework without introducing new physical equations or constants. The computational tools in this repository explore one specific structural ansatz — **Λ_geom = 1 / Rs²** — that was identified during numerical investigation carried out after the preprint was written.

This ansatz is not derived from the interpretive framework; it is a candidate numerical realization of its central conjecture. The models are presented as exploratory numerical studies of structural compatibility, not as physical predictions or extensions of the preprint.

The bounce regularization parameter **Ec²** is a free numerical parameter of the integrator, not a new physical constant — it controls the scale at which classical FRW breaks down in the simulation, does not affect late-time dynamics, and has no derived value within the framework.

---

## Structural Result

Numerical integration of the FRW sector reveals a narrow parent-mass window (log₁₀ M/M☉ ≈ 22–23) in which the inherited geometric vacuum scale produces ΛCDM-like late-time expansion — without a free dark-energy parameter.

This selection effect arises from internal FRW consistency constraints and is presented as a structural observation, not an observational fit or prediction.

Diagnostic runs using the accretion-driver interface (V2 exponential engine) further show that introducing a phenomenological coupling at moderate strength produces a dynamical equation of state overlapping with the w₀–wₐ confidence region reported by current DESI constraints — while maintaining Ω_Λ ≈ 0.70 and t₀ ≈ 13.3 Gyr. This is noted as a structural feature of the driver form, not a prediction.

---

## Conceptual Context

The project connects to the broader Black Hole Universe paradigm (Pathria 1972; Gaztañaga 2022) and to cosmological natural selection (Smolin 1992), but differs in focus: rather than exploring reproduction rates or parameter variation, it tests whether the vacuum energy scale can be geometrically inherited from a parent Schwarzschild radius.

Its distinctive feature is the focus on a **minimal geometric inheritance**: the dark energy scale is determined solely by the horizon radius of a parent black hole, without additional dynamical mechanisms or parameter variation.

The relation Λ = 1/Rs² is not derived from a fundamental theory. It is treated as an explicit structural ansatz — the sole interpretive link between the parent black hole and the internal FRW cosmology. All other dynamics follow from standard GR and the Friedmann equations.

---

## Motivation for the Λ = 1/Rs² Ansatz

Under causal isolation within a parent event horizon, the Schwarzschild radius R_s is the unique inherited geometric scale. Since Λ carries dimensions of [length]⁻², the relation Λ = 1/R_s² is the only dimensionally consistent scaling that introduces no additional constants or degrees of freedom. Any alternative (e.g., 1/R_s^n for n ≠ 2) would require a new, arbitrary length scale, violating the framework's minimality principle.

This choice is structurally parallel to the Bekenstein–Hawking entropy relation (S_BH ∝ R_s²), where the horizon area sets the system's information capacity. To the author's knowledge, this specific identification of Λ as a vacuum scale inherited from a parent R_s has not been proposed in prior literature.

---

## Tools

### BH–FRW Evolution Sandbox — [`/evolution-sandbox/`](evolution-sandbox/index.html)

Primary tool. Integrates FRW dynamics from an effective quantum bounce to late-time expansion and beyond.

- Geometric Λ determined solely by parent mass M — no free dark energy parameter
- LQC-inspired bounce: E² → E²(1 − E²/Ec²)
- Automatic Friedmann closure: Ω_k = 1 − Ω_m − Ω_r − Ω_Λ(M)
- Epoch markers: radiation–matter equality, matter–Λ equality, onset of acceleration z_acc
- Physical time axis in Gyr alongside dimensionless τ
- Log-scale display for all three diagnostic plots
- CSV export with full parameter header

### Fit Analysis & Driver Interface — [`/fit-analysis-tool/`](fit-analysis-tool/index.html)

Diagnostic interface for phenomenological exploration of dynamical dark energy within the BH-vacuum framework. Superimposes an accretion-coupling driver on the geometric baseline Λ = 1/Rs² and integrates the resulting w(z) trajectory for CPL comparison (w₀, wₐ, χ² vs ΛCDM).

The current default uses an exponential driver (V2 engine) which at moderate coupling strengths produces a dynamical equation of state overlapping with current DESI constraints (w₀ ≈ −0.84, wₐ < 0, phantom crossing at z ≈ 0.5, t₀ ≈ 13.3 Gyr). This is a structural observation, not a fit. The driver parametrization is external to the core geometric framework.

---

## Scope

**This framework does:**
- Explore a geometric inheritance hypothesis linking BH thermodynamics and FRW cosmology
- Test structural compatibility of Λ = 1/Rs² with observed late-time FRW dynamics
- Identify a narrow consistency window in parent mass as a structural FRW result
- Implement a phase-boundary bounce without a physical singularity

**Boundaries:**
- Prediction of specific cosmological observables is not the primary goal — the focus is on structural consistency
- Λ = 1/Rs² is not derived from a fundamental theory; it is treated as an explicit ansatz
- No microscopic bounce mechanism is provided (Ec² is a free numerical parameter of the integrator, not a physical constant)
- General Relativity is not modified; no new dynamical equations are introduced
- The accretion-driver parameters (η, τ, β, q) belong to the diagnostic interface only and are not part of the core framework

---

## Repository Structure

```
/
├── index.html                            # Repository hub — links to all tools
├── README.md                             # This file
├── .gitignore
│
├── /evolution-sandbox                    # Primary tool: geometric Λ, full FRW integration
│   ├── index.html                        # Browser-native sandbox (no build step required)
│   ├── README.md                         # Detailed documentation
│   └── /data                             # Reference trajectories (logM=22.5, quantum mode)
│       ├── bh_frw_full_logM22_5_Ec1e8_Q.csv
│       ├── bh_frw_full_logM22_5_Ec1e10_Q.csv
│       └── bh_frw_full_logM22_5_Ec1e12_Q.csv
│
├── /fit-analysis-tool                    # Diagnostic driver interface: phenomenological w(z) exploration
│   ├── index.html                        # V2 exponential engine (default)
│   ├── README.md                         # Detailed documentation
│   ├── /data
│   │   └── example_expdriver_w0-084.csv  # Reference trajectory: exp-driver, w₀≈−0.84
│   └── /archive
│       └── v1_linear.html               # V1 additive engine, deprecated
│
└── /docs
    └── Recursive Black Hole Cosmology v.1.pdf   # Main paper
```

---

## Citation

```bibtex
@misc{zlotnikov2026recursive,
  author = {Zlotnikov, Andrii},
  title  = {Recursive Black Hole Cosmology: An Interpretive Framework},
  year   = {2026},
  month  = feb,
  doi    = {10.5281/zenodo.18783687}
}
```

---

*All speculative elements are explicitly identified as interpretive and conditional.  
Feedback and criticism welcome.*
