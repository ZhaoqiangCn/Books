---
description: 在Ubuntu 14.04使用cron实现作业自动化
---

# Cron

### 启动Cron服务 <a id="&#x4E00;&#x542F;&#x52A8;cron&#x670D;&#x52A1;"></a>

基本上所有的Linux发行版在默认情况下都预安装了cron工具。即使未预装cron，也很简单，执行命令手动安装它：

```text
apt-get install cron
```

接着检查cron服务的状态，默认情况它应该运行于后台。如果它未启动，那么可以手动启动此服务。

```text
service cron start
service cron status
```

### Crontab命令 <a id="&#x4E09;crontab&#x547D;&#x4EE4;&#x7684;&#x7528;&#x6CD5;"></a>

#### 对Cron作业进行列表 <a id="1&#x5BF9;cron&#x4F5C;&#x4E1A;&#x8FDB;&#x884C;&#x5217;&#x8868;"></a>

使用以下命令列出当前用户计划的cron作业。

```text
crontab –l
```

会列出当前用户的所有cron作业，如果想查看其它用户的cron作业，可以使用如下命令：

```text
crontab –l –u username
```

#### 编辑Cron作业 <a id="2&#x7F16;&#x8F91;cron&#x4F5C;&#x4E1A;"></a>

要添加一个新cron作业，或者是编辑现有的cron作业

```text
crontab -e
```

#### 移除Cron作业 <a id="3&#x79FB;&#x9664;cron&#x4F5C;&#x4E1A;"></a>

使用下面的命令移除已经计划的cron作业

```text
crontab –r
```

使用下面的命令移除所有已计划的cron作业，且无需再次确认

```text
crontab –ir
```

### 用Crontab计划任务 <a id="&#x56DB;&#x7528;crontab&#x8BA1;&#x5212;&#x4EFB;&#x52A1;"></a>

#### Cron配置类型 <a id="1cron&#x914D;&#x7F6E;&#x7C7B;&#x578B;"></a>

1. 系统级Crontab
2. 用户级Crontab

#### 系统级crontab

这些cron作业被系统服务和关键作业所使用，且需要root级的权限才能执行。可以在/etc/crontab文件中查看系统级的cron作业

![](../.gitbook/assets/image%20%282%29.png)

#### 用户级crontab

用户级的cron作业是针对每个用户单独分开的。因此每个用户都可以使用crontab命令创建自己的cron作业，还可以使用以下命令编辑或查看自己的cron作业:

```text
crontab –e
```



