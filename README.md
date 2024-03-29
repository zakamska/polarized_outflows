# polarized_outflows

`polarized_outflows` is a Python notebook to calculate the Stokes parameters resulting from scattering from an axisymmetric outflow. The code was written by Nadia Zakamska. This notebook is written for Python 3, and it depends on a handful of standard mathematical and plotting packages, plus `mcint` written by Tristan Snowsill and available at https://pypi.org/project/mcint/ (a copy compatible with `polarized_outflows` is available here as well). If you use `polarized_outflows` in your research, please cite Alexandroff et al. 2018 https://ui.adsabs.harvard.edu/abs/2022arXiv221114945L/abstract and Zakamska and Alexandroff 2023 MNRAS https://ui.adsabs.harvard.edu/abs/2023MNRAS.525.2716Z/abstract. 

The notebook is fully self-contained. It starts with an illustration of how to set up `mcint` and then proceeds to the astrophysically relevant models. In Cell 3 of the notebook the user needs to make two choices. The first choice is physically insignificant and impacts only the speed and the quality of the calculations. `nmc_large` is the number of Monte Carlo trials for calculating multi-dimensional integrals. The error bars displayed on the final figures reflect this value. For quick exploration of the parameter space, one can use `nmc_large=10000`, then the calculations take only a few seconds (for electrons) or a minute per model (for dust). For better quality figures, one can use `nmc_large=100000`. These calculations take longer: for the case of electron scattering, where analytical functions are available for the phase function and the polarization phase function of scattering, each model takes about 1.5 minutes, but for the case of dust scattering, where the phase functions are interpolated from numerical tables, each model takes 10 minutes or more. 

The second choice is dust vs electron scattering. Setting `electrons=True` loads analytical functions for the phase function and polarization fraction of Thomson scattering. Setting `electrons=False` loads Small Magellanic Cloud phase functions and polarization fractions by Bruce Draine from https://www.astro.princeton.edu/~draine/dust/scat.html. The relevant tables are provided here for convenience, but users interested in using these models should look at the original complete distribution and cite Draine 2003 https://ui.adsabs.harvard.edu/abs/2003ApJ...598.1017D/abstract. The numerical tables provided can be replaced by the user with any other functions or tables that describe the phase function of scattering and the polarization phase function. As described in Zakamska and Alexandroff 2023, the polarization phase function is defined to be a signed value, in agreement with the definition used by Draine 2003 as seen in his Figure 5, and retaining this information is essential for getting the correct polarization position angles. 

These two choices set up the nomenclature for output files: files starting with `el_` are for electron scattering, files starting with `dust_` are for dust scattering, files with `low_` in them are the low-quality files computed with `nmc_large<100000` and files with `high_` in them are the high-quality files computed with `nmc_large>=100000`. 

The notebook then proceeds to compute the emitted line profile, the scattered line profile, the polarization fraction and the Stokes parameters for a number of geometries for the emitter, the scatterer and the observer. Continuum polarization is also recorded. The calculation involves multi-dimensional integrals over the solid angle spanned by the emitter and the scatterer as discussed by Zakamska and Alexandroff 2023. These are the integrals in the Cell 6 of the notebook. 

For each geometry, the code generates a data table with all the necessary data to be able to reproduce the figures, and a pdf figure. The current output file naming system is set to reflect the choices of geometry: the first two values are the min and max polar angle of the emitter, the second two values are the min and max polar angle of the scatterer and the last value is the polar angle of the observer. The user can modify the parameters of the emitter, scatterer or observer to try different geometries. The model is currently predominantly used for computing scattering by a wind which is either edge-on or toward the observer, but the model can be trivially modified to include the back-scattering cone (which can even be dust-extincted if desired). The Stokes parameters are additive, so all one would need to do is add all Stokes parameters from the forward cone and the back cone to compute the total profile. 

## Contact

Feel free to contact me: zakamska@jhu.edu
