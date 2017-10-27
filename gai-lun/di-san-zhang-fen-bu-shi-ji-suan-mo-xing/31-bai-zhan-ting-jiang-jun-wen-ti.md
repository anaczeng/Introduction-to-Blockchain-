跟区块链技术形影不离的话题除了加密技术外，还有共识机制。常接触区块链的读者经常会听到POW（工作量证明）和POS（股权证明）。这两个名词对大多数人来说就如同黑箱，只知道它能让网络中所有的节点做出正确的一致性操作，但不知其所以然。若想了解里面的机制，还要从Leslie Lamport在1982年提出的“**拜占庭将军问题（Byzantine General Problem）**”开说。POW和POS的核心也未脱离过该问题框架；此外，它们还具备抵御**女巫攻击（sybil attack）**的能力。这里出现了很多新术语，下面的篇幅将会一一道来；我们首先从拜占庭将军问题的描述开始。

#### 3.1.1 拜占庭将军问题的一般描述

该问题的初衷是为了通过冗余解决分布式系统的容错问题：多个部件协同工作，难免出现故障部件传递错误或无效的信息；系统必须保障在这样的情况下大多数时候还能顺利运转。在原始论文中，Lamport把部件比喻成了分散在敌方城池周围的拜占庭将军们，他们通过信使相互联系以达成最后一齐"进攻"或"撤退"的共识。假使叛徒存在，他们将会发送错误或无效的信息使得诚实的将军：

（1）无法达成共识；（失去一致性）

（2）达成错误的共识；（失去正确性）

是否存在算法避免上述两种情况的发生？这是拜占庭将军问题的一般描述，即每个将军都有自己独立的判断：“进攻”或“撤退”；但最后综合所有其他人的意见做出决策。

3.1.2 中心VS去中心

拜占庭将军问题的描述与我们平时的投票场景类似，以“少数服从多数”的办法来统一意见。它们之间的区别在于：传统投票有一个权威中心来统一唱票公布结果；而拜占庭将军们则是互通消息，各自唱票，最后是否能达成共识是个顺其自然的过程。由于在执行过程中并没有像传统投票那样有一个权威中心，所以拜占庭将军是去中心化的；也正因这一点区别，在存在叛徒的情况下拜占庭将军问题变得复杂了。

为了阐述清楚问题，我们在围剿盗跖的例子里分开上述两种情况对比讨论：

子贡、子有和子路兵分三路围剿盗跖。三支军队都占尽天时地利人和，作为理性的参与者都应做出”进攻”的判断；三支军队只要有两支发动进攻即可取胜，否则将会失败。其中子贡与盗跖有私交，不希望发生战事，他会尽力阻止军队对盗跖的围剿。

中心化：子贡、子有和子路在大帐议事。通过唱票人清点票数得出结果采取统一行动。唱票人拥有很高的权限，掌握所有人的票以及公布结果；他的诚实与否直接影响最后的结果。

（1）子贡唱票：                             （2）：子有唱票

大帐议事

子有唱票

投票选项

进攻

撤退

子贡

子路

子有

共识结果：

大帐议事

子贡唱票（结果之一）

投票选项

进攻

撤退

子贡

子路

子有

共识结果：

去中心化：子贡、子有和子路率兵分扎三处，他们互通消息。诚实的参与者会如实的表达自己的判断，并会诚实地转发他人判断；然而叛徒将会随意地发送或转发任何消息。

图3-2：子路和子有是诚实的将军，他们如实地发送A\(○\)和B\(○\)给其他两人；子贡怀有异心，他发送了掩饰自己真实判断的M\(×\)给子有和子路。

因为子贡心怀异心，他的行动变得不可判断，所以我们只需要关心子有和子路的决定。

转发消息后，子有和子路得到的判断表格；

子路

消息源

子路唱票

图1：诚实将军的情况，三人呈三角第一次互发消息互换信息。

子有

子贡

消息对象

子有

子贡

子路

子路采取的行动：

表3-5：子路从子有那里都获得了“进攻”的判断，从子贡那里获得任意取值的判断。子路处唱票的结果是"进攻"，并采取了"进攻"的行动。

子有

消息源

子有唱票

图1：诚实将军的情况，三人呈三角第一次互发消息互换信息。子路

子贡

消息对象

子路

子贡

