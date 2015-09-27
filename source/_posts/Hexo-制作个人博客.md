title: Hexo 制作个人博客并托管到Github上
date: 2015-09-14 23:08:15
tags:Hexo git
---
最近发现一个轻便易用的个人blog系统——hexo。配置好一堆东西后，就挂到github上了。

Hexo的官网为:[Hexo](http://hexo.io)。由于Hexo是使用Node.js开发的，所以死前必须安装好Node。安装Hexo的命令相当简单：
``` shell
npm install hexo-cli -g
```

进入将要创建博客的目录，执行：
```
hexo init <目录名称>
cd <目录名称>
```
进入博客目录后，执行以下命令安装依赖的模块：
```
npm install
```
实践过程中，发现Hexo 3.0 把Server独立成模块了，需要另外安装，在博客的目录里执行：
```
npm install hexo-server --save
```
此时，只需要执行以下命令把服务器启动起来，浏览器访问：http://localhost:4000/ 即可访问到本地博客
 ```
 hexo server
 ```
 创建第一篇博文，命令是格式是 hexo new [layout] <名称>。其中，layout有三种可选值：post（正式博文），draft（不公开的草稿），page（单网页）；下面命令创建了一个名为“博客名称”的草稿。
 ```
 hexo new draft "博文名称" 
 ```
 草稿是不会在博客中显示的，顾名思义就是没写完还不想发布博文，所以就先写写草稿吧。当草稿写好了，使用命令 hexo publish [layout] <filename> 就可以把草稿发布成公开的博文了。
 Hexo博客可以根据个人喜好更改博客的主题，在这个链接中选择自己喜欢的主题:[https://hexo.io/themes/](https://hexo.io/themes/)。一般而言，每个主题在github中都会给出主题的安装方法。如本文使用的主题：https://github.com/ppoffice/hexo-theme-icarus
 ```
 git clone https://github.com/ppoffice/hexo-theme-icarus.git themes/icarus
 ```

* Rename themes\icarus\_config.yml.example to themes\icarus\_config.yml;
* Copy themes\icarus\_config.yml.site.example to your hexo blog's root directory and rename it to _config.yml;
* Then modify theme setting in _config.yml to icarus.

需要注意的是博客根目录下的_config.yml和主题根目录下的_config.yml文件的作用都是用于配置博客的。（**配置过程中遇到过一个坑，就是_config.yml文件里的键值配置中间的冒号后面必须要有个空格，否则配置读取会失败的**）

最后，是把Hexo生成的静态博客部署到Github中。此过程中遇到的坑就是根目录下的_config.yml配置文件里的deploy属性,当时提交到github中死活不通过。这是repo的url配置有误导致的，采用以下方式配置就ok了。
```
deploy: 
  type: git
  repo: https://{username}:{password}@github.com/{username}/{username}.github.io.git
  branch: master
```
配置完毕后，仅需以下两行命令就可以把博客系统部署到github上了
```
hexo generate
hexo deploy
```
如果部署过程中报错:ERROR Deployer not found : git
则需要安装缺失的模块后，重新generate和deloy
``` 
npm install hexo-deployer-git --save
```

访问:[http://{username}.github.io](http://{username}.github.io),验证自己的成果吧！