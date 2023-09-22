author:: null
source:: [Github图床](https://zlogs.net/blog/19/10052139/)
clipped:: [[2022-08-26]]
published:: 

## [](#1-2点击Repositories "1.2点击Repositories")1.2点击Repositories

## [](#1-3点击NEW "1.3点击NEW")1.3点击NEW

![](https://img1.zlogs.net/19/20191005214514.png)

## [](#1-4创建项目 "1.4创建项目")1.4创建项目

![](https://img1.zlogs.net/19/20191005215135.png)

详情参考[OAuth Apps和Personal access tokens获取与配置](https://zlogs.net/2019/10/05/201910051840/)，下面将做简要介绍

## [](#2-1点击设置 "2.1点击设置")2.1点击设置

![](https://img1.zlogs.net/19/20191005222309.png)

## [](#2-2点击Developer-settings "2.2点击Developer settings")2.2点击Developer settings

![w](https://img1.zlogs.net/19/20191005222507.png)

## [](#2-3点击tokens点击new "2.3点击tokens点击new")2.3点击tokens点击new

![](https://img1.zlogs.net/19/20191005222624.png)

## [](#2-4输入密码 "2.4输入密码")2.4输入密码

![](https://img1.zlogs.net/19/20191005222849.png)

## [](#2-5输入note，勾选权限 "2.5输入note，勾选权限")2.5输入note，勾选权限

![](https://img1.zlogs.net/19/20191005222959.png)

## [](#2-6点击文末生成 "2.6点击文末生成")2.6点击文末生成

![](https://img1.zlogs.net/19/20191005223240.png)

## [](#2-7复制并备份生成的代码 "2.7复制并备份生成的代码")2.7复制并备份生成的代码

此代码只出现一次，一定要备份

![](https://img1.zlogs.net/19/20191005224944.png)

## [](#3-1下载picgo，并安装 "3.1下载picgo，并安装")3.1下载picgo，并安装

地址[https://molunerfinn.com/PicGo/](https://molunerfinn.com/PicGo/)

## [](#3-2右击picgo，打开详细窗口 "3.2右击picgo，打开详细窗口")3.2右击picgo，打开详细窗口

![](https://img1.zlogs.net/19/20191005225743.png)

## [](#3-3配置picgo "3.3配置picgo")3.3配置picgo

![](https://img1.zlogs.net/19/20191005225656.png)

> 设置仓库名：用户名/仓库名
> 
> > 用户名为github用户名，仓库名为1.4创建项目的仓库名
> 
> 设置分支名：master
> 
> > 当然也可以创建其他分支，再设置
> 
> 设定Token：为2.7步生产的代码
> 
> > 此代码一定要备份，且不要公开
> 
> 指定存储路径：可以自定义其他的，相当于创建一个文件夹
> 
> > 按照上图img2019，会在github上生成一个img2019文件夹，方便整理，注意后面加`\`
> 
> 设置自定义域名：`https://raw.githubusercontent.com/用户名/项目名/分支名`
> 
> > 如我的`https://raw.githubusercontent.com/ZanderZhao/my-images/master`
> 
> > 设置自定义域名作用是上传图片后会返回图片地址到剪贴板，即“上面自定义域名+图片名”会直接返回到剪贴板,此步可以优化，详见6.优化。

## [](#3-4点击确定 "3.4点击确定")3.4点击确定

完成配置

## [](#4-1将图片拖到小窗口 "4.1将图片拖到小窗口")4.1将图片拖到小窗口

![](https://img1.zlogs.net/19/20191005231328.png)

## [](#4-2剪贴板会返回图片地址 "4.2剪贴板会返回图片地址")4.2剪贴板会返回图片地址

Ctrl+V 粘贴到下方显示

返回地址结果是

`https://raw.githubusercontent.com/ZanderZhao/my-images/master/img2019/图片名`

## [](#5-1时间戳重命名可以防止自定义命名出现重复，发生替换 "5.1时间戳重命名可以防止自定义命名出现重复，发生替换")5.1时间戳重命名可以防止自定义命名出现重复，发生替换

![](https://img1.zlogs.net/19/20191005232910.png)

## [](#5-2设置链接格式可以返回想要的链接 "5.2设置链接格式可以返回想要的链接")5.2设置链接格式可以返回想要的链接

![](https://img1.zlogs.net/19/20191005232144.png)

## [](#6-0直接用githubusercontent "6.0直接用githubusercontent")6.0直接用githubusercontent

-   优点
    -   方便读者定位github仓库
    -   替换文件马上更新，没有延迟
-   缺点
    -   速度太慢，而且部分区域可能加载不了
    -   如果更换其他图床的话，需要一个个改`raw.githubusercontent.com`字段
    -   上传图库的话，会产生小绿点，但是没有什么实际提交，图片多无效提交记录也多

## [](#6-1新建组织，直接用githubusercontent "6.1新建组织，直接用githubusercontent")6.1新建组织，直接用githubusercontent

新建一个组织，然后自己为管理员，新建仓库，按照上文继续进行

-   优点
    -   方便读者定位github仓库
    -   替换文件马上更新，没有延迟
    -   不会产生较多无效提交记录
-   缺点
    -   速度太慢，而且部分区域可能加载不了
    -   如果更换其他图床的话，需要一个个改`raw.githubusercontent.com`字段

## [](#6-2使用jsdelivr的cdn "6.2使用jsdelivr的cdn")6.2使用jsdelivr的cdn

> jsdelivr加速github的public repo不需要付费，不想要注册登陆，直接使用对于地址即可。

如果使用cdn可以是`https://cdn.jsdelivr.net/gh/用户名/项目名`或者`https://cdn.jsdelivr.net/gh/用户名/项目名@分支名`

如果不`@分支`默认是master分支，即使master分支不是default分支，如果直接替换github的文件，cdn有缓存延迟。

-   优点
    -   方便读者定位github仓库
    -   速度比raw.githubusercontent.com的快
-   缺点
    -   如果直接更新github的文件的话，更新缓存需要一定时间
    -   如果更换其他图床的话，需要一个个改`cdn.jsdelivr.net`字段

## [](#6-3使用github-pages "6.3使用github pages")6.3使用github pages

绑定域名，picgo配置就填入`https://域名`，但是[如果是github page的话，每小时只能构建10次](https://help.github.com/cn/github/working-with-github-pages/about-github-pages#usage-limits)。

-   优点
    -   更换图床直接改域名指向就可（若只启用pages不绑定域名没有此优点）
    -   速度比raw.githubusercontent.com的快
    -   如果直接更新github的文件的话，构建需要一定时间，但是更新速度比jsdelivr快，几分钟的事
-   缺点
    -   普通每小时只能构建10次，超过10次不再构建

## [](#6-4使用cloudflare-jsdelivr "6.4使用cloudflare+jsdelivr")6.4使用cloudflare+jsdelivr

1.使用cloudflare解析域名

2.添加一个解析，如`img1.zlogs.net`,A记录解析或者CNAME解析都可以，指向任意地方，如A-8.8.8.8、CNAME-zanderzhao.github.io等,**一定**要开启CDN，就是那个小黄色云朵要开启，目的是让域名解析到cloudflare

3.选择页面规则，创建页面规则

![](https://img1.zlogs.net/20/20200414025332.png)

4.页面规则配置如下,根据下列配置自己的，可以点击了解更多查看配置信息

![](https://img1.zlogs.net/20/20200414025141.png)

-   优点
    -   更换图床直接改域名指向就可
    -   速度比raw.githubusercontent.com的快
    -   方便读者定位图片所在github仓库
-   缺点
    -   如果直接更新github的文件的话，更新缓存需要一定时间
    -   页面规则301重定向可能耗费时间，但是实测还行，没感觉

## [](#6-5使用腾讯CDN-cloudflare-jsdelivr "6.5使用腾讯CDN+cloudflare+jsdelivr")6.5使用腾讯CDN+cloudflare+jsdelivr

-   问题
    -   用了一段时间，发现移动可能会访问不了，准备国内走腾讯，国外走cloudflare

## [](#7-0直接用githubusercontent "7.0直接用githubusercontent")7.0直接用githubusercontent

不做演示

## [](#7-1新建组织，直接用githubusercontent "7.1新建组织，直接用githubusercontent")7.1新建组织，直接用githubusercontent

-   7.1.1新建一个组织[https://github.com/plugins-zander](https://github.com/plugins-zander)，然后自己就是管理员
    
-   7.1.2新建仓库[https://github.com/plugins-zander/img](https://github.com/plugins-zander/img)
    
-   7.1.3上传头像到[https://github.com/plugins-zander/img/tree/master/avatar/zander](https://github.com/plugins-zander/img/tree/master/avatar/zander)
    
-   7.1.4则图片地址为`https://raw.githubusercontent.com/plugins-zander/img/master/avatar/zander/default.jpg`
    
-   下图为效果
    

![](https://raw.githubusercontent.com/plugins-zander/img/master/avatar/zander/default.jpg)

## [](#7-2使用jsdelivr的cdn "7.2使用jsdelivr的cdn")7.2使用jsdelivr的cdn

-   7.2.1新建一个组织[https://github.com/plugins-zander](https://github.com/plugins-zander)，然后自己就是管理员
    
-   7.2.2新建仓库[https://github.com/plugins-zander/img](https://github.com/plugins-zander/img)
    
-   7.2.3上传头像到[https://github.com/plugins-zander/img/tree/master/avatar/zander](https://github.com/plugins-zander/img/tree/master/avatar/zander)
    
-   7.2.4则图片地址为`https://cdn.jsdelivr.net/gh/plugins-zander/img/avatar/zander/default.jpg`或者`https://cdn.jsdelivr.net/gh/plugins-zander/img@master/avatar/zander/default.jpg`
    
-   下图为效果
    

![](https://cdn.jsdelivr.net/gh/plugins-zander/img/avatar/zander/default.jpg)  
或者  
![](https://cdn.jsdelivr.net/gh/plugins-zander/img@master/avatar/zander/default.jpg)

## [](#7-3使用github-pages "7.3使用github pages")7.3使用github pages

-   7.3.1新建一个组织[https://github.com/plugins-zander](https://github.com/plugins-zander)，然后自己就是管理员
    
-   7.3.2新建仓库[https://github.com/plugins-zander/img](https://github.com/plugins-zander/img)
    
-   7.3.3上传头像到[https://github.com/plugins-zander/img/tree/master/avatar/zander](https://github.com/plugins-zander/img/tree/master/avatar/zander)
    
-   7.3.4在域名服务商处将域名`img.zlogs.net` CNAME解析到`plugins-zander.github.io`
    
-   7.3.5在github在仓库[https://github.com/plugins-zander/img](https://github.com/plugins-zander/img)设置里面开启pages并绑定域名`img.zlogs.net`
    
-   7.3.6则图片地址为`https://img.zlogs.net/avatar/zander/default.jpg`
    
-   下图为效果
    

![](https://img.zlogs.net/avatar/zander/default.jpg)

## [](#7-4使用cloudflare-jsdelivr "7.4使用cloudflare+jsdelivr")7.4使用cloudflare+jsdelivr

-   7.4.1新建一个组织[https://github.com/plugins-zander](https://github.com/plugins-zander)，然后自己就是管理员
    
-   7.4.2新建仓库[https://github.com/plugins-zander/img1](https://github.com/plugins-zander/img1)
    
-   7.4.3上传头像到[https://github.com/plugins-zander/img1/tree/master/20/20200413235956.jpg](https://github.com/plugins-zander/img1/tree/master/20/20200413235956.jpg)
    
-   7.4.4使用cloudflare解析域名
    
-   7.4.5在cloudflare解析处将域名`img1.zlogs.net` CNAME解析到`plugins-zander.github.io`,并开启CDN
    
-   7.4.6选择页面规则，创建页面规则
    

![](https://img1.zlogs.net/20/20200414025332.png)

-   7.4.7页面规则配置如下,根据下列配置自己的，可以点击了解更多查看配置信息

![](https://img1.zlogs.net/20/20200414025141.png)

-   7.4.8则图片地址为`https://img1.zlogs.net/20/20200413235956.jpg`
    
-   下图为效果
    

![](https://img1.zlogs.net/20/20200413235956.jpg)

> 补充：
> 
> 江苏联通jsdelivr和github-pages速度感觉差不多
> 
> 301跳转速度可以忽略
> 
> 以上说明针对不同版本可能存在差异

## [](#8-1web工具 "8.1web工具")8.1web工具

-   项目地址
    
    -   [https://github.com/xiebruce/PicUploader](https://github.com/xiebruce/PicUploader)
-   宝塔安装步骤
    
    -   > 准备阶段
        
        -   建立网站
            
        -   申请证书
            
        -   设置网站nginx配置文件(替换location部分)
            
        -   ```
                location / {
                    index dashboard.php;
                    try_files $uri $uri/ index.php$is_args$args;
                }
            
                location ~ \.php$ {
                    fastcgi_pass 127.0.0.1:9000;
                    fastcgi_index index.php;
                    include fastcgi.conf;
                }
            ```
            
-   > 下载阶段
    
    -   下载解压到网站目录
    -   将运行文件夹权限设置成`www755`
    -   绑定安装目录，设置密码
-   > 通用配置阶段
    
    -   选择图床
    -   图片压缩选项
    -   设置文件格式`{Y}{m}{d}{H}{i}{s}`
    -   返回链接类型`custom`数值为`![]({{url}})`
    -   常用目录`/20`
    -   不启用水印
    -   保存
-   > 本地服务器
    
    -   下载文件已有文件在`img1`里面，将图床目录`img1`设置为`www755`
    -   前缀`/www/wwwroot/imgs.zlogs.net/img1`
    -   文件夹`/20`
    -   域名`https://img1.zlogs.net`
-   > Github
    
    -   plugins-zander/img1
    -   master
    -   `/20`
    -   Upload from PicUploader
    -   Token [https://github.com/settings/tokens](https://github.com/settings/tokens)
    -   [https://img1.zlogs.net](https://img1.zlogs.net/)