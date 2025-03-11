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

## **Propagating environment settings**

## **Managing jobs**

### **qdel**

### **qstat**

## **Interactive jobs**

