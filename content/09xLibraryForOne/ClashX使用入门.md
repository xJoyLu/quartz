author:: 本文作者： Kerronex
source:: [ClashX使用入门](https://bfchengnuo.com/2021/06/23/ClashX%E4%BD%BF%E7%94%A8%E5%85%A5%E9%97%A8/)
clipped:: [[2022-09-30]]
published:: 

发表于 2021-06-23 | 分类于 [其他](https://bfchengnuo.com/categories/%E5%85%B6%E4%BB%96/) | 热度2158 | 字数统计 6,317

提醒：本文发布于 463 天前，文中所描述的信息可能已发生改变，请谨慎使用。

起因还要从去年还是前年的那次大规模封杀说起，因为种种原因 SS 原作者早已弃坑，SSR 作者也是如此，以现在的防火墙技术识别 SS 的流量特征应该不难，每次都是大规模的『关机保平安』；  
我买的机场也开始提供 SS + V2ray 的方式，并且建议优先使用 V2ray，我也就顺势切换了，接下来遇到的一个问题就是 SS 客户端不支持，需要找一个替代的，最好多种协议都支持，一轮调研下来，Clash 脱颖而出（当时起码是 Star 最高的），于是就开始使用 ClashX。

不像其他的客户端，可以有完整的 GUI 配置，ClashX 比较传统的使用配置文件方式，说起配置文件，V2ray 本身就以复杂的配置著称，不过换来的是高稳定性与强大的功能。  
起初我只是找了份模版，然后简单加上节点信息，这样跟之前的 SS 没太大区别，用了好长时间。  
后来，闲得无聊，搜了下配置文件相关的信息，发现可配置的东西是真的多，功能也是真牛逼，我也没完全掌握，以后用到相关的功能再更新吧。

## [](#版本选择 "版本选择")版本选择

Clash 有两个版本，普通版和 Pro 版，对应到 Mac 平台就是 ClashX 和 ClashX Pro，倒不是说 Pro 收费，是 Pro 支持更多的功能，如 TUN、代理集、规则集、脚本等，但是不开源，但是还是建议使用 Pro 版本，获得更好的体验（例如通过 TUN 可接管设备的所有 TCP 和 UDP 流量，可以做软路由等等）。

## [](#基本配置 "基本配置")基本配置

首先说明，因为我的机场不提供订阅服务，虽然可以进行转换，但我还是更愿意使用传统的手动增加节点方式，订阅相关的规则暂时略过。

ClashX 主文件 Config.yaml 内容：

1  
2  
3  
4  
5  
6  
7  
8  
9  
10  
11  
12  
13  
14  
15  
16  
17  
18  
19  
20  
21  
22  
23  
24  
25  

#---------------------------------------------------#  
\## 配置文件需要放置在 $HOME/.config/clash/\*.yaml  
  
\## 这份文件是clashX的基础配置文件，请尽量新建配置文件进行修改。  
\## ！！！只有这份文件的端口设置会随ClashX启动生效  
#---------------------------------------------------#  
  
port: 1090  
socks-port: 1080  
allow-lan: false  
mode: Rule  
log-level: info  
external-controller: 127.0.0.1:9090  
  
Proxy:  
  
Proxy Group:  
  
Rule:  
\- DOMAIN-SUFFIX,google.com,DIRECT  
\- DOMAIN-KEYWORD,google,DIRECT  
\- DOMAIN,google.com,DIRECT  
\- DOMAIN-SUFFIX,ad.com,REJECT  
\- GEOIP,CN,DIRECT  
\- MATCH,DIRECT  

这些都是最基本的端口与规则模式信息，一般情况都是会另新建一个配置文件来配置详细的规则和节点。

## [](#DNS "DNS")DNS

这部分的功能非常实用，虽然最开始我完全看不懂，也不知道什么意思，在这里的配置也让我踩坑了好几次，首先来看一个示例配置（Pro 版）：

1  
2  
3  
4  
5  
6  
7  
8  
9  
10  
11  
12  
13  
14  
15  
16  
17  
18  
19  
20  
21  
22  
23  
24  
25  
26  
27  
28  
29  
30  
31  
32  
33  
34  
35  
36  
37  
38  
39  
40  
41  
42  
43  
44  
45  
46  
47  
48  
49  
50  
51  
52  
53  
54  
55  
56  
57  
58  
59  
60  
61  
62  
63  
64  
65  
66  
67  
68  
69  
70  
71  
72  
73  
74  
75  
76  
77  
78  
79  
80  
81  
82  
83  
84  
85  
86  
87  
88  
89  
90  
91  
92  
93  
94  
95  
96  
97  
98  
99  
100  
101  
102  
103  
104  
105  
106  
107  
108  
109  
110  
111  
112  
113  
114  
115  
116  
117  
118  
119  
120  
121  
122  
123  
124  
125  
126  
127  
128  
129  
130  
131  
132  
133  
134  
135  
136  
137  
138  
139  
140  

\# DNS 服务器配置(可选；若不配置，程序内置的 DNS 服务会被关闭)  
dns:  
 enable: true  
 listen: 0.0.0.0:53  
 ipv6: true \# 当此选项为 false 时, AAAA 请求将返回空  
  
 \# 以下填写的 DNS 服务器将会被用来解析 DNS 服务的域名  
 \# 仅填写 DNS 服务器的 IP 地址  
 default-nameserver:  
 - 223.5.5.5  
 - 114.114.114.114  
 enhanced-mode: fake-ip \# 或 redir-host  
 fake-ip-range: 198.18.0.1/16 \# Fake IP 地址池 (CIDR 形式)  
 \# use-hosts: true # 查询 hosts 并返回 IP 记录  
  
 \# 在以下列表的域名将不会被解析为 fake ip，这些域名相关的解析请求将会返回它们真实的 IP 地址  
 fake-ip-filter:  
 \# 以下域名列表参考自 vernesong/OpenClash 项目，并由 Hackl0us 整理补充  
 \# === LAN ===  
 - '\*.lan'  
 \# === Linksys Wireless Router ===  
 - '\*.linksys.com'  
 - '\*.linksyssmartwifi.com'  
 \# === Apple Software Update Service ===  
 - 'swscan.apple.com'  
 - 'mesu.apple.com'  
 \# === Windows 10 Connnect Detection ===  
 - '\*.msftconnecttest.com'  
 - '\*.msftncsi.com'  
 \# === NTP Service ===  
 - 'time.\*.com'  
 - 'time.\*.gov'  
 - 'time.\*.edu.cn'  
 - 'time.\*.apple.com'  
  
 - 'time1.\*.com'  
 - 'time2.\*.com'  
 - 'time3.\*.com'  
 - 'time4.\*.com'  
 - 'time5.\*.com'  
 - 'time6.\*.com'  
 - 'time7.\*.com'  
  
 - 'ntp.\*.com'  
 - 'ntp.\*.com'  
 - 'ntp1.\*.com'  
 - 'ntp2.\*.com'  
 - 'ntp3.\*.com'  
 - 'ntp4.\*.com'  
 - 'ntp5.\*.com'  
 - 'ntp6.\*.com'  
 - 'ntp7.\*.com'  
  
 - '\*.time.edu.cn'  
 - '\*.ntp.org.cn'  
 - '+.pool.ntp.org'  
  
 - 'time1.cloud.tencent.com'  
 \# === Music Service ===  
 \## NetEase  
 - '+.music.163.com'  
 - '\*.126.net'  
 \## Baidu  
 - 'musicapi.taihe.com'  
 - 'music.taihe.com'  
 \## Kugou  
 - 'songsearch.kugou.com'  
 - 'trackercdn.kugou.com'  
 \## Kuwo  
 - '\*.kuwo.cn'  
 \## JOOX  
 - 'api-jooxtt.sanook.com'  
 - 'api.joox.com'  
 - 'joox.com'  
 \## QQ  
 - '+.y.qq.com'  
 - '+.music.tc.qq.com'  
 - 'aqqmusic.tc.qq.com'  
 - '+.stream.qqmusic.qq.com'  
 \## Xiami  
 - '\*.xiami.com'  
 \## Migu  
 - '+.music.migu.cn'  
 \# === Game Service ===  
 \## Nintendo Switch  
 - '+.srv.nintendo.net'  
 \## Sony PlayStation  
 - '+.stun.playstation.net'  
 \## Microsoft Xbox  
 - 'xbox.\*.microsoft.com'  
 - '+.xboxlive.com'  
 \# === Other ===  
 \## QQ Quick Login  
 - 'localhost.ptlogin2.qq.com'  
 \## Golang  
 - 'proxy.golang.org'  
 \## STUN Server  
 - 'stun.\*.\*'  
 - 'stun.\*.\*.\*'  
  
 \# 支持 UDP / TCP / DoT / DoH 协议的 DNS 服务，可以指明具体的连接端口号。  
 \# 所有 DNS 请求将会直接发送到服务器，不经过任何代理。  
 \# Clash 会使用最先获得的解析记录回复 DNS 请求  
 nameserver:  
 - https://doh.pub/dns-query  
 - https://dns.alidns.com/dns-query  
   
 \# 当 fallback 参数被配置时, DNS 请求将同时发送至上方 nameserver 列表和下方 fallback 列表中配置的所有 DNS 服务器.  
 \# 当解析得到的 IP 地址的地理位置不是 CN 时，clash 将会选用 fallback 中 DNS 服务器的解析结果。  
 \# fallback:  
 \#   - https://dns.google/dns-query  
  
 \# 如果使用 nameserver 列表中的服务器解析的 IP 地址在下方列表中的子网中，则它们被认为是无效的，  
 \# Clash 会选用 fallback 列表中配置 DNS 服务器解析得到的结果。  
 #  
 \# 当 fallback-filter.geoip 为 true 且 IP 地址的地理位置为 CN 时，  
 \# Clash 会选用 nameserver 列表中配置 DNS 服务器解析得到的结果。  
 #  
 \# 当 fallback-filter.geoip 为 false, 如果解析结果不在 fallback-filter.ipcidr 范围内，  
 \# Clash 总会选用 nameserver 列表中配置 DNS 服务器解析得到的结果。  
 #  
 \# 采取以上逻辑进行域名解析是为了对抗 DNS 投毒攻击。  
 fallback-filter:  
 geoip: false  
 ipcidr:  
 - 240.0.0.0/4  
 - 0.0.0.0/32  
 \# domain:  
 \#   - '+.google.com'  
 \#   - '+.facebook.com'  
 \#   - '+.youtube.com'  
  
tun:  
 enable: true #如果需要启用 TUN 模式，请设置为 true  
 stack: system \# 或 gvisor  
 macOS-auto-route: true  
 macOS-auto-detect-interface: true  
 dns-hijack:  
 - tcp://8.8.8.8:53  
 - tcp://8.8.4.4:53  

clash DNS 请求逻辑：

1.  当访问一个域名时，nameserver 与 fallback 列表内的所有服务器并发请求，得到域名对应的 IP 地址。
2.  clash 将选取 nameserver 列表内，解析最快的结果。
3.  若解析结果中，IP 地址属于国外，那么 clash 将选择 fallback 列表内，解析最快的结果。

因此，在 nameserver 和 fallback 内都放置无污染、解析速度较快的国内 DNS 服务器，以达到最快的解析速度。  
但是 fallback 列表内服务器会用在解析境外网站，为了结果绝对无污染，尽量使用支持 DoT/DoH 的服务器。

DNS 配置注意事项：

1.  如果您为了确保 DNS 解析结果无污染，请仅保留列表内以 tls:// 或 https:// 开头的 DNS 服务器，但是通常对于国内域名没有必要。
2.  如果您不在乎可能解析到污染的结果，更加追求速度。请将 nameserver 列表的服务器插入至 fallback 列表内，并移除重复项。

关于 DNS over HTTPS (DoH) 和 DNS over TLS (DoT) 的选择：  
对于两项技术双方各执一词，而且会无休止的争论，各有利弊。各位请根据具体需求自行选择，但是配置文件内默认启用 DoT，因为目前国内没有封锁或管制。  
**DoH:** 以 https:// 开头的 DNS 服务器。拥有更好的伪装性，且几乎不可能被运营商或网络管理封锁，但查询效率和安全性可能略低。  
**DoT:** 以 tls:// 开头的 DNS 服务器。拥有更高的安全性和查询效率，但端口有可能被管制或封锁。

> 这里有个坑，或许是我网络的问题，fallback 中的地址我全部连不上，这就导致一个很严重的后果，国外的网站全部无法命中，甚至 AppStore 都挂了。。。  
> 后面通过调整日志等级到 DEBUG 才知道是 DNS 解析的问题。  
> 除非你所在的地区 DNS 污染特别严重，否则非常不建议使用 fallback，拖慢速度还不稳定，一般情况 fake-Ip 足够了。

### [](#fake-ip "fake-ip")fake-ip

下面补充说明下这个 fake-ip 是什么东西；

> 虽然 Fake IP 这个概念早在 2001 年就被提出来了，但是到 Clash 提供 fake-ip 增强模式以后，依然有很多人对 Fake IP 这个概念以及其作用知之甚少。
> 
> 参考：[https://blog.skk.moe/post/what-happend-to-dns-in-proxy/](https://blog.skk.moe/post/what-happend-to-dns-in-proxy/)

当 TCP 连接建立时，Clash DNS 会直接返回一个保留地址的 IP（即 Fake IP；Clash 默认使用 198.18.0.0/16），同时 Clash 继续解析域名规则和 IP 规则。  
PS：开启增强模式后可以尝试 nslookup 看一下解析情况。

由于 TCP/IP 的协议特性，在应用发起 TCP 连接时，会先发出一个 DNS question（发一个 IP Packet），获取要连接的服务器的 IP 地址，然后直接向这个 IP 地址发起连接。  
在不使用代理的情况下，DNS 查询流程想必大家很熟悉了，如果使用了代理，直连模式下以使用 SOCKS5 代理的浏览器为例：

1.  浏览器不再需要从自己的 DNS 缓存中寻找域名对应的 ip，因为已经有了 SOCKS5 代理，浏览器可以直接将域名封装在 SOCKS5 流量之中发往代理客户端（clash）
2.  代理客户端从 SOCKS5 流量中抽出域名并设法获得解析结果
3.  代理客户端将你的 SOCKS5 流量还原成标准的 TCP 请求
4.  代理客户端将这个 TCP 连接建立起来，TCP 连接可以承载的是 HTTPS

传统上，大部分浏览器等应用都会调用系统的内置方法去解析域名，这时候如果你想做一些魔法操作，那么就是在系统这一层上，你可以在本地或者其他地方搭建一个黑魔法 DNS 服务器，然后设置系统的 DNS 为它，就可以实现一些黑魔法效果。

例如，在上面的 2 和 3 之间，可以插入一步：代理客户端使用 **某种协议** 将浏览器发出的 SOCKS5 的流量重组并发给远端服务器；  
远端服务器使用相同的协议还原，然后拿到域名，进行解析；这样就实现了域名在远端进行解析。  
这种就是非直连的方式代理，各有优劣，各自体会。

---

然后再说说分流；分流是一个麻烦事。一般情况下，你可能会需要使用域名进行分流（不论是白名单还是黑名单）。不过更多情况下你会使用到基于 IP 的规则来进行分流。  
这里可以通过 GUI 的界面来观察连接，如果 TUN 显示一个域名使用了大量端口占用了大量的 ip 池资源，可以考虑将它放到 fake-ip-filter 中不使用 fake-ip。

在域名规则下，如果判断是直连，那么代理客户端没必要进行 DNS 解析，交给原本的流程使用系统接口即可。  
在 ip 规则下，当然需要先解析域名，然后匹配规则，但是由于某种协议可以封装域名，因此最终还是会讲域名发给远端，也就是你本地匹配规则的 ip 与最终代理请求的 ip 可能并不是一个。

### [](#全局流量代理 "全局流量代理")全局流量代理

全局流量代理可能会出现在路由器上或者 TUN/TAP 型的支持全局代理客户端上。用户不再主动为每个应用程序设置代理。**此时应用程序是不会感知到代理客户端的存在，它们会正常的发起 TCP 连接**，并且由于 TCP/IP 协议，在拿到 DNS 解析结果之前，连接是不能建立的。

这时候配合上面说的 DNS 解析过程就比较有趣了，前半部分不变，最终会调用系统接口进行解析域名，这时候会向系统配置的 DNS 服务器发起请求；  
如果我们在系统的网络设置之中有设置上游 DNS 地址，例如代理客户端可能会修改系统设置中的 DNS 到 127.0.0.1 或者别的 IP、也可能保留用户之前的设置，这无所谓，因为… **操作系统发出的 DNS 解析请求会经过代理客户端并最终被截获**；  
代理客户端可以将这个解析请求原样发出去、或者用自己的黑魔法，总之都会拿到一个解析结果；  
代理客户端将这个解析结果返回回去，操作系统拿到了这个解析结果并返回给浏览器 浏览器对这个解析结果的 IP 建立一个 TCP 连接并发送出去，**这个 TCP 连接被代理客户端截获**。  
由于之前代理客户端进行的 DNS 解析请求这一动作，代理客户端可以找到这个只包含目标 IP 的 TCP 连接原来的目标域名；  
如果是支持 redir 的代理客户端，那么代理客户端就会直接将域名和 TCP 连接中的其它数据封装成 **某种协议** 发给远端服务器；或者封装成 SOCKS5 后交给支持 SOCKS5 的代理客户端。

和应用程序直接将流量封装成 SOCKS5 大有不同，在类似于透明代理的环境下浏览器和其它应用程序是正常地发起 TCP 连接。因此除非得到一个 DNS 解析结果，否则 TCP 连接不会建立；代理客户端也会需要通过这个 DNS 查询动作，才能找到之后的 TCP 连接的域名。  
你大概能够发现，浏览器、应用程序直接设置 SOCKS5 代理的话，可以不在代理客户端发起 DNS 解析请求就能将流量发送给远端服务器；  
而**在透明代理模式下，不论是否需要 IP 规则分流都需要先进行一次 DNS 解析才能建立连接**。 有没有办法能像直接设置 SOCKS5 代理一样省掉一次 DNS 解析呢？  
有，就是代理客户端自己不先执行查询动作，丢一个 Fake IP 回去让浏览器、应用程序立刻建立 TCP 连接。

有了 Fake IP，代理客户端无需进行 DNS 解析。最后不论是浏览器、代理客户端还是远端服务器都不会去和 Fake IP 进行连接，因为在代理客户端这里就已经完成了截获、重新封装。  
即使按照域名规则分流，代理客户端都没有进行 DNS 解析的需要。只有在遇到了按照 IP 进行分流的规则时，代理客户端才需要进行一次解析拿到一个 IP 用于判断。即便如此，这个 IP 只用于分流规则的匹配，不会被用于实际的连接。

PS：Clash 的增强模式既有 redir-host 也有 Fake IP。

---

这里有个很有意思的问题，如果操作系统或者浏览器缓存了 Fake IP，但是代理客户端中 Fake IP 和域名的映射表丢失以后，会出现什么状况？可能会出现什么错误信息？  
你应该大概意识到 Clash 在 Fake IP 模式下偶发的无法上网的原因了。

在使用 Fake-ip 模式后，Application 拿到的是 Clash DNS 返回的 Fake IP，所以也不会出现某些应用程序拒绝连接一些 IP 的情况；和 redir-host 模式一样，在大部分情况下 fake-ip 模式下也可以完全无视 DNS 污染。

## [](#节点 "节点")节点

这部分可参考 SS-Rule，写的很好，或者可以看看官方推荐的[文档](https://lancellc.gitbook.io/clash/clash-config-file/proxies/config-a-vmess-proxy)或者 wiki，我因为没有订阅连接，只能自己手动配置，下面是我用到的几个：  
需要注意的是，在 [v1.9](https://github.com/Dreamacro/clash/releases/tag/v1.9.0) 版本后，作者调整了配置的格式（改动很小），下面使用的是最新的个数，详情可以看官方的说明。

1  
2  
3  
4  
5  
6  
7  
8  
9  
10  
11  
12  
13  
14  
15  
16  
17  
18  
19  
20  
21  
22  
23  
24  
25  
26  
27  
28  
29  
30  
31  
32  
33  
34  
35  
36  
37  
38  
39  
40  
41  
42  
43  
44  
45  
46  
47  
48  
49  
50  
51  
52  
53  
54  
55  
56  
57  
58  
59  
60  
61  
62  
63  
64  
65  
66  
67  
68  
69  
70  
71  
72  
73  
74  
75  
76  
77  
78  
79  
80  
81  
82  
83  
84  
85  
86  
87  
88  
89  
90  
91  
92  
93  
94  
95  
96  
97  
98  
99  
100  
101  
102  
103  
104  
105  
106  
107  
108  
109  
110  
111  
112  
113  
114  
115  
116  
117  
118  
119  
120  
121  
122  
123  
124  
125  
126  
127  
128  
129  
130  
131  
132  

proxies:  
 \# shadowsocks  
 \# 支持加密方式：  
 \#   aes-128-gcm aes-192-gcm aes-256-gcm  
 \#   aes-128-cfb aes-192-cfb aes-256-cfb  
 \#   aes-128-ctr aes-192-ctr aes-256-ctr  
 \#   rc4-md5 chacha20 chacha20-ietf xchacha20  
 \#   chacha20-ietf-poly1305 xchacha20-ietf-poly1305  
  
 - name: "ss1"  
 type: ss  
 server: server  
 port: 443  
 cipher: chacha20-ietf-poly1305  
 password: "password"  
 \# udp: true  
  
 \# vmess  
 \# 支持加密方式：auto / aes-128-gcm / chacha20-poly1305 / none  
 - name: "vmess"  
 type: vmess  
 server: server  
 port: 443  
 uuid: uuid  
 alterId: 32  
 cipher: auto  
 \# udp: true  
 \# tls: true  
 \# skip-cert-verify: true  
 \# servername: example.com # 优先级高于 wss host  
 \# network: ws  
 \# ws-opts:  
 \#   path: /path  
 \#   headers:  
 \#     Host: v2ray.com  
 \#   max-early-data: 2048  
 \#   early-data-header-name: Sec-WebSocket-Protocol  
   
 - name: "vmess-http"  
 type: vmess  
 server: server  
 port: 443  
 uuid: uuid  
 alterId: 32  
 cipher: auto  
 \# udp: true  
 \# network: http  
 \# http-opts:  
 \#   # method: "GET"  
 \#   # path:  
 \#   #   - '/'  
 \#   #   - '/video'  
 \#   # headers:  
 \#   #   Connection:  
 \#   #     - keep-alive  
   
 - name: vmess-grpc  
 server: server  
 port: 443  
 type: vmess  
 uuid: uuid  
 alterId: 32  
 cipher: auto  
 network: grpc  
 tls: true  
 servername: example.com  
 \# skip-cert-verify: true  
 grpc-opts:  
 grpc-service-name: "example"  
  
 \# socks5  
 - name: "socks"  
 type: socks5  
 server: server  
 port: 443  
 \# username: username  
 \# password: password  
 \# tls: true  
 \# skip-cert-verify: true  
 \# udp: true  
  
 \# http  
 - name: "http"  
 type: http  
 server: server  
 port: 443  
 \# username: username  
 \# password: password  
 \# tls: true # https  
 \# skip-cert-verify: true  
   
 \# Trojan  
 - name: "trojan"  
 type: trojan  
 server: server  
 port: 443  \- name: "trojan"  
 type: trojan  
 server: server  
 port: 443  
 password: yourpsk  
 \# udp: true  
 \# sni: example.com # aka server name  
 \# alpn:  
 \#   - h2  
 \#   - http/1.1  
 \# skip-cert-verify: true  
   
 - name: trojan-grpc  
 server: server  
 port: 443  
 type: trojan  
 password: "example"  
 network: grpc  
 sni: example.com  
 \# skip-cert-verify: true  
 udp: true  
 grpc-opts:  
 grpc-service-name: "example"  
  
 - name: trojan-ws  
 server: server  
 port: 443  
 type: trojan  
 password: "example"  
 network: ws  
 sni: example.com  
 \# skip-cert-verify: true  
 udp: true  
 \# ws-opts:  
 \# path: /path  
 \# headers:  
 \#   Host: example.com  

我用的是原版 SS，SSR 上面没贴，如果需要支持 UDP，需要手动开启；Trojan 也支持，听说很牛逼，vmess 如果效果还是不理想可以切换试试看，我暂时还没用过。  
我主力就是 vmess，订阅模式使用 proxy-providers 来定义，体验应该最好（大概），使用的时候通过 use 关键字。

1  
2  
3  
4  
5  
6  
7  
8  
9  
10  
11  
12  
13  
14  
15  
16  
17  
18  
19  
20  
21  
22  
23  
24  
25  

proxy-groups:  
 - name: Proxy  
 type: url-test  
 use:  
 - provider1  
  
proxy-providers:  
 provider1:  
 type: http  
 \# 使用 url 在线订阅  
 url: "url"  
 interval: 3600  
 path: ./provider1.yaml  
 health-check:  
 enable: true  
 interval: 600  
 url: http://www.gstatic.com/generate\_204  
 test:  
 type: file  
 \# 从文件中读取  
 path: /test.yaml  
 health-check:  
 enable: true  
 interval: 36000  
 url: http://www.gstatic.com/generate\_204  

使用 proxy-providers 省去了我们自己维护 proxy 节点，直接从在线或者本地文件读取 proxy 节点信息，其他规则还是我们自己定义，顺便提一嘴，如果你没机场只是偶尔临时用，可以看看 [proxypool](https://github.com/zu1k/proxypool) 这个项目，从互联网爬取免费的节点，还有好心人提供了 proxy-providers 的在线地址，可以临时顶一顶，不过毕竟免费风险还是有的，这个自己取舍。

订阅模式需要注意的是拉取的不一定只有节点，包括代理组、规则集可能都有，这样就可能面临一个问题，你自定义的一些规则等配置在下一次更新订阅后可能会丢失，这个自测吧，如果真的被重置，可以尝试使用 Parser 规则解决。  
如果你的机场不提供 clash 订阅连接，可以使用在线服务进行转换，这个一搜一大堆不多说。

## [](#代理组 "代理组")代理组

这部分也很重要，配合上门的节点分组，避免一个节点挂掉还得手动换，选择最佳的节点连接。

1  
2  
3  
4  
5  
6  
7  
8  
9  
10  
11  
12  
13  
14  
15  
16  
17  
18  
19  
20  
21  
22  
23  
24  
25  
26  
27  
28  
29  
30  
31  
32  
33  
34  
35  
36  
37  
38  
39  
40  
41  
42  
43  
44  
45  
46  
47  
48  
49  
50  

proxy-groups:  
 \# 代理的转发链, 在 proxies 中不应该包含 relay. 不支持 UDP.  
 \# 流量: clash <-> http <-> vmess <-> ss1 <-> ss2 <-> 互联网  
 - name: "relay"  
 type: relay  
 proxies:  
 - http  
 - vmess  
 - ss1  
 - ss2  
  
 \# url-test 可以自动选择与指定 URL 测速后，延迟最短的服务器  
 - name: "auto"  
 type: url-test  
 proxies:  
 - ss1  
 - ss2  
 - vmess1  
 url: 'http://www.gstatic.com/generate\_204'  
 interval: 300  
  
 \# fallback 可以尽量按照用户书写的服务器顺序，在确保服务器可用的情况下，自动选择服务器  
 - name: "fallback-auto"  
 type: fallback  
 proxies:  
 - ss1  
 - ss2  
 - vmess1  
 url: 'http://www.gstatic.com/generate\_204'  
 interval: 300  
  
 \# load-balance 可以使相同 eTLD 请求在同一条代理线路上  
 - name: "load-balance"  
 type: load-balance  
 proxies:  
 - ss1  
 - ss2  
 - vmess1  
 url: 'http://www.gstatic.com/generate\_204'  
 interval: 300  
  
 \# select 用来允许用户手动选择 代理服务器 或 服务器组  
 \# 您也可以使用 RESTful API 去切换服务器，这种方式推荐在 GUI 中使用  
 - name: Proxy  
 type: select  
 proxies:  
 - ss1  
 - ss2  
 - vmess1  
 - auto  

这里注意 Proxy 这个关键组，GUI 默认使用这个（其实是后面的规则配的是这个），它的类型是 select 可以允许我们在 GUI 中手动选择一个节点或者组，默认我使用 auto，也就是 url-test 模式的。

## [](#规则集 "规则集")规则集

这个功能只有 Pro 版本才支持，普通版只有规则；简单说就是一组规则的集合，只不过可以在线获取，定时更新，也就是可以直接用别人写好的分流规则，非常爽啊：

1  
2  
3  
4  
5  
6  
7  
8  
9  
10  
11  
12  
13  
14  
15  
16  
17  
18  
19  
20  
21  
22  
23  
24  
25  
26  
27  
28  
29  
30  
31  
32  
33  
34  
35  
36  
37  
38  
39  
40  
41  
42  
43  
44  
45  
46  
47  
48  
49  
50  
51  
52  
53  
54  
55  
56  
57  
58  
59  
60  
61  
62  
63  
64  
65  
66  
67  
68  
69  
70  
71  
72  

rule-providers:  
 apple-proxy:  
 type: http  
 behavior: classical  
 url: "https://cdn.jsdelivr.net/gh/Hackl0us/SS-Rule-Snippet@master/Rulesets/Clash/Basic/Apple-proxy.yaml"  
 path: ./ruleset/Apple-proxy.yaml  
 interval: 3600  
  
 apple-direct:  
 type: http  
 behavior: classical  
 url: "https://cdn.jsdelivr.net/gh/Hackl0us/SS-Rule-Snippet@master/Rulesets/Clash/Basic/Apple-direct.yaml"  
 path: ./ruleset/Apple-direct.yaml  
 interval: 3600  
  
 icloud:  
 type: http  
 behavior: domain  
 url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/icloud.txt"  
 path: ./ruleset/icloud.yaml  
 interval: 86400  
  
 apple:  
 type: http  
 behavior: domain  
 url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/apple.txt"  
 path: ./ruleset/apple.yaml  
 interval: 86400  
  
 private:  
 type: http  
 behavior: domain  
 url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/private.txt"  
 path: ./ruleset/private.yaml  
 interval: 86400  
  
 cn:  
 type: http  
 behavior: classical  
 url: "https://cdn.jsdelivr.net/gh/Hackl0us/SS-Rule-Snippet@master/Rulesets/Clash/Basic/CN.yaml"  
 path: ./ruleset/CN.yaml  
 interval: 3600  
  
 ad-keyword:  
 type: http  
 behavior: classical  
 url: "https://cdn.jsdelivr.net/gh/Hackl0us/SS-Rule-Snippet@master/Rulesets/Clash/Basic/common-ad-keyword.yaml"  
 path: ./ruleset/common-ad-keyword.yaml  
 interval: 3600  
  
 foreign:  
 type: http  
 behavior: classical  
 url: "https://cdn.jsdelivr.net/gh/Hackl0us/SS-Rule-Snippet@master/Rulesets/Clash/Basic/foreign.yaml"  
 path: ./ruleset/foreign.yaml  
 interval: 3600  
  
 telegram:  
 type: http  
 behavior: classical  
 url: "https://cdn.jsdelivr.net/gh/Hackl0us/SS-Rule-Snippet@master/Rulesets/Clash/App/social/Telegram.yaml"  
 path: ./ruleset/Telegram.yaml  
 interval: 3600  
  
 lan:  
 type: http  
 behavior: classical  
 url: "https://cdn.jsdelivr.net/gh/Hackl0us/SS-Rule-Snippet@master/Rulesets/Clash/Basic/LAN.yaml"  
 path: ./ruleset/LAN.yaml  
 interval: 3600  
  
 microsoft: {type: http, behavior: classical, path: ./Filter/Microsoft, url: https://cdn.jsdelivr.net/gh/Semporia/Clash-X@master/Filter/Microsoft.yaml, interval: 3600}  

然后配置下最终规则，整个配置就算完成了：

1  
2  
3  
4  
5  
6  
7  
8  
9  
10  
11  
12  
13  
14  
15  
16  
17  
18  

rules:  
 - RULE-SET,private,DIRECT  
 - RULE-SET,icloud,DIRECT  
 - RULE-SET,apple,DIRECT  
 - RULE-SET,microsoft,DIRECT  
 - DOMAIN,clash.razord.top,DIRECT  
 - DOMAIN,yacd.haishan.me,DIRECT  
 - RULE-SET,apple-proxy,Proxy  
 - RULE-SET,apple-direct,DIRECT  
 - RULE-SET,cn,DIRECT  
 - RULE-SET,ad-keyword,REJECT  
 - RULE-SET,foreign,Proxy  
 - RULE-SET,telegram,Proxy  
 - RULE-SET,lan,DIRECT  
 - GEOIP,CN,DIRECT  
 - MATCH,Proxy  
  
\# - RULE-SET,apple,DIRECT,no-resolve  

这里说下 Clash 支持的几种规则；

-   DOMAIN-SUFFIX：域名后缀匹配
-   DOMAIN：域名匹配
-   DOMAIN-KEYWORD：域名关键字匹配
-   IP-CIDR：IP段匹配
-   SRC-IP-CIDR：源IP段匹配
-   GEOIP：GEOIP 数据库（国家代码）匹配
-   DST-PORT：目标端口匹配
-   SRC-PORT：源端口匹配
-   PROCESS-NAME：源进程名匹配
-   RULE-SET：Rule Provider 规则匹配
-   MATCH：全匹配

写法上面已经有示例了，特别的情况，如果你不想让 Clash 进行 DNS 解析，可以在后面加上 no-resolve。  
自带的两种规则是 REJECT 和 DIRECT，很好理解，广告相关的一般直接使用 REJECT，不需要代理的就使用 DIRECT，剩下的就需要指定我们配的代理组，例如本例的 Proxy。  
`MATCH`需要位于规则列表末尾，除了那些漏网之鱼。

## [](#脚本 "脚本")脚本

同样，这也是 Pro 的专有功能，除了全局、直连、规则，还增加了一个更灵活的脚本模式，来应对日益增多的 Rule 规则。但是目前用的人很少，我也没这个需求，暂不关注。

## [](#参考规则 "参考规则")参考规则

这里推荐几个开箱即用的规则：

[Profiles](https://github.com/DivineEngine/Profiles)  
[clash-rules](https://github.com/Loyalsoldier/clash-rules)  
[SS-Rule-Snippet](https://github.com/Hackl0us/SS-Rule-Snippet)  
[GeoIP2-CN](https://github.com/Hackl0us/GeoIP2-CN)