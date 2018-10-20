---
title: Windows支持多用户远程连接
date: 2018-10-20 22:37:19
tags: 工具、技巧
---
### Windows默认情况下仅支持一个用户通过远程桌面连接，当多个用户需要同时连接同一个PC时，需要修改最大连接数限制，步骤如下：
> 1、点击 开始-->运行-->输入"gpedit.msc"，进入本地组策略编辑器
>
> 2、点击 计算机配置-->管理模板-->Windows组件-->远程桌面服务-->远程桌面会话主机-->连接-->限制连接的数量
>
> 3、点击 启用，输入最大连接数

{% asset_img RemoteConnectNumSet.png SetMaxConnectNum  %}

