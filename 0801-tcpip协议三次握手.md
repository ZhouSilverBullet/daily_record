





fragment这么写，进行封装

![image-20190801102438247](/Users/zhousaito/Library/Application Support/typora-user-images/image-20190801102438247.png)

https://github.com/huanghaibin-dev/CalendarView/issues/505



UI动效

https://blog.csdn.net/bingdianlanxin/article/details/65445184





TCP/IP 三次握手和4次挥手

为什么是三次握手

第一次，客户端发送一个序列号给服务端，服务端然后接收了这个序列号 ，然后 

第二次， 序列号+1 和 自己的序列号  给客户端

第三次，客户端带上服务器的序列号+1 同时可以携带数据进行通信了。



为什么4次挥手(可以是客户端挥手，也可以是服务端挥手)

假设是客户端挥手

第一次， 客户端发送自己的序列号fin 然后告诉服务端 我**要**断开了

第二次，服务端拿这客户端的序列号 ack 告诉客户端说 我知道了

第三次，服务端发送给客户端序列号fin 我已经跟你**传输完成**，我也要和你断开了

第四次，客户端发送ack，我断开了连接

注：其中第一次和第三次可能会同时发送，就相当于已经传输完成了，这样就只有3次挥手了



挥手为什么会是4次而握手为什么只有三次呢

因为挥手的时候双方都有些在写数据，确保数据写入完整性，所以**挥手** 第二次和第三次不能合并再一起

**握手**的话，就是建立安全连接，2次不安全；4次没有必要，因为我第二次就告诉你我已经准备好了，

