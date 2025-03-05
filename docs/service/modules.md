# Environment Modules

## Overview
The Environment Modules (Lmod) is a tool to help users manage their Unix or Linux shell environment, by allowing groups of related environment-variable settings to be made or removed dynamically.

Lmod is a Lua-based module system that easily handles the MODULEPATH hierarchical problem. Lmod provide a convenient way to dynamically change the users’ environment through modulefiles. 

This includes easily adding or removing directories to the PATH environment variable. Modulefiles for library packages provide environment variables that specify where the library and header files can be found.

## Listing the loaded modules

* To list all the modules already loaded by the user

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

* To find out what modules are available to be loaded a user can do

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

* If there are many modules on a system, it can be difficult to see what modules are available to load. Lmod provides the **overview command** to provide a concise listing

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

* Keyword search tool : This will search any help message or whatis description for the word(s) given on the command

=== ":material-powershell: Command"

    ```bash
    $> module keyword <keyword>
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

* Spider command : Another way to search for modules is with the “module spider” command. This command searches the entire list of possible modules. 

=== ":material-powershell: Command"

    ```bash
    $> module spider <keyword>
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

There are several ways to use the show sub-command to show the contents of a modulefile. The first is to show the module functions instead of executing them:

=== ":material-powershell: Command"

    ```bash
    $> module show <packageName>
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

Modulefiles can contain help messages. To access a modulefile’s help do:

=== ":material-powershell: Command"

    ```bash
    $> module help <packageName>
    ```

=== ":material-alpha-e-box-outline: Example"

    ```bash
    $> module help apps/relion/5.0.0/gpu/cuda-12.6
    ----------------- Module Specific Help for "apps/relion/5.0.0/gpu/cuda-12.6" -----------------
    Relion version 5.0.0 built on top of GPU build tools:
    RELION (for REgularised LIkelihood OptimisatioN, pronounce rely-on) is a stand-alone 
    computer program that employs an empirical Bayesian approach to refinement of 
    (multiple) 3D reconstructions or 2D class averages in electron cryo-microscopy.
    https://relion.readthedocs.io/en/release-5.0/index.html
    ```

## Loding modules

* To load packages a user simply does:

=== ":material-powershell: Command"

    ```bash
    $> module load <package1> <package2> ...
    ```

=== ":material-alpha-e-box-outline: Example"

    ```bash
    $> module list
    No modules loaded
    $> module load apps/relion/4.0.1/gpu/cuda-12.6
    $> module list
    Currently Loaded Modules:
      1) gcc/11.5.0   2) cuda/12.6   3) openmpi/5.0.3/gcc-11.5.0   4) apps/relion/4.0.1/gpu/cuda-12.6 
    ```

## Unloading modules

* To unload packages a user does:

=== ":material-powershell: Command"

    ```bash
    $> module unload <package1> <package2> ...
    ```

=== ":material-alpha-e-box-outline: Example"

    ```bash
    $> module list
    Currently Loaded Modules:
      1) gcc/11.5.0   2) cuda/12.6   3) openmpi/5.0.3/gcc-11.5.0   4) apps/relion/4.0.1/gpu/cuda-12.6 
    $> module unload apps/relion/4.0.1/gpu/cuda-12.6
    $> module list
    No modules loaded
    ```

## Removing all the modules loaded

* To remove all the loaded modules

=== ":material-powershell: Command"

    ```bash
    $> module purge
    ```

=== ":material-alpha-e-box-outline: Example"

    ```bash
    $> module list
    Currently Loaded Modules:
      1) gcc/11.5.0   2) cuda/12.6   3) openmpi/5.0.3/gcc-11.5.0   4) apps/relion/4.0.1/gpu/cuda-12.6 
    $> module purge
    $> module list
    No modules loaded
    ```

## Modules help

* To get a list of all the commands that module knows about 

=== ":material-powershell: Command"

    ```bash
    $> module help
    ```

=== ":material-alpha-e-box-outline: Example"

    ```bash
    $> module help
    Usage: module [options] sub-command [args ...]

    Options:
    -h -? -H --help                   This help message
    -s availStyle --style=availStyle  Site controlled avail style: system (default: system)
    --regression_testing              Lmod regression testing
    -b --brief                        brief listing with only user specified modules
    -D                                Program tracing written to stderr
    --debug=dbglvl                    Program tracing written to stderr (where dbglvl is a number 1,2,3)
    --pin_versions                    When doing a restore use specified version, do not follow defaults
    -d --default                      List default modules only when used with avail
    -q --quiet                        Do not print out warnings
    --expert                          Expert mode
    -t --terse                        Write out in machine readable format for commands: list, avail, spider, savelist
    --initial_load                    loading Lmod for first time in a user shell
    --latest                          Load latest (ignore default)
    -I --ignore_cache                 Treat the cache file(s) as out-of-date
    --novice                          Turn off expert and quiet flag
    --raw                             Print modulefile in raw output when used with show
    -w twidth --width=twidth          Use this as max term width
    -v --version                      Print version info and quit
    -r --regexp                       use regular expression match
    --gitversion                      Dump git version in a machine readable way and quit
    --dumpversion                     Dump version in a machine readable way and quit
    --dumpname                        Dump the name Lmod in a machine readable way and quit
    --check_syntax --checkSyntax      Checking module command syntax: do not load
    --config                          Report Lmod Configuration
    --miniConfig                      Report Lmod Configuration differences
    --config_json                     Report Lmod Configuration in json format
    --mt                              Report Module Table State
    --timer                           report run times
    -f --force                        force removal of a sticky module or save an empty collection
    --redirect                        Send the output of list, avail, spider to stdout (not stderr)
    --no_redirect                     Force output of list, avail and spider to stderr
    --show_hidden -A --all            Avail and spider will report hidden modules
    --spider_timeout=timeout          a timeout for spider
    -T --trace                        trace major changes such as loads
    --nx --no_extensions              Do not print extensions
    --loc --location                  Just print the file location when using show
    --terse_show_extensions           report extensions when doing a terse avail
    --pod                             Generate pod format

    module [options] sub-command [args ...]

    Help sub-commands:
    help                              prints this message
    help                module [...]  print help message from module(s)

    Loading/Unloading sub-commands:
    load | add          module [...]  load module(s)
    try-load | try-add  module [...]  Add module(s), do not complain if not found
    del | unload        module [...]  Remove module(s), do not complain if not found
    swap | sw | switch  m1 m2         unload m1 and load m2
    purge                             unload all modules
    refresh                           reload aliases from current list of modules.
    update                            reload all currently loaded modules.

    Listing / Searching sub-commands:
    list                              List loaded modules
    list                s1 s2 ...     List loaded modules that match the pattern
    avail | av                        List available modules
    avail | av          string        List available modules that contain "string".
    category | cat                    List all categories
    category | cat      s1 s2 ...     List all categories that match the pattern and display their modules
    overview | ov                     List all available modules by short names with number of versions
    overview | ov       string        List available modules by short names with number of versions that contain "string"
    spider                            List all possible modules
    spider              module        List all possible version of that module file
    spider              string        List all module that contain the "string".
    spider              name/version  Detailed information about that version of the module.
    whatis              module        Print whatis information about module
    keyword | key       string        Search all name and whatis that contain "string".

    Searching with Lmod:
    All searching (spider, list, avail, keyword) support regular expressions:


    -r spider           '^p'          Finds all the modules that start with `p' or `P'
    -r spider           mpi           Finds all modules that have "mpi" in their name.
    -r spider           'mpi$         Finds all modules that end with "mpi" in their name.

    Handling a collection of modules:
    save | s                          Save the current list of modules to a user defined "default" collection.
    save | s            name          Save the current list of modules to "name" collection.
    reset                             The same as "restore system"
    restore | r                       Restore modules from the user's "default" or system default.
    restore | r         name          Restore modules from "name" collection.
    restore             system        Restore module state to system defaults.
    savelist                          List of saved collections.
    describe | mcc      name          Describe the contents of a module collection.
    disable             name          Disable (i.e. remove) a collection.

    Deprecated commands:
    getdefault          [name]        load name collection of modules or user's "default" if no name given.
                                        ===> Use "restore" instead  <====
    setdefault          [name]        Save current list of modules to name if given, otherwise save as the default list for you the user.
                                        ===> Use "save" instead. <====

    Miscellaneous sub-commands:
    is-loaded           modulefile    return a true status if module is loaded
    is-avail            modulefile    return a true status if module can be loaded
    show                modulefile    show the commands in the module file.
    use [-a]            path          Prepend or Append path to MODULEPATH.
    unuse               path          remove path from MODULEPATH.
    tablelist                         output list of active modules as a lua table.

    Important Environment Variables:
    LMOD_COLORIZE                     If defined to be "YES" then Lmod prints properties and warning in color.


    Lmod Web Sites

    Documentation:    https://lmod.readthedocs.org
    GitHub:           https://github.com/TACC/Lmod
    SourceForge:      https://lmod.sf.net
    TACC Homepage:    https://www.tacc.utexas.edu/research-development/tacc-projects/lmod

    To report a bug please read https://lmod.readthedocs.io/en/latest/075_bug_reporting.html

    Modules based on Lua: Version 8.7.53 2024-10-12 19:57 -05:00
        by Robert McLay mclay@tacc.utexas.edu    
    ```