# Atmospheric Polarization Modelling with FORS2/IPOL

## Project Overview

This project reproduces and investigates atmospheric polarization models presented in Pereira et al. (2025) using FORS2/IPOL observations from the Very Large Telescope (VLT). The goal is to understand the polarization patterns produced by scattered moonlight and evaluate how different scattering models reproduce the observed sky polarization and intensity.

The project focuses on three atmospheric scattering models:

* Anisotropic Rayleigh scattering
* Four-species Mie scattering
* Combined Rayleigh–Mie scattering

The models are compared to observations of blank sky fields and standard stars obtained with FORS2/IPOL.

---

## Scientific Motivation

Moonlight scattered in the Earth's atmosphere introduces polarized background light that can contaminate astronomical polarimetric observations. Understanding this atmospheric polarization is therefore important for accurate polarization measurements of astrophysical sources.

This repository reproduces the analysis of Pereira et al. (2025) and investigates the applicability of the resulting models for correcting astronomical polarimetric observations.

---

## Repository Structure

### `Model_8_MIE.ipynb`

Main analysis notebook.

This notebook contains the complete modelling workflow:

1. Loading and organizing FORS2 observations.
2. Extraction of observational metadata.
3. Computation of Moon geometry.
4. Standard-star normalization.
5. Construction of anisotropic Rayleigh models.
6. Construction of four-species Mie models.
7. Construction of combined Rayleigh–Mie models.
8. Comparison of model predictions with observations.

Main outputs:

* Polarization degree vs Moon separation angle.
* Intensity vs Moon separation angle.
* Rayleigh model fits.
* Mie model fits.
* Combined model comparisons.
* Filter-dependent model behaviour.

---

### `Model_8_MIE_patat.ipynb`

Application of the atmospheric polarization model to observational data.

This notebook investigates whether the atmospheric polarization models can be used to correct polarimetric measurements.

Main tasks:

* Calculate model Stokes parameters.
* Compute atmospheric polarization corrections.
* Apply corrections to standard-star observations.
* Compare corrected and uncorrected measurements.
* Evaluate model performance in the q–u plane.

Outputs include:

* q–u diagrams.
* Corrected Stokes parameters.
* Corrected polarization degree.
* Validation against ESO reference values.

---

### `Observation_scatter_plot.ipynb`

Observational geometry analysis.

This notebook visualizes the spatial relation between:

* Moon position.
* Observed sky fields.
* Moon separation angle.

Main outputs:

* Moon position plots.
* Field distribution plots.
* Moon-separation coverage.

These figures are primarily used to understand the geometry of the observational dataset.

---

### `binning_figur.ipynb`

Visualization of the spatial binning procedure.

This notebook documents the binning scheme used throughout the polarization analysis.

Main outputs:

* Detector images.
* Spatial binning overlays.
* Figures used in the methodology section of the report.

---

### `Beams_3.ipynb`

Early-stage data exploration and beam identification notebook.

This notebook was used during development to:

* Inspect FORS2 headers.
* Explore observational metadata.
* Identify ordinary and extraordinary beams.
* Group observations into sky fields.
* Classify observations according to observing conditions.

The notebook contains several exploratory analysis steps that contributed to the final processing pipeline implemented in later notebooks.

---

## Data Requirements

The notebooks require FORS2/IPOL FITS observations.

The paths must be updated locally before execution:

```python
directory = Path("...")
standard_directory = Path("...")
```

The repository does not include raw observational data.

---

## Main Processing Workflow

### 1. Data ingestion

FITS files are read and metadata extracted from headers.

Relevant quantities include:

* Observation date.
* Filter.
* Exposure time.
* Chip number.
* Target coordinates.
* Instrument configuration.

---

### 2. Observation grouping

Observations are grouped into sky fields using coordinate matching.

Fields are separated according to:

* Filter.
* Chip.
* Observing conditions.

---

### 3. Standard-star normalization

Observations of CT1–CT4 are used to normalize intensity measurements.

The normalization procedure follows the methodology described in González-Gaitán et al. (2020).

---

### 4. Moon geometry

For every observation:

* Moon position is calculated.
* Moon separation angle is computed.
* Altitude and azimuth coordinates are determined.

These quantities form the basis of the scattering models.

---

### 5. Atmospheric scattering models

#### Anisotropic Rayleigh model

Used primarily to reproduce the observed polarization degree.

The anisotropy parameter δ is fitted to the observations.

---

#### Four-species Mie model

Used primarily to reproduce the observed intensity distribution.

The model consists of multiple aerosol populations with different scattering properties.

---

#### Combined Rayleigh–Mie model

A weighted combination of the two scattering mechanisms:

[
M_{\mathrm{total}}
==================

(1-\omega_{\mathrm{mie}})
M_{\mathrm{Rayleigh}}
+
\omega_{\mathrm{mie}}
M_{\mathrm{Mie}}
]

where (\omega_{\mathrm{mie}}) controls the relative Mie contribution.

---

### 6. Model evaluation

Model predictions are compared with observations for:

* Polarization degree.
* Intensity.
* Filter dependence.

Comparisons are performed separately for:

* B filter.
* V filter.
* R filter.
* I filter.

---

## Required Python Packages

The notebooks were developed using:

```python
numpy
pandas
matplotlib
scipy
astropy
photutils
pathlib
```

Additional packages may be required depending on the local environment.

---

## References

Pereira et al. (2025)

González-Gaitán et al. (2020)

FORS2 Instrument Documentation
