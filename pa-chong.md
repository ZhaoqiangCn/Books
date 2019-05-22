# 第三章 - Web Crawler

## 静态网页

* 通过Requests.get\(\)获取网页的HTML信息
* 通过beautifulsoup4解析HTML信息，find\_all匹配的返回的结果是一个列表。提取匹配结果后，使用text属性，提取文本内容，滤除br标签。随后使用replace方法，剔除空格，替换为回车进行分段。&nbsp;在html中是用来表示空格的。replace\('\xa0'\*8,'\n\n'\)就是去掉下图的八个空格符号，并用回车代替
* 一般静态页面的正文部分的标签是“showtxt”

## 动态网页

* 通过fiddler抓取网页的json包信息，然后解析json数据，分析数据中包含图片的节点，分析图片下载服务器的地址，最后整合数据得到每张图片的下载地址。

  ```python
  html = json.loads(req.text)
  for each in html['preview_photos']:
      print('图片ID:', each['id'])
  ```

* 验证Request Headers，通过Fiddler的抓包信息，可以看到Requests Headers里又很多参数。
  * User-Agent：这里面存放浏览器的信息
  * Referer：这个参数也可以用于反爬虫，它表示这个请求是从哪发出的。
  * authorization：在我们用浏览器访问的时候，服务器会为访问者分配这个用户ID。如果后台设计者，验证这个参数，对于没有用户ID的请求一律禁止访问，这样就又起到了反爬虫的作用。

    ```python
    if __name__ == '__main__':
        target = 'http://unsplash.com/napi/feeds/home'
        headers = {'authorization':'your Client-ID'}
        req = requests.get(url=target, headers=headers, verify=False)
        print(req.text)
    ```

## 视频

## 手机APP



