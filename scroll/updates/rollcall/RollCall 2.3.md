
## Rollup标准

RIP 是“Rollup标准”，目前第一个 RIP 是RIP-7212，即“r1 曲线预编译”。

RIP 的最终确定与以太坊 L1 上区块的最终确认方式非常相似，这意味着它不能被更改或回滚。RIP 的生命周期与常见的 EIP 生命周期相同，EIP 的生命周期一般会经历了 draft, review, last call 和 final call 四个阶段。

有关 EIP 生命周期的更多信息，请参见：

https://eips.ethereum.org/

目前，RIP-7212 现在已经确定

## Rollup 采用

如 [@ulerdogan](https://twitter.com/ulerdogan) 所述 ，至少有三个 Rollup 团队已经承诺实现这一新标准。Polygon 将在其 Napoli 升级中采用该标准， zkSync 已经做好准备工作，预计将于 4 月发布。Optimism 和  Kakarot 都在努力集成这个预编译。 

这就引出了另一个问题： 社区应该如何跟踪所有 RIP，包括哪些 rollup 支持哪个标准？

RIPs GitHub 存储库可能会引入一个“注册表”，该注册表将以 JSON 格式存储有关 RIP 支持的信息。一旦 Rollup 团队在主网上添加了对特定 RIP 的支持，他们只需在注册表中更新其状态即可。 

接下来，我们将决定哪些协议符合注册表的条件，以及谁将负责决定哪些 EVM 链是 rollup，哪些不是？

[@CarlBeek](https://twitter.com/CarlBeek) 的建议是，默认简单的包含，“如果它表现地像 rollup ，那么它可能是一个 rollup”。如果没有，将其他链添加到此注册表中也没有太大的坏处，因为我们的目标是提供有用的资源，而不是重新定义 rollup。 


## Rollup 规范
我们如何检查不同的实现是否规范，以及协议是否真实地实现了标准化的 RIP？ 

在以太坊 L1 的情况下，我们有执行规范测试，经常用于检查不同的客户端实现。在 Rollup 的情况下，我们可以简单地 fork 同一个存储库，或是创建一个单独的存储库，为 RIP-7212 以及其他标准提供标准的测试。 

当涉及到各种 RIP 的标准规范时，可能存在许多细微差别。例如，如果一个 rollup 实现了这个特定的预编译，但收取了不同的 gas 费费用，该怎么办？ 这是很有可能的，因为某些预编译的执行和验证成本在 OP 和 ZK rollup 之间有很大差异。 

在最新的电话会中，我们讨论了许多不同的解决方案。 

[@adietrichs](https://twitter.com/adietrichs) 建议我们要严格遵守标准。例如，如果 Rollup 收取标准 gas 费用，那么则符合 RIP-7212 标准，但是，Rollup 可以通过采用多维费用市场来抵消成本不匹配。

[@yoavw](https://twitter.com/yoavw) 建议 RIP 可以定义最高价格，这样 Rollups 就可以在执行后简单地退还任何剩余的 gas。 

[@shemnon](https://twitter.com/shemnon) 提出 EOF 会让事情变得容易得多。

## 开发者体验

最后的讨论是关于开发者体验的话题。

例如，如果有人要构建一个支持 RIP-7212 的 DApp，而我想将其部署在多个 Rollups 中，我是否需要在注册表中逐个手动检查每个 Rollup 的支持？ 

幸运的是，有一种名为“渐进式预编译（progressive precompiles）”的替代提案，链首先采用兼容（但成本较高）的 Solidity 版本，然后最终将合约转换为预编译。但是，这与 RIP 采用的当前寻址方案不兼容。

[@yoavw](https://twitter.com/yoavw) 提出了一个全新的预编译，允许以标准化的方式检查链上的 RIP 支持。 


本周的 RollCall 分组会议是对 Rollup 标准化框架如何随着时间的推移而发展和成熟的有趣探索。 感谢  [@adietrichs](https://twitter.com/adietrichs) 、 [@CarlBeek](https://twitter.com/CarlBeek) [@ulerdogan](https://twitter.com/ulerdogan) [@shemnon](https://twitter.com/shemnon) [@ETazou](https://twitter.com/ETazou) [@yoavw](https://twitter.com/yoavw) [@parithosh_j](https://twitter.com/parithosh_j) [@stasbreadless](https://twitter.com/stasbreadless) 

