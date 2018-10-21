---
title: Windows Ping加时间戳
date: 2018-10-21 13:04:45
tags: 工具、技巧
---

### 在c盘下面新建文件 ping.vbs，在 ping.vbs中输入代码如下:

```bash
Dim args, flag, unsuccOut
args=""
otherout=""
flag=0
 
If WScript.Arguments.count = 0 Then
WScript.Echo "Usage: cscript tping.vbs [-t] [-a] [-n count] [-l size] [-f] [-i TTL] [-v TOS]"
WScript.Echo "                         [-s count] [[-j host-list] | [-k host-list]]"
WScript.Echo "                         [-r count] [-w timeout] destination-list"
wscript.quit
End if
 
For i=0 to WScript.Arguments.count - 1
args=args & " " & WScript.Arguments(i)
Next
 
Set shell = WScript.CreateObject("WScript.Shell")
Set re=New RegExp
re.Pattern="^Reply|^Request|^来自|^请求"
 
Set myping=shell.Exec("ping" & args)
 
while Not myping.StdOut.AtEndOfStream
   strLine=myping.StdOut.ReadLine()
'WScript.Echo  "原数据" & chr(9) & strLine
   r=re.Test(strLine)
   If r Then
WScript.Echo date & " "& time & chr(9) & strLine
flag=1
   Else
unsuccOut=unsuccOut & strLine
   End if
Wend
 
if flag = 0 then
WScript.Echo unsuccOut
end if
```
### 切到脚本所在目录，然后调出cmd，执行如下命令:
```bash
cscript ping.vbs www.baidu.com -t -l 1000 -w 5000>sseping.txt
```