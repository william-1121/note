**gRPC**应用程序使用 **protocol buffer** 进行服务定义和数据序列化，代码使用 **proto3**



#### 一 、Protocol Buffer Compiler Installation：

+ 使用包管理器安装

```
$ apt install -y protobuf-compiler
$ protoc --version  # Ensure compiler version is 3+
```



+ 安装预编译的二进制文件

1. 使用命令下载版本 （官网 [github.com/google/protobuf/releases](https://github.com/google/protobuf/releases) ），

```
$ PB_REL="https://github.com/protocolbuffers/protobuf/releases"
$ curl -LO $PB_REL/download/v3.15.8/protoc-3.15.8-linux-x86_64.zip
```

2. 解压

```
$ unzip protoc-3.15.8-linux-x86_64.zip -d $HOME/.local
```

3. 更新环境变量

```
$ export PATH="$PATH:$HOME/.local/bin"
```





#### 二、 Dart plugin for the protocol compiler:

1. Install  `proc-gen-dart`

   ```
   $ dart pub global activate protoc_plugin
   ```

   

2. Update `PATH`  so that the `protoc` compiler can find the plugin:

   - *just in your **active** terminal session*

   ```
   $ export PATH="$PATH:$HOME/.pub-cache/bin"
   ```

   注：若使用上述命令更新路径后，仅限当前项目

   

   - *for **future** terminal sessions*

   Home目录下有个**.bashrc**文件，打开它，把上面的命令复制到该文件的最后一行，保存即可

   打开终端 输入env 在PATH中可见

   或使用下面的命令行

   ```
   echo 'export PATH="$PATH:$HOME/.pub-cache/bin"' >> ~/.bashrc
   ```

   