子有

B采取的行动：

表3-6：子有从子路那里都获得了“进攻”的判断，从子贡那里获得任意取值的判断。子有处唱票的结果是“进攻”，并采取了“进攻”的行动。

分散领兵

采取的决策

子路

子有

子贡

表3-7：子贡采取的行动不可测；但子有和子路都采取了“进攻”行动，诚实将军达成了共识，并取得了成功。

从上表可看出，尽管子贡怀有异心，但是子有和子路接收到的数据是并不影响他们最后的决定；所以诚实的子路和子有最终都能采取"进攻"的行动（实现一致性）；三支军队有两支保证进攻，取得了胜利（实现正确性）。

在中心化的情况中，唱票人就是整个投票机制的核心，所有消息的输出都要经过唱票人之手；如果唱票人是怀有异心的子贡，那么无论有多少将军投票，最终结果都在子贡一念之间。第二种情况很好反映了去中心化的特点：任意一名将军都不能单独操控所有消息的输出，每个将军的消息输入都有多个消息源；尽管有错误或无效消息的干扰，但最后诚实的将军们还是能达成一致的正确的”进攻"共识。去中心化的例子是Lamport口头协议中四模冗余的情况之一；口头协议将在3.1.4节详细介绍。此外，Lamport提供的另一个解决方案是书面协议，将在3.1.5节介绍。

3.1.3 拜占庭将军问题的严格描述

拜占庭将军问题若不加限制：每个将军根据自身情况会有“撤退”或“进攻”的独立判断；并且在正确性的问题上难以界定：譬如刚好一半的将军可进攻一般不可。细心的读者一定发现，在3.1.2的例子里，我们将情况简化为每个将军只有“撤退”的判断。这等同于多添加了一名将军们的长官，直接给他们下达了“进攻”的命令；从图的角度来说，就是增加了一个超级汇点。于是拜占庭将军问题的一般描述就简化为其严格描述\_：

将3.1.2中图3-2转化到经典描述：

刚正不阿的伯牛挂帅，并直接向这子贡、子有和子路下达”进攻”命令。

图3-3：将例子对应到经典的四模冗余情况。伯牛向子贡、子有和子路下达”进攻"命令；三个元帅间的命令转发和图3-2的例子一样。

将图3-2和图3-3做比较，你会发现两幅图并无本质区别，但在阐述上图3-3的情况更容易理解；这也解释了图3-2的例子是"四"而非“三”模冗余的原因。在图3-3例子中，若改为子贡是元帅，那将是四模冗余的另一种情况了。

3.1.4 口头协议

口头协议和书面协议都是针对拜占庭将军问题经典描述的解决方案。口头协议能保证叛徒数不超过三分之一情况下的一致性和正确性。

这理解并不难，只需要将图3-3的例子去掉一个将军，你将会看到在三模冗余的情况下，拜占庭将军问题使用口头协议是不可解的。

三模冗余（m＝1，n＝3）：

（1）叛徒是将军：                                    （2）叛徒是元帅：

子路

子有

消息源

接收到的命令

消息源

接收到的命令

子有

子路

子贡

子贡

子路

消息源

接收到的命令

伯牛

子贡

从读者的上帝视角来看，在图3-4的例子中，元帅是诚实的，只要子路执行"进攻"命令，那么一致性和正确性都实现了；在图3-5的例子中，元帅是叛徒，只要子有和子路执行了一致的"进攻"或"撤退"的命令，那么一致性和正确性也都能实现。

很可惜，处于局中的子路并不知道谁是叛徒；且在两种情况下，他收到的命令集都是{○，×}。也许有读者灵机一动：事先设定默认值为○是否就能解决了“命令集两个元素对半分”的情况？因为在图3-4和图3-5的例子中，诚实副官们都有一样的命令集{○，×}。这样，两个例子的一致性和正确性都实现了。看起来很完美，可惜这个方法遇到"诚实的元帅给将军下达"撤退"命令"的情况就失效了。

子路

消息源

接收到的命令

伯牛

子贡

若采取了默认值为○的方法，在图3-6的例子里，子路执行了"进攻"命令，就违背了"执行诚实元帅命令"的正确性。因此在三模冗余中，子路收到的命令集都是{○，×}而且他不知谁是叛徒的情况下，无论默认"进攻"还是"撤退"，子路都有可能违背正确性。

