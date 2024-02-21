充满了开发者活力的 ETHGlobal Tokyo 黑客松圆满结束！

在超过 1000 名黑客和约 220 个团队中，有 72 个项目提交了Scroll部署合约的赏金，恭喜所有的获奖者们！

我们选取了其中一些在 Scroll 上部署的有趣项目


# BorrowFi
![](borrowfi.png)
DeFi 生态中的许多借贷协议具有共同的特征（它们都有利率，并且涉及抵押和清算），但没有使用标准。我们提出了一个新的 EIP-6882 标准来解决这个问题，并创建了一个聚合器 dapp，可以从集成池中找到最佳费率。这使用户能够利用不同的协议而无需搜索最佳利率，将极大地改善 DeFi 借贷的体验。

BorrowFi首先创建了一个新标准，可用于包装借贷协议以规范其合约方法。然后我们用它来检索现有的贷款池，如 Aave V3 和 Curve。最后，通过我们的聚合器合约，我们的 dapp 可以查询最佳利率并触发以这些利率借款的交易调用。

- ETHGlobal: https://ethglobal.com/showcase/borrowfi-ore25
- Github: https://github.com/massun-onibakuchi/huff-standard4borrow
- EIP-6882: https://github.com/ethereum/EIPs/pull/6882


# DeFuture 

Defutures 是一个完全去中心化的期货交易所，它与现有的 DeFi 协议集成，然后使用它们为期货头寸提供执行价格（Strike Price）。Defutures 专注于帮助加密货币交易初学者。
它设计简单、容易且稳定，与众不同。它不支持开仓，而是与现有的 DeFi 协议的 AMM 集成，用它来提供期货头寸的行使价，利用AMM的LP和保证金组合成期货组合。现有的现货对和期货对在给定情况下会相互收敛，当收敛时，期货交易背后的逻辑就实现了。

- Demo: http://eth-tokyo-defutures.s3-website-ap-northeast-1.amazonaws.com/
- ETHGlobal: https://ethglobal.com/showcase/defuture-g31hx
- Github: https://github.com/ETHGlobal-Tokyo-ValleyDance/defutures

# GaaS

GaaS ( Gate-as-a-Service) 可以使用任意链上事件和交易来为任何应用程序设计进入门槛，而不再需要手动的巨型电子表格。例如

1.  创建一个进入门槛，使您的应用程序或内容专供高级用户使用。例如，经常在 DeFi 平台上交易的 AAVE 交易员。
2.  创建一个进入门槛，使您的应用程序或内容专供质押者使用。例如，质押ApeCoin ($APE) 至少 1 个月的用户。
3.  然后要求用户满足这些链上要求，然后才能访问您的网站。


- Demo: https://gaas-pink.vercel.app/
- ETHGlobal: https://ethglobal.com/showcase/gaas-exadm
- Github: https://github.com/tracychen/GaaS


# SocialSecuritySnap
![](SocialSnap.png)
该项目旨在通过开发插件来提高安全性、用户体验并提供额外服务，从而增强名为 MetaMask Snap 的以太坊区块链钱包。MetaMask 是一个浏览器扩展，允许用户轻松管理加密货币和数字资产，以及执行交易。该项目的主要目标如下：

主要组件包括 MetaMask Snaps、Lens Protocol、GPT-4、Worldcoin 和 Superfluid。以下概述了每种技术是如何集成的以及它们在项目中的各自作用：

MetaMask Snaps：我们使用 MetaMask Snaps 来扩展 MetaMask 的功能，允许我们在执行交易之前显示额外的信息和安全功能。

Lens协议：Lens协议已集成到项目中以提供额外的安全层。我们使用 Lens Protocol API 来获取被关注用户的个人资料和合约执行历史。此信息显示在 MetaMask 中，帮助用户识别潜在的垃圾邮件或不可信合约。

GPT-4：我们使用 GPT-4 API 来分析和审查交易中正在执行的方法。GPT-4 提供了合约信息的摘要，以及潜在风险的描述，这些都显示在 MetaMask 中供用户考虑。

Worldcoin：Worldcoin 的 KYC（了解你的客户）功能已集成到该项目中，以确保只有经过验证的用户才能访问该服务。尚未完成 KYC 流程的用户在交易确认时会被提示验证其身份。

Superfluid：我们集成了 Superfluid 以启用按秒计费的订阅服务。这一创新功能为用户提供了更灵活和精确的订阅计划。


- Demo: https://eth-tokyo-social-security-snap-site.vercel.app/
- ETHGlobal: https://ethglobal.com/showcase/socialsecuritysnap-b5vyt
- Github: https://github.com/yusakapon/ETHTokyo-SocialSecuritySnap


# Penguin Network

Penguin Network 通过让中继器在以太坊 Layer 1 存放保证金，引入了跨链无信任消息传递的生态系统。中继者将承担 Slash 的风险，但他们可以通过负责跨链通信来赚取佣金。中继者还可以通过为资产锁定在 Layer1 上的AAVE 协议中获得收益。Slash 使用存储在以太坊 Layer 1 中的每个Layer2的区块哈希执行，因此中继器可以在任何Layer2之间进行任意消息传递。目前，任意链间通信主要由链本身的排序器执行，但 Penguin Network 的协议带来了更多的中继器，并实现了更去中心化、更快和更便宜的通信。

- ETHGlobal: https://ethglobal.com/showcase/penguin-network-jhkvu
- Github: https://github.com/Penguin-Network-ETHGlobal-Tokyo/Penguin-Network


特别感谢 @ETHGlobal (https://twitter.com/ETHGlobal)在东京举办精彩的编程马拉松！