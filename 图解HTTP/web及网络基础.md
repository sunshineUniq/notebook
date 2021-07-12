TCP/IP: 网络基础， 是互联网相关的各类协议族的总称

TCP/IP与HTTP的关系： 后者是前者的子集。

protocol: 协议---不同的硬件、操作系统之间的通信的规则

#### 分层管理

TCP/IP按层次分为下面4层： 应用层、传输层、网络层、数据链路层

应用层：提供服务：  如FTP， DNS， HTTP

传输层：数据传输

	- TCP： Transmission Control Protocol 传输控制协议
	-  UDP： User Data Protocol 用户数据报协议

网络层： 选择传输链路

	- 数据包：网络传输最小的单位

网络链路层： 处理硬件部分 exp: 控制操作系统、硬件的设备驱动、NIC、光纤等

#### TCP/IP通信传输流

封装： 发送层层与层之间传输数据，每经过一层打上一个属于该层的首部信息；接收层，每经过一层会把对应的首部去掉

#### 与HTTP密切相关的协议：IP、TCP和DNS

IP协议： 负责传输

IP协议的作用： 传送各种数据包给对方

确保传输的条件： IP 地址、 MAC地址（Media Access Control Address)

IP 地址指明了节点被分配到的地址

MAC 地址：网卡所属的固定地址

IP地址和MAC 地址的关系： 可以进行配对，前者可变，后者基本不会更改

- 使用ARP协议凭借MAC 地址进行通信
  - ARP协议：解析地址，address Resolution Protocol

**没有人能全面掌握互联网中的传输情况**

- 路由选择机制 routing

TCP 协议： 确保可靠性

- 字节流服务： Byte Stream Service
- 大数据分割成数据包，单位是报文段（segment)
- 可靠的传输服务：把数据准确可靠地传递给对方
- 三次握手策略（three-way handshaking): 
  - TCP 协议把数据包送出去后，TCP 一定会确认是否成功送达
  - TCP的标志：SYN（synchronize)和ACK（acknowledgement)

#### URI 和URL

- URI（Uniform Resource Identifier)统一资源标识符（IANA： 统一资源标识符方案）

- URL（Uniform Resource Locator) 统一资源定位符

- URI 用字符串标识某一资源，URL表示该资源的地址，URL 是URI 的子集

- URI 格式： RFC

  ```
  http://user:pass@www.example.jp:80/dir/index.htm?uid=1#ch1
  http:// 协议方案名
  user:pass  登陆信息（认证）可选
  www.example.jp 服务器地址
  80: 服务器端口号  可选
  /dir/index.htm 带层次的文件路径
  uid=1 查询字符串  可选
  ch1 片段标识符   可选
  ```

  

