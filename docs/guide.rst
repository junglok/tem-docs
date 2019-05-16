***********
Users guide
***********

Accessing TEM service farm
==========================

Understanding environment modules
=================================
The Environment Modules system is a tool to help users manage their Unix or Linux shell environment, by allowing groups of related environment-variable settings to be made or removed dynamically.

* **Listing available modules**

.. code-block:: bash

  $> module avail
  -------------- /tem/home/tem/Modules/Modules/default/modulefiles --------------------
  apps/gcc/4.4.7/anaconda/5.2           apps/gcc/4.4.7/relion/cuda92/3.0-beta
  apps/gcc/4.4.7/chimera/1.13           apps/gcc/4.4.7/relion/gpu/2.1
  apps/gcc/4.4.7/cistem/1.0.0           apps/gcc/4.4.7/relion/gpu/3.0-beta
  apps/gcc/4.4.7/eman/2.1               cuda/8.0
  apps/gcc/4.4.7/phenix/1.13-2998       cuda/9.2
  apps/gcc/4.4.7/relion/cpu/1.4         dot
  apps/gcc/4.4.7/relion/cpu/2.1         modules
  apps/gcc/4.4.7/relion/cpu/3.0-beta    mpi/gcc/openmpi/1.6.5
  apps/gcc/4.4.7/relion/cuda92/2.1


* **Show module details**
.. code-block:: bash

  $> module show apps/gcc/4.4.7/relion/cpu/3.0-beta
  -------------------------------------------------------------------
  /tem/home/tem/Modules/Modules/default/modulefiles/apps/gcc/4.4.7/relion/cpu/3.0-beta:

  module-whatis    Setups `relion-3.0-beta-cpu' environment variables
  module           load mpi/gcc/openmpi/1.6.5
  setenv           relion_version 3.0-beta-cpu
  prepend-path     PATH /tem/home/tem/relion3/cpu/bin
  prepend-path     LD_LIBRARY_PATH /tem/home/tem/relion3/cpu/lib
  setenv     RELION_QUEUE_NAME tem
  setenv     RELION_MPI_MAX 11
  setenv     RELION_THREAD_MAX 28
  setenv     RELION_QSUB_COMMAND qsub
  setenv     RELION_QSUB_TEMPLATE /tem/home/tem/relion3/cpu/bin/qsub.csh
  setenv     RELION_CTFFIND_EXECUTABLE /tem/home/tem/ctffind-4.1.8/bin/ctffind
  setenv     RELION_RESMAP_EXECUTABLE /tem/home/tem/relion-1.4/ResMap/ResMap-1.1.4-linux64
  setenv     RELION_MOTIONCORR_EXECUTABLE /tem/home/tem/MotionCor2/MotionCor2-01-30-2017
  setenv     RELION_UNBLUR_EXECUTABLE /tem/home/tem/unblur_1.0.2/bin/unblur_openmp_7_17_15.exe
  setenv     RELION_SUMMOVIE_EXECUTABLE /tem/home/tem/summovie_1.0.2/bin/sum_movie_openmp_7_17_15.exe
  conflict         apps/gcc/4.4.7/relion
  -------------------------------------------------------------------


Job manager (Torque)
====================
