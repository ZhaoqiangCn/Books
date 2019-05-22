# WebTemplate

### Model-View-Controller

![](../.gitbook/assets/image%20%283%29.png)

Python处理URL的函数就是C：Controller，Controller负责业务逻辑，比如检查用户名是否存在，取出用户信息等等；

包含变量{{ name }}的模板就是V：View，View负责显示逻辑，通过简单地替换一些变量，View最终输出的就是用户看到的HTML。

MVC中的Model在哪？Model是用来传给View的，这样View在替换变量的时候，就可以从Model中取出相应的数据。 上面的例子中，Model就是一个`dict`：

```text
{ 'name': 'Michael' }
```

通过MVC，我们在Python代码中处理M：Model和C：Controller，而V：View是通过模板处理的，这样，我们就成功地把Python代码和HTML代码最大限度地分离了。HTML代码全部放到模板里，写起来更有效率。



