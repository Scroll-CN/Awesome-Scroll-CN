*原文：\<ZK Rewind: The Year in Recap\>*

*作者：Zero Knowledge Validator*

*翻译：Junwei*

> 我们回顾了 2022 年 ZK 行业的最大亮点。

随着 2022 年即将结束，我们想整理一份关于零知识技术领域进展的报告。对于整个行业来说，今年是忙碌的一年，但我们可以自信地说，2022 年是零知识证明实现突破的一年。

我们将涵盖如下部分： 

1. 公众兴趣
2. 融资
3. zk(E)VM之年
4. 测试网变得越来越快
5. ZK跨链桥
6. 新的语言
7. 可信设置登场
8. 从应用程序到 zkApps
9. 社区越来越大
10. 研究很重要
11. 结论

#  公众兴趣![📣](https://s.w.org/images/core/emoji/14.0.0/svg/1f4e3.svg)

根据谷歌趋势数据，2022 年人们对搜索“零知识证明”的兴趣激增，即使在今年下半年严酷的熊市中，兴趣也一直保持上升趋势。

![零知识技术在公共利益方面取得了突破性的一年](https://zkvalidator.com/wp-content/uploads/2022/12/Screenshot-2022-12-30-at-14.40.49.webp)

深入研究数据，关键字“SNARKs”在全球范围内的月搜索量在 100,000 到 1,000,000 之间，同比增长了 900%。

此外，[Decrypt](http://decrypt.co/)和[Coindesk](https://coindesk.com/)等以区块链为重点的主要媒体在 2022 年似乎也对零知识领域更感兴趣。就 Decrypt 而言，在 2021 年期间，它仅发表了 18 篇包含“零知识证明”一词的文章，而在2022年期间这个数字总共跃升至60件。Coindesk 也不例外，2022 年写了 81 篇零知识证明相关的文章，比 2021 年多了 54 篇。

![今年主流媒体对零知识技术的报道比以往任何时候都多。](https://zkvalidator.com/wp-content/uploads/2022/12/Articles-containing-the-term-Zero-Knowledge-Proofs.webp)

# 融资

投资者也跳上了 ZK 的列车。今年，我们计算出至少有超过 7.25 亿美元的资金用于“纯粹的零知识“参与者”。其中包括 Aleo、Aztec、Scroll、RiscZero、Matter Labs、Elusiv 和 Mina Protocol。最大的两轮融资是 Aleo 和[Matter Labs 各融资了 2 亿美元](https://techcrunch.com/2022/11/16/matter-labs-the-company-behind-zksync-raises-200-million-to-scale-ethereum/)，其次是[Aztec 的 1 亿美元融资](https://medium.com/aztec-protocol/aztec-raises-100-million-to-build-encrypted-ethereum-dd5062ba949c)。

除了私募股权融资外，一些基金会还承诺提供资金，以促进零知识应用在各自生态系统中的发展。Polkadot 发布了[Pioneers Prize](https://pioneersprize.polkadot.network/)计划，奖励 993,286 DOT，特别关注零知识技术。此外，NEAR 基金会在 Tornado Cash 事件发生后启动了一项资助计划，以支持 ZK 项目。

![In 2022, funding for Zero Knowledge projects reach over $700M.](https://zkvalidator.com/wp-content/uploads/2022/12/Earn-rewards-with-purpose..webp)

与此同时，零知识项目方和组织的联盟（如 ZKV）发起了[ZPrize 计划](https://www.zprize.io/)，奖金高达 700 万美元。这些竞赛旨在关键通用算法的性能、库的可用性和多样性等各个领域推动 ZK 技术发展的目标相一致的挑战。

今年，[Gitcoin ZK Side Rounds](https://zkvalidator.com/zk-tech-side-round-wrapup/)进行了三轮，匹配的奖金总额为 466,000 美元。在所有轮次中，不同的公共产品项目募集了近 100 万美元。这些Side Round主要侧重于提高可用性的工具类，以及创建新的应用程序以将用户带入 ZK 领域。有几个团队参与了这项计划，包括 ZKV、0xParc、Gnosis、Anoma、Penumbra、Mina、Geometry、Aztec 等。

#  zk(E)VM之年

https://youtu.be/mrf9HjjL_38

尽管2022年有很多突破，但今年的流行语可能是零知识虚拟机（zkVM）和零知识以太坊虚拟机（zkEVM）。许多项目正基于此构建一些变体，因为它们被视为高度可行的以太坊区块链的的扩展性解决方案。 

过去的这个夏天，在巴黎举行的 EthCC 活动期间，各个团队围绕这些解决方案发布了大量公告。

在那次活动中，Polygon 推出了他们的 zkEVM。Polygon 的 zkEVM 与传统的 zk rollup 不同，旨在实现与以太坊虚拟机操作码级别的兼容性，并提供更快、更便宜的交易。其在 7 月公布后，又进行了多次更新，最新消息是[主网前的最终版本公开测试网](https://polygon.technology/blog/final-approach-last-testnet-for-an-upgraded-polygon-zkevm)已于 12 月 21 日发布。 

另一方面，zkSync 同样在 EthCC 上宣布在 10 月份将他们的 zkVM，即zkSync 2.0 推送到主网上。虽然他们最终发布了一个非常精简的版本(Baby Alpha)，但 zkSync 2.0 将提供一些主要的差异点，例如帐户抽象、对 Solidity 和 Vyper 的支持以及 LLVM 编译器。 

也出现更多的玩家。最值得注意的公告之一是 RiscZero 构建了一个“通用零知识虚拟机”。此外，正在以太坊上构建基于 zkEVM 的 zkRollup 的 Scroll，推出了带演示功能的[Pre-Alpha 测试网](https://scroll.io/blog/preAlphaTestnet)（也在 EthCC 期间宣布！）。

#  测试网变得越来越快![⏩](https://s.w.org/images/core/emoji/14.0.0/svg/23e9.svg)

随着零知识技术在区块链行业的传播，三个有前景的参与者向主网迈出了重要的一步。

在今年的最后一个季度，Aleo 进行了重大改进并推出了他们的 Testnet 3，该测试网分为三个阶段。该版本允许开发者在网络上开始编写、部署和执行 Aleo 程序。此外，它还引入了一种新的共识算法 AleoBFT，它将PoS共识算法（基于 DiemBFT）与PoW的证明者激励方案相结合。

<iframe id="twitter-widget-0" scrolling="no" frameborder="0" allowtransparency="true" allowfullscreen="true" class="" title="推特推文" src="https://platform.twitter.com/embed/Tweet.html?dnt=false&amp;embedId=twitter-widget-0&amp;features=eyJ0ZndfdGltZWxpbmVfbGlzdCI6eyJidWNrZXQiOlsibGlua3RyLmVlIiwidHIuZWUiLCJ0ZXJyYS5jb20uYnIiLCJ3d3cubGlua3RyLmVlIiwid3d3LnRyLmVlIiwid3d3LnRlcnJhLmNvbS5iciJdLCJ2ZXJzaW9uIjpudWxsfSwidGZ3X2hvcml6b25fdGltZWxpbmVfMTIwMzQiOnsiYnVja2V0IjoidHJlYXRtZW50IiwidmVyc2lvbiI6bnVsbH0sInRmd190d2VldF9lZGl0X2JhY2tlbmQiOnsiYnVja2V0Ijoib24iLCJ2ZXJzaW9uIjpudWxsfSwidGZ3X3JlZnNyY19zZXNzaW9uIjp7ImJ1Y2tldCI6Im9uIiwidmVyc2lvbiI6bnVsbH0sInRmd19zaG93X2J1c2luZXNzX3ZlcmlmaWVkX2JhZGdlIjp7ImJ1Y2tldCI6Im9uIiwidmVyc2lvbiI6bnVsbH0sInRmd19jaGluX3BpbGxzXzE0NzQxIjp7ImJ1Y2tldCI6ImNvbG9yX2ljb25zIiwidmVyc2lvbiI6bnVsbH0sInRmd190d2VldF9yZXN1bHRfbWlncmF0aW9uXzEzOTc5Ijp7ImJ1Y2tldCI6InR3ZWV0X3Jlc3VsdCIsInZlcnNpb24iOm51bGx9LCJ0ZndfbWl4ZWRfbWVkaWFfMTU4OTciOnsiYnVja2V0IjoidHJlYXRtZW50IiwidmVyc2lvbiI6bnVsbH0sInRmd19zZW5zaXRpdmVfbWVkaWFfaW50ZXJzdGl0aWFsXzEzOTYzIjp7ImJ1Y2tldCI6ImludGVyc3RpdGlhbCIsInZlcnNpb24iOm51bGx9LCJ0ZndfZXhwZXJpbWVudHNfY29va2llX2V4cGlyYXRpb24iOnsiYnVja2V0IjoxMjA5NjAwLCJ2ZXJzaW9uIjpudWxsfSwidGZ3X2R1cGxpY2F0ZV9zY3JpYmVzX3RvX3NldHRpbmdzIjp7ImJ1Y2tldCI6Im9uIiwidmVyc2lvbiI6bnVsbH0sInRmd192aWRlb19obHNfZHluYW1pY19tYW5pZmVzdHNfMTUwODIiOnsiYnVja2V0IjoidHJ1ZV9iaXRyYXRlIiwidmVyc2lvbiI6bnVsbH0sInRmd19zaG93X2JsdWVfdmVyaWZpZWRfYmFkZ2UiOnsiYnVja2V0Ijoib24iLCJ2ZXJzaW9uIjpudWxsfSwidGZ3X3Nob3dfZ292X3ZlcmlmaWVkX2JhZGdlIjp7ImJ1Y2tldCI6Im9uIiwidmVyc2lvbiI6bnVsbH0sInRmd19zaG93X2J1c2luZXNzX2FmZmlsaWF0ZV9iYWRnZSI6eyJidWNrZXQiOiJvbiIsInZlcnNpb24iOm51bGx9LCJ0ZndfdHdlZXRfZWRpdF9mcm9udGVuZCI6eyJidWNrZXQiOiJvbiIsInZlcnNpb24iOm51bGx9fQ%3D%3D&amp;frame=false&amp;hideCard=false&amp;hideThread=false&amp;id=1599524202767425536&amp;lang=en&amp;origin=https%3A%2F%2Fzkvalidator.com%2Fzk-tech-in-2022%2F&amp;sessionId=2190aee250bff195dcf53c11d2504e03bbfebd8e&amp;theme=light&amp;widgetsVersion=a3525f077c700%3A1667415560940&amp;width=550px" data-tweet-id="1599524202767425536" style="box-sizing: border-box; max-width: 100%; width: 550px; margin: 0px; line-height: 1; border: none; position: static; visibility: visible; height: 370px; display: block; flex-grow: 1;"></iframe>

另一个在他们的测试网上取得进步的参与者是 Namada，它是 Anoma 的一个分支实例，将隐私资产带入了 Cosmos 生态系统。他们运行了一个隐私测试网，其中 ZKV 是验证者的一部分，并于 12 月 20 日启动了他们的第一个公共测试网。

最后但同样重要的是，我们也一直在关注 Penumbra 的发展，其是 Cosmos 的带隐私功能的去中心化交易所 (DEX)。在 2022 年期间，Penumbra 遵循快速发布的理念，推出了 35 个版本的公共测试网。在此过程中，该团队引入了重要的改进，例如新颖的分层承诺树，是一种 Merkle 树可以将 Penumbra 加速 4,000 倍，以及他们为 Penumbra 系统Poseidon哈希的零知识证明友好的实例，Poseidon377。

#  ZK跨链桥

https://youtu.be/f4kBUe2n0Qk

尽管处于非常早期的阶段，但一些项目已经在 ZK 领域取得了进展。我们指的是 ZK 跨链桥 — 无需信任的跨链桥接解决方案。他们旨在取代其他桥架构，这些架构是 2022 年的主要的安全问题之一。 

2022 年 10 月，Succinct 推出了[第一个演示](https://blog.succinct.xyz/post/2022/10/18/demo-instructions/)。该版本桥接了 Goerli（以太坊测试网）和 Gnosis 链，允许用户将“Succinct 代币”（他们创建的 ERC-20代币）存入 Goerli 存款合约，并在 Gnosis 链上接收铸造的 Succinct 代币。同样在 10 月，zkBridge 发表了他们在斯坦福构建的解决方案的[论文。](https://arxiv.org/pdf/2210.00264.pdf)

沿着这一思路的另一个新颖概念是 zkIBC 的诞生。该解决方案旨在使用零知识证明[将 Cosmos 的签名跨链通信协议 (IBC) 引入以太坊。](https://ethresear.ch/t/bringing-ibc-to-ethereum-using-zk-snarks/13634)大体上，他们基于以太坊上轻客户端状态的 zk-snark 证明验证，来构建最小化信任、可互操作的消息传递协议。

#  新的语言

在零知识项目中，公开了两种新语言。2022年初，Aleo推出LEO；一种受 Rust 启发的静态类型编程语言，专为编写隐私应用程序而构建。同时，在 10 月，Aztec 发布了他们的 Noir 语言。Noir 是一种基于 Rust 的领域特定语言 (DSL)，用于创建和验证零知识证明。 

#  可信设置登场

可信设置仪式（TCS，Trusted Setup Ceremonies）也是年底叙事的一部分。对于入门者来说，TSC 是一组参与者协作生成一组密码参数的过程，每次运行某些密码学协议时都必须使用这些参数。进行了TSC的项目是 Namada 和 Manta。前者共有 2510 人参加了[仪式](https://ceremony.namada.net/)，而后者则有超过 3559 名贡献者参与了这个[过程](https://twitter.com/MantaNetwork/status/1605763514517184512/photo/1)。据说以太坊基金会也计划在 2023 年初进行可信设置。 

![2022 年有很多 ZK 协议的可信设置仪式。](https://zkvalidator.com/wp-content/uploads/2022/12/Screenshot-2022-12-30-at-16.24.32.webp)

#  从应用程序到 zkApps

https://youtu.be/bjSAf41PWWI

11 月中旬，Mina Protocol 启动了一项计划，旨在促进所谓的 zkApps 的发展，zkApps是允许开发人员利用 Mina 的零知识技术的智能合约。这标志着 ZK 领域的一个重要里程碑，因为它可能会使用零知识释放出大量的创新和用例浪潮，并且由于构建 zkApps 的 SnarkyJS 库，可能会吸引超过 83,000 名的Typescript 开发人员中的一些人.

#  社区越来越大

随着零知识证明采用的增加，对这项技术感兴趣的人数大幅增加。[ZK Hack](https://zkhack.dev/)和 zkSummit是社区中的两个标志性事件，在这两个事件中都聚集了 2500 多人。这些活动的一个亮点是多个生态项目的聚集，以及生态系统新人接触重要项目的机会。

![ZK 事件是 2022 年的重要组成部分](https://zkvalidator.com/wp-content/uploads/2022/12/FgPPfv3WAAAuzBE-1024x768.webp)

#  研究很重要

认为零知识局限于区块链行业是错误的。通用研究正在兴起。学术界围绕该主题发表了大量论文。据[谷歌学术](https://scholar.google.com/scholar?hl=en&as_sdt=0%2C5&as_ylo=2022&as_yhi=2022&q=zero+knowledge&btnG=)统计，仅在 2022 年，零知识研究就发表了 67,100 篇文章，比 2021 年增加了 2,000 篇。但是，这方面的论文数量自 2018 年以来大幅下降。

#  结论

我们的年度总结到此结束！尽管过去一年的大部分叙述都是围绕可扩展性展开的，但我们希望在接下来的几个月里，我们能够看到一波使用零知识的以隐私为中心的协议浪潮。

2022 年是零知识证明取得突破的一年：ZK 技术正从研究走向区块链行业及现实世界的其他领域。我们认为这是一个更大可能性的开端。