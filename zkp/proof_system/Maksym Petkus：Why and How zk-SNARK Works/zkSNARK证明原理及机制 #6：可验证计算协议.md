*原文：<Why and How zk-SNARK Works 6: Verifiable Computation Protocol>*

*翻译：Junwei*



我们对[多项式证明协议](zkSNARK证明原理及机制 #3：非交互性和分布式可信设置.md)进行了许多重要的修改，使其可以适用于通用计算，所以现在让我们看看它是如何定义的。假定函数$f(^*)$ 为所要证明的计算结果，对应运算步骤$d$，变量数$n$和相应的系数

$$\{c_{L,i,j},c_{R,i,j},c_{O,i,j}\}_{i\in\{1,...,n\},j\in\{1,...,d\}}$$

- **设置**

	- 为左运算数构建变量多项式$$\{l_i(x)\}_{i\in\{1,...,n\}}$$，对于所有运算步骤$$j\in\{1,...,d\}$$，变量多项式的求值结果为对应系数，即$$l_i(j)=c_{L,i,j}$$，右运算数和输出同理

	- 随机取样 $$s,\alpha$$

	- 计算$$t(x)=(x-1)(x-2)...(x-d)$$和其求值$$g^{t(s))}$$

	- 计算证明密钥

		$$(\{g^{s^k}\}_{k\in[d]},\{g^{l_i(s)},g^{r_i(s)},g^{o_i(s)},g^{\alpha l_i(s)},g^{\alpha r_i(s)},g^{\alpha o_i(s)}\}_{i\in\{1,...,n\}})$$

	- 计算验证密钥

		$$g^{t(s)},g^{\alpha}$$

- **证明**

	- 计算函数$f$ (\$)以及对应的变量值$$\{v_i\}_{i\in\{1,...,n\}}$$

	- 计算$$h(x)=\frac{L(x)\times R(x)-O(x)}{t(x)}$$，其中$$L(x)=\sum_{i=1}^nv_i·l_i(x)$$，$$R(x),O(x)$$同理

	- 变量赋值并加总得到运算数多项式

		$$g^{L(s)}={(g^{l_1(s)})}^{v_1}...{(g^{l_n(s)})}^{v_n}$$, $$g^{R(s)}=\displaystyle\prod_{i=1}^n{(g^{r_i(s)})}^{v_i}$$, $$g^{O(s)}=\displaystyle\prod_{i=1}^n{(g^{o_i(s)})}^{v_i}$$

	- 为位移后的多项式变量赋值

		$$g^{\alpha L(s)}={(g^{\alpha l_1(s)})}^{v_1}...{(g^{l_n(s)})}^{v_n}$$, $$g^{\alpha R(s)}=\displaystyle\prod_{i=1}^n{(g^{\alpha r_i(s)})}^{v_i}$$, $$g^{\alpha O(s)}=\displaystyle\prod_{i=1}^n{(g^{\alpha o_i(s)})}^{v_i}$$

	- 根据所提供的$$s$$的各阶加密值$${g^{s^k}}_{k\in[d]}$$，计算加密后的求值$$g^{h(s)}$$

	- 设置证明：$$(g^{L(s)},g^{R(s)},g^{O(s)},g^{\alpha L(s)},g^{\alpha R(s)},g^{\alpha O(s)})$$

