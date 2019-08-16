
***************************
TEM infrastructure overview
***************************
GSDC (Global Science experimental Data hub Center) supports data processing for Structural Biology with Cryo-EM, Lightsource, and X-ray Laser experiments.
Cryo-EM instrumentations are operated by KBSI. Cryo-EM facilities are directly connected to GSDC Datacenter through KREONet with 10Gbps dedicated/shared optical fiber links. GSDC provides Peta-bytes scale of storages and GPU equipped computational power. Here is an overview of GSDC's TEM infrastructre for Cryo-EM users.

* Overall architecture between KBSI's Cryo-EM facilities and GSDC's TEM service farm

.. image:: images/tem_service_farm.jpg
    :scale: 60 %
    :align: center

Computing and storage resources
===============================

* Hardware specification of TEM service farm

+--------------+-----------------------------+---------------------------------------------------------------------------+-----------------+
| Category     | Name                        | Specification                                                             | Resources size  |
+--------------+-----------------------------+---------------------------------------------------------------------------+-----------------+
| Login        | tem-ui.sdfarm.kr            | - CPU : Intel(R) Xeon(R) CPU E5-2697v3 @ 2.60GHz 14Core * 2 CPUs          | 28 cores        |
|              |                             | - RAM : DDR4 8GB * 24 (192GB)                                             |                 |
|              |                             | - HDD : 12G SAS HDD 1.2TB * 2EA (RAID-1)                                  |                 |
+--------------+-----------------------------+---------------------------------------------------------------------------+-----------------+
| Computing    | tem-ce.sdfarm.kr            | - CPU : Intel(R) Xeon(R) CPU E5-2697v3 @ 2.60GHz 14Core * 2 CPUs          | 28 cores        |
| (master)     |                             | - RAM : DDR4 8GB * 24 (192GB)                                             |                 |
|              |                             | - HDD : 12G SAS HDD 1.2TB * 2EA (RAID-1)                                  |                 |
+--------------+-----------------------------+---------------------------------------------------------------------------+-----------------+
| Computing    | tem-wn[1001-1011].sdfarm.kr | - CPU : Intel(R) Xeon(R) CPU E5-2697v3 @ 2.60GHz 14Core * 2 CPUs          | 308 cores       |
| (workers)    |                             | - RAM : DDR4 8GB * 24 (192GB)                                             |                 |
|              |                             | - HDD : 12G SAS HDD 1.2TB * 2EA (RAID-1)                                  |                 |
|              +-----------------------------+---------------------------------------------------------------------------+-----------------+
|              | tem-gpu[01-05].sdfarm.kr    | - CPU : Intel® Xeon® CPU E5-2690v4 @ 2.60GHz 14Core * 2 CPUs              | 140 cores       |
|              |                             | - RAM : DDR4 16GB * 24 (384GB)                                            |                 |
|              |                             | - SSD : 6G SATA SSD 800GB * 2EA (RAID-1)                                  |                 |
|              |                             | - GPU : NVIDIA P100 * 2ea (tem-gpu[01-03])                                |                 |
|              |                             | - GPU : NVIDIA  P40 * 2ea (tem-gpu[04-05])                                |                 |
+--------------+-----------------------------+---------------------------------------------------------------------------+-----------------+
| Storage      | Dell EMC Isilon NAS         | Network attached storage 700 TB                                                             |
+--------------+-----------------------------+---------------------------------------------------------------------------+-----------------+
| Total                                      | 504 CPU cores, 10 GPGPUs, 700TB Storage                                                     |
+--------------+-----------------------------+---------------------------------------------------------------------------+-----------------+

Cluster management softwares
============================

