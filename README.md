<!---![FastMAPO Logo](img/fastmapol1.png)--->
<img src="img/fastmapol1.png" alt="drawing" width="500"/>

# Agorithm Theoretical Basis Document (ATBD) for the Fast Multi-Angle Polarimetric Ocean and Land algorithm (FastMAPOL)

Authors: Meng Gao, Kirk Knobelspiesse, Pengwang Zhai, Kamal Aryal, Bryan Franz


## Introduction

## Algorithm Description
### Forward model
### Neural network model
### Inversion algorithm
### Input data screening and quality control


## Data products
PACE FastMAPOL polarimeter L2 products include four data groups:

- geolocation_data
- geophysical_data
- diagnostic_data
- sensor_band_parameters

The HARP2 FastMAPOL L2 product suite includes a list of aerosol optical properties for both fine and coarse modes:

- Aerosol optical depth (aot and aot_fine/coarse)
- Aerosol single scattering albedo (ssa and ssa_fine/coarse)
- Ångström coefficient (angstrom_440_870 and angstrom_440_670)
- Aerosol fine mode optical depth fraction (fmf)

As well as aerosol microphysical properties:

- Aerosol effective radius (reff_fine/coarse) and variance (veff_fine/coarse)
- Aerosol refractive index: real part (mr and mr_fine/coarse), imaginary part (mi and mi_fine/coarse)
- Aerosol spherical fraction (sph and sph_fine/coarse)
- Aerosol volume density (vd_fine/coarse)
- Aerosol fine mode volume fraction (fvf)
- Aerosol layer height (alh)

And a set of other products:

- Wind speed (wind_speed)
- Chlorophyll-a (chla)
- Remote sensing reflectance (Rrs*)

The remote sensing reflectance characterizes ocean-leaving reflectance. It is derived via atmospheric correction based on the retrieved aerosol properties at all HARP2 viewing angles. Therefore, it includes an angle dimension, as in the L1C data. There are two versions of remote sensing reflectance: Rrs1 (before BRDF correction) and Rrs2 (after BRDF correction). Due to the large size of Rrs1 and Rrs2, they are optional outputs in the standard L2 file. Instead, their angular means and standard deviations are typically included as Rrs1_mean/std and Rrs2_mean/std.

## Performance Analysis
### Retrieval uncertainties
### Retrieval speed
### Validations


## Reference

- 1. NN forward model and retrievals:   Gao, M., Franz, B. A., Knobelspiesse, K., Zhai, P.-W., Martins, V., Burton, S., Cairns, B., Ferrare, R., Gales, J., Hasekamp, O., Hu, Y., Ibrahim, A., McBride, B., Puthukkudy, A., Werdell, P. J., and Xu, X.: Efficient multi-angle polarimetric inversion of aerosols and ocean color powered by a deep neural network forward model, Atmos. Meas. Tech., 14, 4083–4110, https://doi.org/10.5194/amt-14-4083-2021, 2021.

- 2. Cloud mask and data screening:     Gao, M., K. Knobelspiesse, B. A. Franz, P.-W. Zhai, V. Martins, S. P. Burton, B. Cairns, R. Ferrare, M. A. Fenn, O. Hasekamp, Y. Hu, A. Ibrahim, A. M. Sayer, P. J. Werdell, and X. Xu. 2021. "Adaptive Data Screening for Multi-Angle Polarimetric Aerosol and Ocean Color Remote Sensing Accelerated by Deep Learning." Frontiers in Remote Sensing, 2: [10.3389/frsen.2021.757832]

- 3. Uncertainty quantification:        Gao, M., K. Knobelspiesse, B. Franz, P.-W. Zhai, A. Sayer, A. Ibrahim, B. Cairns, O. Hasekamp, Y. Hu, V. Martins, J. Werdell, and X. Xu. 2022. "Effective uncertainty quantification for multi-angle polarimetric aerosol remote sensing over ocean." Atmos. Meas. Tech., 15 (16): 4859–4879 [10.5194/amt-15-4859-2022]

- 4. Correlation and residual analysis: Gao, M., K. Knobelspiesse, B. A. Franz, P.-W. Zhai, B. Cairns, X. Xu, and J. V. Martins. 2022. "The impact and estimation of uncertainty correlation for multi-angle polarimetric remote sensing of aerosols and ocean color." Atmos. Meas. Tech., 16, 2067–2087, [10.5194/amt-16-2067-2023]
 
- 5. Global scale retrieval testing:    Gao, M., Franz, B. A., Zhai, P.-W., Knobelspiesse, K., Sayer, A., Xu, X., Martins, V., Cairns, B., Castellanos, P., Fu, G., Hannadige, N., Hasekamp, O., Hu, Y., Ibrahim, A., Patt, F., Puthukkudy, A., and Werdell, P. J.: Simultaneous retrieval of aerosol and ocean properties from PACE HARP2 with uncertainty assessment using cascading neural network radiative transfer models, Atmos. Meas. Tech., 16, 5863–5881, https://doi.org/10.5194/amt-16-5863-2023, 2023
