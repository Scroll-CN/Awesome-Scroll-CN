
## 概述

我们很高兴宣布将于 2024 年 7 月 3 日进行 Curie 升级。此次升级引入了数据可用性 (DA) 压缩，以减少 Layer 1 DA 大小及其相关的 Gas 费用，预计将使 Scroll 链上的 Gas 费降低 2 倍。此外，此次升级还将纳入两种交易类型：EIP-1559 和 EIP-2930，来稳定 Scroll 的 Gas 费用。最后，此次升级还将支持坎昆升级中的新 EVM 操作码 `TLOAD` 、 `TSTORE` 和 `MCOPY` 。


## 升级内容

### 交易数据压缩

在之前的 Bernoulli 升级中，Scroll 将 Rollup 交易数据从 calldata 迁移至了 blob 空间，以使 DA 更加便宜。 Curie 升级使用 zstd 算法进一步压缩存储在 blob 中的数据。这种压缩平均将数据大小减少 2.8 倍，允许每个 blob 存储更多事务，从而降低每个事务的数据可用性成本。

### 支持EIP-1559和EIP-2930交易类型

通过 Curie 升级，Scroll 现在支持 EIP-1559 和 EIP-2930 交易类型。这将带来两个好处。首先，它提升了兼容性并提供更好的灵活性，允许开发者使用这两种类型发送交易。其次，EIP-1559 模型由基本费用和优先费用组成，有助于提高交易费用的可预测性和稳定性。 Scroll 采用了 EIP-1559 定价模型的修改版本，具有以下几个方面的特点：

- Curie 升级中的定价模型与 EIP-1559 交易接口兼容，允许用户使用现有的 SDK 和钱包发送 EIP-1559 类型的交易。
- 基础费用将取自于 L1 的基础费用，从而进行更准确的交易定价

### 支持 `TLOAD` 、 `TSTORE` 和 `MCOPY` 操作码

Curie 升级包括对三个新操作码的支持，这些操作码在优化智能合约中的内存和存储管理方面发挥着至关重要的作用：

- `TLOAD` 和 `TSTORE` ：这两个操作码用于处理瞬时存储(Transient storage)，即交易结束时会清除的临时存储区域。 `TLOAD` 用于从瞬时存储中检索值，而 `TSTORE` 用于在其中存储值。瞬态存储非常适合那些不需要在交易间保留的中间数据，有助于降低 Gas 成本并提高合约效率。
- `MCOPY` ：该操作码为高效的内存操作而设计的，用于将数据从一个内存位置复制到另一个内存位置，从而在合约执行期间实现快速的数据复制和管理。

通过新添加的操作码，用户可以安全地使用最新的 Solidity 编译器版本（当前为 0.8.26）来构建合约。

### 动态区块时间

目前，l2geth 中的出块时间固定为每个块 3 秒。为了提高 Scroll 链的吞吐量，Curie 升级将引入动态出块时间。在交易拥堵期间，一旦区块中的交易达到电路限制，就会密封打包该区块，而不是等待 3 秒的时间间隔。正常情况下内，区块仍将以按 3 秒的间隔密封，以确保一致的用户体验。

## 技术细节

升级后，模块将运行以下版本：

- 合约：仓库提交 `b0242c2938aa48013ff8261da0dcf7e46706dd04` 
	- https://github.com/scroll-tech/scroll/tree/b0242c2938aa48013ff8261da0dcf7e46706dd04
- 节点：l2geth repo v5.5.0
	- https://github.com/scroll-tech/go-ethereum/releases/tag/scroll-v5.5.0
- 电路：zkevm- Circuits repo v0.11.4
	- https://github.com/scroll-tech/zkevm-circuits/releases/tag/v0.11.4

### 合约变更

此次升级的代码变更记录在以下 PR 之中：

- PR 1317
	- https://github.com/scroll-tech/scroll/pull/1317
- PR 1343
	- https://github.com/scroll-tech/scroll/pull/1343
- PR 1354
	- https://github.com/scroll-tech/scroll/pull/1354
- PR 1372
	- https://github.com/scroll-tech/scroll/pull/1372

主要变更如下：

- Rollup 合约 ( `ScrollChain` ) 现在将同时接受版本 1 和 2 的批次（Batch）。版本 1 用于Curie 升级之前未压缩的 blob，而版本 2 用于Curie 升级之后压缩的 blob。合约变更后将确保它能接受版本 2 的批次。
- `L1GasPriceOracle` 合约是 L2 上预部署的合约，排序器使用它来估计将 Scroll 交易提交至以太坊的成本（也称为“L1 数据费用”），该合约将被更新。 Curie 升级后将更改公式来估计 blob DA 的数据费用，从而提供更准确的 DA 成本估算：
	- 原公式： `(l1GasUsed(txRlp) + overhead) * l1BaseFee * scalar`
	- 新公式： `l1BaseFee * commitScalar + len(txRlp) * l1BlobBaseFee * blobScalar`

