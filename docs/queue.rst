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
    <iframe src="https://calendar.google.com/calendar?cid=dWg4MWNzMTFtaHA4Y3I2ZnFqcDAwNWtzOW9AZ3JvdXAuY2FsZW5kYXIuZ29vZ2xlLmNvbQ" frameborder="0" allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe>
  </div>

