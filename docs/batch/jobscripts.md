# PBS (Portable Batch System) Job Scripts

**Job scripts** form the basis of batch jobs. A job script is simply a text file with instructions of the work to execute.
Job scripts are *usually* written in `bash` and thus mimic commands a user would execute interactively through a shell; but instead are executed on 
specific resources allocated by the scheduler when available. Scripts can also be written in other languages - commonly *Python*.

## **Basics of a Job Script**
Sample basic PBS scripts are shown below:

!!! example "PBS Job Scripts"
    === "Bash"
        ```bash
        #!/bin/bash
        #PBS -N hello_pbs
        #PBS -j oe
        #PBS -k eod
        #PBS -q cpuQ
        #PBS -l walltime=00:05:00
        #PBS -l select=2:ncpus=16:mem=64GB:mpiprocs=16

        ### Set temp to scratch (note that <GroupDir> should be replaced with the proper name)
        setenv TMPDIR /tem/scratch/<GroupDir>/temp && mkdir -p ${TMPDIR}

        ### Specify desired module environment to be loaded
        module purge
        module load openmpi/5.0.3/gcc-11.5.0
        module list

        ### Compile and Run MPI Program
        mpicc -o hello_c /tem/el9/samples/hello_c.c -fopenmp
        mpirun --mca btl tcp,self --mca btl_tcp_port_min_v4 32768 --mca btl_tcp_port_range_v4 32768 -n 32 --machinefile $PBS_NODEFILE ./hello_c
        ```

        ---

        The first line denotes the interpreter to be used for the script:
        ```bash
        #!/bin/bash
        ```
    === "Python"
        ```python
        #!/usr/bin/python
        #PBS -N hello_python_pbs
        #PBS -j oe
        #PBS -k eod
        #PBS -q cpuQ
        #PBS -l walltime=00:05:00
        #PBS -l select=1:ncpus=8

        import sys
        print("Hello, world!!\n\n")

        print("Python version:")
        print(sys.version)
        print("Version info:")
        print(sys.version_info)
        ```

        ---

        The  first line denotes the interpreter to be used for the script:
        ```python
        #!/usr/bin/python
        ```
        indicates this is a `python` script

**Focusing on the `bash` example for discussion**, the remainder of the script contains two main sections:

1.  The lines beginning with `#PBS` are **directives** that will be interpreted by PBS when this script is submitted with `qsub`.
    Each of these lines contains an instruction that will be used by `qsub` to control job resources, execution, etc...

2.  The remaining **script contents** are simply `bash` commands that will be run inside the batch environment on the selected resources and define the work to be done in this job.


### **PBS directives**

The example above contains several **directives** which are interpreted by the `qsub` submission program:

* **`-N hello_pbs`**
  > provides a *job name*. This name will be displayed by the scheduler for diagnostic and file output. 
  > If omitted, and a script is used to submit the job, the job's name is the name of the script.
* **`-j oe`**
  > requests we *combine any standard text output (`o`) and error (`e`) into one output file*.
  > (By default, PBS will write program output and error to different log files. This behavior is contrary to what many users expect from terminal interaction, where output and error are generally interspersed. This optional flag changes that behavior.)
* **`-q cpuQ`**
  > specifies the desired PBS *queue* for this job.
* **`-l walltime=00:05:00`**
  > requests 5 minutes as the maximum job execution (*walltime*) time.  Specified in `HH:MM:SS` format.
* **`-l select=2:ncpus=16:mem=64GB:mpiprocs=16`** 
  > a computational *resource chunk* request, detailing the quantity and configuration of *compute nodes* required for this job. This example requests a *selection* of 2 nodes, where each node must have 16 CPU cores and 64GB free memory, each of which we will use as an MPI rank in our application.


### **Script contents**

The remaining script contains shell commands that define the job execution workflow. 
The commands here are arbitrary, however we strongly recommend the general structure presented above.  This includes:

1.  **(*Optional*) Explicitly setting the `TMPDIR` variable.**

    Many programs can write temporary data to `TMPDIR`, which is usually small (e.g., 30 ~ 40 GBytes) and shared among normal users. Specifying your own directory for temporary
    files can help you avoid the risk of your own programs and other users' programs failing when no more space is available.

2.  **Loading and reporting the specific module environment required for this job.**

    While strictly not necessary, we recommend this as best practice as it facilitates debugging and reproducing later. (Manually specifying module versions allows you to recreate the same execution environment in the future.)

3.  **Defining any environment variables specific to the chosen module environment.**

    Occasionally users will want to define particular run time environment variables e.g. for a specific MPI or library chosen via the `module load` commands.

4.  **Remaining job-specific steps.**

    In the example above, we first compile and then execute `hello_c.c`, a simple MPI program with having total 32 processes on 2 nodes.

---

