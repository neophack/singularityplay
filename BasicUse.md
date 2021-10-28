## Install Singularity >= 2.6

```shell
# install dependency
sudo apt update
sudo apt install build-essential python libarchive-dev

# install singularity
wget https://github.com/sylabs/singularity/archive/refs/tags/2.6.1.tar.gz
tar xzfv 2.6.1.tar.gz
cd singularity-2.6.1
./autogen.sh
./configure --prefix=/usr/local
make
sudo make install
```
## Create New Image Test
```
$ singularity image.create -s 2048 test.img
$ sudo singularity build -w test.img docker://ubuntu
```
## Execute Comand To Print System Version
```
$ singularity exec test.img cat /etc/issue
```
### Create New Sandbox
```
sudo singularity build --sandbox ubuntu/ docker://ubuntu
sudo singularity build ubuntu.simg ubuntu/
```
