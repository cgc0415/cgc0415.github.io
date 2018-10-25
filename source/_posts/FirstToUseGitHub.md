---
title: 首次使用Github
date: 2018-10-25 22:11:40
tags: github
categories: 版本控制
---

## 1、配置用户名和邮箱

{% asset_img ConfigUserNameAndEmail.png pic:配置用户名和邮箱 %}

## 2、创建SSH-KEY

{% asset_img CreateSSH-KEY.png pic:创建SSH-KEY %}

然后系统提示输入文件保存位置等信息，连续敲三次回车即可 
如果一切顺利的话，可以在用户主目录里找到.ssh目录，里面有**id_rsa**和**id_rsa.pub**两个文件，这两个就是SSH Key的秘钥对，**id_rsa是私钥**，不能泄露出去，**id_rsa.pub是公钥**，可以放心地告诉任何人。

>* Linux下生成的SSH key文件保存在中～/.ssh/id_rsa.pub 
>*  Windows下保存在C:\Users\lzw.ssh

## 3、添加SSH-KEY到github

然后用文本编辑工具打开该公钥文件，使用notepad++或者sublime。不要使用记事本打开，因为记事本的默认编码不是utf-8，拷贝里面的全部内容，将它粘帖到github帐号管理中的添加SSH key界面中。 
打开github帐号管理中的添加SSH key界面的步骤如下：

> 1、登录github
>
> 2、点击右上方的Accounting settings图标
>
> 3、选择 SSH key 
>
> 4、点击 Add SSH key

在出现的界面中填写SSH key的名称，填一个你自己喜欢的名称即可，然后将上面拷贝的~/.ssh/id_rsa.pub文件内容粘帖到key一栏，在点击“add key”按钮就可以了。 
添加过程github会提示你输入一次你的github密码

## 4、验证SSH-KEY是否生效

验证SSH-KEY是否添加成功：

{% asset_img CheckSSH-KEY.png pic:验证SSH-KEY是否生效 %}

看到You've successfully authenticated，则表示SSH-KEY已添加成功并生效！