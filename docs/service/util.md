# Utilities for GSDC TEM Cluster

## **cluster.mydata**

Users can perform the following command (`cluster.mydata`) to check storage quota limit, usage ratio and so on. `cluster.mydata` tool is available on all the login nodes.

```bash
$> which cluster.mydata
/usr/local/bin/cluster.mydata
```

```bash
$> cluster.mydata
____ ____  ____   ____   _____ _____ __  __    ____ _           _
/ ___/ ___||  _ \ / ___| |_   _| ____|  \/  |  / ___| |_   _ ___| |_ ___ _ __
| |  _\___ \| | | | |       | | |  _| | |\/| | | |   | | | | / __| __/ _ \ '__|
| |_| |___) | |_| | |___    | | | |___| |  | | | |___| | |_| \__ \ ||  __/ |
\____|____/|____/ \____|   |_| |_____|_|  |_|  \____|_|\__,_|___/\__\___|_|

+ Official GSDC TEM Users Guide  : https://tem-docs.readthedocs.io/en/al9

+ Scratch/Home Quota Information : $> cluster.mydata
+ TEM Cluster Status Information : $> cluster.status
+------------------------------------------------------------------------+
+ Hostname............: tem-ui-al9.sdfarm.kr
+ OS Release..........: AlmaLinux release 9.5 (Teal Serval)
+ System Uptime.......: 20 days 0 hours 18 minutes 12 seconds
+ Users...............: Currently 2 user(s) logged on
+ Processes...........: 1123 running
+ CPU usage...........: 0.07, 0.13, 0.19 (1, 5, 15 min)
+ Memory (used/total).: 7699 MB / 384883 MB
+ Swap in use.........: 0 MB
+------------------------------------------------------------------------+
+ TEM Storage (used/total).......: 2.4 PBytes / 7.2 PBytes (34%)
+ Current User...................: <UserID>
* User Home Directory............: /tem/home/<UserID>
  ** Disk Quota Limit............: 0k
  ** Disk Usage..................: 19.87G
  ** Number of Files.............: 267373
* Group Scratch Directory........: /tem/scratch/<GroupDir>
  ** Disk Quota Limit............: 80T
  ** Disk Usage..................: 71.75T
  ** Number of Files.............: 5330260
+------------------------------------------------------------------------+
```

## **cluster.status**

Users can monitor the status and the usage ratio of all worker nodes with the following command (`cluster.status`).
`cluster.status` tool is available on all the login nodes.


```bash
$> which cluster.status
/usr/local/bin/cluster.status
```

