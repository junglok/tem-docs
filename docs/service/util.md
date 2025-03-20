# Utilities for GSDC TEM Cluster

## **TMUX**

Tmux is a terminal multiplexer. It allows you to create several "pseudo terminals" from a single terminal. 
This is very useful for running multiple programs with a single connection, such as when you're remotely connecting to a machine using Secure Shell (SSH).

Tmux also decouples your programs from the main terminal, protecting them from accidentally disconnecting. You can detach tmux from the current terminal, and all your programs will continue to run safely in the background. Later, you can reattach tmux to the same or a different terminal.

### Get stared with tmux

When you login-in the login servers, a tmux session will be created by default for your convenience.
If the default session is not activated, type `tmux` in order to start using tmux. This command launches a tmux server, creates a session with a single window, and attaches to it.   

![alt text](../images/tmux-1.png)
/// caption
Default tmux session (session number is 22 in this example)
///
