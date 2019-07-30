************
Batch Queues
************

Batch queue list
================

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
| Shared       | **sharedq**     | - tem-wn[1010-1011].sdfarm.kr                                      | - 112 logical CPU cores            |
|              | (default)       |                                                                    | - hyperthreading(H/T) enabled      |
+--------------+-----------------+--------------------------------------------------------------------+------------------------------------+
| Experimental | **exp01**       | - tem-gpu04.sdfarm.kr (48 cores, 128GB memory and 2 P40 GPGPUs)    | - logical CPU cores, H/T enabled   |
|              +-----------------+--------------------------------------------------------------------+------------------------------------+
|              | **exp02**       | - tem-gpu05.sdfarm.kr (48 cores, 128GB memory and 2 P40 GPGPUs)    | - logical CPU cores, H/T enabled   |
+--------------+-----------------+--------------------------------------------------------------------+------------------------------------+


Time schedule for queue assignment
==================================

.. raw:: html

  <div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; max-width: 100%; height: auto;">
    <iframe src="https://calendar.google.com/calendar/embed?src=uh81cs11mhp8cr6fqjp005ks9o%40group.calendar.google.com&ctz=Asia%2FSeoul" style="border: 0" width="800" height="600" frameborder="0" scrolling="no"></iframe>
  </div>

