******
cisTEM
******
cisTEM is user-friendly software to process cryo-EM images of macromolecular complexes and obtain high-resolution 3D reconstructions from them. It comprises a number of tools to process image data including movies, micrographs and stacks of single-particle images, implementing a complete “pipeline” of processing steps to obtain high-resolution single-particle reconstructions. (from cisTEM official site https://cistem.org)

Executing cisTEM
================

How to start cisTEM data analysis tool
--------------------------------------

1. You can find out cisTEM applications' environment module path by listing all the module available on TEM service farm.

.. code-block:: bash

  $> module avail

  -------- /tem/el7/Modules/apps --------
  apps/cistem/1.0.0
  apps/relion/cpu/3.0.7
  apps/relion/cpu/3.1.0
  apps/relion/cpu/4.0.0
  apps/relion/gpu/3.0.7
  apps/relion/gpu/3.1.0

  ---- /tem/el7/Modules/acceleration ----
  cuda/9.2  cuda/11.2

  -------- /tem/el7/Modules/mpi ---------
  mpi/gcc/4.8.5/openmpi/4.0.3
  mpi/gcc/8.3.1/mpich/3.4.3
  mpi/gcc/8.3.1/openmpi/4.0.3
  mpi/gcc/openmpi/4.0.3

  ----- /tem/el7/Modules/virtualenv -----
  conda/2020.11  topaz/cuda-9.2/0.2.4
  pyem/0.5       topaz/cuda-11.0/0.2.4

  ------- /tem/el7/Modules/tools --------
  tools/aspera-cli/3.9.6
  tools/ctffind/4.1.14
  tools/gctf/1.18_b2
  tools/motioncor2/1.3.1
  tools/resmap/1.1.4
  tools/summovie/1.0.2
  tools/unblur/1.0.2

  ----- /tem/el7/Modules/experiment -----
  PyRosetta/4
  python/3.7
  rosetta/mpich-3.4.3/3.13
  rosetta/openmpi-4.0.3/3.13


2. Check the module details for cisTEM application

.. code-block:: bash

  $> module show apps/cistem/1.0.0 

  -------------------------------------------------------------------
  /tem/el7/Modules/apps/apps/cistem/1.0.0:

  module-whatis   {Setups cistem 1.0.0 environment variables}
  module          load mpi/gcc/openmpi/4.0.3
  prepend-path    PATH /tem/el7/cistem-1.0.0-beta
  conflict        apps/cistem
  -------------------------------------------------------------------

3. Load the environment module for cisTEM  application which you want to execute. As the module specified is loaded, all the modules with dependency are also loaded (you can check these modules with “module list” command)

.. code-block:: bash

  $> module load apps/cistem/1.0.0 
  $> module list
  Currently Loaded Modulefiles:
    1) mpi/gcc/openmpi/4.0.3   2) apps/cistem/1.0.0

4. Check the cisTEM application binary path

.. code-block:: bash

  $> which cisTEM
  /tem/el7/cistem-1.0.0-beta/cisTEM


5. Execute the cisTEM application (we assume that X11 forwarding is enabled)

.. code-block:: bash

  $> cisTEM


.. image:: images/cistem-screenshot-re.png
  :scale: 40 %
  :align: center

On startup, the GUI presents a list of previously opened projects, as well as options to create a new project or open an existing project. 
To continue a previous project, click on the provided link.


Run profiles for job submission
===============================

Profile templates
-----------------

If you need cisTEM to work on multiple computing servers in a cluster which is managed with Torque, you should check out (or create) a "Run Profile" in cisTEM's settings tab.
You can find a shell script available in following file paths.

.. code-block:: bash

  /tem/el7/qsub-cisTEM-cpu-noout.sh             ## output, error 로그 파일을 생성하지 않는 cisTEM 작업 템플릿
  /tem/el7/qsub-cisTEM-cpu.sh                   ## output, error 로그 파일을 생성하는 cisTEM 작업 템플릿


