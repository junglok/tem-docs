***************
TEM farm basics
***************

Accessing TEM service farm
==========================
Before you use GSDC's service farm, you should send an application form to TEM service manager and get an user account to access the farm (please see the contact information for the application form). If you already have valid user accounts, you can log into UI (user interface) nodes to access/use various kind of cluster resources and software environments (including data analysis tools, e.g., relion, cisTEM, eman, etc.).

For Linux/Mac users
-------------------

.. code-block:: bash

  $> ssh -Y -o Port=<port> <userID>@tem-ui.sdfarm.kr

-Y (or -X) options : enable trusted X11 (or untrusted X11) forwarding

For Windows users
-----------------

  * Using MobaXterm (https://mobaxterm.mobatek.net) :
    MobaXterm is an enhanced terminal for Windows with self-contained X11 server, tabbed SSH client, network tools and much more.

.. image:: images/mobaxterm_resized.JPG
    :scale: 70 %
    :align: center

..

  * Using Putty with Xwindows manager (e.g., Xming, Xmanager, etc.) (https://www.putty.org) :
    If you use putty terminal application, you must install a 3rd-party Xwindows manager in advance.

.. image:: images/putty-1_resized.JPG
    :scale: 70 %
    :align: center

.. image:: images/putty-2_resized.JPG
    :scale: 70 %
    :align: center



Understanding environment modules
=================================
The Environment Modules system is a tool to help users manage their Unix or Linux shell environment, by allowing groups of related environment-variable settings to be made or removed dynamically.

* **Listing available modules**

.. code-block:: bash

  $> module avail
  ----------- /tem/home/tem/Modules/Modules/default/modulefiles ------------
  apps/gcc/4.4.7/cistem/1.0.0     cuda/9.2
  apps/gcc/4.4.7/relion/cpu/3.0.7 modules
  apps/gcc/4.4.7/relion/gpu/3.0.7 mpi/gcc/openmpi/1.8.8

* **Show module details**

.. code-block:: bash

  $> module show apps/gcc/4.4.7/relion/gpu/3.0.7
  -------------------------------------------------------------------
  /tem/home/tem/Modules/Modules/default/modulefiles/apps/gcc/4.4.7/relion/gpu/3.0.7:

  module-whatis    Setups `relion-3.0.7' environment variables
  module           load mpi/gcc/openmpi/1.8.8
  module           load cuda/9.2
  setenv           relion_version 3.0.7
  prepend-path     PATH /tem/home/tem/_Applications/relion-3.0.7/gpu/bin
  prepend-path     LD_LIBRARY_PATH /tem/home/tem/_Applications/relion-3.0.7/gpu/lib
  setenv           LANG en_US.UTF-8
  setenv           RELION_QUEUE_NAME tem
  setenv           RELION_QSUB_COMMAND qsub
  setenv           RELION_QSUB_TEMPLATE /tem/home/tem/_Applications/relion-3.0.7/gpu/bin/qsub-relion3-gpu.bash
  setenv           RELION_QSUB_EXTRA_COUNT 3
  setenv           RELION_QSUB_EXTRA1 Number of Nodes
  setenv           RELION_QSUB_EXTRA2 Number of processes per each node
  setenv           RELION_QSUB_EXTRA3 Number of GPUs per node
  setenv           RELION_QSUB_EXTRA1_DEFAULT 1
  setenv           RELION_QSUB_EXTRA2_DEFAULT 3
  setenv           RELION_QSUB_EXTRA3_DEFAULT 2
  setenv           RELION_CTFFIND_EXECUTABLE /tem/home/tem/_Applications/ctffind-4.1.13/bin/ctffind
  setenv           RELION_GCTF_EXECUTABLE /tem/home/tem/_Applications/Gctf_v1.18_b2/bin/Gctf_v1.18_b2_sm60_cu9.2
  setenv           RELION_RESMAP_EXECUTABLE /tem/home/tem/_Applications/ResMap-1.1.4/ResMap-1.1.4-linux64
  setenv           RELION_MOTIONCORR_EXECUTABLE /tem/home/tem/_Applications/MotionCor2/MotionCor2_1.2.6-Cuda92
  setenv           RELION_UNBLUR_EXECUTABLE /tem/home/tem/_Applications/unblur_1.0.2/bin/unblur_openmp_7_17_15.exe
  setenv           RELION_SUMMOVIE_EXECUTABLE /tem/home/tem/_Applications/summovie_1.0.2/bin/sum_movie_openmp_7_17_15.exe
  conflict         apps/gcc/4.4.7/relion
  -------------------------------------------------------------------

* **Loading modules**

.. code-block:: bash

  $> module load <module_path>
  or
  $> module add <module_path>
  e.g., $> module load apps/gcc/4.4.7/relion/gpu/3.0.7


* **Listing loaded modules**

.. code-block:: bash

  $> module load apps/gcc/4.4.7/relion/gpu/3.0.7
  $> module list
  Currently Loaded Modulefiles:
  1) cuda/9.2                          2) mpi/gcc/openmpi/1.8.8             3) apps/gcc/4.4.7/relion/gpu/3.0.7


* **Unloading modules**

.. code-block:: bash

  $> module unload <module_path>
  or
  $> module rm <module_path>
  e.g., $> module unload apps/gcc/4.4.7/relion/gpu/3.0.7


* **Unloading all the modules**

.. code-block:: bash

  $> module purge


* **Module environment help**

.. code-block:: bash

  $> module --help
    Modules Release 3.2.10 2012-12-21 (Copyright GNU GPL v2 1991):

    Usage: module [ switches ] [ subcommand ] [subcommand-args ]

    Switches:
        -H|--help               this usage info
        -V|--version            modules version & configuration options
        -f|--force              force active dependency resolution
        -t|--terse              terse    format avail and list format
        -l|--long               long     format avail and list format
        -h|--human              readable format avail and list format
        -v|--verbose            enable  verbose messages
        -s|--silent             disable verbose messages
        -c|--create             create caches for avail and apropos
        -i|--icase              case insensitive
        -u|--userlvl <lvl>      set user level to (nov[ice],exp[ert],adv[anced])
    Available SubCommands and Args:
        + add|load              modulefile [modulefile ...]
        + rm|unload             modulefile [modulefile ...]
        + switch|swap           [modulefile1] modulefile2
        + display|show          modulefile [modulefile ...]
        + avail                 [modulefile [modulefile ...]]
        + use [-a|--append]     dir [dir ...]
        + unuse                 dir [dir ...]
        + update
        + refresh
        + purge
        + list
        + clear
        + help                  [modulefile [modulefile ...]]
        + whatis                [modulefile [modulefile ...]]
        + apropos|keyword       string
        + initadd               modulefile [modulefile ...]
        + initprepend           modulefile [modulefile ...]
        + initrm                modulefile [modulefile ...]
        + initswitch            modulefile1 modulefile2
        + initlist
        + initclear



Job manager (Torque)
====================

Resources manager and job scheduler
-----------------------------------

* Resource manager : Torque(OpenPBS) v6.1.2
* Job scheduler : Torque default FIFO job scheduler


Directives in Torque job scripts
--------------------------------

Torque defines some useful directives (starting with \'#PBS\') which can be used to describe job's resources requirements. Users must include those directives in job scripts to submit and execute jobs.
The order of directives is not important, but the directives must be written prior to job execution commands.

**Resource limits**
~~~~~~~~~~~~~~~~~~~

The "-l" option is used to request resources, including nodes, memory, time, etc.


* Nodes and PPN (Processor Per Node)

.. code-block:: bash

  To request a single core on the farm:
  #PBS -l nodes=1:ppn=1

  To request one whole node on the farm:
  #PBS -l nodes=1:ppn=28

  To request 4 whole nodes on the farm:
  #PBS -l nodes=4:ppn=28

  To request 3 whole nodes with 2 GPUs on the farm:
  #PBS -l nodes=3:ppn=28:gpus=2

  To request 1 node with use of 6 cores and 1 GPU:
  #PBS -l nodes=1:ppn=6:gpus=1



* Wall clock time

.. code-block:: bash

  To request 20 hours of wall clock time:
  #PBS -l walltime=20:00:00

If a computational job will have not finished yet until the specified wall clock time, Torque (or maui scheduler) will release the resources that are allocated to the job and stop the job's runnning.
If you don't define walltime, the default value is "infinite".

* Memory

.. code-block:: bash

  To request 4GB memory:
  #PBS -l mem=4GB
  or
  #PBS -l mem=4000MB

  To request 24GB memory:
  #PBS -l mem=24000MB

..

**Job name**
~~~~~~~~~~~~

You can define a job name using "-N" option. If you omit this directive, the default job name is the same as the file name of job script.

.. code-block:: bash

  #PBS -N my_first_job


**Queue name**
~~~~~~~~~~~~~~

In general, a "queue" can be thought of a mapped set of computing resources. You can specify a queue name (using "-q" option) which the job is enqueued to. 

.. code-block:: bash

  #PBS -q tem


**Job log files**
~~~~~~~~~~~~~~~~~
When Torque executes an user's job, Torque creates 2 different types of log files (standard output stream and standart error stream) by default. If the job's name is "my_first_job" and the submitted job ID is "123456", you can find 2 files (my_first_job.o123456 and my_first_job.e123456) that are created in the job execution base directory. You can also merge the two streams into one file using "-j oe" option. In that case, my_first_job.o1234567 file contains the standard error stream.

.. code-block:: bash

  #PBS -j oe


Torque job script examples
--------------------------

**Simple sequential job**
~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: bash

  #PBS -N my_job
  #PBS -l walltime=40:00:00
  #PBS -l nodes=1:ppn=1
  #PBS -q tem

  cd $PBS_O_WORKDIR
  /usr/bin/time ./mysci > mysci.hist


**Serial job with OpenMP multithreading**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: bash

  #PBS -N my_job
  #PBS -l walltime=1:00:00
  #PBS -l nodes=1:ppn=28
  #PBS -q tem

  export OMP_NUM_THREADS=28
  cd $PBS_O_WORKDIR
  ./a.out > my_results


**Simple MPI parallel job**
~~~~~~~~~~~~~~~~~~~~~~~

Here is an example of an MPI job that uses 4 nodes with 4 cores each, running one process per core (16 processes total).

.. code-block:: bash

  #PBS -N my_job
  #PBS -l walltime=10:00:00
  #PBS -l nodes=4:ppn=4
  #PBS -q tem

  module load mpi/gcc/openmpi/1.8.8
  cd $PBS_O_WORKDIR
  mpirun -machinefile $PBS_NODEFILE ./a.out


**Parallel job with MPI and OpenMP**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This example is a hybrid MPI/OpenMP job. It runs one MPI process per node with 28 threads per process. The assumption here is that the code was written to support multi-level parallelism. 

.. code-block:: bash

  #PBS -N my_job
  #PBS -l walltime=20:00:00
  #PBS -l nodes=4:ppn=28
  #PBS -q tem

  module load mpi/gcc/openmpi/1.8.8
  export OMP_NUM_THREADS=28
  cd $PBS_O_WORKDIR
  mpirun --bynode -machinefile $PBS_NODEFILE ./a.out


Job submission
--------------

myscript.job : the script file name of a PBS batch job

.. code-block:: bash

  $> qsub myscript.job

In response to this command you’ll see a line with your job ID:

.. code-block:: bash

  123456.tem-ce.sdfarm.kr


Monitoring and managing your jobs
---------------------------------

**Status of queued jobs**
~~~~~~~~~~~~~~~~~~~~~~~~~

* qstat

Use the qstat command to check the status of your jobs. You can see whether your job is queued or running, along with information about requested resources. If the job is running you can see elapsed time and resources used.

.. code-block:: bash

  ### By itself, qstat lists all jobs in the system:
  $> qstat

  ### To list all the jobs belonging to a particular user:
  $> qstat -u tem_user

  ### To list the status of a particular job, in standard or alternate format:
  $> qstat 123456
  $> qstat -a 123456

  ### To get all the details about a particular job (full status):
  $> qstat -f 123456

..

**Managing your jobs**
~~~~~~~~~~~~~~~~~~~~~~

* Deleting (canceling) a job

Situations may arise in which you want to delete one of your jobs from the PBS queue. Perhaps you set the resource limits incorrectly, neglected to copy an input file, or had incorrect or missing commands in the batch file. Or maybe the program is taking too long to run (infinite loop). The PBS command to delete a batch job is qdel. It applies to both queued and running jobs.

.. code-block:: bash

  $> qdel 123456
..

* Altering a queued job

You can alter certain attributes of your job while it’s in the queue using the qalter command. This can be useful if you want to make a change without losing your place in the queue. You cannot make any alterations to the executable portion of the script, nor can you make any changes after the job starts running.
The options argument consists of one or more PBS directives in the form of command-line options. For example, to change the walltime limit on job 123456 to 5 hours and have email sent when the job ends (only):

.. code-block:: bash

  ### The syntax is: qalter [options ...] jobid
  $> qalter -l walltime=5:00:00 -m e 123456
