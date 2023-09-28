2023年5月14日，ETHGlobal Lisbon黑客松在里斯本落下帷幕。参赛的 183 个项目中有 46 个部署在了 Scroll 上 ，其中有 3 个进入前 10 名。恭喜所有的开发者。

以下是在本次黑客马拉松中部署在 Scroll 上的一些激动人心的项目。

## Guardian Oracle-Keeper Protocol
一种新颖的链上协议，使用具有附加功能的包装代币进行更有效的清算。具体来说，协议通过一对守护者代币实现，可以包装任何一对 ERC20 代币并将它们部署在一个或多个 DEX 上。这些代币监听“转账”功能，并在交易发生后立即计算价格，并调用回调函数，这些回调通常是由 DeFi 协议执行的清算或再平衡操作。
- ETHGlobal: [Guardian Oracle-Keeper Protocol | ETHGlobal](https://ethglobal.com/showcase/guardian-oracle-keeper-protocol-rpcws)
- Github: [GitHub - jordan-public/guardian-oracle-keeper: Guardian Oracle-Keeper Protocol](https://github.com/jordan-public/guardian-oracle-keeper)

## Natural Chain
“Natural Chain”是一个人工智能工具包，使用户能够使用自然语言与EVM生态系统进行交互，实现创建和部署智能合约，查询等任务。
具体来说，Natural Chain使用LangChain来设计代理，将执行与EVM生态系统相关的复杂任务，以及执行此操作所需的工具。LangChain允许使用几乎任何可用的大型语言模型。黑客松中使用 Chat GPT 3.5，因为它兼顾了性能、低廉的价格和速度。
- Demo: [Streamlit](https://naturalchain.cenit.finance/)
- ETHGlobal: [Natural Chain - AI Toolkit for the Blockchain | ETHGlobal](https://ethglobal.com/showcase/natural-chain-ai-toolkit-for-the-blockchain-ho5mq)
- Github: [GitHub - miguel-bm/naturalchain](https://github.com/miguel-bm/naturalchain)


## Credential Corgi
Credential Corgi 使用 GPT-4 创建认证标准，颁发与ZKP兼容的证书，以及第三方和凭证持有者之间的请求证明交换。
Credential Corgi 合约部署在八个 EVM 链上，UI 是使用 Next.js 在 TypeScript 中构建的 Web 应用程序。为了生成零知识证明，Credential Corgi 使用了SnarkyJS库。
- Demo: [https://credentialcorgi.com](https://credentialcorgi.com/)
- ETHGlobal: [Credential Corgi | ETHGlobal](https://ethglobal.com/showcase/credential-corgi-a7a0r)
- Github: [GitHub - tkeith/credential-corgi](https://github.com/tkeith/credential-corgi)

## Donation Station
Donation Station使得你可以在自己喜欢的 L2 上捐赠，以及让你通过浏览器插件直接在 Twitter 上捐赠，从而在下一轮Gitcoin捐赠中为你节省高昂的Gas费。
- ETHGlobal: [Donation Station | ETHGlobal](https://ethglobal.com/showcase/donation-station-g09ok)
- Github: [GitHub - lennardevertz/ethLisbon2023: ETHGlobal Lisbon 2023 Hackathon project](https://github.com/lennardevertz/ethLisbon2023)


## Kinetex
“Kinetex”是一个基于ZK证明的点对点交易平台，具有即时订单确认和低Gas成本。与专业做市商一起安全快速地转移流动性。
具体来说，Kinetex从SuccinctLabs分叉了LightClient实现，对其中用于跨链交易进行了更改和优化。主要区别在于即时跨链转账和强大的气体优化。设法在所有支持的网络上将Gas成本降低到 60-90k 左右。
- Demo: [Kinetex v2 | Proto](https://dp.kinetex.io/)
- ETHGlobal: [Kinetex Flash (zk) | ETHGlobal](https://ethglobal.com/showcase/kinetex-flash-zk-zh8vj)
- Github: [GitHub - KinetexNetwork/ethglobal-lisbon-zk-resolving](https://github.com/KinetexNetwork/ethglobal-lisbon-zk-resolving)

## Shortly
Shortly是一个 web3 营销工具。它允许团队跟踪、激励和奖励他们的附属公司、DAO 贡献者，从而团队可以通过社区生成的内容增加流量。
- Demo: [Shortly | ETHGlobal Lisbon Hack](https://shortlylisbon.webflow.io/)
- ETHGlobal: [Shortly | ETHGlobal](https://ethglobal.com/showcase/shortly-a1c05)
- Github: [GitHub - kaymomin/shortly](https://github.com/kaymomin/shortly)


感谢每一位来到里斯本与我们一起度过周末的黑客！

我们很快就会在 ETHDam 再次见到你们。