```bash
$> cluster.status

        Current DateTime : 2025-06-18 09:49:22.880048
----------------------------------------------------------------------------------------------------------------------------------
NODE          QUEUE     STATE                    [GPU]T/U/F  [CPU]T/U/F  UTILIZATION                          [MEM]T/U/F(GB)
----------------------------------------------------------------------------------------------------------------------------------
tem-cpu00-al9  cpuQ      free                           n/a     28/25/3  [#########################---]       187.3/151.8/ 35.5
tem-cpu01-al9  cpuQ      free                           n/a     28/24/4  [########################----]       187.3/144.0/ 43.3
tem-cpu02-al9  cpuQ      free                           n/a     28/24/4  [########################----]       187.3/144.0/ 43.3
tem-cpu03-al9  cpuQ      free                           n/a     28/0/28  [----------------------------]       187.3/  0.0/187.3
tem-cpu04-al9  cpuQ      free                           n/a     28/0/28  [----------------------------]       187.3/  0.0/187.3
tem-cpu05-al9  cpuQ      free                           n/a     28/0/28  [----------------------------]       187.3/  0.0/187.3
tem-cpu06-al9  cpuQ      free                           n/a     28/0/28  [----------------------------]       187.3/  0.0/187.3
tem-cpu07-al9  cpuQ      free                           n/a     28/0/28  [----------------------------]       187.3/  0.0/187.3
tem-cpu08-al9  cpuQ      free                           n/a     28/0/28  [----------------------------]       187.3/  0.0/187.3
tem-cpu09-al9  cpuQ      free                           n/a     28/24/4  [########################----]       187.3/144.0/ 43.3
tem-cpu10-al9  cpuQ      free                           n/a     28/24/4  [########################----]       187.3/144.0/ 43.3
tem-cpu11-al9  cpuQ      free                           n/a     28/0/28  [----------------------------]       187.3/  0.0/187.3
tem-gpu01-al9  gpuQ      free       4/1/3 [#---] (a100.20g)     32/2/30  [##------------------------------]   376.1/ 23.4/352.6
tem-gpu02-al9  gpuQ      free       4/4/0 [####] (a100.20g)    32/10/22  [##########----------------------]   376.1/ 80.0/296.1
tem-gpu05-al9  gpuQ      free       4/0/4 [----] (v100.32g)     32/0/32  [--------------------------------]   375.6/  0.0/375.6
tem-gpu06-al9  gpuQ      free         2/1/1 [#-] (p100.16g)     28/2/26  [##--------------------------]       376.3/ 23.4/352.9
tem-gpu07-al9  gpuQ      free         2/2/0 [##] (p100.16g)     28/5/23  [#####-----------------------]       376.3/ 40.0/336.3
tem-gpu08-al9  gpuQ      free         2/2/0 [##] (p100.16g)     28/5/23  [#####-----------------------]       377.3/ 40.0/337.3
tem-gpu09-al9  gpuQ      free         2/2/0 [##] ( p40.24g)     28/5/23  [#####-----------------------]       124.0/ 40.0/ 84.0
tem-gpu10-al9  gpuQ      free         2/0/2 [--] ( p40.24g)     28/0/28  [----------------------------]       250.1/  0.0/250.1
tem-gpu11-al9  gpuQ      free   8/6/2 [######--] (a100.40g)    32/15/17  [###############-----------------]   375.6/120.0/255.6
tem-gpu12-al9  gpuQ      free   8/0/8 [--------] (a100.40g)     32/0/32  [--------------------------------]   375.6/  0.0/375.6
----------------------------------------------------------------------------------------------------------------------------------
        [CPU] Total 636 / Used 165 cores ( 25.94 % )
        [GPU] Total  38 / Used  18    ea ( 47.37 % )
----------------------------------------------------------------------------------------------------------------------------------
Enter 'f' to refresh TEM cluster status. (f)
Enter 'j' to display jobs with the refreshed cluster status. (j)
Enter 'q' to quit. (q)

 Select? (f/j/q) j
List of Jobs:

tem-ce-al9.sdfarm.kr:
                                                            Req'd  Req'd   Elap
Job ID          Username Queue    Jobname    SessID NDS TSK Memory Time  S Time
--------------- -------- -------- ---------- ------ --- --- ------ ----- - -----
11651.tem-ce-a* tem      cpuQ     cryosparc* 995567   1   1  8000m   --  R 00:25
11668.tem-ce-a* tem      gpuQ     cryosparc* 844481   1   2   24gb   --  R 00:08
11669.tem-ce-a* tem      gpuQ     cryosparc* 27201*   1   2   24gb   --  R 00:07
11670.tem-ce-a* tem      gpuQ     run_submi* 356861   4  20  160gb   --  R 00:06
11671.tem-ce-a* tem      gpuQ     run_submi* 442473   4  20  160gb   --  R 00:06
11672.tem-ce-a* tem      cpuQ     run_submi* 10004*   5 120  720gb   --  R 00:00

* NODE  : CPU 또는 GPU 장치를 가진 계산서버 이름
* QUEUE : 각 서버가 속한 큐 이름
* STATE
    - free : 계산서버에 CPU 또는 GPU 작업이 할당되어 실행중이나, 해당 서버의 모든 자원을 할당받은 상태는 아님
    - job-busy : 계산서버에 작업들이 할당되어 실행중이고, 작업들이 모든 자원을 할당받아 busy 한 상태
    - offline : 작업들이 할당되어 실행중이나, 새로운 작업들은 할당되지 않을 예정인 상태 (예, 장애, 재부팅 등 관리모드 전환)
    - down : 장애발생으로 계산서버가 가용하지 못한 상태
* [GPU] T/U/F : 각 GPU 계산서버에 설치된 GPU 카드 총 개수, 사용중인 개수(#), 유휴 카드 개수(-)
* [CPU] T/U/F : 각 CPU 계산서버의 총 코어 개수, 사용중인 개수(#), 유휴 코어 개수(-)
* [MEM] T/U/F : 각 계산서버의 총 메모리 양, 사용중인 양, 유휴 양 (GB단위)
```

