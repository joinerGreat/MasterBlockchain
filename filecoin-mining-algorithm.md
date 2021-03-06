# Filecoin挖矿算法

<!-- TOC -->

- [Filecoin挖矿算法](#filecoin%E6%8C%96%E7%9F%BF%E7%AE%97%E6%B3%95)
    - [存储挖矿](#%E5%AD%98%E5%82%A8%E6%8C%96%E7%9F%BF)
        - [抵押](#%E6%8A%B5%E6%8A%BC)
        - [接收订单](#%E6%8E%A5%E6%94%B6%E8%AE%A2%E5%8D%95)
        - [密封](#%E5%AF%86%E5%B0%81)
        - [证明](#%E8%AF%81%E6%98%8E)
    - [检索挖矿](#%E6%A3%80%E7%B4%A2%E6%8C%96%E7%9F%BF)
        - [接收订单](#%E6%8E%A5%E6%94%B6%E8%AE%A2%E5%8D%95)
        - [发送](#%E5%8F%91%E9%80%81)

<!-- /TOC -->

Filecoin其实存在于IPFS（InterPlanetary File System，星际文件系统）的激励层，而IPFS能够提供去中心化的数据存储和访问功能。因此，Filecoin需要大量的数据读写操作，这就要求矿工的挖矿过程进行数据读写操作。Filecoin的挖矿共分为存储挖矿和检索挖矿两部分，分别进行对数据的存储和检索工作。

## 存储挖矿

存储挖矿分为四部分：抵押、接收订单、密封和证明。

### 抵押

抵押的主要目的是为了保证存储矿工能够为网络提供存储服务。存储矿工首先在区块链上进行一次抵押交易，该交易主要通过保存一个抵押品来抵押存储矿工的存储容量。而当存储矿工成功生成了他们提交数据的存储证明，那么存储矿工先前的抵押品就可以退回。如果存储矿工未完成相应的存储证明，那么将会失去部分数量的抵押品。一旦区块链上（分配表）出现了一个抵押交易，那么矿工就可以向存储市场提供他们的存储空间，并且可以设置一定的价格，并生成一个卖单挂到市场的订单账本中。

### 接收订单

接收订单的主要目的是为了从存储市场中获取存储请求。系统就会检查矿工在存储市场上的卖单是否与对应的来自客户端的买单相匹配。一旦卖单和买单想匹配，那么客户就会将自己的数据发送给存储矿工。而实际上，矿工收到的是一个个数据片。当存储矿工收到数据片后，就把数据存储到自己的硬盘中，与此同时，矿工和客户端都会签署一个交易订单，并将之提交到区块链上。

### 密封

密封的目的是为未来的证明准备数据片。存储矿工的存储空间被分为几个扇区，每一部分都包含分配给矿工的数据片。网络通过分配表对每个存储矿工的各个存储扇区进行跟踪。当一个存储扇区存储满了之后，该扇区就会被密封。密封操作过程很慢，它需要依次将一个扇区的数据转换保存为一个副本。而每个数据的物理拷贝都与存储矿工的公钥相关联。

### 证明

存储矿工需要证明他们存储了提交的数据片。当存储矿工被分配到一个数据的时候，他们必须重复生成数据副本证明，以此来保证存储矿工确实保存了数据。该证明将推送到区块链中，并被全网验证。

## 检索挖矿

检索挖矿分为两部分：接收订单和发送。

### 接收订单

索引矿工从索引市场中获取数据请求。索引矿工通过向网络中传播卖单来宣布他们的数据片。他们设置一个价格，然后添加一个卖单到市场的订单账本中。然后，索引矿工检查他们的订单是否与对应的客户买单相匹配。

### 发送

一旦订单匹配，索引矿工将会发送他们的数据片给客户端。客户端收到数据片后，矿工和客户端签署一个交易订单并提交到区块链中。
