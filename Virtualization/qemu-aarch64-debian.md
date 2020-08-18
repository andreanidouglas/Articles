---
title: ARM 64bit Debian on your x86 PC
published: true
description: Running a VM environment for arm 64bit OS like Debian
tags: qemu, arm, debian, linux
---

#ARM machines and QEMU

ARM processors runs on most all mobile phones with Android or iOS even obscure OSes like PinePhone.
The advantage of such architecture is the SOC (System on a chip) availables are very power-efficient and can run on a couple of watts, with an impressive Watts to Perfomance ration [Arm Takes Wing](https://blog.cloudflare.com/arm-takes-wing/).


Fugaku supercomputer node image
Even supercomputers are using ARM. (Supercomputer Fugaku by Fujitsu)[https://www.top500.org/system/179807/]

The only problem with such technology, is the availabity of commodity hardware to run a development workstation on. This is where emulation comes in, through the amazing project over [QEMU] (https://www.qemu.org/). 

With QEMU, is possible to emulate several computer architectures, including arm 64bit, called aarch64, within various capacities and architectures. This may not be the fastest way, but is definatelly cheap, since you can run it on any x86/amd64 pc with some memory and cores to spare to the emulated machine.

#Configuring the machine

QEMU is a terminal based solution and altough there is GUI options, like virt-manager, is not optimal for different architectures other than x86.

The main command to run arm 64 bit emulation is: `qemu-system-aarch64`. This command needs several options that needs to be configured.

##Memory

The options `-m` sets in MegaBytes, how much memory the host (your pc) will allocate to the emulator. Give it a amount compatible that would not let the host without memory for its operations (eg on a 8GB host give it 2048, for 16GB host 8192).

##CPU
The cpu options will specify which kind of cpu architecture to run. Several options are available in the command `qemu-system-aarch64 -cpu help` but for now lets choose cortex-a57 or cortex-a72 the smp option needs to be configured according to the host specs. In this case, 2 cores with 2 threads each.

```
-cpu cortex-a72 -M virt -smp cores=2,threads=4
```

##Disk and bootloader
ARM machines unless common x86 computers do not have a bios to load all the configuration and store the bootloader. Instead we need a bootloader compatible, one of the options is the TianoCore project EDK2 compiled for arm. On most debian based distros you can find it on `/usr/share/qemu-efi-aarch/QEMU_EFI.fd` after installing package `qemu-efi-aarch64`.

For system disk, we can use a create a disk with the following command `qemu-img create -f raw debian-arm.img 64G`
Also we need a debian boot disk to install the operating system. Visit https://get.debian.org and download the newest arm64 image.

We can add that to our qemu emulator with the options

```
-bios /usr/share/qemu-efi-aarch64/QEMU_EFI.fd \
-drive if=none,file=debian-arm.img,id=hd0 -device virtio-blk-device,drive=hd0 \
-drive if=virtio,file=debian-10.5.0-arm64-netinst.iso,format=raw
```

##Networking

In order to have access to network and grab packages to enhance the debian experience we need a device for network communication. A very compatible network device is the Intel e1000.

```
-device e1000,netdev=net0 -netdev user,id=net0
```

##Display and peripherals
Finally, we need a display to interact with the OS and appropriate video and peripheral devices.

```
-device virtio-gpu-pci \
-device qemu-xhci \
-device usb-kbd
-display none
-serial stdio
```

##Installing debian 

Full command

```
qemu-system-aarch64 -m 8192 -cpu cortex-a72 -M virt -smp cores=2,threads=2 \
	-bios /usr/share/qemu-efi-aarch/QEMU_EFI.fd
       	-drive if=none,file=debian-arm.img,format=raw,id=hd0 -device virtio-blk-device,drive=hd0 \
       	-drive if=virtio,file=debian-10.5.0-arm64-netinst.iso,format=raw \
       	-device e1000,netdev=net0 -netdev user,id=net0 \
	-device nec-usb-xhci,id=xhci  \
	-device usb-tablet,bus=xhci.0 \
        -device virtio-gpu-pci -device usb-kbd -display none -serial stdio

```

Now, we can boot and install debian in our virtual emulated machine. Use the terminal (that is receiving serial data) to complete the install.

PS: To locate the installation media:
* Load CD-ROM drivers from removable media?: Select No
* Manually select a CD-ROM module and device?: Select Yes
* Module needed for accessing the CD-ROM: Select none
* Device file for accessing the CD-ROM: Enter /dev/vdb and press continue

## Running system for use

After the installation is completed, use the following command to use the system.

```
qemu-system-aarch64 -m 8192 -cpu cortex-a72 -M virt -smp cores=4,threads=2\
	-bios /usr/share/qemu-efi-aarch/QEMU_EFI.fd
       	-drive if=none,file=debian-arm.img,format=raw,id=hd0 -device virtio-blk-device,drive=hd0 \
       	-drive if=virtio,file=debian-10.5.0-arm64-netinst.iso,format=raw \
       	-device e1000,netdev=net0 -netdev user,id=net0 \
	-device nec-usb-xhci,id=xhci  \
	-device usb-tablet,bus=xhci.0 \
	-device usb-kbd \
	-device virtio-gpu-pci -display gtk,show-cursor=on
```

