# PBS (Portable Batch System) Job Scripts

**Job scripts** form the basis of batch jobs. A job script is simply a text file containing instructions for the work to execute.
Job scripts are *usually* written in `bash`, mimicking commands a user would run interactively through a shell, but they execute on 
specific resources allocated by the scheduler when available. Scripts can also be written in other languages, commonly *Python*.

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

        The first line specifies the interpreter for the script:
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

        The first line specifies the interpreter for the script:
        ```python
        #!/usr/bin/python
        ```
        indicating this is a `python` script

**Focusing on the `bash` example**, the rest of the script contains two main sections:

1.  Lines beginning with `#PBS` are **directives** that PBS interprets when the script is submitted with `qsub`.
    Each line gives `qsub` an instruction for controlling job resources, execution, and so on.

2.  The remaining **script contents** are simply `bash` commands that run inside the batch environment on the selected resources, defining the job's work.


### **PBS directives**

The example above contains several **directives** interpreted by the `qsub` submission program:

* **`-N hello_pbs`**
  > sets a *job name*, displayed by the scheduler for diagnostics and file output. 
  > If omitted, and a script is used to submit the job, the job's name defaults to the script's name.
* **`-j oe`**
  > *combines standard output (`o`) and error (`e`) into one output file*.
  > (By default, PBS writes program output and error to separate log files. This differs from typical terminal interaction, where output and error are usually interspersed. This optional flag changes that behavior.)
* **`-q cpuQ`**
  > specifies the PBS *queue* for this job.
* **`-l walltime=00:05:00`**
  > sets 5 minutes as the maximum job execution (*walltime*) time, specified in `HH:MM:SS` format.
* **`-l select=2:ncpus=16:mem=64GB:mpiprocs=16`** 
  > a computational *resource chunk* request, detailing the quantity and configuration of *compute nodes* required. This example requests 2 nodes (chunks), each with 16 CPU cores and 64GB of free memory, with each core used as an MPI rank. In this document, *node* and *chunk* are used interchangeably.


### **Script contents**

The remaining script contains shell commands that define the job's execution workflow. 
These commands are arbitrary, but we strongly recommend the general structure shown above, which includes:

1.  **(*Optional*) Explicitly setting the `TMPDIR` variable.**

    Many programs write temporary data to `TMPDIR`, which is usually small (e.g., 30–40 GB) and shared among all users. Specifying your own directory for temporary
    files helps avoid the risk of your own or other users' programs failing when space runs out.

2.  **Loading and reporting the specific module environment required for this job.**

    While not strictly necessary, we recommend this as best practice, since it makes debugging and later reproduction easier. (Manually specifying module versions lets you recreate the same execution environment in the future.)

3.  **Defining any environment variables specific to the chosen module environment.**

    Users occasionally need to define specific runtime environment variables, e.g., for an MPI implementation or library chosen via the `module load` commands.

4.  **Remaining job-specific steps.**

    In the example above, we first compile and then execute `hello_c.c`, a simple MPI program running a total of 32 processes across 2 nodes.
    `btl_tcp_port_min_v4` and `btl_tcp_port_range_v4` are OpenMPI-specific parameters that set the TCP port range used by the MPI application. 

---

## Common `#PBS` directives

### **Resource requests**
Resources (compute node configuration, job duration) are requested through a combination of *resource selection* flags, each preceded by `-l`.

For example:
```pre
#PBS -l walltime=00:05:00
#PBS -l select=1:ncpus=64:mpiprocs=4:ngpus=4:mem=256GB
```
specifies job `walltime` and compute node (chunk) selection. See more details below.


#### **`select` statements**
Resources are specified through a `select` statement. The general form of a *homogeneous* selection statement is
```pre
select=<# NODES>:ncpus=<# CPU Cores/node>:mem=<RAM/node>:mpiprocs=<# MPI Ranks/node>:ompthreads=<# OpenMP Threads/rank>:ngpus=<# GPUs/node>
```
where *node* and *chunk* can be used interchangeably:

**`<# NODES>`** 
> the total number of compute nodes requested, followed by a colon-separated list (see below)

**`<# CPU Cores/node>`** 
> the *total* number of CPUs requested *on each node*, which can be a mix of MPI ranks and/or OpenMP threads

**`<RAM/node>`** 
> how much main memory (RAM) the job can access *on each node*. 
> (Optional; the default is system-dependent, but the system default is a very small amount, 256MB, so as best practice we recommend explicitly specifying the memory size required.)
  
**`<# MPI Ranks/node>`** 
> the number of MPI ranks *on each node* (optional, defaults to 1)

**`<# OpenMP Threads/node>`** 
> the number of OpenMP threads *per MPI rank on each node* (optional, defaults to 1)

**`<# GPUs/node>`** 
> the number of GPUs *per node* (optional, defaults to 0)

Together, these specify a *resource chunk*. Homogeneous resource chunks are the most common case, but 
*heterogeneous* selection statements can be built from multiple chunks separated by a **+** (examples below).

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
Within the **script contents**, a job's specifics often depend slightly on the PBS and `module` execution environment.
Both running under PBS and loading certain [module files](../service/modules.md) create environment variables useful when writing
portable scripts—for example, scripts shared among users or run across several different configurations.

### PBS execution environment variables
PBS creates several environment variables accessible within a job's execution environment.
Some of the more useful ones:

|  <div style="width:110px">Variable</div> | Value |
|---------------|-------|
| `PBS_JOBID`     | The PBS Job ID for this job.<br>Example: `1473351.tem-ce-al9` |
| `PBS_JOBNAME`   | The name of this job. Matches the `-N` specified.<br>Example: `hello_pbs` |
| `PBS_O_WORKDIR` | The working directory from where the job was submitted. |
| `PBS_SELECT`    | The resource specification `-l select=` line for this job.<br>This can be useful for setting runtime-specific configuration options that might depend on resource selection.<br>(e.g. processor layout, CPU binding, etc...)<br>Example: `2:ncpus=128:mpiprocs=2:ompthreads=2:mem=200GB:ngpus=1`  |
| `PBS_NODEFILE`  | A file whose contents lists the nodes assigned to this job.<br> Typically listed as one node name per line, for each MPI rank in the job.<br>Each node will be listed for as many times as it has MPI ranks. <br>Example: `/var/spool/pbs/aux/1473351.tem-ce-al9` |
<!-- | `PBS_QUEUE`     | The name of the PBS execution queue.<br>In general this will be an *execution* queue, and different than the *routing* queue specified by `-q` in the job script.<br>Example: `cpu` | -->