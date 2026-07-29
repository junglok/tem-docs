# TEM Data Analysis Tools

## **AreTomo**

**Description**
> (Alignment and Reconstruction for Electron Tomography) A GPU-accelerated software package providing an integrated solution for fiducial-free alignment and reconstruction in cryoEM tomography.

**URL**
> [https://msg.ucsf.edu/software](https://msg.ucsf.edu/software)

???+ note "ModulePaths for AreTomo"

    ```bash
    apps/aretomo/1.3.4/gpu/cuda-11.8
    apps/aretomo2/1.1.2/gpu/cuda-11.8
    apps/aretomo2/1.1.2/gpu/cuda-12.6
    apps/aretomo3/2.0.3/gpu/cuda-11.8
    apps/aretomo3/2.0.3/gpu/cuda-12.6    
    ```

## **CisTEM**

**Description**
> GUI-based software for processing cryo-EM images of macromolecular complexes to obtain high-resolution 3D reconstructions. It provides tools for processing image data—movies, micrographs, and stacks of single-particle images—implementing a complete "pipeline" of steps for high-resolution single-particle reconstructions.

**URL**
> [https://cistem.org](https://cistem.org)

???+ note "ModulePaths for cisTEM"

    ```bash
    apps/cistem/1.0.0/cpu/gcc-11.5.0
    ```

## **CryoDRGN**

**Description**
> CryoDRGN is a neural-network-based algorithm for heterogeneous cryo-EM reconstruction. It models a continuous distribution over 3D structures using a neural-network-based representation of the volume.


**URL**
> [https://github.com/ml-struct-bio/cryodrgn](https://github.com/ml-struct-bio/cryodrgn)

> [https://ez-lab.gitbook.io/cryodrgn](https://ez-lab.gitbook.io/cryodrgn)

???+ note "ModulePaths for cryoDRGN"

    ```bash
    apps/cryodrgn/4.3.0/gpu/cuda-12.x
    ```

## **CrYOLO**

**Description**
> An application for fast, accurate cryo-EM particle picking, based on convolutional neural networks and the popular You Only Look Once (YOLO) object detection system.

**URL**
> [https://cryolo.readthedocs.io](https://cryolo.readthedocs.io)

???+ note "ModulePaths for cryolo"

    ```bash
    apps/cryolo/1.9.9/gpu/cuda-11.x
    ```

## [**CryoSPARC**](../apps/cryosparc.md)

**Description**
> A state-of-the-art scientific software platform for cryo-electron microscopy (cryo-EM), used in research and drug discovery pipelines.

**URL**
> [https://cryosparc.com](https://cryosparc.com)

???+ tip "Remarks on CryoSPARC"

    Each research group gets its own running CryoSPARC instance in its scratch directory (/tem/scratch/__GroupDir__/.cryosparc).
    For more details, see [CryoSPARC](../apps/cryosparc.md).


## **CTFFind4**

**Description**
> A new version of ctffind (a program for finding the CTFs of electron micrographs) that runs significantly faster than CTFFind3 and may give slightly better results when processing data from detectors other than scanned photographic film.

**URL**
> [https://grigoriefflab.umassmed.edu/ctffind4](https://grigoriefflab.umassmed.edu/ctffind4)

???+ note "ModulePaths for CTFFind4"

    ```bash
    apps/ctffind/4.1.14/cpu/gcc-11.5.0
    apps/ctffind/4.1.14/cpu/intel-compiler-2024.0.2
    ```

## **deepEMhancer**

**Description**
> DeepEMhancer is a Python package for post-processing cryo-EM maps, as described in "DeepEMhancer: a deep learning solution for cryo-EM volume post-processing" (Sanchez-Garcia et al., 2021). It's a deep learning model trained on pairs of experimental volumes and atomic-model-corrected volumes, able to produce post-processed maps from raw volume input, preferably half maps.

**URL**
> [https://github.com/rsanchezgarc/deepEMhancer](https://github.com/rsanchezgarc/deepEMhancer)

???+ note "ModulePaths for deepEMhancer"

    ```bash
    apps/deepemhancer/0.17/gpu/cuda-11.x
    ```

## **Dynamo**

TBD

## **EMRNA**

**Description**
> A tool that performs deep-learning-based automated RNA modeling from cryo-EM maps.

**URL**
> [http://huanglab.phys.hust.edu.cn/EMRNA](http://huanglab.phys.hust.edu.cn/EMRNA)

???+ note "ModulePaths for EMRNA"

    ```bash
    apps/emrna/1.5/gpu/cuda-11.1
    ```

## **EternaFold**

**Description**
> A tool that uses multitask learning to improve RNA structure prediction. Its training tasks include: 1) predicting single structures, 2) maximizing the likelihood of structure probing data, and 3) predicting experimentally measured affinities of RNA molecules to proteins and small molecules.

**URL**
> [https://github.com/eternagame/EternaFold](https://github.com/eternagame/EternaFold)

???+ note "ModulePaths for EternaFold"

    ```bash
    apps/eternafold/1.3.1/cpu/gcc-11.5.0
    ```

## **GCtfFind**

**Description**
> GCtfFind is a new application that robustly estimates the contrast transfer function (CTF) of cryoET tilt series and cryoEM micrographs—essential information for cryoET subtomogram averaging and cryoEM single-particle reconstruction.

**URL**
> [https://github.com/czimaginginstitute/GCtfFind](https://github.com/czimaginginstitute/GCtfFind)

???+ note "ModulePaths for GCtfFind"

    ```bash
    apps/gctffind/1.0.0/gpu/cuda-11.8
    apps/gctffind/1.0.0/gpu/cuda-12.6
    ```

## **IMOD**

**Description**
> IMOD is a set of image processing, modeling, and display programs for tomographic reconstruction and 3D reconstruction of EM serial and optical sections. It contains tools for assembling and aligning data across image stacks of various types and sizes, viewing 3D data from any orientation, and modeling and displaying image files.

**URL**
> [https://bio3d.colorado.edu/imod](https://bio3d.colorado.edu/imod)

???+ note "ModulePaths for IMOD"

    ```bash
    apps/imod/5.1.1/gpu/cuda-12.6
    ```

## **IsoNet**

**Description**
> (ISOtropic reconstructioN of Electron Tomography) A tool that trains deep convolutional neural networks to reconstruct meaningful content in the missing wedge for electron tomography and increase signal-to-noise ratio, using information learned from the original tomogram.

**URL**
> [https://github.com/IsoNet-cryoET/IsoNet](https://github.com/IsoNet-cryoET/IsoNet)

???+ note "ModulePaths for IsoNet"

    ```bash
    apps/isonet/0.2.1/gpu/cuda-12.5
    apps/isonet/0.3.0/gpu/cuda-12.5
    ```

## **MotionCor**

**Description**
> A multi-GPU program that corrects beam-induced sample motion in dose-fractionated movie stacks. It uses a robust iterative alignment algorithm to precisely measure and correct both global and non-uniform local motion at single-pixel level across the whole frame, suitable for single-particle and tomographic images alike.

**URL**
> * [MotionCor2](https://msg.ucsf.edu/software)
> * [MotinoCor3](https://github.com/czimaginginstitute/MotionCor3)

???+ note "ModulePaths for MotionCor"

    ```bash
    apps/motioncor2/1.6.4/gpu/cuda-11.8
    apps/motioncor3/1.1.1/gpu/cuda-11.8
    apps/motioncor3/1.1.1/gpu/cuda-12.6
    ```

## **PyEM**

**Description**
> A collection of Python modules and command-line utilities for electron microscopy of biological samples.

**URL**
> [https://github.com/asarnow/pyem](https://github.com/asarnow/pyem)

???+ note "ModulePaths for PyEM"

    ```bash
    apps/pyem/0.65
    ```

## **PyTOM**

**Description**
> PyTom is a software package for analyzing volumetric data from cryo electron tomography (cryo-ET). It covers a complete pipeline: tomogram reconstruction, localizing macromolecular complexes in tomograms, fine alignment of subtomograms extracted at these locations, and their classification.

**URL**
> * [https://pytom.sites.uu.nl](https://pytom.sites.uu.nl)
> * [https://github.com/SBC-Utrecht/PyTom](https://github.com/SBC-Utrecht/PyTom) 

???+ note "ModulePaths for PyTom"

    ```bash
    apps/pytom/1.1/gpu/cuda-12.x
    ```

## [**Relion**](../apps/relion.md)

**Description**
> Relion (for REgularised LIkelihood OptimisatioN, pronounced "rely-on") is a software package that uses an empirical Bayesian approach for electron cryo-microscopy (cryo-EM) structure determination. It's developed by Sjors Scheres's group at the MRC Laboratory of Molecular Biology.

**URL**
> * [Relion 4.x](https://relion.readthedocs.io/en/release-4.0)
> * [Relion 5.x](https://relion.readthedocs.io/en/release-5.0)

???+ note "ModulePaths for Relion"

    ```bash
    apps/relion/4.0.1/cpu/gcc-11.5.0
    apps/relion/4.0.1/cpu/intel-compiler-2024.0.2
    apps/relion/4.0.1/gpu/cuda-11.8
    apps/relion/4.0.1/gpu/cuda-12.6

    apps/relion/5.0.0/cpu/gcc-11.5.0
    apps/relion/5.0.0/cpu/intel-compiler-2024.0.2
    apps/relion/5.0.0/gpu/cuda-11.8
    apps/relion/5.0.0/gpu/cuda-12.6
    ```

## **ResMap**

**Description**
> (Resolution Map) A Python (NumPy/SciPy) application with a Tkinter GUI. It's an easy-to-use package for computing the local resolution of 3D density maps in structural biology, primarily electron cryo-microscopy (cryo-EM). ResMap has both a GUI (window) and a command-line interface.

**URL**
> [https://resmap.sourceforge.net](https://resmap.sourceforge.net)

???+ note "ModulePaths for ResMap"

    ```bash
    apps/resmap/1.1.4
    ```

## **SumMovie**

**Description**
> A tool that uses alignment results from the Unblur software to calculate movie frame sums.

**URL**
> [https://grigoriefflab.umassmed.edu/unblur_summovie](https://grigoriefflab.umassmed.edu/unblur_summovie)

???+ note "ModulePaths for SumMovie"

    ```bash
    apps/summovie/1.0.2
    ```

## **Topaz**

**Description**
> A pipeline for particle detection in cryo-electron microscopy images, using convolutional neural networks trained on positive and unlabeled examples. Topaz also includes deep-learning-based micrograph denoising methods.

**URL**
> [https://github.com/tbepler/topaz](https://github.com/tbepler/topaz)

???+ note "ModulePaths for Topaz"

    ```bash
    apps/topaz/0.2.5/gpu/cuda-11.8
    apps/topaz/0.2.5/gpu/cuda-12.4

    apps/topaz/0.3.1/gpu/cuda-11.8
    apps/topaz/0.3.1/gpu/cuda-12.4
    ```

## **Topaz for CryoSPARC**

**Description**
> A pipeline for particle detection in cryo-electron microscopy images, using convolutional neural networks trained on positive and unlabeled examples. Topaz also includes deep-learning-based micrograph denoising methods. This module runs on Python 3.6.

**URL**
> [https://guide.cryosparc.com/processing-data/all-job-types-in-cryosparc/deep-picking/topaz](https://guide.cryosparc.com/processing-data/all-job-types-in-cryosparc/deep-picking/topaz)

???+ note "ModulePaths for Topaz (for CryoSPARC)"

    ```bash
    apps/topaz/0.2.5a/gpu/cuda-11.3
    ```



## **Topaz for Picking Filaments**

**Description**
> A version of Topaz with added support for filament start-end coordinate picking (new options -f, -fp, and -fl in the extract.py command), for subsequent helical reconstruction in RELION.

**URL**
> [https://github.com/3dem/topaz](https://github.com/3dem/topaz)

???+ note "ModulePaths for Topaz filaments picking"

    ```bash
    apps/topaz/0.2.5_filaments/gpu/cuda-11.8
    apps/topaz/0.2.5_filaments/gpu/cuda-12.4
    ```

## **Unblur**

**Description**
> A tool that aligns movie frames recorded on an electron microscope to reduce image blurring from beam-induced motion. It reads movie stacks stored in MRC/CCP4 format and generates frame sums for use in subsequent image processing.

**URL**
> [https://grigoriefflab.umassmed.edu/unblur_summovie](https://grigoriefflab.umassmed.edu/unblur_summovie)

???+ note "ModulePaths for Unblur"

    ```bash
    apps/unblur/1.0.2
    ```
