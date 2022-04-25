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

.. _nwp:
RMI MINI-EPS
------------



To use Lumache, first install it using pip:

.. code-block:: console

   (.venv) $ pip install lumache

Creating recipes
----------------

To retrieve a list of random ingredients,
you can use the ``lumache.get_random_ingredients()`` function:

.. autofunction:: lumache.get_random_ingredients

The ``kind`` parameter should be either ``"meat"``, ``"fish"``,
or ``"veggies"``. Otherwise, :py:func:`lumache.get_random_ingredients`
will raise an exception.

.. autoexception:: lumache.InvalidKindError

For example:

>>> import lumache
>>> lumache.get_random_ingredients()
['shells', 'gorgonzola', 'parsley']

