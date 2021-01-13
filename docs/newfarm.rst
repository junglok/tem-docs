************************
GSDC TEM 신규 데이터 분석 팜
************************

1. EL7 신규 데이터 분석 팜 자원 현황
=============================

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

2. 신규 분석 팜 관리 소프트웨어
========================

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


3. 데이터 분석 도구
===============

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
|          |             |                                                                    | | (apps/relion/cpu/3.1.7)              |
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
|          | CryoSPARC   | | CryoSPARC is the state-of-the-art platform used globally for     | | v2.14.2                              |
|          |             | | obtaining 3D structural information from single particle cryo-EM |                                        |
|          |             | | data.                                                            |                                        |
|          |             |                                                                    |                                        |
|          |             | - https://cryosparc.com                                            |                                        |
|          +-------------+--------------------------------------------------------------------+----------------------------------------+
|          |             |                                                                    |                                        |
+----------+-------------+--------------------------------------------------------------------+----------------------------------------+


4. EL7 신규 분석 팜 접속
====================

리눅스/맥 사용자
------------

.. code-block:: bash

  $> ssh -Y -o Port=<port> <userID>@tem-ui-el7.sdfarm.kr

-Y (or -X) options : enable trusted X11 (or untrusted X11) forwarding


윈도우즈 사용자
-----------

기존에 사용하시던 MobaXTerm, Putty 등의 SSH 클라이언트 프로그램을 사용하는 것은 같습니다. 다만, 접속 로그인 노드는 tem-ui-el7.sdfarm.kr를 사용하셔야 합니다.


5. 데이터 분석 도구 모듈 경로 및 작업 제출 템플릿
======================================

데이터 분석 도구들의 Module 경로
--------------------------

.. code-block:: bash

  $> module avail
  -------- /tem/el7/Modules/apps --------
  apps/cistem/1.0.0      
  apps/relion/cpu/3.0.7  
  apps/relion/cpu/3.1.0  
  apps/relion/gpu/3.0.7  
  apps/relion/gpu/3.1.0  

  ---- /tem/el7/Modules/acceleration ----
  cuda/9.2  

  -------- /tem/el7/Modules/mpi ---------
  mpi/gcc/openmpi/4.0.3  

  ----- /tem/el7/Modules/virtualenv -----
  conda/2020.11  

  ------- /tem/el7/Modules/tools --------
  tools/ctffind/4.1.14    
  tools/gctf/1.18_b2      
  tools/motioncor2/1.3.1  
  tools/resmap/1.1.4      
  tools/summovie/1.0.2    
  tools/unblur/1.0.2      


데이터 분석 작업 PBS 작업 템플릿 경로
-----------------------------

.. code-block:: bash

  /tem/el7/qsub-cisTEM-cpu-noout.sh             ## output, error 로그 파일을 생성하지 않는 cisTEM 작업 템플릿
  /tem/el7/qsub-cisTEM-cpu.sh                   ## output, error 로그 파일을 생성하는 cisTEM 작업 템플릿
  /tem/el7/qsub-relion-3.0.7-cpu.bash           ## Relion 3.0.7 CPU MPI 작업 템플릿
  /tem/el7/qsub-relion-3.1.0-cpu.bash           ## Relion 3.1.0 CPU MPI 작업 템플릿
  /tem/el7/qsub-relion-3.0.7-cpu.bash           ## Relion 3.0.7 GPU 가속 활용하는 MPI 작업 템플릿
  /tem/el7/qsub-relion-3.1.0-gpu.bash           ## Relion 3.1.0 GPU 가속 활용하는 MPI 작업 템플릿


6. EL7 신규 분석 팜 배치 큐 (Batch Queues) 
======================================

+--------------+-----------------+-----------------------------------------------------------------------+------------------------------------+
| Category     | Queue Name      | Assigned Computing Resources                                          | Remarks                            |
+--------------+-----------------+-----------------------------------------------------------------------+------------------------------------+
| Shared       | **cpuQ**        | - tem-wn[1001-1002]-el7.sdfarm.kr (36 cores and 384GB memory per node)| - 380 Physical CPU cores           |
|              |                 | - tem-wn[1003-1013]-el7.sdfarm.kr (28 cores and 192GB memory per node)|                                    |
|              +-----------------+-----------------------------------------------------------------------+------------------------------------+
|              | **gpuQ**        | - tem-gpu[01-03]-el7.sdfarm.kr (28 cores, 2 P100 GPUs and 384GB mem.) | - 140 Physical CPU cores           | 
|              |                 | - tem-gpu04-el7.sdfarm.kr (28 cores, 2 P40 GPGPUs and 128GB memory)   | - 10 GPGPUs                        |
|              |                 | - tem-gpu05-el7.sdfarm.kr (28 cores, 2 P40 GPGPUs and 256GB memory)   | - P100 has 16GB device memory      |
|              |                 |                                                                       | - P40 has 24GB device memory       |
+--------------+-----------------+-----------------------------------------------------------------------+------------------------------------+