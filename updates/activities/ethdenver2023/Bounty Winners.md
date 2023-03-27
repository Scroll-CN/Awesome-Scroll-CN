ETHDenver 真是太棒了！我们有55个出色的参赛项目争夺了总计 16 , 000美元的奖金。 以下是获胜者：

# ZK 应用

## Hunter Z Hunter
Hunter Z Hunter是一个基于区块链的照片寻宝游戏，使用ezkl库来为一个4层的机器学习神经网络生成证明和验证器。Ezkl [https://github.com/zkonduit/ezkl] 是一个库，用于将机器学习模型转换为零知识电路，底层使用halo2证明系统。
Build Box: https://app.buidlbox.io/projects/hunter-z-hunter
Demo: https://www.youtube.com/watch?v=0lpMyRItCXQ
Github: https://github.com/hunter-z-hunter

## Facade
Facade是一种零知识多重签名钱包，可以通过本地证明生成和中继实现链上匿名。
Facade 钱包允许所有者像普通的多签钱包一样执行所有交易，但默认是匿名的。利用零知识证明的力量，所有者将在本地生成证明，证明所有者正确地签署了交易调用数据，同时也证明了钱包的所有权。  
  
然后将证明传递给中继器，证明包含的交易调用数据将由 Facade 执行。诸如钱包所有者和签名之类的输入要么被加密，要么作为私有输入传递给电路。  
  
钱包在收到证明后将验证证明，如果正确，则像普通智能钱包一样执行交易调用数据，从而允许匿名进行交易。
Build Box: https://app.buidlbox.io/projects/facade
Github: https://github.com/cwkang1998/facade


# Scroll x Lens 跨链去中心化社交

## Swosh Cash
Swosh Cash 是一种简化资产转移的工具。它使用Lens来改善用户体验，将您的社交图谱纳入其中！
Swosh 在不依赖中心化参与者（如 OpenSea）的情况下，使代币转移变得高效和顺畅，支持
- 一次高效转移多个 NFT/代币
- 智能和 Gas 优化
- 多链功能（首先是 Base Görli、Scroll Alpha、Mumbai、Görli、Optimism Görli、Arbitrum Görli）
- Lens Protocol 集成以寻找您的朋友来改善用户体验
Website: https://swosh.cash/
Build Box: https://app.buidlbox.io/projects/swosh
Demo: https://www.youtube.com/watch?v=zvyGlNzbzPM&t=180s
Github: https://github.com/jonathangus/swosh.cash

## L's with Frens
L's with Frens 使用Lens展示了朋友间最大的链上损失。还记得你在滑点中被清算的那个时刻吗？现在，你可以将这一瞬间作为NFT铸造到Scroll上。
Build Box: https://app.buidlbox.io/projects/ls-with-frens
Demo: https://www.youtube.com/watch?v=NSEjhqyLSQg&t=47s
Github: https://github.com/thomaspanf/ethden23-Ls-with-frens


# 在Scroll上部署合约

## Composooor: $1,000
Composoor 是一个前端和智能合约库，用于构建链上和链下的混合可组合应用程序。Composooor 设计基于一种标准化的方式，让智能合约在交易准备时发出缺失数据信号，而这些数据应该来自链下资源。钱包可以解码此错误并找到丢失的数据，方法是通过去中心化协议或 API 获取丢失的数据，或者通过执行从该来源获取的一些代码来生成它。
Build Box: https://app.buidlbox.io/projects/composooor
Demo: https://www.youtube.com/watch?v=SFA_YiK-z0s
Github: https://github.com/kairos-loan/composooor


## 0xFable
一款完全链上交易的纸牌游戏，使用零知识证明来启用游戏中的隐私元素。
游戏逻辑完全在链上。这使开发人员能够使用卡片分叉合同并实施新的游戏模式。开发人员还可以创建自己的卡片集。
因为区块链默认是公开透明的，所以我们需要使用零知识证明来启用游戏的隐私元素。特别是，我们需要隐藏玩家牌组和手中的牌，并确保牌是从牌组中随机抽取的。
为此，我们实现了三个 ZK 电路：
-   抽奖证明：证明使用链上随机抽取了正确的牌，并且正确更新了提交给玩家手牌和剩余牌组内容的默克尔根
-   出牌证明：证明玩家打出了一张确实在他手上的牌
-   设置证明：证明玩家根据链上随机抽取了初始手牌（基本上是迭代抽取证明）
Build Box: https://app.buidlbox.io/projects/0xfable
Demo: https://www.loom.com/share/c5b6e1033a184ff681c727d811bfead3
Github: https://github.com/norswap/cards


## Rhinestone
Rhinestone 是结合了 ERC-4337（通过 alt mempool 进行帐户抽象）和 ERC-2535（钻石代理模式）的第一个模块化实现
账户抽象的理想解决方案是智能合约钱包的基础设施，使它们变得简单、定制和模块化。首先，理想的解决方案应该易于任何人使用，即使对以太坊和 ERC-4337 基础设施知之甚少。其次，用户应该能够选择他们想要的所有功能，而不是被要求使用他们不想要的功能。最后，与第二点相关的是，特性应该易于选择和编辑，并且易于开发人员构建。
Rhinestone 构建了一个拖拽式 UI 的前端，允许用户简单地选择他们想要在钱包中的插件。根据插件的不同，系统可能会提示用户通过添加所需变量来配置插件。然后，我们将其转化为代码并创建上面指定的智能合约。

Website: https://www.rhinestone.wtf/
Build Box: https://app.buidlbox.io/projects/rhinestone
Demo: https://www.youtube.com/watch?v=kiAcFDuTYw8&t=6s
Github: https://github.com/kopy-kat/ethdenver-aa


## Peanut Protocol
Peanut 是一个基础设施项目，允许你将代币发送给完全不知道其链上身份的人，只需发送一个 Claim 链接！
Website: https://peanut.to/
Build Box: https://app.buidlbox.io/projects/peanut-protocol
Github: https://github.com/ProphetFund/peanut-contracts


## Dynamic Stableswap
Dynamic Stableswap 保护流动性提供者在剧烈波动时期（例如稳定币脱钩时）免受套利者的侵害。这是通过交易手续费为波动率的动态函数来实现的。
Dynamic Stableswap 假设如果交易量很大，那么波动性也会很高，这意味着应该增加该特定池的费用。费用没有上限，这意味着它们可以超过 100%，有效地阻止套利者在稳定币脱钩时进行交易。

Website: https://dynamicstableswap.netlify.app/#/
Build Box: https://app.buidlbox.io/projects/dynamic-stableswap
Github: https://hackmd.io/@albertsu/dynamic-stableswap


## AI Coliseum
AI Coliseum 使用 zk 证明验证 ML 输出
Build Box: https://app.buidlbox.io/projects/npc-wars
Github: https://github.com/omurovec/npc-wars


## Mercury Protocol
Mercury Protocol 创新地允许用户在交易数据的同时保持他们的完全主权。
在我们最初的 Mercury 协议架构中，我们使用 Starknet 和 Cairo 对进行Layer 2验证。Cairo 是一种非常年轻的语言，有时会很麻烦，所以我们很高兴发现并试用了 Scroll。我们用 Solidity 重写了我们的 Cairo 合约，并将它们部署在 Scroll L2 上。

Build Box: https://app.buidlbox.io/projects/mercury-protocol
Demo: https://www.youtube.com/watch?v=NM60ABl1hys
Github: https://github.com/mercury-protocol/ethdenver


## My Mül
My Mul 是一款类似链上 3D NFT 游戏，具有完全可互操作的游戏行为和角色，可以轻松集成到任何开放的游戏生态系统中。角色根据链上交互而变化。
My Mul允许从智能合约的 abi 生成 behave graph 节点，并允许 3d 模型以可互操作的格式写入和读取任何 evm 兼容的区块链，该格式可以导入到开放游戏中平台。

Build Box:https://app.buidlbox.io/projects/bull-bear
Demo: https://www.youtube.com/watch?v=jvxd7spiOmo
Github:  https://github.com/oveddan/my-mul


## Abrey
Abrey是一个去中心化的点对点声誉系统。他们同时提交了EIP的草案，来使链上声誉标准化

Website: https://www.gmabrey.xyz/
Build Box: https://app.buidlbox.io/projects/arbey
Demo: https://www.youtube.com/watch?v=MsAfUggpA7Y
Github: https://github.com/arbeyyerba/contracts

## RNGesus
RNGesus 使用 DRAND 将可验证随机性上链。这对于（尚未）无法访问 Chainlink VRF 的执行环境很有用。
Build Box: https://app.buidlbox.io/projects/rngesus
Demo: https://www.youtube.com/watch?v=684vvZtA_As
Github: https://github.com/kevincharm/rngesus