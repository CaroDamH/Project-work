# README – Atmospheric Polarization Modelling and Analysis

## Overview

This project reproduces and investigates the atmospheric polarization models presented in Pereira et al. (2025) using FORS2/IPOL observations obtained with the VLT. The code is designed to:

1. Extract and organize observational metadata from FITS files.
2. Analyze observations of blank sky fields and standard stars.
3. Compute observational quantities such as Moon separation angle and polarization degree.
4. Reproduce anisotropic Rayleigh and four-species Mie scattering models.
5. Construct combined Rayleigh–Mie scattering models.
6. Compare model predictions with observations in polarization degree and intensity.

The repository consists primarily of four Jupyter notebooks:

* `Model_8_MIE.ipynb`
* `Model_8_MIE_patat.ipynb`
* `Observation_scatter_plot.ipynb`
* `binning_figur.ipynb`

---

# 1. Model_8_MIE.ipynb

## Purpose

This is the main notebook used throughout the project. It contains the complete workflow from reading observations to reproducing the scattering models and comparing them with the measured data.

## Main tasks

### Data ingestion

The notebook:

* Reads FORS2 FITS files.
* Extracts metadata from FITS headers.
* Organizes observations by:

  * filter
  * target field
  * observing time
  * Moon geometry
  * observational conditions

### Standard stars

Observations of:

* CT1
* CT2
* CT3
* CT4

are loaded and used for normalization of the measured intensity curves.

The notebook extracts:

* filter information
* observation date
* chip number
* exposure times

for each standard star observation.

### Observation geometry

For each observation:

* Moon position is computed.
* Field position is computed.
* Moon-field separation angle is calculated.
* Relevant observing geometry is stored for later modelling.

### Polarization analysis

The notebook calculates:

* Stokes parameters
* polarization degree
* position angle
* normalized quantities used in the comparison with Pereira et al. (2025)

### Rayleigh scattering model

The anisotropic Rayleigh model is implemented.

Model outputs include:

* polarization degree as a function of Moon separation
* normalized intensity curves

The anisotropy parameter:

[
\delta
]

is fitted to the observational data.

### Mie scattering model

The four-species Mie model is implemented using weighted aerosol populations.

The notebook computes:

* scattering intensity
* polarization degree
* wavelength dependence

for the FORS2 filters:

* B
* V
* R
* I

### Combined Rayleigh–Mie model

A combined model is constructed according to

[
M_{\rm total}
=============

(1-\omega_{\rm mie})M_{\rm Rayleigh}
+
\omega_{\rm mie}M_{\rm Mie}.
]

Several values of

[
\omega_{\rm mie}
]

are investigated, including:

* 10%
* 30%
* 50%
* 70%

The resulting model predictions are compared directly with the observations.

### Model comparison

The notebook produces figures showing:

* polarization degree versus Moon separation angle
* intensity versus Moon separation angle
* comparison of Rayleigh, Mie, and combined models
* filter-dependent behaviour

These figures form the basis for the discussion presented in the report.

---

# 2. Model_8_MIE_patat.ipynb

## Purpose

Extension of the main modelling notebook.

This notebook investigates the application of the atmospheric polarization model as a correction method for astronomical observations.

## Main tasks

### Moon polarization correction

The notebook calculates:

* expected atmospheric polarization
* model Stokes parameters
* correction terms

for each observation.

### Corrected quantities

The following quantities are produced:

* (Q_{\rm moon})
* (U_{\rm moon})
* corrected (Q)
* corrected (U)
* corrected polarization degree

### Standard-star validation

The correction is tested using standard stars.

Comparisons are made between:

* uncorrected measurements
* corrected measurements
* ESO reference values

in the q–u plane.

### Stability analysis

The notebook is used to evaluate whether the correction:

* depends on aperture radius
* depends on annulus size
* behaves consistently between filters

---

# 3. Observation_scatter_plot.ipynb

## Purpose

This notebook focuses on the observational geometry.

It is primarily used to visualize the spatial relationship between:

* observing fields
* Moon position
* sky coordinates

during the observing campaign.

## Main tasks

### Target identification

Observations are grouped by:

* field
* filter
* observing time

### Coordinate calculations

Using Astropy:

* Moon coordinates are calculated.
* Field coordinates are calculated.
* Altitude and azimuth values are obtained.

### Moon separation analysis

For every observation:

* angular separation from the Moon is computed
* Moon position is stored
* field position is stored

### Scatter plots

The notebook generates figures showing:

* Moon position
* field distribution
* separation angle coverage

These plots are used to understand how the observations sample the sky relative to the Moon.

---

# 4. binning_figur.ipynb

## Purpose

This notebook is used to visualize and document the spatial binning procedure applied to the FORS2 images.

## Main tasks

### Image inspection

The notebook:

* loads FITS images
* displays CCD data
* visualizes the detector layout

### Binning visualization

The notebook illustrates:

* bin boundaries
* spatial bin locations
* detector coverage

used in the polarization analysis.

### Figure generation

The figures produced are primarily intended for:

* method descriptions
* thesis illustrations
* documentation of the binning procedure

rather than scientific analysis.

---

# Required Python Packages

The notebooks rely on the following packages:

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

# Data Requirements

The notebooks expect:

1. FORS2/IPOL FITS observations.
2. Standard-star observations (CT1–CT4).
3. Directory paths updated to match the local file structure.

Before running the notebooks, the user must modify:

```python
directory = Path(...)
standard_directory = Path(...)
```

to point to the correct locations of the FITS files.

---

# Output Products

The notebooks generate:

* polarization-degree curves
* intensity curves
* Rayleigh model fits
* Mie model fits
* combined model predictions
* Moon-separation plots
* q–u diagrams
* detector binning figures

These outputs are used throughout the report to evaluate atmospheric scattering models and their impact on astronomical polarimetric observations.
