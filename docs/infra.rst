
***************************
TEM infrastructure overview
***************************
GSDC (Global Science experimental Data hub Center) supports data processing for Structural Biology with Cryo-EM, Lightsource, and X-ray Laser experiments.
Cryo-EM instrumentations are operated by KBSI. Cryo-EM facilities are directly connected to GSDC Datacenter through KREONet with 10Gbps dedicated/shared optical fiber links. GSDC provides Peta-bytes scale of storages and GPU equipped computational power. Here is an overview of GSDC's TEM infrastructre for Cryo-EM users.

* Interconnection between KBSI's Cryo-EM facilities and GSDC's TEM service farm

.. image:: images/tem_service_farm.jpg

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
|              | tem-gpu[01-05].sdfarm.kr    | - CPU : Intel® Xeon® CPU E5-2690v4 @ 2.60GHz 14Core * 2 CPUs              | 140 cores       |
|              |                             | - RAM : DDR4 16GB * 24 (384GB)                                            |                 |
|              |                             | - SSD : 6G SATA SSD 800GB * 2EA (RAID-1)                                  |                 |
|              |                             | - GPU : NVIDIA P100 * 2ea (tem-gpu[01-03])                                |                 |
|              |                             | - GPU : NVIDIA  P40 * 2ea (tem-gpu[04-05])                                |                 |
+--------------+-----------------------------+---------------------------------------------------------------------------+-----------------+
| Computing    | tem-ce.sdfarm.kr            | - CPU : Intel(R) Xeon(R) CPU E5-2697v3 @ 2.60GHz 14Core * 2 CPUs          | 28 cores        |
| (master)     |                             | - RAM : DDR4 8GB * 24 (192GB)                                             |                 |
|              |                             | - HDD : 12G SAS HDD 1.2TB * 2EA (RAID-1)                                  |                 |
|              |                             |                                                                           |                 |
+--------------+-----------------------------+---------------------------------------------------------------------------+-----------------+
| Computing    | tem-wn[1001-1011].sdfarm.kr | - CPU : Intel(R) Xeon(R) CPU E5-2697v3 @ 2.60GHz 14Core * 2 CPUs          | 308 cores       |
| (workers)    |                             | - RAM : DDR4 8GB * 24 (192GB)                                             |                 |
|              |                             | - HDD : 12G SAS HDD 1.2TB * 2EA (RAID-1)                                  |                 |
+--------------+-----------------------------+---------------------------------------------------------------------------+-----------------+
| Storage      | Dell EMC Isilon NAS         | Network attached storage 700 TB                                                             |
+--------------+-----------------------------+---------------------------------------------------------------------------+-----------------+

+--------------+----------+-----------+-----------+
| row 1, col 1 | column 2 | column 3  | column 4  |
+--------------+----------+-----------+-----------+
| row 2        |                                  |
+--------------+----------+-----------+-----------+
| row 3        |          |           |           |
+--------------+----------+-----------+-----------+



Cluster management softwares
============================


Data analysis tools
===================


