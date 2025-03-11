# PBS (Portable Batch System) Professional Job Scripts

**Job scripts** form the basis of batch jobs. A job script is simply a text file with instructions of the work to execute.
Job scripts are *usually* written in `bash` and thus mimic commands a user would execute interactively through a shell; but instead are executed on 
specific resources allocated by the scheduler when available. Scripts can also be written in other languages - commonly *Python*.

## Basics of a Job Script
Sample basic PBS scripts are shown below:

!!! example "PBS Job Scripts"
    === "bash"
        ```bash
        #!/bin/bash
        #PBS -N hello_pbs
        #PBS -j oe
        #PBS -k eod
        #PBS -q cpuQ
        #PBS -l walltime=00:05:00
        #PBS -l select=2:ncpus=16:mpiprocs=16

        ### Set temp to scratch (note that <GroupDir> should be replaced with proper name)
        setenv TMPDIR /tem/scratch/<GroupDir>/temp && mkdir -p ${TMPDIR}

        ### Specify desired module environment to be loaded
        module purge
        module load openmpi/5.0.3/gcc-11.5.0
        module list

        ### Compile and Run MPI Program
        mpicc -o hello_c /tem/el9/samples/hello_c.c -fopenmp
        mpirun -n 32 --machinefile $PBS_NODEFILE ./hello_c
        ```

        ---

        The first line denotes the interpreter to be used for the script:
        ```bash
        #!/bin/bash
        ```
    === "Python"
        ```python
        #!/usr/bin/python
        #PBS -N hello_pbs
        #PBS -j oe
        #PBS -k eod
        #PBS -q main
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
        #!/glade/u/apps/opt/conda/envs/npl/bin/python
        ```
        indicates this is a `python` script

**Focusing on the `bash` example for discussion**, the remainder of the script contains two main sections:

1.  The lines beginning with `#PBS` are **directives** that will be interpreted by PBS when this script is submitted with `qsub`.
    Each of these lines contains an instruction that will be used by `qsub` to control job resources, execution, etc...

2.  The remaining **script contents** are simply `bash` commands that will be run inside the batch environment on the selected resources and define the work to be done in this job.


### PBS directives

The example above contains several **directives** which are interpreted by the `qsub` submission program:

* `-N hello_pbs` provides a *job name*.  This name will be displayed by the scheduler for diagnostic and file output.  If omitted, and a script is used to submit the job, the job's name is the name of the script.
* `-j oe` requests we *combine any standard text output (`o`) and error (`e`) into one output file*.
  (By default, PBS will write program output and error to different log files. This behavior is contrary to what many users expect from terminal interaction, where output and error are generally interspersed. This optional flag changes that behavior.)
* `-q cpuQ` specifies the desired PBS *queue* for this job.
* `-l walltime=00:05:00` requests 5 minutes as the maximum job execution (*walltime*) time.  Specified in `HH:MM:SS` format.
* `-l select=2:ncpus=16:mpiprocs=16` is a computational *resource chunk* request, detailing the quantity and configuration of *compute nodes* required for this job. This example requests a *selection* of 2 nodes, where each node must have 16 CPU cores, each of which we will use as an MPI rank in our application.


### Script contents

The remaining script contains shell commands that define the job execution workflow. 
The commands here are arbitrary, however we strongly recommend the general structure presented above.  This includes:

1.  **Explicitly setting the `TMPDIR` variable**.

    As described here, many programs write temporary data to `TMPDIR`, which is usually small and
    shared among st users.  Specifying your own directory for temporary
    files can help you avoid the risk of your own programs and other
    users' programs failing when no more space is available.

2.  **Loading and reporting the specific module environment required for this job.**

    While strictly not necessary, we recommend this as best practice as it facilitates debugging and reproducing later. (Manually specifying module versions allows you to recreate the same execution environment in the future.)

3.  **(*Optional*) Defining any environment variables specific to the chosen module environment.**

    Occasionally users will want to define particular run time environment variables e.g. for a specific MPI or library chosen via the `module load` commands.

4.  **Remaining job-specific steps.**

    In the example above, we first compile and then execute `hello_c.c`, a simple MPI program with having total 32 processes on 2 nodes.

---
