---
description: 单网口群晖VMM安装K-LEDE实现旁路模式
---

# LEDE - Install

### 基本设置

```text
vi /etc/config/network 编辑配置文件，修改LEDE管理地址
/etc/init.d/network restart 重启网络
# 进去管理界面，删除WAN，WAN6
# 关闭Lan的DHCP
# 设定DSN等信息
```

![](../../.gitbook/assets/image%20%281%29.png)

