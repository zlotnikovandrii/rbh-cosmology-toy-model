Recursive Black Hole Cosmology — Research Interface V1

Accompanying interpretive framework:

Recursive Black Hole Cosmology: An Interpretive Framework
DOI: https://doi.org/10.5281/zenodo.18783687

Overview

This repository contains an exploratory phenomenological research interface accompanying the interpretive framework of Recursive Black Hole Cosmology.

It implements a background-level cosmological module that numerically explores a minimal mapping between parent black hole accretion history and an effective cosmological Λ-sector inside a horizon-separated region.

This is not a precision cosmology solver.
This is a structural research demonstrator.

What this model does

The interface computes:

Background FRW evolution

Effective Λ(t) constructed from a capacity-suppressed driver

H(z), Ω_Λ(z), w_Λ(z)

CPL phenomenological fits (w₀, wₐ)

Stability diagnostics

Controlled parameter sweeps

The core phenomenological structure is:

Λ = 1 + η · f(t) / Ṽ(t)^β

where:

f(t) encodes a simplified accretion driver

Ṽ(t) is a capacity-like volume proxy

η is a coupling strength

β controls suppression strength

The model is designed to test structural sensitivity, not to reproduce full observational cosmology.

What this model does NOT do

No perturbation analysis (no structure growth, no CMB, no power spectrum)

No dynamical mass evolution M(t)

No Lagrangian derivation of Λ

No precision fitting to DESI / Planck likelihoods

No MCMC or statistical inference

No new fundamental fields

The Λ sector is phenomenological and background-only.
This is intentional.

Purpose of V1

The goal of this version is to:

Test numerical stability of the inheritance–capacity mapping

Explore how different accretion regimes affect w(z)

Identify structural limits of minimal parameterization

Provide a transparent sandbox for controlled experimentation

V1 establishes internal consistency and parameter sensitivity.

It does not attempt to model the full complexity of cosmic history.

Structural limitation of V1

The current smooth single-phase driver form couples amplitude and late-time slope (w₀–wₐ linkage).

Increasing |wₐ| generically induces a deviation of w₀ from −1 within this minimal mapping.

Pivot-anchored or multi-phase accretion drivers are not implemented in V1.

This limitation reflects the baseline functional form, not a numerical instability.

Interpretation boundaries

This interface should be understood as:

A controlled toy environment

A background-level research calculator

A demonstrator of a conceptual bridge

It should not be interpreted as:

A predictive cosmological model

An observationally calibrated dark energy theory

A replacement for ΛCDM

Numerical notes

RK2 midpoint integrator (O(dt²))

Explicit detection of a = 1 crossing

UV regulator floor to prevent singular coupling

η = 0 → exact ΛCDM

q ≈ 0 → Λ = 1 exactly

Internal invariants are verified.

Relation to the main framework

This module complements the interpretive paper:

Recursive Black Hole Cosmology: An Interpretive Framework
DOI: https://doi.org/10.5281/zenodo.18783687

The paper remains interpretive and conceptual.
This repository provides a minimal computational scaffold suitable for controlled experimentation.

Future directions (not included in V1)

Astrophysically motivated accretion driver presets

Dynamic mass evolution M(t)

More flexible late-time anchoring

Alternative capacity mappings

Perturbation sector

License

Specify your preferred license here (MIT recommended for open exploratory research tools).
