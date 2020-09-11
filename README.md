# WT3020-PatchMB
New fixes to add support for different flash drive sizes to openwrt for wt3020. (1,2,3,4 are separate items).

### <b>1. Dump 16MB PlugAndPlay/Stable (4.14 Kernel, 19.07.3, tested!)</b>

<div>
<img src="https://github.com/denisandroid/WT3020-PatchMB/blob/master/openwrt_16mb_4.19-19.07/Screenshot_OpenWrt_Luci1.png" width="400" height="250"/>
<img src="https://github.com/denisandroid/WT3020-PatchMB/blob/master/openwrt_16mb_4.19-19.07/Screenshot_OpenWrt_Luci2.png" width="400" height="250"/>
</div>

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

### <b>2. Dump 8MB, breed + nexx firmware, flash with the programmer or flash the image through the ```breed``` bootloader.. </b>

```
https://github.com/denisandroid/WT3020-PatchMB/blob/master/openwrt_8mb_4.19-19.07/dump_8mb_nexx_breed.bin
```

### <b>3. Patching the git version to the official version (19.07.3, tested!)</b>

```
cd /tmp
wget http://downloads.openwrt.org/releases/19.07.3/targets/ramips/mt7620/packages/kernel_4.14.180-1-18384755d38fc43c447d83d4a3e07054_mipsel_24kc.ipk
opkg install "/tmp/kernel_4.14.180-1-18384755d38fc43c447d83d4a3e07054_mipsel_24kc.ipk" --force-downgrade --force-reinstall

opkg update
opkg install nano
```


```
nano /etc/opkg/distfeeds.conf

/// add to the end
src/gz openwrt_kmods http://downloads.openwrt.org/releases/19.07.3/targets/ramips/mt7620/kmods/4.14.180-1-18384755d38fc43c447d83d4a3e07054
```

```
opkg update
```


```
nano /usr/lib/opkg/status

/// full_replace version 4.14.195 -> 4.14.180
/// 4.14.195 git version
/// 4.14.180 official version

/// (test)
/// 4.19.137-1-2 -> 4.19.120-1-1
/// 204.2-r11210-29b4104d69 -> 204.2-r11063-85e04e9f46
```

```
/// Required for linking official linux kmod and our git linux kmod.

/// 4.14.195 git version
/// 4.14.180 official version

mv /lib/modules/4.14.180/* /lib/modules/4.14.195/
rm -R /lib/modules/4.14.180/
ln -s /lib/modules/4.14.195/ /lib/modules/4.14.180
```

```
nano /usr/lib/os-release

///Replace completely with this
NAME="OpenWrt"
VERSION="19.07.3"
ID="openwrt"
ID_LIKE="lede openwrt"
PRETTY_NAME="OpenWrt 19.07.3"
VERSION_ID="19.07.3"
HOME_URL="https://openwrt.org/"
BUG_URL="https://bugs.openwrt.org/"
SUPPORT_URL="https://forum.openwrt.org/"
BUILD_ID="r11063-85e04e9f46"
OPENWRT_BOARD="ramips/mt7620"
OPENWRT_ARCH="mipsel_24kc"
OPENWRT_TAINTS=""
OPENWRT_DEVICE_MANUFACTURER="OpenWrt"
OPENWRT_DEVICE_MANUFACTURER_URL="https://openwrt.org/"
OPENWRT_DEVICE_PRODUCT="Generic"
OPENWRT_DEVICE_REVISION="v0"
OPENWRT_RELEASE="OpenWrt 19.07.3 r11063-85e04e9f46"
```

```
nano /etc/openwrt_version

r11063-85e04e9f46
```

```
nano /etc/openwrt_release

DISTRIB_ID='OpenWrt'
DISTRIB_RELEASE='19.07-Generic'
DISTRIB_REVISION='r11063-85e04e9f46'
DISTRIB_TARGET='ramips/mt7620'
DISTRIB_ARCH='mipsel_24kc'
DISTRIB_DESCRIPTION='OpenWrt 19.07-Generic r11063-85e04e9f46'
DISTRIB_TAINTS=''
```

```
nano /etc/banner

  _______                     ________        __
 |       |.-----.-----.-----.|  |  |  |.----.|  |_
 |   -   ||  _  |  -__|     ||  |  |  ||   _||   _|
 |_______||   __|_____|__|__||________||__|  |____|
          |__| W I R E L E S S   F R E E D O M
 -----------------------------------------------------
 OpenWrt 19.07-Generic, r11063-85e04e9f46
 -----------------------------------------------------
```

As a result, you will get a working git version that does not swear at conflicts and perfectly works from the official kmod modules from the repository.

### <b>4. Build patch 16MB Stable release (4.14 Kernel, 19.07.3, tested!)</b>

```
git clone https://github.com/openwrt/openwrt.git --branch openwrt-19.07 --single-branch r11063-85e04e9f46
cd ./r11063-85e04e9f46/

patch -p1 < WT3020-Add-support-for-16M-flash-stable4.19-19.07.patch

wget https://downloads.openwrt.org/releases/19.07.4/targets/ramips/mt7620/config.buildinfo -O .config

./scripts/feeds update -a
./scripts/feeds install -a

make defconfig
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
2. Stitch clean spi 16mb (recommended winbond w25q64fv) 8mb ready dump (described above) or dump fused with your working 8mb memory flash.
3. Using the "breed" loader, we install sysupgrade or using any other running openwrt we update sysupgrade.
4. Next, we make patches to convert the git version to the official version (described above) in an already working modem (I warn you, the first launch of the modem will take a long time, since the user 8mb spi is converted to 16mb spi)


### <b>5. Build patch 16MB Nightly (5.4 Kernel, tested!)</b>
It is not recommended, since after the build you will not be able to install any of the possible packages due to unresolved dependencies.

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
