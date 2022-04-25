The RMI-PYSTEPS probabilistic nowcast product
==============================================

.. _pysteps:

pySTEPS
-------

pySTEPS (PYthon Short-Term Ensemble Prediction System) is a community-driven initiative for developing and maintaining an easy to use, modular, free and open source Python framework for short-term ensemble prediction systems.

In the *RMI-configuration* pysteps uses three components: an extrapolated (and evolved) radar component, a noise component and an NWP component. 
These three components are decomposed into a cascade of different spatial scales.

For each level of the cascade the radar image is evolved using an AR(2)-model and extrapolated using a local *Lucas-Kanade* optical flow algorithm.
The three components (extrapolation, noise and NWP) are blended on each cascade level indiviually using skill-dependent weights before the final precipitation field is reconstructed. 
Also, there exists an option to perturb the motion field as determined by the optical flow algorithm but in the current configuration this option is inactive.

.. note::
   More detailed information can be found in:
   Pulkkinen, S., D. Nerini, A. Perez Hortal, C. Velasco-Forero, U. Germann, A. Seed, and L. Foresti, 2019: Pysteps: an open-source Python library for probabilistic precipitation nowcasting (v1.0). *Geosci. Model Dev.*, 12 (10), 4185–4219, doi:10.5194/gmd-12-4185-2019.

.. _radar:

Radar Analysis
---------------
The radar analyses used by RMI-PYSTEPS are composite post-processed 5 minute accumulated rainfall products.
This product is created at the RMI by combining (if available) images from 5 radars:
- Helchteren (Belgium)
- Jabbeke (Belgium)
- Wideumont (Belgium)
- Avenois (France)
- Neuheilenback (Germany)
and applying several post-processing algorithms (beam-blockage correction, non-meteorological echo mitigation, mean-field bias gauge merging, ...).
The result is a 1km-resolution 700x700 radar accumulated rainfall analysis, produced every 5 minutes.

.. _radar example:

.. figure:: /docs/source/figures/radar_example.png
   :alt: Radar analysis for 2021-01-27 04:30 UTC
   :align: center
   :width: 400px
   
   RMI radar analysis of 5 min. accumulated rainfall valid at 2021-01-27 04:30 UTC

.. _nwp:

RMI MINI-EPS
------------

The NWP component used for the pySTEPS nowcast is provided by RMI's operational NWP models ALARO and AROME.
Both models have a 1.3 km resolution and are run 4 times a day, providing a forecast up  leadtimes of 48 hours. 
Both ALARO and AROME use a non-hydrostatic dynamical core. The main difference between both model lies in their treatment of (deep) convection and microphysics. For the pySTEPS nowcast, the most recent and 2 previous rainfall forecasts of both the AROME and ALARO are used to create a lagged ensemble of 6 members. The NWP rainfall fields are regridded to the radar grid before they are used by pySTEPS.

.. _nwp example:

.. figure:: /docs/source/figures/figures/model_example.png
   :alt: Rainfall forecast for 2021-01-27 04:30 UTC
   :align: center
   :width: 400px
   
   ALARO (left) and AROME (right) forecast of 5 min. accumulated rainfall valid at 2021-01-27 04:30 UTC. Both forecast were started at 2021-01-27 00:00 UTC.

.. note::
Termonia, P., Fischer, C., Bazile, E., Bouyssel, F., Brožková, R., Bénard, P., Bochenek, B., Degrauwe, D., Derková, M., El Khatib, R., Hamdi, R., Mašek, J., Pottier, P., Pristov, N., Seity, Y., Smolíková, P., Španiel, O., Tudor, M., Wang, Y., Wittmann, C., and Joly, A.: The ALADIN System and its canonical model configurations AROME CY41T1 and ALARO CY40T1, *Geosci. Model Dev*., 11, 257–281, https://doi.org/10.5194/gmd-11-257-2018, 2018. 


The pySTEPS Product
--------------------
Currently, the pySTEPS nowcast is run every 2 hours (00:05, 02:05, 04:05, ...) for 71 timesteps of 5 minutes, resulting in a forecast range of 5h and 55 min. The nowcast has a domain identical to the radar analysis domain and exists of 48 members. Forecasted rainfall fields are provided every timestep (5 min). 
