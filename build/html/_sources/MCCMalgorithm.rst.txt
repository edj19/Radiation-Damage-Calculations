MCCM algorithm
===============
The possible damage induced by radiation in solid materials has been a topic of great interest for the 
scientific community.The effects that may be induced by this way depend on the nature of the study material.
To obtain a good effectiveness inside the material volume,inclusive at high depth,it is well-known that 
the gamma radiation is the best candiate. One of researchs of our group is to research the influence
of materials properties under defects.Different defects have different impacts on the optical、electrical 
and magnetic material properties,However it is difficult to study the single defect's effect which can give
a more clear point of material properties interpretation.Because when the heavy-ions and neutron irradiated the 
materials,it is a complicated process with various defects and difficult to distinguish different defects effect 
on material properties.But the good news is that gamma-ray irradiation can separate the defects on the basis of 
material atom displacement threshold energy(:math:`E_d`) when our group reasearch the gamma-ray influence different
dioxides.

Basic Models and Methods 
-------------------------
.. image:: ../images/model1.jpg




MCCM algorithm
---------------

The number of atom displacements in the voxel volume :math:`N_{dpa}` from the MCCM algorithm is an extended sum over
the calculated discrete electron flux values at a given depth :math:`z` ,generalized for any k-atom in the materials:

.. math::
    N_{dpa}=\sum_k(n_k\sum_i N^e_{dpa,k}(E_i)\Phi(E_i,z)\Delta E_i)

where :math:`n_k` is the relative fraction of the k-atom in its crystalline sublattice and :math:`N^e_{dpa,k}` is 
obtained for each one of these atoms.The number of atoms displaced per electron was calculated following the expression proposed by Oen and Holmes:

.. math::
    N^c_{dpa}(E)=\int^E_{E_c}N_a\sigma_{dpa}(E')\frac{1}{(-dE'/dx)}dE'

where

.. math::
    E_c=\sqrt{(mc^2)^2+\frac{Mc^2T_d}{2}}-mc^2

is the cutoff kinetic energy of electrons in order to displace an atom from its crystalline site,:math:`N_a` is the
number of atoms in a unit of volume in the sample and (-dE/dx) is the electron stopping power,calculated following the
expression given by Bethe and Ashkin:

.. math::
    -\frac{dE}{dx}=2\pi N_a Z^2_m r^2_0 (\frac{mc^2}{\beta^2}){\ln(\frac{mc^2\beta^2\gamma^2 E}{2I^2})-\frac{1}{\gamma^2}[1+(2\gamma-1)\ln2+\frac18 (\gamma-1)^2]}

where :math:`Z^2_m` is the mass square atomic number of the sample material and :math:`I` is the mean excitation potential
of the atom.

The incident gamma radiation produces secondary electrons inside material. These electrons can remove
an atom from its lattice position through elastic scattering processes.The removed atom is known as a 
primary knock-in atom(PKA) and the corresponding cross section, :math:`\sigma_{PKA}`,is obtained starting from 
the McKinley-Feshbach approximation.If any of these recoil atoms has a kinetic energy above the displacement
threshold energy :math:`T_d`,the secondary atoms can be knocked on by the PKA and removed from the lattice.The
number of secondary displaced atoms can be caclulated by introducing the damage function  :math:`v(T)`. Then,the 
total number of displaced atoms per target atom can be obtained by writing the displacement per atom cross
section as follows:

.. math::
    \sigma_{dpa}(E)=\sigma_{PKA}(E)\nu(T)

with

.. math::
    \sigma_{PKA}(E)=\frac{\pi Z^2_a r^2_0}{\beta^4 \gamma^2}{(\frac{T_m}{T_d}-1)-\beta^2\ln(\frac{T_m}{T_d})+\pi\alpha\beta [2(\sqrt{\frac{T_m}{T_d}}-1)-\ln(\frac{T_m}{T_d})]}

For the damage function we use the Kinchin-Pease model 

.. math::
    \nu(T)=
    \begin{cases}
    0& T<T_d\\
    1&  T_d\leq T\leq 2T_d\\
    \frac{T}{2T_d}&  T>2T_d
    \end{cases}

where

==================      ==================================================================
Notation                   Meanings
==================      ==================================================================
:math:`Z_a`              atomic number of target atom
:math:`r_0`              electron classical radius
:math:`\alpha`           :math:`Z_a/137`
:math:`\beta`            ration of electron velocity to light velocity
:math:`\gamma`           :math:`1/(1-\beta^2)`
:math:`T_m`              :math:`2E(E+2mc^2)/Mc^2` (maximum kinetic energy of recoil atoms)
:math:`E`                electron kinetic energy
:math:`mc^2`             electron rest energy
:math:`M`                atomic mass
==================      ==================================================================

In order to evaluate the damage function,the average atom recoil kinetic energy :math:`T_{av}` was
used obtained by the expression

.. math::
    T_{av} = \frac{1}{\sigma_{PKA}}\frac{\pi Z^2_a r^2_0}{\beta^4 \gamma^2}T_m [\ln(\frac{T_m}{T_d})-\beta^2(1-\frac{T_d}{T_m})+\pi\alpha\beta (\sqrt{\frac{T_d}{T_M}}-1)^2]

MCNP
-----
MCNP is a general purpose Monte Carlo N-Particle code that can be used for neutron,photon,electron,or coupled neutron/photon/electron
transport,including the capbility to calculate eigenvalues for critical systems.For beginners,its tutorials are unfriendly
and obscure, and for this purpose,I rewrite a simple and intelligible tutorial for beginners which can reduce time and vigour for the 
research works.Okay,let's begin our tour.

.. image:: ../images/mcnp.jpg

Surface Cards
^^^^^^^^^^^^^^
Surface can be defined by **equations**, **points** ,or **macrobodies**.In this simple tutorial,I only introduce the **equations**
section which is most popurlar use in the simulation works.If your work involes other section,you can sql official documentation.
Okay,You can define your surfaces with the following form and relative explainations are in the table below.
::

    def surface_card():
    /*
        Form:  j  k  a  list
    */
    return 0;


.. image:: ../images/sheet.jpg

Cell Cards
^^^^^^^^^^^^
If you have read the surface cards section,it is cheerful to use these surfaces to define the cell or geometry for your model.
The geometry of MCNP treats an arbitrary three-dimensional configuration of user-fined materials in geometric cells
bounded by first- and second-degree surfaces. The calls are defined by the **intersections**, **unions**, and **complements**
of the regions bounded by the surfaces.Each surface divides all space into two regions,one with positive sense with respect to
the surface and the other with negative sense. Define :math:`S=f(x,y,z)=0` as the equation of a surface in the problem.For 
any set of points :math:`(x,y,z)`,if :math:`S=0` the points are on the surface. If :math:`S` is negative,the points are 
said to have a negative sense with respect to that surface and,conversely,a positive sense if :math:`S` is positive.

Data Cards
^^^^^^^^^^^^^



Some Examples
^^^^^^^^^^^^^^
Fmn examples:

F4:N 10
FM4   0.04789   999 102
M999  92238.13 1

The F4 neutron tally is the track length estimate of the average fluence in cell 10.Material 999 is 238U with an atomic fraction
of 100%
where 
C=0.04787 normalization factor(such as **atom/barn.cm**),which you can regard it as atom density and calculate with the following
formula:

.. math::
    N=\frac{n}{V}=\frac{\rho N_{A}}{M}

Conclusions
------------