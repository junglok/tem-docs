# Environment Modules

## Overview
The Environment Modules (Lmod) is a tool to help users manage their Unix or Linux shell environment, by allowing groups of related environment-variable settings to be made or removed dynamically.

Lmod is a Lua-based module system that easily handles the MODULEPATH hierarchical problem. Lmod provide a convenient way to dynamically change the users’ environment through modulefiles. 

This includes easily adding or removing directories to the PATH environment variable. Modulefiles for library packages provide environment variables that specify where the library and header files can be found.

## Listing the loaded modules

> * To list all the modules already loaded by the user

=== ":material-powershell: Command"

    ```bash
    $> module list
    ```

=== ":material-alpha-e-box-outline: Example"

    ```bash
    $> module list
    Currently Loaded Modules:
      1) gcc/11.5.0   2) cuda/12.6   3) openmpi/5.0.3/gcc-11.5.0   4) apps/relion/4.0.1/gpu/cuda-12.6 

    ```

## Finding out what modules are available

> * To find out what modules are available to be loaded a user can do

=== ":material-powershell: Command"

    ```bash
    $> module avail
    ```

=== ":material-alpha-e-box-outline: Example"

    ```bash
    $> module avail
    ---------------------------------- /tem/el9/system/lmod/8.7.53/modulefiles/applications ----------------
    apps/aretomo/1.3.4/gpu/cuda-11.8                       apps/relion/4.0.1/gpu/cuda-11.8
    apps/aretomo2/1.1.2/gpu/cuda-11.8                      apps/relion/4.0.1/gpu/cuda-12.6               (D)
    apps/aretomo2/1.1.2/gpu/cuda-12.6               (D)    apps/relion/5.0.0/cpu/gcc-11.5.0
    apps/aretomo3/2.0.3/gpu/cuda-11.8                      apps/relion/5.0.0/cpu/intel-compiler-2024.0.2 (D)
    apps/aretomo3/2.0.3/gpu/cuda-12.6               (D)    apps/relion/5.0.0/gpu/cuda-11.8
    apps/ctffind/4.1.14/cpu/gcc-11.5.0                     apps/relion/5.0.0/gpu/cuda-12.6               (D)
    apps/ctffind/4.1.14/cpu/intel-compiler-2024.0.2 (D)    apps/resmap/1.1.4
    apps/isonet/0.2.1/gpu/cuda-12.5                        apps/summovie/1.0.2
    apps/isonet/0.3.0/gpu/cuda-12.5                        apps/topaz/0.2.5/gpu/cuda-11.8
    apps/motioncor2/1.6.4/gpu/cuda-11.8                    apps/topaz/0.2.5/gpu/cuda-12.4                (D)
    apps/motioncor3/1.1.1/gpu/cuda-11.8                    apps/topaz/0.2.5_filaments/gpu/cuda-11.8
    apps/motioncor3/1.1.1/gpu/cuda-12.6             (D)    apps/topaz/0.2.5_filaments/gpu/cuda-12.4      (D)
    apps/pyem/0.65                                         apps/topaz/0.3.1/gpu/cuda-11.8
    apps/relion/4.0.1/cpu/gcc-11.5.0                       apps/topaz/0.3.1/gpu/cuda-12.4                (D)
    apps/relion/4.0.1/cpu/intel-compiler-2024.0.2   (D)    apps/unblur/1.0.2
    ------------------------------------ /tem/el9/system/lmod/8.7.53/modulefiles/virtual -------------------
    anaconda3/2024.10-1
    -------------------------------------- /tem/el9/system/lmod/8.7.53/modulefiles/mpi ---------------------
    openmpi/5.0.3/gcc-11.5.0    openmpi/5.0.3/intel-compiler-2024.0.2 (D)
    ---------------------------------- /tem/el9/system/lmod/8.7.53/modulefiles/acceleration ----------------
    cuda/11.8    cuda/12.6 (D)
    ------------------------------------ /tem/el9/system/lmod/8.7.53/modulefiles/compiler ------------------
    gcc/11.5.0                      intel/dnnl/3.3.0                    intel/itac/2022.0
    intel/advisor/2024.0            intel/dpct/2024.0.0                 intel/mkl/2024.0
    intel/ccl/2021.11.2             intel/dpl/2022.3                    intel/mkl32/2024.0
    intel/compiler-rt/2024.0.2      intel/ifort/2024.0.2                intel/mpi/2021.11
    intel/compiler-rt32/2024.0.2    intel/ifort32/2024.0.2              intel/oclfpga/2024.0.0
    intel/compiler/2024.0.2         intel/inspector/2024.0              intel/tbb/2021.11
    intel/compiler32/2024.0.2       intel/intel_ipp_ia32/2021.10        intel/tbb32/2021.11
    intel/dal/2024.0.0              intel/intel_ipp_intel64/2021.10     intel/vtune/2024.0
    intel/debugger/2024.0.0         intel/intel_ippcp_ia32/2021.9
    intel/dev-utilities/2024.0.0    intel/intel_ippcp_intel64/2021.9

    Where:
    D:  Default Module
    If the avail list is too long consider trying:
    "module --default avail" or "ml -d av" to just list the default modules.
    "module overview" or "ml ov" to display the number of modules for each name.
    Use "module spider" to find all possible modules and extensions.
    Use "module keyword key1 key2 ..." to search for all possible modules matching any of the "keys".
    ```

