
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

* Hardware specification of TEM service farm

+--------------+---------------------------------+---------------------------------------------------------------------------+-----------------+
| Category     | Name                            | Specification                                                             | Resources size  |
+--------------+---------------------------------+---------------------------------------------------------------------------+-----------------+
| Login        | **tem-ui-el7.sdfarm.kr**        | - CPU : Intel(R) Xeon(R) Gold 6150 CPU @ 2.70GHz 18Core * 2 CPUs          | 72 cores (H/T)  |
|              |                                 | - RAM : DDR-4 2,666MHz 16GB * 24EA (384GB)                                |                 |
|              |                                 | - HDD : 12G SAS HDD 1.2TB * 2EA (RAID-1)                                  |                 |
+--------------+---------------------------------+---------------------------------------------------------------------------+-----------------+
| Web-Login    | **tem-cs-el7.sdfarm.kr**        | - CPU : Intel(R) Xeon(R) CPU E5-2697v3 @ 2.60GHz 14Core * 2 CPUs          | 56 cores (H/T)  |
| (CryoSPARC)  |                                 | - RAM : DDR4 8GB * 24 (192GB)                                             |                 |
|              |                                 | - HDD : 12G SAS HDD 1.2TB * 2EA (RAID-1)                                  |                 |
+--------------+---------------------------------+---------------------------------------------------------------------------+-----------------+
| Computing    | tem-ce-el7.sdfarm.kr            | - CPU : Intel(R) Xeon(R) CPU E5-2697v3 @ 2.60GHz 14Core * 2 CPUs          | 56 cores (H/T)  |
| (master)     |                                 | - RAM : DDR4 8GB * 24 (192GB)                                             |                 |
|              |                                 | - HDD : 12G SAS HDD 1.2TB * 2EA (RAID-1)                                  |                 |
+--------------+---------------------------------+---------------------------------------------------------------------------+-----------------+
| Computing    | tem-wn[1001-1002]-el7.sdfarm.kr | - CPU : Intel(R) Xeon(R) Gold 6150 CPU @ 2.70GHz 18Core * 2 CPUs          | 380 cores       |
| (workers)    |                                 | - RAM : DDR-4 2,666MHz 16GB * 24EA (384GB)                                |                 |
|              |                                 | - HDD : 12G SAS HDD 1.2TB * 2EA (RAID-1)                                  |                 |
|              +---------------------------------+---------------------------------------------------------------------------+                 |
|              | tem-wn[1003-1013]-el7.sdfarm.kr | - CPU : Intel(R) Xeon(R) CPU E5-2697v3 @ 2.60GHz 14Core * 2 CPUs          |                 |
|              |                                 | - RAM : DDR4 8GB * 24 (192GB)                                             |                 |
|              |                                 | - HDD : 12G SAS HDD 1.2TB * 2EA (RAID-1)                                  |                 |
|              +---------------------------------+---------------------------------------------------------------------------+-----------------+
|              | tem-gpu[01-05]-el7.sdfarm.kr    | - CPU : Intel® Xeon® CPU E5-2690v4 @ 2.60GHz 14Core * 2 CPUs              | - 140 cores     |
|              |                                 | - RAM : DDR4 16GB * 24 (384GB)                                            | - 10 GPGPUs     |
|              |                                 | - SSD : 6G SATA SSD 800GB * 2EA (RAID-1)                                  |                 |
|              |                                 | - GPU : NVIDIA P100 * 2ea (each tem-gpu[01-03]-el has 2 P100 GPU devices) |                 |
|              |                                 | - GPU : NVIDIA  P40 * 2ea (each tem-gpu[04-05]-el has 2 P40 GPU devices)) |                 |
+--------------+---------------------------------+---------------------------------------------------------------------------+-----------------+
| Storage      | Dell EMC Isilon NAS             | Network attached storage 800 TB                                                             |
+--------------+---------------------------------+---------------------------------------------------------------------------+-----------------+
| Total                                          | 612 CPU cores (physical), 10 GPGPUs, 800TB Storage                                          |
+--------------+---------------------------------+---------------------------------------------------------------------------+-----------------+

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
|              | cuda                   | - Compute Unified Device Architecture(CUDA)                | 9.2 (cuda/9.2)                 |
|              |                        | - NVIDIA CUDA Runtime & Toolkit                            |                                |
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
|          | CryoSPARC   | | CryoSPARC is the state-of-the-art platform used globally for     | | v3.0.1                               |
|          |             | | obtaining 3D structural information from single particle cryo-EM |                                        |
|          |             | | data.                                                            |                                        |
|          |             |                                                                    |                                        |
|          |             | - https://cryosparc.com                                            |                                        |
|          +-------------+--------------------------------------------------------------------+----------------------------------------+
|          |             |                                                                    |                                        |
+----------+-------------+--------------------------------------------------------------------+----------------------------------------+

