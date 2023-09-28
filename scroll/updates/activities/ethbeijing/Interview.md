本次 ETHBeijing 黑客松共有 57 个团队报名参赛，参加 Public Goods，Layer 2，Open Reserach 三个主赛道，Scroll 赞助了其中的 Layer2 赛道，以及额外的在Scroll上部署合约的Bounty。

最终 Layer2 赛道共有 16 支参赛队伍报名，Scroll Bounty也有 16 支参赛队伍选择。此外报名 Public Goods 和 Open Reseach 的参赛队伍许多也尝试或研究了 Scroll 的 Alpha 测试网。

Scroll CN 对其中的一些参赛项目进行了专访，其中一些项目部署在 Scroll 的 Alpha 测试网上，一些项目给 Scroll 的 Alpha 测试网贡献了工具，一些可能借助  Scroll 的 Alpha 测试网开发了创新型的应用。他们可能没有入选最终的Demo Day，他们可能因为忙中出错，错过了提交时间，但他们都是这次 ETHBeijing 最了不起的 Hackers。

# GasLockR

## 简单介绍一下自己的团队和项目?

我们的团队由四人组成，分别是我，贤渊，啸天，Alex。队伍是线上组建的，发布组队信息 后，直到开赛日下午，四人才第一次碰面开始讨论。大家本身在各自技术栈是很有经验的，对 这个项目的idea非常有热情和喜爱，因此也能有默契地配合，短短三天高质量的完成了项目的 从0到1。除了Alex还在Oxford上学外，其他人都是刚毕业不久，我26岁但已经是团队里年龄最 大的人了，大家都是对web3和加密世界有信仰的。 项目的idea是我思考了很久并和队友们讨论最终细化的，初心是想构建一个有利于以太坊和L2 生态并能不断成长的产品。项目是围绕三个现有问题来探讨的:目前L2越来越被依赖，但L2针 对gas价格并不能提供很好的服务水平协议(SLA);另外，钱包必须有启动资金来支付gas才能 开始链上交互，造成了先有鸡还是先有蛋的问题;以及每笔交易需要思考和确认当下的gas价 格，这类UX对web3新用户非常不友好并造成了困惑。 GasLockR提供了一种有效的方法来对冲gas价格波动上涨的风险，我们利用ZK协处理器来获取 历史gas价格，并根据实时更新的金融模型，来提供可验证的gas定价。它可以用作链上基础设 施来构建协议和服务，从而解决上述的可靠性和用户体验等问题。我们提出GasFi一词，并把 GasLockR作为第一个免信任的GasFi衍生品协议。借助GasLockR，其他钱包或服务如帐户抽象 (ERC-4337)将能够为其用户提供 SLA，从而让用户和组织依赖 L2，建立对生态的信任。基于 GasLockR，我们做了一款针对gas价格的保险服务作为MVP，来展示其作为金融基础设施的性 能:用户可以通过web GUI支付少量保费，来保护未来一段时间L2 gas价格波动的风险。

## 这次的项目和 Scroll 有什么联系?

在未来大多数链上活动将会在L2进行，而zk-Rollup是L2的未来。根据前文的介绍，我们 是希望GasLockR能更好地服务L2生态，尤其是Rollup，GasLockR中的R也有代表Rollup的 含义。在目前已有的zk-Rollup中，Scroll的zkEVM是最能原生兼容以太坊应用程序和工具 的设计。因此我们希望GasLockR能在未来首先与Scroll生态合作推广。

## 为什么会部署在 Scroll 的 Alpha 测试网上呢?

我们希望把产品部署在zk-Rollup生态中进行测试，而由于Scroll的zkEVM的兼容性，我们 选择将产品部署到Scroll来测试产品的通用性和运行。另外，Scroll对于开发者从以太坊 L1迁移的要求非常低，因此可以免去许多学习成本。

## 测试网部署的体验如何，部署过程中有没有遇到什么问题

测试网总体的部署体验是良好的，符合预期效果。其中有一个小问题，GasLockR合约中用 到了solidity中的关键字block.basefee，成功部署合约后，但在调用时返回了错误: Returned error: {"jsonrpc":"2.0","error":"invalid opcode: BASEFEE","id":3338453673810132}。对此问题，我们已与Scroll的开发人员积极进行了 沟通，并会不断跟进。

## 黑客松之后项目的项目规划是怎么规划的?

