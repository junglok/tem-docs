*********
cryoSPARC
*********
CryoSPARC is the state-of-the-art platform used globally for obtaining 3D structural information from single particle cryo-EM data. 
The cryoSPARC platform enables automated, high quality and high-throughput structure discovery of proteins, viruses and molecular complexes 
for research and drug discovery. (from CryoSPARC offical site https://cryosparc.com)

.. note::
  cryoSPARC offical site : https://cryosparc.com

.. note::
  At the time of writing this document (Mar. 2020), unforturnatelly, cryoSPARC v2.x does not provide the method of installing **a single cryoSPARC instance**
  (consisting of web applcation, command core, and database) **for use by a number of users with the complete isolation and security of their project data**.
  This problem might be resolved with later versions of cryoSPARC after CryoSPARC re-designs the product with the concept of "Hub" (as mentioned in cryoSPARC forum 
  https://discuss.cryosparc.com/t/use-linux-user-accounts/3480).
  In the meanwhile, thus, we had to decide that each user must setup **a completely isolated cryoSPARC instance independently within thier own home directories** 
  (/tem/home/<userhome>).
  This method relies on the UNIX system for security and is more tedious to manage but provides stronger access restrictions for users own dataset.
  For users convenience, we are ready to install and setup a cryoSPARC instance with **administrative automation codes on behalf of users**.  

Prerequisites
=============

Now, cryoSPARC is available free of charge for academic use. For a completely isolated cryoSPARC instance, user must have their own non-commercial license key for cryoSPARC v2.
**Please visit the CryoSPARC official site, request a license key and inform the valid key to GSDC TEM service administrator by e-mail.**  

Getting a cryoSPARC instance 
============================

CryoSPARC is a backend and frontend software system that provides data processing and image analysis capabilities for single particle cryo-EM, 
along with a browser based user interface and command line tools. CryoSPARC is composed of three major components : cryosparc_master, cryospace_database and cryosparc_worker.

* **cryosparc_master** : Master processes (webapps, command cores, databases, etc.) run together on one node (for our case, tem-ui.sdfarm.kr login node). These processes host HTML5 based web applications, spawn or submit jobs to a cluster scheduler (for example, to PBS-based batch system)

* **cryosparc_worker** : Worker process can be spawned on any available worker nodes, and do data processing and image analysis tasks which are pre-defined within cryoSPRAC software packags.

* **cryosparc_database** : CryoSPARC database is built on top of mongoDB, managing the metadata of users workflows, jobs, backend clusters or workers as well as users. 

1. (Admin) Install and setup a cryoSPARC instance
-------------------------------------------------

On behalf of users, administrator can execute ansible configuration automation code-snippets to install and setup a cryoSPARC instance, using a given valid license key.
Master, worker and database sub-packages will be installed during configuration automation, which are located in **/tem/home/<user>/.cryosparc** after finishing setup.
A setup procedure includes registering both cluster(lane or worker nodes) instance and webapp's admin/normal users account. 
The whole setup will take about 10 minutes. 

After finishing installation, **/tem/home/<user>/.cryosparc** has following directories/files structure:

.. code-block:: bash

  $> cd ~/.cryosparc
  $> tree -L 1 ./
  .
  ├─ cluster_info.json              ## cluster(lane) information to register    
  ├─ cluster_script.sh              ## PBS script template to submit jobs to worker cluster(lane)    
  ├─ cryosparc2_master              ## cryosparc_master package install path
  ├─ cryosparc2_master.tar.gz
  ├─ cryosparc2_worker              ## cryosparc_worker package install path
  ├─ cryosparc2_worker.tar.gz
  └─ cryosparc_database             ## cryosparc_database package install path


.. warning::
  **!! CAUTION !!** **DO NOT** delete or modify cryoSPARC instance base directory, **/tem/home/<user>/.cryosparc**. The cryoSPARC base directory contains database. If this directory is deleted,
  all the project, job and workflow information will be corrupted and lost.

Also, the configuration code-snippets implicitly add cryoSPARC instance's binary path to PATH environment variable.

.. code-block:: bash

   $> cat /tem/home/<user>/.bashrc
   ...
   # User specific aliases and functions
   export PATH='/tem/home/<user>/.cryosparc/cryosparc2_master/bin':$PATH


2. (User) Verifying installation
--------------------------------

By default, master processes (webapp, command-core, database, etc.) are automatilly started during configuration automation.
Users should check and verify whether the master processes are working correctly on tem-ui.sdfarm.kr login node or not. 

* **Checking environment variables for cryoSPARC instance**

.. code-block:: bash

   $> cryosparcm env
   
   export "CRYOSPARC_HTTP_PORT=39000"
   export "CRYOSPARC_MASTER_HOSTNAME=tem-ui.sdfarm.kr"
   export "CRYOSPARC_CLICK_WRAP=true"
   export "CRYOSPARC_COMMAND_VIS_PORT=39003"
   export "CRYOSPARC_INSECURE=true"
   export "CRYOSPARC_DEVELOP=false"
   **export "CRYOSPARC_DB_PATH=/tem/home/<user>/.cryosparc/cryosparc_database"**
   export "CRYOSPARC_HTTP_RTP_PORT=39006"
   **export "CRYOSPARC_LICENSE_ID=<license_key>"**
   export "CRYOSPARC_MONGO_PORT=39001"
   export "CRYOSPARC_MONGO_CACHE_GB=4"
   export "CRYOSPARC_HEARTBEAT_SECONDS=60"
   export "CRYOSPARC_COMMAND_PROXY_PORT=39004"
   **export "CRYOSPARC_ROOT_DIR=/tem/home/<user>/.cryosparc/cryosparc2_master"**
   export "CRYOSPARC_COMMAND_CORE_PORT=39002"
   **export "CRYOSPARC_BASE_PORT=39000"**
   export "CRYOSPARC_PATH=/tem/home/<user>/.cryosparc/cryosparc2_master/deps/anaconda/bin:/tem/home/<user>/.cryosparc/cryosparc2_master/deps/external/mongodb/bin:/tem/home/<user>/.cryosparc/cryosparc2_master/bin"
   export "CRYOSPARC_LIVE_ENABLED=false"
   export "CRYOSPARC_COMMAND_RTP_PORT=39035"
   export "CRYOSPARC_SUPERVISOR_SOCK_FILE=/tmp/cryosparc-supervisor-627a9991e2f2f069094732dfd78d1696.sock"
   export "CRYOSPARC_LD_LIBRARY_PATH="
   export "LD_LIBRARY_PATH=:"
   export "LD_PRELOAD=/tem/home/<user>/.cryosparc/cryosparc2_master/deps/anaconda/lib/libpython2.7.so.1.0"
   export "PYTHONPATH="
   export "PYTHONNOUSERSITE=true"

User must see what kinds of environment variables are set for the cryoSPARC instance. 

.. note::
   Especially, user should check **CRYOSPARC_BASE_PORT** (above example, 39000), which is **the listening port of cryoSPARC web application**. 
   Later, this port number is used to make SSH tunneling between client and tem-ui.sdfarm.kr login node. 
   **Via the tunneled connection over SSH, users can access the web UI of cryoSPARC instance.**    

* **Checking the status of cryoSPARC instance**

.. code-block:: bash

   $> cryosparcm status
   ----------------------------------------------------------------------------
   CryoSPARC System master node installed at
   /tem/home/<user>/.cryosparc/cryosparc2_master
   Current cryoSPARC version: v2.14.2
   ----------------------------------------------------------------------------

   cryosparcm process status:
   app                              STOPPED   Not started
   app_dev                          STOPPED   Not started
   **command_core                     RUNNING   pid 171073, uptime 1 day, 5:35:11**
   **command_proxy                    RUNNING   pid 171175, uptime 1 day, 5:35:02**
   command_rtp                      STOPPED   Not started
   **command_vis                      RUNNING   pid 171170, uptime 1 day, 5:35:03**
   **database                         RUNNING   pid 170997, uptime 1 day, 5:35:14**
   watchdog_dev                     STOPPED   Not started
   **webapp                           RUNNING   pid 171178, uptime 1 day, 5:35:00**
   webapp_dev                       STOPPED   Not started

   ----------------------------------------------------------------------------

   global config variables:

   export CRYOSPARC_LICENSE_ID="<license_key>"
   export CRYOSPARC_MASTER_HOSTNAME="tem-ui.sdfarm.kr"
   export CRYOSPARC_DB_PATH="/tem/home/<user>/.cryosparc/cryosparc_database"
   **export CRYOSPARC_BASE_PORT=39000**
   export CRYOSPARC_DEVELOP=false
   export CRYOSPARC_INSECURE=true
   export CRYOSPARC_CLICK_WRAP=true




Launching CryoSPARC instance
============================