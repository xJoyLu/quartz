温馨提示：

本文最后更新于 2022-11-18，若内容或图片失效，请留言反馈。部分素材来自网络，若不小心影响到您的利益，请联系我们删除。

> 破解方法来自github上一个大佬 [somebasj](https://github.com/somebasj/ParallelsDesktopCrack) ，不过直接用他提供的脚本激活基本没法成功，所以我这边出个教程帮助大家成功激活。

> 按照github上的描述，这个激活方式是全面支持intel和arm芯片的，不过我这边只有m1的mac，所以intel芯片的激活未测试。

> 2022年11月9日注：最新的18.1可以激活可以加载虚拟机（m1、mac os 13系统亲测）。最新的mac os 13系统使用该教程破解依然可以生效。

## 准备工作

1.  下载pd  
    官网下载地址：  
    18.1：[https://download.parallels.com/desktop/v18/18.1.0-53311/ParallelsDesktop-18.1.0-53311.dmg](https://download.parallels.com/desktop/v18/18.1.0-53311/ParallelsDesktop-18.1.0-53311.dmg)  
    18.0.1： [https://download.parallels.com/desktop/v18/18.0.1-53056/ParallelsDesktop-18.0.1-53056.dmg](https://download.parallels.com/desktop/v18/18.0.1-53056/ParallelsDesktop-18.0.1-53056.dmg)
2.  下载破解补丁  
    18.1：
    
    parallelsdesktopcrack.zip
    
    来源：默认网盘
    
    [](https://pan.luoxx.top/s/DNCM)  
    18.0.1：
    
    parallelsdesktopcrack.zip
    
    来源：默认网盘
    
    [](https://pan.luoxx.top/s/OPfw)

## 激活方式1

> github作者更新了激活脚本，应该是可以直接一键激活了，大家可以先试一下，不行再使用 `激活方式2`

-   使用方法  
    下载补丁后解压，然后cd进入解压后的目录，然后执行 `chmod +x ./install.sh && sudo ./install.sh` 命令即可。  
    ps：执行该命令会需要输入密码以授权。
- 备注：
	- 1、系统设置-隐私与安全性--完全磁盘访问权限--终端（勾选）； 
	- 2、把破解文件夹Crack中的prl_disp_service复制到chflags：//后面路径的文件夹里面 然后按照“激活方法1”操作就行了

## 激活方式2

-   如果安装过pd17或者更早版本，可以完全卸载以确保之后能成功激活。（可选，不卸载也行，不过可能会有坑）  
    建议使用 [App Cleaner](https://macapp.org.cn/app/app-cleaner-and-uninstaller-pro.html) 来卸载，这样卸载的比较干净  
    ps：**卸载之前请先备份好自己的虚拟机**，不然卸载完就啥都没了，虚拟机文件存放目录为 `~/Parallels`。 就是如下图这样的一个文件，复制一份到其他地方保存好。  
    ![image-1662517049731](https://cdn.luoxx.top/halo/image-1662517049731.png)
    
-   下载pd18安装文件，安装，安装之后到激活那一步就不用继续走了，退出pd。
    
-   下载破解补丁到 `下载目录` ，也就是 `~/Downloads`, 然后解压缩，不要修改解压后的文件夹名称，这样操作都是为了保障后续执行脚本路径正确。
    
-   打开终端，开始执行命令破解，作者提供的一键破解脚本有点问题，所以 `install.sh` 文件忽略即可，我们手动执行命令破解
    

1.  进入破解补丁的目录

```bash
cd ~/Downloads/parallelsdesktopcrack
```

2.  杀掉pd的进程

```bash
killall -9 prl_client_app
killall -9 prl_disp_service
```

3.  复制破解补丁文件到pd目录 (执行命令时提示要输入密码的话就输入自己电脑的密码然后回车)

```bash
sudo cp -f prl_disp_service "/Applications/Parallels Desktop.app/Contents/MacOS/Parallels Service.app/Contents/MacOS/prl_disp_service"
sudo chown root:wheel "/Applications/Parallels Desktop.app/Contents/MacOS/Parallels Service.app/Contents/MacOS/prl_disp_service"
sudo chmod 755 "/Applications/Parallels Desktop.app/Contents/MacOS/Parallels Service.app/Contents/MacOS/prl_disp_service"
```

4.  签名 (执行命令时提示要输入密码的话就输入自己电脑的密码然后回车)

```bash
sudo codesign -f -s - --timestamp=none --all-architectures --entitlements ParallelsService.entitlements "/Applications/Parallels Desktop.app/Contents/MacOS/Parallels Service.app/Contents/MacOS/prl_disp_service"
```

5.  创建并编辑激活秘钥文件 (执行命令时提示要输入密码的话就输入自己电脑的密码然后回车)

```bash
#先删除原来的证书文件（如果有的话，此命令报错没关系）
sudo rm -f /Library/Preferences/Parallels/licenses.json
#生成新的证书文件
sudo cp -f licenses.json "/Library/Preferences/Parallels/licenses.json"
sudo chown root:wheel "/Library/Preferences/Parallels/licenses.json"
sudo chmod 444 "/Library/Preferences/Parallels/licenses.json"
sudo chflags uchg "/Library/Preferences/Parallels/licenses.json"
sudo chflags schg "/Library/Preferences/Parallels/licenses.json"
```

-   至此，破解已完成，再次打开pd就不会弹出激活弹出了。  
    ps：恢复之前备份的虚拟机，只要在创建虚拟机的流程那里选择打开，然后选择之前备份的虚拟机文件即可。

## 激活方式3

> 由于前两种激活方式有一小部分朋友的机器上会有各种各样的报错情况，所以这边又加上了一种更直接的方式。  
> tnt团队也出了一个这个版本的破解程序，也是用的这个github大佬提供的资源。  
> 如果前两种方式行不通的，可以试一试。

下载地址：

-   tnt网站地址：[https://appstorrent.ru/61-parallels-desktop.html](https://appstorrent.ru/61-parallels-desktop.html) （需要科学上网才能访问）
    
-   Parallels Desktop 18.0.1-53056 Intel for macOS 11+  
    
    ParallelsDesktop-18_0_1-53056_by_Day.dmg
    
    来源：百度网盘 | 提取码：36hi
    
    [](https://pan.baidu.com/s/14Raub9nSoWWwK-tL7P3Vsw?pwd=36hi)
    
-   Parallels Desktop 18.0.1-53056 U2B  
    
    Parallels_Desktop_18_0_1-53056_U2B.dmg
    
    来源：百度网盘 | 提取码：2r3h
    
    [](https://pan.baidu.com/s/11ioZuUl70iWjIZEu8X6Q8A?pwd=2r3h)
    

ps1：tnt网站上提供了两种安装包，我也不知道 `U2B` 是个啥版本，不过建议arm芯片的还是先安装这个版本试试，毕竟另外那个明确写了是intel版本  
ps2：建议完全卸载老版本pd之后再安装这个版本  
ps3：这种方式博主没试过，不确定是不是百分百ok

## 其他补充操作

1.  配置host屏蔽pd检测（以防万一）  
    补丁作者原话：

> Parallels Desktop may upload client info or logs to server.  
> You can use a firewall block there domains.  
> Or use Hosts, AdGuardHome filter DNS resolve.

大概就是说pd服务器可能会检测你本地的pd状态，最好使用防火墙或者host屏蔽掉pd的检测，以防哪天破解失效。

我们这边采用配置host的方式，比较简单。

编辑host文件

```bash
sudo vim /etc/hosts
```

在文件最后面加上以下配置

```bash
5.0.0.1 download.parallels.com
5.0.0.1 update.parallels.com
5.0.0.1 desktop.parallels.com
5.0.0.1 download.parallels.com.cdn.cloudflare.net
5.0.0.1 update.parallels.com.cdn.cloudflare.net
5.0.0.1 desktop.parallels.com.cdn.cloudflare.net
5.0.0.1 www.parallels.cn
5.0.0.1 www.parallels.com
5.0.0.1 reportus.parallels.com
5.0.0.1 parallels.com
5.0.0.1 parallels.cn
5.0.0.1 pax-manager.myparallels.com
5.0.0.1 myparallels.com
5.0.0.1 my.parallels.com
```

然后 esc + :wq 保存修改即可

使用clash代理的时候，会导致host配置失效，解决方法为：在clash的yml配置文件中，修改配置 dns: enable: false。

```yml
dns:
  enable: false
```

这样修改之后host就能生效了，但是如果clash设置了自动更新订阅的话，更新订阅的时候配置文件又会被覆盖掉，着实比较麻烦，没有特别好的解决办法，估计只能自己写一个定时任务，定时修改这个配置了，定时任务我自己写了一个，详见这篇博客 [https://luoxx.top/archives/mac-clash-yml-auto-update。](https://luoxx.top/archives/mac-clash-yml-auto-update%E3%80%82)

-   补充一个新的更方便的防止host文件被修改的方法，感谢网友 `ttkanni` 提供的方法

```bash
sudo chflags uchg /etc/hosts #锁定Hosts文件，只读
sudo chflags nouchg /etc/hosts #解锁Hosts文件，读写
```

## 激活出错的情况

有一些朋友激活时遇到无权限的问题，我这边始终没法复现，不过遇到报错之后可以尝试一下以下方案

1.  文件赋予最高的权限

```bash
#如果当前目录不是破解补丁所在目录，则需要先cd进入破解补丁所在目录，比如 cd ~/Downloads/ParallelsDesktop_18.0.1.53056_Patch
chmod 777 *
```

2.  给予终端全盘访问权限  
    `设置-安全性与隐私-隐私-完全磁盘访问权限`  
    这个里面勾上终端，没有的话点击左下角加号手动添加一下终端
    
3.  手动将破解文件夹下的 `prl_disp_service` 文件复制替换到 `/Applications/Parallels\ Desktop.app/Contents/MacOS/Parallels\ Service.app/Contents/MacOS/` 目录下。有很多报错是因为复制无权限造成的，可以在访达自己操作这一步，然后继续破解操作。
    

## 效果展示

![image-1662518173883](https://cdn.luoxx.top/halo/image-1662518173883.png)

>