# Preparing a Deep Learning Server on Ubuntu 18.04

**************************************************************
Preparing a Deep Learning Server on Ubuntu 18.04

last updated: 06/28/2019
murat genc
muratagenc@gmail.com 
**************************************************************

Hardware:
2 x GeForce GT 710 1GB GPU
1 x Intel i3
16G DDR3 memory 
250G SSD drive 


## basic o.s. installation
*************************************************************************************************
install ubuntu 18, minimal, using its own keyboard/mouse/monitor
erase the whole disk
network is on dhcp, check the ip before restarting
reboot


### update o.s.
*************************************************************************************************
sudo apt update
sudo apt upgrade
sudo apt autoremove
reboot


### enable remote desktop (just in case)
*************************************************************************************************
sudo apt install -y vino
gnome-control-center sharing
turn sharing on, right upper corner, turn the switch on
screen sharing on (vnc://zgenc.local)
check allow connections to control the secreen,
check require password, type a password
turn on wired connection 1 (or wireless)
test with Remmina or another vnc client


### enable ssh
*************************************************************************************************
sudo apt install openssh-server
test: ssh zihni@zgenc.local


### change root password
*************************************************************************************************
sudo -i
passwd
<type new password twice> 


### install gcc/g++/make/net-tools
*************************************************************************************************
apt install gcc g++ net-tools

check gcc version; gcc --version
apt install build-essential

root@zgenc:~# gcc --version
gcc (Ubuntu 7.4.0-1ubuntu1~18.04.1) 7.4.0
Copyright (C) 2017 Free Software Foundation, Inc


### prepare cuda installation 
*************************************************************************************************
bash -c "echo blacklist nouveau > /etc/modprobe.d/blacklist-nvidia-nouveau.conf"
bash -c "echo options nouveau modeset=0 >> /etc/modprobe.d/blacklist-nvidia-nouveau.conf"

Confirm the content of the new modprobe config file:
cat /etc/modprobe.d/blacklist-nvidia-nouveau.conf
blacklist nouveau
options nouveau modeset=0

Update kernel initramfs
Enter the following linux command to regenerate initramfs:
update-initramfs -u
reboot

### download and install cuda
*************************************************************************************************
become root: su 
wget https://developer.nvidia.com/compute/cuda/10.1/Prod/local_installers/cuda_10.1.168_418.67_linux.run
sh cuda_10.1.168_418.67_linux.run

| CUDA Installer                                                               │
│ - [X] Driver                                                                 │
│      [X] 418.67                                                              │
│ + [X] CUDA Toolkit 10.1                                                      │
│   [X] CUDA Samples 10.1                                                      │
│   [X] CUDA Demo Suite 10.1                                                   │
│   [X] CUDA Documentation 10.1                                                │
│   Options                                                                    │
│   Install    


Done!
===========
= Summary =
===========

Driver:   Installed
Toolkit:  Installed in /usr/local/cuda-10.1/
Samples:  Installed in /root/, but missing recommended libraries

Please make sure that
 -   PATH includes /usr/local/cuda-10.1/bin
 -   LD_LIBRARY_PATH includes /usr/local/cuda-10.1/lib64, or, add /usr/local/cuda-10.1/lib64 to /etc/ld.so.conf and run ldconfig as root

To uninstall the CUDA Toolkit, run cuda-uninstaller in /usr/local/cuda-10.1/bin
To uninstall the NVIDIA Driver, run nvidia-uninstall

Please see CUDA_Installation_Guide_Linux.pdf in /usr/local/cuda-10.1/doc/pdf for detailed information on setting up CUDA.
Logfile is /var/log/cuda-installer.log

### set environmental variables for your user
*************************************************************************************************
exit (no more ROOT!)
export PATH="/usr/local/cuda-10.1/bin:$PATH"

edit /etc/ld.so.conf
include /etc/ld.so.conf.d/*.conf
include /usr/local/cuda-10.1/lib64

run ldconfig as root
root@zgenc:/home/zihni# nano /etc/ld.so.conf
root@zgenc:/home/zihni# ldconfig
root@zgenc:/home/zihni# 



### check nvidia drivers for the GPUs installed
*************************************************************************************************
nvidia-smi

root@zgenc:/home/zihni# nvidia-smi
Fri Jun 28 23:44:47 2019       
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 418.67       Driver Version: 418.67       CUDA Version: 10.1     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|===============================+======================+======================|
|   0  GeForce GT 710      Off  | 00000000:01:00.0 N/A |                  N/A |
| 40%   37C    P0    N/A /  N/A |      0MiB /   980MiB |     N/A      Default |
+-------------------------------+----------------------+----------------------+
|   1  GeForce GT 710      Off  | 00000000:02:00.0 N/A |                  N/A |
| 40%   32C    P0    N/A /  N/A |      0MiB /   981MiB |     N/A      Default |
+-------------------------------+----------------------+----------------------+
                                                                               
+-----------------------------------------------------------------------------+
| Processes:                                                       GPU Memory |
|  GPU       PID   Type   Process name                             Usage      |
|=============================================================================|
|    0                    Not Supported                                       |
|    1                    Not Supported                                       |
+-----------------------------------------------------------------------------+

reboot!

### prep for Anaconda! 
*************************************************************************************************
(I think Anaconda does not require Python 3.7 pre-installation, seems like it does it itself!
it also install jupyter etc, a ton of stuff...)
#install python 2.7
sudo apt upgrade python (this will do it)
#install python 3.7
sudo add-apt-repository ppa:deadsnakes/ppa
#python3.7 --version 
zihni@zgenc:~$ python3.7 --version 
Python 3.7.3


### install conda: The World's Most Popular Python/R Data Science Platform
*************************************************************************************************
Linux, Python 3.7 version: https://repo.anaconda.com/archive/Anaconda3-2019.03-Linux-x86_64.sh 

...
[/home/zihni/anaconda3] >>> 
PREFIX=/home/zihni/anaconda3
installing: python-3.7.3-h0371630_0 ...
Python 3.7.3
installing: conda-env-2.6.0-1 ...
installing: blas-1.0-mkl ...
installing: ca-certificates-2019.1.23-0 ...
....
installing: statsmodels-0.9.0-py37h035aef0_0 ...
installing: seaborn-0.9.0-py37_0 ...
installing: anaconda-2019.03-py37_0 ...
installation finished.
Do you wish the installer to initialize Anaconda3
by running conda init? [yes|no]
[no] >>> yes
==> For changes to take effect, close and re-open your current shell. <==

so do it, re-open your shell, or may be better apt update/upgrade/autoremove and reboot.


### update everything with conda
*************************************************************************************************
sudo chmod 777 -R /home/zihni/anaconda3
conda update --all


### install cuDNN: NVIDIA cuDNN is a GPU-accelerated library of primitives for deep neural networks.
*************************************************************************************************
download runtime/developer/samples deb files for ubuntu 18.04:
https://developer.nvidia.com/compute/machine-learning/cudnn/secure/v7.6.1.34/prod/10.1_20190620/Ubuntu18_04-x64/libcudnn7_7.6.1.34-1%2Bcuda10.1_amd64.deb etc...

install: 
(base) zihni@zgenc:~$ sudo dpkg -i libcudnn*
Selecting previously unselected package libcudnn7.
(Reading database ... 155760 files and directories currently installed.)
Preparing to unpack libcudnn7_7.6.1.34-1+cuda10.1_amd64.deb ...
Unpacking libcudnn7 (7.6.1.34-1+cuda10.1) ...
Selecting previously unselected package libcudnn7-dev.
Preparing to unpack libcudnn7-dev_7.6.1.34-1+cuda10.1_amd64.deb ...
Unpacking libcudnn7-dev (7.6.1.34-1+cuda10.1) ...
Selecting previously unselected package libcudnn7-doc.
Preparing to unpack libcudnn7-doc_7.6.1.34-1+cuda10.1_amd64.deb ...
Unpacking libcudnn7-doc (7.6.1.34-1+cuda10.1) ...
Setting up libcudnn7 (7.6.1.34-1+cuda10.1) ...
Setting up libcudnn7-dev (7.6.1.34-1+cuda10.1) ...
update-alternatives: using /usr/include/x86_64-linux-gnu/cudnn_v7.h to provide /usr/include/cudnn.h (libcudnn) in auto mode
Setting up libcudnn7-doc (7.6.1.34-1+cuda10.1) ...
Processing triggers for libc-bin (2.27-3ubuntu1) ...


### prepare an conda environmental for TensorFlow and install tf-gpu
*************************************************************************************************
conda create -y --name tfgpu python=3.7

when it's done it says:
# To activate this environment, use
#
#     $ conda activate tfgpu
#
# To deactivate an active environment, use
#
#     $ conda deactivate


(base) zihni@zgenc:~$ conda deactivate
zihni@zgenc:~$ conda activate tfgpu

## #install tensorflow FOR this environment:
*************************************************************************************************
(tfgpu) zihni@zgenc:~$ conda install tensorflow-gpu

then test it if tf works under this new environment:
(tfgpu) zihni@zgenc:~$ python
Python 3.7.3 (default, Mar 27 2019, 22:11:17) 
[GCC 7.3.0] :: Anaconda, Inc. on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import tensorflow as tf
>>> print(tf.Session(config=tf.ConfigProto(log_device_placement=True)))

somewhere in the output, it says:
2019-06-29 00:47:59.254849: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1115] Created TensorFlow device (/job:localhost/replica:0/task:0/device:GPU:0 with 732 MB memory) -> physical GPU (device: 0, name: GeForce GT 710, pci bus id: 0000:01:00.0, compute capability: 3.5)

2019-06-29 00:47:59.255119: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1115] Created TensorFlow device (/job:localhost/replica:0/task:0/device:GPU:1 with 734 MB memory) -> physical GPU (device: 1, name: GeForce GT 710, pci bus id: 0000:02:00.0, compute capability: 3.5)

### create another environment for pytorch (this is to work with different DNN frameworks) --you can do it while you're in tfgpu
*************************************************************************************************
(tfgpu) zihni@zgenc:~$ conda create -y --name pytorch python=3.7

### switch to pytorch environment and do installations
*************************************************************************************************
(tfgpu) zihni@zgenc:~$ conda activate pytorch
(pytorch) zihni@zgenc:~$ 

### test pytorch environment:
*************************************************************************************************
(pytorch) zihni@zgenc:~$ python
Python 3.7.3 (default, Mar 27 2019, 22:11:17) 
[GCC 7.3.0] :: Anaconda, Inc. on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import torch
>>> print(torch.cuda.get_device_name(0))
GeForce GT 710
>>> print(torch.cuda.get_device_name(1))
GeForce GT 710
>>> 

### create another environment for Jupyter Notebook
*************************************************************************************************
(pytorch) zihni@zgenc:~$ conda create -y --name jnb python=3.7

#install jupyter etc
*************************************************************************************************
conda install -y -q -c numpy matplotlib jupyter nb_conda

### on YOUR machine (the client)
*************************************************************************************************
ssh -L 8000:localhost:8888 zihni@zgenc.local

login olduktan sonra server'da:
	activate jnb
	jupyter notebook

go to localhost:8000 on your machine (client) to see jupyter is working or not...

it works...
now, run jupyter notebook and copy the token to setup a password for the web page:
(jnb) zihni@zgenc:~$ jupyter notebook

    To access the notebook, open this file in a browser:
        file:///run/user/1000/jupyter/nbserver-7698-open.html
    Or copy and paste one of these URLs:
        http://localhost:8888/?token=b555a88b596f20f8fa9b0a07e14a9267bbda874dd0b25ef0

### check the list of conda environments:
*************************************************************************************************
(base) zihni@zgenc:~$ conda info --envs 
# conda environments:
#
base                  *  /home/zihni/anaconda3
jnb                      /home/zihni/anaconda3/envs/jnb
pytorch                  /home/zihni/anaconda3/envs/pytorch
tfgpu                    /home/zihni/anaconda3/envs/tfgpu


### run:
*************************************************************************************************
ssh -L 8000:localhost:8888 zihni@zgenc.local on your client computer

copy the token and setup a password, you're done!

### check all conda environments on jupyter notebook website by clicking on Conda tab:
*************************************************************************************************
5 Conda environments  
root /home/zihni/anaconda3
anaconda3 /home/zihni/anaconda3
jnb /home/zihni/anaconda3/envs/jnb
pytorch /home/zihni/anaconda3/envs/pytorch
tfgpu /home/zihni/anaconda3/envs/tfgpu

## PS: my tfgpu environment was not visible under New, so I had to run:
*************************************************************************************************
(base) zihni@zgenc:~$ conda activate tfgpu
(tfgpu) zihni@zgenc:~$ conda install jupyter
Collecting package metadata (current_repodata.json): done
Solving environment: done
....

and then I logged out/in on jupyter website, it was then visible!


### install keras under tfgpu environment 
*************************************************************************************************
(tfgpu) zihni@zgenc:~$ conda install keras
Collecting package metadata (current_repodata.json): done
Solving environment: done
...

*************************************************************************************************

## NOTE: you can run jupyter notebook from any environment (conda install jupyter) SO THAT, you can use only that environment for your all files you create.... so, don't use jnb... it doesn't see your other frameworks...

*************************************************************************************************

## NOTE: install missing python modules with pip, ex: pip install --upgrade sklearn

*************************************************************************************************
## NOTE: install gpustat and watch your gpus:
pip install --upgrade gpustat

(base) zihni@zgenc:~$ gpustat
zgenc  Sat Jun 29 02:18:36 2019
[0] GeForce GT 710   | 37'C,  ?? % |   835 /   980 MB | (Not Supported)
[1] GeForce GT 710   | 34'C,  ?? % |    24 /   981 MB | (Not Supported)

use it with watch, updates every 2 sec.

watch gpustat
*************************************************************************************************
## NOTE:
Add swap
For adding 1 gigabyte you would do sudo ./addswap.sh 1 G. For adding 1 megabyte do sudo ./addswap.sh 1 M.
Script

This script is also available on my personal GitHub repository.

#!/bin/bash
set -e  # bail if anything goes wrong

is_root(){
   if [ "$( id -u )" -ne 0  ] ; then
      return 1
   fi
   return 0
}

get_swap_amount(){
    # Obtain amount of swap in Gigabytes
    awk '/SwapTotal/{printf "%.2f",($2/1048576)}' /proc/meminfo
}

make_swap_file(){ 
   # This is the function that does the job of creatig swap file
   # and enabling it.  All files are timestamped
   printf "Current swap ammount: %f\n" "$(get_swap_amount)"
   printf "Working on creating swap file\n"
   DATE=$(date +%s) # append date of creation to filename
   filename="/swapfile.""$DATE" # File will be /swapfile.$DATE
   dd if=/dev/zero  of="$filename" bs=1"$2" count="$1"
   chmod 600 "$filename"
   mkswap "$filename" && 
   swapon "$filename" && 
   printf "\nCreated and turned on %s\n"  "$filename"
   printf "Current swap ammount: %f" "$(get_swap_amount)"
}


ask_to_enable_on_boot(){
   # Prompt user to enable this new swap file on boot. If user
   # enters y, the swap file will be added to /etc/fstab
   printf "Do you want to turn on this file at boot?[y/n]\n"
   read ANSWER
   case "$ANSWER" in
    [Yy]) printf "\n%s none swap defaults 0 0\n" "$filename"  >> /etc/fstab &&
       printf "\n %s added to /etc/fstab successfuly\n" "$filename"
       exit 0 ;;
    [Nn]) printf "Exiting\n" && exit 0 ;;
    *) printf "Wrong input: %s . Exiting. /etc/fstab not altered\n" "$ANSWER" && exit 1 ;;
   esac

}

bad_arguments(){
     # check if second argument is a character 
     case "$2" in 
         [A-Z]) return 1;;
         *) return 0;;
     esac

    # Check if first argument is a digit. 
    # https://stackoverflow.com/a/3951175/3701431
    case "$1" in
        ''|*[!0-9]*) return 0;;
        *) return 1 ;;
    esac 

}

main(){

    # Check if we're root and if args are OK. If everything is ok, do stuff

    if is_root 
    then
        if [ $# -ne 2   ] ||  bad_arguments "$@"
        then
            printf "%s\n" ">>> ERR: $0: bad or insufficient arguments" > /dev/stderr
            printf "%s\n" ">>> Usage: $0 INTEGER LETTER" > /dev/stderr
            exit 2
        fi
        make_swap_file "$@" && ask_to_enable_on_boot
    else
        printf ">>> ERR: $0 must run as root\n" > /dev/stderr
        exit 1
    fi
}

main "$@"

Test run

$ sudo ./addswap.sh 1 

## #run this file and add 8G more...
(base) zihni@zgenc:~$ nano add_swap.sh
(base) zihni@zgenc:~$ sudo sh add_swap.sh 8 G
[sudo] password for zihni: 
Current swap ammount: 2.000000
Working on creating swap file
8+0 records in
8+0 records out
8589934592 bytes (8.6 GB, 8.0 GiB) copied, 32.6842 s, 263 MB/s
Setting up swapspace version 1, size = 8 GiB (8589930496 bytes)
no label, UUID=62ec1943-6133-4016-8416-9ba079854b58

Created and turned on /swapfile.1561791888
Current swap ammount: 10.000000Do you want to turn on this file at boot?[y/n]
y

 /swapfile.1561791888 added to /etc/fstab successfuly




