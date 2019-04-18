# 命令

### Git命令

```text
#建立本地仓库
git init 
#关联远程仓库
git remote add origin git@github.com:ZhaoqiangCn/awesome-python3-webapp.git
#添加和提交
git add .
git commit -m"添加文件"
#由于远程库是空的，第一次推送master分支时，加上-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来
git push -u origin master
#在以后的推送或者拉取时就可以简化命令，如下：
git push origin master
#从远程获取内容
git pull origin master
```

### Git提交空文件夹

项目根目录运行

```text
find . -type d -empty -exec touch {}/.gitignore \;
```



{% hint style="info" %}
abcasdasd

## 

asdasdasd阿斯打死打伤打
{% endhint %}

