

# 导言



> 我认为思想是运动的，而论证是驱动思想到某个方向的动力。
> 
> 
>  ——约翰·克雷格（John Craig, 1699）


我们在上一篇博客[《概率论沉思录：初等抽样论》](https://github.com)中介绍了传统的抽样理论。其中，我们导出了几种经典的抽样分布，也即给定关于所观察现象的假设HH，数据DD的概率分布p(D∣H)p(D∣H)。在上一篇博客中提到的伯努利坛子模型中，假设HH即坛子的内容，数据DD即重复抽球所生成的红球和白球序列。但正如我们我们在上一篇博客的末尾所述，几乎所有实际的科学推断问题都处在相反的使用场景：我们已知数据DD，希望确定假设HH。更一般地说，已知数据DD，如何求概率分布p(H1∣D),p(H2∣D),⋯p(H1∣D),p(H2∣D),⋯，以指出给定假设{H1,H2,⋯}{H1,H2,⋯}中哪一个成立？


例如，我们的假设可能是对生成数据的物理机制的各种推断。但是从根本上讲，物理因果关系不是问题的必要组成部分，重要的只是假设和数据之间有某种逻辑关系。我们将这类问题称为**假设检验（hypothesis testing）**。



> **注** 本书\[1]\[2]采用贝叶斯派的视角，参数估计的过程实际上就是在进行假设检验了。因此，接下来讲的假设检验将与频率派的假设检验不太一样。事实上，贝叶斯派的假设检验不需要概率之外的特定工具（ad hoc devices），而频率派需要。


# 1 科学推断的基本原理


首先，我们引入先验概率的概念。除了与当前问题有关的新信息或数据DD之外，我们用XX来表示机器人几乎总是会拥有的其它信息。这至少包括它从离开工厂到收到当前问题为止的所有过去经验。对于机器人来说，所有概率至少要以XX为条件。我们称仅以XX为条件的概率P(A∣X)P(A∣X)为**先验概率（prior probability）**。需要注意的是，“先验”一词并不一定意味着时间上更早，这种区别纯粹是逻辑上的。根据定义，除了当前问题的直接数据DD之外的任何其它信息都是“先验信息”。



> **注** 还需要指出的是，伊曼努尔·康德（Immanuel Kant）引入a\-priori\[3]一词来表示可以独立于经验而知道真假的命题，而我们这里使用的“先验信息”不表示这种意思。XX只简单地表示机器人拥有的我们所称“数据”之外的其它信息。


引入先验概率后，再加上我们在博客[《概率论沉思录：定量规则》](https://github.com)中提到的乘法规则，我们就可以着手解决假设检验问题了。现做如下命题定义：


* XX：先验信息。
* HH：待检验的假设。
* DD：数据。


根据乘法规则，我们有：


P(DH∣X)\=P(D∣HX)P(H∣X)\=P(H∣DX)P(D∣X)P(DH∣X)\=P(D∣HX)P(H∣X)\=P(H∣DX)P(D∣X)在上一篇博客[《概率论沉思录：初等抽样论》](https://github.com)中，我们并不需要特别注意先验信息XX，因为所有概率都以HH为条件，所以我们可以隐含地假设，定义问题的一般先验信息已经包含在HH中。但是现在，所求的这些概率不再至少以HH为条件，而是至少以XX为条件，因此需要为它们使用不同的符号。


考虑上式的最后一个等式，进行移项后可以将P(H∣DX)P(H∣DX)表示为P(H∣X)P(H∣X)乘上一个对HH先验概率的调整因子：


P(H∣DX)⏟H的后验概率\=P(H∣X)⏟H的先验概率P(D∣HX)P(D∣X)调整因子P(H∣DX)H的后验概率\=P(H∣X)H的先验概率P(D∣HX)P(D∣X)调整因子(1\)关于上述等式的各项，我们做以下的名词约定：


* P(H∣DX)P(H∣DX)：称为**后验概率（posterior probability）**。同样需要注意的是，这仅意味着“在逻辑上处在特定推理链的后面”，而不一定“时间上更晚”。一个人的先验概率可能是另一个人的后验概率。实际上只有一种概率，我们使用不同的名称仅指组织计算的特定方式。
* P(D∣HX)P(D∣HX)：称为**似然（likelihood）**，记作L(H)L(H)。可以看出P(D∣HX)P(D∣HX)是我们在上一篇博客[《概率论沉思录：初等抽样论》](https://github.com)中介绍的抽样分布，它在固定HH时依赖于DD。但是在这篇博客中，我们将根据不同的假设{H,H′,⋯}{H,H′,⋯}考察固定的数据集DD，当固定DD考察P(D∣HX)P(D∣HX)对HH的依赖时，我们称其为“似然”。似然L(H)L(H)本身并不是HH的概率。它是一个无量纲的数值函数。当与HH的先验概率和归一化因子相乘时，它可以成为概率。
* P(D∣X)P(D∣X)：称为**归一化因子**。注意，很多文献和教材将这里的归一化因子称为“证据”，但“证据”在本书中已经被用于定义其它的东西，故在此说明一下。


对于许多科学推断问题，式(1)(1)指出了需要计算哪些概率才能判断我们的全部证据证明了哪些结论是合情的。如果P(H∣DX)P(H∣DX)非常接近1（或0），那么我们可以得出结论：HH非常可能为真（或假），并采取相应的行动。但是，如果P(H∣DX)P(H∣DX)距1/21/2不远，则机器人会警告我们可用的证据不足以证明任何可靠的结论，我们需要获得更多更好的证据。


# 2 二元假设检验


最简单的假设检验问题只有两个假设要检验，并且只有两种可能的结果。首先，我们使式(1)(1)变成这种二元情形。它给出了HH为真的概率；对于HH为假的概率，我们同样可以写出


P(¯H∣DX)\=P(¯H∣X)P(D∣¯HX)P(D∣X)P(¯¯¯¯¯H∣DX)\=P(¯¯¯¯¯H∣X)P(D∣¯¯¯¯¯HX)P(D∣X)取两个等式的比值，得到


P(H∣DX)P(¯H∣DX)\=P(H∣X)P(¯H∣X)P(D∣HX)P(D∣¯HX)P(H∣DX)P(¯¯¯¯¯H∣DX)\=P(H∣X)P(¯¯¯¯¯H∣X)P(D∣HX)P(D∣¯¯¯¯¯HX)这里我们拥有的量，即HH为真的概率与它为假的概率之比，我们称其为命题HH的 **“几率”（odds）**。



> **注** odds在赌博的场景中一般翻译成“赔率”，在本书中它只是用作p/(1−p)p/(1−p)的代名词，是概率的单调函数。本书中都翻译成几率。


定义O(H∣DX)≡P(H∣DX)P(¯H∣DX)O(H∣DX)≡P(H∣DX)P(¯¯¯¯¯H∣DX)，我们可以将上式写为：


O(H∣DX)\=O(H∣X)P(D∣HX)P(D∣¯HX)O(H∣DX)\=O(H∣X)P(D∣HX)P(D∣¯¯¯¯¯HX)可见HH的后验几率等于HH的先验几率乘以一个叫做似然比的无量纲因子。


在许多应用中，取几率的对数会更方便，因为我们可以累加各项。我们定义一个新函数，称为给定DD和XX时HH的**证据（evidence）**：


e(H∣DX)≡10log10O(H∣DX)e(H∣DX)≡10log10O(H∣DX)它仍然是概率的单调函数。通过使用底数1010并将因子1010放在前面，我们现在以**分贝（decibels，以下简写为dBdB）** 为单位来衡量证据。在给定DD的情况下，HH的证据等于HH的先验证据加上通过计算下式最后一项中的对数似然所得到的dBdB数量：


e(H∣DX)\=e(H∣X)\+10log10\[P(D∣HX)P(D∣¯HX)]e(H∣DX)\=e(H∣X)\+10log10\[P(D∣HX)P(D∣¯¯¯¯¯HX)]现在假设这个新信息DD实际上包含几个不同的命题：D\=D1D2D3⋯D\=D1D2D3⋯。那么，应用乘法规则有：P(D∣HX)P(D∣¯HX)\=P(D1∣HX)P(D1∣¯HX)⋅P(D2∣D1HX)P(D2∣D1¯HX)⋅⋯P(D∣HX)P(D∣¯¯¯¯¯HX)\=P(D1∣HX)P(D1∣¯¯¯¯¯HX)⋅P(D2∣D1HX)P(D2∣D1¯¯¯¯¯HX)⋅⋯。但在许多情况下，获得D2D2的概率不受关于D1D1的知识的影响，即P(D2∣D1HX)\=P(D2∣HX)P(D2∣D1HX)\=P(D2∣HX)，也即机器人分配给D1D1和D2D2的概率是**独立（independent）** 的。再次重申：我们关注的是逻辑独立性，而不是物理的因果独立性。通常，随着机器人的知识状态（以HH和XX表示）发生变化，以它们为条件的概率可能会从相互独立的变为相互依赖的，反之亦然。但是事件的真实属性保持不变。


如果在给定HXHX的条件下，数据D1,D2,D3,⋯D1,D2,D3,⋯的概率是逻辑独立的，则似然比可以展开为


e(H∣DX)\=e(H∣X)\+∑i10log10\[P(Di∣HX)P(Di∣¯HX)]e(H∣DX)\=e(H∣X)\+∑i10log10\[P(Di∣HX)P(Di∣¯¯¯¯¯HX)](2\)其中的和式取遍我们获得的所有额外信息。


为了对这里的数值有直观的认识，我们可以将证据（ee）、几率（OO）和概率（pp）构建成如下的表：





| 证据 (ee) | 几率 (OO) | 概率 (p)(p) |
| --- | --- | --- |
| 00 | 1:11:1 | 1/21/2 |
| 33 | 2:12:1 | 2/32/3 |
| 66 | 4:14:1 | 4/54/5 |
| 1010 | 10:110:1 | 10/1110/11 |
| 2020 | 100:1100:1 | 100/101100/101 |
| 3030 | 1000:11000:1 | 0\.9990\.999 |
| 4040 | 10000:110000:1 | 0\.99990\.9999 |
| −e−e | 1/O1/O | 1−p1−p |



进一步绘制成如下所示的图：



[![](https://images.cnblogs.com/cnblogs_com/blogs/538207/galleries/2106514/o_dfe1a252.png)](https://images.cnblogs.com/cnblogs_com/blogs/538207/galleries/2106514/o_dfe1a252.png)



从上面的图和表中我们可以明显地看出为什么以分贝（dBdB）为单位给出证据非常有力。当概率接近11或00时，我们的直觉很差。对我们来说，0\.9990\.999和0\.99990\.9999的概率差别没多大意义，但是30dB30dB和40dB40dB的证据之间的差别确实对我们有明确意义。


现在让我们将式(2)(2)应用于一个特定的工业质量问题中（尽管也可以将其表述为其它问题）。假设先验信息XX如下：


* XX：我们有11台自动机器，这些机器将其生产出的小部件输出到11个盒子中。该过程对应于小部件生产的早期阶段，因为有10台机器会生产1/6的坏部件。第11台机器更糟，会生产1/3的坏部件。每台机器输出的部件被分别放在一个未贴标签的盒子中，并存储在仓库中。


我们选择一个盒子并抽样检测其中的一些小部件，将它们分为“好”和“坏”。我们的目标是判断是否选择了那个糟糕机器对应的盒子，然后判断是要接受还是拒绝它。


我们把这项工作交给我们的机器人，看看它是如何工作的。首先，它必须找到待检验假设的先验证据。我们定义以下两个假设：


* AA：选择了1/31/3的次品率的坏批次。
* BB：选择了1/61/6的次品率的好批次。


先验信息XX的定性部分告诉我们，只有两种可能性。因此，在XX产生的逻辑背景下，两个命题是互否的关系：给定XX，我们有¯A\=B,¯B\=A¯¯¯¯A\=B,¯¯¯¯B\=A。


唯一的定量先验信息是有11台机器，我们不知道是哪台机器制造了我们选择的批次，因此根据无差别原则有P(A∣X)\=1/11P(A∣X)\=1/11，于是


e(A∣X)\=10log10P(A∣X)P(¯A∣X)\=10log101/1110/11\=−10dBe(A∣X)\=10log10P(A∣X)P(¯¯¯¯A∣X)\=10log101/1110/11\=−10dB（同理，我们有e(B∣X)\=10dBe(B∣X)\=10dB）


在此问题中，XX与计算有关的唯一信息只是这些数值，即±10dB±10dB。因此，我们没必要说我们仅在谈论11台机器的问题。可能只有一台机器，而这里的先验信息是我们之前使用它的经验：使用该机器时，有多少概率遇到好批次/坏批次。在这里，重要的是好批次/坏批次的先验概率。


如果我们取出一个坏部件，将会增加这是坏批次的证据；如果我们取出一个好部件，将会减少这是坏批次的证据。我们设NN为批次中的部件总数，我们依次抽取nn个部件进行检测，且假设N≫nN≫n，也即我们连续进行nn次有放回抽样，此时正如我们在上一篇博客[《概率论沉思录：初等抽样论》](https://github.com)中提到的，超几何分布的极限形式，即二项分布将适用。设我们检测的nn个部件中，有bb个坏部件和gg个好部件，则我们可以得到这是坏批次的后验证据为


e(A∣DX)\=e(A∣X)\+b∑i\=110log10\[P(坏∣AX)P(坏∣¯AX)]\+g∑i\=110log10\[P(好∣AX)P(好∣¯AX)]\=e(A∣X)\+b⋅10log101/31/6\+g⋅10log102/35/6≈e(A∣X)\+3b−ge(A∣DX)\=e(A∣X)\+b∑i\=110log10\[P(坏∣AX)P(坏∣¯¯¯¯AX)]\+g∑i\=110log10\[P(好∣AX)P(好∣¯¯¯¯AX)]\=e(A∣X)\+b⋅10log101/31/6\+g⋅10log102/35/6≈e(A∣X)\+3b−g(3\)可见，一旦我们使用对数，计算是多么简单。机器人的思想以一种非常简单直接的方式“朝某个方向被驱动”。假设我们抽样的样本有80%的小部件是坏的，我们可以将其可视化为如下所示的图：



[![](https://images.cnblogs.com/cnblogs_com/blogs/538207/galleries/2106514/o_41c7a9bb.png)](https://images.cnblogs.com/cnblogs_com/blogs/538207/galleries/2106514/o_41c7a9bb.png)



现在，我们拥有的只是选择了坏批次的假设的概率、几率或证据。最终，我们必须做一个决定：是接受它，还是拒绝它。这时我们该怎么办呢？当然，我们可以事先决定：如果假设AA的概率达到一定的值，那么就判定AA为真，如果它下降到某个值，那么就判定AA为假。


概率论本身不会告诉我们做出决策的临界值在哪里。这必须基于价值判断：做出错误决定的后果是什么？进行进一步检测的代价是什么？这会将我们带入决策论领域，我们后面会进行讨论。目前比较明显的是犯第一类错误（接受坏批次）可能比犯另一类错误（拒绝好批次）的后果更为严重。这将对我们如何设置临界值产生明显的影响。


因此，我们可以给机器人一些指示，例如“如果AA的证据大于0dB0dB，则拒绝该批次（它很可能是坏的而不是好的）。如果AA的证据低至−13dB−13dB，则接受该批次（它至少有95%95%的概率是好的）。否则，请继续检测。”


上述方法是我们的机器人根据命题AA的后验概率达到一定水平后选择拒绝它或接受它的方法，这个非常有用且强大的流程在统计文献中称为 **“序列推断（sequential inference）”**，该术语表明检测次数不是预先确定的，而是取决于我们发现的数据值的顺序。


# 3 多重假设检验


假定在刚刚讨论的序列检测过程中，我们测试了50个小部件，结果每个小部件都是坏的。根据式(3)(3)，坏批次假设证据e(A∣DX)e(A∣DX)的最终结果是140dB140dB，这是1−10−141−10−14的概率。但是，我们的常识会倾向于拒绝这一结论，我们会对这个批次中只有1/31/3是坏部件产生怀疑。


在当前的问题中，我们可以使机器人在看到“太多”坏部件时对AA持怀疑态度，方法是额外提供一个指出这种可能性的假设。我们在假设AA：我们有一个有1/31/3坏部件的盒子，假设BB：我们有一个有1/61/6坏部件的盒子的基础之上，添加第三个假设CC：制造小部件的机器完全出了问题，会生产99%99%的坏部件。


现在，我们必须调整先前的概率，以考虑这种新的可能性。但是我们不希望问题的性质发生重大改变。因此，我们让假设CC的先验概率P(C∣X)P(C∣X)非常低，为10−610−6（−60dB−60dB）。


我们定义以下三个假设：


* AA：我们选择了有1/31/3坏部件的盒子。
* BB：我们选择了有1/61/6坏部件的盒子。
* CC：我们选择了有99/10099/100坏部件的盒子。


这三个假设的初始概率依次为：P(A∣X)\=111(1−10−6),P(B∣X)\=1011(1−10−6),P(C∣X)\=10−6P(A∣X)\=111(1−10−6),P(B∣X)\=1011(1−10−6),P(C∣X)\=10−6。因子1−10−61−10−6实际上可以忽略不计，于是我们有


e(A∣X)\=−10dB,e(B∣X)\=10dB,e(C∣X)\=−60dBe(A∣X)\=−10dB,e(B∣X)\=10dB,e(C∣X)\=−60dB设与数据有关的命题DD是“我们抽样检测的nn个部件中，每个都是坏部件”，则我们可以得到命题CC的后验证据为


e(C∣DX)\=e(C∣X)\+10log10\[P(D∣CX)P(D∣¯CX)]e(C∣DX)\=e(C∣X)\+10log10\[P(D∣CX)P(D∣¯¯¯¯CX)](4\)其中P(D∣CX)\=(99100)nP(D∣CX)\=(99100)n（我们仍然假设盒子里的小部件总数NN比被抽样检测的数量nn大很多，因此这里近似为无放回抽样）。而对于P(D∣¯CX)P(D∣¯¯¯¯CX)，我们在计算的过程中将会用到两次乘法规则：


P(D∣¯CX)\=P(D∣X)P(¯C∣DX)P(¯C∣X)\=P(D∣X)\[P(A∣DX)\+P(B∣DX)]P(A∣X)\+P(B∣X)\=P(D∣X)\[P(D∣AX)P(A∣X)P(D∣X)\+P(D∣BX)P(B∣X)P(D∣X)]P(A∣X)\+P(B∣X)\=P(D∣AX)P(A∣X)\+P(D∣BX)P(B∣X)P(A∣X)\+P(B∣X)\=(13)n(111)\+(16)n(1011)(111)\+(1011)(1−10−6忽略不计)\=(111)(13)n\+(1011)(16)nP(D∣¯¯¯¯CX)\=P(D∣X)P(¯¯¯¯C∣DX)P(¯¯¯¯C∣X)\=P(D∣X)\[P(A∣DX)\+P(B∣DX)]P(A∣X)\+P(B∣X)\=P(D∣X)\[P(D∣AX)P(A∣X)P(D∣X)\+P(D∣BX)P(B∣X)P(D∣X)]P(A∣X)\+P(B∣X)\=P(D∣AX)P(A∣X)\+P(D∣BX)P(B∣X)P(A∣X)\+P(B∣X)\=(13)n(111)\+(16)n(1011)(111)\+(1011)(1−10−6忽略不计)\=(111)(13)n\+(1011)(16)n于是我们有


e(C∣DX)\=e(C∣X)\+10log10\[(99100)n(111)(13)n\+(1011)(16)n]e(C∣DX)\=e(C∣X)\+10log10\[(99100)n(111)(13)n\+(1011)(16)n](5\)如果n\>5n\>5，一个很好的近似是


e(C∣DX)≈−49\.6\+4\.73n,n\>5e(C∣DX)≈−49\.6\+4\.73n,n\>5如果n\<5n\<5，一个很好的近似是


e(C∣DX)≈−60\+7\.73n,n\<3e(C∣DX)≈−60\+7\.73n,n\<3与此同时，我们想知道假设AA和BB发生了什么。在测试了nn个小部件并且证明了它们都是坏的之后，假设AA和假设BB的证据以及近似形式如下：


e(A∣DX)\=e(A∣X)\+10log10\[(13)n(16)n\+1110×10−6(99100)n]≈{−10\+3n,n\<7,\+49\.6−4\.73n,n\>8e(A∣DX)\=e(A∣X)\+10log10\[(13)n(16)n\+1110×10−6(99100)n]≈{−10\+3n,n\<7,\+49\.6−4\.73n,n\>8(6\)e(B∣DX)\=e(B∣X)\+10log10\[(16)n(13)n\+11×10−6(99100)n]≈{10−3n,n\<10,\+59\.6−7\.73n,n\>11e(B∣DX)\=e(B∣X)\+10log10\[(16)n(13)n\+11×10−6(99100)n]≈{10−3n,n\<10,\+59\.6−7\.73n,n\>11(7\)假设AA、BB、CC的证据随抽样次数的变化如下图所示：



[![](https://images.cnblogs.com/cnblogs_com/blogs/538207/galleries/2106514/o_0879d567.png)](https://images.cnblogs.com/cnblogs_com/blogs/538207/galleries/2106514/o_0879d567.png)



可以看到，曲线AA和曲线BB的初始直线部分代表我们在引入新假设CC之前发现的解。新假设CC在初始时会被暂时搁置， 它的影响直到CC穿过BB时才出现。从这一点往后，曲线AA不再继续向上，而是转而向下。机器人确实已经学会了如何怀疑。但是，曲线B在这一点上并没有改变，它一直线性延伸到A和C具有相同合情性的位置。


对这种现象的解释是，上述的多重序列检测可以近似看作是交替进行的二元假设检验：最初B的合情性远高于C，我们实际上基本上是在针对B检验A，然后重现了式(3)的解。在积累了足够的证据后，C的合情性达到了与B相同的水平之后，基本上将是针对C而不是B检验A。


更一般地说，只要我们有一组离散的假设，则其中任何一个的合情性变化都将近似是针对单个备择假设——所有假设当中最合情的那个备择假设进行检验的结果。


# 4 连续概率分布函数


接下来，我们对上面的例子进行扩展。直截了当的是引入更多的“离散”假设。更有趣的是引入一系列连续的假设，例如


* Hf：机器人以f的比例生产坏部件（f可以是0⩽f⩽1中的任何数值）。


这样，与离散的先验分布不同，我们的机器人需要考虑f在区间(0⩽f⩽1)中具有的连续分布，并将根据观察到的样本计算f取各种值的后验概率，由此可以做出各种决策。在继续我们对假设检验问题的讨论之前，我们先来讨论连续概率分布。


我们在博客[《概率论沉思录：定量规则》](https://github.com)中导出的推断规则仅针对离散命题（A,B,⋯）的有限集合情况得出，但我们在实践中可以将涉及连续假设的问题进行转换，然后用这些规则进行处理。假设f是我们感兴趣的任意连续实参数变量，则我们可以定义以下离散、互斥且完备的命题：


F′≡(f⩽q),F′′≡(f\>q)因此，我们的规则一定适用于它们。给定一些先验信息X，则F′的概率通常取决于q，从而定义


G(q)≡p(F′∣X)它显然是单调增加的。接下来我们来看f位于指定区间（a1\<f⩽a2）的概率是多少。我们定义以下命题：


A≡(f⩽a1),B≡(f⩽a2),W≡(a1\<f⩽a2)则布尔代数关系为B\=A\+W，由于A和W互斥，则加法规则可简化为P(B∣X)\=P(A∣X)\+P(W∣X)。又因为P(B∣X)\=G(a2)，P(A∣X)\=G(a1)，所以我们有


P(a1\<f⩽a2∣X)\=P(W∣X)\=G(a2)−G(a1)在当前情况下，G(q)是连续可微的，所以我们也可以写出


P(a1\<f⩽a2∣X)\=∫a2a1g(f)df其中g(f)\=G′(f)⩾0是G的导数，通常称为**概率分布函数（probability distribution function）**，或给定X时f的**概率密度函数（probanility density function）**。我们此后使用缩写PDF来表示它，与上述两种英文名称均一致。它的积分G(f)可以称为f的**累积分布函数（cumulative distribution function）**。


# 5 检验无数假设


现在假定我们同时要检验无数个假设。我们可以使用分析的方法来使问题变得更简单。但是，之前我们采用的对数形式的公式就不太好用了，因此我们下面会回到式(1)中的原始概率形式：


P(A∣DX)\=P(A∣X)P(D∣AX)P(D∣X)现在让A代表假设“坏部件比例在(f,f\+df)的范围内”，其先验PDF为：


P(A∣X)\=g(f∣X)df这给出了坏部件比例在df区间内的概率。令D表示迄今为止我们的实验结果：


* D：抽样检测n个小部件，其中有b个坏部件和n−b个好部件。


那么f的后验PDF是


P(A∣DX)\=P(A∣X)P(D∣AX)P(D∣X)\=g(f∣DX)df因此，先验PDF与后验PDF由


g(f∣DX)\=g(f∣X)P(D∣AX)P(D∣X)关联。分母是归一化常数。如果需要，通常可以要求后验PDF满足归一化条件P(0⩽f⩽1∣DX)\=∫10g(f∣DX)df\=1⇒∫10g(f∣X)P(D∣AX)P(D∣X)df\=1，从而更简单地确定该分母：


P(D∣X)\=∫10g(f∣X)P(D∣AX)df我们有df→0时，P(D∣AX)→P(D∣HfX)（详细证明过程请参见原书）。考虑假设Hf：机器人以f的比例生产坏部件，则在每次试验中取出坏部件的概率为f，取出好部件的概率为(1−f)。现在，我们不仅有假设盒子里的小部件总数N比被抽样检测的数量n大很多，因此不同试验的概率在给定f时是逻辑独立的；而且f还是一个连续的数值。因此，类似我们在上一篇博客[《概率论沉思录：初等抽样论》](https://github.com)中推导二项分布那样，可以得到


P(D∣HfX)\=fb(1−f)n−b（注意，这里与二项分布不同的是，实验数据D是有顺序的）


因此，我们的后验PDF就可以表示为


g(f∣DX)\=fb(1−f)n−bg(f∣X)∫10fb(1−f)n−bg(f∣X)df我们在这篇博客中介绍的二元假设检验检验、多重假设检验都做为特殊情况包含在了这个公式中。例如我们之前讨论的针对A、B、C三种假设的检验，其对应的先验PDF如下所示：


g(f∣X)\=111(1−10−6)⏟假设A的先验PDFδ(f−13)\+1011(1−10−6)⏟假设B的先验PDFδ(f−16)\+10−6⏟假设C的先验PDFδ(f−99/100)这里的δ函数在除了0以外的点函数值都等于0，而在其整个定义域上的积分等于1。当f分别取值16,13,99100时，先验PDF分别为1011(1−10−6),111(1−10−6),10−6。


运用这里的后验PDF表达式来重新考虑我们之前提到的针对A、B、C三种假设的检验问题，我们考虑对单个假设C进行假设检验（fA\=16,fB\=13,fC\=99100），有


P(C∣DX)\=(99100)n10−6δ(0)(13)n111(1−10−6)δ(0)\+(16)n1011(1−10−6)δ(0)\+(99100)m10−6δ(0)\=(99100)n10−6(13)n111(1−10−6)\+(16)n1011(1−10−6)\+(99100)n10−6对比我们之前得到的e(C∣DX)：


e(C∣DX)\=e(C∣X)\+10log10\[(99100)n(111)(13)n\+(1011)(16)n]\=10log1010−61−10−6\+10log10\[(99100)n(111)(13)n\+(1011)(16)n]\=10log10\[10−6(99100)n(1−10−6)(111)(13)n\+(1−10−6)(1011)(16)n]我们发现，e(C∣DX)现在可以由e(C∣DX)\=10log10\[P(C∣DX)1−P(C∣DX)]得到。


现在，假设在检测刚开始时我们的机器人是刚出厂的，除了知道一台机器可能生产好部件也可能生成坏部件之外，它没有其它关于机器的先验知识。此时，机器人没有理由对于一个特定区间df分配比其它区间更高的概率。因此，我们让机器人分配均匀先验概率密度g(f∣X)\=常数。为了使得∫10g(f∣X)df\=1，我们取g(f∣X)\=1,0⩽f⩽1。此时，式(8)中的积分就是著名的第一类欧拉积分（现在通常称为完全Beta函数），我们有：


g(f∣DX)\=fb(1−f)n−b∫10fb(1−f)n−bdf\=fb(1−f)n−bB(b\+1,n−b\+1)\=(n\+1)!b!(n−b)!fb(1−f)n−b
> **注** 数学中有两种类型的**欧拉积分（Euler intergral）**\[4]：
> 
> 
> 1. 第一类欧拉积分（Beta函数）：


B(x,y)\=∫10tx−1(1−t)y−1dt\=Γ(x)Γ(y)Γ(x\+y)
> 2. 第二类欧拉积分（Gamma函数）：


Γ(z)\=∫∞0tz−1e−tdt上述后验分布在(0⩽f⩽1)中有一个峰，通过令g′(f∣DX)\=0可以得到这是在f\=ˆf\=bn处。其物理意义是观察到的坏部件比例或相对频率。为了寻找峰的尖锐程度，我们想对该函数进行进一步分析，由于该函数包括几个因子的累乘，我们对其进行取对数，得到：


L(f)≡lng(f∣DX)\=blnf\+(n−b)ln(1−f)\+常数然后在ˆf处对L(f)做Tayler展开：


L(f)\=L(ˆf)\+L′(ˆf)(f−ˆf)⏟0\+L′′(ˆf)2!(f−ˆf)2\+o((f−ˆf)2)\=L(ˆf)−(f−ˆf)22σ2\+o((f−ˆf)2)其中σ2≡ˆf(1−ˆf)N（这里需要注意L′′(f)\=−nf2\+2bf−bf2(1−f)2,L′′(ˆf)\=−nb2n2\+2bbn−bˆf2(1−ˆf)2\=b(bn−1)ˆf2(1−ˆf)2\=−b(1−ˆf)ˆf2(1−ˆf)2\=−bˆf2(1−ˆf)\=−bbnˆf(1−ˆf)\=−nˆf(1−ˆf)）。


对于这个近似值，我们就得到了式(9)的近似分布：


g(f∣DX)≈Kexp{−(f−ˆf)22σ2}该分布称为**高斯分布（Gaussian distribution）**（或称**正态分布（normal distribution）**）。其中K\=1√2πσ2是归一化常数，用于保证∫10g(f∣DX)\=1。实际上，只要b≫1且(n−b)≫1，这是在整个区间(0\<f\<1)中对式(9)的一个很好的逼近。



> **注** 关于二项分布的正态逼近，有棣莫弗\-拉普拉斯（de Moivre\-Laplace）中心极限定理对其进行刻画。设n重伯努利试验中，事件A在每次试验中出现的概率为p（0\<p\<1），记Sn为n次试验中事件A出现的次数，则当n→∞时，有Snn→N(p,√pqn)（依分布）。这里的Snn对应我们前面提到的bn，p对应我们前面提到的ˆf\=bn，q对应我们前面提到的1−ˆf。


因此，在n次试验中观察到b个坏部件后，f的最概然值（the most likely value）是观察到的坏部件的比例，这合理地描述了机器人关于f的知识状态。考虑f的准确性，这个估计使得ˆf±σ很可能包含真实值。参数σ称为PDF(10)的**标准差（standard deviation）**，σ2称为PDF(10)的**方差（variance）**。更准确地说，根据式(10)进行分析，机器人分配概率如下：


f的真实值包含在 ˆf±0\.68σ 中的概率为 50%；包含在 ˆf±1\.65σ 中的概率为 90%；包含在 ˆf±2\.57σ 中的概率为 99%；随着测试次数n的增加，这些区间会根据σ2\=ˆf(1−ˆf)n，正比于1√n按比例缩小。



> **注** 这里可以想到质量控制里用的较多的3 sigma法则（也被称为68\-95\-99\.7法则）\[5]，也即对于服从正态分布N(μ,σ2)随机变量X，其观测值包含在μ±σ中的概率为68\.3%；包含在μ±2σ中的概率为95\.4%；包含在μ±3σ中的概率为99\.7%。


这样，我们看到机器人从对f的“无知”状态开始，随着从测试中积累信息，它对f的估计越来越确定，这与常识吻合。但是我们在这里需要强调，**f不会随时间变化，σ不是f的真实属性而只是机器人表示其关于f的知识状态的概率分布的属性**。


# 6 简单假设与复合假设


到目前为止，我们考虑的假设（A、B、C、Hf）指的是单个参数f\=M/N，即盒子中坏部件的未知比例，而且为f指定了一个明确定义的值（在Hf中，它可以是0⩽f⩽1中的任何数值）。这种假设称为**简单假设（simple hypothesis）**，因为如果定义了一个包含所有参数的参数空间Ω，这样的假设在Ω中由单个点表示。


然而，有时我们不需要检验Ω中的所有简单假设，只关心参数是位于某个子集Ω1⊆Ω还是其补集Ω2\=Ω−Ω1中，而不关心该子集中f的特定值。我们称形如H≡f∈Ω1的假设为**复合假设（compound/composite hypothesis）**。我们是否可以直接处理复合假设，而不要求机器人检验Ω1中的每个简单假设呢？


事实上，在式(8)中，我们几乎完成了所有工作，接下来我们只需要再进行一次积分消除冗余参数即可。参数空间Ω由\[0,1]中的所有f组成。假设若f\>0\.1，我们需要采取一些措施（如关闭并重新调整机器）；若f⩽0\.1，则应该让机器继续运行。那么我们定义Ω1为\[0\.1,1]中的所有f,令复合假设H≡f∈Ω1。由于f的实际值无关紧要，f现在称为**冗余参数（nuisance parameter）**，我们想消去它。通过对冗余参数f求积分，可以将其从式(8)中消去：


P(Ω1∣DX)\=∫Ω1fb(1−f)n−bg(f∣X)∫Ωfb(1−f)n−bg(f∣X)df在f是均匀先验PDF的情况下，结果是不完全Beta函数：f在任何指定区间(a1\<f\<a2)中的后验概率为


P(a1\<f\<a2∣DX)\=(N\+1)!n!(N−n)!∫a2a1fb(1−f)n−bdf计算机能够轻松计算这种形式的式子。


# 参考


* \[1] Jaynes E T. Probability theory: The logic of science\[M]. Cambridge university press, 2003\.
* \[2] 杰恩斯. 廖海仁译. 概率论沉思录\[M]. 人民邮电出版社, 2024\.
* \[3] Kant I, Meiklejohn J M D, Abbott T K, et al. Critique of pure reason\[M]. London: JM Dent, 1934\.
* \[4] [《维基百科：欧拉积分》](https://github.com)
* \[5] [《维基百科：68–95–99\.7法则》](https://github.com):[西部世界官网](https://www.xbsj9.com)


  * [导言](#%E5%AF%BC%E8%A8%80)
* [1 科学推断的基本原理](#tid-eWwWXf)
* [2 二元假设检验](#tid-7FEZY4)
* [3 多重假设检验](#tid-rADbed)
* [4 连续概率分布函数](#tid-YSHPzi)
* [5 检验无数假设](#tid-akKSbj)
* [6 简单假设与复合假设](#tid-BK6fEh)
* [参考](#%E5%8F%82%E8%80%83)

   \_\_EOF\_\_

   ![](https://github.com/orion-orion)猎户座  - **本文链接：** [https://github.com/orion\-orion/p/18621496](https://github.com)
 - **关于博主：** 研究生小菜一枚，机器学习半吊子，并行计算混子。
 - **版权声明：** 欢迎您对我的文章进行转载，但请务必保留原始出处哦(\*^▽^\*)。
 - **声援博主：** 如果您觉得文章对您有帮助，可以点击文章右下角**【[推荐](javascript:void(0);)】**一下。
     
