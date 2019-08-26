---
title: 如何使用substrate打造web3项目
date: 2019-08-26 23:31:08
tags: substrate 
web3
polkadot
---

# Web3生态圈

![image-20190826170220354](/Users/s1m0n/Library/Application Support/typora-user-images/image-20190826170220354.png)

第零层

**整个****Web3****架构的基础，由两部分组成****:**

- - **p2p** **网络连接层：基于传统互联网协议** **TCP/IP**， **WebSocket**，**DNS** **等等，提供了点对点的连接**

- **跨平台计算指令语言：部分基于传统虚拟机，提供了跨平台的通用计算指令集**

- ![image-20190826170338734](/Users/s1m0n/Library/Application Support/typora-user-images/image-20190826170338734.png)



**第一层**

**建立在第零层之上，提供了分布式计算和交互的功能，由四个组件组成** **:**

- - **去信任** **/** **低信任** **交互协议：去信任或者低信任的交互协议让节点之间可以进行交互，达成共识，也可以理解成是单链协议**
  - **去信任共享安全交互平台：作为共享安全的平台可以让很多小型的应用链共享安全性，达到安全高效去信任化的跨链交流**
  - **分布式数据存储协议：类似于传统的云存储服务，但是建立与去中心化基础之上，让用户真正的能够拥有自己的数据**
  - **临时信息交流协议：提供了去中心化的临时信息交流方式，这类消息是不同于链上交易消息，是不需要长期储存的**

- ![image-20190826170518169](/Users/s1m0n/Library/Application Support/typora-user-images/image-20190826170518169.png)

- 第二层

- **建立于更低的两层协议之上，提供了更高级的功能。目前的第二层协议有六大类，大多都是处于前期开发状态：**

- - **State Channels** **状态通道，链下信息交流，链上最终确认**
  - **Plasma** **协议，解决链上扩容问题**
  - **加密存储，提供端对端数据加密存储方案**
  - **存储激励机制，提供冗余备份存储方案，保障数据能够真正的拥有多个异地备份**
  - **大量运算协议，提供可靠和便宜的运算方案**
  - **分布式私密管理，使用加密算法提供了去中心化分布式的私密管理**

第三层

**第三层为项目开发提供了高级语言和代码库** 

**Protocol-extensible developer APIs & languages** **基于核心协议的开发语言和接口** 

![image-20190826170705130](/Users/s1m0n/Library/Application Support/typora-user-images/image-20190826170705130.png)

第四层

**Web3****技术架构的顶层，让用户可以轻松的使用****Web3****技术**

**Protocol-extensible user-interface cradle** **基于核心协议的用户界面应用**

![image-20190826170744010](/Users/s1m0n/Library/Application Support/typora-user-images/image-20190826170744010.png)

# 波卡生态圈

**波卡生态圈目前实现了****Web3****生态圈中的几个关键组件：**

- **去信任共享安全交互平台：就是波卡主链，作为中继链，为平行链提供了安全的交互平台**
- **去信任** **/** **低信任** **交互协议：各个使用****Substrate****创建的独立链和平行链就属于这部分**
- **部分第二层协议的实现：现在有多个团队包括****Parity****在基于****Substrate****开发****layer 2****第二层的扩容方案**
- **开发语言和代码库：****polkadot.js, ink, Substrate**
- **应用：官方应用就有**  **Polkadot Portal**  **网页钱包，**  **Polkadot Extension**  **浏览器签名插件，** **Parity Signer**  **手机钱包和签名应用。还有大量的第三方应用正在开发**
- ![image-20190826172301369](/Users/s1m0n/Library/Application Support/typora-user-images/image-20190826172301369.png)

# 传统区块链项目架构一览

![image-20190826172452347](/Users/s1m0n/Library/Application Support/typora-user-images/image-20190826172452347.png)

- **示例：用户通过手机钱包发送交易，到交易执行，确认，反馈结果给用户**

![image-20190826172552844](/Users/s1m0n/Library/Application Support/typora-user-images/image-20190826172552844.png)

![image-20190826172608859](/Users/s1m0n/Library/Application Support/typora-user-images/image-20190826172608859.png)

![image-20190826172626284](/Users/s1m0n/Library/Application Support/typora-user-images/image-20190826172626284.png)

