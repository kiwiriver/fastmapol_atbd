<!---![FastMAPO Logo](img/fastmapol1.png)--->
<img src="img/fastmapol1.png" alt="drawing" width="500"/>

# FastMAPOL ATBD: Agorithm Theoretical Basis Document for the Fast Multi-Angle Polarimetric Ocean and Land algorithm

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

### geophysical_data group: aerosol and surface products
Aerosol optical properties for both fine and coarse modes:

- Aerosol optical depth (aot and aot_fine/coarse)
- Aerosol single scattering albedo (ssa and ssa_fine/coarse)
- Ångström coefficient (angstrom_440_870 and angstrom_440_670)
- Aerosol fine mode optical depth fraction (fmf)

Aerosol microphysical properties:

- Aerosol effective radius (reff_fine/coarse) and variance (veff_fine/coarse)
- Aerosol refractive index: real part (mr and mr_fine/coarse), imaginary part (mi and mi_fine/coarse)
- Aerosol spherical fraction (sph and sph_fine/coarse)
- Aerosol volume density (vd_fine/coarse)
- Aerosol fine mode volume fraction (fvf)
- Aerosol layer height (alh)

Surface and ocean products:

- Wind speed (wind_speed)
- Chlorophyll-a (chla)
- Remote sensing reflectance (Rrs*)

The remote sensing reflectance characterizes ocean-leaving reflectance. It is derived via atmospheric correction based on the retrieved aerosol properties at all HARP2 viewing angles. Therefore, it includes an angle dimension, as in the L1C data. There are two versions of remote sensing reflectance: Rrs1 (before BRDF correction) and Rrs2 (after BRDF correction). Due to the large size of Rrs1 and Rrs2, they are optional outputs in the standard L2 file. Instead, their angular means and standard deviations are typically included as Rrs1_mean/std and Rrs2_mean/std.

### diagnostic_data: data quality evaluations
Since the retrieval algorithm is based on optimal estimation by minimizing a $\chi^2$ cost function defined as the difference between measurement (m) and forward model fitting (f), normalized by total uncertainties ($\sigma$).

$\chi^2 = \frac{1}{N} \sum (f - m)^2/\sigma^2$

Here N is the total number of measureents used in retreival. The algorithm also adaptively evalue fitting performance, if the fitting perform poor, it will be removed from the retreival process. Therefore, the $\chi^2$ and $N$ can be used to evaluate retrieval performance, the pixels with small $\chi^2$ (good fitting) and large $N$ (more pixels can be fitted) will better quality. A more quantitatively approach based on error propogation can be also used to compute retrieval uncertainty, which will be include in future product.

To support L3 data processing, a quality flag is also defined, which is usually based on $\chi^2$ and $N$. For the HARP2 test data, currently we choose
- quality_flag = 0: when $\chi^2<1.5$ and $N_{ref}>60$ and $N_{DoLP}>60$
- quality_flag = 1: when $\chi^2<1.5$ and $N_{ref}>40$ and $N_{DoLP}>40$
- quality_flag > 1: for higher value $\chi^2$ and lower values of $N_{ref}$ and $N_{DoLP}$
Quality flag will be updated with future L1 data calibration improvement.

## Performance Analysis
### Retrieval uncertainties
### Retrieval speed
### Validations


## Reference

- PACE radiative transfer simulator: Zhai, P.-W., Gao, M., Franz, B. A., Werdell, P. J., Ibrahim, A., Hu, Y., and Chowdhary, J.: A Radiative Transfer Simulator for PACE: Theory and Applications, Frontiers in Remote Sensing, 3, 840188, https://doi.org/10.3389/frsen.2022.840188, 2022
- 
- NN forward model and retrievals:   Gao, M., Franz, B. A., Knobelspiesse, K., Zhai, P.-W., Martins, V., Burton, S., Cairns, B., Ferrare, R., Gales, J., Hasekamp, O., Hu, Y., Ibrahim, A., McBride, B., Puthukkudy, A., Werdell, P. J., and Xu, X.: Efficient multi-angle polarimetric inversion of aerosols and ocean color powered by a deep neural network forward model, Atmos. Meas. Tech., 14, 4083–4110, https://doi.org/10.5194/amt-14-4083-2021, 2021.

- Cloud mask and data screening:     Gao, M., K. Knobelspiesse, B. A. Franz, P.-W. Zhai, V. Martins, S. P. Burton, B. Cairns, R. Ferrare, M. A. Fenn, O. Hasekamp, Y. Hu, A. Ibrahim, A. M. Sayer, P. J. Werdell, and X. Xu. 2021. "Adaptive Data Screening for Multi-Angle Polarimetric Aerosol and Ocean Color Remote Sensing Accelerated by Deep Learning." Frontiers in Remote Sensing, 2: [10.3389/frsen.2021.757832]

- Uncertainty quantification:        Gao, M., K. Knobelspiesse, B. Franz, P.-W. Zhai, A. Sayer, A. Ibrahim, B. Cairns, O. Hasekamp, Y. Hu, V. Martins, J. Werdell, and X. Xu. 2022. "Effective uncertainty quantification for multi-angle polarimetric aerosol remote sensing over ocean." Atmos. Meas. Tech., 15 (16): 4859–4879 [10.5194/amt-15-4859-2022]

- Correlation and residual analysis: Gao, M., K. Knobelspiesse, B. A. Franz, P.-W. Zhai, B. Cairns, X. Xu, and J. V. Martins. 2022. "The impact and estimation of uncertainty correlation for multi-angle polarimetric remote sensing of aerosols and ocean color." Atmos. Meas. Tech., 16, 2067–2087, [10.5194/amt-16-2067-2023]
 
- Global scale retrieval testing:    Gao, M., Franz, B. A., Zhai, P.-W., Knobelspiesse, K., Sayer, A., Xu, X., Martins, V., Cairns, B., Castellanos, P., Fu, G., Hannadige, N., Hasekamp, O., Hu, Y., Ibrahim, A., Patt, F., Puthukkudy, A., and Werdell, P. J.: Simultaneous retrieval of aerosol and ocean properties from PACE HARP2 with uncertainty assessment using cascading neural network radiative transfer models, Atmos. Meas. Tech., 16, 5863–5881, https://doi.org/10.5194/amt-16-5863-2023, 2023
 
- FastMAPOL/Component with coastal application:  Kamal Aryal, Peng-Wang Zhai, Meng Gao, Bryan A. Franz, Kirk Knobelspiesse, and Yongxiang Hu, Machine learning based aerosol and ocean color joint retrieval algorithm for multiangle polarimeters over coastal waters, Optics Express, 32,17,29921-29942 (2024), https://doi.org/10.1364/OE.522794


