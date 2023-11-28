
本文提供了使用不同的以太坊开发环境在 Scroll Alpha 测试网上部署智能合约的详细说明：Truffle, Hardhat, Hardhat结合Truffle, Brownie, and Foundry。

## Truffle
Truffle是以太坊流行的开发环境，测试框架。要使用 Truffle 进行部署，请执行以下步骤：

使用 npm 全局安装 Truffle：

```
npm install -g truffle
```

您可以运行以下命令来创建初始项目：

```
truffle unbox metacoin
```

如果要创建完整的空白项目运行：
```
truffle init
```

删除Metacoin项目附带的旧合约和测试文件。将旧合约文件名替换为您的合约。这是要部署的新合约。

确保 truffle.config.js 中的 solidity 版本与 .sol 文件中的版本相同。

接下来运行仪表板：

```
truffle dashboard
```

这将在本地启动一个 Truffle仪表板。

现在，如果这不起作用，您可以通过以下方式调整truffle.config.js。

```
// Configure your compilers
  compilers: {
    solc: {
      version: "0.8.17",      // Fetch exact version from solc-bin
    }
  },
  dashboard: {
    port: 24013,
    host:"localhost" ,
  },
  
  networks: { 
    // ... network configurations, including the network named 'dashboard'
  }
```

通过运行Truffle迁移，合约将编译，您的浏览器应该会弹出。如果它没有转到本地：24013。

```
truffle migrate --network dashboard
```

批准交易并在 Truffle 仪表板上检查部署状态。

## Hardhat

Hardhat 是一个开发环境，用于编译、部署、测试和调试您的以太坊软件。若要使用Hardhat进行部署，请执行以下步骤：

安装 Hardhat 和 dotenv，这是一个将环境变量从 `.env` 文件加载到 `process.env` 中的模块。

```
npm install --save-dev hardhat
yarn add --dev hardhat
npm install dotenv
```

设置一个新的安全帽项目。
```
npx hardhat
```

删除新创建项目中的所有旧合约文件。更新 Hardhat 配置文件中的 Solidity 版本，并将您的新合约代码粘贴到新文件中。在项目的根目录中创建一个 `.env` 文件，您将在其中存储环境变量。

确保你有一个包含 \*.ENV 的 .GITIGNORE 文件。提交 .env 意味着提交私钥。

```
networks: {
  scroll: {
    url: "https://scroll-alphanet.public.blastapi.io",
    accounts: [process.env.PRIVATE_KEY]
  }
}
```

在 `hardhat.config.js` 文件的顶部添加这些行以包含 dotenv。

```
const dotenv = require("dotenv");
dotenv.config({ path: __dirname + '/.env' });
```

将这些行添加到 `scripts/deploy.js` 文件的顶部。

```
const [deployer] = await ethers.getSigners();
console.log("Deploying contracts with the account:", deployer.address);
```

使用Hardhat运行部署脚本。

```
npx hardhat run --network scroll scripts/deploy.js
```


## 带 Truffle 仪表盘的Hardhat

如果你更喜欢使用Hardhat进行开发，但又不想手动传递你的私钥，那么我得到了好消息。您可以将Truffle 仪表板与Hardhat一起使用。方法如下

将Truffle 仪表板添加到hardhat.config.js文件。

```
networks: {
  scroll: {
    url: "https://scroll-alphanet.public.blastapi.io",
    accounts: [process.env.PRIVATE_KEY]
  },
  'truffle-dashboard': {
    url: "http://localhost:24012/rpc"
  }
}
```

要使用 Truffle 仪表板使用 Hardhat 进行部署，请重复与常规 Hardhat 设置相同的步骤，但要部署智能合约，请使用 `truffle-dashboard` 网络运行部署脚本。

```
npx hardhat run --network truffle-dashboard scripts/deploy.js
```

## Brownie

Brownie是一个用于以太坊智能合约测试，调试，交互和部署的Python框架。要使用Brownie进行部署，请执行以下操作：

安装 Brownie 库和 `python-dotenv` 库来处理环境变量。

在我们这样做之前，我假设你自己的虚拟环境已经启动并运行。如果没有，并且想要动态创建一个依赖项，请先安装这些依赖项。

```
python3 -m pip install --user pipx
python3 -m pipx ensurepath
```

