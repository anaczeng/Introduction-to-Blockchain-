区块链既然是未来互联网的基础技术支撑之一，那它究竟是什么呢？“区块链”有两层含义：

* **由“区块”和“哈希指针”构成的链式数据结构**。数据结构就是组织数据的方式方法。区块链可以将它想象成一种特殊的记事本：一个区块是一页纸，都用哈希指针这种装订线串起来。
* **去中心化的时间戳系统**。这里的时间戳系统特指通过加密手段来保证电子系统中记录事件发生前后顺序的系统，它采用了“区块链”这种数据结构。去中心化粗略可理解为每个人都可以拥有一本“区块链”记事本：每个持有者都能对其做读写操作，并且从中能获取的数据都是一致的。

从这两层含义可明显看出“区块链”的核心作用是**记录**。相比其它方式，区块链记录的有效数据具有以下的优势：

* 在“**记录即发生，不记录不发生**”的前提下**真实可信**；
* **一致**且**不受操纵**；
* **可追溯**（可选）。

#### 1.2.1 区块链有效数据真实性的前提

区块链因其特殊的数据结构能保证写入的数据不被篡改，但它和普通记事本一样，自身并不能保证写入的数据是否符合已发生的客观事实。若数据在写入之初已失真，便无真实可言；而区块链不可篡改的性质使错误难以修改反倒成了劣势。举个例子：

> 子贡在卫国钱庄存入一百两黄金后，却笔误在自己的账本上写道“存卫国钱庄一千两黄金”。几日后，子贡发现了错误。若是普通账本，他直接在此处修改便了事；但是“区块链”账本，子贡得从错误的那页开始把后面的账目重新做。![](/assets/zigong-example1.png)_图1-3：子贡记账。普通账本，错误处直接修改；区块链账本，得从错误处开始连带之后的账目重新做。_

然而在“记录即发生”的情况下，区块链不仅能避免上述劣势，还能保证有效数据记录的事件发生过且如此发生的。何为“记录即发生”？**即当数据写入时，事件才得以依照写入的数据发生**。它有两种情况：

* 记录和事件同步发生，记录等于事件的发生；
* 记录和事件异步发生，但事件的发生完全按照记录执行。

这样保证了数据在写入时是真实可信的。而当数据写入区块链后，其不可篡改的性质使得数据改动的开销非常大；区块链不可篡改的性质是由其特殊的数据结构所决定的，在第二章将会详细介绍。因此，“记录即发生”能保证“区块链有效数据记录的事件发生过且如此发生的”。

> 二月初一，子贡在区块链账本上记下两笔账：存入卫国钱庄一百两黄金；二月初七子时整，卫国钱庄转移五十两黄金至鲁国钱庄。第一笔账目在记下的的同时，卫国钱庄的库房里就出现了子贡的一百两黄金。第二笔账直到二月初七子时才执行发生，子贡在卫国钱庄的一百两黄金减至五十两，鲁国钱庄的库房出现了子贡的五十两黄金。
>
> ![](/assets/zigong-example2.png)_图1-4：子贡记账。账目一记录和事件同时发生；账目二记录和事件异步发生。_

“记录即发生”仅这前提并不能完全保证区块链有效数据的真实性。当事件没有被记录在区块链上，它是否就没发生过或是失真的呢？仍以子贡记账为例：

> 一日，子贡仆人在鲁国钱庄取了子贡存下的五十两黄金，然区块链账本上并无此记录。事后，子贡和鲁国钱庄因账目起了纷争。请问区块链账本的记录能作为双方对簿公堂的依据吗？明显不能，只在“记录即发生”前提下的区块链账本并不保证记录全部的账目。
>
> ![](/assets/zigong-example3.png)
>
> _图1-5：子贡记账。仆人取金，区块链账本无记录。该区块链账本记录的真实性并不完备。_

