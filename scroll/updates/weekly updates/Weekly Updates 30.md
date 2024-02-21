
# Scroll 全新外观升级
经过几个月的努力，我们推出了全新的外观，包括一个全新的网站和文档。 在我们改版的网站上，您可以找到有关我们的生态系统、贡献者的信息，以及跨链桥接到 Scroll 的简化途径。

# Beta测试网

## 测试网现状
截至 2023 年 8 月 27 日  21 : 00，Beta测试网共有约 385,936  个钱包地址，新增了329,939个钱包地址，处理了约 1,484,859 笔用户交易，生成了 261,702 个区块，平均区块时间约为 3 秒。
![](30-0.png)
## 跨链桥
我们全新改进的认领 UI 大大提高了从 Scroll 到以太坊L1的提款效率。
虽然我们的 ZK 技术可以在几个小时内完成提款，而Op Rollup则需要 7 天，但从L2提款仍然需要在不同时间支付两种不同形式的Gas费。
- 第 1 步：要发起提款，用户需要在Scroll链上支付 L2 Gas，这将有效地将您的代币存在跨链桥合约中以传输到以太坊 L1。 
- 第 2 步：在以太坊上支付 L1 Gas 以完成交易。
为了在以太坊上继续交易的其余部分，我们需要传输在步骤 1 期间在Scroll上发生的状态变更。 因此，我们使用ZK提交有效性证明，这需要几个小时才能完成。关键问题是Gas费的变化

这意味着我们无法在第 1 步时向用户预先收取这两项费用。相反，我们需要用户在步骤 1 区块最终确认后的第 2 步支付第二笔费用。 为了优化此过程，我们创建了两个交易的历史记录页面。


在跨链桥页面的顶部，始终有一个交易历史记录按钮，可让您跟踪所有跨链交易。 单击“认领”按钮将返回到“认领”UI，您可以在其中查看您的认领是否已准备好并进行最终提款。


## EVM 兼容性
在技术方面，我们将继续推动着 EVM 兼容性，在针对标准 EVM 测试套件进行测试时，我们达到了 99.8% 的新高。 在评估了剩余的 0.2% 之后，我们很高兴地向大家分享这不会影响我们 L2 的运作。


# 生态项目

我们在 Discord 服务器中推出了一个全新的论坛，允许在 Scroll 生态系统中构建的项目分享他们的最新更新、功能改进、研究等等！ 要参与讨论，请在 Discord 上加入我们：
https://discord.com/invite/scroll

## Chainlink
Oracle 网络是 DeFi 的核心支柱之一，允许去中心化应用程序无缝连接到外部和现实世界的信息。 Scroll 将集成 Chainlink，以扩展其行业领先的预言机网络。

作为对去中心化，可持续和可扩展性充满热情的倡导者，此次合作将加速Scroll生态系统的发展，为开发者提供低成本和可靠的预言机服务，允许智能合约在Scroll和外部系统之间自动传输数据，最大限度地提高生态系统的增长。

## zkMarkets
zkMarkets正在构建一个独特的 NFT 市场。 他们提供各种工具，例如 NFT 验证、量身定制的Launchpad

## 1RPC by Automata Network
1RPC 是一个免费的隐私保护 RPC 服务。 1RPC 使用独特的保护技术设计来确保不存储用户的元数据。
以下是使用 1RPC 的极简流程：
→ 在 1RPC 上搜索Scroll  
→ 点击钱包图标 
→ 批准钱包消息
- **Chain ID**: 534351
- **Currency**: ETH
- **1RPC URL**: 1rpc.io/scroll/sepolia
- **Explorer URL**: sepolia-blockscout.scroll.io

## Innovaz
Innovaz 是一个 NFT 市场即服务平台，允许任何人推出自己量身定制的 NFT 市场。 通过访问许多现成的模板，Scroll Sepolia 上的开发者可以在短短 15 分钟内创建和启动 NFT 市场！

## Owlto Finance
Owlto Finance 是一个去中心化的 Rollup 跨链桥，专注于以太坊的Layer2 生态系统，在发送或接收资产时提供廉价和快速的服务。

# 活动预告
## ETHWarsaw 
8 月 29 日至 9 月 3 日，可以在 ETHWarsaw 期间找到我们。我们的高级研究员 Toghrul Maharramov 将谈论无需信任的跨链桥，同时 Orest Tarasiuk 将参加圆桌讨论，探讨 L2 的相关内容。
- 8.29
	- Toghrul Maharramov 和 Orest Tarasiuk 将在 ZKWarsaw Day 上发表演讲
- 8.30
	- Toghrul Maharramov 将在 L2 Warsaw 上发表演讲
- 8.31 - 9.4
	- Orest Tarasiuk 将参加 ETHWarsaw 的圆桌
	- Toghrul Maharramov 将在 ETHWarsaw 发表演讲