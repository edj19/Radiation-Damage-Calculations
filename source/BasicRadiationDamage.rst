Basic Radiation Damage model
================================

Overview
---------
.. code-block:: python
   :emphasize-lines: 3,5

   def some_function():
       interesting = False
       print 'This line is highlighted.'
       print 'This one is not...'
       print '...but this one is.'


Columb scattering with target atom
-------------------------------------
A universal one-parameter differential scattering cross section equation in reduced notation
is expressed by Lindhard et al. as:

.. math::
    d\sigma_{sc} = \frac{\pi a^2_{TF}}{2}\frac{f(t^{1/2})}{t^{3/2}}dt

where t is a dimensionless collision parameter defined by:

.. math::
    t\equiv \epsilon^2\frac{T}{T_{max}}=\epsilon^2\sin^2(\frac{\theta_c}{2})

T is the transferred energy to the target,and $T_{max}$ is the maximum transferred energy as:

.. math::
    T_{max}=\frac{4M_1M_2}{(M_1+M_2)^2}E_p
