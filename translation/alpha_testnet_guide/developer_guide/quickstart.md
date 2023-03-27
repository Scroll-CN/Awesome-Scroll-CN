# 开发者快速上手

在 Scroll 上，你最喜欢的智能合约开发测试工具都可以正常使用。

由于 Scroll 是字节码层面的 EVM 等效，你只需将你的开发工具指向 Scroll Alpha Testnet RPC Provider。

如果你遇到任何问题，请联系[我们的 Discord](https://discord.gg/scroll)。

## 获取测试网ETH

在Scroll上构建之前，您需要一些测试代币。查看我们的[水龙头](../user_guide/faucet.md)页面，在Goerli上获得 ETH 测试代币。然后，使用我们的[跨链桥](../user_guide/bridge/README.md)将 ETH 测试代币桥接到 Scroll Alpha 测试网（Layer 2）。

如需详细指引，可以从用​​户指南的[设置](../user_guide/setup.md)页面开始。

## 网络配置

使用下表将您的以太坊工具配置到 Scroll Alpha 测试网。
| 网络名字 | Goerli 测试网                                                         | Scroll Alpha 测试网                  |
| -------- | ---------------------------------------------------------------------- | --------------------------------- |
| RPC URL  | https://endpoints.omniatech.io/v1/eth/goerli/public | https://alpha-rpc.scroll.io/l2 |
| Chain ID | 5                                                                 | 534353                            |
| 代币符号 | ETH                                  | ETH                     |
| 区块链浏览器   |     https://goerli.etherscan.io/                                                                  |      https://blockscout.scroll.io/                          |


## 配置工具

### Hardhat

修改你的 Hardhat 配置文件`hardhat.config.ts`以指向 Scroll Alpha 测试网公开 RPC。

```typescript
...

const config: HardhatUserConfig = {
  ...
  networks: {
    scrollAlpha: {
      url: "https://alpha-rpc.scroll.io/l2" || "",
      accounts:
        process.env.PRIVATE_KEY !== undefined ? [process.env.PRIVATE_KEY] : [],
    },
  },
};

...
```

### Foundary

要使用 Scroll Alpha 测试网公共 RPC 进行部署，请运行：

```
forge create ... --rpc-url=https://alpha-rpc.scroll.io/l2
```

### Remix Web IDE

编译合约后，使用 Remix 进行部署的最简单方法是[设置 Metamask](../user_guide/setup.md)，然后选择“Scroll Alpha Testnet”网络。

![在MetaMask中选择 Scroll AlphaTestnet 作为网络](img/quickstart_1.png)

现在，在“Deploy and Run Transactions”选项卡中，点击“Environment”下拉菜单并选择“Injected Provider - MetaMask”。

![在Remix中，使用 MetaMask 作为Network Provider以访问 Scroll Alpha 测试网](img/quickstart_2.png)

连接你的钱包并选择 Scroll Alpha Testnet。在 Remix 中应该会自动选择帐户，然后你单击“部署”即可。

### Truffle

假设你已经设置了 truffle 环境，请到 Truffle[配置文件](https://trufflesuite.com/docs/truffle/reference/configuration/) `truffle.js`，并确保已经安装了 HDWalletProvider：`npm install @truffle/hdwallet-provider@1.4.0`

```typescript
const HDWalletProvider = require("@truffle/hdwallet-provider")
...
module.exports = {
  networks: {
    scrollAlpha: {
      provider: () =>
        new HDWalletProvider(process.env.PRIVATE_KEY, "https://alpha-rpc.scroll.io/l2"),
      network_id: '*',
    },
  }
}
```

### Brownie

要添加 Scroll Alpha 测试网，请运行以下命令：

```
brownie networks add Ethereum scrollAlpha host=https://alpha-rpc.scroll.io/l2 chainid=534353
```

要将其设置为默认网络，请在项目配置文件中添加以下内容：

```
networks:
    default: scrollAlpha
```

### ether.js

在`ethers`脚本中设置 Scroll Alpha Testnet Provider。

```javascript
import { ethers } from 'ethers';

const provider = new ethers.providers.JsonRpcProvider(

'https://alpha-rpc.scroll.io/l2'

);
```

### scaffold-eth

要使用 Scaffold-eth 进行部署，你需要将 Hardhat 和 React 设置指向 Scroll Alpha 测试网。

#### 配置Hardhat

在`packages/hardhat/hardhat.config.js`文件中，你需要添加网络并选择其为默认网络。

```javascript
...
//
// Select the network you want to deploy to here:
//
const defaultNetwork = "scrollAlpha";
...
module.exports = {
...
	networks: {
...
          scrollAlpha: {
            url: "https://alpha-rpc.scroll.io/l2",
            accounts: {
              mnemonic: mnemonic(),
            },
          },
	}
...
}
```

确保为部署的钱包充值了资金！

#### 配置前端

要配置你的前端，你需要添加 Scroll Alpha Testnet 作为网络，然后选择它为默认设置。

添加网络，请修改`packages/react-app/src/constants.js`.

```javascript
...
export const NETWORKS = {
...
  scrollAlpha: {
    name: "scrollAlpha",
    color: "#e9d0b8",
    chainId: 534353,
    rpcUrl: "https://alpha-rpc.scroll.io/l2",
    blockExplorer: "https://blockscout.scroll.io",
  },
...
}
```

接下来，修改`packages/react-app/src/App.jsx`

```javascript
...
/// 📡 What chain are your contracts deployed to?
const initialNetwork = NETWORKS.scrollAlpha;
...
```
