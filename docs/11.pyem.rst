.. _pyem:

*********
UCSF PyEM
*********

UCSF pyem is a suite of Python programs for data analysis in electron microscopy of biological samples. 
Key features include symmetry expansion, multi-body refinement, partial signal subtraction, metadata queries, and interoperability with other cryo-EM image processing suites.

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
  apps/relion/cpu/4.0.0
  apps/relion/cpu/4.0.1
  apps/relion/cpu/5.0.0
  apps/relion/gpu/4.0.0
  apps/relion/gpu/4.0.1
  apps/relion/gpu/5.0.0

  ---- /tem/el7/Modules/acceleration ----
  cuda/9.2  cuda/11.2

  -------- /tem/el7/Modules/mpi ---------
  mpi/gcc/4.8.5/openmpi/4.0.3
  mpi/gcc/8.3.1/mpich/3.4.3
  mpi/gcc/8.3.1/openmpi/4.0.3
  mpi/gcc/openmpi/4.0.3

  ----- /tem/el7/Modules/virtualenv -----
  conda/2020.11  topaz/cuda-9.2/0.2.4
  pyem/0.5   topaz/cuda-11.0/0.2.4

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

.. code-block:: bash

  (pyem) $> module list
  Currently Loaded Modulefiles:
    1) conda/2020.11   2) pyem/0.5
  
.. code-block:: bash
  (pyem) $> echo $PATH 
  echo $PATH
  /tem/el7/conda3-2020.11/envs/pyem/bin:/tem/el7/conda3-2020.11/bin:/tem/el7/conda3-2020.11/condabin:
  /usr/local/torquex/bin:/usr/local/torquex/sbin:/usr/local/torquex/bin:/usr/local/torquex/sbin:/tem/el7/Modules/bin:
  /usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin


All the pyem programs (i.e., pyem python files) can be found in the absolute directory path of **/tem/el7/conda3-2020.11/envs/pyem/bin**. 
You can now run the pyem programs (all .py files in the above directory path) using their absolute paths or using just the name of program.

