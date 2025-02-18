author:: null
source:: [mac上用Automator编写自动脚本_destiny_ac的博客-CSDN博客_mac自动按键脚本](https://blog.csdn.net/destiny_ac/article/details/43965909#)
clipped:: [[2022-08-29]]
published:: 

最近努力学习新知识，在公司内网上阅读一些优秀文章，但是发现这些文章：是通过通过flash控件展示，并且不提供无法下载地址（类似《百度文库》）。一次忍了，两次再忍了，三次就无法忍受：都在我电脑上展示了，这么做就是恶心人了。。。。  
于是花了大半天时间，使用mac上自带软件Automator，从零开始完成了自己的工具：《连续抓图导出PDF》。

> 实现原理：自动截屏、翻页=》merge生成PDF文档。（感兴趣的人，可以下载附件看看源码）

在写这个脚本过程中，本以为会很快，但是还是碰到了不少问题；于是就记录并分享出来。

首先：最基本用法，可以直接参考Automator帮助，本文章只写自认为容易忽略或者难点的几个地方。

---

变量新建就不说了；这里主要说变量再控件上使用，几种方法（有的方法只对部分控件有用）：

## 从下拉列表直接选择“变量”

![这里写图片描述](https://img-blog.csdn.net/20150227115326841)

## 将“变量”拖进区域

![这里写图片描述](https://img-blog.csdn.net/20150227115813754)  
当然你也可以，抛弃使用已存在的变量，直接通过下拉框选择一个“新建变量”。

## “输入变量名”弹出提示，“回车”选择

![这里写图片描述](https://img-blog.csdn.net/20150227120247943)  
![这里写图片描述](https://img-blog.csdn.net/20150227120259112)

最后，如果上面三种方法你尝试都不行的话，基本上可以宣告，那个是不支持变量的。  
比如，LOOP的“次数”，是不支持变量的：  
![这里写图片描述](https://img-blog.csdn.net/20150227120551615)

---

## 脚本使用

Automator脚本支持：shell脚本（bash、perl、python、ruby等）、appleScript、javascript几种，你可以选择不同的脚本来运行。  
![这里写图片描述](https://img-blog.csdn.net/20150227150607647)

## 脚本[参数传递](https://so.csdn.net/so/search?q=%E5%8F%82%E6%95%B0%E4%BC%A0%E9%80%92&spm=1001.2101.3001.7020)

> 脚本和变量之间，是无法直接获取或设置的

### “变量”[值传递](https://so.csdn.net/so/search?q=%E5%80%BC%E4%BC%A0%E9%80%92&spm=1001.2101.3001.7020)到脚本

– shell脚本

```
        获取到的输入：只能是通过输入的一行一行的字符串
        也即如果，想获取变量值的话，可以通过，“获得变量的值”控件来输出值，然后传递到脚本然后再读取。
        如：下面是获取“页数”、“URL”、“临时文件夹”三个变量值到输出，然后传递给perl脚本。
```

![这里写图片描述](https://img-blog.csdn.net/20150227151258533)

– AppleScript脚本

```
AppleScript的输入不是一行一行的字符串，貌似是键值队（还不熟悉这块），结果没搞懂如何传递的变量——搞懂后，再补充。
于是我考虑的解决方案是：通过分隔符“|”将输入的多行转换成一行，然后在AppleScript进行反转。的确是有些trick -_-!——不过后来查资料发现，也有人这么整。
```

![这里写图片描述](https://img-blog.csdn.net/20150227152004323)  
perl代码：

```
@input = ();
while (<>) {
        $_=~s/(^\s*)|(\s*$)//g;
        push(@input,$_);
}
print join "|" ,@input;
```

AppleScript代码：

```
on run input

    set myArray to my theSplit((item 1 of input) as string, "|")
    set outputPath to item 1 of myArray
    set pagenum to item 2 of myArray as number
    set myurl to item 3 of myArray
    set tempDir to item 4 of myArray

    return myArray
end run

on theSplit(theString, theDelimiter)
    
    set oldDelimiters to AppleScript's text item delimiters

    
    set AppleScript's text item delimiters to theDelimiter

    
    
    set theArray to text items of theString

    
    set AppleScript's text item delimiters to oldDelimiters

    
    return theArray
end theSplit
```

### 脚本结果，设置到“变量”中

脚本中的变量，是无法设置到脚本中，怎么办呢？其也只能通过脚本输出结果，然后“设定变量的值”控件，对变量进行设置。  
\- - 设置一个变量

![这里写图片描述](https://img-blog.csdn.net/20150227152844534)

> 注意：这里有一个问题，如果脚本输出的是多行，其实只把第一行字符串，赋值到“变量”中

-   -   设置多个变量

但是如果要设置多个变量值，咋办？  
于是又是一个trick方法来了，利用上面“只会把第一行赋值给变量”的机制，通过“漏斗”方式逐个对变量进行赋值：  
![这里写图片描述](https://img-blog.csdn.net/20150227153354101)  
如上图，依次对“导出路径”、“页数”等多个变量进行逐个复制。  
其中perl代码作用是：过滤第一行字符串：

```
$count=0;
while(<>){
    print $_ if $count >0 ; 
    $count = $count + 1 ;
}
```

---

Automator提供“录制”功能，位于右上角：  
![这里写图片描述](https://img-blog.csdn.net/20150227121126612)  
注意如果你使用录制功能，需要mac再偏好设置里，设置一下“允许Automator控制你的电脑”，这样在运行时才有用：  
![这里写图片描述](https://img-blog.csdn.net/20150227121530641)

但是实际操作起来，我碰到了下面两个问题：

> 1、鼠标录制，总是不准  
> 2、键盘录制，则永远也没有录制上去

第一个问题，我没有找到很好办法；最后没有使用；  
第二个问题，不是录入，而是写代码，通过appleScript来实现：

## 键盘操作

![这里写图片描述](https://img-blog.csdn.net/20150227122227102)  
脚本代码是：

```
on run {input, parameters}
    
    set timeoutSeconds to 0
    set uiScript to "keystroke \"a\" " 
    my doWithTimeout(uiScript, timeoutSeconds)
    return input
end run

on doWithTimeout(uiScript, timeoutSeconds)
    set endDate to (current date) + timeoutSeconds
    repeat
        try
            run script "tell application \"System Events\"
" & uiScript & "
end tell"
            exit repeat
        on error errorMessage
            if ((current date) > endDate) then
                error "Can not " & uiScript
            end if
        end try
    end repeat
end doWithTimeout
```

接下来，看看键盘操作（均是修改，标注的那一行）几种情况解决方案：

### 普通字符

普通字符，比较简单，使用keystroke ，输入字符就可以，比如输入”a”字符：

```
set uiScript to "keystroke \"a\" "
```

### 特殊字符

对于一些特殊字符，没有特殊ASCII码，比如：上、下、左、右键。因此可以考虑另外一个通过“键值”（即操作系统对按键的虚拟值）来实现，key code ：

比如：“右”按键的代码是：

```
set uiScript to "key code 124  "
```

当然，key code 也可以输入普通字符，如：  
“a” 按键代码是：

```
set uiScript to "key code 0  "
```

“A”按键代码是：

```
set uiScript to "key code 0  using {shift down} "
```

mac系统的虚拟键值，可以通过终端命令执行下面命令查询到：

```
$ grep '^ *kVK' /System/Library/Frameworks/Carbon.framework/Versions/A/Frameworks/HIToolbox.framework/Versions/A/Headers/Events.h|tr -d ,|while read x y z;do printf '%d %s %s\n' $z $z ${x#kVK_};done|sort -n
```

或者你直接查下“附1-key code 表”也行：

### 组合键

上两个方法，都可以配合组合键进行使用：

```
set uiScript to "key code 124 using {control down, option down, command down,shift down}" --control+option+command+right+shift
```

---

Automator对于系列处理动作的流程，制作非常简单，仅仅需要拖拽基本就可以实现。  
但是在分支、循环等这种逻辑上，处理起来要复杂很多。 基本稍微复杂一点的都需要脚本配合才可以的。

## 简单循环

Automator只提供了简单的“Loop”循环控件，这个循环控件可控执行很差，因为：

-   只能从脚本开头循环
    
-   循环策略支持：  
    A）次数/时间，但是无法通过变量控制  
    B）询问方式  
    试想一下，你就是需要从中间块循环，但是他非要从开头开始，你是无法选择的，这是个多么想哭的事情。
    

## 复杂循环

那么对于复杂的循环怎么处理？  
Automator支持workflow的调用，因此如果你需要循环的话一种解决方案就是：将需要循环块的部分，写成workflow1，然后再主workflow通过脚本控制workflow1的循环。

Created with Raphaël 2.1.2 workflow开始 准备工作 调用workflow1 是否结束？ 结束 yes no

> 注意：新建workflow1时，选择“工组流程”：  
> ![这里写图片描述](https://img-blog.csdn.net/20150227162701530)

这里实现主要有两个问题：  
1、workflow之间的变量是无法共享的（至少现在我发现是这样的）。它也只能想字符串一样传递。  
但是这个问题：上面脚本使用一节中的“多变量的赋值”方法可以解决。

2、如何脚本调用，workflow？  
通过 do shell script cmd，进行执行cmd命令调用，但是这里有一个问题就是：命令执行是不等待结束立即返回的（实现方法是新起进程执行）——目前还没有找到能够等待返回的方法。

```
on run input

    set myArray to my theSplit((item 1 of input) as string, "|")
    set outputPath to item 1 of myArray
    set pagenum to item 2 of myArray as number
    set myurl to item 3 of myArray
    set tempDir to item 4 of myArray

    delay 10
    set mycount to 1000 as number
    repeat
        run_workflow(tempDir & "/" & (mycount) & ".pdf", "/Users/xxxx/Desktop/test2/自动截频.workflow")
        if pagenum ≤ 1 then
            exit repeat
        end if
        set pagenum to pagenum - 1
        set mycount to mycount + 1

        
        set timeoutSeconds to 2
        set uiScript to "keystroke (ASCII character 29)  "
        my doWithTimeout(uiScript, timeoutSeconds)
    end repeat
    delay 1
    return myArray
end run


on run_workflow(inputVars, workflowPath)
    set {tid, AppleScript's text item delimiters} to {AppleScript's text item delimiters, linefeed}
    set theInputsList to inputVars as text
    set AppleScript's text item delimiters to tid
    set cmd to "automator -i '" & theInputsList & "' " & workflowPath
    return do shell script cmd
end run_workflow

on theSplit(theString, theDelimiter)
    
    set oldDelimiters to AppleScript's text item delimiters

    
    set AppleScript's text item delimiters to theDelimiter

    
    
    set theArray to text items of theString

    
    set AppleScript's text item delimiters to oldDelimiters

    
    return theArray
end theSplit

on doWithTimeout(uiScript, timeoutSeconds)
    set endDate to (current date) + timeoutSeconds
    repeat
        try
            run script "tell application \"System Events\"
" & uiScript & "
end tell"
            exit repeat
        on error errorMessage
            if ((current date) > endDate) then
                error "Can not " & uiScript
            end if
        end try
    end repeat
end doWithTimeout
```

## 附1-key code 表

十进制

十六进制

按键

0

0x00

ANSI\_A

1

0x01

ANSI\_S

2

0x02

ANSI\_D

3

0x03

ANSI\_F

4

0x04

ANSI\_H

5

0x05

ANSI\_G

6

0x06

ANSI\_Z

7

0x07

ANSI\_X

8

0x08

ANSI\_C

9

0x09

ANSI\_V

10

0x0A

ISO\_Section

11

0x0B

ANSI\_B

12

0x0C

ANSI\_Q

13

0x0D

ANSI\_W

14

0x0E

ANSI\_E

15

0x0F

ANSI\_R

16

0x10

ANSI\_Y

17

0x11

ANSI\_T

18

0x12

ANSI\_1

19

0x13

ANSI\_2

20

0x14

ANSI\_3

21

0x15

ANSI\_4

22

0x16

ANSI\_6

23

0x17

ANSI\_5

24

0x18

ANSI\_Equal

25

0x19

ANSI\_9

26

0x1A

ANSI\_7

27

0x1B

ANSI\_Minus

28

0x1C

ANSI\_8

29

0x1D

ANSI\_0

30

0x1E

ANSI\_RightBracket

31

0x1F

ANSI\_O

32

0x20

ANSI\_U

33

0x21

ANSI\_LeftBracket

34

0x22

ANSI\_I

35

0x23

ANSI\_P

36

0x24

Return

37

0x25

ANSI\_L

38

0x26

ANSI\_J

39

0x27

ANSI\_Quote

40

0x28

ANSI\_K

41

0x29

ANSI\_Semicolon

42

0x2A

ANSI\_Backslash

43

0x2B

ANSI\_Comma

44

0x2C

ANSI\_Slash

45

0x2D

ANSI\_N

46

0x2E

ANSI\_M

47

0x2F

ANSI\_Period

48

0x30

Tab

49

0x31

Space

50

0x32

ANSI\_Grave

51

0x33

Delete

53

0x35

Escape

55

0x37

Command

56

0x38

Shift

57

0x39

CapsLock

58

0x3A

Option

59

0x3B

Control

60

0x3C

RightShift

61

0x3D

RightOption

62

0x3E

RightControl

63

0x3F

Function

64

0x40

F17

65

0x41

ANSI\_KeypadDecimal

67

0x43

ANSI\_KeypadMultiply

69

0x45

ANSI\_KeypadPlus

71

0x47

ANSI\_KeypadClear

72

0x48

VolumeUp

73

0x49

VolumeDown

74

0x4A

Mute

75

0x4B

ANSI\_KeypadDivide

76

0x4C

ANSI\_KeypadEnter

78

0x4E

ANSI\_KeypadMinus

79

0x4F

F18

80

0x50

F19

81

0x51

ANSI\_KeypadEquals

82

0x52

ANSI\_Keypad0

83

0x53

ANSI\_Keypad1

84

0x54

ANSI\_Keypad2

85

0x55

ANSI\_Keypad3

86

0x56

ANSI\_Keypad4

87

0x57

ANSI\_Keypad5

88

0x58

ANSI\_Keypad6

89

0x59

ANSI\_Keypad7

90

0x5A

F20

91

0x5B

ANSI\_Keypad8

92

0x5C

ANSI\_Keypad9

93

0x5D

JIS\_Yen

94

0x5E

JIS\_Underscore

95

0x5F

JIS\_KeypadComma

96

0x60

F5

97

0x61

F6

98

0x62

F7

99

0x63

F3

100

0x64

F8

101

0x65

F9

102

0x66

JIS\_Eisu

103

0x67

F11

104

0x68

JIS\_Kana

105

0x69

F13

106

0x6A

F16

107

0x6B

F14

109

0x6D

F10

111

0x6F

F12

113

0x71

F15

114

0x72

Help

115

0x73

Home

116

0x74

PageUp

117

0x75

ForwardDelete

118

0x76

F4

119

0x77

End

120

0x78

F2

121

0x79

PageDown

122

0x7A

F1

123

0x7B

LeftArrow

124

0x7C

RightArrow

125

0x7D

DownArrow

126

0x7E

UpArrow

## 附1-《连续抓图导出PDF》脚本

[http://download.csdn.net/detail/destiny\_ac/8461453](http://download.csdn.net/detail/destiny_ac/8461453)