.. _topaz:

*****
Topaz
*****

A pipeline for particle detection in cryo-electron microscopy images using convolutional neural networks trained from positive and unlabeled examples. 
Topaz also includes methods for micrograph and tomogram denoising using deep denoising models.

* Official **Topaz** site : https://github.com/tbepler/topaz

Topaz Executables
=================

Basically, topaz uses NVIDIA GPUs with CUDA support for GPU acceleration in order to provide the features like automatic particle picking, denoising, etc. 
Here, we have installed Topaz into seperate conda environments, where each is built upon CUDA 9.x and CUDA 11.x. 
You can find out each version of topaz executables with the following commands:


.. code-block:: bash

  $> module avail

  ------------------------------------------- /tem/el7/Modules/apps -------------------------------------------
  apps/cistem/1.0.0      apps/relion/cpu/3.1.0  apps/relion/gpu/3.1.0
  apps/relion/cpu/3.0.7  apps/relion/gpu/3.0.7

  --------------------------------------- /tem/el7/Modules/acceleration ---------------------------------------
  cuda/9.2
  cuda/11.2

  ------------------------------------------- /tem/el7/Modules/mpi --------------------------------------------
  mpi/gcc/openmpi/4.0.3

  ---------------------------------------- /tem/el7/Modules/virtualenv ----------------------------------------
  conda/2020.11
  pyem/0.5  
  topaz/cuda-9.2/0.2.4
  topaz/cuda-11.0/0.2.4  

  ------------------------------------------ /tem/el7/Modules/tools -------------------------------------------
  tools/ctffind/4.1.14  tools/motioncor2/1.3.1  tools/summovie/1.0.2
  tools/gctf/1.18_b2    tools/resmap/1.1.4      tools/unblur/1.0.2


Topaz binary executable with CUDA 9.2
-------------------------------------

.. code-block:: bash

  $> module load topaz/cuda-9.2/0.2.4
  Loading topaz/cuda-9.2/0.2.4
    Loading requirement: conda/2020.11

  (topaz-v0.2.4-cuda9.2) $>

 
.. code-block:: bash

  (topaz-v0.2.4-cuda9.2) $> which topaz
  /tem/el7/conda3-2020.11/envs/topaz-v0.2.4-cuda9.2/bin/topaz


With above command, you can find that the path of topaz executable with CUDA 9.x support is **/tem/el7/conda3-2020.11/envs/topaz-v0.2.4-cuda9.2/bin/topaz**.

Topaz binary executable with CUDA 11.2
--------------------------------------

.. code-block:: bash

  $> module load topaz/cuda-11.0/0.2.4
  Loading topaz/cuda-11.0/0.2.4
    Loading requirement: conda/2020.11

  (topaz-v0.2.4-cuda11.0) $>

 
.. code-block:: bash

  (topaz-v0.2.4-cuda11.0) $> which topaz
  /tem/el7/conda3-2020.11/envs/topaz-v0.2.4-cuda11.0/bin/topaz


With above command, you can find that the path of topaz executable with CUDA 11.x support is **/tem/el7/conda3-2020.11/envs/topaz-v0.2.4-cuda11.0/bin/topaz**.


Using Topaz in CryoSPARC
========================



Using Topaz in Relion (v3.1+)
=============================