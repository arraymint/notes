# 协议和端口

端口为协议的子集

## 协议

协议号是存在于IP数据报的bai首du部的20字节的固定部分，占有8bit。该字段是指出此zhi数据报所携带的dao是数据是使用何种协议，以便目的主机的IP层知道将数据部分上交给哪个处理过程。也就是协议字段告诉IP层应当如何交付数据。

- ICMP 网络控制消息协议
- TCP
- UDP

## 端口

当协议为TCP/UDP时，可设置端口。

端口的作用是让应用层的各种应用进程都能将其数据通过端口向下交付给运输层。

## Q&A

ping采用哪种协议？

ICMP(v4)，协议号为1，不存在端口。

之前对协议和端口联系不懂的时候，还以为任何程序都存在端口，ping不通是因为端口的原因，后来才发现ping采用ICMP协议，没有端口。