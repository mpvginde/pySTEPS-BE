Technical Information
======================

The RMI-PYSTEPS products are stored per nowcast run in a netCDF file following the `CF 1.7 conventions <https://cfconventions.org/Data/cf-conventions/cf-conventions-1.7/cf-conventions.html>`_. 
Each netCDF file contains 3 variables:

* lon[x,y]: a 700 x 700 matrix containing the longitude of each gridpoint [degrees East].
* lat[x,y]: a 700 x 700 matrix containing the latitude of each gridpoint [degrees North].
* precip_intesity[x,y,time,ens_number]: a 700 x 700 x 71 x 48 array containing the instantaneous precipitation rate [mm h-1].

and 4 dimension:

* ens_number: a vector of size 48 containing the ensemble member number
* time: a vector of size 71 containing the forecast time [seconds since start of the forecast]
* y: a vector of size 700 containing the y coordinate in the Cartesian coordinate system [m]
* x: a vector of size 700 containing the x coordinate in the Cartesian coordinate system [m]

The `PROJ <https://proj.org>`_ string for the coordinate reference system is::

  +proj=lcc +lat_1=49.83333333333334 +lat_2=51.16666666666666 +lat_0=50.797815 +lon_0=4.359215833333333 +x_0=649328 +y_0=665262 +ellps=GRS80 +towgs84=0,0,0,0,0,0,0 +units=m +no_defs

.. _domainexample:

.. figure:: figures/qpe_domain.eps
   :alt: The RMI-PYSTEPS output domain
   :align: center
   :width: 400px
   
   The RMI-PYSTEPS output domain.

