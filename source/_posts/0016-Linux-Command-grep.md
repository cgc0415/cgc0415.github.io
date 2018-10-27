---
title: grep命令
date: 2018-10-27 22:24:33
tags: grep命令
categories: Linux相关
---

#### 在文件test.txt中查找"hello"关键字以及前后5行的内容

```shell
grep -C 5 "hello" test.txt
```

#### 搜索test.txt中含有关键字"hello"的行号

```shell
grep -n "hello" test.txt
```

#### 查看test第13-15行

```shell
sed -n '13,15p' test.txt 
```

#### 统计当前文件夹下目录的个数

```shell
ls -l|grep "^d"|wc -l
```

#### 统计文件夹下目录的个数，包括子文件夹里的

```shell
ls -lR|grep "^d"|wc -l
```

#### 统计当前文件夹下文件的个数

```shell
ls -l |grep "^-"|wc -l
```

#### 统计当前文件夹下文件的个数，包括子文件夹里的

```shell
ls -lR|grep "^-"|wc -l
```

