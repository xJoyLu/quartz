author:: null
source:: [mac隐藏文件的显示与取消显示 – GiTMBA](https://www.gitmba.com/1556.html)
clipped:: [[2022-11-30]]
published:: 

介绍

本文介绍如何把苹果电脑MAC系统的隐藏文件显示出来与取消显示隐藏的具体操作方法  
显示隐藏文件

打开终端，输入命令：

1.  defaults write com.apple.finder AppleShowAllFiles \-boolean true ; killall Finder
    
    `defaults write com.apple.finder AppleShowAllFiles -boolean true ; killall Finder`

该命令将finder的隐藏文件显示出来，并重新启动Finder。  
取消显示隐藏文件

打开终端，输入命令：

1.  defaults write com.apple.finder AppleShowAllFiles \-boolean false ; killall Finder
    
    `defaults write com.apple.finder AppleShowAllFiles -boolean false ; killall Finder`

该命令将finder的隐藏文件隐藏，并重新启动Finder。  
显示以.开头的文件

在Finder中，按快捷键Command+Shift+.

可以显示隐藏文件、文件夹，再按一次，恢复隐藏。  
前往任何文件夹

finder下使用Command+Shift+G 可以前往任何文件夹，包括隐藏文件夹。