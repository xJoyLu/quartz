author:: Ted
source:: [UUP dump｜3分鐘學會如何下載整合更新的Win10/Win11映像檔(ISO)](https://adersaytech.com/online-tool/uup-dump-review.html)
clipped:: [[2022-11-23]]
published:: 

![UUP dump｜3分鐘學會如何下載整合更新的Win10/Win11映像檔(ISO) 3](https://adersaytech.com/wp-content/uploads/2021/10/UUP-dump-review-1024x576.jpg "UUP dump｜3分鐘學會如何下載整合更新的Win10/Win11映像檔(ISO) 4")

**文章最後更新時間：2022 年 5 月 28 日**

每當[重灌電腦](https://adersaytech.com/windowsos-tutorial/win11-clean-installation.html)後，透過 [Windows Update](https://zh.wikipedia.org/wiki/Windows_Update) 來更新系統版本與[驅動程式](https://zh.wikipedia.org/wiki/%E9%A9%B1%E5%8A%A8%E7%A8%8B%E5%BA%8F)，應該是大多數人的第一個動作，因為除了可以把系統更新到最新的版本之外，驅動程式也會一起更新到穩定的版本，讓電腦的穩定性與安全性有保障。

但是如果你手上的 ISO 映像檔是比較舊的版本，在重灌完成後所要做的系統更新可能會很多且花時間，電腦效能非常好與網路速度非常快的話那還好，不然可是要等待一段時間才會更新安裝好。

舉個例子來說，Win10 21H1 的初始 ISO 檔案組建是 v19043.928，經過一段時間後，累積的更新越來越多，組建的版號已經變成 v19043.1263，這時候如果你是用初始的 ISO 來重灌電腦的話，之後所需要做的系統更新會比較花時間。

那有沒有辦法可以下載已經整合更新的 Win11/Win10 ISO 映像檔？當然是沒問題，只要透過 [UUP dump](https://uupdump.net/?lang=zh-tw) 工具就可以輕鬆下載任何組建(整合更新)，讓你不用每次重灌電腦都要安裝一堆系統更新。

如果在閱讀文章過程中有任何問題，歡迎隨時在底下留言，或是透過[聯絡我](https://adersaytech.com/contact-ader)跟我溝通討論，讓我們開始今天的主題吧！

**內容目錄**  [顯示](https://adersaytech.com/online-tool/uup-dump-review.html#) 

## UUP dump 是什麼？

![UUP dump 網站](https://adersaytech.com/wp-content/uploads/2021/10/uup-dump-website-1024x234.webp "UUP dump｜3分鐘學會如何下載整合更新的Win10/Win11映像檔(ISO) 5")

[UUP dump](https://uupdump.net/?lang=zh-tw) 是一個網頁版的 Windows ISO 映像檔下載工具，由 [whatever127](https://github.com/whatever127) 所開發維護，所有檔案都是透過微軟的伺服器取得，再經過開發者撰寫的腳本，把檔案整合在一起，形成特定組建的 ISO 檔。

透過 UUP dump 也可以下載到各種版本的 Win10/Win11/Win Server，例如家用版、專業版、教育版、工作站版、企業版等版本，都可以輕鬆取得，可以單一版本下載，或是把所有版本都整合到同一個 ISO 檔案內。

除了微軟已經對外正式發行的組建之外，也可以下載到預覽測試版本的組建，對於有特定組建版本需求的人來說，UUP dump 是一個不可或缺的好用工具！

## Windows 組建版本列表

想要透過 UUP dump 下載特定組建版本的 ISO，首先就是必須要知道組建號碼，雖然透過關鍵字也可以查詢，但往往用關鍵字查詢的結果都會很多，一般使用者很容易搞混。

所以如果可以知道想要的組建號碼，直接利用組建去查詢，會比較快且精準，下方列出微軟官方所提供的組建列表，可以直接點擊前往。

-   [Windows 11 正式發行組建](https://docs.microsoft.com/zh-tw/windows/release-health/windows11-release-information)
-   [Windows 10 正式發行組建](https://docs.microsoft.com/zh-tw/windows/release-health/release-information)
-   [Win10/Win11 預覽版組建](https://docs.microsoft.com/zh-tw/windows-insider/flight-hub/)

## 如何使用 UUP dump？

![如何使用uup dump下載映像檔](https://adersaytech.com/wp-content/uploads/2021/10/how-to-use-uup-dump.webp "UUP dump｜3分鐘學會如何下載整合更新的Win10/Win11映像檔(ISO) 6")

這個章節會示範如何利用 UUP dump 工具來下載特定組建的 ISO 映像檔，版本則是選擇 Windows 11 專業版來當作教學。

根據微軟 Windows 11 版本發行紀錄，截至我撰寫文章的當下，最新的版本是 22000.282，會以此組建號碼當作搜尋下載目標，如果你有其他組建的下載需求，操作方式都是一樣的。

**預估時間：** 3 minutes

#### STEP 1：搜尋 OS 組建

![UUP dump｜3分鐘學會如何下載整合更新的Win10/Win11映像檔(ISO) 7](https://adersaytech.com/wp-content/uploads/2021/10/uup-dump-search-build.webp "UUP dump｜3分鐘學會如何下載整合更新的Win10/Win11映像檔(ISO) 8")

[點我](https://uupdump.net/?lang=zh-tw)前往 UUP dump 工具頁面，在搜尋框內輸入組建號碼，或是使用關鍵字搜尋也可以，下方有一些常用的關鍵字可以直接選取搜尋。

#### STEP 2：選擇下載版本

![UUP dump｜3分鐘學會如何下載整合更新的Win10/Win11映像檔(ISO) 9](https://adersaytech.com/wp-content/uploads/2021/10/select-build-to-download.webp "UUP dump｜3分鐘學會如何下載整合更新的Win10/Win11映像檔(ISO) 10")

以我的搜尋為例子，搜尋完成後可以看到有四個結果，兩個是給 x64 系統，兩個給 Arm64 系統，主要差別是前方有「Cumulative」字樣的，這個代表指預先安裝重要的系統更新，一些小更新不安裝以減少 ISO 檔案大小。

我自己習慣會選擇 Cumulative 的 ISO 檔案來下載，因為檔案小一點，其餘的功能小更新則留到系統安裝完成後再透過 WU 更新即可。

#### STEP 3：選擇 ISO 語言

![選擇ISO語言](https://adersaytech.com/wp-content/uploads/2021/10/uup-dump-select-iso-language.webp "UUP dump｜3分鐘學會如何下載整合更新的Win10/Win11映像檔(ISO) 11")

根據自己想要下載的語系選擇，我自己是繁體中文使用者，所以選擇中文(繁體)的選項，按下一步。

#### STEP 4：選擇 ISO 版本

![UUP dump｜3分鐘學會如何下載整合更新的Win10/Win11映像檔(ISO) 12](https://adersaytech.com/wp-content/uploads/2021/10/uup-dump-select-iso-version.webp "UUP dump｜3分鐘學會如何下載整合更新的Win10/Win11映像檔(ISO) 13")

這邊可以選擇下載後 ISO 內所含的版本，如果你只有單一版本需求，只要勾選想要的即可，我這邊會選擇專業版(Pro)。

右方的額外版本則是告訴你還有哪些版本可以加入選擇，在下一個步驟可以設定。

#### STEP 5：下載套建

![下載uup dump 套件](https://adersaytech.com/wp-content/uploads/2021/10/uup-dump-download-script.webp "UUP dump｜3分鐘學會如何下載整合更新的Win10/Win11映像檔(ISO) 14")

下載方式選擇「使用 aria2 下載並轉換」的選項，下方的轉換選項可以依照自己需求來選擇，如果有勾選「執行清理工作」，這樣在 ISO 製作完成時檔案會更小一點。

**這個步驟所下載的檔案並非 ISO 映像檔，只是把這些選項設定的「下載工具」下載到電腦，後續要透過這個工具進行 ISO 下載。**

如果你想要整合其他版本的 Win11，例如家用版、企業版等，下載方式的選項請選擇第三個「使用 aria2 下載、轉換並建立而外版本」，這樣下方就會多出可選擇加入的版本，如下圖。  
![多版本整合下載](https://adersaytech.com/wp-content/uploads/2021/10/uup-dump-multi-versions-download.webp "UUP dump｜3分鐘學會如何下載整合更新的Win10/Win11映像檔(ISO) 15")

#### STEP 6：執行下載腳本

![UUP dump｜3分鐘學會如何下載整合更新的Win10/Win11映像檔(ISO) 16](https://adersaytech.com/wp-content/uploads/2021/10/uup-dump-execute-download-script.webp "UUP dump｜3分鐘學會如何下載整合更新的Win10/Win11映像檔(ISO) 17")

套件下載回來電腦後，把它解壓縮開，執行裡面的 CMD 腳本，如圖所示。

#### STEP 7：開始下載檔案

![CMD視窗會開始下載檔案](https://adersaytech.com/wp-content/uploads/2021/10/uup-dump-CMD-download-components.webp "UUP dump｜3分鐘學會如何下載整合更新的Win10/Win11映像檔(ISO) 18")

到這個步驟才真正開始下載 ISO 所需要的檔案，腳本會把所有你剛剛勾選的的自訂選項需要的檔案下載回來，之後才會做合併的動作。

#### STEP 8：開始合併生成 ISO 檔

![合併生成ISO](https://adersaytech.com/wp-content/uploads/2021/10/uup-dump-create-iso.webp "UUP dump｜3分鐘學會如何下載整合更新的Win10/Win11映像檔(ISO) 19")

當所有必要檔案都下載完成後，腳本會開始把這些檔案安裝合併到 ISO 映像檔內，需要一小段時間，過程是全自動執行。

#### STEP 9：整合更新 ISO 製作完成

![整合更新檔的ISO製作完成](https://adersaytech.com/wp-content/uploads/2021/10/uup-dump-complete-iso-creation.webp "UUP dump｜3分鐘學會如何下載整合更新的Win10/Win11映像檔(ISO) 20")

看到 CMD 視窗最後一段有跑出「Press 0 to exit.」就代表 ISO 檔案已經整合完成，按一下數字鍵的 0，就可以離開腳本視窗。

在原本的資料夾內就可以找到已經建立好的 ISO 映像檔，如下圖。  
![ISO映像檔在原本的資料夾內](https://adersaytech.com/wp-content/uploads/2021/10/ISO-file-in-folder.webp "UUP dump｜3分鐘學會如何下載整合更新的Win10/Win11映像檔(ISO) 21")

之後再透過 [Rufus](https://adersaytech.com/practical-software/rufus-review.html) 或是 [Ventoy](https://adersaytech.com/practical-software/ventoy-tool-review.html) 軟體來把 ISO 檔案製作成 USB 開機隨身碟就完成囉！

**Supply:**

-   Microsoft

**Tools:**

-   UUP dump

## 總結

利用有含整合更新的 ISO 檔重灌電腦後，所必須要做的系統更新會少很多，除了可以減少更新所需的時間之外，也可以減少網路頻寬的使用，對於有大量安裝系統的人或是有特定組建需求的人來說，UUP dump 會是一個非常好用的工具。

除了常見的家用版與專業版之外，UUP dump 還可以下載到各式各樣的版本，讓你不會因為想要找特定版本浪費一堆時間，最後還找不到。

如果還沒嘗試過，快點跟著本篇教學一起試試看吧！

## 常見問題

### Cumulative 更新與 Feature 更新有什麼不一樣？

Cumulative 更新只有包含系統必要的更新，Feature 更新則有包含一些功能性的更新，所以一般來說，Cumulative 更新的 ISO 檔案大小會比 Feature 更新的 ISO 還要小一點點。

### 如何查詢 Windows 組建號碼？

微軟有提供組建號碼可以查詢，如下：  
1. [Windows 11 查詢](https://docs.microsoft.com/zh-tw/windows/release-health/windows11-release-information)  
2. [Windows 10 查詢](https://docs.microsoft.com/zh-tw/windows/release-health/release-information)  
3. [測試預覽版查詢](https://docs.microsoft.com/zh-tw/windows-insider/flight-hub/)

### 轉換選項的「在整合更新後執行清理」是什麼意思？

在腳本合併完整合更新檔案後，會針對 install.wim 做一次清理與優化，可以使檔案更小一點。

### 轉換選項的「整合 .NET Framework 3.5」是什麼意思？

Win10/Win11 預設的環境並沒有安裝 .NET Framework 3.5，如果有需要可以在安裝完成後手動增加安裝，勾選此選項的話，腳本會預先把 .NET Framework 3.5 安裝到 ISO 映像檔案內，重灌完成後就不用再手動安裝。

### 轉換選項的「使用 install.esd 而非 install.wim 建立 ISO 檔」是什麼意思？

ESD 的檔案壓縮率會比 WIM 要來的高，所以如果選擇這個選項，檔案大小會減少很多，但是如果自己有手動客製化的需求，則需再把 ESD 轉換成 WIM，才能進行掛載的動作。

## UUP dump 簡介

##### UUP dump

![UUP dump｜3分鐘學會如何下載整合更新的Win10/Win11映像檔(ISO) 22](https://adersaytech.com/wp-content/uploads/2021/10/UUP-dump-review-300x169.jpg "UUP dump｜3分鐘學會如何下載整合更新的Win10/Win11映像檔(ISO) 23")

UUP dump 是一個網頁版的 Windows ISO 映像檔下載工具，由 whatever127 所開發維護，所有檔案都是透過微軟的伺服器取得，再經過開發者撰寫的腳本，把檔案整合在一起，形成特定組建的 ISO 檔。除了微軟已經對外正式發行的組建之外，也可以下載到預覽測試版本的組建。