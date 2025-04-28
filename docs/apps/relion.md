# Relion

RELION (for REgularised LIkelihood OptimisatioN, pronounce rely-on) is a stand-alone computer program that employs an empirical Bayesian approach to refinement of (multiple) 3D reconstructions or 2D class averages in electron cryo-microscopy (cryo-EM).

## Executing relion

1. Find out relion applications module path by `module keyword` command

``` bash
$> module keyword relion
------------------------------------------------------------------------------------------------------------
The following modules match your search criteria: "relion"
------------------------------------------------------------------------------------------------------------

  apps/relion/4.0.1/cpu: apps/relion/4.0.1/cpu/gcc-11.5.0, apps/relion/4.0.1/cpu/intel-compiler-2024.0.2
    RELION (for REgularised LIkelihood OptimisatioN, pronounce rely-on)

  apps/relion/4.0.1/gpu: apps/relion/4.0.1/gpu/cuda-11.8, apps/relion/4.0.1/gpu/cuda-12.6
    RELION (for REgularised LIkelihood OptimisatioN, pronounce rely-on)

  apps/relion/5.0.0/cpu: apps/relion/5.0.0/cpu/gcc-11.5.0, apps/relion/5.0.0/cpu/intel-compiler-2024.0.2
    RELION (for REgularised LIkelihood OptimisatioN, pronounce rely-on)

  apps/relion/5.0.0/gpu: apps/relion/5.0.0/gpu/cuda-11.8, apps/relion/5.0.0/gpu/cuda-12.6
    RELION (for REgularised LIkelihood OptimisatioN, pronounce rely-on)

------------------------------------------------------------------------------------------------------------
To learn more about a package execute:
   $ module spider Foo
where "Foo" is the name of a module.
To find detailed information about a particular package you
must specify the version if there is more than one version:
   $ module spider Foo/11.1
------------------------------------------------------------------------------------------------------------
```

2. Load the environment module of relion which you want to use. As the module specified is loaded, all other dependent modules are also automatically loaded (you can check these modules with `module list` command)
3. Check the binary path of the relion application
4. Execute the relion (we assume that X11 forwarding is enabled)