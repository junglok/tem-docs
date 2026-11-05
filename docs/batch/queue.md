# PBS Batch Queues

## **Batch Queue Definition**

The GSDC TEM computing cluster offers multiple batch queues with different characteristics for users submitting jobs to analyze large-scale Cryo-EM data. 
A batch queue is a logical set of CPU and GPU computing resources. Users interact with a specific queue to manage their own jobs. 

Within each queue, submitted jobs run on a first-come-first-served basis, though backfilling (smallest and best-fit) may apply depending on resource availability.
Multiple jobs requiring CPU and/or GPU resources can run concurrently if enough resources are available in the queue.

The cores, memory and GPUs listed below are the most a single chunk (`-l select=...`) can request on each node.
A chunk asking for more than any node in the queue provides (e.g., `ncpus=64` or `mem=384GB`) is never placed and stays queued.

## **Batch Queues**

---

### **cpuQ**

???+ tip "More detailed information about cpuQ"

    **Category(shared or dedicated)** : Shared

    **QueueName** : cpuQ

    **Assigned Computing Resources**
    > * tem-cpu[00-11]-al9 : Intel® Xeon® CPU E5-2697v3@2.60GHz, 28 cores schedulable (`ncpus=`), up to 187GB memory per node (`mem=`)
    
    **Remarks** : Total 336 CPU Cores (12 nodes)

---

### **gpuQ**

???+ tip "More detailed information about gpuQ"

    **Category(shared or dedicated)** : Shared

    **QueueName** : gpuQ
    
    **Assigned Computing Resources**
    > * tem-gpu[01-02]-al9 : Intel® Xeon® Gold 6226R CPU@2.90GHz, 32 cores schedulable (`ncpus=`), up to 376GB memory per node (`mem=`), NVIDIA A100 40GB * 2EA
    > * tem-gpu05-al9 : Intel® Xeon® Gold 6334 CPU@3.60GHz, 32 cores schedulable (`ncpus=`), up to 375GB memory per node (`mem=`), NVIDIA V100 32GB * 4EA
    > * tem-gpu[06-08]-al9 : Intel® Xeon® CPU E5-2690v4@2.60GHz, 28 cores schedulable (`ncpus=`), up to 376GB memory per node (`mem=`), NVIDIA P100 16GB * 2EA
    > * tem-gpu09-al9 : Intel® Xeon® Gold 6126 CPU, 28 cores schedulable (`ncpus=`), up to 250GB memory per node (`mem=`), NVIDIA P40 24GB * 2EA
    > * tem-gpu10-al9 : Intel® Xeon® Gold 6150 CPU, 28 cores schedulable (`ncpus=`), up to 250GB memory per node (`mem=`), NVIDIA P40 24GB * 2EA
    > * tem-gpu[11-12]-al9 : Intel® Xeon® Gold 6334 CPU@3.60GHz, 32 cores schedulable (`ncpus=`), up to 375GB memory per node (`mem=`), NVIDIA A100 80GB * 4EA
    
    
    **Remarks** : Total 300 CPU cores, 26 NVIDIA GPUs (10 nodes). MIG is disabled on all A100 GPUs, so each physical card counts as one GPU (`ngpus=1`).

---