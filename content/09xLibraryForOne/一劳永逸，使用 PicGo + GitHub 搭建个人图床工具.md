author:: alwaysbeta50 声望4 粉丝关注作者
source:: [一劳永逸，使用 PicGo + GitHub 搭建个人图床工具](https://segmentfault.com/a/1190000041076406)
clipped:: [[2022-08-26]]
published:: 

**原文链接：** [一劳永逸，使用 PicGo + GitHub 搭建个人图床工具](https://link.segmentfault.com/?enc=hZkkZ4k5B%2FcrmurPt%2B6apw%3D%3D.3TU51e08gQudmKO5%2Fajzw4Z5FSS0ByJWOYizuoAfeUol0zViSeIAG1Qv8icrPX93IIiNwp5WFXDfNxWcaox36A%3D%3D)

经常写博客的同学都知道，有一个稳定又好用的图床是多么重要。我之前用过七牛云 + Mpic 和微博图床，但总感觉配置起来比较麻烦，用起来也不是很顺手。而且更让人担心的是，万一有一天图床服务不能用了怎么办？那之前的图片岂不是都挂了。

直到遇到了 PicGo + GitHub，彻底打消了我的所有顾虑，而且配置简单，使用优雅。背靠 GitHub 和微软，稳定性问题基本不用担心。还有就是支持 Windowns，macOS 和 Linux 平台。

唯一的缺点，如果算的话，就是隐密性问题。因为所有图片都是上传到了 GitHub 的一个公有仓库，如果在意这点的话就不太适合。不过我上传的都是技术文章中的配图，这一点对我来说根本不是问题。

下面就来手把手教大家如何配置，非常简单。

### 配置 GitHub

新建仓库：

![](https://segmentfault.com/img/remote/1460000041076408)

这里需要注意：仓库得设置为 Public 。因为后面通过客户端访问算是外部访问，因此无法访问 Private ，这样的话图片传上来之后只能存储不能显示。

仓库建好之后，点击页面右上角，进入 Settings：

![](https://segmentfault.com/img/remote/1460000041076409)

然后进入 Developer settings：

![](https://segmentfault.com/img/remote/1460000041076410)

点击 Personal access tokens，再点 Generate new token 新建 token。

![](https://segmentfault.com/img/remote/1460000041076411)

填写 Notes 信息，选择 token 过期时间，为了安全，GitHub 会强烈建议不要设置成永久。这个大家根据自己实际情况选择，到期之后重新生成即可。

复选框的话，repo 一定要全选，其他的无所谓，我是都勾选了。

确定之后，就生成我们需要的 token 了。

![](https://segmentfault.com/img/remote/1460000041076412)

### 配置 PicGo

下载 PicGo：点击[下载地址](https://link.segmentfault.com/?enc=HjTqji0A%2FyAWHgeCD4Qvew%3D%3D.CDLJkxcpWT%2BHMlkfVaLMRHxbX0W%2F6tg1tekY3RzKxfbgpD1DSpkrCCaj9MrVkNwT)，然后安装。

![](https://segmentfault.com/img/remote/1460000041076413)

-   设定仓库名：上文在 GitHub 创建的仓库。
-   设定分支名：main。
-   设定 Token：上文生成的 token。
-   指定存储路径：为空的话会上传到跟目录，也可以指定路径。
-   设定自定义域名：可以为空，这里为了使用 CDN 加快图片的访问速度，按这样格式填写：[https://cdn.jsdelivr.net/gh/G...](https://link.segmentfault.com/?enc=UP1FnAXiSrLppgr%2F%2BfPV0g%3D%3D.lPU58xmkLVjvNY%2BtdolhZlcH2CxNQthIIlslHlDfo3qVIMPuyId9NEMUz8XgVj7C) 用户名/仓库名

配置完成后就可以使用了。

![](https://segmentfault.com/img/remote/1460000041076414)

直接拖拽，或者点击上传都可以。

![](https://segmentfault.com/img/remote/1460000041076415)

上传成功之后，在 GitHub 的仓库就可以看到了。

![](https://segmentfault.com/img/remote/1460000041076416)

最后，在相册里复制外链，粘贴到我们的 markdown 文档中，就可以看到图片了。

希望各位老板玩的愉快。

---

**热情推荐：**

-   **[技术博客](https://link.segmentfault.com/?enc=Suhayi4cVKb2YvzedliLsg%3D%3D.Zi4wROTvWaExGUO%2Bh%2FguCYzrI3KyZW0HdFdbmJUUASdlUW4E7UbgiOxOefwswGeJ)：** 硬核后端技术干货，内容包括 Python、Django、Docker、Go、Redis、ElasticSearch、Kafka、Linux 等。
-   **[Go 程序员](https://link.segmentfault.com/?enc=nIxVWjqAoI9WSWMpyYhTCw%3D%3D.lF0qey3QXFWgJAh4PAI63TgDwO7f4MDln88OiErMQtizJs87CCu1yfEdFrMIG15l)：** Go 学习路线图，包括基础专栏，进阶专栏，源码阅读，实战开发，面试刷题，必读书单等一系列资源。
-   **[面试题汇总](https://link.segmentfault.com/?enc=scuys%2FIDuB00iCE0rzq1YQ%3D%3D.%2F6y%2FEoJkVhLaGHAAPKSc3ATIg3XpW19FO%2FRQ5NHW6brUPkt4Us5I93ZjNyWJ%2Fc3T)：** 包括 Python、Go、Redis、MySQL、Kafka、数据结构、算法、编程、网络等各种常考题。