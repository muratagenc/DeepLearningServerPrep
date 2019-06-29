<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.0 Transitional//EN">
<html>
<head>
	<meta http-equiv="content-type" content="text/html; charset=utf-8"/>
	<title></title>
	<meta name="generator" content="LibreOffice 6.0.7.3 (Linux)"/>
	<meta name="created" content="2019-06-29T03:18:27.205672637"/>
	<meta name="changed" content="2019-06-29T03:19:21.350933395"/>
	<style type="text/css">
		@page { margin: 0.79in }
		p { margin-bottom: 0.1in; line-height: 115% }
	</style>
</head>
<body lang="en-US" dir="ltr">
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">**************************************************************</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">Preparing
a Deep Learning Server on Ubuntu 18.04</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">last
updated: 06/28/2019</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">murat
genc</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">muratagenc@gmail.com
</font>
</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">**************************************************************</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">Hardware:</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">2
x GeForce GT 710 1GB GPU</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">1
x Intel i3</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">16G
DDR3 memory </font>
</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">250G
SSD drive </font>
</p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">#basic
o.s. installation</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">*************************************************************************************************</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">install
ubuntu 18, minimal, using its own keyboard/mouse/monitor</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">erase
the whole disk</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">network
is on dhcp, check the ip before restarting</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">reboot</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">#update
o.s.</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">*************************************************************************************************</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">sudo
apt update</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">sudo
apt upgrade</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">sudo
apt autoremove</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">reboot</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">#enable
remote desktop (just in case)</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">*************************************************************************************************</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">sudo
apt install -y vino</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">gnome-control-center
sharing</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">turn
sharing on, right upper corner, turn the switch on</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">screen
sharing on (vnc://zgenc.local)</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">check
allow connections to control the secreen,</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">check
require password, type a password</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">turn
on wired connection 1 (or wireless)</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">test
with Remmina or another vnc client</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">#enable
ssh</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">*************************************************************************************************</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">sudo
apt install openssh-server</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">test:
ssh zihni@zgenc.local</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">#change
root password</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">*************************************************************************************************</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">sudo
-i</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">passwd</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">&lt;type
new password twice&gt; </font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">#install
gcc/g++/make/net-tools</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">*************************************************************************************************</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">apt
install gcc g++ net-tools</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">check
gcc version; gcc --version</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">apt
install build-essential</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">root@zgenc:~#
gcc --version</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">gcc
(Ubuntu 7.4.0-1ubuntu1~18.04.1) 7.4.0</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">Copyright
(C) 2017 Free Software Foundation, Inc</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">#prepare
cuda installation </font>
</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">*************************************************************************************************</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">bash
-c &quot;echo blacklist nouveau &gt;
/etc/modprobe.d/blacklist-nvidia-nouveau.conf&quot;</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">bash
-c &quot;echo options nouveau modeset=0 &gt;&gt;
/etc/modprobe.d/blacklist-nvidia-nouveau.conf&quot;</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">Confirm
the content of the new modprobe config file:</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">cat
/etc/modprobe.d/blacklist-nvidia-nouveau.conf</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">blacklist
nouveau</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">options
nouveau modeset=0</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">Update
kernel initramfs</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">Enter
the following linux command to regenerate initramfs:</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">update-initramfs
-u</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">reboot</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">#download
and install cuda</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">*************************************************************************************************</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">become
root: su </font>
</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">wget
https://developer.nvidia.com/compute/cuda/10.1/Prod/local_installers/cuda_10.1.168_418.67_linux.run</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">sh
cuda_10.1.168_418.67_linux.run</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">|
CUDA Installer                                                       
       │</font></p>
<p style="margin-bottom: 0in; line-height: 100%">│ <font face="FreeMono, monospace">-
[X] Driver                                                           
     │</font></p>
<p style="margin-bottom: 0in; line-height: 100%">│      <font face="FreeMono, monospace">[X]
418.67                                                              │</font></p>
<p style="margin-bottom: 0in; line-height: 100%">│ <font face="FreeMono, monospace">+
[X] CUDA Toolkit 10.1                                                
     │</font></p>
<p style="margin-bottom: 0in; line-height: 100%">│   <font face="FreeMono, monospace">[X]
CUDA Samples 10.1                                                    
 │</font></p>
<p style="margin-bottom: 0in; line-height: 100%">│   <font face="FreeMono, monospace">[X]
CUDA Demo Suite 10.1                                                 
 │</font></p>
<p style="margin-bottom: 0in; line-height: 100%">│   <font face="FreeMono, monospace">[X]
CUDA Documentation 10.1                                              
 │</font></p>
<p style="margin-bottom: 0in; line-height: 100%">│   <font face="FreeMono, monospace">Options
                                                                   │</font></p>
<p style="margin-bottom: 0in; line-height: 100%">│   <font face="FreeMono, monospace">Install
   </font>
</p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">Done!</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">===========</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">=
Summary =</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">===========</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">Driver:
  Installed</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">Toolkit:
 Installed in /usr/local/cuda-10.1/</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">Samples:
 Installed in /root/, but missing recommended libraries</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">Please
make sure that</font></p>
<p style="margin-bottom: 0in; line-height: 100%"> <font face="FreeMono, monospace">-
  PATH includes /usr/local/cuda-10.1/bin</font></p>
<p style="margin-bottom: 0in; line-height: 100%"> <font face="FreeMono, monospace">-
  LD_LIBRARY_PATH includes /usr/local/cuda-10.1/lib64, or, add
/usr/local/cuda-10.1/lib64 to /etc/ld.so.conf and run ldconfig as
root</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">To
uninstall the CUDA Toolkit, run cuda-uninstaller in
/usr/local/cuda-10.1/bin</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">To
uninstall the NVIDIA Driver, run nvidia-uninstall</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">Please
see CUDA_Installation_Guide_Linux.pdf in /usr/local/cuda-10.1/doc/pdf
for detailed information on setting up CUDA.</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">Logfile
is /var/log/cuda-installer.log</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">#set
environmental variables for your user</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">*************************************************************************************************</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">exit
(no more ROOT!)</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">export
PATH=&quot;/usr/local/cuda-10.1/bin:$PATH&quot;</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">edit
/etc/ld.so.conf</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">include
/etc/ld.so.conf.d/*.conf</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">include
/usr/local/cuda-10.1/lib64</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">run
ldconfig as root</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">root@zgenc:/home/zihni#
nano /etc/ld.so.conf</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">root@zgenc:/home/zihni#
ldconfig</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">root@zgenc:/home/zihni#
</font>
</p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">#check
nvidia drivers for the GPUs installed</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">*************************************************************************************************</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">nvidia-smi</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">root@zgenc:/home/zihni#
nvidia-smi</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">Fri
Jun 28 23:44:47 2019       </font>
</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">+-----------------------------------------------------------------------------+</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">|
NVIDIA-SMI 418.67       Driver Version: 418.67       CUDA Version:
10.1     |</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">|-------------------------------+----------------------+----------------------+</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">|
GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile
Uncorr. ECC |</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">|
Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util 
Compute M. |</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">|===============================+======================+======================|</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">|
  0  GeForce GT 710      Off  | 00000000:01:00.0 N/A |               
  N/A |</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">|
40%   37C    P0    N/A /  N/A |      0MiB /   980MiB |     N/A     
Default |</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">+-------------------------------+----------------------+----------------------+</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">|
  1  GeForce GT 710      Off  | 00000000:02:00.0 N/A |               
  N/A |</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">|
40%   32C    P0    N/A /  N/A |      0MiB /   981MiB |     N/A     
Default |</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">+-------------------------------+----------------------+----------------------+</font></p>
<p style="margin-bottom: 0in; line-height: 100%">                    
                                                          
</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">+-----------------------------------------------------------------------------+</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">|
Processes:                                                       GPU
Memory |</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">|
 GPU       PID   Type   Process name                            
Usage      |</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">|=============================================================================|</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">|
   0                    Not Supported                                
      |</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">|
   1                    Not Supported                                
      |</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">+-----------------------------------------------------------------------------+</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">reboot!</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">#prep
for Anaconda! </font>
</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">*************************************************************************************************</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">(I
think Anaconda does not require Python 3.7 pre-installation, seems
like it does it itself!</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">it
also install jupyter etc, a ton of stuff...)</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">#install
python 2.7</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">sudo
apt upgrade python (this will do it)</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">#install
python 3.7</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">sudo
add-apt-repository ppa:deadsnakes/ppa</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">#python3.7
--version </font>
</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">zihni@zgenc:~$
python3.7 --version </font>
</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">Python
3.7.3</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">#install
conda: The World's Most Popular Python/R Data Science Platform</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">*************************************************************************************************</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">Linux,
Python 3.7 version:
https://repo.anaconda.com/archive/Anaconda3-2019.03-Linux-x86_64.sh </font>
</p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">...</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">[/home/zihni/anaconda3]
&gt;&gt;&gt; </font>
</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">PREFIX=/home/zihni/anaconda3</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">installing:
python-3.7.3-h0371630_0 ...</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">Python
3.7.3</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">installing:
conda-env-2.6.0-1 ...</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">installing:
blas-1.0-mkl ...</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">installing:
ca-certificates-2019.1.23-0 ...</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">....</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">installing:
statsmodels-0.9.0-py37h035aef0_0 ...</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">installing:
seaborn-0.9.0-py37_0 ...</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">installing:
anaconda-2019.03-py37_0 ...</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">installation
finished.</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">Do
you wish the installer to initialize Anaconda3</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">by
running conda init? [yes|no]</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">[no]
&gt;&gt;&gt; yes</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">==&gt;
For changes to take effect, close and re-open your current shell. &lt;==</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">so
do it, re-open your shell, or may be better apt
update/upgrade/autoremove and reboot.</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">#update
everything with conda</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">*************************************************************************************************</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">sudo
chmod 777 -R /home/zihni/anaconda3</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">conda
update --all</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">#install
cuDNN: NVIDIA cuDNN is a GPU-accelerated library of primitives for
deep neural networks.</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">*************************************************************************************************</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">download
runtime/developer/samples deb files for ubuntu 18.04:</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">https://developer.nvidia.com/compute/machine-learning/cudnn/secure/v7.6.1.34/prod/10.1_20190620/Ubuntu18_04-x64/libcudnn7_7.6.1.34-1%2Bcuda10.1_amd64.deb
etc...</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">install:
</font>
</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">(base)
zihni@zgenc:~$ sudo dpkg -i libcudnn*</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">Selecting
previously unselected package libcudnn7.</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">(Reading
database ... 155760 files and directories currently installed.)</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">Preparing
to unpack libcudnn7_7.6.1.34-1+cuda10.1_amd64.deb ...</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">Unpacking
libcudnn7 (7.6.1.34-1+cuda10.1) ...</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">Selecting
previously unselected package libcudnn7-dev.</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">Preparing
to unpack libcudnn7-dev_7.6.1.34-1+cuda10.1_amd64.deb ...</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">Unpacking
libcudnn7-dev (7.6.1.34-1+cuda10.1) ...</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">Selecting
previously unselected package libcudnn7-doc.</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">Preparing
to unpack libcudnn7-doc_7.6.1.34-1+cuda10.1_amd64.deb ...</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">Unpacking
libcudnn7-doc (7.6.1.34-1+cuda10.1) ...</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">Setting
up libcudnn7 (7.6.1.34-1+cuda10.1) ...</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">Setting
up libcudnn7-dev (7.6.1.34-1+cuda10.1) ...</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">update-alternatives:
using /usr/include/x86_64-linux-gnu/cudnn_v7.h to provide
/usr/include/cudnn.h (libcudnn) in auto mode</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">Setting
up libcudnn7-doc (7.6.1.34-1+cuda10.1) ...</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">Processing
triggers for libc-bin (2.27-3ubuntu1) ...</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">#prepare
an conda environmental for TensorFlow and install tf-gpu</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">*************************************************************************************************</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">conda
create -y --name tfgpu python=3.7</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">when
it's done it says:</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">#
To activate this environment, use</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">#</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">#
    $ conda activate tfgpu</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">#</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">#
To deactivate an active environment, use</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">#</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">#
    $ conda deactivate</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">(base)
zihni@zgenc:~$ conda deactivate</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">zihni@zgenc:~$
conda activate tfgpu</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">#install
tensorflow FOR this environment:</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">*************************************************************************************************</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">(tfgpu)
zihni@zgenc:~$ conda install tensorflow-gpu</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">then
test it if tf works under this new environment:</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">(tfgpu)
zihni@zgenc:~$ python</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">Python
3.7.3 (default, Mar 27 2019, 22:11:17) </font>
</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">[GCC
7.3.0] :: Anaconda, Inc. on linux</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">Type
&quot;help&quot;, &quot;copyright&quot;, &quot;credits&quot; or
&quot;license&quot; for more information.</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">&gt;&gt;&gt;
import tensorflow as tf</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">&gt;&gt;&gt;
print(tf.Session(config=tf.ConfigProto(log_device_placement=True)))</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">somewhere
in the output, it says:</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">2019-06-29
00:47:59.254849: I
tensorflow/core/common_runtime/gpu/gpu_device.cc:1115] Created
TensorFlow device (/job:localhost/replica:0/task:0/device:GPU:0 with
732 MB memory) -&gt; physical GPU (device: 0, name: GeForce GT 710,
pci bus id: 0000:01:00.0, compute capability: 3.5)</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">2019-06-29
00:47:59.255119: I
tensorflow/core/common_runtime/gpu/gpu_device.cc:1115] Created
TensorFlow device (/job:localhost/replica:0/task:0/device:GPU:1 with
734 MB memory) -&gt; physical GPU (device: 1, name: GeForce GT 710,
pci bus id: 0000:02:00.0, compute capability: 3.5)</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">#create
another environment for pytorch (this is to work with different DNN
frameworks) --you can do it while you're in tfgpu</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">*************************************************************************************************</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">(tfgpu)
zihni@zgenc:~$ conda create -y --name pytorch python=3.7</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">#switch
to pytorch environment and do installations</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">*************************************************************************************************</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">(tfgpu)
zihni@zgenc:~$ conda activate pytorch</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">(pytorch)
zihni@zgenc:~$ </font>
</p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">#test
pytorch environment:</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">*************************************************************************************************</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">(pytorch)
zihni@zgenc:~$ python</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">Python
3.7.3 (default, Mar 27 2019, 22:11:17) </font>
</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">[GCC
7.3.0] :: Anaconda, Inc. on linux</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">Type
&quot;help&quot;, &quot;copyright&quot;, &quot;credits&quot; or
&quot;license&quot; for more information.</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">&gt;&gt;&gt;
import torch</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">&gt;&gt;&gt;
print(torch.cuda.get_device_name(0))</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">GeForce
GT 710</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">&gt;&gt;&gt;
print(torch.cuda.get_device_name(1))</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">GeForce
GT 710</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">&gt;&gt;&gt;
</font>
</p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">#create
another environment for Jupyter Notebook</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">*************************************************************************************************</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">(pytorch)
zihni@zgenc:~$ conda create -y --name jnb python=3.7</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">#install
jupyter etc</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">*************************************************************************************************</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">conda
install -y -q -c numpy matplotlib jupyter nb_conda</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">#on
YOUR machine (the client)</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">*************************************************************************************************</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">ssh
-L 8000:localhost:8888 zihni@zgenc.local</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">login
olduktan sonra server'da:</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">	activate
jnb</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">	jupyter
notebook</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">go
to localhost:8000 on your machine (client) to see jupyter is working
or not...</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">it
works...</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">now,
run jupyter notebook and copy the token to setup a password for the
web page:</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">(jnb)
zihni@zgenc:~$ jupyter notebook</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%">    <font face="FreeMono, monospace">To
access the notebook, open this file in a browser:</font></p>
<p style="margin-bottom: 0in; line-height: 100%">       
<font face="FreeMono, monospace">file:///run/user/1000/jupyter/nbserver-7698-open.html</font></p>
<p style="margin-bottom: 0in; line-height: 100%">    <font face="FreeMono, monospace">Or
copy and paste one of these URLs:</font></p>
<p style="margin-bottom: 0in; line-height: 100%">       
<font face="FreeMono, monospace">http://localhost:8888/?token=b555a88b596f20f8fa9b0a07e14a9267bbda874dd0b25ef0</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">#check
the list of conda environments:</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">*************************************************************************************************</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">(base)
zihni@zgenc:~$ conda info --envs </font>
</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">#
conda environments:</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">#</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">base
                 *  /home/zihni/anaconda3</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">jnb
                     /home/zihni/anaconda3/envs/jnb</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">pytorch
                 /home/zihni/anaconda3/envs/pytorch</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">tfgpu
                   /home/zihni/anaconda3/envs/tfgpu</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">#run:</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">*************************************************************************************************</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">ssh
-L 8000:localhost:8888 zihni@zgenc.local on your client computer</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">copy
the token and setup a password, you're done!</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">#check
all conda environments on jupyter notebook website by clicking on
Conda tab:</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">*************************************************************************************************</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">5
Conda environments  </font>
</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">root
/home/zihni/anaconda3</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">anaconda3
/home/zihni/anaconda3</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">jnb
/home/zihni/anaconda3/envs/jnb</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">pytorch
/home/zihni/anaconda3/envs/pytorch</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">tfgpu
/home/zihni/anaconda3/envs/tfgpu</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">PS:
my tfgpu environment was not visible under New, so I had to run:</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">*************************************************************************************************</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">(base)
zihni@zgenc:~$ conda activate tfgpu</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">(tfgpu)
zihni@zgenc:~$ conda install jupyter</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">Collecting
package metadata (current_repodata.json): done</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">Solving
environment: done</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">....</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">and
then I logged out/in on jupyter website, it was then visible!</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">#install
keras under tfgpu environment </font>
</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">*************************************************************************************************</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">(tfgpu)
zihni@zgenc:~$ conda install keras</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">Collecting
package metadata (current_repodata.json): done</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">Solving
environment: done</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">...</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">*************************************************************************************************</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">NOTE:
you can run jupyter notebook from any environment (conda install
jupyter) SO THAT, you can use only that environment for your all
files you create.... so, don't use jnb... it doesn't see your other
frameworks...</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">*************************************************************************************************</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">NOTE:
install missing python modules with pip, ex: pip install --upgrade
sklearn</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">*************************************************************************************************</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">NOTE:
install gpustat and watch your gpus:</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">pip
install --upgrade gpustat</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">(base)
zihni@zgenc:~$ gpustat</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">zgenc
 Sat Jun 29 02:18:36 2019</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">[0]
GeForce GT 710   | 37'C,  ?? % |   835 /   980 MB | (Not Supported)</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">[1]
GeForce GT 710   | 34'C,  ?? % |    24 /   981 MB | (Not Supported)</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">use
it with watch, updates every 2 sec.</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">watch
gpustat</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">*************************************************************************************************</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">NOTE:</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">Add
swap</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">For
adding 1 gigabyte you would do sudo ./addswap.sh 1 G. For adding 1
megabyte do sudo ./addswap.sh 1 M.</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">Script</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">This
script is also available on my personal GitHub repository.</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">#!/bin/bash</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">set
-e  # bail if anything goes wrong</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">is_root(){</font></p>
<p style="margin-bottom: 0in; line-height: 100%">   <font face="FreeMono, monospace">if
[ &quot;$( id -u )&quot; -ne 0  ] ; then</font></p>
<p style="margin-bottom: 0in; line-height: 100%">      <font face="FreeMono, monospace">return
1</font></p>
<p style="margin-bottom: 0in; line-height: 100%">   <font face="FreeMono, monospace">fi</font></p>
<p style="margin-bottom: 0in; line-height: 100%">   <font face="FreeMono, monospace">return
0</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">}</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">get_swap_amount(){</font></p>
<p style="margin-bottom: 0in; line-height: 100%">    <font face="FreeMono, monospace">#
Obtain amount of swap in Gigabytes</font></p>
<p style="margin-bottom: 0in; line-height: 100%">    <font face="FreeMono, monospace">awk
'/SwapTotal/{printf &quot;%.2f&quot;,($2/1048576)}' /proc/meminfo</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">}</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">make_swap_file(){
</font>
</p>
<p style="margin-bottom: 0in; line-height: 100%">   <font face="FreeMono, monospace">#
This is the function that does the job of creatig swap file</font></p>
<p style="margin-bottom: 0in; line-height: 100%">   <font face="FreeMono, monospace">#
and enabling it.  All files are timestamped</font></p>
<p style="margin-bottom: 0in; line-height: 100%">   <font face="FreeMono, monospace">printf
&quot;Current swap ammount: %f\n&quot; &quot;$(get_swap_amount)&quot;</font></p>
<p style="margin-bottom: 0in; line-height: 100%">   <font face="FreeMono, monospace">printf
&quot;Working on creating swap file\n&quot;</font></p>
<p style="margin-bottom: 0in; line-height: 100%">   <font face="FreeMono, monospace">DATE=$(date
+%s) # append date of creation to filename</font></p>
<p style="margin-bottom: 0in; line-height: 100%">  
<font face="FreeMono, monospace">filename=&quot;/swapfile.&quot;&quot;$DATE&quot;
# File will be /swapfile.$DATE</font></p>
<p style="margin-bottom: 0in; line-height: 100%">   <font face="FreeMono, monospace">dd
if=/dev/zero  of=&quot;$filename&quot; bs=1&quot;$2&quot; count=&quot;$1&quot;</font></p>
<p style="margin-bottom: 0in; line-height: 100%">   <font face="FreeMono, monospace">chmod
600 &quot;$filename&quot;</font></p>
<p style="margin-bottom: 0in; line-height: 100%">   <font face="FreeMono, monospace">mkswap
&quot;$filename&quot; &amp;&amp; </font>
</p>
<p style="margin-bottom: 0in; line-height: 100%">   <font face="FreeMono, monospace">swapon
&quot;$filename&quot; &amp;&amp; </font>
</p>
<p style="margin-bottom: 0in; line-height: 100%">   <font face="FreeMono, monospace">printf
&quot;\nCreated and turned on %s\n&quot;  &quot;$filename&quot;</font></p>
<p style="margin-bottom: 0in; line-height: 100%">   <font face="FreeMono, monospace">printf
&quot;Current swap ammount: %f&quot; &quot;$(get_swap_amount)&quot;</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">}</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">ask_to_enable_on_boot(){</font></p>
<p style="margin-bottom: 0in; line-height: 100%">   <font face="FreeMono, monospace">#
Prompt user to enable this new swap file on boot. If user</font></p>
<p style="margin-bottom: 0in; line-height: 100%">   <font face="FreeMono, monospace">#
enters y, the swap file will be added to /etc/fstab</font></p>
<p style="margin-bottom: 0in; line-height: 100%">   <font face="FreeMono, monospace">printf
&quot;Do you want to turn on this file at boot?[y/n]\n&quot;</font></p>
<p style="margin-bottom: 0in; line-height: 100%">   <font face="FreeMono, monospace">read
ANSWER</font></p>
<p style="margin-bottom: 0in; line-height: 100%">   <font face="FreeMono, monospace">case
&quot;$ANSWER&quot; in</font></p>
<p style="margin-bottom: 0in; line-height: 100%">    <font face="FreeMono, monospace">[Yy])
printf &quot;\n%s none swap defaults 0 0\n&quot; &quot;$filename&quot;
 &gt;&gt; /etc/fstab &amp;&amp;</font></p>
<p style="margin-bottom: 0in; line-height: 100%">       <font face="FreeMono, monospace">printf
&quot;\n %s added to /etc/fstab successfuly\n&quot; &quot;$filename&quot;</font></p>
<p style="margin-bottom: 0in; line-height: 100%">       <font face="FreeMono, monospace">exit
0 ;;</font></p>
<p style="margin-bottom: 0in; line-height: 100%">    <font face="FreeMono, monospace">[Nn])
printf &quot;Exiting\n&quot; &amp;&amp; exit 0 ;;</font></p>
<p style="margin-bottom: 0in; line-height: 100%">    <font face="FreeMono, monospace">*)
printf &quot;Wrong input: %s . Exiting. /etc/fstab not altered\n&quot;
&quot;$ANSWER&quot; &amp;&amp; exit 1 ;;</font></p>
<p style="margin-bottom: 0in; line-height: 100%">   <font face="FreeMono, monospace">esac</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">}</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">bad_arguments(){</font></p>
<p style="margin-bottom: 0in; line-height: 100%">     <font face="FreeMono, monospace">#
check if second argument is a character </font>
</p>
<p style="margin-bottom: 0in; line-height: 100%">     <font face="FreeMono, monospace">case
&quot;$2&quot; in </font>
</p>
<p style="margin-bottom: 0in; line-height: 100%">         <font face="FreeMono, monospace">[A-Z])
return 1;;</font></p>
<p style="margin-bottom: 0in; line-height: 100%">         <font face="FreeMono, monospace">*)
return 0;;</font></p>
<p style="margin-bottom: 0in; line-height: 100%">     <font face="FreeMono, monospace">esac</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%">    <font face="FreeMono, monospace">#
Check if first argument is a digit. </font>
</p>
<p style="margin-bottom: 0in; line-height: 100%">    <font face="FreeMono, monospace">#
https://stackoverflow.com/a/3951175/3701431</font></p>
<p style="margin-bottom: 0in; line-height: 100%">    <font face="FreeMono, monospace">case
&quot;$1&quot; in</font></p>
<p style="margin-bottom: 0in; line-height: 100%">        <font face="FreeMono, monospace">''|*[!0-9]*)
return 0;;</font></p>
<p style="margin-bottom: 0in; line-height: 100%">        <font face="FreeMono, monospace">*)
return 1 ;;</font></p>
<p style="margin-bottom: 0in; line-height: 100%">    <font face="FreeMono, monospace">esac
</font>
</p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">}</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">main(){</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%">    <font face="FreeMono, monospace">#
Check if we're root and if args are OK. If everything is ok, do stuff</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%">    <font face="FreeMono, monospace">if
is_root </font>
</p>
<p style="margin-bottom: 0in; line-height: 100%">    <font face="FreeMono, monospace">then</font></p>
<p style="margin-bottom: 0in; line-height: 100%">        <font face="FreeMono, monospace">if
[ $# -ne 2   ] ||  bad_arguments &quot;$@&quot;</font></p>
<p style="margin-bottom: 0in; line-height: 100%">        <font face="FreeMono, monospace">then</font></p>
<p style="margin-bottom: 0in; line-height: 100%">            <font face="FreeMono, monospace">printf
&quot;%s\n&quot; &quot;&gt;&gt;&gt; ERR: $0: bad or insufficient
arguments&quot; &gt; /dev/stderr</font></p>
<p style="margin-bottom: 0in; line-height: 100%">            <font face="FreeMono, monospace">printf
&quot;%s\n&quot; &quot;&gt;&gt;&gt; Usage: $0 INTEGER LETTER&quot; &gt;
/dev/stderr</font></p>
<p style="margin-bottom: 0in; line-height: 100%">            <font face="FreeMono, monospace">exit
2</font></p>
<p style="margin-bottom: 0in; line-height: 100%">        <font face="FreeMono, monospace">fi</font></p>
<p style="margin-bottom: 0in; line-height: 100%">       
<font face="FreeMono, monospace">make_swap_file &quot;$@&quot; &amp;&amp;
ask_to_enable_on_boot</font></p>
<p style="margin-bottom: 0in; line-height: 100%">    <font face="FreeMono, monospace">else</font></p>
<p style="margin-bottom: 0in; line-height: 100%">        <font face="FreeMono, monospace">printf
&quot;&gt;&gt;&gt; ERR: $0 must run as root\n&quot; &gt; /dev/stderr</font></p>
<p style="margin-bottom: 0in; line-height: 100%">        <font face="FreeMono, monospace">exit
1</font></p>
<p style="margin-bottom: 0in; line-height: 100%">    <font face="FreeMono, monospace">fi</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">}</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">main
&quot;$@&quot;</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">Test
run</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">$
sudo ./addswap.sh 1 </font>
</p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">#run
this file and add 8G more...</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">(base)
zihni@zgenc:~$ nano add_swap.sh</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">(base)
zihni@zgenc:~$ sudo sh add_swap.sh 8 G</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">[sudo]
password for zihni: </font>
</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">Current
swap ammount: 2.000000</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">Working
on creating swap file</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">8+0
records in</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">8+0
records out</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">8589934592
bytes (8.6 GB, 8.0 GiB) copied, 32.6842 s, 263 MB/s</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">Setting
up swapspace version 1, size = 8 GiB (8589930496 bytes)</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">no
label, UUID=62ec1943-6133-4016-8416-9ba079854b58</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">Created
and turned on /swapfile.1561791888</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">Current
swap ammount: 10.000000Do you want to turn on this file at boot?[y/n]</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><font face="FreeMono, monospace">y</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%">
<font face="FreeMono, monospace">/swapfile.1561791888 added to
/etc/fstab successfuly</font></p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
<p style="margin-bottom: 0in; line-height: 100%"><br/>

</p>
</body>
</html>
