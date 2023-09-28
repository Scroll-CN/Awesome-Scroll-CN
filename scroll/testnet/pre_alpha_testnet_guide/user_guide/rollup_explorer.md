# Rollup 浏览器

Rollup 浏览器 显示有关 Scroll L2 块及其汇总状态的基本信息。

### Rollup 状态

Pre-Alpha 测试网中的 Scroll L2 区块有 4 种 rollup状 态：

-   **`Precommitted`** 表示一个区块已经被包含在 Scroll L2 区块链中。虽然Precommitted区块因为没有发布在Scroll L1上，所以还不是Scroll L2 链的一部分，但是信任排序器（sequencer）的用户可以认为这个区块是暂时敲定的。
-   **`Committed`** 表示该区块的交易数据已经发布到 L1 上的 rollup 合约中。这确保了块数据可用，但不能证明它已以有效方式执行。
-   **`Finalized`** 表示在 Scroll L1 链上的有效性证明通过验证，已经证明了该区块中交易的正确执行。最终区块被认为是 Scroll L2 链的一部分。
-   **`Skipped`** 表示由于缺乏证明算力或代码中的错误而跳过了该块的有效性证明生成。这只是 Pre-Alpha 测试网的临时状态。


### Rollup表

该表提供了有关 Scroll L2 区块的 rollup 状态的信息。这些列是：

-   `L2 Block No.`显示区块编号
-   `Block Hash` 显示缩写的区块哈希。单击区块哈希将在 Scroll L2 区块浏览器中打开区块详情页面的新标签页。
-   `Tx(s)`显示区块中的交易数量。
-   `Timestamp`显示自生成块以来经过的时间。
-   `Status`显示此块的rollup状态。
-   `Commit Tx Hash`显示发布此 Scroll L2 区块交易数据的 Scroll L1 交易的交易哈希缩写。单击哈希将在 L1 区块浏览器中打开交易详细信息页面的新标签页。
-   `Finalize Tx Hash`显示了将此 Scroll L2 区块的有效性证明提交给 Scroll L1 上的 rollup 合约，Scroll L1 的交易哈希缩写。单击哈希将在 Scroll L1 区块浏览器中打开交易详情页面的新标签卡。