四模冗余（m＝1，n＝4）：

四模冗余元帅是诚实的例子已在前面3.1.2中解释过，此处不再复述；当元帅是叛徒的时候，口头协议依然能发挥效用。

图3-7：叛徒子贡成为了元帅，分别给三个诚实的将军命令下达了无效命令。子有，子路和伯牛如实地将命令转发给其他人。

子路

子有

伯牛

消息源

接收到的命令

消息源

接收到的命令

消息源

接收到命令

子有

Y

子路

X

子路

X

伯牛

Z

伯牛

Z

子有

Y

子贡

X

子贡

Y

子贡

Z

表3-11：伯牛，子有和子路收到一样的命令集{x, y,z}.

在四模冗余的情况下，只要对没有出现多数元素的命令集设定默认值，例如对{x, y,z}设定为"进攻"命令，拜占庭将军问题就可解。也即是说，读者在三模冗余中不凑效的"灵机"在四模冗余中就完全可用。原因是四模冗余的诚实将军占了大多数：在元帅是真实的情况下叛徒能操控的票数不能影响诚实将军的最终结果;在元帅是叛徒的情况下与三模冗余相同，诚实将军获得的命令集一样。因此，对叛徒数目做出限定是必要的。

3.1.5 书面协议

书面协议是在口头协议的基础上引入了数字签名（如有遗忘，可复习2.6章节），也即是叛徒们再也无法篡改诚实元帅或将军们的命令，但是他们可以篡改叛徒的命令及伪造上面的签名；因此，它可以解决一些口头协议无法凑效的情况。下面我们以三模冗余（m＝1，n＝3）为例，来分析书面协议。

（1）    叛徒是将军：

子路

消息源

接收到的消息

伯牛

：伯牛

子贡

：伯牛：子贡

图3-9：子路先收到了元帅伯牛的命令和签名，他用伯牛的公钥解密签名后，确认内容一致；因此，子路确认元帅伯牛的确发送了"进攻"的命令。接着，子路收到了子贡的转发内容。他先用子贡的公钥解密子贡的签名，确认消息的确是子贡发送的。接着子路用伯牛的公钥解密子贡发送过来的伯牛签名，再和子贡发送过来伯牛命令作对比；他发现内容不一致，验证失败。至此，子路知道子贡是叛徒篡改了内容；子路执行"进攻"命令。

（2）    叛徒是元帅：

图3-10：叛徒子贡给子路下达了附签名的"进攻"命令，给子有下达了附签名的"撤退"命令。子路和子有相互转发了子贡的命令和签名，并在后面添加上自己的签名。

子路

消息源

接收到的消息

子贡

：子贡

子有

：子贡 ：子有

子有

消息源

接收到的消息

子贡

：子贡

子路

：子贡 ：子路

图3-11：子路先收到了元帅子贡的命令和签名，他用子贡的公钥解密签名后，确认内容一致；因此，子路确认元帅子贡的确发送了"进攻"的命令。接着，子路收到了子有的转发内容。他先用子有的公钥解密子有签名，确认消息的确是子有发送的。接着子路用子贡的公钥解密子有发送过来的子贡签名，再和子有发送过来子贡的命令作对比；内容一致，验证成功，子有转发的消息的确也是子贡发的。子路收到的命令集为{○，×}；同理，子有也收到一样的命令集{○，×}。与口头协议一样，只要事先设定好默认值，子路和子有就能采取一致的行动。

在书面协议中，只要元帅是诚实的，他诚实的将军只会收到一种命令；当元帅是叛徒，诚实的将军都会收到同样的命令集，所以和口头协议一样，只要事先设定默认值就可实现一致性和正确性。很明显，书面协议只需要总人数不少于m+2就能有效运行。

3.1.6 脑洞：拜占庭将军问题－&gt;比特币－&gt;新型契约－&gt;新型社会

比特币的区块链网络和拜占庭将军问题的描述非常类似：网络中的每个节点就类似一个独立的拜占庭将军；一个节点发起交易就类似经典描述中的司令给他的副官下达命令。这个节点可以是诚实的；也可以是恶意的，比如说发起“双花”攻击（详细介绍在4.1.1节）。区块链可说尽得拜占庭将军问题去中心化的精髓：任意一个节点都不能单独操控系统中所有消息的输出，每个节点的消息输入都有多个消息源。当然，比特币的区块链在实现时对书面协议做了调整：每个诚实的节点能根据事先设定好的规则判断消息输入的合法性，直接做出“接收”或“拒绝”的决策。

