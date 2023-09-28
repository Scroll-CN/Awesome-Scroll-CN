Avneesh Agarwal

本指南将向您展示如何将任何智能合约部署到[Scroll zkEVM](https://scroll.io/?ref=blog.thirdweb.com)网络。

最后，您将学习如何创建一个简单的 NFT Drop 智能合约，将其部署到**[Scroll Alpha Testnet](https://thirdweb.com/scroll-alpha-testnet?ref=blog.thirdweb.com)**，并在智能合约上铸造 NFT。

让我们开始吧！

## 什么是Scroll zkEVM？

Scroll zkEVM 是一个Layer 2网络，旨在解决以太坊主网的可扩展性问题，例如TPS和Gas费。

“EVM”是以太坊虚拟机；负责存储以太坊网络的状态、交易和智能合约。“ZK”指的是它是一个zkRollup，这意味着它“汇总”一批交易并在链下（即不在 EVM 上）执行它们。

零知识证明可以通过密码学来证明这些交易发生的结果，并发送有效性证明以完成区块链上的交易。

## 在Scroll zkEVM上创建智能合约

首先，前往您的 thirdweb 仪表板中的 Contracts 页面并点击**Deploy Contract**：

![部署新合约](https://blog.thirdweb.com/content/images/2023/03/SCR-20230304-uu3-1-.png)

您将被带到 thirdweb 浏览器(https://thirdweb.com/explore?ref=thirdweb)页面——在这里您可以浏览 web3 中的顶级协议的智能合约，只需点击几下即可部署它们！

> 注意：您还可以使用 thirdweb 命令行(https://portal.thirdweb.com/cli?ref=thirdweb)，通过从终端运行以下命令来设置智能合约环境：

```bash
npx thirdweb create contract
```

> 在我们的命令行指南(https://blog.thirdweb.com/guides/the-ultimate-guide-to-thirdweb-cli/)中了解更多相关信息，将引导您完成一个易上手的步骤流程来创建您的合约。

或者，让我们回到浏览器页面(https://thirdweb.com/explore?ref=thirdweb)：

![thirdweb 探索页面](https://blog.thirdweb.com/content/images/2023/03/SCR-20230309-bpg-2.png)

  
在这里，选择您选择的智能合约。本指南中，我们将使用NFT Drop (ERC721)(https://thirdweb.com/thirdweb.eth/DropERC721?ref=thirdweb)合约来创建我们的 NFT 集合：

![thirdweb 的 NFT Drop 合约](https://blog.thirdweb.com/content/images/2023/03/SCR-20230304-rkv-2.png)

使用图像、名称、描述等设置您的智能合约，并配置哪个钱包地址将接收来自初始销售和二级市场销售的资金：

![填充合同的元数据](https://blog.thirdweb.com/content/images/2023/03/contract-metadata-2-1-1.png)



## 将Scroll Alpha 测试网添加到您的控制面板和钱包

要将智能合约部署到 Scroll，我们首先需要将其作为网络添加到[Dashboard](https://thirdweb.com/dashboard?ref=thirdweb)。

为此，请单击网络按钮，然后切换到测试网选项卡。现在，搜索“Scroll”并选择 Scroll Alpha Testnet：

![搜索“Scroll”并选择 Scroll Alpha Testnet](https://blog.thirdweb.com/content/images/2023/04/Search-for-scroll.png)

现在它会提示您添加并切换到 Scroll Alpha Testnet：

![添加并切换到滚动 alpha 测试网](https://blog.thirdweb.com/content/images/2023/04/add-Scroll-Alpha-Testnet-to-wallet.png)

我们现在可以看到网络已经添加，我们现在可以将其部署到它上面。

![](https://blog.thirdweb.com/content/images/2023/04/Switched-to-Scroll-Alpha-Testnet.png)

如果钱包中没有资金，我们需要将一些 Goerli ETH 桥接到 Scroll Alpha 测试网。

## 在您的钱包中获取 Scroll Alpha 测试网资金

一旦您将 Scroll Alpha 测试网添加到您的钱包。前往[Scroll Bridge](https://scroll.io/alpha/bridge?ref=blog.thirdweb.com)并将一些 Goerli ETH 桥接到 Scroll Alpha 测试网。

如果您没有Goerli ETH，您可以使用如下的水龙头
- https://goerlifaucet.com
- https://faucet.paradigm.xyz
- https://goerli-faucet.pk910.de

![](https://blog.thirdweb.com/content/images/2023/04/go-to-scroll-bridge-and-bridge-some-funds.png)

输入要桥接的数量后，单击发送 ETH 到 Scroll Alpha Testnet

![](https://blog.thirdweb.com/content/images/2023/04/Bridge-initiated.png)

资金现在已经开始桥接，等待一段时间，交易完成。完成此过程后，您的钱包中将有测试网资金，这意味着您现在已准备好部署智能合约！

![资金已到达您在 Scroll Alpha Faucet 上的钱包](https://blog.thirdweb.com/content/images/2023/04/Funds-arived-in-wallet.png)

## 将智能合约部署到 Scroll 区块链

现在您已经有了测试网 ETH，让我们回到我们构建NFT Drop(https://thirdweb.com/thirdweb.eth/DropERC721?ref=thirdweb)合约的 thirdweb 仪表板。

我们已经填写了Metadata，因此在选择链后单击“立即部署”。它会提示你进行两笔交易，你必须批准它们。

![确认交易以部署合约](https://blog.thirdweb.com/content/images/2023/04/Deploy-Contract-to-scroll-zkEVM-Alpha-Testnet-.png)

大功告成，你刚刚部署了合约到 Scroll zkEVM Alpha 测试网。

## 调用智能合约函数

让我们看看如何通过调用一些方法来使用智能合约，例如铸造NFT ！

从浏览器选项卡中，您可以查看智能合约上的所有可用方法，并直接通过连接的钱包它们：

![从资源管理器中调用读取名称函数](https://blog.thirdweb.com/content/images/2023/03/contract-explorer-2.png)

### 设置我们的 NFT

在我们的示例中，我们创建了一个 NFT drop 智能合约，接下来我们快速设置它并通过执行以下步骤铸造我们的第一个 NFT：

1.  Lazy Mint一批 NFT。
2.  配置我们的 Claim 条件。
3.  立刻铸造 NFT！

详细过程，请查看其他指南(https://blog.thirdweb.com/tag/nft-drop/)了解更多信息！ 

设置 NFT 后，我们可以单击选项卡`Claim`中的按钮来铸造我们的第一个 NFT，

![认领 NFT](https://blog.thirdweb.com/content/images/2023/03/image-94.png)