For qsub-cisTEM-cpu.sh,

.. code-block:: bash

  #!/bin/bash
  queue=
  while getopts ":q:" OPTION
  do
    case "${OPTION}" in
      q) queue="${OPTARG}";;
    esac
  done
  shift $((OPTIND-1))

  cat - <<EOF | qsub
  #!/bin/bash
  #PBS -N cisTEM.${1}
  ${queue:+#PBS -l nodes=1:ppn=1:${queue}}
  ${queue:+#PBS -q ${queue}}

  module load apps/cistem/1.0.0
  ${@}
  EOF

For qsub-cisTEM-cpu-noout.sh,

.. code-block:: bash

  #!/bin/bash
  queue=
  while getopts ":q:" OPTION
  do
    case "${OPTION}" in
      q) queue="${OPTARG}";;
    esac
  done
  shift $((OPTIND-1))

  cat - <<EOF | qsub
  #!/bin/bash
  #PBS -N cisTEM.${1}
  #PBS -e /dev/null
  #PBS -o /dev/null
  ${queue:+#PBS -l nodes=1:ppn=1:${queue}}
  ${queue:+#PBS -q ${queue}}

  module load apps/cistem/1.0.0
  ${@}
  EOF


Adding a new Run Profile
------------------------

In cisTEM settings, add a new "Run Profile" (called TORQUE here) with the following parameters :

* Manager Command: /tem/el7/cistem-1.0.0-beta/$command 
* Gui Address: Automatic
* Controller Address: Automatic
* Command -> Edit:

  * Command: /tem/el7/qsub-cisTEM-cpu.sh **-q cpuQ** $command
  * No. Copies: 84
  * Delay (ms): 10

.. image:: images/cistem-run-profile-re.png
  :scale: 50 %
  :align: center

Examples of running cisTEM jobs
===============================

With the above cisTEM setting, here, we provide some examples of running cisTEM jobs with cisTEM GUI tools.

Importing Movies and images
---------------------------

Once a project is open or has been newly created, Assets can be imported. These will usually be Movies or Images but can also be Particle Positions, 3D Volumes and Refinement Packages.
Click on Assets, then Movies and Import. In the dialog, select "Add Directory" and navigate to the directory containing your own movies.
The movies are all part of a group called "All Movies". Additional groups can be created using "Add" to select subsets of a dataset for further processing. 
You should continue with all the data for now. If images are available instead of movies,
these can be imported as Image Assets in the same way as Movies, by clicking "Images".

.. image:: images/cisTEM-importmovies.png
  :scale: 40 %
  :align: center


Movie Alignment
---------------

Movie data collection and frame alignment have been part of the single-particle image processing pipeline since it was first introduced by Brilot et al. in 2012. The original software **Unblur** was developed further by Grant & Grigorieff (2015) when exposure weighting was added to take into account the radiation-dependent signal loss when adding movie frames, yielding signal-optimized frame sums. cisTEM implements the Unblur algorithm in the Align Movies panel, which also provides some background to the method. Click “Actions” and select “Align Movies” to call up the panel.


.. image:: images/cisTEM-alignmovies-1.png
  :scale: 40 %
  :align: center

Actions panels display parameters that you can change. Some of these are shown on the main panel while others are only accessible when "Show Expert Options" is selected. 
Movie alignment usually works with the default parameters and you should simply click "Start Alignment" near the bottom of the panel.
You will notice that next to the start button a menu is shown that allows you to select different run profiles.
The Local profile should **NOT** be selected because it will launch alignment jobs onto the login node but you should change to other profiles (for example, TORQUE profile) 
if these were previously set up under Settings.

The alignment of all the  movies takes less than a minute. While the job is running, X,Y traces are displayed for some of the movies and a progress bar indicates the time left until completion of the job. 
After termination (you must click on “Finish” at the end of all jobs), you can inspect the results by clicking "Results"


.. image:: images/cisTEM-alignmovies-2.png
  :scale: 40 %
  :align: center

