.. _pyem:

*********
UCSF PyEM
*********

UCSF pyem is a collection of Python modules and command-line utilities for electron microscopy of biological samples.

* Official **PyEM** site : https://github.com/asarnow/pyem


PyEM
====

Basically, pyem a collection of Python modules and command-line utilities for electron microscopy. Here, we have distributed PyEM into a seperate conda environment, 
where each pyem python utility (or program) is built with the dependencies of python runtime, numpy, scipy, matplotlib, seaborn, numba, pandas and natsort. 
You can find out each version of pyem modules environment with the following commands:

.. code-block:: bash

  $> module avail

  -------- /tem/el7/Modules/apps --------
  apps/cistem/1.0.0
  apps/relion/cpu/3.0.7
  apps/relion/cpu/3.1.0
  apps/relion/cpu/4.0.0
  apps/relion/gpu/3.0.7
  apps/relion/gpu/3.1.0
  apps/relion/gpu/4.0.0

  ---- /tem/el7/Modules/acceleration ----
  cuda/9.2  cuda/11.2

  -------- /tem/el7/Modules/mpi ---------
  mpi/gcc/4.8.5/openmpi/4.0.3
  mpi/gcc/8.3.1/mpich/3.4.3
  mpi/gcc/8.3.1/openmpi/4.0.3
  mpi/gcc/openmpi/4.0.3

  ----- /tem/el7/Modules/virtualenv -----
  conda/2020.11  topaz/cuda-9.2/0.2.4
  **pyem/0.5**   topaz/cuda-11.0/0.2.4

  ------- /tem/el7/Modules/tools --------
  tools/aspera-cli/3.9.6
  tools/ctffind/4.1.14
  tools/gctf/1.18_b2
  tools/motioncor2/1.3.1
  tools/resmap/1.1.4
  tools/summovie/1.0.2
  tools/unblur/1.0.2

  ----- /tem/el7/Modules/experiment -----
  PyRosetta/4
  python/3.7
  rosetta/mpich-3.4.3/3.13
  rosetta/openmpi-4.0.3/3.13



PyEM Executables
================

To use pyem utilities (or .py programs), you shoud load pyem module environment with the following command:

.. code-block:: bash

  $> module load pyem/0.5
  Loading pyem/0.5
  Loading requirement: conda/2020.11
  (pyem) $>

  (pyem) $> module list
  Currently Loaded Modulefiles:
    1) conda/2020.11   2) pyem/0.5
  (pyem) $> echo $PATH 
  echo $PATH
  /tem/el7/conda3-2020.11/envs/pyem/bin:/tem/el7/conda3-2020.11/bin:/tem/el7/conda3-2020.11/condabin:/usr/local/torquex/bin:/usr/local/torquex/sbin:/usr/local/torquex/bin:/usr/local/torquex/sbin:/tem/el7/Modules/bin:/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin

All the pyem programs (i.e., pyem python files) can be found in the absolute directory path of **/tem/el7/conda3-2020.11/envs/pyem/bin**. 
You can now run the pyem programs (all .py files in the above directory path) using their absolute paths or using just the name of program.

