# PET_implementation

<!-- *** -->

* create VM for ubuntu desktop 20.4
* After the os is runnning in the vm check the kernel version using -> 
    ```*uname -r*``` output ```5.15.0-126-generic```
* then run \
```wget https://cdn.kernel.org/pub/linux/kernel/v5.x/linux-5.15.tar.xz```
* ```tar -xf linux-5.15.tar.xz```
* ```cd linux-5.15/```
* ```sudo apt update```
* ```sudo apt install gcc-aarch64-linux-gnu binutils-aarch64-linux-gnu```
* ```sudo apt install build-essential libncurses-dev bison flex libssl```
* ```aarch64-linux-gnu-gcc --version```
* ```make ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- menuconfig```
* Navigate to Kernel hacking -> Memory Debugging and enable KASAN: runtime memory debugger
* ```make ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- -j$(nproc)```
* ```make ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- modules```
* ```make ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- dtbs```
* ```sudo make ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- modules_install```
* ```sudo make ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- install```
* ```sudo update-grub```
* ```sudo reboot```


***
#### Check Kernel Configuration
#### ```grep KASAN /boot/config-$(uname -r)```

***
#### [compile-and-install-the-linux-kernel](https://cylab.be/blog/343/compile-and-install-the-linux-kernel)
* create VM for ubuntu desktop 20.4
* After the os is runnning in the vm check the kernel version using -> 
    ```*uname -r*``` output ```5.15.0-126-generic```
* then run \
```wget https://cdn.kernel.org/pub/linux/kernel/v5.x/linux-5.15.tar.xz```
* ```tar -xf linux-5.15.tar.xz```
* ```cd linux-5.15/```
* ```make mrproper```
* ```cp /boot/config-$(uname -r) .config```
* ```make menuconfig```
* Navigate to Kernel hacking -> Memory Debugging and enable KASAN: runtime memory debugger
* ```make -j 3```
* ```sudo make modules_install```
##### Getting error
```ph@ph-Standard-PC-Q35-ICH9-2009:~/linux-5.15$ sudo make modules_install
[sudo] password for ph: 
arch/x86/Makefile:142: CONFIG_X86_X32 enabled but no binutils support
sed: can't read modules.order: No such file or directory
make: *** [Makefile:1501: __modinst_pre] Error 2```
```
* ```sudo apt install binutils-multiarch```
* ```nano .config```
    Search for CONFIG_X86_X32 and set it to n
* ```make -j 5```