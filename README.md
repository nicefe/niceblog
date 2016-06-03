# niceblog
用来存放nice-blog的代码啦

>发布说明

联系益达，获得当前niceblog和nicefe.github.io的权限。
clone到本地，执行npm install

    git clone https://github.com/nicefe/niceblog && npm install

可以先运行下hexo s 来查看下运行效果
    hexo s

###创建一篇文章
执行 hexo n '你的文章名'
会在source/_posts下创建一个你的文章名的markdown文件，在里面写文章balbala
如果你的hexo s没有关闭，可以直接在网页上刷新，看到你的文章效果

###发布
先执行 hexo g
生成静态文件
再执行 hexo deploy
这个时候会默认提示你输入用户名和密码。这个时候输入。
顺利的话跑完，就部署到https://nicefe.github.io上去了。

##注意！
为了保证不冲突，最好每次hexo deploy之前都要先更新一下当前的niceblog项目代码。尽量减少冲突。
