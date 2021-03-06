## RPC

### 成熟的 RPC 框架方案

* Thrift
    - [x] 拥有功能强大的代码生成引擎
    - [x] 非常广泛的语言支持
    
        > C++, C#, Cocoa, Erlang, Haskell, Java, Ocami, Perl, PHP, Python, Ruby, Smalltalk
    
    - [x] 规范的描述文件（ IDL ）
    - [x] 基于 `SOCKET` 的通讯方式、
    - [x] 实现了多线程（`TThreadPolServer`）、单线程非阻塞 `IO`（`TNonBlockingServer`）、多线程非阻塞 `IO`（`THsHaServer`）
    - [x] 实现了最高效的二进制序列化协议 `TCompactProtocol`，但并不支持所有语言
    - [x] 成熟在开源软件
    - [ ] 需要先确定好他的数据结构，当数据结构发生变化时，必须重新编辑 `IDL` 文件
    - [ ] `RPC` 方法非线程安全

* gRPC
    - [x] 使用 `HTTP/2` 协议
    - [x] 使用 `ProtoBuf`（`Protocol Buffers`） 作为序列化工具
    
        > 类似 `XML` 把数据结构信息，以某种格式保存起来。主要用于数据存储、传输协议格式等场合
    
    - [x] 天生适合移动端到服务器端的通讯
    - [x] 和 `REST` 一样遵循 `HTTP` 协议
    - [x] 和 `REST` 不同的是 `gRPC` 使用了静态路径来提高性能
    - [x] 用格式化的错误码代替了 `HTTP` 的状态码来标识错误
    - [x] 提供了集群服务
    - [ ] 某些情况下在性能方面较 `Thrift` 差

* RMI
    - [x] 基于 `JAVA` 远程方法协议
    - [x] `JAVA` 的原生序列化
    - [x] 面向对象
    - [x] 非常高效稳定，特别是在数据结构复杂、数据量大的情况下
    - [ ] 不能跨语言
    - [ ] 只能通过 `RMI` 协议来进行访问
    - [ ] 无法穿透防火墙

* Hessian
    - [x] 基于 `Binary-RPC` 协议实现（自定义串行化机制将请求序列化和反序列化，产生和处理二进制流）
    - [x] 基于 `HTTP` 协议传输数据
    - [x] 由自身的 `API` 发起和接收请求
    - [x] 简单易用，面向接口，无需配置防火墙
    - [x] 轻量级，效率高，复杂对象序列化速度仅次于 `RMI`，简单对象序列化优于 `RMI`
    - [ ] 缺乏安全机制，传输没有加密处理
    - [ ] 异常机制不完善
    - [ ] 事务处理欠缺

* Hprose
    - [x] 动态的 `RPC`
    - [x] 支持的语言众多，兼容性较好
    - [x] 文档齐全
    - [x] 集成 `workerman` 的 `workerman-thrift-rpc` 框架
    - [ ] 仅是功能更强大的 `Web Service`

        > 基于 `SOAP` 消息格式的 `Web Service` 在性能和安全方面已经落后了

* Dubbo
    - [x] 分布式服务框架
    - [x] 高性能，多节点自发现远程调用
    - [ ] 开源后社区活跃度较低

### RPC 和传统的 cURL 比较

* 传统的远程调用如 `cURL` 是基于 `HTTP` 协议，简单、粗暴、超强的跨平台性
* `RPC` 框架则会基于 `tcp` 或者更底层的协议，在传输方式和序列化上有更多的优势

    > `TCP` 是传输层协议，`HTTP` 是应用层协议，应用层在传输层之上

* 所以传统的 `cURL` 方式在高并发的情况下，阻塞式的 `IO` 明显已经支撑不了业务需求
* 所以 `cURL` 和 `RPC` 的区别主要在于以下因素
    * 通讯协议
    * 序列化方式
    * 资源描述（接口描述）
    * 安全


### Thrift

#### 简介

> `Thrift` 是一个跨语言的服务部署框架，由 `facebook` 在 `2007` 年开发并贡献到 `apache` 基金，与 `2008` 年进入 `apache` 开源项目  
> `Thrift` 是通过中间接口语言 `IDL` 来定义接口和所需数据的类型，然后通过编译器生成不同语言的相关代码，从而实现跨语言的支持