因此，“记录即发生”和“不记录不发生”构成了区块链有效数据真实性的完整前提。把“不记录不发生”的约束加到子贡记账的例子，就是子贡若不在区块链账本上记上一笔“鲁国钱庄仆人取出五十两黄金”，那子贡的仆人就死活取不出五十两黄金。

“记录即发生，不记录不发生”在物理世界看起来很荒谬，而且漏洞很多，但在虚拟世界中实现起来并不难。这一点在比特币系统中体现得非常完美，交易记录在主链（即有效的）中才发生，交易没记录在主链中即不曾发生过，所以交易记录都是真实的。而现阶段的公证链却是一个反例，因社会数字化进程仍未达到完全电子化的阶段，很多需要公证的事件都发生在公证链记录之前，即使使用了区块链技术也不能排除人为因素的数据造假；而且没记录在公证链上的事件也不能保证没有发生。社会的数字化和“记录即发生，不记录不发生”这个前提能划上等号，因此区块链有效数据的真实性和社会数字化进程息息相关。

#### 1.2.2 区块链记录的数据是一致且不受操纵的

区块链系统的每个标准参与者都拥有一份完整的数据，且每份数据都是一致的；这是由分布式系统的共识机制来实现的，在第三章将会详细介绍。在子贡记账的例子中，就是卫国钱庄、鲁国钱庄、甚至子贡仆人都拥有一份完整且记录一致的账本。区块链记录的数据是不可操纵的。回想我们能对自己记事本做的操作只有四种：写入、旧数据更新、查询和删除。真正影响记录数据的操作只有写更删三种。写入区块链的数据是不可篡改的，且在区块链系统中受到共识机制的约束，更新旧数据几乎是不可能的。那么在写入真实数据的情况下，唯一有可能被操纵的操作就是删除。然而，这对区块链系统来说可操作性非常小，除非将所有的参与者持有的数据都删除。这种数据不受操纵的优势就是去中心化的具体表现之一。譬如在子贡记账的例子中，子贡可以销毁自己的账本，甚至可以命令仆人销毁仆人的账本；但是子贡无法命令卫国钱庄或鲁国钱庄销毁他们的账本。

![](/assets/zigong-example4.png)

_图1-6：子贡记账。每个参与者都拥有一份完整且记录一致的账本。_

#### 1.2.3 区块链记录的数据可具备可追溯的性质

可追溯性质不像前两个性质，并非所有的区块链应用都具备该性质；但它是比特币系统中的重要性质。鉴于区块链概念是从比特币系统中提取出来的，这里还是值得一提。可追溯即是记录的事件可以追本溯源；事件是有源头的。

> 子贡在卫国钱庄存入的一百两黄金是从自家金矿开采提炼加工的，这是这一百两黄金在区块链账本中的初始记录。最后在子贡仆人手上的五十两黄金，是可以在区块链账本中向前追溯它的来源：子贡仆人-&gt;鲁国钱庄-&gt;卫国钱庄-&gt;子贡金矿。
>
> ![](/assets/zigong-example5.png)_图1-7：子贡记账。区块链账本可追溯子贡仆人手中五十两黄金的来源。_

数据的可追溯意味着数据是可认证且不可抵赖的。可认证意味着数据不可被他人伪造，例如子贡的仆人不能伪装成子贡记账；不可抵赖意味着可向第三方证明数据来源，例如子贡记得帐不能抵赖说成是自己仆人伪装自己记的。数字签名可以实现数据可追溯的性质，在第二章将会详细介绍。

#### 1.2.4 区块链的技术性质

区块链拥有这些优势，得益于计算机科学中密码学技术和分布式系统。在密码学技术中，哈希函数具有保证数据不被篡改的性质，数字签名还具有可认证和不可抵赖的性质。分布式系统实现了去中心化的性质。

![](/assets/relationship-between-tech-and-advantage.png)图1-8：技术及其性质与区块链优势之间的关系。