.. code-block:: bash

  (pyem) $>ls -al /tem/el7/conda3-2020.11/envs/pyem/bin/*.py
  lrwxrwxrwx. 1 tem tem 49 Mar 31  2021 /tem/el7/conda3-2020.11/envs/pyem/bin/angdist.py -> /tem/el7/conda3-2020.11/envs/pyem/pyem/angdist.py
  lrwxrwxrwx. 1 tem tem 46 Mar 31  2021 /tem/el7/conda3-2020.11/envs/pyem/bin/cfsc.py -> /tem/el7/conda3-2020.11/envs/pyem/pyem/cfsc.py
  lrwxrwxrwx. 1 tem tem 53 Mar 31  2021 /tem/el7/conda3-2020.11/envs/pyem/bin/csparc2star.py -> /tem/el7/conda3-2020.11/envs/pyem/pyem/csparc2star.py
  lrwxrwxrwx. 1 tem tem 50 Mar 31  2021 /tem/el7/conda3-2020.11/envs/pyem/bin/ctf2star.py -> /tem/el7/conda3-2020.11/envs/pyem/pyem/ctf2star.py
  lrwxrwxrwx. 1 tem tem 48 Mar 31  2021 /tem/el7/conda3-2020.11/envs/pyem/bin/emcalc.py -> /tem/el7/conda3-2020.11/envs/pyem/pyem/emcalc.py
  lrwxrwxrwx. 1 tem tem 45 Mar 31  2021 /tem/el7/conda3-2020.11/envs/pyem/bin/map.py -> /tem/el7/conda3-2020.11/envs/pyem/pyem/map.py
  lrwxrwxrwx. 1 tem tem 46 Mar 31  2021 /tem/el7/conda3-2020.11/envs/pyem/bin/mask.py -> /tem/el7/conda3-2020.11/envs/pyem/pyem/mask.py
  lrwxrwxrwx. 1 tem tem 50 Mar 31  2021 /tem/el7/conda3-2020.11/envs/pyem/bin/par2star.py -> /tem/el7/conda3-2020.11/envs/pyem/pyem/par2star.py
  lrwxrwxrwx. 1 tem tem 46 Mar 31  2021 /tem/el7/conda3-2020.11/envs/pyem/bin/pose.py -> /tem/el7/conda3-2020.11/envs/pyem/pyem/pose.py
  lrwxrwxrwx. 1 tem tem 64 Mar 31  2021 /tem/el7/conda3-2020.11/envs/pyem/bin/projection_subtraction.py -> /tem/el7/conda3-2020.11/envs/pyem/pyem/projection_subtraction.py
  lrwxrwxrwx. 1 tem tem 49 Mar 31  2021 /tem/el7/conda3-2020.11/envs/pyem/bin/project.py -> /tem/el7/conda3-2020.11/envs/pyem/pyem/project.py
  lrwxrwxrwx. 1 tem tem 50 Mar 31  2021 /tem/el7/conda3-2020.11/envs/pyem/bin/recenter.py -> /tem/el7/conda3-2020.11/envs/pyem/pyem/recenter.py
  lrwxrwxrwx. 1 tem tem 53 Mar 31  2021 /tem/el7/conda3-2020.11/envs/pyem/bin/reconstruct.py -> /tem/el7/conda3-2020.11/envs/pyem/pyem/reconstruct.py
  lrwxrwxrwx. 1 tem tem 47 Mar 31  2021 /tem/el7/conda3-2020.11/envs/pyem/bin/setup.py -> /tem/el7/conda3-2020.11/envs/pyem/pyem/setup.py
  lrwxrwxrwx. 1 tem tem 46 Mar 31  2021 /tem/el7/conda3-2020.11/envs/pyem/bin/sort.py -> /tem/el7/conda3-2020.11/envs/pyem/pyem/sort.py
  lrwxrwxrwx. 1 tem tem 47 Mar 31  2021 /tem/el7/conda3-2020.11/envs/pyem/bin/stack.py -> /tem/el7/conda3-2020.11/envs/pyem/pyem/stack.py
  lrwxrwxrwx. 1 tem tem 51 Mar 31  2021 /tem/el7/conda3-2020.11/envs/pyem/bin/star2bild.py -> /tem/el7/conda3-2020.11/envs/pyem/pyem/star2bild.py
  lrwxrwxrwx. 1 tem tem 46 Mar 31  2021 /tem/el7/conda3-2020.11/envs/pyem/bin/star.py -> /tem/el7/conda3-2020.11/envs/pyem/pyem/star.py
  lrwxrwxrwx. 1 tem tem 54 Mar 31  2021 /tem/el7/conda3-2020.11/envs/pyem/bin/subparticles.py -> /tem/el7/conda3-2020.11/envs/pyem/pyem/subparticles.py
  lrwxrwxrwx. 1 tem tem 48 Mar 31  2021 /tem/el7/conda3-2020.11/envs/pyem/bin/subset.py -> /tem/el7/conda3-2020.11/envs/pyem/pyem/subset.py
  lrwxrwxrwx. 1 tem tem 48 Mar 31  2021 /tem/el7/conda3-2020.11/envs/pyem/bin/varmap.py -> /tem/el7/conda3-2020.11/envs/pyem/pyem/varmap.py
  
  (pyem) $> which csparc2star.py
  /tem/el7/conda3-2020.11/envs/pyem/bin/csparc2star.py
