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

### **qdel**

### **qstat**

## **Interactive jobs**

