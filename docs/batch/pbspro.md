# Starting and managing jobs with PBS

Batch processing is a method of running software programs called jobs in batches automatically. 
While users are required to submit the jobs, no other interaction by the user is required to process the batch.
Batches may automatically be run at scheduled times as well as being run on the available computer resources.
For additional background, see [Batch Computing Overview](https://en.wikipedia.org/wiki/Batch_processing). 
GSDC TEM computing cluster uses the Portable Batch System as implemented in Altair's PBS Pro across shared resources.

**URL**
> [PBS Pro (Community Edition)](https://github.com/openpbs/openpbs)

> [PBS Pro (Commercial)](https://altair.com/pbs-professional)

---

## **Job scripts**
[Job scripts](./jobscripts.md) form the basis of batch jobs. A job script is simply a text file with instructions of the work to
execute. Job scripts are usually written in `bash` and thus mimic commands a user would execute interactively through a shell,
but instead are executed on specific resources allocated by the scheduler when available.
Scripts can also be written in other languages - commonly Python.
See our [job scripts](./jobscripts.md) page for a detailed discussion of job scripts and examples.

## **Submitting jobs**

In the examples that follow, `job.pbs`, `script_name` etc. represent a job script files submitted for batch execution.
[PBS Pro](https://github.com/openpbs/openpbs) can be used to schedule both interactive jobs and batch compute jobs.

To submit a batch job, use the `qsub` command followed by the name of your PBS batch script file.

```bash
qsub job.pbs
```

## **Propagating environment settings**

Some users find it useful to set environment variables in their login environment that can be temporarily used for multiple batch jobs without modifying the job script.
This practice can be particularly useful during iterative development and debugging work.

PBSPro has two approaches to propagation:

1. Specific variables can be forwarded to the job upon request.
2. The entire environment can be forwarded to the job.

In general, the first approach is preferred because the second may have unintended consequences.

These settings are controlled by qsub arguments that can be used at the command line or as directives within job scripts. Here are examples of both approaches:

```bash
# Selectively forward runtime variables to the job (lower-case v)
qsub -v DEBUG=true,CASE_NAME job.pbs
```

When you use the selective option (lower-case `v`), you can either specify only the variable name to propagate the current value (as in `CASE_NAME` in the example), 
or you can explicitly set it to a given value at submission time (as in `DEBUG`).

```bash
# Forward the entire environment to the job (upper-case V)
qsub -V job.pbs
```

## **Managing jobs**

Here are some of the most useful commands for managing and monitoring jobs that have been launched with PBS. Most of these commands will only modify or query data from jobs that are active on the same system.

### **`qdel`**

Run `qdel` with the job ID to kill a pending or running job.

```bash
qdel jobID
```

Kill all of your own pending or running jobs. (Be sure to use backticks as shown.)

```bash
qdel `qselect -u $USER`
```

### **`qstat`**

Run this to see the status of all of your own unfinished jobs.

```bash
qstat -u $USER
```

Your output will be similar to what is shown just below. Most column headings are self-explanatory – `NDS` for nodes, `TSK` for tasks, and so on.

In the status `(S)` column, most jobs are either queued `(Q)` or running `(R)`. Sometimes jobs are held `(H)`, which might mean 
they are dependent on the completion of another job.

```pre
tem-ce-al9.sdfarm.kr:
                                                            Req'd  Req'd   Elap
Job ID          Username Queue    Jobname    SessID NDS TSK Memory Time  S Time
--------------- -------- -------- ---------- ------ --- --- ------ ----- - -----
838.tem-ce-al9* tem      cpuQ     cryosparc*  95965   1   1  8000m   --  R 00:01
840.tem-ce-al9* tem      gpuQ     cryosparc*  84478   1   6   16gb   --  R 00:00
841.tem-ce-al9* tem      gpuQ     cryosparc*  84594   1   6   16gb   --  R 00:00
```

Following are examples of `qstat` with some other commonly used options and arguments.

Get a long-form summary of the status of an unfinished job.

```bash
qstat -f jobID
```
!!! warning
    Use the above command only sparingly; it places a high load on PBSPro.

Get a single-line summary of the status of an unfinished or recently completed job (within 72 hours).

```bash
qstat -x jobID
```

Get information about unfinished jobs in a specified execution queue.

```bash
qstat queue_name
```
See job activity by queue (e.g., pending, running) in terms of numbers of jobs.

```bash
qstat -Q
```

Display information for all of your pending, running, and finished jobs.

```bash
qstat -x -u $USER
```

Display information for all of your unfinished jobs with `exec_host` and any `scheduler_comment` below the basic information.

```bash
qstat -n -s -u $USER
```

Display information for all the jobs (including other users jobs)

```bash
qstat -a
```

## **Interactive jobs**

Interactive jobs provide an interactive session on a compute node, useful for debugging, testing code, and running short tasks that require user interaction.

Users can start an interactive job on GSDC TEM login nodes using the `qsub -I` command. 
The `-I` flag is used to request an interactive session. The following example shows how to start an interactive job with specified resources on `cpuQ`:

```bash
qsub -I -q cpuQ -l select=1:ncpus=4:mem=32GB -l walltime=01:00:00
```

The result for the above command is following:

```bash
qsub: waiting for job 850.tem-ce-al9.sdfarm.kr to start
qsub: job 850.tem-ce-al9.sdfarm.kr ready

[tem@tem-cpu00-al9 ~]$ Do something

...

[tem@tem-cpu00-al9 ~]$ exit
logout
qsub: job 850.tem-ce-al9.sdfarm.kr completed
```
