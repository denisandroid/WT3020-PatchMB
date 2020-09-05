# WT3020-PatchMB
New patches to add support for different flash drive sizes to openwrt for wt3020.


### 16MB Nightly (5.4 Kernel, tested!)
```
git clone https://github.com/openwrt/openwrt.git
git pull

patch -p1 < WT3020-Add-support-for-16M-flash-nightly5.4.patch

./scripts/feeds update -a
./scripts/feeds install -a

make defconfig 
make menuconfig
make
```
