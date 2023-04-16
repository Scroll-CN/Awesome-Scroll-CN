
ETHGlobal：Scaling Ethereum 2023 黑客松已经结束！在这三周内，我们收到了123个提交作品来竞争2万美元的赏金。

以下是获胜者名单：


# 赛道 1: 通过应用ZK为以太坊未来赋能

我们的“应用ZK赋能以太坊未来”类别是为了那些以有趣的方式利用ZK的dApp而设立的。

我们有两个获胜者，每人获得2500美元：

## ZKaptcha

ZKaptcha是一种基于零知识证明的验证码系统，由 @ketan_jog 和 @digamadev 开发。可用于保护 Web3 中的智能合约功能免受机器人的干扰。它使用基于文本的验证码挑战，需要用户识别弹出窗口中的文本并提交。该验证码系统使用零知识证明来证明用户知道哈希的原像，证明哈希属于该智能合约的有效验证码集合。
该项目由三个主要组件组成，可用于在链上实现低验证成本。后端由AWS服务器生成captcha图像，每个用户都有一组预生成的验证码图像，图像的哈希被构建成默克尔树，并定期更新客户端的默克尔树根；链下的证明者负责生成证明，证明用户正确解决了captcha问题；链上的验证者负责验证默克尔树和零知识证明，更新声誉评分。

ETH Global Showcase: https://ethglobal.com/showcase/zkaptcha-4q4qz
Demo: https://zkaptchasite.vercel.app/
Github: https://github.com/GraphitiLabs/zkaptcha


## zk proof of evm execution
zk proof of evm execution 由@sohamzemse构建，使用由PSE、Scroll和其他贡献者开发的zkevm电路以及Foundry的Anvil主网分叉来证明隐私区块。
整个项目使用Rust编写，并使用zkevm-circuits和ethers-rs。面临的挑战包括需要在Rust中编写所有代码来计算主网分叉的状态根，以及MPT电路尚在工作中。

ETH Global Showcase :https://ethglobal.com/showcase/zk-proof-of-evm-execution-ix960
Github: https://github.com/zemse/zk-proof-of-evm-execution


# 赛道 2:  便宜且快速的区块空间
在便宜且快速的区块空间赛道，我们同样有两个获胜者，每人获得2500美元：

## SCALE: Smart Contract Access Logic for EVM

SCALE 由 @ICscript、@Ajmal_Ahamed_K、@Aritra_Chat和@shainlafazan开发，可以使用访问逻辑控制智能合约的交互，从而更轻松地基于白名单控制与智能合约的交互。
Molecule Protocol是一种智能合约访问控制列表（ACL, ACLAccess Control List) 中间件，解决了区块链中的合规性问题。现在合规性仅通过用户界面实现，而智能合约仍然未被保护。链上数据昂贵且发布速度缓慢，而区块链不可变性使得更新数据（如扩大制裁名单）具有挑战性。Molecule Protocol通过使用 ACL 实现灵活的逻辑更改，并只发布一次数据以供所有智能合约使用来减少链上数据重复，从而解决了这些问题。

ETH Global Showcase: https://ethglobal.com/showcase/scale-smart-contract-access-logic-for-evm-65e08
Demo: https://goerli.etherscan.io/address/0xbc556d9f36ffc359f5b3ec814b296de8945e9e45#writeContract
Github: https://github.com/calvinmd/ScalingETH2023


## Fiat Paymaster

Fiat Paymaster 由@agfviggiano和@delaaxe开发，实现了一个帐户抽象支付中心，允许使用 PayPal 支付 Scroll 上的 gas 费。它利用了新的 ERC 4337 账户抽象标准。

ETH Global Showcase: https://ethglobal.com/showcase/fiat-paymaster-rm3k3
Demo: https://fiat-paymaster.vercel.app/
Github: https://github.com/aviggiano/fiat-paymaster


# 赛道 3 : # 在 Scroll 上部署智能合约

在我们的最后一个赛道“在 Scroll 上部署智能合约”中，我们共有 84 名获奖者成功将智能合约部署到 Scroll 上，分享了 10,000 美元的奖池！


最后感谢所有参赛者。我们之后还会有更多的黑客松，我们迫不及待地想看看开发者接下来会做什么！