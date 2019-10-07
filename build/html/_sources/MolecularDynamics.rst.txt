Molecular Dynamics
===================

Radiation Damage Simulations with Molecular Dynamics

Before introducing the simulation,many people may think why we need simulations,what can we do through simulations

Basic Concepts and Methods
---------------------------
Molecular dynamics simulations compute the motions of individual molecules in models of solids,liquids and gases and it is a 
technique that allows a numerical "thought experiment" to be carried out using a model that,to a limited extent,approximates a real
physical or chemical system.Such a "virtual laboratory" approach has the advantage that many such "experiments" can be easily
set up and carried out in succession by simply varying the control parameters.Morever,extreme conditions,such high temperature and obvious
downside is that the results are only as good as the numerical model.In addition,the results can be artificially biased if the 
molecular dynamics calculation is unable to sample an adequate number of microstates over the time it is allowed to run.


Lammps Tutortials
------------------
LAMMPS is a classical molecular dynamics(MD) code that models ensembles of particles in a liquid,solid,or gaseous state.It can 
model atomic,polymeric,biological,solid-state(metals,ceramics,oxides),granular,coarse-grained,or macroscopic systems using 
a variety of interatomic potentials(force fields) and boundary conditions.It can model 2d or 3d systems with only a few
particles up to millions or billions.

Install LAMMPS
^^^^^^^^^^^^^^^^^^^
In this section,I will show you the most direct method to compile and buid the parallel lammps in you Linux(Ubuntu) system.
Before install the lammps,you should install the **MPICH** and **FFTW** in your PC machine.

Prerequisites
""""""""""""""""

.. note::
   * **MPICH** should be installed firstly

   Before you install the mpich,you should execute the following command in order to meet some of the dependencies:

   .. code-block:: c

       sudo apt install gfortran
       sudo apt install gcc
       sudo apt install g++

   Then you can go to it's `source website <http://www.mpich.org/>`_ and download the package,like **mpich-3.3.1.tar.gz**,when 
   you unzip the package,read the **README** file,you can can implement the following commands:

   .. code-block:: c

       tar -zxvf mpich-3.3.1.tar.gz
       cd mpich-3.2
       ./configure --prefix=/home/day/computer/mpich3/( = you should remmember this path)
       make & make install

   Okay you have install the mpich in your system,next you should configure enviroment

   .. code-block:: c

      cd ~
      vim .bashrc
   
   In the **.bashrc** file,add the following statements

   .. code-block:: c

      export PATH=/home/day/computer/mpich3/bin:$PATH
      export MANPATH=//home/day/computer/mpich3/man:$MANPATH

   Exit the **.bashrc** file and execute the following command.Of course you can test your installation after execute the command with
   the help of **mpirun -np k ./examples/cpi** statement.

   .. code-block:: c

      source .bashrc



   * **FFTW** 
   Second Let's start the **FFTW** installation,you can download the source code from `the official website <http://fftw.org/>`_
   and execute the following commands

   .. code-block:: c

      tar -zxvf fftw
      cd fftw-3.3.8
      ./configure --prefix=/home/day/material/lammps/fftw3/ --enable-shared=yes ( = you should remmember this path)
      make -j n
      make install

   Okay It's done!

Obtaining and building the Lammps 
""""""""""""""""""""""""""""""""""""
Next download the `lammps source code <https://lammps.sandia.gov/>`_ and execute the following commands

.. code-block:: c

   tar -zxvf lammps
   cd lammps-22Aug18/src
   cd STUBS/
   make
   cd ../MAKE
   vim Makefile.mpi(modify details see below)
   cd ..
   make mpi

When you finish the commands,you can see a executable file **lmp_mpi** in the src/ folder,you can make a directory lammps sibling
directory and copy the **lmp_mpi** in this folder.Remmember to add the its path to **.bashrc** in order to you can call 
lammps command in any folders.

.. note::
   If you want install the optional packages that extend LAMMPS functionality which enable a specific set of features.You can
   use the following command to check relative packages:

   .. code-block:: c

      cd lammps-22Aug18/src
      make package-status
    
   And use the following commands to install and uninstall the packages.

   .. code-block:: c

      make yes-package
      make no-package




DL_POLY Tutorials
-----------------
DL_POLY is a package of subroutines,programs and data files,designed to facilitate molecular dynamics simulations of macromolecules,
polymers,ionic systems and solutions on a distributed memory parallel computer.

Install DL_POLY
^^^^^^^^^^^^^^^^
In this section,I will show you the simplest way to install the DL_POLY in you Linux(Ubuntu) system.What you should install
**gfortran** and **MPICH** in your computer before install the DL_POLY which are introduced in the Lammps Install section.
Consequently you only need to download the source code from `the official website <https://www.scd.stfc.ac.uk/Pages/DL_POLY.aspx>`_ 
and execute the following commands

.. code-block:: c

   unzip dl_poly_4.09.zip
   cd dl_poly_4.09
   cd source
   ln -s ../build/Makefile-MPI Makefile
   vim Makefile (**modify the Makefile**)
   make hpc

If you want a **JAVA-GUI** to visualize your simulation system and examine basic properties,you should execute 

.. code-block:: c

   cd ../java
   ./build

Okay you have install the DL_POLY in your PC and you can see a executable file **DLPOLY.Z** in the execute folder.Hope
you have installed successfully!