+--------------+------------------------+------------------------------------------------------------+--------------------------------+
| Category     | Name                   | Description                                                | Version                        |
|              |                        |                                                            | (module path)                  |
+--------------+------------------------+------------------------------------------------------------+--------------------------------+
| OS           | Scientific Linux       | Operating system                                           | 6.x                            |
+--------------+------------------------+------------------------------------------------------------+--------------------------------+
| System       | Environment module     | - Module environment                                       | v3.2.10                        |
| middleware   |                        | - https://modules.readthedocs.io/en/latest                 |                                |
|              +------------------------+------------------------------------------------------------+--------------------------------+
|              | OpenPBS(torque)        | - Cluster resources management                             | v6.1.2                         |
|              |                        | - http://www.adaptivecomputing.com/products/torque         |                                |
|              +------------------------+------------------------------------------------------------+--------------------------------+
|              | OpenMPI                | - Messaging Pass Interface(MPI)                            | | v1.8.8                       |
|              |                        | - Reference implementation for MPI standard                | | (mpi/gcc/openmpi/1.8.8)      |
|              |                        | - https://www.open-mpi.org                                 |                                |
|              +------------------------+------------------------------------------------------------+--------------------------------+
|              | cuda                   | - Compute Unified Device Architecture(CUDA)                | 9.1 (cuda/9.1)                 |
|              |                        | - NVIDIA CUDA Runtime & Toolkit                            |                                |
|              |                        | - https://developer.nvidia.com/cuda-toolkit                |                                |
|              +------------------------+------------------------------------------------------------+--------------------------------+
|              | python                 | - Python runtime                                           | v2.6.6                         |
+--------------+------------------------+------------------------------------------------------------+--------------------------------+


Data analysis tools
===================

.. table:: data_analysis_tools

  +--------------+---------------------+--------------------------------------------------------------------+----------------------------------------+
  | Category     | Name                | Description                                                        | Version                                |
  |              |                     |                                                                    | (module path)                          |
  +--------------+---------------------+--------------------------------------------------------------------+----------------------------------------+
  | Data         | **Relion**          | | A stand-alone computer program that employs an empirical Bayesian|                                        |
  | Analysis     |                     | | approach to refinement of (multiple) 3D reconstructions or 2D    |                                        |
  | Tools        |                     | | class averages in electron cryo-microscopy (cryo-EM).            |                                        |
  |              |                     |                                                                    | | v3.0.7                               |
  |              |                     |                                                                    | | (apps/gcc/4.4.7/relion/cpu/3.0.7)    |
  |              |                     |                                                                    | | (apps/gcc/4.4.7/relion/gpu/3.0.7)    |
  |              |                     | - https://www3.mrc-lmb.cam.ac.uk/relion/index.php                  |                                        |
  |              |                     |                                                                    |                                        |
  |              |                     |                                                                    |                                        |
  |              |                     |                                                                    |                                        |
  |              |                     |                                                                    |                                        |
  |              |                     |                                                                    |                                        |
  |              |                     |                                                                    |                                        |
  |              +---------------------+--------------------------------------------------------------------+----------------------------------------+
  |              | **cisTEM**          | | User-friendly software to process cryo-EM images of              | | v1.0.0                               |
  |              |                     | | macromolecular complexes and obtain high-resolution 3D           | | (apps/gcc/4.4.7/cistem/1.0.0)        |
  |              |                     | | reconstructions.                                                 |                                        |
  |              |                     |                                                                    |                                        |
  |              |                     | - https://cistem.org                                               |                                        |
  |              +---------------------+--------------------------------------------------------------------+----------------------------------------+
  |              | **CryoSPARC**       | | CryoSPARC is the state-of-the-art platform used globally for     | | Not deployed yet (TBD)               |
  |              |                     | | obtaining 3D structural information from single particle cryo-EM |                                        |
  |              |                     | | data.                                                            |                                        |
  |              |                     |                                                                    |                                        |
  |              |                     | - https://cryosparc.com                                            |                                        |
  |              +---------------------+--------------------------------------------------------------------+----------------------------------------+
  |              |                     |                                                                    |                                        |
  +--------------+---------------------+--------------------------------------------------------------------+----------------------------------------+

