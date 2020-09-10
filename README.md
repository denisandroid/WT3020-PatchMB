# WT3020-PatchMB
New patches to add support for different flash drive sizes to openwrt for wt3020.

### 1. Dump 16MB PlugAndPlay/Stable (4.14 Kernel, 19.07.3, tested!)
1. The Dump, flash with the programmer or flash the image through the ```breed``` bootloader.. 

```
Fully patched for the official version, kmod works from the repository, ready to go.
The build settings were used from the official version! Luci included!

https://github.com/denisandroid/WT3020-PatchMB/blob/master/openwrt_16mb_4.19-19.07/dump_16mb_nexx_patch_fullrelease_ulinversion.bin
```

```
Not patched git version, kmod from repository doesn't work, software works. For kmod to work, you need to install packages from the git repo.
The build settings were used from the official version! Luci included!

https://github.com/denisandroid/WT3020-PatchMB/blob/master/openwrt_16mb_4.19-19.07/dump_16mb_nexx_not_patched_gitversion.bin
```

2. Sysupgrade/Factory

```
Not patched and clean git version.
The build settings were used from the official version! Luci included!

https://github.com/denisandroid/WT3020-PatchMB/blob/master/openwrt_16mb_4.19-19.07/git_build/openwrt-19.07-snapshot-r11210-29b4104d69-ramips-mt7620-wt3020-16M-squashfs-sysupgrade.bin

https://github.com/denisandroid/WT3020-PatchMB/blob/master/openwrt_16mb_4.19-19.07/git_build/openwrt-19.07-snapshot-r11210-29b4104d69-ramips-mt7620-wt3020-16M-squashfs-factory.bin
```

### 2. Dump 8MB, breed + nexx firmware, flash with the programmer or flash the image through the ```breed``` bootloader.. 

```
https://github.com/denisandroid/WT3020-PatchMB/blob/master/openwrt_16mb_4.19-19.07/dump_8%D0%BC%D0%B1_nexx_breed.bin
```


### 3. Build patch 16MB Nightly (5.4 Kernel, tested!)
```
git clone https://github.com/openwrt/openwrt.git
git pull

patch -p1 < WT3020-Add-support-for-16M-flash-nightly5.4.patch

./scripts/feeds update -a
./scripts/feeds install -a

make defconfig 
```
<b>Choose:</b>
1. Target System (MediaTek Ralink MIPS)
2. Subtarget (MT7620 based boards)
3. Target Profile (Nexx WT3020 (16MB))

// Note, assembly without luci, if you need a graphical interface, install it in a working system as a separate package or mark the required item in the menuconfig.

```
make menuconfig
make -j3
```
