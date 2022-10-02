Rebuild kernel (master doc: https://www.raspberrypi.com/documentation/computers/linux_kernel.html#cross-compiling-the-kernel):
```
sudo apt install git bc bison flex libssl-dev make
KERNEL=kernel7l
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- bcm2711_defconfig
make -j12 ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- zImage modules dtbs
```

Copy compiled kernel to sdcard:
```
mkdir -p mnt/root
mkdir -p mnt/boot/overlays
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- INSTALL_MOD_PATH=mnt/root modules_install
cp arch/arm64/boot/Image mnt/boot/$KERNEL.img
cp arch/arm/boot/zImage mnt/boot/$KERNEL.img
cp arch/arm/boot/dts/*.dtb mnt/boot/
cp arch/arm/boot/dts/overlays/*.dtb* mnt/fat32/overlays/
cp arch/arm/boot/dts/overlays/*.dtb* mnt/boot/overlays/
cp arch/arm/boot/dts/overlays/README mnt/boot/overlays/
```
