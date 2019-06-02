---
title: 0023-树莓派相关
date: 2019-06-02 13:51:57
tags: 树莓派
---

### 1、连接WiFi

（1）将树莓派外接一个显示器（可用HDMI接口），键盘
（2）找到/etc/wpa_supplicant/wpa_supplicant.conf文件，修改其中的WifiID（ssid）及密码（psk）
```
country=CN
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
 
network={
        ssid="***"
        key_mgmt=WPA-PSK
        psk="***"
}
```
（3）重启树莓派
（4）查询获取到的IP，观察wlan0中IP信息
```
root@raspberrypi:/# ifconfig
eth0      Link encap:Ethernet  HWaddr b8:27:eb:XX:XX:XX  
          inet6 addr: fe80::6d6a:35f5:5f5c:2351/64 Scope:Link
          UP BROADCAST MULTICAST  MTU:1500  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)

lo        Link encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:203842 errors:0 dropped:0 overruns:0 frame:0
          TX packets:203842 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:82362372 (78.5 MiB)  TX bytes:82362372 (78.5 MiB)

wlan0     Link encap:Ethernet  HWaddr b8:27:eb:XX:XX:XX  
          inet addr:192.168.XX.XXX  Bcast:192.168.31.255  Mask:255.255.255.0
          inet6 addr: fe80::ba27:ebff:fecb:d88e/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:191486 errors:0 dropped:19 overruns:0 frame:0
          TX packets:278266 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:18741736 (17.8 MiB)  TX bytes:50965793 (48.6 MiB)
```

### 2、samba服务

（1）添加samba用户
```sudo smbpasswd -a root
sudo smbpasswd -a root
```
然后输入相应的密码

（2）重启、停止samba服务
```
sudo /etc/init.d/samba restart
sudo /etc/init.d/samba stop
```

### 3、安装vim编辑器

（1）首先删除默认vi编辑器
```
 sudo apt-get remove vim-common
```

（2）然后重装vim
```
sudo apt-get install vim
```

（3）优化vim配置
为方便使用，需在/etc/vim/vimrc文件后面添加下面三句
```
set nu  #显示行号
syntax on  #语法高亮
set tabstop=4  #tab退四格
```



