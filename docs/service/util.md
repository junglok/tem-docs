# Utilities for GSDC TEM Cluster

## **TMUX**

Tmux is a terminal multiplexer. It allows you to create several "pseudo terminals" from a single terminal. 
This is very useful for running multiple programs with a single connection, such as when you're remotely connecting to a machine using Secure Shell (SSH).

Tmux also decouples your programs from the main terminal, protecting them from accidentally disconnecting. You can detach tmux from the current terminal, and all your programs will continue to run safely in the background. Later, you can reattach tmux to the same or a different terminal.

### Get started with tmux

When you login-in the login servers, a tmux session will be created by default for your convenience.
If the default session is not activated, type `tmux` in order to start using tmux. This command launches a tmux server, creates a session with a single window, and attaches to it.   

![alt text](../images/tmux-1.png)
/// caption
Default tmux session (session number is 22 in this example)
///

### Useful keybindings

Tmux operates using a series of keybindings (keyboard shortcuts) triggered by pressing the **prefix** combination.

By default, the prefix is **`Ctrl+B`**. After that, for instance, press `c` to create a new window in the current session.

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