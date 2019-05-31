---
title: 0022-工具技巧
date: 2019-05-31 22:14:07
tags: 工具技巧
---

### 1、SecureCRT保存日志

（1） 打开`Options->Session Options...`，，选择`LogFile`
（2） Log file name格式

```
%H_%S_%Y%M%D-%h%m%s.log
```

参数说明：

```
%H---主机IP
%S---Session名
%Y%M%D---年月日
%h%m%s---时分秒
```

### 2、VS（Visual Studio）输出重定向到文件

（1）、右键点击解决工程->项目属性

（2）、配置属性->生成事件->生成后事件

在命令行中输入`"$(TargetPath)  >$(outdir)\1.txt"`

（3）、重新编译整个项目，此时就会在debug目录下多了一个1.txt文件，里面就是程序运行时的控制台输出结果。