## **TMUX**

Tmux is a terminal multiplexer. It allows you to create several "pseudo terminals (sessions)" from a single terminal. 
This is very useful for running multiple programs with a single connection, such as when you're remotely connecting to a machine using Secure Shell (SSH).

Tmux also decouples your programs from the main terminal, protecting them from accidentally disconnecting. You can detach tmux from the current terminal, 
and all your programs will continue to run safely in the background. Later, you can reattach tmux to the same or a different terminal.

### **Get started with tmux**

When you login-in the login server, a tmux session will be created by default for your convenience.
If the default session is not activated, type `tmux` in order to start using tmux. This command launches a tmux server, creates a session with a single window, and attaches to it.   

![alt text](../images/tmux-1.png)
/// caption
Default tmux session (session number is 22 in this example)
///

### **Listing all the tmux sessions**

To list all the tmux sessions created by an user, type **`tmux ls`**.

```bash
$> tmux ls
2: 9 windows (created Tue Mar 11 12:35:06 2025) (attached)
21: 1 windows (created Thu Mar 20 09:21:30 2025)
22: 1 windows (created Thu Mar 20 13:02:43 2025) (attached)
```

### **Switching between tmux sessions or windows**

Tmux operates using a series of keybindings (keyboard shortcuts) triggered by pressing the **prefix** combination.

By default, the prefix is **`Ctrl+b`**. After that, for instance, press **`c`** to create a new window in the current session.

To traverse between tmux sessions (or windows), press **`Ctrl+b`** and **`w`**.

```bash
(0)   - 2: 9 windows (attached)
(1)   ├─> 1: USERID@tem-cs-al9:/tem/home/USERID(bash)~: "tem-cs-al9.sdfarm.kr"
(2)   ├─> 2: USERID@tem-cs-al9:/tem/home/USERID(bash)~: "tem-cs-al9.sdfarm.kr"
(3)   ├─> 3: USERID@tem-cs-al9:/tem/home/USERID(bash)~: "tem-cs-al9.sdfarm.kr"
(4)   ├─> 4: USERID@tem-cs-al9:/tem/home/USERID(bash)~*: "tem-cs-al9.sdfarm.kr"
(5)   ├─> 5: USERID@tem-ce-al9:/tem/el9/applications(bash)~: "tem-cs-al9.sdfarm.kr"
(6)   ├─> 6: USERID@tem-cs-al9:/tem/home/USERID(bash)~: "tem-cs-al9.sdfarm.kr"
(7)   ├─> 7: USERID@tem-cs-al9:/tem/home/USERID(bash)~: "tem-cs-al9.sdfarm.kr"
(8)   ├─> 8: USERID@tem-cs-al9:/tem/home/USERID(python ./pbspro_client.py)#~: "tem-cs-al9.sdfarm.kr"
(9)   └─> 9: USERID@tem-cs-al9:/tem/home/USERID(bash)~-: "tem-cs-al9.sdfarm.kr"
(M-a) - 21: 1 windows
(M-b) └─> 1: USERID@tem-cs-al9:/tmp(bash)~*: "tem-cs-al9.sdfarm.kr"
(M-c) - 22: 1 windows (attached)
(M-d) └─> 1: USERID@tem-cs-al9:/tem/home/USERID(bash)*: "tem-cs-al9.sdfarm.kr"
```


### **Useful keybindings**

Tmux provides several keybindings to execute commands quickly in a tmux session. Here are some of the most useful ones.

```bash
Tmux prefix key: Ctrl-b
Key bindings after prefix:
    - ? : Show key bindings except copy-mode keys
    - / : Show key bindings
    - c : New window
    - w : Choose window tree
    - % : Dynamic split window
    - ' : Horizontal split window
    - - : Vertical split window
    - z : Zoom pane
    - \ : Dump current pane to file at home
    - | : Pipe current pane output to file at home
    - Alt-s : Synchronize panes
    - Alt-m : Toggle mouse use (on, off)
    - Alt-x : Kill current pane
    - Alt-Shift-X : Kill current window
    - Alt-Ctrl-x : Kill current session
    - ` : Switch to app launcher
    - ? : Show man
    - m : Show MOTD
```