.. code-block:: bash

  (pyem) $>ls -al /tem/el7/conda3-2020.11/envs/pyem/bin/*.py
  lrwxrwxrwx. 1 tem tem 49 Mar 31  2021 angdist.py -> /tem/el7/conda3-2020.11/envs/pyem/pyem/angdist.py
  lrwxrwxrwx. 1 tem tem 46 Mar 31  2021 cfsc.py -> /tem/el7/conda3-2020.11/envs/pyem/pyem/cfsc.py
  lrwxrwxrwx. 1 tem tem 53 Mar 31  2021 csparc2star.py -> /tem/el7/conda3-2020.11/envs/pyem/pyem/csparc2star.py
  lrwxrwxrwx. 1 tem tem 50 Mar 31  2021 ctf2star.py -> /tem/el7/conda3-2020.11/envs/pyem/pyem/ctf2star.py
  lrwxrwxrwx. 1 tem tem 48 Mar 31  2021 emcalc.py -> /tem/el7/conda3-2020.11/envs/pyem/pyem/emcalc.py
  lrwxrwxrwx. 1 tem tem 45 Mar 31  2021 map.py -> /tem/el7/conda3-2020.11/envs/pyem/pyem/map.py
  lrwxrwxrwx. 1 tem tem 46 Mar 31  2021 mask.py -> /tem/el7/conda3-2020.11/envs/pyem/pyem/mask.py
  lrwxrwxrwx. 1 tem tem 50 Mar 31  2021 par2star.py -> /tem/el7/conda3-2020.11/envs/pyem/pyem/par2star.py
  lrwxrwxrwx. 1 tem tem 46 Mar 31  2021 pose.py -> /tem/el7/conda3-2020.11/envs/pyem/pyem/pose.py
  lrwxrwxrwx. 1 tem tem 64 Mar 31  2021 projection_subtraction.py -> /tem/el7/conda3-2020.11/envs/pyem/pyem/projection_subtraction.py
  lrwxrwxrwx. 1 tem tem 49 Mar 31  2021 project.py -> /tem/el7/conda3-2020.11/envs/pyem/pyem/project.py
  lrwxrwxrwx. 1 tem tem 50 Mar 31  2021 recenter.py -> /tem/el7/conda3-2020.11/envs/pyem/pyem/recenter.py
  lrwxrwxrwx. 1 tem tem 53 Mar 31  2021 reconstruct.py -> /tem/el7/conda3-2020.11/envs/pyem/pyem/reconstruct.py
  lrwxrwxrwx. 1 tem tem 47 Mar 31  2021 setup.py -> /tem/el7/conda3-2020.11/envs/pyem/pyem/setup.py
  lrwxrwxrwx. 1 tem tem 46 Mar 31  2021 sort.py -> /tem/el7/conda3-2020.11/envs/pyem/pyem/sort.py
  lrwxrwxrwx. 1 tem tem 47 Mar 31  2021 stack.py -> /tem/el7/conda3-2020.11/envs/pyem/pyem/stack.py
  lrwxrwxrwx. 1 tem tem 51 Mar 31  2021 star2bild.py -> /tem/el7/conda3-2020.11/envs/pyem/pyem/star2bild.py
  lrwxrwxrwx. 1 tem tem 46 Mar 31  2021 star.py -> /tem/el7/conda3-2020.11/envs/pyem/pyem/star.py
  lrwxrwxrwx. 1 tem tem 54 Mar 31  2021 subparticles.py -> /tem/el7/conda3-2020.11/envs/pyem/pyem/subparticles.py
  lrwxrwxrwx. 1 tem tem 48 Mar 31  2021 subset.py -> /tem/el7/conda3-2020.11/envs/pyem/pyem/subset.py
  lrwxrwxrwx. 1 tem tem 48 Mar 31  2021 varmap.py -> /tem/el7/conda3-2020.11/envs/pyem/pyem/varmap.py

.. code-block:: bash

  (pyem) $> which csparc2star.py
  /tem/el7/conda3-2020.11/envs/pyem/bin/csparc2star.py


.. code-block:: bash

  (pyem) $> csparc2star.py --help
  usage: csparc2star.py [-h] [--boxsize BOXSIZE] [--class CLS] [--minphic MINPHIC] [--stack-path STACK_PATH] [--micrograph-path MICROGRAPH_PATH] [--copy-micrograph-coordinates COPY_MICROGRAPH_COORDINATES] [--swapxy]
                        [--invertx] [--inverty] [--cached] [--transform TRANSFORM] [--relion2] [--loglevel LOGLEVEL]
                        [input [input ...]] output

  positional arguments:
    input                 Cryosparc metadata .csv (v0.6.5) or .cs (v2+) files
    output                Output .star file

  optional arguments:
    -h, --help            show this help message and exit
    --boxsize BOXSIZE     Cryosparc refinement box size (if different from particles)
    --class CLS           Keep this class in output, may be passed multiple times
    --minphic MINPHIC     Minimum posterior probability for class assignment
    --stack-path STACK_PATH
                          Path to single particle stack
    --micrograph-path MICROGRAPH_PATH
                          Replacement path for micrographs
    --copy-micrograph-coordinates COPY_MICROGRAPH_COORDINATES
                          Source for micrograph paths and particle coordinates (file or quoted glob)
    --swapxy              Swap X and Y axes when converting particle coordinates from normalized to absolute
    --invertx             Invert particle coordinate X axis
    --inverty             Invert particle coordinate Y axis
    --cached              Keep paths from the Cryosparc 2+ cache when merging coordinates
    --transform TRANSFORM
                          Apply rotation matrix or 3x4 rotation plus translation matrix to particles (Numpy format)
    --relion2, -r2        Relion 2 compatible outputs
    --loglevel LOGLEVEL, -l LOGLEVEL
                          Logging level and debug output
  (pyem) $>