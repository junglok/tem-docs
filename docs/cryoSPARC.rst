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
  In the meanwhile, hhus, we had to decide that each user must setup **a completely isolated cryoSPARC instance independently within thier own home directories** 
  (/tem/home/<userhome>).
  This method relies on the UNIX system for security and is more tedious to manage but provides stronger access restrictions for users own dataset.
  For users convenience, we are ready to install and setup a cryoSPARC instance with **administrative automation codes on behalf of users**.  

Prerequisites
=============

Now, cryoSPARC is available free of charge for academic use. For a completely isolated cryoSPARC instance, user must have their own non-commercial license key for cryoSPARC v2.
Please visit the CryoSPARC official site, request a license key and inform the valid key to GSDC TEM service admin. by e-mail.  

Getting a cryoSPARC instance 
============================

CryoSPARC is a backend and frontend software system that provides data processing and image analysis capabilities for single particle cryo-EM, 
along with a browser based user interface and command line tools. CryoSPARC is composed of three major components : cryosparc_master, cryospace_database and cryosparc_worker.

* **cryosparc_master** : Master processes (webapps, command cores, databases, etc.) run together on one node (for our case, tem-ui.sdfarm.kr login node). These processes host 
HTML5 based web applications, spawn or submit jobs to a cluster scheduler (for example, to PBS-based batch system)

* **cryosparc_worker** : Worker process can be spawned on any available worker nodes, 
and do data processing and image analysis tasks which are pre-defined within cryoSPRAC software packags.

* **cryosparc_database** : CryoSPARC database is built on top of mongoDB, managing the metadata of users workflows, jobs, backend clusters or workers as well as users. 

1. (Admin) Install and setup a cryoSPARC instance

On behalf of users, administrator can execute ansible configuration automation code-snippets to install and setup a cryoSPARC instance, using a given valid license key.
Master, worker and database sub-packages will be installed during configuration automation, which are located in **/tem/home/<user>/.cryosparc** after setups.
A setup procedure includes registering both cluster(lane or worker nodes) instance and webapp's admin/normal users account. 
The whole setup will take about 10 minutes. 

After installation, **/tem/home/<user>/.cryosparc** has following directories/files structure:

.. code-block:: bash

  $> cd ~/.cryosparc
  $> tree -L 1 .

  .
  ├─ cluster_info.json              ## cluster(lane) information to register    
  ├─ cluster_script.sh              ## PBS script template to submit jobs to worker cluster(lane)    
  ├─ cryosparc2_master              ## cryosparc_master package install path
  ├─ cryosparc2_master.tar.gz
  ├─ cryosparc2_worker              ## cryosparc_worker package install path
  ├─ cryosparc2_worker.tar.gz
  └─ cryosparc_database             ## cryosparc_database package install path


.. warning::
  **CAUTION!**. ** DO NOT** delete cryoSPARC instance base directory, **/tem/home/<user>/.cryosparc**. The cryoSPARC base directory contains database. If this directory is deleted,
  all the projet, job and workflow information will be corrupted and lost.




2. (User) Verifying installation


Launching CryoSPARC instance
============================