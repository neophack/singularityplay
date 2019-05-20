## Install Singularity >= 2.6

```shell
# install dependency
sudo apt update
sudo apt install build-essential python libarchive-dev

# install singularity
wget https://github.com/sylabs/singularity/releases/download/2.6.1/singularity-2.6.1.tar.gz
tar xzfv singularity-2.6.1.tar.gz
cd singularity-2.6.1
./configure --prefix=/usr/local
make
sudo make install
```
## Create From Docker
```shell
sudo singularity build --writable autoware.img docker://autoware/autoware:1.7.0-kinetic
```
## Test Img
```
$ sudo singularity shell --nv autoware.img 
Singularity: Invoking an interactive shell within container...

Singularity autoware.img:~> nvidia-smi
Mon May 20 07:13:38 2019       
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 410.73       Driver Version: 410.73       CUDA Version: 10.0     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|===============================+======================+======================|
|   0  GeForce GTX 105...  Off  | 00000000:01:00.0 Off |                  N/A |
| N/A   45C    P0    N/A /  N/A |      0MiB /  4042MiB |      2%      Default |
+-------------------------------+----------------------+----------------------+
                                                                               
+-----------------------------------------------------------------------------+
| Processes:                                                       GPU Memory |
|  GPU       PID   Type   Process name                             Usage      |
|=============================================================================|
|  No running processes found                                                 |
+-----------------------------------------------------------------------------+
```
## Test Autoware
```
$ git clone --recurse-submodules https://github.com/lgsvl/Autoware.git -b lgsvl_develop
$ sudo singularity shell --nv --bind Autoware/ autoware.img
$ cd /Autoware/ros
$ rosdep update
$ rosdep install -y --from-paths src --ignore-src --rosdistro kinetic
$ ./catkin_make_release
```

error

1.libcuda.so file not recognized: File truncated
```
ln -s /usr/local/cuda/lib64/stubs/libcuda.so /usr/lib/gcc/x86_64-linux-gnu/5/../../../x86_64-linux-gnu/libcuda.so
```
