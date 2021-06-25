****
FAQs
****

* `how to resolve the problems on (re)starting your own cryosparc instance`_
* `how to repair cryosparc database corruption caused by duplicated mongod executions`_  

.. _how to resolve the problems on (re)starting your own cryosparc instance:

How to resolve the problems on (re)starting your own cryosparc instance?
------------------------------------------------------------------------

You should check all the cryosparc related processes (i.e., supervisord, mongod, command_core, command_vis, command_rtp, webapp, app, liveapp) to be terminated successfully first on **tem-cs-el7.sdfarm.kr** server.

.. code-block:: bash

    (log-in tem-cs-el7 first)
    (example) userid@tem-cs-el7 $> cryosparcm stop

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

    (example) userid@tem-cs-el7 $>  ps aux | grep <userid> | grep cryosparc
    userid    2449  0.0  0.0 152792 17480 ?        Ss   Jun24   0:18 python /tem/home/userid/.cryosparc/cryosparc2_master/deps/anaconda/envs/cryosparc_master_env/bin/supervisord -c /tem/home/userid/.cryosparc/cryosparc2_master/supervisord.conf
    userid    2472  1.2  0.0 1429268 57412 ?       Sl   Jun24  13:19 mongod --dbpath /tem/home/userid/.cryosparc/cryosparc_database --port 39031 --oplogSize 64 --replSet meteor --nojournal --wiredTigerCacheSizeGB 4
    userid    2900  0.2  0.0 860572 83028 ?        Sl   Jun24   2:23 python -c import cryosparc_command.command_core as serv; serv.start(port=39032)
    userid    4332  0.1  0.1 854192 236396 ?       Sl   Jun24   1:53 python -c import cryosparc_command.command_vis as serv; serv.start(port=39033)
    userid    4378  0.4  0.0 1190536 196316 ?      Sl   Jun24   4:59 python -c import cryosparc_command.command_rtp as serv; serv.start(port=39035)
    userid    5586  0.1  0.0 1331136 116972 ?      Sl   Jun24   1:17 /tem/home/userid/.cryosparc/cryosparc2_master/cryosparc_webapp/nodejs/bin/node ./bundle/main.js
    userid    5625  0.1  0.0 1049868 97640 ?       Sl   Jun24   1:22 /tem/home/userid/.cryosparc/cryosparc2_master/cryosparc_app/nodejs/bin/node ./bundle/main.js
    userid    5690  0.2  0.0 1326136 81432 ?       Sl   Jun24   2:12 /tem/home/userid/.cryosparc/cryosparc2_master/cryosparc_liveapp/nodejs/bin/node ./bundle/main.js

    (example) userid@tem-cs-el7 $> kill -9 2449 2472 2900 4332 4378 5586 5625 5690


Second, find your own cryosparc unix socket files on /tmp directory, and if exists, delete the files using rm command.

.. code-block:: bash

    userid@tem-cs-el7 $> cd /tmp
    (example) userid@tem-cs-el7 $> ls -al | grep <userid> | grep sock
   
    srwx------.  1 test02       test02          0 Jun 24 16:39 cryosparc-supervisor-627a9991e2f2f069094732dfd78d1696.sock
    srwx------.  1 test02       test02          0 Jun 24 16:39 mongodb-39031.sock

    (example) userid@tem-cs-el7 $> rm cryosparc-supervisor-627a9991e2f2f069094732dfd78d1696.sock
    (example) userid@tem-cs-el7 $> rm mongodb-39031.sock 



Then, start your cryosparc instance.

.. code-block:: bash

    (example) userid@tem-cs-el7 $> cryosparcm start

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


 
.. _how to repair cryosparc database corruption caused by duplicated mongod executions:  

With duplicated mongod executions, cryosparc database can be corrupted resulting in **"database: ERROR (spawn error)"** on (re)starting cryosparc instance. To address this abnormal case, you can try to repair the database with followings:

First, **stop all the cryosparc processes and delete the unix socket files.** See `how to resolve the problems on (re)starting your own cryosparc instance`_  for more details.

Second, try to repair the cryosparc database i.e., mongodb.

.. code-block:: bash

    userid@tem-cs-el7 $> cryosparcm env
    userid@tem-cs-el7 $> cd .cryosparc
    userid@tem-cs-el7 $> tar cvfz cryosparc_database.backup.tar.gz cryosparc_database
    userid@tem-cs-el7 $> eval $(cryosparcm env) 
    userid@tem-cs-el7 $> cd cryosparc_database
    userid@tem-cs-el7 $> mongod --dbpath ./ --repair
 
 
  
