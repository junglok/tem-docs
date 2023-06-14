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

.. image:: images/batch.png
  :scale: 70 %
  :align: center


.. tabularcolumns:: |\Y{0.1}|\Y{0.1}|\Y{0.5}|\Y{0.3}|
.. table:: My Table
   :widths: auto
   :class: longtable

+--------------+-----------------+-----------------------------------------------------------------------+------------------------------------+
| Category     | Queue Name      | Assigned Computing Resources                                          | Remarks                            |
+==============+=================+=======================================================================+====================================+
| Shared       | **cpuQ**        | - tem-wn[1001-1002]-el7.sdfarm.kr (36 cores and 384GB memory per node)| - 380 Physical CPU cores           |
|              |                 | - tem-wn[1003-1013]-el7.sdfarm.kr (28 cores and 192GB memory per node)|                                    |
|              +-----------------+-----------------------------------------------------------------------+------------------------------------+
|              | **gpuQ**        | - tem-gpu[01-03]-el7.sdfarm.kr (28 cores, 2 P100 GPUs and 384GB mem.) | - 204 Physical CPU cores           | 
|              |                 | - tem-gpu[04-05]-el7.sdfarm.kr (28 cores, 2 P40 GPUs and 256GB mem.)  | - 14 GPUs                          |
|              |                 | - tem-gpu[06-07]-el7.sdfarm.kr (32 cores, 2 A100 GPUs and 256GB mem.) | - P100 16GB device memory          |
|              |                 |                                                                       | - P40 24GB device memory           |
|              |                 |                                                                       | - A100 40GB device memory          |   
+--------------+-----------------+-----------------------------------------------------------------------+------------------------------------+
