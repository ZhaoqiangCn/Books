# IPKG

#### **确定当前的处理器类型：**

```text
cat /proc/cpuinfo | grep cpu
uname –machine 
```

#### **根据CPU类型去下载对应的CPU Bootstrap Script安装包：**

```text
ARM (armv5tejl)：
http://ipkg.nslu2-linux.org/feeds/optware/syno-x07/cross/unstable/syno-x07-bootstrap_1.2-7_arm.xsh
 
PowerPC (ppc_6xx)：
http://ipkg.nslu2-linux.org/feeds/optware/ds101g/cross/unstable/ds101-bootstrap_1.0-4_powerpc.xsh
 
PowerPC (ppc_85xx, e500v?)：
http://ipkg.nslu2-linux.org/feeds/optware/syno-e500/cross/unstable/syno-e500-bootstrap_1.2-7_powerpc.xsh
 
Marvell Kirkwood 88F6281, 88F6282, 88FR131 (ARMv5TE Feroceon)：
http://ipkg.nslu2-linux.org/feeds/optware/cs08q1armel/cross/stable/syno-mvkw-bootstrap_1.2-7_arm.xsh
 
Intel Atom：
http://ipkg.nslu2-linux.org/feeds/optware/syno-i686/cross/unstable/syno-i686-bootstrap_1.2-7_i686.xsh
 
```

```text
Synology ds216+ii：
wget http://ipkg.nslu2-linux.org/feeds/optware/syno-i686/cross/unstable/syno-i686-bootstrap_1.2-7_i686.xsh
将脚本可执行化：
chmod +x syno-i686-bootstrap_1.2-7_i686.xsh 
执行脚本：
sh syno-i686-bootstrap_1.2-7_i686.xsh 
删除脚本：
rm syno-i686-bootstrap_1.2-7_i686.xsh 
更新一下软件源：
/opt/bin/ipkg update
ipkg版本：ipkg -v

链接:
http://ipkg.nslu2-linux.org/feeds/optware/syno-i686/cross/unstable/
```

#### **变量加入系统path：**

vi /root/.profile在path这行结尾分号之前，加入：/opt/sbin:/opt/bin最后保存即可，生效只需录入su切换下用户或者重启就行。 

