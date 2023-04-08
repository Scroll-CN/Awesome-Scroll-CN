# 在Scroll上开发

## 欢迎

欢迎使用 Scroll 开发者文档！

Scroll 是建立在以太坊上的Layer 2网络（更准确地说是“zkRollup”）。

如果你有以太坊上开发的经验，那么你的代码、依赖项和工具，可以在Scroll上开箱即用。这是因为我们的网络与 EVM 在字节码层面兼容，设计初衷就是让开发者拥有以太坊一样的开发体验。

{% hint style="info" %}

### 刚接触 zkRollup

Scroll 通过链下执行交易获得安全性和速度，并生成交易正确执行的加密证明。此加密证明在 Layer 1 的智能合约中得到验证，确保在 Scroll Layer 2 上执行的所有代码同在以太坊 Layer 1 上执行的一样。
[更多关于 Scroll 架构的信息](https://scroll.io/blog/architecture)

{% endhint %}

在我们最新的 Alpha 测试网中，Scroll构建在Goerli测试网上。

## 入门

**希望在 Scroll 的 Pre-Alpha 测试网上开发？**

- 关于要点：查看[**开发者快速上手**](scroll/testnet/alpha_testnet_guide/developer_guide/quickstart.md)
- 在 Scroll 上部署你的第一个智能合约，请阅读我们的[**合约部署教程**](scroll/testnet/alpha_testnet_guide/developer_guide/contract_deployment.md)
- 我们还有许多[**生态项目集成**](scroll/testnet/alpha_testnet_guide/developer_guide/integrations.md)和[**已经部署的合约地址**](testnet_contract.md)，可以在此之上进行开发。


## 为什么要在 Scroll 上开发？

<details>

<summary><em><strong>吞吐量</strong></em><strong> —— Scroll 为以太坊创造了更多的安全区块空间。</strong></summary>

ZK Rollups 允许网络容纳更多交易，从而最大限度地减少链上拥堵。Scroll 通过使用零知识证明验证网络状态转换，继承了以太坊的安全性，可以在不影响去中心化的情况下处理更多交易。

</details>

<details>

<summary><em><strong>成本</strong></em><strong> —— Scroll 为用户节省 gas 费用。</strong></summary>

在以太坊上，对区块空间的竞争导致每笔交易的成本更高，因为每笔交易都会竞价以包含在下一个区块中。Scroll 利用最近在零知识证明和硬件加速方面取得的突破，极大地增加了安全区块空间并最大限度地降低了用户的交易成本。

</details>

<details>

<summary><strong>速度 ——Scroll 更快地向用户提供反馈。</strong></summary>

合并后，以太坊每 12 秒确认一个区块。Scroll的区块每 3 秒生成一个，并且为了降低风险操作，交易一旦包含在块中就可以被认为是最终确认的。这为社交和游戏应用程序中的链上交互打开了新的可能性。

</details>

<details>

<summary><strong>联盟——Scroll 建立在以太坊的愿景之上。</strong></summary>

Scroll 构建在以太坊的愿景之上。我们的宗旨是共建以太坊，而不是分裂它。去中心化、无需许可、抗审查和归属社区是我们工作和正在构建的路线图的核心。我们秉承开源精神，与以太坊基金会的隐私和扩容探索团队（PSE）密切合作，以支持他们在 zkEVM 上的工作，而zkEVM有朝一日可能会成为以太坊的核心。 我们还与治理 DAOs 和其他开源协议合作，以确保在部署应用程序的同时，我们也在努力扩大它们的影响——无论是在公共产品、核心基础设施还是下一代零知识用例中.

</details>

<details>

<summary><strong>社区——Scroll 将用户和开发者聚集在一起。</strong></summary>

我们知道在主网发布之前开源开发和吸引用户参与的难度所在！但Scroll 拥有着蓬勃发展的用户和开发者社区，有过 100,000 名渴望在我们的测试网上测试的用户的 Discord 社区，我们很高兴将开发者与提供真实反馈的用户联系在一起。

</details>


## 感谢你与我们一起构建开发

我们正在努力为网络带来更多的集成和支持更多的基础设施，并为我们未来的主网版本感到兴奋。

加入我们不断壮大的开发者社区。您可以在[Discord](https://discord.gg/scroll)上找到我们，加入我们的[论坛](https://community.scroll.io/)或在[Twitter 上](https://twitter.com/Scroll_ZKP)关注我们的进展。[](https://twitter.com/Scroll_ZKP)