比赛结束后，许多评委和开发者来与我们交流，给项目提了很多宝贵的建议，我们会认真 考虑并完善功能。此外，我们会不断推进GasLockR项目的落地，与链上钱包和其他项目进 行合作，来用作链上基础设施构建更多服务。黑客松只是一个开始，请期待GasLockR接下 来的成长，欢迎大家关注官方推特@gaslockr，也欢迎所有感兴趣的朋友们合作来共建更 好的web3生态!

## 项目链接
- Demo: https://gaslockr.azurewebsites.net/
- Demo视频：[https://www.youtube.com/watch?v=fprzRbCeay4](https://www.youtube.com/watch?v=fprzRbCeay4)
- Github：[https://github.com/GasLockR](https://github.com/GasLockR)

# 九转以太坊

## 简单介绍一下自己的团队和项目？
我们是九转以太坊团队，团队成员均来自山东大学，由两位博士生，一位硕士生以及一位本科生组成。我们的项目叫做 Deep Stack Fantasy。我们从令智能合约开发者深痛恶绝的 “stack too deep” 问题——即只允许同时使用最多16个变量，否则编译不通过——出发，旨在扩展 EVM 对栈的访问限制，并修改 Solidity 编译器以消除该问题。本项目能够增强开发者编程体验，以更有效率的方式编写合约逻辑，把精力放在更高层的逻辑上，而不是纠结如何把变量个数减少到16个以内这种问题。Web3 社区的发展壮大与各开发者愿意投入的时间和精力关系成正比，而增强开发体验无疑会增加开发者的粘性。
 
## 这次的项目和 Scroll 有什么联系？
Sroll 作为 Layer2 的 zkEVM 解决方案，需要完全兼容 EVM，因此与以太坊共享智能合约工具链不够友好、表达能力受限的问题。Scroll 基于零知识证明方案，扩展 EVM 栈访问限制对性能的影响可以忽略不计，并且该改动是向下兼容的，因此与原版 EVM 相比，Scroll可以几乎“免费”地增强合约表达能力，提升开发体验，而无需付出性能或兼容性代价。
 
在本次黑客松比赛中，我们与 Scroll 的工程师讨论了零知识证明实现细节，尤其是确定了 zkevm-circuits 中， stack pointer offset 与零知识证明电路体积的关系是恒定的，因此扩展EVM栈访问限制并不会带来性能负担，确定在 zkEVM 上实现本项目是完全可行的。
 
该改动是对 EVM 指令进行扩展，需要修改 Scroll 本身的代码并等待网络中的节点升级。
 
## 黑客松之后项目是什么样的规划？
 
本次黑客松比赛期间，我们完成了对以太坊原版 EVM 的修改，并大致完成了 Solidity 编译器的修改。黑客松之后，我们首先需要做的是将“invalid jump”的问题解决，以便使修改版编译器产生的字节码能够完美在原版 EVM 运行。完成此项修补工作后，我们计划对Scroll的零知识证明的代码进行修改，以实现我们对 EVM 新增的两条扩展指令的功能。与此同时，尝试搭建 Scroll 测试链以完成对该项目的调试工作。当然，这些后续工作离不开与 Scroll 工程师的技术交流。最终目标是，使Solidity开发者在 Scroll 上开发、部署合约时摆脱16个变量的制约，增强其开发体验，以此提升社区凝聚力。

## 项目链接
- Demo
	- [Remix-IDE with DSF Solidity Compiler](https://remix.ethereum.org/#lang=en&optimize=false&runs=200&evmVersion=null&version=https://124.220.19.52/soljson.js)
	- [Example sol file](https://124.220.19.52/test100.sol)
	- [DSF Solidity Compiler (solijson.js)](https://124.220.19.52/soljson.js)
- Demo 视频： https://youtu.be/AiOXepNjYzw
- Github
	- [solidity-deep-stack](https://github.com/deep-stack-fantasy/solidity-deep-stack)
	- [go-ethereum-deep-stack](https://github.com/deep-stack-fantasy/go-ethereum-deep-stack)


# Honeypot Finance

## 简单介绍一下自己的团队和项目？
大家好，我们是base在加拿大的团队Honeypot Finance，我们团队最早来自BERA的孵化器投资，但是鉴于BERA的进展比较慢，我们可能fork我们的项目首发在Scroll上！

我们正在打磨用governance去管理合约升级的流程基础，使用这个流程与社区一起共同投票去build+update我们的DAPPs。我们开发团队率先构建了一个DEX在上面，很快就将推出产品，让大家一起来优化DEX、决策奖励机制和构建更多的DAPPs :-)。

我们说安全问题本质是信任问题，“合约不可更改”想解决的是信任问题，但是governance也能解决信任问题后，反过来我们希望合约可以小步迭代敏捷开发，最终成长成链上的巨无霸。

本次我们参加ETH-Beijing hackathon，做了一个有趣的开源的基金管理工具“y=e^x”，以基金的形式来持有一系列的DeFi合约，例如创建市商流动性池、借贷合约、到其他的DEX上采买资产等。我们的观点是个人投资人做LPer（流动性提供者）被动交易太容易亏损了，还是得形成组织，主动管理并且有完善的风控措施才行。相关代码我们发布在[GitHub](https://github.com/KAndHisC/yex)上，欢迎大家一起献言献策，贡献代码！

  
## 这次的项目和 Scroll 有什么联系？

不得不说，这次参赛最大的收获就是了解到了咱们Scroll社区和相关技术！我们这次比赛作品就是部署在Scroll上，后续也会在Scroll上继续维护。

我们希望能给Scroll社区带来一些有趣的想法，贡献我们的价值，也非常看好Scroll社区的技术积淀和用户规模。借助Scroll提供的扩容方案大幅降低gasfee，对DEX的健康运作是非常有利的，又能提升大家参与投票的积极性，建立一个公平有序的社区。

  
## 如果是部署在 Scroll 的 Alpha 测试网上，是什么考虑呢？
原因有两个：

-   低gasfee！对DEX有了解的同学应该知道，gasfee和toxic flow是正相关性，因为高gasfee导致的高交易成本阻碍了不知情的普通用户发生交易。另一方面，投票率和gasfee负相关，花一大笔钱去投票，对资产较少的用户来说非常不划算，最终会影响governance的公平性，甚至变成寡头机制。   
-   迁移到Scroll没有任何负担！在Web3这样轻资产的团队里，最大的成本就是技术人员的薪酬成本。如果使用Layer2的扩容技术还需要额外的学习成本的话，会降低技术人员的输出效率和水平，未来性能的增益甚至不能覆盖当下的团队运行成本，对初创团队来说是非常危险的。

## 测试网部署的体验如何，部署过程中有没有遇到什么问题  

部署过程非常流畅，没有什么问题，如果要说的话，可能是用户太多太热情了，rpc负载可能有点大，偶尔会卡。另外Scroll的浏览器比较朴素，还可以再加把劲。

## 黑客松之后项目是怎么规划的？

这次赛后我和我们团队拉了会议推荐咱们Scroll，未来Honeypot Finance会fork到Scroll上，并且因为Scroll测试网和主网进展更快，将来在Scroll首发的概率更大。我们会以最快的速度，将我们的项目迁移到Scroll测试网，大家可以期待一下！

对于“y=e^x”基金，我们已经在Scroll测试网上部署了合约，相关的页面很快会发布在我们的GitHub项目主页，非常欢迎大家一起体验，以及贡献代码和想法！

## 项目链接
- Github：https://github.com/KAndHisC/yex

# Terminal 3

## 简单介绍一下自己的团队和项目？
我们团队来自现场组队，包含了AI工程师@Masa、前端工程师@Allen、后端工程师@Joze、产品经理@Jialin和UI设计师@Yoyo。我们的项目名叫Terminal3，是一款基于AI的Crypto all-in-one的操作终端产品，用户可以通过我们的平台完成任意复杂的操作，同时我们提供可组合性的工作流编排，同时智能分析每一个工作流的安全风险，让所有Web3用户低门槛的进行任意复杂的链上操作。

## 这次的项目和 Scroll 有什么联系？
这次我们深度集成了Scroll的知识到我们的大语言模型中，全面支持让用户通过自然语言交互的方式进行网络选择以及资产跨链，大大降低了用户使用scroll交互的操作门槛

## 如果是部署在 Scroll 的 Alpha 测试网上，是什么考虑呢？
我们认为Scroll是L2中非常优质的解决方案，这次的尝试也是想亲身实践感受一下Scroll网络，同时在未来，我们会继续深度集成Scroll生态的各种应用，让用户能够快捷、方便的在Scroll网络上进行各种尝试和探索


## 测试网部署的体验如何，部署过程中有没有遇到什么问题
部署的体验非常流畅，通过官方的文档，我们很顺利的完成的整套流程的开发和部署流程


## 黑客松之后项目的项目规划是什么？
我们将会继续将这个项目开发下去并且商业化，同时会深度集成Scroll生态的重要生态项目，真正将Terminal3变成所有web3用户进入web3的入口


## 项目链接
- Demo: https://drive.google.com/file/d/1TIknvd-KOH5hj-vfDkPpAnMuGSaakcjC/view
- Demo 视频： https://www.youtube.com/watch?v=Zh_sfqds19g&feature=youtu.be 
- Github:
	- [Project](https://github.com/EthBeijing-Terminal3)
	- [前端(React)](https://github.com/EthBeijing-Terminal3/extension)
	- [中间件(node.js)](https://github.com/EthBeijing-Terminal3/service-api)
	- [后端(flask)](https://github.com/EthBeijing-Terminal3/gpt_backend)
	- [AI安全检测(Python)](https://github.com/EthBeijing-Terminal3/AI_security_check)



# NirVANA

## 简单介绍一下自己的团队和项目?  

我们的项目名称是 NirVANA，一个基于 ERC2535 的模块化 SBT 发行工具，支持合约部署后再次添 加 / 替换 / 删除 模块，目前已支持:DAO 治理，社交恢复，ZK 验证模块。我们希望通过模块化功能释 放 SBT 的力量。  
我们团队来自东北大学链协，目前一个前端开发，一个合约和 ZK 开发。

## 这次的项目和 Scroll 有什么联系?  

我们参赛的赛道是 Layer2 赛道，Scroll 是 EVM 兼容的而且具有强扩展性，所以我们选择在 Scroll 上 部署我们的项目。

## 如果是部署在 Scroll 的 Alpha 测试网上，是什么考虑呢?  
1. Scroll 是 EVM 兼容的，开发人员可以无缝地在 Scroll 部署。 
2. Scroll 有更高的性能和更低的 Gas 费。  
3. Scroll 有更强的扩展性。

##  测试网部署的体验如何，部署过程中有没有遇到什么问题  
我们当时不知道如何在 Scroll 网络上验证合约代码，Scroll 的工程师在现场直接指导我们解决了。

## 黑客松之后有什么打算?  
我们将会在短暂休息调整状态后继续开发。  
1. 第一步是支持更多的功能模块:引入 ChainLink 动态 SBT 模块，更多的 ZK 电路模块等
2. 第二步是支持更多 SBT 协议:例如 ERC5727、ERC6147 等  
3. 第三步是支持社区定制模块以及完善更好的 UI/UX，提供更好的用户体验  
我们将争取在 Scroll 主网上线的同时上线我们的正式版。
感谢 Scroll 对我们的支持，希望以后有技术困难能和 Scroll 社区继续沟通。

## 项目链接
1. Demo链接: [https://nirvava.vercel.app/](https://nirvava.vercel.app/)
2. Demo视频: [https://www.youtube.com/watch?v=9misRClva3Q](https://www.youtube.com/watch?v=9misRClva3Q)
3. Github：
	1. 合约: [https://github.com/xiaoyuanxun/NirVANA](https://github.com/xiaoyuanxun/NirVANA)
	2. 前端: [https://github.com/beyond009/NirVANA-FE](https://github.com/beyond009/NirVANA-FE)


# SLOADS

## 简单介绍一下自己的团队和项目？
团队是临时组队的，当天晚上队长介绍完项目后，另外两个小伙伴加入了
Foundry 是一个以太坊智能合约开发框架。SLOADS 项目准备给它添加一个 feature，能够非常方便检索智能合约里面的所有 storage slot，特别是动态数据结构的，如 Array，Map。基于此，开发者可以更加方便地深入探索链上智能合约的状态，比如查找某个 token 的所有持币地址。工作内容：需要修改 foundry，foundry-std 里面的 cheatcode，以及 foundry-evm。

## 这次的项目和 Scroll 有什么联系？
没有直接联系。不过未来有人使用foundry来开发scroll 上的合约，则可能用到我们新添加的这个feature

## 黑客松之后项目的项目规划是什么？
后续项目将merge 到 foundry： https://github.com/foundry-rs/foundry/pull/4710

## 项目链接
- Demo 视频：[https://www.bilibili.com/video/BV1LT411x72Q/](https://www.bilibili.com/video/BV1LT411x72Q/)
- Github：[https://github.com/0xevm](https://github.com/0xevm)