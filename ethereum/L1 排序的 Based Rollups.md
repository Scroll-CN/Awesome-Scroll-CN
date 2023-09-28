**TLDR：** 在本文中，我们描述了一类特殊 rollups 的集合，称之为 “based” 或 “L1排序的”。这种 L1 排序的 rollup 是最简单的，并且继承了 L1 的活性和去中心化。此外，Based Rollups 与所基于的 L1 在经济上保持一致。

**定义**
当 rollup 的排序由所基于的 L1 所驱动时，它被称为 “based” 或 “L1排序的”。更具体地说，Based Rollups 中，下一个 L1 区块的提议者（Proposer）可以与 MEV 搜寻者（Searcher）和生产者（Builder）合作，无需许可地将下一个 Rollup 区块作为一部分包含在下一个 L1 区块内。

**优点**

-   **活性（liveness）** : Based Rollups 享有与 L1 相同的活性保证。请注意，带有逃生舱（escape hatches）的非 Based Rollups 的活性会降低：
    -   **较弱的结算保证**：逃生舱的交易必须在等待一定暂停期限才会得到结算。
    -   **基于审查的 MEV**：带有逃生舱的 Rollups 在暂停期间，容易受到短期内排序器审查带来的不利 MEV 影响 。
    -   **网络效应面临风险**：由排序器活性故障触发的大规模退出（例如对去中心化 PoS 排序机制的 51% 攻击）将破坏 Rollup 的网络效应。请注意，与 L1 不同，Rollup 不能使用社会共识从排序器活性故障中优雅地恢复。在所有已知的非 Based Rollups 设计中，大规模退出是达摩克利斯之剑。
    -   **Gas 惩罚**：通过逃生舱结算的交易通常会为其用户带来 gas 惩罚（例如由于交易非批量打包的次优数据压缩）。
-   **去中心化（decentralization）** : Based Rollups 继承了 L1 的去中心化，自然复用了 L1 搜寻者-生产者-提议者的基础设施。L1 搜索者和生产者受到激励，在他们的 L1 区块中包含 rollup 区块来提取 rollup 的 MEV。然后这又会激励 L1 区块提议者在 L1 上包含 rollup 区块。
-   **简洁性（simplicity）**：Based Rollups 排序是最简单的，甚至比中心化排序要简单得多。Based Rollups 不需要验证排序器签名，不需要逃生舱，也不需要外部 PoS 共识。
    -   _历史记录_：2021 年 1 月，Vitalik 将基于L1排序的方案称为[“完全无政府状态” ](https://vitalik.ca/general/2021/01/05/rollup.html#who-can-submit-a-batch)。这有同时提交多个 rollup 区块的风险，导致 gas 和工作量的浪费。现在的区块提议者 — 生产者分离方案（Proposer-Builder Separation, PBS）可以严格控制的 L1 排序，每个 L1 区块最多有一个 rollup 块，并且没有 gas 浪费。当 rollup 的 `n+1` 区块（或对于 `k >= 1`，`n+k`）包含区块 `n` 的 SNARK 证明时，可以避免浪费 zk-rollup 的证明工作。
-  **成本**：Based Rollups 的 gas 开销为零 —— 甚至不需要验证来自去中心化或中心化排序器的签名。Based Rollups 的简洁性降低了开发成本，缩短了发布时间，并减小了代码漏洞的暴露面积。Based Rollups 的排序也是无需代币的，避免了基于代币的排序器的监管负担。
-  **L1 经济一致**：源自 Based Rollups 的 MEV 自然流向了所基于的 L1。这些流动性加强了 L1 经济安全，并且在 MEV 销毁的情况下，提高了 L1 原生代币的经济稀缺性。这种与 L1 在经济上的紧密结合可能有助于构建 Based Rollups 的合理性。重要的是，尽管牺牲了 MEV 收入，Based Rollups 保留了从 L2 拥塞费（例如 EIP-1559 形式的 L2 基础费用）中获得收入的选项。
-  **主权性（sovereignty）**：尽管将排序委托给了 L1，但 Based Rollups 保留了主权性。Based Rollups 可以有一个治理代币，收取基本费用，并且可以在合适的时候使用这些基本费用的收益（例如 Optimism 为公共产品提供资金）。

**缺点**

-  **无 MEV 收入**： Based Rollups 将 MEV 放手给了 L1，使其收入限制为基本费用。与直觉相反，这可能会增加 Based Rollups 的总收入。原因是 rollup 的格局似乎是赢家通吃，获胜的 rollup 可能会利用 Based Rollups 的安全性、去中心化、简洁性和一致性来实现主导地位并最终实现收入最大化。
-  **排序约束**：将排序委托给 L1 会降低排序灵活性。这使得某些排序服务变得更加困难，甚至可能是无法实现的：
    -   **预确认**：快速预确认对于中心化排序不是问题，并且可以通过外部 PoS 共识来实现。使用L1 排序进行快速预确认是一个开放性问题，有着许多有前景的研究方向，包括EigenLayer、Inclusion Lists 和 Builder Bonds。
    -   **FCFS**：Arbitrum 风格的 FCFS 排序在 L1 上有待考证。EigenLayer 可能解锁 L1 的 FCFS 排序。


**命名**

“Based Rollups” 这个名称源于 Base L1。这与 Coinbase 最近宣布的 [Base 链](https://base.org/)有所冲突，这是一个巧合。事实上，Coinbase 在[他们的 Base 公告中](https://www.coinbase.com/blog/introducing-base)分享了两个设计目标：
- **tokenlessness**：“我们没有发行新网络代币的计划。”
- **decentralisation**：“ 我们 [...] 计划随着时间的推移逐步去中心化区块链。”
Base可以通过成为 Based Rollups 来实现无代币的去中心化。