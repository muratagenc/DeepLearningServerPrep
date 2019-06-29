<p>************************************************************** Preparing a Deep Learning Server on Ubuntu 18.04</p>

<p>last updated: 06/28/2019 murat genc muratagenc@gmail.com  **************************************************************</p>

<p>Hardware: 2 x GeForce GT 710 1GB GPU 1 x Intel i3 16G DDR3 memory  250G SSD drive </p>

<p> #basic o.s. installation ************************************************************************************************* install ubuntu 18, minimal, using its own keyboard/mouse/monitor erase the whole disk network is on dhcp, check the ip before restarting reboot</p>

<p> #update o.s. ************************************************************************************************* sudo apt update sudo apt upgrade sudo apt autoremove reboot</p>

<p> #enable remote desktop (just in case) ************************************************************************************************* sudo apt install -y vino gnome-control-center sharing turn sharing on, right upper corner, turn the switch on screen sharing on (vnc://zgenc.local) check allow connections to control the secreen, check require password, type a password turn on wired connection 1 (or wireless) test with Remmina or another vnc client</p>

<p> #enable ssh ************************************************************************************************* sudo apt install openssh-server test: ssh zihni@zgenc.local</p>

<p> #change root password ************************************************************************************************* sudo -i passwd <type new password twice> </p>

<p> #install gcc/g++/make/net-tools ************************************************************************************************* apt install gcc g++ net-tools</p>

<p>check gcc version; gcc --version apt install build-essential</p>

<p>root@zgenc:~# gcc --version gcc (Ubuntu 7.4.0-1ubuntu1~18.04.1) 7.4.0 Copyright (C) 2017 Free Software Foundation, Inc</p>

<p> #prepare cuda installation  ************************************************************************************************* bash -c &quot;echo blacklist nouveau > /etc/modprobe.d/blacklist-nvidia-nouveau.conf&quot; bash -c &quot;echo options nouveau modeset=0 >> /etc/modprobe.d/blacklist-nvidia-nouveau.conf&quot;</p>

<p>Confirm the content of the new modprobe config file: cat /etc/modprobe.d/blacklist-nvidia-nouveau.conf blacklist nouveau options nouveau modeset=0</p>

<p>Update kernel initramfs Enter the following linux command to regenerate initramfs: update-initramfs -u reboot</p>

<p>#download and install cuda ************************************************************************************************* become root: su  wget https://developer.nvidia.com/compute/cuda/10.1/Prod/local_installers/cuda_10.1.168_418.67_linux.run sh cuda_10.1.168_418.67_linux.run</p>

<p>| CUDA Installer &#9474; &#9474; - [X] Driver &#9474; &#9474; [X] 418.67 &#9474; &#9474; + [X] CUDA Toolkit 10.1 &#9474; &#9474; [X] CUDA Samples 10.1 &#9474; &#9474; [X] CUDA Demo Suite 10.1 &#9474; &#9474; [X] CUDA Documentation 10.1 &#9474; &#9474; Options &#9474; &#9474; Install </p>

<p> Done! =========== = Summary = ===========</p>

<p>Driver: Installed Toolkit: Installed in /usr/local/cuda-10.1/ Samples: Installed in /root/, but missing recommended libraries</p>

<p>Please make sure that  - PATH includes /usr/local/cuda-10.1/bin  - LD_LIBRARY_PATH includes /usr/local/cuda-10.1/lib64, or, add /usr/local/cuda-10.1/lib64 to /etc/ld.so.conf and run ldconfig as root</p>

<p>To uninstall the CUDA Toolkit, run cuda-uninstaller in /usr/local/cuda-10.1/bin To uninstall the NVIDIA Driver, run nvidia-uninstall</p>

<p>Please see CUDA_Installation_Guide_Linux.pdf in /usr/local/cuda-10.1/doc/pdf for detailed information on setting up CUDA. Logfile is /var/log/cuda-installer.log</p>

