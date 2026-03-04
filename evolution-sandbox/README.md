# BH-FRW Full Evolution Sandbox

**Numerical integration of FRW dynamics under a geometric vacuum ansatz**

*Part of the [Recursive Black Hole Cosmology](https://doi.org/10.5281/zenodo.18783687) framework · Andrii Zlotnikov*

---

## What This Tool Does

Integrates the full cosmological evolution of an FRW universe in which the dark energy scale is set by the Schwarzschild radius of a parent black hole:

> $\Lambda_{\rm geom} = 1 / R_s^2$, where $R_s = 2GM / c^2$

The simulation runs from an effective phase boundary (bounce) through radiation and matter domination to late-time acceleration and beyond. Parent mass $M$ is the single inherited parameter; no free dark energy parameter is introduced.

The bounce at $\tau = 0$ represents a classical phase boundary — a regularization of the FRW breakdown — not a Big Bang singularity. The label $\tau = 0$ marks the moment after which standard FRW evolution is tracked forward.

---

## Core Equations

| Quantity | Expression |
|----------|------------|
| Schwarzschild radius | $R_s = 2GM / c^2$ |
| Geometric vacuum scale | $\Lambda_{\rm geom} = 1 / R_s^2$ |
| Dark energy density | $\rho_\Lambda = \Lambda_{\rm geom} c^2 / (8\pi G)$ |
| Friedmann equation | $H^2 = H_0^2 \left[\Omega_m a^{-3} + \Omega_r a^{-4} + \Omega_\Lambda + \Omega_k a^{-2}\right]$ |
| Closure condition | $\Omega_k = 1 - (\Omega_m + \Omega_r + \Omega_\Lambda)$ |
| LQC-style bounce | $E^2 \to E^2(1 - E^2/E_c^2)$ |

$\Omega_\Lambda$ and $\Omega_k$ are computed internally — never set manually.

---

## Computational Pipeline

1. **Input** — Parent mass $M$ via slider (log₁₀ scale)
2. **Geometry** — Compute $R_s$, set $\Lambda = 1/R_s^2$, derive $\Omega_\Lambda$
3. **Closure** — $\Omega_k$ computed automatically
4. **Integration** — Backward pass ($a = 1 \to$ bounce), then forward pass (bounce $\to a > 1$), with optional LQC correction
5. **Output** — Trajectories $a(\tau)$, $H(\tau)$, $E^2/E_c^2(\tau)$, physical time $t$ in Gyr

---

## What It Shows

- Two-pass integration with bounce detection and exact $a = 1$ crossing via interpolation
- Epoch markers computed from density equality conditions and acceleration criteria: radiation–matter equality, matter–$\Lambda$ equality, onset of acceleration ($z_{\rm acc}$)
- Physical time in Gyr alongside conformal time $\tau$ (with $\tau = 0$ at the bounce)
- Log-scale display for all three plots — recommended for resolving early-universe dynamics
- CSV export with full parameter metadata

---

## Structural Observation

Sweeping parent mass over $\log_{10}(M/M_\odot) = 15\ldots25$ shows that late-time expansion structurally compatible with a $\Lambda$CDM-like universe — in the sense of $\Omega_\Lambda \sim 0.7$ and $t_0 \sim 13$–$14$ Gyr — emerges only within a narrow mass range near $\log_{10}(M/M_\odot) \approx 22$–$23$.

This is a consequence of FRW dynamics under the scaling $\Lambda \propto 1/M^2$, not a result of observational fitting. Outside this window the geometric vacuum scale is either catastrophically large or negligibly small relative to matter density.

---

## Interface Controls

| Parameter | Role | Note |
|-----------|------|------|
| $\log_{10}(M/M_\odot)$ | Parent mass → sets $\Lambda$ | Range 15–25 |
| $\Omega_m$ | Matter density prior | Not derived |
| $\Omega_r$ | Radiation density prior | Keep $> 0$ |
| $H_0$ | Hubble normalization | Fixed, not self-consistent in this version |
| $\log_{10}(E_c^2)$ | Critical density for bounce | Free numerical parameter |
| Quantum mode | Enables LQC-style correction | Off = classical breakdown |
| Log scale | Per-plot logarithmic display | Recommended for all three |

---

## Known Limitations

- **$\Omega_m$ and $\Omega_r$ are external priors** — not derived within the framework
- **$E_c^2$ is a free parameter** — the bounce scale has no derived value; it affects $a_{\rm bounce}$ but not late-time dynamics
- **$H_0$ is not self-consistent** — age $t_0$ is integrated directly; $H_0$ is not iteratively solved to match a target
- **Forward integration stops at $a = 1.2$** — the forward pass is hardcoded to terminate at $a_{\rm stop} = 1.2$ (z ≈ −0.17); evolution beyond this point is not computed
- **CSV seam artifact** — the backward/forward join at $a = 1$ produces an apparent non-monotonic step in exported data; this is a recording artifact, not a physical discontinuity
- **$\Omega_r = 0$ runs** — without radiation the forward integrator may terminate early; use $\Omega_r > 0$ for physically realistic evolution
- **Homogeneous FRW only** — no perturbations, no structure formation

---

## Usage

Open `index.html` in any modern browser. No server, no dependencies, no build step.

Enable **Log scale** for all three plots when exploring the bounce region — linear scale compresses early-universe dynamics against the full 13–14 Gyr baseline. Use **Export CSV** to save the trajectory with parameters embedded in the header.

---

## Scope

**Tests:** structural consequences of $\Lambda = 1/R_s^2$ within standard FRW cosmology; internal consistency of the Friedmann sector under geometric scaling.

**Does not:** predict observables, fit data, derive the ansatz, model a microscopic bounce, include perturbations, or modify General Relativity.

For the motivation behind the $\Lambda = 1/R_s^2$ ansatz, see the [main README](../README.md#motivation-for-the--1rs-ansatz).

All interpretations remain conditional on the stated ansatz.
