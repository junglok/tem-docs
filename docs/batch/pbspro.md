# Starting and managing jobs with PBS

Batch processing runs programs, called jobs, automatically in batches.
Users submit the jobs; no further interaction is needed to process them.
Batches can run at scheduled times or whenever computer resources become available.
For more background, see [Batch Computing Overview](https://en.wikipedia.org/wiki/Batch_processing). 
The GSDC TEM computing cluster uses the Portable Batch System, as implemented in Altair's PBS Pro, across its shared resources.

**URL**
> [PBS Pro (Community Edition)](https://github.com/openpbs/openpbs)

> [PBS Pro (Commercial)](https://altair.com/pbs-professional)

---

## **Job scripts**
[Job scripts](./jobscripts.md) form the basis of batch jobs. A job script is simply a text file containing instructions for the work to
execute. Job scripts are usually written in `bash`, mimicking commands a user would run interactively through a shell,
but they execute on specific resources allocated by the scheduler when available.
Scripts can also be written in other languages, commonly Python.
See our [job scripts](./jobscripts.md) page for a detailed discussion and examples.

## **Submitting jobs**

In the examples below, `job.pbs`, `script_name`, etc., represent job script files submitted for batch execution.
[PBS Pro](https://github.com/openpbs/openpbs) can schedule both interactive jobs and batch compute jobs.

To submit a batch job, use the `qsub` command followed by the name of your PBS batch script file.

```bash
$> qsub job.pbs
```

## **Propagating environment settings**

Some users find it useful to set environment variables in their login environment that can be reused across multiple batch jobs without modifying the job script.
This is especially handy during iterative development and debugging.

PBSPro supports two approaches to propagation:

1. Forward specific variables to the job on request.
2. Forward the entire environment to the job.

The first approach is generally preferred, since the second can have unintended consequences.

These settings are controlled by qsub arguments, usable either at the command line or as directives within job scripts. Here are examples of both:

```bash
# Selectively forward runtime variables to the job (lower-case v)
$> qsub -v DEBUG=true,CASE_NAME job.pbs
```

With the selective option (lower-case `v`), you can either specify just the variable name to propagate its current value (as with `CASE_NAME` above), 
or explicitly set a value at submission time (as with `DEBUG`).

```bash
# Forward the entire environment to the job (upper-case V)
$> qsub -V job.pbs
```

## **Managing jobs**

Here are the most useful commands for managing and monitoring jobs launched with PBS. Most of them only modify or query data for jobs active on the same system.

### **qdel**

#### **Canceling a single job**
Run `qdel` with the job ID to cancel a pending or running job.

```bash
$> qdel jobID
```

#### **Stopping all of your own jobs**
Cancel all of your own pending or running jobs. (Be sure to use backticks as shown.)

```bash
$> qdel `qselect -u $USER`
```

### **qstat**

#### **Status of all your own jobs**
Run this to see the status of all of your own unfinished jobs.

```bash
$> qstat -u $USER
```

Your output will look similar to what's shown below. Most column headings are self-explanatory – `NDS` for nodes, `TSK` for tasks, and so on.

In the status `(S)` column, most jobs are either queued `(Q)` or running `(R)`. Jobs are sometimes held `(H)`, which usually means 
they depend on another job finishing first.

```pre
tem-ce-al9.sdfarm.kr:
                                                            Req'd  Req'd   Elap
Job ID          Username Queue    Jobname    SessID NDS TSK Memory Time  S Time
--------------- -------- -------- ---------- ------ --- --- ------ ----- - -----
838.tem-ce-al9* USERID   cpuQ     cryosparc*  95965   1   1  8000m   --  R 00:01
840.tem-ce-al9* USERID   gpuQ     cryosparc*  84478   1   6   16gb   --  R 00:00
841.tem-ce-al9* USERID   gpuQ     cryosparc*  84594   1   6   16gb   --  R 00:00
```

Below are examples of `qstat` with other commonly used options and arguments.

#### **Status of an unfinished job**

Get a detailed summary of an unfinished job's status.

```bash
$> qstat -f jobID
```
!!! warning
    Use this command sparingly; it places a heavy load on PBSPro.

#### **Status of jobs within some periods**
Get a one-line summary of an unfinished or recently completed job's status (within 72 hours).

```bash
$> qstat -x jobID
```

#### **Status of jobs on a specified queue**
Get information about unfinished jobs in a specified execution queue.

```bash
$> qstat queue_name
```

#### **Status of jobs by queue**
See job activity by queue (e.g., pending, running) as a count of jobs.

```bash
$> qstat -Q
```

#### **Status of all of your jobs**
Display information for all of your pending, running, and finished jobs.

```bash
$> qstat -x -u $USER
```

#### **Status of all your own jobs with comments**
Show information for all your unfinished jobs, with `exec_host` and any `scheduler_comment` listed below the basic information.

```bash
$> qstat -n -s -u $USER
```

#### **Status of all jobs**
Show information for all jobs, including other users' jobs.

```bash
$> qstat -a
```

## **Interactive jobs**

Interactive jobs give you an interactive session on a compute node, useful for debugging, testing code, and running short tasks that need user interaction.

Start an interactive job on GSDC TEM login nodes with the `qsub -I` command. 
The `-I` flag requests an interactive session. The example below starts an interactive job with specified resources on `cpuQ`:

```bash
$> qsub -I -q cpuQ -l select=1:ncpus=4:mem=32GB -l walltime=01:00:00
```

The result of the above command is as follows:

```bash
qsub: waiting for job 850.tem-ce-al9.sdfarm.kr to start
qsub: job 850.tem-ce-al9.sdfarm.kr ready

[USERID@tem-cpu00-al9 ~]$ Do something

...

[USERID@tem-cpu00-al9 ~]$ exit
logout
qsub: job 850.tem-ce-al9.sdfarm.kr completed
```

## **Interactive jobs with GUI(X11)-based applications**

You can also start an interactive job supporting GUI (X11)-based applications with the `qsub -X -V -I` command.

The example below starts an interactive job with specified resources on `cpuQ`, with environment variables and X11-forwarding set:

```bash
$> qsub -X -V -I -q cpuQ -l select=1:ncpus=1:mem=16GB -l walltime=01:00:00
```

The result of the above command is as follows:

```bash
qsub: waiting for job 900.tem-ce-al9.sdfarm.kr to start
qsub: job 900.tem-ce-al9.sdfarm.kr ready

[USERID@tem-cpu00-al9 ~]$ echo $DISPLAY
localhost:50.0
...
[USERID@tem-cpu00-al9 ~]$ xclock
[USERID@tem-cpu00-al9 ~]$ exit
logout
qsub: job 900.tem-ce-al9.sdfarm.kr completed
```