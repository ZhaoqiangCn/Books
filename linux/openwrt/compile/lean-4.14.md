---
description: L大源码&SSRPlus ，移植后固件版本为4.14
---

# Lean-4.14

### 安装依赖

```bash
sudo apt-get update
sudo apt-get -y install build-essential asciidoc binutils bzip2 gawk gettext git libncurses5-dev libz-dev patch unzip zlib1g-dev lib32gcc1 libc6-dev-i386 subversion flex uglifyjs git-core gcc-multilib p7zip p7zip-full msmtp libssl-dev texinfo libglib2.0-dev xmlto qemu-utils upx autoconf automake libtool autopoint
```

### 克隆openwrt及lean的包到本地

```text
git clone https://github.com/openwrt/openwrt
git clone https://github.com/ZhaoqiangCn/lede
```

**这样，我们本地即有lede 和openwrt两个文件夹。lede文件夹是lean的源码，openwrt文件夹是官方的源码。**

### **正式进入移植步骤**

拷贝lede/packgage/lean文件夹到openwrt/package 里面

### 自定义要安装的包

```bash
vi openwrt/include/target.mk

DEFAULT_PACKAGES:=base-files libc libgcc busybox dropbear mtd uci opkg netifd fstools uclient-fetch logd block-mount coremark \
kmod-nf-nathelper kmod-nf-nathelper-extra kmod-ipt-raw wget libustream-openssl ca-certificates \
default-settings luci luci-app-ddns luci-app-sqm luci-app-upnp luci-app-adbyby-plus luci-app-autoreboot \
luci-app-filetransfer luci-app-ssr-plus luci-app-vsftpd ddns-scripts_aliyun \
luci-app-pptp-server luci-app-arpbind luci-app-vlmcsd luci-app-wifischedule luci-app-wol luci-app-ramfree \
luci-app-sfe luci-app-flowoffload luci-app-nlbwmon luci-app-usb-printer luci-app-accesscontrol luci-app-zerotier luci-app-xlnetacc
```

```bash
DEFAULT_PACKAGES.router:=dnsmasq-full iptables ip6tables ppp ppp-mod-pppoe firewall odhcpd-ipv6only odhcp6c kmod-ipt-offload
```

### 修改目标路由器固件的包

```bash
vi openwrt/target/linux/x86/Makefile

DEFAULT_PACKAGES += partx-utils mkf2fs fdisk e2fsprogs wpad kmod-usb-hid \
kmod-ath5k kmod-ath9k kmod-ath9k-htc kmod-ath10k kmod-rt2800-usb kmod-e1000e kmod-igb kmod-igbvf kmod-ixgbe kmod-pcnet32 kmod-tulip kmod-vmxnet3 kmod-i40e kmod-i40evf \
htop lm-sensors autocore automount autosamba luci-app-zerotier luci-app-ipsec-vpnd luci-app-pptp-server luci-proto-bonding luci-app-zerotier \
ath10k-firmware-qca988x ath10k-firmware-qca9888 ath10k-firmware-qca9984 brcmfmac-firmware-43602a1-pcie intel-microcode amd64-microcode\
alsa-utils kmod-ac97 kmod-sound-hda-core kmod-sound-hda-codec-realtek kmod-sound-hda-codec-via kmod-sound-via82xx kmod-usb-audio \
kmod-usb-net kmod-usb-net-asix kmod-usb-net-asix-ax88179 kmod-usb-net-rtl8150 kmod-usb-net-rtl8152 \
shadowsocks-libev-ss-redir v2ray shadowsocksr-libev-server shadowsocksr-libev-ssr-local
```

### 应用fullconenat 

以下拷贝到openwrt下面的同目录里，覆盖openwrt官方的。

拷贝 lede/package/network/config/firewall/makefile

拷贝 lede/package/network/config/firewall/patches

### 修改“活动连接数” \(可选\)

```bash
vi openwrt/package/kernel/linux/files/sysctl-nf-conntrack.conf

net.netfilter.nf_conntrack_max=16384 修改为 65536
```

### 修改主机名和ssr-plus彩蛋

```bash
vi openwrt/package/lean/default-settings/files/zzz-default-settings

uci set system.@system[0].timezone=CST-8
uci set system.@system[0].hostname=Openwrt-x86 新增
uci set system.@system[0].zonename=Asia/Shanghai
...

echo 0xDEADBEEF > /etc/config/google_fu_mode 解封ssr彩蛋
exit 0
```

在该文件exit 0 上方适当的位置加上加入下列命令，设置Wan网口，添加pppoe拨号账户密码，装好即可上网

```text
uci set network.wan.proto='pppoe'
uci set network.wan.username='宽带账号'
uci set network.wan.password='宽带密码'
uci set network.wan.ifname='eth3'   //我的wan接口是eth3，你要根据自己的路由器情况改
uci set network.wan6.ifname='eth3'
uci commit network
```

修改管理ip地址和lan口配置，可以在该文件exit 0 上方适当的位置加上加上下列命令

```text
uci set network.lan.ipaddr='192.168.0.8'    //改成你想要默认的管理ip
uci set network.lan.proto='static'          //wan口静态IP方式
uci set network.lan.type='bridge'           //设置桥接
uci set network.lan.ifname='eth0 eth1 eth2 eth4 eth5' //根据自己的路由器情况改Lan口 
uci commit network
```

### ssr-plus 处理

luci-app-ssr-plus/luasrc/model/cbi/shadowsocksr/server.lua

删除 local ipkg = require\("luci.model.ipkg"\)'

luci-app-ssr-plus/luasrc/model/cbi/shadowsocksr/client-config.lua

删除 local ipkg = require\("luci.model.ipkg"\)'

### 安装feeds

```text
./scripts/feeds update -a && ./scripts/feeds install -a
```

### 进行编译

注意dsnmasq 和 dnsmasq-full 只能选一个

```bash
make menuconfig
```

### 进行编译，输入下列命令

```text
make -j4 V=s
```

