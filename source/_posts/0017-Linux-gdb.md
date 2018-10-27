---
title: gdb调试
date: 2018-10-27 22:32:21
tags: gdb
categories: Linux相关
---

### 前言

使用gdb调试前，在编译程序时，要加 -g 选项，否则你将看不见程序的函数名、变量名，所代替的全是运行时的内存地址。

```shell
gdb -q a.out // -q(uiet)表示不打印gdb的版权信息
```

### 调试环境

#### 运行参数

> set args 可指定运行时参数。（如：set args 10 20 30 40 50）
> show args 命令可以查看设置好的运行参数。

#### 环境变量

> path <dir> 可设定程序的运行路径。
> show paths 查看程序的运行路径。
> set environment varname [=value] 设置环境变量。如：set env USER=hchen
> show environment [varname] 查看环境变量。

#### 工作目录

> cd <dir> 相当于shell的cd命令。
> pwd 显示当前的所在目录。

### 设置观察点

观察点一般来观察某个表达式（变量也是一种表达式）的值是否有变化了，如果有变化，马上停住程序。我们有下面的几种方法来设置观察点：

```shell
watch <expr>
```

为表达式（变量）expr设置一个观察点。一量表达式值有变化时，马上停住程序。[如watch i==100，当该条件成立时程序会暂停执行]

观察某个地址的数据变化  watch *(int*)0x00000000

### 分割窗口

> layout：用于分割窗口，可以一边查看代码，一边测试：
> layout src：显示源代码窗口
> layout asm：显示反汇编窗口
> layout regs：显示源代码/反汇编和CPU寄存器窗口
> layout split：显示源代码和反汇编窗口
> Ctrl + L：刷新窗口

### 调试过程

#### 开始调试

> a.  gdb <program> 
>
> program也就是你的执行文件，一般在当前目录下。
>
> b. gdb <program> core
>
> 用gdb同时调试一个运行程序和core文件，core是程序非法执行后core dump后产生的文件。

#### 列出源码

> 从第n行开始（编译时要加 -g 选项）
>
> l n

#### 设置断点

```shell
break n //在第n行添加断点
break func //在函数func入口处添加断点
```

#### 查看断点信息

```shell
info break
```

#### 断点命中后自动打印调用栈

```shell
set pagination off
b malloc
commands 1 （1表示断点编号，用i b可以查询所有断点）
bt
continue
end
c
```

#### 单步执行

> n --->next的首字母

#### 继续执行

> c --->continue的首字母

#### 打印变量的值

> p varname

#### 查看调用栈

> bt

#### 退出函数

> finish

#### 退出gdb

> q --->quit的首字母

#### gdb中执行shell命令

> shell <command string>