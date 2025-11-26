# Globus Connect Personal – Installation & Data Transfer Guide

Globus Connect Personal (GCP) lets you turn your own laptop or desktop (Windows, macOS, or Linux) into a Globus collection, so you can move data to and from institutional (e.g., KISTI GSDC) storage using the Globus Web App.  ￼

This guide shows how to:

1.	Install GCP on Windows, macOS, and Linux

2.	Create a personal collection on your computer

3.	Make local folders accessible

4.	Transfer files between your PC and a remote Globus collection


## 1. Overview & Concepts

- **Globus Web App** – Web interface at `https://app.globus.org` used to manage collections and transfers.  
- **Collection** – A named location (endpoint) that Globus can access. Your laptop with GCP installed becomes a *personal collection*.  
- **Globus Connect Personal (GCP)** – Lightweight client that runs under your user account and connects your local filesystem to Globus. Available for:
  - macOS 10.13+  
  - Currently supported Windows versions  
  - Common x86 Linux distributions  

GCP is free to install and use for users at non‑profit research and education institutions.  

---

## 2. Prerequisites

Before installation, you should have:

1. **A Globus account / identity**

   You can log in with:
   - Your institution (university / lab) single sign-on  
   - Or Google, ORCID, GitHub, or a Globus ID account  

   ![Globus login screen](https://docs.globus.org/guides/tutorials/manage-files/images/transfer-files/login-1.png)

2. **A remote Globus collection to transfer to/from**

   - Typically an institutional (e.g., KISTI GSDC) collection on an HPC/HTC cluster or storage system.  
   - KISTI GSDC collection name for TEM : **TEM_Collection@KISTI-GSDC**

3. **Permissions on your own computer**

   - Ability to install software in some directory you can write to (does *not* have to be system-wide Program Files, etc.).  

---

## 3. Install Globus Connect Personal on Windows

> Works on currently supported Windows versions.  

### 3.1 Download

1. Visit the Globus Connect Personal page: `https://www.globus.org/globus-connect-personal`.  
2. Click **Install now** for Windows (or follow your institution’s documentation link).  
3. On the download page, click **Download Globus Connect Personal for Windows**.  

   ![Download Globus Connect Personal for Windows](https://docs.globus.org/globus-connect-personal/install/images/gcp-download-win.png)

### 3.2 Run the Installer

1. Double‑click the downloaded installer (`GlobusConnectPersonal-x.y.z.exe`).  
2. If you are the only user and have administrator rights, you can accept the default install location and click **Install**.  
3. If you **don’t** have admin privileges or want a different location:
   - Click **Browse**  
   - Choose a directory you can write to (e.g., `C:\Users\<you>\Apps\GlobusConnectPersonal`)  
   - Continue with installation.  

After installation, GCP launches automatically and shows a **Log In** button.  

---

## 4. Install Globus Connect Personal on macOS

> Requires macOS 10.13 or higher.  

### 4.1 Download

1. Go to `https://www.globus.org/globus-connect-personal`.  
2. Under **Globus Connect Personal for Mac**, click **Install now**.  
3. On the download page, click **Download Globus Connect Personal for Mac** to get a `.dmg` file.  

   ![Download Globus Connect Personal for Mac](https://docs.globus.org/globus-connect-personal/install/images/gcp-download-mac.png)

### 4.2 Install the App

1. Open the downloaded `.dmg` file.  
2. Drag **Globus Connect Personal** into the **Applications** folder.  
3. Open **Finder → Applications**, then double‑click **Globus Connect Personal** to launch it.  

GCP will show a **Log In** button for the first-time setup.

---

## 5. Install Globus Connect Personal on Linux

> Supports common x86 GNU/Linux distributions.  

### 5.1 Optional GUI Prerequisite

If you want to use the graphical interface, install Tcl/Tk:  

```bash
# Ubuntu / Debian / Linux Mint
sudo apt-get install tk tcllib

# Fedora / CentOS / RHEL
sudo yum install tk tcllib

# openSUSE
sudo zypper install tk tcllib
```

Without Tcl/Tk you can still use GCP in command‑line mode only.

### 5.2 Download & Extract

You can either use a browser via the install page or download directly:

```bash
# Download latest release
wget https://downloads.globus.org/globus-connect-personal/linux/stable/globusconnectpersonal-latest.tgz

# Extract
tar xzf globusconnectpersonal-latest.tgz

# Change into the extracted directory (replace x.y.z with the version)
cd globusconnectpersonal-x.y.z
```

### 5.3 First Launch

Run:

```bash
./globusconnectpersonal
```

The first run walks you through setup (GUI or text prompts depending on environment).  

Later, you can start it in the background:

```bash
./globusconnectpersonal -start &
```

## 6. First-Time Setup & Collection Creation

These steps are similar on all platforms.

1. **Click “Log In” in the GCP window**

   - GCP opens your default browser to complete authentication.

2. **Authenticate with Globus**

   - Choose your organization or another identity provider, and log in.
   - If asked, consent to allow GCP/Globus to use your identity.

3. **Grant GCP permissions**

   - You’ll see a consent page requesting permission for GCP to create and manage a personal collection on your behalf.  
   - Click **Allow**.  

4. **Configure your collection**

   You’ll be asked to provide:

   - **Collection display name** – e.g., `MyLaptop`, `Lab-PC-01`, or something your users will recognize.  
   - **Description** (optional).  
   - **Default directory** – typically your home directory.

5. **Finish setup**

   - After setup completes, GCP starts running and connects to the Globus service.  
   - You’ll see a Globus icon:
     - **Windows:** in the system tray / taskbar.  
     - **macOS:** in the menu bar (top of the screen).  
     - **Linux:** GUI status window or CLI messages; you can check status via `./globusconnectpersonal -status`.  

At this point, your PC is a Globus collection and can be used in the Web App.

---

## 7. Make Local Folders Accessible for Transfer

By default, only a limited part of your filesystem (typically your home directory) is accessible to Globus. To upload/download to other paths (e.g., external drives), you must explicitly allow them.  

> **Security tip:** Only expose folders that actually need to be accessed via Globus.

### 7.1 Windows – Accessible Folders

1. Right‑click the **Globus** icon in the taskbar and choose **Options…**.  
2. In the **Access** tab:
   - You’ll see your home directory listed by default.  
   - Click **+** to add more folders (e.g., `D:\data\project1`).  
   - Optionally tick **Sharable** if your institution has a Globus subscription that allows creating guest collections.  

   ![Windows File Manager (example environment)](https://docs.globus.org/guides/tutorials/manage-files/images/transfer-files/filemgr-1.png)

3. **Path syntax from Globus:**
   - `/~/` maps to your Windows home directory (e.g., `C:\Users\yourname`).  
   - `/C/path/to/dir` corresponds to `C:\path\to\dir` and so on.  

### 7.2 macOS – Accessible Directories

1. Click the **Globus** icon in the menu bar → **Preferences…**.  
2. In **Access**:
   - Your home directory (e.g., `/Users/yourname`) is allowed by default.  
   - Click **+** to add additional directories.  
   - You can choose whether each directory is sharable (requires a subscription for sharing).  

### 7.3 Linux – Accessible Directories (config file)

On Linux, you can manage accessible paths via the GUI (if Tcl/Tk is installed) or via the config file:  

- Paths and permissions are stored in `~/.globusonline/lta/config-paths` as CSV:

```text
<path>,<sharing flag>,<R/W flag>
~/,0,1
/data/project,0,1
```

- `sharing flag` – `1` allow sharing, `0` disable  
- `R/W flag` – `1` read/write, `0` read‑only  

After editing `config-paths`, restart GCP:

```bash
./globusconnectpersonal -stop
./globusconnectpersonal -start &
```

---

## 8. Transfer Data with the Globus Web App

Once GCP is installed, running, and configured, users can transfer files using any browser.

### 8.1 Log In to Globus

1. Go to **https://app.globus.org** (or visit `https://www.globus.org` and click **Login**).  
2. Log in with your institution or other identity.  

### 8.2 Open the File Manager

After login you land on the **File Manager** page.

![Globus File Manager – empty state](https://docs.globus.org/guides/tutorials/manage-files/images/transfer-files/filemgr-1.png)

### 8.3 Select Your Personal Collection

1. In the **Collection** field, type the name you gave your PC’s collection (e.g., `MyLaptop`).  
2. Select it from the list; Globus connects and shows the default path (e.g., `/~/`).  

### 8.4 Select the Remote Collection

You can run File Manager in **two‑panel mode**:

1. Click **Transfer or Sync to…** on the right side to open a second panel.  
2. In the right panel’s **Collection** field, search for your remote collection (e.g., your HPC system’s Globus collection).  
3. Navigate to the directory you’re allowed to read/write.

![Two‑panel File Manager with Transfer or Sync to…](https://docs.globus.org/guides/tutorials/manage-files/images/transfer-files/filemgr-5.png)

### 8.5 Start a Transfer

To **upload from your PC to the remote system**:

1. Left panel: your **personal collection** (GCP)  
   - Navigate to the folder and select the files/directories you want to transfer.  
2. Right panel: **remote collection** (HPC / storage)  
   - Navigate to the destination directory.  
3. Click **Start** above the panel that represents the *destination* (depends on UI layout).  

To **download from the remote collection to your PC**, reverse which side is source/destination.

Globus will:

- Queue the transfer  
- Automatically retry on network glitches  
- Verify file integrity with checksums by default.  

![Transfer request submitted](https://docs.globus.org/guides/tutorials/manage-files/images/transfer-files/filemgr-7.png)

### 8.6 Monitor Transfer Status

1. Click **Activity** in the left navigation to see current and past transfers.  
2. Click a transfer’s details icon to see per‑file status and error messages if any.  
3. You will also receive email notifications when transfers finish or fail.

Even if you close your browser or log out, the transfer continues on the Globus service side.  

---

## 9. Tips & Troubleshooting

### 9.1 Common Issues

- **“Path not allowed” or missing folders in File Manager**

  - Ensure the folder is added to Accessible Folders/Directories (Windows/macOS) or `config-paths` (Linux).  
  - Confirm your OS user has permission to read/write that folder locally.

- **Install permission errors (e.g., can’t write to `C:\Program Files`)**

  - Install into a directory you own (e.g., your home directory).  

- **GCP icon shows “Not Connected”**

  - A firewall or network rule may be blocking connections to the Globus service.  
  - Try a different network (home vs campus VPN) or contact your IT staff with the Globus firewall requirements documentation.  

- **Browser login cannot be started from GCP**

  - Some security tools block launching a browser. In that case, you can use a **GCP Setup Key** as described in the troubleshooting guide.  

### 9.2 Advanced (Windows) – Very Long Paths

If you are working with extremely deep directory structures or very long filenames on Windows, you may need to enable **long path support** in the OS registry for GCP to handle paths up to 4096 characters. This change requires admin rights and a reboot; see the Windows GCP install documentation for details.  

### 9.3 Official Help

- **Main GCP docs (Windows/macOS/Linux)** – detailed installation & configuration.  
- **“How to Log In and Transfer Files” tutorial** – step‑by‑step File Manager walkthrough.  
- **GCP Troubleshooting Guide** – in‑depth help for install, firewall, and permission problems.  