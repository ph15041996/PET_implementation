# PET_implementation

***

* create VM for ubuntu desktop 2*04
* After the os is runnning in the vm check the kernel version using -> 
    ```*uname -r*``` output ```5.15.0-126-generic```
* then run \
```wget https://cdn.kernel.org/pub/linux/kernel/v5.x/linux-5.15.tar.xz```
* ```tar -xf linux-5.15.tar.xz```
* ```sudo apt update```
* ```sudo apt install gcc-aarch64-linux-gnu binutils-aarch64-linux-gnu```
* ```sudo apt install build-essential libncurses-dev bison flex libssl```
* ```aarch64-linux-gnu-gcc --version```
* ```make ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- menuconfig```
* ```make ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- -j$(nproc)```
* ```make ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- modules```
* ```make ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- dtbs```
* ```sudo make ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- modules_install```
* ```sudo make ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- install```
* ```sudo update-grub```
* ```sudo reboot```