2023 年 11 月 17 日至 2023 年 11 月 19 日，ETHGlobal Istanbul 黑客松成功举办。

在提交的 427 个项目中，有 160 多个团队选择在 Scroll 上进行开发，分享了我们一共 17,000 美元的奖金池。并且我们很自豪的是，我们延续了之前 ETHGlobal 的记录，依然是部署项目最多的 Layer2。

我们的 17,000 美元奖金池分为两条赛道，分别是
- 最佳用例奖：共 $10,000，10 个团队，每个团队各 $1000，
- 部署奖池：共 $7,000，在总共 160 份参赛作品中，有 125 支团队获得了我们的奖池份额。

我们将在此着重介绍我们的 10 个最佳用例奖获胜团队


## Stark-Bridge-n-Frog

Starkcurve 是 Starknet 网络的原生曲线。原子互换是一种能够在两条链之间安全地交换货币的机制。为了实现这一点，它要求两个网络在同一椭圆曲线上运行。在部署了 ERC4337 后，我们可以使用 starkcurve ，在 starknet 和任何兼容 ERC4337 的 L1/L2 之间部署。

Stark-Bridge-n-Frog 开发了一个 Starkcurve Schnorr 曲线验证器，并集成到原子互换的跨链器中。然后，我们通过在 Layer 2 上部署青蛙市场来演示跨链过程。

- ETHGlobal： 
	- https://ethglobal.com/showcase/stark-bridge-n-frog-gqv3u
- Github：
	- https://github.com/rdubois-crypto/Stark-Bridge-n-Frog


## Memento

Memento 是作为以太坊改进提案 (EIP) 的概念证明而开发的：通过可验证延迟函数 (VDF) 进行“时间胶囊”加密。该 EIP 通过引入一种对区块链上的数据进行安全、时间锁定加密的机制，解决了以太坊生态系统中的一个关键差距。

Memento 允许用户加密文本或文件，并设置解密内容的特定时间延迟，从而为以太坊中的数据管理带来新的安全性和完整性水平。该应用程序设计为用户友好型，使用户能够轻松创建时间封装的内容，这些内容在预定的解锁时间之前保持加密状态。


- Demo：
	- https://www.memento.run/
- ETHGlobal： 
	- https://ethglobal.com/showcase/memento-vingq
- Github：
	- https://github.com/igorperic17/memento/


## Footy Stars

FootyStars 是一个可验证的足球比赛模拟器，为未来现实世界的足球比赛奠定了基础。
- 比赛结果是“无需信任的”，也就是任何人都可以通过检查模拟是否正确执行从链下 zkML 生成的证明来验证模拟是否正确。
- 真实世界：FootyStars 提供比赛结果的能力意味着它现在足以有利于涉及现实世界的游戏比赛。
- NFT 驱动的开放经济：玩家卡牌不再被锁定在游戏开发者的“围墙”中，因为 FootyStars 中的每个玩家都是 ERC721 NFT（这意味着经理可以轻松地交易它们，甚至可以使用它们参与 DeFi，就像 BAYC 等 PFP NFT 一样）。
- 可投资的收藏品：球员评分由球员的真实表现决定（通过透明的算法，其中 Opta / Squawka 等多个体育数据提供商的数据的外部预言机将充当数据源）以及 DAO 选举的 FootyStars 陪审团，将球员卡评级的权力民主化（这增强了 FootyStars 球员卡的可投资性， 因为没有中心化实体掌握任何玩家卡 NFT 的评级）。

- ETHGlobal：
	- https://ethglobal.com/showcase/footy-stars-zw8ug
- Github：
	- https://github.com/Footy-Stars/README


## Prompt to Chain

Prompt to Chain 用于在 Scroll 上验证 AI 生成的内容。只有在区块链上生成提示语的 NFT 表示后，AI 才会开始生成 AI 图像。这确保了在区块链上没有等效的、可跟踪的 NFT 的情况下，无法生成任何 AI 图像。然后，智能合约所有者可以更新 NFT 的元数据，以证明其来源是由 AI 创建的图像。

Prompt to Chain 展示了区块链和人工智能如何协同保护用户免受未经验证的人工智能生成图像的影响。使用区块链提供的公开账本，它允许任何人验证何时如何生成了 AI 图像。奖激励LLM开发者将区块链解决方案作为防止滥用人工智能制造假新闻的保障措施。

