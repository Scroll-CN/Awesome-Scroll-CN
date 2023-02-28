# 常见错误

## MetaMask 交易中不正确的Nonce

当存储在您的 MetaMask 钱包中的本地 nonce 与 Scroll 测试网节点中的 nonce 不同时，您将遇到此错误。这可能是因为最近有一笔排队中的交易，或者是测试网因修复bug和功能发布而重置。尽管我们的目标是尽量减少这种情况，但我们可能会在 Alpha 阶段重置网络以加快开发进展。我们会在重置网络前提前通知用户。

要解决此问题，您需要在 MetaMask 中为 Scroll Alpha 网络重置您的帐户。重置帐户的步骤是：

1. 在浏览器中打开**MetaMask**
2. 在顶部区域选择 **Scroll Alpha Testnet**
3. 点击顶部右侧的 **账户图标**
4. 选择 **设置**
5. 前往 **高级**
6. 单击 **重置帐户**

在 MetaMask 账户重置后，您不会丢失任何资产。

*注意：删除并重新添加网络不足以解决此问题 - 您必须上重置您的帐户。*

## 跨链桥/交易没有任何响应

如果没有错误或控制台日志出现，这可能是由于 nonce 问题，请按照上文所述重置您的 MetaMask 帐户

## 区块链浏览器显示“内部服务器错误

使用隐身窗口，或打开浏览器开发人员控制台并删除`_explorer_key` cookie（或所有 cookie：https://www.contentstack.com/docs/developers/how-to-guides/clear-caches-and-cookies-in-different-browsers/）。