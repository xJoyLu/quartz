author:: 孜然aa
source:: [vscode插件ftp-simple使用记录 - 掘金](https://juejin.cn/post/7043686949411880991)
clipped:: [[2022-07-29]]
published:: 

#稍后阅读

   

[![](https://p3-passport.byteacctimg.com/img/mosaic-legacy/3791/5035712059~300x300.image)](https://juejin.cn/user/1689323426553400)

2021年12月20日 15:43 ·  阅读 656

-   想要本地文件上传到服务器，想要借助ftp来实现，看了网上推荐的一些插件，最后选择了ftp-simple。一方面是使用简单，另一方面是下载量相对是比较多的。由于网上对ftp-simple的使用说明较少，第一次使用费了一些功夫，为了防止忘记，特做此记录。

1.  在vscode中下载插件ftp-simpl
    
    ![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/46157e1d3ae04053bc98a53ff37822e1~tplv-k3u1fbpfcp-zoom-in-crop-mark:3024:0:0:0.awebp?)
    
2.  打开命令面板（两种方式）。
    
    -   第一种是快捷键ctrl+shift+p
    -   第二种是 设置（左下角）-> 命令面板
3.  输入ftp-simple，找到config -setting点击进入
    
    ![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/8e1f2e0daffd44bab02aaf99a370be3b~tplv-k3u1fbpfcp-zoom-in-crop-mark:3024:0:0:0.awebp?)
    
4.  点击以后会自动生成基础配置项
    
    ![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/7469c8d7b94a4e4b9191d0680eaa36eb~tplv-k3u1fbpfcp-zoom-in-crop-mark:3024:0:0:0.awebp?)
    
5.  参数说明：
    
    -   name: ftp服务器的名字，可以随意填写
    -   host: 自己的服务器域名
    -   port: 端口号，要与ftp服务端口对应
    -   type: ftp
    -   username: ftp服务的用户名
    -   password: ftp服务密码
    -   path：远程路径
    -   autosave： 自动保存
6.  在左侧目录你想要上传的文件上点击右键。有以下功能选择：
    
    ![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/4ddbb4b213214623b01ac3106aec8f71~tplv-k3u1fbpfcp-zoom-in-crop-mark:3024:0:0:0.awebp?)
    
    save-upload可以上传到远程目录，上传方式有两种，include，exclude，区别在于是否连同文件夹一起上传，可根据自己需求选择。（撰文不易，三连鼓励）