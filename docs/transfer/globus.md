# **Globus Connect Personal – Installation & Data Transfer Guide**

Globus Connect Personal (GCP) turns your own workstation or desktop (Windows, macOS, or Linux) into a Globus collection, so you can move data to and from institutional storage (e.g., KISTI GSDC) using the Globus Web App.

This guide shows how to:

1.	Install GCP on Windows, macOS, and Linux

2.	Create a personal collection on your computer

3.	Make local folders accessible

4.	Transfer files between your PC and a remote Globus collection


## **Overview & Concepts**

- **Globus Web App** – the web interface at [https://app.globus.org](https://app.globus.org) for managing collections and transfers.  
- **Collection** – a named location (endpoint) Globus can access. Once GCP is installed, your workstation becomes a *personal collection*.  
- **Globus Connect Personal (GCP)** – a lightweight client that runs under your user account and connects your local filesystem to Globus. Available for:
    - macOS 10.13+  
    - Currently supported Windows versions  
    - Common x86 Linux distributions  

GCP is free for users at non‑profit research and education institutions.  

---

## **Prerequisites**

Before installation, you should have:

### 1. A Globus account/identity

You can log in [https://app.globus.org](https://app.globus.org) with:
  
  - Your institution (university / lab) single-sign-on (SSO) 
  - Or Google, ORCID, GitHub, or a Globus ID account

![Globus login screen](https://docs.globus.org/guides/tutorials/manage-files/images/transfer-files/login-1.png)

### 2. A remote Globus collection to transfer to/from

   - Typically an institutional collection (e.g., KISTI GSDC) on a data computing cluster or storage system.  
   - KISTI GSDC collection name for TEM: **`TEM_Collection@KISTI-GSDC`**

### 3. Permissions on your own computer

   - Ability to install software into any directory you can write to (it doesn't need to be a system-wide location like Program Files).  

---

## **Install Globus Connect Personal on Windows**

### 1. Download

1. Visit the Globus Connect Personal page: [https://www.globus.org/globus-connect-personal](https://www.globus.org/globus-connect-personal).  
2. Click **Install now** for Windows (or follow your institution’s documentation link).  
3. On the download link, click **Download Globus Connect Personal for Windows**.  

   ![Download Globus Connect Personal for Windows](https://docs.globus.org/globus-connect-personal/install/images/gcp-download-win.png)

### 2. Run the Installer

1. Double‑click the downloaded installer (`GlobusConnectPersonal-x.y.z.exe`).  
2. If you're the only user and have administrator rights, accept the default install location and click **Install**.  
3. If you don't have admin privileges, or want a different location:
   - Click **Browse**  
   - Choose a directory you can write to (e.g., `C:\Users\<you>\Apps\GlobusConnectPersonal`)  
   - Continue the installation.  

After installation, GCP launches automatically and shows a **Log In** button.  

---

## **Install Globus Connect Personal on macOS**

### 1. Download

1. Go to [https://www.globus.org/globus-connect-personal](https://www.globus.org/globus-connect-personal).  
2. Under **Globus Connect Personal for Mac**, click **Install now**.  
3. On the download link, click **Download Globus Connect Personal for Mac** to get a `.dmg` file.  

   ![Download Globus Connect Personal for Mac](https://docs.globus.org/globus-connect-personal/install/images/gcp-download-mac.png)

### 2. Install the App

1. Open the downloaded `.dmg` file.  
2. Drag **Globus Connect Personal** into the **Applications** folder.  
3. Open **Finder → Applications** and double‑click **Globus Connect Personal** to launch it.  

GCP shows a **Log In** button for first-time setup.

---

## **Install Globus Connect Personal on Linux**

### 1. GUI Prerequisite (Optional)

If you want to use the graphical interface, install Tcl/Tk:  

```bash
# Ubuntu / Debian / Linux Mint
sudo apt-get install tk tcllib

# Fedora / CentOS / RHEL
sudo yum install tk tcllib

# openSUSE
sudo zypper install tk tcllib
```

Without Tcl/Tk, GCP still works in command‑line mode only.

### 2. Download & Extract

You can either use a browser via the install page or download directly:

```bash
# Download latest release
wget https://downloads.globus.org/globus-connect-personal/linux/stable/globusconnectpersonal-latest.tgz

# Extract
tar xzf globusconnectpersonal-latest.tgz

# Change into the extracted directory (replace x.y.z with the version)
cd globusconnectpersonal-x.y.z
```

### 3. First Launch

Run:

```bash
./globusconnectpersonal
```

The first run walks you through setup (GUI or text prompts, depending on your environment).  

Later, start it in the background with:

```bash
./globusconnectpersonal -start &
```

## **First-Time Setup & Collection Creation**

These steps are similar on all platforms.

1. **Click "Log In" in the GCP window**

   - GCP opens your default browser to complete authentication.

2. **Authenticate with Globus**

   - Choose your organization or another identity provider and log in.
   - If asked, consent to let GCP/Globus use your identity.

3. **Grant GCP permissions**

   - A consent page will ask permission for GCP to create and manage a personal collection on your behalf.  
   - Click **Allow**.  

4. **Configure your collection**

   You'll be asked to provide:

   - **Collection display name** – e.g., `MyWorkStation`, `Lab-PC-01`, or something recognizable.  
   - **Description** (optional).  
   - **Default directory** – typically your home directory.

5. **Finish setup**

   - Once setup completes, GCP starts running and connects to the Globus service.  
   - You'll see a Globus icon:
     - **Windows:** in the system tray / taskbar.  
     - **macOS:** in the menu bar (top of the screen).  
     - **Linux:** GUI status window or CLI messages; you can check status via `./globusconnectpersonal -status`.  

At this point, your PC is a Globus collection and can be used in the Web App.

---

## **Make Local Folders Accessible for Transfer**

By default, Globus can only access a limited part of your filesystem (typically your home directory). To upload or download to other paths (e.g., external drives), you must explicitly allow them.  

> **Security tip:** Only expose folders that actually need to be accessed via Globus.

### 1. Windows – Accessible Folders

1. Right‑click the **Globus** icon in the taskbar and choose **Options…**.
  
2. In the **Access** tab:
     
    * Your home directory is listed by default.  
    * Click **+** to add more folders (e.g., `D:\data\project1`).  
    * Optionally tick **Sharable** if your institution's Globus subscription allows guest collections.  

3. Path syntax from Globus:

    * `/~/` maps to your Windows home directory (e.g., `C:\Users\yourname`).  
    * `/C/path/to/dir` corresponds to `C:\path\to\dir`, and so on.  

### 2. macOS – Accessible Directories

1. Click the **Globus** icon in the menu bar → **Preferences…**.  

2. In **Access**:

    * Your home directory (e.g., `/Users/yourname`) is allowed by default.  
    * Click **+** to add more directories.  
    * You can choose whether each directory is sharable (sharing requires a subscription).  

### 3. Linux – Accessible Directories (config file)

On Linux, manage accessible paths via the GUI (if Tcl/Tk is installed) or via the config file:  

- Paths and permissions are stored in `~/.globusonline/lta/config-paths` as CSV:

```bash
<PATH>,<SHARING_FLAG>,<R/W_FLAG>

/home/user,0,0
/data/project,0,1
```

- `SHARING_FLAG` : `1` allow sharing, `0` disable  
- `R/W_FLAG` : `1` read/write, `0` read‑only  

After editing `config-paths`, restart GCP:

```bash
./globusconnectpersonal -stop
./globusconnectpersonal -start &
```

---

## **Transfer Data with the Globus Web App**

Once GCP is installed, running, and configured, you can transfer files from any browser.

For a detailed step-by-step guide on file transfer, see [https://docs.globus.org/guides/tutorials/manage-files/transfer-files/](https://docs.globus.org/guides/tutorials/manage-files/transfer-files/) 

### 1. Log In to Globus

1. Go to [https://app.globus.org](https://app.globus.org).
  
2. Log in with your institution or another identity (Google, ORCID, GitHub, or a Globus ID account).  

### 2. Open the File Manager

After login, you land on the **File Manager** page.

![Globus File Manager – empty state](https://docs.globus.org/guides/tutorials/manage-files/images/transfer-files/filemgr-1.png)

### 3. Select Your Personal Collection

1. In the left panel's **Collection** field, type the name you gave your PC's collection (e.g., `MyWorkStation`).  

2. Select it from the list. Globus connects and shows the default path (e.g., `/~/`).  

### 4. Select the Remote Collection

You can run File Manager in **two‑panel mode**:

1. Click **Transfer or Sync to…** on the right side to open a second panel.  
2. In the right panel's **Collection** field, search for your remote collection (e.g., **TEM_Collection@KISTI-GSDC**).
3. If additional authentication is required, you'll be redirected to the GSDC TEM OIDC server. Enter your user ID and password (+OTP) there to complete authentication.  
4. Navigate to the directory you're allowed to read/write.

![Two‑panel File Manager with Transfer or Sync to…](https://docs.globus.org/guides/tutorials/manage-files/images/transfer-files/filemgr-5.png)

### 5. Start a Transfer

To **upload from your PC to the remote system**:

1. Left panel: your **personal collection** (GCP) 
 
   - Navigate to the folder and select the files/directories to transfer.  

2. Right panel: **remote collection** (HPC storage like KISTI-GSDC)  

   - **`TEM_Collection@KISTI-GSDC`**
   - Navigate to the destination directory.  

3. Click **Start** above the panel representing the *destination* (this depends on the UI layout).  

To **download from the remote collection to your PC**, reverse the source and destination.

Globus will:

- Queue the transfer  
- Retry automatically on network glitches  
- Verify file integrity with checksums by default.  

![Transfer request submitted](https://docs.globus.org/guides/tutorials/manage-files/images/transfer-files/filemgr-7.png)

### 6. Monitor Transfer Status

1. Click **Activity** in the left navigation to see current and past transfers.
  
2. Click a transfer's details icon to see per‑file status and any error messages.

3. You'll also get email notifications when transfers finish or fail.

The transfer continues on the Globus service side even if you close your browser or log out.  

---

## **Tips & Troubleshooting**

### 1. Common Issues

- **"Path not allowed" or missing folders in File Manager**

    * Make sure the folder is added to Accessible Folders/Directories (Windows/macOS) or `config-paths` (Linux).  
    * Confirm your OS user has local read/write permission for that folder.

- **Install permission errors (e.g., can't write to `C:\Program Files`)**

    * Install into a directory you own (e.g., your home directory).  

- **GCP icon shows "Not Connected"**

    * A firewall or network rule may be blocking connections to the Globus service.  
    * Try a different network (home vs. campus VPN), or contact your IT staff with the Globus firewall requirements documentation.  

- **Browser login won't start from GCP**

    * Some security tools block launching a browser. In that case, use a **GCP Setup Key** as described in the troubleshooting guide.  

### 2. Advanced (Windows) – Very Long Paths

If you work with extremely deep directory structures or very long filenames on Windows, you may need to enable **long path support** in the OS registry so GCP can handle paths up to 4096 characters.

This change requires admin rights and a reboot; see the Windows GCP install documentation below for details. 

[https://docs.globus.org/globus-connect-personal/install/windows/#enable_long_path_support](https://docs.globus.org/globus-connect-personal/install/windows/#enable_long_path_support) 

### 3. Globus Official Help

- **Main GCP docs (Windows/macOS/Linux)** : detailed installation & configuration. [https://docs.globus.org/globus-connect-personal/#install](https://docs.globus.org/globus-connect-personal/#install)
  
- **How to Log In and Transfer Files tutorial** : step‑by‑step File Manager walkthrough. [https://docs.globus.org/guides/tutorials/manage-files/transfer-files/](https://docs.globus.org/guides/tutorials/manage-files/transfer-files/) 

- **GCP Troubleshooting Guide** : in‑depth help for install, firewall, and permission problems. [https://docs.globus.org/globus-connect-personal/#troubleshooting_configuration](https://docs.globus.org/globus-connect-personal/#troubleshooting_configuration) 