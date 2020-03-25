*********
cryoSPARC
*********
CryoSPARC is the state-of-the-art platform used globally for obtaining 3D structural information from single particle cryo-EM data. 
The cryoSPARC platform enables automated, high quality and high-throughput structure discovery of proteins, viruses and molecular complexes 
for research and drug discovery.

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

* **cryosparc_master** : Master processes (webapps, command_core, databases, etc.) run together on one node (for our case, tem-ui.sdfarm.kr login node). These processes host HTML5 based web applications, spawn or submit jobs to a cluster scheduler (for example, to PBS-based batch system)

* **cryosparc_worker** : Worker process can be spawned on any available worker nodes, and do data processing and image analysis tasks which are pre-defined within cryoSPRAC software packages.

* **cryosparc_database** : CryoSPARC database is built on top of mongoDB, managing the metadata of users workflows, projects, jobs, backend clusters or workers as well as users. 

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

By default, master processes (webapp, command_core, database, etc.) are automatilly started during configuration automation.
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
   export "CRYOSPARC_DB_PATH=/tem/home/<user>/.cryosparc/cryosparc_database"
   export "CRYOSPARC_HTTP_RTP_PORT=39006"
   export "CRYOSPARC_LICENSE_ID=<license_key"
   export "CRYOSPARC_MONGO_PORT=39001"
   export "CRYOSPARC_MONGO_CACHE_GB=4"
   export "CRYOSPARC_HEARTBEAT_SECONDS=60"
   export "CRYOSPARC_COMMAND_PROXY_PORT=39004"
   export "CRYOSPARC_ROOT_DIR=/tem/home/<user>/.cryosparc/cryosparc2_master"
   export "CRYOSPARC_COMMAND_CORE_PORT=39002"
   export "CRYOSPARC_BASE_PORT=39000"
   export "CRYOSPARC_PATH=/tem/home/<user>/.cryosparc/cryosparc2_master/deps/anaconda/bin:/tem/home/<user>/.cryosparc/cryosparc2_master/deps/external/mongodb/bin:/tem/home/<user>/.cryosparc/cryosparc2_master/bin"
   export "CRYOSPARC_LIVE_ENABLED=false"
   export "CRYOSPARC_COMMAND_RTP_PORT=39035"
   export "CRYOSPARC_SUPERVISOR_SOCK_FILE=/tmp/cryosparc-supervisor-627a9991e2f2f069094732dfd78d1696.sock"
   export "CRYOSPARC_LD_LIBRARY_PATH="
   export "LD_LIBRARY_PATH=:"
   export "LD_PRELOAD=/tem/home/<user>/.cryosparc/cryosparc2_master/deps/anaconda/lib/libpython2.7.so.1.0"
   export "PYTHONPATH="
   export "PYTHONNOUSERSITE=true"

You can findwhat kinds of environment variables have been set for the cryoSPARC instance. 

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
   command_core                     RUNNING   pid 171073, uptime 1 day, 5:35:11
   command_proxy                    RUNNING   pid 171175, uptime 1 day, 5:35:02
   command_rtp                      STOPPED   Not started
   command_vis                      RUNNING   pid 171170, uptime 1 day, 5:35:03
   database                         RUNNING   pid 170997, uptime 1 day, 5:35:14
   watchdog_dev                     STOPPED   Not started
   webapp                           RUNNING   pid 171178, uptime 1 day, 5:35:00
   webapp_dev                       STOPPED   Not started

   ----------------------------------------------------------------------------

   global config variables:

   export CRYOSPARC_LICENSE_ID="<license_key>"
   export CRYOSPARC_MASTER_HOSTNAME="tem-ui.sdfarm.kr"
   export CRYOSPARC_DB_PATH="/tem/home/<user>/.cryosparc/cryosparc_database"
   export CRYOSPARC_BASE_PORT=39000
   export CRYOSPARC_DEVELOP=false
   export CRYOSPARC_INSECURE=true
   export CRYOSPARC_CLICK_WRAP=true


Launching CryoSPARC instance
============================

We assume that user's network setup looks like (most commonly used scenario):

.. code-block:: bash

                   internet
   [ localhost ]==============[ firewall | tem-ui.sdfarm.kr ]

For Linux/Mac users 
-------------------

With the following command, you can start an SSH tunnel to export **CRYOSPARC_BASE_PORT** from tem-ui.sdfarm.kr to your local client machine.

.. code-block:: bash

   $> ssh -N -f -L localhost:39000:tem-ui.sdfarm.kr:<CRYOSPARC_BASE_PORT> -o Port=<ssh_port> <userid>@tem-ui.sdfarm.kr

   ## -N : Do not execute a remote command. This is useful option for just forwarding ports.
   ## -f : Requests ssh to go to background just before command execution.
   ## -L [bind_address:]port:host:hostport

.. note::
   You can close the terminal window (because 'ssh' will be run in the background) after running the above command. The tunnel will stay open.   

Now, open your browser (Chrome/Firefox/Safari recommended) and navigate to http://localhost:39000. You should be presented with the cryoSPARC login page.

For Windows users 
-----------------

* Using MobaXterm

  * Open 'MobaXterm' application.
  * 'MobaXterm' -> 'Tools' -> 'MobaSSHTunnel (port forwarding)' : Open MobaSSHTunnel dialog box.
  * 'New SSH tunnel' : Set a forwarded port binding option and save the setting.
  * Give the name to the saved port forwarding settings, and start the tunnel connection.

.. note::
   You must use **CRYOSPARC_BASE_PORT** for the 'Remote server' port section.   

.. image:: images/mobaxterm-tunnel1.JPG
    :scale: 50 %
    :align: center

Now, open your browser (Chrome/Firefox/Safari recommended) and navigate to http://localhost:39000. You should be presented with the cryoSPARC login page.


* Using Putty
  
  * Open 'PuTTy Configuration' dialog box.
  * 'PuTTy Configuration' -> 'Session' : Load a SSH session to connect tem-ui login node with the known <ssh_port>.
  * 'PuTTy Configuration' -> 'Connection' -> 'SSH' -> 'Tunnels' : Set a forwarded port binding option and add the entry.

.. note::
   You must use **tem-ui.sdfarm.kr:CRYOSPARC_BASE_PORT** for the 'Destination' field. 

.. image:: images/putty-tunnel.JPG
    :scale: 60 %
    :align: center

Now, open your browser (Chrome/Firefox/Safari recommended) and navigate to http://localhost:39000. You should be presented with the cryoSPARC login page.

Exploring CryoSPARC web apps
============================

.. note::
   For details on user interface and usages of cryoSPARC, refer to cryoSPARC's official document.
   https://cryosparc.com/docs/reference/general 

CryoSPARC login
---------------

E-mail and password information will be notified to users as the installation and setup is finished.
Given e-mail and password, users can login to cryoSPARC web interfaces. 

.. image:: images/cryosparc-login.png
    :scale: 50 %
    :align: center

CryoSPARC dashboard
-------------------

.. image:: images/cryosparc-dashboard.png
    :scale: 45 %
    :align: center

CryoSPARC project
-----------------

.. image:: images/cryosparc-project.png
    :scale: 45 %
    :align: center

CryoSPARC cluster(lane)
-----------------------

.. image:: images/cryosparc-cluster.png
    :scale: 45 %
    :align: center


Tutorial on processing T20S
===========================

* Please refer to CryoSPARC's webpage for the tutorial on processing T20S : https://cryosparc.com/docs/tutorials/t20s

Trouble shooting
================
