## 引言

随着搭载 M1 Pro 和 M1 Max 芯片的新款 MacBook Pro 上市，Apple 历史上的第二次平台迁移已经打下了扎实的基础；M1 系列芯片的优秀表现，也让用户在选购时无需在其与 Intel 平台旧款间纠结。

然而，如果说 M1 系列 Mac 机型目前还有什么制约用户、特别是办公用户选购的因素，那就是**缺少运行 Windows 的完善方案**。在过去，Mac 用户运行 Windows 的选择很多：既可以使用 Apple 官方支持的 BootCamp 安装双系统，也可以使用虚拟机。由于当时与主流 PC 同属 X86 架构，虚拟机工具选择也很多样，从付费的 Parallels Desktop 和 VMware Fusion，到免费的 VirtualBox、QEMU 都可堪此任。

![](https://cdn.sspai.com/2021/11/03/article/7d440f2e11715fa9b2988602093159a4?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

回到当下，BootCamp 已经被 Apple 抛弃，而虚拟机方案也因架构的鸿沟而进展迟缓。截至目前，只有新近发布的 [Parallels Desktop 17](https://www.parallels.com/cn/blogs/parallels-desktop-17-just-released/) 宣布支持 Windows 11 ARM64 版。这固然是利好消息，但不少用户可能对其较高的售价感到顾虑（每年 498 元，双十一期间[折扣](https://prf.hn/l/7R0aWV9)至 349 元；利益声明：通过前述链接购买，少数派将获得佣金）。

那么，是否有在 M1 系列 Mac 上虚拟 Windows 11 的免费方案，它们的表现是否能满足日常使用的需求呢？这就是本文要回答的问题。

**请注意：**

1.  本文适用于使用 M1、M1 Pro 或 M1 Max 芯片的 Mac 机型。对于使用 Intel 处理器的机型，一般建议直接使用免费且完善的 [VMware Fusion Player](https://customerconnect.vmware.com/web/vmware/evalcenter?p=fusion-player-personal) 即可。本文亦不介绍使用 Parallels Desktop 17 安装 Windows 11 的步骤，因为该操作有完整的[官方文档](https://kb.parallels.com/en/125375)，且属于开发商技术支持范围。
2.  本文所述运行情况及方法步骤仅适用于写作时（2021 年 11 月初）的情况，这随时间推移会发生变化，请注意检索后续进展。
3.  本文假定读者了解 macOS 下「终端」和 Windows 下 PowerShell 的基本操作，已经在 Mac 上安装了包管理工具 [Homebrew](https://brew.sh/) 并了解其基本用法。

## 准备工作：从官方渠道获取 Windows 11 ARM64

尽管微软已经推出了自家的 ARM 架构硬件产品 Surface Pro X，也为其第一时间升级了 Windows 11，却没有提供独立的 Windows 11 ARM64 版的 ISO 安装镜像供下载。诚然，网上现成的资源已经一搜可得，但我们**并不推荐下载使用这类来源不明的安装镜像**。这不仅违反许可协议，更重要的是无法保障安全。

相比之下，以变通方式从官方渠道获得安装文件是更为稳妥的选择。截至目前，具体途径主要有两种：

1.  从微软的「统一更新平台」（Unified Update Platform，UUP）下载所需文件，然后打包为 ISO 格式镜像并安装。
2.  下载微软针对 Hyper-V 虚拟化平台提供的 Windows 预览体验计划版（Windows Insider Preview）虚拟系统盘文件，然后转换为其他虚拟机软件可以读取的格式并挂载。

比较而言，两种方法不分轩轾：第一种方法比较快捷，可以省去安装的时间；后一种方法则比较通用，得到的镜像文件也可以留备后用。因此，下面依次介绍这两种方法。

### 方法一：从 UUP 文件打包 ISO 镜像

UUP [上线](https://blogs.windows.com/windows-insider/2016/11/03/introducing-unified-update-platform-uup/#tbWVyzxoZgZ75qLv.97)于 2016 年年底，可以理解为微软的「增量更新」技术，即在更新系统时根据硬件环境、与最新版本的差距等条件，只下载所需的升级文件，从而加快升级效率。换个角度看，UUP 也就为不同硬件平台提供了下载专用安装文件的渠道。

不过，UUP 并没有公开文件目录和下载渠道；而且，能从 UUP 直接获得只是增量更新文件，离我们需要的 ISO 安装镜像还有不小差距。好在，已经有人帮忙做完了功课；诸如 [UUP dump](https://uupdump.net/) 这类的第三方网站，将过滤、下载和转换的步骤简化为了向导和自动化脚本。由于这个项目是[开源](https://github.com/uup-dump/converter)的，其下载来源和安全性均较有保障。

使用 UUP dump 获取 Windows 11 安装镜像的方法是：首先，访问 UUP dump 网站（有中文翻译），从首页的「快速选项」中，点选「最新 Beta 通道版本」右侧的「arm64」按钮（因为截至目前，两个更稳定的通道尚未提供 Windows 11）。

在找到的更新中，**从上往下浏览**，选择版本号最高的、名称形如「Windows 11 Insider Preview [版本号](https://sspaime.feishu.cn/docs/co_release)」的链接点击。

![](https://cdn.sspai.com/2021/11/03/article/42e4a73d11c50d90dcbbb7c9b02495a2?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

在「选择语言」步骤，保持「中文（简体）」（或你想要使用的其他语言，如英文）；在「选择版本」步骤，勾选你希望使用的版本（建议是你拥有正版许可证的版本，方便后续激活，一般 Home 版居多）；最后在「摘要」步骤直接点击「创建下载包」即可。

解开压缩包至单独文件夹，其中的 `uup_download_macos.sh` 即为下载和生成 ISO 镜像的脚本。如其 readme 文件所述，需要先用 Homebrew 安装若干依赖才能运行：

```
brew tap sidneys/homebrew
brew install cabextract wimlib cdrtools sidneys/homebrew/chntpw
```

从终端执行 `uup_download_macos.sh`，等待进度完成（下载量约 5GB），便能在脚本统一目录下看到名称形如 `22000.1_PROFESSIONAL_ARM64_ZH-CN.ISO` 的输出文件了；这就是我们需要的安装镜像。

### 方法二：从 Hyper-V 格式虚拟盘转换

除了前述转制 ISO 的方法，还可以一步到位，使用微软直接提供的 Windows 11 ARM64 预览版虚拟机。具体而言，下载到的是一个虚拟硬盘文件，将其挂载到空白虚拟机上作为系统盘即可使用。

遗憾的是，微软提供的是针对自家 Hyper-V 虚拟化平台的格式，而 Hyper-V 并没有 macOS 版本。因此，还需要将其转换为其他虚拟机软件能读取的格式。

具体方法是：首先，访问 Windows 11 Insider Preview 的[下载页面](https://www.microsoft.com/en-us/software-download/windowsinsiderpreviewARM64?wa=wsignin1.0)。注意，该页面需要登录[加入了「预览体验计划」](https://insider.windows.com/zh-cn/register)（但无任何门槛或费用）的微软账号才能访问。点击蓝色的「Windows Client ARM64 Insider Preview - [版本号]」按钮下载虚拟机，这将得到一个名称形如 `Windows11_InsiderPreview_Client_ARM64_en-us_22483.VHDX` 的文件（约 10GB）。

然后，通过 Homebrew 安装转换格式所需的工具：

```
brew install qemu
```

接着，将上述 VHDX 格式的虚拟硬盘转换为其他虚拟机可用的格式。具体的目标格式取决于你使用的软件（见后文）；例如，如果选用 VMware，则应转换为 VMDK 格式：

```
qemu-img convert -p -f vhdx -O vmdk Windows11_InsiderPreview_Client_ARM64_en-us_22483.VHDX win11.vmdk
```

其中，`-p` 选项指显示进度条；`-f` 和 `-O` 选项分别用于指定输入和输出格式；最后两个参数分别为输入和输出的文件路径，请根据实际情况和需求调整。例如，如果选用 UTM，则应将命令中的各处 `vmdk` 替换为 `qcow2`。

## 用 VMware Fusion 安装

VMware Fusion 是老牌商业虚拟机开发商 VMware 针对 macOS 开发的虚拟机软件。该软件原为收费软件，但从 2020 年起宣布[针对非商业用途免费提供基础版](https://docs.vmware.com/en/VMware-Fusion/12/rn/VMware-Fusion-12-Release-Notes.html)，即 VMware Fusion Player。

截至目前，VMware Fusion 尚未正式支持 Apple silicon 处理器或 Windows 11 ARM64 版，但于 9 月[发布](https://blogs.vmware.com/teamfusion/2021/09/fusion-for-m1-public-tech-preview-now-available.html)了一个技术预览版（免费，但需要注册 VMware 账号）。根据 VMware 发布的[测试指南](https://communities.vmware.com/t5/Fusion-for-Apple-Silicon-Tech/Fusion-Tech-Preview-Testing-Guide/ta-p/2867908?attachment-id=105429)，Windows 10 或 11 的支持是隐藏的，需要通过手动修改参数的方法才能启用。

用 VMware Fusion 安装 Windows 11 的具体步骤是：下载安装后打开 VMware Fusion。点击左上角的加号，选择「新建」。在弹出的向导中，点击「创建自定义虚拟机」>「继续」。在「选择操作系统」步骤，可以发现软件只列举了少量 Linux 发行版，并不包含 Windows。因此，暂且选择兜底的「其他」>「其他 64 位 Arm」，然后点击「继续」。

![](https://cdn.sspai.com/2021/11/03/article/15dfcef2acdc963ba78e22a2eae46618?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

下一个「选择虚拟磁盘」步骤同样点击「继续」。在最后一步，点击「自定义设置」。为虚拟机指定一个存放位置后，会同时弹出虚拟机窗口和一个设置窗口。

这里，先进入「处理器和内存」页面，分配 2 个核心，4GB（4096MB）内存。这是微软推荐的[最小配置](https://support.microsoft.com/en-us/windows/windows-11-system-requirements-86c11283-ea52-4782-9efd-7674389a7ba3)；根据经验，足以支撑系统本身和日常的浏览、办公操作了；更低的配置也可以开机，但可用性很差。

完成这些设置后，先不要开机，回到 VMware Fusion 主窗口，在刚才创建的虚拟机名称上点击右键，选择「在 Finder 中显示」；然后，在显示出的虚拟机文件图标上再次点击右键，选择「显示包内容」，展示其内部文件。这里，找到以 vmx 结尾的配置文件，在其上点击右键，选择惯用的纯文本编辑器打开（也可以用自带的「文本编辑」）。

![](https://cdn.sspai.com/2021/11/03/article/e1cadd46a702ac593aa9fceb57ed55ef?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

找到 `guestOS` 开头的一行配置，将其改为 `guestOS = "arm-windows11-64"`，然后保存文件。

![](https://cdn.sspai.com/2021/11/03/article/7bb60181e9a0a440a8dac6bc871fe99f?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

回到虚拟机配置界面。可以看到这里相比之前多出了「默认程序」等针对 Windows 虚拟机的选项，而「鼠标和键盘」中也可以选择为 Windows 10 适配的配置了；这表明已经成功开启了 Windows 支持。

接下来的设置根据你选择的安装方式有所不同：

-   如果选择方式一，即通过 ISO 安装：进入「CD/DVD」页面，勾选「连接 CD/DVD 驱动器」，然后在下拉菜单中选择之前准备好的 ISO 格式安装镜像。然后，进入「硬盘」页面，分配 64GB 的空间（同上，为官方建议最低配置，但可以按需增减）。
-   如果选择方式二，即通过转制虚拟机文件安装：进入「硬盘」页面，点击「高级设置」，移除默认创建的硬盘。然后点击右上角的「增加设备」按钮，选择「现有硬盘」，选择之前准备好的 VMDK 格式虚拟硬盘文件。

### 绕过 Windows 11 的安装限制

Windows 11 对于硬件条件有比较特殊的要求，主要包括要求支持 TPM（可信平台模块）2.0 和安全引导（Secure Boot）等，否则会拒绝安装（相关讨论可参阅少数派此前的[指南](https://sspai.com/post/67498)）。

绕过方法也很简单。在安装界面的第一步，即显示「现在安装」（Install Now）按钮的界面，按 Shift - F10 打开命令提示符界面，然后输入 `regedit` 并回车，打开注册表编辑器。

此时，在左侧窗格定位到 `Computer\HKEY_LOCAL_MACHINE\SYSTEM\Setup` 路径，在 `Setup` 键上点击右键，选择「New」>「Key」，新建一个名为 `LabConfig` 的键。

然后，在右侧窗格空白处点击右键，选择「New」>「DWORD (32-bit) Value」，新建一个名为 `BypassTPMCheck` 的 DWORD 类型值，双击将其值改为 1。用同样的方式新建一个名为 `BypassSecureBootCheck` 的 DWORD 类型值，也将其值改为 1。

![](https://cdn.sspai.com/2021/11/03/article/965404c6bcd4dc59aa2755ec19702b96?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

关闭注册表编辑器，即可绕过限制完成安装。

### 为虚拟机启用网络

在传统虚拟机配置流程中，安装完系统后的第一步就是安装开发商提供的专用驱动和辅助程序，对于 VMware 而言，即 VMware Tools。遗憾的是，由于 VMware 尚未正式支持 Windows 11 ARM64，VMware Tools 也没有完成适配；这对正常使用最重大的障碍，就是虚拟机因为找不到网卡而不能上网。

对此，社区用户目前发现了一个吊诡但快捷的方案：以管理员权限打开 Windows Terminal 终端（可以在开始菜单搜索「Terminal」找到，在其上点击右键选择「以管理员身份运行」），然后运行如下命令：

```
bcdedit /debug on
bcdedit /dbgsettings net hostip:10.0.0.1 port:50000
```

如果你觉得上面的命令莫名其妙，那是因为……这是没有办法的办法。[`bcedit`](https://docs.microsoft.com/zh-cn/windows-hardware/drivers/devtest/bcd-boot-options-reference) 是 Windows 上用于调试启动选项的命令行工具；而上述两行命令的作用，就是首先启用内核调试器，然后添加一个专用于内核调试的以太网网络连接。是的，这么做的唯一目的就是为系统添加一个无需驱动的虚拟网卡。也正因如此，命令中的 `hostip` 和 `port` 选项的值可以任意填写，因为它们指的均是用于内核调试主机的 IP 地址和端口，这对于我们的目的并不重要。

完成设置后，重新启动虚拟机，即可正常联网。

### 使用远程桌面变通实现高清分辨率

缺乏驱动导致的另一个问题是虚拟机无法随着窗口缩放灵活适配分辨率，也不能支持 Retina 分辨率的高清显示。

不过，注意到 Windows 操作系统均可以通过 RDP 协议从远程访问，这不需要任何额外驱动的内置支持，而分辨率高低也可以自主设定；又注意到在 VMware 的默认组网方式（NAT）下，虚拟机和宿主机处于同一个虚拟局域网（`vmnet8`）中。

因此，只要把虚拟机当作一台「远程」机器，从宿主机通过远程桌面客户端连接，即可回避没有显示驱动的问题，以高清分辨率显示其界面。

为此，首先在虚拟机中启用远程桌面。方法是进入「设置」>「系统」>「远程桌面」，打开「远程桌面」选项的开关。

![](https://cdn.sspai.com/2021/11/03/article/415573019f916bd01d93ec70aecad224?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

接着，打开 Windows Terminal 终端，执行 `ipconfig` 命令，记下显示的本机 IP 地址（如下图中显示的 `192.168.162.128`）。

![](https://cdn.sspai.com/2021/11/03/article/427bec848b2e883ed7f77325a030c630?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

然后，下载安装免费的 [Microsoft Remote Desktop](https://itunes.apple.com/app/microsoft-remote-desktop/id1295203466?mt=12) 应用（当然，你也可以使用 Jump Desktop 等更好的付费软件）。打开后，点击「Add PC」按钮，在「PC name」栏填入上一步记下的 IP 地址，并在「User account」栏添加虚拟机的管理员账号。

最后，切换到「Display」选项卡，勾选「Optimize for Retina displays」和「Update the session resolution on resize」，点击「Save」。

![](https://cdn.sspai.com/2021/11/03/article/70c300691ecfb685c246442163628f9b?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

这样一来，便可以用上高清分辨率、随窗口尺寸实时缩放的虚拟机了。由于是本地传输画面，除了偶有卡顿之外，基本不会感受到延迟。如果你想进一步提高响应速度，可以考虑关闭动画、阴影和壁纸等视觉元素。

## 用 UTM 安装

[UTM](https://mac.getutm.app/) 是一个开源的虚拟机软件，以命令行虚拟机工具 [QEMU](https://www.qemu.org/) 为底层，可以说是后者的图形界面包装。UTM 最为人所知的亮相可能是在 iOS 越狱新闻中——这是目前极少见能[在 iOS 上运行](https://getutm.app/install/)的虚拟机。

而在 macOS 上，UTM 的表现同样出色。最容易发现的特征之一，就是它严格按照现代 macOS 界面规范设计，与 macOS Big Sur 后的新原生风格非常搭调，在普遍「不修边幅」的开源世界显得鹤立鸡群。

得益于在 iOS 上的积累，UTM 非常快速地实现了对 Apple silicon 的适配，去年 Windows 10 ARM 版推出后不久即可通过 UTM 在 M1 芯片 MacBook Pro 上运行。

![](https://cdn.sspai.com/2021/11/03/article/77782c80c2fa5c6795a4fda897397f86?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

具体到用法上，UTM 的使用方式与 VMware 大同小异，且官方文档已经更新了[安装 Windows 11 的步骤](https://mac.getutm.app/gallery/windows-11-arm)，参照前文 VMware 的步骤和该文档提示操作即可。这里，仅对个人尝试后发现的常见问题作出提示。

### 关于安装方式

官方文档演示的是本文分类下的方法二，即通过导入虚拟硬盘安装，并且没有转换格式。但正如文档尾部所述，UTM 对 VHDX 格式的支持并不完善，容易发生蓝屏、应用闪退等问题。

因此，仍然建议按照前文所述方法，将下载到的文件转换为原生的 QCOW2 格式再导入。

此外，使用 ISO 镜像安装的方案在 UTM 上仍然是可行的，但同样需要修改注册表来绕过 TPM 和 Secure Boot 这两项安装条件（方法见上文）。

同时，由于 UTM 对 USB 总线的模拟[存在缺陷](https://github.com/utmapp/UTM/issues/3194)，安装过程中有一定机率会出现类似于「掉盘」的问题，即无法继续从 ISO 镜像读取数据。截至目前，社区没有发现能完全避免的方式，如果遇到从头安装即可，一般不会连续「中奖」。

### 关于网络和显示驱动

与 VMware 的情况相同，由于对 Apple silicon 的适配处于早期阶段，相关驱动的开发也没有充分跟上。

比 VMware 稍好一点的是，这边使用的驱动和辅助工具 [SPICE Guest Tools](https://mac.getutm.app/support/)（ISO 格式，下载后挂载到虚拟机的光驱安装）至少实现了网卡支持，不需要通过命令行魔改一个网卡出来。

但是，显示驱动则同样很不完善，不仅无法支持高分辨率，而且还会随机发生[鼠标指针突然蒸发](https://github.com/utmapp/UTM/issues/3188)的问题。对此，建议同样是使用上文介绍的远程桌面方式，绕过这个问题。

## 性能比较及选择建议

经过上述设置步骤后，通过 VMware Fusion 和 UTM 安装的 Windows 11 均可以正常联网，运行也比较流畅。根据测试，浏览器、Office 等常见应用的运行也没有问题。

至于性能，我做了一个不严谨的测试。在一台配备 M1 Max 处理器的 16 寸 MacBook Pro 上，使用前文所述的配置（双核、4GB 内存）通过 ISO 镜像全新安装，GeekBench 5 的运行成绩如下表所示：

**虚拟机\评分项**

**单核**

**多核**

VMware Fusion

1392

2485

UTM

1307

2242

Parallels Desktop

1522

2833

可见，VMware Fusion 的纸面性能稍强于 UTM，两者均不及 Parallels Desktop，但差距不大；实际使用中的感受也大体如此。

因此，**如果要求不高，只是偶尔有使用 Windows 的需求，建议选用 VMware Fusion 即可。**不仅免费，因为有商业公司支撑，后续的适配可能也比开源项目更及时和完善。

另一方面，**如果你的日常工作对 Windows 环境依赖较多，那么付费但有官方支持的 Parallels Desktop 可能还是更好的选择。**多花的成本一方面可以获得更简单顺畅的安装流程，也可以获得融合模式（即直接让 Windows 应用的窗口显示在 Mac 桌面上）等改善使用体验的进阶功能。相比之下，VMware 的免费正式版虽然值得期待，但官方目前仍然没有就时间表给出准信，因此并不值得特地等待。