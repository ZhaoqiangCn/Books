# Issue

### ModuleNotFoundError: No module named 'requests'

由于Pycharm新建项目的时候是在虚拟环境中运行解释器，所以没有安装Requests。

解决办法：在Pycharm中打开，执行pip install requests

![](../../.gitbook/assets/image%20%283%29.png)

### indexerror: list index out of range

一般列表是空的未读取到数据的情况会报此错误。

解决办法：在处理数据之前加入判断条件

```python
def get_contents(self, target):
    req = requests.get(url=target)
    html = req.text
    bf = BeautifulSoup(html,"html.parser")
    texts = bf.find_all('div', class_='showtxt')
    if(len(texts)):
        print(texts[0])
        texts = texts[0].text.replace('\xa0' * 8, '\n\n')
    else:
        dl.get_contents(target)
    return texts
```

### UnicodeEncodeError: 'ascii' codec can't encode characters

系统编码 报错的字符是一个Unicode字符，查了下发现是python3，只有str和Unicode两种编码，去查了python3的系统编码：

```python
>>> import sys
>>> sys.getdefaultencoding()
'utf-8'
```

输入输出编码 既然不是系统编码，而且前面输出都没有问题，所以可能也不是之前读写文件的编码错误，可能是print的时候，也就是标准输入输出的时候编码问题了；那么print的时候做了什么，用的是什么编码呢？ 我们已经知道在python3中，输出的时候，会把str/Unicode 变成utf8的编码；来看一下环境中的输出编码是什么：

```python
>>> import sys 
>>> sys.stdout.encoding
'ANSI_X3.4-1968'
```

解决方法 这样看来应该就是输入输出print的锅了，那么如何解决呢？ 也就是如何修改标准输出编码方式呢？ 有如下解决方法：

* PYTHONIOENCODING 运行程序的时候加上： 

```python
PYTHONIOENCODING=utf-8 python code.py
```

* 重新定义输出标准 

```python
import codecs
sys.stdout = codecs.getwriter("utf-8")(sys.stdout.detach())
sys.stdout.write("Your content....")
```

### Screen命令中文乱码

 其实只要在使用 screen 的时候加一个 **-U** 参数就应该就没问题了

```text
#创建utf8编码模式的新会话
screen -U -S new_screen_test

#查看当前会话
screen -ls

#切换会话(utf8编码查看)
screen -U -r new_screen_test
```

