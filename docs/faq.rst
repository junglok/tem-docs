**************************
Frequently Asked Questions
**************************

* 1. `how to resolve the problems on (re)starting your own cryosparc instance`_
* 2. `how to repair cryosparc database corruption caused by duplicated mongod executions`_
* 3. `how to update cryosparc softwares`_ 

.. _how to resolve the problems on (re)starting your own cryosparc instance:

How to resolve the problems on (re)starting your own cryosparc instance?
========================================================================

You should check all the cryosparc related processes (i.e., supervisord, mongod, command_core, command_vis, command_rtp, webapp, app, liveapp) 
to be terminated successfully first on **tem-cs-el7.sdfarm.kr** or **tem-ui-el7.sdfarm.kr** server.

.. code-block:: bash

    (log into tem-cs-el7.sdfarm.kr or tem-ui-el7.sdfarm.kr server first on which the CryoSPARC is running)
    (example) userid@tem-[cs|ui]-el7 $> cryosparcm stop

    CryoSPARC is running.
    Stopping cryoSPARC
    app: stopped
    command_core: stopped
    command_rtp: stopped
    command_vis: stopped
    liveapp: stopped
    webapp: stopped
    database: stopped
    Shut down

    (example) userid@tem-[cs|ui]-el7 $>  ps aux | grep <userid> | grep cryosparc
    userid    2449  0.0  0.0 152792 17480 ?        Ss   Jun24   0:18 python /tem/scratch/<GroupDir>/.cryosparc/cryosparc_master/deps/anaconda/envs/cryosparc_master_env/bin/supervisord -c /tem/scratch/<GroupDir>/.cryosparc/cryosparc_master/supervisord.conf
    userid    2472  1.2  0.0 1429268 57412 ?       Sl   Jun24  13:19 mongod --dbpath /tem/scratch/<GroupDir>/.cryosparc/cryosparc_database --port 39031 --oplogSize 64 --replSet meteor --nojournal --wiredTigerCacheSizeGB 4
    userid    2900  0.2  0.0 860572 83028 ?        Sl   Jun24   2:23 python -c import cryosparc_command.command_core as serv; serv.start(port=39032)
    userid    4332  0.1  0.1 854192 236396 ?       Sl   Jun24   1:53 python -c import cryosparc_command.command_vis as serv; serv.start(port=39033)
    userid    4378  0.4  0.0 1190536 196316 ?      Sl   Jun24   4:59 python -c import cryosparc_command.command_rtp as serv; serv.start(port=39035)
    userid    5586  0.1  0.0 1331136 116972 ?      Sl   Jun24   1:17 /tem/scratch/<GroupDir>/.cryosparc/cryosparc_master/cryosparc_webapp/nodejs/bin/node ./bundle/main.js
    userid    5625  0.1  0.0 1049868 97640 ?       Sl   Jun24   1:22 /tem/scratch/<GroupDir>/.cryosparc/cryosparc_master/cryosparc_app/nodejs/bin/node ./bundle/main.js
    userid    5690  0.2  0.0 1326136 81432 ?       Sl   Jun24   2:12 /tem/scratch/<GroupDir>/.cryosparc/cryosparc_master/cryosparc_liveapp/nodejs/bin/node ./bundle/main.js

    (example) userid@tem-[cs|ui]-el7 $> ps aux | grep <userid> | grep -E "cryosparc|node" | awk '{print $2}' | xargs -I{} kill -9 {}


Second, find your own cryosparc unix socket files on /tmp directory, and if exists, delete the files using rm command.

.. code-block:: bash

    userid@tem-[cs|ui]-el7 $> cd /tmp
    (example) userid@tem-[cs|ui]-el7 $> ls -al | grep <userid> | grep sock
   
    srwx------.  1 userid       userid          0 Jun 24 16:39 cryosparc-supervisor-627a9991e2f2f069094732dfd78d1696.sock
    srwx------.  1 userid       userid          0 Jun 24 16:39 mongodb-39031.sock

    (example) userid@tem-[cs|ui]-el7 $> rm cryosparc-supervisor-627a9991e2f2f069094732dfd78d1696.sock
    (example) userid@tem-[cs|ui]-el7 $> rm mongodb-39031.sock 



Then, start your cryosparc instance.

