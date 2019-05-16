***********
Users guide
***********

Accessing TEM service farm
==========================

Understanding environment modules
=================================
The Environment Modules system is a tool to help users manage their Unix or Linux shell environment, by allowing groups of related environment-variable settings to be made or removed dynamically.

* **Listing available modules**

``
$> module avail
-------------- /tem/home/tem/Modules/Modules/default/modulefiles --------------------
apps/gcc/4.4.7/anaconda/5.2           apps/gcc/4.4.7/relion/cuda92/3.0-beta
apps/gcc/4.4.7/chimera/1.13           apps/gcc/4.4.7/relion/gpu/2.1
apps/gcc/4.4.7/cistem/1.0.0           apps/gcc/4.4.7/relion/gpu/3.0-beta
apps/gcc/4.4.7/eman/2.1               cuda/8.0
apps/gcc/4.4.7/phenix/1.13-2998       cuda/9.2
apps/gcc/4.4.7/relion/cpu/1.4         dot
apps/gcc/4.4.7/relion/cpu/2.1         modules
apps/gcc/4.4.7/relion/cpu/3.0-beta    mpi/gcc/openmpi/1.6.5
apps/gcc/4.4.7/relion/cuda92/2.1
``

Job manager (Torque)
====================