- ETHGlobal：
	- https://ethglobal.com/showcase/prompt-to-chain-66hqe
- Github：
	- https://github.com/lorenz234/prompttochain


## ZKvote.cc

为了应对跨链投票的挑战，ZKvote.cc 通过跨链桥将投票代币与标准 ERC-20 集成，处理链下投票，并采用 ZK 证明进行安全的 L2 状态传输，确保了与现有跨链桥架构的兼容性。

- Demo: 
	- https://6559798734e0765ede2c6b37--zk-layer-vote.netlify.app/
- ETHGlobal：
	- https://ethglobal.com/showcase/zkvote-cc-rsvkt
- Github：
	- https://github.com/oxor-io/zk-layer-vote



## GoldenGate

GoldenGate 是一种跨链桥协议，它使链之间的桥接更容易、更便宜、更安全，同时改善用户体验。

用户可以以结构化意图的形式表达他们的需求：
例如将
”我在 Polygon 上有 10 个 ETH，我希望将其转移到 CELO 并在 30 秒内获得至少 9.98 个 ETH” 
翻译为
{ source_chain： 1101， destination_chain： 42220， input_token： ETH， output_token： ETH， input_amount： 10.0， minimum_output： 9.98， time_limit_seconds： 30 }

然后可以提供给求解器，然后求解器竞争提供最有竞争力的出价来满足此要求。


- ETHGlobal：
	- https://ethglobal.com/showcase/goldengate-g61rr
- Github：
	- https://github.com/konradstrachan/ethistanbulhackathon2023


## Ephemeral ZK L3s


Ephemeral ZK L3s 尝试使用状态通道为 web3 中的用户提供 web2 的游戏体验。通过递归聚合玩家在状态通道游戏中的状态更改，并在游戏结束时使用 zk 证明验证最终的游戏状态来最大限度地减少链上足迹。

- ETHGlobal：
	- https://ethglobal.com/showcase/ephemeral-zk-l3s-sv8rk
- Github：
	- https://github.com/rishotics/ephemeral_ZK_L3s


## zkmap

ZKMAP使用户能够生成特定于他们想要使用的应用程序的位置证明。这对于需要位置认证的服务特别有用。
聊天应用：根据生成的证据，特定区域内的用户可以访问指定的聊天室。该功能不仅用于社交互动，还可以作为本地化沟通和网络的平台。
这种位置证明系统开辟了多种应用： 活动出席验证：在活动中，用户可以生成单个证明来铸造出席证明 NFT。
地理限制：用户可以证明他们在某些地理边界之外，例如在美国境外，这对于访问特定的启动板或服务至关重要。
法律和安全应用：在刑事调查中，嫌疑人可以证明他们在事件发生时不在犯罪现场。
紧急服务完整性：在土耳其地震等灾难期间，该系统可以防止通过虚假呼叫恶意滥用紧急服务，确保帮助到达实际在灾区的人们。

- Demo：
	- https://linktr.ee/zkmap
- ETHGlobal：
	- https://ethglobal.com/showcase/zkmap-n2z06
- Github：
	- https://github.com/Volthai7us/eth-global-istanbul

## SaferBridge

SaferBridge 是一个信任最小化、无需许可的 Layer2 跨链桥，它通过 Layer 1 来路由资金。SaferBridge的每个部分都是无需信任和许可的。SaferBridge 首先将存款批量发送至 L1 合约，并先将交易 payload 发送到Layer 1，然后再返回至目标 Layer 2。这个过程为每个用户节省了 80% 的 gas 费用，唯一支付的协议费用是激励协议内部元件的各种步骤。

- ETHGlobal：
	- https://ethglobal.com/showcase/saferbridge-yr26i
- Github：
	- https://github.com/Robbiekruszynski/ist_bridge_2023


## Vitalik's Secret

Vitalik's Secret 是一个完全无需许可的谜题，即使是谜题创建者，也没有更多的线索。任何人都可以尝试破解它：提出最佳解决方案的人将获得奖品。

- Demo：
	- https://vitalik-secret.vercel.app/
- ETHGlobal：
	- https://ethglobal.com/showcase/vitaliks-secret-ajwsw
- Github：
	- https://github.com/wighawag/vitalik-secret/


我们衷心感谢我们的获奖者，以及所有参加黑客马拉松的开发者。 请继续关注我们下一次黑客松回顾电话会议的信息

我们将邀请一些获胜者现场演示他们的项目。 一会见 !💛