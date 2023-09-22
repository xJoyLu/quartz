author:: bjszz
source:: [关于获取cookie方法的实验（以抖音pc端为例） - 『编程语言区』 - 吾爱破解 - LCG](https://www.52pojie.cn/thread-1662783-1-1.html)
clipped:: [[2022-07-20]]
published:: 

我将利用三种方法来实验获取cookie，分别是HttpWebRequest，HttpWebResponse，提交请求的方式获取。CefSharp方式和Selenium方式 获取代码在下方，一、HttpWebRequest，HttpWebResponse，提交请求的方式获取，手机扫码登录pc端获取cookie.  
1、获取二维码链接：  

\[C#\] *纯文本查看* *复制代码*

1

`string` `url =` `"https://sso.douyin.com/get_qrcode/?aid=6383&app_name=douyin_web&device_platform=web&referer=&user_agent=Mozilla%2F5.0+(Windows+NT+6.3%3B+WOW64)+AppleWebKit%2F537.36+(KHTML,+like+Gecko)+Chrome%2F55.0.2883.87+UBrowser%2F6.2.4098.3+Safari%2F537.36&cookie_enabled=true&screen_width=1600&screen_height=900&browser_language=zh-CN&browser_platform=Win32&browser_name=Mozilla&browser_version=5.0+(Windows+NT+6.3%3B+WOW64)+AppleWebKit%2F537.36+(KHTML,+like+Gecko)+Chrome%2F55.0.2883.87+UBrowser%2F6.2.4098.3+Safari%2F537.36&browser_online=true&timezone_name=Asia%2FShanghai&next=https:%2F%2Fcreator.douyin.com%2F&service=https:%2F%2Fwww.douyin.com&is_vcd=1&fp=kesopiod_fB4eRss7_Stsz_434j_AiPQ_6xhtUsqmqpSN"``;`

  
2、请求二维码代码：  

\[Asm\] *纯文本查看* *复制代码*

01

02

03

04

05

06

07

08

09

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

`public` `static string GetUrl(string Url)`

 `{`

 `string html =` `""``;`

 `string charset =` `"utf-8"``;`

 `try`

 `{`

 `System.Net.ServicePointManager.SecurityProtocol = SecurityProtocolType.Tls12;`

 `HttpWebRequest request = (HttpWebRequest)WebRequest.Create(Url);  //创建一个链接`

 `request.UserAgent =` `"Mozilla/4.0 (compatible; MSIE 9.0; Windows NT 6.1)"``;`

 `request.Referer = Url;`

 `request.Proxy = null;`

 `request.Headers.``Add``(``"Accept-Encoding"``,` `"gzip"``);`

 `request.KeepAlive = true;`

 `request.Accept =` `"*/*"``;`

 `HttpWebResponse response = request.GetResponse() as HttpWebResponse;  //获取反馈`

 `if` `(response.Headers[``"Content-Encoding"``] ==` `"gzip"``)`

 `{`

 `GZipStream gzip = new GZipStream(response.GetResponseStream(), CompressionMode.Decompress);//解压缩`

 `StreamReader reader = new StreamReader(gzip, Encoding.GetEncoding(charset));`

 `html = reader.ReadToEnd();`

 `reader.Close();`

 `}`

 `else`

 `{`

 `StreamReader reader = new StreamReader(response.GetResponseStream(), Encoding.GetEncoding(charset));`

 `html = reader.ReadToEnd();`

 `reader.Close();`

 `}`

 `response.Close();`

 `return html;`

 `}`

 `catch (System.Exception ex)`

 `{`

 `return ex.ToString();`

 `}`

 `}`

3、请求返回Base64转图片方法：

\[C#\] *纯文本查看* *复制代码*

01

02

03

04

05

06

07

08

09

10

11

12

13

14

15

16

17

`public` `Image Base64ToImage(``string` `strbase64)`

 `{`

 `try`

 `{`

 `byte``[] arr = Convert.FromBase64String(strbase64);`

 `MemoryStream ms =` `new` `MemoryStream(arr);`

 `System.Drawing.Image mImage = System.Drawing.Image.FromStream(ms);`

 `ms.Close();`

 `return` `mImage;`

 `}`

 `catch` `(Exception ex)`

 `{`

 `MessageBox.Show(ex.ToString());`

 `return` `null``;`

 `}`

 `}`

  
4、获取二维码成功后，可用手机扫码，建立时间事件来监听扫码行为，处理扫码成功后方法：  

\[C#\] *纯文本查看* *复制代码*

01

02

03

04

05

06

07

08

09

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

`public` `void` `getSetCookie()`

 `{`

 `string` `Url =` `"https://sso.douyin.com/check_qrconnect/?aid=6383&app_name=douyin_web&device_platform=web&referer=&user_agent=Mozilla%2F5.0+(Windows+NT+6.3%3B+WOW64)+AppleWebKit%2F537.36+(KHTML,+like+Gecko)+Chrome%2F55.0.2883.87+UBrowser%2F6.2.4098.3+Safari%2F537.36&cookie_enabled=true&screen_width=1600&screen_height=900&browser_language=zh-CN&browser_platform=Win32&browser_name=Mozilla&browser_version=5.0+(Windows+NT+6.3%3B+WOW64)+AppleWebKit%2F537.36+(KHTML,+like+Gecko)+Chrome%2F55.0.2883.87+UBrowser%2F6.2.4098.3+Safari%2F537.36&browser_online=true&timezone_name=Asia%2FShanghai&next=https:%2F%2Fcreator.douyin.com%2F&token="` `+ token +` `"&service=https:%2F%2Fwww.douyin.com%2F&correct_service=https:%2F%2Fwww.douyin.com%2F&is_vcd=1&fp=kesopiod_fB4eRss7_Stsz_434j_AiPQ_6xhtUsqmqpSN"``;`

 `System.Net.ServicePointManager.SecurityProtocol = SecurityProtocolType.Tls12;`

 `HttpWebRequest request = (HttpWebRequest)WebRequest.Create(Url);` 

 `request.UserAgent =` `"Mozilla/4.0 (compatible; MSIE 9.0; Windows NT 6.1)"``;`

 `request.Referer = Url;`

 `HttpWebResponse response = request.GetResponse()` `as` `HttpWebResponse;` 

 `StreamReader reader =` `new` `StreamReader(response.GetResponseStream(), Encoding.GetEncoding(``"utf-8"``));`

 `string` `html = reader.ReadToEnd();`

 `string` `status = Regex.Match(html,` `@"""status"":""([\s\S]*?)"""``).Groups[1].Value;`

 `string` `redirect_url = Regex.Match(html,` `@"""redirect_url"":""([\s\S]*?)"""``).Groups[1].Value;`

 `if` `(status ==` `"1"``)`

 `{`

 `label1.Text =` `"未扫码.."``;`

 `}`

 `else` `if` `(status ==` `"2"``)`

 `{`

 `label1.Text =` `"已扫码.."``;`

 `}`

 `else` `if` `(redirect_url !=` `""``)`

 `{`

 `timer1.Stop();`

 `label1.Text =` `"登录成功"``;`

 `string` `content = response.GetResponseHeader(``"Set-Cookie"``);`

 `Uri uri =` `new` `Uri(``"http://douyin.com"``);`

 `string` `cookies = CookieHelper.GetCookies(content, uri);`

 `string` `cookies2 = getSetCookie2(cookies);`

 `textBox1.Text = cookies2 + cookies;`

 `}`

 `reader.Close();`

 `}`

5、处理扫码成功后方法2：

\[C#\] *纯文本查看* *复制代码*

01

02

03

04

05

06

07

08

09

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

`public` `string` `getSetCookie2(``string` `cookie)`

 `{`

 `string` `Url =` `"https://sso.douyin.com/check_login/?service=https:%2F%2Fwww.douyin.com&aid=6383"``;`

 `System.Net.ServicePointManager.SecurityProtocol = SecurityProtocolType.Tls12;`

 `HttpWebRequest request = (HttpWebRequest)WebRequest.Create(Url);` 

 `request.UserAgent =` `"Mozilla/4.0 (compatible; MSIE 9.0; Windows NT 6.1)"``;`

 `request.Referer = Url;`

 `request.Headers.Add(``"Cookie"``, cookie);`

 `HttpWebResponse response = request.GetResponse()` `as` `HttpWebResponse;` 

 `StreamReader reader =` `new` `StreamReader(response.GetResponseStream(), Encoding.GetEncoding(``"utf-8"``));`

 `string` `html = reader.ReadToEnd();`

 `string` `has_login = Regex.Match(html,` `@"""has_login"":([\s\S]*?),"``).Groups[1].Value;`

 `if` `(has_login ==` `"true"``)`

 `{`

 `reader.Close();`

 `label1.Text =` `"登录成功"``;`

 `string` `content = response.GetResponseHeader(``"Set-Cookie"``);`

 `Uri uri =` `new` `Uri(``"http://douyin.com"``);`

 `string` `cookies = CookieHelper.GetCookies(content, uri);`

 `return` `cookies;`

 `}`

 `else`

 `{`

 `reader.Close();`

 `label1.Text =` `"登录失败"``;`

 `return` `""``;`

 `}`

 `}`

  
6、扫码后提示“请使用手机验证码登录”，实验结果获取cookie失败。只是提示已扫码。  
二、利用CefSharp获取抖音cookie,并保存本地。  
1、添加控件tabPage1。添加窗体载入事件，加载抖音网页，代码：  

\[C#\] *纯文本查看* *复制代码*

1

2

3

4

5

6

7

`private` `void` `Webbrowser_Load(``object` `sender, EventArgs e)`

 `{`

 `browser =` `new` `ChromiumWebBrowser(get_code_url);`

 `Control.CheckForIllegalCrossThreadCalls =` `false``;`

 `tabPage1.Controls.Add(browser);`

 `}`

  
2、通过网页扫码提示登录成功，添加获取cookie按钮，调用获取cookie方法，并保存本地：  

\[C#\] *纯文本查看* *复制代码*

01

02

03

04

05

06

07

08

09

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

`private` `void` `button5_Click(``object` `sender, EventArgs e)`

 `{`

 `CookieVisitor visitor =` `new` `CookieVisitor();`

 `visitor.SendCookie += Visitor_SendCookie;`

 `ICookieManager cookieManager = browser.GetCookieManager();`

 `cookieManager.VisitAllCookies(visitor);`

 `MessageBox.Show(``"cookie已获取"``);`

 `}`

 `public` `static` `string` `COOKIE =` `""``;`

 `private` `void` `Visitor_SendCookie(CefSharp.Cookie obj)`

 `{`

 `COOKIE += obj.Name +` `"="` `+ obj.Value +` `";"``;`

 `File.WriteAllText(AppDomain.CurrentDomain.BaseDirectory +` `@"cookie.txt"``, COOKIE, Encoding.Default);`

 `textBox2.Text = COOKIE;`

 `}`

 `public` `class` `CookieVisitor : CefSharp.ICookieVisitor`

 `{`

 `public` `event` `Action<CefSharp.Cookie> SendCookie;`

 `public` `void` `Dispose()`

 `{`

 `}`

 `public` `bool` `Visit(CefSharp.Cookie cookie,` `int` `count,` `int` `total,` `ref` `bool` `deleteCookie)`

 `{`

 `deleteCookie =` `false``;`

 `SendCookie?.Invoke(cookie);`

 `return` `true``;`

 `}`

 `}`

3、成功获取到cookie,但是由于CefSharp包太大，软件打包后不方便，不推荐此方法。

三、利用Selenium包获取cookie,  
1、下载谷歌浏览器的chromedriver.exe放入软件根目录，在谷歌浏览器界面打开抖音主页扫码，  
利用Selenium的IWebDriver自带获取cookie方法webDriver.Manage().Cookies.AllCookies;获取cookie,但是发生异常，异常提示  
cookie的name为空，可利用webDriver.Manage().Cookies.DeleteCookieNamed("");去除cookie内空name,然后调用webDriver.Manage().Cookies.AllCookies;方法，以上消失。  

\[C#\] *纯文本查看* *复制代码*

01

02

03

04

05

06

07

08

09

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

`public` `void` `login()`

 `{`

 `webDriver.Navigate().GoToUrl(get_code_url);`

 `Thread.Sleep(10000);`

 `ReadOnlyCollection<Cookie> cookies1;`

 `while` `(``true``)`

 `{`

 `if` `(webDriver.PageSource.Contains(``"退出登录"``))`

 `{`

 `webDriver.Manage().Cookies.DeleteCookieNamed(``""``);`

 `cookies1 = webDriver.Manage().Cookies.AllCookies;`

 `break``;`

 `}`

 `}`

 `StringBuilder sb =` `new` `StringBuilder();`

 `foreach` `(``var` `item` `in` `cookies1)`

 `{`

 `sb.Append(item.Name +` `"="` `+ item.Value +` `";"``);`

 `}`

 `textBox1.Text = sb.ToString();`

 `File.WriteAllText(AppDomain.CurrentDomain.BaseDirectory +` `@"logincookie.txt"``, textBox1.Text, Encoding.Default);`

 `}`

  
2、然后利用获取的cookie，加载到浏览器就可以登录。  

\[C#\] *纯文本查看* *复制代码*

01

02

03

04

05

06

07

08

09

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

`webDriver.Navigate().GoToUrl(get_code_url);`

 `Thread.Sleep(10000);`

 `if` `(File.Exists(path))`

 `{`

 `string` `cookies2 = File.ReadAllText(path);`

 `string``[] cookieal3 = cookies2.Split(``new` `string``[] {` `";"` `}, StringSplitOptions.None);`

 `foreach` `(``var` `item` `in` `cookieal3)`

 `{`

 `if` `(!``string``.IsNullOrEmpty(item) && !item.Equals(``"="``))`

 `{`

 `string``[] cookie = item.Split(``new` `string``[] {` `"="` `}, StringSplitOptions.None);`

 `if` `(cookie.Length > 1)`

 `{`

 `OpenQA.Selenium.Cookie cook =` `new` `OpenQA.Selenium.Cookie(cookie[0].Trim(), cookie[1].Trim(),` `""``, DateTime.Now.AddDays(1));`

 `webDriver.Manage().Cookies.AddCookie(cook);`

 `}`

 `}`

 `}`

 `}`

 `else` `{`

 `MessageBox.Show(``"请先登录"``);`

 `return``;`

 `}`

  
总结，本次实验，利用了三种方法，对抖音cookie进行了获取，第一种方法是利用HttpWebRequest，HttpWebResponse，提交请求的方式获取，由于方式特殊，被拦截，第二种方法获取也很方便，但nuget包巨大，不推荐，第三种方法，利用谷歌浏览器获取，对不熟悉操作的人也不是很方便，后两种方法，都获取成功。