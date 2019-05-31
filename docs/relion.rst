******
Relion
******

Executing Relion GUI tools
==========================

How to start Relion data analysis tool
--------------------------------------

1. You can find out relion applications' environment module path by listing all the module available on TEM service farm

.. code-block:: bash

  $> module avail

  ----------------------- /tem/home/tem/Modules/Modules/versions -----------------------
  3.2.10
  ----------------------- /tem/home/tem/Modules/Modules/default/modulefiles -----------
  apps/gcc/4.4.7/anaconda/5.2           apps/gcc/4.4.7/relion/cuda92/3.0-beta
  apps/gcc/4.4.7/chimera/1.13           apps/gcc/4.4.7/relion/gpu/2.1
  apps/gcc/4.4.7/cistem/1.0.0           apps/gcc/4.4.7/relion/gpu/3.0-beta
  apps/gcc/4.4.7/eman/2.1               cuda/8.0
  apps/gcc/4.4.7/phenix/1.13-2998       cuda/9.2
  apps/gcc/4.4.7/relion/cpu/1.4         dot
  apps/gcc/4.4.7/relion/cpu/2.1         modules
  apps/gcc/4.4.7/relion/cpu/3.0-beta    mpi/gcc/openmpi/1.6.5
  apps/gcc/4.4.7/relion/cuda92/2.1

2. Check the module details for the specific relion version (e.g., Relion v2.1 with GPGPU support)

.. code-block:: bash

  $> module show apps/gcc/4.4.7/relion/gpu/2.1
  -------------------------------------------------------------------
  /tem/home/tem/Modules/Modules/default/modulefiles/apps/gcc/4.4.7/relion/gpu/2.1:

  module-whatis    Setups `relion-2.1' environment variables
  module           load mpi/gcc/openmpi/1.6.5
  module           load cuda/8.0
  setenv           relion_version 2.1
  prepend-path     PATH /tem/home/tem/relion-2.1/bin
  prepend-path     LD_LIBRARY_PATH /tem/lib/glibc-2.14/lib:/tem/home/tem/relion-2.1/lib
  setenv           RELION_QUEUE_NAME tem
  setenv           RELION_MPI_MAX 11
  setenv           RELION_THREAD_MAX 28
  setenv           RELION_QSUB_COMMAND qsub
  setenv           RELION_QSUB_TEMPLATE /tem/home/tem/relion-2.1/bin/qsub.bash
  setenv           RELION_CTFFIND_EXECUTABLE /tem/home/tem/ctffind-4.1.8/bin/ctffind
  setenv           RELION_GCTF_EXECUTABLE /tem/home/tem/Gctf_v1.06/bin/Gctf-v1.06_sm_20_cu8.0_x86_64
  setenv           RELION_RESMAP_EXECUTABLE /tem/home/tem/relion-1.4/ResMap/ResMap-1.1.4-linux64
  setenv           RELION_MOTIONCORR_EXECUTABLE /tem/home/tem/MotionCor2/MotionCor2-01-30-2017
  setenv           RELION_UNBLUR_EXECUTABLE /tem/home/tem/unblur_1.0.2/bin/unblur_openmp_7_17_15.exe
  setenv           RELION_SUMMOVIE_EXECUTABLE /tem/home/tem/summovie_1.0.2/bin/sum_movie_openmp_7_17_15.exe
  conflict         apps/gcc/4.4.7/relion
  -------------------------------------------------------------------

3. Load the environment module for the version of relion application which you want to execute. As the module specified is loaded, all the modules with dependency are also loaded (you can check these modules with "module list" command)

.. code-block:: bash

  $> module load apps/gcc/4.4.7/relion/gpu/2.1
  $> module list
  Currently Loaded Modulefiles:
    1) mpi/gcc/openmpi/1.6.5           3) apps/gcc/4.4.7/relion/gpu/2.1
    2) cuda/8.0

4. Check the relion application binary path

.. code-block:: bash

  $> which relion
  /tem/home/tem/relion-2.1/bin/relion


5. Execute the relion application (we assume that X11 forwarding is enabled)

.. code-block:: bash

  $> relion


.. image:: images/relion-screenshot.png
    :scale: 70 %
    :align: center




Torque batch script for Relion
==============================

