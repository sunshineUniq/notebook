服务器端

```java
#include <stdio.h>
#include <winsock2.h>
#pragma comment (lib, "ws2_32.lib")  //加载 ws2_32.dll
 
int main(){
	int err;
 
    //初始化 DLL
    WSADATA wsaData;
	printf("Server is waiting............\n");
    WSAStartup( MAKEWORD(2, 2), &wsaData);
 
    //创建套接字
    SOCKET servSock = socket(PF_INET, SOCK_STREAM, IPPROTO_TCP);
 
    //绑定套接字
    sockaddr_in sockAddr;
    memset(&sockAddr, 0, sizeof(sockAddr));  //每个字节都用0填充
    sockAddr.sin_family = PF_INET;  //使用IPv4地址
    sockAddr.sin_addr.s_addr = inet_addr("127.0.0.1");  //具体的IP地址
    sockAddr.sin_port = htons(1234);  //端口
    bind(servSock, (SOCKADDR*)&sockAddr, sizeof(SOCKADDR));
 
    //进入监听状态
    listen(servSock, 20);
 
    //接收客户端请求
    SOCKADDR clntAddr;
    int nSize = sizeof(SOCKADDR);
    SOCKET clntSock = accept(servSock, (SOCKADDR*)&clntAddr, &nSize);
 
    //向客户端发送数据
    char *str = "Hello World!";
    send(clntSock, str, strlen(str)+sizeof(char), NULL);
 
	//接受数据
 
	char recvBuf[100];
	err = recv(clntSock,recvBuf,100,0);
 
	printf("%s\n",recvBuf); //输出接受数据
 
    //关闭套接字
    closesocket(clntSock);
    closesocket(servSock);
 
    //终止 DLL 的使用
    WSACleanup();
 
	system("pause");
    return 0;
}
  
```

  2）客户端代码

```java
#include <stdio.h>
#include <stdlib.h>
#include <WinSock2.h>
#pragma comment(lib, "ws2_32.lib")  //加载 ws2_32.dll
 
int main(){
	int err;
 
    //初始化DLL
    WSADATA wsaData;
 
    WSAStartup(MAKEWORD(2, 2), &wsaData);
 
    //创建套接字
    SOCKET sock = socket(PF_INET, SOCK_STREAM, IPPROTO_TCP);
 
    //向服务器发起请求
    sockaddr_in sockAddr;
    memset(&sockAddr, 0, sizeof(sockAddr));  //每个字节都用0填充
    sockAddr.sin_family = PF_INET;
    sockAddr.sin_addr.s_addr = inet_addr("127.0.0.1");
    sockAddr.sin_port = htons(1234);
    connect(sock, (SOCKADDR*)&sockAddr, sizeof(SOCKADDR));
 
    //接收服务器传回的数据
    char szBuffer[MAXBYTE] = {0};
    recv(sock, szBuffer, MAXBYTE, NULL);
 
    //输出接收到的数据
    printf("Message form server: %s\n", szBuffer);
 
	//发送数据
	err = send(sock,"This is Client", strlen("This is Client")+1, 0);
 
    //关闭套接字
    closesocket(sock);
 
    //终止使用 DLL
    WSACleanup();

    system("pause");
    return 0;
}
```