#### 客户端流程

* 创建 `Socket`
    
    - `TSocket` - 采用 `TCP`/`Socket` 进行数据传输，阻塞型客户端，采用系统函数 `read` 和 `write` 进行读写数据（`BIO`）
    - `TNonblockingSocket` - 非阻塞客户端（`NIO`）
    
        > `BIO`（同步阻塞），一个连接开启一个线程  
        > `NIO`（同步非阻塞），不在需要为每个连接创建单独的线程，基于 `Reactor`，一个请求开启一个线程
        
        > 连接和请求的区别在于是否有 `IO` 请求

* 创建 `Transport` 传输控制

    - `TSSLSocket` - 继承 `TSocket`，阻塞型 `Socket`, 　用于客户端，采用 `openssl` 的接口进行读写数据
    - `THttpTransport` - 采用 `HTTP` 传输协议进行数据传输
    - `TFileTransport` – 采用文件形式进行传输
    - `TMemoryTransport` – 将内存用于 `IO`，`Java` 实现时内部实际使用了简单的 `ByteArrayOutputStream`
    - `TZlibTransport` – 使用 `zlib` 进行压缩，与其他传输方式联合使用。当前无 `Java` 实现
    - `TFramedTransport` – 以 `frame` 为单位进行传输，非阻塞式服务中使用。类似于 `Java` 中的 `NIO`
    - `TFastFramedTransport` - 与 `TFramedTransport` 相比，始终使用相同的 `Buffer`，提高了内存的使用率
    - `TSaslClientTransport` - 提供 `SSL` 校验

* 在 `Transport` 传输控制的基础上创建 `Protocol` 传输方式

    > 必须与服务端 `Protocol ` 保持一致
    
    - `TBinaryProtocol` – 二进制格式
    - `TCompactProtocol` – 压缩格式
    - `TDenseProtocol` - 继承 `TCompactProtocol`，不包含 `meta` 信息
    - `TJSONProtocol` – `JSON` 格式
    - `TSimpleJSONProtocol` – 提供 `JSON` 只写协议, 生成的文件很容易通过脚本语言解析

* 在 `Protocol ` 传输方式的基础上创建 `Client` 客户端

* 开启 `Transport` 传输

* `Client` 客户端调用 `Service` 服务端

* 关闭 `Client` 客户端

#### 实现的服务模式

- [x] `TSimpleServer` - 简单的单线程服务模型，一般用于测试
- [x] `TThreadedServer` – 多线程服务模型，使用阻塞式 `IO`，每个请求创建一个线程
- [x] `TThreadPoolServer` – 多线程服务模型，使用标准的阻塞式 `IO`，预先创建一组线程处理请求
- [x] `TThreadedSelectorServer` 允许你用多个线程来处理网络 `IO`，它维护了两个线程池（网络 `IO` 处理线程池、请求处理线程池）
- [x] `TNonblockingServer` – 多线程服务模型，使用非阻塞式 `IO`
- [x] `THsHaServer` - 半同步半异步的服务模型，一个单独的线程用来处理网络 `IO`，一个 `worker` 线程池用来进行消息的处理

#### 服务端流程

* 基于实现的服务模式创建 `Processor` 处理器

* 创建 `Socket`

    - `TServerSocket` - 阻塞型 `Socket`，用于服务器端，`accecpt` 到的 `Socket` 类型都是 `TSocket`（阻塞型）
    - `TNonblockingServerSocket` - 非阻塞型 `Socket`，用于服务器端 (`NIO`)

* 创建 `Transport` 传输控制
    
    - `TSaslServerTransport` - 提供 `SSL` 校验

* 在 `Transport ` 传输控制的基础上创建 `Protocol` 传输方式

    > 必须与客户端的 `Protocol` 保持一致

* 在 `Protocol ` 传输方式的基础上创建 `Service` 服务端

* 开启 `Transport` 传输

* `Service` 服务端进行相关处理

* 关闭 `Service ` 服务端

#### 数据类型

**基本数据类型**