> * If there are many modules on a system, it can be difficult to see what modules are available to load. Lmod provides the **overview command** to provide a concise listing

=== ":material-powershell: Command"

    ```bash
    $> module overview
    ```

=== ":material-alpha-e-box-outline: Example"

    ```bash
    $> module overview
    ------------- /tem/el9/system/lmod/8.7.53/modulefiles/applications ----------
    apps/aretomo/1.3.4/gpu    (1)   apps/relion/4.0.1/gpu          (2)
    apps/aretomo2/1.1.2/gpu   (2)   apps/relion/5.0.0/cpu          (2)
    apps/aretomo3/2.0.3/gpu   (2)   apps/relion/5.0.0/gpu          (2)
    apps/ctffind/4.1.14/cpu   (2)   apps/resmap                    (1)
    apps/isonet/0.2.1/gpu     (1)   apps/summovie                  (1)
    apps/isonet/0.3.0/gpu     (1)   apps/topaz/0.2.5/gpu           (2)
    apps/motioncor2/1.6.4/gpu (1)   apps/topaz/0.2.5_filaments/gpu (2)
    apps/motioncor3/1.1.1/gpu (2)   apps/topaz/0.3.1/gpu           (2)
    apps/pyem                 (1)   apps/unblur                    (1)
    apps/relion/4.0.1/cpu     (2)
    ---------------- /tem/el9/system/lmod/8.7.53/modulefiles/virtual -----------
    anaconda3 (1)
    ------------------ /tem/el9/system/lmod/8.7.53/modulefiles/mpi -------------
    openmpi/5.0.3 (2)
    ------------- /tem/el9/system/lmod/8.7.53/modulefiles/acceleration ---------
    cuda (2)
    --------------- /tem/el9/system/lmod/8.7.53/modulefiles/compiler -----------
    gcc                 (1)   intel/dnnl                (1)   intel/itac    (1)
    intel/advisor       (1)   intel/dpct                (1)   intel/mkl     (1)
    intel/ccl           (1)   intel/dpl                 (1)   intel/mkl32   (1)
    intel/compiler-rt   (1)   intel/ifort               (1)   intel/mpi     (1)
    intel/compiler-rt32 (1)   intel/ifort32             (1)   intel/oclfpga (1)
    intel/compiler      (1)   intel/inspector           (1)   intel/tbb     (1)
    intel/compiler32    (1)   intel/intel_ipp_ia32      (1)   intel/tbb32   (1)
    intel/dal           (1)   intel/intel_ipp_intel64   (1)   intel/vtune   (1)
    intel/debugger      (1)   intel/intel_ippcp_ia32    (1)
    intel/dev-utilities (1)   intel/intel_ippcp_intel64 (1)
    ```

## Searching modules

> * Keyword search tool : This will search any help message or whatis description for the word(s) given on the command

=== ":material-powershell: Command"

    ```bash
    $> module keyword
    ```

