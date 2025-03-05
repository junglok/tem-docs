# Environment Modules

## Overview
The Environment Modules (Lmod) is a tool to help users manage their Unix or Linux shell environment, by allowing groups of related environment-variable settings to be made or removed dynamically.

Lmod is a Lua-based module system that easily handles the MODULEPATH hierarchical problem. Lmod provide a convenient way to dynamically change the users’ environment through modulefiles. 

This includes easily adding or removing directories to the PATH environment variable. Modulefiles for library packages provide environment variables that specify where the library and header files can be found.

## Listing the loaded modules

* To list all the modules already loaded by the user

=== "Command"

    ```bash
    $> module list
    ```

=== "Example"

    ```bash
    $> module list

    Currently Loaded Modules:
      1) gcc/11.5.0   2) cuda/12.6   3) openmpi/5.0.3/gcc-11.5.0   4) apps/relion/4.0.1/gpu/cuda-12.6 

    ```

## Finding out what modules are available

## Searching modules

## Showing the defails of the module

## Accessing a modulesfile's help

## Loding modules

## Unloading modules

## Removing all the modules loaded

## Modules help