- [x] `bool` - 布尔值
- [x] `byte` - 有符号字节
- [x] `i16` - 16 位有符号整型
- [x] `i32` - 32 位有符号整型
- [x] `i64` - 64 位有符号整型
- [x] `double` - 64 位浮点型
- [x] `string` - 编码无关的文本

**Struct**

* 可以嵌套，但不能嵌套自身
* 其成员有明确类型
* 成员是被正整数编号过的，其中的编号使不能重复的，这个是为了在传输过程中编码使用
* 成员分割符可以是逗号或分号，并且可以混用，为了规范可以确定使用其中一种
* 字段会有 `optional` 和 `required` 之分和 `protobuf` 一样，但是如果不指定则为无类型，但是在序列化传输的时候也会序列化进去，`optional` 是不填充则不会被序列化，`required` 是必须填充也必须序列化
* 每个字段可以设置默认值
* 同一文件可以定义多个 `struct`，也可以定义在不同的文件，进行 `include` 引入

```
struct Message
{
    1: required string msg,     // 字段必须填写
    2: optional i32 type = 0;   // 默认值
    3: i32 time                 // 默认字段类型为 optional
}
```

**Containers**

* `list<t>` - 元素类型为 `t` 的有序表，容许元素重复

    > 对应 `C++` 的 `vector`，`Java` 的 `ArrayList` 或者其他语言的数组
    
* `set<t>` - 元素类型为 `t` 的无序表，不容许元素重复

    > 对应 `C++` 中的 `set`，`Java` 中的 `HashSet`，`Python` 中的 `set`
    
* `map<t, t>` - 键类型为 `t`，值类型为 `t` 的 `kv` 对，键不容许重复

    > 对用 `C++` 中的 `map`，`Java` 的 `HashMap`，`PHP` 对应 `array`，`Python`/`Ruby` 的 `dictionary`
    

```
struct User {
    1: map<Numberz, UserId> user_map,
    2: set<Numberz> num_sets,
    3: list<Stusers> users
}
```

**Enum**

> 枚举常量必须是 32 位的正整数

* 编译器默认从 0 开始赋值
* 可以赋予某个常量的某个整数
* 允许常量是十六进制整数
* 末尾没有分号
* 给常量赋缺省值时，使用常量的全称

```
enum Operation {
    CMD_OK = 0,
    CMD_NOT_EXIT = 2000,
    CMD_EXIT = 2001,
    CMD_ADD = 2002
}

struct Student {
    1: required i32 userId;
    2: required string userName;
    3: optional EnOpType cmd_code = EnOpType.CMD_OK;
    4: optional string language = "english"
}
```

**Exception**

> `Exception` 几乎与 `Struct` 一致，使用 `exception` 关键字定义，而且异常是继承每种语言的基础异常类

```
exception EHandler {
    1: i32 errorCode,
    2: string message,
    3: StUser userinfo
}
```

**Services**

> `Services` 的定义方法在语义上等同于面向对象语言中的接口  
> `Thrift` 编译器会产生执行这些接口的 `client` 和 `server stub`

```
service Common {
    void ping(),
    bool postTweet(1: Student user);
    Student searchTweets(1:string name);
    oneway void zip()
}
```

**Namespace**

> `Thrift` 中的命名空间类似于 `C++` 中的 `namespace` 和 `Java` 中的 `package`，它们提供了一种组织代码的简便方式  
> 名字空间也可以用于解决类型定义中的名字冲突

```
namespace cpp api
namespace java api
namespace php api
```

**Includes**

> 便于管理、重用和提高模块性/组织性，常常分割 `Thrift` 定义在不同的文件中  
> 包含文件搜索方式与 `C++` 一样  
> `Thrift` 允许文件包含其它 `Thrift` 文件，用户需要使用 `Thrift` 文件名作为前缀访问被包含的对象

```
include "test.thrift"   
...
struct StudentSearchResult {
    1: in32 uid; 
    ...
}
```

#### IDL

> `IDL` 都是基于 `Thrift Type` 书写的文件，以 `.thrift` 为后缀命名

```
struct User{
    1: i64 id,
    2: string name,
    3: i64 timestamp,
    4: bool vip  
}

service UserService{
    User getById(1: i64 id)
}
```