合约升级流程注意事项：
- `ScrollChain` 合约将经过通常的 14 天时间锁流程进行升级。
- `L1GasPriceOracle` 将由排序器在 Curie 硬分叉的区块上自动更新。

### 节点变更

l2geth节点的新版本为 v5.5.0。节点运营商必须在 Curie 分叉区块之前升级其节点。主要变化包括：
- 在 Curie 硬分叉区块上启用 `TLOAD` 、 `TSTORE` 和 `MCOPY` 操作码。
- 调整 Rollup 验证器模块，使其继续处理压缩的批次。
- 支持 EIP-1559 定价模型。
- 启用对动态区块时间的支持。

请参考发布说明获取更多信息。
- https://github.com/scroll-tech/go-ethereum/releases/tag/scroll-v5.5.0

### ZKEVM 电路变更

zkevm 电路的新版本是 v0.11.4
1. 新的 zstd 算法已经实现并集成入批处理电路中，从而实现了 Blob 内的压缩 DA。批次中的最大块数从目前的 15 个增加至 45 个，平均每个 blob 可以包含大约 600 笔交易。
2. 添加了如下的操作码： `TLOAD` 、 `TSTORE` 、 `MCOPY` 和 `BASEFEE` 。
3. 支持新的交易类型：EIP-2930 和 EIP-1559。
4. 实现新的 L1 数据收费机制，提供更准确、公平的 L1 数据收费。内部代码重构和清理。

请参阅此处的发布日志。
- https://github.com/scroll-tech/zkevm-circuits/releases/tag/v0.11.4

### 审计

电路变更已经经过 Zellic 和 Trail of Bits 的审计。 Zellic 的审计报告可以在下方找到。 Trail of Bits 已完成最终审计，报告将在准备好后发布。
- https://github.com/Zellic/publications/blob/master/Scroll%20zkEVM%20-%20Zellic%20Audit%20Report.pdf

## 升级时间表

1. 在升级前的几周内，对新合约、节点和电路进行了广泛的内部测试。
2. 支持多个版本的合约于 2024 年 6 月 12 日通过 Scroll Multisig 合约启动，随后有 14 天的升级交易时间锁。
3. 2024 年 6 月 12 日发布了新的 l2geth 版本，为 Curie 升级设定了区块高度。
4. 此次升级于 2024 年 6 月 17 日部署在 Scroll Sepolia 测试网上，并进行了严格测试。
5. 2024 年 7 月 3 日，Scroll 团队将在 Scroll 主网上执行合约升级。
6. 在指定的区块高度处，所有 Scroll 节点都会激活 Curie 升级，从而完成整个升级过程。

社区可以追踪以下合同的升级流程：
- L1 Scroll 多签地址： `0xEfc9D1096fb65c832207E5e7F13C2D1102244dbe` （以太坊上）
- L1 时间锁地址： `0x1A658B88fD0a3c82fa1a0609fCDbD32e7dd4aB9C` （以太坊上）
- [L1 升级提案交易](https://app.safe.global/transactions/tx?safe=eth:0xEfc9D1096fb65c832207E5e7F13C2D1102244dbe&id=multisig_0xEfc9D1096fb65c832207E5e7F13C2D1102244dbe_0xd0404efeb770e62efe86df424bb4b644f7e609276ac33a12fbfe5c3a9302e317)


## 兼容性

### 排序器和跟随节点 (l2geth)
此升级是一次硬分叉，引入了 `TLOAD` 、 `TSTORE` 和 `MCOPY` 操作码。运行 `l2geth` 节点的运营商需要在硬分叉块之前升级到 v5.5.0。有关更多信息，请参阅节点发布说明。

https://github.com/scroll-tech/go-ethereum/releases/tag/scroll-v5.5.0

### Dapps 和索引器

对于 Dapps，此次升级是向后兼容的。开发者应调整 Gas 费设置来包含 EIP-1559 定价模型。请注意，Dapps 在应用程序逻辑中不能再依赖固定的 3 秒区块时间。

对于索引器，数据格式保持不变。然而，数据内容将会发生变化：
- 自 Curie 升级后， `BatchHeader` 中的 `version` 字段将更改为 2。
- 存储在 blob 中的数据将被压缩，并且可以通过 zstd v1.5.6 解压缩。

## 下一步？

在 Scroll，我们不断致力于新功能和升级，来使 Scroll zkEVM 更强大。在接下来的几个月中，我们计划使用递归证明将多个批量证明聚合为单个有效性证明来进行 L1 验证，以进一步降低 Gas 费用。

