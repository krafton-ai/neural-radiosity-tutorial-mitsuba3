# (Almost) Everything about installing dependencies
## Installation
Test environment
- Ubuntu 20.4
- NVIDIA driver version 515.86.01
- CUDA driver version 11.7
- CUDA runtime version 11.7
- GCC >= 8
- CMake >= 3.21

```bash
git clone https://{}/neural-radiosity-repr.git
python3 -m pip install --upgrade pip
pip install matplotlib==3.7.1 mitsuba==3.2.1 ninja==1.11.1 torch==1.13.1 torchvision==0.14.1 tqdm==4.65.0 imageio==2.25.0 opencv-python==4.7.0.72
```

To install Tiny-CUDA-NN, check the [official documentation](https://github.com/NVlabs/tiny-cuda-nn#pytorch-extension).
In short, 
```bash
# but first, you may need to update CUDA toolkit and CMake as the following sections
apt-get install build-essential git python3-dev python3-pip libopenexr-dev libxi-dev libglfw3-dev libglew-dev libomp-dev libxinerama-dev libxcursor-dev ffmpeg
pip install "git+https://github.com/NVlabs/tiny-cuda-nn/#subdirectory=bindings/torch"
```

## When you encounter 'no LLVM.so' error while using 'llvm_ad_rgb' variant of Mitsuba3
```bash
# if you encounter something like 'no LLVM.so' error,
apt-get update
apt-get -y install llvm
find / -iname libLLVM.so  # verify the installation
pip uninstall mitsuba drjit
pip install -r requirements.txt
```

## Installation on WSL

1. Go to Microsoft Store and install Windows Subsystem for Linux (WSL). See [here](https://learn.microsoft.com/en-us/windows/wsl/install) for more detailed information.
2. Go to Microsoft Store and install VSCode.
3. Open a VSCode window, and install the `WSL` extension from VSCode. See [here](https://jmcunst.tistory.com/152) if you are not aware of VSCode Extensions.
4. In a VSCode window, press `ctrl+shift+p` and write `WSL` to find `WSL: Connect to WSL` option. You can now open a VSCode window on a virtualized Ubuntu environment by pressing the option. See [here](https://learn.microsoft.com/ko-kr/windows/wsl/tutorials/wsl-vscode#from-vs-code) if you are not aware of the `ctrl+shift+p` command in VSCode.
5. The remaining steps are the same as in the [Installation](#installation) section above.

## Update CUDA Toolkit

- For instance, Tiny-CUDA-NN requires a recent verion of CUDA toolkit which is 11.5 or higher.
- To install, CUDA toolkit 11.7, follow the [link](https://developer.nvidia.com/cuda-11-7-0-download-archive?target_os=Linux&target_arch=x86_64&Distribution=Ubuntu&target_version=20.04&target_type=runfile_local)
- You can also find other versions of toolkits in the [NVIDIA archive](https://developer.nvidia.com/cuda-toolkit-archive)
- Anyway the above 11.7 link will introduce the following installation instructions:
```bash
wget https://developer.download.nvidia.com/compute/cuda/11.7.0/local_installers/cuda_11.7.0_515.43.04_linux.run
sh cuda_11.7.0_515.43.04_linux.run

# 1. accept the license stuff
# 2. uncheck `Driver`, `CUDA Samples xx.x`, `CUDA Demo Suite xx.x`, `CUDA Documentation  xx.x`.
#    we only need 'CUDA Toolkit xx.x`
```
- After the installation is finished, open `~/.bashrc` and add some paths as follow.
```vim
...
export PATH=/usr/local/cuda-11.7/bin:$PATH
export LD_LIBRARY_PATH=/usr/local/cuda-11.7/lib64
```

## Update CMake
- Get the [CMake binary](https://cmake.org/download/) for Linux such as `cmake-3.26.0-rc6-linux-x86_64.sh`.
- Install the binary by hitting `sh cmake-3.26.0-rc6-linux-x86_64.sh`.
- Add some environment variables
```vim
...
export PATH=~/cmake-3.26.0-rc6-linux-x86_64/bin:$PATH
export CMAKE_PREFIX_PATH=~/cmake-3.26.0-rc6-linux-x86_64:$CMAKE_PREFIX_PATH
```