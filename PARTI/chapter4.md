# 第四章编码和演化
因为系统需要升级，升级过程如果是在线进行则可能会造成新旧版本的数据和代码同时存在，这时候就会要求数据和代码需要两种兼容：
1. **向前兼容**：老代码兼容新数据结构。
2. **向后兼容**：新代码兼容老数据结构。

其中向前兼容相比之下更难实现。

## 数据编码
数据在内存和硬盘或者传输过程中有不同的表示。内存中的数据具有一定结构，硬盘和传输过程中的数据则是序列化的。两者之间存在一定转换关系，内存中结构化数据变成序列化数据叫**编码**，序列化数据变成结构化数据叫**解码**。

如果使用非三方编码方式，则不同语言无法通用，所以一般有如下一些通用编码方式。
1. **json**： 用的很广，但是没有限制数据类型，而且数据精度也经常会出问题。还有没法对二进制数据编码。
2. **xml**：用的很广，依然没有限制数据类型，没法对二进制编码。
3. **protobuff**：谷歌的协议
4. **thrift**: facebook的协议
5. **avro**: hadoop的协议。

这些协议都比较小，可以帮助前后向兼容，可以支持多语言。数据从一个进程传递到另一个进程一般需要借助
## 数据服务借助数据库
## 借助服务：*rest* 和 *rpc*，
微服务架构的基础，微服务架构的主要目标是使得应用跟容易维护和变动，使其更容易实施和演化。这些微服务叫web服务这种叫法有些混淆：
- 一般用户端的web服务面向大众
- 微服务在内网运行，支持这种调用的服务一般叫中间件
 
有两种最出名的web服务**REST**和**SOAP**：
- REST用url以及http协议，按照这种方式设计的API叫RESTful
- SOAP是一种用xml作为协议的API。

REST协议使用更为广泛，支持更好。
所有这些都基于**RPC**(remote procedure call)，但是RPC有很多问题：
1. 远程请求可能因为网络问题失败，本地请求不会。
1. 远程请求的服务难以调试。
1. 远程请求的运行时间难以掌控。
1. 远程请求传输大object会很困难。
1. 远程请求通过不同编程语言可能会引起变量名风格的不一致。

## 异步信息发送：
异步信息发送，像rpc一样一个应用发送一个应用接收，像数据库一样使用一种叫message broken或者message broker的中间件而不是直接通过网络。它的优点有：
- 当服务不可用时可以缓存起来提高系统可靠性。
- 可以在服务重连后自动发送。
- 发送端不需要知道接收端的ip和端口号。
- 可以一对多发送。
- 发送和接收解耦。

异步信息发送是异步的。比较著名的开源MQ有**RabbitMQ**，**ActiveMQ**, **Apache Kafka**，等等
### 分布式ACTOR架构

## 总结
讨论了
1. 多种编码方法。
2. 前后向兼容。
3. 数据流方式。