# 安装Hexo
Node和Git bash都安装好后,本地创建一个文件夹,如myBlog,用于存放hexo的配置文件,然后进入myBlog里安装Hexo:

`npm install -g hexo`

# 初始化hexo
`hexo init`

# 利用hexo指令安装一个完整的hexo项目
`hexo generate（简写：hexo g)`

# 在本地运行hexo项目
`hexo server(简写：hexo s)`

> 注意：运行hexo s后出现页面打不开的情况时，先检查端口号是否被占用。hexo项目默认端口号为4000。如果电脑上安装了“福昕阅读器”，4000端口就被该软件占用了。

> 解决方法:
> `hexo s -p 5000 (换个新的未使用的端口号)`