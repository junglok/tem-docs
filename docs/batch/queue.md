# PBS Batch Queues

## **Batch Queue Definition**

GSDC TEM computing cluster provides multiple batch queues with different characteristics to users who submit jobs to analyze large-scale Cryo-EM data. 
A batch queue means a logical set of CPU and GPU computing resources. Users interact with a specific queue to manange their own jobs. 

Within each queue, submitted jobs are executed in order (First-in-first-out basis, but sometimes backfilling way as whether the required resources are available or not).
Note that multiple jobs requiring CPU and/or GPU resources can be executed concurrently if there are enough available resources in the queue.