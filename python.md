# 第一章 - Python



## 1.笔记

### 爬虫心得

* 通过Requests.get\(\)获取网页的HTML信息
* 通过beautifulsoup4解析HTML信息，find\_all匹配的返回的结果是一个列表。提取匹配结果后，使用text属性，提取文本内容，滤除br标签。随后使用replace方法，剔除空格，替换为回车进行分段。&nbsp;在html中是用来表示空格的。replace\('\xa0'\*8,'\n\n'\)就是去掉下图的八个空格符号，并用回车代替
* 一般静态页面的正文部分的标签是“showtxt”

### 语法基础

#### \_\_init\_\_

注意到\_\_init\_\_方法的第一个参数永远是self，表示创建的实例本身，因此，在\_\_init\_\_方法内部，就可以把各种属性绑定到self，因为self就指向创建的实例本身。有了\_\_init\_\_方法，在创建实例的时候，就不能传入空的参数了，必须传入与\_\_init\_\_方法匹配的参数，但self不需要传，Python解释器自己会把实例变量传进去

#### \_\_XXX

在Python中，实例的变量名如果以\_\_开头，就变成了一个**私有变量**（private），只有内部可以访问，外部不能访问

私有变量可以通过以下方式被外部变量访问和修改：

```python
class Student(object):
    ...

    def get_name(self):
        return self.__name
        
    def get_score(self):
        return self.__score
        
    def set_score(self, score):
        self.__score = score
```

## 2.排错

### ModuleNotFoundError: No module named 'requests'

由于Pycharm新建项目的时候是在虚拟环境中运行解释器，所以没有安装Requests。

解决办法：在Pycharm中打开，执行pip install requests

![](.gitbook/assets/image.png)

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