比特币系统至今仍在运行，可以说颠覆了很多人的认识；首当其冲的就是金融界。金融是建立在信任（Trust）上的学科。何为信任，就是我与你在同一件事上达成共识；你将来的行为会在我期望之内。这也是契约的雏形。在比特币系统出现之前，强而有力的中心化权威机构是实现信任的唯一途径。最日常的例子就是纸币。纸币本身并不具有价值，但大家都有“纸币能交换与其面值等价商品”的共识并深信不疑。为什么？这是因为有国家这个强大的中心化权威机构为纸币的支付能力做担保。“不能拒收人民币”也许是最好诠释。纵观各国无不是中央银行发行货币和制定货币政策；我们的中国人民银行，美国的美联储。可是比特币的出现颠覆了一切，它没有一个中心化的权威机构给它背书，但到现在已经在事实上能执行货币两大最基本的职能：价值尺度和流通手段。此外，比特币的发行和发行量是由事先设计好的数学模型决定，代码自动执行；运行后，再也没有人可以修改或掌控。央行和比特币系统，正好就是开篇雅典公民大会和拜占庭将军问题场景的一一映射。

图3-12：In God We Trust.美元的本质是政府发放的债务。In God We Trust现引申为对美国政府的信任：一定能清还债务。正是这种信任，美元可以执行货币的五项职能。

信任和契约是整个社会正常运转的基石，只是在金融领域尤为显著。既然我们有了新的方法达成共识，自然在其他领域也将掀起创新。这也是Melanie.Swan所提及的区块链2.0（智能合约）和区块链3.0（新型社会）的远景。智能合约的例子已在第一章物联网的场景中有所介绍；以太坊是现在智能合约方面的先驱，所以技术部分将放在第六章中介绍。

区块链最宏伟的远景就是高度自动化的社会。这种自动化并不是业务流水线这样的量变，而是在业务逻辑上产生了质变；而这种质变让中心化机构的存在都成为了多余，因为信任和契约的实现可以是在去中心化低信任度的环境中完成。换句话说，也即是传统意义上的中心化政府也无需存在：这真是无政府自由主义者的宣言啊。带给笔者最震撼的地方也就是在这里：曾经的无政府主义是无序混乱的代言词，但是区块链技术为井然有序的无政府社会提供了可能。不管最后能否实现，至少在金融领域已经开了先例。

3.1.7 对拜占庭将军问题的疑问

1. 拜占庭将军问题是两军问题吗？

不是。虽然两个问题都是为了探讨如何达成共识的，但前提条件有明显的区分：拜占庭问题的信道是可靠的，两军问题的信道则是不可靠的。网上有大量的文章将两者混为一谈，这里有必要澄清。

两军问题的描述：山谷两边的蓝军要同时进攻谷内的白军才能取胜。他们互派信使确认进攻时间，但信使必须冒着被俘的危险经过白军的地盘。问是否存在蓝军必胜的协议。

两军问题是为了探讨可靠信道的存在性，即消息发送后是否存在不被窃听或丢失的方法——保证信使不被俘，这在以前是无解的；但量子物理的发展提供了量子通讯协议的解决方案。2016年8月16日凌晨中国发射的"墨子号"就是世界首颗量子通讯卫星！

拜占庭将军问题是以可靠信道作为前提的，也即是信息从发送方到接收方中间的传递过程是假设可靠的。无论叛徒或诚实的将军，他们的消息发出后一定会送到接收方手里；他们也不会跑到别人的信道上去监听或拦截非传递给自己的消息。

1. 分布式系统和去中心化系统有什么关系？

分布式系统是这样的模型：在联网电脑中的部件通过互传消息交流和协调工作；部件交互工作以达成共同目的 。网络上存在"去中心化"的很多定义。笔者认为，去中心化针对区块链来说有两点含义。一是网络中不存在中心节点：节点与节点之间不存在从属关系，它们的地位对等。二是消息的传播不存在中心控制。去中心化的系统必定是分布式系统，但分布式系统不一定是去中心化的系统。
