---
title: 0018_Java开发环境配置
date: 2018-11-07 21:05:18
tags: JDK
categories: Java
---

### 下载Java JDK
首先[<font color=blue>下载Java JDK</font>][1]，根据自己的系统选择对应的版本：
{% asset_img DownloadJDK.png pic:下载JDK %}

### 配置环境变量
安装完成后，右击"计算机"->"属性"->"高级系统设置"->"环境变量"
在"系统变量"中设置3项属性，JAVA_HOME,PATH,CLASSPATH(大小写无所谓),若已存在则点击"编辑"，不存在则点击"新建"。
- 变量名：JAVA_HOME
- 变量取值：C:\Program Files\Java\jdk-11.0.1
- 变量名：CLASSPATH
- 变量取值：.;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar;  //记得前面有个"."
- 变量名：Path
- 变量取值：%JAVA_HOME%\bin;%JAVA_HOME%\jre\bin;

### 测试JDK是否安装成功
1、"开始"->"运行"，键入"cmd"；
2、键入命令: java -version、java、javac 几个命令，出现以下信息，说明环境变量配置成功；
{% asset_img TestJDK.png pic:测试JDK是否安装成功 %}

[1]: https://www.oracle.com/technetwork/java/javase/downloads/jdk11-downloads-5066655.html