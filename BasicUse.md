## Create New Image Test
```
$ singularity image.create -s 2048 test.img
$ sudo singularity build -w test.img docker://ubuntu
```
## Execute Comand To Print System Version
```
$ singularity exec test.img cat /etc/issue
```
