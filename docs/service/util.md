# Utilities for GSDC TEM Cluster

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

### **Traversing between tmux sessions or windows**

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
    (M-c) - 23: 1 windows (attached)
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