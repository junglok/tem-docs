# PBS Batch Queues

## **Batch Queue Definition**

The GSDC TEM computing cluster offers multiple batch queues with different characteristics for users submitting jobs to analyze large-scale Cryo-EM data. 
A batch queue is a logical set of CPU and GPU computing resources. Users interact with a specific queue to manage their own jobs. 

Within each queue, submitted jobs run on a first-come-first-served basis, though backfilling (smallest and best-fit) may apply depending on resource availability.
Multiple jobs requiring CPU and/or GPU resources can run concurrently if enough resources are available in the queue.

## **Batch Queues**

---

### **cpuQ**

???+ tip "More detailed information about cpuQ"

    **Category(shared or dedicated)** : Shared

    **QueueName** : cpuQ

    **Assigned Computing Resources**
    > * tem-cpu[00-13]-al9.sdfarm.kr : Intel® Xeon® CPU E5-2697v3@2.60GHz 28 Cores, 192GB Main Memory
    
    **Remarks** : Total 380 CPU Cores

---

### **gpuQ**

???+ tip "More detailed information about qpuQ"

    **Category(shared or dedicated)** : Shared

    **QueueName** : gpuQ
    
    **Assigned Computing Resources**
    > * tem-gpu[01-02]-al9.sdfarm.kr : Intel® Xeon® Gold 6226R CPU@2.90GHz 32 Cores, 384GB Memory, NVIDIA A100 40GB * 2EA (Logically A100 20GB * 4EA using MIG)
    > * tem-gpu[05-05]-al9.sdfarm.kr : Intel® Xeon® Gold 6334R CPU@3.60GHz 32 Cores, 384GB Memory, NVIDIA V100 32GB * 4EA
    > * tem-gpu[06-08]-al9.sdfarm.kr : Intel® Xeon® CPU E5-2690v4@2.60GHz 28 Cores, 384GB Memory, NVIDIA P100 16GB * 2EA
    > * tem-gpu[09-10]-al9.sdfarm.kr : Intel® Xeon® CPU E5-2690v4@2.60GHz 28 Cores, 256GB Memory, NVIDIA P40 24GB * 2EA
    > * tem-gpu[11-12]-al9.sdfarm.kr : Intel® Xeon® Gold 6334R CPU@3.60GHz 32 Cores, 384GB Memory, NVIDIA A100 80GB * 4EA  (Logically A100 40GB * 8EA using MIG)
    
    
    **Remarks** : Total 300 CPU cores, 26 NVIDIA GPUs (MIG GPU Instances : 38 GPUs Total)

---