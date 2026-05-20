# Conda Environment Configuration Guide

## Overview

The system-wide Conda installation is located at:

```
/tem/al9/system/miniconda3-py312_25.1.1-2
```

The default `envs` directory is **read-only** and managed by the system administrator:

```
/tem/al9/system/miniconda3-py312_25.1.1-2/envs
```

To create and manage your own Conda environments, you must add a writable `envs` directory under your group's scratch space. This guide explains how to configure it.

---

## Directory Structure

| Path | Description |
|------|-------------|
| `/tem/al9/system/miniconda3-py312_25.1.1-2` | System Conda installation (read-only) |
| `/tem/al9/system/miniconda3-py312_25.1.1-2/envs` | System default envs directory (read-only) |
| `/tem/home/<UserID>` | Your home directory |
| `/tem/scratch/<GroupDir>` | Your group's scratch directory |
| `/tem/scratch/<GroupDir>/envs` | **Recommended location for your group's environments** |

> Replace `<UserID>` with your actual user ID and `<GroupDir>` with your group's scratch directory name.

---

## Step 1: Load the Conda Module

Before using Conda, load the module:

```bash
module load miniconda3/py312_25.1.1-2
```

Verify that Conda is available:

```bash
conda --version
# conda 25.1.1
```

---

## Step 2: Create the Group Envs Directory

Create the `envs` directory under your group's scratch space if it does not already exist:

```bash
mkdir -p /tem/scratch/<GroupDir>/envs
```

> **Note:** This directory is shared within your group. Coordinate with your group members to avoid naming conflicts when creating environments.

---

## Step 3: Add the Custom Envs Directory to Conda Config

Register the group `envs` directory as an additional environment path using `conda config`:

```bash
conda config --add envs_dirs /tem/scratch/<GroupDir>/envs
```

Verify the configuration was applied:

```bash
conda config --show envs_dirs
```

Expected output:

```
envs_dirs:
  - /tem/scratch/<GroupDir>/envs
  - /tem/al9/system/miniconda3-py312_25.1.1-2/envs
```

> The newly added path is prepended to the list, so Conda will search it **first** when looking up environments.

---

## Step 4: Create a Conda Environment

Create a new environment in your group's `envs` directory:

```bash
conda create --prefix /tem/scratch/<GroupDir>/envs/<env-name> python=3.12
```

Or, since the directory is already registered, you can use the shorthand `--name` option:

```bash
conda create --name <env-name> python=3.12
```

> When using `--name`, Conda will automatically place the environment in the first writable path listed in `envs_dirs` — which is `/tem/scratch/<GroupDir>/envs`.

---

## Step 5: Activate and Use the Environment

Activate the environment by name:

```bash
conda activate <env-name>
```

Or by full path:

```bash
conda activate /tem/scratch/<GroupDir>/envs/<env-name>
```

Deactivate when done:

```bash
conda deactivate
```

### If the Active Environment Name Is Not Shown in the Prompt

After activation, the shell prompt should display the active environment name, for example:

```
(<env-name>) [user@hostname ~]$
```

If the environment name does **not** appear in your prompt, set the following environment variable before activating:

```bash
export BASH_POWERLINE=yes
conda activate <env-name>
```

To make this setting persistent across sessions, add it to your `~/.bashrc`:

```bash
echo 'export BASH_POWERLINE=yes' >> ~/.bashrc
source ~/.bashrc
```

---

## Step 6: List Available Environments

```bash
conda env list
```

Example output:

```
# conda environments:
#
base                  /tem/al9/system/miniconda3-py312_25.1.1-2
<env-name>         *  /tem/scratch/<GroupDir>/envs/<env-name>
```

---

## Removing a Custom Envs Directory from Config

If you need to remove the custom path from your Conda configuration:

```bash
conda config --remove envs_dirs /tem/scratch/<GroupDir>/envs
```

---

## Notes and Best Practices

- **Module must be loaded first.** Always run `module load miniconda3/py312_25.1.1-2` before using Conda in a new shell session. Consider adding it to your `~/.bashrc` or job script.
- **The `conda config` change is persistent.** It is saved to `~/.condarc` in your home directory and applies to all future sessions automatically.
- **Do not install packages into the base environment.** The base environment is system-managed and read-only. Always create and activate a dedicated environment.
- **Disk quota.** Conda environments can be large. Monitor your group's scratch usage periodically:

  ```bash
  cluster.mydata
  ```
