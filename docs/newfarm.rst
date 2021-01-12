******************
GSDC TEM 신규 분석 팜
******************

EL 7.x 신규 분석 팜 접속
====================

리눅스/맥 사용자
------------

.. code-block:: bash

  $> ssh -Y -o Port=<port> <userID>@tem-ui-el7.sdfarm.kr
  -Y (or -X) options : enable trusted X11 (or untrusted X11) forwarding


윈도우즈 사용자
-----------

기존에 사용하시던 MobaXTerm, Putty 등의 SSH 클라이언트 프로그램을 사용하는 것은 같습니다. 다만, 접속 로그인 노드는 **tem-ui-el7.sdfarm.kr**를 사용하셔야 합니다.


EL7.x 기반 재빌드가 완료된 데이터 분석 도구들
===================================

데이터 분석 도구들의 Module 경로
--------------------------

.. code-block:: bash

  $> module avail
  -------- /tem/el7/Modules/apps --------
  apps/cistem/1.0.0      
  apps/relion/cpu/3.0.7  
  apps/relion/cpu/3.1.0  
  apps/relion/gpu/3.0.7  
  apps/relion/gpu/3.1.0  

  ---- /tem/el7/Modules/acceleration ----
  cuda/9.2  

  -------- /tem/el7/Modules/mpi ---------
  mpi/gcc/openmpi/4.0.3  

  ----- /tem/el7/Modules/virtualenv -----
  conda/2020.11  

  ------- /tem/el7/Modules/tools --------
  tools/ctffind/4.1.14    
  tools/gctf/1.18_b2      
  tools/motioncor2/1.3.1  
  tools/resmap/1.1.4      
  tools/summovie/1.0.2    
  tools/unblur/1.0.2      


데이터 분석 작업 PBS 작업 템플릿 경로
-----------------------------

.. code-block:: bash

  /tem/el7/qsub-cisTEM-cpu-noout.sh             ## output, error 로그 파일을 생성하지 않는 cisTEM 작업 템플릿
  /tem/el7/qsub-cisTEM-cpu.sh                   ## output, error 로그 파일을 생성하는 cisTEM 작업 템플릿
  /tem/el7/qsub-relion-3.0.7-cpu.bash           ## Relion 3.0.7 CPU MPI 작업 템플릿
  /tem/el7/qsub-relion-3.1.0-cpu.bash           ## Relion 3.1.0 CPU MPI 작업 템플릿
  /tem/el7/qsub-relion-3.0.7-cpu.bash           ## Relion 3.0.7 GPU 가속 활용하는 MPI 작업 템플릿
  /tem/el7/qsub-relion-3.1.0-gpu.bash           ## Relion 3.1.0 GPU 가속 활용하는 MPI 작업 템플릿