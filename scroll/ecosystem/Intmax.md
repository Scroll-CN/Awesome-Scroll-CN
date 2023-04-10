Intmax 项目——一个新颖的以太坊 L2 zkRollup 网络，用于各种网络服务和金融。

在 Intmax，我们的使命是构建一个扩展平台。鉴于其安全性和去中心化性，我们选择将其构建为以太坊 L2 — zkRollup。我们认为，为了让加密货币真正实现主流适应，需要有同时实现超扩展和隐私的基础设施。

# 引入 Intmax zkRollup

Intmax zkRollup 配备了一个新的架构，用户和 zkRollup 节点（运营商）在底层进行通信。当用户进行交易时，运营商返回其资产的默克尔证明。

由于这种在线通信，不需要将交易历史存储在链上以执行合约，因此 Intmax 的 gas 成本大大降低（比典型的 zkRollups 节省 95% 的成本！）。

此外，Intmax 上的用户可以默认保持隐私，因为系统不必在链上发布数据。

你可能想知道如果数据不在链上，是否会引入新的单点故障？答案是否定的！由于 Intmax 上的安全性和活跃性是隔离的，因此用户始终可以安全地将资金提取到 L1。

这意味着 Intmax 具有与典型的 zkRollups 相同的安全假设——仅依赖于以太坊 L1——而其他链下数据可用性解决方案，如 zkPorter、StarkNet 的 Validium 或使用 Celestia 的解决方案，是基于加密经济学安全性或信任的有限数量的成员——数据可用性委员会成员。

![](https://miro.medium.com/v2/resize:fit:1400/1*ocMHbq7YvBWqLv3sR8yFNw.png)

没有历史数据的 zkRollup

有关此的更多详细信息，请参阅[以太坊研究帖子](https://ethresear.ch/t/a-zkrollup-with-no-transaction-history-data-to-enable-secret-smart-contract-execution-with-calldata-efficiency/10961)

# 进一步缩放 + 从 L2 到 L1 的快速传输

上述方法已经具备了显着的扩展和隐私功能，但 Intmax 还开发了一种额外的机制（称为预共识机制）以进一步降低 gas 成本。

随着最近的发展，零知识证明 (ZKP) 可以包含另一个 ZKP。这种技术称为“递归 ZKP”。Mina Blockchain 使用它来减小其块大小。我们用它来降低验证的 Gas 成本，并确保快速确认。

该机制结合了 zkRollup 和 Optimistic Rollup 方法，因此它具有 zkRollup 安全性 + Optimistic Rollup 效率。

![](https://miro.medium.com/v2/resize:fit:1400/1*6tufnFugHTJr2idG5FtVvQ.png)

预共识机制

**关于预共识机制的更多信息，请参见**[**以太坊研究帖**](https://ethresear.ch/t/a-pre-consensus-mechanism-to-secure-instant-finality-and-long-interval-in-zkrollup/8749)

# 硬件加速——zkcloud

要生成 ZKP，通常需要进行计算。今天，由于昂贵且复杂的数学运算，此过程缓慢且昂贵。

为了使 Intmax zkRollup 更快，我们还在优化专用硬件，例如用于 ZKP 的现场可编程门阵列 (FPGA)。这将演变成一个名为“zkcloud”的服务，在未来为其他去中心化协议提供计算。

[zkcloud alpha 版本](https://zkcloud.io/)已经上线，它可以帮助开发者更轻松地使用 ZKP 编写智能合约和程序。它目前支持 Groth16 和 PLONK 证明，STARKs 即将推出。

# **下一步是什么？**

我们即将宣布一些激动人心的消息！同时，如果您有任何问题，请联系我们