然后，您可以继续使用pipx命令而不是pip命令来创建虚拟环境并同时安装Brownie。

```
pipx install python-dotenv eth-brownie
```

如果你想用原本的方式做：

```
python3 -m venv ./myv
source ./myv/bin/activate
pip install python-dotenv eth-brownie
```

使用标准ERC20智能合约建立一个新的Brownie项目

```
brownie bake token
cd token
```

使用Scroll Alpha 测试网信息创建一个 `network-config.yaml` 文件。

```
live:
- name: Ethereum
  networks:
  - chainid: 534353
   explorer: https://blockscout.scroll.io/
   host: https://scroll-alphanet.public.blastapi.io
   id: testnet-scroll
   name: Testnet (scroll)
```

导入网络配置并使用私钥创建新帐户。my-new-account是示例名字，你可以在这里传递任何你想要的名字。在此提示之后，系统将要求您输入私钥并选择密码。

```
brownie networks import ./network-config.yaml
brownie accounts new my-new-account
```

编译您的合约。
```
brownie compile
```
如果选择使用 .env 文件，则需要从部署脚本中的 `.env` 文件加载私钥。确保你有一个包含 \*.ENV 的 .GITIGNORE 文件。提交 .env 意味着提交私钥。

```
import os
from dotenv import load_dotenv 

load_dotenv()  # loads .env

private_key = os.getenv("PRIVATE_KEY")

account = accounts.add(os.getenv("PRIVATE_KEY"))
```

调整部署脚本 `token.py` 以使用新帐户和网络。

```
from brownie import Token, accounts

account = accounts.load("my-new-account")

def main():
    return Token.deploy("Test Token", "TST", 18, 1e21, {'from': account})
```

使用 Brownie 运行部署脚本。

```
brownie run token.py --network testnet-scroll
```


## Foundry

Foundry是一个基于Rust的以太坊智能合约开发工具包。它具有内置测试、自动合约 API 生成以及对不同以太坊网络的支持。

初始化一个新的Foundry项目并构建它。

```
forge init foundry-demo
cd foundry-demo && forge build
```

安装OpenZeppelin合约。

```
forge install OpenZeppelin/openzeppelin-contracts
```

在根文件夹中创建一个重新映射文件，允许您为项目的依赖项指定 Solidity 重新映射。

```
forge remappings > remappings.txt
```

编译您的合约

```
forge build
```

部署合约。正如你所知道的，你可以绕过部署脚本的创建，但不建议这样做。对于黑客松来说，这可能很好，但对于任何智能合约开发，你不应该像这样传递你的私钥。

不要忘记最后的遗留标志

```
forge create --rpc-url https://alpha-rpc.scroll.io/l2 --private-key <PRIVATE_KEY_HERE> src/EtherWallet.sol:EtherWallet --legacy
```

相反，您可以创建一个 .env 文件。再确保您有一个 .gitignore 文件并包含 \*.env。

接下来，创建文件夹 **script**（如果尚不存在）并包含部署脚本。它应该看起来像这样。这是官方文档中的一个例子。

```
// SPDX-License-Identifier: UNLICENSED
pragma solidity ^0.8.13;

import "forge-std/Script.sol";
import "../src/NFT.sol";

contract MyScript is Script {
    function run() external {
        uint256 deployerPrivateKey = vm.envUint("PRIVATE_KEY");
        vm.startBroadcast(deployerPrivateKey);

        NFT nft = new NFT("NFT_tutorial", "TUT", "baseUri");

        vm.stopBroadcast();
    }
}
```

在项目运行的根目录下

```
source .env
```

其次

```
forge script script/<SCRIPTNAME>.s.sol:MyScript --rpc-url https://alpha-rpc.scroll.io/l2 --broadcast --verify -vvvv --legacy
```

如果将 rpc url 作为环境变量传递，则还可以运行以下命令。在此命令中，我假设您将 rpc url 的变量命名为SCROLL_RPC_URL

```
forge script script/NFT.s.sol:MyScript --rpc-url $SCROLL_RPC_URL --broadcast --verify -vvvv --legace
```

每个开发环境都有其优势和功能。尝试在 Scroll Alpha 测试网上部署您的合约，看看哪一个最适合您的工作流程。请记住在确保您的私钥安全下编码！