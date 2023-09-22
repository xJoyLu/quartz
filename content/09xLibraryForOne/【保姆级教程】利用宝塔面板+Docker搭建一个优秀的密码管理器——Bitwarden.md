  
Bitwarden 是一款开源密码管理器，它会将所有密码加密存储在服务器上，它的工作方式与 LastPass、1Password 或 Dashlane 相同。  
  
  
  
官方的版本搭建对服务器要求很高，搭建不容易，GitHub上有人用 Rust 实现了 Bitwarden 服务器，项目叫 vaultwarden，并且提供了 Docker 镜像，这个实现更进一步降低了对机器配置的要求，并且 Docker 镜像体积很小，部署非常方便。这个项目目前在GitHub也有9.8k的star，非常受欢迎。  
  
  
  
此外，官方服务器中需要付费订阅的一些功能，在这个实现中是免费的。  
  
  
  
这篇文章就利用宝塔面板来docker搭建Bitwarden。  
  
视频  
  
一：简介  
项目：https://github.com/dani-garcia/vaultwarden  
  
二：要求  
aapanel 6.8.13 （宝塔海外版）  
  
一个解析好的域名  
  
腾讯轻量云香港服务器 （演示系统：Debian 10）  
  
三：部署  
aapanel安装  
官方地址：https://forum.aapanel.com/d/9-aapanel-linux-panel-6812-installation-tutorial  
  
Centos :  
yum install -y wget && wget -O install.sh http://www.aapanel.com/script/install_6.0_en.sh && bash install.sh  
Ubuntu/Deepin :  
wget -O install.sh http://www.aapanel.com/script/install-ubuntu_6.0_en.sh && sudo bash install.sh  
Debian :  
wget -O install.sh http://www.aapanel.com/script/install-ubuntu_6.0_en.sh && bash install.sh  
Docker安装  
官方地址：https://docs.docker.com/engine/install/debian/  
  
  
  
sudo apt-get update  
  
  
sudo apt-get install \  
    apt-transport-https \  
    ca-certificates \  
    curl \  
    gnupg \  
    lsb-release  
  
  
 curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg  
  
  
echo \  
  "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian \  
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null  
  
  
 sudo apt-get update  
 sudo apt-get install docker-ce docker-ce-cli containerd.io  
  
  
 sudo docker run hello-world  
 systemctl enable docker #设置docker开机自动启动  
   
 systemctl status docker #查看docker状态  
正式部署  
用Docker来部署，两行命令就够了，命令如下：  
  
docker run -d --name bitwardenrs \  
  --restart unless-stopped \  
  -e WEBSOCKET_ENABLED=true \  
  -v /www/wwwroot/demo/:/data/ \  
  -p 6666:80 \  
  -p 3012:3012 \  
  vaultwarden/server:latest  
注意：/www/wwwroot/demo/ 请修为自己的路径  
  
安装截图，如下：  
  
  
  
四：设置反向代理  
上面的设置好之后，我们还需要设置反向代理才可以打开网站，但是在设置之前，我们需要新建一个站点，并且设置好SSL证书。这些还是用宝塔面板来操作。我们需要把【http://127.0.0.1:6666】设置反向代理，如图：  
  
  
  
代码如下：  
  
  
        location / {  
    proxy_pass http://127.0.0.1:6666/;  
    rewrite ^/(.*)$ /$1 break;  
    proxy_redirect off;  
    proxy_set_header Host $host;  
    proxy_set_header X-Forwarded-Proto $scheme;  
    proxy_set_header X-Real-IP $remote_addr;  
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;  
    proxy_set_header Upgrade-Insecure-Requests 1;  
    proxy_set_header X-Forwarded-Proto https;  
  }  
五：登录Bitwarden  
设置好反向代理之后，我们就可以打开站点，如图：  
  
  
  
注意：创建账号，需要在开启了ssl证书的情况下才会成功。  
  
注册账号后，就可以用这个账号来登录Bitwarden了，如图：  
  
  
  
六：配置  
因为现在的状态是所有人都可以注册这个网站，这个东西只是自己使用，所以我们需要关闭掉注册，使用下面的命令。使用之前可以在宝塔面板中删除掉之前的容器，然后运行以下命令来重新创建容器并开启禁止用户注册的功能。  
  
不必担心，因为指定了 volume 映射，删除容器后不会删除数据。SIGNUPS_ALLOWED=false 代表禁止注册！  
  
6.1、禁用新用户的注册  
docker stop bitwardenrs  #停止容器  
docker rm -f bitwardenrs  #删除容器  
docker run -d --name bitwardenrs \  
  --restart unless-stopped \  
  -e SIGNUPS_ALLOWED=false \  
  -e WEBSOCKET_ENABLED=true \  
  -v /www/wwwroot/demo/:/data/ \  
  -p 6666:80 \  
  -p 3012:3012 \  
  vaultwarden/server:latest  
运行完在容器列表里就又可以重新看到了，然后再去试下创建账号就会出现一个不能创建账号的错误提示：  
  
  
  
七：设置自动同步  
bitwarden 默认是不会自动同步的，不管你是添加或者删除又或是修改了一条记录，都只是先保存在本地，只有当你手动点一下同步时才会进行同步。此时我们可以打开 WebSockets notifications 功能，这样手机修改后会立刻自动同步到云端。所以，我们还需要需要上面的反向代理。  
  
打开网站配置文件，直接复制过去就可以了。（可以把前面第四步的反向代理那段替换掉）  
  
  
  
    location / {  
        proxy_pass http://127.0.0.1:6666;  
        proxy_set_header Host $host;  
        proxy_set_header X-Real-IP $remote_addr;  
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;  
        proxy_set_header X-Forwarded-Proto $scheme;  
    }  
    
    location /notifications/hub {  
        proxy_pass http://127.0.0.1:3012;  
        proxy_set_header Upgrade $http_upgrade;  
        proxy_set_header Connection "upgrade";  
    }  
    
    location /notifications/hub/negotiate {  
        proxy_pass http://127.0.0.1:6666;  
    }  
八：下载客户端  
登录Bitwarden，在右上角点击头像，然后点击【获取应用】，如图：  
  
  
  
我们看到，基本所有都支持了，  
  
  
  
用chrome插件来演示一下。如图：  
  
  
  
点击小齿轮，输入我们搭建的网站地址：  
  
  
  
保存登陆即可。  
  
  
  
  
  
自动生成密码展示：  
  
  
  
小纸条功能展示：  
  
  
  
  
  
同理，手机端也一样操作即可。  
  
这样我们使用Chrome也可以方便的管理自己的密码了，最重要的是Bitwarden完全开源，完全免费。  
  
十：总结  
目前比较流行的密码管理软件有 1Password、LastPass 、KeePass、Enpass以及SafeInCloud等，但是完全免费开源的只有Bitwarden。我们只需要借助Docker就可以很容易搭建一个自己的密码管理平台。  
  
bitwarden优点：全平台，免费、开源，在安卓上体验很好，有多种双重验证，自动填充功能正常，有密码泄露检测，适应大部分 APP，可以自定义字段，可以正则匹配网址，可以自定义图标，会根据网址或 APP 自动获取 ico，可以指纹解锁，中文翻译很好。  
  
咕咕鸽也是才开始使用，对这个工具还不是非常熟悉，欢迎大家在评论区和本鸽分享一下它的其他好玩的功能！