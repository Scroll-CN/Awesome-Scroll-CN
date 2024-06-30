
ETHGlobal Circuit Breaker 黑客松落下了帷幕，我们收到了非常多项目的申请，非常感谢社区开发者对 Scroll 的热情。

此次黑客松，我们捐赠了 10,000 美元的奖金池，并将其分配给两个特殊的赛道，目的是鼓励 Scroll 上的开发者将他们的才能运用到需求最大的领域。 
- Scroll 上最好的 ZK 隐私应用
- Scroll 上的最佳扩容 ZK 使用

最终 Shadow Warfare、Unknown Finance、priv.cast 和 Urban Odyssey 四个团队赢得了我们的奖金。


## 隐私赛道
## Pri.cast

随着 Farcaster 将自己打造成领先的加密社交平台，建立抵御女巫攻击的工具的需求日益增长。 通过利用 ZK 证明，priv.cast 正在使用 Frames 实现抗女巫攻击的隐私投票。

priv.cast 使用了 Noir、Anon Aadhaar、Airstack、Farcaster 构建并部署在 Scroll 上。用户可以在中创建民意调查。用户通过生成零知识证明对民意调查进行投票，该零知识证明经过验证并发送到应用程序的外部存储。一旦每个人都完成了投票，所有证明的 Merkle 根就会使用递归证明得到。最终证明上传到链上以更新用户的投票。Airstack 用于获取用户的配置文件。生成并验证 Anon Aadhar 证明，以防止通过多个远端配置文件投票来防止女巫攻击。


- ETHGlobal: https://ethglobal.com/showcase/priv-cast-hzitq
- Demo: https://priv-cast.vercel.app/
- GitHub: https://github.com/gabrielantonyxaviour/priv.cast


### Urban Odyssey

Urban Odyssey 是一款沉浸式、协作 P2E 游戏，将玩家带入一个独特的链上世界，其主要目标是将自然和技术的最佳部分结合起来，以改善城市生活。

Urban Odyssey 邀请玩家扮演两个富有远见的角色：绿色技术和可持续城市发展的倡导者 EcoGuardians 以及先进数字基础设施和智慧城市解决方案的先驱 TechnoMads 。通过利用现实世界元数据的力量，玩家将把他们的城市转变为繁荣的生态系统或尖端技术中心。
- ETHGlobal: https://ethglobal.com/showcase/urban-odyssey-d0vor
- Demo: https://urban-odyssey.vercel.app/
- GitHub: https://github.com/neerajnerlekar/circuitbreaker-urbanOdyssey


## 扩容赛道


### Shadow Warfare

Shadow Warfare 是一个充满众多城市的世界中，每个独特的地点都设有防御工事，玩家将把自己定位为这些地点的“领导者”，在那里他们将使用 ZK 证明来隐藏防御军队，不让对手的领导者发现。

Shadow Warfare 使用 Noir 生成这些证明，然后使用部署的 EVM 验证器在链上进行验证，确保规则合规性。只有军队的组成哈希存储在链上，以保持战略保密性和完整性。


- ETHGlobal: https://ethglobal.com/showcase/shadow-warfare-gxvty
- GitHub: https://github.com/Switch-Labs/shadow_warfare/blob/main/README.md

### Unknown Finance

Unknown Finance 是一款将现实生活中的信用评分带入 DeFi 的应用程序，为某些社区提供抵押贷款不足的可能性。

假设您是某个农民协会的成员，该协会在 AAVE 中拥有活跃的存款，可以代表其成员产生一些收益。例如，通过使用 Unknown Finance，该社区的任何成员都可以证明他/她的钱包地址属于具有传统实体信用评分的真实人，社区可以信任该信用评分来委托营运资金的信用额度。作为未来的一步，我们希望将该系统与电子邮件钱包集成，以进一步减少入门摩擦，并将传统社区带入 DeFi

- ETHGlobal: https://ethglobal.com/showcase/unknown-finance-e24oc
- Demo: https://proof-of-fun-frontend.vercel.app/
- GitHub: https://github.com/dacarva/proof-of-fun