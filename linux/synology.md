# Synology

### Best Trace

```text
wget http://cdn.ipip.net/17mon/besttrace4linux.zip
unzip besttrace4linux.zip #7z
chmod +x besttrace32
#如何使用
./besttrace32 -q 1 目标IP
```

### Speed Test

```text
wget https://raw.githubusercontent.com/sivel/speedtest-cli/master/speedtest.py
chmod +x speedtest.py
./speedtest.py
```

### VMM - LEDE

```text
vi /etc/config/network 编辑配置文件，修改LEDE管理地址
/etc/init.d/network restart 重启网络
# 进去管理界面，删除WAN，WAN6
# 关闭Lan的DHCP
# 设定DSN等信息
```

![](../.gitbook/assets/image%20%281%29.png)

