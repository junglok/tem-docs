
***************************
TEM infrastructure overview
***************************
GSDC (Global Science experimental Data hub Center) supports data processing for Structural Biology with Cryo-EM, Lightsource, and X-ray Laser experiments.
Cryo-EM instrumentations are operated by KBSI. Cryo-EM facilities are directly connected to GSDC Datacenter through KREONet with 10Gbps dedicated/shared optical fiber links. GSDC provides Peta-bytes scale of storages and GPU equipped computational power. Here is an overview of GSDC's TEM infrastructre for Cryo-EM users.

* Overall architecture between KBSI's Cryo-EM facilities and GSDC's TEM service farm

.. image:: images/tem_service_farm.jpg
    :scale: 75 %
    :align: center

Computing and storage resources
===============================

* `Hardware specification of TEM service farm`_

Cluster management softwares
============================

+--------------+------------------------+------------------------------------------------------------+--------------------------------+
| Category     | Name                   | Description                                                | Version                        |
|              |                        |                                                            | (module path)                  |
+--------------+------------------------+------------------------------------------------------------+--------------------------------+
| OS           | Scientific Linux       | Operating system                                           | 7.9                            |
+--------------+------------------------+------------------------------------------------------------+--------------------------------+
| System       | Environment module     | - Module environment                                       | v4.4.1                         |
| M/W          |                        | - https://modules.readthedocs.io/en/latest                 |                                |
|              +------------------------+------------------------------------------------------------+--------------------------------+
|              | OpenPBS(torque)        | - Cluster resources management                             | v6.1.2                         |
|              |                        | - http://www.adaptivecomputing.com/products/torque         |                                |
|              +------------------------+------------------------------------------------------------+--------------------------------+
|              | OpenMPI                | - Messaging Pass Interface(MPI)                            | | v4.0.3                       |
|              |                        | - Reference implementation for MPI standard                | | (mpi/gcc/openmpi/4.0.3)      |
|              |                        | - https://www.open-mpi.org                                 |                                |
|              +------------------------+------------------------------------------------------------+--------------------------------+
|              | cuda                   | - Compute Unified Device Architecture(CUDA)                | | 9.2 (cuda/9.2)               |
|              |                        | - NVIDIA CUDA Runtime & Toolkit                            | | 11.2 (cuda/11.2)             |
|              |                        | - https://developer.nvidia.com/cuda-toolkit                |                                |
|              +------------------------+------------------------------------------------------------+--------------------------------+
|              | Anaconda               | - Python based virtual environemnt                         | 2020.11 (conda/2020.11)        |
|              |                        | - https://www.anaconda.com/                                |                                |
|              +------------------------+------------------------------------------------------------+--------------------------------+
|              | Python                 | - Python runtime                                           | v2.7.5                         |
+--------------+------------------------+------------------------------------------------------------+--------------------------------+


Data analysis tools
===================


+----------+-------------+--------------------------------------------------------------------+----------------------------------------+
| Category | Name        | Description                                                        | Version                                |
|          |             |                                                                    | (module path)                          |
+----------+-------------+--------------------------------------------------------------------+----------------------------------------+
| Tools    | **Relion**  | | A stand-alone computer program that employs an empirical Bayesian|                                        |
|          |             | | approach to refinement of (multiple) 3D reconstructions or 2D    |                                        |
|          |             | | class averages in electron cryo-microscopy (cryo-EM).            |                                        |
|          |             |                                                                    | | v3.0.7                               |
|          |             |                                                                    | | (apps/relion/cpu/3.0.7)              |
|          |             |                                                                    | | (apps/relion/gpu/3.0.7)              |
|          |             | - https://www3.mrc-lmb.cam.ac.uk/relion/index.php                  |                                        |
|          |             |                                                                    |                                        |
|          |             |                                                                    | | v3.1.0                               |
|          |             |                                                                    | | (apps/relion/cpu/3.1.0)              |
|          |             |                                                                    | | (apps/relion/gpu/3.1.0)              |
|          |             |                                                                    |                                        |
|          |             |                                                                    |                                        |
|          +-------------+--------------------------------------------------------------------+----------------------------------------+
|          | **cisTEM**  | | User-friendly software to process cryo-EM images of              | | v1.0.0                               |
|          |             | | macromolecular complexes and obtain high-resolution 3D           | | (apps/cistem/1.0.0)                  |
|          |             | | reconstructions.                                                 |                                        |
|          |             |                                                                    |                                        |
|          |             | - https://cistem.org                                               |                                        |
|          +-------------+--------------------------------------------------------------------+----------------------------------------+
|          |**CryoSPARC**| | CryoSPARC is the state-of-the-art platform used globally for     | | v3.0.1                               |
|          |             | | obtaining 3D structural information from single particle cryo-EM | | v3.2.0                               |
|          |             | | data.                                                            |                                        |
|          |             |                                                                    |                                        |
|          |             | - https://cryosparc.com                                            |                                        |
|          +-------------+--------------------------------------------------------------------+----------------------------------------+
|          | **Topaz**   | | A pipeline for particle detection in cryoem images using         | | v0.2.4                               |
|          |             | | convolutional neural networks trained from positive and unlabeled| | (topaz/cuda-9.2/0.2.4)               |
|          |             | | data.                                                            | | (topaz/cuda-11.0/0.2.4)              |
|          |             |                                                                    |                                        |
|          |             | - https://github.com/tbepler/topaz                                 |                                        |
|          +-------------+--------------------------------------------------------------------+----------------------------------------+
|          | **PyEM**    | | A collection of Python modules and command-line utilities for    | | v0.5                                 |
|          |             | | electron microscopy of biological samples.                       | | (pyem/0.5)                           |
|          |             | - https://github.com/asarnow/pyem                                  |                                        |
+----------+-------------+--------------------------------------------------------------------+----------------------------------------+