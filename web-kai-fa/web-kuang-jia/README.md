# WebFrame

### Web Server Gateway Interface

#### WSGI处理函数

我们来看一个最简单的Web版本的“Hello, web!”：

```python
def application(environ, start_response):
    start_response('200 OK', [('Content-Type', 'text/html')])
    return [b'<h1>Hello, web!</h1>']
```

上面的`application()`函数就是符合WSGI标准的一个HTTP处理函数，它接收两个参数：

* environ：一个包含所有HTTP请求信息的`dict`对象；
* start\_response：一个发送HTTP响应的函数。

{% hint style="info" %}
 有了WSGI，我们关心的就是如何从`environ`这个`dict`对象拿到HTTP请求信息，然后构造HTML，通过`start_response()`发送Header，最后返回Body。
{% endhint %}

#### WSGI服务器

Python内置了一个WSGI服务器，这个模块叫wsgiref

```python
# server.py
# 从wsgiref模块导入:
from wsgiref.simple_server import make_server
# 导入我们自己编写的application函数:
from hello import application

# 创建一个服务器，IP地址为空，端口是8000，处理函数是application:
httpd = make_server('', 8000, application)
print('Serving HTTP on port 8000...')
# 开始监听HTTP请求:
httpd.serve_forever()
```

#### 扩展

稍微改造一下，从`environ`里读取`PATH_INFO`，这样可以显示更加动态的内容

```python
def application(environ, start_response):
    start_response('200 OK', [('Content-Type', 'text/html')])
    body = '<h1>Hello, %s!</h1>' % (environ['PATH_INFO'][1:] or 'web')
    return [body.encode('utf-8')]
```



