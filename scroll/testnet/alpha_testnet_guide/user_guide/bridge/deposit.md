# 从Goerli 存款至 Scroll Alpha

### 使用说明

1. 首先，切换到钱包中的**Goerli网络。**
2. 在跨链桥应用程序中，确保**Goerli**在顶部，**Scroll Alpha**在底部。您可以点击“ **↓** ”按钮切换位置。
3. 选择您要从 Goerli 转移到 Scroll Alpha 的代币（`ETH`）
4. 如果这是您第一次转移代`ETH`币，您需要 **批准** Goerli 跨链桥合约才能访问您的 `ETH` 代币。
5. 接下来，单击 **发送** 按钮进行存款。您的钱包会弹出一个窗口，要求确认转账交易。
6. 转账交易发送并确认后，代币将从您的 Goerli 钱包中扣除。

### 代币何时会到达您的 Scroll Alpha 钱包？

大约需要 **8～14 分钟（等待Goerli上的区块最终安全确认 ）**，代币将出现在您的 Scroll Alpha 钱包中， 您可以通过如下方式查看存款交易进度：

1. 单击跨链桥应用程序右上角的钱包地址。 

	![](scroll/testnet/alpha_testnet_guide/user_guide/bridge/img/deposit_1.png)

弹出面板列出了您在跨链桥应用程序中进行的最近交易（见下图）。有两种状态：L1 状态和L2 状态。此时，因为我们是从 L1 跨至 L2 ，一旦在Goerli测试网上被最终确认，将会显示 `success`状态。随后，你的自己将会被中继至L2

2.  点击最新的 Goerli 交易哈希

    ![](scroll/testnet/alpha_testnet_guide/user_guide/bridge/img/deposit_2.png)

将会在新的标签页显示交易详情，您可以看到此笔交易已经在 Goerli 上得到确认

![](scroll/testnet/alpha_testnet_guide/user_guide/bridge/img/deposit_3.png)

3.  返回[跨链桥](https://scroll.io/prealpha/bridge)应用。一旦您的交易在 L2 上的状态显示`success`，您应该会看到 Scroll Alpha 钱包中的资金和交易哈希：

    ![](scroll/testnet/alpha_testnet_guide/user_guide/bridge/img/deposit_4.png)

