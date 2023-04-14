*原文：<Why and How zk-SNARK Works 3: Non-interactivity & Distributed Setup>*

*翻译：Junwei*

# 非交互性

至此，我们有了一个交互式的零知识方案。为什么会这样？因为证明仅对原始验证者有效，所以没有其他人（其他验证者）可以信任相同的证明，因为：

- 验证者可以与证明者串通并公开那些可以用来伪造证明的秘密参数$s,α$， 如<u>Remark 3.1</u>所提到的一样

- 同样的，验证者可以自己生成虚假的证明

- 验证者必须存储$α$和$t(s)$，直到所有相关证明都得到验证，这可能会泄露秘密参数，这给额外的攻击面提供了机会

因此，需要与每个验证者进行单独交互，才能证明一个声明（在这里是多项式证明）。

虽然交互式证明系统有它的用例，例如，当证明者只想说服一个专门的验证者（称为指定的验证者，更多信息详见[[JSI96](https://medium.com/@imolfar/why-and-how-zk-snark-works-3-non-interactivity-distributed-setup-c0310c0e5d1c#4b56)]）时，证明不会被重复用于向其他人证明相同的声明，但是当需要同时（例如在区块链等分布式系统中）或永久令多方可信时，效率非常低。证明者将被要求始终保持在线并为每个验证者执行相同的计算。

因此，我们需要秘密参数是可重用的、公开的、可信的和不会被滥用的。

让我们首先考虑在生成秘密$(t(s), α)$ 之后如何将它们保密。我们可以像验证者在发送给证明者之前，对s的幂值加密一样对它们进行加密。然而，如<u>Remark 3.2</u>中所述，我们使用的同态加密不支持两个加密值的乘法，但这在检验$t(s)$和$h$加密值相乘以及$p$和$α$相乘都是必需。这正是密码学配对适用的地方。

## 加密值的乘法

密码学配对（双线性映射）是一种数学结构，可以表示为函数$e(g, g)$，给定来自数组的两个加密输入（例如$g^a、g^b$），允许将它们确定性地映射到一组不同数组输出中的乘法表示，即$e(g^a, g^b ) = e(g, g)^{ab}$：

![img](img/3-1.webp)

因为*源数组*和*输出数组*（通常称为群）不同，所以配对的结果不能用作另一个配对操作的输入。我们可以将输出群（也称为“目标群”）视为来自“不同的空间”。因此，我们不能将配对结果乘以另一个加密值，我们一次只能将两个加密值相乘。

在某种意义上，它类似于哈希函数，将所有可能的输入值映射到可能输出集合中的一个元素，并且它不是简单可逆的。

> *注意：乍一看，这种限制只会影响其他相关的功能，但有意思的是，在 zkSNARK中，它是方案安全性所依赖的最重要的属性，请参见<u>Remark 3.3</u>。*

配对函数$e(g, g)$的基本数学类比（技术上不正确的）是说，有一种方法可以“交换”每个输入的底数和指数，这样底数g在转换过程中被修改成指数，例如，$g^a → a^g$ 。然后将两个“交换”后的输入相乘，这样原始的$a$和$b$在相同的指数下可以相乘，例如：

$$
e(g^a,g^b)=a^a·b^g=(ab)^g
$$
因此，因为在“交换”过程中基数被改变，输出结果$(ab)^g$在另一组配对中（例如，$e (( ab ) ^g , g^d )$），不会产生所需的加密乘法$abd$。配对的核心属性可以用以下等式来表示：

$$
e(g^a,g^b)=e(g^b,g^a)=e(g^{ab},g^1)=e(g^1,g^{ab})=e(g^1,g^a)^b=e(g^1,g^1)^{ab}
$$
从技术上讲，配对的结果是目标集的不同生成元$g$下原始值的加密乘积，即$e(g^a, g^b ) = g^{ab}$。因此它具有同态加密的性质，例如，我们可以将多个配对的加密乘积加在一起：

$$
e(g^a,g^b)·e(g^c,g^d)=g^{ab}·g^{cd}=g^{ab+cd}=e(g,g)^{ab+cd}
$$

> *注意：密码学配对利用椭圆曲线来实现这些属性，因此从现在开始，符号 $g^n$将代表曲线上的生成元点累加n次，而不是我们在前面部分中使用的乘法群生成元。*

研究[[DBS04](https://medium.com/@imolfar/why-and-how-zk-snark-works-3-non-interactivity-distributed-setup-c0310c0e5d1c#0ea5)]为探索密码学配对提供了一个起点。

## 可信设置

有了密码学配对，我们现在可以准备设置安全的可重用公共参数。让我们假设我们信任一个诚实方来生成秘密值$s$和$α$。一旦$α$和$s$的所有幂值$（i = 0, 1, …, d）$以及相应的$α$位移被加密，就必须删除原始值

$$
g^{\alpha},g^{s^1},g^{\alphas^i}
$$
这些参数通常称为公共参考字符串或 CRS。CRS生成后，任何证明者和任何验证者都可以使用它来执行非交互式零知识证明协议。虽然不是至关重要的，但CRS 的优化版本将包括加密的目标多项式求值$g^{t(s)}$。

此外，CRS 分为两组$（i = 0, 1, …, d）$，包括：

- 证明密钥（也叫做求值密钥）：$$(g^{s^i}, g^{\alpha s^i}) $$

- 验证密钥：$$(g^{t(s)}, g^{\alpha}) $$

由于能够将加密值相乘，验证者可以在协议的最后一步检查多项式$t(s)$和$h$加密值相乘，以及$p$和$α$加密值相乘：

- 验证者可以利用验证密钥，处理从证明者处收到的加密后的多项式求值
	- 在加密空间内检验 $$p=t·h$$：
		-   $$e(g^p,g^1)=e(g^t,g^h)$$等价于$$e(g,g)^p=e(g,g)^{t·h} $$
	- 检验多项式约束：
		-   $$e(g^p,g^{\alpha})=e(g^{p^{'}}, g) $$

## 信任多方中的任何一方

可信设置应当是有效的，但因为上述的可信设置中，使用CRS时将不得不相信一方删除了α和s，而目前没有办法证明这一点（无知证明是一个活跃的研究领域[[DK18](https://medium.com/@imolfar/why-and-how-zk-snark-works-3-non-interactivity-distributed-setup-c0310c0e5d1c#2823)]），因此并不是有效的。我们有必要尽量减少或消除这种信任的需要。否则，不诚实的一方将能够在不被发现的情况下生成虚假的证明。

实现这一目标的其中一种方法，是由多方使用前面所介绍的数学工具，来生成复合CRS，这样任何一方都不知道秘密。下面，让我们考虑三个编号分别为A、B和C的参与方Alice、Bob和Carol，对于$i = 1 , 2 , …, d$：

- Alice随机取样随机数，并发布她的CRS

	 $$(g^{s_A^i},g^{\alpha_A},g^{\alpha_A S^i_A}) $$

- Bob随机取样随机数，并通过同态相乘聚合Alice的CRS

	$$({(g^{s_A^i})}^{s_B^i},{(g^{\alpha_A})}^{\alpha_B},{(g^{\alpha_A S^i_A})}^{\alpha_B S^i_B})=(g^{{(s_As_B)}^i},g^{\alpha_A\alpha_B},g^{\alpha_A\alpha_B {(s_As_B)}^i}) $$

	发布Alice-Bob两方的CRS

	$$(g^{s_{AB}^i},g^{\alpha_{AB}},g^{\alpha_{AB} S^i_{AB}}) $$

- Carol对她的随机数做相同的处理

	$$({(g^{s_{AB}^i})}^{s_C^i},{(g^{\alpha_{AB}})}^{\alpha_C},{(g^{\alpha_{AB} S^i_{AB}})}^{\alpha_C S^i_C})=(g^{{(s_As_Bs_C)}^i},g^{\alpha_A\alpha_B\alpha_C},g^{\alpha_A\alpha_B\alpha_C {(s_As_Bs_C)}^i}) $$

	发布Alice-Bob-Carol的CRS

	$$(g^{s_{ABC}^i},g^{\alpha_{ABC}},g^{\alpha_{ABC} S^i_{ABC}}) $$

协议的结果是，我们得到合成的$s^i$和$α$，其中

$$
s^i=s_A^is_B^is_C^i,\alpha=\alpha_A\alpha_B\alpha_C
$$
并且没有参与者知道其他参与者的秘密参数，除非他们串通。事实上，为了知道$s$和$α$，一个人必须与所有其他参与者串通一气。因此，只要其中一个参与方是诚实的，就不可能生成虚假证明。

> *注意：可以根据需要让尽可能多的参与者重复此过程。*

我们可能会遇到的问题是如何验证参与者是否使CRS的每个值保持一致，因为恶意方可以对随机取样多个不同的$s₁、s₂、… $和$α₁, α₂, …$（或直接提供随机数作为聚合的公共参考字符串），使CRS无效且不可用。

幸运的是，因为我们可以使用配对使加密值相乘，所以我们能够执行一致性检验，从第一个参数开始并确保后面的每一个参数都是从它派生而来。参与者发布的每个 CRS 都可以按如下方式进行检验：

- 我们将s的一次幂作为标准值，并检验所有其他次幂是否与其一致：

	$$e(g^{s^i},g)=e(g^{s^1},g^{i-1}) $$

	例如

	- 二阶：$$e(g^{s^2},g)=e(g^{s^1},g^{s^1})\Rightarrow e(g,g)^{s^2}=e(g,g)^{s^{1+1}} $$
	- 三阶：$$e(g^{s^3},g)=e(g^{s^1},g^{s^2})\Rightarrow e(g,g)^{s^3}=e(g,g)^{s^{1+2}} $$

- 我们现在检验上一步中α位移是否正确：

	$$e(g^{s^i},g^{\alpha})=e(g^{\alpha s^i},g)|_{i\in[d]} $$

	例如

	- 三阶：$$e(g^{s^3},g^{\alpha})=e(g^{\alpha s^3},g)\Rightarrow e(g,g)^{s^3·\alpha}=e(g,g)^{\alpha s^3} $$

其中$i ∈ {2 , …, d }$ 是“ i is in 2 , 3 , …, d ”的缩写形式，$[d]$是范围 1 , 2 , …, d的缩写形式，在下一节中这样表示符号更方便。

请注意，虽然我们检验了每个参与者使用的秘密参数一致性，但并没有对之后的每一个参与者（在我们的示例中为Bob和Carol）强制使用之前发布的CRS。因此，如果恶意方是整条链的最后一个，他可以忽略先前的CRS 并从头开始构造有效参数，就好像他是链上的第一个参与者，因此是唯一知道秘密值$s$和$α$的人。

我们可以通过额外要求除第一个参与者之外的每个人加密并发布他的秘密参数来解决这个问题，例如，Bob 还需要发布：

$$
(g^{s_B^i},g^{\alpha_B},g^{\alpha_Bs_B^i})|_{i \in[d]}
$$
这样就可以检验Bob的CRS是Alice的CRS的若干倍数，对于$i \in 1 , 2 ,…, d$：

- $e(g^{s^i_{AB}},g)=e(g^{s^i_{A}},g^{s^i_{B}})$
- $e(g^{\alpha_{AB}},g)=e(g^{\alpha_A},g^{\alpha_B})$
- $e(g^{\alpha_{AB}s^i_{AB}},g)=e(g^{\alpha_As_A^i},g^{\alpha_Bs_B^i})$

同样，Carol必须证明她的CRS 是Alice-Bob的CRS的若干倍数。

这是一个稳健的CRS设置方案，不完全依赖任何一方。事实上，即使所有其他人都串通起来，只要有一方诚实并删除并且永远不共享其秘密参数就可以了。因此，CRS设置（有时称为仪式[[Wil16](https://medium.com/@imolfar/why-and-how-zk-snark-works-3-non-interactivity-distributed-setup-c0310c0e5d1c#191c)]）中不相关的参与者越多，伪造证明的可能性就越小，如果对立的多方参与，则概率就变得可以忽略不计。该方案允许对CRS设置不熟悉的其他不受信任方加入，因为验证步骤可确保他们不会破坏（其中包括使用不可靠的$α$和$s$）最终的公共参考字符串。

# 多项式的简洁非交互零知识证明

我们现在准备巩固升级的zk-SNARKOP协议。为简洁起见，正式版本中我们将使用大括号来表示由其旁边下标所填充的一组元素，例如

$$
\{s^i\}_{i\in[d]}
$$
表示集合$s^1, s^2, …, s^d$ 。在对目标多项式$t(x)$和证明者多项式的次数$d$达成一致：

- 设置
	- 取样随机值$$s,\alpha $$
	- 计算加密值 $$g^{\alpha} $$和$${g^{s^i}}_{i \in[d]},{g^{\alpha s^i}}_{i\in{0,...,d}} $$
	- 证明密钥：$$({g^{s^i}}_{i\in[d]},{g^{\alpha s^i}}_{i\in{\{0,...,d\}}}) $$
	- 验证密钥：$$(g^{\alpha},g^{t(s)}) $$

- 证明
	- 分配系数$$\{c_i\}_{i\in\{0,...,d\}} $$（即知识）给多项式，$$p(x)=c_dx^d+...+c_1x^1+c_0x^0 $$
	- 计算多项式 $$h(x)=\frac{p(x)}{t(x)} $$
	- 利用$${g^{s^i}}_{i \in[d]} $$计算加密后的多项式$$g^{p(s)} $$和$$g^{h(s)} $$
	- 利用$${g^{\alpha s^i}}_{i \in[d]} $$计算加密后的位移多项式$$g^{\alpha p(s)} $$
	- 取样随机值$$\delta $$
	- 设定随机证明 $$\pi=(g^{\delta p(s)},g^{\delta h(s)},g^{\delta \alpha p(s)}) $$

- 验证
	- 解析证明$$\pi $$为$$(g^{p},g^{h},g^{p^{'}}) $$
	- 检验多项式约束 $$e(g^{p^{'}},g)=e(g^p,g^{\alpha}) $$
	- 检验多项式因子 $$e(g^p,g)=e(g^{t(s)},g^h) $$

**Remark 3.3** 如果可以将配对的结果重用于另一个配对乘法，那么这样的协议将是完全不安全的，因为证明者可以设置
$$
g^{P^{'}}=e(g^p,g^{\alpha})
$$
然后将通过“多项式约束”的检验：

$$
e(e(g^p,g^{\alpha}),g)=e(g^p,g^{\alpha})
$$

# 结论

我们得到了多项式问题的零知识简洁非交互式协议，这是一个特殊的用例。虽然有人会说，证明者可以通过将$t(x)$乘以另一个多项式来轻松构建多项式p(x)使其通过检验，但这种构建方式仍然有用。

验证者知道证明者有一个有效的多项式，但不知道具体是哪个多项式。我们可以添加多项式其他特性的额外证明，例如：可以被多个多项式相除，多项式的平方。未来可能存在接受、存储和奖励所有已证明多项式的服务，或者是对特定形式的未知多项式进行加密求值的需求。不管如何，通用方案将可能诞生无数的应用程序。

# 参考资料

- [JSI96] — Markus Jakobsson, Kazue Sako, and Russell Impagliazzo. “Designated verifier proofs and their applications”. In: International Conference on the Theory and Applications of Cryptographic Techniques. Springer. 1996, pp. 143–154.

- [DBS04] — Ratna Dutta, Rana Barua, and Palash Sarkar. Pairing-Based Cryptographic Protocols: A Survey. Cryptology ePrint Archive, Report 2004/064. https://eprint.iacr.org/2004/064. 2004.

- [DK18] — Apoorvaa Deshpande and Yael Kalai. Proofs of Ignorance and Applications to 2-Message Witness Hiding. Cryptology ePrint Archive, Report 2018/896. https://eprint.iacr.org/2018/896. 2018.

- [Wil16] — Zooko Wilcox. The Design of the Ceremony. 2016. url: https://z.cash/blog/the-design-of-the-ceremony/ (visited on 2018–05–01).

