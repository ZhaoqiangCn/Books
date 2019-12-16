---
description: Ubuntu&Debian 常用命令
---

# Command

### 常用指令

{% embed url="https://blog.csdn.net/ljianhui/article/details/11100625" %}

#### ls

* -l ：列出长数据串，包含文件的属性与权限数据等 
* -a ：列出全部的文件，连同隐藏文件（开头为.的文件）一起列出来（常用） 
* -d ：仅列出目录本身，而不是列出目录的文件数据 
* -h ：将文件容量以较易读的方式（GB，kB等）列出来 
* -R ：连同子目录的内容一起列出（递归列出），等于该目录下的所有文件都会显示出来  

{% code title="这些参数也可以组合使用，下面举两个例子：" %}
```text
ls -l #以长数据串的形式列出当前目录下的数据文件和目录 
ls -lR #以长数据串的形式列出当前目录下的所有文件
```
{% endcode %}

#### grep

#### find

#### cp

#### mv

#### rm

#### ps

#### kill

#### tar

#### chmod

#### Screen

* screen -S name 启动一个名字为name的screen
* screen -ls 是列出所有的screen
* screen -r name或者id，就可以回到某个screen了
* screen -S name -X quit 删除screen
* ctrl + a + d 可以回到前一个screen，当时在当前screen运行的程序不会停止

#### Rclone

{% code title="Google" %}
```text
nohup rclone -v mount myspacesh:CopyFromShare /root/myspacesh --allow-other --dir-cache-time 2h --buffer-size 32M --poll-interval 5m --tpslimit 2 &
nohup rclone -v mount myspaceshto:CopyFromShare /root/myspaceshto --allow-other --dir-cache-time 2h --buffer-size 32M --poll-interval 5m --tpslimit 2 &
fusermount -u /root/myspaceshto
rclone copy -v myspacesh:CopyFromShare/'TPimage MegaPack' myspaceshto:CopyFromShare/inbox/'TPimage MegaPack'
rclone copy -v drivefrom:CopyFromShare/M1-50 driveto:CopyFromShare/M1-250
```
{% endcode %}

#### Shell脚本

{% code title="Shell" %}
```text
#!/bin/bash
echo "Hello world!"

chmod +x hello.sh
```
{% endcode %}



