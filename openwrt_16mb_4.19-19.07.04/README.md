# Openwrt_16mb_4.19-19.07.04 (tested!)


### 1. The Dump, flash with the programmer or flash the image through the ```breed``` bootloader.. 

```
The build settings were used from the official version! Luci included!

https://github.com/denisandroid/WT3020-PatchMB/blob/master/openwrt_16mb_4.19-19.07.04/dump_16mb_nexx_fullrelease_ulinversion.bin
```

### 2. Sysupgrade/Factory

```
The build settings were used from the official version! Luci included!
No patch required to mask the version!!!

https://github.com/denisandroid/WT3020-PatchMB/blob/master/openwrt_16mb_4.19-19.07.04/openwrt-19.07.4-ramips-mt7620-wt3020-16M-squashfs-sysupgrade.bin

https://github.com/denisandroid/WT3020-PatchMB/blob/master/openwrt_16mb_4.19-19.07.04/openwrt-19.07.4-ramips-mt7620-wt3020-16M-squashfs-sysupgrade.bin
```



### 3. Make 16MB Stable release (4.14 Kernel, 19.07.4, tested!)

```
git clone https://github.com/openwrt/openwrt --branch openwrt-19.07
git checkout d5810aa61367a9424599935572f622d27f8303f0
cd ./openwrt/

patch -p1 < 0001-1.-Patch-version.patch
patch -p1 < 0002-2.WT3020-Add-support-for-16M-flash-stable4.19-19.07.patch

wget https://downloads.openwrt.org/releases/19.07.4/targets/ramips/mt7620/config.buildinfo -O .config

./scripts/feeds update -a
./scripts/feeds install -a

```

<b>Choose:</b>
1. Target System (MediaTek Ralink MIPS)
2. Subtarget (MT7620 based boards)
3. Target Profile (Nexx WT3020 (16MB))

```
make menuconfig
make -j3
```

1. Wait, collected img you will find on the path ```bin/targets/ramips/mt7620/```
2. Stitch clean spi 16mb (recommended winbond w25q128fv) 8mb ready dump (described above) or dump fused with your working 8mb memory flash.
3. Using the "breed" loader, we install sysupgrade or using any other running openwrt we update sysupgrade.
4. No patch required to mask the version!!! Just use!

