ETHBarcelona 活动期间，Scroll的研究员 Toghrul Maharramov 发表了关于zkRollup不变性和可升级性的演讲。
![](Immutablility%20and%20Upgradeability_%20Security%20vs%20Security%20-%20Toghrul%20Maharramov%20-%20ETHBarcelona%20Talk.jpeg)
对于zkRollup而言，不变性和可升级性是安全性的两个不同纬度。Arbitrum, Optimism, Polygon zkEVM, Scroll, Starknet, zkSync 这些Rollup通常会有两类情况，一类拥有不变性，一类拥有可升级性，但都是出于安全性角度的不同取舍。
![](Immutablility%20and%20Upgradeability_%20Security%20vs%20Security%20-%20Toghrul%20Maharramov%20-%20ETHBarcelona%20Talk%203.jpeg)

在我们的情况下，我们假设Rollup拥有28天的升级延迟。
![](Immutablility%20and%20Upgradeability_%20Security%20vs%20Security%20-%20Toghrul%20Maharramov%20-%20ETHBarcelona%20Talk%208.jpeg)
通常，我们在对Rollup做升级时，我们会在Base Layer重新部署新版本的跨链桥，新版本的Rollup将直接链接新版本的跨链桥。
![](Immutablility%20and%20Upgradeability_%20Security%20vs%20Security%20-%20Toghrul%20Maharramov%20-%20ETHBarcelona%20Talk%2011.jpeg)
有时我们只需要对跨链桥合约做升级，Rollup将直接链接新版本的跨链桥。
![](Immutablility%20and%20Upgradeability_%20Security%20vs%20Security%20-%20Toghrul%20Maharramov%20-%20ETHBarcelona%20Talk%2013.jpeg)

不变性的优点在于，不需同步假设，没有复杂的退出机制，防止Rug
![](Immutablility%20and%20Upgradeability_%20Security%20vs%20Security%20-%20Toghrul%20Maharramov%20-%20ETHBarcelona%20Talk%2014.jpeg)
但同样也有缺点，在出现漏洞受到攻击时协议较为脆弱，在需要协议升级时没有状态迁移的机制。
![](Immutablility%20and%20Upgradeability_%20Security%20vs%20Security%20-%20Toghrul%20Maharramov%20-%20ETHBarcelona%20Talk%2015.jpeg)

可升级性的优点在于可以处理出现漏洞的脆弱性，可以引入协议升级
![](Immutablility%20and%20Upgradeability_%20Security%20vs%20Security%20-%20Toghrul%20Maharramov%20-%20ETHBarcelona%20Talk%2016.jpeg)
可升级性的缺点在于需要同步假设，有复杂的退出机制，无法防止Rug
![](Immutablility%20and%20Upgradeability_%20Security%20vs%20Security%20-%20Toghrul%20Maharramov%20-%20ETHBarcelona%20Talk%2017.jpeg)


对于zkEVM而言，理想状态下，我们希望zkEVM拥有不变性来保障安全性，但同时，我们希望zkEVM保持兼容性，因此需要有可升级性。
![](Immutablility%20and%20Upgradeability_%20Security%20vs%20Security%20-%20Toghrul%20Maharramov%20-%20ETHBarcelona%20Talk%2018.jpeg)


因此现在的一个方案是，在有延迟升级机制下，引入安全委员会来快速通过延迟时间。
![](Immutablility%20and%20Upgradeability_%20Security%20vs%20Security%20-%20Toghrul%20Maharramov%20-%20ETHBarcelona%20Talk%2019.jpeg)
这里的安全委员会，是外部的领域专业人士的集合，例如L2Beat。只要他们的投票达到了规定的阈值，他们将可以快速通过延迟，进行升级。
![](Immutablility%20and%20Upgradeability_%20Security%20vs%20Security%20-%20Toghrul%20Maharramov%20-%20ETHBarcelona%20Talk%2020.jpeg)

通常情况下，在内部团队3/5的多签钱包发起28天的延迟升级，9/12的安全委员会多签可以发起快速通过延迟。
![](Immutablility%20and%20Upgradeability_%20Security%20vs%20Security%20-%20Toghrul%20Maharramov%20-%20ETHBarcelona%20Talk%2021.jpeg)

引入安全委员会也会带来新的问题，例如协调问题，还有潜在的不做验证直接投票快速通过的问题。
![](Immutablility%20and%20Upgradeability_%20Security%20vs%20Security%20-%20Toghrul%20Maharramov%20-%20ETHBarcelona%20Talk%2022.jpeg)

另一个方案是Enshrined Validating Bridge。原理是不再通过跨链桥合约来验证L2的证明，而是通过内嵌在L1协议中，通过社会共识来验证证明。
![](Immutablility%20and%20Upgradeability_%20Security%20vs%20Security%20-%20Toghrul%20Maharramov%20-%20ETHBarcelona%20Talk%2023.jpeg)
![](Immutablility%20and%20Upgradeability_%20Security%20vs%20Security%20-%20Toghrul%20Maharramov%20-%20ETHBarcelona%20Talk%2024.jpeg)

缺点是影响了L1的中立性，增加了L1的协调负担。
![](Immutablility%20and%20Upgradeability_%20Security%20vs%20Security%20-%20Toghrul%20Maharramov%20-%20ETHBarcelona%20Talk%2025.jpeg)
并且增加了L1的升级难度，需要设计同质化的验证跨链桥合约。
![](Immutablility%20and%20Upgradeability_%20Security%20vs%20Security%20-%20Toghrul%20Maharramov%20-%20ETHBarcelona%20Talk%2026.jpeg)


所以有完美的解决方案吗，实际上目前并不存在。每一个上文提出的方案都对安全性的其他方面做出了取舍。当然我们期待在未来两年，随着L2协议的完善，会达成共识有一个合理的解决方案。
![](Immutablility%20and%20Upgradeability_%20Security%20vs%20Security%20-%20Toghrul%20Maharramov%20-%20ETHBarcelona%20Talk%2027.jpeg)
![](Immutablility%20and%20Upgradeability_%20Security%20vs%20Security%20-%20Toghrul%20Maharramov%20-%20ETHBarcelona%20Talk%2028.jpeg)
![](Immutablility%20and%20Upgradeability_%20Security%20vs%20Security%20-%20Toghrul%20Maharramov%20-%20ETHBarcelona%20Talk%2029.jpeg)