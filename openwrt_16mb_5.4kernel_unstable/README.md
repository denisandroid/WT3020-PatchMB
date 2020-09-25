# Openwrt_16mb_5.4 (Tested!)



### <b>1. Build 16MB Nightly (5.4 Kernel)</b>
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