## Common `#PBS` directives

### **Resource requests**
Resources (compute node configuration, job duration) are requested through a combination of *resource selection* flags, each preceded with `-l`.

For example:
```pre
#PBS -l walltime=00:05:00
#PBS -l select=1:ncpus=64:mpiprocs=4:ngpus=4:mem=256GB
```
specifies job `walltime` and compute node selection. See more details below.


#### **`select` statements**
Resources are specified through a `select` statement. The general form of a *homogeneous* selection statement is
```pre
select=<# NODES>:ncpus=<# CPU Cores/node>:mem=<RAM/node>:mpiprocs=<# MPI Ranks/node>:ompthreads=<# OpenMP Threads/rank>:ngpus=<# GPUs/node>
```
where

**`<# NODES>`** 
> the total number of compute nodes requested, followed by a colon-separated list (see below)

**`<# CPU Cores/node>`** 
> the *total* number of CPUs requested *on each node*, which can be a mix of MPI Ranks and/or OpenMP threads,

**`<RAM/node>`** 
> how much main memory (RAM) the job will be able to access *on each node*. 
> (Optional, default is system dependent, but system default is very small amount memory 256MBytes, so as the best practice, we recommend to explicitly specify the size of memory required),
  
**`<# MPI Ranks/node>`** 
> the number of MPI Ranks *on each node* (Optional, defaults to 1),

**`<# OpenMP Threads/node>`** 
> the number of OpenMP ranks *per MPI Rank on each node* (Optional, defaults to 1)

**`<# GPUs/node>`** 
> the number of GPUs *per node*. (Optional, defaults to 0).

Taken together, this specifies a *resource chunk*. Homogeneous resource chunks are the most common case, however, 
*heterogeneous* selection statements can be constructed by multiple chunks separated by a **+** (examples below).

##### Examples
*  4 128-core nodes, each running 128 MPI ranks (4 `x` 128 = 512 MPI ranks total).
   ```pre
   select=4:ncpus=128:mpiprocs=128
   ```

*  4 128-core nodes, each running 32 MPI ranks with 4 OpenMP threads per rank (4 `x` 32 = 128 MPI ranks total, each with 4 threads = 512 total CPU cores).
   ```pre
   select=4:ncpus=128:mpiprocs=32:ompthreads=4
   ```

*  2 64-core nodes, each running 4 MPI ranks, 4 GPUS, and 384 GB memory (8 GPUs total, with 8 MPI ranks).
   ```pre
   select=2:ncpus=64:mpiprocs=4:ngpus=4:mem=384GB
   ```

*  A heterogeneous selection, 96 128-core nodes each with 128 MPI ranks, and 32 128-core nodes each with 16 MPI ranks and 8 OpenMP threads
   ```pre
   select=96:ncpus=128:mpiprocs=128+32:ncpus=128:mpiprocs=16:ompthreads=8
   ```

#### `walltime` statements
The `-l walltime=HH:MM:SS` resource directive specifies maximum job duration.
Jobs still running when this wall time is exceeded will be terminated automatically by the scheduler. (Optional, defaults to infinite)
```pre
walltime=HH:MM:SS
```

## **Execution environment variables**
Within the **script contents** of the job script, it is common for the specifics of the job to depend slightly on the PBS and specific `module` execution environment.
Both running under PBS and loading certain [module files](../service/modules.md) create some environment variables that might be useful when writing
portable scripts; for example scripts that might be shared among users or executed within several different configurations.

### PBS execution environment variables
PBS creates a number of environment variables that are accessible within a job's execution environment.
Some of the more useful ones are:

|  <div style="width:110px">Variable</div> | Value |
|---------------|-------|
| `PBS_JOBID`     | The PBS Job ID for this job.<br>Example: `1473351.tem-ce-al9` |
| `PBS_JOBNAME`   | The name of this job. Matches the `-N` specified.<br>Example: `hello_pbs` |
| `PBS_O_WORKDIR` | The working directory from where the job was submitted. |
| `PBS_SELECT`    | The resource specification `-l select=` line for this job.<br>This can be useful for setting runtime-specific configuration options that might depend on resource selection.<br>(e.g. processor layout, CPU binding, etc...)<br>Example: `2:ncpus=128:mpiprocs=2:ompthreads=2:mem=200GB:ngpus=1`  |
| `PBS_NODEFILE`  | A file whose contents lists the nodes assigned to this job.<br> Typically listed as one node name per line, for each MPI rank in the job.<br>Each node will be listed for as many times as it has MPI ranks. <br>Example: `/var/spool/pbs/aux/1473351.tem-ce-al9` |
<!-- | `PBS_QUEUE`     | The name of the PBS execution queue.<br>In general this will be an *execution* queue, and different than the *routing* queue specified by `-q` in the job script.<br>Example: `cpu` | -->