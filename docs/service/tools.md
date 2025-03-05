# TEM Data Analysis Tools

## AreTomo
**Description** 
> (Alignment and Reconstruction for Electron Tomography) GPU-accelerated software package that provides an integrated solution to both fiducial-free alignment and reconstruction for cryoEM tomography.
 
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

## CryoSPARC
**Description**
> A state of the art scientific software platform for cryo-electron microscopy (cryo-EM) used in research and drug discovery pipelines.

**URL**
> [https://cryosparc.com](https://cryosparc.com)

???+ tip "Remarks on CryoSPARC"

    Running CryoSPARC instance is provided per each Research Group basis on their scratch directory (/tem/scratch/__GroupName__/.cryosparc).
    For more details, please refer to [CryoSPARC](../apps/cryosparc.md)


## CTFFind4
**Description**
> A new version of ctffind (a program for finding CTFs of electron micrographs) that should run significantly faster than CTFFind3 and may give slightly improved results when processing data from detectors other than scanned photographic film.

**URL**
> [https://grigoriefflab.umassmed.edu/ctffind4](https://grigoriefflab.umassmed.edu/ctffind4)

???+ note "ModulePaths for CTFFind4"

    ```bash
    apps/ctffind/4.1.14/cpu/gcc-11.5.0
    apps/ctffind/4.1.14/cpu/intel-compiler-2024.0.2
    ```

## IsoNet
**Description**
> (ISOtropic reconstructioN of Electron Tomography) A tool that trains deep convolutional neural networks to reconstruct meaningful contents in the missing wedge for electron tomography, and to increase signal-to-noise ratio, using the information learned from the original tomogram.

**URL**
> [https://github.com/IsoNet-cryoET/IsoNet](https://github.com/IsoNet-cryoET/IsoNet)

???+ note "ModulePaths for IsoNet"

    ```bash
    apps/isonet/0.2.1/gpu/cuda-12.5
    apps/isonet/0.3.0/gpu/cuda-12.5
    ```

## MotionCor
**Description**
> A multi-GPU program that corrects beam-induced sample motion on dose fractionated movie stacks. It implements a robust iterative alignment algorithm that delivers precise measurement and correction of both global and non-uniform local motions at single pixel level across the whole frame, suitable for both single-particle and tomographic images.

**URL**
> * [MotionCor2](https://msg.ucsf.edu/software)
> * [MotinoCor3](https://github.com/czimaginginstitute/MotionCor3)

???+ note "ModulePaths for MotionCor"

    ```bash
    apps/motioncor2/1.6.4/gpu/cuda-11.8
    apps/motioncor3/1.1.1/gpu/cuda-11.8
    apps/motioncor3/1.1.1/gpu/cuda-12.6
    ```

## PyEM
**Description**
> A collection of Python modules and command-line utilities for electron microscopy of biological samples.

**URL**
> [https://github.com/asarnow/pyem](https://github.com/asarnow/pyem)

???+ note "ModulePaths for PyEM"

    ```bash
    apps/pyem/0.65
    ```

## Relion
**Description**
> Relion (for REgularised LIkelihood OptimisatioN, pronounce rely-on) is a software package that employs an empirical Bayesian approach for electron cryo-microscopy (cryo-EM) structure determination. It is developed in the group of Sjors Scheres at the MRC Laboratory of Molecular Biology.

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

## ResMap
**Description**
> (Resolution Map) a Python (NumPy/SciPy) application with a Tkinter GUI. It is an easy to use software package for computing the local resolution of 3D density maps studied in structural biology, primarily electron cryo-microscopy (cryo-EM). ResMap has a both a GUI (window) and a command line interface.

**URL**
> [https://resmap.sourceforge.net](https://resmap.sourceforge.net)

???+ note "ModulePaths for ResMap"

    ```bash
    apps/resmap/1.1.4
    ```

## SumMovie
**Description**
> A tool that uses the alignment results from the software application Unblur to calculate movie frame sums.

**URL**
> [https://grigoriefflab.umassmed.edu/unblur_summovie](https://grigoriefflab.umassmed.edu/unblur_summovie)

???+ note "ModulePaths for SumMovie"

    ```bash
    apps/summovie/1.0.2
    ```

## Topaz
**Description**
> A pipeline for particle detection in cryo-electron microscopy images using convolutional neural networks trained from positive and unlabeled examples. Topaz includes methods for micrograph denoising using deep denoising models.

**URL**
> [https://github.com/tbepler/topaz](https://github.com/tbepler/topaz)

???+ note "ModulePaths for Topaz"

    ```bash
    apps/topaz/0.2.5/gpu/cuda-11.8
    apps/topaz/0.2.5/gpu/cuda-12.4

    apps/topaz/0.3.1/gpu/cuda-11.8
    apps/topaz/0.3.1/gpu/cuda-12.4
    ```

## Topaz for picking Filaments
**Description**
> A program with added support for filament start-end coordinate picking (new options -f, -fp and -fl in the extract command extract.py) in Topaz, for subsequent helical reconstruction in RELION.

**URL**
> [https://github.com/3dem/topaz](https://github.com/3dem/topaz)

???+ note "ModulePaths for Topaz filaments picking"

    ```bash
    apps/topaz/0.2.5_filaments/gpu/cuda-11.8
    apps/topaz/0.2.5_filaments/gpu/cuda-12.4
    ```

## Unblur
**Description**
> A tool used to align the frames of movies recorded on an electron microscope to reduce image blurring due to beam-induced motion. It reads stacks of movies that are stored in MRC/CCP4 format and generates frame sums that can be used in subsequent image processing.

**URL**
> [https://grigoriefflab.umassmed.edu/unblur_summovie](https://grigoriefflab.umassmed.edu/unblur_summovie)

???+ note "ModulePaths for Unblur"

    ```bash
    apps/unblur/1.0.2
    ```