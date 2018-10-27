---
title: TCP通信-客户端和服务端代码
date: 2018-10-27 21:14:19
tags: TCP通信
categories: Linux相关
---

### 客户端：

```c
#include <stdio.h>
#include <WinSock2.h>
  
#pragma comment(lib,"ws2_32.lib")
  
int main()
{
    SOCKET soc;
    SOCKADDR_IN serverAddr;
    SOCKADDR_IN clientAddr;
  
    unsigned char buf[1024];
  
    WSADATA wsa;
    WSAStartup(MAKEWORD(1,1),&wsa);
  
    if ((soc = socket(AF_INET,SOCK_STREAM,IPPROTO_TCP)) <= 0)
    {
        printf("create socket fail!\n");
        return -1;
    }
  
    serverAddr.sin_family = AF_INET;
    serverAddr.sin_port = htons(4999);
    serverAddr.sin_addr.S_un.S_addr = inet_addr("127.0.0.1");
  
    if (connect(soc,(SOCKADDR *)&serverAddr,sizeof(serverAddr)) != 0)
    {
        printf("connect fail!\n");
        return -1;
    }
  
    while(1)
    {
        scanf("%s",buf);
        if (send(soc,(const char *)buf,strlen((const char *)buf)+1,0) <= 0)
        {
            printf("Error!\n");
        }
    }
  
    getchar();
    return 0;
}
```

### 服务端：

```c
#include <stdio.h>
#include <WinSock2.h>
 
#pragma comment(lib, "ws2_32.lib")
 
#include <iostream>
using namespace std;
 
int main()
{
    const int BUF_SIZE = 64;
 
    WSADATA wsd; //WSADATA变量
    SOCKET sServer; //服务器套接字
    SOCKET sClient; //客户端套接字
    SOCKADDR_IN addrServ;; //服务器地址
    char buf[BUF_SIZE]; //接收数据缓冲区
    char sendBuf[BUF_SIZE];//返回给客户端得数据
    int retVal; //返回值
 
    //初始化套结字动态库
    if (WSAStartup(MAKEWORD(2,2), &wsd) != 0)
    {
        cout << "WSAStartup failed!" << endl;
        return 1;
    }
    //创建套接字
    sServer = socket(AF_INET, SOCK_STREAM, IPPROTO_TCP);
    if(INVALID_SOCKET == sServer)
    {
        cout << "socket failed!" << endl;
        WSACleanup();//释放套接字资源;
        return  -1;
    }
    //服务器套接字地址
    addrServ.sin_family = AF_INET;
    addrServ.sin_port = htons(4999);
    addrServ.sin_addr.s_addr = INADDR_ANY;
    //绑定套接字
    retVal = bind(sServer, (LPSOCKADDR)&addrServ, sizeof(SOCKADDR_IN));
 
    if(SOCKET_ERROR == retVal)
    {
        cout << "bind failed!" << endl;
        closesocket(sServer); //关闭套接字
        WSACleanup(); //释放套接字资源;
        return -1;
    }
    //开始监听
    retVal = listen(sServer, 1);
    if(SOCKET_ERROR == retVal)
    {
        cout << "listen failed!" << endl;
        closesocket(sServer); //关闭套接字
        WSACleanup(); //释放套接字资源;
        return -1;
    }
    //接受客户端请求
    sockaddr_in addrClient;
    int addrClientlen = sizeof(addrClient);
    sClient = accept(sServer,(sockaddr FAR*)&addrClient, &addrClientlen);
    if(INVALID_SOCKET == sClient)
    {
        cout << "accept failed!" << endl;
        closesocket(sServer); //关闭套接字
        WSACleanup(); //释放套接字资源;
        return -1;
    }
 
    while(true)
    {
        //接收客户端数据
        ZeroMemory(buf, BUF_SIZE);
        retVal = recv(sClient, buf, BUF_SIZE, 0);
        if (SOCKET_ERROR == retVal)
        {
            cout << "recv failed!" << endl;
            closesocket(sServer); //关闭套接字
            closesocket(sClient); //关闭套接字
            WSACleanup(); //释放套接字资源;
            return -1;
        }
        if(buf[0] == '0')
        break;
        cout << "客户端发送的数据: " << buf <<endl;
        cout << "向客户端发送数据: " ;
        cin >> sendBuf;
        send(sClient, sendBuf, strlen(sendBuf), 0);
    }
    
    //退出
    closesocket(sServer); //关闭套接字
    closesocket(sClient); //关闭套接字
    WSACleanup(); //释放套接字资源;
 
    return 0;
}
```

