******
Relion
******
RELION (for REgularised LIkelihood OptimisatioN, pronounce rely-on) is a stand-alone computer program that employs an empirical Bayesian approach to refinement of (multiple) 3D reconstructions or 2D class averages in electron cryo-microscopy (cryo-EM). (from Relion offcial site https://www3.mrc-lmb.cam.ac.uk/relion/index.php?title=Main_Page)


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
    :scale: 50 %
    :align: center



Torque batch script for Relion
==============================

RELION_QSUB_TEMPLATE variable
-----------------------------
Relion defines lots of environment variables that can be used to execute different types of subtasks in the analysis workflows. Among these, "RELION_QSUB_TEMPLATE" describes the location of a proper Torque batch job script to interact with Torque-based service farm (already included in the environment modules)

.. code-block:: bash

  (for relion 1.4) RELION_QSUB_TEMPLATE /tem/home/tem/relion-1.4/bin/qsub.bash
  (for relion 2.1) RELION_QSUB_TEMPLATE /tem/home/tem/relion-2.1/cpu/bin/qsub.bash
  (for relion 2.1 w/ GPU support) RELION_QSUB_TEMPLATE /tem/home/tem/relion-2.1/bin/qsub.bash
  (for relion 3.0-beta) RELION_QSUB_TEMPLATE /tem/home/tem/relion3/cpu/bin/qsub.bash
  (for relion 3.0-beta w/ GPU support) RELION_QSUB_TEMPLATE /tem/home/tem/relion3/gpu/bin/qsub.bash


Torque strings defined by Relion
--------------------------------

.. table:: torque_strings_of_relion

  +----------------------+------------------------+------------------------------------------------------------+
  | String               | Variable type          | Description                                                |
  +----------------------+------------------------+------------------------------------------------------------+
  | **XXXcommandXXX**    | string                 | relion command + arguments                                 |
  +----------------------+------------------------+------------------------------------------------------------+
  | **XXXqueueXXX**      | string                 | Name of the queue to submit job to                         |
  +----------------------+------------------------+------------------------------------------------------------+
  | **XXXmpinodesXXX**   | integer                | The number of MPI processes to use                         |
  +----------------------+------------------------+------------------------------------------------------------+
  | **XXXthreadsXXX**    | integer                | The number of threads to use on each MPI process           |
  +----------------------+------------------------+------------------------------------------------------------+
  | **XXXcoresXXX**      | integer                | The number of MPI processes times the number of threads    |
  +----------------------+------------------------+------------------------------------------------------------+
  | **XXXdedicatedXXX**  | integer                | The minimum number of cores on each node                   |
  |                      |                        | (use this to fill entire nodes)                            |
  +----------------------+------------------------+------------------------------------------------------------+
  | **XXXnodesXXX**      | integer                | The total number of nodes to be requested                  |
  +----------------------+------------------------+------------------------------------------------------------+
  | **XXXextra1XXX**     | string                 | Installation-specific                                      |
  +----------------------+------------------------+------------------------------------------------------------+
  | **XXXextra2XXX**     | string                 | Installation-specific                                      |
  +----------------------+------------------------+------------------------------------------------------------+


Job script template
-------------------


.. code-block:: bash

  #!/bin/bash

  ### Inherit all current environment variables
  #PBS -V

  ### Job name
  #PBS -N XXXnameXXX

  ### Queue name
  #PBS -q XXXqueueXXX

  ### Specify the number of nodes and thread (ppn) for your job.
  #PBS -l nodes=XXXmpinodesXXX:ppn=XXXthreadsXXX

  ###########################################################
  ### Print Environment Variables
  ###########################################################
  echo ------------------------------------------------------
  echo -n 'Job is running on node '; cat $PBS_NODEFILE
  echo ------------------------------------------------------
  echo PBS: qsub is running on $PBS_O_HOST
  echo PBS: originating queue is $PBS_O_QUEUE
  echo PBS: executing queue is $PBS_QUEUE
  echo PBS: working directory is $PBS_O_WORKDIR
  echo PBS: execution mode is $PBS_ENVIRONMENT
  echo PBS: job identifier is $PBS_JOBID
  echo PBS: job name is $PBS_JOBNAME
  echo PBS: node file is $PBS_NODEFILE
  echo PBS: current home directory is $PBS_O_HOME
  echo PBS: PATH = $PBS_O_PATH
  echo PBS: PBS_GPUFILE=$PBS_GPUFILE
  echo PBS: CUDA_VISIBLE_DEVICES=$CUDA_VISIBLE_DEVICES
  echo ------------------------------------------------------

  ###########################################################
  # Switch to the working directory;
  cd $PBS_O_WORKDIR
  ###########################################################

  ### Run:
  module load mpi/gcc/openmpi/1.6.5
  mpirun --prefix /tem/home/tem/openmpi-1.6.5 -machinefile $PBS_NODEFILE XXXcommandXXX

  echo "Done!"
