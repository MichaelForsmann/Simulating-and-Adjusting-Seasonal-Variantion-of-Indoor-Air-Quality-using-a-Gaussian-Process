## What this repository contains

- Simulation and adjustment of seasonal variance in indoor air quality 
  measurements using a Gaussian process with a periodic kernel
- Rescaling of short sampling windows (10 days for PM₂.₅ and black carbon, 
  10 weeks for VOCs, NO₂ and NOₓ) into half-year cumulative exposure 
  estimates via Eq. (1) of the main manuscript
- Comparison of seasonal-correction function families: periodic Gaussian 
  process, harmonic regression with 2 and 3 terms, and four-season step 
  correction (Supplementary Fig. S3)
- Multiplicative pump-flow drift correction for PM₂.₅ and black carbon 
  using a GP with radial basis function kernel (Supplementary Eq. S2)
- Train/test evaluation with household-level splitting to ensure 
  outcome-blind correction selection

## Method

Each observed concentration is rescaled by the ratio of the mean seasonal 
trend over the preceding half-year to the trend at the sampling week:

    Cᵢ,ₐ = (Cᵢ / G_T(wᵢ)) · (1/Δ) · ∫ G_T(t) dt

where G_T is the periodic GP trend, wᵢ is the sampling week, and Δ = 365/(7·2) 
weeks. The integral is evaluated by Simpson's 1/3 rule on 499 points. The 
correction improved household-level variance explained for strongly seasonal 
pollutants (e.g. NOₓ, R² from 0.03 to 0.22) and reduced to approximately 
unity for pollutants with little seasonal structure.

## Key dependencies

| Package       | Version | License           |
|---------------|---------|-------------------|
| Pyro          | —       | Apache 2.0        |
| NumPyro       | 0.21.0  | Apache 2.0        |
| SciPy         | 1.17.1  | BSD 3-Clause      |
| Matplotlib    | 3.10.9  | PSF / BSD-compat. |
| NumPy         | —       | BSD 3-Clause      |

## License

MIT License
[![DOI](https://zenodo.org/badge/924144145.svg)](https://doi.org/10.5281/zenodo.22828001)