.. code-block:: bash

    (example) userid@tem-[cs|ui]-el7 $> cryosparcm start

    Starting cryoSPARC System master process..
    CryoSPARC is not already running.
    database: started
    command_core: started
        command_core connection succeeded
        command_core startup successful
    command_vis: started
    command_rtp: started
        command_rtp connection succeeded
        command_rtp startup successful
    webapp: started
    app: started
    liveapp: started
    -----------------------------------------------------

    CryoSPARC master started.
        From this machine, access cryoSPARC at
            http://localhost:39030
        and access cryoSPARC Live at
            http://localhost:39036
    please note the legacy cryoSPARC Live application is running at
            http://localhost:39037

    From other machines on the network, access cryoSPARC at
        http://tem-[cs|ui]-el7.sdfarm.kr:39030
    and access cryoSPARC Live at
        http://tem-[cs|ui]-el7.sdfarm.kr:39036


    Startup can take several minutes. Point your browser to the address
    and refresh until you see the cryoSPARC web interface.


 
.. _how to repair cryosparc database corruption caused by duplicated mongod executions:  

How to repair cryosparc database corruption? 
============================================

With duplicated mongod executions, cryosparc database can be corrupted resulting in **"database: ERROR (spawn error)"** on (re)starting cryosparc instance. To address this abnormal case, you can try to repair the database with followings:


First, **stop all the cryosparc processes and delete the unix socket files.** See `how to resolve the problems on (re)starting your own cryosparc instance`_  for more details.

Second, try to repair the cryosparc database i.e., mongodb.

.. code-block:: bash

    userid@tem-[cs|ui]-el7 $> cryosparcm env
    userid@tem-[cs|ui]-el7 $> cd /tem/scratch/<GroupDir>/.cryosparc
    userid@tem-[cs|ui]-el7 $> tar cvfz cryosparc_database.backup.tar.gz cryosparc_database
    userid@tem-[cs|ui]-el7 $> eval $(cryosparcm env) 
    userid@tem-[cs|ui]-el7 $> cd cryosparc_database
    userid@tem-[cs|ui]-el7 $> mongod --dbpath ./ --repair
 
 
  
.. _how to update cryosparc softwares:

How to upgrade (or downgrade) to the specific version of cryosparc softwares? 
============================================================================

The following update guides summarize the procedure for cryosparc's master and worker software updates. 
For more details, please refer to https://guide.cryosparc.com/setup-configuration-and-management/software-updates.

1. Checking for updates
-----------------------

Log into the **tem-cs-el7.sdfarm.kr** or **tem-ui-el7.sdfarm.kr** server where the cryosparc master is installed using ssh. Then, run this command if you want to check updates.

.. code-block:: bash

    userid@tem-[cs|ui]-el7 $> cryosparcm update --check
    CryoSPARC current version v4.0.0
            update starting on Wed Mar 18 12:09:52 EDT 2021

    current version v4.0.0
        new version v4.1.0

    Update available!

Also, you can use this command **cryosparcm update --list** to get a full list of available versions.

.. code-block:: bash

    userid@tem-[cs|ui]-el7 $> cryosparcm update --check
    CryoSPARC current version v4.0.0
            update starting on Wed Mar 18 12:09:52 EDT 2021

    Available versions:

    v2.0.18
    v2.0.20
    v2.0.23
    v2.0.27
    v2.1.0
    v2.2.0
    v2.3.0
    v2.3.2
    v2.4.0
    v2.4.2
    v2.4.5
    v2.4.6
    v2.5.0
    v2.5.2-locref-mask-patch
    v2.8.0
    v2.8.1
    v2.8.2
    v2.8.3
    v2.9.0
    v2.11.0
    v2.12.0
    v2.12.2
    v2.12.4
    v2.13.0
    v2.13.2
    v2.14.0
    v2.14.2
    v2.15.0
    v3.0.0
    v3.0.1
    v3.1.0
    v3.2.0

    To install a specific version, use 
        $ cryosparcm update --version=vXX.YY.ZZ[-branchname]


2. Before you update: complete or kill running jobs
---------------------------------------------------

Before you update the cryosparc softwares, you must wait for all the running cryosparc jobs completed (or kill your jobs).  
You also must check all the cryosparc related processes (i.e., supervisord, mongod, command_core, command_vis, command_rtp, webapp, app, liveapp) to be terminated successfully.

