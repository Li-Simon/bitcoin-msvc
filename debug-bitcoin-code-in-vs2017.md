# **下载与编译**

1. Download bitcoin code from Github

[https://github.com/Li-Simon/bitcoin-msvc](https://github.com/Li-Simon/bitcoin-msvc)

2.编译：

1. 用VS2017打开bitcoin solution,再在每个project中 include boost库就可以了。
2. 编译的时候会出错，但是只要把X64改成X86就可以了。

![](/Debug  Bitcoin code in VS2017/import.png)

3.编译的结果；最终会在debug 文件夹下生成bitoind.exe bitcoin-cli.exe等exe文件![](/Debug  Bitcoin code in VS2017/import2.png)

4.Debug

右击 Bitcoind--&gt;debug-&gt;start new instance，则可以一步步debug  Bitcoind\(Bitcoin server端\)

从main函数一直debug下去，可以知道BTC 服务端是怎么起来的，比如解析命令行参数， 读取配置文件bitcoin.cong, 配置日志，安装网络环境，网络初始化，加载区块链数据，导入区块，启动节点服务，监听网络P2P请求（比如接受来自比特币客户端的请求）               一本好的参考教程是 申屠青春主编的《区块链开发指南》，详见4.2.2节初始化与启动

![](/Debug  Bitcoin code in VS2017/import3.png)

# **通过debug.log来了解代码逻辑**

1. 只有启动服务端Bitcoind.exe， 才可以启动客户端Bitcoin-cli.exe 否则会出现找不到服务器的错误
   ![](/Debug  Bitcoin code in VS2017/import4.png)

1. .三种bitcoin network
   1. 主网络:就是真正比特币交易的网络，如果不加参数默认是主网络
   2. testnet：用来测试比特币的网络，里面也需要挖矿，也有交易
      1. 通过bitcoind -testnet启动服务端，客服端则用bitcoin-cli -testnet来运行
   3. regtest：在本地搭建的一个完整的网络，挖矿难度极低
      1. 与testnet类似的启动
   4. 这些有关bitcoin的术语可以在https://bitcoin.org/en/glossary/regression-test-mode中进行查询
2. 默认的debug输出路径是C:\Users\pili\AppData\Roaming\Bitcoin，debug.log就是运行bitcoind的日志文件，当然，不同网络存放的debug.log路径不同，比如testnet就存放在C:\Users\pili\AppData\Roaming\Bitcoin\testnet3下
3. -debug 输出更多的debug信息
   1. 通常只输出一些主要的debug信息，如果在命令行中加入-debug参数，如：bitcoind -testnet -debug则可以输出完整的日志文件