![image-20190826172645278](/Users/s1m0n/Library/Application Support/typora-user-images/image-20190826172645278.png)

![image-20190826172702757](/Users/s1m0n/Library/Application Support/typora-user-images/image-20190826172702757.png)

- **事例：新节点加入现有网络**

  ![image-20190826173512398](/Users/s1m0n/Library/Application Support/typora-user-images/image-20190826173512398.png)

  ![image-20190826173550592](/Users/s1m0n/Library/Application Support/typora-user-images/image-20190826173550592.png)

  ![image-20190826173607119](/Users/s1m0n/Library/Application Support/typora-user-images/image-20190826173607119.png)

![image-20190826173621544](/Users/s1m0n/Library/Application Support/typora-user-images/image-20190826173621544.png)

# 安全性与代币经济学

- **好的区块链项目必须要由很好的攻击抗性**
- **没有不透风的墙，也没有无漏洞的软件**
- **攻击成本** **>** **攻击收益** **=** **相对安全**
- **攻击成本** **<** **攻击收益** **=** **绝对不安全**
- **Polkadot: http://research.web3.foundation/en/latest/polkadot/Token%20Economics/**

- **最常见的攻击类型是****Denial of Service****拒绝服务攻击**
- **攻击者发送无用交易填充网络，阻止用户正常交易确认**
- **一个没有稳健的经济体系的网络是很难防范拒绝服务攻击的**
- **平台币不值钱** ➤ **交易费低廉** ➤ **低攻击成本** ➤ **大量攻击** ➤ **平台币更加贬值**
- **解决方案：接入波卡中继链，利用波卡经济体系保障网络安全**

# 如何开发区块链项目

- **分叉现有项目**

- - **快速**
  - **受限与现有项目架构，扩展性有限制**
  - **继承所有安全隐患**

- **全新项目从零开始**

- - **费时费力费钱**
  - **对团队有很高的要求**

- **使用** **Substrate** **框架**

- **由****Gavin Wood****带领的****Parity****团队开发**

- **Substrate****的前身是****Polkadot PoC-2****的版本**

- **目标是成为一个真正意义上的通用区块链开发框架**

- **本身实现了功能性可以与以太坊相比的区块链**

- **现有多个基于****Substrate****的项目**

- - **包括****CENNZnet**

- **可以预见，接下来基于** **Substrate** **的项目会越来越多，而更早一步的掌握和熟练** **Substrate** **的开发技能则能够让你在成功的道路上比别人提前一步**

- **Substrate** **三大特性：**
- ![image-20190826173927544](/Users/s1m0n/Library/Application Support/typora-user-images/image-20190826173927544.png)

- - **可升级：无分叉升级共识逻辑**
  - **高效率：****BABE/Grandpa****混合共识机制、轻节点**
  - **创新性：模块化设计、****Wasm****解释器**

# CENNZnet介绍

- **基于****Substrate****开发**
- **打造一个完整的区块链生态圈，为****dApp****开发者提供一个开发和部署****dApp****的平台**
- ![image-20190826174042953](/Users/s1m0n/Library/Application Support/typora-user-images/image-20190826174042953.png)

PL^G

- **基于****Substrate****的区块链工具包**

- **包含了多个通用模块**

- - **通用资产模块**
  - **交易费模块**

CENNZnet

- - **公链**

  - **包含了大部分****Substrate****提供的模块**

  - - **质押模块**
    - **共识机制模块**
    - **智能合约**

  - **PL^G****所提供的模块**

  - **CENNZnet****核心模块**

  - - **交易所**
    - **加密通讯**

  - dapps

  - - - **端对端加密通讯应用：****Sylo** [**https://www.sylo.io**](https://www.sylo.io/)
      - **身份认证和权限管理应用：****SingleSource**  [**http://mysinglesource.io**](http://mysinglesource.io/)
      - **第三方开发者通过智能合约部署的应用**

  - 

# 展望未来

- - **看到去中心化，去信任化，分布式的应用可以取代大部分传统的中心化应用**

  - **用户拥有真正的选择权**

  - **通过成为提名人维护网络安全和赚取利息**

  - **更多的新星区块链企业**

  - - **托管验证人节点**
    - **区块链银行**
    - **全自动理财服务**

  - **更多的****DAO** **分布式自治组织**

  - **企业和组织更加公开透明**

  - **用户资料更加隐私安全**