<p>#set environmental variables for your user ************************************************************************************************* exit (no more ROOT!) export PATH=&quot;/usr/local/cuda-10.1/bin:$PATH&quot;</p>

<p>edit /etc/ld.so.conf include /etc/ld.so.conf.d/*.conf include /usr/local/cuda-10.1/lib64</p>

<p>run ldconfig as root root@zgenc:/home/zihni# nano /etc/ld.so.conf root@zgenc:/home/zihni# ldconfig root@zgenc:/home/zihni# </p>

<p>#check nvidia drivers for the GPUs installed ************************************************************************************************* nvidia-smi</p>

<p>root@zgenc:/home/zihni# nvidia-smi Fri Jun 28 23:44:47 2019  +-----------------------------------------------------------------------------+ | NVIDIA-SMI 418.67 Driver Version: 418.67 CUDA Version: 10.1 | |-------------------------------+----------------------+----------------------+ | GPU Name Persistence-M| Bus-Id Disp.A | Volatile Uncorr. ECC | | Fan Temp Perf Pwr:Usage/Cap| Memory-Usage | GPU-Util Compute M. | |===============================+======================+======================| | 0 GeForce GT 710 Off | 00000000:01:00.0 N/A | N/A | | 40% 37C P0 N/A / N/A | 0MiB / 980MiB | N/A Default | +-------------------------------+----------------------+----------------------+ | 1 GeForce GT 710 Off | 00000000:02:00.0 N/A | N/A | | 40% 32C P0 N/A / N/A | 0MiB / 981MiB | N/A Default | +-------------------------------+----------------------+----------------------+   +-----------------------------------------------------------------------------+ | Processes: GPU Memory | | GPU PID Type Process name Usage | |=============================================================================| | 0 Not Supported | | 1 Not Supported | +-----------------------------------------------------------------------------+</p>

<p>reboot!</p>

<p>#prep for Anaconda!  ************************************************************************************************* (I think Anaconda does not require Python 3.7 pre-installation, seems like it does it itself! it also install jupyter etc, a ton of stuff...) #install python 2.7 sudo apt upgrade python (this will do it) #install python 3.7 sudo add-apt-repository ppa:deadsnakes/ppa #python3.7 --version  zihni@zgenc:~$ python3.7 --version  Python 3.7.3</p>

<p> #install conda: The World's Most Popular Python/R Data Science Platform ************************************************************************************************* Linux, Python 3.7 version: https://repo.anaconda.com/archive/Anaconda3-2019.03-Linux-x86_64.sh </p>

<p>... [/home/zihni/anaconda3] >>>  PREFIX=/home/zihni/anaconda3 installing: python-3.7.3-h0371630_0 ... Python 3.7.3 installing: conda-env-2.6.0-1 ... installing: blas-1.0-mkl ... installing: ca-certificates-2019.1.23-0 ... .... installing: statsmodels-0.9.0-py37h035aef0_0 ... installing: seaborn-0.9.0-py37_0 ... installing: anaconda-2019.03-py37_0 ... installation finished. Do you wish the installer to initialize Anaconda3 by running conda init? [yes|no] [no] >>> yes ==> For changes to take effect, close and re-open your current shell. <==</p>

<p>so do it, re-open your shell, or may be better apt update/upgrade/autoremove and reboot.</p>

<p> #update everything with conda ************************************************************************************************* sudo chmod 777 -R /home/zihni/anaconda3 conda update --all</p>

<p> #install cuDNN: NVIDIA cuDNN is a GPU-accelerated library of primitives for deep neural networks. ************************************************************************************************* download runtime/developer/samples deb files for ubuntu 18.04: https://developer.nvidia.com/compute/machine-learning/cudnn/secure/v7.6.1.34/prod/10.1_20190620/Ubuntu18_04-x64/libcudnn7_7.6.1.34-1%2Bcuda10.1_amd64.deb etc...</p>

<p>install:  (base) zihni@zgenc:~$ sudo dpkg -i libcudnn* Selecting previously unselected package libcudnn7. (Reading database ... 155760 files and directories currently installed.) Preparing to unpack libcudnn7_7.6.1.34-1+cuda10.1_amd64.deb ... Unpacking libcudnn7 (7.6.1.34-1+cuda10.1) ... Selecting previously unselected package libcudnn7-dev. Preparing to unpack libcudnn7-dev_7.6.1.34-1+cuda10.1_amd64.deb ... Unpacking libcudnn7-dev (7.6.1.34-1+cuda10.1) ... Selecting previously unselected package libcudnn7-doc. Preparing to unpack libcudnn7-doc_7.6.1.34-1+cuda10.1_amd64.deb ... Unpacking libcudnn7-doc (7.6.1.34-1+cuda10.1) ... Setting up libcudnn7 (7.6.1.34-1+cuda10.1) ... Setting up libcudnn7-dev (7.6.1.34-1+cuda10.1) ... update-alternatives: using /usr/include/x86_64-linux-gnu/cudnn_v7.h to provide /usr/include/cudnn.h (libcudnn) in auto mode Setting up libcudnn7-doc (7.6.1.34-1+cuda10.1) ... Processing triggers for libc-bin (2.27-3ubuntu1) ...</p>

<p> #prepare an conda environmental for TensorFlow and install tf-gpu ************************************************************************************************* conda create -y --name tfgpu python=3.7</p>

<p>when it's done it says: # To activate this environment, use # # $ conda activate tfgpu # # To deactivate an active environment, use # # $ conda deactivate</p>

<p> (base) zihni@zgenc:~$ conda deactivate zihni@zgenc:~$ conda activate tfgpu</p>

<p>#install tensorflow FOR this environment: ************************************************************************************************* (tfgpu) zihni@zgenc:~$ conda install tensorflow-gpu</p>

<p>then test it if tf works under this new environment: (tfgpu) zihni@zgenc:~$ python Python 3.7.3 (default, Mar 27 2019, 22:11:17)  [GCC 7.3.0] :: Anaconda, Inc. on linux Type &quot;help&quot;, &quot;copyright&quot;, &quot;credits&quot; or &quot;license&quot; for more information. >>> import tensorflow as tf >>> print(tf.Session(config=tf.ConfigProto(log_device_placement=True)))</p>

<p>somewhere in the output, it says: 2019-06-29 00:47:59.254849: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1115] Created TensorFlow device (/job:localhost/replica:0/task:0/device:GPU:0 with 732 MB memory) -> physical GPU (device: 0, name: GeForce GT 710, pci bus id: 0000:01:00.0, compute capability: 3.5)</p>

<p>2019-06-29 00:47:59.255119: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1115] Created TensorFlow device (/job:localhost/replica:0/task:0/device:GPU:1 with 734 MB memory) -> physical GPU (device: 1, name: GeForce GT 710, pci bus id: 0000:02:00.0, compute capability: 3.5)</p>

<p>#create another environment for pytorch (this is to work with different DNN frameworks) --you can do it while you're in tfgpu ************************************************************************************************* (tfgpu) zihni@zgenc:~$ conda create -y --name pytorch python=3.7</p>

<p>#switch to pytorch environment and do installations ************************************************************************************************* (tfgpu) zihni@zgenc:~$ conda activate pytorch (pytorch) zihni@zgenc:~$ </p>

<p>#test pytorch environment: ************************************************************************************************* (pytorch) zihni@zgenc:~$ python Python 3.7.3 (default, Mar 27 2019, 22:11:17)  [GCC 7.3.0] :: Anaconda, Inc. on linux Type &quot;help&quot;, &quot;copyright&quot;, &quot;credits&quot; or &quot;license&quot; for more information. >>> import torch >>> print(torch.cuda.get_device_name(0)) GeForce GT 710 >>> print(torch.cuda.get_device_name(1)) GeForce GT 710 >>> </p>

<p>#create another environment for Jupyter Notebook ************************************************************************************************* (pytorch) zihni@zgenc:~$ conda create -y --name jnb python=3.7</p>

<p>#install jupyter etc ************************************************************************************************* conda install -y -q -c numpy matplotlib jupyter nb_conda</p>

<p>#on YOUR machine (the client) ************************************************************************************************* ssh -L 8000:localhost:8888 zihni@zgenc.local</p>

<p>login olduktan sonra server'da:  activate jnb  jupyter notebook</p>

<p>go to localhost:8000 on your machine (client) to see jupyter is working or not...</p>

<p>it works... now, run jupyter notebook and copy the token to setup a password for the web page: (jnb) zihni@zgenc:~$ jupyter notebook</p>

<p> To access the notebook, open this file in a browser:  file:///run/user/1000/jupyter/nbserver-7698-open.html  Or copy and paste one of these URLs:  http://localhost:8888/?token=b555a88b596f20f8fa9b0a07e14a9267bbda874dd0b25ef0</p>

<p>#check the list of conda environments: ************************************************************************************************* (base) zihni@zgenc:~$ conda info --envs  # conda environments: # base * /home/zihni/anaconda3 jnb /home/zihni/anaconda3/envs/jnb pytorch /home/zihni/anaconda3/envs/pytorch tfgpu /home/zihni/anaconda3/envs/tfgpu</p>

<p> #run: ************************************************************************************************* ssh -L 8000:localhost:8888 zihni@zgenc.local on your client computer</p>

<p>copy the token and setup a password, you're done!</p>

<p>#check all conda environments on jupyter notebook website by clicking on Conda tab: ************************************************************************************************* 5 Conda environments  root /home/zihni/anaconda3 anaconda3 /home/zihni/anaconda3 jnb /home/zihni/anaconda3/envs/jnb pytorch /home/zihni/anaconda3/envs/pytorch tfgpu /home/zihni/anaconda3/envs/tfgpu</p>

<p>PS: my tfgpu environment was not visible under New, so I had to run: ************************************************************************************************* (base) zihni@zgenc:~$ conda activate tfgpu (tfgpu) zihni@zgenc:~$ conda install jupyter Collecting package metadata (current_repodata.json): done Solving environment: done ....</p>

<p>and then I logged out/in on jupyter website, it was then visible!</p>

<p> #install keras under tfgpu environment  ************************************************************************************************* (tfgpu) zihni@zgenc:~$ conda install keras Collecting package metadata (current_repodata.json): done Solving environment: done ...</p>

<p>*************************************************************************************************</p>

<p>NOTE: you can run jupyter notebook from any environment (conda install jupyter) SO THAT, you can use only that environment for your all files you create.... so, don't use jnb... it doesn't see your other frameworks...</p>

<p>*************************************************************************************************</p>

<p>NOTE: install missing python modules with pip, ex: pip install --upgrade sklearn</p>

<p>************************************************************************************************* NOTE: install gpustat and watch your gpus: pip install --upgrade gpustat</p>

<p>(base) zihni@zgenc:~$ gpustat zgenc Sat Jun 29 02:18:36 2019 [0] GeForce GT 710 | 37'C, ?? % | 835 / 980 MB | (Not Supported) [1] GeForce GT 710 | 34'C, ?? % | 24 / 981 MB | (Not Supported)</p>

<p>use it with watch, updates every 2 sec.</p>

<p>watch gpustat ************************************************************************************************* NOTE: Add swap For adding 1 gigabyte you would do sudo ./addswap.sh 1 G. For adding 1 megabyte do sudo ./addswap.sh 1 M. Script</p>

<p>This script is also available on my personal GitHub repository.</p>

<p>#!/bin/bash set -e # bail if anything goes wrong</p>

<p>is_root(){  if [ &quot;$( id -u )&quot; -ne 0 ] ; then  return 1  fi  return 0 }</p>

<p>get_swap_amount(){  # Obtain amount of swap in Gigabytes  awk '/SwapTotal/{printf &quot;%.2f&quot;,($2/1048576)}' /proc/meminfo }</p>

<p>make_swap_file(){   # This is the function that does the job of creatig swap file  # and enabling it. All files are timestamped  printf &quot;Current swap ammount: %f\n&quot; &quot;$(get_swap_amount)&quot;  printf &quot;Working on creating swap file\n&quot;  DATE=$(date +%s) # append date of creation to filename  filename=&quot;/swapfile.&quot;&quot;$DATE&quot; # File will be /swapfile.$DATE  dd if=/dev/zero of=&quot;$filename&quot; bs=1&quot;$2&quot; count=&quot;$1&quot;  chmod 600 &quot;$filename&quot;  mkswap &quot;$filename&quot; &amp;&amp;   swapon &quot;$filename&quot; &amp;&amp;   printf &quot;\nCreated and turned on %s\n&quot; &quot;$filename&quot;  printf &quot;Current swap ammount: %f&quot; &quot;$(get_swap_amount)&quot; }</p>

<p> ask_to_enable_on_boot(){  # Prompt user to enable this new swap file on boot. If user  # enters y, the swap file will be added to /etc/fstab  printf &quot;Do you want to turn on this file at boot?[y/n]\n&quot;  read ANSWER  case &quot;$ANSWER&quot; in  [Yy]) printf &quot;\n%s none swap defaults 0 0\n&quot; &quot;$filename&quot; >> /etc/fstab &amp;&amp;  printf &quot;\n %s added to /etc/fstab successfuly\n&quot; &quot;$filename&quot;  exit 0 ;;  [Nn]) printf &quot;Exiting\n&quot; &amp;&amp; exit 0 ;;  *) printf &quot;Wrong input: %s . Exiting. /etc/fstab not altered\n&quot; &quot;$ANSWER&quot; &amp;&amp; exit 1 ;;  esac</p>

<p>}</p>

<p>bad_arguments(){  # check if second argument is a character   case &quot;$2&quot; in   [A-Z]) return 1;;  *) return 0;;  esac</p>

<p> # Check if first argument is a digit.   # https://stackoverflow.com/a/3951175/3701431  case &quot;$1&quot; in  ''|*[!0-9]*) return 0;;  *) return 1 ;;  esac </p>

<p>}</p>

<p>main(){</p>

<p> # Check if we're root and if args are OK. If everything is ok, do stuff</p>

<p> if is_root   then  if [ $# -ne 2 ] || bad_arguments &quot;$@&quot;  then  printf &quot;%s\n&quot; &quot;>>> ERR: $0: bad or insufficient arguments&quot; > /dev/stderr  printf &quot;%s\n&quot; &quot;>>> Usage: $0 INTEGER LETTER&quot; > /dev/stderr  exit 2  fi  make_swap_file &quot;$@&quot; &amp;&amp; ask_to_enable_on_boot  else  printf &quot;>>> ERR: $0 must run as root\n&quot; > /dev/stderr  exit 1  fi }</p>

<p>main &quot;$@&quot;</p>

<p>Test run</p>

<p>$ sudo ./addswap.sh 1 </p>

<p>#run this file and add 8G more... (base) zihni@zgenc:~$ nano add_swap.sh (base) zihni@zgenc:~$ sudo sh add_swap.sh 8 G [sudo] password for zihni:  Current swap ammount: 2.000000 Working on creating swap file 8+0 records in 8+0 records out 8589934592 bytes (8.6 GB, 8.0 GiB) copied, 32.6842 s, 263 MB/s Setting up swapspace version 1, size = 8 GiB (8589930496 bytes) no label, UUID=62ec1943-6133-4016-8416-9ba079854b58</p>

<p>Created and turned on /swapfile.1561791888 Current swap ammount: 10.000000Do you want to turn on this file at boot?[y/n] y</p>

<p> /swapfile.1561791888 added to /etc/fstab successfuly</p>

<p></p>

<p> </p>
