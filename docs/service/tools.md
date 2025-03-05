# TEM Data Analysis Tools

## AreTomo
* Description : (Alignment and Reconstruction for Electron Tomography) GPU-accelerated software package that provides an integrated solution to both fiducial-free alignment and reconstruction for cryoEM tomography.
* URL : [https://msg.ucsf.edu/software](https://msg.ucsf.edu/software)

???+ note "ModulePaths for AreTomo"

    ```bash
    apps/aretomo/1.3.4/gpu/cuda-11.8
    apps/aretomo2/1.1.2/gpu/cuda-11.8
    apps/aretomo2/1.1.2/gpu/cuda-12.6
    apps/aretomo3/2.0.3/gpu/cuda-11.8
    apps/aretomo3/2.0.3/gpu/cuda-12.6    
    ```

## CryoSPARC
* Description : A state of the art scientific software platform for cryo-electron microscopy (cryo-EM) used in research and drug discovery pipelines.
* URL : [https://cryosparc.com](https://cryosparc.com)

???+ tip "Remarks on CryoSPARC"

    Running CryoSPARC instance is provided per each Research Group basis on their scratch directory (/tem/scratch/__GroupName__/.cryosparc).
    For more details, please refer to [CryoSPARC](../apps/cryosparc.md)


## CTFFind4
* Description : A new version of ctffind (a program for finding CTFs of electron micrographs) that should run significantly faster than CTFFind3 and may give slightly improved results when processing data from detectors other than scanned photographic film.
* URL : [https://grigoriefflab.umassmed.edu/ctffind4](https://grigoriefflab.umassmed.edu/ctffind4)

???+ note "ModulePaths for CTFFind4"

    ```bash
    apps/ctffind/4.1.14/cpu/gcc-11.5.0
    apps/ctffind/4.1.14/cpu/intel-compiler-2024.0.2
    ```

## IsoNet
* Description : (ISOtropic reconstructioN of Electron Tomography) A tool that trains deep convolutional neural networks to reconstruct meaningful contents in the missing wedge for electron tomography, and to increase signal-to-noise ratio, using the information learned from the original tomogram.
* URL : [https://github.com/IsoNet-cryoET/IsoNet](https://github.com/IsoNet-cryoET/IsoNet)

???+ note "ModulePaths for IsoNet"

    ```bash
    apps/isonet/0.2.1/gpu/cuda-12.5
    apps/isonet/0.3.0/gpu/cuda-12.5
    ```

## MotionCor
* Description : A multi-GPU program that corrects beam-induced sample motion on dose fractionated movie stacks. It implements a robust iterative alignment algorithm that delivers precise measurement and correction of both global and non-uniform local motions at single pixel level across the whole frame, suitable for both single-particle and tomographic images.
* URL
  ** [MotionCor2](https://msg.ucsf.edu/software)
  ** [MotinoCor3](https://github.com/czimaginginstitute/MotionCor3)

???+ note "ModulePaths for MotionCor"

    ```bash
    apps/motioncor2/1.6.4/gpu/cuda-11.8
    apps/motioncor3/1.1.1/gpu/cuda-11.8
    apps/motioncor3/1.1.1/gpu/cuda-12.6
    ```

## PyEM

## Relion

## ResMap

## SumMovie

## Topaz

## Unblur