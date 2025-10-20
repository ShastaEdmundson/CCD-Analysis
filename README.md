# Rotation Curve Analysis of NGC 5526

This project analyzes spectral data collected using the KAST optical spectrograph on the Shane 3-meter telescope at Lick Observatory to derive the rotation curve of the edge-on spiral galaxy NGC 5526.  
Through calibration, wavelength mapping, and Doppler shift measurements of the H-alpha line, I modeled the galaxy’s rotational velocity profile and compared my findings with the classic results of Rubin & Ford (1970) — foundational evidence for dark matter.

---

## Background

Between 1967 and 1969, Vera Rubin and Kent Ford studied the Andromeda Galaxy (M31), finding that stellar orbital velocities remained nearly constant even at large galactic radii. This is contrary to the predictions of Kepler’s laws.  
This “flat rotation curve” implied the presence of unseen mass (predicted to be dark matter) extending beyond the luminous regions of galaxies.

The goal of this analysis was to reproduce a similar study using modern CCD spectroscopic data to determine whether NGC 5526 exhibits a comparable velocity–radius relationship.

---

## Observation Summary

- **Date:** May 17–18, 2025  
- **Location:** Shane 3-m Telescope, Lick Observatory  
- **Instrument:** KAST Optical Spectrograph (Blue Side)  
- **Targets:**
  - Calibration Star: *BD +33 2642*  
  - Galaxy: *NGC 5526*  
- **Exposure Details:**
  - Galaxy: 2×1200s + 1×900s exposures  
  - Calibration Star: 3×60s exposures  
- **Calibration Frames:**
  - Bias (0s), Dome Flats (15s), Arclamps (He, Hg-Cd, Ne, 5s)

---

##  Data Reduction Workflow

All processing was performed in Python using `Astropy`, `NumPy`, and `Photutils`.  
The main steps included:

1. **Bias and Flat-Field Correction**  
   - Created master bias and master dome flats via median stacking.  
   - Subtracted master bias and normalized flat fields.

2. **Spectral Calibration**  
   - Used He/Hg-Cd/Ne lamp spectra to map pixel → wavelength.  
   - Derived a dispersion relation of **3.03 Å/pixel**.  

3. **Spectrum Extraction**  
   - Located galactic center (row ≈ 93) via Gaussian fitting.  
   - Extracted 1D spectrum by median-collapsing around the center.  
   - Identified the **H-alpha emission line** at **6594 ± 0.12 Å**.

4. **Velocity Determination**  
   - Calculated redshift: *z = 0.0047 ± 0.00002* (≈30% off from literature *z = 0.0067*).  
   - Fitted Gaussians across the slit to derive wavelength shifts.  
   - Converted pixel offsets → arcseconds → kpc.  
   - Applied Doppler formula to compute velocities per radius bin.

5. **Rotation Curve Construction**  
   - Plotted velocity vs. galactocentric distance.  
   - Fitted 3rd-degree polynomial to model rotational velocity profile.

---

##  Results

- **Blue-shifted velocity:** −105 ± 15 km/s  
- **Red-shifted velocity:** +139 ± 9 km/s  
- **Average rotational velocity:** 122 ± 9 km/s  

This value is consistent with typical spiral galaxy rotation speeds (100–250 km/s; Rubin 1980).  
However, signal-to-noise limitations, especially on the blue side, prevented reliable outer-disk measurements beyond ≈3 kpc.  

A complete rotation curve extending to large radii would likely flatten which is consistent with dark matter halo models.

---

##  Discussion & Limitations

- Weak H-alpha emission and use of the blue-side spectrograph limited S/N.  
- Outer disk data were insufficient to confirm flattening.  
- Despite noise, the detection of distinct red- and blue-shifted regions supports expected rotational motion.  

Further improvement could come from:
- Longer exposures or red-side spectroscopy.  
- Inclusion of multiple emission lines for velocity cross-checking.  
- Comparison with existing velocity maps from literature or SDSS data.

---

##  Tools & Libraries

- **Python**: Astropy, NumPy, Pandas, Matplotlib, Photutils, SciPy  
- **Data Visualization**: Matplotlib, Seaborn  
- **Modeling**: `scipy.optimize.curve_fit` for Gaussian fitting  

---

## Key Skills Demonstrated

- CCD data calibration and noise correction  
- Wavelength calibration and dispersion mapping  
- Redshift and velocity derivation via Doppler shift  
- Gaussian modeling and error propagation  
- Data visualization and scientific reporting in Python  

---

##  References

- Rubin, V. C., & Ford, W. K. Jr. (1970). *Rotation of the Andromeda Nebula from a Spectroscopic Survey of Emission Regions.* ApJ, 159, 379.  
- Rubin, V. C. et al. (1980). *Rotational Properties of 21 Sc Galaxies with a Large Range of Luminosities and Radii.* ApJ, 238, 471.  
- [KAST Arc Spectra Calibration](https://mthamilton.ucolick.org/techdocs/instruments/kast/kast_arcSpectra.html)

