# cryoDRGN User Guide

This page is a basic guide for using **cryoDRGN** on the AlmaLinux 9.x based GSDC TEM cluster.
cryoDRGN is a deep-learning-based tool for continuous particle structure and heterogeneity analysis in Cryo-EM. On the GSDC cluster, it is distributed via a **Conda environment**.

---

## 1. Environment Setup

cryoDRGN is installed within a Conda virtual environment on the system. Before running any tasks, you must load Conda using `Environment Modules` and activate the cryoDRGN environment.

```bash
# Load the Conda module
module load miniconda3/py312_25.1.1-2

# Load and activate the cryoDRGN virtual environment (Update the name to match the actual installed environment on the cluster)
module load apps/cryodrgn/4.3.0/gpu/cuda-12.x
```

---

## 2. Workspace Setup & PBS Job Submission

The GSDC TEM cluster uses PBSPro as its job scheduler. Since the cryoDRGN model training process heavily relies on GPU computation, you must not run it directly on the login node.
Instead, you need to write a **PBSPro batch script** and submit the job to a queue with GPU resources.

### Recommended Directory Structure
To keep your raw input data separate from your output results, it is highly recommended to create a dedicated project directory and manage your files as shown below:

```text
my_cryodrgn_project/         # Working directory (Create and submit your script here)
├── inputs/                  # Raw data folder
│   ├── particles.mrcs
│   └── run_data.star
├── outputs/                 # Folder where cryoDRGN training results will be saved (automatically created)
└── run_cryodrgn.sh          # PBS batch script for job submission
```

### Example PBS Script (`run_cryodrgn.sh`)
Create the script inside your `my_cryodrgn_project/` directory. The `$PBS_O_WORKDIR` environment variable automatically points to the path where the `qsub` command is executed.

```bash
#!/bin/bash
#PBS -N my_cryodrgn_job
#PBS -q gpuQ
#PBS -l select=1:ncpus=8:ngpus=1:mem=64GB
#PBS -j oe
#PBS -k eod

# Navigate to the directory where the job was submitted (my_cryodrgn_project)
cd $PBS_O_WORKDIR

# Load module and activate environment
module load miniconda3/py312_25.1.1-2
module load apps/cryodrgn/4.3.0/gpu/cuda-12.x

# Run training (Read from the inputs/ folder and direct output to the outputs/ folder)
cryodrgn train_vae inputs/particles.mrcs \
    --ctf inputs/ctf.pkl \
    --poses inputs/poses.pkl \
    -z 8 \
    --n-epochs 50 \
    -o outputs/vae_results
```

### Submitting and Monitoring Jobs
After writing the job script, use the `qsub` command from within your project directory to submit the job.
```bash
qsub run_cryodrgn.sh
```
You can check your job status using the `qstat` command.
For more detailed information on queues and job management commands, please refer to the [Job Scripts](../batch/jobscripts.md) and [Running Jobs (PBSPro)](../batch/pbspro.md) pages.

---

## 3. Basic Pipeline

The typical data processing workflow using cryoDRGN is outlined below. You can check detailed options for specific commands by running `cryodrgn [command] --help`.

### Step 1: Metadata Parsing
Before training, convert metadata (such as STAR files) derived from Relion or CryoSPARC into a format (`.pkl`) that cryoDRGN can read. Since this requires minimal computational resources, you can run this preprocessing directly on the login node.
```bash
# Parse pose information
cryodrgn parse_pose_vd inputs/run_data.star -o inputs/poses.pkl

# Parse CTF information
cryodrgn parse_ctf_star inputs/run_data.star -o inputs/ctf.pkl
```

### Step 2: VAE Model Training
Submit the `run_cryodrgn.sh` script via PBS to train the model on a GPU node using the extracted particle images and parsed metadata.

### Step 3: Result Analysis and Visualization
After the training is complete, analyze the results to generate volumes or visualize the distribution. This process targets the generated output folder.
```bash
cryodrgn analyze outputs/vae_results/00_vae128/ -o outputs/analysis_results
```

---

For more details on CryoDRGN usage guide, please refer to [CryoDRGN User Guide](https://ez-lab.gitbook.io/cryodrgn).