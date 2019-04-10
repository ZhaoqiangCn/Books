---
description: Ubuntu & Debian
---

# 第四章 - Linux

### 常用指令

#### Screen

* screen -S name 启动一个名字为name的screen
* screen -ls 是列出所有的screen
* screen -r name或者id，就可以回到某个screen了
* screen -S name -X quit 删除screen
* ctrl + a + d 可以回到前一个screen，当时在当前screen运行的程序不会停止

#### Rclone

{% code-tabs %}
{% code-tabs-item title="Google" %}
```text
nohup rclone -v mount myspacesh:CopyFromShare /root/myspacesh --allow-other --dir-cache-time 2h --buffer-size 32M --poll-interval 5m --tpslimit 2 &
nohup rclone -v mount myspaceshto:CopyFromShare /root/myspaceshto --allow-other --dir-cache-time 2h --buffer-size 32M --poll-interval 5m --tpslimit 2 &
fusermount -u /root/myspaceshto
rclone copy -v myspacesh:CopyFromShare/'TPimage MegaPack' myspaceshto:CopyFromShare/inbox/'TPimage MegaPack'
rclone copy -v drivefrom:CopyFromShare/M1-50 driveto:CopyFromShare/M1-250
```
{% endcode-tabs-item %}
{% endcode-tabs %}

#### Shell脚本

{% code-tabs %}
{% code-tabs-item title="Shell" %}
```text
#!/bin/bash
echo "Hello world!"

chmod +x hello.sh
```
{% endcode-tabs-item %}
{% endcode-tabs %}





