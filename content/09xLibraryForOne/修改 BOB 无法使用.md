系统升级之后快捷键就不能用了，我目前的解决方法是创建了两个shell脚本：

[show.sh](https://link.zhihu.com/?target=http%3A//show.sh)

```text
defaults write com.apple.finder AppleShowAllFiles -boolean true ; killall Finder
```

[hide.sh](https://link.zhihu.com/?target=http%3A//hide.sh)

```text
defaults write com.apple.finder AppleShowAllFiles -boolean false ; killall Finde
```
---
常见代理工具的绕过方法
Clash X
ClashX 用户需要修改 proxyIgnoreList.plist 文件，其路径为 ~/.config/clash/proxyIgnoreList.plist，将下面这一行内容写入该文件：
<string>sequoia.apple.com</string>

修改完成后的效果：
image

参考教程：https://www.cnblogs.com/PowerTips/p/14775956.html

如果在 ~/.config/clash 目录下没有 proxyIgnoreList.plist 文件，你也可以直接下载下面的这个压缩包，将解压后的文件放入该目录中：
-> 点击这里下载模版文件：proxyIgnoreList_example.zip