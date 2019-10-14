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

![](../../.gitbook/assets/image%20%2813%29.png)

#### 用户级crontab

用户级的cron作业是针对每个用户单独分开的。因此每个用户都可以使用crontab命令创建自己的cron作业，还可以使用以下命令编辑或查看自己的cron作业:

```text
crontab –e
```

### 用Crontab调度作业 

可以使用指定的语法调度cron作业，而且还有速记缩写命令，使的管理cron作业很简单。 Crontab语法如下：

```text
* * * * * command to be executed
- - - - - -
| | | | | |
| | | | | --- 预执行的命令
| | | | ----- 表示星期0～7（其中星期天可以用0或7表示）
| | | ------- 表示月份1～12
| | --------- 表示日期1～31
| ----------- 表示小时1～23（0表示0点）
------------- 表示分钟1～59 每分钟用*或者 */1表示
每五分钟执行    */5 * * * *
每小时执行    0 * * * *
每天执行    0 0 * * *
每周执行    0 0 * * 0
每月执行    0 0 1 * *
每年执行    0 0 1 1 *
```

### Cron作业配置实例 <a id="&#x516D;&#x65B0;cron&#x4F5C;&#x4E1A;&#x914D;&#x7F6E;&#x5B9E;&#x4F8B;"></a>

下面的例子，创建一个cron作业，它每分钟输出文本“test cron job to execute every minute”并把文本发送到user@vexxhost.com邮箱。 首先用crontab命令编辑

```text
SHELL=/bin/bash
HOME=/
MAILTO=”user@vexxhost.com”
#This is a comment
* * * * * echo 'test cron job to execute every minute'
```





