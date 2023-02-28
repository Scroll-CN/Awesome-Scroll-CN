# 合约部署教程

我们的 Alpha 测试网允许社区在 Scroll 上部署智能合约。在本教程中，我们将说明如何在 Scroll 测试网上部署合约。这个[演示程序仓库](https://github.com/scroll-tech/scroll-contract-deploy-demo)说明了如何使用[Hardhat](https://hardhat.org/)和[Foundry](https://github.com/foundry-rs/foundry)进行合约部署。

{% hint style="info" %}

注意：在开始部署合约之前，你需要从Goerli的[水龙头](../user_guide/faucet.md)请求测试代币，并使用[跨链桥](https://scroll.io/alpha/bridge)将一些 `ETH` 从 Goerli 充值到 Scroll Alpha 。

{% endhint %}

### 使用 Hardhat 部署合约

1. 如果你还没有安装[nodejs](https://nodejs.org/en/download/)和[yarn](https://classic.yarnpkg.com/lang/en/docs/install)。
2. 克隆仓库并安装依赖项
```
git clone https://github.com/scroll-tech/scroll-contract-deploy-demo.git
cd scroll-contract-deploy-demo
yarn install
```
3. 在根目录下，按照示例 `.env.example` 创建文件`.env`。更改 `.env` 中的 `PRIVATE_KEY` 为你自己的帐户私钥
4. 运行 `yarn compile` 编译合约。
5. 运行 `yarn deploy:scrollTestnet` 以在 Scroll Alpha Testnet 上部署合约。
6. 运行 `yarn test` 进行 hardhat 测试。



### 实用 Foundry 部署合约
1. 克隆仓库
```
git clone https://github.com/scroll-tech/scroll-contract-deploy-demo.git
cd scroll-contract-deploy-demo
```
2.  安装 Foundry
```
curl -L https://foundry.paradigm.xyz | bash
foundryup
```
3. 运行 `forge build` 构建项目
4. 使用 Foundry 部署你的合约
```
forge create --rpc-url https://alpha-rpc.scroll.io/l2 \
  --value <lock_amount> \
  --constructor-args <unlock_time> \
  --private-key <your_private_key> \
  --legacy \
  contracts/Lock.sol:Lock
```
	- `<lock_amount>`是合约中要锁定的`ETH`的金额。尝试将其设置为少量，例如`0.0000001ether`.
	- `<unlock_time>`是 Unix 时间戳，在这之后锁定在合约中的资金将可以提取。尝试将其设置为将来的某个 Unix 时间戳，例如`1696118400`（此 Unix 时间戳对应于 2023 年 10 月 1 日）。

例如：

```
forge create --rpc-url https://alpha-rpc.scroll.io/l2 \
  --value 0.00000000002ether \
  --constructor-args 1696118400 \
  --private-key 0xabc123abc123abc123abc123abc123abc123abc123abc123abc123abc123abc1 \
  --legacy contracts/Lock.sol:Lock
```

### 问题和反馈

感谢参与和开发 Scroll Alpha 测试网。如果遇到任何问题，可以加入我们的[Discord](https://discord.com/invite/s84eJSdFhn)并在`developers`频道中询问我们。

#### 开发人员说明
1. .`SELFDESTRUCT` 操作码已被禁用，Scroll 中将不支持，因为它计划在之后从 EVM 中删除。
2. 目前，我们将 Layer 2 的 Gas 价格设置为与以太坊 Layer1 相同。但是，这些 Gas 价格未来可能会发生变化，根据证明成本进行匹配。我们将尽量努力减少这些更改，主要将在有安全需要的情况，对 ZK 不友好的预编译进行变更。