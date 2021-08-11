gRPC is very powerful and there is a lot more you can discover by playing around with it yourself 

The example in this tutorial should leave you with a solid fundation.

started by introducing gRPC generally and explaining how it works from protocol buffers down to the client.



```
protoc --dart_out=grpc:lib/src/generated -Iprotos protos/helloworld.proto
```



grpc

基于定义服务的思想，指定可以通过参数和返回类型远程调用的方法

在服务端，服务器实现了这个接口并运行一个grpc服务器来处理客户端的调用

在客户端，客户端有一个存根，它提供与服务器相同的方法

grpc客户端和服务端可以在各种环境中运行和相互通信。



四种服务方法（生命周期）：

+ 一元RPC，客户端向服务器发送单个请求并返回单个响应，就像普通的函数调用一样。

  ```protobuf
  rpc SayHello(HelloRequest) returns (HelloResponse);
  ```

+ 服务器流式RPC，客户端向服务器发送请求并获取一系列消息。客户端从返回的流中读取，知道没有消息。gRPC保证单个RPC调用中的消息排序。

  ```
  rpc LotsReplies(HelloRequest) returns (stream HelloResponse);
  ```

+ 客户端流式RPC，其中客户端写入一系列消息并将它们发送到服务器，再次使用提供的流。一旦客户端完成写入消息，它等待服务器读取他们并返回其响应。gRPC再次保证单个RPC调用中的消息排序。

  ```
  rpc LostsOfGreetings(stream HelloRequest) returns (HelloResponse);
  ```

+ 双向流式RPC，其中双方使用读写流发送一系列消息。这两个流独立运行，因此客户端和服务端可以按照他们喜欢的任何顺序进行读写： 例如，服务器在写入响应之前等待接受所有客户端消息，或者它可以交替读取消息，然后写入消息，或者其他一些读写的组合，保留每个流中消息的顺序。

  ```
  rpc BidiHello(stream HelloRequest) returns (stream HelloResponse);
  ```

截止日期/超时：gRPC允许客户端指定他们愿意等待RPC完成多长时间，然后RPC会因DEADLINE_EXCEEDED错误而终止。在服务端，服务器可以查询特定RPC是否超时，或者完成RPC还剩多长时间。

RPC终端：在gRPC中，客户端和服务端都独立的自行确定调用是否成功，他们的结果不一致

取消RPCs：客户端和服务端可以随时取消RPC，取消会立即终止RPC，这样就不会进一步工作。emmmm这不是“undo”，取消之前所做的更改不会回滚。

元数据：关于特定RPC调用的信息（如身份验证详细信息），以键值对列表的形式，其中键是字符串，值通常是字符串（也可以是二进制数据）。元数据对gRPC本身不透明，它允许客户端向服务端提供与调用相关的信息，反之亦然

信道： 提供主机到端口上的gRPC服务器的连接，并在创建客户端存根时使用。客户端可以指定信道参数来修改gRPC的默认行为例如打开和关闭消息压缩。信道有状态，包括连接和空闲



使用场景：

​	low latency, highly scalable, distributed systems.

​	developing mobile clients which are communicating to a cloud server.

​	designing a new protocol that needs to be accurate, efficient and language independent.

​	layered design to enable extension eg. authentication, load balancing, logging and monitoring etc.





 