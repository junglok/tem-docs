************
Batch Queues
************

Batch queue list
================

TEM farm provides multiple batch queues with different characteristics to users who submit jobs to analyze large-scale Cryo-EM data. 
A batch queue means a logical set of CPU and GPU computing resources.
Users interact with a specific queue to manange their own jobs. 
Within each queue, submitted jobs are executed in order (First-in-first-out).
Note that multiple jobs requiring CPU and/or GPU resources can be executed concurrently if there are enough available resources in the queue.

.. image:: images/queues-description.jpg
  :scale: 60 %
  :align: center

+--------------+-----------------+--------------------------------------------------------------------+------------------------------------+
| Category     | Queue Name      | Assigned Computing Resources                                       | Remarks                            |
+--------------+-----------------+--------------------------------------------------------------------+------------------------------------+
| Dedicated    | **q01**         | - tem-wn[1001-1003].sdfarm.kr (28 cores and 192GB memory per node) | - USER/GROUP Access Control        |
|              |                 | - tem-gpu01.sdfarm.kr (28 cores, 2 P100 GPGPUs and 384GB memory)   |                                    | 
|              +-----------------+--------------------------------------------------------------------+                                    |
|              | **q02**         | - tem-wn[1004-1006].sdfarm.kr (28 cores and 192GB memory per node) |                                    |
|              |                 | - tem-gpu02.sdfarm.kr (28 cores, 2 P100 GPGPUs and 384 GB memory)  |                                    |
|              +-----------------+--------------------------------------------------------------------+                                    |
|              | **q03**         | - tem-wn[1007-1009].sdfarm.kr (28 cores and 192GB memory per node) |                                    |
|              |                 | - tem-gpu03.sdfarm.kr (28 cores, 2 P100 GPGPUs and 384 GB memory)  |                                    |
+--------------+-----------------+--------------------------------------------------------------------+------------------------------------+
| Shared       | **sharedq**     | - tem-wn[1010-1011].sdfarm.kr (28 cores and 192GB memory per node) | - hyperthreading(H/T) enabled      |
|              | (default)       | - tem-gpu04.sdfarm.kr (24 cores, 2 P40 GPGPUs and 128GB memory)    | - 232 logical CPU cores total      |
|              |                 | - tem-gpu05.sdfarm.kr (36 cores, 2 P40 GPGPUs and 256GB memory)    | - 4 P40 GPGPUs total               |
+--------------+-----------------+--------------------------------------------------------------------+------------------------------------+


Time schedule for queue assignment
==================================

.. raw:: html

  <div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; max-width: 100%; height: auto;">
    <iframe src="https://calendar.google.com/calendar/embed?src=uh81cs11mhp8cr6fqjp005ks9o%40group.calendar.google.com&ctz=Asia%2FSeoul" style="border: 0" width="1050" height="700" frameborder="0" scrolling="no"></iframe>
  </div>