=== ":material-alpha-e-box-outline: Example"

    ```bash
    $> module keyword nvidia
    -----------------------------------------------------------
    The following modules match your search criteria: "nvidia"
    -----------------------------------------------------------
    cuda: cuda/11.8, cuda/12.6
        NVIDIA CUDA
    -----------------------------------------------------------
    To learn more about a package execute:
    $ module spider Foo
    where "Foo" is the name of a module.
    To find detailed information about a particular package you
    must specify the version if there is more than one version:
    $ module spider Foo/11.1
    -----------------------------------------------------------
    ```

> * Spider command : Another way to search for modules is with the “module spider” command. This command searches the entire list of possible modules. 

=== ":material-powershell: Command"

    ```bash
    $> module spider
    ```

=== ":material-alpha-e-box-outline: Example"

    ```bash
    $> module spider cuda
    ------------------------------------------------------------------
    cuda:
    ------------------------------------------------------------------
        Description:
        NVIDIA CUDA
        Versions:
            cuda/11.8
            cuda/12.6
    ------------------------------------------------------------------
    For detailed information about a specific "cuda" package 
    (including how to load the modules) use the module's full name.
    Note that names that have a trailing (E) are extensions provided 
    by other modules.
    For example:
        $ module spider cuda/12.6
    ------------------------------------------------------------------
    ```

## Showing the defails of the module

> There are several ways to use the show sub-command to show the contents of a modulefile. The first is to show the module functions instead of executing them:

=== ":material-powershell: Command"

    ```bash
    $> module show
    ```

=== ":material-alpha-e-box-outline: Example"

    ```bash
    $> module show apps/relion/5.0.0/gpu/cuda-12.6
    ------------------------------------------------------------------------------
    /tem/el9/system/lmod/8.7.53/modulefiles/applications/apps/relion/5.0.0/gpu/cuda-12.6.lua:
    ------------------------------------------------------------------------------
    help([[
    Relion version 5.0.0 built on top of GPU build tools:
    RELION (for REgularised LIkelihood OptimisatioN, pronounce rely-on) is 
    a stand-alone computer program that employs an empirical Bayesian approach to refinement of
    (multiple) 3D reconstructions or 2D class averages in electron cryo-microscopy.

    https://relion.readthedocs.io/en/release-5.0/index.html

    ]])
    whatis("Name:         RELION")
    whatis("Version:      5.0.0 on top of GPU build tools")
    whatis("Description:  RELION (for REgularised LIkelihood OptimisatioN, pronounce rely-on)")
    whatis("URL:          https://relion.readthedocs.io/")
    whatis("Categories:   Cryo-EM, Cryo-ET, data analysis, MPI")
    whatis("Keywords:     RHEL9, data analysis, GPU build tools")
    depends_on("anaconda3/2024.10-1")
    depends_on("gcc/11.5.0")
    depends_on("cuda/12.6")
    depends_on("openmpi/5.0.3/gcc-11.5.0")
    prepend_path("PATH","/tem/el9/applications/relion-5.0.0-gpu-cuda-12.6/bin")
    prepend_path("LD_LIBRARY_PATH","/tem/el9/applications/relion-5.0.0-gpu-cuda-12.6/lib")
    setenv("LANG","en_US.UTF-8")
    setenv("TORCH_HOME","~/.cache/torch")
    setenv("RELION_QUEUE_USE","yes")
    setenv("RELION_QUEUE_NAME","gpuQ")
    setenv("RELION_QSUB_COMMAND","qsub")
    setenv("RELION_QSUB_EXTRA_COUNT","4")
    setenv("RELION_QSUB_EXTRA1","Number of Nodes")
    setenv("RELION_QSUB_EXTRA2","Number of processes per each node")
    setenv("RELION_QSUB_EXTRA3","Number of GPUs per node")
    setenv("RELION_QSUB_EXTRA4","Amount of memory(GB) per each node")
    setenv("RELION_QSUB_EXTRA1_DEFAULT","1")
    setenv("RELION_QSUB_EXTRA2_DEFAULT","3")
    setenv("RELION_QSUB_EXTRA3_DEFAULT","2")
    setenv("RELION_QSUB_EXTRA4_DEFAULT","64")
    conflict("apps/relion")
    ```


## Accessing a modulesfile's help

## Loding modules

## Unloading modules

## Removing all the modules loaded

## Modules help