.. code-block:: bash

    (example) userid@tem-[cs|ui]-el7 $> cryosparcm stop

    CryoSPARC is running.
    Stopping cryoSPARC
    app: stopped
    command_core: stopped
    command_rtp: stopped
    command_vis: stopped
    liveapp: stopped
    webapp: stopped
    database: stopped
    Shut down

    (example) userid@tem-[cs|ui]-el7 $>  ps aux | grep <userid> | grep cryosparc
    userid    2449  0.0  0.0 152792 17480 ?        Ss   Jun24   0:18 python /tem/home/userid/.cryosparc/cryosparc2_master/deps/anaconda/envs/cryosparc_master_env/bin/supervisord -c /tem/home/userid/.cryosparc/cryosparc2_master/supervisord.conf
    userid    2472  1.2  0.0 1429268 57412 ?       Sl   Jun24  13:19 mongod --dbpath /tem/home/userid/.cryosparc/cryosparc_database --port 39031 --oplogSize 64 --replSet meteor --nojournal --wiredTigerCacheSizeGB 4
    userid    2900  0.2  0.0 860572 83028 ?        Sl   Jun24   2:23 python -c import cryosparc_command.command_core as serv; serv.start(port=39032)
    userid    4332  0.1  0.1 854192 236396 ?       Sl   Jun24   1:53 python -c import cryosparc_command.command_vis as serv; serv.start(port=39033)
    userid    4378  0.4  0.0 1190536 196316 ?      Sl   Jun24   4:59 python -c import cryosparc_command.command_rtp as serv; serv.start(port=39035)
    userid    5586  0.1  0.0 1331136 116972 ?      Sl   Jun24   1:17 /tem/home/userid/.cryosparc/cryosparc2_master/cryosparc_webapp/nodejs/bin/node ./bundle/main.js
    userid    5625  0.1  0.0 1049868 97640 ?       Sl   Jun24   1:22 /tem/home/userid/.cryosparc/cryosparc2_master/cryosparc_app/nodejs/bin/node ./bundle/main.js
    userid    5690  0.2  0.0 1326136 81432 ?       Sl   Jun24   2:12 /tem/home/userid/.cryosparc/cryosparc2_master/cryosparc_liveapp/nodejs/bin/node ./bundle/main.js

    (example) userid@tem-[cs|ui]-el7 $> kill -9 2449 2472 2900 4332 4378 5586 5625 5690


Find your own cryosparc unix socket files on /tmp directory, and if exists, delete the files using rm command.

.. code-block:: bash

    userid@tem-[cs|ui]-el7 $> cd /tmp
    (example) userid@tem-[cs|ui]-el7 $> ls -al | grep <userid> | grep sock
   
    srwx------.  1 userid       userid          0 Jun 24 16:39 cryosparc-supervisor-627a9991e2f2f069094732dfd78d1696.sock
    srwx------.  1 userid       userid          0 Jun 24 16:39 mongodb-39031.sock

    (example) userid@tem-[cs|ui]-el7 $> rm cryosparc-supervisor-627a9991e2f2f069094732dfd78d1696.sock
    (example) userid@tem-[cs|ui]-el7 $> rm mongodb-39031.sock

 

3. Back-up cryosparc databases
------------------------------

We also highly recommend making a backup of your database as described below.

