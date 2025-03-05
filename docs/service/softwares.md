# GSDC TEM Cluster Management Softwares

## Operating System (OS)

* Name : AlmaLinux
* Version : 9.4
* Description : Open-source, community-driven Linux operating system
* URL : [https://almalinux.org](https://almalinux.org)

## Build Tools (Compilers)

### GNU 
* Name : GNU Compiler
* Version : 11.5.0
* Description : Compiler for the GNU operating system
* URL : [https://gcc.gnu.org](https://gcc.gnu.org)

???+ note "ModulePaths for GNU Compiler"

    ```bash
    gcc/11.5.0
    ```

### Intel
* Name : Intel Compiler Collection (OneAPI)
* Version : 2024.0
* Description : Compiler collection for generating Intel CPU optimized executable
* URL : [https://www.intel.com/content/www/us/en/developer/tools/oneapi/toolkits.html](https://www.intel.com/content/www/us/en/developer/tools/oneapi/toolkits.html)

???+ note "ModulePaths for Intel Compiler"

    ```bash
    intel/dal/2024.0.0              intel/ifort32/2024.0.2          intel/mkl/2024.0
    intel/advisor/2024.0            intel/debugger/2024.0.0         intel/inspector/2024.0              intel/mkl32/2024.0
    intel/ccl/2021.11.2             intel/dev-utilities/2024.0.0    intel/intel_ipp_ia32/2021.10        intel/mpi/2021.11
    intel/compiler-rt/2024.0.2      intel/dnnl/3.3.0                intel/intel_ipp_intel64/2021.10     intel/oclfpga/2024.0.0
    intel/compiler-rt32/2024.0.2    intel/dpct/2024.0.0             intel/intel_ippcp_ia32/2021.9       intel/tbb/2021.11
    intel/compiler/2024.0.2         intel/dpl/2022.3                intel/intel_ippcp_intel64/2021.9    intel/tbb32/2021.11
    intel/compiler32/2024.0.2       intel/ifort/2024.0.2            intel/itac/2022.0                   intel/vtune/2024.0
    ```

## Environment Modules
* Name : LMOD
* Version : 8.7.53
* Description : A Lua based module system that easily handles the MODULEPATH Hierarchical problem. Environment Modules provide a convenient way to dynamically change the users’ environment through modulefiles.
* URL : [https://lmod.readthedocs.io/en/latest](https://lmod.readthedocs.io/en/latest)

## Batch System
* Name : PBS Professional (Community Edition)
* Version : 23.06.06
* Description : Job scheduling and workload management in high-performance computing (HPC) environments – clusters, clouds, and supercomputers – improving system efficiency and people’s productivity.
* URL : [https://github.com/openpbs/openpbs](https://github.com/openpbs/openpbs)

## MPI (Message Passing Interfaces)
* Name : OpenMPI
* Version : 5.0.3
* Description : An open source Message Passing Interface implementation that is developed and maintained by a consortium of academic, research, and industry partners.
* URL : [https://www.open-mpi.org](https://www.open-mpi.org)

???+ note "ModulePaths for MPI"

    ```bash
    openmpi/5.0.3/gcc-11.5.0
    openmpi/5.0.3/intel-compiler-2024.0.2
    ```

## Virtual Environments
* Name : Anaconda
* Version : 2024.10-1
* Description : A collection of tools and a distribution of the Python and R programming languages for data science and machine learning. It's used to develop and manage data science and AI projects.
* URL : [https://anaconda.com](https://anaconda.com)

???+ note "ModulePaths for Anaconda"

    ```bash
    anaconda3/2024.10-1
    ```

## NVIDIA Software Development Kit (SDK)
* Name : CUDA
* Version : 11.8 or above
* Description : A parallel computing platform and programming model created by NVIDIA
* URL : [https://developer.nvidia.com/cuda-toolkit](https://developer.nvidia.com/cuda-toolkit)

???+ note "ModulePaths for CUDA"

    ```bash
    cuda/11.8
    cuda/12.6
    ```