- **验证**

	- 解析证明为$(g^L,g^R,g^O,g^{\alpha L},g^{\alpha R},g^{alpha O},g^h)$

	- 变量多项式约束检验

		$e(g^L,g^{\alpha}=e(g^{L^{'}}, g))$$, $$e(g^R,g^{\alpha}=e(g^{R^{'}}, g)$$, $$e(g^O,g^{\alpha}=e(g^{O^{'}}, g)$

	- 运算有效性检验

		$e(g^L,g^R)=e(g^t,g^h)·e(g^O,g)$

> *注意：使用符号$$\prod$$可以更简洁地表示多个元素的乘积，例如：*

$$
\displaystyle\prod_{i=1}^{n}v_i=v_1·v_2·...·v_n
$$

对于$i ∈ \{1, …, n\}$的所有变量多项式 { $lᵢ$($x$ ) $, rᵢ$ ($x$) $, oᵢ$ ($x$) }和目标多项式$t$($x$)的集合称为QAP(*Quadratic Arithmetic Programs*，在 [[Gen+12](https://medium.com/@imolfar/why-and-how-zk-snark-works-6-verifiable-computation-protocol-1aa19f95a5cc#8bfc) ]中引入）。

虽然该协议足够稳健以验证通用计算，但必须解决两个安全问题。

# 运算数和输出的不可互换性

因为我们对所有运算数的变量多项式约束检验都使用相同的$α$，所以无法阻止证明者：

- 混淆使用来自其他运算数的变量多项式，例如$L^′(s) = o_1(s) + r_1(s) + r_1(s) + …$
- 完全交换*运算数多项式*，例如交换$O$($s$)与$L$($s$)将产生运算$O(s) × R(s) = L( s)$
- 重复使用相同的运算数多项式，例如$L$($s$) × $L$($s$) = $O$($s$)

这种可互换性意味着证明者可以变更执行程序来有效地证明其他一些计算。显然避免这种行为的方法是对不同的运算数使用不同的$α$，具体来说我们将协议修改如下：

- $$设置$$

	...

	- 随机取样 $$\alpha_l,\alpha_r,\alpha_o$$，而不是$$\alpha$$

	- 计算对应“位移”项$$\{g^{\alpha_l l_i(s)},g^{\alpha_r r_i(s)},g^{\alpha_o o_i(s)}\}_{i\in\{1,...,n\}}$$

	- 证明密钥

		$$(\{g^{s^k}\}_{k\in[d]},\{g^{l_i(s)},g^{r_i(s)},g^{o_i(s)},g^{\alpha_l l_i(s)},g^{\alpha_r r_i(s)},g^{\alpha_o o_i(s)})$$

	- 计算验证密钥

		$$g^{t(s)},g^{\alpha_l},g^{\alpha_r},g^{\alpha_o}$$

- $$证明$$

	...

	- 为“位移后“的多项式的变量赋值

		$$g^{\alpha_l L(s)}=\displaystyle\prod_{i=1}^n{(g^{\alpha _l l_i(s)})}^{v_i}$$, $$g^{\alpha_r R(s)}=\displaystyle\prod_{i=1}^n{(g^{\alpha_r r_i(s)})}^{v_i}$$, $$g^{\alpha_o O(s)}=\displaystyle\prod_{i=1}^n{(g^{\alpha_o o_i(s)})}^{v_i}$$

	- 设置证明：$$(g^{L(s)},g^{R(s)},g^{O(s)},g^{\alpha_l L(s)},g^{\alpha_r R(s)},g^{\alpha_o O(s)})$$

- $$验证$$

	...

	- 变量多项式约束检验

		$e(g^L,g^{\alpha_l}=e(g^{L^{'}}, g))$$, $$e(g^R,g^{\alpha_r}=e(g^{R^{'}}, g)$$, $$e(g^O,g^{\alpha_o}=e(g^{O^{'}}, g)$

现在再使用来自其他运算数的可变多项式是不可能的，因为证明者不知道如下的$α-$ s：

$$
\alpha_l, \alpha_r,\alpha_O
$$

# 跨运算数的变量一致性

对于任何变量$v_i，$我们必须将其值分配给每个相应运算数的变量多项式，即：

$$
(g^{l_i(s)})^{v_i},(g^{r_i(s)})^{v_i},(g^{o_i(s)})^{v_i}
$$
因为每个运算数多项式的有效性是单独检验的，所以没有强制要求在相应的变量多项式中使用相同值的约束。这意味着左运算数中变量$v_1$可能与右运算数或输出中的变量$v_1$值不同。

我们可以通过熟悉的多项式约束的方法（就像我们在变量多项式中所做的那样）强制跨运算数的变量值相等。如果我们可以创建一个跨所有运算数的“校验和位移后的”变量多项式，这将限制证明者只能给变量赋相同的值。验证者可以将每个变量的多个多项式组合成一个，例如，

$$
g^{l_i(s)+r_i(s)+o_i(s)}
$$
并将其位移随机值$β$，即

$$
g^{\beta(l_i(s)+r_i(s)+o_i(s))}
$$
随后将该位移后的多项式提供给证明者，证明者对其和变量多项式分别赋值：

$$
{(g^{l_i(s)})}^{v_{L,i}},{(g^{r_i(s)})}^{v_{R,i}},{(g^{o_i(s)})}^{v_{O,i}},{(g^{\beta(l_i(s)+r_i(s)+o_i(s))})}^{v_{\beta,i}}
$$
$β$被加密并添加到验证密钥$g^{\beta}$中。现在，如果所有$v_i$的值都相同，即

$$
v_{L,i}=v_{R,i}=v_{O,i}=v_{L,i}=v_{\beta,i}
$$
则如下的等式应当成立：

$$
e(g^{v_{L,i}·l_i(s)}·g^{v_{R,i}·r_i(s)}·g^{v_{O,i}·o_i(s)}, g^{\beta})=e(g^{v_{\beta,i}·\beta(l_i(s)+r_i(s)+o_i(s))},g)
$$
虽然这是一种有效的一致性检验，但由仍然有概率出现$l$($s$)$、 r$($s$ )$、o$ ($s$) 中有两个及以上的多项式求值相同或一个多项式可被另一个多项式整除等。这将使证明者可以伪造变量值

$$
v_{L,i},v_{R,i},v_{O,i},v_{\beta,i}
$$
这样至少可能有两个变量值不相等但等式仍然成立，使检验失效：

$$
(v_{L,i}+l_i(s)+v_{R,i}·r_i(s)+v_{O,i}·o_i(s))·\beta=v_{\beta,i}·\beta·(l_i(s)+r_i(s)+o_i(s))
$$
例如以一个单步运算为例，其中$l$($x$) = $r$($x$)。我们将这两个多项式的求值表示为$w$=$l$($s$)=$r (s)$和$y=o(s)$。则等式将转化成如下形式：

$$
\beta(v_{L}w+v_Rw+v_Oy)=v_O·\beta(2w+y)
$$
这样的形式下，对于任意的$v_R$和$v_O$，只要设置$v_{\beta}=v_O,v_L=2v_O-v_R$，等式将转化成如下形式，通过检验

$$
\beta(2v_Ow-v_Rw+v_Rw+v_Oy)=v_O·\beta(2w+y)
$$
因此之前的一致性检验将失效，一种解决方案是对于每个运算数使用不同的$β$，确保运算数的变量多项式的值不可预测。对协议进行如下的修改

- 设置

	- ...

	- 随机取样 $$\beta_l,\beta_r,\beta_o$$

	- 计算，加密并将变量一致性多项式添加至证明密钥：

		$${g^{\beta_ll_i(s)+\beta_rr_i(s)+\beta_oo_i(s)}}$$

	- 加密$$\beta-s$$并添加至验证密钥：$(g^{\beta_l},g^{\beta_r},g^{\beta_o})$

- 证明

	- ...为变量一致性多项式的变量赋值$对于i\in\{1,...,n\}，g^{z_i(s)}={(g^{\beta_ll_i(s)+\beta_rr_i(s)+\beta_oo_i(s)})}^{v_i}$

	- 在加密空间将赋值后的多项式相加

	  $$g^{Z(s)}=\displaystyle\prod_{i=1}^ng^{z_i(s)}=g^{\beta_lL(s)+\beta_rR(s)+\beta_oO(s)}$$

	- 将$$g^{Z(s)}$$添加至证明

- 验证

	- ...在所提供的运算数多项式和“校验和”多项式间检查一致性

		$e(g^L,g^{\beta_l})·e(g^R,g^{\beta_r})·e(g^O,g^{\beta_o})=e(g^Z,g)$

		等价于

		${e(g,g)}^{\beta_lL+\beta_rR+\beta_oO}={e(g,g)}^Z$

伪造相同的变量值将无法在这种结构中实现，因为不同的$β$ -s 使得多项式没法被篡改。然而，此时存在类似于<u>Remark 4.1</u> 中的缺陷，具体是因为如下项

$$
g^{\beta_l},g^{\beta_r},g^{\beta_o}
$$
是公开可用的，恶意方可以修改任何变量多项式零次方的系数，因为它不依赖于$s$，即，

$$
g^{\beta_ls^0}=g^{\beta_l}
$$

# 变量和变量一致性多项式的不可延展性

## 可变多项式的延展性

以如下两步运算为例说明[Remark  4.1](zkSNARK证明原理及机制 #5：变量多项式.md):

$$
{\color{green}a}\times {\color{blue}1} ={\color{red}b}\\
{\color{green}3a}\times {\color{blue}1} ={\color{red}c}
$$
预期结果是$b$ = $a$和$c$ = 3 $a$，$c$与$b$之间具有明确的关系$c$ = 3 $b$。这意味着左运算数的变量多项式求值为$l_a(1) = 1$ 和$l_a(2) = 3$。无论$l_a(x)$的形式如何，证明者都可以通过提供修改后的多项式$l_a^{'}$ 不成比例地分配$a$的值 $l_a^{'}(x) = al_a (x)+1$。因此多项式求值将是$l_a^{'}(1) = a+1$和$l_a^{'}(2) = 3a+1$，因此结果$b$ = $a$ + 1 和$c$ = 3 $a$ + 1，其中$c ≠3b$   ，实际上意味着$a$的值在不同的运算中是不同的。

因为证明者可以获取
$$
g^{\alpha_l}, g^{\beta_l}
$$
他可以同时满足*正确的运算数多项式*和*变量值一致性检验*：

- ...证明

	- 通过赋值不成比例的变量，来构建左运算数多项式

		$L(x)=a·l_a(x)+1$

	- 正常构建右运算数多项式和输出多项式

		$R(x)=r_1(x),O(x)=b·o_b(x)+c·o_c(x)$

	- 计算$h(X)=\frac{L(x)·R(x)-O(x)}{t(x)}$

	- 计算加密多项式: $g^{L(S)}=(g^{l_a(s)})^a·g^1$，正常计算$g^{R(s)},g^{O(s)}$

	- 计算位移后的加密多项式: $\alpha g^{L(S)}=(g^{l_a(s)})^a·g^{\alpha}$，正常计算$g^{\alpha R(s)},g^{\alpha O(s)}$

	- 计算变量一致性检验多项式

		$g^{Z(s)}=\displaystyle\prod_{i\in\{1,a,b,c\}}(g^{\beta_ll_i(s)+\beta_rr_i(s)+\beta_oo_i(s)})^i·g^{\beta_l}=g^{\beta_l(L(s)+1)+\beta_rR(s)+\beta_oO(s)}$

		其中下标$_i$代表对应变量的标识，上标$^i$代表对应变量的值；而没有定义的变量多项式等于0

	- 设置证明：$(g^{L(s)},g^{R(s)},g^{O(s)},g^{\alpha_lL(s)},g^{\alpha_rR(s)},g^{\alpha_oO(s)},g^{Z(s)}g^{h(s)})$

- 验证

	- 变量多项式约束检验

		$e(g^{L^{'}},g)=e(g^L,g^{\alpha})\Rightarrow e(g^{\alpha a·l_a(s)+\alpha},g)=e(g^{al_a(s)+1},g^{\alpha})$

		正常检验$g^{R^{'}},g^{O^{'}}$

	- 变量一致性检验

		$e(g^L,g^{\beta_l})·e(g^R,g^{\beta_r})·e(g^O,g^{\beta_o})=e(g^Z,g)\Rightarrow$

		$e(g,g)^{(a·l_a+1)\beta_l+R\beta_r+O\beta_o}=e(g,g)^{\beta_l(L+1)+\beta_rR+\beta_oO}$

	- 有效运算检验$e(g^L,g^R)=e(g^t,g^h)·e(g^O,g)$

## 变量一致性多项式的延展性

此外，由于已知

$$
g^{\beta_l},g^{\beta_r},g^{\beta_o}
$$
可以在不同的运算数中使用相同变量的不同值。例如，如果我们有一步运算：

$$
{\color{green}a}\times {\color{blue}a} ={\color{red}b}\\
$$
可以用变量多项式表示：

$$
{\color{green}l_a(x)=x},{\color{blue}r_a(x)=x},{\color{red}o_a(x)=0}\\
{\color{green}l_b(x)=0},{\color{blue}r_b(x)=0},{\color{red}o_b(x)=x}
$$
虽然预期输出为$b = a ²$，但我们可以设置$a$的不同值，例如$a$ = 2（左运算数）、$a$ = 5（右运算数），如下所示：

- 证明

	- ...取$a=2$构建左运算数多项式数：$L(x)=2l_a(x)+10l_b(x)$

	- 取$a=5$构建右运算数多项式数：$R(x)=2r_a(x)+3+10r_b(x)$

	- 取$b=10$构建输出多项式：$O(x)=2o_a(x)+10o_b(x)$

	- ...计算加密多项式

		$g^{L(s)}=(g^{l_a(s)})^2·(g^{l_b(s)})^{10}=g^{2l_a(s)+10l_b(s)}$

		$g^{R(s)}=(g^{r_a(s)})^2·(g)^3·(g^{r_b(s)})^{10}=g^{2r_a(s)+3+10r_b(s)}$

		$g^{O(s)}=(g^{o_a(s)})^2·(g^{o_b(s)})^{10}=g^{2o_a(s)+10o_b(s)}$

	- 计算变量一致性多项式

		$g^{Z(s)}=(g^{\beta_ll_a(s)+\beta_rr_a(s)+\beta_oo_a(s)})^2·(g^{\beta_r})^3·(g^{\beta_ll_b(s)+\beta_rr_b(s)+\beta_oo_b(s)})^{10}=$

		$g^{\beta_l(2l_a(s)+10l_b(s))+\beta_r(2r_a(s)+3+10r_b(s))+\beta_o(2o_a(s)+10o_b(s))}$

- 验证

	- ...变量值一致性检验成立

		$e(g^L,g^{\beta_l})·e(g^R,g^{\beta_r})·e(g^O,g^{\beta_o})=e(g^Z,g)$

*注意：多项式$o_a(x),l_b(x),r_b(x)$实际上可以被省略，因为他们对任意的$x$求值均为0，但我们出于完整性在这里保留了它们*

这种情况破坏了证明的可靠性。很明显，加密的$\beta$不应该提供给证明者。

## 不可延展性

解决延展性问题的一种方法是通过在设置阶段将加密空间中的随机值$γ$ (gamma ) 乘以验证密钥中的加密$β-s$ ，使其与加密的$Z(s)$ 不兼容：
$$
g^{\beta_l\gamma},g^{\beta_r\gamma},g^{\beta_o\gamma}
$$
此类连续隐藏值进行加密后，将不存在修改加密的$Z(s)$的可行性，因为$Z(s)$不是$γ$的倍数，例如，

$$
g^{Z(s)}·g^{v^{'}·\beta_l\gamma}=g^{\beta_l(L(s)+v^{'}\gamma)+\beta_rR(s)+\beta_oO(s)}
$$
因为证明者不知道γ，所以修改多项式将是随机的。因此我们需要平衡协议中的变量值一致性检查方程，将$Z(s)$与$γ$相乘：：

- 设置

	- ...取样随机数$\beta_l,\beta_r,\beta_o,\gamma$
	- ...设置验证密钥：$(...,g^{\beta_l\gamma},g^{\beta_r\gamma},g^{\beta_o\gamma},g^{\gamma})$

- 证明...

- 验证

	- ...变量值一致性检验成立

		$e(g^L,g^{\beta_l\gamma})·e(g^R,g^{\beta_r\gamma})·e(g^O,g^{\beta_o\gamma})=e(g^Z,g^{\gamma})$

值得注意的是，我们排除了变量多项式为$0$次的情况（例如$l_1(x) = 1x⁰$），否则在证明密钥的变量一致性多项式中可能暴露$β$的加密值

$$
\{g^{\beta_ll_i(s)+\beta_rr_i(s)+\beta_oo_i(s)}\}_{i\in\{1,...,n\}}
$$
如果其中任何两个运算数或输出为零，例如，对于$l_1(x) = 1, r_1(s) = 0, o_1(s) = 0 $，则

$$
g^{\beta_ll_1(s)+\beta_rr_1(s)+\beta_oo_1(s)}=g^{\beta_l}
$$
类似地，我们也可以隐藏$α -s$来解决变量多项式的延展性问题。然而，这不是必需的，因为对变量多项式的任何篡改都会反映在无法篡改的变量 一致性多项式中。

# 优化变量值一致性检查

变量值一致性检验现在是有效的，但它增加了4个代价高昂的配对运算和4个新项到验证密钥中。匹诺曹（Pinocchio）协议[Par+13 ]巧妙得利用“位移”，为每个运算数选择了生成元g：

- 设置

	- ...取样随机数$\beta,\gamma, \rho_l,\rho_r$，设置$\rho_o=\rho_l·\rho_r$

	- 设置生成元$g_l=g^{\rho_l},g_r=g^{\rho_r},g_o=g^{\rho_o}$

	- 设置证明密钥：

		$(\{g^{s^k}\}_{k\in[d]},\{g_l^{l_i(s)},g_r^{r_i(s)},g_o^{o_i(s)},g_l^{\alpha_l l_i(s)},g_r^{\alpha_r r_i(s)},g_o^{\alpha_o o_i(s)},g_l^{\beta l_i(s)},g_r^{\beta r_i(s)},g_o^{\beta o_i(s)}\}_{i\in[n]})$

	- 设置验证密钥：$(g_o^{t(s)},g^{\alpha_l},g^{\alpha_r},g^{\alpha_o},g^{\beta\gamma},g^{\gamma})$

- 证明

	- ...赋值变量

		$g^{Z(s)}=\displaystyle\prod_{i=1}^n(g_l^{\beta l_i(s)}·g_r^{\beta r_i(s)}·g_o^{\beta o_i(s)})^{v_i}$

- 验证

	- ...变量多项式约束检验

		$e(g_l^{L^{'}},g)=e(g_l^L,g^{\alpha_l})$，同理$g^R_r,g_o^O$

	- 变量值一致性检验

		$e(g_l^L·g_r^R·g_o^O,g^{\beta\gamma})=e(g^Z,g^{\gamma})$

	- 有效运算检验

		$e(g_l^L·g_r^R)=e(g^t_o,g^h)e(g_o^O,g)\Rightarrow$

		$e(g,g)^{\rho_l\rho_rLR}=e(g,g)^{\rho_lrho_rth+\rho_l\rho_rO}$

生成元的这种随机性进一步增加了安全性，使变量多项式的延展性（如Remark 4.1中所述）失效，因为想要增加值，它必须是如下任何一个的倍数

$$
\rho_l,\rho_r,\rho_o
$$
但其原始值或加密值均不可用（如前所述，我们没有使用可能暴露加密值的0次变量多项式）。

优化使得验证密钥两个元素更小，并从验证步骤中删除了两个配对运算。

> *注意：在2016年Jens Groth的论文[Gro16 ]中，进一步改进了协议。*

# 参考文献

[Par+13] — Bryan Parno, Craig Gentry, Jon Howell, and Mariana Raykova. *Pinocchio: Nearly* *Practical Verifiable Computation*. Cryptology ePrint Archive, Report 2013/279. https://eprint.iacr.org/2013/279. 2013.

[Gen+12] — Rosario Gennaro, Craig Gentry, Bryan Parno, and Mariana Raykova. *Quadratic* *Span Programs and Succinct NIZKs without PCPs*. Cryptology ePrint Archive, Report 2012/215. https://eprint.iacr.org/2012/215. 2012.

[Gro16] — Jens Groth. *On the Size of Pairing-based Non-interactive Arguments*. Cryptology ePrint Archive, Report 2016/260. https://eprint.iacr.org/2016/260. 2016.
