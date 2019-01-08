# CUDA-installation-in-Ubuntu-18.04-and-above
I have made list of all the steps that I have done to install CUDA in my Ubuntu 18.04. This will work for any Ubuntu 17.04 and above.
It will take quite a bit to complete the whole process, so please be patient. ( Took me 4 hrs to debug though all the error that came in between. )

Setps to install CUDA in Ubuntu:

1. First open the terminal

2. Enter command  `nvidia-smi`  in terminal to check the installed nvidia driver. If nvidia driver higher than 'nvidia-387' is installed then skip to step 4.

3. If nvidia driver is not installed, execute these command:
```
sudo apt-get purge nvidia*
sudo add-apt-repository ppa:graphics-drivers
sudo apt-get update
sudo apt-get install nvidia-3xx
nvidia-smi
```

4. Once nvidia driver is verified, download .run file
cuda-toolkit-9.1:  https://developer.nvidia.com/cuda-91-download-archive?target_os=Linux&target_arch=x86_64&target_distro=Ubuntu&target_version=1704&target_type=runfilelocal
cuda-toolkit-9.0: https://developer.nvidia.com/cuda-90-download-archive?target_os=Linux&target_arch=x86_64&target_distro=Ubuntu&target_version=1704&target_type=runfilelocal

> I was having problem installing cuda using .deb since it overwrites display driver on its own. So I used .run file. This is signifiacntly easy way. And the CUDA toolkit for Ubuntu 18.04 is not available for downloads. We can use .run file of Ubuntu 17.04 for later versions of Ubuntu as well.

5.  `cd 'go_to_download_dir_of_run_file'`   The .run file should be in read/write mode, if not you can change this by executing:
```sudo chmod +x cuda_9.1.85_387.26_linux.run 
sudo ./cuda_9.1.85_387.26_linux.run --override
```

6. CUDA 9.x need gcc-6 and g++-6 to install. Check of gcc version by typing  `gcc-6 -v` . If gcc version is gcc-6 then you can skip this step. Else in terminal execute:

```
sudo apt install gcc-6
sudo apt install g++-6
```
Then,
```cd '/usr/bin'
sudo rm gcc gcc-ar gcc-nm gcc-ranlib g++
ln -s gcc-6 gcc
ln -s gcc-ar-6 gcc-ar
ln -s gcc-nm-6 gcc-nm
ln gcc-ranlib-6 gcc-ranlib
ln g++-6 g++
```

7. Now go to download dir and install CUDA using .run
```
cd 'go_to_download_dir_of_run_file'
sudo sh cuda_9.1.85_387.26_linux.run
```

8. First it will display the liscence aggrement hit ENTER till you reach end. Then it will prompt you to accept the aggrement. Type  `agree` .

9. Then type  `yes`  to installing with an unsupported configuration?

10. Now comes the most important step, this is where you skip installing drivers that overrites our existing driver. Type  `no`  to Install NVIDIA Accelerated Graphics Driver for Linux-x86_64 38x.xx ?

11. Follow the rest of the prompts as default by just hitting ENTER.

12. At the end of installation it will display that the CUDA toolkit is successfully installed but with some  `Warning` . Don't worry about the warning.

13. The last step will be to add the cuda to PATH variable.
```cd 'to_your_user_dir'
sudo nano ~/.bashrc
```
At the end of the file, type:
```# CUDA
export PATH="/usr/local/cuda/lib64:$PATH"
```
Then ` ctrl+x ` followed by ` y ` and ` ENTER ` will return back to terminal.
Then in your terminal, type:
```
source ~/.bashrc
```

14. Finally type  `nvcc --version` , if every is OKAY, it should display that CUDA 9.x is available for current Nvidia driver. (edited)