.. code-block:: bash

    userid@tem-[cs|ui]-el7 $> cryosparcm backup

    Backing up to /tem/scratch/<GroupDir>/.cryosparc/cryosparc_database/backup/cryosparc_backup_2021_04_20_15h00.archive

    CryoSPARC is not already running.

    Starting the database in case it's not already running.
    database: started

    Executing mongodump.

    2021-04-20T15:00:42.606+0900    writing admin.system.version to archive '/tem/scratch/<GroupDir>/.cryosparc/cryosparc_database/backup/cryosparc_backup_2021_04_20_15h00.archive'
    2021-04-20T15:00:42.608+0900    done dumping admin.system.version (1 document)
    2021-04-20T15:00:42.609+0900    writing meteor.events to archive '/tem/scratch/<GroupDir>/.cryosparc/cryosparc_database/backup/cryosparc_backup_2021_04_20_15h00.archive'
    2021-04-20T15:00:42.617+0900    writing meteor.fs.files to archive '/tem/scratch/<GroupDir>/.cryosparc/cryosparc_database/backup/cryosparc_backup_2021_04_20_15h00.archive'
    2021-04-20T15:00:42.617+0900    writing meteor.notifications to archive '/tem/scratch/<GroupDir>/.cryosparc/cryosparc_database/backup/cryosparc_backup_2021_04_20_15h00.archive'
    2021-04-20T15:00:42.618+0900    writing meteor.fs.chunks to archive '/tem/scratch/<GroupDir>/.cryosparc/cryosparc_database/backup/cryosparc_backup_2021_04_20_15h00.archive'
    2021-04-20T15:00:42.661+0900    done dumping meteor.notifications (315 documents)
    2021-04-20T15:00:42.661+0900    writing meteor.jobs to archive '/tem/scratch/<GroupDir>/.cryosparc/cryosparc_database/backup/cryosparc_backup_2021_04_20_15h00.archive'
    2021-04-20T15:00:42.692+0900    done dumping meteor.fs.files (8386 documents)
    2021-04-20T15:00:42.692+0900    writing meteor.cache_files to archive '/tem/scratch/<GroupDir>/.cryosparc/cryosparc_database/backup/cryosparc_backup_2021_04_20_15h00.archive'
    2021-04-20T15:00:42.693+0900    done dumping meteor.jobs (166 documents)

    ... (omit)

    2021-04-20T15:00:42.751+0900    done dumping meteor.file_index (0 documents)
    2021-04-20T15:00:42.755+0900    done dumping meteor.exposures (0 documents)
    2021-04-20T15:00:42.770+0900    done dumping meteor.events (25676 documents)
    2021-04-20T15:00:45.182+0900    [####....................]  meteor.fs.chunks  1535/8386  (18.3%)
    2021-04-20T15:00:48.182+0900    [########................]  meteor.fs.chunks  3048/8386  (36.3%)
    2021-04-20T15:00:51.182+0900    [###############.........]  meteor.fs.chunks  5475/8386  (65.3%)
    2021-04-20T15:00:53.903+0900    [########################]  meteor.fs.chunks  8386/8386  (100.0%)
    2021-04-20T15:00:53.905+0900    done dumping meteor.fs.chunks (8386 documents)

    Complete!

After backing up your cryosparc database, you should check the status of cryosparc daemons and stop them again.

.. code-block:: bash

    userid@tem-[cs|ui]-el7 $> cryosparcm status
    userid@tem-[cs|ui]-el7 $> cryosparcm stop


4. Cryosparc master updates
---------------------------

To begin automatic master updates with the newest available version of cryoSPARC, just run

.. code-block:: bash

    userid@tem-[cs|ui]-el7 $> cryosparcm update

    CryoSPARC current version v4.0.0
              update starting on Tue Apr 20 15:36:12 KST 2021

    No version specified - updating to latest version.

    =============================
    Updating to version v4.1.0.
    =============================
    CryoSPARC is not already running.
    If you would like to restart, use cryosparcm restart
      Removing previous downloads...
      Downloading master update...
      % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                     Dload  Upload   Total   Spent    Left  Speed
      0     0    0     0    0     0      0      0 --:--:--  0:00:02 --:--:--     0
    100  785M  100  785M    0     0  2072k      0  0:06:27  0:06:27 --:--:-- 3897k
      Downloading worker update...
      % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                     Dload  Upload   Total   Spent    Left  Speed
      0     0    0     0    0     0      0      0 --:--:--  0:00:02 --:--:--     0
    100 1807M  100 1807M    0     0  2312k      0  0:13:20  0:13:20 --:--:-- 7988k
      Done.

    Update will now be applied to the master installation,
    followed by worker installations on other nodes.

      Deleting old files...
      Extracting...
      Done.

    ===================================================
    Installing latest master dependencies.
    ===================================================

      Checking dependencies...
      Dependencies for python have changed - reinstalling...
      ------------------------------------------------------------------------

      Installing anaconda python...
      ------------------------------------------------------------------------
    PREFIX=/tem/scratch/<GroupDir>/.cryosparc/cryosparc_master/deps/anaconda
    Unpacking payload ...
    
    Solving environment: done

    ## Package Plan ##

      environment location: /tem/scratch/<GroupDir>/.cryosparc/cryosparc_master/deps/anaconda

      added / updated specs:
        - _libgcc_mutex==0.1=main
        - ca-certificates==2020.1.1=0
        - certifi==2020.4.5.1=py37_0
        - cffi==1.14.0=py37he30daa8_1
        - chardet==3.0.4=py37_1003
        - conda-package-handling==1.6.1=py37h7b6447c_0
        - conda==4.8.3=py37_0
        - cryptography==2.9.2=py37h1ba5d50_0
        - idna==2.9=py_1
        - ld_impl_linux-64==2.33.1=h53a641e_7
        - libedit==3.1.20181209=hc058e9b_0
        - libffi==3.3=he6710b0_1
        - libgcc-ng==9.1.0=hdf63c60_0
        - libstdcxx-ng==9.1.0=hdf63c60_0
        - ncurses==6.2=he6710b0_1
        - openssl==1.1.1g=h7b6447c_0
        - pip==20.0.2=py37_3
        - pycosat==0.6.3=py37h7b6447c_0
        - pycparser==2.20=py_0
        - pyopenssl==19.1.0=py37_0
        - pysocks==1.7.1=py37_0
        - python==3.7.7=hcff3b4d_5
        - readline==8.0=h7b6447c_0
        - requests==2.23.0=py37_0
        - ruamel_yaml==0.15.87=py37h7b6447c_0
        - setuptools==46.4.0=py37_0
        - six==1.14.0=py37_0
        - sqlite==3.31.1=h62c20be_1
        - tk==8.6.8=hbc83047_0
        - tqdm==4.46.0=py_0
        - urllib3==1.25.8=py37_0
        - wheel==0.34.2=py37_0
        - xz==5.2.5=h7b6447c_0
        - yaml==0.1.7=had09818_2
        - zlib==1.2.11=h7b6447c_3


    The following NEW packages will be INSTALLED:

      _libgcc_mutex      pkgs/main/linux-64::_libgcc_mutex-0.1-main
      ca-certificates    pkgs/main/linux-64::ca-certificates-2020.1.1-0
      certifi            pkgs/main/linux-64::certifi-2020.4.5.1-py37_0
      cffi               pkgs/main/linux-64::cffi-1.14.0-py37he30daa8_1
      chardet            pkgs/main/linux-64::chardet-3.0.4-py37_1003
      conda              pkgs/main/linux-64::conda-4.8.3-py37_0
      conda-package-han~ pkgs/main/linux-64::conda-package-handling-1.6.1-py37h7b6447c_0
      cryptography       pkgs/main/linux-64::cryptography-2.9.2-py37h1ba5d50_0
      idna               pkgs/main/noarch::idna-2.9-py_1
      ld_impl_linux-64   pkgs/main/linux-64::ld_impl_linux-64-2.33.1-h53a641e_7
      libedit            pkgs/main/linux-64::libedit-3.1.20181209-hc058e9b_0
      libffi             pkgs/main/linux-64::libffi-3.3-he6710b0_1
      libgcc-ng          pkgs/main/linux-64::libgcc-ng-9.1.0-hdf63c60_0
      libstdcxx-ng       pkgs/main/linux-64::libstdcxx-ng-9.1.0-hdf63c60_0
      ncurses            pkgs/main/linux-64::ncurses-6.2-he6710b0_1
      openssl            pkgs/main/linux-64::openssl-1.1.1g-h7b6447c_0
      pip                pkgs/main/linux-64::pip-20.0.2-py37_3
      pycosat            pkgs/main/linux-64::pycosat-0.6.3-py37h7b6447c_0
      pycparser          pkgs/main/noarch::pycparser-2.20-py_0
      pyopenssl          pkgs/main/linux-64::pyopenssl-19.1.0-py37_0
      pysocks            pkgs/main/linux-64::pysocks-1.7.1-py37_0
      python             pkgs/main/linux-64::python-3.7.7-hcff3b4d_5
      readline           pkgs/main/linux-64::readline-8.0-h7b6447c_0
      requests           pkgs/main/linux-64::requests-2.23.0-py37_0
      ruamel_yaml        pkgs/main/linux-64::ruamel_yaml-0.15.87-py37h7b6447c_0
      setuptools         pkgs/main/linux-64::setuptools-46.4.0-py37_0
      six                pkgs/main/linux-64::six-1.14.0-py37_0
      sqlite             pkgs/main/linux-64::sqlite-3.31.1-h62c20be_1
      tk                 pkgs/main/linux-64::tk-8.6.8-hbc83047_0
      tqdm               pkgs/main/noarch::tqdm-4.46.0-py_0
      urllib3            pkgs/main/linux-64::urllib3-1.25.8-py37_0
      wheel              pkgs/main/linux-64::wheel-0.34.2-py37_0
      xz                 pkgs/main/linux-64::xz-5.2.5-h7b6447c_0
      yaml               pkgs/main/linux-64::yaml-0.1.7-had09818_2
      zlib               pkgs/main/linux-64::zlib-1.2.11-h7b6447c_3


    Preparing transaction: done
    Executing transaction: done
    installation finished.
      ------------------------------------------------------------------------
        Done.
        anaconda python installation successful.
      ------------------------------------------------------------------------
      Extracting all conda packages...
      ------------------------------------------------------------------------
    ............................................................................
      ------------------------------------------------------------------------
        Done.
        conda packages installation successful.
      ------------------------------------------------------------------------
      Main dependency installation completed. Continuing...
      ------------------------------------------------------------------------
      Completed.
      Currently checking hash for mongodb
      Dependencies for mongodb have not changed.
      Completed dependency check.

    ===================================================
    Successfully updated master to version v4.1.0.
    ---
    Starting cryoSPARC System master process..
    CryoSPARC is not already running.
    database: started
    command_core: started
        command_core connection succeeded
        command_core startup successful
    command_vis: started
    command_rtp: started
        command_rtp connection succeeded
        command_rtp startup successful
    webapp: started
    app: started
    liveapp: started
    -----------------------------------------------------

    CryoSPARC master started.
    From this machine, access cryoSPARC at
        http://localhost:39030
    and access cryoSPARC Live at
        http://localhost:39036
    please note the legacy cryoSPARC Live application is running at
        http://localhost:39037

    From other machines on the network, access cryoSPARC at
        http://tem-cs-el7.sdfarm.kr:39030
    and access cryoSPARC Live at
        http://tem-cs-el7.sdfarm.kr:39036


    Startup can take several minutes. Point your browser to the address
    and refresh until you see the cryoSPARC web interface.

    ===================================================
    Now updating worker nodes.
    ===================================================

    All workers:
    ---------------------------------------------------
    Done updating all worker nodes.
    If any nodes failed to update, you can manually update them.
    Cluster worker installations must be manually updated.

    To update manually, copy the cryosparc_worker.tar.gz file into the
    cryosparc worker installation directory, and then run
        $ bin/cryosparcw update
    from inside the worker installation directory.

Or, you can update the master with a specific version.

.. code-block:: bash

    userid@tem-[cs|ui]-el7 $> cryosparcm update --version=vXX.YY.ZZ



After updating the master of your cryosparc instance, you should check the status of cryosparc daemons and stop them again in order to re-install the worker softwares.

.. code-block:: bash

    userid@tem-[cs|ui]-el7 $> cryosparcm status
    userid@tem-[cs|ui]-el7 $> cryosparcm stop

5. Cryosparc worker updates
---------------------------

Since we adopt the clustered installation method for cryosparc instances, we shoud manually update the cryosparc worker. 
But simply with cryosparc worker updates (guided from cryosparc official site), you might face up with the version mismatch problem of CUDA SDK runtime libraries (the root cause is unknwon now).
So we decide to newly install all the cryosparc worker softwares to address this issues.

If you successully update the cryosparc master softwares above, 
you must find **cryosparc_worker.tar.gz** tar ball in **~/.cryosparc/cryosparc_master** directory.

.. code-block:: bash

    userid@tem-[cs|ui]-el7 $> cd /tem/scratch/<GroupDir>/.cryosparc/cryosparc_master                  
    userid@tem-[cs|ui]-el7 $> ls -al *.tar.gz
    -rw-r-----. 1 userid userid  823226956 Apr 20 15:42 cryosparc_master.tar.gz
    -rw-r-----. 1 userid userid 1895278500 Apr 20 15:56 cryosparc_worker.tar.gz


First, modity the name of the previous worker directory to that with .orig postfix and copy/uncompress the worker tar ball to .cryosparc directory.


If your master installation directory is "cryosparc_master", use these commands.

.. code-block:: bash

    userid@tem-[cs|ui]-el7 $> cd /tem/scratch/<GroupDir>/.cryosparc
    userid@tem-[cs|ui]-el7 $> mv cryosparc_worker cryosparc_worker.orig
    userid@tem-[cs|ui]-el7 $> cp /tem/scratch/<GroupDir>/.cryosparc/cryosparc_master/cryosparc_worker.tar.gz /tem/scratch/<GroupDir>/.cryosparc
    userid@tem-[cs|ui]-el7 $> tar xvfz cryosparc_worker.tar.gz

 
Then, re-install all the cryosparc worker softwares with the followings (note that cryosparc version 3.2.0+ requires CUDA SDK 11.x+):

.. code-block:: bash

    userid@tem-[cs|ui]-el7 $> cd /tem/scratch/<GroupDir>/.cryosparc/cryosparc_worker          
    userid@tem-[cs|ui]-el7 $> eval $(cryosparcm env)
    userid@tem-[cs|ui]-el7 $> ./install.sh --license $CRYOSPARC_LICENSE_ID --cudapath /usr/local/cuda-11.2
    ******* CRYOSPARC SYSTEM: WORKER INSTALLER ***********************

    Installation Settings:
       License ID              : xxxxxxxxxxxx
       Root Directory          : /tem/scratch/<GroupDir>/.cryosparc/cryosparc_worker
       Standalone Installation : false
       Version                 : v4.1.0

    ******************************************************************

    CUDA check..
    Found nvidia-smi at /bin/nvidia-smi

    CUDA Path was provided as /usr/local/cuda-11.2
    Checking CUDA installation...
    Found nvcc at /usr/local/cuda-11.2/bin/nvcc
    The above cuda installation will be used but can be changed later.

    ******************************************************************

    Setting up hard-coded config.sh environment variables

    ******************************************************************

    Installing all dependencies.

    Warning: conda environment not found; this indicates that a cryoSPARC installation is either incomplete or in progress
    Checking dependencies...
    Dependencies for python have changed - reinstalling...
      ------------------------------------------------------------------------
      Installing anaconda python...
      ------------------------------------------------------------------------
    PREFIX=/tem/scratch/<GroupDir>/.cryosparc/cryosparc_worker/deps/anaconda
    Unpacking payload ...
    
    Solving environment: done

    ## Package Plan ##

      environment location: /tem/scratch/<GroupDir>/.cryosparc/cryosparc_worker/deps/anaconda

      added / updated specs:
        - _libgcc_mutex==0.1=main
        - ca-certificates==2020.1.1=0
        - certifi==2020.4.5.1=py37_0
        - cffi==1.14.0=py37he30daa8_1
        - chardet==3.0.4=py37_1003
        - conda-package-handling==1.6.1=py37h7b6447c_0
        - conda==4.8.3=py37_0
        - cryptography==2.9.2=py37h1ba5d50_0
        - idna==2.9=py_1
        - ld_impl_linux-64==2.33.1=h53a641e_7
        - libedit==3.1.20181209=hc058e9b_0
        - libffi==3.3=he6710b0_1
        - libgcc-ng==9.1.0=hdf63c60_0
        - libstdcxx-ng==9.1.0=hdf63c60_0
        - ncurses==6.2=he6710b0_1
        - openssl==1.1.1g=h7b6447c_0
        - pip==20.0.2=py37_3
        - pycosat==0.6.3=py37h7b6447c_0
        - pycparser==2.20=py_0
        - pyopenssl==19.1.0=py37_0
        - pysocks==1.7.1=py37_0
        - python==3.7.7=hcff3b4d_5
        - readline==8.0=h7b6447c_0
        - requests==2.23.0=py37_0
        - ruamel_yaml==0.15.87=py37h7b6447c_0
        - setuptools==46.4.0=py37_0
        - six==1.14.0=py37_0
        - sqlite==3.31.1=h62c20be_1
        - tk==8.6.8=hbc83047_0
        - tqdm==4.46.0=py_0
        - urllib3==1.25.8=py37_0
        - wheel==0.34.2=py37_0
        - xz==5.2.5=h7b6447c_0
        - yaml==0.1.7=had09818_2
        - zlib==1.2.11=h7b6447c_3


    The following NEW packages will be INSTALLED:

      _libgcc_mutex      pkgs/main/linux-64::_libgcc_mutex-0.1-main
      ca-certificates    pkgs/main/linux-64::ca-certificates-2020.1.1-0
      certifi            pkgs/main/linux-64::certifi-2020.4.5.1-py37_0
      cffi               pkgs/main/linux-64::cffi-1.14.0-py37he30daa8_1
      chardet            pkgs/main/linux-64::chardet-3.0.4-py37_1003
      conda              pkgs/main/linux-64::conda-4.8.3-py37_0
      conda-package-han~ pkgs/main/linux-64::conda-package-handling-1.6.1-py37h7b6447c_0
      cryptography       pkgs/main/linux-64::cryptography-2.9.2-py37h1ba5d50_0
      idna               pkgs/main/noarch::idna-2.9-py_1
      ld_impl_linux-64   pkgs/main/linux-64::ld_impl_linux-64-2.33.1-h53a641e_7
      libedit            pkgs/main/linux-64::libedit-3.1.20181209-hc058e9b_0
      libffi             pkgs/main/linux-64::libffi-3.3-he6710b0_1
      libgcc-ng          pkgs/main/linux-64::libgcc-ng-9.1.0-hdf63c60_0
      libstdcxx-ng       pkgs/main/linux-64::libstdcxx-ng-9.1.0-hdf63c60_0
      ncurses            pkgs/main/linux-64::ncurses-6.2-he6710b0_1
      openssl            pkgs/main/linux-64::openssl-1.1.1g-h7b6447c_0
      pip                pkgs/main/linux-64::pip-20.0.2-py37_3
      pycosat            pkgs/main/linux-64::pycosat-0.6.3-py37h7b6447c_0
      pycparser          pkgs/main/noarch::pycparser-2.20-py_0
      pyopenssl          pkgs/main/linux-64::pyopenssl-19.1.0-py37_0
      pysocks            pkgs/main/linux-64::pysocks-1.7.1-py37_0
      python             pkgs/main/linux-64::python-3.7.7-hcff3b4d_5
      readline           pkgs/main/linux-64::readline-8.0-h7b6447c_0
      requests           pkgs/main/linux-64::requests-2.23.0-py37_0
      ruamel_yaml        pkgs/main/linux-64::ruamel_yaml-0.15.87-py37h7b6447c_0
      setuptools         pkgs/main/linux-64::setuptools-46.4.0-py37_0
      six                pkgs/main/linux-64::six-1.14.0-py37_0
      sqlite             pkgs/main/linux-64::sqlite-3.31.1-h62c20be_1
      tk                 pkgs/main/linux-64::tk-8.6.8-hbc83047_0
      tqdm               pkgs/main/noarch::tqdm-4.46.0-py_0
      urllib3            pkgs/main/linux-64::urllib3-1.25.8-py37_0
      wheel              pkgs/main/linux-64::wheel-0.34.2-py37_0
      xz                 pkgs/main/linux-64::xz-5.2.5-h7b6447c_0
      yaml               pkgs/main/linux-64::yaml-0.1.7-had09818_2
      zlib               pkgs/main/linux-64::zlib-1.2.11-h7b6447c_3


    Preparing transaction: done
    Executing transaction: done
    installation finished.
      ------------------------------------------------------------------------
        Done.
        anaconda python installation successful.
      ------------------------------------------------------------------------
      Extracting all conda packages...
      ------------------------------------------------------------------------
    
      ------------------------------------------------------------------------
        Done.
        conda packages installation successful.
      ------------------------------------------------------------------------
      Preparing to install all pip packages...
      ------------------------------------------------------------------------
    Processing ./deps_bundle/python/python_packages/pip_packages/pycuda-2020.1.tar.gz
    Skipping wheel build for pycuda, due to binaries being disabled for it.
    Installing collected packages: pycuda
        Running setup.py install for pycuda ... done
    Successfully installed pycuda-2020.1
      ------------------------------------------------------------------------
        Done.
        pip packages installation successful.
      ------------------------------------------------------------------------
      Main dependency installation completed. Continuing...
      ------------------------------------------------------------------------
    Completed.
    Currently checking hash for ctffind
    Dependencies for ctffind have changed - reinstalling...
      ------------------------------------------------------------------------
      ctffind 4.1.10 installation successful.
      ------------------------------------------------------------------------
    Completed.
    Currently checking hash for cudnn
    Dependencies for cudnn have changed - reinstalling...
      ------------------------------------------------------------------------
      cudnn 8.1.0.77 for CUDA 11 installation successful.
      ------------------------------------------------------------------------
    Completed.
    Currently checking hash for gctf
    Dependencies for gctf have changed - reinstalling...
      ------------------------------------------------------------------------
      Gctf v1.06 installation successful.
      ------------------------------------------------------------------------
    Completed.
    Completed dependency check.

    ******* CRYOSPARC WORKER INSTALLATION COMPLETE *******************

    In order to run processing jobs, you will need to connect this
    worker to a cryoSPARC master.

    ******************************************************************


6. Running the new cryosparc instance
---------------------------------------

All the cryosparc master and worker updates has completed. So, you need to re-execute cryosparc instance daemons (assume userid's CRYOSPARC_BASE_PORT is 39030).

.. code-block:: bash

    userid@tem-[cs|ui]-el7 $> cd ~/
    userid@tem-[cs|ui]-el7 $> cryosparcm env
    userid@tem-[cs|ui]-el7 $> cryosparcm status
    userid@tem-[cs|ui]-el7 $> cryosparcm start

    Starting cryoSPARC System master process..
    CryoSPARC is not already running.
    database: started
    command_core: started
        command_core connection succeeded
        command_core startup successful
    command_vis: started
    command_rtp: started
        command_rtp connection succeeded
        command_rtp startup successful
    webapp: started
    app: started
    liveapp: started
    -----------------------------------------------------

    CryoSPARC master started. 
    From this machine, access cryoSPARC at
        http://localhost:39030
    and access cryoSPARC Live at
        http://localhost:39036
    please note the legacy cryoSPARC Live application is running at
        http://localhost:39037

    From other machines on the network, access cryoSPARC at
        http://tem-[cs|ui]-el7.sdfarm.kr:39030
    and access cryoSPARC Live at
        http://tem-[cs|ui]-el7.sdfarm.kr:39036


    Startup can take several minutes. Point your browser to the address
    and refresh until you see the cryoSPARC web interface.
