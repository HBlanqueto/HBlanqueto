Linux being an open source project, has the opportunity to build it to improve performance and resource consumption when compiling it, so this is my little guide that I use every time I compile the different versions of the kernel as [Vanilla](https://github.com/torvalds/linux), [Xanmod](https://github.com/xanmod/linux/tree/5.10.59-rt51-xanmod1), [Zen](https://github.com/zen-kernel/zen-kernel), [Hardenend](https://github.com/Whonix/hardened-kernel), among others.

The purpose of this is that in the end you will get a .deb package of your kernel built for an easier installation and uninstallation from your system.

## Dependencies ℹ️

These are necessary dependencies you need to build the kernel. In case you are missing any dependencies, I recommend looking for them in [Debian --Packages](https://www.debian.org/distrib/packages).

```
sudo apt install dwarves rsync meson build-essential bc kmod cpio flex libncurses5-dev libelf-dev libssl-dev bison flex-doc ncurses-doc make git ca-certificates 
```

Clang & LLVM dependencies
```
sudo apt install clang clang-tools lld llvm
```

## Modprobed-db ⚠️

[modprobed-db](https://github.com/graysky2/modprobed-db) It is a tool that allows you to load the **modules that you are using at the moment**.

```
git clone https://github.com/graysky2/modprobed-db
cd modprobed-db
make 
sudo make install
modprobed-db
modprobed-db store
```

## Download It 💻

Before start, It's necessary you have the source code of you favorite kernel which could be [Vanilla](https://github.com/torvalds/linux), [Xanmod](https://github.com/xanmod/linux/tree/5.10.59-rt51-xanmod1), [Zen](https://github.com/zen-kernel/zen-kernel), [Hardenend](https://github.com/Whonix/hardened-kernel) or another. 

```
git clone <URL of your kernel> --depth 1
```
## Prepare all 🦾

**Go to kernel folder**

```
cd ~/path/to/folder/
```

Prepare folder and files
```
make clean && make mrproper
```

Create .config file with modprobed-db
```
make LSMOD=$HOME/.config/modprobed.db localmodconfig
```

If you want to edit something manual, then execute:
```
make menuconfig
```

## Building 📦

Build Kernel with GCC
```
nice make -j`nproc` bindeb-pkg
```

Build Kernel with Clang
```
nice make CC=clang CXX=clang++ LD=ld.lld HOSTLD=ld.lld HOSTCC=clang HOSTCXX=clang++ LLVM=1 LLVM_IAS=1 -j`nproc` bindeb-pkg
```

## Install It 🧑‍💻

Install one by one package generated.
```
sudo dpkg -i <package name>.deb
```

Install all packages generated. 

```
sudo apt install ~/path/to/files/*.deb
```

**Example:** `sudo apt install ~/*.deb`

In this way you will have finished building your kernel, now you can restart and if you use grub and go "advanced options" you will see that it is right there to boot.

## Extra 💎

If you use [dkms](https://es.wikipedia.org/wiki/Dynamic_Kernel_Module_Support) and compiled the kernel with clang, You have to add `CC=clang LD=ld.lld` to the **dkms.conf** (depending the module cd **/usr/src/module_name/dkms.conf**)

```
$ cd /usr/src/*module_name

$ cat dkms.conf
PACKAGE_NAME="broadcom-sta"
PACKAGE_VERSION="6.30.223.271"
MAKE[0]="make CC=clang LD=ld.lld KVER=$kernelver"
BUILT_MODULE_NAME[0]="wl"
DEST_MODULE_LOCATION[0]="/updates/dkms"
AUTOINSTALL="YES"
REMAKE_INITRD="YES"

```

## Sources 📃
- https://wiki.debian.org/BuildADebianKernelPackage
- https://wiki.archlinux.org/title/Modprobed-db
- https://www.reddit.com/r/Fedora/comments/hp9bns/zen_and_xanmod_kernels_on_fedora_32_howto/
- https://github.com/dell/dkms/issues/124
- https://apt.llvm.org/

