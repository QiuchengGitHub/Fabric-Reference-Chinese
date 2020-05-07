#<center>Fabric中文官方文档  V1.1</center>#

##welcome##
![](http://hyperledger-fabric.readthedocs.io/en/release-1.1/_images/hyperledger_fabric_logo_color.png)

Hyperledger Fabric是一个分布式账本解决方案平台，支持模块化架构，提供高度机密性、弹性（resiliency）、灵活性和可扩展性。它被设计成支持不同组件的插拔式实现，并适用于整个经济生态系统中存在的复杂性（complexity and intricacies）。

不同于其他区块链解决方案，Hyperledger Fabric提供了一个独特地弹性的（elastic）和可扩展的架构。规划企业区块链的未来需要建立在全面审核（fully-vetted）、开源的架构之上。Hyperledger Fabric就是你的起点。

我们推荐第一次使用的用户，从“入门”章节开始熟悉Hyperledger Fabric相关的一些组件和基础事务流（basic transaction flow）。理解了之后，再继续探究示例类库、技术规范（technical specifications）、APIs等等。

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		如果你有该文档未介绍到的问题，或者在运行任何教程时碰到了问题，请访问“十二、 仍有问题”章节来获取额外的帮助。
		</td>
	</tr>
</table>


##目录##
###一、入门###
####预处理####
#####安装 cURL#####
如果你还没有安装cURL工具，请下载最新的版本进行安装。否则运行本文档的curl命令时会报错。

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		如果你是Windows操作系统使用者，请参考下方有关Windows的详细介绍。
		</td>
	</tr>
</table>

#####Docker和Docker Compose#####
你还需要安装下列Hyperledger Fabric所需相关工具：

+ MacOSX, *nix, 或 Windows 10: Docker 17.06.2-ce 或更高版本
+ 老版本Windows: Docker Toolbox，以及Docker 17.06.2-ce 或更高版本

你可以在终端提示中使用下列命令来检查Docker版本：

	docker --version

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		为Mac或Windows安装Docker或Docker Toolbox时，也需要安装Docker Compose。如果你已经安装了Docker，需要确认Docker Compose的版本为1.14.0或者更高。否则我们建议你重新安装一个新的版本来使用。
		</td>
	</tr>
</table>

你可以在终端提示下使用下列命令来检查Docker Compose的版本：

	docker-compose --version

#####Go编程语言#####
Hyperledger Fabric的很多容器都使用了Go编程语言1.9.x。

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		不支持使用Go 1.8.x版本
		<p>
		Go - version 1.9.x
		</td>
	</tr>
</table>

鉴于要使用Go来编写chaincode程序，我们要正确设置两个环境变量。可以在合适的启动文件中加入环境变量来永久生效，比如如果你在Linux上使用bash shell，你可以修改你个人的 ~/。bashrc文件

首先，你必须设置环境变量GOPATH来指定包含下载的Fabric代码的Go workspace:

	export GOPATH=$HOME/go

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		一定要设置GOPATH变量
		<p>
		即使在Linux中，GO的GopATH变量可以是一个冒号分隔的目录列表，如果未设置，将使用$home /Go的默认值，但是当前的Fabric构建框架仍然要求你设置并导出该变量，并且它必须只包含GO workspace的单个目录名。工作区。（此限制可能会在将来的版本中去除）。
		</td>
	</tr>
</table>

其次，你需要（在适当的启动文件中）扩展你的命令搜索路径，使其包含Go的bin目录，例如在Linux下使用bash的示例：

	export PATH=$PATH:$GOPATH/bin

即使在一个新的Go workspace安装路径中不存在该目录，Fabric构建系统也会在后期自动创建该目录。因此，如果你当前没有该目录，也需要如上扩展你的shell搜索路径。

#####Node.js Runtime and NPM#####
如果你后期需要针对Hyperledger Fabric SDK做开发，你需要安装Node.js 8.9.x或更高版本。

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		本次不支持Node.js 9.x版本
		<p>
		只支持Node.js - 8.9.x 或更高版本
		</td>
	</tr>
</table>

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		安装Node.js时也要求安装NPM，我们建议你确认下所安装的NPM的版本。你可以使用下列命令来升级你的npm工具：
		</td>
	</tr>
</table>

	npm install npm@5.6.0 -g

######Python######
<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		下列只适用于Ubuntu 16.04版本使用者
		</td>
	</tr>
</table>

默认情况下，Ubuntu 16.04使用的是基于python3类库的Python 3.5.1。Fabric Node.js SDK需要使用Python 2.7版本来确保npm操作正确完成。所有请使用下列命令回退（retrieve）到2.7版本：
	
	sudo apt-get install python

检查你的版本:
	
	python --version

#####Windows extras#####
如何你在Windows 7上进行开发，你会倾向于在Docker Quickstart终端里使用Git Bash而不是内置的Windows shell。

虽然经验告诉我们Windows是一个局限性的开发环境。但是跑一些Docker基础场景还是可以的，比如入门章节的内容，但是你在使用make和docker命令时可能会碰到一些问题。

在Windows 10上，你应该使用本地Docker分布式，并且可以使用Windows PowerShell。但是，对于下载平台特定的二进制命令要执行成功，您仍然需要unMAME命令可用。您可以将其作为Git的一部分，但要注意仅支持64位版本。

在运行任何git clone命令之前，先运行下列命令：

	git config --global core.autocrlf false
	git config --global core.longpaths true

你可以使用下列命令来检查参数设置：

	git config --get core.autocrlf
	git config --get core.longpaths

这些需要分别被设置为false和true。

Git和Docker Toolbox自带的curl命令是旧版本的，无法正确处理在开始时使用的重定向。请确保从cURL下载页面安装并使用较新版本。

对于Node.js，你也需要必需的Visual Studio C++构建工具，该工具是免费的并可以使用下列命令安装：

	npm install --global windows-build-tools

参考NPM windows-build-tools页面（https://www.npmjs.com/package/windows-build-tools）以获得更多信息。

完成之后，你可以使用下列命令来安装NPM GRPC模块：

	npm install --global grpc

截止目前，你的环境应该已经准备完毕了。

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		如果你有该文档未介绍到的问题，或者在运行任何教程时碰到了问题，请访问“十二、 仍有问题”章节来获取额外的帮助。
		</td>
	</tr>
</table>

####Hyperledger Fabric Samples####
<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		如果你的运行环境是Windows，你需要用到Docker Quickstart终端来执行后面的终端命令。如果你还没有安装，请参考“预处理”章节完成安装。
		<p>
		如果你使用的是Windows 7或者macOS上的Docker Toolbox，当安装和执行示例时，你会用到如下路径：C\Users（Windows 7）或 /Users（macOS）。
		<p>
		如果你使用的是Mac上的Docker，你需要使用如下路径：/Users，/Volumes，/private或/tmp。如果要使用另一个路径，请参考Docker文档。
		<p>
		如果你使用的是Windows上的Docker，请参阅Docker文档的共享驱动器，并使用一个共享驱动器下的位置。
		</td>
	</tr>
</table>

在你的机器上选择一个路径，该路径用于放置Hyperledger Fabric示例程序。在终端窗口中执行下列命令：

	git clone -b master https://github.com/hyperledger/fabric-samples.git
	cd fabric-samples
	git checkout {TAG}

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		为了确保这些样本与之前下载的BRAGE二进制文件兼容，请坚持示例{TAG}是否匹配你的Fabric版本，例如，v1.1.0。要查看所有fabric示例tags，请使用“git tag”命令。
		</td>
	</tr>
</table>

#####下载平台特定的二进制文件#####
下面，我们将安装Hyperledger Fabric平台特定二进制文件。该过程被设计为补充上面的Hyperledger Fabric示例，但是也可以独立使用。如果您没有安装上面的示例，那么简单地创建并输入一个目录，以提取平台特定二进制文件的内容。

进入指定的目录，执行下面的命令：

	curl -sSL https://goo.gl/6wtTN5 | bash -s 1.1.0

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		如果在运行上述命令时报错，可能是因为当前环境不支持该命令或者你的curl版本太老了。
		<p>
		请访问“预处理”章节获取相关信息。或者，你可以替换未缩短的URL：https://github.com/hyperledger/fabric/blob/master/scripts/bootstrap.sh
		</td>
	</tr>
</table>

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		你可以针对任何发布的Hyperledger Fabric版本执行上述命令。只需将“1.1.0”这个版本号做相应替换即可。
		</td>
	</tr>
</table>

上述命令下载并执行BASH脚本，该脚本将下载和提取所有设置网络所需的特定平台二进制文件，并将它们放置到上面创建的克隆目录中。它检索四个平台特定二进制文件：

+ cryptogen，
+ configtxgen，
+ configtxlator，
+ peer
+ orderer and
+ fabric-ca-client

并将他们放置在当前工作目录的bin子目录中。

您可能希望将其添加到路径环境变量中，以便可以在不完全限定每个二进制路径的情况下拾取这些变量。例如：

	export PATH=<path to download location>/bin:$PATH

最终，该脚本会从Docker Hub下载Hyperledger Fabric docker镜像到你本地并标记他们为“latest”。

脚本列出了结束后安装的所有Docker镜像列表。

查看每个镜像的名称；这些组件将最终构成我们的Hyperledger Fabric网络。你将会注意到，你有两个实例是相同的镜像ID - 一个标记为“x86_64-1.x.x”而另一个标记为“latest”。

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		在不同的架构中，x86_64会被你自己架构的字符识别码做替换。
		</td>
	</tr>
</table>

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		如果你有该文档未介绍到的问题，或者在运行任何教程时碰到了问题，请访问“十二、 仍有问题”章节来获取额外的帮助。
		</td>
	</tr>
</table>

####Install Prerequisites####
在我们开始之前，希望你能检查你已经完成了所以的准备工作。

####Install Binaries and Docker Images####
为Hyperledger Fabric二进制文件开发真正的安装程序时，我们提供了一个脚本，它将下载特定于平台的二进制文件到你的系统。脚本还将下载Docker镜像到您的本地注册表

####Hyperledger Fabric Samples####
我们提供了一系列示例程序，在开始教程之前，你可以安装并运行这些示例。

####API Documentation####
Hyperledger Fabric的Golang API文档可以在Fabric的godoc站点（https://godoc.org/github.com/hyperledger/fabric）找到。

####Hyperledger Fabric SDKs####
Hyperledger Fabric提供了多种SDKs来支持多编程语言。 下面是两个正式发布的SDKs:Node.js和Java：

+ Hyperledger Fabric Node SDK（https://github.com/hyperledger/fabric-sdk-node）和Node SDK documentation（https://fabric-sdk-node.github.io/）.
+ Hyperledger Fabric Java SDK（https://github.com/hyperledger/fabric-sdk-java）.

此外，还有三个还没正式发布的SDKs（Python、Go和REST），但是可以自由下载和测试：

+ Hyperledger Fabric Python SDK.（https://github.com/hyperledger/fabric-sdk-py）
+ Hyperledger Fabric Go SDK.（https://github.com/hyperledger/fabric-sdk-go）
+ Hyperledger Fabric REST SDK.（https://github.com/hyperledger/fabric-sdk-rest）

####Hyperledger Fabric CA####
Hyperledger Fabric提供了可选的证书认证服务，您可以选择使用它来生成证书和关键材料，以配置和管理区块链网络中的身份。然而，任何可以生成ECDSA证书的CA认证方式都可以被接入进来使用。

###二、核心概念###
####介绍####
Hyperledger Fabric是一个分布式账本解决方案平台，支持模块化架构，提供高度机密性、弹性（resiliency）、灵活性和可扩展性。它被设计成支持不同组件的插拔式实现，并适用于整个经济生态系统中存在的复杂性（complexity and intricacies）。

不同于其他区块链解决方案，Hyperledger Fabric提供了一个独特地弹性的（elastic）和可扩展的架构。规划企业区块链的未来需要建立在全面审核（fully-vetted）、开源的架构之上。Hyperledger Fabric就是你的起点。

我们推荐第一次使用的用户，从“入门”章节开始熟悉Hyperledger Fabric相关的一些组件和基础事务流（basic transaction flow）。理解了之后，再继续探究示例类库、技术规范（technical specifications）、APIs等等。

#####Blockchain是什么?#####
######一个分布式账本######
区块链网络的核心是一个分布式账本，该账本记录了网络中发生的所有交易。

区块链账本通常被描述为是分权的，因为网络中每一个参与者都拥有完整的备份，并且每个参与者都在维护中进行协作。我们知道，分权和协作是反映企业在现实世界中交换商品和服务的强有力的属性。

![](images/basic_network.png)

除了分权和协作，记录到区块链的信息只支持追加，通过使用加密技术来保证一旦交易被添加到账本，它就不能被修改。这种不可修改的特性使得确定信息的来源很简单，因为参与者可以确信信息在创建之后没有被改变。这就是为什么区块链有时被描述为证据系统。

######智能合约######
为了支持信息的一致更新，并实现整个账本功能（交易、查询等）——区块链网络使用智能合约来提供对账本的访问控制。

![](images/Smart_Contract.png)

智能合约不仅仅只是一种用于封装信息和保证简单跨网络传输的关键机制，它也可以被改写来允许参与者自动执行事务某些方面的工作。

例如，一个智能合约可以被指定为规定一个物品的运输成本，该成本取决于它何时到达。当双方意见一致并写到账本时，会触发对应资金的自动转手。

######共识（Consensus）######
保持账本交易在网络中同步的过程-以确保只有当交易被适当的参与者批准时，账本才更新，而当账本进行更新时，它们以相同的顺序更新同一交易-被称为共识。

![](images/consensus.png)

后期我们会深度学习账本、智能合约和共识。对于现在，只要有如下认识即可：区块链是一个共享的、多备份的交易系统，使用智能合约来实现更新并通过共识机制来保持一致性同步。

#####区块链为什么有用?#####
######目前的记录系统######
目前的交易网络只不过是自从业务记录被保存以来就存在的网络的稍有更新的版本。业务网络的成员相互交易，但他们保持各自的交易记录。而他们交易的东西——无论是十六世纪的佛兰芒挂毯还是今天的证券——每卖出一次就必须建立起它们的出处，以确保出售一项商品的商家拥有一系列所有权来验证其所有权。

你所处的业务往来看起来如下所示：

![](images/current_network.png)

现代技术已经把这个过程从石板和纸文件夹搬到了硬盘和云平台，但底层结构是相同的。管理网络参与者身份的统一系统是不存在的，建立出处是费力的，需要数天的时间来清除证券交易（世界上的证券交易数有数万亿美元），合同必须手动签署和执行，并且系统中的每一个数据库包含唯一信息，因此只能表示单点故障。

基于现状来构建一个跨业务网络的记录系统来共享信息和过程是不可能实现的，即使可见度和信任度的需求是明确的、迫切的。

######区块链不同之处######
如果不是由“现代”交易系统所代表的低效巢，那么商业网络就有了在网络上建立身份、执行交易和存储数据的标准方法吗？如果建立一个资产的来源，可以通过查阅一笔交易，一旦被写入，不能被改变，因此可以被信任。（What if, instead of the rat’s nest of inefficiencies represented by the “modern” system of transactions, business networks had standard methods for establishing identity on the network, executing transactions, and storing data? What if establishing the provenance of an asset could be determined by looking through a list of transactions that, once written, cannot be changed, and can therefore be trusted?)

那么业务网络会看起来如下所示：

![](images/future_net.png)

这是一个区块链网络，每个参与者都有自己的账本副本。除了账本信息被共享，更新账本的过程也会被共享。不像当前的系统，一个参与者的私有程序才能更新它的私有账本，一个区块链系统有共享程序来更新共享账本。

有能力通过共享账本协调业务网络，区块链网络可以减少与私有信息和处理相关的时间、成本和风险，同时提高信任和可见性。

截至目前，你已经了解了区块链是有用的，并且了解了为什么区块链是有用的。还有一些其他的重要细节信息，但它们都是基于共享信息和处理的基础思想。

#####Hyperledger Fabric是什么?#####
Linux基金会在2015成立了Hyperledger来推动跨行业的区块链技术。它并不是宣布了一个单独的区块链标准，而是通过一个社区来鼓励开发区块链技术，其知识产权鼓励开放开发和随着时间的推移采用关键标准。

Hyperledger Fabric是Hyperledger中的一个区块链项目。类似于其他区块链技术，Hyperledger Fabric是一个账本，使用智能合约，并且是一个供参与者管理交易信息的系统。

Hyperledger Fabric与其他区块链系统的区别是，它是私有的、有权限的。与允许未知的身份参与到网络（需要类似工作量证明Proof of Work协议来验证交易和保护网络）中的开放权限的系统不同，Hyperledger Fabric网络的成员通过一个信任的Membership Service Provider（MSP）来实现登记。

Hyperledger Fabric也提供了多个可插拔的选项。账本数据可以存储于多种格式，共识机制可以被换入和换出，并且支持不同的MSPs实现。

Hyperledger Fabric也提供了创建channels的功能，允许一组参与者来创建一个分离的交易账本。 这是网络中一个特别重要的选项，因为其中一些参与者可能是竞争对手，不希望他们做的每一笔交易被所有参与者都知晓。例如，他们给部分参与者提供的额外的好处，而不是给所有参与者。如果两个参与者形成一个频道，那么这些参与者（而不是其他人）都有该频道的分类帐的副本。

######共享账本######
Hyperledger Fabric有一个账本子系统，包括两个组件：世界状态（the world state）和交易日志。对于所属的每一个Hyperledger Fabric网络，参与者都有一个账本的副本与之对应。

世界状态组件描述的是给定时间点的账本状态。它是账本数据库。交易日志组件记录所有影响世界状态当前值的交易信息，它是时间状态的变更历史记录。账本，就是由世界状态数据库和交易日志历史组成的。

账本为世界状态提供了一个可替换的数据存储方式。默认情况下，是LevelDB类型的key-value存储数据库。交易日志是不需要实现可插拔的。它只是被区块链网络用来简单记录账本数据库的前后变化值。

######智能合约######
Hyperledger Fabric智能合约被写入chaincode并被区块链外部的应用所调用。当外部应用想操作账本时，调用智能合约即可。在绝大多数场景中，chaincode只作用于账本的数据库组件以及世界状态（比如，查询），而不与交易日志交互。

Chaincode可以以多种编程语言来实现。目前支持Go和Java，其他的语言会在将来的版本得到支持。

######隐私######
根据网络的需要，B2B网络中的参与者可能对他们共享了多少信息十分敏感。对于其他网络，隐私可能不是最关注的点之一。

Hyperledger Fabric支持一个（使用channels）将隐私作为关键操作需求并相对开放的网络。

######共识######
交易必须以其发生的顺序写到账本中，即使它们可能存在于网络中不同的参与者集合之间。要做到这一点，必须建立交易的顺序，并且必须建立驳回不良交易的方法，来剔除那些错误（或者恶意）插入到账本的交易信息。

这目前还是计算机科学的研究领域，并且有多种方式可以实现，但都有各自的利弊。例如，PBFT（Practical Byzantine Fault Tolerance）为文件备份提供了一种机制，即使在“腐败”的情况下也能使其在各节点间交互并保证备份一致性。此外，在Bitcoin中，排序是通过一个称为挖掘的过程发生的，在这个过程中，参与的计算机竞争来解决一个密码难题，它定义了所有进程随后建立的顺序。

Hyperledger Fabric已经被设计成允许网络启动者选择最能代表参与者之间存在的关系的一致性机制。与隐私一样，存在着一系列需求；从关系高度结构化的网络到更对等的网络。

我们会深度学习Hyperledger Fabric的共识机制，目前包括SOLO，Kafka并且很快将扩展到SBFT(Simplified Byzantine Fault Tolerance)。

#####我可以从哪儿学到更多?#####
######入门######
我们提供了一系列教程，介绍了区块链网络中的大部分关键组件并讲解他们如何协同合作，你也在一个运行的区块链网络中获取源代码并运行一些示例。我们也提供了使用Hyperledger Fabric来操作区块链网络的教程。

######Hyperledger Fabric模型######
更深入地了解本文介绍的组件和概念以及其他几个方面，并描述它们如何在一个示例交易流中协同工作。
#####Hyperledger Fabric功能#####
Hyperledger Fabric是一个分布式账本技术（DLT,distributed ledger technology）实现。并以一个模块化的区块链架构驱动企业就绪（enterprise-ready）网络的安全，可扩展性，机密性以及性能。Hyperledger Fabric提供了下列区块链网络功能：
#####身份管理#####
为了实现权限网络，Hyperledger Fabric提供了一个会员身份服务来管理用户IDs和认证网络中的所有参与者。访问控制列表可用于通过授权特定的网络操作来提供额外的许可层。例如，可以允许特定的用户ID调用一个chaincode应用，但阻止其部署新的chaincode。
#####隐私和机密性#####
Hyperledger Fabric考虑到了商业利益的竞争，允许任何需要私密、机密交易的团体和其他团体共存于同一个权限网络之中。。私有channels信道是可用于为网络成员的特定子集提供交易私密性和机密性的受限消息路径。信道上的所有数据，包括交易、成员和channel信息，对任何未明确授予该channel访问权限的网络成员来说是不可访问的。
#####高效处理#####
Hyperledger Fabric按照节点类型分配网络角色。为了向网络提供并发性和并行性，交易的执行与交易的排序和提交是分离开的。先执行交易然后对交易进行排序的处理方式使每个peer节点能够同时处理多个交易。这种并发执行增加了每个peer的处理效率，并加速了向排序服务传递交易的效率。

除了启用并行处理之外，分工也缓解了排序节点交易执行和账本维护的压力，同时也将peer节点从排序（共识）工作负担中解脱出来。角色的区分也限制了授权和认证所需的处理；所有peer节点不必信任所有的排序节点，反之亦然，因此一个节点上的进程可以独立于另一个节点运行。
#####Chaincode功能#####
Chaincode应用编码了逻辑，这些逻辑由channel上特定类型的交易来调用。例如，chaincode为资产所有权变化定义的参数，确保所有转移所有权的交易都遵循相同的规则和要求。系统chaincode为整个channel定义了操作参数。生命周期和configuration system chaincode为该channel定义了规则；背书（endorsement）和validation system chaincode定义了背书和验证交易的要求。
#####模块化设计#####
Hyperledger Fabric是模块化架构实现，为网络设计提供了功能选择。例如，用于身份、排序（共识）和加密的特定算法可以插入到任何Hyperledger Fabric网络中。好处是，实现了任何行业或公共领域都可以采用的通用区块链架构，并保证其网络可以跨市场、监管和地理边界进行互操作。
####Hyperledger Fabric模型####
本节概述了Hyperledger Fabric的关键设计特性，实现了一个全面但可定制的，企业级的区块链解决方案的承诺：

+ Assets - 资产定义允许网络上绝大多数有价值属性的东西进行交换，从古董车到货币期货。
+ Chaincode - Chaincode执行与交易排序是分开的，限制了跨节点类型的信任和验证所需的级别，并优化了网络可扩展性和性能。
+ 账本特性 - 不可变的、共享的账本针对每个channel进行整个交易历史的编码，并且通包括SQL类似的查询能力以进行有效的审计和争议解决。
+ Channels隐私 - Channels在一个共同的网络中实现了多方交易的高度隐私性和保密性，这也是竞争企业和管理产业所注重的。
+ 安全&会员服务 - 权限会员系统提供了一个可信的区块链网络，参与者知道所有交易可以被授权的监管者和审计员检测和跟踪。
+ 共识 - 一种独特的共识方式实现了企业需要的灵活性和可扩展性。
#####资产#####
资产可以是有形资产（房地产和硬件），也可以是无形资产（合同和知识产权）。Hyperledger Fabric使用chaincode交易提供了修改资产的功能。

在Hyperledger Fabric中，资产是以键值对集合存在的，状态变化被记录为channel账本上的交易信息。资产可以用二进制和/或JSON格式表示。

在你的Hyperledger Fabric应用中使用Hyperledger Composer工具就可以轻易地定义和使用资产。
#####Chaincode#####
Chaincode是定义一个或多个资产的软件，以及用于修改资产的交易指令。换句话说，就是业务逻辑。Chaincode强制执行读取或更改键值对或其他状态数据库信息的规则。Chaincode针对账本的当前状态数据库执行操作，并通过交易提议发起。Chaincode执行导致一组键值写入（写集），它可以提交给网络并应用于所有peers上的账本。
#####账本特性#####
账本是Fabric中所有状态转变的有序的、防篡改的记录。状态转换是参与方提交的chaincode调用（“交易”）的结果。每笔交易都会产生一组资产键值对，这些资产键值对作为创建、更新或删除提交到账本。

账本由区块链（“链”）组成，在blocks中存储不可变的、有序的记录，以及保持当前Fabric状态的一个状态数据库。每个channel都有一个账本。每个peer维护当前成员所属所有channel的账本副本。

+ 使用基于关键字的查找，范围查询和组合关键字查询来查询和更新账本
+ 使用rich查询语言只读查询（如果使用CouchDB作为状态数据库）
+ 只读历史查询 - 查询某个关键字的账本历史，开启数据来源场景
+ 交易是由在chaincode中读取和写入的键值对的版本组成的
+ 交易包含每个背书peer的签名并将提交给ordering service
+ 交易是以blocks的形式排序的，从一个ordering service被“分发”到一个channel上的peers上
+ Peers针对背书政策验证交易并强制执行该政策
+ 在追加一个block之前，会执行版本检查，以确保从chaincode执行时间以来所读取的资产的状态没有被改变
+ 一旦交易被验证和提交，就具有不可更改性
+ 一个channel的账本包含一个配置block，该block定义了政策、访问控制列表和其他相关信息
+ 通道包含成员资格服务提供者实例，允许来自不同证书颁发机构的加密材料

请参阅账本主题，深入了解数据库、存储结构和“查询能力”。
#####Channels隐私#####
Hyperledger Fabric基于每个channel使用不可变的账本，以及可以操作和修改资产当前状态的chaincode（即更新键值对）。账本存在于channel的作用域中——它可以在整个网络上被共享（假设每个参与者都在一个公共channel上运行），或者它可以被私有化，只包括一组特定的参与者。

在后一种场景中，这些参与者将创建一个单独的channel，从而隔离（isolate/segregate）他们的交易和账本。为了解决想要完全透明和隐私之间的鸿沟的场景，chaincode只能安装在需要访问资产状态来执行读和写的peers上（换句话说，如果一个chaincode没有安装在一个peer上，那么它就不能正确地与账本进行交互）。

为了进一步混淆数据，chaincode内的值可以使用诸如AES之类的常用加密算法在向排序服务发送交易并将块附加到分类帐之前加密（部分或全部）。一旦已加密的数据被写入到账本中，它只能被拥有生成密文相关秘钥权限的用户解密。有关chaincode加密的进一步细节，请参见开发人员主题的chaincode部分。
#####安全&会员服务#####
Hyperledger Fabric底层是交易网络，其中所有参与者身份都是确定的。公钥基础设施用于生成与组织、网络组件、终端用户或客户端应用程序相关联的密码证书。因此，可以在更宽的网络和channel级别上控制和管理数据访问权限。Hyperledger Fabric的这种“许可”的设计理念，再加上渠道的存在和能力，有助于解决那些最关注隐私和机密性的场景。

请参阅会员服务提供者（MSP）主题，以更好地理解加密实现，以及在Hyperledger Fabric中使用的签名、验证、认证方法。
#####共识#####
在分布式账本技术中，共识最近成了单个方法中的一个特定算法的同义词。然而，共识不仅仅是简单地同意交易的顺序，而且这种理解上的差异，因其在整个交易流程中的基础性作用在Hyperledger Fabric中显得十分突出，从提案和背书，到排序、验证和提交。简而言之，共识定义为一组包含块的事务的正确性的全循环验证。

当block中交易的顺序和结果满足明确的策略准则检查时，将最终达成共识。这些检查和权衡发生在交易的整个生命周期中，并且包括使用背书政策来指定哪些特定成员必须认可某一特定交易类别，以及确保这些政策在system chaincode得到执行和支持。在提交之前，peers会使用这些system chaincodes确认有足够的背书存在，并且它们来自适当的实体。此外，在包含交易的任何blocks被追加到账本之前，当账本的当前状态是同意或者赞同时，将执行版本检查。此最后检查提供了防止双重开销操作和可能危及数据完整性的其他威胁，并允许对非静态变量执行函数。

除了大量的背书，有效性和版本检查，也有不间断的身份验证发生于交易流程的各个方向。访问控制列表是基于网络的层次结构（从ordering service到channels）实现的，并且当payloads作为交易提案在不同的价格组件间传递时，会被反复的签名、验证和认证。总而言之，共识不只是局限于一批交易的商定顺序，而是一个总体特征，它是在交易从提议到提交的过程中发生的正在进行的验证的副产品。

请查看共识的直观交易流程图（“六、架构参考”的“交易流程”章节）
####身份####
#####什么是身份?#####
区块链网络中的不同角色包括peers、orderers、client应用、管理员等等。每一个参与者——网络内外部的能够消费服务的活跃元素——都有一个封装在X.509数字证书中的数字身份。这些身份真的很重要，因为它们决定了角色在区块链网络中对资源和信息的确切权限。

数字身份还具有一些额外的属性，Fabric使用这些属性来确定权限，并且赋予了身份和相关属性联合一个特殊名称-主体（principal）。主体就像userIDs或groupIDs，但是更灵活一些，因为它们可以包括一个参与者身份的广泛属性，比如参与者的组织、组织单元、角色甚至参与者的特定身份。当我们谈论主体时，它们是决定其权限的属性。

对于一个可验证的身份，它必须来自一个可信的权威。会员服务提供者（MSP）就是Fabric中的实现。更具体地说，MSP是一个定义管理该组织的有效身份的规则的组件。Fabric中默认的MSP实现是使用X.509证书作为身份，采用传统的公钥基础设施（PKI）分层模型（稍后在PKI上更多）。
#####一个展示身份用法的简单场景#####
假定你逛一个超市要买一些商品。在出口处，你看见一个指示只接受Visa、MasterCard和AMEX卡的提示。如果你尝试使用其他卡来支付是不起作用的，即使该卡是真实有效并且确实账户上有钱。因为不接受这种类型的卡来支持。

![](images/identity.diagram.6.png)

有一个有效的信用卡是不够的-它也必须被商店认可！PKIs和MSPs以相同的方式协同工作——PKI提供身份列表，而MSP表示其中哪些是参与网络的给定组织的成员。

PKI认证中心和MSPs提供了类似的功能组合。PKI就像一个银行卡发行商——它提供了许多不同类型的可验证的身份。另一方面，MSP类似于由商店认可的银行卡发行商列表，确定哪些身份是商店支付网络的可信成员（参与者）。MSPS将可验证的身份转换成区块链网络的成员。

让我们进一步了解这些概念。
#####什么是PKIs?#####
公钥基础设施（PKI）是在网络中提供安全通信的互联网技术的集合。PKIs是PKI将S放入HTTPS中，如果你在Web浏览器上阅读此文档，你可能会使用PKI来确保它来自一个经过验证的源。

![](images/identity.diagram.7.png)

公钥基础设施（PKI）的要素。PKI由认证中心组成，它们向当事人发出数字证书（例如，服务使用者、服务提供者），然后使用它们在与环境交换的消息中对自己进行认证。CA证书吊销列表（CRL）构成证书不再有效的依据。很多原因会导致证书的撤销操作。例如，与证书相关联的加密私有材料已经被暴露。

区块链网络不仅仅是一个通信网络，它依赖于PKI标准来确保各种网络参与者之间的安全通信，并确保发布在区块链上的消息被正确地认证。因此，了解PKI的基础知识以及了解MSPs为什么如此重要是非常重要的。

这里是PKI的四个关键要素：

+ 数字证书
+ 公钥和私钥
+ 认证中心
+ 认证撤回列表

让我们快速地过一下这些PKI基础知识，如果你想知道更多的细节，维基百科是一个很好的地方。
#####数字证书#####
数字证书是包含与证书持有者相关的一组属性的文档。最常见的证书类型是符合X.509标准的证书，它允许在其结构中对一方的身份细节进行编码。

例如，在密歇根底特律的米切尔汽车制造部门的Mary Morris可能有一个具有C＝US、ST＝密歇根、L＝底特律、O＝米切尔汽车、OU=制造、CN＝Mary Morris /UID＝123456的数字属性的数字证书。玛丽的证书与她的政府身份证相似，它为Mary提供了可以用来证明相关身份的关键事实信息。X.509证书中还有很多其他属性，但现在我们只关注这些即可。

![](images/identity.diagram.8.png)

数字证书描述Mary Morris的相关信息。玛丽是证书的主题，高亮的主题文本显示了关于玛丽的关键事实。如你所见，该证书还保存了很多其他的信息。最重要的是，玛丽的公钥是在她的证书中分发的，而她的私有签名密钥不是。这个签名密钥必须保密。

重要的是，玛丽的所有属性可以用一种叫做密码学的数学技术（字面上的“secret writing”）来记录，这样篡改会使证书失效。密码学允许玛丽向他人证明她的身份，只要另一方信任证书颁发者，即证书颁发机构（CA）。只要CA安全地保存某些密码信息（意思是它私钥的隐私性），任何读取证书的人都可以确信玛丽的信息没有被篡改——它总是具有Mary Morris的那些特定属性。把玛丽的X.509证书看作是不可能改变的数字证书。
#####认证，公钥和私钥#####
认证和消息完整性是安全通信中的重要概念。身份验证要求交换消息的各方保证创建特定消息的身份。对于具有“完整性”的消息，意味着在传输过程中不能修改。例如，您可能希望确保与真实的Mary Morris通信，而不是冒充者。或者，如果玛丽给你发了一条消息，你可能想确保它在传输过程中没有被其他人篡改。

传统的认证机制依赖于数字签名，顾名思义，它允许一方对其消息进行数字签名。数字签名还提供了签名消息完整性的保证。

从技术上讲，数字签名机制要求每一方持有两个密码连接的密钥：一个广泛可用的公钥，充当认证锚，以及用于在消息上产生数字签名的私钥。数字签名消息的接收者可以通过检查所附签名在预期发送者的公钥下有效，来验证接收到的消息的来源和完整性。

私钥和相应公钥之间的唯一关系是使安全通信成为可能的密码魔术。密钥之间的唯一的数学关系使得私钥可以用于在仅对应的公钥可以匹配的消息上产生签名，并且仅在同一消息上产生签名。

![](images/identity.diagram.9.png)

在上述示例中，Mary使用她的私钥来签名消息。使用Mary公钥的任何人都可以验证该签名。
#####认证中心#####
如你所见，一个参与者或一个节点能够通过一个由系统信任的权威发布的数字身份来参与区块链网络。在最常见的情况下，数字身份（或简单身份）具有符合X.509标准并由证书颁发机构（CA）颁发的经密码验证的数字证书的形式。

CAs是Internet安全协议的一个常见部分，您可能已经听说过一些很流行的协议：Symantec（最初VISISIN）、GeoTrust、DigiCert、GoDaddy和Comodo等等。

![](images/identity.diagram.11.png)

证书颁发机构将证书分发给不同的参与者。这些证书由CA进行数字签名，并将参与者与参与者的公钥绑定在一起（并且可选地绑定属性的综合列表）绑定。因此，如果信任CA（并且知道它的公钥），它可以信任特定的参与者绑定到证书中包含的公钥，并通过验证在参与者证书上的CA签名来获取所包含的属性。

证书可以广泛传播，因为它们既不包括参与者的私钥也不包括CA的私钥。因此，它们可以用作信任来自不同参与者的消息的信任锚。

CAs也有证书，这使得他们广泛使用。这允许由给定CA颁发的身份验证的消费者通过检查证书只能由相应私钥持有者（CA）生成。

在区块链设置中，希望与网络交互的每个参与者都需要身份。在这个设置中，您可能会说，一个或多个CAs可以用来从数字的角度定义组织的成员。正是CA为一个组织的参与者提供了一个可验证的数字身份的基础。
######Root CAs,Intermediate CAs and Chains of Trust######
CAs有两种口味: Root CAs和Intermediate CAs。因为Root CAs（Symantec，Geotrust等）必须安全地向互联网用户分发数以亿计的证书，所以将这个过程推广到所谓的中间CAs是有意义的。这些中间的CAs有Root CA或其他中间机构颁发的证书，允许建立由链中的任何CA颁发的任何证书的“信任链”。这种追踪根CA的能力不仅允许CAS的功能扩展，同时还提供安全性——允许使用证书的组织有信心地使用中间CAs——它限制了Root CA的暴露，如果Root CA被破坏将危及整个信任链。如果中间CA被破坏，则破坏性相对较小。

![](images/identity.diagram.1.png)

信任链是建立在Root CA和一组中间CAs之间的，只要这些中间CAs的证书的颁发CA是Root CA本身或是与Root CA有信任链关系的CA即可。

中间CAs在跨多个组织颁发证书时提供了极大的灵活性，这在一个权限区块链系统（比如Fabric）中十分有用。例如，您将看到不同的组织可以使用不同的Root CAs，或者使用相同的Root CA但具有不同的中间CAs——这取决于不同的网络需求。
######Fabric CA######
因为CAs非常重要，所以Faby提供了一个内置的CA组件来允许你在区块链网络中创建CAs。这个称为Fabric CA的组件是一个私有Root CA提供者，能够管理具有X.509证书形式的Fabric参与者的数字身份。由于Fabruc CA是针对Root CA需要定制的CA，所以它本质上不能够在浏览器中提供SSL证书以用于一般/自动使用。但是，由于某些CA必须用于管理身份（即使在测试环境中），所以可以使用Fabric CA来提供和管理证书。使用公共/商业Root或中间CA来提供身份证明也是可能的，而且也是完全合适的。

如果你感兴趣，你可以在CA文档中获得大量信息。
#####证书撤销列表#####
证书撤销列表（CRL）很容易理解--它就是一个认证中心已知的撤销证书的列表。映射到商店的场景中，证书撤销列表就是被偷信用卡的统计列表。

当一个第三方想验证另一方的身份时，首先会去CRL检查该证书是否被撤销。作为校验方，也不是必须去检查CRL，但是如果不检查，他们就无法避免该风险。

![](images/identity.diagram.12.png)

使用CRL来检查某个证书是否还有效。如果冒名顶替者试图将受损的数字证书传递给验证方，则可以首先针对CA发布的CRL进行检查，以确保其未被列为不再有效。

需要注意，一个证书被撤销与一个证书过期有很大的差别。被撤销的证书没有过期，他们是完全有效的证书。更多关于CRLs的进一步信息，点击这里（https://hyperledger-fabric-ca.readthedocs.io/en/latest/users-guide.html#generating-a-crl-certificate-revocation-list）。

现在，您已经看到PKI如何通过信任链提供可验证的身份，下一步是看这些身份如何被用来表示区块链网络的可信成员。这就是会员服务提供商（MSP）发挥作用的地方——它标识了区块链网络中给定组织成员的参与者。
####Membership####
如果你已经读过了前面的文档，你就已经了解了PKI如何通过信任链提供可验证的身份。现在让我们看看这些身份如何被用来表示区块链网络的可信成员。

这就是会员服务提供商（MSP）发挥作用的地方--它标识哪些根CAs和中间CAs被信任来定义信任域的成员，例如一个组织，既可以通过列出成员的身份，也可以通过识别哪些CAS被授权发布有效的身份作为他们的成员，或-通常情况下-通过两者的结合。

MSP的作用远超于简单列出谁是网络参与者或者channel的成员。一个MSP可以识别一个参与者可能在MSP所代表的组织范围内扮演的特定角色（例如，管理员，或者作为子组织组的成员），并为在网络和channel的上下文中定义基础访问特权（例如，channel管理员、readers、writers）。

MSP的配置信息会通告给相应组织成员参与的所有信道（以channel MSP的形式）。除了channel MSP之外，peers、orderers和clients还维护本地MSP来认证channel上下文之外的成员消息，并定义特定组件（例如，谁能够在对等点上安装链码的能力）的权限。

此外，MSP可以允许标识已被撤销的身份列表——如前面所讨论的，但我们将讨论该处理是如何扩展到MSP。

我们很快就会讨论local和channel MSPs。现在，让简单看看MSPs的功能。
#####映射MSPs到组织#####
组织是一个管理的成员群体。这可以像跨国公司一样大，或者像花店一样小。组织最重要的概念是：他们在单个MSP下管理他们的成员。请注意，这与X.509证书中定义的组织概念不同，我们稍后将对此进行讨论。

组织和它的MSP之间的排他性关系使得在定义组织之后再定义MSP是明智的，在大多数策略配置中都是这种约定。例如，组织ORG1可能会有一个称为ORG1-MSP的MSP。在某些情况下，组织可能需要多个成员组——例如，channel用于在组织之间执行非常不同的业务功能时。在这些情况下，有多个MSP并相应地命名它们是有意义的，例如ORG2-MSP-NATIONAL和ORG2-MSP-GOVERNMENT，反映了不同的成员信任root。

![](images/membership.diagram.3.png)

一个组织的两种不同的MSP配置。第一种配置展示了MSP和组织之间最典型的关系--单个MSP定义了组织的成员列表。在第二种配置中，不同的MSPs被用来表示不同的组织群组，比如national、international和government。
######Organizational Units和MSPs######
一个组织通常被切分为多个组织单元（organizational units，OUs），每个组织单元都有特定的职责。例如，ORG1组织可能有ORG1-MANUFACTURING和ORG1-DISTRIBUTION OUs来反映这些单独的业务线。当CA颁发X.509证书时，证书中的OU字段指定身份所属的业务线。

稍后我们将了解OUs是如何帮助控制组织的各个部分的（即区块链网络的成员）。例如，只有来自OG1-MANUFACTURING OU的身份可能能够访问某个channel，而ORG1-DISTRIBUTION不能。

最后，虽然这是对OUs的轻微滥用，在财团中可以使用不同的组织来区分彼此。在这种情况下，不同的组织使用相同的Root CAs和中间CAs来建立信任链，但是分配OU字段来标识每个组织的成员。我们后面会看到如何配置MSPS来实现这一点。
#####Local and Channel MSPs#####
MSPs出现在区块链网络的两个地方：channel配置中（channel MSPs）和参与者的本地契约中（local MSP）。Local MSPs是为client（users)和nodes（peers和orderers）定义的。Node local MSPs定义了该node的许可（例如，谁是peer管理员）。Users的local MSPs允许用户侧在其交易中作为channel成员（例如在一个chaincode交易中）进行身份验证，或者作为特定角色的所有者进入系统（例如，在配置交易中作为ORG管理员）。

每一个node和user都必须拥有一个local MSP定义，因为它定义了谁在该级别具有管理或参与权限（peer管理员不一定是channel管理员，反之亦然）。

相比之下，channel MSP在channel级别定义管理和参与权利。参与channel的每个组织都必须为它定义一个MSP。Channel上的peers和orderers都将共享相同的channel MSPs的视图，因此将能够正确地验证channel参与者。这意味着，如果组织希望加入该channel，则需要将包含该组织成员的信任链的MSP包含在channel配置中。否则，来自该组织的身份的交易将被拒绝。

Local MSP和channel MSP之间的关键区别不是它们如何工作--两者都是讲身份转换为角色——而是它们的作用域。

![](images/membership.diagram.4.png)

Local和channel MSPs。每个peer的信任domain（例如，组织）是被peer的local MSP所定义的，例如，ORG1或ORG2。一个组织添加到一个channel是通过将组织的MSP添加到该channel的配置中来实现的。例如，上图的channel由ORG1和ORG2两者管理。类似的原则适用于网络、orderers和users，但为了简单起见，这里没有展示这些。

如上图所示，通过观察当区块链管理员安装和实例化智能合约时发生了什么，有助于理解local和channel MSP是如何使用的。

管理员B以RCA1发布的身份连接到peer并存储在他们的local MSP中。当B试图在peer上安装智能合约时，peer检查其local MSP，OGR1-MSP，以验证B的身份确实是ORG1的成员。成功的验证将允许安装命令成功完成。随后，B希望在channel上实例化智能合约。因为这是一个channel操作，channel上的所有组织都必须同意。因此，peer必须在成功提交此命令之前检查channel的MSPs。（还有其他操作会发生，但是我们暂且只关注上述操作。）

Local MSPs只定义在它们所应用的node或user的文件系统上。因此，在物理和逻辑上，每个node或user只有一个local MSP。然而，当channel MSP对channel中的所有nodes可用时，它们在channel配置中被逻辑地定义一次。然而，channel MSP也在channel中每个node的文件系统中被实例化，并通过协商保持同步。因此，尽管每个node的本地文件系统上都有每个channel MSP的副本，但逻辑上，channel MSP驻留在channel或网络上。 
#####MSP Levels#####
Channel和local MSPs之间的划分反映了组织管理本地资源的需求，例如一个peer或orderer node，以及它们的channel资源，例如在channel或网络级别工作的账本、智能合约和财团。将这些MSP视为不同的级别是有帮助的，更高层次上的MSP涉及到网络管理，而在较低级别的MSP处理私人资源管理的身份。MSPs在每一级管理中都是强制性的，它们必须为网络、channel、peer、orderer和users定义。

![](images/membership.diagram.2.png)

MSP级别。Peer和orderer的MSPs是local的，而channel（包括网络配置channel）的MSP在该channel的所有参与者之间共享。在这个图中，网络配置channel由ORG1管理，但是另一个应用channel可以由ORG1和ORG2管理。Peer是ORG2的成员，由ORG2管理，而ORG1管理图形的orderer。ORG1信任来自RCA1的身份，而ORG2信任来自RCA2的身份。请注意，这些是管理身份，反映谁可以管理这些组件。因此，当ORG1管理网络时，Org2.MSP确实存在于网络定义中。

+ **Network MSP**: 网络的配置定义了谁是该网络中的成员--通过定义参与者组织的MSP--以及这些成员中的哪些成员被授权执行管理任务（例如，创建channel）。
+ **Channel MSP**: 对于一个channel来说，分别维护其成员的MSP是重要的。Channel在特定的一组组织之间提供私人通信，而这些组织又具有对其的管理控制。在该channel的MSP上下文中解释的channel策略定义了谁有能力参与信道上的某些动作，例如，添加组织或实例化chaincodes。注意，管理channel的权限与管理网络配置channel（或任何其他channel）的能力之间没有必然的关系。行政权存在于被管理的范围内（除非规则被写入否则参见下面的角色属性的讨论）。
+ **Peer MSP**: 该local MSP定义在每一个peer的文件系统上并且每一个peer只有一个MSP实例。从概念上讲，它执行与channel MSPs完全相同的功能，其限制仅适用于定义它的peer。使用peer的local MSP来评估授权的动作的一个示例是在peer上安装chaincode。
+ **Orderer MSP**: 类似于一个peer MSP，一个orderer local MSP也是定义在node的文件系统上并且只适用于该node。类似于peer nodes，orderers也只被单个组织所拥有，因此它有一个单独的MSP来列出信任的参与者或nodes。
#####Msp Structure#####
到目前为止，您已经看到MSP中最重要的元素是Root或中间CAs的规范，它们用于在各自的组织中建立一个参与者或节点的成员关系。然而，有更多的元素与这两个元素一起使用来辅助会员功能。

![](images/membership.diagram.5.png)

上述图表展示了如何在一个本地文件系统中存储一个local MSP。虽然channel MSPs在物理上不是严格以这种方式构建的，但是这样来思考也是一种很有帮助的方式。

如你所见，一个MSP有9个元素。将这些元素对应到一个目录结构来理解是最简单的，MSP的名称是root文件夹，每一个子文件夹代表MSP配置中的不同元素。

让我们进一步学习这些文件夹并理解他们为什么这么重要。

+ **Root CAs**: 该文件夹包含由此MSP中所有组织所信任的root CAs的自签名X.509证书的列表。在这个MSP文件夹中必须至少有一个root CA x.509证书。

	这是最重要的文件夹，因为它标识了CAs。只有通过这些CAs，所有其他证书才能被衍生并被认为是相应组织的成员。
+ **Intermediate CAs**: 该文件夹包含了本组织所信任的中间CAs的X.509证书列表。每一个证书必须被MSP中的一个Root CAs或者中间CAs签名，因为中间CAs发行的CA链最终会指向信任的Root CA。

	中间CA可以代表组织的不同细分（如ORG1的ORG1-MANUFACTURING和OGR1-DISTRIBUTION），或者组织本身（如果商业CA被用于组织的身份管理，情况可能是这样）。在后一种情况下，中间CAs可以用来表示组织细分。在这里，您可以找到更多关于MSP配置的最佳实践。请注意，可能存在一个没有中间CA的功能网络，在这种情况下，该文件夹将是空的。

	类似于Root CA文件夹，该文件夹定义了用于发行认证组织成员证书的CAs。
+ **Organizational Units (OUs)**: 这些展示在$FABRIC_CFG_PATH/msp/config.yaml文件中，并且包含组织单元的列表，这些组织单元的成员被该MSP认定为组织的组成部分。当你希望将组织的成员限定为持有身份（由MSP指定的CAs中的一个签名）并具有特定OU信息的成员时，这尤其有用。 

	指定OUs是可选的。如果没指定OUs，所有的身份都是MSP的组成部分--被Root CA和中间CA文件夹鉴定--并且被作为组织的成员。
+ **Administrators**: 该文件夹包含一个身份列表，身份列表定义了哪些参与者具有管理该组织的角色。按照标准的MSP，列表中应该有一个或多个X.509证书。

	值得注意的是，仅仅因为一个演员有一个管理员的角色，这并不意味着他们可以管理特定的资源！给定的身份对于管理系统的实际权力由管理系统资源的策略决定。例如，一个channel策略可能指定OGR1-MANUFACTURING管理员有权向该channel添加新的组织，而OG1-DISTRIBUTION管理员没有这样的权限。

	即使X.509证书具有一个角色属性（例如，指定一个参与者是一个管理员），但它指的是它在组织中的角色，而不是区块链网络。这与OU属性的目的类似，OU属性--如果它已被定义--指的是组织中的一个参与者的定位。

	如果一个channel的策略已被写定，以允许来自组织（或特定组织）的任何管理员允许执行某些channel功能（例如实例化链码），则可以使用角色属性来授予channel级的管理权限。通过这种方式，组织角色可以赋予网络角色。
+ **Revoked Certificates**: 如果一个参与者的身份被撤销，该身份的识别信息--不是身份自身--被存放在此文件夹。对于基于X.509的身份，这些标识符是称为主题密钥标识符（SKI）和权限访问标识符（AKI）的字符串对，每当X.509证书被用于确保证书没有被撤销时，都会对其进行检查。

	此列表在概念上与CA证书撤销列表（CRL）相同，但也涉及撤销组织的成员资格。因此，MSP、local或channel的管理员可以通过对CA的更新CRL进行广告，从而撤销来自组织的参与者或node。这个“list of lists”是可选的。它只会因为证书被撤销而存在。
+ **Node Identity**: 该文件夹包含node的身份，即，与密钥存储库的内容相结合的密码材料将允许节点在发送到其channel和网络的其他参与者的消息中进行身份验证。对于基于X.509的身份，此文件夹包含X.509证书。这是在交易发起响应中peer放置的证书，例如，指示peer已经认可它，随后可以在验证时期对所得到的交易的背书策略进行检查。

	此文件夹对于local MSPs是必须的，并且node必须只有一个X.509证书。它不用于channel MSPs。
+ **KeyStore for Private Key**: 该文件夹是针对peer或orderer节点（或客户端的local MSP）的local MSP定义的，并包含节点的签名密钥。该密钥与节点标识文件夹中包含的节点的身份进行加密匹配，并用于签署数据--例如，签署交易发起响应--作为背书阶段的一部分。

	此文件夹对于local MSP是必需的，并且必须包含一个私钥。显然，对该文件夹的访问必须仅限于对该peer具有管理权限的身份。

	一个channel MSPs的配置不包含此文件夹，因为channel MSPs目的只在于提高身份校验功能，而不提供签名能力。
+ **TLS Root CA**: 该文件夹包含一个由本组织为TLS通信所信任的Root CAs的自签名X.509证书的列表。TLS通信的一个例子是当一个peer需要连接到一个orderer，以便它可以接收分类帐更新。

	MSP TLS信息涉及网络内的节点-peers和orderers，换句话说，不是消费网络的应用和管理机制。

	在该文件夹至少有一个TLS Root CA X.509证书。
+ **TLS Intermediate CA**: 该文件夹包含一个由本组织为TLS通信所信任的中间CAs列表。当商业CAs用于组织的TLS证书时，该文件夹特别有用。类似于成员中介CAS，指定中介TLS CAs是可选的。

	关于TLS的更多详细信息，请点击这里。（http://hyperledger-fabric.readthedocs.io/en/release-1.1/enable_tls.html）

如果你已经阅读了这个文档以及我们的身份文档，你应该很好地掌握身份和会员是如何在Hyperledger Fabric中工作的。您已经看到了如何使用PKI和MSPs来标识区块链网络中的参与者协作。除了了解了MSPs的物理和逻辑结构外，您还了解了证书、公钥/私钥和roots of trust work是如何工作的。
####Peers####
一个区块链网络主要由一组peer nodes组成。Peers是网络的一个基础元素，因为它们持有账本和智能合约。请记住，账本不可改变地记录由智能合约生成的所有交易。智能合约和账本用于分别封装网络中的共享处理和共享信息。Peer的这些方面使它们成为理解Hyperledger Fabric网络的突破口。

区块链网络的其他元素当然也很重要：账本和智能合约，orderers，policies，channels，applications，organizations，identities和会员，你可以在分别介绍他们的章节中获得更多信息。本章关注的是peers以及在Hyperledger Fabric区块链网络中peers与那些其他元素之间的关系。

![](images/peers.diagram.1.png)

一个区块链网络是有peer nodes构成的，每一个peer node都可以持有账本和智能合约的副本。在这个示例中，网络N是由peers P1，P2和P3组成的。P1，P2和P3每一个单独维护他们自己的账本L1的实例。P1，P2和P3使用chaincode S1来访问账本L1的副本。

Peers可以被创建、启动、停止、重新配置甚至是删除。它们暴露了一些APIs，使得管理员和应用实现与服务的交互。我们将在本章后续部分深入探讨这些服务。
#####A word on terminology#####
Hyperledger Fabric采用一种技术概念来实现智能合约，它称为chaincode——简单地说是一种访问账本的代码，用支持的一种编程语言编写。在本主题中，我们通常使用术语chaincode，但是如果你更习惯智能合约这个术语也是可以的。智能合约和chaincode是一回事！
#####Ledgers和Chaincode#####
让我们进一步看看一个peer。我们可以看到，是peer持有账本和chaincode。更准确地说，peer实际上持有账本的实例和chaincode的实例。注意，在Fabric网络中这是有意提供的冗余--它避免了单点故障。我们将在本主题后续部分了解更多关于区块链网络的分布式和分散特性。

![](images/peers.diagram.2.png)

一个peer持有账本的实例和chaincode的实例。在这个示例中，P1持有账本实例L1和chaincode实例S1。在一个单独的peer上，可以持有多个账本和chaincode实例。

由于peer持有账本和chaincode，所以当应用和管理员要访问这些资源时，必须与peer交互。这就是为什么peers被当做Hyperledger Fabric区块链网络中的最最基础的模块。当一个peer被初次创建时，既没有账本也没有chaincode。后面我们将学习账本是如何在peer上创建的以及chaincode是如何在peer上被安装的。
######Multiple Ledgers######
一个peer可以持有不止一个账本，这是很有用的设计，因为这样实现了一个灵活的系统设计。最简单的peer配置是只有单个账本，但是如果需要，一个peer持有两个或多个账本也是合理的。

![](images/peers.diagram.3.png)

一个peer持有多个账本。Peers持有一个或多个账本，并且每一个账本有0或多个chaincode应用在其上。在这个示例中，我们可以看到peer P1持有账本L1和L2。账本L1通过使用chaincode S1来访问。账本L2可以使用chaincode S1和S2来访问。

虽然一个peer持有一个账本实例而不持有任何访问该账本的chaincode是可能的，但是以这种方式来配置peers是十分罕见的。绝大多数的peers会至少持有一个chaincode，用于查询或更新该peer的账本实例。值得一提的是，无论用户是否安装了外部应用程序所需使用的chaincode，peers总是存在的特殊system chaincodes可以使用。这些在本主题中没有详细讨论。
######Multiple Chaincodes######
一个peer拥有的账本数量和访问账本的chaincode的数量之间没有应该固定的关系。一个peer可以有多个chaincodes和多个账本。

![](images/peers.diagram.4.png)

一个peer持有多个chaincodes的示例。每一个账本可以由多个chaincodes来访问。在这个示例中，我们可以看到peer P1持有账本L1和L2。L1通过chaincodes S1和S2来访问；L2通过S3和S1来访问。也就是说，S1既可以访问L1也可以访问L2。

在稍后章节，我们会学习当一个peer持有多个账本或多个chaincodes时，为什么channels的概念在Hyperledger Fabric中是如此的重要。
#####Applications和Peers#####
现在我们将展示应用程序如何与peers交互来访问账本。账本查询交互涉及应用程序和peer之间的简单的三步对话；账本更新交互涉及得较多，需要两个额外的步骤。我们已经简化了这些步骤，以帮助您开始使用Hyperledger Fabric，但不用担心——最重要的是要了解在application-peer交互过程中，对账本查询和账本更新交易类型的差异处理。

当应用程序需要访问账本和chaincodes时，他们通常是连接到对应的peers上来实现。Hyperledger Fabric Software Development Kit（SDK）为开发者简化了这些操作--它的APIs帮助应用程序连接到peers，调用chaincodes来生成交易，向网络提交交易（这些交易会被排序和记录到分布式账本）并且当处理完成时接收相应事件。

通过一个peer连接，应用程序可以执行chaincodes来查询或更新账本。账本查询交易的结果是立即返回的，但账本更新涉及一些复杂的交互，这些交互发生在应用程序、peers和orderers之间。让我们看的深入一些。

![](images/peers.diagram.6.png)

Peers，结合orderers，确保每一个peer之上的账本是最新的。在这个示例中，应用程序A连接到P1并调用chaincode S1来查询或更新账本L1。P1调用S1来生成建议响应，该建议响应包含查询结果或是建议的账本更新操作。应用程序A接收到建议响应，对于查询本次处理结束。对于更新操作，应用程序A根据所有的响应结果构建一个交易，并将其发送给O1来进行排序。O1从整个网络收集交易信息并处理到blocks中，并将结果分配给所有的peers，包括P1。P1在将其应用到L1之前会验证该笔交易。一旦L1被更新，P1会生成一个事件来标识完成，并发送给应用程序A。

一个peer能立即返回查询结果给应用程序，是因为查询所需的所有条件都存储在该peer的本地账本副本中。Peers不需要与其他peers商榷就可以返回查询结果给应用程序。应用程序可以连接到一个或多个peers来发布查询--例如在多个peers之间证实一个结果或者如果怀疑信息过期时从另一个peer获取最新的结果。在上面图表中，你可以看到账本查询是一个简单的三步处理。

更新事务以与查询事务相同的方式启动，但有两个额外的步骤。虽然账本更新应用程序也连接到peers来调用一个chaincode，但是不同于账本查询应用程序，一个单独的peer在此时不能执行账本更新，因为其他peers必须先认同本次改变--一个叫做共识的过程。因此，peers返回应用程序一个建议更新的结果--该peer会服从其他peers的事先协议（发生较早的交易）。第一个额外步骤（步骤4）--要求应用程序向整个peers网络发送一组适当的建议更新，作为对各自账本的承诺的交易。这是由应用程序使用一个orderer将交易打包成blocks，并将它们分发给peers的整个网络来实现的，在它们被应用到每个peer的本地账本副本之前，可以对它们进行验证。由于整个排序处理需要一些时间完成（秒级），所以应用程序被异步通知，如步骤五所示。

在本章稍后部分，你将学习该排序处理的更多详细特性。
#####Peers和Channels#####
虽然本章是关于peers的而不是关于channels的，但是花一定时间来理解peers是如何通过channels与其他peers，应用程序交互是值得的--区块链网络中的一组组件可以私下通信和处理的机制。

这些组件通常是peer nodes，orderer nodes和应用程序，并且通过加入一个channel一起来共同共享和管理该channel的账本的完全相同副本。从概念上讲，你可以认为channels和朋友组相似（虽然一个channel的成员不需要是朋友！）一个人可能有好几个朋友组，每个小组都有他们一起做的活动。这些群体可能是完全分离的（一组工作上朋友，一组爱好相同的朋友），或者它们之间可以有交叉。然而，每一个群体都是自己的实体，具有一种“规则”。

![](images/peers.diagram.5.png)

Channels允许一个特定的peers和应用程序集合在区块链网络中彼此通信。在这个示例中，应用程序A可以使用channel C直接与peers P1和P2通信。你可以将channel看作是特定应用程序和peers之间通信的途径。（为了简单起见，在这个图中没有显示orderers，但orderers在功能网络中是必须存在的。）

我们看到，channels与peers存在的方式不一样--将一个channel理解为物理peers集合组成的逻辑结构更为恰当。理解这一点是至关重要的--peers提供访问和管理channels的控制点。
#####Peers和Organizations#####
现在，你理解了peers以及peers与账本、chaincodes和channels之间的关系，那么你就能看透多个组织是如何集合到一起组成一个区块链网络了。

区块链网络被多个组织而并非单个组织所管理。Peers是如何构建这种分布式网络的核心，因为它们是由这些组织拥有的，并且是这些组织的网络连接点。

![](images/peers.diagram.8.png)

具有多个组织的区块链网络中的Peers。区块链网络是由不同组织拥有和贡献的peers构成的。在这个示例中，我们看见四个组织贡献了八个peers来构成网络。Channel C连接网络N中的五个peers--P1，P3，P5，P7和P8。这些组织拥有的其他peers没有被加入到该channel，但是这些peers通常被加入到至少一个其他的channel中。已经由特定组织开发的应用程序将连接到它们自己的组织的peers。同样，为了简单起见，在这个图中没有展示orderer node。

能看到一个区块链网络的形成过程中发生了什么是十分重要的。网络是由多个组织构成和管理的，这些组织也为网络提供资源。Peers是我们在本主题中讨论的资源，但是组织提供的资源不仅仅是peers。这里有一个原则--如果没有组织将各自的资源贡献给集体网络，网络就不复存在。此外，网络随着这些协作组织提供的资源而增长和缩小（即提供的资源越多，网络越大，反之亦然）。

你可以发现，（除了ordering service）没有集中式的资源--在上述示例中，如果组织不贡献他们的peers，则网络N就不存在了。这反映了一个事实，除非并且只有当组织贡献资源来构成网络，否则网络在任何意义上都没有存在的价值。此外，网络不依赖于任何独立的组织--只要有一个组织存在，则网络就存在，无论别的组织是来还是走。这是网络分散的核心所在。

如上述示例所示，不同组织中的应用程序可以相同也可以不同。这完全取决于一个组织的应用程序如何处理他们peers上的账本副本。这意味着应用和呈现逻辑可以从组织到组织各不相同，即使它们各自的peers拥有完全相同的账本数据。

应用程序要么连接到组织中的peers，要么连接到另一个组织中的peers，这取决于所需的账本交互的性质。对于“账本-查询”交互，应用程序通常连接到它们自己的组织的peers。对于“账本-更新”交互，我们稍后会看到为什么应用程序需要连接到每个组织中的peers，这些组织需要支持账本更新。
#####Peers和Identity#####
现在，你已经看到了不同组织的peers是如何集合在一起并构成一个区块链网络的，因此花点时间来理解peers是如何被管理员分配给组织是值得的。

Peers都会被分配一个身份，这个身份是从一个特定证书颁发机构指定的数字证书。你可以在本指南其他章节获取更多关于X.509数字证书如何工作的信息，但现在将数字证书理解为一个ID卡，它提供了大量关于一个peer的可验证信息。网络中的每个peer都由管理员从其拥有的组织中指派数字证书。

![](images/peers.diagram.9.png)

当一个peer连接到一个channel，它的数字证书通过一个channel MSP来验证它自己的组织。在这个示例中，P1和P2有CA1发行的身份。Channel C的决策来自于其channel配置中的政策：来自CA1的身份应当使用ORG1.MSP与Org1联系在一起。类似的，P3和P4被ORG2.MSP认定为Org2的组成部分。

当一个peer使用一个channel连接到区块链网络时，该channel配置中的政策会使用该peer的身份来确定其权限。身份到组织的映射是由一个组件提供的，该组件被称为MSP--它确定一个peer如何分配给特定组织中的特定角色，并相应地获得对区块链资源的适当访问权限。此外，一个peer只能被一个组织拥有，并且只能与单个MSP关联。我们将在本章稍后部分进一步学习peer的访问控制，并且在该指南的别处有一个完整的章节专门介绍MSPs和访问控制政策。但是目前，将MSP理解为在区块链网络中提供一个独立身份和一个特定组织角色直接的联系即可。

稍稍扯远一点，peers以及与区块链网络交互的所有事物都从他们的数字证书和MSP中获取他们的组织身份。Peers、应用程序、终端用户、管理员、orderers如果想与区块链网络交互，就必须具有身份和关联的MSP。我们使用一个身份给每个与区块链交互的实体命名--一个主体（a principal）。在本指南中，你可以学到更多关于主体和组织的知识，但是现在你知道的足够多，可以继续学习peers了。

最后，请注意，peer的物理存储地点不是很重要--它可能在云里，可能被一个数据中心的一个组织所拥有，或者存在于一个本地机器--是他关联的身份标识了它被一个特定组织所拥有。在上述示例中，P3可以存储在Org1的数据中心，但是只要他关联的数字证书是CA2发行的，那么它就是属于Org2的。
#####Peers和Orderers#####
我们已经看到，peers构成了一个区块链网络，托管账本和chaincodes合同，可以通过peer-connected的应用程序查询和更新。然而，应用程序和peers彼此交互以确保每个peer的账本保持一致的机制是由称为orderers的特殊nodes所提供的，这些节点是我们现在要学习的知识。

一笔更新交易与一笔查询交易十分不同，因为单个peer靠它自己无法更新账本--它需要网络中其他peers的同意。在账本更新操作被应用到本地账本之前，一个peer需要网络中的其他peers来批准本次更新。这种处理被称为共识--与查询相比会花费更长时间。但当所有所需peers批准了该笔交易，该交易会被提交到账本，peers也会通知连接它们的应用程序账本已经被更新了。在本章，你会学到peers和orderers如何管理共识处理的详细信息。

具体地说，想要更新账本的应用程序处理过程涉及3个阶段，这三个阶段确保了区块链网络中的所有peers保持它们的账本彼此一致。在第一阶段，应用程序与背书peers的子集一起工作，每一个背书peer都为应用程序提供提议账本更新的背书，但不会将建议的更新应用到账本的副本。在第二阶段，这些分散的背书作为交易被收集在一起并打包成blocks。在最后阶段，这些blocks被分发回每个peer，在peer上每笔交易在被应用到该peer的账本副本之前都会被验证。

你会发现，orderer节点是这个过程的核心--因此，让我们更详细地研究应用程序和peers如何使用orderers来生成可以持续应用于分布式、复制的账本的账本更新。
#####阶段1:提议#####
交易工作流的阶段1涉及应用程序和一个peers集合之间的交互--它不涉及orderers。阶段1仅关注一个应用程序请求不同组织的背书peers同意所提议的chaincode调用的结果。

为了启动阶段1，应用程序生成一个交易提议，并发送给所需的一组peers进行背书操作。然后每个peer独立地使用交易提议执行chaincode来生成交易提议响应。它不将此更新应用于账本，而是peer签名并返回给应用程序。一旦应用程序收到足够数量的签名提议响应，交易流程的第一阶段就完成了。让我们更详细地查看这个阶段。

![](images/peers.diagram.10.png)

交易提议由peers独立执行，并返回背书提议响应。在这个示例中，应用程序A1生成交易T1提议P，该提议被发送给channel C的peer P1和peer P2。P1使用交易T1提议P执行S1生成了交易T1响应R1,并使用E1进行背书。P2独立地使用交易T1提议P执行S1生成交易T1响应R2并使用E2进行背书。应用程序A1接收到交易T1的两个背书响应，并命名为E1和E2。

一开始，应用程序会选取一组peers来生成一组提议账本更新。应用程序会选择那些peers？好吧，这取决于背书政策（defined for a chaincode），背书政策定义了在提议账本被网络接受之前需要进行背书操作的组织集合。从字面上看，这意味着达成共识--每一个重要的组织都必须在提议账本被任何peers的账本接受之前，对提议的账本变更进行背书。

一个peer通过添加它的数字签名来背书提议响应，并使用私钥来签名整个载体（payload）。该背书随后可以被用来证明该组织的peer生成了一个特定的响应。在我们的示例中，如果peer P1被组织Org1所拥有，背书E1会绑定一个数字证据“账本L1上的交易T1响应R1是由Org1的peer P1提供的”。

当应用程序从足够多的peers接收到签名提议响应，阶段1就结束了。我们注意到，不同的peers可以返回不同的结果，因此对于同一个交易提议，应用程序接收到的交易响应也是不一致的。简单地说，结果是在不同的状态下在不同的对等体上产生不同的结果，在这种情况下，应用程序可以简单地请求一个更新的建议响应。不太可能，但更严重的是，chaincode的不确定性导致了结果的差异性。不确定性是chaincodes和账本的敌人，并且如果发生了则表明提议交易出了严重的问题，因为不一致的结果很显然不能被应用到账本。一个独立的peer不可能知道它们的交易结果是非确定性的--在不确定被检测到之前，交易响应就会被收集并比较。（严格地说，即使这样也是不够的，但是我们将这个讨论推迟到交易主题，其中非确定性被详细讨论。）

在阶段1结束时，应用程序如果希望，可以自由地丢弃不一致的交易响应，尽早地、有效地终止交易工作流。稍后我们会看到，如果应用程序试图使用一组不一致的交易响应来更新账本，该操作会被拒绝。
#####阶段2:打包#####
交易工作流的第二个阶段是打包阶段。Orderer是该处理的核心--它接收包含多个应用程序提供的背书交易提议响应的交易信息。它相对于其他交易将每一个交易排序，并将批量交易打包成blocks，以便分发回连接到orderer的所有peers，包括最初的背书peers。

![](images/peers.diagram.11.png)

一个orderer节点的首要角色是打包提议账本更新。在这个示例中，应用程序A1发送一个被E1和E2背书的交易T1到orderer O1。并行地，应用程序A2发送被E1背书的交易T2到orderer O1。O1将来自应用程序A1的交易T1和来自应用程序A2的交易T2以及来自网络中其他应用程序的其他交易打包到block B2。在B2中我们可以看到，交易顺序是T1，T2，T3，T4，T6，T5--可能与这些交易到达该orderer节点的顺序不一致！（该示例展示了一个非常简化的orderer配置。）

一个orderer从网络中特定的channel上的许多不同应用程序接收所提议的账本更新。它的工作是将这些提议更新安排成一个定义良好的序列，并将它们打包成blocks便于后续的分发。这些blocks将成为区块链的blocks！一旦orderer生成了所需大小的block，或者在经过了最大时间之后，block将被发送到特定channel上连接到它的所有peers。我们将在阶段3看到这个块是如何被处理的。

值得注意的是，一个block中的交易顺序不一定与交易到达orderer的顺序相同。交易可以按任意顺序打包成一个block，并且这个序列会成为执行顺序。重要的是这里要有一个严格的顺序，至于顺序是什么就不那么重要了。

Blocks内交易的严格排序使得Hyperledger Fabric与其他一些区块链略有不同，在有些区块链中相同的交易可以打包成多个不同的blocks。在Hyperledger Fabric中，这是不可能发生的--因为一旦交易已被写入一个块，它在账本中的位置是不可改变的，因此，由一个orderers集合生成的blocks被认为是最终的。Hyperledger Fabric的最终确定意味着一种叫做账本fork的灾难性事件不可能发生。一旦交易被封装进一个block，就不能在将来的某个时间点为该交易重写历史记录。

我们还可以看到，尽管peers持有账本和chaincodes，但orderers肯定不会这样做。每一个到达orderer的交易都被机械地打包到一个block中--orderer对交易的价值不作判断，只是简单地打包。这是Hyperledger Fabric的一个重要行为--所有交易都按严格的顺序编排--交易从不会被丢弃或取消优先级。

在阶段2结束时，我们看到，orderers负责简单但是至关重要的处理，处理涉及收集提议交易更新，对他们排序，将他们打包到blocks并准备分发。
#####阶段3:验证#####
交易工作流的最后阶段涉及从orderer到peers的blocks的distribution和subsequent验证，blocks可以在peers上于账本。具体地说，在每个peer上，一个block内的每一笔交易都被验证，以确保它被应用到账本之前已经被所有的相关组织取得共识。保留失败的交易用于审计，但不会被应用到账本。

![](images/peers.diagram.12.png)

Orderer节点的第二个角色是将blocks分配给peers。在这个示例中，orderer O1将block B2分发给peer P1和peer P2。Peer P1处理block B2，最终将一个新的block追加到P1的账本L1。并行地，peer P2处理block B2，最终将一个新的block追加到P2的账本L1。一旦处理完成，账本L1就实现了在peers P1和P2上的一致更新，并且任何一个都可以通知连接的应用程序交易已经被处理完成。

Orderer将blocks分发给所有连接到orderer上的peers标识着阶段3的开始。Peers都通过channels连接到orderers上，因此，当一个新的block被生成时，所有连接到orderer的peers都会获取一份新block的副本。每个peer都会独立地处理该block，但是channel上的每一个peer处理该block的方式都是一样的。通过这种方式，账本可以实现一致性更新。需要注意的是，并不是所有的peer都需要连接到一个orderer上--peers可以使用八卦协议（gossip protocol）从其他peers获取blocks，这些peers也可以独立地处理这些blocks。这个问题我们后面再讨论。

在接收到一个block后，peer将按其出现在block中的顺序依次处理每笔交易。对于每笔交易，每个peer将根据生成交易的chaincode的背书策略验证该笔交易已经被所需的组织达成共识。例如，一些交易可能只需要由单个组织认可，而另一些交易在被认为有效之前需要多个背书。这个验证过程验证了所有相关组织都产生了相同的结果。

如果一笔交易被正确的背书，peer则会尝试将该笔交易追加到账本。要完成这个操作，peer必须执行账本一致性校验来验证账本的当前状态与更新完成时账本状态是否一致。即使交易被完全认可，这也未必总是可行的。例如，另一个交易可能已经更新了账本中的相同资产，从而使得交易更新不再有效，因此不能再被应用。在这种情况下，每个peer的账本副本因为遵循相同的验证规则而保证网络上的一致。

当一个peer在成功验证了每笔独立的交易之后，会更新账本。失败的交易不会被应用到账本，但它们会为了审计目的而保留，如同成功的交易一样。这意味着，除了block中每笔交易的有效或无效指示符外，peer blocks几乎与从orderer接收的blocks完全相同。

我们还注意到，阶段3不需要运行着的chaincodes--这只是在阶段1完成的，这很重要。这意味着chaincodes只需要在认可节点上可用，而不必在整个区块链网络中可用。这非常有用，因为它实现了chaincode的逻辑对背书组织是保密的。这与chaincodes的输出（交易提议响应）相反，这些输出被共享到channel中的每个peer，不管它们是否支持该交易的背书。背书peers的这种特殊设计是为了实现可扩展性。

最后，每当一个block被提交到peer的账本时，peer会生成一个对应的事件。Block事件包括完整的block内容，而block交易事件仅包括摘要信息，例如block中的每笔交易是有效还是无效。Chaincode执行所产生的chaincode事件也可以在此时发布。应用程序可以注册这些事件类型，以便在发生事件时可以通知它们。这些通知标识交易工作流第三个阶段（也是最后一个节点）的结束。

总之，阶段3见证了那些由orderer生成的blocks被一致性应用到账本。Blocks中交易的严格顺序使得每个peer能够验证该笔交易更新是否被一致性地应用到了整个区块链网络中。
#####Orderers和Consensus#####
整个交易工作流的处理被称为共识，因为所有的peers最终就交易的顺序和内容达成了一致，该处理发生在orderers上。共识是一个多步骤的过程，应用程序只在过程完成时被通知账本更新--这可能在不同的时间点发生在不同的peers上。

我们将在后面的orderer章节讨论的更加详细，但是现在，将orderers视为收集和分发来自peers应用程序的提议账本更新的节点，以验证和包括在账本上。

就是这样！现在我们完成了peers和其他与Hyperledger Fabric相关的组件的学习。我们已经看到，在多种途径下，peers都是最最基础的元素--它们形成网络、主机chaincodes和账本，处理交易提议和响应，并通过不断地向其应用交易更新来保持账本的最新状态。
####Ledger####
账本是所有状态交易的有序的、防篡改的记录。状态交易是参与方提交的chaincode调用的结果（“交易”）。每笔交易都会产生一组资产键值对，这些资产键值对作为创建、更新或删除操作被提交。

账本由区块链（“chain”）组成的，以存储blocks中不可变的、有序的记录，以及一个维护当前状态的状态数据库。每个channel都有一个账本。每个peer维护其所属channel的账本副本。
#####Chain#####
链（“chain”）是一个交易日志，以hash-linked的blocks作为结构，在链中每一个block包含N笔交易的有序集合。Block头包含一个该block的交易的哈希值，以及上一个block头的哈希值。以这种方式，账本上的所有交易被有序的加密链接在一起。换句话说，除非破坏哈希链接，否则想篡改账本数据是不可能的。最新block的哈希值是根据之前所有发生的交易计算出来的，从而确保所有peers处于一致和可信状态。

链存储于peer的文件系统中（无论是本地存储还是附加存储），有效地支持区块链工作负载的只能追加的特性。
#####State Database#####
账本的当前状态数据是根据链中包含所有历史交易日志计算得出的。由于当前状态表示channel已知的所有最新键值，因此有时称为“世界状态”。

链码调用针对当前状态数据执行交易。为了使这些chaincode交互高效执行，所有keys的最新值都存储在状态数据库中。状态数据库只是进入链的交易日志的一个索引视图，因此它可以在任何时候从链中重新生成。在接受事务之前，状态数据库将在peer启动时自动恢复（或如果需要的话生成）。

状态数据库的选项包括LevelDB和CouchDB。LevelDB是内嵌于peer的默认状态数据库，用于以键值对的格式处理和存储chaincode数据。CouchDB是一个可选择的额外的状态数据库，当你的chaincode数据设置为JSON格式是提供了额外的查询支持，支持JSON内容的丰富的查询。
#####交易流#####
在高层次上，交易流由应用客户端发送给特定的背书peers的交易提议组成。背书peers验证客户端签名，并执行chaincode功能来模拟交易。输出是chaincode结果，一组键值版本在链式代码（读取集）中读取，以及在链式代码（写集）中写入的一组键/值。提议响应连同背书签名一起发送回客户端。

客户端将背书组装成交易载体并将其广播到一个ordering服务。该ordering服务将有序交易作为blocks传递到channel上的所有peers。

在提交之前，peers会验证该交易。首先，他们会检查背书策略来确认所有分配到的特定peers都对该结果签名了，并且他们会针对交易载体认证签名。

其次，peers会针对交易读集合执行一个版本检查，来确认确保数据完整性并防止双重支出等威胁。Hyperledger Fabric有并发控制，从而交易（由endorsers）并行执行以提高吞吐量，并且在提交之后，（由所有peers）验证每笔交易没有被其他交易修改。换言之，它确保在chaincode执行期间读取的数据在执行（认可）时间之后没有改变，因此执行结果仍然是有效的，并且可以提交到账本状态数据库。如果所读取的数据已被另一交易更改，则该block中的交易被标记为无效，并且不应用到账本状态数据库。客户端应用程序被告警，并且可以处理错误或重试。

请参阅交易流、读写集语义和CoucDB作为状态数据库主题，以便深入研究交易结构、并发控制和状态数据库。

###三、教程###
我们提供了一些教程来帮助你学习Hyperledger Fabric。第一个教程是面向Hyperledger Fabric应用开发者，编写你的第一个应用程序。该教程通过使用Hyperledger Fabric Node SDK为你展示你所编写的第一个区块链应用程序的完整处理过程。

第二个教程面向Hyperledger Fabric网络运维人员，构建你的第一个区块链网络。该教程展示了使用Hyperledger Fabric来构建一个区块链网络的完整过程并提供了一个简单的、基础的应用程序来进行测试。

也提供了一些其他的教程，比如如果更新你的channel，如何新增一个组织到一个channel，如何更新Hyperledger Fabric的版本以及如何更新网络中的组件等等。

最后，我们提供了两个chaincode教程。一个面向开发者，chaincode开发者，另一个面向运维人员，chaincode运维人员。

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		如果你有该文档未介绍到的问题，或者在运行任何教程时碰到了问题，请访问“十二、 仍有问题”章节来获取额外的帮助。
		</td>
	</tr>
</table>

####构建你的第一个网络####
<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		这些指令已验证过可以和最新的稳定的Docker images以及所提供tar文件中预编译安装工具一起工作。如果你使用来自当前master分支的图像或工具运行这些命令，则可能会看到配置和错误信息。
		</td>
	</tr>
</table>

“构建你的第一个网络”（BYFN,build your first newwork）的场景提供了一个包含两个组织的简单Hyperledger Fabric网络，每个组织维护两个peer节点以及一个“solo” ordering服务。
#####Install prerequisites#####
你需要下载并安装Hyperledger Fabric示例。你会注意到，在fabric-samples目录中提供了一些示例。我们将会使用first-network示例。让我们现在打开该子目录。

	cd fabric-samples/first-network

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		文档提供了这些命令必须在已经下载的fabric-samples资源的子目录first-network下执行。如果你选择在其他路径下执行这些命令，提供的很多脚本都无法找到对应的类库。
		</td>
	</tr>
</table>
#####Want to run it now?#####
我们提供了一个注释完整的脚本--byfn.sh--该脚本会促使这些Docker images快速启动一个由4个peers和一个orderer节点组成的Hyperledger Fabric网络，4个peers代表两个不同组织。它还将启动一个容器来运行脚本执行，实现将peers添加到一个channel中，部署和实例化chaincode并驱动对所部署chaincode的交易执行。

下面是byfn.sh脚本的help文档：

	./byfn.sh --help
	Usage:
	byfn.sh up|down|restart|generate [-c <channel name>] [-t <timeout>] [-d <delay>] [-f <docker-compose-file>] [-s <dbtype>]
	byfn.sh -h|--help (print this message)
  		-m <mode> - one of 'up', 'down', 'restart' or 'generate'
    		- 'up' - bring up the network with docker-compose up
    		- 'down' - clear the network with docker-compose down
    		- 'restart' - restart the network
    		- 'generate' - generate required certificates and genesis block
 		-c <channel name> - channel name to use (defaults to "mychannel")
  		-t <timeout> - CLI timeout duration in seconds (defaults to 10)
  		-d <delay> - delay duration in seconds (defaults to 3)
  		-f <docker-compose-file> - specify which docker-compose file use (defaults to docker-compose-cli.yaml)
  		-s <dbtype> - the database backend to use: goleveldb (default) or couchdb
  		-l <language> - the chaincode language: golang (default) or node
  		-a - don't ask for confirmation before proceeding

  		Typically, one would first generate the required certificates and genesis block, then bring up the network. e.g.:

      		byfn.sh -m generate -c mychannel
     	 	byfn.sh -m up -c mychannel -s couchdb

如果你不指定一个channel名称，则该脚本会使用默认名称“mychannel”。CLI超时参数（使用-t指定）是一个可选值；如果你选择不设置，则该CLI会在10秒（默认设置）之后放弃查询请求。
######Generate Network Artifacts######
准备好了吗？好的，然后执行下列命令：

	./byfn.sh -m generate

你将会看见一个关于将要发生什么的简要描述，连同一个yes/no命令行提示。输入y或点击回车键来执行。
	
	Generating certs and genesis block for with channel 'mychannel' and CLI timeout of '10'
	Continue? [Y/n] y
	proceeding ...
	/Users/xxx/dev/fabric-samples/bin/cryptogen

	##########################################################
	##### Generate certificates using cryptogen tool #########
	##########################################################
	org1.example.com
	2017-06-12 21:01:37.334 EDT [bccsp] GetDefault -> WARN 001 Before using BCCSP, please call InitFactories(). Falling back to bootBCCSP.
	...

	/Users/xxx/dev/fabric-samples/bin/configtxgen
	##########################################################
	#########  Generating Orderer Genesis block ##############
	##########################################################
	2017-06-12 21:01:37.558 EDT [common/configtx/tool] main -> INFO 001 Loading configuration
	2017-06-12 21:01:37.562 EDT [msp] getMspConfig -> INFO 002 intermediate certs folder not found at [/Users/xxx/dev/byfn/crypto-config/ordererOrganizations/example.com/msp/intermediatecerts]. Skipping.: [stat /Users/xxx/dev/byfn/crypto-config/ordererOrganizations/example.com/msp/intermediatecerts: no such file or directory]
	...
	2017-06-12 21:01:37.588 EDT [common/configtx/tool] doOutputBlock -> INFO 00b Generating genesis block
	2017-06-12 21:01:37.590 EDT [common/configtx/tool] doOutputBlock -> INFO 00c Writing genesis block

	#################################################################
	### Generating channel configuration transaction 'channel.tx' ###
	#################################################################
	2017-06-12 21:01:37.634 EDT [common/configtx/tool] main -> INFO 001 Loading configuration
	2017-06-12 21:01:37.644 EDT [common/configtx/tool] doOutputChannelCreateTx -> INFO 002 Generating new channel configtx
	2017-06-12 21:01:37.645 EDT [common/configtx/tool] doOutputChannelCreateTx -> INFO 003 Writing new channel tx

	#################################################################
	#######    Generating anchor peer update for Org1MSP   ##########
	#################################################################
	2017-06-12 21:01:37.674 EDT [common/configtx/tool] main -> INFO 001 Loading configuration
	2017-06-12 21:01:37.678 EDT [common/configtx/tool] doOutputAnchorPeersUpdate -> INFO 002 Generating anchor peer update
	2017-06-12 21:01:37.679 EDT [common/configtx/tool] doOutputAnchorPeersUpdate -> INFO 003 Writing anchor peer update

	#################################################################
	#######    Generating anchor peer update for Org2MSP   ##########
	#################################################################
	2017-06-12 21:01:37.700 EDT [common/configtx/tool] main -> INFO 001 Loading configuration
	2017-06-12 21:01:37.704 EDT [common/configtx/tool] doOutputAnchorPeersUpdate -> INFO 002 Generating anchor peer update
	2017-06-12 21:01:37.704 EDT [common/configtx/tool] doOutputAnchorPeersUpdate -> INFO 003 Writing anchor peer update

第一步为我们各种网络实体生成所有证书和密钥，用于启动ordering服务的创始区块和交易配置channel所需的配置信息集合。
######Bring Up the Network######
下面，你可以使用下列命令来启动网络：

	./byfn.sh -m up

上述命令将编译Golang chaincode images并旋转（spin up）相应的容器。GO是默认的chaincode语言，虽然Node.js chaincode也有支持。如果您想使用node.js的chaincode运行本教程，请执行以下命令：

	# we use the -l flag to specify the chaincode language
	# forgoing the -l flag will default to Golang

	./byfn.sh -m up -l node

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		参阅Hyperledger Fabric的Shim文档来获取更多关于node.js chaincode Shim APIs的信息。
		</td>
	</tr>
</table>

再一次，你会被提示是否继续或放弃。输入y或点击返回键。

	Starting with channel 'mychannel' and CLI timeout of '10'
	Continue? [Y/n]
	proceeding ...
	Creating network "net_byfn" with the default driver
	Creating peer0.org1.example.com
	Creating peer1.org1.example.com
	Creating peer0.org2.example.com
	Creating orderer.example.com
	Creating peer1.org2.example.com
	Creating cli


	 ____    _____      _      ____    _____
	/ ___|  |_   _|    / \    |  _ \  |_   _|
	\___ \    | |     / _ \   | |_) |   | |
	 ___) |   | |    / ___ \  |  _ <    | |
	|____/    |_|   /_/   \_\ |_| \_\   |_|

	Channel name : mychannel
	Creating channel...

日志会从这儿继续打印。此处会运行所有的容器，然后驱动一个完整的端到端的应用程序场景。在成功完成之后，会打印下列信息到你的终端窗口：

	Query Result: 90
	2017-05-16 17:08:15.158 UTC [main] main -> INFO 008 Exiting.....
	===================== Query on peer1.org2 on channel 'mychannel' is successful =====================
	
	===================== All GOOD, BYFN execution completed =====================
	
	
	 _____   _   _   ____
	| ____| | \ | | |  _ \
	|  _|   |  \| | | | | |
	| |___  | |\  | | |_| |
	|_____| |_| \_| |____/

您可以滚动这些日志来查看各种交易。如果你没有得到这个结果，那么跳到故障排除部分，看看我们是否能帮助你发现哪里出了问题。
######Bring Down the Network######
最后，让我们将其停止，这样我们就可以一步一步地探索网络设置了。以下命令会kill你的容器，删除加密材料和四个工件，并从Docker注册表删除chaincode images：
	
	./byfn.sh -m down

再一次，你会被提示是否继续，输入y或点击返回键：
	
	Stopping with channel 'mychannel' and CLI timeout of '10'
	Continue? [Y/n] y
	proceeding ...
	WARNING: The CHANNEL_NAME variable is not set. Defaulting to a blank string.
	WARNING: The TIMEOUT variable is not set. Defaulting to a blank string.
	Removing network net_byfn
	468aaa6201ed
	...
	Untagged: dev-peer1.org2.example.com-mycc-1.0:latest
	Deleted: sha256:ed3230614e64e1c83e510c0c282e982d2b06d148b1c498bbdcc429e2b2531e91
	...

如果你想要深入学习底层工具和启动机制，请继续阅读。在后续章节中，我们将详解各种步骤以及构建一个功能齐全的Hyperledger Fabric网络的所需条件。

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		下面概述的手动步骤假定CLI容器中的CORE_LOGGING_LEVEL被设置为DEBUG。您可以通过修改first-network目录中的docker-compose-cli.yaml文件来设置它。例如:
		</td>
	</tr>
</table>
![](images/picture1.jpg)
#####密码生成器#####
我们将使用密码工具来为我们各种各样的网络实体生成加密材料（x509证书和签名秘钥）。这些证书代表身份，它们允许实体在传递和处理时进行签署/验证操作。
######它是如何工作的?######
加密依赖一个文件--crypto-config.yaml--该文件包含了网络拓扑结构，并且允许我们为组织和归属于这些组织的组件生成一组证书和密钥。每个组织都被提供一个唯一的根证书（CA证书），它将特定的组件（peers和orderers）绑定到该组织。通过给每个组织分配一个唯一的CA证书，我们模仿一个典型的网络，参与成员将使用它自己的证书颁发机构。Hyperledger Fabric内的交易和通信由一个实体的私钥（密钥存储）签名，然后通过公钥（签名证书）进行验证。

您会注意到该文件中有一个count变量。我们使用它来指定每个组织的peers的数量；在我们的示例中，每个组织有两个peers。我们现在不深入研究X.509证书和公钥基础设施的细节。如果你感兴趣，你可以在自己的时间浏览这些主题。

在运行这个工具之前，让我们快速看一下crypto-config.yaml文件的一个片段。尤其要注意OrdererOrgs头下的“name”，“Domain”和“Specs”参数：

	OrdererOrgs:
	#---------------------------------------------------------
	# Orderer
	# --------------------------------------------------------
	- Name: Orderer
	  Domain: example.com
	  CA:
	      Country: US
	      Province: California
	      Locality: San Francisco
	  #   OrganizationalUnit: Hyperledger Fabric
	  #   StreetAddress: address for org # default nil
	  #   PostalCode: postalCode for org # default nil
	  # ------------------------------------------------------
	  # "Specs" - See PeerOrgs below for complete description
	# -----------------------------------------------------
	  Specs:
	    - Hostname: orderer
	# -------------------------------------------------------
	# "PeerOrgs" - Definition of organizations managing peer nodes
	 # ------------------------------------------------------
	PeerOrgs:
	# -----------------------------------------------------
	# Org1
	# ----------------------------------------------------
	- Name: Org1
	  Domain: org1.example.com
	  EnableNodeOUs: true

网络实体的命名约定如下--“{{.Hostname}}.{{.Domain}}”。因此，使用我们的ordering节点作为参考点，则以一个ordering节点开头--orderer.example.com，它关联到一个orderer的MSP ID。该文件包含大量的定义和语法相关内容。您还可以参考会员服务提供商（MSP）文档，对MSP进行更深层次的学习。

在运行了加密工具之后，生成的证书和秘钥都会被保存到crypto-config目录下。
#####配置交易生成器#####
加密工具用于生成四个配置产物：

+ orderer创世区块，
+ channel配置交易，
+ 以及两个锚peer交易--每一个peer组织一个。

请参阅配置文件来了解该工具功能的完整描述。

Orderer block是ordering服务的创世区块，在channel创建的时候，channel配置交易文件被广播给orderer。锚peer交易，顾名思义，指定该channel上的每一个组织的锚peer。
######它是如何工作的?######
配置文件--configtx.yaml--该文件包含了示例网络的定义。有三个成员--一个Orderer Org（OrdererOrg）和两个Peer Orgs（Org1和Org2）每一个都管理和维护两个peer节点。该文件也指定了一个consortium--SampleConsortium--由两个Peer Orgs组成。注意此文件顶部的“Profiles”部分。你会注意到我们有两个唯一的headers。一个用于orderer创世区块--TwoOrgsOrdererGenesis--另一个用于channel--TwoOrgsChannel。

这些headers非常重要，因为当我们创建工件时，我们将把它们作为参数传递。

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		注意，我们的SampleConsortium定义在系统级的profile中，并被我们channel级的profile引用。Channels存在于一个consortium作用域之中，并且所有的consortia必须定义在最大的网络作用域之中。
		</td>
	</tr>
</table>

该文件还包含两个值得注意的说明部分。首先，我们为每一个Peer Org（peer0.org1.example.com和peer0.org2.example.com）指定锚peers。其次，我们为每个成员指向MSP目录的位置，进而允许我们为创世区块中的每个组织保存根证书。这是一个至关重要的概念。现在，与ordering服务通信的任何网络实体都可以验证其数字签名。
#####运行工具#####
您可以使用configtxgen和加密命令手动生成证书/密钥和各种配置artifacts。或者，你可以尝试修改byfn.sh脚本来完成你的目标。
######手动生成artifacts######
你可以参考byfn.sh脚本中的generateCerts方法中的命令，这些命令是生成crypto-config.yaml文件中定义的网络配置所需的证书所需要的。然而，为了方便起见，我们也将在这里提供参考。

首先让我们运行加密工具。库在bin目录中，所以我们需要提供工具位置的相对路径：

	../bin/cryptogen generate --config=./crypto-config.yaml

在终端中你应该会看到下列信息：
	
	org1.example.com
	org2.example.com

证书和秘钥（即MSP材料）会被输出到一个目录--crypto-config--在first-network目录的根节点上。

其次，我们需要告诉加密工具去哪儿查找所需的configtx.yaml文件。我们会告诉它从我们当前工作路径去查找：

	export FABRIC_CFG_PATH=$PWD

然后，调用配置工具来创建创世区块：

	../bin/configtxgen -profile TwoOrgsOrdererGenesis -outputBlock ./channel-artifacts/genesis.block

在终端你会看见类似的输出：

	2017-10-26 19:21:56.301 EDT [common/tools/configtxgen] main -> INFO 001 Loading configuration
	2017-10-26 19:21:56.309 EDT [common/tools/configtxgen] doOutputBlock -> INFO 002 Generating genesis block
	2017-10-26 19:21:56.309 EDT [common/tools/configtxgen] doOutputBlock -> INFO 003 Writing genesis block

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		The orderer genesis block and the subsequent artifacts we are about to create will be output into the channel-artifacts directory at the root of this project.
		</td>
	</tr>
</table>
######创建一个Channel配置交易######
下面，我们需要创建channel交易工件。确保替换$CHANNEL_NAME或设置CHANNEL_NAME作为环境变量，这样就能顺利被下列指令所识别：

	# The channel.tx artifact contains the definitions for our sample channel

	export CHANNEL_NAME=mychannel  && ../bin/configtxgen -profile TwoOrgsChannel -outputCreateChannelTx ./channel-artifacts/channel.tx -channelID $CHANNEL_NAME

在终端你会看见类似的输出：

	2017-10-26 19:24:05.324 EDT [common/tools/configtxgen] main -> INFO 001 Loading configuration
	2017-10-26 19:24:05.329 EDT [common/tools/configtxgen] doOutputChannelCreateTx -> INFO 002 Generating new channel configtx
	2017-10-26 19:24:05.329 EDT [common/tools/configtxgen] doOutputChannelCreateTx -> INFO 003 Writing new channel tx

接下来，我们将在正在构建的channel上定义Org1的锚peer。再一次，请确保为下列命令替换$CHANNEL_NAME或设置环境变量。终端输出将模拟channel交易工件：

	../bin/configtxgen -profile TwoOrgsChannel -outputAnchorPeersUpdate ./channel-artifacts/Org1MSPanchors.tx -channelID $CHANNEL_NAME -asOrg Org1MSP

现在，我们将在同样的channel上为Org2定义锚peer：

	../bin/configtxgen -profile TwoOrgsChannel -outputAnchorPeersUpdate ./channel-artifacts/Org2MSPanchors.tx -channelID $CHANNEL_NAME -asOrg Org2MSP
#####启动网络#####
我们将利用一个脚本来支持我们的网络。Docker-compose文件引用我们先前下载的images，并用我们之前生成的genesis.block启动orderer。

我们将手动地执行这些命令，以此来了解每个调用的语法和功能。

首先，让我们启动网络：

	docker-compose -f docker-compose-cli.yaml up -d

如果你想要查看网络的实时日志，则不要使用-d参数。如果您允许日志流，那么您需要打开第二个终端来执行CLI调用。

CLI容器将闲置1000秒钟。如果它在你需要的时候消失了，你可以用一个简单的命令重新启动它：
		
	docker start cli
######环境变量######
要保证peer0.org1.example.com的下列CLI命令工作，我们需要先设置下列四个环境变量。Peer0.org1.example.com的这些变量是内置于CLI容器的，因此可以直接使用。但是，如果你想发生调用到其他peer或其他orderer，那么你需要相应地提供这些值。检查docker-compose-base.yaml的这些特定路径：
	
	# Environment variables for PEER0

	CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.example.com/users/Admin@org1.example.com/msp
	CORE_PEER_ADDRESS=peer0.org1.example.com:7051
	CORE_PEER_LOCALMSPID="Org1MSP"
	CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/ca.crt
######创建并加入channel######
回想一下，在之前的“创建一个channel配置交易”章节中，我们使用加密工具创建了channel配置交易。您可以重复该过程以创建额外的channel配置交易，使用传递给加密工具的configtx.yaml中相同或不同的配置文件。然后，您可以重复本节中定义的处理过程，以建立网络中的其他channels。

我们将使用docker exec命令进入CLI容器：

	docker exec -it cli bash

如果成功，你会看见如下信息：

	root@0d78bb69300d:/opt/gopath/src/github.com/hyperledger/fabric/peer#

下一步，我们将传入生成的channel配置交易工件到orderer作为创建channel请求部分。

使用-c标识来指定我们的channel名称并使用-f标识来指定我们的channel配置交易。在此示例中是channel.tx，当然你可以使用别的名称来指定你自己的配置交易。再一次，我们将在我们的CLI容器中设置CHANNEL_NAME环境变量，这样我们就不需要再明确地传递该参数了：

	export CHANNEL_NAME=mychannel

	# the channel.tx file is mounted in the channel-artifacts directory within your CLI container
	# as a result, we pass the full path for the file
	# we also pass the path for the orderer ca-cert in order to verify the TLS handshake
	# be sure to export or replace the $CHANNEL_NAME variable appropriately
	
	peer channel create -o orderer.example.com:7050 -c $CHANNEL_NAME -f ./channel-artifacts/channel.tx --tls --cafile /opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		注意作为命令组成部分传递的--cafile。这是orderer的root证书的本地路径，允许我们验证TLS握手。
		</td>
	</tr>
</table>

该命令返回一个创世区块--<channel-ID.block>--我们将使用它来加入channel。创世区块包含channel.tx中指定的配置信息。如果你没有修改默认channel名称，则该命令会返回你一个名为mychannel.block的原型。

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		您将继续留在CLI容器中学习剩下的这些手动命令。还必须记住，当操作目标是peer0.org1.example.com以外的peer时，需要预先声明相应的环境变量。
		</td>
	</tr>
</table>

现在我们将peer0.org1.example.com加入到channel。

	# By default, this joins ``peer0.org1.example.com`` only
	# the <channel-ID.block> was returned by the previous command
	# if you have not modified the channel name, you will join with mychannel.block
	# if you have created a different channel name, then pass in the appropriately named block
	
	 peer channel join -b mychannel.block

你可以通过对四个环境变量进行适当的更改，使其他peers按需加入channel。

我们不必加入每个peer，只要加入peer0.org2.example.com，这样我们就可以在我们的channel中正确地更新锚peer定义。由于我们重写了在CLI容器中内置的默认环境变量，完整的命令应该如下：

	CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org2.example.com/users/Admin@org2.example.com/msp CORE_PEER_ADDRESS=peer0.org2.example.com:7051 CORE_PEER_LOCALMSPID="Org2MSP" CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org2.example.com/peers/peer0.org2.example.com/tls/ca.crt peer channel join -b mychannel.block

或者，您可以选择单独设置这些环境变量，而不是传递整个字符串。一旦它们被设置，您只需要再次发出peer channel连接命令，则CLI容器将代表pee0.org2.example.com执行。
######更新锚peers######
下列命令是channel更新并且他们会传播到channel的定义。本质上，我们在channel的创世区块的顶部增加额外的配置信息。请注意，我们不是在修改创世区块，只是简单地将增量添加到定义锚peers的链中。

更新channel定义为Org1定义锚peer为peer0.org1.example.com:

	peer channel update -o orderer.example.com:7050 -c $CHANNEL_NAME -f ./channel-artifacts/Org1MSPanchors.tx --tls --cafile /opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem

现在更新channel定义来为Org2定义锚peer为peer0.org2.example.com。同样地，对于Org2 peer的peer channel连接命令，我们需要用恰当的环境变量来完成这个调用。

	CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org2.example.com/users/Admin@org2.example.com/msp CORE_PEER_ADDRESS=peer0.org2.example.com:7051 CORE_PEER_LOCALMSPID="Org2MSP" CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org2.example.com/peers/peer0.org2.example.com/tls/ca.crt peer channel update -o orderer.example.com:7050 -c $CHANNEL_NAME -f ./channel-artifacts/Org2MSPanchors.tx --tls --cafile /opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem
######安装和实例化chaincode######
<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		我们将使用一个简单的已经存在的chaincode。来学习如何编写你自己的chaincode，参考为开发者教程准备的chaincode。
		</td>
	</tr>
</table>

应用程序通过chaincode与区块链账本交互。因此，我们需要在每个peer上安装chaincode来执行和背书我们的交易，并实例化channel上的chaincode。

首先，安装示例Go或者Node.js chaincode到四个peer节点中任何一个上。这些命令将指定类型的源代码放在我们peer的文件系统上。

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		对于每个chaincode名称和版本，你只能安装一个版本的源代码。源代码存在于peer文件系统的chaincode名称和版本上下文中，它是语言不可知的。同样，实例化的chaincode容器将反映在peer上安装了哪种语言。
		</td>
	</tr>
</table>
#######Golang#######
	# this installs the Go chaincode
	peer chaincode install -n mycc -v 1.0 -p github.com/chaincode/chaincode_example02/go/
#######Node.js#######
	# this installs the Node.js chaincode
	# make note of the -l flag; we use this to specify the language
	peer chaincode install -n mycc -v 1.0 -l node -p /opt/gopath/src/github.com/chaincode/chaincode_example02/node/

下一步，实例化channel上的chaincode。该步骤会实例化channel上的chaincode，设置chaincode的背书策略，并且为目标peer启动一个chaincode容器。注意-P参数。这是我们针对待校验chaincode的策略，该策略指定了一笔交易的所需背书级别。

在下列的命令中，你会发现我们使用-P "OR('Org1MSP.peer','Org2MSP.peer')"来指定我们的策略。这意味着我们需要一个peer的背书，而该peer必须属于Org1或Org2。如果我们将OR换成AND，那么我们就需要两个背书。
#######Golang#######
	# be sure to replace the $CHANNEL_NAME environment variable if you have not exported it
	# if you did not install your chaincode with a name of mycc, then modify that argument as well
	
	peer chaincode instantiate -o orderer.example.com:7050 --tls --cafile /opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem -C $CHANNEL_NAME -n mycc -v 1.0 -c '{"Args":["init","a", "100", "b","200"]}' -P "OR ('Org1MSP.peer','Org2MSP.peer')"
#######Node.js#######
<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		No.js chaincode的实例化大约需要一分钟。命令不是挂起的，而是在image被编译时安装fabric-shim层。
		</td>
	</tr>
</table>

	# be sure to replace the $CHANNEL_NAME environment variable if you have not exported it
	# if you did not install your chaincode with a name of mycc, then modify that argument as well
	# notice that we must pass the -l flag after the chaincode name to identify the language
	
	peer chaincode instantiate -o orderer.example.com:7050 --tls --cafile /opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem -C $CHANNEL_NAME -n mycc -l node -v 1.0 -c '{"Args":["init","a", "100", "b","200"]}' -P "OR ('Org1MSP.peer','Org2MSP.peer')"

更多关于策略实现的详细信息，请参见[背书策略文档](http://hyperledger-fabric.readthedocs.io/en/latest/endorsement-policies.html)。

如果你需要额外的peers来和账本交互，那么你需要将它们加入channel，并且在对应peer的文件系统上安装相同的名称，版本和语言的chaincode源代码。只要peers尝试与制定的chaincode交互，就会为对应的peer启动一个chaincode容器。再次说明，Node.js images的编译速度回比较慢。

一旦该chaincode在channel上被实例化，我们就可以放弃"l"参数了。我们只需要传入channel标识和chaincode的名称。
######查询######
让我们查询a的值来确认chaincode被正确地实例化了并且状态数据库也是可用的。查询的语法如下：

	# be sure to set the -C and -n flags appropriately

	peer chaincode query -C $CHANNEL_NAME -n mycc -c '{"Args":["query","a"]}'
######调用######
现在从a转10给b。该笔交易会创建一个新的block并更新状态数据库。调用语法如下：

	# be sure to set the -C and -n flags appropriately

	peer chaincode invoke -o orderer.example.com:7050  --tls --cafile /opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem  -C $CHANNEL_NAME -n mycc -c '{"Args":["invoke","a","b","10"]}'
######查询######
确认下之前的调用成功执行了。我们初始化a的时候值为100并且刚刚通过调用转出了10。因此查询结果应该是90。查询语法如下：

	# be sure to set the -C and -n flags appropriately

	peer chaincode query -C $CHANNEL_NAME -n mycc -c '{"Args":["query","a"]}'

我们应该看到如下输出：
	
	Query Result: 90

请随意尝试上述的命令，完成转入或转出操作。
######背后发生了什么?######
<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		这些步骤所描述的场景对应的是使用"./byfn.sh up"命令运行后对应的场景。使用./byfn.sh down来清理你的网络并确保该命令成功执行。然后使用同样的docker-compose提示来再次运行你的网络。
		</td>
	</tr>
</table>

+ A script - script.sh - 内置于CLI容器。该脚本根据提供的channel名称驱动createChannel命令，并使用channel.tx文件完成channel配置。

+ CreateChannel命令的输出是一个创世区块--<你的channel名称>.block--该区块存储于peer的文件系统并包含channel.tx中指定的channel配置信息。

+ JoinChannel命令作用于所有四个peers，命令作用结果作为先前生成的创世区块的输入。该命令指示peers加入<你的channel名称>并创建使用<你的channel名称>.block来创建一个链。

+ 现在，我们拥有了一个包含四个peers和两个组织的channel。这就是我们的TwoOrgsChannel配置。

+ peer0.org1.example.com和peer1.org1.example.com属于Org1;peer0.org2.example.com和peer1.org2.example.com属于Org2。

+ 这些关联关系是通过crypto-config.yaml定义的，并且MSP路径是在docker compose中指定的。

+ 然后Org1MSP的锚peers（peer0.org1.example.com）和Org2MSP的锚peers（peer0.org2.example.com）被更新。我们通过传递Org1MSPanchors.tx和Org2MSPanchors.tx到ordering服务来实现更新，一同传递的信息还有我们channel的名称。

+ Chaincode - chaincode_example02 - 安装在peer0.org1.example.com和peer0.org2.example.com之上。

+ 该chaincode在peer0.org2.example.com上被“实例化”。实例化会将该chaincode添加到channel，启动目标peer的容器，并且初始化与该chaincode关联的键值对。该示例中初始化值是["a","100" "b","200"]。“实例化”的最终结果会启动名为dev-peer0.org2.example.com-mycc-1.0的容器。

+ 实例化也传入一个背书策略参数。策略使用 -P "OR('Org1MSP.peer','Org2MSP.peer')"来指定，这意味着所有的交易必须被Org1或者Org2的peer完成背书。

+ 一个针对“a”的数值的查询被发布到peer0.org1.example.com。Chaincode是之前安装到peer0.org1.example.com的，因此会为Org1启动一个名为dev-peer0.org1.example.com-mycc-1.0的容器。查询的结果也会返回。之前没有写操作，所以a的查询结果仍会返回“100”。

+ 从a转出10给b的调用被发送到peer0.org1.example.com。

+ 该chaincode随后被安装到peer1.org2.example.com。

+ 查询a值的请求被发送到peer1.org2.example.com。这会启动一个名为dev-peer1.org2.example.com-mycc-1.0的third容器。值90被返回，也正确地反映了之前a被转出了10。
######这说明了什么？######
Chaincode必须被安装在一个peer上，这样它才能成功地对账本执行读/写操作。而且，直到一个初始化或传统交易--读/写--在该chaincode（例如查询a的值）上执行时，才会为peer启动一个chaincode容器。交易会触发容器的启动。此外，一个channel中的所有peers都维护了一份包含区块链的账本的精确副本，以存储blocks中不可变的、有序的记录，以及一个状态数据库来保持当前状态的快照。这包含了那些没有安装chaincode的peers（比如上述示例中的peer1.org1.example.com）。最终，在安装完成（比如上述示例中的peer1.org2.example.com）之后，该chaincode是可访问的，因为它已经被实例化了。
######如何才能查看这些交易？######
查看CLI Docker容器的日志：

	docker logs -f cli

你应该看到如下输出：

	2017-05-16 17:08:01.366 UTC [msp] GetLocalMSP -> DEBU 004 Returning existing local MSP
	2017-05-16 17:08:01.366 UTC [msp] GetDefaultSigningIdentity -> DEBU 005 Obtaining default signing identity
	2017-05-16 17:08:01.366 UTC [msp/identity] Sign -> DEBU 006 Sign: plaintext: 0AB1070A6708031A0C08F1E3ECC80510...6D7963631A0A0A0571756572790A0161
	2017-05-16 17:08:01.367 UTC [msp/identity] Sign -> DEBU 007 Sign: digest: E61DB37F4E8B0D32C9FE10E3936BA9B8CD278FAA1F3320B08712164248285C54
	Query Result: 90
	2017-05-16 17:08:15.158 UTC [main] main -> INFO 008 Exiting.....
	===================== Query on peer1.org2 on channel 'mychannel' is successful =====================
	
	===================== All GOOD, BYFN execution completed =====================
	
	
	 _____   _   _   ____
	| ____| | \ | | |  _ \
	|  _|   |  \| | | | | |
	| |___  | |\  | | |_| |
	|_____| |_| \_| |____/

你可以滚动日志来查看多笔交易。
######如何查看chaincode日志？######
检查独立的chaincode容器来查看每个容器执行的各笔交易。下面是每个融入输出的集合：

	$ docker logs dev-peer0.org2.example.com-mycc-1.0
	04:30:45.947 [BCCSP_FACTORY] DEBU : Initialize BCCSP [SW]
	ex02 Init
	Aval = 100, Bval = 200
	
	$ docker logs dev-peer0.org1.example.com-mycc-1.0
	04:31:10.569 [BCCSP_FACTORY] DEBU : Initialize BCCSP [SW]
	ex02 Invoke
	Query Response:{"Name":"a","Amount":"100"}
	ex02 Invoke
	Aval = 90, Bval = 210
	
	$ docker logs dev-peer1.org2.example.com-mycc-1.0
	04:31:30.420 [BCCSP_FACTORY] DEBU : Initialize BCCSP [SW]
	ex02 Invoke
	Query Response:{"Name":"a","Amount":"90"}
#####理解Docker Compose拓扑结构#####
BYFN示例为我们提供了两种格式的Docker Compose文件，两者都是从docker-compose-base.yaml继承而来。第一种格式，docker-compose-cli.yaml，为我们提供了一个CLI容器，容器包含一个orderer和四个peers。我们使用这个文件来完成这个页面上的所有指令。

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		本节的其余部分介绍的是为SDK设计的docker-compose文件。有关运行这些测试的详细信息，请参阅[Node SDK报告](https://github.com/hyperledger/fabric-sdk-node)。
		</td>
	</tr>
</table>

第二种格式，docker-compose-e2e.yaml，旨在使用Node.js SDK来运行端到端的测试。除了使用SDK的功能之外，其主要差异是有现成的针对fabric-ca servers的容器。这样的好处是，我们可以发送REST调用给组织CAs来实现用户注册和入会。

如果你想使用docker-compose-e2e.yaml时不必先运行byfn.sh脚本，那么我们需要做四个小修改。我们需要为我们的组织的CA指定私钥。你可以在你的crypto-config文件夹中定义这些值。例如，要为Org1指定私钥我们应当遵循该路径--crypto-config/peerOrganizations/org1.example.com/ca/。私钥是一个长hash值并以_sk结尾。Org2的路径应该是--crypto-config/peerOrganizations/org2.example.com/ca/。

在docker-compose-e2e.yaml文件中，更新ca0和ca1的FABRIC_CA_SERVER_TLS_KEYFILE变量。你也需要修改启动ca服务器命令中的路径。你为每一个CA容器提供相同的私钥两次。
#####使用CouchDB#####
状态数据库可以从默认（goleveldb）切换至CouchDB。CouchDB也支持相同的chaincode功能，而且，如果chaincode数据是以JSON格式组装的情况下，CouchDB还提供了额外针对状态数据库进行丰富且复杂查询的能力。

若要使用CouchDB来替换默认数据库（goleveldb），请遵循前面所述的用于生成工件的相同程序，但在启动网络时，如下传递docker-compose-couch.yaml：

	docker-compose -f docker-compose-cli.yaml -f docker-compose-couch.yaml up -d

chaincode_example02现在应当底层使用的是CouchDB。

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		如果你选择实现fabric-couchdb容器端口到主机端口的映射，请确保你意识到了安全问题。在开发环境中映射端口使CouchDB REST API可用，并通过CouchDB Web接口（Fauxton）实现数据库的可视化。生产环境可能会避免执行端口映射，以限制对CouchDB容器的外部访问。
		</td>
	</tr>
</table>

你可以使用上面列出的步骤对CoucDB状态数据库使用chaincode_example02 chaincode，但是为了行使CouchDB查询能力，你需要使用以JSON格式建模的chaincode（例如，marbles02）。您可以在fabric/examples/chaincode/go目录中找到marbles02 chaincode。

你将遵循前述“创建并加入channel”章节中同样的处理来创建并加入channel。一旦你将peers加入到channel，使用下列步骤与marbles02 chaincode进行交互：

+ 在peer0.org1.example.com上安装并实例化chaincode：

		# be sure to modify the $CHANNEL_NAME variable accordingly for the instantiate command
		peer chaincode install -n marbles -v 1.0 -p github.com/chaincode/marbles02/go
		peer chaincode instantiate -o orderer.example.com:7050 --tls --cafile /opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem -C $CHANNEL_NAME -n marbles -v 1.0 -c '{"Args":["init"]}' -P "OR ('Org0MSP.peer','Org1MSP.peer')"
	
+ 创建一些marbles并移动它们：

		# be sure to modify the $CHANNEL_NAME variable accordingly

		peer chaincode invoke -o orderer.example.com:7050 --tls --cafile /opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem -C $CHANNEL_NAME -n marbles -c '{"Args":["initMarble","marble1","blue","35","tom"]}'
		peer chaincode invoke -o orderer.example.com:7050 --tls --cafile /opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem -C $CHANNEL_NAME -n marbles -c '{"Args":["initMarble","marble2","red","50","tom"]}'
		peer chaincode invoke -o orderer.example.com:7050 --tls --cafile /opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem -C $CHANNEL_NAME -n marbles -c '{"Args":["initMarble","marble3","blue","70","tom"]}'
		peer chaincode invoke -o orderer.example.com:7050 --tls --cafile /opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem -C $CHANNEL_NAME -n marbles -c '{"Args":["transferMarble","marble2","jerry"]}'
		peer chaincode invoke -o orderer.example.com:7050 --tls --cafile /opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem -C $CHANNEL_NAME -n marbles -c '{"Args":["transferMarblesBasedOnColor","blue","jerry"]}'
		peer chaincode invoke -o orderer.example.com:7050 --tls --cafile /opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem -C $CHANNEL_NAME -n marbles -c '{"Args":["delete","marble1"]}'

+ 如果你选择了在docker-compose中映射CouchDB端口，现在你可以通过CouchDB web接口（Fauxton）来访问状态数据库，打开浏览器并访问下列URL：

	http://localhost:5984/_utils

你应当能看见一个名为mychannel（或者你特殊的channel名称）的数据库以及数据库中的文件。

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		对于下列命令，确保恰当地更新$CHANNEL_NAME变量。
		</td>
	</tr>
</table>

你可以从CLI中运行常规查询（例如读取marble2）：
	
	peer chaincode query -C $CHANNEL_NAME -n marbles -c '{"Args":["readMarble","marble2"]}'

会展示marble2的明细输出：

	Query Result: {"color":"red","docType":"marble","name":"marble2","owner":"jerry","size":50}

你可以检索指定marble的历史信息--例如marble1：

	peer chaincode query -C $CHANNEL_NAME -n marbles -c '{"Args":["getHistoryForMarble","marble1"]}'

Marble1上发生的交易会被输出展示：

	Query Result: [{"TxId":"1c3d3caf124c89f91a4c0f353723ac736c58155325f02890adebaa15e16e6464", "Value":{"docType":"marble","name":"marble1","color":"blue","size":35,"owner":"tom"}},{"TxId":"755d55c281889eaeebf405586f9e25d71d36eb3d35420af833a20a2f53a3eefd", "Value":{"docType":"marble","name":"marble1","color":"blue","size":35,"owner":"jerry"}},{"TxId":"819451032d813dde6247f85e56a89262555e04f14788ee33e28b232eef36d98f", "Value":}]

你也可以基于数据内容执行丰富查询，比如查询ower为jerry的marble信息：

	peer chaincode query -C $CHANNEL_NAME -n marbles -c '{"Args":["queryMarblesByOwner","jerry"]}'

输出会展示jerry拥有的两个marbles：

	Query Result: [{"Key":"marble2", "Record":{"color":"red","docType":"marble","name":"marble2","owner":"jerry","size":50}},{"Key":"marble3", "Record":{"color":"blue","docType":"marble","name":"marble3","owner":"jerry","size":70}}]

#####为什么选择CouchDB#####
CouchDB是一种NoSQL解决方案。它是一个面向文档的数据库，数据库中文档字段以键值对格式存储。字段可以是一个简单的键值对，也可以是list或map。除了LevelDB所支持的键/复合键/键范围查询之外，CouchDB也支持完整的数据丰富查询能力，例如对整个区块链数据的non-key查询，因为其数据内容以JSON格式存储，并且完全可查询。因此，CouchDB可以满足chaincode，审计，报告需求等很多使用场景，这些场景都是LevelDB所不支持的。

CouchDB还可以增强区块链网络中遵从安全性和数据保护安全性。因为它能够通过过滤和屏蔽交易中的单个属性来实现字段级安全性，并且通常只授权只读权限。

此外，CouchDB落入CAP定理的AP类型（可用性和分区容错）。它使用具有最终一致性的主-母复制模型。更多信息可以在CouchDB文档的最终一致性页面上找到。但是，在每个fabric peer下，没有数据库副本，要保证对数据库的写入一致性和持久性（而不是最终一致性）。

CouchDB是Fabric第一个插拔式的外部状态数据库，可以并且应该还有其他外部数据库选项。例如，IBM为其区块链启用关系数据库。CP类型（一致性和分区容错）数据库也可能需要，从而不需要通过应用级别的保障来达成数据一致性。

#####数据持久化注意点#####
如果peer容器或CouchDB容器需要数据持久化，一种选择是将docker-host中的目录安装到容器中的相关目录中。例如，你可以在docker-compose-base.yaml文件中按照peer容器的规范增加下面两行配置：

	volumes:
 		- /var/hyperledger/peer0:/var/hyperledger/production

对于CouchDB容器，你可以按照CouchDB容器规范增加下面两行配置：

	volumes:
 		- /var/hyperledger/couchdb0:/opt/couchdb/data

#####故障排除#####
+ 重新启动你的网络。使用下列命令来移除artifacts, crypto, containers和chaincode images:
	
	./byfn.sh -m down

	<table>
		<tr>
			<td bgcolor=#6A5ACD>
				<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
			</td>
		</tr>
		<tr>
			<td bgcolor=#7FFFD4>
			如果你不移除老的容器和镜像，可能会报错。
			</td>
		</tr>
	</table>

+ 如果你发现了Docker错误，首先检查你docker的版本（先决条件），然后尝试重启你的Docker程序。Docker的问题通常不能立即被识别。例如，你可能发现由于无法访问容器中安装的加密材料所引发的错误。

	如果出现了该错误，移除镜像并从头开始：
	
		docker rm -f $(docker ps -aq)
		docker rmi -f $(docker images -q)

+ 当你创建、实例化、调用或查询命令时报错了，确保你已经正确地更新了channel名称和chaincode名称。在提供的示例命令中，有占位符。

+ 如果你发现了下列错误：

		Error: Error endorsing chaincode: rpc error: code = 2 desc = Error installing chaincode code mycc:1.0(chaincode /var/hyperledger/production/chaincodes/mycc.1.0 exits)

	你很可能使用的是之前运行留下的chaincode镜像（例如，dev-peer1.org2.example.com-mycc-1.0或dev-peer0.org1.example.com-mycc-1.0）。移除并再次尝试。

		docker rmi -f $(docker images | grep peer[0-9]-peer[0-9] | awk '{print $3}')

+ 如果你发现类似如下的错误：

		Error connecting: rpc error: code = 14 desc = grpc: RPC failed fast due to transport failure
		Error: rpc error: code = 14 desc = grpc: RPC failed fast due to transport failure

	确保你运行网络中的镜像为“1.0.0”，并以及被重新标记为“latest”。

+ 如果你发现下列错误：

		[configtx/tool/localconfig] Load -> CRIT 002 Error reading configuration: Unsupported Config Type ""
		panic: Error reading configuration: Unsupported Config Type ""

	则说明你没有正确设置FABRIC_CFG_PATH环境变量。配置文件工具需要通过该变量来定位configtx.yaml。返回并执行export FABRIC_CFG_PATH=$PWD，然后重新创建channel artifacts。

+ 清理网络，使用下列选项：

		./byfn.sh -m down

+ 如果您看到一个错误说你仍然有“active endpoints”，则修剪你的Docker网络。这将抹去你以前的网络，让你拥有一个全新的环境：

		docker network prune
	
	你会看见如下信息：

		WARNING! This will remove all networks not used by at least one container.
		Are you sure you want to continue? [y/N]

	选择 y.

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		如果仍然报错，在Hyperledger Rocket论坛或StackOverflow的fabric-questions频度上传你的日志信息。
		</td>
	</tr>
</table>

####编写第一个应用程序####
<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		如果你仍对Fabric网络的基础架构不熟悉，请先返回阅读之前的章节。
		</td>
	</tr>
</table>

在本章，我们会看几个示例程序来学习Fabric应用是如何工作的。这些应用（以及应用使用的智能合约）--共同被定义为fabcar--提供了针对Fabric功能的广泛演示。尤其是，我们将展示与证书颁发机构交互并生成注册证书的过程，之后我们将利用这些身份来查询和更新分类账。

我们将完成下面三个原则步骤：

1. 设置一个开发环境。我们的应用程序需要一个交互的网络，所以我们将下载一个精简的组件，仅用于注册/注册、查询和更新：

![](images/AppConceptsOverview.png)

2. 学习我们的应用将使用的示例智能合约的参数。我们的智能合约包含多种功能来支持我们以不同的方式与账本进行交互。我们将深入检查该账本来学习我们的应用程序将使用的功能。

3. 开发能够查询和更新账本中资产的应用程序。我们将深入应用程序代码（我们的应用程序是JavaScript编写的）并手动操作变量以运行不同类型的查询和更新。

在完成本次教程之后，你应该对应用程序如何结合智能合约与账本交互有一个基础的理解。

#####设置DEV环境#####
如果你已经阅读过了章节“Building Your First Network”，你应该已经设置好了dev环境并且也已经下载了fabric-samples以及相关附件。要运行该教程，你现在需要做的是卸载已经存在的网络，可以通过下列命令实现：

	./byfn.sh -m down

如果你没有应该开发环境，访问Prerequisites页面确保在你的机器上安装必要的依赖。

接下来，访问Hyperledger Fabric Samples页面并遵循提供的指令。一旦完成克隆fabric-samples库，以及下载最新的稳定Fabric映像和可用的实用工具后，就返回到本教程。

此时，一切都应该安装就绪。切换到你fabric-samples库的fabcar子目录并查看里面的内容：

	cd fabric-samples/fabcar  && ls

你应该看见如下资源：

	enrollAdmin.js     invoke.js       package.json    query.js        registerUser.js startFabric.sh

在开始之前，我们需要做一点工作。运行下列命令来杀死任何不新鲜的或激活的容器：

	docker rm -f $(docker ps -aq)

清除所有缓存网络：

	# Press 'y' when prompted by the command

	docker network prune

最后，如果你已经运行过该教程，你还需要删除fabcar智能合约的底层chaincode镜像。如果你是第一次，则你的系统上不会存在该chaincode镜像：

	docker rmi dev-peer0.org1.example.com-fabcar-1.0-5c906e402ed29f20260ae42283216aa75549c571e2e380f3615826365d8269ba

######安装客户端&启动网络######
<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		下列指令需要你位于fabric-samples的子目录fabcar中。在本教程的其余部分保持位于此子目录的根目录。
		</td>
	</tr>
</table>

运行下列命令来安装应用程序所需的Fabric依赖。我们关心的是fabric-ca-client，它允许我们的应用程序与CA服务器通信并检索身份资料，同时fabric-client允许我们加载身份资料，并与peers和ordering service交互。

	npm install

使用startFabric.sh脚本启动你的网络。该命令将旋转我们的各种Fabric实体，并启动一个智能合约容器，用于以Golang编写的链式代码：

	./startFabric.sh

您还可以针对Node.js编写的chaincode来运行此教程。如果你想这么做，请采用下列命令：

	./startFabric.sh node

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		注意，Node.js chaincode场景大概耗费90秒来完成，也许会更久。The script is not hanging, rather the increased time is a result of the fabric-shim being installed as the chaincode image is being built.
		</td>
	</tr>
</table>

现在，你可以获得了一个示例网络和一些代码，让我们来看看不同的片段是如何组合在一起的。

#####应用程序如何与网络交互#####
要更深入地了解fabcar网络中的组件（以及它们是如何部署的）以及应用程序如何在更细粒度的层次上与这些组件交互，请参阅[理解Fabcar网络](https://hyperledger-fabric.readthedocs.io/en/release-1.1/understand_fabcar_network.html)。

开发人员更感兴趣的是查看应用程序做了什么，以及查看代码本身来探究应用程序是如何构造的。现在，需要知道的最重要的事情是应用程序使用SDK来访问允许查询和更新分类账的API。

#####注册管理员用户#####
<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		下面两个章节涉及与证书颁发机构的交互。当运行下面的程序时，你会发现追踪CA日志是十分有用的。
		</td>
	</tr>
</table>

要追踪你的CA日志，切分你的终端或新开一个shell窗口并如下执行：

	docker logs -f ca.example.com

现在，跳回到fabcar目录的终端...

当我们启动网络时，一个管理员用户--admin--会注册到CA。现在，我们需要发送一个注册调用到CA服务器并获取该用户的注册验证。这里我们不详细阐述注册细节，但足以说明SDK和扩展我们的应用程序需要这个证书，以便为管理员创建一个用户对象。然后，我们将使用这个admin对象来注册并加入一个新用户。发送admin注册调用到CA服务器：

	node enrollAdmin.js

该程序会调用一个证书请求文件（CSR）请求并最终输出一个eCert和关键材料到一个新建的文件夹hfc-key-store，该文件夹位于该项目的根目录。当应用程序需要为各个用户创建或加载身份对象时，会查找该路径。

#####注册并加入user1#####
使用刚刚生成的admin eCert，我们将再一次与CA服务器交互来注册和加入一个新用户。该用户-user1-就是我们查询和更新账本时使用的身份。这里需要注意的是，为新用户发出注册和加入调用的是admin身份（即，该用户扮演注册员的角色）。为user1发送注册和加入调用：

	node registerUser.js

类似于admin注册，该程序调用一个CSR并输出keys和eCert到hfc-key-store子目录。至此，我们有了两个独立用户的身份材料--admin & user1。是时候与账本交互了...

#####查询账本#####
查询是你如何阅读账本数据的方式。数据以键值对的集合形式存储，你可以查询单个key的值，多个keys的值，或者如果账本是JSON这类富数据存储格式编写的，则可以执行复杂搜索（例如，查找所有包含特定关键字的资产）。

下面是一个查询如何工作的示意图：

![](images/QueryingtheLedger.png)

首先，让我们运行query.js程序来返回账本中包含所有cars的列表。我们将使用我们的第二个身份--user1--作为该应用程序的签名实体。程序中的下列命令指定了user1作为签名人：

	fabric_client.getUserContext('user1', true);

回想一下，user1注册材料已经放入我们的hfc-key-store子目录中，所以我们只需要告诉应用程序获取该身份。在定义了用户对象之后，我们现在可以从账本中进行读取操作。应用程序中预置了一个查询所有cars的函数，所以我们可以简单地如下运行程序：

	node query.js

返回应该看起来类似：

	Successfully loaded user1 from persistence
	Query has completed, checking results
	Response is  [{"Key":"CAR0", "Record":{"colour":"blue","make":"Toyota","model":"Prius","owner":"Tomoko"}},
	{"Key":"CAR1",   "Record":{"colour":"red","make":"Ford","model":"Mustang","owner":"Brad"}},
	{"Key":"CAR2", "Record":{"colour":"green","make":"Hyundai","model":"Tucson","owner":"Jin Soo"}},
	{"Key":"CAR3", "Record":{"colour":"yellow","make":"Volkswagen","model":"Passat","owner":"Max"}},
	{"Key":"CAR4", "Record":{"colour":"black","make":"Tesla","model":"S","owner":"Adriana"}},
	{"Key":"CAR5", "Record":{"colour":"purple","make":"Peugeot","model":"205","owner":"Michel"}},
	{"Key":"CAR6", "Record":{"colour":"white","make":"Chery","model":"S22L","owner":"Aarav"}},
	{"Key":"CAR7", "Record":{"colour":"violet","make":"Fiat","model":"Punto","owner":"Pari"}},
	{"Key":"CAR8", "Record":{"colour":"indigo","make":"Tata","model":"Nano","owner":"Valeria"}},
	{"Key":"CAR9", "Record":{"colour":"brown","make":"Holden","model":"Barina","owner":"Shotaro"}}]

有10个cars。Adriana拥有一辆黑色Tesla，型号为S，Brad拥有一辆红色福特野马，Pari的车是一辆紫色菲亚特Punto，等等。账本是基于键值对的，在我们的实现中，key从CAR0到CAR9。这在随后会变的十分重要。

让我们进一步查看该程序。使用一个编辑器（例如atom或visual studio）打开query.js。

应用程序的开始部分定义了一些特定的变量，例如channel名称，证书存储位置和网站端点。在我们的示例应用程序中，这些变量是内置的，但是在实际使用的应用程序中，这些变量应当由app dev指定。

	var channel = fabric_client.newChannel('mychannel');
	var peer = fabric_client.newPeer('grpc://localhost:7051');
	channel.addPeer(peer);
	
	var member_user = null;
	var store_path = path.join(__dirname, 'hfc-key-store');
	console.log('Store path:'+store_path);
	var tx_id = null;

这是我们构造查询的块：

	// queryCar chaincode function - requires 1 argument, ex: args: ['CAR4'],
	// queryAllCars chaincode function - requires no arguments , ex: args: [''],
	const request = {
	  //targets : --- letting this default to the peers assigned to the channel
	  chaincodeId: 'fabcar',
	  fcn: 'queryAllCars',
	  args: ['']
	};

当应用程序跑起来之后，它会调用peer上的fabcar chaincode，在不传参的前提下运行其内部的queryAllCars函数。

如果想看一下智能合约内部的可用函数，切换目录到fabric-samples根目录的chaincode/fabcar/go子目录，并且用编辑器打开fabcar.go。

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		在fabcar chaincode的Node.js版本中定义了这些相同的函数。
		</td>
	</tr>
</table>

你可以看到我们有如下函数可用：initLedger，queryCar，queryAllCars，createCar和changeCarOwner。

让我们进一步查看queryAllCars函数来探究它是如何与账本交互的。

	func (s *SmartContract) queryAllCars(APIstub shim.ChaincodeStubInterface) sc.Response {

	      startKey := "CAR0"
	      endKey := "CAR999"
	
	      resultsIterator, err := APIstub.GetStateByRange(startKey, endKey)

这里定义了queryAllCars的范围。CAR0和CAR999之间的所有car--一共1000辆car，假定每一个key都被恰当的标记了--都将被查询返回。

下面是关于一个应用程序如何调用chaincode中不同方法的说明。每个函数都必须根据chaincode shim接口中的可用API进行编码，这反过来又允许智能合同容器正确地与peer账本进行接口对接。

![](images/RunningtheSample.png)

我们能看见queryAllCars函数，以及createCar函数，该函数允许我们更新账本并最终将一个新的block追加到链上。

但是首先，回到query.js程序并编辑构造函数请求查询CAR4。我们通过改变query.js中的queryAllCars函数为queryCar函数来实现这一操作，并将CAR4作为特定的key。

Query.js程序应该看起来如下：

	const request = {
	  //targets : --- letting this default to the peers assigned to the channel
	  chaincodeId: 'fabcar',
	  fcn: 'queryCar',
	  args: ['CAR4']
	};

保存程序并返回fabcar目录。现在再次运行该程序：

	node query.js

你应该看到如下信息：

	{"colour":"black","make":"Tesla","model":"S","owner":"Adriana"}

如果您回过头来看一下我们之前查询每辆车的结果，您可以看到CAR4是Adriana的黑色Tesla，型号是S，这也是这里返回的结果。

使用queryCar函数，我们可以针对任何key（例如 CAR0）来查询并获得对应的car信息。

太好了。此时你应该熟悉了智能合约里的基础查询函数以及query程序里的各种参数。是时候更新账本了...

#####更新账本#####
我们已经完成了一些账本查询并增加了一些代码，现在是时候尝试更新账本了。Now that we’ve done a few ledger queries and added a bit of code, we’re ready to update the ledger. There are a lot of potential updates we could make, but let’s start by creating a car.

Below we can see how this process works. An update is proposed, endorsed, then returned to the application, which in turn sends it to be ordered and written to every peer’s ledger:

![](images/UpdatingtheLedger.png)

Our first update to the ledger will be to create a new car. We have a separate Javascript program – invoke.js – that we will use to make updates. Just as with queries, use an editor to open the program and navigate to the code block where we construct our invocation:

	// createCar chaincode function - requires 5 args, ex: args: ['CAR12', 'Honda', 'Accord', 'Black', 'Tom'],
	// changeCarOwner chaincode function - requires 2 args , ex: args: ['CAR10', 'Barry'],
	// must send the proposal to endorsing peers
	var request = {
	  //targets: let default to the peer assigned to the client
	  chaincodeId: 'fabcar',
	  fcn: '',
	  args: [''],
	  chainId: 'mychannel',
	  txId: tx_id
	};
You’ll see that we can call one of two functions – createCar or changeCarOwner. First, let’s create a red Chevy Volt and give it to an owner named Nick. We’re up to CAR9 on our ledger, so we’ll use CAR10 as the identifying key here. Edit this code block to look like this:

	var request = {
	  //targets: let default to the peer assigned to the client
	  chaincodeId: 'fabcar',
	  fcn: 'createCar',
	  args: ['CAR10', 'Chevy', 'Volt', 'Red', 'Nick'],
	  chainId: 'mychannel',
	  txId: tx_id
	};
Save it and run the program:

	node invoke.js
There will be some output in the terminal about ProposalResponse and promises. However, all we’re concerned with is this message:

	The transaction has been committed on peer localhost:7053
To see that this transaction has been written, go back to query.js and change the argument from CAR4 to CAR10.

In other words, change this:

	const request = {
	  //targets : --- letting this default to the peers assigned to the channel
	  chaincodeId: 'fabcar',
	  fcn: 'queryCar',
	  args: ['CAR4']
	};
To this:

	const request = {
	  //targets : --- letting this default to the peers assigned to the channel
	  chaincodeId: 'fabcar',
	  fcn: 'queryCar',
	  args: ['CAR10']
	};
Save once again, then query:

	node query.js
Which should return this:

	Response is  {"colour":"Red","make":"Chevy","model":"Volt","owner":"Nick"}
Congratulations. You’ve created a car!

So now that we’ve done that, let’s say that Nick is feeling generous and he wants to give his Chevy Volt to someone named Dave.

To do this go back to invoke.js and change the function from createCar to changeCarOwner and input the arguments like this:

	var request = {
	  //targets: let default to the peer assigned to the client
	  chaincodeId: 'fabcar',
	  fcn: 'changeCarOwner',
	  args: ['CAR10', 'Dave'],
	  chainId: 'mychannel',
	  txId: tx_id
	};
The first argument – CAR10 – reflects the car that will be changing owners. The second argument – Dave – defines the new owner of the car.

Save and execute the program again:

	node invoke.js
Now let’s query the ledger again and ensure that Dave is now associated with the CAR10 key:

	node query.js
It should return this result:

	Response is  {"colour":"Red","make":"Chevy","model":"Volt","owner":"Dave"}
The ownership of CAR10 has been changed from Nick to Dave.
<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		In a real world application the chaincode would likely have some access control logic. For example, only certain authorized users may create new cars, and only the car owner may transfer the car to somebody else.
		</td>
	</tr>
</table>
#####Summary#####
Now that we’ve done a few queries and a few updates, you should have a pretty good sense of how applications interact with the network. You’ve seen the basics of the roles smart contracts, APIs, and the SDK play in queries and updates and you should have a feel for how different kinds of applications could be used to perform other business tasks and operations.

In subsequent documents we’ll learn how to actually write a smart contract and how some of these more low level application functions can be leveraged (especially relating to identity and membership services).
#####Additional Resources#####
The Hyperledger Fabric Node SDK repo is an excellent resource for deeper documentation and sample code. You can also consult the Fabric community and component experts on Hyperledger Rocket Chat.

####Adding an Org to a Channel####
<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		Ensure that you have downloaded the appropriate images and binaries as outlined in Hyperledger Fabric Samples and Prerequisites that conform to the version of this documentation (which can be found at the bottom of the table of contents to the left). In particular, your version of the fabric-samples folder must include the eyfn.sh (“Extending Your First Network”) script and its related scripts.
		</td>
	</tr>
</table>
This tutorial serves as an extension to the Building Your First Network (BYFN) tutorial, and will demonstrate the addition of a new organization – Org3 – to the application channel (mychannel) autogenerated by BYFN. It assumes a strong understanding of BYFN, including the usage and functionality of the aforementioned utilities.

While we will focus solely on the integration of a new organization here, the same approach can be adopted when performing other channel configuration updates (updating modification policies or altering batch size, for example). To learn more about the process and possibilities of channel config updates in general, check out Updating a Channel Configuration). It’s also worth noting that channel configuration updates like the one demonstrated here will usually be the responsibility of an organization admin (rather than a chaincode or application developer).
<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		Make sure the automated byfn.sh script runs without error on your machine before continuing. If you have exported your binaries and the related tools (cryptogen, configtxgen, etc) into your PATH variable, you’ll be able to modify the commands accordingly without passing the fully qualified path.
		</td>
	</tr>
</table>
#####Setup the Environment#####
We will be operating from the root of the first-network subdirectory within your local clone of fabric-samples. Change into that directory now. You will also want to open a few extra terminals for ease of use.

First, use the byfn.sh script to tidy up. This command will kill any active or stale docker containers and remove previously generated artifacts. It is by no means necessary to bring down a Fabric network in order to perform channel configuration update tasks. However, for the sake of this tutorial, we want to operate from a known initial state. Therefore let’s run the following command to clean up any previous environments:

	./byfn.sh -m down
Now generate the default BYFN artifacts:

	./byfn.sh -m generate
And launch the network making use of the scripted execution within the CLI container:

	./byfn.sh -m up
Now that you have a clean version of BYFN running on your machine, you have two different paths you can pursue. First, we offer a fully commented script that will carry out a config transaction update to bring Org3 into the network.

Also, we will show a “manual” version of the same process, showing each step and explaining what it accomplishes (since we show you how to bring down your network before this manual process, you could also run the script and then look at each step).
#####Bring Org3 into the Channel with the Script#####
You should be in first-network. To use the script, simply issue the following:

	./eyfn.sh up
The output here is well worth reading. You’ll see the Org3 crypto material being added, the config update being created and signed, and then chaincode being installed to allow Org3 to execute ledger queries.

If everything goes well, you’ll get this message:

	========= All GOOD, EYFN test execution completed ===========
eyfn.sh can be used with the same Node.js chaincode and database options as byfn.sh by issuing the following (instead of ./byfn.sh -m -up):

	./byfn.sh up -c testchannel -s couchdb -l node
And then:

	./eyfn.sh up -c testchannel -s couchdb -l node
For those who want to take a closer look at this process, the rest of the doc will show you each command for making a channel update and what it does.
#####Bring Org3 into the Channel Manually#####
<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		The manual steps outlined below assume that the CORE_LOGGING_LEVEL in the cli and Org3cli` containers is set to DEBUG.
		<p>
		For the cli container, you can set this by modifying the docker-compose-cli.yaml file in the first-network directory. e.g.
		<p>
		cli:
		  container_name: cli
		  image: hyperledger/fabric-tools:$IMAGE_TAG
		  tty: true
		  stdin_open: true
		  environment:
		    - GOPATH=/opt/gopath
		    - CORE_VM_ENDPOINT=unix:///host/var/run/docker.sock
		    #- CORE_LOGGING_LEVEL=INFO
		    - CORE_LOGGING_LEVEL=DEBUG
		For the Org3cli container, you can set this by modifying the docker-compose-org3.yaml file in the first-network directory. e.g.
		<p>
		Org3cli:
		  container_name: Org3cli
		  image: hyperledger/fabric-tools:$IMAGE_TAG
		  tty: true
		  stdin_open: true
		  environment:
		    - GOPATH=/opt/gopath
		    - CORE_VM_ENDPOINT=unix:///host/var/run/docker.sock
		    #- CORE_LOGGING_LEVEL=INFO
		    - CORE_LOGGING_LEVEL=DEBUG
		</td>
	</tr>
</table>
If you’ve used the eyfn.sh script, you’ll need to bring your network down. This can be done by issuing:

	./eyfn.sh down
This will bring down the network, delete all the containers and undo what we’ve done to add Org3.

When the network is down, bring it back up again.

	./byfn.sh -m generate
Then:

	./byfn.sh -m up
This will bring your network back to the same state it was in before you executed the eyfn.sh script.

Now we’re ready to add Org3 manually. As a first step, we’ll need to generate Org3’s crypto material.
#####Generate the Org3 Crypto Material#####
In another terminal, change into the org3-artifacts subdirectory from first-network.

	cd org3-artifacts
There are two yaml files of interest here: org3-crypto.yaml and configtx.yaml. First, generate the crypto material for Org3:

	../../bin/cryptogen generate --config=./org3-crypto.yaml
This command reads in our new crypto yaml file – org3-crypto.yaml – and leverages cryptogen to generate the keys and certificates for an Org3 CA as well as two peers bound to this new Org. As with the BYFN implementation, this crypto material is put into a newly generated crypto-config folder within the present working directory (in our case, org3-artifacts).

Now use the configtxgen utility to print out the Org3-specific configuration material in JSON. We will preface the command by telling the tool to look in the current directory for the configtx.yaml file that it needs to ingest.

	export FABRIC_CFG_PATH=$PWD && ../../bin/configtxgen -printOrg Org3MSP > ../channel-artifacts/org3.json
The above command creates a JSON file – org3.json – and outputs it into the channel-artifacts subdirectory at the root of first-network. This file contains the policy definitions for Org3, as well as three important certificates presented in base 64 format: the admin user certificate (which will be needed to act as the admin of Org3 later on), a CA root cert, and a TLS root cert. In an upcoming step we will append this JSON file to the channel configuration.

Our final piece of housekeeping is to port the Orderer Org’s MSP material into the Org3 crypto-config directory. In particular, we are concerned with the Orderer’s TLS root cert, which will allow for secure communication between Org3 entities and the network’s ordering node.

	cd ../ && cp -r crypto-config/ordererOrganizations org3-artifacts/crypto-config/
Now we’re ready to update the channel configuration...
#####Prepare the CLI Environment#####
The update process makes use of the configuration translator tool – configtxlator. This tool provides a stateless REST API independent of the SDK. Additionally it provides a CLI, to simplify configuration tasks in Fabric networks. The tool allows for the easy conversion between different equivalent data representations/formats (in this case, between protobufs and JSON). Additionally, the tool can compute a configuration update transaction based on the differences between two channel configurations.

First, exec into the CLI container. Recall that this container has been mounted with the BYFN crypto-config library, giving us access to the MSP material for the two original peer organizations and the Orderer Org. The bootstrapped identity is the Org1 admin user, meaning that any steps where we want to act as Org2 will require the export of MSP-specific environment variables.

	docker exec -it cli bash
Now install the jq tool into the container. This tool allows script interactions with JSON files returned by the configtxlator tool:

	apt update && apt install -y jq
Export the ORDERER_CA and CHANNEL_NAME variables:

	export ORDERER_CA=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem  && export CHANNEL_NAME=mychannel
Check to make sure the variables have been properly set:

	echo $ORDERER_CA && echo $CHANNEL_NAME
<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		If for any reason you need to restart the CLI container, you will also need to re-export the two environment variables – ORDERER_CA and CHANNEL_NAME. The jq installation will persist. You need not install it a second time.
		</td>
	</tr>
</table>
#####Fetch the Configuration#####
Now we have a CLI container with our two key environment variables – ORDERER_CA and CHANNEL_NAME exported. Let’s go fetch the most recent config block for the channel – mychannel.

The reason why we have to pull the latest version of the config is because channel config elements are versioned.. Versioning is important for several reasons. It prevents config changes from being repeated or replayed (for instance, reverting to a channel config with old CRLs would represent a security risk). Also it helps ensure concurrency (if you want to remove an Org from your channel, for example, after a new Org has been added, versioning will help prevent you from removing both Orgs, instead of just the Org you want to remove).

	peer channel fetch config config_block.pb -o orderer.example.com:7050 -c $CHANNEL_NAME --tls --cafile $ORDERER_CA
This command saves the binary protobuf channel configuration block to config_block.pb. Note that the choice of name and file extension is arbitrary. However, following a convention which identifies both the type of object being represented and its encoding (protobuf or JSON) is recommended.

When you issued the peer channel fetch command, there was a decent amount of output in the terminal. The last line in the logs is of interest:

	2017-11-07 17:17:57.383 UTC [channelCmd] readBlock -> DEBU 011 Received block: 2
This is telling us that the most recent configuration block for mychannel is actually block 2, NOT the genesis block. By default, the peer channel fetch config command returns the most recent configuration block for the targeted channel, which in this case is the third block. This is because the BYFN script defined anchor peers for our two organizations – Org1 and Org2 – in two separate channel update transactions.

As a result, we have the following configuration sequence:

+ block 0: genesis block
+ block 1: Org1 anchor peer update
+ block 2: Org2 anchor peer update
#####Convert the Configuration to JSON and Trim It Down#####
Now we will make use of the configtxlator tool to decode this channel configuration block into JSON format (which can be read and modified by humans). We also must strip away all of the headers, metadata, creator signatures, and so on that are irrelevant to the change we want to make. We accomplish this by means of the jq tool:

	configtxlator proto_decode --input config_block.pb --type common.Block | jq .data.data[0].payload.data.config > config.json
This leaves us with a trimmed down JSON object – config.json, located in the fabric-samples folder inside first-network – which will serve as the baseline for our config update.

Take a moment to open this file inside your text editor of choice (or in your browser). Even after you’re done with this tutorial, it will be worth studying it as it reveals the underlying configuration structure and the other kind of channel updates that can be made. We discuss them in more detail in Updating a Channel Configuration.
#####Add the Org3 Crypto Material#####
<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		The steps you’ve taken up to this point will be nearly identical no matter what kind of config update you’re trying to make. We’ve chosen to add an org with this tutorial because it’s one of the most complex channel configuration updates you can attempt.
		</td>
	</tr>
</table>
We’ll use the jq tool once more to append the Org3 configuration definition – org3.json – to the channel’s application groups field, and name the output – modified_config.json.

	jq -s '.[0] * {"channel_group":{"groups":{"Application":{"groups": {"Org3MSP":.[1]}}}}}' config.json ./channel-artifacts/org3.json > modified_config.json
Now, within the CLI container we have two JSON files of interest – config.json and modified_config.json. The initial file contains only Org1 and Org2 material, whereas “modified” file contains all three Orgs. At this point it’s simply a matter of re-encoding these two JSON files and calculating the delta.

First, translate config.json back into a protobuf called config.pb:

	configtxlator proto_encode --input config.json --type common.Config --output config.pb
Next, encode modified_config.json to modified_config.pb:

	configtxlator proto_encode --input modified_config.json --type common.Config --output modified_config.pb
Now use configtxlator to calculate the delta between these two config protobufs. This command will output a new protobuf binary named org3_update.pb:

	configtxlator compute_update --channel_id $CHANNEL_NAME --original config.pb --updated modified_config.pb --output org3_update.pb
This new proto – org3_update.pb – contains the Org3 definitions and high level pointers to the Org1 and Org2 material. We are able to forgo the extensive MSP material and modification policy information for Org1 and Org2 because this data is already present within the channel’s genesis block. As such, we only need the delta between the two configurations.

Before submitting the channel update, we need to perform a few final steps. First, let’s decode this object into editable JSON format and call it org3_update.json:

	configtxlator proto_decode --input org3_update.pb --type common.ConfigUpdate | jq . > org3_update.json
Now, we have a decoded update file – org3_update.json – that we need to wrap in an envelope message. This step will give us back the header field that we stripped away earlier. We’ll name this file org3_update_in_envelope.json:

	echo '{"payload":{"header":{"channel_header":{"channel_id":"mychannel", "type":2}},"data":{"config_update":'$(cat org3_update.json)'}}}' | jq . > org3_update_in_envelope.json
Using our properly formed JSON – org3_update_in_envelope.json – we will leverage the configtxlator tool one last time and convert it into the fully fledged protobuf format that Fabric requires. We’ll name our final update object org3_update_in_envelope.pb:

	configtxlator proto_encode --input org3_update_in_envelope.json --type common.Envelope --output org3_update_in_envelope.pb
#####Sign and Submit the Config Update#####
Almost done!

We now have a protobuf binary – org3_update_in_envelope.pb – within our CLI container. However, we need signatures from the requisite Admin users before the config can be written to the ledger. The modification policy (mod_policy) for our channel Application group is set to the default of “MAJORITY”, which means that we need a majority of existing org admins to sign it. Because we have only two orgs – Org1 and Org2 – and the majority of two is two, we need both of them to sign. Without both signatures, the ordering service will reject the transaction for failing to fulfill the policy.

First, let’s sign this update proto as the Org1 Admin. Remember that the CLI container is bootstrapped with the Org1 MSP material, so we simply need to issue the peer channel signconfigtx command:

	peer channel signconfigtx -f org3_update_in_envelope.pb
The final step is to switch the CLI container’s identity to reflect the Org2 Admin user. We do this by exporting four environment variables specific to the Org2 MSP.
<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		Switching between organizations to sign a config transaction (or to do anything else) is not reflective of a real-world Fabric operation. A single container would never be mounted with an entire network’s crypto material. Rather, the config update would need to be securely passed out-of-band to an Org2 Admin for inspection and approval.
		</td>
	</tr>
</table>
Export the Org2 environment variables:

	# you can issue all of these commands at once

	export CORE_PEER_LOCALMSPID="Org2MSP"
	
	export CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org2.example.com/peers/peer0.org2.example.com/tls/ca.crt
	
	export CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org2.example.com/users/Admin@org2.example.com/msp
	
	export CORE_PEER_ADDRESS=peer0.org2.example.com:7051
Lastly, we will issue the peer channel update command. The Org2 Admin signature will be attached to this call so there is no need to manually sign the protobuf a second time:
<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		The upcoming update call to the ordering service will undergo a series of systematic signature and policy checks. As such you may find it useful to stream and inspect the ordering node’s logs. From another shell, issue a docker logs -f orderer.example.com command to display them.
		</td>
	</tr>
</table>
Send the update call:

	peer channel update -f org3_update_in_envelope.pb -c $CHANNEL_NAME -o orderer.example.com:7050 --tls --cafile $ORDERER_CA
You should see a message digest indication similar to the following if your update has been submitted successfully:

	2018-02-24 18:56:33.499 UTC [msp/identity] Sign -> DEBU 00f Sign: digest: 3207B24E40DE2FAB87A2E42BC004FEAA1E6FDCA42977CB78C64F05A88E556ABA
You will also see the submission of our configuration transaction:

	2018-02-24 18:56:33.499 UTC [channelCmd] update -> INFO 010 Successfully submitted channel update
The successful channel update call returns a new block – block 5 – to all of the peers on the channel. If you remember, blocks 0-2 are the initial channel configurations while blocks 3 and 4 are the instantiation and invocation of the mycc chaincode. As such, block 5 serves as the most recent channel configuration with Org3 now defined on the channel.

Inspect the logs for peer0.org1.example.com:

	docker logs -f peer0.org1.example.com
Follow the demonstrated process to fetch and decode the new config block if you wish to inspect its contents.
#####Configuring Leader Election#####
<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		This section is included as a general reference for understanding the leader election settings when adding organizations to a network after the initial channel configuration has completed. This sample defaults to dynamic leader election, which is set for all peers in the network in peer-base.yaml.
		</td>
	</tr>
</table>
Newly joining peers are bootstrapped with the genesis block, which does not contain information about the organization that is being added in the channel configuration update. Therefore new peers are not able to utilize gossip as they cannot verify blocks forwarded by other peers from their own organization until they get the configuration transaction which added the organization to the channel. Newly added peers must therefore have one of the following configurations so that they receive blocks from the ordering service:

1. To utilize static leader mode, configure the peer to be an organization leader:

	CORE_PEER_GOSSIP_USELEADERELECTION=false
	CORE_PEER_GOSSIP_ORGLEADER=true

	<table>
		<tr>
			<td bgcolor=#6A5ACD>
				<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
			</td>
		</tr>
		<tr>
			<td bgcolor=#7FFFD4>
			This configuration must be the same for all new peers added to the channel.
			</td>
		</tr>
	</table>
2. To utilize dynamic leader election, configure the peer to use leader election:

	CORE_PEER_GOSSIP_USELEADERELECTION=true
	CORE_PEER_GOSSIP_ORGLEADER=false

	<table>
		<tr>
			<td bgcolor=#6A5ACD>
				<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
			</td>
		</tr>
		<tr>
			<td bgcolor=#7FFFD4>
			Because peers of the newly added organization won’t be able to form membership view, this option will be similar to the static configuration, as each peer will start proclaiming itself to be a leader. However, once they get updated with the configuration transaction that adds the organization to the channel, there will be only one active leader for the organization. Therefore, it is recommended to leverage this option if you eventually want the organization’s peers to utilize leader election.
			</td>
		</tr>
	</table>
#####Join Org3 to the Channel#####
At this point, the channel configuration has been updated to include our new organization – Org3 – meaning that peers attached to it can now join mychannel.

First, let’s launch the containers for the Org3 peers and an Org3-specific CLI.

Open a new terminal and from first-network kick off the Org3 docker compose:

	docker-compose -f docker-compose-org3.yaml up -d
This new compose file has been configured to bridge across our initial network, so the two peers and the CLI container will be able to resolve with the existing peers and ordering node. With the three new containers now running, exec into the Org3-specific CLI container:

	docker exec -it Org3cli bash
Just as we did with the initial CLI container, export the two key environment variables: ORDERER_CA and CHANNEL_NAME:

	export ORDERER_CA=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem && export CHANNEL_NAME=mychannel
Check to make sure the variables have been properly set:

	echo $ORDERER_CA && echo $CHANNEL_NAME
Now let’s send a call to the ordering service asking for the genesis block of mychannel. The ordering service is able to verify the Org3 signature attached to this call as a result of our successful channel update. If Org3 has not been successfully appended to the channel config, the ordering service should reject this request.
<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		Again, you may find it useful to stream the ordering node’s logs to reveal the sign/verify logic and policy checks.
		</td>
	</tr>
</table>
Use the peer channel fetch command to retrieve this block:

	peer channel fetch 0 mychannel.block -o orderer.example.com:7050 -c $CHANNEL_NAME --tls --cafile $ORDERER_CA
Notice, that we are passing a 0 to indicate that we want the first block on the channel’s ledger (i.e. the genesis block). If we simply passed the peer channel fetch config command, then we would have received block 5 – the updated config with Org3 defined. However, we can’t begin our ledger with a downstream block – we must start with block 0.

Issue the peer channel join command and pass in the genesis block – mychannel.block:

	peer channel join -b mychannel.block
If you want to join the second peer for Org3, export the TLS and ADDRESS variables and reissue the peer channel join command:

	export CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org3.example.com/peers/peer1.org3.example.com/tls/ca.crt && export CORE_PEER_ADDRESS=peer1.org3.example.com:7051

	peer channel join -b mychannel.block
#####Upgrade and Invoke Chaincode#####
The final piece of the puzzle is to increment the chaincode version and update the endorsement policy to include Org3. Since we know that an upgrade is coming, we can forgo the futile exercise of installing version 1 of the chaincode. We are solely concerned with the new version where Org3 will be part of the endorsement policy, therefore we’ll jump directly to version 2 of the chaincode.

From the Org3 CLI:

	peer chaincode install -n mycc -v 2.0 -p github.com/chaincode/chaincode_example02/go/
Modify the environment variables accordingly and reissue the command if you want to install the chaincode on the second peer of Org3. Note that a second installation is not mandated, as you only need to install chaincode on peers that are going to serve as endorsers or otherwise interface with the ledger (i.e. query only). Peers will still run the validation logic and serve as committers without a running chaincode container.

Now jump back to the original CLI container and install the new version on the Org1 and Org2 peers. We submitted the channel update call with the Org2 admin identity, so the container is still acting on behalf of peer0.org2:

	peer chaincode install -n mycc -v 2.0 -p github.com/chaincode/chaincode_example02/go/
Flip to the peer0.org1 identity:

	export CORE_PEER_LOCALMSPID="Org1MSP"

	export CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/ca.crt
	
	export CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.example.com/users/Admin@org1.example.com/msp
	
	export CORE_PEER_ADDRESS=peer0.org1.example.com:7051
And install again:

	peer chaincode install -n mycc -v 2.0 -p github.com/chaincode/chaincode_example02/go/
Now we’re ready to upgrade the chaincode. There have been no modifications to the underlying source code, we are simply adding Org3 to the endorsement policy for a chaincode – mycc – on mychannel.
<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		Any identity satisfying the chaincode’s instantiation policy can issue the upgrade call. By default, these identities are the channel Admins.
		</td>
	</tr>
</table>
Send the call:

	peer chaincode upgrade -o orderer.example.com:7050 --tls $CORE_PEER_TLS_ENABLED --cafile $ORDERER_CA -C $CHANNEL_NAME -n mycc -v 2.0 -c '{"Args":["init","a","90","b","210"]}' -P "OR ('Org1MSP.peer','Org2MSP.peer','Org3MSP.peer')"
You can see in the above command that we are specifying our new version by means of the v flag. You can also see that the endorsement policy has been modified to -P "OR ('Org1MSP.peer','Org2MSP.peer','Org3MSP.peer')", reflecting the addition of Org3 to the policy. The final area of interest is our constructor request (specified with the c flag).

As with an instantiate call, a chaincode upgrade requires usage of the init method. If your chaincode requires arguments be passed to the init method, then you will need to do so here.

The upgrade call adds a new block – block 6 – to the channel’s ledger and allows for the Org3 peers to execute transactions during the endorsement phase. Hop back to the Org3 CLI container and issue a query for the value of a. This will take a bit of time because a chaincode image needs to be built for the targeted peer, and the container needs to start:

	peer chaincode query -C $CHANNEL_NAME -n mycc -c '{"Args":["query","a"]}'
We should see a response of Query Result: 90.

Now issue an invocation to move 10 from a to b:

	peer chaincode invoke -o orderer.example.com:7050  --tls $CORE_PEER_TLS_ENABLED --cafile $ORDERER_CA -C $CHANNEL_NAME -n mycc -c '{"Args":["invoke","a","b","10"]}'
Query one final time:

	peer chaincode query -C $CHANNEL_NAME -n mycc -c '{"Args":["query","a"]}'
We should see a response of Query Result: 80, accurately reflecting the update of this chaincode’s world state.
#####Conclusion#####
The channel configuration update process is indeed quite involved, but there is a logical method to the various steps. The endgame is to form a delta transaction object represented in protobuf binary format and then acquire the requisite number of admin signatures such that the channel configuration update transaction fulfills the channel’s modification policy.

The configtxlator and jq tools, along with the ever-growing peer channel commands, provide us with the functionality to accomplish this task.

####Upgrading Your Network Components####
<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		When we use the term “upgrade” in this documentation, we’re primarily referring to changing the version of a component (for example, going from a v1.0.x binary to a v1.1 binary). The term “update,” on the other hand, refers not to versions but to configuration changes, such as updating a channel configuration or a deployment script.
		</td>
	</tr>
</table>
#####Overview#####
Because the Building Your First Network (BYFN) tutorial defaults to the “latest” binaries, if you have run it since the release of v1.1, your machine will have v1.1 binaries and tools installed on it and you will not be able to upgrade them.

As a result, this tutorial will provide a network based on Hyperledger Fabric v1.0.6 binaries as well as the v1.1 binaries you will be upgrading to. In addition, we will show how to update channel configurations to recognize Capability Requirements.

However, because BYFN does not support the following components, our script for upgrading BYFN will not cover them:

+ Fabric-CA
+ Kafka
+ SDK

The process for upgrading these components will be covered in a section following the tutorial.

At a high level, our upgrade tutorial will perform the following steps:
	1. Back up the ledger and MSPs.
	2. Upgrade the orderer binaries to Fabric v1.1.
	3. Upgrade the peer binaries to Fabric v1.1.
	4. Enable v1.1 channel capability requirements.
<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		In production environments, the orderers and peers can be upgraded on a rolling basis simultaneously (in other words, you don’t need to upgrade your orderers before upgrading your peers). Where extra care must be taken is in enabling capabilities. All of the orderers and peers must be upgraded before that step (if only some orderers have been upgraded when capabilities have been enabled, a catastrophic state fork can be created).
		</td>
	</tr>
</table>
This tutorial will demonstrate how to perform each of these steps individually with CLI commands.
######Prerequisites######
If you haven’t already done so, ensure you have all of the dependencies on your machine as described in Prerequisites.
######Launch a v1.0.6 Network######
To begin, we will provision a basic network running Fabric v1.0.6 images. This network will consist of two organizations, each maintaining two peer nodes, and a “solo” ordering service.

We will be operating from the first-network subdirectory within your local clone of fabric-samples. Change into that directory now. You will also want to open a few extra terminals for ease of use.
######Clean up######
We want to operate from a known state, so we will use the byfn.sh script to initially tidy up. This command will kill any active or stale docker containers and remove any previously generated artifacts. Run the following command:

	./byfn.sh -m down
######Generate the Crypto and Bring Up the Network######
With a clean environment, launch our v1.0.6 BYFN network using these four commands:

	git fetch origin

	git checkout v1.0.6
	
	./byfn.sh -m generate
	
	./byfn.sh -m up -t 3000 -i 1.0.6
<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		If you have locally built v1.0.6 images, then they will be used by the example. If you get errors, consider cleaning up v1.0.6 images and running the example again. This will download 1.0.6 images from docker hub.
		</td>
	</tr>
</table>
If BYFN has launched properly, you will see:

	===================== All GOOD, BYFN execution completed =====================
We are now ready to upgrade our network to Hyperledger Fabric v1.1.
######Get the newest samples######
<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		The instructions below pertain to whatever is the most recently published version of v1.1.x, starting with 1.1.0-rc1. Please substitute ‘1.1.x’ with the version identifier of the published release that you are testing. e.g. replace ‘v1.1.x’ with ‘v1.1.0’.
		</td>
	</tr>
</table>
Before completing the rest of the tutorial, it’s important to get the v1.1.x version of the samples, you can do this by:

	git fetch origin

	git checkout v1.1.x
######Want to upgrade now?######
We have a script that will upgrade all of the components in BYFN as well as enabling capabilities. Afterwards, we will walk you through the steps in the script and describe what each piece of code is doing in the upgrade process.

To run the script, issue these commands:

	# Note, replace '1.1.x' with a specific version, for example '1.1.0'.
	# Don't pass the image flag '-i 1.1.x' if you prefer to default to 'latest' images.
	
	./byfn.sh upgrade -i 1.1.x
If the upgrade is successful, you should see the following:

	===================== All GOOD, End-2-End UPGRADE Scenario execution completed =====================
if you want to upgrade the network manually, simply run ./byfn.sh -m down again and perform the steps up to – but not including – ./byfn.sh upgrade -i 1.1.x. Then proceed to the next section.
<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		Many of the commands you’ll run in this section will not result in any output. In general, assume no output is good output.
		</td>
	</tr>
</table>
######Upgrade the Orderer Containers######
<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		Pay CLOSE attention to your orderer upgrades. If they are not done correctly – specifically, if only some orderers are upgraded and not others – a state fork could be created (meaning, ledgers would no longer be consistent). This MUST be avoided.
		</td>
	</tr>
</table>
Orderer containers should be upgraded in a rolling fashion (one at a time). At a high level, the orderer upgrade process goes as follows:

1. Stop the orderer.
2. Back up the orderer’s ledger and MSP.
3. Restart the orderer with the latest images.
4. Verify upgrade completion.

As a consequence of leveraging BYFN, we have a solo orderer setup, therefore, we will only perform this process once. In a Kafka setup, however, this process will have to be performed for each orderer.
<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		This tutorial uses a docker deployment. For native deployments, replace the file orderer with the one from the release artifacts. Backup the orderer.yaml and replace it with the orderer.yaml file from the release artifacts. Then port any modified variables from the backed up orderer.yaml to the new one. Utilizing a utility like diff may be helpful. To decrease confusion, the variable General.TLS.ClientAuthEnabled has been renamed to General.TLS.ClientAuthRequired (just as it is specified in the peer configuration.). If the old name for this variable is still present in the orderer.yaml file, the new orderer binary will fail to start.
		</td>
	</tr>
</table>
Let’s begin the upgrade process by bringing down the orderer:

	docker stop orderer.example.com

	export LEDGERS_BACKUP=./ledgers-backup
	
	# Note, replace '1.1.x' with a specific version, for example '1.1.0'.
	# Set IMAGE_TAG to 'latest' if you prefer to default to the images tagged 'latest' on your system.
	
	export IMAGE_TAG=`uname -m`-1.1.x

We have created a variable for a directory to put file backups into, and exported the IMAGE_TAG we’d like to move to.

Once the orderer is down, you’ll want to backup its ledger and MSP:

	mkdir -p $LEDGERS_BACKUP

	docker cp orderer.example.com:/var/hyperledger/production/orderer/ ./$LEDGERS_BACKUP/orderer.example.com

In a production network this process would be repeated for each of the Kafka-based orderers in a rolling fashion.

Now download and restart the orderer with our new fabric image:

	docker-compose -f docker-compose-cli.yaml up -d --no-deps orderer.example.com
Because our sample uses a “solo” ordering service, there are no other orderers in the network that the restarted orderer must sync up to. However, in a production network leveraging Kafka, it will be a best practice to issue peer channel fetch <blocknumber> after restarting the orderer to verify that it has caught up to the other orderers.
######Upgrade the Peer Containers######
Next, let’s look at how to upgrade peer containers to Fabric v1.1. Peer containers should, like the orderers, be upgraded in a rolling fashion (one at a time). As mentioned during the orderer upgrade, orderers and peers may be upgraded in parallel, but for the purposes of this tutorial we’ve separated the processes out. At a high level, we will perform the following steps:

1. Stop the peer.
2. Back up the peer’s ledger and MSP.
3. Remove chaincode containers and images.
4. Restart the peer with with latest image.
5. Verify upgrade completion.

We have four peers running in our network. We will perform this process once for each peer, totaling four upgrades.

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		Again, this tutorial utilizes a docker deployment. For native deployments, replace the file peer with the one from the release artifacts. Backup your core.yaml and replace it with the one from the release artifacts. Port any modified variables from the backed up core.yaml to the new one. Utilizing a utility like diff may be helpful.
		</td>
	</tr>
</table>

Let’s bring down the first peer with the following command:

	export PEER=peer0.org1.example.com

	docker stop $PEER
We can then backup the peer’s ledger and MSP:

	mkdir -p $LEDGERS_BACKUP

	docker cp $PEER:/var/hyperledger/production ./$LEDGERS_BACKUP/$PEER
With the peer stopped and the ledger backed up, remove the peer chaincode containers:

	CC_CONTAINERS=$(docker ps | grep dev-$PEER | awk '{print $1}')
	if [ -n "$CC_CONTAINERS" ] ; then docker rm -f $CC_CONTAINERS ; fi
And the peer chaincode images:

	CC_IMAGES=$(docker images | grep dev-$PEER | awk '{print $1}')
	if [ -n "$CC_IMAGES" ] ; then docker rmi -f $CC_IMAGES ; fi
Now we’ll re-launch the peer using the v1.1 image tag:

	docker-compose -f docker-compose-cli.yaml up -d --no-deps $PEER
<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		Although, BYFN supports using CouchDB, we opted for a simpler implementation in this tutorial. If you are using CouchDB, however, follow the instructions in the Upgrading CouchDB section below at this time and then issue this command instead of the one above:
		</td>
	</tr>
</table>

	docker-compose -f docker-compose-cli.yaml -f docker-compose-couch.yaml up -d --no-deps $PEER
We’ll talk more generally about how to update CouchDB after the tutorial.
######Verify Upgrade Completion######
We’ve completed the upgrade for our first peer, but before we move on let’s check to ensure the upgrade has been completed properly with a chaincode invoke. Let’s move 10 from a to b using these commands:

	docker-compose -f docker-compose-cli.yaml up -d --no-deps cli

	docker exec -it cli bash
	
	peer chaincode invoke -o orderer.example.com:7050  --tls --cafile /opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem  -C mychannel -n mycc -c '{"Args":["invoke","a","b","10"]}'
Our query earlier revealed a to have a value of 90 and we have just removed 10 with our invoke. Therefore, a query against a should reveal 80. Let’s see:

	peer chaincode query -C mychannel -n mycc -c '{"Args":["query","a"]}'
We should see the following:

	Query Result: 80
After verifying the peer was upgraded correctly, make sure to issue an exit to leave the container before continuing to upgrade your peers. You can do this by repeating the process above with a different peer name exported.

	export PEER=peer1.org1.example.com
	export PEER=peer0.org2.example.com
	export PEER=peer1.org2.example.com

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		All peers must be upgraded BEFORE enabling capabilities.
		</td>
	</tr>
</table>
######Enable Capabilities for the Channels######
Because v1.0.x Fabric binaries do not understand the concept of channel capabilities, extra care must be taken when initially enabling capabilities for a channel.

Although Fabric binaries can and should be upgraded in a rolling fashion, it is critical that the ordering admins not attempt to enable v1.1 capabilities until all orderer binaries are at v1.1.x+. If any orderer is executing v1.0.x code, and capabilities are enabled for a channel, the blockchain will fork as v1.0.x orderers invalidate the change and v1.1.x+ orderers accept it. This is an exception for the v1.0 to v1.1 upgrade. For future upgrades, such as v1.1 to v1.2, the ordering network will handle the upgrade more gracefully and prevent the state fork.

In order to minimize the chance of a fork, attempts to enable the application or channel v1.1 capabilities before enabling the orderer v1.1 capability will be rejected. Since the orderer v1.1 capability can only be enabled by the ordering admins, making it a prerequisite for the other capabilities prevents application admins from accidentally enabling capabilities before the orderer is ready to support them.

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		Once a capability has been enabled, disabling it is not recommended or supported.
		</td>
	</tr>
</table>

Once a capability has been enabled, it becomes part of the permanent record for that channel. This means that even after disabling the capability, old binaries will not be able to participate in the channel because they cannot process beyond the block which enabled the capability to get to the block which disables it.

For this reason, think of enabling channel capabilities as a point of no return. Please experiment with the new capabilities in a test setting and be confident before proceeding to enable them in production.

Note that enabling capability requirements on a channel which a v1.0.0 peer is joined to will result in a crash of the peer. This crashing behavior is deliberate because it indicates a misconfiguration which might result in a state fork.

The error message displayed by failing v1.0.x peers will say:

	Cannot commit block to the ledger due to Error validating config which passed
	initial validity checks: ConfigEnvelope LastUpdate did not produce the supplied
	config result

We will enable capabilities in the following order:

1. Orderer System Channel

	a. Orderer Group
	b. Channel Group
2. Individual Channels
	a. Orderer Group
	b. Channel Group
	c. Application Group

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		In order to minimize the chance of a fork a best practice is to enable the orderer system capability first and then enable individual channel capabilities.
		</td>
	</tr>
</table>
For each group, we will enable the capabilities in the following order:

1. Get the latest channel config
2. Create a modified channel config
3. Create a config update transaction

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		This process will be accomplished through a series of config update transactions, one for each channel group. In a real world production network, these channel config updates would be handled by the admins for each channel. Because BYFN all exists on a single machine, it is possible for us to update each of these channels.
		</td>
	</tr>
</table>

For more information on updating channel configs, click on Adding an Org to a Channel or the doc on Updating a Channel Configuration.

Get back into the cli container by reissuing docker exec -it cli bash.

Now let’s check the set environment variables with:

	env|grep PEER
You’ll also need to install jq:

	apt-get update

	apt-get install -y jq
######Orderer System Channel Capabilities######
Let’s set our environment variables for the orderer system channel. Issue each of these commands:

	CORE_PEER_LOCALMSPID="OrdererMSP"

	CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem
	
	CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/ordererOrganizations/example.com/users/Admin@example.com/msp
	
	ORDERER_CA=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem
And let’s set our channel name to testchainid:

	CH_NAME=testchainid
######Orderer Group######
The first step in updating a channel configuration is getting the latest config block:

	peer channel fetch config config_block.pb -o orderer.example.com:7050 -c $CH_NAME  --tls --cafile $ORDERER_CA
<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		We require configtxlator v1.0.0 or higher for this next step.
		</td>
	</tr>
</table>
To make our config easy to edit, let’s convert the config block to JSON using configtxlator:

	configtxlator proto_decode --input config_block.pb --type common.Block --output config_block.json
This command uses jq to remove the headers, metadata, and signatures from the config:

	jq .data.data[0].payload.data.config config_block.json > config.json
Next, add capabilities to the orderer group. The following command will create a copy of the config file and add our new capabilities to it:

	jq -s '.[0] * {"channel_group":{"groups":{"Orderer": {"values": {"Capabilities": .[1]}}}}}' config.json ./scripts/capabilities.json > modified_config.json
Note what we’re changing here: Capabilities are being added as a value of the orderer group under channel_group. The specific channel we’re working in is not noted in this command, but recall that it’s the orderer system channel testchainid. It should be updated first because it is this channel’s configuration that will be copied by default during the creation of any new channel.

Now we can create the config update:

	configtxlator proto_encode --input config.json --type common.Config --output config.pb

	configtxlator proto_encode --input modified_config.json --type common.Config --output modified_config.pb
	
	configtxlator compute_update --channel_id $CH_NAME --original config.pb --updated modified_config.pb --output config_update.pb
Package the config update into a transaction:

	configtxlator proto_decode --input config_update.pb --type common.ConfigUpdate --output config_update.json

	echo '{"payload":{"header":{"channel_header":{"channel_id":"'$CH_NAME'", "type":2}},"data":{"config_update":'$(cat config_update.json)'}}}' | jq . > config_update_in_envelope.json
	
	configtxlator proto_encode --input config_update_in_envelope.json --type common.Envelope --output config_update_in_envelope.pb
Submit the config update transaction:

	<table>
		<tr>
			<td bgcolor=#6A5ACD>
				<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
			</td>
		</tr>
		<tr>
			<td bgcolor=#7FFFD4>
			The command below both signs and submits the transaction to the ordering service.
			</td>
		</tr>
	</table>
	peer channel update -f config_update_in_envelope.pb -c $CH_NAME -o orderer.example.com:7050 --tls true --cafile $ORDERER_CA
Our config update transaction represents the difference between the original config and the modified one, but the orderer will translate this into a full channel config.
######Channel Group######
Now let’s move on to enabling capabilities for the channel group at the orderer system level.

The first step, as before, is to get the latest channel configuration.

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		This set of commands is exactly the same as the steps from the orderer group.
		</td>
	</tr>
</table>

	peer channel fetch config config_block.pb -o orderer.example.com:7050 -c $CH_NAME --tls --cafile $ORDERER_CA

	configtxlator proto_decode --input config_block.pb --type common.Block --output config_block.json
	
	jq .data.data[0].payload.data.config config_block.json > config.json
Next, create a modified channel config:

	jq -s '.[0] * {"channel_group":{"values": {"Capabilities": .[1]}}}' config.json ./scripts/capabilities.json > modified_config.json
Note what we’re changing here: Capabilities are being added as a value of the top level channel_group (in the testchainid channel, as before).

Create the config update transaction:

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		This set of commands is exactly the same as the third step from the orderer group.
		</td>
	</tr>
</table>

	configtxlator proto_encode --input config.json --type common.Config --output config.pb

	configtxlator proto_encode --input modified_config.json --type common.Config --output modified_config.pb
	
	configtxlator compute_update --channel_id $CH_NAME --original config.pb --updated modified_config.pb --output config_update.pb
Package the config update into a transaction:

	configtxlator proto_decode --input config_update.pb --type common.ConfigUpdate --output config_update.json

	echo '{"payload":{"header":{"channel_header":{"channel_id":"'$CH_NAME'", "type":2}},"data":{"config_update":'$(cat config_update.json)'}}}' | jq . > config_update_in_envelope.json
	
	configtxlator proto_encode --input config_update_in_envelope.json --type common.Envelope --output config_update_in_envelope.pb
Submit the config update transaction:

	peer channel update -f config_update_in_envelope.pb -c $CH_NAME -o orderer.example.com:7050 --tls true --cafile $ORDERER_CA
######Enabling Capabilities on Existing Channels######
Set the channel name to mychannel:

	CH_NAME=mychannel
#######Orderer Group#######
Get the channel config:

	peer channel fetch config config_block.pb -o orderer.example.com:7050 -c $CH_NAME  --tls --cafile $ORDERER_CA

	configtxlator proto_decode --input config_block.pb --type common.Block --output config_block.json
	
	jq .data.data[0].payload.data.config config_block.json > config.json
Let’s add capabilities to the orderer group. The following command will create a copy of the config file and add our new capabilities to it:

	jq -s '.[0] * {"channel_group":{"groups":{"Orderer": {"values": {"Capabilities": .[1]}}}}}' config.json ./scripts/capabilities.json > modified_config.json
Note what we’re changing here: Capabilities are being added as a value of the orderer group under channel_group. This is exactly what we changed before, only now we’re working with the config to the channel mychannel instead of testchainid.

Create the config update:

	configtxlator proto_encode --input config.json --type common.Config --output config.pb

	configtxlator proto_encode --input modified_config.json --type common.Config --output modified_config.pb
	
	configtxlator compute_update --channel_id $CH_NAME --original config.pb --updated modified_config.pb --output config_update.pb
Package the config update into a transaction:

	configtxlator proto_decode --input config_update.pb --type common.ConfigUpdate --output config_update.json

	echo '{"payload":{"header":{"channel_header":{"channel_id":"'$CH_NAME'", "type":2}},"data":{"config_update":'$(cat config_update.json)'}}}' | jq . > config_update_in_envelope.json
	
	configtxlator proto_encode --input config_update_in_envelope.json --type common.Envelope --output config_update_in_envelope.pb
Submit the config update transaction:

	peer channel update -f config_update_in_envelope.pb -c $CH_NAME -o orderer.example.com:7050 --tls true --cafile $ORDERER_CA
#######Channel Group#######
<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		While this may seem repetitive, remember that we’re performing the same process on different groups. In a production network, as we’ve said, this process would likely be split up among the various channel admins.
		</td>
	</tr>
</table>
Fetch, decode, and scope the config:

	peer channel fetch config config_block.pb -o orderer.example.com:7050 -c $CH_NAME --tls --cafile $ORDERER_CA

	configtxlator proto_decode --input config_block.pb --type common.Block --output config_block.json
	
	jq .data.data[0].payload.data.config config_block.json > config.json
Create a modified config:

	jq -s '.[0] * {"channel_group":{"values": {"Capabilities": .[1]}}}' config.json ./scripts/capabilities.json > modified_config.json
Note what we’re changing here: Capabilities are being added as a value of the top level channel_group (in mychannel, as before).

Create the config update:

	configtxlator proto_encode --input config.json --type common.Config --output config.pb

	configtxlator proto_encode --input modified_config.json --type common.Config --output modified_config.pb
	
	configtxlator compute_update --channel_id $CH_NAME --original config.pb --updated modified_config.pb --output config_update.pb
Package the config update into a transaction:

	configtxlator proto_decode --input config_update.pb --type common.ConfigUpdate --output config_update.json

	echo '{"payload":{"header":{"channel_header":{"channel_id":"'$CH_NAME'", "type":2}},"data":{"config_update":'$(cat config_update.json)'}}}' | jq . > config_update_in_envelope.json
	
	configtxlator proto_encode --input config_update_in_envelope.json --type common.Envelope --output config_update_in_envelope.pb
Because we’re updating the config of the channel group, the relevant orgs – Org1, Org2, and the OrdererOrg – need to sign it. This task would usually be performed by the individual org admins, but in BYFN, as we’ve said, this task falls to us.

First, switch into Org1 and sign the update:

	CORE_PEER_LOCALMSPID="Org1MSP"

	CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/ca.crt
	
	CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.example.com/users/Admin@org1.example.com/msp
	
	CORE_PEER_ADDRESS=peer0.org1.example.com:7051
	
	peer channel signconfigtx -f config_update_in_envelope.pb
And do the same as Org2:

	CORE_PEER_LOCALMSPID="Org2MSP"

	CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org2.example.com/peers/peer0.org2.example.com/tls/ca.crt
	
	CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org2.example.com/users/Admin@org2.example.com/msp
	
	CORE_PEER_ADDRESS=peer0.org1.example.com:7051
	
	peer channel signconfigtx -f config_update_in_envelope.pb
And as the OrdererOrg:

	CORE_PEER_LOCALMSPID="OrdererMSP"

	CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem
	
	CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/ordererOrganizations/example.com/users/Admin@example.com/msp
	
	peer channel update -f config_update_in_envelope.pb -c $CH_NAME -o orderer.example.com:7050 --tls true --cafile $ORDERER_CA
#######Application Group#######
For the application group, we will need to reset the environment variables as one organization:

	CORE_PEER_LOCALMSPID="Org1MSP"

	CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/ca.crt
	
	CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org1.example.com/users/Admin@org1.example.com/msp
	
	CORE_PEER_ADDRESS=peer0.org1.example.com:7051
Now, get the latest channel config (this process should be very familiar by now):

	peer channel fetch config config_block.pb -o orderer.example.com:7050 -c $CH_NAME --tls --cafile $ORDERER_CA

	configtxlator proto_decode --input config_block.pb --type common.Block --output config_block.json
	
	jq .data.data[0].payload.data.config config_block.json > config.json
Create a modified channel config:

	jq -s '.[0] * {"channel_group":{"groups":{"Application": {"values": {"Capabilities": .[1]}}}}}' config.json ./scripts/capabilities.json > modified_config.json
Note what we’re changing here: Capabilities are being added as a value of the Application group under channel_group (in mychannel).

Create a config update transaction:

	configtxlator proto_encode --input config.json --type common.Config --output config.pb

	configtxlator proto_encode --input modified_config.json --type common.Config --output modified_config.pb
	
	configtxlator compute_update --channel_id $CH_NAME --original config.pb --updated modified_config.pb --output config_update.pb
Package the config update into a transaction:

	configtxlator proto_decode --input config_update.pb --type common.ConfigUpdate --output config_update.json

	echo '{"payload":{"header":{"channel_header":{"channel_id":"'$CH_NAME'", "type":2}},"data":{"config_update":'$(cat config_update.json)'}}}' | jq . > config_update_in_envelope.json
	
	configtxlator proto_encode --input config_update_in_envelope.json --type common.Envelope --output config_update_in_envelope.pb
Org1 signs the transaction:

	peer channel signconfigtx -f config_update_in_envelope.pb
Set the environment variables as Org2:

	export CORE_PEER_LOCALMSPID="Org2MSP"

	export CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org2.example.com/peers/peer0.org2.example.com/tls/ca.crt
	
	export CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org2.example.com/users/Admin@org2.example.com/msp
	
	export CORE_PEER_ADDRESS=peer0.org2.example.com:7051
Org2 submits the config update transaction with its signature:

	peer channel update -f config_update_in_envelope.pb -c $CH_NAME -o orderer.example.com:7050 --tls true --cafile $ORDERER_CA
Congratulations! You have now enabled capabilities on all of your channels.
#######Verify that Capabilities are Enabled#######
But let’s test just to make sure by moving 10 from a to b, as before:

	peer chaincode invoke -o orderer.example.com:7050  --tls --cafile /opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem  -C mychannel -n mycc -c '{"Args":["invoke","a","b","10"]}'
And then querying the value of a, which should reveal a value of 70. Let’s see:

	peer chaincode query -C mychannel -n mycc -c '{"Args":["query","a"]}'
We should see the following:

	Query Result: 70

In which case we have successfully added capabilities to all of our channels.

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		Although all peer binaries in the network should have been upgraded prior to this point, enabling capability requirements on a channel which a v1.0.0 peer is joined to will result in a crash of the peer. This crashing behavior is deliberate because it indicates a misconfiguration which might result in a state fork.
		</td>
	</tr>
</table>
######Upgrading Components BYFN Does Not Support######
Although this is the end of our update tutorial, there are other components that exist in production networks that are not supported by the BYFN sample. In this section, we’ll talk through the process of updating them.
#######Fabric CA Container#######
To learn how to upgrade your Fabric CA server, click over to the CA documentation.
#######Upgrade Node SDK Clients#######
<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		Upgrade Fabric CA before upgrading Node SDK Clients.
		</td>
	</tr>
</table>

Use NPM to upgrade any Node.js client by executing these commands in the root directory of your application:

	npm install fabric-client@1.1

	npm install fabric-ca-client@1.1
These commands install the new version of both the Fabric client and Fabric-CA client and write the new versions package.json.
#######Upgrading the Kafka Cluster#######
It is not required, but it is recommended that the Kafka cluster be upgraded and kept up to date along with the rest of Fabric. Newer versions of Kafka support older protocol versions, so you may upgrade Kafka before or after the rest of Fabric.

If your Kafka cluster is older than Kafka v0.11.0, this upgrade is especially recommended as it hardens replication in order to better handle crash faults.

Refer to the official Apache Kafka documentation on upgrading Kafka from previous versions to upgrade the Kafka cluster brokers.

Please note that the Kafka cluster might experience a negative performance impact if the orderer is configured to use a Kafka protocol version that is older than the Kafka broker version. The Kafka protocol version is set using either the Kafka.Version key in the orderer.yaml file or via the ORDERER_KAFKA_VERSION environment variable in a Docker deployment. Fabric v1.0 provided sample Kafka docker images containing Kafka version 0.9.0.1. Fabric v1.1 provides sample Kafka docker images containing Kafka version v1.0.0.

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		You must configure the Kafka protocol version used by the orderer to match your Kafka cluster version, even if it was not set before. For example, if you are using the sample Kafka images provided with Fabric v1.0.x, either set the ORDERER_KAFKA_VERSION environment variable, or the Kafka.Version key in the orderer.yaml to 0.9.0.1. If you are unsure about your Kafka cluster version, you can configure the orderer’s Kafka protocol version to 0.9.0.1 for maximum compatibility and update the setting afterwards when you have determined your Kafka cluster version.
		</td>
	</tr>
</table>
#######Upgrading Zookeeper#######
An Apache Kafka cluster requires an Apache Zookeeper cluster. The Zookeeper API has been stable for a long time and, as such, almost any version of Zookeeper is tolerated by Kafka. Refer to the Apache Kafka upgrade documentation in case there is a specific requirement to upgrade to a specific version of Zookeeper. If you would like to upgrade your Zookeeper cluster, some information on upgrading Zookeeper cluster can be found in the Zookeeper FAQ.
#######Upgrading CouchDB#######
If you are using CouchDB as state database, upgrade the peer’s CouchDB at the same time the peer is being upgraded. To upgrade CouchDB:

1. Stop CouchDB.
2. Backup CouchDB data directory.
3. Delete CouchDB data directory.
4. Install CouchDB v2.1.1 binaries or update deployment scripts to use a new Docker image (CouchDB v2.1.1 pre-configured Docker image is provided alongside Fabric v1.1).
5. Restart CouchDB.

The reason to delete the CouchDB data directory is that upon startup the v1.1 peer will rebuild the CouchDB state databases from the blockchain transactions. Starting in v1.1, there will be an internal CouchDB database for each channel_chaincode combination (for each chaincode instantiated on each channel that the peer has joined).

#######Upgrade Chaincodes With Vendored Shim#######
A number of third party tools exist that will allow you to vendor a chaincode shim. If you used one of these tools, use the same one to update your vendoring and re-package your chaincode.

If your chaincode vendors the shim, after updating the shim version, you must install it to all peers which already have the chaincode. Install it with the same name, but a newer version. Then you should execute a chaincode upgrade on each channel where this chaincode has been deployed to move to the new version.

If you did not vendor your chaincode, you can skip this step entirely.

####Chaincode Tutorials####
#####What is Chaincode?#####
Chaincode is a program, written in Go, node.js, and eventually in other programming languages such as Java, that implements a prescribed interface. Chaincode runs in a secured Docker container isolated from the endorsing peer process. Chaincode initializes and manages ledger state through transactions submitted by applications.

A chaincode typically handles business logic agreed to by members of the network, so it may be considered as a “smart contract”. State created by a chaincode is scoped exclusively to that chaincode and can’t be accessed directly by another chaincode. However, within the same network, given the appropriate permission a chaincode may invoke another chaincode to access its state.

#####Two Personas#####
We offer two different perspectives on chaincode. One, from the perspective of an application developer developing a blockchain application/solution entitled Chaincode for Developers, and the other, Chaincode for Operators oriented to the blockchain network operator who is responsible for managing a blockchain network, and who would leverage the Hyperledger Fabric API to install, instantiate, and upgrade chaincode, but would likely not be involved in the development of a chaincode application.

####Chaincode for Developers####
#####What is Chaincode?#####
Chaincode is a program, written in Go, node.js, that implements a prescribed interface. Eventually, other programming languages such as Java, will be supported. Chaincode runs in a secured Docker container isolated from the endorsing peer process. Chaincode initializes and manages the ledger state through transactions submitted by applications.

A chaincode typically handles business logic agreed to by members of the network, so it similar to a “smart contract”. A chaincode can be invoked to update or query the ledger in a proposal transaction. Given the appropriate permission, a chaincode may invoke another chaincode, either in the same channel or in different channels, to access its state. Note that, if the called chaincode is on a different channel from the calling chaincode, only read query is allowed. That is, the called chaincode on a different channel is only a Query, which does not participate in state validation checks in subsequent commit phase.

In the following sections, we will explore chaincode through the eyes of an application developer. We’ll present a simple chaincode sample application and walk through the purpose of each method in the Chaincode Shim API.
#####Chaincode API#####
Every chaincode program must implement the Chaincode interface:

+ Go
+ node.js

whose methods are called in response to received transactions. In particular the Init method is called when a chaincode receives an instantiate or upgrade transaction so that the chaincode may perform any necessary initialization, including initialization of application state. The Invoke method is called in response to receiving an invoke transaction to process transaction proposals.

The other interface in the chaincode “shim” APIs is the ChaincodeStubInterface:

+ Go
+ node.js

which is used to access and modify the ledger, and to make invocations between chaincodes.

In this tutorial, we will demonstrate the use of these APIs by implementing a simple chaincode application that manages simple “assets”.

#####Simple Asset Chaincode#####
Our application is a basic sample chaincode to create assets (key-value pairs) on the ledger.
######Choosing a Location for the Code######
If you haven’t been doing programming in Go, you may want to make sure that you have Go Programming Language installed and your system properly configured.

Now, you will want to create a directory for your chaincode application as a child directory of $GOPATH/src/.

To keep things simple, let’s use the following command:

	mkdir -p $GOPATH/src/sacc && cd $GOPATH/src/sacc
Now, let’s create the source file that we’ll fill in with code:

	touch sacc.go

######Housekeeping######
First, let’s start with some housekeeping. As with every chaincode, it implements the Chaincode interface in particular, Init and Invoke functions. So, let’s add the go import statements for the necessary dependencies for our chaincode. We’ll import the chaincode shim package and the peer protobuf package. Next, let’s add a struct SimpleAsset as a receiver for Chaincode shim functions.

	package main

	import (
	    "fmt"
	
	    "github.com/hyperledger/fabric/core/chaincode/shim"
	    "github.com/hyperledger/fabric/protos/peer"
	)
	
	// SimpleAsset implements a simple chaincode to manage an asset
	type SimpleAsset struct {
	}

######Initializing the Chaincode######
Next, we’ll implement the Init function.

	// Init is called during chaincode instantiation to initialize any data.
	func (t *SimpleAsset) Init(stub shim.ChaincodeStubInterface) peer.Response {
	
	}

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		Note that chaincode upgrade also calls this function. When writing a chaincode that will upgrade an existing one, make sure to modify the Init function appropriately. In particular, provide an empty “Init” method if there’s no “migration” or nothing to be initialized as part of the upgrade.
		</td>
	</tr>
</table>

Next, we’ll retrieve the arguments to the Init call using the ChaincodeStubInterface.GetStringArgs function and check for validity. In our case, we are expecting a key-value pair.

	// Init is called during chaincode instantiation to initialize any
	// data. Note that chaincode upgrade also calls this function to reset
	// or to migrate data, so be careful to avoid a scenario where you
	// inadvertently clobber your ledger's data!
	func (t *SimpleAsset) Init(stub shim.ChaincodeStubInterface) peer.Response {
	  // Get the args from the transaction proposal
	  args := stub.GetStringArgs()
	  if len(args) != 2 {
	    return shim.Error("Incorrect arguments. Expecting a key and a value")
	  }
	}

Next, now that we have established that the call is valid, we’ll store the initial state in the ledger. To do this, we will call ChaincodeStubInterface.PutState with the key and value passed in as the arguments. Assuming all went well, return a peer.Response object that indicates the initialization was a success.

	// Init is called during chaincode instantiation to initialize any
	// data. Note that chaincode upgrade also calls this function to reset
	// or to migrate data, so be careful to avoid a scenario where you
	// inadvertently clobber your ledger's data!
	func (t *SimpleAsset) Init(stub shim.ChaincodeStubInterface) peer.Response {
	  // Get the args from the transaction proposal
	  args := stub.GetStringArgs()
	  if len(args) != 2 {
	    return shim.Error("Incorrect arguments. Expecting a key and a value")
	  }
	
	  // Set up any variables or assets here by calling stub.PutState()
	
	  // We store the key and the value on the ledger
	  err := stub.PutState(args[0], []byte(args[1]))
	  if err != nil {
	    return shim.Error(fmt.Sprintf("Failed to create asset: %s", args[0]))
	  }
	  return shim.Success(nil)
	}
######Invoking the Chaincode######
First, let’s add the Invoke function’s signature.

	// Invoke is called per transaction on the chaincode. Each transaction is
	// either a 'get' or a 'set' on the asset created by Init function. The 'set'
	// method may create a new asset by specifying a new key-value pair.
	func (t *SimpleAsset) Invoke(stub shim.ChaincodeStubInterface) peer.Response {
	
	}
As with the Init function above, we need to extract the arguments from the ChaincodeStubInterface. The Invoke function’s arguments will be the name of the chaincode application function to invoke. In our case, our application will simply have two functions: set and get, that allow the value of an asset to be set or its current state to be retrieved. We first call ChaincodeStubInterface.GetFunctionAndParameters to extract the function name and the parameters to that chaincode application function.

	// Invoke is called per transaction on the chaincode. Each transaction is
	// either a 'get' or a 'set' on the asset created by Init function. The Set
	// method may create a new asset by specifying a new key-value pair.
	func (t *SimpleAsset) Invoke(stub shim.ChaincodeStubInterface) peer.Response {
	    // Extract the function and args from the transaction proposal
	    fn, args := stub.GetFunctionAndParameters()
	
	}
Next, we’ll validate the function name as being either set or get, and invoke those chaincode application functions, returning an appropriate response via the shim.Success or shim.Error functions that will serialize the response into a gRPC protobuf message.

	// Invoke is called per transaction on the chaincode. Each transaction is
	// either a 'get' or a 'set' on the asset created by Init function. The Set
	// method may create a new asset by specifying a new key-value pair.
	func (t *SimpleAsset) Invoke(stub shim.ChaincodeStubInterface) peer.Response {
	    // Extract the function and args from the transaction proposal
	    fn, args := stub.GetFunctionAndParameters()
	
	    var result string
	    var err error
	    if fn == "set" {
	            result, err = set(stub, args)
	    } else {
	            result, err = get(stub, args)
	    }
	    if err != nil {
	            return shim.Error(err.Error())
	    }
	
	    // Return the result as success payload
	    return shim.Success([]byte(result))
	}
######Implementing the Chaincode Application######
As noted, our chaincode application implements two functions that can be invoked via the Invoke function. Let’s implement those functions now. Note that as we mentioned above, to access the ledger’s state, we will leverage the ChaincodeStubInterface.PutState and ChaincodeStubInterface.GetState functions of the chaincode shim API.

	// Set stores the asset (both key and value) on the ledger. If the key exists,
	// it will override the value with the new one
	func set(stub shim.ChaincodeStubInterface, args []string) (string, error) {
	    if len(args) != 2 {
	            return "", fmt.Errorf("Incorrect arguments. Expecting a key and a value")
	    }
	
	    err := stub.PutState(args[0], []byte(args[1]))
	    if err != nil {
	            return "", fmt.Errorf("Failed to set asset: %s", args[0])
	    }
	    return args[1], nil
	}
	
	// Get returns the value of the specified asset key
	func get(stub shim.ChaincodeStubInterface, args []string) (string, error) {
	    if len(args) != 1 {
	            return "", fmt.Errorf("Incorrect arguments. Expecting a key")
	    }
	
	    value, err := stub.GetState(args[0])
	    if err != nil {
	            return "", fmt.Errorf("Failed to get asset: %s with error: %s", args[0], err)
	    }
	    if value == nil {
	            return "", fmt.Errorf("Asset not found: %s", args[0])
	    }
	    return string(value), nil
	}
######Pulling it All Together######
Finally, we need to add the main function, which will call the shim.Start function. Here’s the whole chaincode program source.

	package main

	import (
	    "fmt"
	
	    "github.com/hyperledger/fabric/core/chaincode/shim"
	    "github.com/hyperledger/fabric/protos/peer"
	)
	
	// SimpleAsset implements a simple chaincode to manage an asset
	type SimpleAsset struct {
	}
	
	// Init is called during chaincode instantiation to initialize any
	// data. Note that chaincode upgrade also calls this function to reset
	// or to migrate data.
	func (t *SimpleAsset) Init(stub shim.ChaincodeStubInterface) peer.Response {
	    // Get the args from the transaction proposal
	    args := stub.GetStringArgs()
	    if len(args) != 2 {
	            return shim.Error("Incorrect arguments. Expecting a key and a value")
	    }
	
	    // Set up any variables or assets here by calling stub.PutState()
	
	    // We store the key and the value on the ledger
	    err := stub.PutState(args[0], []byte(args[1]))
	    if err != nil {
	            return shim.Error(fmt.Sprintf("Failed to create asset: %s", args[0]))
	    }
	    return shim.Success(nil)
	}
	
	// Invoke is called per transaction on the chaincode. Each transaction is
	// either a 'get' or a 'set' on the asset created by Init function. The Set
	// method may create a new asset by specifying a new key-value pair.
	func (t *SimpleAsset) Invoke(stub shim.ChaincodeStubInterface) peer.Response {
	    // Extract the function and args from the transaction proposal
	    fn, args := stub.GetFunctionAndParameters()
	
	    var result string
	    var err error
	    if fn == "set" {
	            result, err = set(stub, args)
	    } else { // assume 'get' even if fn is nil
	            result, err = get(stub, args)
	    }
	    if err != nil {
	            return shim.Error(err.Error())
	    }
	
	    // Return the result as success payload
	    return shim.Success([]byte(result))
	}
	
	// Set stores the asset (both key and value) on the ledger. If the key exists,
	// it will override the value with the new one
	func set(stub shim.ChaincodeStubInterface, args []string) (string, error) {
	    if len(args) != 2 {
	            return "", fmt.Errorf("Incorrect arguments. Expecting a key and a value")
	    }
	
	    err := stub.PutState(args[0], []byte(args[1]))
	    if err != nil {
	            return "", fmt.Errorf("Failed to set asset: %s", args[0])
	    }
	    return args[1], nil
	}
	
	// Get returns the value of the specified asset key
	func get(stub shim.ChaincodeStubInterface, args []string) (string, error) {
	    if len(args) != 1 {
	            return "", fmt.Errorf("Incorrect arguments. Expecting a key")
	    }
	
	    value, err := stub.GetState(args[0])
	    if err != nil {
	            return "", fmt.Errorf("Failed to get asset: %s with error: %s", args[0], err)
	    }
	    if value == nil {
	            return "", fmt.Errorf("Asset not found: %s", args[0])
	    }
	    return string(value), nil
	}
	
	// main function starts up the chaincode in the container during instantiate
	func main() {
	    if err := shim.Start(new(SimpleAsset)); err != nil {
	            fmt.Printf("Error starting SimpleAsset chaincode: %s", err)
	    }
	}
######Building Chaincode######
Now let’s compile your chaincode.

	go get -u --tags nopkcs11 github.com/hyperledger/fabric/core/chaincode/shim
	go build --tags nopkcs11
Assuming there are no errors, now we can proceed to the next step, testing your chaincode.

######Testing Using dev mode######
Normally chaincodes are started and maintained by peer. However in “dev mode”, chaincode is built and started by the user. This mode is useful during chaincode development phase for rapid code/build/run/debug cycle turnaround.

We start “dev mode” by leveraging pre-generated orderer and channel artifacts for a sample dev network. As such, the user can immediately jump into the process of compiling chaincode and driving calls.

#####Install Hyperledger Fabric Samples#####
If you haven’t already done so, please install the Hyperledger Fabric Samples.

Navigate to the chaincode-docker-devmode directory of the fabric-samples clone:

	cd chaincode-docker-devmode

#####Download Docker images#####
We need four Docker images in order for “dev mode” to run against the supplied docker compose script. If you installed the fabric-samples repo clone and followed the instructions to Download Platform-specific Binaries, then you should have the necessary Docker images installed locally.

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		If you choose to manually pull the images then you must retag them as latest.
		</td>
	</tr>
</table>

Issue a docker images command to reveal your local Docker Registry. You should see something similar to following:

	docker images
	REPOSITORY                     TAG                                  IMAGE ID            CREATED             SIZE
	hyperledger/fabric-tools       latest                           b7bfddf508bc        About an hour ago   1.46GB
	hyperledger/fabric-tools       x86_64-1.1.0                     b7bfddf508bc        About an hour ago   1.46GB
	hyperledger/fabric-orderer     latest                           ce0c810df36a        About an hour ago   180MB
	hyperledger/fabric-orderer     x86_64-1.1.0                     ce0c810df36a        About an hour ago   180MB
	hyperledger/fabric-peer        latest                           b023f9be0771        About an hour ago   187MB
	hyperledger/fabric-peer        x86_64-1.1.0                     b023f9be0771        About an hour ago   187MB
	hyperledger/fabric-javaenv     latest                           82098abb1a17        About an hour ago   1.52GB
	hyperledger/fabric-javaenv     x86_64-1.1.0                     82098abb1a17        About an hour ago   1.52GB
	hyperledger/fabric-ccenv       latest                           c8b4909d8d46        About an hour ago   1.39GB
	hyperledger/fabric-ccenv       x86_64-1.1.0                     c8b4909d8d46        About an hour ago   1.39GB

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		If you retrieved the images through the Download Platform-specific Binaries, then you will see additional images listed. However, we are only concerned with these four.
		</td>
	</tr>
</table>

Now open three terminals and navigate to your chaincode-docker-devmode directory in each.

#####Terminall - Start the newwork#####
	docker-compose -f docker-compose-simple.yaml up
The above starts the network with the SingleSampleMSPSolo orderer profile and launches the peer in “dev mode”. It also launches two additional containers - one for the chaincode environment and a CLI to interact with the chaincode. The commands for create and join channel are embedded in the CLI container, so we can jump immediately to the chaincode calls.

#####Terminal2 - Build & start the chaincode#####
	docker exec -it chaincode bash

You should see the following:

	root@d2629980e76b:/opt/gopath/src/chaincode#

Now, compile your chaincode:

	cd sacc
	go build

Now run the chaincode:

	CORE_PEER_ADDRESS=peer:7052 CORE_CHAINCODE_ID_NAME=mycc:0 ./sacc

The chaincode is started with peer and chaincode logs indicating successful registration with the peer. Note that at this stage the chaincode is not associated with any channel. This is done in subsequent steps using the instantiate command.

#####Terminal3 - Use the chaincode#####
Even though you are in --peer-chaincodedev mode, you still have to install the chaincode so the life-cycle system chaincode can go through its checks normally. This requirement may be removed in future when in --peer-chaincodedev mode.

We’ll leverage the CLI container to drive these calls.

	docker exec -it cli bash


	peer chaincode install -p chaincodedev/chaincode/sacc -n mycc -v 0
	peer chaincode instantiate -n mycc -v 0 -c '{"Args":["a","10"]}' -C myc

Now issue an invoke to change the value of “a” to “20”.

	peer chaincode invoke -n mycc -c '{"Args":["set", "a", "20"]}' -C myc

Finally, query a. We should see a value of 20.

	peer chaincode query -n mycc -c '{"Args":["query","a"]}' -C myc

#####Testing new chaincode#####
By default, we mount only sacc. However, you can easily test different chaincodes by adding them to the chaincode subdirectory and relaunching your network. At this point they will be accessible in your chaincode container.

#####Chaincode encryption#####
In certain scenarios, it may be useful to encrypt values associated with a key in their entirety or simply in part. For example, if a person’s social security number or address was being written to the ledger, then you likely would not want this data to appear in plaintext. Chaincode encryption is achieved by leveraging the entities extension which is a BCCSP wrapper with commodity factories and functions to perform cryptographic operations such as encryption and elliptic curve digital signatures. For example, to encrypt, the invoker of a chaincode passes in a cryptographic key via the transient field. The same key may then be used for subsequent query operations, allowing for proper decryption of the encrypted state values.

For more information and samples, see the Encc Example within the fabric/examples directory. Pay specific attention to the utils.go helper program. This utility loads the chaincode shim APIs and Entities extension and builds a new class of functions (e.g. encryptAndPutState & getStateAndDecrypt) that the sample encryption chaincode then leverages. As such, the chaincode can now marry the basic shim APIs of Get and Put with the added functionality of Encrypt and Decrypt.

#####Managing external dependencies for chaincode written in Go#####
If your chaincode requires packages not provided by the Go standard library, you will need to include those packages with your chaincode. There are many tools available for managing (or “vendoring”) these dependencies. The following demonstrates how to use govendor:

	govendor init
	govendor add +external  // Add all external package, or
	govendor add github.com/external/pkg // Add specific external package

This imports the external dependencies into a local vendor directory. peer chaincode package and peer chaincode install operations will then include code associated with the dependencies into the chaincode package.

####Chaincode for Operators####
#####What is Chaincode?#####
Chaincode is a program, written in Go, and eventually in other programming languages such as Java, that implements a prescribed interface. Chaincode runs in a secured Docker container isolated from the endorsing peer process. Chaincode initializes and manages ledger state through transactions submitted by applications.

A chaincode typically handles business logic agreed to by members of the network, so it may be considered as a “smart contract”. State created by a chaincode is scoped exclusively to that chaincode and can’t be accessed directly by another chaincode. However, within the same network, given the appropriate permission a chaincode may invoke another chaincode to access its state.

In the following sections, we will explore chaincode through the eyes of a blockchain network operator, Noah. For Noah’s interests, we will focus on chaincode lifecycle operations; the process of packaging, installing, instantiating and upgrading the chaincode as a function of the chaincode’s operational lifecycle within a blockchain network.

#####Chaincode lifecycle#####
The Hyperledger Fabric API enables interaction with the various nodes in a blockchain network - the peers, orderers and MSPs - and it also allows one to package, install, instantiate and upgrade chaincode on the endorsing peer nodes. The Hyperledger Fabric language-specific SDKs abstract the specifics of the Hyperledger Fabric API to facilitate application development, though it can be used to manage a chaincode’s lifecycle. Additionally, the Hyperledger Fabric API can be accessed directly via the CLI, which we will use in this document.

We provide four commands to manage a chaincode’s lifecycle: package, install, instantiate, and upgrade. In a future release, we are considering adding stop and start transactions to disable and re-enable a chaincode without having to actually uninstall it. After a chaincode has been successfully installed and instantiated, the chaincode is active (running) and can process transactions via the invoke transaction. A chaincode may be upgraded any time after it has been installed.

#####Packaging#####
The chaincode package consists of 3 parts:

+ the chaincode, as defined by ChaincodeDeploymentSpec or CDS. The CDS defines the chaincode package in terms of the code and other properties such as name and version,
+ an optional instantiation policy which can be syntactically described by the same policy used for endorsement and described in Endorsement policies, and
+ a set of signatures by the entities that “own” the chaincode.

The signatures serve the following purposes:

+ to establish an ownership of the chaincode,
+ to allow verification of the contents of the package, and
+ to allow detection of package tampering.

The creator of the instantiation transaction of the chaincode on a channel is validated against the instantiation policy of the chaincode.

######Creating the package######
There are two approaches to packaging chaincode. One for when you want to have multiple owners of a chaincode, and hence need to have the chaincode package signed by multiple identities. This workflow requires that we initially create a signed chaincode package (a SignedCDS) which is subsequently passed serially to each of the other owners for signing.

The simpler workflow is for when you are deploying a SignedCDS that has only the signature of the identity of the node that is issuing the install transaction.

We will address the more complex case first. However, you may skip ahead to the Installing chaincode section below if you do not need to worry about multiple owners just yet.

To create a signed chaincode package, use the following command:

	peer chaincode package -n mycc -p github.com/hyperledger/fabric/examples/chaincode/go/chaincode_example02 -v 0 -s -S -i "AND('OrgA.admin')" ccpack.out

The -s option creates a package that can be signed by multiple owners as opposed to simply creating a raw CDS. When -s is specified, the -S option must also be specified if other owners are going to need to sign. Otherwise, the process will create a SignedCDS that includes only the instantiation policy in addition to the CDS.

The -S option directs the process to sign the package using the MSP identified by the value of the localMspid property in core.yaml.

The -S option is optional. However if a package is created without a signature, it cannot be signed by any other owner using the signpackage command.

The optional -i option allows one to specify an instantiation policy for the chaincode. The instantiation policy has the same format as an endorsement policy and specifies which identities can instantiate the chaincode. In the example above, only the admin of OrgA is allowed to instantiate the chaincode. If no policy is provided, the default policy is used, which only allows the admin identity of the peer’s MSP to instantiate chaincode.

######Package signing######
A chaincode package that was signed at creation can be handed over to other owners for inspection and signing. The workflow supports out-of-band signing of chaincode package.

The ChaincodeDeploymentSpec may be optionally be signed by the collective owners to create a SignedChaincodeDeploymentSpec (or SignedCDS). The SignedCDS contains 3 elements:

1. The CDS contains the source code, the name, and version of the chaincode.
2. An instantiation policy of the chaincode, expressed as endorsement policies.
3. The list of chaincode owners, defined by means of Endorsement.

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		Note that this endorsement policy is determined out-of-band to provide proper MSP principals when the chaincode is instantiated on some channels. If the instantiation policy is not specified, the default policy is any MSP administrator of the channel.
		</td>
	</tr>
</table>

Each owner endorses the ChaincodeDeploymentSpec by combining it with that owner’s identity (e.g. certificate) and signing the combined result.

A chaincode owner can sign a previously created signed package using the following command:

	peer chaincode signpackage ccpack.out signedccpack.out

Where ccpack.out and signedccpack.out are the input and output packages, respectively. signedccpack.out contains an additional signature over the package signed using the Local MSP.

######Installing chaincode######
The install transaction packages a chaincode’s source code into a prescribed format called a ChaincodeDeploymentSpec (or CDS) and installs it on a peer node that will run that chaincode.

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		You must install the chaincode on each endorsing peer node of a channel that will run your chaincode.
		</td>
	</tr>
</table>

When the install API is given simply a ChaincodeDeploymentSpec, it will default the instantiation policy and include an empty owner list.

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		Chaincode should only be installed on endorsing peer nodes of the owning members of the chaincode to protect the confidentiality of the chaincode logic from other members on the network. Those members without the chaincode, can’t be the endorsers of the chaincode’s transactions; that is, they can’t execute the chaincode. However, they can still validate and commit the transactions to the ledger.
		</td>
	</tr>
</table>

To install a chaincode, send a SignedProposal to the lifecycle system chaincode (LSCC) described in the System Chaincode section. For example, to install the sacc sample chaincode described in section Simple Asset Chaincode using the CLI, the command would look like the following:

	peer chaincode install -n asset_mgmt -v 1.0 -p sacc

The CLI internally creates the SignedChaincodeDeploymentSpec for sacc and sends it to the local peer, which calls the Install method on the LSCC. The argument to the -p option specifies the path to the chaincode, which must be located within the source tree of the user’s GOPATH, e.g. $GOPATH/src/sacc. See the CLI section for a complete description of the command options.

Note that in order to install on a peer, the signature of the SignedProposal must be from 1 of the peer’s local MSP administrators.

######Instantiate######
The instantiate transaction invokes the lifecycle System Chaincode (LSCC) to create and initialize a chaincode on a channel. This is a chaincode-channel binding process: a chaincode may be bound to any number of channels and operate on each channel individually and independently. In other words, regardless of how many other channels on which a chaincode might be installed and instantiated, state is kept isolated to the channel to which a transaction is submitted.

The creator of an instantiate transaction must satisfy the instantiation policy of the chaincode included in SignedCDS and must also be a writer on the channel, which is configured as part of the channel creation. This is important for the security of the channel to prevent rogue entities from deploying chaincodes or tricking members to execute chaincodes on an unbound channel.

For example, recall that the default instantiation policy is any channel MSP administrator, so the creator of a chaincode instantiate transaction must be a member of the channel administrators. When the transaction proposal arrives at the endorser, it verifies the creator’s signature against the instantiation policy. This is done again during the transaction validation before committing it to the ledger.

The instantiate transaction also sets up the endorsement policy for that chaincode on the channel. The endorsement policy describes the attestation requirements for the transaction result to be accepted by members of the channel.

For example, using the CLI to instantiate the sacc chaincode and initialize the state with john and 0, the command would look like the following:

	peer chaincode instantiate -n sacc -v 1.0 -c '{"Args":["john","0"]}' -P "OR ('Org1.member','Org2.member')"

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		Note the endorsement policy (CLI uses polish notation), which requires an endorsement from either member of Org1 or Org2 for all transactions to sacc. That is, either Org1 or Org2 must sign the result of executing the Invoke on sacc for the transactions to be valid.
		</td>
	</tr>
</table>

After being successfully instantiated, the chaincode enters the active state on the channel and is ready to process any transaction proposals of type ENDORSER_TRANSACTION. The transactions are processed concurrently as they arrive at the endorsing peer.

######Upgrade######
A chaincode may be upgraded any time by changing its version, which is part of the SignedCDS. Other parts, such as owners and instantiation policy are optional. However, the chaincode name must be the same; otherwise it would be considered as a totally different chaincode.

Prior to upgrade, the new version of the chaincode must be installed on the required endorsers. Upgrade is a transaction similar to the instantiate transaction, which binds the new version of the chaincode to the channel. Other channels bound to the old version of the chaincode still run with the old version. In other words, the upgrade transaction only affects one channel at a time, the channel to which the transaction is submitted.

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		Note that since multiple versions of a chaincode may be active simultaneously, the upgrade process doesn’t automatically remove the old versions, so user must manage this for the time being.
		</td>
	</tr>
</table>

There’s one subtle difference with the instantiate transaction: the upgrade transaction is checked against the current chaincode instantiation policy, not the new policy (if specified). This is to ensure that only existing members specified in the current instantiation policy may upgrade the chaincode.

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		Note that during upgrade, the chaincode Init function is called to perform any data related updates or re-initialize it, so care must be taken to avoid resetting states when upgrading chaincode.
		</td>
	</tr>
</table>

######Stop and Start######
Note that stop and start lifecycle transactions have not yet been implemented. However, you may stop a chaincode manually by removing the chaincode container and the SignedCDS package from each of the endorsers. This is done by deleting the chaincode’s container on each of the hosts or virtual machines on which the endorsing peer nodes are running, and then deleting the SignedCDS from each of the endorsing peer nodes:

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		TODO - in order to delete the CDS from the peer node, you would need to enter the peer node’s container, first. We really need to provide a utility script that can do this.
		</td>
	</tr>
</table>

	docker rm -f <container id>
	rm /var/hyperledger/production/chaincodes/<ccname>:<ccversion>

Stop would be useful in the workflow for doing upgrade in controlled manner, where a chaincode can be stopped on a channel on all peers before issuing an upgrade.

######CLI######
<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		We are assessing the need to distribute platform-specific binaries for the Hyperledger Fabric peer binary. For the time being, you can simply invoke the commands from within a running docker container.
		</td>
	</tr>
</table>

To view the currently available CLI commands, execute the following command from within a running fabric-peer Docker container:

	docker run -it hyperledger/fabric-peer bash
	# peer chaincode --help

Which shows output similar to the example below:

	Usage:
	  peer chaincode [command]
	
	Available Commands:
	  install     Package the specified chaincode into a deployment spec and save it on the peer's path.
	  instantiate Deploy the specified chaincode to the network.
	  invoke      Invoke the specified chaincode.
	  list        Get the instantiated chaincodes on a channel or installed chaincodes on a peer.
	  package     Package the specified chaincode into a deployment spec.
	  query       Query using the specified chaincode.
	  signpackage Sign the specified chaincode package
	  upgrade     Upgrade chaincode.
	
	Flags:
	      --cafile string      Path to file containing PEM-encoded trusted certificate(s) for the ordering endpoint
	  -h, --help               help for chaincode
	  -o, --orderer string     Ordering service endpoint
	      --tls                Use TLS when communicating with the orderer endpoint
	      --transient string   Transient map of arguments in JSON encoding
	
	Global Flags:
	      --logging-level string       Default logging level and overrides, see core.yaml for full syntax
	      --test.coverprofile string   Done (default "coverage.cov")
	  -v, --version
	
	Use "peer chaincode [command] --help" for more information about a command.

To facilitate its use in scripted applications, the peer command always produces a non-zero return code in the event of command failure.

Example of chaincode commands:

	peer chaincode install -n mycc -v 0 -p path/to/my/chaincode/v0
	peer chaincode instantiate -n mycc -v 0 -c '{"Args":["a", "b", "c"]}' -C mychannel
	peer chaincode install -n mycc -v 1 -p path/to/my/chaincode/v1
	peer chaincode upgrade -n mycc -v 1 -c '{"Args":["d", "e", "f"]}' -C mychannel
	peer chaincode query -C mychannel -n mycc -c '{"Args":["query","e"]}'
	peer chaincode invoke -o orderer.example.com:7050  --tls --cafile $ORDERER_CA -C mychannel -n mycc -c '{"Args":["invoke","a","b","10"]}'

#####System chaincode#####
System chaincode has the same programming model except that it runs within the peer process rather than in an isolated container like normal chaincode. Therefore, system chaincode is built into the peer executable and doesn’t follow the same lifecycle described above. In particular, install, instantiate and upgrade do not apply to system chaincodes.

The purpose of system chaincode is to shortcut gRPC communication cost between peer and chaincode, and tradeoff the flexibility in management. For example, a system chaincode can only be upgraded with the peer binary. It must also register with a fixed set of parameters compiled in and doesn’t have endorsement policies or endorsement policy functionality.

System chaincode is used in Hyperledger Fabric to implement a number of system behaviors so that they can be replaced or modified as appropriate by a system integrator.

The current list of system chaincodes:

1. LSCC Lifecycle system chaincode handles lifecycle requests described above.
2. CSCC Configuration system chaincode handles channel configuration on the peer side.
3. QSCC Query system chaincode provides ledger query APIs such as getting blocks and transactions.
4. ESCC Endorsement system chaincode handles endorsement by signing the transaction proposal response.
5. VSCC Validation system chaincode handles the transaction validation, including checking endorsement policy and multiversioning concurrency control.

Care must be taken when modifying or replacing these system chaincodes, especially LSCC, ESCC and VSCC since they are in the main transaction execution path. It is worth noting that as VSCC validates a block before committing it to the ledger, it is important that all peers in the channel compute the same validation to avoid ledger divergence (non-determinism). So special care is needed if VSCC is modified or replaced.

####System Chaincode Plugins####
System chaincodes are specialized chaincodes that run as part of the peer process as opposed to user chaincodes that run in separate docker containers. As such they have more access to resources in the peer and can be used for implementing features that are difficult or impossible to be implemented through user chaincodes. Examples of System Chaincodes are ESCC (Endorser System Chaincode) for endorsing proposals, QSCC (Query System Chaincode) for ledger and other fabric related queries and VSCC (Validation System Chaincode) for validating a transaction at commit time respectively.

Unlike a user chaincode, a system chaincode is not installed and instantiated using proposals from SDKs or CLI. It is registered and deployed by the peer at start-up.

System chaincodes can be linked to a peer in two ways: statically and dynamically using Go plugins. This tutorial will outline how to develop and load system chaincodes as plugins.

#####Developing Plugins#####
A system chaincode is a program written in Go and loaded using the Go plugin package.

A plugin includes a main package with exported symbols and is built with the command go build -buildmode=plugin.

Every system chaincode must implement the Chaincode Interface and export a constructor method that matches the signature func New() shim.Chaincode in the main package. An example can be found in the repository at examples/plugin/scc.

Existing chaincodes such as the QSCC can also serve as templates for certain features - such as access control - that are typically implemented through system chaincodes. The existing system chaincodes also serve as a reference for best-practices on things like logging and testing.

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		On imported packages: the Go standard library requires that a plugin must include the same version of imported packages as the host application (fabric, in this case)
		</td>
	</tr>
</table>

#####Configuring Plugins#####
Plugins are configured in the chaincode.systemPlugin section in core.yaml:

	chaincode:
	  systemPlugins:
	    - enabled: true
	      name: mysyscc
	      path: /opt/lib/syscc.so
	      invokableExternal: true
	      invokableCC2CC: true

A system chaincode must also be whitelisted in the chaincode.system section in core.yaml:

	chaincode:
	  system:
	    mysyscc: enable

####Videos####
Refer to the Hyperledger Fabric channel on YouTube

This collection contains developers demonstrating various v1 features and components such as: ledger, channels, gossip, SDK, chaincode, MSP, and more...
	
###四、操作指南###
####Upgrading from v1.0.x####
At a high level, upgrading a Fabric network to v1.1 can be performed by following these steps:

+ Upgrade binaries for orderers, peers, and fabric-ca. These upgrades may be done in parallel.
+ Upgrade client SDKs.
+ Enable v1.1 channel capability requirements.
+ (Optional) Upgrade the Kafka cluster.

To help understand this process, we’ve created the Upgrading Your Network Components tutorial that will take you through most of the major upgrade steps, including upgrading peers, orderers, as well as enabling capability requirements.

Because our tutorial leverages the Building Your First Network (BYFN) sample, it has certain limitations (it does not use Fabric CA, for example). Therefore we have included a section at the end of the tutorial that will show how to upgrade your CA, Kafka clusters, CouchDB, Zookeeper, vendored chaincode shims, and Node SDK clients.

If you want to learn more about capability requirements, click here.

####Updating a Channel Configuration####
#####What is a Channel Configuration?#####
Channel configurations contain all of the information relevant to the administration of a channel. Most importantly, the channel configuration specifies which organizations are members of channel, but it also includes other channel-wide configuration information such as channel access policies and block batch sizes.

This configuration is stored on the ledger in a block, and is therefore known as a configuration (config) block. Configuration blocks contain a single configuration. The first of these blocks is known as the “genesis block” and contains the initial configuration required to bootstrap a channel. Each time the configuration of a channel changes it is done through a new configuration block, with the latest configuration block representing the current channel configuration. Orderers and peers keep the current channel configuration in memory to facilitate all channel operations such as cutting a new block and validating block transactions.

Because configurations are stored in blocks, updating a config happens through a process called a “configuration transaction” (even though the process is a little different from a normal transaction). Updating a config is a process of pulling the config, translating into a format that humans can read, modifying it and then submitting it for approval.

For a more in-depth look at the process for pulling a config and translating it into JSON, check out Adding an Org to a Channel. In this doc, we’ll be focusing on the different ways you can edit a config and the process for getting it signed.

#####Editing a Config#####
Channels are highly configurable, but not infinitely so. Different configuration elements have different modification policies (which specify the group of identities required to sign the config update).

To see the scope of what’s possible to change it’s important to look at a config in JSON format. The Adding an Org to a Channel tutorial generates one, so if you’ve gone through that doc you can simply refer to it. For those who have not, we’ll provide one here (for ease of readability, it might be helpful to put this config into a viewer that supports JSON folding, like atom or Visual Studio).

######Click here to see the config######
A config might look intimidating in this form, but once you study it you’ll see that it has a logical structure.

Beyond the definitions of the policies – defining who can do certain things at the channel level, and who has the permission to change who can change the config – channels also have other kinds of features that can be modified using a config update. Adding an Org to a Channel takes you through one of the most important – adding an org to a channel. Some other things that are possible to change with a config update include:

+ Batch Size. These parameters dictate the number and size of transactions in a block. No block will appear larger than absolute_max_bytes large or with more than max_message_count transactions inside the block. If it is possible to construct a block under preferred_max_bytes, then a block will be cut prematurely, and transactions larger than this size will appear in their own block.

	{
	  "absolute_max_bytes": 102760448,
	  "max_message_count": 10,
	  "preferred_max_bytes": 524288
	}
+ Batch Timeout. The amount of time to wait after the first transaction arrives for additional transactions before cutting a block. Decreasing this value will improve latency, but decreasing it too much may decrease throughput by not allowing the block to fill to its maximum capacity.

	{ "timeout": "2s" }
+ Channel Restrictions. The total number of channels the orderer is willing to allocate may be specified as max_count. This is primarily useful in pre-production environments with weak consortium ChannelCreation policies.

	{
	 "max_count":1000
	}
+ Channel Creation Policy. Defines the policy value which will be set as the mod_policy for the Application group of new channels for the consortium it is defined in. The signature set attached to the channel creation request will be checked against the instantiation of this policy in the new channel to ensure that the channel creation is authorized. Note that this config vzlue is only set in the orderer system channel.

	{
	"type": 3,
	"value": {
	  "rule": "ANY",
	  "sub_policy": "Admins"
	  }
	}
+ Kafka brokers. When ConsensusType is set to kafka, the brokers list enumerates some subset (or preferably all) of the Kafka brokers for the orderer to initially connect to at startup. Note that it is not possible to change your consensus type after it has been established (during the bootstrapping of the genesis block).

	{
	  "brokers": [
	    "kafka0:9092",
	    "kafka1:9092",
	    "kafka2:9092",
	    "kafka3:9092"
	  ]
	}
+ Anchor Peers Definition. Defines the location of the anchor peers for each Org.

	{
	  "host": "peer0.org2.example.com",
	    "port": 7051
	}
+ Hashing Structure. The block data is an array of byte arrays. The hash of the block data is computed as a Merkle tree. This value specifies the width of that Merkle tree. For the time being, this value is fixed to 4294967295 which corresponds to a simple flat hash of the concatenation of the block data bytes.

	{ "width": 4294967295 }
+ Hashing Algorithm. The algorithm used for computing the hash values encoded into the blocks of the blockchain. In particular, this affects the data hash, and the previous block hash fields of the block. Note, this field currently only has one valid value (SHA256) and should not be changed.

	{ "name": "SHA256" }
+ Block Validation. This policy specifies the signature requirements for a block to be considered valid. By default, it requires a signature from some member of the ordering org.

	{
	  "type": 3,
	  "value": {
	    "rule": "ANY",
	    "sub_policy": "Writers"
	  }
	}
+ Orderer Address. A list of addresses where clients may invoke the orderer Broadcast and Deliver functions. The peer randomly chooses among these addresses and fails over between them for retrieving blocks.

	{
	  "addresses": [
	    "orderer.example.com:7050"
	  ]
	}

Just as we add an Org by adding their artifacts and MSP information, you can remove them by reversing the process.

Note that once the consensus type has been defined and the network has been bootstrapped, it is not possible to change it through a configuration update.

There is another important channel configuration (especially for v1.1) known as Capability Requirements. It has its own doc that can be found here.

Let’s say you want to edit the block batch size for the channel (because this is a single numeric field, it’s one of the easiest changes to make). First to make referencing the JSON path easy, we define it as an environment variable.

To establish this, take a look at your config, find what you’re looking for, and back track the path.

If you find batch size, for example, you’ll see that it’s a value of the Orderer. Orderer can be found under groups, which is under channel_group. The batch size value has a parameter under value of max_message_count.

Which would make the path this:

	 export MAXBATCHSIZEPATH=".channel_group.groups.Orderer.values.BatchSize.value.max_message_count"

Next, display the value of that property:

	jq "$MAXBATCHSIZEPATH" config.json

Which should return a value of 10 (in our sample network at least).

Now, let’s set the new batch size and display the new value:

	jq “$MAXBATCHSIZEPATH = 20” config.json > modified_config.json
	jq “$MAXBATCHSIZEPATH” modified_config.json

Once you’ve modified the JSON, it’s ready to be converted and submitted. The scripts and steps in Adding an Org to a Channel will take you through the process for converting the JSON, so let’s look at the process of submitting it.

#######Get the Necessary Signatures#######
Once you’ve successfully generated the protobuf file, it’s time to get it signed. To do this, you need to know the relevant policy for whatever it is you’re trying to change.

By default, editing the configuration of:

+ A particular org (for example, changing anchor peers) requires only the admin signature of that org.
+ The application (like who the member orgs are) requires a majority of the application organizations’ admins to sign.
+ The orderer requires a majority of the ordering organizations’ admins (of which there are by default only 1).
+ The top level channel group requires both the agreement of a majority of application organization admins and orderer organization admins.

If you have made changes to the default policies in the channel, you’ll need to compute your signature requirements accordingly.

Note: you may be able to script the signature collection, dependent on your application. In general, you may always collect more signatures than are required.

The actual process of getting these signatures will depend on how you’ve set up your system, but there are two main implementations. Currently, the Fabric command line defaults to a “pass it along” system. That is, the Admin of the Org proposing a config update sends the update to someone else (another Admin, typically) who needs to sign it. This Admin signs it (or doesn’t) and passes it along to the next Admin, and so on, until there are enough signatures for the config to be submitted.

This has the virtue of simplicity – when there are enough signatures, the last Admin can simply submit the config transaction (in Fabric, the peer channel update command includes a signature by default). However, this process will only be practical in smaller channels, since the “pass it along” method can be time consuming.

The other option is to submit the update to every Admin on a channel and wait for enough signatures to come back. These signatures can then be stitched together and submitted. This makes life a bit more difficult for the Admin who created the config update (forcing them to deal with a file per signer) but is the recommended workflow for users which are developing Fabric management applications.

Once the config has been added to the ledger, it will be a best practice to pull it and convert it to JSON to check to make sure everything was added correctly. This will also serve as a useful copy of the latest config.

####Membership Service Providers(MSP)####
The document serves to provide details on the setup and best practices for MSPs.

Membership Service Provider (MSP) is a component that aims to offer an abstraction of a membership operation architecture.

In particular, MSP abstracts away all cryptographic mechanisms and protocols behind issuing and validating certificates, and user authentication. An MSP may define their own notion of identity, and the rules by which those identities are governed (identity validation) and authenticated (signature generation and verification).

A Hyperledger Fabric blockchain network can be governed by one or more MSPs. This provides modularity of membership operations, and interoperability across different membership standards and architectures.

In the rest of this document we elaborate on the setup of the MSP implementation supported by Hyperledger Fabric, and discuss best practices concerning its use.

#####MSP Configuration#####
To setup an instance of the MSP, its configuration needs to be specified locally at each peer and orderer (to enable peer, and orderer signing), and on the channels to enable peer, orderer, client identity validation, and respective signature verification (authentication) by and for all channel members.

Firstly, for each MSP a name needs to be specified in order to reference that MSP in the network (e.g. msp1, org2, and org3.divA). This is the name under which membership rules of an MSP representing a consortium, organization or organization division is to be referenced in a channel. This is also referred to as the MSP Identifier or MSP ID. MSP Identifiers are required to be unique per MSP instance. For example, shall two MSP instances with the same identifier be detected at the system channel genesis, orderer setup will fail.

In the case of default implementation of MSP, a set of parameters need to be specified to allow for identity (certificate) validation and signature verification. These parameters are deduced by RFC5280, and include:

+ A list of self-signed (X.509) certificates to constitute the root of trust
+ A list of X.509 certificates to represent intermediate CAs this provider considers for certificate validation; these certificates ought to be certified by exactly one of the certificates in the root of trust; intermediate CAs are optional parameters
+ A list of X.509 certificates with a verifiable certificate path to exactly one of the certificates of the root of trust to represent the administrators of this MSP; owners of these certificates are authorized to request changes to this MSP configuration (e.g. root CAs, intermediate CAs)
+ A list of Organizational Units that valid members of this MSP should include in their X.509 certificate; this is an optional configuration parameter, used when, e.g., multiple organisations leverage the same root of trust, and intermediate CAs, and have reserved an OU field for their members
+ A list of certificate revocation lists (CRLs) each corresponding to exactly one of the listed (intermediate or root) MSP Certificate Authorities; this is an optional parameter
+ A list of self-signed (X.509) certificates to constitute the TLS root of trust for TLS certificate.
+ A list of X.509 certificates to represent intermediate TLS CAs this provider considers; these certificates ought to be certified by exactly one of the certificates in the TLS root of trust; intermediate CAs are optional parameters.

Valid identities for this MSP instance are required to satisfy the following conditions:

+ They are in the form of X.509 certificates with a verifiable certificate path to exactly one of the root of trust certificates;
+ They are not included in any CRL;
+ And they list one or more of the Organizational Units of the MSP configuration in the OU field of their X.509 certificate structure.

For more information on the validity of identities in the current MSP implementation, we refer the reader to MSP Identity Validity Rules.

In addition to verification related parameters, for the MSP to enable the node on which it is instantiated to sign or authenticate, one needs to specify:

+ The signing key used for signing by the node (currently only ECDSA keys are supported), and
+ The node’s X.509 certificate, that is a valid identity under the verification parameters of this MSP.

It is important to note that MSP identities never expire; they can only be revoked by adding them to the appropriate CRLs. Additionally, there is currently no support for enforcing revocation of TLS certificates.

#####How to generate MSP certificates and their signing keys?#####
To generate X.509 certificates to feed its MSP configuration, the application can use Openssl. We emphasise that in Hyperledger Fabric there is no support for certificates including RSA keys.

Alternatively one can use cryptogen tool, whose operation is explained in Getting Started.

Hyperledger Fabric CA can also be used to generate the keys and certificates needed to configure an MSP.

#####MSP setup on the peer & orderer side#####
To set up a local MSP (for either a peer or an orderer), the administrator should create a folder (e.g. $MY_PATH/mspconfig) that contains six subfolders and a file:

1. a folder admincerts to include PEM files each corresponding to an administrator certificate
2. a folder cacerts to include PEM files each corresponding to a root CA’s certificate
3. (optional) a folder intermediatecerts to include PEM files each corresponding to an intermediate CA’s certificate
4. (optional) a file config.yaml to configure the supported Organizational Units and identity classifications (see respective sections below).
5. (optional) a folder crls to include the considered CRLs
6. a folder keystore to include a PEM file with the node’s signing key; we emphasise that currently RSA keys are not supported
7. a folder signcerts to include a PEM file with the node’s X.509 certificate
8. (optional) a folder tlscacerts to include PEM files each corresponding to a TLS root CA’s certificate
9. (optional) a folder tlsintermediatecerts to include PEM files each corresponding to an intermediate TLS CA’s certificate

In the configuration file of the node (core.yaml file for the peer, and orderer.yaml for the orderer), one needs to specify the path to the mspconfig folder, and the MSP Identifier of the node’s MSP. The path to the mspconfig folder is expected to be relative to FABRIC_CFG_PATH and is provided as the value of parameter mspConfigPath for the peer, and LocalMSPDir for the orderer. The identifier of the node’s MSP is provided as a value of parameter localMspId for the peer and LocalMSPID for the orderer. These variables can be overridden via the environment using the CORE prefix for peer (e.g. CORE_PEER_LOCALMSPID) and the ORDERER prefix for the orderer (e.g. ORDERER_GENERAL_LOCALMSPID). Notice that for the orderer setup, one needs to generate, and provide to the orderer the genesis block of the system channel. The MSP configuration needs of this block are detailed in the next section.

Reconfiguration of a “local” MSP is only possible manually, and requires that the peer or orderer process is restarted. In subsequent releases we aim to offer online/dynamic reconfiguration (i.e. without requiring to stop the node by using a node managed system chaincode).

#####Organizational Units#####
In order to configure the list of Organizational Units that valid members of this MSP should include in their X.509 certificate, the config.yaml file needs to specify the organizational unit identifiers. Here is an example:

	OrganizationalUnitIdentifiers:
	  - Certificate: "cacerts/cacert1.pem"
	    OrganizationalUnitIdentifier: "commercial"
	  - Certificate: "cacerts/cacert2.pem"
	    OrganizationalUnitIdentifier: "administrators"

The above example declares two organizational unit identifiers: commercial and administrators. An MSP identity is valid if it carries at least one of these organizational unit identifiers. The Certificate field refers to the CA or intermediate CA certificate path under which identities, having that specific OU, should be validated. The path is relative to the MSP root folder and cannot be empty.

#####Identity Classification#####
The default MSP implementation allows to further classify identities into clients and peers, based on the OUs of their x509 certificates. An identity should be classified as a client if it submits transactions, queries peers, etc. An identity should be classified as a peer if it endorses or commits transactions. In order to define clients and peers of a given MSP, the config.yaml file needs to be set appropriately. Here is an example:

	NodeOUs:
	  Enable: true
	  ClientOUIdentifier:
	    Certificate: "cacerts/cacert.pem"
	    OrganizationalUnitIdentifier: "client"
	  PeerOUIdentifier:
	    Certificate: "cacerts/cacert.pem"
	    OrganizationalUnitIdentifier: "peer"

As shown above, the NodeOUs.Enable is set to true, this enables the identify classification. Then, client (peer) identifiers are defined by setting the following properties for the NodeOUs.ClientOUIdentifier (NodeOUs.PeerOUIdentifier) key:

a.OrganizationalUnitIdentifier: Set this to the value that matches the OU that the x509 certificate of a client (peer) should contain.

b.Certificate: Set this to the CA or intermediate CA under which client (peer) identities should be validated. The field is relative to the MSP root folder. It can be empty, meaning that the identity’s x509 certificate can be validated under any CA defined in the MSP configuration.

When the classification is enabled, MSP administrators need to be clients of that MSP, meaning that their x509 certificates need to carry the OU that identifies the clients. Notice also that, an identity can be either a client or a peer. The two classifications are mutually exclusive. If an identity is neither a client nor a peer, the validation will fail.

Finally, notice that for upgraded environments the 1.1 channel capability needs to be enabled before identify classification can be used.

#####Channel MSP setup#####
At the genesis of the system, verification parameters of all the MSPs that appear in the network need to be specified, and included in the system channel’s genesis block. Recall that MSP verification parameters consist of the MSP identifier, the root of trust certificates, intermediate CA and admin certificates, as well as OU specifications and CRLs. The system genesis block is provided to the orderers at their setup phase, and allows them to authenticate channel creation requests. Orderers would reject the system genesis block, if the latter includes two MSPs with the same identifier, and consequently the bootstrapping of the network would fail.

For application channels, the verification components of only the MSPs that govern a channel need to reside in the channel’s genesis block. We emphasise that it is the responsibility of the application to ensure that correct MSP configuration information is included in the genesis blocks (or the most recent configuration block) of a channel prior to instructing one or more of their peers to join the channel.

When bootstrapping a channel with the help of the configtxgen tool, one can configure the channel MSPs by including the verification parameters of MSP in the mspconfig folder, and setting that path in the relevant section in configtx.yaml.

Reconfiguration of an MSP on the channel, including announcements of the certificate revocation lists associated to the CAs of that MSP is achieved through the creation of a config_update object by the owner of one of the administrator certificates of the MSP. The client application managed by the admin would then announce this update to the channels in which this MSP appears.

#####Best Practices#####
In this section we elaborate on best practices for MSP configuration in commonly met scenarios.

1) Mapping between organizations/corporations and MSPs

We recommend that there is a one-to-one mapping between organizations and MSPs. If a different type of mapping is chosen, the following needs to be to considered:

+ One organization employing various MSPs. This corresponds to the case of an organization including a variety of divisions each represented by its MSP, either for management independence reasons, or for privacy reasons. In this case a peer can only be owned by a single MSP, and will not recognize peers with identities from other MSPs as peers of the same organization. The implication of this is that peers may share through gossip organization-scoped data with a set of peers that are members of the same subdivision, and NOT with the full set of providers constituting the actual organization.
+ Multiple organizations using a single MSP. This corresponds to a case of a consortium of organisations that are governed by similar membership architecture. One needs to know here that peers would propagate organization-scoped messages to the peers that have an identity under the same MSP regardless of whether they belong to the same actual organization. This is a limitation of the granularity of MSP definition, and/or of the peer’s configuration.

2) One organization has different divisions (say organizational units), to which it wants to grant access to different channels.

Two ways to handle this:

+ Define one MSP to accommodate membership for all organization’s members. Configuration of that MSP would consist of a list of root CAs, intermediate CAs and admin certificates; and membership identities would include the organizational unit (OU) a member belongs to. Policies can then be defined to capture members of a specific OU, and these policies may constitute the read/write policies of a channel or endorsement policies of a chaincode. A limitation of this approach is that gossip peers would consider peers with membership identities under their local MSP as members of the same organization, and would consequently gossip with them organisation-scoped data (e.g. their status).
+ Defining one MSP to represent each division. This would involve specifying for each division, a set of certificates for root CAs, intermediate CAs, and admin Certs, such that there is no overlapping certification path across MSPs. This would mean that, for example, a different intermediate CA per subdivision is employed. Here the disadvantage is the management of more than one MSPs instead of one, but this circumvents the issue present in the previous approach. One could also define one MSP for each division by leveraging an OU extension of the MSP configuration.

3) Separating clients from peers of the same organization.

In many cases it is required that the “type” of an identity is retrievable from the identity itself (e.g. it may be needed that endorsements are guaranteed to have derived by peers, and not clients or nodes acting solely as orderers).

There is limited support for such requirements.

One way to allow for this separation is to to create a separate intermediate CA for each node type - one for clients and one for peers/orderers; and configure two different MSPs - one for clients and one for peers/orderers. Channels this organization should be accessing would need to include both MSPs, while endorsement policies will leverage only the MSP that refers to the peers. This would ultimately result in the organization being mapped to two MSP instances, and would have certain consequences on the way peers and clients interact.

Gossip would not be drastically impacted as all peers of the same organization would still belong to one MSP. Peers can restrict the execution of certain system chaincodes to local MSP based policies. For example, peers would only execute “joinChannel” request if the request is signed by the admin of their local MSP who can only be a client (end-user should be sitting at the origin of that request). We can go around this inconsistency if we accept that the only clients to be members of a peer/orderer MSP would be the administrators of that MSP.

Another point to be considered with this approach is that peers authorize event registration requests based on membership of request originator within their local MSP. Clearly, since the originator of the request is a client, the request originator is always deemed to belong to a different MSP than the requested peer and the peer would reject the request.

4) Admin and CA certificates.

It is important to set MSP admin certificates to be different than any of the certificates considered by the MSP for root of trust, or intermediate CAs. This is a common (security) practice to separate the duties of management of membership components from the issuing of new certificates, and/or validation of existing ones.

5) Blacklisting an intermediate CA.

As mentioned in previous sections, reconfiguration of an MSP is achieved by reconfiguration mechanisms (manual reconfiguration for the local MSP instances, and via properly constructed config_update messages for MSP instances of a channel). Clearly, there are two ways to ensure an intermediate CA considered in an MSP is no longer considered for that MSP’s identity validation:

1. Reconfigure the MSP to no longer include the certificate of that intermediate CA in the list of trusted intermediate CA certs. For the locally configured MSP, this would mean that the certificate of this CA is removed from the intermediatecerts folder.
2. Reconfigure the MSP to include a CRL produced by the root of trust which denounces the mentioned intermediate CA’s certificate.

In the current MSP implementation we only support method (1) as it is simpler and does not require blacklisting the no longer considered intermediate CA.

6) CAs and TLS CAs

MSP identities’ root CAs and MSP TLS certificates’ root CAs (and relative intermediate CAs) need to be declared in different folders. This is to avoid confusion between different classes of certificates. It is not forbidden to reuse the same CAs for both MSP identities and TLS certificates but best practices suggest to avoid this in production.

####Channel Configuration(configtx)####
Shared configuration for a Hyperledger Fabric blockchain network is stored in a collection configuration transactions, one per channel. Each configuration transaction is usually referred to by the shorter name configtx.

Channel configuration has the following important properties:

1. Versioned: All elements of the configuration have an associated version which is advanced with every modification. Further, every committed configuration receives a sequence number.
2. Permissioned: Each element of the configuration has an associated policy which governs whether or not modification to that element is permitted. Anyone with a copy of the previous configtx (and no additional info) may verify the validity of a new config based on these policies.
3. Hierarchical: A root configuration group contains sub-groups, and each group of the hierarchy has associated values and policies. These policies can take advantage of the hierarchy to derive policies at one level from policies of lower levels.

#####Anatomy of a configuration#####
Configuration is stored as a transaction of type HeaderType_CONFIG in a block with no other transactions. These blocks are referred to as Configuration Blocks, the first of which is referred to as the Genesis Block.

The proto structures for configuration are stored in fabric/protos/common/configtx.proto. The Envelope of type HeaderType_CONFIG encodes a ConfigEnvelope message as the Payload data field. The proto for ConfigEnvelope is defined as follows:

	message ConfigEnvelope {
	    Config config = 1;
	    Envelope last_update = 2;
	}

The last_update field is defined below in the Updates to configuration section, but is only necessary when validating the configuration, not reading it. Instead, the currently committed configuration is stored in the config field, containing a Config message.

	message Config {
	    uint64 sequence = 1;
	    ConfigGroup channel_group = 2;
	}

The sequence number is incremented by one for each committed configuration. The channel_group field is the root group which contains the configuration. The ConfigGroup structure is recursively defined, and builds a tree of groups, each of which contains values and policies. It is defined as follows:

	message ConfigGroup {
	    uint64 version = 1;
	    map<string,ConfigGroup> groups = 2;
	    map<string,ConfigValue> values = 3;
	    map<string,ConfigPolicy> policies = 4;
	    string mod_policy = 5;
	}

Because ConfigGroup is a recursive structure, it has hierarchical arrangement. The following example is expressed for clarity in golang notation.

	// Assume the following groups are defined
	var root, child1, child2, grandChild1, grandChild2, grandChild3 *ConfigGroup
	
	// Set the following values
	root.Groups["child1"] = child1
	root.Groups["child2"] = child2
	child1.Groups["grandChild1"] = grandChild1
	child2.Groups["grandChild2"] = grandChild2
	child2.Groups["grandChild3"] = grandChild3
	
	// The resulting config structure of groups looks like:
	// root:
	//     child1:
	//         grandChild1
	//     child2:
	//         grandChild2
	//         grandChild3

Each group defines a level in the config hierarchy, and each group has an associated set of values (indexed by string key) and policies (also indexed by string key).

Values are defined by:

	message ConfigValue {
	    uint64 version = 1;
	    bytes value = 2;
	    string mod_policy = 3;
	}

Policies are defined by:

	message ConfigPolicy {
	    uint64 version = 1;
	    Policy policy = 2;
	    string mod_policy = 3;
	}

Note that Values, Policies, and Groups all have a version and a mod_policy. The version of an element is incremented each time that element is modified. The mod_policy is used to govern the required signatures to modify that element. For Groups, modification is adding or removing elements to the Values, Policies, or Groups maps (or changing the mod_policy). For Values and Policies, modification is changing the Value and Policy fields respectively (or changing the mod_policy). Each element’s mod_policy is evaluated in the context of the current level of the config. Consider the following example mod policies defined at Channel.Groups["Application"] (Here, we use the golang map reference syntax, so Channel.Groups["Application"].Policies["policy1"] refers to the base Channel group’s Application group’s Policies map’s policy1 policy.)

+ policy1 maps to Channel.Groups["Application"].Policies["policy1"]
+ Org1/policy2 maps to Channel.Groups["Application"].Groups["Org1"].Policies["policy2"]
+ /Channel/policy3 maps to Channel.Policies["policy3"]

Note that if a mod_policy references a policy which does not exist, the item cannot be modified.

#####Configuration updates#####
Configuration updates are submitted as an Envelope message of type HeaderType_CONFIG_UPDATE. The Payload data of the transaction is a marshaled ConfigUpdateEnvelope. The ConfigUpdateEnvelope is defined as follows:

	message ConfigUpdateEnvelope {
	    bytes config_update = 1;
	    repeated ConfigSignature signatures = 2;
	}

The signatures field contains the set of signatures which authorizes the config update. Its message definition is:

	message ConfigSignature {
	    bytes signature_header = 1;
	    bytes signature = 2;
	}

The signature_header is as defined for standard transactions, while the signature is over the concatenation of the signature_header bytes and the config_update bytes from the ConfigUpdateEnvelope message.

The ConfigUpdateEnvelope config_update bytes are a marshaled ConfigUpdate message which is defined as follows:

	message ConfigUpdate {
	    string channel_id = 1;
	    ConfigGroup read_set = 2;
	    ConfigGroup write_set = 3;
	}

The channel_id is the channel ID the update is bound for, this is necessary to scope the signatures which support this reconfiguration.

The read_set specifies a subset of the existing configuration, specified sparsely where only the version field is set and no other fields must be populated. The particular ConfigValue value or ConfigPolicy policy fields should never be set in the read_set. The ConfigGroup may have a subset of its map fields populated, so as to reference an element deeper in the config tree. For instance, to include the Application group in the read_set, its parent (the Channel group) must also be included in the read set, but, the Channel group does not need to populate all of the keys, such as the Orderer group key, or any of the values or policies keys.

The write_set specifies the pieces of configuration which are modified. Because of the hierarchical nature of the configuration, a write to an element deep in the hierarchy must contain the higher level elements in its write_set as well. However, for any element in the write_set which is also specified in the read_set at the same version, the element should be specified sparsely, just as in the read_set.

For example, given the configuration:

	Channel: (version 0)
	    Orderer (version 0)
	    Appplication (version 3)
	       Org1 (version 2)

To submit a configuration update which modifies Org1, the read_set would be:

	Channel: (version 0)
    	Application: (version 3)

and the write_set would be

	Channel: (version 0)
	    Application: (version 3)
	        Org1 (version 3)

When the CONFIG_UPDATE is received, the orderer computes the resulting CONFIG by doing the following:

1. Verifies the channel_id and read_set. All elements in the read_set must exist at the given versions.
2. Computes the update set by collecting all elements in the write_set which do not appear at the same version in the read_set.
3. Verifies that each element in the update set increments the version number of the element update by exactly 1.
4. Verifies that the signature set attached to the ConfigUpdateEnvelope satisfies the mod_policy for each element in the update set.
5. Computes a new complete version of the config by applying the update set to the current config.
6. Writes the new config into a ConfigEnvelope which includes the CONFIG_UPDATE as the last_update field and the new config encoded in the config field, along with the incremented sequence value.
7. Writes the new ConfigEnvelope into a Envelope of type CONFIG, and ultimately writes this as the sole transaction in a new configuration block.

When the peer (or any other receiver for Deliver) receives this configuration block, it should verify that the config was appropriately validated by applying the last_update message to the current config and verifying that the orderer-computed config field contains the correct new configuration.

#####Permitted configuration groups and values#####
Any valid configuration is a subset of the following configuration. Here we use the notation peer.<MSG> to define a ConfigValue whose value field is a marshaled proto message of name <MSG> defined in fabric/protos/peer/configuration.proto. The notations common.<MSG>, msp.<MSG>, and orderer.<MSG> correspond similarly, but with their messages defined in fabric/protos/common/configuration.proto, fabric/protos/msp/mspconfig.proto, and fabric/protos/orderer/configuration.proto respectively.

Note, that the keys {{org_name}} and {{consortium_name}} represent arbitrary names, and indicate an element which may be repeated with different names.

	&ConfigGroup{
	    Groups: map<string, *ConfigGroup> {
	        "Application":&ConfigGroup{
	            Groups:map<String, *ConfigGroup> {
	                {{org_name}}:&ConfigGroup{
	                    Values:map<string, *ConfigValue>{
	                        "MSP":msp.MSPConfig,
	                        "AnchorPeers":peer.AnchorPeers,
	                    },
	                },
	            },
	        },
	        "Orderer":&ConfigGroup{
	            Groups:map<String, *ConfigGroup> {
	                {{org_name}}:&ConfigGroup{
	                    Values:map<string, *ConfigValue>{
	                        "MSP":msp.MSPConfig,
	                    },
	                },
	            },
	
	            Values:map<string, *ConfigValue> {
	                "ConsensusType":orderer.ConsensusType,
	                "BatchSize":orderer.BatchSize,
	                "BatchTimeout":orderer.BatchTimeout,
	                "KafkaBrokers":orderer.KafkaBrokers,
	            },
	        },
	        "Consortiums":&ConfigGroup{
	            Groups:map<String, *ConfigGroup> {
	                {{consortium_name}}:&ConfigGroup{
	                    Groups:map<string, *ConfigGroup> {
	                        {{org_name}}:&ConfigGroup{
	                            Values:map<string, *ConfigValue>{
	                                "MSP":msp.MSPConfig,
	                            },
	                        },
	                    },
	                    Values:map<string, *ConfigValue> {
	                        "ChannelCreationPolicy":common.Policy,
	                    }
	                },
	            },
	        },
	    },
	
	    Values: map<string, *ConfigValue> {
	        "HashingAlgorithm":common.HashingAlgorithm,
	        "BlockHashingDataStructure":common.BlockDataHashingStructure,
	        "Consortium":common.Consortium,
	        "OrdererAddresses":common.OrdererAddresses,
	    },
	}

#####Orderer system channel configuration#####
The ordering system channel needs to define ordering parameters, and consortiums for creating channels. There must be exactly one ordering system channel for an ordering service, and it is the first channel to be created (or more accurately bootstrapped). It is recommended never to define an Application section inside of the ordering system channel genesis configuration, but may be done for testing. Note that any member with read access to the ordering system channel may see all channel creations, so this channel’s access should be restricted.

The ordering parameters are defined as the following subset of config:

	&ConfigGroup{
	    Groups: map<string, *ConfigGroup> {
	        "Orderer":&ConfigGroup{
	            Groups:map<String, *ConfigGroup> {
	                {{org_name}}:&ConfigGroup{
	                    Values:map<string, *ConfigValue>{
	                        "MSP":msp.MSPConfig,
	                    },
	                },
	            },
	
	            Values:map<string, *ConfigValue> {
	                "ConsensusType":orderer.ConsensusType,
	                "BatchSize":orderer.BatchSize,
	                "BatchTimeout":orderer.BatchTimeout,
	                "KafkaBrokers":orderer.KafkaBrokers,
	            },
	        },
	    },

Each organization participating in ordering has a group element under the Orderer group. This group defines a single parameter MSP which contains the cryptographic identity information for that organization. The Values of the Orderer group determine how the ordering nodes function. They exist per channel, so orderer.BatchTimeout for instance may be specified differently on one channel than another.

At startup, the orderer is faced with a filesystem which contains information for many channels. The orderer identifies the system channel by identifying the channel with the consortiums group defined. The consortiums group has the following structure.

	&ConfigGroup{
	    Groups: map<string, *ConfigGroup> {
	        "Consortiums":&ConfigGroup{
	            Groups:map<String, *ConfigGroup> {
	                {{consortium_name}}:&ConfigGroup{
	                    Groups:map<string, *ConfigGroup> {
	                        {{org_name}}:&ConfigGroup{
	                            Values:map<string, *ConfigValue>{
	                                "MSP":msp.MSPConfig,
	                            },
	                        },
	                    },
	                    Values:map<string, *ConfigValue> {
	                        "ChannelCreationPolicy":common.Policy,
	                    }
	                },
	            },
	        },
	    },
	},

Note that each consortium defines a set of members, just like the organizational members for the ordering orgs. Each consortium also defines a ChannelCreationPolicy. This is a policy which is applied to authorize channel creation requests. Typically, this value will be set to an ImplicitMetaPolicy requiring that the new members of the channel sign to authorize the channel creation. More details about channel creation follow later in this document.

#####Application channel configuration#####
Application configuration is for channels which are designed for application type transactions. It is defined as follows:

	&ConfigGroup{
	    Groups: map<string, *ConfigGroup> {
	        "Application":&ConfigGroup{
	            Groups:map<String, *ConfigGroup> {
	                {{org_name}}:&ConfigGroup{
	                    Values:map<string, *ConfigValue>{
	                        "MSP":msp.MSPConfig,
	                        "AnchorPeers":peer.AnchorPeers,
	                    },
	                },
	            },
	        },
	    },
	}

Just like with the Orderer section, each organization is encoded as a group. However, instead of only encoding the MSP identity information, each org additionally encodes a list of AnchorPeers. This list allows the peers of different organizations to contact each other for peer gossip networking.

The application channel encodes a copy of the orderer orgs and consensus options to allow for deterministic updating of these parameters, so the same Orderer section from the orderer system channel configuration is included. However from an application perspective this may be largely ignored.

#####Channel creation#####
When the orderer receives a CONFIG_UPDATE for a channel which does not exist, the orderer assumes that this must be a channel creation request and performs the following.

1. The orderer identifies the consortium which the channel creation request is to be performed for. It does this by looking at the Consortium value of the top level group.
2. The orderer verifies that the organizations included in the Application group are a subset of the organizations included in the corresponding consortium and that the ApplicationGroup is set to version 1.
3. The orderer verifies that if the consortium has members, that the new channel also has application members (creation consortiums and channels with no members is useful for testing only).
4. The orderer creates a template configuration by taking the Orderer group from the ordering system channel, and creating an Application group with the newly specified members and specifying its mod_policy to be the ChannelCreationPolicy as specified in the consortium config. Note that the policy is evaluated in the context of the new configuration, so a policy requiring ALL members, would require signatures from all the new channel members, not all the members of the consortium.
5. The orderer then applies the CONFIG_UPDATE as an update to this template configuration. Because the CONFIG_UPDATE applies modifications to the Application group (its version is 1), the config code validates these updates against the ChannelCreationPolicy. If the channel creation contains any other modifications, such as to an individual org’s anchor peers, the corresponding mod policy for the element will be invoked.
6. The new CONFIG transaction with the new channel config is wrapped and sent for ordering on the ordering system channel. After ordering, the channel is created.

####Endorsement policies####
Endorsement policies are used to instruct a peer on how to decide whether a transaction is properly endorsed. When a peer receives a transaction, it invokes the VSCC (Validation System Chaincode) associated with the transaction’s Chaincode as part of the transaction validation flow to determine the validity of the transaction. Recall that a transaction contains one or more endorsement from as many endorsing peers. VSCC is tasked to make the following determinations:

+ all endorsements are valid (i.e. they are valid signatures from valid certificates over the expected message)
+ there is an appropriate number of endorsements
+ endorsements come from the expected source(s)

Endorsement policies are a way of specifying the second and third points.

#####Endorsement policy syntax in the CLI#####
In the CLI, a simple language is used to express policies in terms of boolean expressions over principals.

A principal is described in terms of the MSP that is tasked to validate the identity of the signer and of the role that the signer has within that MSP. Four roles are supported: member, admin, client, and peer. Principals are described as MSP.ROLE, where MSP is the MSP ID that is required, and ROLE is one of the four strings member, admin, client and peer. Examples of valid principals are 'Org0.admin' (any administrator of the Org0 MSP) or 'Org1.member' (any member of the Org1 MSP), 'Org1.client' (any client of the Org1 MSP), and 'Org1.peer' (any peer of the Org1 MSP).

The syntax of the language is:

EXPR(E[, E...])

where EXPR is either AND or OR, representing the two boolean expressions and E is either a principal (with the syntax described above) or another nested call to EXPR.

For example:
+ AND('Org1.member', 'Org2.member', 'Org3.member') requests 1 signature from each of the three principals
+ OR('Org1.member', 'Org2.member') requests 1 signature from either one of the two principals
+ OR('Org1.member', AND('Org2.member', 'Org3.member')) requests either one signature from a member of the Org1 MSP or 1 signature from a member of the Org2 MSP and 1 signature from a member of the Org3 MSP.

#####Specifying endorsement policies for a chaincode#####
Using this language, a chaincode deployer can request that the endorsements for a chaincode be validated against the specified policy.

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		if not specified at instantiation time, the endorsement policy defaults to “any member of the organizations in the channel”. For example, a channel with “Org1” and “Org2” would have a default endorsement policy of “OR(‘Org1.member’, ‘Org2.member’)”.
		</td>
	</tr>
</table>

The policy can be specified at instantiate time using the -P switch, followed by the policy.

For example:

	peer chaincode instantiate -C <channelid> -n mycc -P "AND('Org1.member', 'Org2.member')"

This command deploys chaincode mycc with the policy AND('Org1.member', 'Org2.member') which would require that a member of both Org1 and Org2 sign the transaction.

Notice that, if the identity classification is enabled (see Membership Service Providers (MSP)), one can use the PEER role to restrict endorsement to only peers.

For example:

	peer chaincode instantiate -C <channelid> -n mycc -P "AND('Org1.peer', 'Org2.peer')"

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		A new organization added to the channel after instantiation can query a chaincode (provided the query has appropriate authorization as defined by channel policies and any application level checks enforced by the chaincode) but will not be able to commit a transaction endorsed by it. The endorsement policy needs to be modified to allow transactions to be committed with endorsements from the new organization (see Upgrade and Invoke Chaincode).
		</td>
	</tr>
</table>

####Error handing####
#####General Overview#####
Hyperledger Fabric code should use the vendored package github.com/pkg/errors in place of the standard error type provided by Go. This package allows easy generation and display of stack traces with error messages.

#####Usage Instructions#####
github.com/pkg/errors should be used in place of all calls to fmt.Errorf() or errors.New(). Using this package will generate a call stack that will be appended to the error message.

Using this package is simple and will only require easy tweaks to your code.

First, you’ll need to import github.com/pkg/errors.

Next, update all errors that are generated by your code to use one of the error creation functions (errors.New(), errors.Errorf(), errors.WithMessage(), errors.Wrap(), errors.Wrapf().

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		See https://godoc.org/github.com/pkg/errors for complete documentation of the available error creation function. Also, refer to the General guidelines section below for more specific guidelines for using the package for Fabric code.
		</td>
	</tr>
</table>

Finally, change the formatting directive for any logger or fmt.Printf() calls from %s to %+v to print the call stack along with the error message.

#####General guidelines for error handing in Hyperledger Fabric#####
+ If you are servicing a user request, you should log the error and return it.
+ If the error comes from an external source, such as a Go library or vendored package, wrap the error using errors.Wrap() to generate a call stack for the error.
+ If the error comes from another Fabric function, add further context, if desired, to the error message using errors.WithMessage() while leaving the call stack unaffected.
+ A panic should not be allowed to propagate to other packages.

#####Example program#####
The following example program provides a clear demonstration of using the package:

	package main
	
	import (
	  "fmt"
	
	  "github.com/pkg/errors"
	)
	
	func wrapWithStack() error {
	  err := createError()
	  // do this when error comes from external source (go lib or vendor)
	  return errors.Wrap(err, "wrapping an error with stack")
	}
	func wrapWithoutStack() error {
	  err := createError()
	  // do this when error comes from internal Fabric since it already has stack trace
	  return errors.WithMessage(err, "wrapping an error without stack")
	}
	func createError() error {
	  return errors.New("original error")
	}
	
	func main() {
	  err := createError()
	  fmt.Printf("print error without stack: %s\n\n", err)
	  fmt.Printf("print error with stack: %+v\n\n", err)
	  err = wrapWithoutStack()
	  fmt.Printf("%+v\n\n", err)
	  err = wrapWithStack()
	  fmt.Printf("%+v\n\n", err)
	}

####Logging Control####
#####Overview#####
Logging in the peer application and in the shim interface to chaincodes is programmed using facilities provided by the github.com/op/go-logging package. This package supports

+ Logging control based on the severity of the message
+ Logging control based on the software module generating the message
+ Different pretty-printing options based on the severity of the message

All logs are currently directed to stderr, and the pretty-printing is currently fixed. However global and module-level control of logging by severity is provided for both users and developers. There are currently no formalized rules for the types of information provided at each severity level, however when submitting bug reports the developers may want to see full logs down to the DEBUG level.

In pretty-printed logs the logging level is indicated both by color and by a 4-character code, e.g, “ERRO” for ERROR, “DEBU” for DEBUG, etc. In the logging context a module is an arbitrary name (string) given by developers to groups of related messages. In the pretty-printed example below, the logging modules “peer”, “rest” and “main” are generating logs.

	16:47:09.634 [peer] GetLocalAddress -> INFO 033 Auto detected peer address: 9.3.158.178:7051
	16:47:09.635 [rest] StartOpenchainRESTServer -> INFO 035 Initializing the REST service...
	16:47:09.635 [main] serve -> INFO 036 Starting peer with id=name:"vp1" , network id=dev, address=9.3.158.178:7051, discovery.rootnode=, validator=true

An arbitrary number of logging modules can be created at runtime, therefore there is no “master list” of modules, and logging control constructs can not check whether logging modules actually do or will exist. Also note that the logging module system does not understand hierarchy or wildcarding: You may see module names like “foo/bar” in the code, but the logging system only sees a flat string. It doesn’t understand that “foo/bar” is related to “foo” in any way, or that “foo/*” might indicate all “submodules” of foo.

#####peer#####
The logging level of the peer command can be controlled from the command line for each invocation using the --logging-level flag, for example

	peer node start --logging-level=debug

The default logging level for each individual peer subcommand can also be set in the core.yaml file. For example the key logging.node sets the default level for the node subcommmand. Comments in the file also explain how the logging level can be overridden in various ways by using environment varaibles.

Logging severity levels are specified using case-insensitive strings chosen from

	CRITICAL | ERROR | WARNING | NOTICE | INFO | DEBUG

The full logging level specification for the peer is of the form

	[<module>[,<module>...]=]<level>[:[<module>[,<module>...]=]<level>...]

A logging level by itself is taken as the overall default. Otherwise, overrides for individual or groups of modules can be specified using the

	<module>[,<module>...]=<level>

syntax. Examples of specifications (valid for all of --logging-level, environment variable and core.yaml settings):

	info                                       - Set default to INFO
	warning:main,db=debug:chaincode=info       - Default WARNING; Override for main,db,chaincode
	chaincode=info:main=debug:db=debug:warning - Same as above

#####Go chaincodes#####
The standard mechanism to log within a chaincode application is to integrate with the logging transport exposed to each chaincode instance via the peer. The chaincode shim package provides APIs that allow a chaincode to create and manage logging objects whose logs will be formatted and interleaved consistently with the shim logs.

As independently executed programs, user-provided chaincodes may technically also produce output on stdout/stderr. While naturally useful for “devmode”, these channels are normally disabled on a production network to mitigate abuse from broken or malicious code. However, it is possible to enable this output even for peer-managed containers (e.g. “netmode”) on a per-peer basis via the CORE_VM_DOCKER_ATTACHSTDOUT=true configuration option.

Once enabled, each chaincode will receive its own logging channel keyed by its container-id. Any output written to either stdout or stderr will be integrated with the peer’s log on a per-line basis. It is not recommended to enable this for production.

######API######
NewLogger(name string) *ChaincodeLogger - Create a logging object for use by a chaincode

(c *ChaincodeLogger) SetLevel(level LoggingLevel) - Set the logging level of the logger

(c *ChaincodeLogger) IsEnabledFor(level LoggingLevel) bool - Return true if logs will be generated at the given level

LogLevel(levelString string) (LoggingLevel, error) - Convert a string to a LoggingLevel

A LoggingLevel is a member of the enumeration

	LogDebug, LogInfo, LogNotice, LogWarning, LogError, LogCritical

which can be used directly, or generated by passing a case-insensitive version of the strings

	DEBUG, INFO, NOTICE, WARNING, ERROR, CRITICAL

to the LogLevel API.

Formatted logging at various severity levels is provided by the functions

	(c *ChaincodeLogger) Debug(args ...interface{})
	(c *ChaincodeLogger) Info(args ...interface{})
	(c *ChaincodeLogger) Notice(args ...interface{})
	(c *ChaincodeLogger) Warning(args ...interface{})
	(c *ChaincodeLogger) Error(args ...interface{})
	(c *ChaincodeLogger) Critical(args ...interface{})
	
	(c *ChaincodeLogger) Debugf(format string, args ...interface{})
	(c *ChaincodeLogger) Infof(format string, args ...interface{})
	(c *ChaincodeLogger) Noticef(format string, args ...interface{})
	(c *ChaincodeLogger) Warningf(format string, args ...interface{})
	(c *ChaincodeLogger) Errorf(format string, args ...interface{})
	(c *ChaincodeLogger) Criticalf(format string, args ...interface{})

The f forms of the logging APIs provide for precise control over the formatting of the logs. The non-f forms of the APIs currently insert a space between the printed representations of the arguments, and arbitrarily choose the formats to use.

In the current implementation, the logs produced by the shim and a ChaincodeLogger are timestamped, marked with the logger name and severity level, and written to stderr. Note that logging level control is currently based on the name provided when the ChaincodeLogger is created. To avoid ambiguities, all ChaincodeLogger should be given unique names other than “shim”. The logger name will appear in all log messages created by the logger. The shim logs as “shim”.

Go language chaincodes can also control the logging level of the chaincode shim interface through the SetLoggingLevel API.

SetLoggingLevel(LoggingLevel level) - Control the logging level of the shim

The default logging level for the shim is LogDebug.

Below is a simple example of how a chaincode might create a private logging object logging at the LogInfo level, and also control the amount of logging provided by the shim based on an environment variable.

	var logger = shim.NewLogger("myChaincode")

	func main() {
	
	    logger.SetLevel(shim.LogInfo)
	
	    logLevel, _ := shim.LogLevel(os.Getenv("SHIM_LOGGING_LEVEL"))
	    shim.SetLoggingLevel(logLevel)
	    ...
	}

####Securing Communication With Transport Layer Security(TLS)####
Fabric supports for secure communication between nodes using TLS. TLS communication can use both one-way (server only) and two-way (server and client) authentication.

#####Configuring TLS for peers nodes#####
A peer node is both a TLS server and a TLS client. It is the former when another peer node, application, or the CLI makes a connection to it and the latter when it makes a connection to another peer node or orderer.

To enable TLS on a peer node set the following peer configuration properties:

+ peer.tls.enabled = true
+ peer.tls.cert.file = fully qualified path of the file that contains the TLS server certificate
+ peer.tls.key.file = fully qualified path of the file that contains the TLS server private key
+ peer.tls.rootcert.file = fully qualified path of the file that contains the certificate chain of the certificate authority(CA) that issued TLS server certificate

By default, TLS client authentication is turned off when TLS is enabled on a peer node. This means that the peer node will not verify the certificate of a client (another peer node, application, or the CLI) during a TLS handshake. To enable TLS client authentication on a peer node, set the peer configuration property peer.tls.clientAuthRequired to true and set the peer.tls.clientRootCAs.files property to the CA chain file(s) that contain(s) the CA certificate chain(s) that issued TLS certificates for your organization’s clients.

By default, a peer node will use the same certificate and private key pair when acting as a TLS server and client. To use a different certificate and private key pair for the client side, set the peer.tls.clientCert.file and peer.tls.clientKey.file configuration properties to the fully qualified path of the client certificate and key file, respectively.

TLS with client authentication can also be enabled by setting the following environment variables:

+ CORE_PEER_TLS_ENABLED = true
+ CORE_PEER_TLS_CERT_FILE = fully qualified path of the server certificate
+ CORE_PEER_TLS_KEY_FILE = fully qualified path of the server private key
+ CORE_PEER_TLS_ROOTCERT_FILE = fully qualified path of the CA chain file
+ CORE_PEER_TLS_CLIENTAUTHREQUIRED = true
+ CORE_PEER_TLS_CLIENTROOTCAS_FILES = fully qualified path of the CA chain file
+ CORE_PEER_TLS_CLIENTCERT_FILE = fully qualified path of the client certificate
+ CORE_PEER_TLS_CLIENTKEY_FILE = fully qualified path of the client key

When client authentication is enabled on a peer node, a client is required to send its certificate during a TLS handshake. If the client does not send its certificate, the handshake will fail and the peer will close the connection.

When a peer joins a channel, root CA certificate chains of the channel members are read from the config block of the channel and are added to the TLS client and server root CAs data structure. So, peer to peer communication, peer to orderer communication should work seamlessly.

#####Configuring TLS for orderer nodes#####
To enable TLS on an orderer node, set the following orderer configuration properties:

+ General.TLS.Enabled = true
+ General.TLS.PrivateKey = fully qualified path of the file that contains the server private key
+ General.TLS.Certificate = fully qualified path of the file that contains the server certificate
+ General.TLS.RootCAs = fully qualified path of the file that contains the certificate chain of the CA that issued TLS server certificate

By default, TLS client authentication is turned off on orderer, as is the case with peer. To enable TLS client authentication, set the following config properties:

+ General.TLS.ClientAuthRequired = true
+ General.TLS.ClientRootCAs = fully qualified path of the file that contains the certificate chain of the CA that issued the TLS server certificate

TLS with client authentication can also be enabled by setting the following environment variables:

+ ORDERER_GENERAL_TLS_ENABLED = true
+ ORDERER_GENERAL_TLS_PRIVATEKEY = fully qualified path of the file that contains the server private key
+ ORDERER_GENERAL_TLS_CERTIFICATE = fully qualified path of the file that contains the server certificate
+ ORDERER_GENERAL_TLS_ROOTCAS = fully qualified path of the file that contains the certificate chain of the CA that issued TLS server certificate
+ ORDERER_GENERAL_TLS_CLIENTAUTHREQUIRED = true
+ ORDERER_GENERAL_TLS_CLIENTROOTCAS = fully qualified path of the file that contains the certificate chain of the CA that issued TLS server certificate

#####Configuring TLS for the peer CLI#####
The following environment variables must be set when running peer CLI commands against a TLS enabled peer node:

+ CORE_PEER_TLS_ENABLED = true
+ CORE_PEER_TLS_ROOTCERT_FILE = fully qualified path of the file that contains cert chain of the CA that issued the TLS server cert

If TLS client authentication is also enabled on the remote server, the following variables must to be set in addition to those above:

+ CORE_PEER_TLS_CLIENTAUTHREQUIRED = true
+ CORE_PEER_TLS_CLIENTCERT_FILE = fully qualified path of the client certificate
+ CORE_PEER_TLS_CLIENTKEY_FILE = fully qualified path of the client private key

When running a command that connects to orderer service, like peer channel <create|update|fetch> or peer chaincode <invoke|instantiate>, following command line arguments must also be specified if TLS is enabled on the orderer:

+ -tls
+ -cafile &lt;fully qualified path of the file that contains cert chain of the orderer CA&gt;

If TLS client authentication is enabled on the orderer, the following arguments must be specified as well:

+ –clientauth
+ –keyfile &lt;fully qualified path of the file that contains the client private key&gt;
+ –certfile &lt;fully qualified path of the file that contains the client certificate&gt;

#####Debugging TLS issues#####
Before debugging TLS issues, it is advisable to enable GRPC debug on both the TLS client and the server side to get additional information. To enable GRPC debug, set the environment variable CORE_LOGGING_GRPC to DEBUG.

If you see the error message remote error: tls: bad certificate on the client side, it usually means that the TLS server has enabled client authentication and the server either did not receive the correct client certificate or it received a client certificate that it does not trust. Make sure the client is sending its certificate and that it has been signed by one of the CA certificates trusted by the peer or orderer node.

If you see the error message remote error: tls: bad certificate in your chaincode logs, ensure that your chaincode has been built using the chaincode shim provided with Fabric v1.1 or newer. If your chaincode does not contain a vendored copy of the shim, deleting the chaincode container and restarting its peer will rebuild the chaincode container using the current shim version. If your chaincode vendored a previous version of the shim, review the documentation on how to upgrade-vendored-shim.

####Bringing up a Kafka-based Ordering Service####
#####Caveat emptor#####
This document assumes that the reader generally knows how to set up a Kafka cluster and a ZooKeeper ensemble. The purpose of this guide is to identify the steps you need to take so as to have a set of Hyperledger Fabric ordering service nodes (OSNs) use your Kafka cluster and provide an ordering service to your blockchain network.

#####Big picture#####
Each channel maps to a separate single-partition topic in Kafka. When an OSN receives transactions via the Broadcast RPC, it checks to make sure that the broadcasting client has permissions to write on the channel, then relays (i.e. produces) those transactions to the appropriate partition in Kafka. This partition is also consumed by the OSN which groups the received transactions into blocks locally, persists them in its local ledger, and serves them to receiving clients via the Deliver RPC. For low-level details, refer to the document that describes how we came to this design — Figure 8 is a schematic representation of the process described above.

#####Steps#####
Let K and Z be the number of nodes in the Kafka cluster and the ZooKeeper ensemble respectively:

1. At a minimum, K should be set to 4. (As we will explain in Step 4 below, this is the minimum number of nodes necessary in order to exhibit crash fault tolerance, i.e. with 4 brokers, you can have 1 broker go down, all channels will continue to be writeable and readable, and new channels can be created.)
2. Z will either be 3, 5, or 7. It has to be an odd number to avoid split-brain scenarios, and larger than 1 in order to avoid single point of failures. Anything beyond 7 ZooKeeper servers is considered an overkill.

	Then proceed as follows:

3. Orderers: Encode the Kafka-related information in the network’s genesis block. If you are using configtxgen, edit configtx.yaml —or pick a preset profile for the system channel’s genesis block— so that:

	1. Orderer.OrdererType is set to kafka.
	2. Orderer.Kafka.Brokers contains the address of at least two of the Kafka brokers in your cluster in IP:port notation. The list does not need to be exhaustive. (These are your bootstrap brokers.)

4. Orderers: Set the maximum block size. Each block will have at most Orderer.AbsoluteMaxBytes bytes (not including headers), a value that you can set in configtx.yaml. Let the value you pick here be A and make note of it — it will affect how you configure your Kafka brokers in Step 6.
5. Orderers: Create the genesis block. Use configtxgen. The settings you picked in Steps 3 and 4 above are system-wide settings, i.e. they apply across the network for all the OSNs. Make note of the genesis block’s location.
6. Kafka cluster: Configure your Kafka brokers appropriately. Ensure that every Kafka broker has these keys configured:

	1. unclean.leader.election.enable = false — Data consistency is key in a blockchain environment. We cannot have a channel leader chosen outside of the in-sync replica set, or we run the risk of overwriting the offsets that the previous leader produced, and —as a result— rewrite the blockchain that the orderers produce.
	2. min.insync.replicas = M — Where you pick a value M such that 1 < M < N (see default.replication.factor below). Data is considered committed when it is written to at least M replicas (which are then considered in-sync and belong to the in-sync replica set, or ISR). In any other case, the write operation returns an error. Then:
	

		1. If up to N-M replicas —out of the N that the channel data is written to— become unavailable, operations proceed normally.
		2. If more replicas become unavailable, Kafka cannot maintain an ISR set of M, so it stops accepting writes. Reads work without issues. The channel becomes writeable again when M replicas get in-sync.
	3. default.replication.factor = N — Where you pick a value N such that N < K. A replication factor of N means that each channel will have its data replicated to N brokers. These are the candidates for the ISR set of a channel. As we noted in the min.insync.replicas section above, not all of these brokers have to be available all the time. N should be set strictly smaller to K because channel creations cannot go forward if less than N brokers are up. So if you set N = K, a single broker going down means that no new channels can be created on the blockchain network — the crash fault tolerance of the ordering service is non-existent.

		Based on what we’ve described above, the minimum allowed values for M and N are 2 and 3 respectively. This configuration allows for the creation of new channels to go forward, and for all channels to continue to be writeable.

	4. message.max.bytes and replica.fetch.max.bytes should be set to a value larger than A, the value you picked in Orderer.AbsoluteMaxBytes in Step 4 above. Add some buffer to account for headers — 1 MiB is more than enough. The following condition applies:

		Orderer.AbsoluteMaxBytes < replica.fetch.max.bytes <= message.max.bytes

		(For completeness, we note that message.max.bytes should be strictly smaller to socket.request.max.bytes which is set by default to 100 MiB. If you wish to have blocks larger than 100 MiB you will need to edit the hard-coded value in brokerConfig.Producer.MaxMessageBytes in fabric/orderer/kafka/config.go and rebuild the binary from source. This is not advisable.)

	5. log.retention.ms = -1. Until the ordering service adds support for pruning of the Kafka logs, you should disable time-based retention and prevent segments from expiring. (Size-based retention —see log.retention.bytes— is disabled by default in Kafka at the time of this writing, so there’s no need to set it explicitly.)

7. Orderers: Point each OSN to the genesis block. Edit General.GenesisFile in orderer.yaml so that it points to the genesis block created in Step 5 above. (While at it, ensure all other keys in that YAML file are set appropriately.)
8. Orderers: Adjust polling intervals and timeouts. (Optional step.)

	1. The Kafka.Retry section in the orderer.yaml file allows you to adjust the frequency of the metadata/producer/consumer requests, as well as the socket timeouts. (These are all settings you would expect to see in a Kafka producer or consumer.)
	2. Additionally, when a new channel is created, or when an existing channel is reloaded (in case of a just-restarted orderer), the orderer interacts with the Kafka cluster in the following ways:

		1. It creates a Kafka producer (writer) for the Kafka partition that corresponds to the channel.
		2. It uses that producer to post a no-op CONNECT message to that partition.
		3. It creates a Kafka consumer (reader) for that partition.
	
		If any of these steps fail, you can adjust the frequency with which they are repeated. Specifically they will be re-attempted every Kafka.Retry.ShortInterval for a total of Kafka.Retry.ShortTotal, and then every Kafka.Retry.LongInterval for a total of Kafka.Retry.LongTotal until they succeed. Note that the orderer will be unable to write to or read from a channel until all of the steps above have been completed successfully.
9. Set up the OSNs and Kafka cluster so that they communicate over SSL. (Optional step, but highly recommended.) Refer to the Confluent guide for the Kafka cluster side of the equation, and set the keys under Kafka.TLS in orderer.yaml on every OSN accordingly.
10. Bring up the nodes in the following order: ZooKeeper ensemble, Kafka cluster, ordering service nodes.

#####Additional considerations#####
1. Preferred message size. In Step 4 above (see Steps section) you can also set the preferred size of blocks by setting the Orderer.Batchsize.PreferredMaxBytes key. Kafka offers higher throughput when dealing with relatively small messages; aim for a value no bigger than 1 MiB.
2. Using environment variables to override settings. When using the sample Kafka and Zookeeper Docker images provided with Fabric (see images/kafka and images/zookeeper respectively), you can override a Kafka broker or a ZooKeeper server’s settings by using environment variables. Replace the dots of the configuration key with underscores — e.g. KAFKA_UNCLEAN_LEADER_ELECTION_ENABLE=false will allow you to override the default value of unclean.leader.election.enable. The same applies to the OSNs for their local configuration, i.e. what can be set in orderer.yaml. For example ORDERER_KAFKA_RETRY_SHORTINTERVAL=1s allows you to override the default value for Orderer.Kafka.Retry.ShortInterval.

#####Kafka Protocol Version Compatibility#####
Fabric uses the sarama client library and vendors a version of it that supports Kafka 0.10 to 1.0, yet is still known to work with older versions.

Using the Kafka.Version key in orderer.yaml, you can configure which version of the Kafka protocol is used to communicate with the Kafka cluster’s brokers. Kafka brokers are backward compatible with older protocol versions. Because of a Kafka broker’s backward compatibility with older protocol versions, upgrading your Kafka brokers to a new version does not require an update of the Kafka.Version key value, but the Kafka cluster might suffer a performance penalty while using an older protocol version.

#####Debugging#####
Set General.LogLevel to DEBUG and Kafka.Verbose in orderer.yaml to true.

#####Example#####
Sample Docker Compose configuration files inline with the recommended settings above can be found under the fabric/bddtests directory. Look for dc-orderer-kafka-base.yml and dc-orderer-kafka.yml.

###五、命令参考###
####peer command####
#####Description#####
The peer command has five different subcommands, each of which allows administrators to perform a specific set of tasks related to a peer. For example, you can use the peer channel subcommand to join a peer to a channel, or the peer chaincode command to deploy a smart contract chaincode to a peer.

#####Syntax#####
The peer command has five different subcommands within it:

	peer chaincode [option] [flags]
	peer channel   [option] [flags]
	peer logging   [option] [flags]
	peer node      [option] [flags]
	peer version   [option] [flags]

Each subcommand has different options available, and these are described in their own dedicated topic. For brevity, we often refer to a command (peer), a subcommand (channel), or subcommand option (fetch) simply as a command.

If a subcommand is specified without an option, then it will return some high level help text as described in the --help flag below.

#####Flags#####
Each peer subcommand has a specific set of flags associated with it, many of which are designated global because they can be used in all subcommand options. These flags are described with the relevant peer subcommand.

The top level peer command has the following flags:

+ --help

	Use --help to get brief help text for any peer command. The --help flag is very useful – it can be used to get command help, subcommand help, and even option help.

	For example

		peer --help
		peer channel --help
		peer channel list --help

	See individual peer subcommands for more detail.
+ --logging-level <string>

	This flag sets the logging level for a peer when it is started.

	There are six possible values for <string> : debug, info, notice, warning, error, and critical.

	If logging-level is not explicitly specified, then it is taken from the CORE_LOGGING_LEVEL environment variable if it is set. If CORE_LOGGING_LEVEL is not set then the file sampleconfig/core.yaml is used to determined the logging level for the peer.

	You can find the current logging level for a specific component on the peer by running peer logging getlevel <component-name>.

+ --version

	Use this flag to show detailed information about how the peer was built. This flag cannot be applied to peer subcommands or their options.

#####Usage#####
Here’s some examples using the different available flags on the peer command.

+ Using the --help flag on the peer channel join command.

		peer channel join --help
	
		Joins the peer to a channel.
		
		Usage:
		  peer channel join [flags]
		
		Flags:
		  -b, --blockpath string   Path to file containing genesis block
		
		Global Flags:
		      --cafile string                       Path to file containing PEM-encoded trusted certificate(s) for the ordering endpoint
		      --certfile string                     Path to file containing PEM-encoded X509 public key to use for mutual TLS communication with the orderer endpoint
		      --clientauth                          Use mutual TLS when communicating with the orderer endpoint
		      --keyfile string                      Path to file containing PEM-encoded private key to use for mutual TLS communication with the orderer endpoint
		      --logging-level string                Default logging level and overrides, see core.yaml for full syntax
		  -o, --orderer string                      Ordering service endpoint
		      --ordererTLSHostnameOverride string   The hostname override to use when validating the TLS connection to the orderer.
		      --tls                                 Use TLS when communicating with the orderer endpoint
		  -v, --version                             Display current version of fabric peer server
	
	This shows brief help syntax for the peer channel join command.
+ Using the --version flag on the peer command.

		peer --version

		peer:
		 Version: 1.1.0-alpha
		 Go version: go1.9.2
		 OS/Arch: linux/amd64
		 Experimental features: false
		 Chaincode:
		  Base Image Version: 0.4.5
		  Base Docker Namespace: hyperledger
		  Base Docker Label: org.hyperledger.fabric
		  Docker Namespace: hyperledger

	This shows that this peer was built using an alpha of Hyperledger Fabric version 1.1.0, compiled with GOLANG 1.9.2. It can be used on Linux operating systems with AMD64 compatible instruction sets.

####peer chaincode####
#####Description#####
The peer chaincode subcommand allows administrators to perform chaincode related operations on a peer, such as installing, instantiating, invoking, packaging, querying, and upgrading chaincode.

#####Syntax#####
The peer chaincode subcommand has the following syntax:

	peer chaincode install      [flags]
	peer chaincode instantiate  [flags]
	peer chaincode invoke       [flags]
	peer chaincode list         [flags]
	peer chaincode package      [flags]
	peer chaincode query        [flags]
	peer chaincode signpackage  [flags]
	peer chaincode upgrade      [flags]

The different subcommand options (install, instantiate...) relate to the different chaincode operations that are relevant to a peer. For example, use the peer chaincode install subcommand option to install a chaincode on a peer, or the peer chaincode query subcommand option to query a chaincode for the current value on a peer’s ledger.

Each peer chaincode subcommand is described together with its options in its own section in this topic.

#####Flags#####
Each peer chaincode subcommand has both a set of flags specific to an individual subcommand, as well as a set of global flags that relate to all peer chaincode subcommands. Not all subcommands would use these flags. For instance, the query subcommand does not need the --orderer flag.

The individual flags are described with the relevant subcommand. The global flags are

+ --cafile <string>

	Path to file containing PEM-encoded trusted certificate(s) for the ordering endpoint

+ --certfile <string>

	Path to file containing PEM-encoded X509 public key to use for mutual TLS communication with the orderer endpoint

+ --keyfile <string>

	Path to file containing PEM-encoded private key to use for mutual TLS communication with the orderer endpoint

+ -o or --orderer <string>

	Ordering service endpoint specifed as <hostname or IP address>:<port>

+ --ordererTLSHostnameOverride <string>

	The hostname override to use when validating the TLS connection to the orderer

+ --tls

	Use TLS when communicating with the orderer endpoint

+ --transient <string>

	Transient map of arguments in JSON encoding

+ --logging-level <string>

	Default logging level and overrides, see core.yaml for full syntax

#####peer chaincode install#####
######Install Description######
The peer chaincode install command allows administrators to install chaincode onto the filesystem of a peer.

######Install Syntas######
The peer chaincode install command has the following syntax:

	peer chaincode install [flags]

Note: An install can also be performed using a chaincode packaged via the peer chaincode package command (see the peer chaincode package section below for further details on packaging a chaincode for installation). The syntax using a chaincode package is as follows:

	peer chaincode install [chaincode-package-file]

where [chaincode-package-file] is the output file from the peer chaincode package command.

######Install Flags######
The peer chaincode install command has the following command-specific flags:

+ -c, --ctor <string>

	Constructor message for the chaincode in JSON format (default “{}”)

+ -l, --lang <string>

	Language the chaincode is written in (default “golang”)

+ -n, --name <string>

	Name of the chaincode that is being installed. It may consist of alphanumerics, dashes, and underscores

+ -p, --path <string>

	Path to the chaincode that is being installed. For Golang (-l golang) chaincodes, this is the path relative to the GOPATH. For Node.js (-l node) chaincodes, this is either the absolute path or the relative path from where the install command is being performed

+ -v, --version <string>

	Version of the chaincode that is being installed. It may consist of alphanumerics, dashes, underscores, periods, and plus signs

######Install Usage######
Here are some examples of the peer chaincode install command:

+ To install chaincode named mycc at version 1.0:

		peer chaincode install -n mycc -v 1.0 -p github.com/hyperledger/fabric/examples/chaincode/go/chaincode_example02
	
		.
		.
		.
		2018-02-22 16:33:52.998 UTC [chaincodeCmd] checkChaincodeCmdParams -> INFO 003 Using default escc
		2018-02-22 16:33:52.998 UTC [chaincodeCmd] checkChaincodeCmdParams -> INFO 004 Using default vscc
		.
		.
		.
		2018-02-22 16:33:53.194 UTC [chaincodeCmd] install -> DEBU 010 Installed remotely response:<status:200 payload:"OK" >
		2018-02-22 16:33:53.194 UTC [main] main -> INFO 011 Exiting.....

	Here you can see that the install completed successfully based on the log message:

		2018-02-22 16:33:53.194 UTC [chaincodeCmd] install -> DEBU 010 Installed remotely response:<status:200 payload:"OK" >
+ To install chaincode package ccpack.out generated with the package subcommand

		peer chaincode install ccpack.out
	
		.
		.
		.
		2018-02-22 18:18:05.584 UTC [chaincodeCmd] install -> DEBU 005 Installed remotely response:<status:200 payload:"OK" >
		2018-02-22 18:18:05.584 UTC [main] main -> INFO 006 Exiting.....
	
	Here you can see that the install completed successfully based on the log message:

		2018-02-22 18:18:05.584 UTC [chaincodeCmd] install -> DEBU 005 Installed remotely response:<status:200 payload:"OK" >

#####peer chaincode instantiate#####
######Instantiate Description######
The peer chaincode instantiate command allows administrators to instantiate chaincode on a channel of which the peer is a member.

######Instantiate Syntas######
The peer chaincode instantiate command has the following syntax:

	peer chaincode instantiate [flags]

######Instantiate Flags######
The peer chaincode instantiate command has the following command-specific flags:

+ -C, --channelID <string>

	Name of the channel where the chaincode should be instantiated

+ -c, --ctor <string>

	Constructor message for the chaincode in JSON format (default “{}”)

+ -E, --escc <string>

	Name of the endorsement system chaincode to be used for this chaincode (default “escc”)

+ -n, --name <string>

	Name of the chaincode that is being instantiated

+ -P, --policy <string>

	Endorsement policy associated to this chaincode. By default fabric will generate an endorsement policy equivalent to “any member from the organizations currently in the channel”

+ -v, --version <string>

	Version of the chaincode that is being instantiated

+ -V, --vscc <string>

	Name of the verification system chaincode to be used for this chaincode (default “vscc”)

The global peer command flags also apply:

+ --cafile <string>
+ --certfile <string>
+ --keyfile <string>
+ -o, --orderer <string>
+ --ordererTLSHostnameOverride <string>
+ --tls
+ --transient <string>

	If `--orderer` flag is not specified, the command will attempt to retrieve
	the orderer information for the channel from the peer before issuing the
	instantiate command.

######Instantiate Usage######
Here are some examples of the peer chaincode instantiate command, which instantiates the chaincode named mycc at version 1.0 on channel mychannel:

+ Using the --tls and --cafile global flags to instantiate the chaincode in a network with TLS enabled:

		export ORDERER_CA=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem
		peer chaincode instantiate -o orderer.example.com:7050 --tls --cafile $ORDERER_CA -C mychannel -n mycc -v 1.0 -c '{"Args":["init","a","100","b","200"]}' -P "OR ('Org1MSP.peer','Org2MSP.peer')"
		
		2018-02-22 16:33:53.324 UTC [chaincodeCmd] checkChaincodeCmdParams -> INFO 001 Using default escc
		2018-02-22 16:33:53.324 UTC [chaincodeCmd] checkChaincodeCmdParams -> INFO 002 Using default vscc
		2018-02-22 16:34:08.698 UTC [main] main -> INFO 003 Exiting.....
+ Using only the command-specific options to instantiate the chaincode in a network with TLS disabled:

		peer chaincode instantiate -o orderer.example.com:7050 -C mychannel -n mycc -v 1.0 -c '{"Args":["init","a","100","b","200"]}' -P "OR    ('Org1MSP.peer','Org2MSP.peer')"


		2018-02-22 16:34:09.324 UTC [chaincodeCmd] checkChaincodeCmdParams -> INFO 001 Using default escc
		2018-02-22 16:34:09.324 UTC [chaincodeCmd] checkChaincodeCmdParams -> INFO 002 Using default vscc
		2018-02-22 16:34:24.698 UTC [main] main -> INFO 003 Exiting.....

#####peer chaincode invoke#####
######Invoke Description######
The peer chaincode invoke command allows administrators to call chaincode functions on a peer using the supplied arguments. The CLI invokes chaincode by sending a transaction proposal to a peer. The peer will execute the chaincode and send the endorsed proposal response (or error) to the CLI. On receipt of a endorsed proposal response, the CLI will construct a transaction with it and send it to the orderer.

######Invoke Syntax######
The peer chaincode invoke command has the following syntax:

	peer chaincode invoke [flags]

######Invoke Flags######
The peer chaincode invoke command has the following command-specific flags:

+ -C, --channelID <string>

	Name of the chaincode that is being invoked

+ -c, --ctor <string>

	Constructor message for the chaincode in JSON format (default “{}”)

+ -n, --name <string>

	Name of the chaincode that is being invoked

The global peer command flags also apply:

+ --cafile <string>
+ --certfile <string>
+ --keyfile <string>
+ -o, --orderer <string>
+ --ordererTLSHostnameOverride <string>
+ --tls
+ --transient <string>

	If `--orderer` flag is not specified, the command will attempt to retrieve
	the orderer information for the channel from the peer before issuing the
	invoke command.

######Invoke Usage######
Here is an example of the peer chaincode invoke command, which invokes the chaincode named mycc at version 1.0 on channel mychannel, requesting to move 10 units from variable a to variable b:

		peer chaincode invoke -o orderer.example.com:7050 -C mychannel -n mycc -c '{"Args":["invoke","a","b","10"]}'
	
		2018-02-22 16:34:27.069 UTC [chaincodeCmd] checkChaincodeCmdParams -> INFO 001 Using default escc
		2018-02-22 16:34:27.069 UTC [chaincodeCmd] checkChaincodeCmdParams -> INFO 002 Using default vscc
		.
		.
		.
		2018-02-22 16:34:27.106 UTC [chaincodeCmd] chaincodeInvokeOrQuery -> DEBU 00a ESCC invoke result: version:1 response:<status:200 message:"OK" > payload:"\n \237mM\376? [\214\002 \332\204\035\275q\227\2132A\n\204&\2106\037W|\346#\3413\274\022Y\nE\022\024\n\004lscc\022\014\n\n\n\004mycc\022\002\010\003\022-\n\004mycc\022%\n\007\n\001a\022\002\010\003\n\007\n\001b\022\002\010\003\032\007\n\001a\032\00290\032\010\n\001b\032\003210\032\003\010\310\001\"\013\022\004mycc\032\0031.0" endorsement:<endorser:"\n\007Org1MSP\022\262\006-----BEGIN CERTIFICATE-----\nMIICLjCCAdWgAwIBAgIRAJYomxY2cqHA/fbRnH5a/bwwCgYIKoZIzj0EAwIwczEL\nMAkGA1UEBhMCVVMxEzARBgNVBAgTCkNhbGlmb3JuaWExFjAUBgNVBAcTDVNhbiBG\ncmFuY2lzY28xGTAXBgNVBAoTEG9yZzEuZXhhbXBsZS5jb20xHDAaBgNVBAMTE2Nh\nLm9yZzEuZXhhbXBsZS5jb20wHhcNMTgwMjIyMTYyODE0WhcNMjgwMjIwMTYyODE0\nWjBwMQswCQYDVQQGEwJVUzETMBEGA1UECBMKQ2FsaWZvcm5pYTEWMBQGA1UEBxMN\nU2FuIEZyYW5jaXNjbzETMBEGA1UECxMKRmFicmljUGVlcjEfMB0GA1UEAxMWcGVl\ncjAub3JnMS5leGFtcGxlLmNvbTBZMBMGByqGSM49AgEGCCqGSM49AwEHA0IABDEa\nWNNniN3qOCQL89BGWfY39f5V3o1pi//7JFDHATJXtLgJhkK5KosDdHuKLYbCqvge\n46u3AC16MZyJRvKBiw6jTTBLMA4GA1UdDwEB/wQEAwIHgDAMBgNVHRMBAf8EAjAA\nMCsGA1UdIwQkMCKAIN7dJR9dimkFtkus0R5pAOlRz5SA3FB5t8Eaxl9A7lkgMAoG\nCCqGSM49BAMCA0cAMEQCIC2DAsO9QZzQmKi8OOKwcCh9Gd01YmWIN3oVmaCRr8C7\nAiAlQffq2JFlbh6OWURGOko6RckizG8oVOldZG/Xj3C8lA==\n-----END CERTIFICATE-----\n" signature:"0D\002 \022_\342\350\344\231G&\237\n\244\375\302J\220l\302\345\210\335D\250y\253P\0214:\221e\332@\002 \000\254\361\224\247\210\214L\277\370\222\213\217\301\r\341v\227\265\277\336\256^\217\336\005y*\321\023\025\367" >
		2018-02-22 16:34:27.107 UTC [chaincodeCmd] chaincodeInvokeOrQuery -> INFO 00b Chaincode invoke successful. result: status:200
		2018-02-22 16:34:27.107 UTC [main] main -> INFO 00c Exiting.....
	
Here you can see that the invoke was submitted successfully based on the log message:

	2018-02-22 16:34:27.107 UTC [chaincodeCmd] chaincodeInvokeOrQuery -> INFO 00b Chaincode invoke successful. result: status:200
&nbsp;

	A successful response indicates that the transaction was submitted for ordering
	successfully. The transaction will then be added to a block and, finally, validated
	or invalidated by each peer on the channel.

#####peer chaincode list#####
######List Description######
The peer chaincode list command allows administrators to list the chaincodes installed on a peer or the chaincodes instantiated on a channel of which the peer is a member.

######List Syntax######
The peer chaincode list command has the following syntax:

	peer chaincode list [--installed|--instantiated -C <channel-name>]

######List Flags######
The peer chaincode instantiate command has the following command-specific flags:

+ -C, --channelID <string>

	Name of the channel to list instantiated chaincodes for

+ --installed

	Use this flag to list the installed chaincodes on a peer

+ --instantiated

	Use this flag to list the instantiated chaincodes on a channel that the peer is a member of

######List Usage######
Here are some examples of the peer chaincode list command:

+ Using the --installed flag to list the chaincodes installed on a peer.

		peer chaincode list --installed
	
		Get installed chaincodes on peer:
		Name: mycc, Version: 1.0, Path: github.com/hyperledger/fabric/examples/chaincode/go/chaincode_example02, Id: 8cc2730fdafd0b28ef734eac12b29df5fc98ad98bdb1b7e0ef96265c3d893d61
		2018-02-22 17:07:13.476 UTC [main] main -> INFO 001 Exiting.....

	You can see that the peer has installed a chaincode called mycc which is at version 1.0.

+ Using the --instantiated in combination with the -C (channel ID) flag to list the chaincodes instantiated on a channel.

		peer chaincode list --instantiated -C mychannel

		Get instantiated chaincodes on channel mychannel:
		Name: mycc, Version: 1.0, Path: github.com/hyperledger/fabric/examples/chaincode/go/chaincode_example02, Escc: escc, Vscc: vscc
		2018-02-22 17:07:42.969 UTC [main] main -> INFO 001 Exiting.....

	You can see that chaincode mycc at version 1.0 is instantiated on channel mychannel.

#####peer chaincode package#####
######Package Description######
The peer chaincode package command allows administrators to package the materials necessary to perform a chaincode install. This ensures the same chaincode package can be consistently installed on multiple peers.

######Package Syntax######
The peer chaincode package command has the following syntax:

	peer chaincode package [output-file] [flags]

######Package Flags######
The peer chaincode package command has the following command-specific flags:

+ -c, --ctor <string>

	Constructor message for the chaincode in JSON format (default “{}”)

+ -i, --instantiate-policy <string>

	Instantiation policy for the chaincode. Currently only policies that require utmost 1 signature (e.g., “OR (‘Org1MSP.peer’,’Org2MSP.peer’)”) are supported.

+ -l, --lang <string>

	Language the chaincode is written in (default “golang”)

+ -n, --name <string>

	Name of the chaincode that is being installed. It may consist of alphanumerics, dashes, and underscores

+ -p, --path <string>

	Path to the chaincode that is being packaged. For Golang (-l golang) chaincodes, this is the path relative to the GOPATH. For Node.js (-l node) chaincodes, this is either the absolute path or the relative path from where the package command is being performed

+ -s, --cc-package

	Create a package for storing chaincode ownership information in addition the raw chaincode deployment spec (however, see note below.)

+ -S, --sign

	Used with the -s flag, specify this flag to add owner endorsements to the package using the local MSP (however, see note below.)

+ -v, --version <string>

	Version of the chaincode that is being installed. It may consist of alphanumerics, dashes, underscores, periods, and plus signs

&nbsp;

	The metadata from `-s` and `-S` commands are not currently used. These commands
	are meant for future extensions and will likely undergo implementation changes.
	It is recommended that they are not used.

######Package Usage######
Here is an example of the peer chaincode package command, which packages the chaincode named mycc at version 1.1, creates the chaincode deployment spec, signs the package using the local MSP, and outputs it as ccpack.out:

	peer chaincode package ccpack.out -n mycc -p github.com/hyperledger/fabric/examples/chaincode/go/chaincode_example02 -v 1.1 -s -S

	.
	.
	.
	2018-02-22 17:27:01.404 UTC [chaincodeCmd] checkChaincodeCmdParams -> INFO 003 Using default escc
	2018-02-22 17:27:01.405 UTC [chaincodeCmd] checkChaincodeCmdParams -> INFO 004 Using default vscc
	.
	.
	.
	2018-02-22 17:27:01.879 UTC [chaincodeCmd] chaincodePackage -> DEBU 011 Packaged chaincode into deployment spec of size <3426>, with args = [ccpack.out]
	2018-02-22 17:27:01.879 UTC [main] main -> INFO 012 Exiting.....

#####peer chaincode query#####
######Query Description######
The peer chaincode query command allows the chaincode to be queried by calling the Invoke method on the chaincode. The difference between the query and the invoke subcommands is that, on successful response, invoke proceeds to submit a transaction to the orderer whereas query just outputs the response, successful or otherwise, to stdout.

######Query Syntax######
The peer chaincode query command has the following syntax:

	peer chaincode query [flags]

######Query Flags######
The peer chaincode query command has the following command-specific flags:

+ -C, --channelID <string>

	Name of the channel where the chaincode should be queried

+ -c, --ctor <string>

	Constructor message for the chaincode in JSON format (default “{}”)

+ -n, --name <string>

	Name of the chaincode that is being queried

+ -r --raw

	Output the query value as raw bytes (default)

+ -x --hex

	Output the query value byte array in hexadecimal. Incompatible with –raw

The global peer command flag also applies:

+ --transient <string>

######Query Usage######
Here is an example of the peer chaincode query command, which queries the peer ledger for the chaincode named mycc at version 1.0 for the value of variable a:

	peer chaincode query -C mychannel -n mycc -c '{"Args":["query","a"]}'

	2018-02-22 16:34:30.816 UTC [chaincodeCmd] checkChaincodeCmdParams -> INFO 001 Using default escc
	2018-02-22 16:34:30.816 UTC [chaincodeCmd] checkChaincodeCmdParams -> INFO 002 Using default vscc
	Query Result: 90

You can see from the output that variable a had a value of 90 at the time of the query.

#####peer chaincode signpackage#####
######signpackage Description######
The peer chaincode signpackage command is used to add a signature to a given chaincode package created with the peer chaincode package command using -s and -S options.

######signpackage Syntax######
The peer chaincode signpackage command has the following syntax:

	peer chaincode signpackage <inputpackage> <outputpackage>

######signpackage Usage######
Here is an example of the peer chaincode signpackage command, which accepts an existing signed package and creates a new one with signature of the local MSP appended to it.

	peer chaincode signpackage ccwith1sig.pak ccwith2sig.pak
	Wrote signed package to ccwith2sig.pak successfully
	2018-02-24 19:32:47.189 EST [main] main -> INFO 002 Exiting.....

#####peer chaincode upgrade#####
######Upgrade Description######
The peer chaincode upgrade command allows administrators to upgrade the chaincode instantiated on a channel to a newer version.

######Upgrade Syntax######
The peer chaincode upgrade command has the following syntax:

	peer chaincode upgrade [flags]

######Upgrade Flags######
The peer chaincode upgrade command has the following command-specific flags:

+ -C, --channelID <string>

	Name of the channel where the chaincode should be upgraded

+ -c, --ctor <string>

	Constructor message for the chaincode in JSON format (default “{}”)

+ -E, --escc <string>

	Name of the endorsement system chaincode to be used for this chaincode (default “escc”)

+ -n, --name <string>

	Name of the chaincode that is being upgraded

+ -P, --policy <string>

	Endorsement policy associated to this chaincode. By default fabric will generate an endorsement policy equivalent to “any member from the organizations currently in the channel”

+ -v, --version <string>

	Version of the upgraded chaincode

+ -V, --vscc <string>

	Name of the verification system chaincode to be used for this chaincode (default “vscc”)

The global peer command flags also apply:

+ --cafile <string>
+ -o, --orderer <string>
+ --tls

	If `--orderer` flag is not specified, the command will attempt to retrieve
	the orderer information for the channel from the peer before issuing the
	upgrade command.

######Upgrade Usage######
Here is an example of the peer chaincode upgrade command, which upgrades the chaincode named mycc at version 1.0 on channel mychannel to version 1.1, which contains a new variable c:

+ Using the --tls and --cafile global flags to upgrade the chaincode in a network with TLS enabled:

		export ORDERER_CA=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem
		peer chaincode upgrade -o orderer.example.com:7050 --tls --cafile $ORDERER_CA -C mychannel -n mycc -v 1.2 -c '{"Args":["init","a","100","b","200","c","300"]}' -P "OR   ('Org1MSP.peer','Org2MSP.peer')"
		
		.
		.
		.
		2018-02-22 18:26:31.433 UTC [chaincodeCmd] checkChaincodeCmdParams -> INFO 003 Using default escc
		2018-02-22 18:26:31.434 UTC [chaincodeCmd] checkChaincodeCmdParams -> INFO 004 Using default vscc
		2018-02-22 18:26:31.435 UTC [chaincodeCmd] getChaincodeSpec -> DEBU 005 java chaincode enabled
		2018-02-22 18:26:31.435 UTC [chaincodeCmd] upgrade -> DEBU 006 Get upgrade proposal for chaincode <name:"mycc" version:"1.1" >
		.
		.
		.
		2018-02-22 18:26:46.687 UTC [chaincodeCmd] upgrade -> DEBU 009 endorse upgrade proposal, get response <status:200 message:"OK" payload:"\n\004mycc\022\0031.1\032\004escc\"\004vscc*,\022\014\022\n\010\001\022\002\010\000\022\002\010\001\032\r\022\013\n\007Org1MSP\020\003\032\r\022\013\n\007Org2MSP\020\0032f\n \261g(^v\021\220\240\332\251\014\204V\210P\310o\231\271\036\301\022\032\205fC[|=\215\372\223\022 \311b\025?\323N\343\325\032\005\365\236\001XKj\004E\351\007\247\265fu\305j\367\331\275\253\307R\032 \014H#\014\272!#\345\306s\323\371\350\364\006.\000\356\230\353\270\263\215\217\303\256\220i^\277\305\214: \375\200zY\275\203}\375\244\205\035\340\226]l!uE\334\273\214\214\020\303\3474\360\014\234-\006\315B\031\022\010\022\006\010\001\022\002\010\000\032\r\022\013\n\007Org1MSP\020\001" >
		.
		.
		.
		2018-02-22 18:26:46.693 UTC [chaincodeCmd] upgrade -> DEBU 00c Get Signed envelope
		2018-02-22 18:26:46.693 UTC [chaincodeCmd] chaincodeUpgrade -> DEBU 00d Send signed envelope to orderer
		2018-02-22 18:26:46.908 UTC [main] main -> INFO 00e Exiting.....
+ Using only the command-specific options to upgrade the chaincode in a network with TLS disabled:

				
		.
		.
		.
		2018-02-22 18:28:31.433 UTC [chaincodeCmd] checkChaincodeCmdParams -> INFO 003 Using default escc
		2018-02-22 18:28:31.434 UTC [chaincodeCmd] checkChaincodeCmdParams -> INFO 004 Using default vscc
		2018-02-22 18:28:31.435 UTC [chaincodeCmd] getChaincodeSpec -> DEBU 005 java chaincode enabled
		2018-02-22 18:28:31.435 UTC [chaincodeCmd] upgrade -> DEBU 006 Get upgrade proposal for chaincode <name:"mycc" version:"1.1" >
		.
		.
		.
		2018-02-22 18:28:46.687 UTC [chaincodeCmd] upgrade -> DEBU 009 endorse upgrade proposal, get response <status:200 message:"OK" payload:"\n\004mycc\022\0031.1\032\004escc\"\004vscc*,\022\014\022\n\010\001\022\002\010\000\022\002\010\001\032\r\022\013\n\007Org1MSP\020\003\032\r\022\013\n\007Org2MSP\020\0032f\n \261g(^v\021\220\240\332\251\014\204V\210P\310o\231\271\036\301\022\032\205fC[|=\215\372\223\022 \311b\025?\323N\343\325\032\005\365\236\001XKj\004E\351\007\247\265fu\305j\367\331\275\253\307R\032 \014H#\014\272!#\345\306s\323\371\350\364\006.\000\356\230\353\270\263\215\217\303\256\220i^\277\305\214: \375\200zY\275\203}\375\244\205\035\340\226]l!uE\334\273\214\214\020\303\3474\360\014\234-\006\315B\031\022\010\022\006\010\001\022\002\010\000\032\r\022\013\n\007Org1MSP\020\001" >
		.
		.
		.
		2018-02-22 18:28:46.693 UTC [chaincodeCmd] upgrade -> DEBU 00c Get Signed envelope
		2018-02-22 18:28:46.693 UTC [chaincodeCmd] chaincodeUpgrade -> DEBU 00d Send signed envelope to orderer
		2018-02-22 18:28:46.908 UTC [main] main -> INFO 00e Exiting.....

####peer channel####
#####Description#####
The peer channel command allows administrators to perform channel related operations on a peer, such as joining a channel or listing the channels to which a peer is joined.

#####Syntax#####
The peer channel command has the following syntax:

	peer channel create       [flags]
	peer channel fetch        [flags]
	peer channel getinfo      [flags]
	peer channel join         [flags]
	peer channel list         [flags]
	peer channel signconfigtx [flags]
	peer channel update       [flags]

For brevity, we often refer to a command (peer), a subcommand (channel), or subcommand option (fetch) simply as a command.

The different command options (create, fetch...) relate to the different channel operations that are relevant to a peer. For example, use the peer channel join command to join a peer to a channel, or the peer channel list command to show the channels to which a peer is joined.

Each peer channel subcommand is described together with its options in its own section in this topic.

#####Flags#####
Each peer channel command option has a set of flags specific to it, and these are described with the relevant subcommand option.

All peer channel command options also have a set of global flags that can be applied to peer channel command options.

The global flags are as follows:

+ --cafile <string>

	where <string> is a fully qualified path to a file containing a PEM-encoded certificate chain of the Certificate Authority of the orderer with whom the peer is communicating. Use in conjunction with the --tls flag.

+ --certfile <string>

	where <string> is a fully qualified path to a file containing a PEM-encoded X.509 certificate used for mutual authentication with the orderer. Use in conjunction with the --clientauth flag.

+ --clientauth

	Use this flag to enable mutual TLS communication with the orderer. Use in conjunction with the --certfile and --keyfile flags.

+ --keyfile <string>

	where <string> is a fully qualified path to a file containing a PEM-encoded X.509 private key used for mutual authentication with the orderer. Use in conjunction with the --clientauth flag.

+ -o, --orderer <string>

	where <string> is the fully qualified address and port of the orderer with whom the peer is communicating. If the port is not specified, it will default to port 7050.

+ --ordererTLSHostnameOverride <string>

	where <string> is the hostname override to use when using TLS to communicate with the orderer specified by the --orderer flag. It is necessary to use this flag when the TLS handshake phase of communications between the peer and the orderer uses a different hostname than the subsequent message exchange phase. Use in conjunction with the --tls flag.

+ --tls

	Use this flag to enable TLS communications with an orderer. The certificates identified by --cafile will be used by TLS to authenticate the orderer.

#####Usage#####
Here’s an example that uses the --orderer global flag on the peer channel create command.

Create a sample channel mychannel defined by the configuration transaction contained in file ./createchannel.txn. Use the orderer at orderer.example.com:7050.

	peer channel create -c mychannel -f ./createchannel.txn --orderer orderer.example.com:7050

	2018-02-25 08:23:57.548 UTC [channelCmd] InitCmdFactory -> INFO 003 Endorser and orderer connections initialized
	2018-02-25 08:23:57.626 UTC [channelCmd] InitCmdFactory -> INFO 019 Endorser and orderer connections initialized
	2018-02-25 08:23:57.834 UTC [channelCmd] readBlock -> DEBU 020 Received block: 0
	2018-02-25 08:23:57.835 UTC [main] main -> INFO 021 Exiting.....

Block 0 is returned indicating that the channel has been successfully created.

#####peer channel create#####
######Create Description######
The peer channel create command allows administrators to create a new channel. This command connects to an orderer to perform this function – it is not performed on the peer, even though the peer command is used.

To create a channel, the administrator uses the command to submit a configuration update transaction to the orderer. This transaction describes the configuration changes required to create a new channel. Moreover, this transaction must be signed by the required organizations as defined by the current orderer configuration. Configuration transactions can be generated by the configtxgen command and signed by the peer channel signconfigtx command.

######Create Syntax######
The peer channel create command has the following syntax:

	peer channel create [flags]

######Create Flags######
The peer channel create command has the following command specific flags:

+ -c, --channelID <string>

	required, where <string> is the name of the channel which is to be created.

+ -f, --file <string>

	required, where <string> identifies a file which contains the configuration transaction required to create this channel. It can be generated by configtxgen command.

+ -t, --timeout <integer>

	optional, where <integer> specifies channel creation timeout in seconds. If not specified, the default is 5 seconds. Note that if the command times out, then the channel may or may not have been created.

The global peer command flags also apply as follows:

+ -o, --orderer required
+ --cafile optional
+ --certfile optional
+ --clientuth optional
+ --keyfile optional
+ --ordererTLSHostnameOverride optional
+ --tls optional

######Create Usage######
Here’s an example of the peer channel create command option.

Create a new channel mychannel for the network, using the orderer at ip address orderer.example.com:7050. The configuration update transaction required to create this channel is defined the file ./createchannel.txn. Wait 30 seconds for the channel to be created.

	peer channel create -c mychannel --orderer orderer.example.com:7050 -f ./createchannel.txn -t 30

	2018-02-23 06:31:58.568 UTC [channelCmd] InitCmdFactory -> INFO 003 Endorser and orderer connections initialized
	2018-02-23 06:31:58.669 UTC [channelCmd] InitCmdFactory -> INFO 019 Endorser and orderer connections initialized
	2018-02-23 06:31:58.877 UTC [channelCmd] readBlock -> DEBU 020 Received block: 0
	2018-02-23 06:31:58.878 UTC [main] main -> INFO 021 Exiting.....
	
	ls -l
	
	-rw-r--r-- 1 root root 11982 Feb 25 12:24 mychannel.block

You can see that channel mychannel has been successfully created, as indicated in the output where block 0 (zero) is added to the blockchain for this channel and returned to the peer, where it is stored in the local directory as mychannel.block.

Block zero is often called the genesis block as it provides the starting configuration for the channel. All subsequent updates to the channel will be captured as configuration blocks on the channel’s blockchain, each of which supersedes the previous configuration.

#####peer channel fetch#####
######Fetch Description######
The peer channel fetch command allows a client to fetch a block from the orderer. The block may contain a configuration transaction or user transactions.

The client must have read access to the channel. This command connects to an orderer to perform this function – it is not performed on the peer, even though the peer client command is used.

######Fetch Syntax######
The peer channel fetch command has the following syntax:

	peer channel fetch [newest|oldest|config|(block number)] [<outputFile>] [flags]

where

+ newest

	returns the most recent block available at the orderer for the channel. This may be a user transaction block or a configuration block.

	This option will also return the block number of the most recent block.

+ oldest
	
	returns the oldest block available at the orderer for the channel. This may be a user transaction block or a configuration block.

	This option will also return the block number of the oldest available block.

+ config

	returns the most recent configuration block available at the orderer for the channel.

	This option will also return the block number of the most recent configuration block.

+ (block number)

	returns the requested block for the channel. This may be a user transaction block or a configuration block.

	Specifying 0 will result in the genesis block for this channel being returned (if it is still available to the network orderer).

+ <outputFile>

	specifies the name of the file where the fetched block is written. If <outputFile> is not specified, then the block is written to the local directory in a file named as follows:

		+ <channelID>_newest.block
		+ <channelID>_oldest.block
		+ <channelID>_config.block
		+ <channelID>_(block number).block
		
######Fetch Flags######
The peer channel fetch command has the following command specific flags:

+ -c, --channelID <string>

	required, where <string> is the name of the channel for which the blocks are to be fetched from the orderer.

The global peer command flags also apply:

+ -o, --orderer required
+ --cafile optional
+ --certfile optional
+ --clientuth optional
+ --keyfile optional
+ --ordererTLSHostnameOverride optional
+ --tls optional

######Fetch Usage######
Here’s some examples of the peer channel fetch command.

+ Using the newest option to retrieve the most recent channel block, and store it in the file mychannel.block.

		peer channel fetch newest mychannel.block -c mychannel --orderer orderer.example.com:7050

		2018-02-25 13:10:16.137 UTC [channelCmd] InitCmdFactory -> INFO 003 Endorser and orderer connections initialized
		2018-02-25 13:10:16.144 UTC [channelCmd] readBlock -> DEBU 00a Received block: 32
		2018-02-25 13:10:16.145 UTC [main] main -> INFO 00b Exiting.....
		
		ls -l
		
		-rw-r--r-- 1 root root 11982 Feb 25 13:10 mychannel.block

	You can see that the retrieved block is number 32, and that the information has been written to the file mychannel.block.

+ Using the (block number) option to retrieve a specific block – in this case, block number 16 – and store it in the default block file.

		peer channel fetch 16  -c mychannel --orderer orderer.example.com:7050
		
		2018-02-25 13:46:50.296 UTC [channelCmd] InitCmdFactory -> INFO 003 Endorser and orderer connections initialized
		2018-02-25 13:46:50.302 UTC [channelCmd] readBlock -> DEBU 00a Received block: 16
		2018-02-25 13:46:50.302 UTC [main] main -> INFO 00b Exiting.....
		
		ls -l
		
		-rw-r--r-- 1 root root 11982 Feb 25 13:10 mychannel.block
		-rw-r--r-- 1 root root  4783 Feb 25 13:46 mychannel_16.block

	You can see that the retrieved block is number 16, and that the information has been written to the default file mychannel_16.block.

For configuration blocks, the block file can be decoded using the configtxlator command. See this command for an example of decoded output. User transaction blocks can also be decoded, but a user program must be written to do this.

#####peer channel getinfo#####
######GetInfo Description######
The peer channel getinfo command allows administrators to retrieve information about the peer’s local blockchain for a particular channel. This includes the current blockchain height, and the hashes of the current block and previous block. Remember that a peer can be joined to more than one channel.

This information can be useful when administrators need to understand the current state of a peer’s blockchain, especially in comparison to other peers in the same channel.

######GetInfo Syntax######
The peer channel getinfo command has the following syntax:

	peer channel getinfo [flags]

######GetInfo Flags######
The peer channel getinfo command has no specific flags.

None of the global peer command flags apply, since this command does not interact with an orderer.

######GetInfo Usage######
Here’s an example of the peer channel getinfo command.

+ Get information about the local peer for channel mychannel.

		peer channel getinfo -c mychannel
	
		2018-02-25 15:15:44.135 UTC [channelCmd] InitCmdFactory -> INFO 003 Endorser and orderer connections initialized
		Blockchain info: {"height":5,"currentBlockHash":"JgK9lcaPUNmFb5Mp1qe1SVMsx3o/22Ct4+n5tejcXCw=","previousBlockHash":"f8lZXoAn3gF86zrFq7L1DzW2aKuabH9Ow6SIE5Y04a4="}
		2018-02-25 15:15:44.139 UTC [main] main -> INFO 006 Exiting.....

	You can see that the latest block for channel mychannel is block 5. You can also see the crytographic hashes for the most recent blocks in the channel’s blockchain.

#####peer channel join#####
######Join Description######
The peer channel join command allows administrators to join a peer to an existing channel. The administrator achieves this by using the command to provide a channel genesis block to the peer. The peer will then automatically retrieve the channel’s blocks from other peers in the network, or the orderer, depending on the configuration, and the availability of other peers.

The administrator can create a local genesis block for use by this command by retrieving block 0 from an existing channel using the peer channel fetch command option. The peer channel create command will also return a local genesis block when a new channel is created.

######Join Syntax######
The peer channel join command has the following syntax:

	peer channel join [flags]

######Join Flags######
The peer channel join command has the following command specific flags:

+ -b, --blockpath <string>

required, where <string> identifies a file containing the channel genesis block. This block can be retrieved using the peer channel fetch command, requesting block 0 from the channel, or using the peer channel create command.

None of the global peer command flags apply, since this command does not interact with an orderer.

######Join Usage######
Here’s an example of the peer channel join command.

+ Join a peer to the channel defined in the genesis block identified by the file ./mychannel.genesis.block. In this example, the channel block was previously retrieved by the peer channel fetch command.

		peer channel join -b ./mychannel.genesis.block
	
		2018-02-25 12:25:26.511 UTC [channelCmd] InitCmdFactory -> INFO 003 Endorser and orderer connections initialized
		2018-02-25 12:25:26.571 UTC [channelCmd] executeJoin -> INFO 006 Successfully submitted proposal to join channel
		2018-02-25 12:25:26.571 UTC [main] main -> INFO 007 Exiting.....

	You can see that the peer has successfully made a request to join the channel.

#####peer channel list#####
######List Description######
The peer channel list command allows administrators list the channels to which a peer is joined.

######List Syntax######
The peer channel list command has the following syntax:

	peer channel list [flags]

######List Flags######
The peer channel list command has no specific flags.

None of the global peer command flags apply, since this command does not interact with an orderer.

######List Usage######
Here’s an example of the peer channel list command.

+ List the channels to which a peer is joined.

		peer channel list

		2018-02-25 14:21:20.361 UTC [channelCmd] InitCmdFactory -> INFO 003 Endorser and orderer connections initialized
		Channels peers has joined:
		mychannel
		2018-02-25 14:21:20.372 UTC [main] main -> INFO 006 Exiting.....

	You can see that the peer is joined to channel mychannel.

#####peer channel signconfigtx#####
######SignConfigTx Description######
The peer channel signconfigtx command helps administrators sign a configuration transaction with the peer’s identity credentials prior to submission to an orderer. Typical configuration transactions include creating a channel or updating a channel configuration.

The administrator supplies an input file to the signconfigtx command which describes the configuration transaction. The command then adds the peer’s public identity to the file, and signs the entire payload with the peer’s private key. The command uses the peer’s public and private credentials stored in its local MSP. A new file is not generated; the input file is updated in place.

signconfigtx only signs the configuration transaction; it does not create it, nor submit it to the orderer. Typically, the configuration transaction has been already created using the configtxgen command, and is subsequently submitted to the orderer by an appropriate command such as peer channel update.

######SignConfigTx Syntax######
The peer channel signconfigtx command has the following syntax:

	peer channel signconfigtx [flags]

######SignConfigTx Flags######
The peer channel signconfigtx command has the following command specific flags:

+ -f, --file <string>

required, where <string> identifies a file containing the channel configuration transaction to be signed on behalf of the peer.

None of the global peer command flags apply, since this command does not interact with an orderer.

######SignConfigTx Usage######
Here’s an example of the peer channel signconfigtx command.

+ Sign the channel update transaction defined in the file ./updatechannel.txn. The example lists the configuration transaction file before and after the command.

		ls -l

		-rw-r--r--  1 anthonyodowd  staff   284 25 Feb 18:16 updatechannel.tx
		
		peer channel signconfigtx -f updatechannel.tx
		
		2018-02-25 18:16:44.456 GMT [channelCmd] InitCmdFactory -> INFO 001 Endorser and orderer connections initialized
		2018-02-25 18:16:44.459 GMT [main] main -> INFO 002 Exiting.....
		
		ls -l
		
		-rw-r--r--  1 anthonyodowd  staff  2180 25 Feb 18:16 updatechannel.tx

	You can see that the peer has successfully signed the configuration transaction by the increase in the size of the file updatechannel.tx from 284 bytes to 2180 bytes.

#####peer channel update#####
######Update Description######
The peer channel update command allows administrators to update an existing channel.

To update a channel, the administrator uses the command to submit a configuration transaction to the orderer which describes the required channel configuration changes. This transaction must be signed by the required organizations as defined in the current channel configuration. Configuration transactions can be generated by the configtxgen command and signed by the peer channel signconfigtx command.

The update transaction is sent by the command to the orderer, which validates the change is authorized, and then distributes a configuration block to every peer on the channel. In this way, every peer on the channel maintains a consistent copy of the channel configuration.

######Update Syntax######
The peer channel update command has the following syntax:

	peer channel update [flags]

######Update Flags######
The peer channel update command has the following command specific flags:

+ -c, --channelID <string>

	required, where <string> is the name of the channel which is to be updated.

+ -f, --file <string>

	required, where <string> identifies a transaction configuration file. This file contains the configuration change required to this channel, and it can be generated by configtxgen command.

The global peer command flags also apply as follows:

+ -o, --orderer required
+ --cafile optional
+ --certfile optional
+ --clientuth optional
+ --keyfile optional
+ --ordererTLSHostnameOverride optional
+ --tls optional

######Update Usage######
Here’s an example of the peer channel update command.

+ Update the channel mychannel using the configuration transaction defined in the file ./updatechannel.txn. Use the orderer at ip address orderer.example.com:7050 to send the configuration transaction to all peers in the channel to update their copy of the channel configuration.

		peer channel update -c mychannel -f ./updatechannel.txn -o orderer.example.com:7050

		2018-02-23 06:32:11.569 UTC [channelCmd] InitCmdFactory -> INFO 003 Endorser and orderer connections initialized
		2018-02-23 06:32:11.626 UTC [main] main -> INFO 010 Exiting.....

	At this point, the channel mychannel has been successfully updated.

####peer version####
#####Description#####
The peer version command displays the version information of the peer. It displays version, Go version, OS/architecture, if experimental features are turned on, and chaincode information. For example:

	peer:
	   Version: 1.1.0-beta-snapshot-a6c3447e
	   Go version: go1.9.2
	   OS/Arch: linux/amd64
	   Experimental features: true
	   Chaincode:
	    Base Image Version: 0.4.5
	    Base Docker Namespace: hyperledger
	    Base Docker Label: org.hyperledger.fabric
	    Docker Namespace: hyperledger

#####Syntax#####
The peer version command has the following syntax:

	peer version

####peer logging####
#####Description#####
The peer logging subcommand allows administrators to dynamically view and configure the log levels of a peer.

#####Syntax#####
The peer logging subcommand has the following syntax:

	peer logging getlevel
	peer logging setlevel
	peer logging revertlevels

The different subcommand options (getlevel, setlevel, and revertlevels) relate to the different logging operations that are relevant to a peer.

Each peer logging subcommand is described together with its options in its own section in this topic.

#####peer logging getlevel#####
######Get Level Description######
The peer logging getlevel command allows administrators to get the current level for a logging module.

######Get Level Syntax######
The peer logging getlevel command has the following syntax:

	peer logging getlevel <module-name>

######Get Level Flags######
The peer logging getlevel command does not have any command-specific flags.

######Get Level Usage######
Here is an example of the peer logging getlevel command:

+ To get the log level for module peer:

		peer logging getlevel peer
		
		2018-02-22 19:10:08.633 UTC [cli/logging] getLevel -> INFO 001 Current log level for peer module 'peer': DEBUG
		2018-02-22 19:10:08.633 UTC [main] main -> INFO 002 Exiting.....

#####peer logging setlevel#####
######Set Level Description######
The peer logging setlevel command allows administrators to set the current level for all logging modules that match the module name regular expression provided.

######Set Level Syntax######
The peer logging setlevel command has the following syntax:

	peer logging setlevel <module-name-regular-expression> <log-level>

######Set Level Flags######
The peer logging setlevel command does not have any command-specific flags.

######Set Level Usage######
Here are some examples of the peer logging setlevel command:

+ To set the log level for modules matching the regular expression peer to log level WARNING:

		peer logging setlevel peer warning
		2018-02-22 19:14:51.217 UTC [cli/logging] setLevel -> INFO 001 Log level set for peer modules matching regular expression 'peer': WARNING
		2018-02-22 19:14:51.217 UTC [main] main -> INFO 002 Exiting.....
+ To set the log level for modules that match the regular expression ^gossip (i.e. all of the gossip logging submodules of the form gossip/<submodule>) to log level ERROR:

		peer logging setlevel ^gossip error

		2018-02-22 19:16:46.272 UTC [cli/logging] setLevel -> INFO 001 Log level set for peer modules matching regular expression '^gossip': ERROR
		2018-02-22 19:16:46.272 UTC [main] main -> INFO 002 Exiting.....

#####peer logging revertlevels#####
######Revert Levels Description######
The peer logging revertlevels command allows administrators to revert the log levels of all modules to their level at the time the peer completed its startup process.

######Revert Levels Syntax######
The peer logging revertlevels command has the following syntax:

	peer logging revertlevels

######Revert Levels Flags######
The peer logging revertlevels command does not have any command-specific flags.

######Revert Levels Usage######
Here is an example of the peer logging revertlevels command:

		peer logging revertlevels
		
		2018-02-22 19:18:38.428 UTC [cli/logging] revertLevels -> INFO 001 Log levels reverted to the levels at the end of peer startup.
		2018-02-22 19:18:38.428 UTC [main] main -> INFO 002 Exiting.....

####peer node####
#####Description#####
The peer node subcommand allows an administrator to start a peer node or check the status of a peer node.

#####Syntax#####
The peer node subcommand has the following syntax:

	peer node start [flags]
	peer node status

#####pert node start#####
######Start Description######
The peer node start command allows administrators to start the peer node process.

The peer node process can be configured using configuration file core.yaml, which must be located in the directory specified by the environment variable FABRIC_CFG_PATH. For docker deployments, core.yaml is pre-configured in the peer container FABRIC_CFG_PATH directory. For native binary deployments, core.yaml is included with the release artifact distribution. The configuration properties located in core.yaml can be overridden using environment variables. For example, peer.mspConfigPath configuration property can be specified by defining CORE_PEER_MSPCONFIGPATH environment variable, where **CORE_** is the prefix for the environment variables.

######Start Syntax######
The peer node start command has the following syntax:

	peer node start [flags]

######Start Flags######
The peer node start command has the following command specific flag:

+ --peer-chaincodedev

		starts peer node in chaincode development mode. Normally chaincode containers are started and maintained by peer. However in devlopment mode, chaincode is built and started by the user. This mode is useful during chaincode development phase for iterative development. See more information on development mode in the chaincode tutorial.

The global peer command flags also apply as described in the peer command topic:

+ –logging-level

#####pert node status#####
######Status Description######
The peer node status command allows administrators to see the status of the peer node process. It will show the status of the peer node process running at the peer.address specified in the peer configuration, or overridden by CORE_PEER_ADDRESS environment variable.

######Status Syntax######
The peer node status command has the following syntax:

	peer node status

######Status Flags######
The peer node status command has no command specific flags.

####configtxgen####
#####Description#####
The configtxgen command allows users to create and inspect channel config related artifacts. The content of the generated artifacts is dictated by the contents of configtx.yaml.

#####Syntax#####
The configtxgen tool has no sub-commands, but supports flags which can be set to accomplish a number of tasks.

	Usage of configtxgen:
	  -asOrg string
	        Performs the config generation as a particular organization (by name), only including values in the write set that org (likely) has privilege to set
	  -channelID string
	        The channel ID to use in the configtx (default "testchainid")
	  -inspectBlock string
	        Prints the configuration contained in the block at the specified path
	  -inspectChannelCreateTx string
	        Prints the configuration contained in the transaction at the specified path
	  -outputAnchorPeersUpdate string
	        Creates an config update to update an anchor peer (works only with the default channel creation, and only for the first update)
	  -outputBlock string
	        The path to write the genesis block to (if set)
	  -outputCreateChannelTx string
	        The path to write a channel creation configtx to (if set)
	  -printOrg string
	        Prints the definition of an organization as JSON. (useful for adding an org to a channel manually)
	  -profile string
	        The profile from configtx.yaml to use for generation. (default "SampleInsecureSolo")
	  -version
	        Show version information

#####Usage#####
######Output a genesis block######
Write a genesis block to genesis_block.pb for channel orderer-system-channel for profile SampleSingleMSPSoloV1_1.

	configtxgen -outputBlock genesis_block.pb -profile SampleSingleMSPSoloV1_1 -channelID orderer-system-channel

######Output a channel creation tx######
Write a channel creation transaction to create_chan_tx.pb for profile SampleSingleMSPChannelV1_1.

	configtxgen -outputCreateChannelTx create_chan_tx.pb -profile SampleSingleMSPChannelV1_1 -channelID application-channel-1

######Inspect a genesis block######
Print the contents of a genesis block named genesis_block.pb to the screen as JSON.

	configtxgen -inspectBlock genesis_block.pb

######Inspect a channel creation tx######
Print the contents of a channel creation tx named create_chan_tx.pb to the screen as JSON.

	configtxgen -inspectChannelCreateTx create_chan_tx.pb

######Print an organization definition######
Construct an organization definition based on the parameters such as MSPDir from configtx.yaml and print it as JSON to the screen. (This output is useful for channel reconfiguration workflows, such as adding a member).

	configtxgen -printOrg Org1

######Output anchor peer tx######
Output a configuration update transaction to anchor_peer_tx.pb which sets the anchor peers for organization Org1 as defined in profile SampleSingleMSPChannelV1_1 based on configtx.yaml.

	configtxgen -outputAnchorPeersUpdate anchor_peer_tx.pb -profile SampleSingleMSPChannelV1_1 -asOrg Org1

#####Configuration#####
The configtxgen tool’s output is largely controlled by the content of configtx.yaml. This file is searched for at FABRIC_CFG_PATH and must be present for configtxgen to operate.

This configuration file may be edited, or, individual properties may be overridden by setting environment variables, such as CONFIGTX_ORDERER_ORDERERTYPE=kafka.

For many configtxgen operations, a profile name must be supplied. Profiles are a way to express multiple similar configurations in a single file. For instance, one profile might define a channel with 3 orgs, and another might define one with 4 orgs. To accomplish this without the length of the file becoming burdensome, configtx.yaml depends on the standard YAML feature of anchors and references. Base parts of the configuration are tagged with an anchor like &OrdererDefaults and then merged into a profile with a reference like <<: *OrdererDefaults. Note, when configtxgen is operating under a profile, environment variable overrides do not need to include the profile prefix and may be referenced relative to the root element of the profile. For instance, do not specify CONFIGTX_PROFILE_SAMPLEINSECURESOLO_ORDERER_ORDERERTYPE, instead simply omit the profile specifics and use the CONFIGTX prefix followed by the elements relative to the profile name such as CONFIGTX_ORDERER_ORDERERTYPE.

Refer to the sample configtx.yaml shipped with Fabric for all possible configuration options. You may find this file in the config directory of the release artifacts tar, or you may find it under the sampleconfig folder if you are building from source.

####configtxlator####
#####Description#####
The configtxlator command allows users to translate between protobuf and JSON versions of fabric data structures and create config updates. The command may either start a REST server to expose its functions over HTTP or may be utilized directly as a command line tool.

#####Syntax#####
The configtxlator tool has four sub-commands.
######configtxlator start######
Starts the REST server.

	usage: configtxlator start [<flags>]

	Start the configtxlator REST server
	
	Flags:
	  --help                Show context-sensitive help (also try --help-long and --help-man).
	  --hostname="0.0.0.0"  The hostname or IP on which the REST server will listen
	  --port=7059           The port on which the REST server will listen

######configtxlator proto_encode######
Converts JSON documents into protobuf messages.

	usage: configtxlator proto_encode --type=TYPE [<flags>]

	Converts a JSON document to protobuf.
	
	Flags:
	  --help                Show context-sensitive help (also try --help-long and --help-man).
	  --type=TYPE           The type of protobuf structure to encode to. For example, 'common.Config'.
	  --input=/dev/stdin    A file containing the JSON document.
	  --output=/dev/stdout  A file to write the output to.

######configtxlator proto_decode######
Converts protobuf messages into JSON documents.

	usage: configtxlator proto_decode --type=TYPE [<flags>]

	Converts a proto message to JSON.
	
	Flags:
	  --help                Show context-sensitive help (also try --help-long and --help-man).
	  --type=TYPE           The type of protobuf structure to decode from. For example, 'common.Config'.
	  --input=/dev/stdin    A file containing the proto message.
	  --output=/dev/stdout  A file to write the JSON document to.

######configtxlator compute_update######
Computes a config update based on an original, and modified config.

	usage: configtxlator compute_update --channel_id=CHANNEL_ID [<flags>]

	Takes two marshaled common.Config messages and computes the config update which transitions between the two.
	
	Flags:
	  --help                   Show context-sensitive help (also try --help-long and --help-man).
	  --original=ORIGINAL      The original config message.
	  --updated=UPDATED        The updated config message.
	  --channel_id=CHANNEL_ID  The name of the channel for this update.
	  --output=/dev/stdout     A file to write the JSON document to.

######configtxlator version######
Shows the version.

	usage: configtxlator version

	Show version information
	
	Flags:
	  --help  Show context-sensitive help (also try --help-long and --help-man).

#####Examples#####
######Decoding######
Decode a block named fabric_block.pb to JSON and print to stdout.

	configtxlator proto_decode --input fabric_block.pb --type common.Block

Alternatively, after starting the REST server, the following curl command performs the same operation through the REST API.

	curl -X POST --data-binary @fabric_block.pb "${CONFIGTXLATOR_URL}/protolator/decode/common.Block"

######Encoding######
Convert a JSON document for a policy from stdin to a file named policy.pb.

	configtxlator proto_encode --type common.Policy --output policy.pb

Alternatively, after starting the REST server, the following curl command performs the same operation through the REST API.

	curl -X POST --data-binary /dev/stdin "${CONFIGTXLATOR_URL}/protolator/encode/common.Policy" > policy.pb

######Pipelines######
Compute a config update from original_config.pb and modified_config.pb and decode it to JSON to stdout.

	configtxlator compute_update --channel_id testchan --original original_config.pb --updated modified_config.pb | configtxlator proto_decode --type common.ConfigUpdate

Alternatively, after starting the REST server, the following curl commands perform the same operations through the REST API.

	curl -X POST -F channel=testchan -F "original=@original_config.pb" -F "updated=@modified_config.pb" "${CONFIGTXLATOR_URL}/configtxlator/compute/update-from-configs" | curl -X POST --data-binary /dev/stdin "${CONFIGTXLATOR_URL}/protolator/encode/common.ConfigUpdate"

#####Additional Notes#####
The tool name is a portmanteau of configtx and translator and is intended to convey that the tool simply converts between different equivalent data representations. It does not generate configuration. It does not submit or retrieve configuration. It does not modify configuration itself, it simply provides some bijective operations between different views of the configtx format.

There is no configuration file configtxlator nor any authentication or authorization facilities included for the REST server. Because configtxlator does not have any access to data, key material, or other information which might be considered sensitive, there is no risk to the owner of the server in exposing it to other clients. However, because the data sent by a user to the REST server might be confidential, the user should either trust the administrator of the server, run a local instance, or operate via the CLI.

####Cryptogen Commands####
Cryptogen is an utility for generating Hyperledger Fabric key material. It is mainly meant to be used for testing environment.

#####Syntax#####
The cryptogen command has different subcommands within it:

	cryptogen [subcommand]

as follows
	
	cryptogen generate
	cryptogen showtemplate
	cryptogen version
	cryptogen extend
	cryptogen help
	cryptogen

These subcommands separate the different functions provided by they utility.

Within each subcommand there are many different options available and because of this, each is described in its own section in this topic.

If a command option is not specified then cryptogen will return some high level help text as described in in the --help flag below.

#####cryptogen flags#####
The cryptogen command also has a set of associated flags:

	cryptogen [flags]

as follows

	cryptogen --help
	cryptogen generate --help

These flags provide more information about cryptogen, and are designated global because they can be used at any command level. For example the --help flag can provide help on the cryptogen command, the cryptogen generate command, as well as their respective options.

#####Flag details#####
+ --help

	Use help to get brief help text for the cryptogen command. The help flag can often be used at different levels to get individual command help, or even a help on a command option. See individual commands for more detail.

#####Usage#####
Here’s some examples using the different available flags on the peer command.

+ --help flag

	cryptogen --help

	usage: cryptogen [<flags>] <command> [<args> ...]
	
	Utility for generating Hyperledger Fabric key material
	
	Flags:
	  --help  Show context-sensitive help (also try --help-long and --help-man).
	
	Commands:
	  help [<command>...]
	    Show help.
	
	  generate [<flags>]
	    Generate key material
	
	  showtemplate
	    Show the default configuration template
	
	  version
	    Show version information
	
	  extend [<flags>]
	    Extend existing network

######The cryptogen generate Command######
The cryptogen generate command allows the generation of the key material.

#####Syntax#####
The cryptogen generate command has the following syntax:

	cryptogen generate [<flags>]

######cryptogen generate flags######
The cryptogen generate command has different flags available to it, and because of this, each flag is described in the relevant command topic.

	cryptogen generate [flags]

as follows

	cryptogen generate --output="crypto-config"	
	cryptogen generate --config=CONFIG

The global cryptogen command flags also apply as described in the cryptogen command flags:

+ --help

#####Flag details#####
+ --output="crypto-config"

	the output directory in which to place artifacts.

+ --config=CONFIG

	the configuration template to use.

#####Usage#####
Here’s some examples using the different available flags on the cryptogen generate command.

	./cryptogen generate --output="crypto-config"

	org1.example.com
	org2.example.com

######The cryptogen showtemplate command######
The cryptogen showtemplate command shows the default configuration template.

#####Syntax#####
The cryptogen showtemplate command has the following syntax:

	cryptogen showtemplate

#####Usage#####
Output from the cryptogen showtemplate command is following:

	cryptogen showtemplate

	# ---------------------------------------------------------------------------
	# "OrdererOrgs" - Definition of organizations managing orderer nodes
	# ---------------------------------------------------------------------------
	OrdererOrgs:
	  # ---------------------------------------------------------------------------
	  # Orderer
	  # ---------------------------------------------------------------------------
	  - Name: Orderer
	    Domain: example.com
	
	    # ---------------------------------------------------------------------------
	    # "Specs" - See PeerOrgs below for complete description
	    # ---------------------------------------------------------------------------
	    Specs:
	      - Hostname: orderer
	
	# ---------------------------------------------------------------------------
	# "PeerOrgs" - Definition of organizations managing peer nodes
	# ---------------------------------------------------------------------------
	PeerOrgs:
	  # ---------------------------------------------------------------------------
	  # Org1
	  # ---------------------------------------------------------------------------
	  - Name: Org1
	    Domain: org1.example.com
	    EnableNodeOUs: false
	
	    # ---------------------------------------------------------------------------
	    # "CA"
	    # ---------------------------------------------------------------------------
	    # Uncomment this section to enable the explicit definition of the CA for this
	    # organization.  This entry is a Spec.  See "Specs" section below for details.
	    # ---------------------------------------------------------------------------
	    # CA:
	    #    Hostname: ca # implicitly ca.org1.example.com
	    #    Country: US
	    #    Province: California
	    #    Locality: San Francisco
	    #    OrganizationalUnit: Hyperledger Fabric
	    #    StreetAddress: address for org # default nil
	    #    PostalCode: postalCode for org # default nil
	
	    # ---------------------------------------------------------------------------
	    # "Specs"
	    # ---------------------------------------------------------------------------
	    # Uncomment this section to enable the explicit definition of hosts in your
	    # configuration.  Most users will want to use Template, below
	    #
	    # Specs is an array of Spec entries.  Each Spec entry consists of two fields:
	    #   - Hostname:   (Required) The desired hostname, sans the domain.
	    #   - CommonName: (Optional) Specifies the template or explicit override for
	    #                 the CN.  By default, this is the template:
	    #
	    #                              "{{.Hostname}}.{{.Domain}}"
	    #
	    #                 which obtains its values from the Spec.Hostname and
	    #                 Org.Domain, respectively.
	    #   - SANS:       (Optional) Specifies one or more Subject Alternative Names
	    #                 to be set in the resulting x509. Accepts template
	    #                 variables {{.Hostname}}, {{.Domain}}, {{.CommonName}}. IP
	    #                 addresses provided here will be properly recognized. Other
	    #                 values will be taken as DNS names.
	    #                 NOTE: Two implicit entries are created for you:
	    #                     - {{ .CommonName }}
	    #                     - {{ .Hostname }}
	    # ---------------------------------------------------------------------------
	    # Specs:
	    #   - Hostname: foo # implicitly "foo.org1.example.com"
	    #     CommonName: foo27.org5.example.com # overrides Hostname-based FQDN set above
	    #     SANS:
	    #       - "bar.{{.Domain}}"
	    #       - "altfoo.{{.Domain}}"
	    #       - "{{.Hostname}}.org6.net"
	    #       - 172.16.10.31
	    #   - Hostname: bar
	    #   - Hostname: baz
	
	    # ---------------------------------------------------------------------------
	    # "Template"
	    # ---------------------------------------------------------------------------
	    # Allows for the definition of 1 or more hosts that are created sequentially
	    # from a template. By default, this looks like "peer%d" from 0 to Count-1.
	    # You may override the number of nodes (Count), the starting index (Start)
	    # or the template used to construct the name (Hostname).
	    #
	    # Note: Template and Specs are not mutually exclusive.  You may define both
	    # sections and the aggregate nodes will be created for you.  Take care with
	    # name collisions
	    # ---------------------------------------------------------------------------
	    Template:
	      Count: 1
	      # Start: 5
	      # Hostname: {{.Prefix}}{{.Index}} # default
	      # SANS:
	      #   - "{{.Hostname}}.alt.{{.Domain}}"
	
	    # ---------------------------------------------------------------------------
	    # "Users"
	    # ---------------------------------------------------------------------------
	    # Count: The number of user accounts _in addition_ to Admin
	    # ---------------------------------------------------------------------------
	    Users:
	      Count: 1
	
	  # ---------------------------------------------------------------------------
	  # Org2: See "Org1" for full specification
	  # ---------------------------------------------------------------------------
	  - Name: Org2
	    Domain: org2.example.com
	    EnableNodeOUs: false
	    Template:
	      Count: 1
	    Users:
	      Count: 1

######The cryptogen extend Command######
The cryptogen extend command allows to extend an existing network, meaning generating all the additional key material needed by the new added entities.

#####Syntax#####
The cryptogen extend command has the following syntax:

	cryptogen extend [<flags>]

#####cryptogen extend flags#####
The cryptogen extend command has different flags available to it, and because of this, each flag is described in the relevant command topic.

	cryptogen extend [flags]

as follows

	cryptogen extend --input="crypto-config"
	cryptogen extend --config=CONFIG

The global cryptogen command flags also apply as described in the cryptogen command flags:

+ --help

#####Flag details#####
+ --input="crypto-config"

	the output directory in which to place artifacts.

+ --config=CONFIG

	the configuration template to use.

#####Usage#####
Here’s some examples using the different available flags on the cryptogen extend command.

	cryptogen extend --input="crypto-config" --config=config.yaml

	org3.example.com

Where config.yaml add a new peer organization called org3.example.com

####Fabric-CA Commands####
The Hyperledger Fabric CA is a Certificate Authority (CA) for Hyperledger Fabric. The commands available for the fabric-ca client and fabric-ca server are described in the links below.

#####Fabric-CA Client#####
The fabric-ca-client command allows you to manage identities (including attribute management) and certificates (including renewal and revocation).

More information on fabric-ca-client commands can be found here.

#####Fabric-CA Server#####
The fabric-ca-server command allows you to initialize and start a server process which may host one or more certificate authorities.

More information on fabric-ca-server commands can be found here.

###六、架构参考###
####Architecture Explained####
The Hyperledger Fabric architecture delivers the following advantages:

+ Chaincode trust flexibility. The architecture separates trust assumptions for chaincodes (blockchain applications) from trust assumptions for ordering. In other words, the ordering service may be provided by one set of nodes (orderers) and tolerate some of them to fail or misbehave, and the endorsers may be different for each chaincode.
+ Scalability. As the endorser nodes responsible for particular chaincode are orthogonal to the orderers, the system may scale better than if these functions were done by the same nodes. In particular, this results when different chaincodes specify disjoint endorsers, which introduces a partitioning of chaincodes between endorsers and allows parallel chaincode execution (endorsement). Besides, chaincode execution, which can potentially be costly, is removed from the critical path of the ordering service.
+ Confidentiality. The architecture facilitates deployment of chaincodes that have confidentiality requirements with respect to the content and state updates of its transactions.
+ Consensus modularity. The architecture is modular and allows pluggable consensus (i.e., ordering service) implementations.

Part I: Elements of the architecture relevant to Hyperledger Fabric v1

1. System architecture
2. Basic workflow of transaction endorsement
3. Endorsement policies

Part II: Post-v1 elements of the architecture

4. Ledger checkpointing (pruning)

#####1.System architecture#####
The blockchain is a distributed system consisting of many nodes that communicate with each other. The blockchain runs programs called chaincode, holds state and ledger data, and executes transactions. The chaincode is the central element as transactions are operations invoked on the chaincode. Transactions have to be “endorsed” and only endorsed transactions may be committed and have an effect on the state. There may exist one or more special chaincodes for management functions and parameters, collectively called system chaincodes.

######1.1.Transactions######
Transactions may be of two types:

+ Deploy transactions create new chaincode and take a program as parameter. When a deploy transaction executes successfully, the chaincode has been installed “on” the blockchain.
+ Invoke transactions perform an operation in the context of previously deployed chaincode. An invoke transaction refers to a chaincode and to one of its provided functions. When successful, the chaincode executes the specified function - which may involve modifying the corresponding state, and returning an output.

As described later, deploy transactions are special cases of invoke transactions, where a deploy transaction that creates new chaincode, corresponds to an invoke transaction on a system chaincode.

Remark: This document currently assumes that a transaction either creates new chaincode or invokes an operation provided by *one already deployed chaincode. This document does not yet describe: a) optimizations for query (read-only) transactions (included in v1), b) support for cross-chaincode transactions (post-v1 feature).*

######1.2.Blockchain datastructures######
#######1.2.1.State#######
The latest state of the blockchain (or, simply, state) is modeled as a versioned key-value store (KVS), where keys are names and values are arbitrary blobs. These entries are manipulated by the chaincodes (applications) running on the blockchain through put and get KVS-operations. The state is stored persistently and updates to the state are logged. Notice that versioned KVS is adopted as state model, an implementation may use actual KVSs, but also RDBMSs or any other solution.

More formally, state s is modeled as an element of a mapping K -> (V X N), where:

+ K is a set of keys
+ V is a set of values
+ N is an infinite ordered set of version numbers. Injective function next: N -> N takes an element of N and returns the next version number.

Both V and N contain a special element ⊥ (empty type), which is in case of N the lowest element. Initially all keys are mapped to (⊥, ⊥). For s(k)=(v,ver) we denote v by s(k).value, and ver by s(k).version.

KVS operations are modeled as follows:

+ put(k,v) for k ∈ K and v ∈ V, takes the blockchain state s and changes it to s' such that s'(k)=(v,next(s(k).version)) with s'(k')=s(k') for all k'!=k.
+ get(k) returns s(k).

State is maintained by peers, but not by orderers and clients.

State partitioning. Keys in the KVS can be recognized from their name to belong to a particular chaincode, in the sense that only transaction of a certain chaincode may modify the keys belonging to this chaincode. In principle, any chaincode can read the keys belonging to other chaincodes. Support for cross-chaincode transactions, that modify the state belonging to two or more chaincodes is a post-v1 feature.

#######1.2.2.Ledger#######
Ledger provides a verifiable history of all successful state changes (we talk about valid transactions) and unsuccessful attempts to change state (we talk about invalid transactions), occurring during the operation of the system.

Ledger is constructed by the ordering service (see Sec 1.3.3) as a totally ordered hashchain of blocks of (valid or invalid) transactions. The hashchain imposes the total order of blocks in a ledger and each block contains an array of totally ordered transactions. This imposes total order across all transactions.

Ledger is kept at all peers and, optionally, at a subset of orderers. In the context of an orderer we refer to the Ledger as to OrdererLedger, whereas in the context of a peer we refer to the ledger as to PeerLedger. PeerLedger differs from the OrdererLedger in that peers locally maintain a bitmask that tells apart valid transactions from invalid ones (see Section XX for more details).

Peers may prune PeerLedger as described in Section XX (post-v1 feature). Orderers maintain OrdererLedger for fault-tolerance and availability (of the PeerLedger) and may decide to prune it at anytime, provided that properties of the ordering service (see Sec. 1.3.3) are maintained.

The ledger allows peers to replay the history of all transactions and to reconstruct the state. Therefore, state as described in Sec 1.2.1 is an optional datastructure.

######1.3.Nodes######
Nodes are the communication entities of the blockchain. A “node” is only a logical function in the sense that multiple nodes of different types can run on the same physical server. What counts is how nodes are grouped in “trust domains” and associated to logical entities that control them.

There are three types of nodes:

1. Client or submitting-client: a client that submits an actual transaction-invocation to the endorsers, and broadcasts transaction-proposals to the ordering service.
2. Peer: a node that commits transactions and maintains the state and a copy of the ledger (see Sec, 1.2). Besides, peers can have a special endorser role.
3. Ordering-service-node or orderer: a node running the communication service that implements a delivery guarantee, such as atomic or total order broadcast.

The types of nodes are explained next in more detail.

#######1.3.1.Client#######
The client represents the entity that acts on behalf of an end-user. It must connect to a peer for communicating with the blockchain. The client may connect to any peer of its choice. Clients create and thereby invoke transactions.

As detailed in Section 2, clients communicate with both peers and the ordering service.

#######1.3.2.Peer#######
A peer receives ordered state updates in the form of blocks from the ordering service and maintain the state and the ledger.

Peers can additionally take up a special role of an endorsing peer, or an endorser. The special function of an endorsing peer occurs with respect to a particular chaincode and consists in endorsing a transaction before it is committed. Every chaincode may specify an endorsement policy that may refer to a set of endorsing peers. The policy defines the necessary and sufficient conditions for a valid transaction endorsement (typically a set of endorsers’ signatures), as described later in Sections 2 and 3. In the special case of deploy transactions that install new chaincode the (deployment) endorsement policy is specified as an endorsement policy of the system chaincode.

#######1.3.3.Ordering service nodes(Orderers)#######
The orderers form the ordering service, i.e., a communication fabric that provides delivery guarantees. The ordering service can be implemented in different ways: ranging from a centralized service (used e.g., in development and testing) to distributed protocols that target different network and node fault models.

Ordering service provides a shared communication channel to clients and peers, offering a broadcast service for messages containing transactions. Clients connect to the channel and may broadcast messages on the channel which are then delivered to all peers. The channel supports atomic delivery of all messages, that is, message communication with total-order delivery and (implementation specific) reliability. In other words, the channel outputs the same messages to all connected peers and outputs them to all peers in the same logical order. This atomic communication guarantee is also called total-order broadcast, atomic broadcast, or consensus in the context of distributed systems. The communicated messages are the candidate transactions for inclusion in the blockchain state.

Partitioning (ordering service channels). Ordering service may support multiple channels similar to the topics of a publish/subscribe (pub/sub) messaging system. Clients can connect to a given channel and can then send messages and obtain the messages that arrive. Channels can be thought of as partitions - clients connecting to one channel are unaware of the existence of other channels, but clients may connect to multiple channels. Even though some ordering service implementations included with Hyperledger Fabric support multiple channels, for simplicity of presentation, in the rest of this document, we assume ordering service consists of a single channel/topic.

Ordering service API. Peers connect to the channel provided by the ordering service, via the interface provided by the ordering service. The ordering service API consists of two basic operations (more generally asynchronous events):

TODO add the part of the API for fetching particular blocks under client/peer specified sequence numbers.

+ broadcast(blob): a client calls this to broadcast an arbitrary message blob for dissemination over the channel. This is also called request(blob) in the BFT context, when sending a request to a service.
+ deliver(seqno, prevhash, blob): the ordering service calls this on the peer to deliver the message blob with the specified non-negative integer sequence number (seqno) and hash of the most recently delivered blob (prevhash). In other words, it is an output event from the ordering service. deliver() is also sometimes called notify() in pub-sub systems or commit() in BFT systems.

Ledger and block formation. The ledger (see also Sec. 1.2.2) contains all data output by the ordering service. In a nutshell, it is a sequence of deliver(seqno, prevhash, blob) events, which form a hash chain according to the computation of prevhash described before.

Most of the time, for efficiency reasons, instead of outputting individual transactions (blobs), the ordering service will group (batch) the blobs and output blocks within a single deliver event. In this case, the ordering service must impose and convey a deterministic ordering of the blobs within each block. The number of blobs in a block may be chosen dynamically by an ordering service implementation.

In the following, for ease of presentation, we define ordering service properties (rest of this subsection) and explain the workflow of transaction endorsement (Section 2) assuming one blob per deliver event. These are easily extended to blocks, assuming that a deliver event for a block corresponds to a sequence of individual deliver events for each blob within a block, according to the above mentioned deterministic ordering of blobs within a blocs.

########Ordering service properties########
The guarantees of the ordering service (or atomic-broadcast channel) stipulate what happens to a broadcasted message and what relations exist among delivered messages. These guarantees are as follows:

1. Safety (consistency guarantees): As long as peers are connected for sufficiently long periods of time to the channel (they can disconnect or crash, but will restart and reconnect), they will see an identical series of delivered (seqno, prevhash, blob) messages. This means the outputs (deliver() events) occur in the same order on all peers and according to sequence number and carry identical content (blob and prevhash) for the same sequence number. Note this is only a logical order, and a deliver(seqno, prevhash, blob) on one peer is not required to occur in any real-time relation to deliver(seqno, prevhash, blob) that outputs the same message at another peer. Put differently, given a particular seqno, no two correct peers deliver different prevhash or blob values. Moreover, no value blob is delivered unless some client (peer) actually called broadcast(blob) and, preferably, every broadcasted blob is only delivered once.

	Furthermore, the deliver() event contains the cryptographic hash of the data in the previous deliver() event (prevhash). When the ordering service implements atomic broadcast guarantees, prevhash is the cryptographic hash of the parameters from the deliver() event with sequence number seqno-1. This establishes a hash chain across deliver() events, which is used to help verify the integrity of the ordering service output, as discussed in Sections 4 and 5 later. In the special case of the first deliver() event, prevhash has a default value.
2. Liveness (delivery guarantee): Liveness guarantees of the ordering service are specified by a ordering service implementation. The exact guarantees may depend on the network and node fault model.

	In principle, if the submitting client does not fail, the ordering service should guarantee that every correct peer that connects to the ordering service eventually delivers every submitted transaction.

To summarize, the ordering service ensures the following properties:

+ Agreement. For any two events at correct peers deliver(seqno, prevhash0, blob0) and deliver(seqno, prevhash1, blob1) with the same seqno, prevhash0==prevhash1 and blob0==blob1;
+ Hashchain integrity. For any two events at correct peers deliver(seqno-1, prevhash0, blob0) and deliver(seqno, prevhash, blob), prevhash = HASH(seqno-1||prevhash0||blob0).
+ No skipping. If an ordering service outputs deliver(seqno, prevhash, blob) at a correct peer p, such that seqno>0, then p already delivered an event deliver(seqno-1, prevhash0, blob0).
+ No creation. Any event deliver(seqno, prevhash, blob) at a correct peer must be preceded by a broadcast(blob) event at some (possibly distinct) peer;
+ No duplication (optional, yet desirable). For any two events broadcast(blob) and broadcast(blob'), when two events deliver(seqno0, prevhash0, blob) and deliver(seqno1, prevhash1, blob') occur at correct peers and blob == blob', then seqno0==seqno1 and prevhash0==prevhash1.
+ Liveness. If a correct client invokes an event broadcast(blob) then every correct peer “eventually” issues an event deliver(*, *, blob), where * denotes an arbitrary value.

#####2.Basic workflow of transaction endorsement#####
In the following we outline the high-level request flow for a transaction.

Remark: Notice that the following protocol *does not assume that all transactions are deterministic, i.e., it allows for non-deterministic transactions.*

######2.1.The client creates a transaction and sends it to endorsing peers of its choice######
To invoke a transaction, the client sends a PROPOSE message to a set of endorsing peers of its choice (possibly not at the same time - see Sections 2.1.2. and 2.3.). The set of endorsing peers for a given chaincodeID is made available to client via peer, which in turn knows the set of endorsing peers from endorsement policy (see Section 3). For example, the transaction could be sent to all endorsers of a given chaincodeID. That said, some endorsers could be offline, others may object and choose not to endorse the transaction. The submitting client tries to satisfy the policy expression with the endorsers available.

In the following, we first detail PROPOSE message format and then discuss possible patterns of interaction between submitting client and endorsers.

######2.1.1.PROPOSE messsage format######
The format of a PROPOSE message is <PROPOSE,tx,[anchor]>, where tx is a mandatory and anchor optional argument explained in the following.

+ tx=<clientID,chaincodeID,txPayload,timestamp,clientSig>, where

		+ clientID is an ID of the submitting client,
		+ chaincodeID refers to the chaincode to which the transaction pertains,
		+ txPayload is the payload containing the submitted transaction itself,
		+ timestamp is a monotonically increasing (for every new transaction) integer maintained by the client,
		+ clientSig is signature of a client on other fields of tx.
		
		The details of txPayload will differ between invoke transactions and deploy transactions (i.e., invoke transactions referring to a deploy-specific system chaincode). For an invoke transaction, txPayload would consist of two fields
	
		+ txPayload = <operation, metadata>, where
				+ operation denotes the chaincode operation (function) and arguments,
				+ metadata denotes attributes related to the invocation.
		For a deploy transaction, txPayload would consist of three fields
		+ txPayload = <source, metadata, policies>, where
			+ source denotes the source code of the chaincode,
			+ metadata denotes attributes related to the chaincode and application,
			+ policies contains policies related to the chaincode that are accessible to all peers, such as the endorsement policy. Note that endorsement policies are not supplied with txPayload in a deploy transaction, but txPayload of a deploy contains endorsement policy ID and its parameters (see Section 3).

+ anchor contains read version dependencies, or more specifically, key-version pairs (i.e., anchor is a subset of KxN), that binds or “anchors” the PROPOSE request to specified versions of keys in a KVS (see Section 1.2.). If the client specifies the anchor argument, an endorser endorses a transaction only upon read version numbers of corresponding keys in its local KVS match anchor (see Section 2.2. for more details).

Cryptographic hash of tx is used by all nodes as a unique transaction identifier tid (i.e., tid=HASH(tx)). The client stores tid in memory and waits for responses from endorsing peers.

#######2.1.2.Message patterns#######
The client decides on the sequence of interaction with endorsers. For example, a client would typically send <PROPOSE, tx> (i.e., without the anchor argument) to a single endorser, which would then produce the version dependencies (anchor) which the client can later on use as an argument of its PROPOSE message to other endorsers. As another example, the client could directly send <PROPOSE, tx> (without anchor) to all endorsers of its choice. Different patterns of communication are possible and client is free to decide on those (see also Section 2.3.).

######2.2.The endorsing peer simulates a transaction and produces an endorsement signature######
On reception of a <PROPOSE,tx,[anchor]> message from a client, the endorsing peer epID first verifies the client’s signature clientSig and then simulates a transaction. If the client specifies anchor then endorsing peer simulates the transactions only upon read version numbers (i.e., readset as defined below) of corresponding keys in its local KVS match those version numbers specified by anchor.

Simulating a transaction involves endorsing peer tentatively executing a transaction (txPayload), by invoking the chaincode to which the transaction refers (chaincodeID) and the copy of the state that the endorsing peer locally holds.

As a result of the execution, the endorsing peer computes read version dependencies (readset) and state updates (writeset), also called MVCC+postimage info in DB language.

Recall that the state consists of key-value pairs. All key-value entries are versioned; that is, every entry contains ordered version information, which is incremented each time the value stored under a key is updated. The peer that interprets the transaction records all key-value pairs accessed by the chaincode, either for reading or for writing, but the peer does not yet update its state. More specifically:

+ Given state s before an endorsing peer executes a transaction, for every key k read by the transaction, pair (k,s(k).version) is added to readset.
+ Additionally, for every key k modified by the transaction to the new value v', pair (k,v') is added to writeset. Alternatively, v' could be the delta of the new value to previous value (s(k).value).

If a client specifies anchor in the PROPOSE message then client specified anchor must equal readset produced by endorsing peer when simulating the transaction.

Then, the peer forwards internally tran-proposal (and possibly tx) to the part of its (peer’s) logic that endorses a transaction, referred to as endorsing logic. By default, endorsing logic at a peer accepts the tran-proposal and simply signs the tran-proposal. However, endorsing logic may interpret arbitrary functionality, to, e.g., interact with legacy systems with tran-proposal and tx as inputs to reach the decision whether to endorse a transaction or not.

If endorsing logic decides to endorse a transaction, it sends <TRANSACTION-ENDORSED, tid, tran-proposal,epSig> message to the submitting client(tx.clientID), where:

+ tran-proposal := (epID,tid,chaincodeID,txContentBlob,readset,writeset),

	where txContentBlob is chaincode/transaction specific information. The intention is to have txContentBlob used as some representation of tx (e.g., txContentBlob=tx.txPayload).

+ epSig is the endorsing peer’s signature on tran-proposal

Else, in case the endorsing logic refuses to endorse the transaction, an endorser may send a message (TRANSACTION-INVALID, tid, REJECTED) to the submitting client.

Notice that an endorser does not change its state in this step, the updates produced by transaction simulation in the context of endorsement do not affect the state!

######2.3.The submitting client collects an endorsement for a transaction and broadcasts it through ordering service######
The submitting client waits until it receives “enough” messages and signatures on (TRANSACTION-ENDORSED, tid, *, *) statements to conclude that the transaction proposal is endorsed. As discussed in Section 2.1.2., this may involve one or more round-trips of interaction with endorsers.

The exact number of “enough” depend on the chaincode endorsement policy (see also Section 3). If the endorsement policy is satisfied, the transaction has been endorsed; note that it is not yet committed. The collection of signed TRANSACTION-ENDORSED messages from endorsing peers which establish that a transaction is endorsed is called an endorsement and denoted by endorsement.

If the submitting client does not manage to collect an endorsement for a transaction proposal, it abandons this transaction with an option to retry later.

For transaction with a valid endorsement, we now start using the ordering service. The submitting client invokes ordering service using the broadcast(blob), where blob=endorsement. If the client does not have capability of invoking ordering service directly, it may proxy its broadcast through some peer of its choice. Such a peer must be trusted by the client not to remove any message from the endorsement or otherwise the transaction may be deemed invalid. Notice that, however, a proxy peer may not fabricate a valid endorsement.

######2.4.The ordering service delivers a transactions to the peers######
When an event deliver(seqno, prevhash, blob) occurs and a peer has applied all state updates for blobs with sequence number lower than seqno, a peer does the following:

+ It checks that the blob.endorsement is valid according to the policy of the chaincode (blob.tran-proposal.chaincodeID) to which it refers.
+ In a typical case, it also verifies that the dependencies (blob.endorsement.tran-proposal.readset) have not been violated meanwhile. In more complex use cases, tran-proposal fields in endorsement may differ and in this case endorsement policy (Section 3) specifies how the state evolves.

Verification of dependencies can be implemented in different ways, according to a consistency property or “isolation guarantee” that is chosen for the state updates. Serializability is a default isolation guarantee, unless chaincode endorsement policy specifies a different one. Serializability can be provided by requiring the version associated with every key in the readset to be equal to that key’s version in the state, and rejecting transactions that do not satisfy this requirement.

+ If all these checks pass, the transaction is deemed valid or committed. In this case, the peer marks the transaction with 1 in the bitmask of the PeerLedger, applies blob.endorsement.tran-proposal.writeset to blockchain state (if tran-proposals are the same, otherwise endorsement policy logic defines the function that takes blob.endorsement).
+ If the endorsement policy verification of blob.endorsement fails, the transaction is invalid and the peer marks the transaction with 0 in the bitmask of the PeerLedger. It is important to note that invalid transactions do not change the state.

Note that this is sufficient to have all (correct) peers have the same state after processing a deliver event (block) with a given sequence number. Namely, by the guarantees of the ordering service, all correct peers will receive an identical sequence of deliver(seqno, prevhash, blob) events. As the evaluation of the endorsement policy and evaluation of version dependencies in readset are deterministic, all correct peers will also come to the same conclusion whether a transaction contained in a blob is valid. Hence, all peers commit and apply the same sequence of transactions and update their state in the same way.
![](images/flow-4.png)
Figure 1. Illustration of one possible transaction flow (common-case path).

#####3.Endorsement policies#####
######3.1 Endorsement policy specification######
An endorsement policy, is a condition on what endorses a transaction. Blockchain peers have a pre-specified set of endorsement policies, which are referenced by a deploy transaction that installs specific chaincode. Endorsement policies can be parametrized, and these parameters can be specified by a deploy transaction.

To guarantee blockchain and security properties, the set of endorsement policies should be a set of proven policies with limited set of functions in order to ensure bounded execution time (termination), determinism, performance and security guarantees.

Dynamic addition of endorsement policies (e.g., by deploy transaction on chaincode deploy time) is very sensitive in terms of bounded policy evaluation time (termination), determinism, performance and security guarantees. Therefore, dynamic addition of endorsement policies is not allowed, but can be supported in future.

######3.2 Transaction evaluation against endorsement policy######
A transaction is declared valid only if it has been endorsed according to the policy. An invoke transaction for a chaincode will first have to obtain an endorsement that satisfies the chaincode’s policy or it will not be committed. This takes place through the interaction between the submitting client and endorsing peers as explained in Section 2.

Formally the endorsement policy is a predicate on the endorsement, and potentially further state that evaluates to TRUE or FALSE. For deploy transactions the endorsement is obtained according to a system-wide policy (for example, from the system chaincode).

An endorsement policy predicate refers to certain variables. Potentially it may refer to:

1. keys or identities relating to the chaincode (found in the metadata of the chaincode), for example, a set of endorsers;
2. further metadata of the chaincode;
3. elements of the endorsement and endorsement.tran-proposal;
4. and potentially more.

The above list is ordered by increasing expressiveness and complexity, that is, it will be relatively simple to support policies that only refer to keys and identities of nodes.

The evaluation of an endorsement policy predicate must be deterministic. An endorsement shall be evaluated locally by every peer such that a peer does not need to interact with other peers, yet all correct peers evaluate the endorsement policy in the same way.

######3.3 Example endorsement policies######
The predicate may contain logical expressions and evaluates to TRUE or FALSE. Typically the condition will use digital signatures on the transaction invocation issued by endorsing peers for the chaincode.

Suppose the chaincode specifies the endorser set E = {Alice, Bob, Charlie, Dave, Eve, Frank, George}. Some example policies:

+ A valid signature from on the same tran-proposal from all members of E.
+ A valid signature from any single member of E.
+ Valid signatures on the same tran-proposal from endorsing peers according to the condition (Alice OR Bob) AND (any two of: Charlie, Dave, Eve, Frank, George).
+ Valid signatures on the same tran-proposal by any 5 out of the 7 endorsers. (More generally, for chaincode with n > 3f endorsers, valid signatures by any 2f+1 out of the n endorsers, or by any group of more than (n+f)/2 endorsers.)
+ Suppose there is an assignment of “stake” or “weights” to the endorsers, like {Alice=49, Bob=15, Charlie=15, Dave=10, Eve=7, Frank=3, George=1}, where the total stake is 100: The policy requires valid signatures from a set that has a majority of the stake (i.e., a group with combined stake strictly more than 50), such as {Alice, X} with any X different from George, or {everyone together except Alice}. And so on.
+ The assignment of stake in the previous example condition could be static (fixed in the metadata of the chaincode) or dynamic (e.g., dependent on the state of the chaincode and be modified during the execution).
+ Valid signatures from (Alice OR Bob) on tran-proposal1 and valid signatures from (any two of: Charlie, Dave, Eve, Frank, George) on tran-proposal2, where tran-proposal1 and tran-proposal2 differ only in their endorsing peers and state updates.

How useful these policies are will depend on the application, on the desired resilience of the solution against failures or misbehavior of endorsers, and on various other properties.

#####4 (post-v1). Validated ledger and PeerLedger checkpointing (pruning)#####
######4.1. Validated ledger (VLedger)######
To maintain the abstraction of a ledger that contains only valid and committed transactions (that appears in Bitcoin, for example), peers may, in addition to state and Ledger, maintain the Validated Ledger (or VLedger). This is a hash chain derived from the ledger by filtering out invalid transactions.

The construction of the VLedger blocks (called here vBlocks) proceeds as follows. As the PeerLedger blocks may contain invalid transactions (i.e., transactions with invalid endorsement or with invalid version dependencies), such transactions are filtered out by peers before a transaction from a block becomes added to a vBlock. Every peer does this by itself (e.g., by using the bitmask associated with PeerLedger). A vBlock is defined as a block without the invalid transactions, that have been filtered out. Such vBlocks are inherently dynamic in size and may be empty. An illustration of vBlock construction is given in the figure below.
![](images/blocks-3.png)
Figure 2. Illustration of validated ledger block (vBlock) formation from ledger (PeerLedger) blocks.

vBlocks are chained together to a hash chain by every peer. More specifically, every block of a validated ledger contains:

+ The hash of the previous vBlock.
+ vBlock number.
+ An ordered list of all valid transactions committed by the peers since the last vBlock was computed (i.e., list of valid transactions in a corresponding block).
+ The hash of the corresponding block (in PeerLedger) from which the current vBlock is derived.

All this information is concatenated and hashed by a peer, producing the hash of the vBlock in the validated ledger.

######4.2. PeerLedger Checkpointing######
The ledger contains invalid transactions, which may not necessarily be recorded forever. However, peers cannot simply discard PeerLedger blocks and thereby prune PeerLedger once they establish the corresponding vBlocks. Namely, in this case, if a new peer joins the network, other peers could not transfer the discarded blocks (pertaining to PeerLedger) to the joining peer, nor convince the joining peer of the validity of their vBlocks.

To facilitate pruning of the PeerLedger, this document describes a checkpointing mechanism. This mechanism establishes the validity of the vBlocks across the peer network and allows checkpointed vBlocks to replace the discarded PeerLedger blocks. This, in turn, reduces storage space, as there is no need to store invalid transactions. It also reduces the work to reconstruct the state for new peers that join the network (as they do not need to establish validity of individual transactions when reconstructing the state by replaying PeerLedger, but may simply replay the state updates contained in the validated ledger).

#######4.2.1. Checkpointing protocol#######
Checkpointing is performed periodically by the peers every CHK blocks, where CHK is a configurable parameter. To initiate a checkpoint, the peers broadcast (e.g., gossip) to other peers message <CHECKPOINT,blocknohash,blockno,stateHash,peerSig>, where blockno is the current blocknumber and blocknohash is its respective hash, stateHash is the hash of the latest state (produced by e.g., a Merkle hash) upon validation of block blockno and peerSig is peer’s signature on (CHECKPOINT,blocknohash,blockno,stateHash), referring to the validated ledger.

A peer collects CHECKPOINT messages until it obtains enough correctly signed messages with matching blockno, blocknohash and stateHash to establish a valid checkpoint (see Section 4.2.2.).

Upon establishing a valid checkpoint for block number blockno with blocknohash, a peer:

+ if blockno>latestValidCheckpoint.blockno, then a peer assigns latestValidCheckpoint=(blocknohash,blockno),
+ stores the set of respective peer signatures that constitute a valid checkpoint into the set latestValidCheckpointProof,
+ stores the state corresponding to stateHash to latestValidCheckpointedState,
+ (optionally) prunes its PeerLedger up to block number blockno (inclusive).

#######4.2.2. Valid checkpoints#######
Clearly, the checkpointing protocol raises the following questions: When can a peer prune its ``PeerLedger``? How many ``CHECKPOINT`` messages are “sufficiently many”?. This is defined by a checkpoint validity policy, with (at least) two possible approaches, which may also be combined:

+ Local (peer-specific) checkpoint validity policy (LCVP). A local policy at a given peer p may specify a set of peers which peer p trusts and whose CHECKPOINT messages are sufficient to establish a valid checkpoint. For example, LCVP at peer Alice may define that Alice needs to receive CHECKPOINT message from Bob, or from both Charlie and Dave.
+ Global checkpoint validity policy (GCVP). A checkpoint validity policy may be specified globally. This is similar to a local peer policy, except that it is stipulated at the system (blockchain) granularity, rather than peer granularity. For instance, GCVP may specify that:

		+ each peer may trust a checkpoint if confirmed by 11 different peers.
		+ in a specific deployment in which every orderer is collocated with a peer in the same machine (i.e., trust domain) and where up to f orderers may be (Byzantine) faulty, each peer may trust a checkpoint if confirmed by f+1 different peers collocated with orderers.

####Transaction Flow####
This document outlines the transactional mechanics that take place during a standard asset exchange. The scenario includes two clients, A and B, who are buying and selling radishes. They each have a peer on the network through which they send their transactions and interact with the ledger.

![](images/step0.png)

Assumptions

This flow assumes that a channel is set up and running. The application user has registered and enrolled with the organization’s certificate authority (CA) and received back necessary cryptographic material, which is used to authenticate to the network.

The chaincode (containing a set of key value pairs representing the initial state of the radish market) is installed on the peers and instantiated on the channel. The chaincode contains logic defining a set of transaction instructions and the agreed upon price for a radish. An endorsement policy has also been set for this chaincode, stating that both peerA and peerB must endorse any transaction.

![](images/step1.png)

1. Client A initiates a transaction

What’s happening? - Client A is sending a request to purchase radishes. The request targets peerA and peerB, who are respectively representative of Client A and Client B. The endorsement policy states that both peers must endorse any transaction, therefore the request goes to peerA and peerB.

Next, the transaction proposal is constructed. An application leveraging a supported SDK (Node, Java, Python) utilizes one of the available API’s which generates a transaction proposal. The proposal is a request to invoke a chaincode function so that data can be read and/or written to the ledger (i.e. write new key value pairs for the assets). The SDK serves as a shim to package the transaction proposal into the properly architected format (protocol buffer over gRPC) and takes the user’s cryptographic credentials to produce a unique signature for this transaction proposal.

![](images/step2.png)

2. Endorsing peers verify signature & execute the transaction

The endorsing peers verify (1) that the transaction proposal is well formed, (2) it has not been submitted already in the past (replay-attack protection), (3) the signature is valid (using MSP), and (4) that the submitter (Client A, in the example) is properly authorized to perform the proposed operation on that channel (namely, each endorsing peer ensures that the submitter satisfies the channel’s Writers policy). The endorsing peers take the transaction proposal inputs as arguments to the invoked chaincode’s function. The chaincode is then executed against the current state database to produce transaction results including a response value, read set, and write set. No updates are made to the ledger at this point. The set of these values, along with the endorsing peer’s signature is passed back as a “proposal response” to the SDK which parses the payload for the application to consume.

{The MSP is a peer component that allows them to verify transaction requests arriving from clients and to sign transaction results(endorsements). The Writing policy is defined at channel creation time, and determines which user is entitled to submit a transaction to that channel.}

![](images/step3.png)

3. Proposal responses are inspected

The application verifies the endorsing peer signatures and compares the proposal responses to determine if the proposal responses are the same. If the chaincode only queried the ledger, the application would inspect the query response and would typically not submit the transaction to Ordering Service. If the client application intends to submit the transaction to Ordering Service to update the ledger, the application determines if the specified endorsement policy has been fulfilled before submitting (i.e. did peerA and peerB both endorse). The architecture is such that even if an application chooses not to inspect responses or otherwise forwards an unendorsed transaction, the endorsement policy will still be enforced by peers and upheld at the commit validation phase.

![](images/step4.png)

4. Client assembles endorsements into a transaction

The application “broadcasts” the transaction proposal and response within a “transaction message” to the Ordering Service. The transaction will contain the read/write sets, the endorsing peers signatures and the Channel ID. The Ordering Service does not need to inspect the entire content of a transaction in order to perform its operation, it simply receives transactions from all channels in the network, orders them chronologically by channel, and creates blocks of transactions per channel.

![](images/step5.png)

5. Transaction is validated and committed

The blocks of transactions are “delivered” to all peers on the channel. The transactions within the block are validated to ensure endorsement policy is fulfilled and to ensure that there have been no changes to ledger state for read set variables since the read set was generated by the transaction execution. Transactions in the block are tagged as being valid or invalid.

![](images/step6.png)

6. Ledger updated

Each peer appends the block to the channel’s chain, and for each valid transaction the write sets are committed to current state database. An event is emitted, to notify the client application that the transaction (invocation) has been immutably appended to the chain, as well as notification of whether the transaction was validated or invalidated.

Note: See the swimlane diagram to better understand the server side flow and the protobuffers.

####Hyperledger Fabric CA's User Guide####
The Hyperledger Fabric CA is a Certificate Authority (CA) for Hyperledger Fabric.

It provides features such as:

+ registration of identities, or connects to LDAP as the user registry
+ issuance of Enrollment Certificates (ECerts)
+ certificate renewal and revocation

Hyperledger Fabric CA consists of both a server and a client component as described later in this document.

For developers interested in contributing to Hyperledger Fabric CA, see the Fabric CA repository for more information.

#####Table of Contents#####
1. Overview
2. Getting Started
	1. Prerequisites
	2. Install
	3. Explore the Fabric CA CLI
3. Configuration Settings
	1. A word on file paths
4. Fabric CA Server
	1. Initializing the server
	2. Starting the server
	3. Configuring the database
	4. Configuring LDAP
	5. Setting up a cluster
	6. Setting up multiple CAs
	7. Enrolling an intermediate CA
	8. Upgrading the server
5. Fabric CA Client
	1. Enrolling the boorstrap identity
	2. Registering a new identity
	3. Enrolling a peer identity
	4. Getting a CA certificate chain from another Fabric CA server
	5. Reenrolling an identity
	6. Revoking a certificate or identity
	7. Generating a CRL(Certificate Revocation List)
	8. Attribute-Base Access Control
	9. Dynamic Server Configuration Update
	10. Enabling TLS
	11. Contact specific CA instance
6. HSM
	1. Configuring Fabric CA server to use softhsm2
7. File Formats
	1. Fabric CA server's configuration file format
	2. Fabric CA client's configuration file format
8.	Troubleshooting

######Overview######
The diagram below illustrates how the Hyperledger Fabric CA server fits into the overall Hyperledger Fabric architecture.

![](images/fabric-ca.png)

There are two ways of interacting with a Hyperledger Fabric CA server: via the Hyperledger Fabric CA client or through one of the Fabric SDKs. All communication to the Hyperledger Fabric CA server is via REST APIs. See fabric-ca/swagger/swagger-fabric-ca.json for the swagger documentation for these REST APIs. You may view this documentation via the http://editor2.swagger.io online editor.

The Hyperledger Fabric CA client or SDK may connect to a server in a cluster of Hyperledger Fabric CA servers. This is illustrated in the top right section of the diagram. The client routes to an HA Proxy endpoint which load balances traffic to one of the fabric-ca-server cluster members.

All Hyperledger Fabric CA servers in a cluster share the same database for keeping track of identities and certificates. If LDAP is configured, the identity information is kept in LDAP rather than the database.

A server may contain multiple CAs. Each CA is either a root CA or an intermediate CA. Each intermediate CA has a parent CA which is either a root CA or another intermediate CA.

######Getting Started######
#######Prerequisites#######
+ Go 1.9+ installation
+ GOPATH environment variable is set correctly
+ libtool and libtdhl-dev packages are installed

The following installs the libtool dependencies on Ubuntu:

	sudo apt install libtool libltdl-dev

The following installs the libtool dependencies on MacOSX:

	brew install libtool

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		libtldl-dev is not necessary on MacOSX if you instal libtool via Homebrew
		</td>
	</tr>
</table>

For more information on libtool, see https://www.gnu.org/software/libtool.

For more information on libltdl-dev, see https://www.gnu.org/software/libtool/manual/html_node/Using-libltdl.html.

#######Install#######
The following installs both the fabric-ca-server and fabric-ca-client binaries in $GOPATH/bin.

	go get -u github.com/hyperledger/fabric-ca/cmd/...

Note: If you have already cloned the fabric-ca repository, make sure you are on the master branch before running the ‘go get’ command above. Otherwise, you might see the following error:

	<gopath>/src/github.com/hyperledger/fabric-ca; git pull --ff-only
	There is no tracking information for the current branch.
	Please specify which branch you want to merge with.
	See git-pull(1) for details.
	
	    git pull <remote> <branch>
	
	If you wish to set tracking information for this branch you can do so with:
	
	    git branch --set-upstream-to=<remote>/<branch> tlsdoc
	
	package github.com/hyperledger/fabric-ca/cmd/fabric-ca-client: exit status 1

#######Start Server Natively#######
The following starts the fabric-ca-server with default settings.

	fabric-ca-server start -b admin:adminpw

The -b option provides the enrollment ID and secret for a bootstrap administrator; this is required if LDAP is not enabled with the “ldap.enabled” setting.

A default configuration file named fabric-ca-server-config.yaml is created in the local directory which can be customized.

#######Start Server via Docker#######
########Docker Hub########
Go to: https://hub.docker.com/r/hyperledger/fabric-ca/tags/

Find the tag that matches the architecture and version of fabric-ca that you want to pull.

Navigate to $GOPATH/src/github.com/hyperledger/fabric-ca/docker/server and open up docker-compose.yml in an editor.

Change the image line to reflect the tag you found previously. The file may look like this for an x86 architecture for version beta.

	fabric-ca-server:
	  image: hyperledger/fabric-ca:x86_64-1.0.0-beta
	  container_name: fabric-ca-server
	  ports:
	    - "7054:7054"
	  environment:
	    - FABRIC_CA_HOME=/etc/hyperledger/fabric-ca-server
	  volumes:
	    - "./fabric-ca-server:/etc/hyperledger/fabric-ca-server"
	  command: sh -c 'fabric-ca-server start -b admin:adminpw'

Open up a terminal in the same directory as the docker-compose.yml file and execute the following:

	# docker-compose up -d

This will pull down the specified fabric-ca image in the compose file if it does not already exist, and start an instance of the fabric-ca server.

########Building Your Own Docker image########
You can build and start the server via docker-compose as shown below.

	cd $GOPATH/src/github.com/hyperledger/fabric-ca
	make docker
	cd docker/server
	docker-compose up -d

The hyperledger/fabric-ca docker image contains both the fabric-ca-server and the fabric-ca-client.

	# cd $GOPATH/src/github.com/hyperledger/fabric-ca
	# FABRIC_CA_DYNAMIC_LINK=true make docker
	# cd docker/server
	# docker-compose up -d

########Explore the Fabric CA CLI########
This section simply provides the usage messages for the Fabric CA server and client for convenience. Additional usage information is provided in following sections.

The following links shows the Server Command Line and Client Command Line.

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		Note that command line options that are string slices (lists) can be specified either by specifying the option with comma-separated list elements or by specifying the option multiple times, each with a string value that make up the list. For example, to specify host1 and host2 for the csr.hosts option, you can either pass --csr.hosts 'host1,host2' or --csr.hosts host1 --csr.hosts host2. When using the former format, please make sure there are no space before or after any commas.
		</td>
	</tr>
</table>

########Configuration Settings########
The Fabric CA provides 3 ways to configure settings on the Fabric CA server and client. The precedence order is:

1. CLI flags
2. Environment variables
3. Configuration file

In the remainder of this document, we refer to making changes to configuration files. However, configuration file changes can be overridden through environment variables or CLI flags.

For example, if we have the following in the client configuration file:

	tls:
	  # Enable TLS (default: false)
	  enabled: false
	
	  # TLS for the client's listenting port (default: false)
	  certfiles:
	  client:
	    certfile: cert.pem
	    keyfile:

The following environment variable may be used to override the cert.pem setting in the configuration file:

	export FABRIC_CA_CLIENT_TLS_CLIENT_CERTFILE=cert2.pem

If we wanted to override both the environment variable and configuration file, we can use a command line flag.

	fabric-ca-client enroll --tls.client.certfile cert3.pem

The same approach applies to fabric-ca-server, except instead of using FABIRC_CA_CLIENT as the prefix to environment variables, FABRIC_CA_SERVER is used.

########A word on file paths########
All the properties in the Fabric CA server and client configuration file that specify file names support both relative and absolute paths. Relative paths are relative to the config directory, where the configuration file is located. For example, if the config directory is ~/config and the tls section is as shown below, the Fabric CA server or client will look for the root.pem file in the ~/config directory, cert.pem file in the ~/config/certs directory and the key.pem file in the /abs/path directory

	tls:
	  enabled: true
	  certfiles:
	    - root.pem
	  client:
	    certfile: certs/cert.pem
	    keyfile: /abs/path/key.pem

######Fabric CA Server######
This section describes the Fabric CA server.

You may initialize the Fabric CA server before starting it. This provides an opportunity for you to generate a default configuration file that can be reviewed and customized before starting the server.

The Fabric CA server’s home directory is determined as follows:
+ if the –home command line option is set, use its value
+ otherwise, if the FABRIC_CA_SERVER_HOME environment variable is set, use its value
+ otherwise, if FABRIC_CA_HOME environment variable is set, use its value
+ otherwise, if the CA_CFG_PATH environment variable is set, use its value
+ otherwise, use current working directory

For the remainder of this server section, we assume that you have set the FABRIC_CA_HOME environment variable to $HOME/fabric-ca/server.

The instructions below assume that the server configuration file exists in the server’s home directory.

#######Initializing the server#######
Initialize the Fabric CA server as follows:

	fabric-ca-server init -b admin:adminpw

The -b (bootstrap identity) option is required for initialization when LDAP is disabled. At least one bootstrap identity is required to start the Fabric CA server; this identity is the server administrator.

The server configuration file contains a Certificate Signing Request (CSR) section that can be configured. The following is a sample CSR.

	cn: fabric-ca-server
	names:
	   - C: US
	     ST: "North Carolina"
	     L:
	     O: Hyperledger
	     OU: Fabric
	hosts:
	  - host1.example.com
	  - localhost
	ca:
	   expiry: 131400h
	   pathlength: 1

All of the fields above pertain to the X.509 signing key and certificate which is generated by the fabric-ca-server init. This corresponds to the ca.certfile and ca.keyfile files in the server’s configuration file. The fields are as follows:

+ cn is the Common Name
+ O is the organization name
+ OU is the organizational unit
+ L is the location or city
+ ST is the state
+ C is the country

If custom values for the CSR are required, you may customize the configuration file, delete the files specified by the ca.certfile and ca.keyfile configuration items, and then run the fabric-ca-server init -b admin:adminpw command again.

The fabric-ca-server init command generates a self-signed CA certificate unless the -u <parent-fabric-ca-server-URL> option is specified. If the -u is specified, the server’s CA certificate is signed by the parent Fabric CA server. In order to authenticate to the parent Fabric CA server, the URL must be of the form <scheme>://<enrollmentID>:<secret>@<host>:<port>, where <enrollmentID> and <secret> correspond to an identity with an ‘hf.IntermediateCA’ attribute whose value equals ‘true’. The fabric-ca-server init command also generates a default configuration file named fabric-ca-server-config.yaml in the server’s home directory.

If you want the Fabric CA server to use a CA signing certificate and key file which you provide, you must place your files in the location referenced by ca.certfile and ca.keyfile respectively. Both files must be PEM-encoded and must not be encrypted. More specifically, the contents of the CA certificate file must begin with -----BEGIN CERTIFICATE----- and the contents of the key file must begin with -----BEGIN PRIVATE KEY----- and not -----BEGIN ENCRYPTED PRIVATE KEY-----.

Algorithms and key sizes

The CSR can be customized to generate X.509 certificates and keys that support Elliptic Curve (ECDSA). The following setting is an example of the implementation of Elliptic Curve Digital Signature Algorithm (ECDSA) with curve prime256v1 and signature algorithm ecdsa-with-SHA256:

	key:
	   algo: ecdsa
	   size: 256

The choice of algorithm and key size are based on security needs.

Elliptic Curve (ECDSA) offers the following key size options:

	size	ASN1 OID	Signature Algorithm
	256	prime256v1	ecdsa-with-SHA256
	384	secp384r1	ecdsa-with-SHA384
	521	secp521r1	ecdsa-with-SHA512

#######Starting the server#######
Start the Fabric CA server as follows:

	fabric-ca-server start -b <admin>:<adminpw>

If the server has not been previously initialized, it will initialize itself as it starts for the first time. During this initialization, the server will generate the ca-cert.pem and ca-key.pem files if they don’t yet exist and will also create a default configuration file if it does not exist. See the Initialize the Fabric CA server section.

Unless the Fabric CA server is configured to use LDAP, it must be configured with at least one pre-registered bootstrap identity to enable you to register and enroll other identities. The -b option specifies the name and password for a bootstrap identity.

To cause the Fabric CA server to listen on https rather than http, set tls.enabled to true.

SECURITY WARNING: The Fabric CA server should always be started with TLS enabled (tls.enabled set to true). Failure to do so leaves the server vulnerable to an attacker with access to network traffic.

To limit the number of times that the same secret (or password) can be used for enrollment, set the registry.maxenrollments in the configuration file to the appropriate value. If you set the value to 1, the Fabric CA server allows passwords to only be used once for a particular enrollment ID. If you set the value to -1, the Fabric CA server places no limit on the number of times that a secret can be reused for enrollment. The default value is -1. Setting the value to 0, the Fabric CA server will disable enrollment for all identities and registration of identities will not be allowed.

The Fabric CA server should now be listening on port 7054.

You may skip to the Fabric CA Client section if you do not want to configure the Fabric CA server to run in a cluster or to use LDAP.

#######Configuring the database#######
This section describes how to configure the Fabric CA server to connect to PostgreSQL or MySQL databases. The default database is SQLite and the default database file is fabric-ca-server.db in the Fabric CA server’s home directory.

If you don’t care about running the Fabric CA server in a cluster, you may skip this section; otherwise, you must configure either PostgreSQL or MySQL as described below. Fabric CA supports the following database versions in a cluster setup:

+ PostgreSQL: 9.5.5 or later
+ MySQL: 5.7 or later

########PostgreSQL########
The following sample may be added to the server’s configuration file in order to connect to a PostgreSQL database. Be sure to customize the various values appropriately. There are limitations on what characters are allowed in the database name. Please refer to the following Postgres documentation for more information: https://www.postgresql.org/docs/current/static/sql-syntax-lexical.html#SQL-SYNTAX-IDENTIFIERS

	db:
	  type: postgres
	  datasource: host=localhost port=5432 user=Username password=Password dbname=fabric_ca sslmode=verify-full

Specifying sslmode configures the type of SSL authentication. Valid values for sslmode are:

	| Mode        	| Description		|
    | --------    	| -------			|
    | disable       | No SSL			|
    | require       | Always SSL (skip verification)|
    | verify-ca	    | Always SSL (verify that the certificate presented by the server was signed by a trusted CA)|
	| verify-full   | Same as verify-ca AND verify that the certificate presented by the server was signed by a trusted CA and the server hostname matches the one in the certificate|

If you would like to use TLS, then the db.tls section in the Fabric CA server configuration file must be specified. If SSL client authentication is enabled on the PostgreSQL server, then the client certificate and key file must also be specified in the db.tls.client section. The following is an example of the db.tls section:

	db:
	  ...
	  tls:
	      enabled: true
	      certfiles:
	        - db-server-cert.pem
	      client:
	            certfile: db-client-cert.pem
	            keyfile: db-client-key.pem

certfiles - A list of PEM-encoded trusted root certificate files.

certfile and keyfile - PEM-encoded certificate and key files that are used by the Fabric CA server to communicate securely with the PostgreSQL server

########PostgreSQL SSL Configuration########
#########Basic instructions for configuring SSL on the PostgreSQL server:#########
1. In postgresql.conf, uncomment SSL and set to “on” (SSL=on)
2. Place certificate and key files in the PostgreSQL data directory.

Instructions for generating self-signed certificates for: https://www.postgresql.org/docs/9.5/static/ssl-tcp.html

Note: Self-signed certificates are for testing purposes and should not be used in a production environment

########PostgreSQL Server - Require Client Certificates########
1. Place certificates of the certificate authorities (CAs) you trust in the file root.crt in the PostgreSQL data directory
2. In postgresql.conf, set “ssl_ca_file” to point to the root cert of the client (CA cert)
3. Set the clientcert parameter to 1 on the appropriate hostssl line(s) in pg_hba.conf.

For more details on configuring SSL on the PostgreSQL server, please refer to the following PostgreSQL documentation: https://www.postgresql.org/docs/9.4/static/libpq-ssl.html

########MySQL########
The following sample may be added to the Fabric CA server configuration file in order to connect to a MySQL database. Be sure to customize the various values appropriately. There are limitations on what characters are allowed in the database name. Please refer to the following MySQL documentation for more information: https://dev.mysql.com/doc/refman/5.7/en/identifiers.html

On MySQL 5.7.X, certain modes affect whether the server permits ‘0000-00-00’ as a valid date. It might be necessary to relax the modes that MySQL server uses. We want to allow the server to be able to accept zero date values.

In my.cnf, find the configuration option sql_mode and remove NO_ZERO_DATE if present. Restart MySQL server after making this change.

Please refer to the following MySQL documentation on different modes available and select the appropriate settings for the specific version of MySQL that is being used.

https://dev.mysql.com/doc/refman/5.7/en/sql-mode.html

	db:
	  type: mysql
	  datasource: root:rootpw@tcp(localhost:3306)/fabric_ca?parseTime=true&tls=custom

If connecting over TLS to the MySQL server, the db.tls.client section is also required as described in the PostgreSQL section above.

########MySQL SSL Configuration########
#########Basic instructions for configuring SSL on MySQL server:#########
1. Open or create my.cnf file for the server. Add or uncomment the lines below in the [mysqld] section. These should point to the key and certificates for the server, and the root CA cert.

	Instructions on creating server and client-side certficates: http://dev.mysql.com/doc/refman/5.7/en/creating-ssl-files-using-openssl.html

	[mysqld] ssl-ca=ca-cert.pem ssl-cert=server-cert.pem ssl-key=server-key.pem

	Can run the following query to confirm SSL has been enabled.

	mysql> SHOW GLOBAL VARIABLES LIKE ‘have_%ssl’;

	Should see:

		| Variable_name     | Value			|
	    | --------    		| -------		|
	    | have_openssl      | YES		    |
		| have_ssl      	| YES		    |
2. After the server-side SSL configuration is finished, the next step is to create a user who has a privilege to access the MySQL server over SSL. For that, log in to the MySQL server, and type:

	mysql> GRANT ALL PRIVILEGES ON . TO ‘ssluser’@’%’ IDENTIFIED BY ‘password’ REQUIRE SSL; mysql> FLUSH PRIVILEGES;

	If you want to give a specific IP address from which the user will access the server change the ‘%’ to the specific IP address.

#########MySQL Server - Require Client Certificates#########
Options for secure connections are similar to those used on the server side.

+ ssl-ca identifies the Certificate Authority (CA) certificate. This option, if used, must specify the same certificate used by the server.
+ ssl-cert identifies MySQL server’s certificate.
+ ssl-key identifies MySQL server’s private key.

Suppose that you want to connect using an account that has no special encryption requirements or was created using a GRANT statement that includes the REQUIRE SSL option. As a recommended set of secure-connection options, start the MySQL server with at least –ssl-cert and –ssl-key options. Then set the db.tls.certfiles property in the server configuration file and start the Fabric CA server.

To require that a client certificate also be specified, create the account using the REQUIRE X509 option. Then the client must also specify proper client key and certificate files; otherwise, the MySQL server will reject the connection. To specify client key and certificate files for the Fabric CA server, set the db.tls.client.certfile, and db.tls.client.keyfile configuration properties.

#######Configuring LDAP#######
The Fabric CA server can be configured to read from an LDAP server.

In particular, the Fabric CA server may connect to an LDAP server to do the following:

+ authenticate an identity prior to enrollment
+ retrieve an identity’s attribute values which are used for authorization.

Modify the LDAP section of the Fabric CA server’s configuration file to configure the server to connect to an LDAP server.

	ldap:
	   # Enables or disables the LDAP client (default: false)
	   enabled: false
	   # The URL of the LDAP server
	   url: <scheme>://<adminDN>:<adminPassword>@<host>:<port>/<base>
	   userfilter: <filter>
	   attribute:
	      # 'names' is an array of strings that identify the specific attributes
	      # which are requested from the LDAP server.
	      names: <LDAPAttrs>
	      # The 'converters' section is used to convert LDAP attribute values
	      # to fabric CA attribute values.
	      #
	      # For example, the following converts an LDAP 'uid' attribute
	      # whose value begins with 'revoker' to a fabric CA attribute
	      # named "hf.Revoker" with a value of "true" (because the expression
	      # evaluates to true).
	      #    converters:
	      #       - name: hf.Revoker
	      #         value: attr("uid") =~ "revoker*"
	      #
	      # As another example, assume a user has an LDAP attribute named
	      # 'member' which has multiple values of "dn1", "dn2", and "dn3".
	      # Further assume the following configuration.
	      #    converters:
	      #       - name: myAttr
	      #         value: map(attr("member"),"groups")
	      #    maps:
	      #       groups:
	      #          - name: dn1
	      #            value: orderer
	      #          - name: dn2
	      #            value: peer
	      # The value of the user's 'myAttr' attribute is then computed to be
	      # "orderer,peer,dn3".  This is because the value of 'attr("member")' is
	      # "dn1,dn2,dn3", and the call to 'map' with a 2nd argument of
	      # "group" replaces "dn1" with "orderer" and "dn2" with "peer".
	      converters:
	        - name: <fcaAttrName>
	          value: <fcaExpr>
	      maps:
	        <mapName>:
	            - name: <from>
	              value: <to>

Where:

+ scheme is one of ldap or ldaps;
+ adminDN is the distinquished name of the admin user;
+ pass is the password of the admin user;
+ host is the hostname or IP address of the LDAP server;
+ port is the optional port number, where default 389 for ldap and 636 for ldaps;
+ base is the optional root of the LDAP tree to use for searches;
+ filter is a filter to use when searching to convert a login user name to a distinguished name. For example, a value of (uid=%s) searches for LDAP entries with the value of a uid attribute whose value is the login user name. Similarly, (email=%s) may be used to login with an email address.
+ LDAPAttrs is an array of LDAP attribute names to request from the LDAP server on a user’s behalf;
+ the attribute.converters section is used to convert LDAP attributes to fabric CA attributes, where * fcaAttrName is the name of a fabric CA attribute; * fcaExpr is an expression whose evaluated value is assigned to the fabric CA attribute. For example, suppose that <LDAPAttrs> is [“uid”], <fcaAttrName> is ‘hf.Revoker’, and <fcaExpr> is ‘attr(“uid”) =~ “revoker*”’. This means that an attribute named “uid” is requested from the LDAP server on a user’s behalf. The user is then given a value of ‘true’ for the ‘hf.Revoker’ attribute if the value of the user’s ‘uid’ LDAP attribute begins with ‘revoker’; otherwise, the user is given a value of ‘false’ for the ‘hf.Revoker’ attribute.
+ the attribute.maps section is used to map LDAP response values. The typical use case is to map a distinguished name associated with an LDAP group to an identity type.

The LDAP expression language uses the govaluate package as described at https://github.com/Knetic/govaluate/blob/master/MANUAL.md. This defines operators such as “=~” and literals such as “revoker*”, which is a regular expression. The LDAP-specific variables and functions which extend the base govaluate language are as follows:

+ DN is a variable equal to the user’s distinguished name.
+ affiliation is a variable equal to the user’s affiliation.
+ attr is a function which takes 1 or 2 arguments. The 1st argument is an LDAP attribute name. The 2nd argument is a separator string which is used to join multiple values into a single string; the default separator string is ”,”. The attr function always returns a value of type ‘string’.
+ map is a function which takes 2 arguments. The 1st argument is any string. The second argument is the name of a map which is used to perform string substitution on the string from the 1st argument.
+ if is a function which takes a 3 arguments where the first argument must resolve to a boolean value. If it evaluates to true, the second argument is returned; otherwise, the third argument is returned.

For example, the following expression evaluates to true if the user has a distinguished name ending in “O=org1,C=US”, or if the user has an affiliation beginning with “org1.dept2.” and also has the “admin” attribute of “true”.

DN =~ “*O=org1,C=US” || (affiliation =~ “org1.dept2.*” && attr(‘admin’) = ‘true’)

NOTE: Since the attr function always returns a value of type ‘string’, numeric operators may not be used to construct expressions. For example, the following is NOT a valid expression:

	value: attr("gidNumber) >= 10000 && attr("gidNumber) < 10006

Alternatively, a regular expression enclosed in quotes as shown below may be used to return an equivalent result:

	value: attr("gidNumber") =~ "1000[0-5]$" || attr("mail") == "root@example.com"

The following is a sample configuration section for the default setting for the OpenLDAP server whose docker image is at https://github.com/osixia/docker-openldap.

	ldap:
	   enabled: true
	   url: ldap://cn=admin,dc=example,dc=org:admin@localhost:10389/dc=example,dc=org
	   userfilter: (uid=%s)

See FABRIC_CA/scripts/run-ldap-tests for a script which starts an OpenLDAP docker image, configures it, runs the LDAP tests in FABRIC_CA/cli/server/ldap/ldap_test.go, and stops the OpenLDAP server.

When LDAP is configured, enrollment works as follows:

+ The Fabric CA client or client SDK sends an enrollment request with a basic authorization header.
+ The Fabric CA server receives the enrollment request, decodes the identity name and password in the authorization header, looks up the DN (Distinguished Name) associated with the identity name using the “userfilter” from the configuration file, and then attempts an LDAP bind with the identity’s password. If the LDAP bind is successful, the enrollment processing is authorized and can proceed.

#######Setting up a cluster#######
You may use any IP sprayer to load balance to a cluster of Fabric CA servers. This section provides an example of how to set up Haproxy to route to a Fabric CA server cluster. Be sure to change hostname and port to reflect the settings of your Fabric CA servers.

haproxy.conf

	global
	      maxconn 4096
	      daemon
	
	defaults
	      mode http
	      maxconn 2000
	      timeout connect 5000
	      timeout client 50000
	      timeout server 50000
	
	listen http-in
	      bind *:7054
	      balance roundrobin
	      server server1 hostname1:port
	      server server2 hostname2:port
	      server server3 hostname3:port

Note: If using TLS, need to use mode tcp.

#######Setting up multiple CAs#######
The fabric-ca server by default consists of a single default CA. However, additional CAs can be added to a single server by using cafiles or cacount configuration options. Each additional CA will have its own home directory.

########cacount########
The cacount provides a quick way to start X number of default additional CAs. The home directory will be relative to the server directory. With this option, the directory structure will be as follows:

	--<Server Home>
	  |--ca
	    |--ca1
	    |--ca2

Each additional CA will get a default configuration file generated in it’s home directory, within the configuration file it will contain a unique CA name.

For example, the following command will start 2 default CA instances:

	fabric-ca-server start -b admin:adminpw --cacount 2

########cafiles########
If absolute paths are not provided when using the cafiles configuration option, the CA home directory will be relative to the server directory.

To use this option, CA configuration files must have already been generated and configured for each CA that is to be started. Each configuration file must have a unique CA name and Common Name (CN), otherwise the server will fail to start as these names must be unique. The CA configuration files will override any default CA configuration, and any missing options in the CA configuration files will be replaced by the values from the default CA.

The precedence order will be as follows:

1. CA Configuration file
2. Default CA CLI flags
3. Default CA Environment variables
4. Default CA Configuration file

A CA configuration file must contain at least the following:

	ca:
	# Name of this CA
	name: <CANAME>
	
	csr:
	  cn: <COMMONNAME>

You may configure your directory structure as follows:

	--<Server Home>
	  |--ca
	    |--ca1
	      |-- fabric-ca-config.yaml
	    |--ca2
	      |-- fabric-ca-config.yaml

For example, the following command will start two customized CA instances:

	fabric-ca-server start -b admin:adminpw --cafiles ca/ca1/fabric-ca-config.yaml
	--cafiles ca/ca2/fabric-ca-config.yaml

#####Enrolling an intermediate CA#####
In order to create a CA signing certificate for an intermediate CA, the intermediate CA must enroll with a parent CA in the same way that a fabric-ca-client enrolls with a CA. This is done by using the -u option to specify the URL of the parent CA and the enrollment ID and secret as shown below. The identity associated with this enrollment ID must have an attribute with a name of “hf.IntermediateCA” and a value of “true”. The CN (or Common Name) of the issued certificate will be set to the enrollment ID. An error will occur if an intermediate CA tries to explicitly specify a CN value.

	fabric-ca-server start -b admin:adminpw -u http://<enrollmentID>:<secret>@<parentserver>:<parentport>

For other intermediate CA flags see Fabric CA server’s configuration file format section.

#####Upgrading the server#####
The Fabric CA server must be upgraded before upgrading the Fabric CA client. Prior to upgrade, it is suggested that the current database be backed up:

+ If using sqlite3, backup the current database file (which is named fabric-ca-server.db by default).
+ For other database types, use the appropriate backup/replication mechanism.

To upgrade a single instance of Fabric CA server:

1. Stop the fabric-ca-server process.
2. Ensure the current database is backed up.
3. Replace previous fabric-ca-server binary with the upgraded version.
4. Launch the fabric-ca-server process.
5. Verify the fabric-ca-server process is available with the following command where <host> is the hostname on which the server was started:

		fabric-ca-client getcainfo -u http://<host>:7054

######Upgrading a cluster:######
To upgrade a cluster of fabric-ca-server instances using either a MySQL or Postgres database, perform the following procedure. We assume that you are using haproxy to load balance to two fabric-ca-server cluster members on host1 and host2, respectively, both listening on port 7054. After this procedure, you will be load balancing to upgraded fabric-ca-server cluster members on host3 and host4 respectively, both listening on port 7054.

In order to monitor the changes using haproxy stats, enable statistics collection. Add the following lines to the global section of the haproxy configuration file:

	stats socket /var/run/haproxy.sock mode 666 level operator
	stats timeout 2m

Restart haproxy to pick up the changes:

	# haproxy -f <configfile> -st $(pgrep haproxy)

To display summary information from the haproxy “show stat” command, the following function may prove useful for parsing the copious amount of CSV data returned:

	haProxyShowStats() {
	   echo "show stat" | nc -U /var/run/haproxy.sock |sed '1s/^# *//'|
	      awk -F',' -v fmt="%4s %12s %10s %6s %6s %4s %4s\n" '
	         { if (NR==1) for (i=1;i<=NF;i++) f[tolower($i)]=i }
	         { printf fmt, $f["sid"],$f["pxname"],$f["svname"],$f["status"],
	                       $f["weight"],$f["act"],$f["bck"] }'
	}

1. Initially your haproxy configuration file is similar to the following:

		server server1 host1:7054 check
		server server2 host2:7054 check

	Change this configuration to the following:

		server server1 host1:7054 check backup
		server server2 host2:7054 check backup
		server server3 host3:7054 check
		server server4 host4:7054 check
2. Restart the HA proxy with the new configuration as follows:

		haproxy -f <configfile> -st $(pgrep haproxy)
	
	"haProxyShowStats" will now reflect the modified configuration, with two active, older-version backup servers and two (yet to be started) upgraded servers:

		sid   pxname      svname  status  weig  act  bck
		  1   fabric-cas  server3   DOWN     1    1    0
		  2   fabric-cas  server4   DOWN     1    1    0
		  3   fabric-cas  server1     UP     1    0    1
		  4   fabric-cas  server2     UP     1    0    1

3. Install upgraded binaries of fabric-ca-server on host3 and host4. The new upgraded servers on host3 and host4 should be configured to use the same database as their older counterparts on host1 and host2. After starting the upgraded servers, the database will be automatically migrated. The haproxy will forward all new traffic to the upgraded servers, since they are not configured as backup servers. Verify using the "fabric-ca-client getcainfo" command that your cluster is still functioning appropriately before proceeding. Also, "haProxyShowStats" should now reflect that all servers are active, similar to the following:

		sid   pxname      svname  status  weig  act  bck
		  1   fabric-cas  server3    UP     1    1    0
		  2   fabric-cas  server4    UP     1    1    0
		  3   fabric-cas  server1    UP     1    0    1
		  4   fabric-cas  server2    UP     1    0    1

4. Stop the old servers on host1 and host2. Verify using the "fabric-ca-client getcainfo" command that your new cluster is still functioning appropriately before proceeding. Then remove the older server backup configuration from the haproxy configuration file, so that it looks similar to the following:

		server server3 host3:7054 check
		server server4 host4:7054 check

5. Restart the HA proxy with the new configuration as follows:

		haproxy -f <configfile> -st $(pgrep haproxy)

	"haProxyShowStats" will now reflect the modified configuration, with two active servers which have been upgraded to the new version:

		sid   pxname      svname  status  weig  act  bck
		  1   fabric-cas  server3   UP       1    1    0
		  2   fabric-cas  server4   UP       1    1    0

######Fabric CA Client######
This section describes how to use the fabric-ca-client command.

The Fabric CA client’s home directory is determined as follows:

+ if the –home command line option is set, use its value
+ otherwise, if the FABRIC_CA_CLIENT_HOME environment variable is set, use its value
+ otherwise, if the FABRIC_CA_HOME environment variable is set, use its value
+ otherwise, if the CA_CFG_PATH environment variable is set, use its value
+ otherwise, use $HOME/.fabric-ca-client

The instructions below assume that the client configuration file exists in the client’s home directory.

#######Enrolling the bootstrap identity#######
First, if needed, customize the CSR (Certificate Signing Request) section in the client configuration file. Note that csr.cn field must be set to the ID of the bootstrap identity. Default CSR values are shown below:

	csr:
	  cn: <<enrollment ID>>
	  key:
	    algo: ecdsa
	    size: 256
	  names:
	    - C: US
	      ST: North Carolina
	      L:
	      O: Hyperledger Fabric
	      OU: Fabric CA
	  hosts:
	   - <<hostname of the fabric-ca-client>>
	  ca:
	    pathlen:
	    pathlenzero:
	    expiry:

See CSR fields for description of the fields.

Then run fabric-ca-client enroll command to enroll the identity. For example, following command enrolls an identity whose ID is admin and password is adminpw by calling Fabric CA server that is running locally at 7054 port.

	export FABRIC_CA_CLIENT_HOME=$HOME/fabric-ca/clients/admin
	fabric-ca-client enroll -u http://admin:adminpw@localhost:7054

The enroll command stores an enrollment certificate (ECert), corresponding private key and CA certificate chain PEM files in the subdirectories of the Fabric CA client’s msp directory. You will see messages indicating where the PEM files are stored.

#######Registering a new identity#######
The identity performing the register request must be currently enrolled, and must also have the proper authority to register the type of the identity that is being registered.

In particular, three authorization checks are made by the Fabric CA server during registration as follows:

1. The registrar (i.e. the invoker) must have the “hf.Registrar.Roles” attribute with a comma-separated list of values where one of the values equals the type of identity being registered; for example, if the registrar has the “hf.Registrar.Roles” attribute with a value of “peer,app,user”, the registrar can register identities of type peer, app, and user, but not orderer.
2. The affiliation of the registrar must be equal to or a prefix of the affiliation of the identity being registered. For example, an registrar with an affiliation of “a.b” may register an identity with an affiliation of “a.b.c” but may not register an identity with an affiliation of “a.c”. If root affiliation is required for an identity, then the affiliation request should be a dot (”.”) and the registrar must also have root affiliation. If no affiliation is specified in the registration request, the identity being registered will be given the affiliation of the registrar.
3. The registrar can register a user with attributes if all of the following conditions are satisfied:
		+ Registrar can register Fabric CA reserved attributes that have the prefix ‘hf.’ only if the registrar possesses the attribute and it is part of the value of the hf.Registrar.Attributes’ attribute. Furthermore, if the attribute is of type list then the value of attribute being registered must be equal to or a subset of the value that the registrar has. If the attribute is of type boolean, the registrar can register the attribute only if the registrar’s value for the attribute is ‘true’.
		+ Registering custom attributes (i.e. any attribute whose name does not begin with ‘hf.’) requires that the registrar has the ‘hf.Registar.Attributes’ attribute with the value of the attribute or pattern being registered. The only supported pattern is a string with a “*” at the end. For example, “a.b.*” is a pattern which matches all attribute names beginning with “a.b.”. For example, if the registrar has hf.Registrar.Attributes=orgAdmin, then the only attribute which the registrar can add or remove from an identity is the ‘orgAdmin’ attribute.
		+ If the requested attribute name is ‘hf.Registrar.Attributes’, an additional check is performed to see if the requested values for this attribute are equal to or a subset of the registrar’s values for ‘hf.Registrar.Attributes’. For this to be true, each requested value must match a value in the registrar’s value for ‘hf.Registrar.Attributes’ attribute. For example, if the registrar’s value for ‘hf.Registrar.Attributes’ is ‘a.b.*, x.y.z’ and the requested attribute value is ‘a.b.c, x.y.z’, it is valid because ‘a.b.c’ matches ‘a.b.*’ and ‘x.y.z’ matches the registrar’s ‘x.y.z’ value.

#######Examples:#######
########Valid Scenarios:########
1. If the registrar has the attribute ‘hf.Registrar.Attributes = a.b.*, x.y.z’ and is registering attribute ‘a.b.c’, it is valid ‘a.b.c’ matches ‘a.b.*’.
2. If the registrar has the attribute ‘hf.Registrar.Attributes = a.b.*, x.y.z’ and is registering attribute ‘x.y.z’, it is valid because ‘x.y.z’ matches the registrar’s ‘x.y.z’ value.
3. If the registrar has the attribute ‘hf.Registrar.Attributes = a.b.*, x.y.z’ and the requested attribute value is ‘a.b.c, x.y.z’, it is valid because ‘a.b.c’ matches ‘a.b.*’ and ‘x.y.z’ matches the registrar’s ‘x.y.z’ value.
4. If the registrar has the attribute ‘hf.Registrar.Roles = peer,client’ and the requested attribute value is ‘peer’ or ‘peer,client’, it is valid because the requested value is equal to or a subset of the registrar’s value.

########Invalid Scenarios:########
1. If the registrar has the attribute ‘hf.Registrar.Attributes = a.b.*, x.y.z’ and is registering attribute ‘hf.Registar.Attributes = a.b.c, x.y.*’, it is invalid because requested attribute ‘x.y.*’ is not a pattern owned by the registrar. The value ‘x.y.*’ is a superset of ‘x.y.z’.
2. If the registrar has the attribute ‘hf.Registrar.Attributes = a.b.*, x.y.z’ and is registering attribute ‘hf.Registar.Attributes = a.b.c, x.y.z, attr1’, it is invalid because the registrar’s ‘hf.Registrar.Attributes’ attribute values do not contain ‘attr1’.
3. If the registrar has the attribute ‘hf.Registrar.Attributes = a.b.*, x.y.z’ and is registering attribute ‘a.b’, it is invalid because the value ‘a.b’ is not contained in ‘a.b.*’.
4. If the registrar has the attribute ‘hf.Registrar.Attributes = a.b.*, x.y.z’ and is registering attribute ‘x.y’, it is invalid because ‘x.y’ is not contained by ‘x.y.z’.
5. If the registrar has the attribute ‘hf.Registrar.Roles = peer,client’ and the requested attribute value is ‘peer,client,orderer’, it is invalid because the registrar does not have the orderer role in its value of hf.Registrar.Roles attribute.
6. If the registrar has the attribute ‘hf.Revoker = false’ and the requested attribute value is ‘true’, it is invalid because the hf.Revoker attribute is a boolean attribute and the registrar’s value for the attribute is not ‘true’.

The table below lists all the attributes that can be registered for an identity. The names of attributes are case sensitive.

	| Name        				| Type    		|   Description  |
    | --------   				| ----- 		| 	----		 |
    | hf.Registrar.Roles		| List      	|   List of roles that the registrar is allowed to manage|
    | hf.Registrar.DelegateRoles| List      	|   List of roles that the registrar is allowed to give to a registree for its ‘hf.Registrar.Roles’ attribute|
    | hf.Registrar.Attributes	| List      	|   List of attributes that registrar is allowed to register|
	| hf.GenCRL	        	    | Boolean      	|   Identity is able to generate CRL if attribute value is true|
	| hf.Revoker	        	| Boolean      	|   Identity is able to revoke a user and/or certificates if attribute value is true|
	| hf.AffiliationMgr	        | Boolean      	|   Identity is able to manage affiliations if attribute value is true|
	| hf.IntermediateCA	        | Boolean	   	|   Identity is able to enroll as an intermediate CA if attribute value is true|

Note: When registering an identity, you specify an array of attribute names and values. If the array specifies multiple array elements with the same name, only the last element is currently used. In other words, multi-valued attributes are not currently supported.

The following command uses the admin identity’s credentials to register a new user with an enrollment id of “admin2”, an affiliation of “org1.department1”, an attribute named “hf.Revoker” with a value of “true”, and an attribute named “admin” with a value of “true”. The ”:ecert” suffix means that by default the “admin” attribute and its value will be inserted into the user’s enrollment certificate, which can then be used to make access control decisions.

	export FABRIC_CA_CLIENT_HOME=$HOME/fabric-ca/clients/admin
	fabric-ca-client register --id.name admin2 --id.affiliation org1.department1 --id.attrs 'hf.Revoker=true,admin=true:ecert'

The password, also known as the enrollment secret, is printed. This password is required to enroll the identity. This allows an administrator to register an identity and give the enrollment ID and the secret to someone else to enroll the identity.

Multiple attributes can be specified as part of the –id.attrs flag, each attribute must be comma separated. For an attribute value that contains a comma, the attribute must be encapsulated in double quotes. See example below.

	fabric-ca-client register -d --id.name admin2 --id.affiliation org1.department1 --id.attrs '"hf.Registrar.Roles=peer,user",hf.Revoker=true'

or

	fabric-ca-client register -d --id.name admin2 --id.affiliation org1.department1 --id.attrs '"hf.Registrar.Roles=peer,user"' --id.attrs hf.Revoker=true

You may set default values for any of the fields used in the register command by editing the client’s configuration file. For example, suppose the configuration file contains the following:

	id:
	  name:
	  type: user
	  affiliation: org1.department1
	  maxenrollments: -1
	  attributes:
	    - name: hf.Revoker
	      value: true
	    - name: anotherAttrName
	      value: anotherAttrValue

The following command would then register a new identity with an enrollment id of “admin3” which it takes from the command line, and the remainder is taken from the configuration file including the identity type: “user”, affiliation: “org1.department1”, and two attributes: “hf.Revoker” and “anotherAttrName”.

	export FABRIC_CA_CLIENT_HOME=$HOME/fabric-ca/clients/admin
	fabric-ca-client register --id.name admin3

To register an identity with multiple attributes requires specifying all attribute names and values in the configuration file as shown above.

Setting maxenrollments to 0 or leaving it out from the configuration will result in the identity being registered to use the CA’s max enrollment value. Furthermore, the max enrollment value for an identity being registered cannot exceed the CA’s max enrollment value. For example, if the CA’s max enrollment value is 5. Any new identity must have a value less than or equal to 5, and also can’t set it to -1 (infinite enrollments).

Next, let’s register a peer identity which will be used to enroll the peer in the following section. The following command registers the peer1 identity. Note that we choose to specify our own password (or secret) rather than letting the server generate one for us.

	export FABRIC_CA_CLIENT_HOME=$HOME/fabric-ca/clients/admin
	fabric-ca-client register --id.name peer1 --id.type peer --id.affiliation org1.department1 --id.secret peer1pw

Note that affiliations are case sensitive except for the non-leaf affiliations that are specified in the server configuration file, which are always stored in lower case. For example, if the affiliations section of the server configuration file looks like this:

	affiliations:
	  BU1:
	    Department1:
	      - Team1
	  BU2:
	    - Department2
	    - Department3

BU1, Department1, BU2 are stored in lower case. This is because Fabric CA uses Viper to read configuration. Viper treats map keys as case insensitive and always returns lowercase value. To register an identity with Team1 affiliation, bu1.department1.Team1 would need to be specified to the –id.affiliation flag as shown below:

	export FABRIC_CA_CLIENT_HOME=$HOME/fabric-ca/clients/admin
	fabric-ca-client register --id.name client1 --id.type client --id.affiliation bu1.department1.Team1

#######Enrolling a peer identity#######
Now that you have successfully registered a peer identity, you may now enroll the peer given the enrollment ID and secret (i.e. the password from the previous section). This is similar to enrolling the bootstrap identity except that we also demonstrate how to use the “-M” option to populate the Hyperledger Fabric MSP (Membership Service Provider) directory structure.

The following command enrolls peer1. Be sure to replace the value of the “-M” option with the path to your peer’s MSP directory which is the ‘mspConfigPath’ setting in the peer’s core.yaml file. You may also set the FABRIC_CA_CLIENT_HOME to the home directory of your peer.

	export FABRIC_CA_CLIENT_HOME=$HOME/fabric-ca/clients/peer1
	fabric-ca-client enroll -u http://peer1:peer1pw@localhost:7054 -M $FABRIC_CA_CLIENT_HOME/msp

Enrolling an orderer is the same, except the path to the MSP directory is the ‘LocalMSPDir’ setting in your orderer’s orderer.yaml file.

All enrollment certificates issued by the fabric-ca-server have organizational units (or “OUs” for short) as follows:

1. The root of the OU hierarchy equals the identity type
2. An OU is added for each component of the identity’s affiliation

For example, if an identity is of type peer and its affiliation is department1.team1, the identity’s OU hierarchy (from leaf to root) is OU=team1, OU=department1, OU=peer.

#######Getting a CA certificate chain from another Fabric CA server#######
In general, the cacerts directory of the MSP directory must contain the certificate authority chains of other certificate authorities, representing all of the roots of trust for the peer.

The fabric-ca-client getcainfo command is used to retrieve these certificate chains from other Fabric CA server instances.

For example, the following will start a second Fabric CA server on localhost listening on port 7055 with a name of “CA2”. This represents a completely separate root of trust and would be managed by a different member on the blockchain.

	export FABRIC_CA_SERVER_HOME=$HOME/ca2
	fabric-ca-server start -b admin:ca2pw -p 7055 -n CA2

The following command will install CA2’s certificate chain into peer1’s MSP directory.

	export FABRIC_CA_CLIENT_HOME=$HOME/fabric-ca/clients/peer1
	fabric-ca-client getcainfo -u http://localhost:7055 -M $FABRIC_CA_CLIENT_HOME/msp

By default, the Fabric CA server returns the CA chain in child-first order. This means that each CA certificate in the chain is followed by its issuer’s CA certificate. If you need the Fabric CA server to return the CA chain in the opposite order, then set the environment variable CA_CHAIN_PARENT_FIRST to true and restart the Fabric CA server. The Fabric CA client will handle either order appropriately.

#######Reenrolling an Identity#######
Suppose your enrollment certificate is about to expire or has been compromised. You can issue the reenroll command to renew your enrollment certificate as follows.

	export FABRIC_CA_CLIENT_HOME=$HOME/fabric-ca/clients/peer1
	fabric-ca-client reenroll

#######Revoking a certificate or identity#######
An identity or a certificate can be revoked. Revoking an identity will revoke all the certificates owned by the identity and will also prevent the identity from getting any new certificates. Revoking a certificate will invalidate a single certificate.

In order to revoke a certificate or an identity, the calling identity must have the hf.Revoker and hf.Registrar.Roles attribute. The revoking identity can only revoke a certificate or an identity that has an affiliation that is equal to or prefixed by the revoking identity’s affiliation. Furthermore, the revoker can only revoke identities with types that are listed in the revoker’s hf.Registrar.Roles attribute.

For example, a revoker with affiliation orgs.org1 and ‘hf.Registrar.Roles=peer,client’ attribute can revoke either a peer or client type identity affiliated with orgs.org1 or orgs.org1.department1 but can’t revoke an identity affiliated with orgs.org2 or of any other type.

The following command disables an identity and revokes all of the certificates associated with the identity. All future requests received by the Fabric CA server from this identity will be rejected.

	fabric-ca-client revoke -e <enrollment_id> -r <reason>

The following are the supported reasons that can be specified using -r flag:

1. unspecified
2. keycompromise
3. cacompromise
4. affiliationchange
5. superseded
6. cessationofoperation
7. certificatehold
8. removefromcrl
9. privilegewithdrawn
10. aacompromise

For example, the bootstrap admin who is associated with root of the affiliation tree can revoke peer1‘s identity as follows:

	export FABRIC_CA_CLIENT_HOME=$HOME/fabric-ca/clients/admin
	fabric-ca-client revoke -e peer1

An enrollment certificate that belongs to an identity can be revoked by specifying its AKI (Authority Key Identifier) and serial number as follows:

	fabric-ca-client revoke -a xxx -s yyy -r <reason>

For example, you can get the AKI and the serial number of a certificate using the openssl command and pass them to the revoke command to revoke the said certificate as follows:

	serial=$(openssl x509 -in userecert.pem -serial -noout | cut -d "=" -f 2)
	aki=$(openssl x509 -in userecert.pem -text | awk '/keyid/ {gsub(/ *keyid:|:/,"",$1);print tolower($0)}')
	fabric-ca-client revoke -s $serial -a $aki -r affiliationchange

The –gencrl flag can be used to generate a CRL (Certificate Revocation List) that contains all the revoked certificates. For example, following command will revoke the identity peer1, generates a CRL and stores it in the <msp folder>/crls/crl.pem file.

	fabric-ca-client revoke -e peer1 --gencrl

A CRL can also be generated using the gencrl command. Refer to the Generating a CRL (Certificate Revocation List) section for more information on the gencrl command.

#######Generating a CRL (Certificate Revocation List)#######
After a certificate is revoked in the Fabric CA server, the appropriate MSPs in Hyperledger Fabric must also be updated. This includes both local MSPs of the peers as well as MSPs in the appropriate channel configuration blocks. To do this, PEM encoded CRL (certificate revocation list) file must be placed in the crls folder of the MSP. The fabric-ca-client gencrl command can be used to generate a CRL. Any identity with hf.GenCRL attribute can create a CRL that contains serial numbers of all certificates that were revoked during a certain period. The created CRL is stored in the <msp folder>/crls/crl.pem file.

The following command will create a CRL containing all the revoked certficates (expired and unexpired) and store the CRL in the ~/msp/crls/crl.pem file.

	export FABRIC_CA_CLIENT_HOME=~/clientconfig
	fabric-ca-client gencrl -M ~/msp

The next command will create a CRL containing all certificates (expired and unexpired) that were revoked after 2017-09-13T16:39:57-08:00 (specified by the –revokedafter flag) and before 2017-09-21T16:39:57-08:00 (specified by the –revokedbefore flag) and store the CRL in the ~/msp/crls/crl.pem file.

	export FABRIC_CA_CLIENT_HOME=~/clientconfig
	fabric-ca-client gencrl --caname "" --revokedafter 2017-09-13T16:39:57-08:00 --revokedbefore 2017-09-21T16:39:57-08:00 -M ~/msp

The –caname flag specifies the name of the CA to which this request is sent. In this example, the gencrl request is sent to the default CA.

The –revokedafter and –revokedbefore flags specify the lower and upper boundaries of a time period. The generated CRL will contain certificates that were revoked in this time period. The values must be UTC timestamps specified in RFC3339 format. The –revokedafter timestamp cannot be greater than the –revokedbefore timestamp.

By default, ‘Next Update’ date of the CRL is set to next day. The crl.expiry CA configuration property can be used to specify a custom value.

The gencrl command will also accept –expireafter and –expirebefore flags that can be used to generate a CRL with revoked certificates that expire during the period specified by these flags. For example, the following command will generate a CRL that contains certificates that were revoked after 2017-09-13T16:39:57-08:00 and before 2017-09-21T16:39:57-08:00, and that expire after 2017-09-13T16:39:57-08:00 and before 2018-09-13T16:39:57-08:00

	export FABRIC_CA_CLIENT_HOME=~/clientconfig
	fabric-ca-client gencrl --caname "" --expireafter 2017-09-13T16:39:57-08:00 --expirebefore 2018-09-13T16:39:57-08:00  --revokedafter 2017-09-13T16:39:57-08:00 --revokedbefore 2017-09-21T16:39:57-08:00 -M ~/msp

The fabric-samples/fabric-ca sample demonstrates how to generate a CRL that contains certificate of a revoked user and update the channel msp. It will then demonstrate that querying the channel using the revoked user credentials will result in an authorization error.

#######Enabling TLS#######
This section describes in more detail how to configure TLS for a Fabric CA client.

The following sections may be configured in the fabric-ca-client-config.yaml.

	tls:
	  # Enable TLS (default: false)
	  enabled: true
	  certfiles:
	    - root.pem
	  client:
	    certfile: tls_client-cert.pem
	    keyfile: tls_client-key.pem

The certfiles option is the set of root certificates trusted by the client. This will typically just be the root Fabric CA server’s certificate found in the server’s home directory in the ca-cert.pem file.

The client option is required only if mutual TLS is configured on the server.

#######Attribute-Based Access Control#######
Access control decisions can be made by chaincode (and by the Hyperledger Fabric runtime) based upon an identity’s attributes. This is called Attribute-Based Access Control, or ABAC for short.

In order to make this possible, an identity’s enrollment certificate (ECert) may contain one or more attribute name and value. The chaincode then extracts an attribute’s value to make an access control decision.

For example, suppose that you are developing application app1 and want a particular chaincode operation to be accessible only by app1 administrators. Your chaincode could verify that the caller’s certificate (which was issued by a CA trusted for the channel) contains an attribute named app1Admin with a value of true. Of course the name of the attribute can be anything and the value need not be a boolean value.

So how do you get an enrollment certificate with an attribute? There are two methods:

1. When you register an identity, you can specify that an enrollment certificate issued for the identity should by default contain an attribute. This behavior can be overridden at enrollment time, but this is useful for establishing default behavior and, assuming registration occurs outside of your application, does not require any application change.

	The following shows how to register user1 with two attributes: app1Admin and email. The ”:ecert” suffix causes the appAdmin attribute to be inserted into user1’s enrollment certificate by default, when the user does not explicitly request attributes at enrollment time. The email attribute is not added to the enrollment certificate by default.

		fabric-ca-client register --id.name user1 --id.secret user1pw --id.type user --id.affiliation org1 --id.attrs 'app1Admin=true:ecert,email=user1@gmail.com'

2. When you enroll an identity, you may explicitly request that one or more attributes be added to the certificate. For each attribute requested, you may specify whether the attribute is optional or not. If it is not requested optionally and the identity does not possess the attribute, an error will occur.

	The following shows how to enroll user1 with the email attribute, without the app1Admin attribute, and optionally with the phone attribute (if the user possesses the phone attribute).

		fabric-ca-client enroll -u http://user1:user1pw@localhost:7054 --enrollment.attrs "email,phone:opt"

The table below shows the three attributes which are automatically registered for every identity.

	| Attribute Name	| Attribute Value  					|
    | --------   		| -------          					|
    | hf.EnrollmentID	| The enrollment ID of the identity	|
    | hf.Type			| The type of the identity			|
	| hf.Affiliation	| The affiliation of the identity	|

To add any of the above attributes by default to a certificate, you must explicitly register the attribute with the ”:ecert” specification. For example, the following registers identity ‘user1’ so that the ‘hf.Affiliation’ attribute will be added to an enrollment certificate if no specific attributes are requested at enrollment time. Note that the value of the affiliation (which is ‘org1’) must be the same in both the ‘–id.affiliation’ and the ‘–id.attrs’ flags.

	fabric-ca-client register --id.name user1 --id.secret user1pw --id.type user --id.affiliation org1 --id.attrs 'hf.Affiliation=org1:ecert'

For information on the chaincode library API for Attribute-Based Access Control, see https://github.com/hyperledger/fabric/tree/release-1.1/core/chaincode/lib/cid/README.md

For an end-to-end sample which demonstrates Attribute-Based Access Control and more, see https://github.com/hyperledger/fabric-samples/tree/release-1.1/fabric-ca/README.md

#######Dynamic Server Configuration Update#######
This section describes how to use fabric-ca-client to dynamically update portions of the fabric-ca-server’s configuration without restarting the server.

All commands in this section require that you first be enrolled by executing the fabric-ca-client enroll command.

########Dynamically updating identities########
This section describes how to use fabric-ca-client to dynamically update identities.

An authorization failure will occur if the client identity does not satisfy all of the following:

+ The client identity must possess the “hf.Registrar.Roles” attribute with a comma-separated list of values where one of the values equals the type of identity being updated; for example, if the client’s identity has the “hf.Registrar.Roles” attribute with a value of “client,peer”, the client can update identities of type ‘client’ and ‘peer’, but not ‘orderer’.
+ The affiliation of the client’s identity must be equal to or a prefix of the affiliation of the identity being updated. For example, a client with an affiliation of “a.b” may update an identity with an affiliation of “a.b.c” but may not update an identity with an affiliation of “a.c”. If root affiliation is required for an identity, then the update request should specify a dot (”.”) for the affiliation and the client must also have root affiliation.

The following shows how to add, modify, and remove an affiliation.

########Getting Identity Information########
A caller may retrieve information on a identity from the fabric-ca server as long as the caller meets the authorization requirements highlighted in the section above. The following command shows how to get an identity.

	fabric-ca-client identity list --id user1

A caller may also request to retrieve information on all identities that it is authorized to see by issuing the following command.

	fabric-ca-client identity list

########Adding an identity########
The following adds a new identity for ‘user1’. Adding a new identity performs the same action as registering an identity via the ‘fabric-ca-client register’ command. There are two available methods for adding a new identity. The first method is via the –json flag where you describe the identity in a JSON string.

	fabric-ca-client identity add user1 --json '{"secret": "user1pw", "type": "user", "affiliation": "org1", "max_enrollments": 1, "attrs": [{"name": "hf.Revoker", "value": "true"}]}'

The following adds a user with root affiliation. Note that an affiliation name of ”.” means the root affiliation.

	fabric-ca-client identity add user1 --json '{"secret": "user1pw", "type": "user", "affiliation": ".", "max_enrollments": 1, "attrs": [{"name": "hf.Revoker", "value": "true"}]}'

The second method for adding an identity is to use direct flags. See the example below for adding ‘user1’.

	fabric-ca-client identity add user1 --secret user1pw --type user --affiliation . --maxenrollments 1 --attrs hf.Revoker=true

The table below lists all the fields of an identity and whether they are required or optional, and any default values they might have.

	| Fields		| Required   | Default Value 		|
    | --------  	| -------    | -------    	 		|
    | ID			| Yes  		 |						|
    | Secret		| No    	 |						|
	| Affiliation	| No		 | Caller’s Affiliation	|
	| Type			| No		 | client				|
	| Maxenrollments| No		 | 0					|
	| Attributes	| No		 |						|

########Modifying an identity########
There are two available methods for modifying an existing identity. The first method is via the –json flag where you describe the modifications in to an identity in a JSON string. Multiple modifications can be made in a single request. Any element of an identity that is not modified will retain its original value.

NOTE: A maxenrollments value of “-2” specifies that the CA’s max enrollment setting is to be used.

The command below make multiple modification to an identity using the –json flag.

	fabric-ca-client identity modify user1 --json '{"secret": "newPassword", "affiliation": ".", "attrs": [{"name": "hf.Regisrar.Roles", "value": "peer,client"},{"name": "hf.Revoker", "value": "true"}]}'

The commands below make modifications using direct flags. The following updates the enrollment secret (or password) for identity ‘user1’ to ‘newsecret’.

	fabric-ca-client identity modify user1 --secret newsecret

The following updates the affiliation of identity ‘user1’ to ‘org2’.

	fabric-ca-client identity modify user1 --affiliation org2

The following updates the type of identity ‘user1’ to ‘peer’.

	fabric-ca-client identity modify user1 --type peer

The following updates the maxenrollments of identity ‘user1’ to 5.

	fabric-ca-client identity modify user1 --maxenrollments 5

By specifying a maxenrollments value of ‘-2’, the following causes identity ‘user1’ to use the CA’s max enrollment setting.

	fabric-ca-client identity modify user1 --maxenrollments -2

The following sets the value of the ‘hf.Revoker’ attribute for identity ‘user1’ to ‘false’. If the identity has other attributes, they are not changed. If the identity did not previously possess the ‘hf.Revoker’ attribute, the attribute is added to the identity. An attribute may also be removed by specifying no value for the attribute.

	fabric-ca-client identity modify user1 --attrs hf.Revoker=false

The following removes the ‘hf.Revoker’ attribute for user ‘user1’.

	fabric-ca-client identity modify user1 --attrs hf.Revoker=

The following demonstrates that multiple options may be used in a single fabric-ca-client identity modify command. In this case, both the secret and the type are updated for user ‘user1’.

	fabric-ca-client identity modify user1 --secret newpass --type peer

########Removing an identity########
The following removes identity ‘user1’ and also revokes any certificates associated with the ‘user1’ identity.

	fabric-ca-client identity remove user1

Note: Removal of identities is disabled in the fabric-ca-server by default, but may be enabled by starting the fabric-ca-server with the –cfg.identities.allowremove option.

########Dynamically updating affiliations########
This section describes how to use fabric-ca-client to dynamically update affiliations. The following shows how to add, modify, remove, and list an affiliation.

########Adding an affiliation########
An authorization failure will occur if the client identity does not satisfy all of the following:

+ The client identity must possess the attribute ‘hf.AffiliationMgr’ with a value of ‘true’.
+ The affiliation of the client identity must be hierarchically above the affiliation being updated. For example, if the client’s affiliation is “a.b”, the client may add affiliation “a.b.c” but not “a” or “a.b”.

The following adds a new affiliation named ‘org1.dept1’.

	fabric-ca-client affiliation add org1.dept1

########Modifying an affiliation########
An authorization failure will occur if the client identity does not satisfy all of the following:

+ The client identity must possess the attribute ‘hf.AffiliationMgr’ with a value of ‘true’.
+ The affiliation of the client identity must be hierarchically above the affiliation being updated. For example, if the client’s affiliation is “a.b”, the client may add affiliation “a.b.c” but not “a” or “a.b”.
+ If the ‘–force’ option is true and there are identities which must be modified, the client identity must also be authorized to modify the identity.

The following renames the ‘org2’ affiliation to ‘org3’. It also renames any sub affiliations (e.g. ‘org2.department1’ is renamed to ‘org3.department1’).

	fabric-ca-client affiliation modify org2 --name org3

If there are identities that are affected by the renaming of an affiliation, it will result in an error unless the ‘–force’ option is used. Using the ‘–force’ option will update the affiliation of identities that are affected to use the new affiliation name.

	fabric-ca-client affiliation modify org1 --name org2 --force

########Removing an affiliation########
An authorization failure will occur if the client identity does not satisfy all of the following:

+ The client identity must possess the attribute ‘hf.AffiliationMgr’ with a value of ‘true’.
+ The affiliation of the client identity must be hierarchically above the affiliation being updated. For example, if the client’s affiliation is “a.b”, the client may remove affiliation “a.b.c” but not “a” or “a.b”.
+ If the ‘–force’ option is true and there are identities which must be modified, the client identity must also be authorized to modify the identity.

The following removes affiliation ‘org2’ and also any sub affiliations. For example, if ‘org2.dept1’ is an affiliation below ‘org2’, it is also removed.

	fabric-ca-client affiliation remove org2

If there are identities that are affected by the removing of an affiliation, it will result in an error unless the ‘–force’ option is used. Using the ‘–force’ option will also remove all identities that are associated with that affiliation, and the certificates associated with any of these identities.

Note: Removal of affiliations is disabled in the fabric-ca-server by default, but may be enabled by starting the fabric-ca-server with the –cfg.affiliations.allowremove option.

########Listing affiliation information########
An authorization failure will occur if the client identity does not satisfy all of the following:

+ The client identity must possess the attribute ‘hf.AffiliationMgr’ with a value of ‘true’.
+ Affiliation of the client identity must be equal to or be hierarchically above the affiliation being updated. For example, if the client’s affiliation is “a.b”, the client may get affiliation information on “a.b” or “a.b.c” but not “a” or “a.c”.

The following command shows how to get a specific affiliation.

	fabric-ca-client affiliation list --affiliation org2.dept1

A caller may also request to retrieve information on all affiliations that it is authorized to see by issuing the following command.

	fabric-ca-client affiliation list

#######Manage Certificates#######
This section describes how to use fabric-ca-client to manage certificates.

########Listing certificate information########
The certificates that are visible to a caller include:

+ Those certificates which belong to the caller
+ If the caller possesses the hf.Registrar.Roles attribute or the hf.Revoker attribute with a value of true, all certificates which belong to identities in and below the caller’s affiliation. For example, if the client’s affiliation is a.b, the client may get certificates for identities who’s affiliation is a.b or a.b.c but not a or a.c.

If executing a list command that requests certificates of more than one identity, only certificates of identities with an affiliation that is equal to or hierarchically below the caller’s affiliation will be listed.

The certificates which will be listed may be filtered based on ID, AKI, serial number, expiration time, revocation time, notrevoked, and notexpired flags.

+ id: List certificates for this enrollment ID
+ serial: List certificates that have this serial number
+ aki: List certificates that have this AKI
+ expiration: List certificates that have expiration dates that fall within this expiration time
+ revocation: List certificates that were revoked within this revocation time
+ notrevoked: List certificates that have not yet been revoked
+ notexpired: List certificates that have not yet expired

You can use flags notexpired and notrevoked as filters to exclude revoked certificates and/or expired certificates from the result set. For example, if you only care about certificates that have expired but have not been revoked you can use the expiration and notrevoked flags to get back such results. An example of this case is provided below.

Time should be specified based on RFC3339. For instance, to list certificates that have expirations between March 1, 2018 at 1:00 PM and June 15, 2018 at 2:00 AM, the input time string would look like 2018-03-01T13:00:00z and 2018-06-15T02:00:00z. If time is not a concern, and only the dates matter, then the time part can be left off and then the strings become 2018-03-01 and 2018-06-15.

The string now may be used to denote the current time and the empty string to denote any time. For example, now:: denotes a time range from now to any time in the future, and ::now denotes a time range from any time in the past until now.

The following command shows how to list certificates using various filters.

List all certificates:

	fabric-ca-client certificate list

List all certificates by id:

	fabric-ca-client certificate list --id admin

List certificate by serial and aki:

	fabric-ca-client certificate list --serial 1234 --aki 1234

List certificate by id and serial/aki:

	fabric-ca-client certificate list --id admin --serial 1234 --aki 1234

List certificates that are neither revoker nor expired by id:

	fabric-ca-client certificate list --id admin --notrevoked --notexpired

List all certificates that have not been revoked for an id (admin):

	fabric-ca-client certificate list --id admin --notrevoked

List all certificates have not expired for an id (admin):

The “–notexpired” flag is equivalent to “–expiration now::”, which means certificates will expire some time in the future.

	fabric-ca-client certificate list --id admin --notexpired

List all certificates that were revoked between a time range for an id (admin):

	fabric-ca-client certificate list --id admin --revocation 2018-01-01T01:30:00z::2018-01-30T05:00:00z

List all certificates that were revoked between a time range but have not expired for an id (admin):

	fabric-ca-client certificate list --id admin --revocation 2018-01-01::2018-01-30 --notexpired

List all revoked certificates using duration (revoked between 30 days and 15 days ago) for an id (admin):

	fabric-ca-client certificate list --id admin --revocation -30d::-15d

List all revoked certificates before a time

	fabric-ca-client certificate list --revocation ::2018-01-30

List all revoked certificates after a time

	fabric-ca-client certificate list --revocation 2018-01-30::

List all revoked certificates before now and after a certain date

	fabric-ca-client certificate list --id admin --revocation 2018-01-30::now

List all certificate that expired between a time range but have not been revoked for an id (admin):

	fabric-ca-client certificate list --id admin --expiration 2018-01-01::2018-01-30 --notrevoked

List all expired certificates using duration (expired between 30 days and 15 days ago) for an id (admin):

	fabric-ca-client certificate list --expiration -30d::-15d

List all certificates that have expired or will expire before a certain time

	fabric-ca-client certificate list --expiration ::2058-01-30

List all certificates that have expired or will expire after a certain time

	fabric-ca-client certificate list --expiration 2018-01-30::

List all expired certificates before now and after a certain date

	fabric-ca-client certificate list --expiration 2018-01-30::now

List certificates expiring in the next 10 days:

	fabric-ca-client certificate list --id admin --expiration ::+10d --notrevoked

The list certificate command can also be used to store certificates on the file system. This is a convenient way to populate the admins folder in an MSP, The “-store” flag points to the location on the file system to store the certificates.

Configure an identity to be an admin, by storing certificates for an identity in the MSP:

	export FABRIC_CA_CLIENT_HOME=/tmp/clientHome
	fabric-ca-client certificate list --id admin --store msp/admincerts

########Contact specific CA instance########
When a server is running multiple CA instances, requests can be directed to a specific CA. By default, if no CA name is specified in the client request the request will be directed to the default CA on the fabric-ca server. A CA name can be specified on the command line of a client command using the caname filter as follows:

	fabric-ca-client enroll -u http://admin:adminpw@localhost:7054 --caname <caname>

######HSM######
By default, the Fabric CA server and client store private keys in a PEM-encoded file, but they can also be configured to store private keys in an HSM (Hardware Security Module) via PKCS11 APIs. This behavior is configured in the BCCSP (BlockChain Crypto Service Provider) section of the server’s or client’s configuration file.

######Configuring Fabric CA server to use softhsm2######
This section shows how to configure the Fabric CA server or client to use a software version of PKCS11 called softhsm (see https://github.com/opendnssec/SoftHSMv2).

After installing softhsm, create a token, label it “ForFabric”, set the pin to ‘98765432’ (refer to softhsm documentation).

You can use both the config file and environment variables to configure BCCSP For example, set the bccsp section of Fabric CA server configuration file as follows. Note that the default field’s value is PKCS11.

	#############################################################################
	# BCCSP (BlockChain Crypto Service Provider) section is used to select which
	# crypto library implementation to use
	#############################################################################
	bccsp:
	  default: PKCS11
	  pkcs11:
	    Library: /usr/local/Cellar/softhsm/2.1.0/lib/softhsm/libsofthsm2.so
	    Pin: 98765432
	    Label: ForFabric
	    hash: SHA2
	    security: 256
	    filekeystore:
	      # The directory used for the software file-based keystore
	      keystore: msp/keystore

And you can override relevant fields via environment variables as follows:

	FABRIC_CA_SERVER_BCCSP_DEFAULT=PKCS11 FABRIC_CA_SERVER_BCCSP_PKCS11_LIBRARY=/usr/local/Cellar/softhsm/2.1.0/lib/softhsm/libsofthsm2.so FABRIC_CA_SERVER_BCCSP_PKCS11_PIN=98765432 FABRIC_CA_SERVER_BCCSP_PKCS11_LABEL=ForFabric

######File Formats######
#######Fabric CA server’s configuration file format#######
A default configuration file is created in the server’s home directory (see Fabric CA Server section for more info). The following link shows a sample Server configuration file.

#######Fabric CA client’s configuration file format#######
A default configuration file is created in the client’s home directory (see Fabric CA Client section for more info). The following link shows a sample Client configuration file.

######Troubleshooting######
1. If you see a Killed: 9 error on OSX when trying to execute fabric-ca-client or fabric-ca-server, there is a long thread describing this problem at https://github.com/golang/go/issues/19734. The short answer is that to work around this issue, you can run the following command:

	# sudo ln -s /usr/bin/true /usr/local/bin/dsymutil
2. The error [ERROR] No certificates found for provided serial and aki will occur if the following sequence of events occurs:

	a. You issue a fabric-ca-client enroll command, creating an enrollment certificate (i.e. an ECert). This stores a copy of the ECert in the fabric-ca-server’s database.
	b. The fabric-ca-server’s database is deleted and recreated, thus losing the ECert from step ‘a’. For example, this may happen if you stop and restart a docker container hosting the fabric-ca-server, but your fabric-ca-server is using the default sqlite database and the database file is not stored on a volume and is therefore not persistent.
	c. You issue a fabric-ca-client register command or any other command which tries to use the ECert from step ‘a’. In this case, since the database no longer contains the ECert, the [ERROR] No certificates found for provided serial and aki will occur.

To resolve this error, you must enroll again by repeating step ‘a’. This will issue a new ECert which will be stored in the current database.

3. When sending multiple parallel requests to a Fabric CA Server cluster that uses shared sqlite3 databases, the server occasionally returns a ‘database locked’ error. This is most probably because the database transaction timed out while waiting for database lock (held by another cluster member) to be released. This is an invalid configuration because sqlite is an embedded database, which means the Fabric CA server cluster must share the same file via a shared file system, which introduces a SPoF (single point of failure), which contradicts the purpose of cluster topology. The best practice is to use either Postgres or MySQL databases in a cluster topology.
4. Suppose an error similar to Failed to deserialize creator identity, err The supplied identity is not valid, Verify() returned x509: certificate signed by unknown authority is returned by a peer or orderer when using an enrollment certificate issued by the Fabric CA Server. This indicates that the signing CA certificate used by the Fabric CA Server to issue certificates does not match a certificate in the cacerts or intermediatecerts folder of the MSP used to make authorization checks.

The MSP which is used to make authorization checks depends on which operation you were performing when the error occurred. For example, if you were trying to install chaincode on a peer, the local MSP on the file system of the peer is used; otherwise, if you were performing some channel specific operation such as instantiating chaincode on a specific channel, the MSP in the genesis block or the most recent configuration block of the channel is used.

To confirm that this is the problem, compare the AKI (Authority Key Identifier) of the enrollment certificate to the SKI (Subject Key Identifier) of the certificate(s) in the cacerts and intermediatecerts folder of appropriate MSP. The command openssl x509 -in <PEM-file> -noout -text | grep -A1 “Authority Key Identifier” will display the AKI and openssl x509 -in <PEM-file> -noout -text | grep -A1 “Subject Key Identifier” will display the SKI. If they are not equal, you have confirmed that this is the cause of the error.

This can happen for multiple reasons including:

a. You used cryptogen to generate your key material but did not start fabric-ca-server with the signing key and certificate generated by cryptogen.

	To resolve (assuming FABRIC_CA_SERVER_HOME is set to the home directory of your fabric-ca-server):
	1. Stop fabric-ca-server.
	2. Copy crypto-config/peerOrganizations/<orgName>/ca/*pem to $FABRIC_CA_SERVER_HOME/ca-cert.pem.
	3. Copy crypto-config/peerOrganizations/<orgName>/ca/*_sk to $FABRIC_CA_SERVER_HOME/msp/keystore/.
	4. Start fabric-ca-server.
	5. Delete any previously issued enrollment certificates and get new certificates by enrolling again.

b. You deleted and recreated the CA signing key and certificate used by the Fabric CA Server after generating the genesis block. This can happen if the Fabric CA Server is running in a docker container, the container was restarted, and its home directory is not on a volume mount. In this case, the Fabric CA Server will create a new CA signing key and certificate.

	Assuming that you can not recover the original CA signing key, the only way to recover from this scenario is to update the certificate in the cacerts (or intermediatecerts) of the appropriate MSPs to the new CA certificate.


####Hyperledger Fabric SDKs####
Hyperledger Fabric intends to offer a number of SDKs for a wide variety of programming languages. The first two delivered are the Node.js and Java SDKs. We hope to provide Python, REST and Go SDKs in a subsequent release.

#####Hyperledger Fabric Node SDK documentation.#####
The Hyperledger Fabric SDK for Node.js provides a powerful API to interact with a Hyperledger Fabric v1.0 blockchain. The SDK is designed to be used in the Node.js JavaScript runtime.

######Overview######
Hyperledger Fabric is the operating system of an enterprise-strength permissioned blockchain network. For a high-level overview of the fabric, visit http://hyperledger-fabric.readthedocs.io/en/latest/.

Applications can be developed to interact with the blockchain network on behalf of the users. APIs are available to:

+ create channels
+ ask peer nodes to join the channel
+ install chaincodes in peers
+ instantiate chaincodes in a channel
+ invoke transactions by calling the chaincode
+ query the ledger for transactions or blocks

######How Different Components of the Fabric Work Together######
The Transaction Flow document provides an excellent description of the application/SDK, peers, and orderers working together to process transactions and producing blocks.

Security on the Fabric is enforced with digital signatures. All requests made to the fabric must be signed by users with appropriate enrollment certificates. For a user's enrollment certificate to be considered valid on the Fabric, it must be signed by a trusted Certificate Authority (CA). Fabric supports any standard CAs. In addition, Fabric provides a CA server. See this overview.

######Features of the SDK for Node.js######
The Hyperledger Fabric SDK for Node.js is designed in an Object-Oriented programming style. Its modular construction enables application developers to plug in alternative implementations of key functions such as crypto suites, the state persistence store, and logging utility.

The SDK's list of features include:

+ fabric-client:

	1. create a new channel
	2. send channel information to a peer to join
	3. install chaincode on a peer
	4. instantiate chaincode in a channel, which involves two steps: propose and transact
	5. submitting a transaction, which also involves two steps: propose and transact
	6. query a chaincode for the latest application state
	7. various query capabilities:

		1. channel height
		2. block-by-number, block-by-hash
		3. all channels that a peer is part of
		4. all installed chaincodes in a peer
		5. all instantiated chaincodes in a channel
		6. transaction-by-id
		7. channel configuration data

	8. monitoring events:

		1. connect to a peer's event stream
		2. listen on block events
		3. listen on transactions events and find out if the transaction was successfully committed to the ledger or marked invalid
		4. listen on custom events produced by chaincodes

	9. serializable User object with signing capabilities
	10. hierarchical configuration settings with multiple layers of overrides: files, environment variable, program arguments, in-memory settings
	11. logging utility with a built-in logger (winston) and can be overriden with a number of popular loggers including log4js and bunyan
	12. pluggable CryptoSuite interface describe the cryptographic operations required for successful interactions with the Fabric. Two implementations are provided out of box:
	
		1. Software-based ECDSA
		2. PKCS#11-compliant ECDSA

	13. pluggable State Store interface for persisting state caches such as users
		1. File-based store
		2. CouchDB-base store which works with both CouchDB database and IBM Cloudant
	14. customizable Crypto Key Store for any software-based cryptographic suite implementation
	15. supports both TLS (grpcs://) or non-TLS (grpc://) connections to peers and orderers, see Remote which is the superclass for peers and orderers
+ fabric-ca-client:
	1. register a new user
	2. enroll a user to obtain the enrollment certificate signed by the Fabric CA
	3. revoke an existing user by enrollment ID or revoke a specific certificate
	4. customizable persistence store

######API Reference######
The SDK is made up of 3 top-level modules that can be accessed through the navigation menu Modules:

+ api: pluggable APIs for application developers to supply alternative implementations of key interfaces used by the SDK. For each interface there are built-in default implementations.
+ fabric-client: this module provides APIs to interact with the core components of a Hypreledger Fabric-based blockchain network, namely the peers, orderers and event streams.
+ fabric-ca-client: this module provides APIs to interact with the optional component, fabric-ca, that contains services for membership management. Creative Commons License

This work is licensed under a Creative Commons Attribution 4.0 International License.

#####Hyperledger Fabric Java SDK documentation.#####
https://github.com/hyperledger/fabric-sdk-java


####Channels####
A Hyperledger Fabric channel is a private “subnet” of communication between two or more specific network members, for the purpose of conducting private and confidential transactions. A channel is defined by members (organizations), anchor peers per member, the shared ledger, chaincode application(s) and the ordering service node(s). Each transaction on the network is executed on a channel, where each party must be authenticated and authorized to transact on that channel. Each peer that joins a channel, has its own identity given by a membership services provider (MSP), which authenticates each peer to its channel peers and services.

To create a new channel, the client SDK calls configuration system chaincode and references properties such as anchor peer**s, and members (organizations). This request creates a **genesis block for the channel ledger, which stores configuration information about the channel policies, members and anchor peers. When adding a new member to an existing channel, either this genesis block, or if applicable, a more recent reconfiguration block, is shared with the new member.

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		See the Channel Configuration (configtx) section for more more details on the properties and proto structures of config transactions.
		</td>
	</tr>
</table>

The election of a leading peer for each member on a channel determines which peer communicates with the ordering service on behalf of the member. If no leader is identified, an algorithm can be used to identify the leader. The consensus service orders transactions and delivers them, in a block, to each leading peer, which then distributes the block to its member peers, and across the channel, using the gossip protocol.

Although any one anchor peer can belong to multiple channels, and therefore maintain multiple ledgers, no ledger data can pass from one channel to another. This separation of ledgers, by channel, is defined and implemented by configuration chaincode, the identity membership service and the gossip data dissemination protocol. The dissemination of data, which includes information on transactions, ledger state and channel membership, is restricted to peers with verifiable membership on the channel. This isolation of peers and ledger data, by channel, allows network members that require private and confidential transactions to coexist with business competitors and other restricted members, on the same blockchain network.


####Capability Requirements####
Because Fabric is a distributed system that will usually involve multiple organizations (sometimes in different countries or even continents), it is possible (and typical) that many different versions of Fabric code will exist in the network. Nevertheless, it’s vital that networks process transactions in the same way so that everyone has the same view of the current network state.

This means that every network – and every channel within that network – must define a set of what we call “capabilities” to be able to participate in processing transactions. For example, Fabric v1.1 introduces new MSP role types of “Peer” and “Client”. However, if a v1.0 peer does not understand these new role types, it will not be able to appropriately evaluate an endorsement policy that references them. This means that before the new role types may be used, the network must agree to enable the v1.1 channel capability requirement, ensuring that all peers come to the same decision.

Only binaries which support the required capabilities will be able to participate in the channel, and newer binary versions will not enable new validation logic until the corresponding capability is enabled. In this way, capability requirements ensure that even with disparate builds and versions, it is not possible for the network to suffer a state fork.

#####Defining Capability Requirements#####
Capability requirements are defined per channel in the channel configuration (found in the channel’s most recent configuration block). The channel configuration contains three locations, each of which defines a capability of a different type.

	| Capability Type 	| Canonical Path					| JSON Path |
    | --------  		| -------    						| -------
    | Channel			| /Channel/Capabilities 		    |	.channel_group.values.Capabilities
					|
    | Orderer			| /Channel/Orderer/Capabilities	    |	.channel_group.groups.Orderer.values.Capabilities
					|
	| Application		| /Channel/Application/Capabilities  | .channel_group.groups.Application.values. Capabilities
					|
+ Channel: these capabilities apply to both peer and orderers and are located in the root Channel group.
+ Orderer: apply to orderers only and are located in the Orderer group.
+ Application: apply to peers only and are located in the Application group.

The capabilities are broken into these groups in order to align with the existing administrative structure. Updating orderer capabilities is something the ordering orgs would manage independent of the application orgs. Similarly, updating application capabilities is something only the application admins would manage. By splitting the capabilities between “Orderer” and “Application”, a hypothetical network could run a v1.6 ordering service while supporting a v1.3 peer application network.

However, some capabilities cross both the ‘Application’ and ‘Orderer’ groups. As we saw earlier, adding a new MSP role type is something both the orderer and application admins agree to and need to recognize. The orderer must understand the meaning of MSP roles in order to allow the transactions to pass through ordering, while the peers must understand the roles in order to validate the transaction. These kinds of capabilities – which span both the application and orderer components – are defined in the top level “Channel” group.

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		It is possible that the channel capabilities are defined to be at version v1.3 while the orderer and application capabilities are defined to be at version 1.1 and v1.4, respectively. Enabling a capability at the “Channel” group level does not imply that this same capability is available at the more specific “Orderer” and “Application” group levels.
		</td>
	</tr>
</table>

#####Setting Capabilities#####
Capabilities are set as part of the channel configuration (either as part of the initial configuration – which we’ll talk about in a moment – or as part of a reconfiguration).

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		We have a two documents that talk through different aspects of channel reconfigurations. First, we have a tutorial that will take you through the process of Adding an Org to a Channel. And we also have a document that talks through Updating a Channel Configuration which gives an overview of the different kinds of updates that are possible as well as a fuller look at the signature process.
		</td>
	</tr>
</table>

Because new channels copy the configuration of the Orderer System Channel by default, new channels will automatically be configured to work with the orderer and channel capabilities of the Orderer System Channel and the application capabilities specified by the channel creation transaction. Channels that already exist, however, must be reconfigured.

The schema for the Capabilities value is defined in the protobuf as:

	message Capabilities {
	      map<string, Capability> capabilities = 1;
	}
	
	message Capability { }

As an example, rendered in JSON:

	{
	    "capabilities": {
	        "V1_1": {}
	    }
	}

######Capabilities in an Initial Configuration######
In the configtx.yaml file distributed in the config directory of the release artifacts, there is a Capabilities section which enumerates the possible capabilities for each capability type (Channel, Orderer, and Application).

The simplest way to enable capabilities is to pick a v1.1 sample profile and customize it for your network. For example:

	SampleSingleMSPSoloV1_1:
	    Capabilities:
	        <<: *GlobalCapabilities
	    Orderer:
	        <<: *OrdererDefaults
	        Organizations:
	            - *SampleOrg
	        Capabilities:
	            <<: *OrdererCapabilities
	    Consortiums:
	        SampleConsortium:
	            Organizations:
	                - *SampleOrg

Note that there is a Capabilities section defined at the root level (for the channel capabilities), and at the Orderer level (for orderer capabilities). The sample above uses a YAML reference to include the capabilities as defined at the bottom of the YAML.

When defining the orderer system channel there is no Application section, as those capabilities are defined during the creation of an application channel. To define a new channel’s application capabilities at channel creation time, the application admins should model their channel creation transaction after the SampleSingleMSPChannelV1_1 profile.

	SampleSingleMSPChannelV1_1:
	     Consortium: SampleConsortium
	     Application:
	         Organizations:
	             - *SampleOrg
	         Capabilities:
	             <<: *ApplicationCapabilities

Here, the Application section has a new element Capabilities which references the ApplicationCapabilities section defined at the end of the YAML.

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		The capabilities for the Channel and Orderer sections are inherited from the definition in the ordering system channel and are automatically included by the orderer during the process of channel creation.
		</td>
	</tr>
</table>


####CouchDB as the State Database####
#####State Database options#####
State database options include LevelDB and CouchDB. LevelDB is the default key-value state database embedded in the peer process. CouchDB is an optional alternative external state database. Like the LevelDB key-value store, CouchDB can store any binary data that is modeled in chaincode (CouchDB attachment functionality is used internally for non-JSON binary data). But as a JSON document store, CouchDB additionally enables rich query against the chaincode data, when chaincode values (e.g. assets) are modeled as JSON data.

Both LevelDB and CouchDB support core chaincode operations such as getting and setting a key (asset), and querying based on keys. Keys can be queried by range, and composite keys can be modeled to enable equivalence queries against multiple parameters. For example a composite key of owner,asset_id can be used to query all assets owned by a certain entity. These key-based queries can be used for read-only queries against the ledger, as well as in transactions that update the ledger.

If you model assets as JSON and use CouchDB, you can also perform complex rich queries against the chaincode data values, using the CouchDB JSON query language within chaincode. These types of queries are excellent for understanding what is on the ledger. Proposal responses for these types of queries are typically useful to the client application, but are not typically submitted as transactions to the ordering service. In fact, there is no guarantee the result set is stable between chaincode execution and commit time for rich queries, and therefore rich queries are not appropriate for use in update transactions, unless your application can guarantee the result set is stable between chaincode execution time and commit time, or can handle potential changes in subsequent transactions. For example, if you perform a rich query for all assets owned by Alice and transfer them to Bob, a new asset may be assigned to Alice by another transaction between chaincode execution time and commit time, and you would miss this “phantom” item.

CouchDB runs as a separate database process alongside the peer, therefore there are additional considerations in terms of setup, management, and operations. You may consider starting with the default embedded LevelDB, and move to CouchDB if you require the additional complex rich queries. It is a good practice to model chaincode asset data as JSON, so that you have the option to perform complex rich queries if needed in the future.

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		A JSON document cannot use the following field names at the top level. These are reserved for internal use.
			<p>
			_deleted
			<p>
			_id
			<p>
			_rev
			<p>
			~version
		</td>
	</tr>
</table>

#####Using CouchDB from Chaincode#####
Most of the chaincode shim APIs can be utilized with either LevelDB or CouchDB state database, e.g. GetState, PutState, GetStateByRange, GetStateByPartialCompositeKey. Additionally when you utilize CouchDB as the state database and model assets as JSON in chaincode, you can perform rich queries against the JSON in the state database by using the GetQueryResult API and passing a CouchDB query string. The query string follows the CouchDB JSON query syntax.

The marbles02 fabric sample demonstrates use of CouchDB queries from chaincode. It includes a queryMarblesByOwner() function that demonstrates parameterized queries by passing an owner id into chaincode. It then queries the state data for JSON documents matching the docType of “marble” and the owner id using the JSON query syntax:

	{"selector":{"docType":"marble","owner":<OWNER_ID>}}

Indexes in CouchDB are required in order to make JSON queries efficient and are required for any JSON query with a sort. Indexes can be packaged alongside chaincode in a /META-INF/statedb/couchdb/indexes directory. Each index must be defined in its own text file with extension *.json with the index definition formatted in JSON following the CouchDB index JSON syntax. For example, to support the above marble query, a sample index on the docType and owner fields is provided:

	{"index":{"fields":["docType","owner"]},"ddoc":"indexOwnerDoc", "name":"indexOwner","type":"json"}

The sample index can be found here.

Any index in the chaincode’s META-INF/statedb/couchdb/indexes directory will be packaged up with the chaincode for deployment. When the chaincode is both installed on a peer and instantiated on one of the peer’s channels, the index will automatically be deployed to the peer’s channel and chaincode specific state database (if it has been configured to use CouchDB). If you install the chaincode first and then instantiate the chaincode on the channel, the index will be deployed at chaincode instantiation time. If the chaincode is already instantiated on a channel and you later install the chaincode on a peer, the index will be deployed at chaincode installation time.

Upon deployment, the index will automatically be utilized by chaincode queries. CouchDB can automatically determine which index to use based on the fields being used in a query. Alternatively, in the selector query the index can be specified using the use_index keyword.

The same index may exist in subsequent versions of the chaincode that gets installed. To change the index, use the same index name but alter the index definition. Upon installation/instantiation, the index definition will get re-deployed to the peer’s state database.

If you have a large volume of data already, and later install the chaincode, the index creation upon installation may take some time. Similarly, if you have a large volume of data already and instantiate a subsequent version of the chaincode, the index creation may take some time. Avoid calling chaincode functions that query the state database at these times as the chaincode query may time out while the index is getting initialized. During transaction processing, the indexes will automatically get refreshed as blocks are committed to the ledger.

#####CouchDB Configuration#####
CouchDB is enabled as the state database by changing the stateDatabase configuration option from goleveldb to CouchDB. Additionally, the couchDBAddress needs to configured to point to the CouchDB to be used by the peer. The username and password properties should be populated with an admin username and password if CouchDB is configured with a username and password. Additional options are provided in the couchDBConfig section and are documented in place. Changes to the core.yaml will be effective immediately after restarting the peer.

You can also pass in docker environment variables to override core.yaml values, for example CORE_LEDGER_STATE_STATEDATABASE and CORE_LEDGER_STATE_COUCHDBCONFIG_COUCHDBADDRESS.

Below is the stateDatabase section from core.yaml:

	state:
	  # stateDatabase - options are "goleveldb", "CouchDB"
	  # goleveldb - default state database stored in goleveldb.
	  # CouchDB - store state database in CouchDB
	  stateDatabase: goleveldb
	  couchDBConfig:
	     # It is recommended to run CouchDB on the same server as the peer, and
	     # not map the CouchDB container port to a server port in docker-compose.
	     # Otherwise proper security must be provided on the connection between
	     # CouchDB client (on the peer) and server.
	     couchDBAddress: couchdb:5984
	     # This username must have read and write authority on CouchDB
	     username:
	     # The password is recommended to pass as an environment variable
	     # during start up (e.g. LEDGER_COUCHDBCONFIG_PASSWORD).
	     # If it is stored here, the file must be access control protected
	     # to prevent unintended users from discovering the password.
	     password:
	     # Number of retries for CouchDB errors
	     maxRetries: 3
	     # Number of retries for CouchDB errors during peer startup
	     maxRetriesOnStartup: 10
	     # CouchDB request timeout (unit: duration, e.g. 20s)
	     requestTimeout: 35s
	     # Limit on the number of records to return per query
	     queryLimit: 10000

CouchDB hosted in docker containers supplied with Hyperledger Fabric have the capability of setting the CouchDB username and password with environment variables passed in with the COUCHDB_USER and COUCHDB_PASSWORD environment variables using Docker Compose scripting.

For CouchDB installations outside of the docker images supplied with Fabric, the local.ini file of that installation must be edited to set the admin username and password.

Docker compose scripts only set the username and password at the creation of the container. The local.ini file must be edited if the username or password is to be changed after creation of the container.

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		CouchDB peer options are read on each peer startup.
		</td>
	</tr>
</table>


####Peer channel-based event services####
#####General overview#####
In previous versions of Fabric, the peer event service was known as the event hub. This service sent events any time a new block was added to the peer’s ledger, regardless of the channel to which that block pertained, and it was only accessible to members of the organization running the eventing peer (i.e., the one being connected to for events).

Starting with v1.1, there are two new services which provide events. These services use an entirely different design to provide events on a per-channel basis. This means that registration for events occurs at the level of the channel instead of the peer, allowing for fine-grained control over access to the peer’s data. Requests to receive events are accepted from identities outside of the peer’s organization (as defined by the channel configuration). This also provides greater reliability and a way to receive events that may have been missed (whether due to a connectivity issue or because the peer is joining a network that has already been running).

#####Available services#####
+ Deliver

This service sends entire blocks that have been committed to the ledger. If any events were set by a chaincode, these can be found within the ChaincodeActionPayload of the block.

+ DeliverFiltered

This service sends “filtered” blocks, minimal sets of information about blocks that have been committed to the ledger. It is intended to be used in a network where owners of the peers wish for external clients to primarily receive information about their transactions and the status of those transactions. If any events were set by a chaincode, these can be found within the FilteredChaincodeAction of the filtered block.

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		The payload of chaincode events will not be included in filtered blocks.
		</td>
	</tr>
</table>

#####How to register for events#####
Registration for events from either service is done by sending an envelope containing a deliver seek info message to the peer that contains the desired start and stop positions, the seek behavior (block until ready or fail if not ready). There are helper variables SeekOldest and SeekNewest that can be used to indicate the oldest (i.e. first) block or the newest (i.e. last) block on the ledger. To have the services send events indefinitely, the SeekInfo message should include a stop position of MAXINT64.

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		If mutual TLS is enabled on the peer, the TLS certificate hash must be set in the envelope’s channel header.
		</td>
	</tr>
</table>

By default, both services use the Channel Readers policy to determine whether to authorize requesting clients for events.

#####Overview of deliver response messages#####
The event services send back DeliverResponse messages.

Each message contains one of the following:

		status – HTTP status code. Both services will return the appropriate failure code if any failure occurs; otherwise, it will return 200 - SUCCESS once the service has completed sending all information requested by the SeekInfo message.
		block – returned only by the Deliver service.
		filtered block – returned only by the DeliverFiltered service.

A filtered block contains:

		channel ID.
		number (i.e. the block number).
		array of filtered transactions.
		transaction ID.

				type (e.g. ENDORSER_TRANSACTION, CONFIG.
				transaction validation code.
		filtered transaction actions.
				array of filtered chaincode actions.
						chaincode event for the transaction (with the payload nilled out).

#####SDK event documentation#####
For further details on using the event services, refer to the SDK documentation.


####Read-Write set semantics####
This documents discusses the details of the current implementation about the semantics of read-write sets.

#####Transaction simulation and read-write set#####
During simulation of a transaction at an endorser, a read-write set is prepared for the transaction. The read set contains a list of unique keys and their committed versions that the transaction reads during simulation. The write set contains a list of unique keys (though there can be overlap with the keys present in the read set) and their new values that the transaction writes. A delete marker is set (in the place of new value) for the key if the update performed by the transaction is to delete the key.

Further, if the transaction writes a value multiple times for a key, only the last written value is retained. Also, if a transaction reads a value for a key, the value in the committed state is returned even if the transaction has updated the value for the key before issuing the read. In another words, Read-your-writes semantics are not supported.

As noted earlier, the versions of the keys are recorded only in the read set; the write set just contains the list of unique keys and their latest values set by the transaction.

There could be various schemes for implementing versions. The minimal requirement for a versioning scheme is to produce non-repeating identifiers for a given key. For instance, using monotonically increasing numbers for versions can be one such scheme. In the current implementation, we use a blockchain height based versioning scheme in which the height of the committing transaction is used as the latest version for all the keys modified by the transaction. In this scheme, the height of a transaction is represented by a tuple (txNumber is the height of the transaction within the block). This scheme has many advantages over the incremental number scheme - primarily, it enables other components such as statedb, transaction simulation and validation for making efficient design choices.

Following is an illustration of an example read-write set prepared by simulation of a hypothetical transaction. For the sake of simplicity, in the illustrations, we use the incremental numbers for representing the versions.

	<TxReadWriteSet>
	  <NsReadWriteSet name="chaincode1">
	    <read-set>
	      <read key="K1", version="1">
	      <read key="K2", version="1">
	    </read-set>
	    <write-set>
	      <write key="K1", value="V1"
	      <write key="K3", value="V2"
	      <write key="K4", isDelete="true"
	    </write-set>
	  </NsReadWriteSet>
	<TxReadWriteSet>

Additionally, if the transaction performs a range query during simulation, the range query as well as its results will be added to the read-write set as query-info.

#####Transaction validation and updating world state using read-write set#####
A committer uses the read set portion of the read-write set for checking the validity of a transaction and the write set portion of the read-write set for updating the versions and the values of the affected keys.

In the validation phase, a transaction is considered valid if the version of each key present in the read set of the transaction matches the version for the same key in the world state - assuming all the preceding valid transactions (including the preceding transactions in the same block) are committed (committed-state). An additional validation is performed if the read-write set also contains one or more query-info.

This additional validation should ensure that no key has been inserted/deleted/updated in the super range (i.e., union of the ranges) of the results captured in the query-info(s). In other words, if we re-execute any of the range queries (that the transaction performed during simulation) during validation on the committed-state, it should yield the same results that were observed by the transaction at the time of simulation. This check ensures that if a transaction observes phantom items during commit, the transaction should be marked as invalid. Note that the this phantom protection is limited to range queries (i.e., GetStateByRange function in the chaincode) and not yet implemented for other queries (i.e., GetQueryResult function in the chaincode). Other queries are at risk of phantoms, and should therefore only be used in read-only transactions that are not submitted to ordering, unless the application can guarantee the stability of the result set between simulation and validation/commit time.

If a transaction passes the validity check, the committer uses the write set for updating the world state. In the update phase, for each key present in the write set, the value in the world state for the same key is set to the value as specified in the write set. Further, the version of the key in the world state is changed to reflect the latest version.

#####Example simulation and validation#####
This section helps with understanding the semantics through an example scenario. For the purpose of this example, the presence of a key, k, in the world state is represented by a tuple (k,ver,val) where ver is the latest version of the key k having val as its value.

Now, consider a set of five transactions T1, T2, T3, T4, and T5, all simulated on the same snapshot of the world state. The following snippet shows the snapshot of the world state against which the transactions are simulated and the sequence of read and write activities performed by each of these transactions.

	World state: (k1,1,v1), (k2,1,v2), (k3,1,v3), (k4,1,v4), (k5,1,v5)
	T1 -> Write(k1, v1'), Write(k2, v2')
	T2 -> Read(k1), Write(k3, v3')
	T3 -> Write(k2, v2'')
	T4 -> Write(k2, v2'''), read(k2)
	T5 -> Write(k6, v6'), read(k5)

Now, assume that these transactions are ordered in the sequence of T1,..,T5 (could be contained in a single block or different blocks)

1. T1 passes validation because it does not perform any read. Further, the tuple of keys k1 and k2 in the world state are updated to (k1,2,v1'), (k2,2,v2')
2. T2 fails validation because it reads a key, k1, which was modified by a preceding transaction - T1
3. T3 passes the validation because it does not perform a read. Further the tuple of the key, k2, in the world state is updated to (k2,3,v2'')
4. T4 fails the validation because it reads a key, k2, which was modified by a preceding transaction T1
5. T5 passes validation because it reads a key, k5, which was not modified by any of the preceding transactions

Note: Transactions with multiple read-write sets are not yet supported.


####Gossip data dissemination protocol####
Hyperledger Fabric optimizes blockchain network performance, security and scalability by dividing workload across transaction execution (endorsing and committing) peers and transaction ordering nodes. This decoupling of network operations requires a secure, reliable and scalable data dissemination protocol to ensure data integrity and consistency. To meet these requirements, Hyperledger Fabric implements a gossip data dissemination protocol.

#####Gossip protocol#####
Peers leverage gossip to broadcast ledger and channel data in a scalable fashion. Gossip messaging is continuous, and each peer on a channel is constantly receiving current and consistent ledger data, from multiple peers. Each gossiped message is signed, thereby allowing Byzantine participants sending faked messages to be easily identified and the distribution of the message(s) to unwanted targets to be prevented. Peers affected by delays, network partitions or other causations resulting in missed blocks, will eventually be synced up to the current ledger state by contacting peers in possession of these missing blocks.

The gossip-based data dissemination protocol performs three primary functions on a Hyperledger Fabric network:

1. Manages peer discovery and channel membership, by continually identifying available member peers, and eventually detecting peers that have gone offline.
2. Disseminates ledger data across all peers on a channel. Any peer with data that is out of sync with the rest of the channel identifies the missing blocks and syncs itself by copying the correct data.
3. Bring newly connected peers up to speed by allowing peer-to-peer state transfer update of ledger data.

Gossip-based broadcasting operates by peers receiving messages from other peers on the channel, and then forwarding these messages to a number of randomly-selected peers on the channel, where this number is a configurable constant. Peers can also exercise a pull mechanism, rather than waiting for delivery of a message. This cycle repeats, with the result of channel membership, ledger and state information continually being kept current and in sync. For dissemination of new blocks, the leader peer on the channel pulls the data from the ordering service and initiates gossip dissemination to peers.

#####Leader election#####
The leader election mechanism is used to elect one peer per each organization which will maintain connection with ordering service and initiate distribution of newly arrived blocks across peers of its own organization. Leveraging leader election provides system with ability to efficiently utilize bandwidth of the ordering service. There are two possible operation modes for leader election module:

1. Static - system administrator manually configures one peer in the organization to be the leader, e.g. one to maintain open connection with the ordering service.
2. Dynamic - peers execute a leader election procedure to select one peer in an organization to become leader, pull blocks from the ordering service, and disseminate blocks to the other peers in the organization..

#####Static leader election#####
Using static leader election allows to manually define a set of leader peers within the organization, it’s possible to define a single node to be a leader or all available peers, it should be taken into account that - making too many peers to connect to the ordering service might lead to inefficient bandwidth utilization. To enable static leader election mode, configure the following parameters within the section of core.yaml:

	peer:
	    # Gossip related configuration
	    gossip:
	        useLeaderElection: false
	        orgLeader: true

Alternatively these parameters could be configured and overrided with environmental variables:

	export CORE_PEER_GOSSIP_USELEADERELECTION=false
	export CORE_PEER_GOSSIP_ORGLEADER=true

Note:
1. Following configuration will keep peer in stand-by mode, i.e. peer will not try to become a leader:
	export CORE_PEER_GOSSIP_USELEADERELECTION=false
	export CORE_PEER_GOSSIP_ORGLEADER=false
2. Setting CORE_PEER_GOSSIP_USELEADERELECTION and CORE_PEER_GOSSIP_USELEADERELECTION with true value is ambiguous and will lead to an error.
3. In static configuration organization admin is responsible to provide high availability of the leader node in case for failure or crashes.

#####Dynamic leader election#####
Dynamic leader election enables organization peers to elect one peer which will connect to the ordering service and pull out new blocks. Leader is elected for set of peers for each organization independently.

Elected leader is responsible to send the heartbeat messages to the rest of the peers as an evidence of liveness. If one or more peers won’t get heartbeats updates during period of time, they will initiate a new round of leader election procedure, eventually selecting a new leader. In case of a network partition in the worst case there will be more than one active leader for organization thus to guarantee resiliency and availability allowing the organization’s peers to continue making progress. After the network partition is healed one of the leaders will relinquish its leadership, therefore in steady state and in no presence of network partitions for each organization there will be only one active leader connecting to the ordering service.

Following configuration controls frequency of the leader heartbeat messages:

	peer:
	    # Gossip related configuration
	    gossip:
	        election:
	            leaderAliveThreshold: 10s

In order to enable dynamic leader election, the following parameters need to be configured within core.yaml:

	peer:
	    # Gossip related configuration
	    gossip:
	        useLeaderElection: true
	        orgLeader: false

Alternatively these parameters could be configured and overrided with environmental variables:

	export CORE_PEER_GOSSIP_USELEADERELECTION=true
	export CORE_PEER_GOSSIP_ORGLEADER=false

#####Gossip messaging#####
Online peers indicate their availability by continually broadcasting “alive” messages, with each containing the public key infrastructure (PKI) ID and the signature of the sender over the message. Peers maintain channel membership by collecting these alive messages; if no peer receives an alive message from a specific peer, this “dead” peer is eventually purged from channel membership. Because “alive” messages are cryptographically signed, malicious peers can never impersonate other peers, as they lack a signing key authorized by a root certificate authority (CA).

In addition to the automatic forwarding of received messages, a state reconciliation process synchronizes world state across peers on each channel. Each peer continually pulls blocks from other peers on the channel, in order to repair its own state if discrepancies are identified. Because fixed connectivity is not required to maintain gossip-based data dissemination, the process reliably provides data consistency and integrity to the shared ledger, including tolerance for node crashes.

Because channels are segregated, peers on one channel cannot message or share information on any other channel. Though any peer can belong to multiple channels, partitioned messaging prevents blocks from being disseminated to peers that are not in the channel by applying message routing policies based on peers’ channel subscriptions.

Notes:

1. Security of point-to-point messages are handled by the peer TLS layer, and do not require signatures. Peers are authenticated by their certificates, which are assigned by a CA. Although TLS certs are also used, it is the peer certificates that are authenticated in the gossip layer. Ledger blocks are signed by the ordering service, and then delivered to the leader peers on a channel.
2. Authentication is governed by the membership service provider for the peer. When the peer connects to the channel for the first time, the TLS session binds with the membership identity. This essentially authenticates each peer to the connecting peer, with respect to membership in the network and channel.


###七、Hyperledger Fabric FAQ###
####Endorsement####
#####Endorsement architecture:#####
Q. How many peers in the network need to endorse a transaction?

A. The number of peers required to endorse a transaction is driven by the endorsement policy that is specified at chaincode deployment time.

Q. Does an application client need to connect to all peers?

A. Clients only need to connect to as many peers as are required by the endorsement policy for the chaincode.

####Security & Access Control####
#####Data Privacy and Access Control:#####
Q. How do I ensure data privacy?

A. There are various aspects to data privacy. First, you can segregate your network into channels, where each channel represents a subset of participants that are authorized to see the data for the chaincodes that are deployed to that channel. Second, within a channel you can restrict the input data to chaincode to the set of endorsers only, by using visibility settings. The visibility setting will determine whether input and output chaincode data is included in the submitted transaction, versus just output data. Third, you can hash or encrypt the data before calling chaincode. If you hash the data then you will need to provide a means to share the source data. If you encrypt the data then you will need to provide a means to share the decryption keys. Fourth, you can restrict data access to certain roles in your organization, by building access control into the chaincode logic. Fifth, ledger data at rest can be encrypted via file system encryption on the peer, and data in-transit is encrypted via TLS.

Q. Do the orderers see the transaction data?

A. No, the orderers only order transactions, they do not open the transactions. If you do not want the data to go through the orderers at all, and you are only concerned about the input data, then you can use visibility settings. The visibility setting will determine whether input and output chaincode data is included in the submitted transaction, versus just output data. Therefore, the input data can be private to the endorsers only. If you do not want the orderers to see chaincode output, then you can hash or encrypt the data before calling chaincode. If you hash the data then you will need to provide a meansto share the source data. If you encrypt the data then you will need to provide a means to share the decryption keys.

####Application-side Programming Model####
#####Transaction execution result:#####
Q. How do application clients know the outcome of a transaction?

A. The transaction simulation results are returned to the client by the endorser in the proposal response. If there are multiple endorsers, the client can check that the responses are all the same, and submit the results and endorsements for ordering and commitment. Ultimately the committing peers will validate or invalidate the transaction, and the client becomes aware of the outcome via an event, that the SDK makes available to the application client.

#####Ledger queries:#####
Q. How do I query the ledger data?

A. Within chaincode you can query based on keys. Keys can be queried by range, and composite keys can be modeled to enable equivalence queries against multiple parameters. For example a composite key of (owner,asset_id) can be used to query all assets owned by a certain entity. These key-based queries can be used for read-only queries against the ledger, as well as in transactions that update the ledger.

If you model asset data as JSON in chaincode and use CouchDB as the state database, you can also perform complex rich queries against the chaincode data values, using the CouchDB JSON query language within chaincode. The application client can perform read-only queries, but these responses are not typically submitted as part of transactions to the ordering service.

Q. How do I query the historical data to understand data provenance?

A. The chaincode API GetHistoryForKey() will return history of values for a key.

Q. How to guarantee the query result is correct, especially when the peer being queried may be recovering and catching up on block processing?

A. The client can query multiple peers, compare their block heights, compare their query results, and favor the peers at the higher block heights.

####Chaincode (Smart Contracts and Digital Assets)####
Q. Does Hyperledger Fabric support smart contract logic?

A. Yes. We call this feature Chaincode. It is our interpretation of the smart contract method/algorithm, with additional features.

A chaincode is programmatic code deployed on the network, where it is executed and validated by chain validators together during the consensus process. Developers can use chaincodes to develop business contracts, asset definitions, and collectively-managed decentralized applications.

Q. How do I create a business contract?

A. There are generally two ways to develop business contracts: the first way is to code individual contracts into standalone instances of chaincode; the second way, and probably the more efficient way, is to use chaincode to create decentralized applications that manage the life cycle of one or multiple types of business contracts, and let end users instantiate instances of contracts within these applications.

Q. How do I create assets?

A. Users can use chaincode (for business rules) and membership service (for digital tokens) to design assets, as well as the logic that manages them.

There are two popular approaches to defining assets in most blockchain solutions: the stateless UTXO model, where account balances are encoded into past transaction records; and the account model, where account balances are kept in state storage space on the ledger.

Each approach carries its own benefits and drawbacks. This blockchain technology does not advocate either one over the other. Instead, one of our first requirements was to ensure that both approaches can be easily implemented.

Q. Which languages are supported for writing chaincode?

A. Chaincode can be written in any programming language and executed in containers. The first fully supported chaincode language is Golang.

Support for additional languages and the development of a templating language have been discussed, and more details will be released in the near future.

It is also possible to build Hyperledger Fabric applications using Hyperledger Composer.

Q. Does the Hyperledger Fabric have native currency?

A. No. However, if you really need a native currency for your chain network, you can develop your own native currency with chaincode. One common attribute of native currency is that some amount will get transacted (the chaincode defining that currency will get called) every time a transaction is processed on its chain.

####Differences in Most Recent Releases####
Q. Where can I find what are the highlighted differences between releases?

A. The differences between any subsequent releases are provided together with the Release Notes.

Q. Where to get help for the technical questions not answered above?

A. Please use StackOverflow.


###八、Ordering Service FAQ###
####General####
Question:	I have an ordering service up and running and want to switch consensus algorithms. How do I do that?

Answer:	This is explicitly not supported.


Question:	What is the orderer system channel?

Answer:	The orderer system channel (sometimes called ordering system channel) is the channel the orderer is initially bootstrapped with. It is used to orchestrate channel creation. The orderer system channel defines consortia and the initial configuration for new channels. At channel creation time, the organization definition in the consortium, the /Channel group’s values and policies, as well as the /Channel/Orderer group’s values and policies, are all combined to form the new initial channel definition.

Question:	If I update my application channel, should I update my orderer system channel?

Answer:	Once an application channel is created, it is managed independently of any other channel (including the orderer system channel). Depending on the modification, the change may or may not be desirable to port to other channels. In general, MSP changes should be synchronized across all channels, while policy changes are more likely to be specific to a particular channel.

Question:	Can I have an organization act both in an ordering and application role?

Answer:	Although this is possible, it is a highly discouraged configuration. By default the /Channel/Orderer/BlockValidation policy allows any valid certificate of the ordering organizations to sign blocks. If an organization is acting both in an ordering and application role, then this policy should be updated to restrict block signers to the subset of certificates authorized for ordering.


Question:	I want to write a consensus implementation for Fabric. Where do I begin?

Answer:	A consensus plugin needs to implement the Consenter and Chain interfaces defined in the consensus package. There are two plugins built against these interfaces already: solo and kafka. You can study them to take cues for your own implementation. The ordering service code can be found under the orderer package.

Question:	I want to change my ordering service configurations, e.g. batch timeout, after I start the network, what should I do?

Answer:	This falls under reconfiguring the network. Please consult the topic on configtxlator.

####Solo####
Question:	How can I deploy Solo in production?

Answer:	Solo is not intended for production. It is not, and will never be, fault tolerant.

####Kafka####
Question:	
How do I remove a node from the ordering service?

Answer:	
This is a two step-process:

1. Add the node’s certificate to the relevant orderer’s MSP CRL to prevent peers/clients from connecting to it.
2. Prevent the node from connecting to the Kafka cluster by leveraging standard Kafka access control measures such as TLS CRLs, or firewalling.


Question:	I have never deployed a Kafka/ZK cluster before, and I want to use the Kafka-based ordering service. How do I proceed?

Answer:	The Hyperledger Fabric documentation assumes the reader generally has the operational expertise to setup, configure, and manage a Kafka cluster (see Caveat emptor). If you insist on proceeding without such expertise, you should complete, at a minimum, the first 6 steps of the Kafka Quickstart guide before experimenting with the Kafka-based ordering service.


Question:	Where can I find a Docker composition for a network that uses the Kafka-based ordering service?

Answer:	Consult the end-to-end CLI example.


Question:	Why is there a ZooKeeper dependency in the Kafka-based ordering service?

Answer:	Kafka uses it internally for coordination between its brokers.

Question:	I’m trying to follow the BYFN example and get a “service unavailable” error, what should I do?

Answer:	Check the ordering service’s logs. A “Rejecting deliver request because of consenter error” log message is usually indicative of a connection problem with the Kafka cluster. Ensure that the Kafka cluster is set up properly, and is reachable by the ordering service’s nodes.

####BFT####
Question:	When is a BFT version of the ordering service going to be available?

Answer:	No date has been set. We are working towards a release during the 1.x cycle, i.e. it will come with a minor version upgrade in Fabric. Track FAB-33 for updates.



###九、欢迎贡献###
We welcome contributions to Hyperledger in many forms, and there’s always plenty to do!

First things first, please review the Hyperledger Code of Conduct before participating. It is important that we keep things civil.

####Maintainers####
Active Maintainers
略

####Using Jira to understand current work items####
略

####Setting up the development environment####
#####Overview#####
Prior to the v1.0.0 release, the development environment utilized Vagrant running an Ubuntu image, which in turn launched Docker containers as a means of ensuring a consistent experience for developers who might be working with varying platforms, such as macOS, Windows, Linux, or whatever. Advances in Docker have enabled native support on the most popular development platforms: macOS and Windows. Hence, we have reworked our build to take full advantage of these advances. While we still maintain a Vagrant based approach that can be used for older versions of macOS and Windows that Docker does not support, we strongly encourage that the non-Vagrant development setup be used.

Note that while the Vagrant-based development setup could not be used in a cloud context, the Docker-based build does support cloud platforms such as AWS, Azure, Google and IBM to name a few. Please follow the instructions for Ubuntu builds, below.

#####Prerequisites#####
+ Git client
+ Go - 1.9 or later (for v1.0.X releases, use Go 1.7.X)
+ (macOS) Xcode must be installed
+ Docker - 17.06.2-ce or later
+ Docker Compose - 1.14.0 or later
+ Pip
+ (macOS) you may need to install gnutar, as macOS comes with bsdtar as the default, but the build uses some gnutar flags. You can use Homebrew to install it as follows:
	
	brew install gnu-tar --with-default-names
+ (macOS) Libtool. You can use Homebrew to install it as follows:
	
	brew install libtool
+ (only if using Vagrant) - Vagrant - 1.9 or later
+ (only if using Vagrant) - VirtualBox - 5.0 or later
+ BIOS Enabled Virtualization - Varies based on hardware
+ Note: The BIOS Enabled Virtualization may be within the CPU or Security settings of the BIOS

#####pip and behave#####
	pip install --upgrade pip

	#PIP packages required for some behave tests
	pip install -r devenv/bddtests-requirements.txt

#####Steps#####
######Set your GOPATH######
Make sure you have properly setup your Host’s GOPATH environment variable. This allows for both building within the Host and the VM.

In case you installed Go into a different location from the standard one your Go distribution assumes, make sure that you also set GOROOT environment variable.

######Note to Windows users######
If you are running Windows, before running any git clone commands, run the following command.

	git config --get core.autocrlf

If core.autocrlf is set to true, you must set it to false by running

	git config --global core.autocrlf false

If you continue with core.autocrlf set to true, the vagrant up command will fail with the error:

	./setup.sh: /bin/bash^M: bad interpreter: No such file or directory

######Cloning the Hyperledger Fabric source######
Since Hyperledger Fabric is written in Go, you’ll need to clone the source repository to your $GOPATH/src directory. If your $GOPATH has multiple path components, then you will want to use the first one. There’s a little bit of setup needed:

	cd $GOPATH/src
	mkdir -p github.com/hyperledger
	cd github.com/hyperledger

Recall that we are using Gerrit for source control, which has its own internal git repositories. Hence, we will need to clone from Gerrit. For brevity, the command is as follows:

	git clone ssh://LFID@gerrit.hyperledger.org:29418/fabric && scp -p -P 29418 LFID@gerrit.hyperledger.org:hooks/commit-msg fabric/.git/hooks/

Note: Of course, you would want to replace LFID with your own Linux Foundation ID.

######Bootstrapping the VM using Vagrant######
If you are planning on using the Vagrant developer environment, the following steps apply. Again, we recommend against its use except for developers that are limited to older versions of macOS and Windows that are not supported by Docker for Mac or Windows.

	cd $GOPATH/src/github.com/hyperledger/fabric/devenv
	vagrant up

Go get coffee... this will take a few minutes. Once complete, you should be able to ssh into the Vagrant VM just created.

	vagrant ssh

Once inside the VM, you can find the source under $GOPATH/src/github.com/hyperledger/fabric. It is also mounted as /hyperledger.

#####Building Hyperledger Fabric#####
Once you have all the dependencies installed, and have cloned the repository, you can proceed to build and test Hyperledger Fabric.

#####Notes#####
NOTE: Any time you change any of the files in your local fabric directory (under $GOPATH/src/github.com/hyperledger/fabric), the update will be instantly available within the VM fabric directory.

NOTE: If you intend to run the development environment behind an HTTP Proxy, you need to configure the guest so that the provisioning process may complete. You can achieve this via the vagrant-proxyconf plugin. Install with vagrant plugin install vagrant-proxyconf and then set the VAGRANT_HTTP_PROXY and VAGRANT_HTTPS_PROXY environment variables before you execute vagrant up. More details are available here: https://github.com/tmatilai/vagrant-proxyconf/

NOTE: The first time you run this command it may take quite a while to complete (it could take 30 minutes or more depending on your environment) and at times it may look like it’s not doing anything. As long you don’t get any error messages just leave it alone, it’s all good, it’s just cranking.

NOTE to Windows 10 Users: There is a known problem with vagrant on Windows 10 (see mitchellh/vagrant#6754). If the vagrant up command fails it may be because you do not have the Microsoft Visual C++ Redistributable package installed. You can download the missing package at the following address: http://www.microsoft.com/en-us/download/details.aspx?id=8328

NOTE: The inclusion of the miekg/pkcs11 package introduces an external dependency on the libtdl.h header file during a build of fabric. Please ensure your libtool and libtdhl-dev packages are installed. Otherwise, you may get a ltdl.h header missing error. You can download the missing package by command: sudo apt-get install -y build-essential git make curl unzip g++ libtool.


####Building Hyperledger Fabric####
The following instructions assume that you have already set up your development environment.

To build Hyperledger Fabric:

	cd $GOPATH/src/github.com/hyperledger/fabric
	make dist-clean all

#####Running the unit tests#####
Use the following sequence to run all unit tests

	cd $GOPATH/src/github.com/hyperledger/fabric
	make unit-test

To run a subset of tests, set the TEST_PKGS environment variable. Specify a list of packages (separated by space), for example:

	export TEST_PKGS="github.com/hyperledger/fabric/core/ledger/..."
	make unit-test

To run a specific test use the -run RE flag where RE is a regular expression that matches the test case name. To run tests with verbose output use the -v flag. For example, to run the TestGetFoo test case, change to the directory containing the foo_test.go and call/execute

	go test -v -run=TestGetFoo

#####Running Node.js Client SDK Unit Tests#####
You must also run the Node.js unit tests to ensure that the Node.js client SDK is not broken by your changes. To run the Node.js unit tests, follow the instructions here.

#####Running Behave BDD Tests#####
Note: currently, the behave tests must be run from within in the Vagrant environment. See the development environment setup instructions if you have not already set up your Vagrant environment.

Behave tests will setup networks of peers with different security and consensus configurations and verify that transactions run properly. To run these tests

	cd $GOPATH/src/github.com/hyperledger/fabric
	make behave

Some of the Behave tests run inside Docker containers. If a test fails and you want to have the logs from the Docker containers, run the tests with this option:

	cd $GOPATH/src/github.com/hyperledger/fabric/bddtests
	behave -D logs=Y


####Building outside of Vagrant####
It is possible to build the project and run peers outside of Vagrant. Generally speaking, one has to ‘translate’ the vagrant setup file to the platform of your choice.

#####Building on Z#####
To make building on Z easier and faster, this script is provided (which is similar to the setup file provided for vagrant). This script has been tested only on RHEL 7.2 and has some assumptions one might want to re-visit (firewall settings, development as root user, etc.). It is however sufficient for development in a personally-assigned VM instance.

To get started, from a freshly installed OS:

	sudo su
	yum install git
	mkdir -p $HOME/git/src/github.com/hyperledger
	cd $HOME/git/src/github.com/hyperledger
	git clone http://gerrit.hyperledger.org/r/fabric
	source fabric/devenv/setupRHELonZ.sh

From this point, you can proceed as described above for the Vagrant development environment.

	cd $GOPATH/src/github.com/hyperledger/fabric
	make peer unit-test behave

######Building on Power Platform######
Development and build on Power (ppc64le) systems is done outside of vagrant as outlined here. For ease of setting up the dev environment on Ubuntu, invoke this script as root. This script has been validated on Ubuntu 16.04 and assumes certain things (like, development system has OS repositories in place, firewall setting etc) and in general can be improvised further.

To get started on Power server installed with Ubuntu, first ensure you have properly setup your Host’s GOPATH environment variable. Then, execute the following commands to build the fabric code:

	mkdir -p $GOPATH/src/github.com/hyperledger
	cd $GOPATH/src/github.com/hyperledger
	git clone http://gerrit.hyperledger.org/r/fabric
	sudo ./fabric/devenv/setupUbuntuOnPPC64le.sh
	cd $GOPATH/src/github.com/hyperledger/fabric
	make dist-clean all

######Building on Centos 7######
You will have to build CouchDB from source because there is no package available from the distribution. If you are planning a multi-orderer arrangement, you will also need to install Apache Kafka from source. Apache Kafka includes both Zookeeper and Kafka executables and supporting artifacts.

	export GOPATH={directory of your choice}
	mkdir -p $GOPATH/src/github.com/hyperledger
	FABRIC=$GOPATH/src/github.hyperledger/fabric
	git clone https://github.com/hyperledger/fabric $FABRIC
	cd $FABRIC
	git checkout master # <-- only if you want the master branch
	export PATH=$GOPATH/bin:$PATH
	make native

If you are not trying to build for docker, you only need the natives.


####Configuration####
Configuration utilizes the viper and cobra libraries.

There is a core.yaml file that contains the configuration for the peer process. Many of the configuration settings can be overridden on the command line by setting ENV variables that match the configuration setting, but by prefixing with ‘CORE_’. For example, logging level manipulation through the environment is shown below:

	CORE_PEER_LOGGING_LEVEL=CRITICAL peer


####Requesting a Linux Foundation Account####
Contributions to the Hyperledger Fabric code base require a Linux Foundation account — follow the steps below to create one if you don’t already have one.

#####Creating a Linux Foundation ID#####
1. Go to the Linux Foundation ID website.
2. Select the option I need to create a Linux Foundation ID, and fill out the form that appears.
3. Wait a few minutes, then look for an email message with the subject line: “Validate your Linux Foundation ID email”.
4. Open the received URL to validate your email address.
5. Verify that your browser displays the message You have successfully validated your e-mail address.
6. Access Gerrit by selecting Sign In, and use your new Linux Foundation account ID to sign in.

#####Configuring Gerrit to Use SSH#####
Gerrit uses SSH to interact with your Git client. If you already have an SSH key pair, you can skip the part of this section that explains how to generate one.

What follows explains how to generate an SSH key pair in a Linux environment — follow the equivalent steps on your OS.

First, create an SSH key pair with the command:

	ssh-keygen -t rsa -C "John Doe john.doe@example.com"

Note: This will ask you for a password to protect the private key as it generates a unique key. Please keep this password private, and DO NOT enter a blank password.

The generated SSH key pair can be found in the files ~/.ssh/id_rsa and ~/.ssh/id_rsa.pub.

Next, add the private key in the id_rsa file to your key ring, e.g.:

	ssh-add ~/.ssh/id_rsa

Finally, add the public key of the generated key pair to the Gerrit server, with the following steps:

1. Go to Gerrit.
2. Click on your account name in the upper right corner.
3. From the pop-up menu, select Settings.
4. On the left side menu, click on SSH Public Keys.
5. Paste the contents of your public key ~/.ssh/id_rsa.pub and click Add key.

Note: The id_rsa.pub file can be opened with any text editor. Ensure that all the contents of the file are selected, copied and pasted into the Add SSH key window in Gerrit.

Note: The SSH key generation instructions operate on the assumption that you are using the default naming. It is possible to generate multiple SSH keys and to name the resulting files differently. See the ssh-keygen documentation for details on how to do that. Once you have generated non-default keys, you need to configure SSH to use the correct key for Gerrit. In that case, you need to create a ~/.ssh/config file modeled after the one below.

	host gerrit.hyperledger.org
	 HostName gerrit.hyperledger.org
	 IdentityFile ~/.ssh/id_rsa_hyperledger_gerrit
	 User <LFID>

where <LFID> is your Linux Foundation ID and the value of IdentityFile is the name of the public key file you generated.

Warning: Potential Security Risk! Do not copy your private key ~/.ssh/id_rsa. Use only the public ~/.ssh/id_rsa.pub.

#####Checking Out the Source Code#####
Once you’ve set up SSH as explained in the previous section, you can clone the source code repository with the command:

	git clone ssh://<LFID>@gerrit.hyperledger.org:29418/fabric fabric

You have now successfully checked out a copy of the source code to your local machine.


####Working with Gerrit####
Follow these instructions to collaborate on Hyperledger Fabric through the Gerrit review system.

Please be sure that you are subscribed to the mailing list and of course, you can reach out on chat if you need help.

Gerrit assigns the following roles to users:

+ Submitters: May submit changes for consideration, review other code changes, and make recommendations for acceptance or rejection by voting +1 or -1, respectively.
+ Maintainers: May approve or reject changes based upon feedback from reviewers voting +2 or -2, respectively.
+ Builders: (e.g. Jenkins) May use the build automation infrastructure to verify the change.

Maintainers should be familiar with the review process. However, anyone is welcome to (and encouraged!) review changes, and hence may find that document of value.

#####Git-review#####
There’s a very useful tool for working with Gerrit called git-review. This command-line tool can automate most of the ensuing sections for you. Of course, reading the information below is also highly recommended so that you understand what’s going on behind the scenes.

#####Getting deeper into Gerrit#####
A comprehensive walk-through of Gerrit is beyond the scope of this document. There are plenty of resources available on the Internet. A good summary can be found here. We have also provided a set of Best Practices that you may find helpful.

#####Working with a local clone of the repository#####
To work on something, whether a new feature or a bugfix:

1. Open the Gerrit Projects page
2. Select the project you wish to work on.
3. Open a terminal window and clone the project locally using the Clone with git hook URL. Be sure that ssh is also selected, as this will make authentication much simpler:

	git clone ssh://LFID@gerrit.hyperledger.org:29418/fabric && scp -p -P 29418 LFID@gerrit.hyperledger.org:hooks/commit-msg fabric/.git/hooks/

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		If you are cloning the fabric project repository, you will want to clone it to the $GOPATH/src/github.com/hyperledger directory so that it will build, and so that you can use it with the Vagrant development environment.
		</td>
	</tr>
</table>
4. Create a descriptively-named branch off of your cloned repository
	
	cd fabric
	git checkout -b issue-nnnn
5. Commit your code. For an in-depth discussion of creating an effective commit, please read this document on submitting changes.
	
	git commit -s -a

Then input precise and readable commit msg and submit.
6. Any code changes that affect documentation should be accompanied by corresponding changes (or additions) to the documentation and tests. This will ensure that if the merged PR is reversed, all traces of the change will be reversed as well.

#####Submitting a Change#####
Currently, Gerrit is the only method to submit a change for review.

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		Please review the guidelines for making and submitting a change.
		</td>
	</tr>
</table>

#####Using git review#####
<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		if you prefer, you can use the git-review tool instead of the following. e.g.
		</td>
	</tr>
</table>

Add the following section to .git/config, and replace <USERNAME> with your gerrit id.

	[remote "gerrit"]
	    url = ssh://<USERNAME>@gerrit.hyperledger.org:29418/fabric.git
	    fetch = +refs/heads/*:refs/remotes/gerrit/*

Then submit your change with git review.

	$ cd <your code dir>
	$ git review

When you update your patch, you can commit with git commit --amend, and then repeat the git review command.

#####Not using git review#####
See the directions for building the source code.

When a change is ready for submission, Gerrit requires that the change be pushed to a special branch. The name of this special branch contains a reference to the final branch where the code should reside, once accepted.

For the Hyperledger Fabric repository, the special branch is called refs/for/master.

To push the current local development branch to the gerrit server, open a terminal window at the root of your cloned repository:

	cd <your clone dir>
	git push origin HEAD:refs/for/master

If the command executes correctly, the output should look similar to this:

	Counting objects: 3, done.
	Writing objects: 100% (3/3), 306 bytes | 0 bytes/s, done.
	Total 3 (delta 0), reused 0 (delta 0)
	remote: Processing changes: new: 1, refs: 1, done
	remote:
	remote: New Changes:
	remote:   https://gerrit.hyperledger.org/r/6 Test commit
	remote:
	To ssh://LFID@gerrit.hyperledger.org:29418/fabric
	* [new branch]      HEAD -> refs/for/master

The gerrit server generates a link where the change can be tracked.


####Reviewing Using Gerrit####
+ Add: This button allows the change submitter to manually add names of people who should review a change; start typing a name and the system will auto-complete based on the list of people registered and with access to the system. They will be notified by email that you are requesting their input.
+ Abandon: This button is available to the submitter only; it allows a committer to abandon a change and remove it from the merge queue.
+ Change-ID: This ID is generated by Gerrit (or system). It becomes useful when the review process determines that your commit(s) have to be amended. You may submit a new version; and if the same Change-ID header (and value) are present, Gerrit will remember it and present it as another version of the same change.
+ Status: Currently, the example change is in review status, as indicated by “Needs Verified” in the upper-left corner. The list of Reviewers will all emit their opinion, voting +1 if they agree to the merge, -1 if they disagree. Gerrit users with a Maintainer role can agree to the merge or refuse it by voting +2 or -2 respectively.

Notifications are sent to the email address in your commit message’s Signed-off-by line. Visit your Gerrit dashboard, to check the progress of your requests.

The history tab in Gerrit will show you the in-line comments and the author of the review.


####Viewing Pending Changes####
Find all pending changes by clicking on the All --> Changes link in the upper-left corner, or open this link.

If you collaborate in multiple projects, you may wish to limit searching to the specific branch through the search bar in the upper-right side.

Add the filter project:fabric to limit the visible changes to only those from Hyperledger Fabric.

List all current changes you submitted, or list just those changes in need of your input by clicking on My --> Changes or open this link


####Submitting a Change to Gerrit####
Carefully review the following before submitting a change. These guidelines apply to developers that are new to open source, as well as to experienced open source developers.

#####Change Requirements#####
This section contains guidelines for submitting code changes for review. For more information on how to submit a change using Gerrit, please see Gerrit.

Changes are submitted as Git commits. Each commit must contain:

+ a short and descriptive subject line that is 72 characters or fewer, followed by a blank line.
+ a change description with your logic or reasoning for the changes, followed by a blank line
+ a Signed-off-by line, followed by a colon (Signed-off-by:)
+ a Change-Id identifier line, followed by a colon (Change-Id:). Gerrit won’t accept patches without this identifier.

A commit with the above details is considered well-formed.

All changes and topics sent to Gerrit must be well-formed. Informationally, commit messages must include:

+ what the change does,
+ why you chose that approach, and
+ how you know it works – for example, which tests you ran.

Commits must build cleanly when applied on top of each other, thus avoiding breaking bisectability. Each commit must address a single identifiable issue and must be logically self-contained.

For example: One commit fixes whitespace issues, another renames a function and a third one changes the code’s functionality. An example commit file is illustrated below in detail:

	[FAB-XXXX] A short description of your change with no period at the end

	You can add more details here in several paragraphs, but please keep each line
	width less than 80 characters. A bug fix should include the issue number.
	
	Change-Id: IF7b6ac513b2eca5f2bab9728ebd8b7e504d3cebe1
	Signed-off-by: Your Name <commit-sender@email.address>

Include the issue ID in the one line description of your commit message for readability. Gerrit will link issue IDs automatically to the corresponding entry in Jira.

Each commit must also contain the following line at the bottom of the commit message:

	Signed-off-by: Your Name <your@email.address>

The name in the Signed-off-by line and your email must match the change authorship information. Make sure your :file:.git/config is set up correctly. Always submit the full set of changes via Gerrit.

When a change is included in the set to enable other changes, but it will not be part of the final set, please let the reviewers know this.

#####Check that your change request is validated by the CI process#####
To ensure stability of the code and limit possible regressions, we use a Continuous Integration (CI) process based on Jenkins which triggers a build on several platforms and runs tests against every change request being submitted. It is your responsibility to check that your CR passes these tests. No CR will ever be merged if it fails the tests and you shouldn’t expect anybody to pay attention to your CRs until they pass the CI tests.

To check on the status of the CI process, simply look at your CR on Gerrit, following the URL that was given to you as the result of the push in the previous step. The History section at the bottom of the page will display a set of actions taken by “Hyperledger Jobbuilder” corresponding to the CI process being executed.

Upon completion, “Hyperledger Jobbuilder” will add to the CR a +1 vote if successful and a -1 vote otherwise.

In case of failure, explore the logs linked from the CR History. If you spot a problem with your CR amend your commit and push it to update it. The CI process will kick off again.

If you see nothing wrong with your CR it might be that the CI process simply failed for some reason unrelated to your change. In that case you may want to restart the CI process by posting a reply to your CR with the simple content “reverify”. Check the CI management page for additional information and options on this.


####Reviewing a Change####
1. Click on a link for incoming or outgoing review.
2. The details of the change and its current status are loaded:

	+ Status: Displays the current status of the change. In the example below, the status reads: Needs Verified.
	+ Reply: Click on this button after reviewing to add a final review message and a score, -1, 0 or +1.
	+ Patch Sets: If multiple revisions of a patch exist, this button enables navigation among revisions to see the changes. By default, the most recent revision is presented.
	+ Download: This button brings up another window with multiple options to download or checkout the current changeset. The button on the right copies the line to your clipboard. You can easily paste it into your git interface to work with the patch as you prefer.

	Underneath the commit information, the files that have been changed by this patch are displayed.

3. Click on a filename to review it. Select the code base to differentiate against. The default is Base and it will generally be what is needed.
4. The review page presents the changes made to the file. At the top of the review, the presentation shows some general navigation options. Navigate through the patch set using the arrows on the top right corner. It is possible to go to the previous or next file in the set or to return to the main change screen. Click on the yellow sticky pad to add comments to the whole file.

	The focus of the page is on the comparison window. The changes made are presented in green on the right versus the base version on the left. Double click to highlight the text within the actual change to provide feedback on a specific section of the code. Press c once the code is highlighted to add comments to that section.

5. After adding the comment, it is saved as a Draft.
6. Once you have reviewed all files and provided feedback, click the green up arrow at the top right to return to the main change page. Click the Reply button, write some final comments, and submit your score for the patch set. Click Post to submit the review of each reviewed file, as well as your final comment and score. Gerrit sends an email to the change-submitter and all listed reviewers. Finally, it logs the review for future reference. All individual comments are saved as Draft until the Post button is clicked.


####Gerrit Recommended Practices####
This document presents some best practices to help you use Gerrit more effectively. The intent is to show how content can be submitted easily. Use the recommended practices to reduce your troubleshooting time and improve participation in the community.

#####Browsing the Git Tree#####
Visit Gerrit then select Projects --> List --> SELECT-PROJECT --> Branches. Select the branch that interests you, click on gitweb located on the right-hand side. Now, gitweb loads your selection on the Git web interface and redirects appropriately.

#####Watching a Project#####
Visit Gerrit, then select Settings, located on the top right corner. Select Watched Projects and then add any projects that interest you.

#####Commit Messages#####
Gerrit follows the Git commit message format. Ensure the headers are at the bottom and don’t contain blank lines between one another. The following example shows the format and content expected in a commit message:

Brief (no more than 50 chars) one line description.

Elaborate summary of the changes made referencing why (motivation), what was changed and how it was tested. Note also any changes to documentation made to remain consistent with the code changes, wrapping text at 72 chars/line.

	Jira: FAB-100
	Change-Id: LONGHEXHASH
	Signed-off-by: Your Name your.email@example.org
	AnotherExampleHeader: An Example of another Value

The Gerrit server provides a precommit hook to autogenerate the Change-Id which is one time use.

Recommended reading: How to Write a Git Commit Message

#####Avoid Pushing Untested Work to a Gerrit Server#####
To avoid pushing untested work to Gerrit.

Check your work at least three times before pushing your change to Gerrit. Be mindful of what information you are publishing.

#####Keeping Track of Changes#####
+ Set Gerrit to send you emails:
+ Gerrit will add you to the email distribution list for a change if a developer adds you as a reviewer, or if you comment on a specific Patch Set.
+ Opening a change in Gerrit’s review interface is a quick way to follow that change.
+ Watch projects in the Gerrit projects section at Gerrit, select at least New Changes, New Patch Sets, All Comments and Submitted Changes.

Always track the projects you are working on; also see the feedback/comments mailing list to learn and help others ramp up.

#####Topic branches#####
Topic branches are temporary branches that you push to commit a set of logically-grouped dependent commits:

To push changes from REMOTE/master tree to Gerrit for being reviewed as a topic in TopicName use the following command as an example:

$ git push REMOTE HEAD:refs/for/master/TopicName

The topic will show up in the review UI and in the Open Changes List. Topic branches will disappear from the master tree when its content is merged.

#####Creating a Cover Letter for a Topic#####
You may decide whether or not you’d like the cover letter to appear in the history.

1. To make a cover letter that appears in the history, use this command:

		git commit --allow-empty

	Edit the commit message, this message then becomes the cover letter. The command used doesn’t change any files in the source tree.
2. To make a cover letter that doesn’t appear in the history follow these steps:

	a. Put the empty commit at the end of your commits list so it can be ignored without having to rebase.

	b. Now add your commits

			git commit ...
			git commit ...
			git commit ...

	c. Finally, push the commits to a topic branch. The following command is an example:

			git push REMOTE HEAD:refs/for/master/TopicName

	If you already have commits but you want to set a cover letter, create an empty commit for the cover letter and move the commit so it becomes the last commit on the list. Use the following command as an example:

			git rebase -i HEAD~#Commits

Be careful to uncomment the commit before moving it. #Commits is the sum of the commits plus your new cover letter.

#####Finding Available Topics#####
	$ ssh -p 29418 gerrit.hyperledger.org gerrit query \ status:open project:fabric branch:master \
	| grep topic: | sort -u

+ gerrit.hyperledger.org Is the current URL where the project is hosted.
+ status Indicates the topic’s current status: open , merged, abandoned, draft, merge conflict.
+ project Refers to the current name of the project, in this case fabric.
+ branch The topic is searched at this branch.
+ topic The name of an specific topic, leave it blank to include them all.
+ sort Sorts the found topics, in this case by update (-u).

#####Downloading or Checking Out a Change#####
In the review UI, on the top right corner, the Download link provides a list of commands and hyperlinks to checkout or download diffs or files.

We recommend the use of the git review plugin. The steps to install git review are beyond the scope of this document. Refer to the git review documentation for the installation process.

To check out a specific change using Git, the following command usually works:

	git review -d CHANGEID

If you don’t have Git-review installed, the following commands will do the same thing:

	git fetch REMOTE refs/changes/NN/CHANGEIDNN/VERSION \ && git checkout FETCH_HEAD

For example, for the 4th version of change 2464, NN is the first two digits (24):

	git fetch REMOTE refs/changes/24/2464/4 \ && git checkout FETCH_HEAD

#####Using Draft Branches#####
You can use draft branches to add specific reviewers before you publishing your change. The Draft Branches are pushed to refs/drafts/master/TopicName

The next command ensures a local branch is created:

	git checkout -b BRANCHNAME

The next command pushes your change to the drafts branch under TopicName:

	git push REMOTE HEAD:refs/drafts/master/TopicName

#####Using Sandbox Branches#####
You can create your own branches to develop features. The branches are pushed to the refs/sandbox/USERNAME/BRANCHNAME location.

These commands ensure the branch is created in Gerrit’s server.

	git checkout -b sandbox/USERNAME/BRANCHNAME
	git push --set-upstream REMOTE HEAD:refs/heads/sandbox/USERNAME/BRANCHNAME

Usually, the process to create content is:

+ develop the code,
+ break the information into small commits,
+ submit changes,
+ apply feedback,
+ rebase.

The next command pushes forcibly without review:

	git push REMOTE sandbox/USERNAME/BRANCHNAME

You can also push forcibly with review:

	git push REMOTE HEAD:ref/for/sandbox/USERNAME/BRANCHNAME

#####Updating the Version of a Change#####
During the review process, you might be asked to update your change. It is possible to submit multiple versions of the same change. Each version of the change is called a patch set.

Always maintain the Change-Id that was assigned. For example, there is a list of commits, c0...c7, which were submitted as a topic branch:

	git log REMOTE/master..master

	c0
	...
	c7
	
	git push REMOTE HEAD:refs/for/master/SOMETOPIC

After you get reviewers’ feedback, there are changes in c3 and c4 that must be fixed. If the fix requires rebasing, rebasing changes the commit Ids, see the rebasing section for more information. However, you must keep the same Change-Id and push the changes again:

	git push REMOTE HEAD:refs/for/master/SOMETOPIC

This new push creates a patches revision, your local history is then cleared. However you can still access the history of your changes in Gerrit on the review UI section, for each change.

It is also permitted to add more commits when pushing new versions.

#####Rebasing#####
Rebasing is usually the last step before pushing changes to Gerrit; this allows you to make the necessary Change-Ids. The Change-Ids must be kept the same.

+ squash: mixes two or more commits into a single one.
+ reword: changes the commit message.
+ edit: changes the commit content.
+ reorder: allows you to interchange the order of the commits.
+ rebase: stacks the commits on top of the master.

#####Rebasing During a Pull#####
Before pushing a rebase to your master, ensure that the history has a consecutive order.

For example, your REMOTE/master has the list of commits from a0 to a4; Then, your changes c0...c7 are on top of a4; thus:

	git log --oneline REMOTE/master..master

	a0
	a1
	a2
	a3
	a4
	c0
	c1
	...
	c7

If REMOTE/master receives commits a5, a6 and a7. Pull with a rebase as follows:

	git pull --rebase REMOTE master

This pulls a5-a7 and re-apply c0-c7 on top of them:

	$ git log --oneline REMOTE/master..master
	a0
	...
	a7
	c0
	c1
	...
	c7

#####Getting Better Logs from Git#####
Use these commands to change the configuration of Git in order to produce better logs:

	git config log.abbrevCommit true

The command above sets the log to abbreviate the commits’ hash.

	git config log.abbrev 5

The command above sets the abbreviation length to the last 5 characters of the hash.

	git config format.pretty oneline

The command above avoids the insertion of an unnecessary line before the Author line.

To make these configuration changes specifically for the current Git user, you must add the path option --global to config as follows:


####Testing####
#####Unit test#####
See building Hyperledger Fabric for unit testing instructions.

See Unit test coverage reports

To see coverage for a package and all sub-packages, execute the test with the -cover switch:

	go test ./... -cover

To see exactly which lines are not covered for a package, generate an html report with source code annotated by coverage:

	go test -coverprofile=coverage.out
	go tool cover -html=coverage.out -o coverage.html

#####System test#####
[WIP] ...coming soon

This topic is intended to contain recommended test scenarios, as well as current performance numbers against a variety of configurations.


####Coding guidelines####
#####Coding Golang#####
We code in Go™ and strictly follow the best practices and will not accept any deviations. You must run the following tools against your Go code and fix all errors and warnings: - golint - go vet - goimports


####Generating gRPC code####
If you modify any .proto files, run the following command to generate/update the respective .pb.go files.

	cd $GOPATH/src/github.com/hyperledger/fabric
	make protos


####Adding or updating Go packages####
Hyperledger Fabric uses Govendor for package management. This means that all required packages reside in the $GOPATH/src/github.com/hyperledger/fabric/vendor folder. Go will use packages in this folder instead of the GOPATH when the go install or go build commands are executed. To manage the packages in the vendor folder, we use Govendor, which is installed in the Vagrant environment. The following commands can be used for package management:

	# Add external packages.
	govendor add +external
	
	# Add a specific package.
	govendor add github.com/kardianos/osext
	
	# Update vendor packages.
	govendor update +vendor
	
	# Revert back to normal GOPATH packages.
	govendor remove +vendor
	
	# List package.
	govendor list


####Install prerequisites####
Before we begin, if you haven’t already done so, you may wish to check that you have all the prerequisites installed on the platform(s) on which you’ll be developing blockchain applications and/or operating Hyperledger Fabric.


####Getting a Linux Foundation account####
In order to participate in the development of the Hyperledger Fabric project, you will need a Linux Foundation account. You will need to use your LF ID to access to all the Hyperledger community development tools, including Gerrit, Jira and the Wiki (for editing, only).


####Getting help####
If you are looking for something to work on, or need some expert assistance in debugging a problem or working out a fix to an issue, our community is always eager to help. We hang out on Chat, IRC (#hyperledger on freenode.net) and the mailing lists. Most of us don’t bite :grin: and will be glad to help. The only silly question is the one you don’t ask. Questions are in fact a great way to help improve the project as they highlight where our documentation could be clearer.


####Reporting bugs####
If you are a user and you have found a bug, please submit an issue using JIRA. Before you create a new JIRA issue, please try to search the existing items to be sure no one else has previously reported it. If it has been previously reported, then you might add a comment that you also are interested in seeing the defect fixed.

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		If the defect is security-related, please follow the Hyperledger security bug reporting process <https://wiki.hyperledger.org/security/bug-handling-process>.
		</td>
	</tr>
</table>

If it has not been previously reported, create a new JIRA. Please try to provide sufficient information for someone else to reproduce the issue. One of the project’s maintainers should respond to your issue within 24 hours. If not, please bump the issue with a comment and request that it be reviewed. You can also post to the relevant Hyperledger Fabric channel in Hyperledger Rocket Chat. For example, a doc bug should be broadcast to #fabric-documentation, a database bug to #fabric-ledger, and so on...


####Submitting your fix####
If you just submitted a JIRA for a bug you’ve discovered, and would like to provide a fix, we would welcome that gladly! Please assign the JIRA issue to yourself, then you can submit a change request (CR).

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		If you need help with submitting your first CR, we have created a brief tutorial for you.
		</td>
	</tr>
</table>

####Fixing issues and working stories####
Review the issues list and find something that interests you. You could also check the “help-wanted” list. It is wise to start with something relatively straight forward and achievable, and that no one is already assigned. If no one is assigned, then assign the issue to yourself. Please be considerate and rescind the assignment if you cannot finish in a reasonable time, or add a comment saying that you are still actively working the issue if you need a little more time.


####Reviewing submitted Change Requests(CRs)####
Another way to contribute and learn about Hyperledger Fabric is to help the maintainers with the review of the CRs that are open. Indeed maintainers have the difficult role of having to review all the CRs that are being submitted and evaluate whether they should be merged or not. You can review the code and/or documentation changes, test the changes, and tell the submitters and maintainers what you think. Once your review and/or test is complete just reply to the CR with your findings, by adding comments and/or voting. A comment saying something like “I tried it on system X and it works” or possibly “I got an error on system X: xxx ” will help the maintainers in their evaluation. As a result, maintainers will be able to process CRs faster and everybody will gain from it.

Just browse through the open CRs on Gerrit to get started.


####Making Feature/Enhancement Proposals####
Review JIRA. to be sure that there isn’t already an open (or recently closed) proposal for the same function. If there isn’t, to make a proposal we recommend that you open a JIRA Epic, Story or Improvement, whichever seems to best fit the circumstance and link or inline a “one pager” of the proposal that states what the feature would do and, if possible, how it might be implemented. It would help also to make a case for why the feature should be added, such as identifying specific use case(s) for which the feature is needed and a case for what the benefit would be should the feature be implemented. Once the JIRA issue is created, and the “one pager” either attached, inlined in the description field, or a link to a publicly accessible document is added to the description, send an introductory email to the hyperledger-fabric@lists.hyperledger.org mailing list linking the JIRA issue, and soliciting feedback.

Discussion of the proposed feature should be conducted in the JIRA issue itself, so that we have a consistent pattern within our community as to where to find design discussion.

Getting the support of three or more of the Hyperledger Fabric maintainers for the new feature will greatly enhance the probability that the feature’s related CRs will be merged.


####Setting up development environment####
Next, try building the project in your local development environment to ensure that everything is set up correctly.


####What makes a good change request?####
+ One change at a time. Not five, not three, not ten. One and only one. Why? Because it limits the blast area of the change. If we have a regression, it is much easier to identify the culprit commit than if we have some composite change that impacts more of the code.
+ Include a link to the JIRA story for the change. Why? Because a) we want to track our velocity to better judge what we think we can deliver and when and b) because we can justify the change more effectively. In many cases, there should be some discussion around a proposed change and we want to link back to that from the change itself.
+ Include unit and integration tests (or changes to existing tests) with every change. This does not mean just happy path testing, either. It also means negative testing of any defensive code that it correctly catches input errors. When you write code, you are responsible to test it and provide the tests that demonstrate that your change does what it claims. Why? Because without this we have no clue whether our current code base actually works.
+ Unit tests should have NO external dependencies. You should be able to run unit tests in place with go test or equivalent for the language. Any test that requires some external dependency (e.g. needs to be scripted to run another component) needs appropriate mocking. Anything else is not unit testing, it is integration testing by definition. Why? Because many open source developers do Test Driven Development. They place a watch on the directory that invokes the tests automagically as the code is changed. This is far more efficient than having to run a whole build between code changes. See this definition of unit testing for a good set of criteria to keep in mind for writing effective unit tests.
+ Minimize the lines of code per CR. Why? Maintainers have day jobs, too. If you send a 1,000 or 2,000 LOC change, how long do you think it takes to review all of that code? Keep your changes to < 200-300 LOC, if possible. If you have a larger change, decompose it into multiple independent changess. If you are adding a bunch of new functions to fulfill the requirements of a new capability, add them separately with their tests, and then write the code that uses them to deliver the capability. Of course, there are always exceptions. If you add a small change and then add 300 LOC of tests, you will be forgiven;-) If you need to make a change that has broad impact or a bunch of generated code (protobufs, etc.). Again, there can be exceptions.

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		Large change requests, e.g. those with more than 300 LOC are more likely than not going to receive a -2, and you’ll be asked to refactor the change to conform with this guidance.
		</td>
	</tr>
</table>

+ Do not stack change requests (e.g. submit a CR from the same local branch as your previous CR) unless they are related. This will minimize merge conflicts and allow changes to be merged more quickly. If you stack requests your subsequent requests may be held up because of review comments in the preceding requests.
+ Write a meaningful commit message. Include a meaningful 50 (or less) character title, followed by a blank line, followed by a more comprehensive description of the change. Each change MUST include the JIRA identifier corresponding to the change (e.g. [FAB-1234]). This can be in the title but should also be in the body of the commit message. See the complete requirements for an acceptable change request.

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		That Gerrit will automatically create a hyperlink to the JIRA item. e.g.
		<p>
		[FAB-1234] fix foobar() panic
		<p>
		Fix [FAB-1234] added a check to ensure that when foobar(foo string)
		is called, that there is a non-empty string argument.
		</td>
	</tr>
</table>

Finally, be responsive. Don’t let a change request fester with review comments such that it gets to a point that it requires a rebase. It only further delays getting it merged and adds more work for you - to remediate the merge conflicts.


####Communication####
We use RocketChat for communication and Google Hangouts™ for screen sharing between developers. Our development planning and prioritization is done in JIRA, and we take longer running discussions/decisions to the mailing list.


####Maintainers####
The project’s maintainers are responsible for reviewing and merging all patches submitted for review and they guide the over-all technical direction of the project within the guidelines established by the Hyperledger Technical Steering Committee (TSC).

#####Becoming a maintainer#####
This project is managed under an open governance model as described in our charter. Projects or sub-projects will be lead by a set of maintainers. New sub-projects can designate an initial set of maintainers that will be approved by the top-level project’s existing maintainers when the project is first approved. The project’s maintainers will, from time-to-time, consider adding or removing a maintainer. An existing maintainer can submit a change set to the MAINTAINERS.rst file. A nominated Contributor may become a Maintainer by a majority approval of the proposal by the existing Maintainers. Once approved, the change set is then merged and the individual is added to (or alternatively, removed from) the maintainers group. Maintainers may be removed by explicit resignation, for prolonged inactivity (3 or more months), or for some infraction of the code of conduct or by consistently demonstrating poor judgement. A maintainer removed for inactivity should be restored following a sustained resumption of contributions and reviews (a month or more) demonstrating a renewed commitment to the project.


####Legal stuff####
Note: Each source file must include a license header for the Apache Software License 2.0. See the template of the license header.

We have tried to make it as easy as possible to make contributions. This applies to how we handle the legal aspects of contribution. We use the same approach—the Developer’s Certificate of Origin 1.1 (DCO)—that the Linux® Kernel community uses to manage code contributions.

We simply ask that when submitting a patch for review, the developer must include a sign-off statement in the commit message.

Here is an example Signed-off-by line, which indicates that the submitter accepts the DCO:

	Signed-off-by: John Doe <john.doe@example.com>

You can include this automatically when you commit a change to your local git repository using git commit -s.


###十、词汇表###
Terminology is important, so that all Hyperledger Fabric users and developers agree on what we mean by each specific term. What is chaincode, for example. The documentation will reference the glossary as needed, but feel free to read the entire thing in one sitting if you like; it’s pretty enlightening!


####Anchor Peer####
A peer node on a channel that all other peers can discover and communicate with. Each Member on a channel has an anchor peer (or multiple anchor peers to prevent single point of failure), allowing for peers belonging to different Members to discover all existing peers on a channel.


####Block####
An ordered set of transactions that is cryptographically linked to the preceding block(s) on a channel.


####Chain####
The ledger’s chain is a transaction log structured as hash-linked blocks of transactions. Peers receive blocks of transactions from the ordering service, mark the block’s transactions as valid or invalid based on endorsement policies and concurrency violations, and append the block to the hash chain on the peer’s file system.


####Chaincode####
Chaincode is software, running on a ledger, to encode assets and the transaction instructions (business logic) for modifying the assets.


####Channel####
A channel is a private blockchain overlay which allows for data isolation and confidentiality. A channel-specific ledger is shared across the peers in the channel, and transacting parties must be properly authenticated to a channel in order to interact with it. Channels are defined by a Configuration-Block.


####Commitment####
Each Peer on a channel validates ordered blocks of transactions and then commits (writes/appends) the blocks to its replica of the channel Ledger. Peers also mark each transaction in each block as valid or invalid.


####Concurrency Control Version Check####
Concurrency Control Version Check is a method of keeping state in sync across peers on a channel. Peers execute transactions in parallel, and before commitment to the ledger, peers check that the data read at execution time has not changed. If the data read for the transaction has changed between execution time and commitment time, then a Concurrency Control Version Check violation has occurred, and the transaction is marked as invalid on the ledger and values are not updated in the state database.


####Configuration Block####
Contains the configuration data defining members and policies for a system chain (ordering service) or channel. Any configuration modifications to a channel or overall network (e.g. a member leaving or joining) will result in a new configuration block being appended to the appropriate chain. This block will contain the contents of the genesis block, plus the delta.


####Consensus####
A broader term overarching the entire transactional flow, which serves to generate an agreement on the order and to confirm the correctness of the set of transactions constituting a block.


####Current State####
The current state of the ledger represents the latest values for all keys ever included in its chain transaction log. Peers commit the latest values to ledger current state for each valid transaction included in a processed block. Since current state represents all latest key values known to the channel, it is sometimes referred to as World State. Chaincode executes transaction proposals against current state data.


####Dynamic Membership####
Hyperledger Fabric supports the addition/removal of members, peers, and ordering service nodes, without compromising the operationality of the overall network. Dynamic membership is critical when business relationships adjust and entities need to be added/removed for various reasons.


####Endorsement####
Refers to the process where specific peer nodes execute a chaincode transaction and return a proposal response to the client application. The proposal response includes the chaincode execution response message, results (read set and write set), and events, as well as a signature to serve as proof of the peer’s chaincode execution. Chaincode applications have corresponding endorsement policies, in which the endorsing peers are specified.


####Endorsement policy####
Defines the peer nodes on a channel that must execute transactions attached to a specific chaincode application, and the required combination of responses (endorsements). A policy could require that a transaction be endorsed by a minimum number of endorsing peers, a minimum percentage of endorsing peers, or by all endorsing peers that are assigned to a specific chaincode application. Policies can be curated based on the application and the desired level of resilience against misbehavior (deliberate or not) by the endorsing peers. A transaction that is submitted must satisfy the endorsement policy before being marked as valid by committing peers. A distinct endorsement policy for install and instantiate transactions is also required.


####Hyperledger Fabric CA####
Hyperledger Fabric CA is the default Certificate Authority component, which issues PKI-based certificates to network member organizations and their users. The CA issues one root certificate (rootCert) to each member and one enrollment certificate (ECert) to each authorized user.


####Genesis Block####
The configuration block that initializes a blockchain network or channel, and also serves as the first block on a chain.


####Gossip Protocol####
The gossip data dissemination protocol performs three functions: 1) manages peer discovery and channel membership; 2) disseminates ledger data across all peers on the channel; 3) syncs ledger state across all peers on the channel. Refer to the Gossip topic for more details.


####Initialize####
A method to initialize a chaincode application.


####Install####
The process of placing a chaincode on a peer’s file system.


####Instantiate####
The process of starting and initializing a chaincode application on a specific channel. After instantiation, peers that have the chaincode installed can accept chaincode invocations.


####Invoke####
Used to call chaincode functions. A client application invokes chaincode by sending a transaction proposal to a peer. The peer will execute the chaincode and return an endorsed proposal response to the client application. The client application will gather enough proposal responses to satisfy an endorsement policy, and will then submit the transaction results for ordering, validation, and commit. The client application may choose not to submit the transaction results. For example if the invoke only queried the ledger, the client application typically would not submit the read-only transaction, unless there is desire to log the read on the ledger for audit purpose. The invoke includes a channel identifier, the chaincode function to invoke, and an array of arguments.


####Leading Peer####
Each Member can own multiple peers on each channel that it subscribes to. One of these peers is serves as the leading peer for the channel, in order to communicate with the network ordering service on behalf of the member. The ordering service “delivers” blocks to the leading peer(s) on a channel, who then distribute them to other peers within the same member cluster.


####Ledger####
A ledger is a channel’s chain and current state data which is maintained by each peer on the channel.


####Member####
A legally separate entity that owns a unique root certificate for the network. Network components such as peer nodes and application clients will be linked to a member.


####Membership Service Provider####
The Membership Service Provider (MSP) refers to an abstract component of the system that provides credentials to clients, and peers for them to participate in a Hyperledger Fabric network. Clients use these credentials to authenticate their transactions, and peers use these credentials to authenticate transaction processing results (endorsements). While strongly connected to the transaction processing components of the systems, this interface aims to have membership services components defined, in such a way that alternate implementations of this can be smoothly plugged in without modifying the core of transaction processing components of the system.


####Membership Services####
Membership Services authenticates, authorizes, and manages identities on a permissioned blockchain network. The membership services code that runs in peers and orderers both authenticates and authorizes blockchain operations. It is a PKI-based implementation of the Membership Services Provider (MSP) abstraction.


####Ordering Service####
A defined collective of nodes that orders transactions into a block. The ordering service exists independent of the peer processes and orders transactions on a first-come-first-serve basis for all channel’s on the network. The ordering service is designed to support pluggable implementations beyond the out-of-the-box SOLO and Kafka varieties. The ordering service is a common binding for the overall network; it contains the cryptographic identity material tied to each Member.


####Peer####
A network entity that maintains a ledger and runs chaincode containers in order to perform read/write operations to the ledger. Peers are owned and maintained by members.


####Policy####
There are policies for endorsement, validation, chaincode management and network/channel management.


####Proposal####
A request for endorsement that is aimed at specific peers on a channel. Each proposal is either an instantiate or an invoke (read/write) request.


####Query####
A query is a chaincode invocation which reads the ledger current state but does not write to the ledger. The chaincode function may query certain keys on the ledger, or may query for a set of keys on the ledger. Since queries do not change ledger state, the client application will typically not submit these read-only transactions for ordering, validation, and commit. Although not typical, the client application can choose to submit the read-only transaction for ordering, validation, and commit, for example if the client wants auditable proof on the ledger chain that it had knowledge of specific ledger state at a certain point in time.


####Software Development Kit(SDK)####
The Hyperledger Fabric client SDK provides a structured environment of libraries for developers to write and test chaincode applications. The SDK is fully configurable and extensible through a standard interface. Components, including cryptographic algorithms for signatures, logging frameworks and state stores, are easily swapped in and out of the SDK. The SDK provides APIs for transaction processing, membership services, node traversal and event handling.

Currently, the two officially supported SDKs are for Node.js and Java, while three more – Python, Go and REST – are not yet official but can still be downloaded and tested.


####State Database####
Current state data is stored in a state database for efficient reads and queries from chaincode. Supported databases include levelDB and couchDB.


####System Chain####
Contains a configuration block defining the network at a system level. The system chain lives within the ordering service, and similar to a channel, has an initial configuration containing information such as: MSP information, policies, and configuration details. Any change to the overall network (e.g. a new org joining or a new ordering node being added) will result in a new configuration block being added to the system chain.

The system chain can be thought of as the common binding for a channel or group of channels. For instance, a collection of financial institutions may form a consortium (represented through the system chain), and then proceed to create channels relative to their aligned and varying business agendas.


####Transaction####
Invoke or instantiate results that are submitted for ordering, validation, and commit. Invokes are requests to read/write data from the ledger. Instantiate is a request to start and initialize a chaincode on a channel. Application clients gather invoke or instantiate responses from endorsing peers and package the results and endorsements into a transaction that is submitted for ordering, validation, and commit.


###十一、发行说明###
####v1.1.0-March 15,2018####
The v1.1 release includes all of the features delivered in v1.1.0-preview and v1.1.0-alpha.

Additionally, there are feature improvements, bug fixes, documentation and test coverage improvements, UX improvements based on user feedback and changes to address a variety of static scan findings (unused code, static security scanning, spelling, linting and more).

Updated to Go version 1.9.2. Updated baseimage version to 0.4.6.


####Known Vulnerabilities####
none


####Resolved Vulnerabilities####
https://jira.hyperledger.org/browse/FAB-4824 https://jira.hyperledger.org/browse/FAB-5406


####Known Issues & Workarounds####
The fabric-ccenv image which is used to build chaincode, currently includes the github.com/hyperledger/fabric/core/chaincode/shim (“shim”) package. This is convenient, as it provides the ability to package chaincode without the need to include the “shim”. However, this may cause issues in future releases (and/or when trying to use packages which are included by the “shim”).

In order to avoid any issues, users are advised to manually vendor the “shim” package with their chaincode prior to using the peer CLI for packaging and/or for installing chaincode.

Please refer to FAB-5177 for more details, and kindly be aware that given the above, we may end up changing the fabric-ccenv in the future.


####v1.1.0-rc1-March 1,2018####
The v1.1 release candidate 1 (rc1) includes all of the features delivered in v1.1.0-preview and v1.1.0-alpha.

Additionally, there are feature improvements, bug fixes, documentation and test coverage improvements, UX improvements based on user feedback and changes to address a variety of static scan findings (unused code, static security scanning, spelling, linting and more).


####Known Vulnerabilities####
none


####Resolved Vulnerabilities####
none


####Known Issues & Workarounds####
The fabric-ccenv image which is used to build chaincode, currently includes the github.com/hyperledger/fabric/core/chaincode/shim (“shim”) package. This is convenient, as it provides the ability to package chaincode without the need to include the “shim”. However, this may cause issues in future releases (and/or when trying to use packages which are included by the “shim”).

In order to avoid any issues, users are advised to manually vendor the “shim” package with their chaincode prior to using the peer CLI for packaging and/or for installing chaincode.

Please refer to FAB-5177 for more details, and kindly be aware that given the above, we may end up changing the fabric-ccenv in the future.


####v1.1.0-alpha-January 25,2018####
This is a feature-complete alpha release of the up-coming 1.1 release. The 1.1 release includes the following new major features:

+ FAB-6911 - Event service for blocks
+ FAB-5481 - Event service for block transaction events
+ FAB-5300 - Certificate Revocation List from CA
+ FAB-3067 - Peer management of CouchDB indexes
+ FAB-6715 - Mutual TLS between all components
+ FAB-5556 - Rolling Upgrade via configured capabilities
+ FAB-2331 - Node.js Chaincode support
+ FAB-5363 - Node.js SDK Connection Profile
+ FAB-830 - Encryption library for chaincode
+ FAB-5346 - Attribute-based Access Control
+ FAB-6089 - Chaincode APIs for creator identity
+ FAB-6421 - Performance improvements

Additionally, there are feature improvements, bug fixes, documentation and test coverage improvements, UX improvements based on user feedback and changes to address a variety of static scan findings (unused code, static security scanning, spelling, linting and more).


####Known Vulnerabilities####
none


####Resolved Vulnerabilities####
none


####Known Issues & Workarounds####
The fabric-ccenv image which is used to build chaincode, currently includes the github.com/hyperledger/fabric/core/chaincode/shim (“shim”) package. This is convenient, as it provides the ability to package chaincode without the need to include the “shim”. However, this may cause issues in future releases (and/or when trying to use packages which are included by the “shim”).

In order to avoid any issues, users are advised to manually vendor the “shim” package with their chaincode prior to using the peer CLI for packaging and/or for installing chaincode.

Please refer to FAB-5177 for more details, and kindly be aware that given the above, we may end up changing the fabric-ccenv in the future.


####v1.1.0-preview-November 1,2017####
This is a preview release of the up-coming 1.1 release. We are not feature complete for 1.1 just yet, but we wanted to get the following functionality published to gain some early community feedback on the following features:

+ FAB-2331 - Node.js Chaincode
+ FAB-5363 - Node.js SDK Connection Profile
+ FAB-830 - Encryption library for chaincode
+ FAB-5346 - Attribute-based Access Control
+ FAB-6089 - Chaincode APIs to retrieve creator cert info
+ FAB-6421 - Performance improvements

Additionally, there are the usual bug fixes, documentation and test coverage improvements, UX improvements based on user feedback and changes to address a variety of static scan findings (unused code, static security scanning, spelling, linting and more).


####Known Vulnerabilities####
none


####Resolved Vulnerabilities####
none


####Known Issues & Workarounds####
The fabric-ccenv image which is used to build chaincode, currently includes the github.com/hyperledger/fabric/core/chaincode/shim (“shim”) package. This is convenient, as it provides the ability to package chaincode without the need to include the “shim”. However, this may cause issues in future releases (and/or when trying to use packages which are included by the “shim”).

In order to avoid any issues, users are advised to manually vendor the “shim” package with their chaincode prior to using the peer CLI for packaging and/or for installing chaincode.

Please refer to FAB-5177 for more details, and kindly be aware that given the above, we may end up changing the fabric-ccenv in the future.


####v1.0.4-October 31,2017####
Bug fixes, documentation and test coverage improvements, UX improvements based on user feedback and changes to address a variety of static scan findings (unused code, static security scanning, spelling, linting and more).


####Known Vulnerabilities####
none


####Resolved Vulnerabilities####
none


####Known Issues & Workarounds####
The fabric-ccenv image which is used to build chaincode, currently includes the github.com/hyperledger/fabric/core/chaincode/shim (“shim”) package. This is convenient, as it provides the ability to package chaincode without the need to include the “shim”. However, this may cause issues in future releases (and/or when trying to use packages which are included by the “shim”).

In order to avoid any issues, users are advised to manually vendor the “shim” package with their chaincode prior to using the peer CLI for packaging and/or for installing chaincode.

Please refer to https://jira.hyperledger.org/browse/FAB-5177 for more details, and kindly be aware that given the above, we may end up changing the fabric-ccenv in the future.


####v1.0.3-October 3,2017####
Bug fixes, documentation and test coverage improvements, UX improvements based on user feedback and changes to address a variety of static scan findings (unused code, static security scanning, spelling, linting and more).


####Known Vulnerabilities####
none


####Resolved Vulnerabilities####
none


####Known Issues & Workarounds####
The fabric-ccenv image which is used to build chaincode, currently includes the github.com/hyperledger/fabric/core/chaincode/shim (“shim”) package. This is convenient, as it provides the ability to package chaincode without the need to include the “shim”. However, this may cause issues in future releases (and/or when trying to use packages which are included by the “shim”).

In order to avoid any issues, users are advised to manually vendor the “shim” package with their chaincode prior to using the peer CLI for packaging and/or for installing chaincode.

Please refer to https://jira.hyperledger.org/browse/FAB-5177 for more details, and kindly be aware that given the above, we may end up changing the fabric-ccenv in the future.


####v1.0.2-August 31,2017####
Bug fixes, documentation and test coverage improvements, UX improvements based on user feedback and changes to address a variety of static scan findings (unused code, static security scanning, spelling, linting and more).


####Known Vulnerabilities####
none


####Resolved Vulnerabilities####
https://jira.hyperledger.org/browse/FAB-5753 https://jira.hyperledger.org/browse/FAB-5899


####Known Issues & Workarounds####
The fabric-ccenv image which is used to build chaincode, currently includes the github.com/hyperledger/fabric/core/chaincode/shim (“shim”) package. This is convenient, as it provides the ability to package chaincode without the need to include the “shim”. However, this may cause issues in future releases (and/or when trying to use packages which are included by the “shim”).

In order to avoid any issues, users are advised to manually vendor the “shim” package with their chaincode prior to using the peer CLI for packaging and/or for installing chaincode.

Please refer to https://jira.hyperledger.org/browse/FAB-5177 for more details, and kindly be aware that given the above, we may end up changing the fabric-ccenv in the future.


####v1.0.1-August 5,2017####
Bug fixes, documentation and test coverage improvements, UX improvements based on user feedback and changes to address a variety of static scan findings (unused code, static security scanning, spelling, linting and more).


####Known Vulnerabilities####
none


####Resolved Vulnerabilities####
https://jira.hyperledger.org/browse/FAB-5329 https://jira.hyperledger.org/browse/FAB-5330 https://jira.hyperledger.org/browse/FAB-5353 https://jira.hyperledger.org/browse/FAB-5529 https://jira.hyperledger.org/browse/FAB-5606 https://jira.hyperledger.org/browse/FAB-5627

####Known Issues & Workarounds####
The fabric-ccenv image which is used to build chaincode, currently includes the github.com/hyperledger/fabric/core/chaincode/shim (“shim”) package. This is convenient, as it provides the ability to package chaincode without the need to include the “shim”. However, this may cause issues in future releases (and/or when trying to use packages which are included by the “shim”).

In order to avoid any issues, users are advised to manually vendor the “shim” package with their chaincode prior to using the peer CLI for packaging and/or for installing chaincode.

Please refer to https://jira.hyperledger.org/browse/FAB-5177 for more details, and kindly be aware that given the above, we may end up changing the fabric-ccenv in the future.


####v1.0.0-July 11,2017####
Bug fixes, documentation and test coverage improvements, UX improvements based on user feedback and changes to address a variety of static scan findings (removal of unused code, static security scanning, spelling, linting and more).


####Known Vulnerabilities####
none


####Resolved Vulnerabilities####
https://jira.hyperledger.org/browse/FAB-5207


####Known Issues & Workarounds####
The fabric-ccenv image which is used to build chaincode, currently includes the github.com/hyperledger/fabric/core/chaincode/shim (“shim”) package. This is convenient, as it provides the ability to package chaincode without the need to include the “shim”. However, this may cause issues in future releases (and/or when trying to use packages which are included by the “shim”).

In order to avoid any issues, users are advised to manually vendor the “shim” package with their chaincode prior to using the peer CLI for packaging and/or for installing chaincode.

Please refer to https://jira.hyperledger.org/browse/FAB-5177 for more details, and kindly be aware that given the above, we may end up changing the fabric-ccenv in the future.


####v1.0.0-rc1-June 23,2017####
Bug fixes, documentation and test coverage improvements, UX improvements based on user feedback and changes to address a variety of static scan findings (unused code, static security scanning, spelling, linting and more).


####Known Vulnerabilities####
none


####Resolved Vulnerabilities####
https://jira.hyperledger.org/browse/FAB-4856 https://jira.hyperledger.org/browse/FAB-4848 https://jira.hyperledger.org/browse/FAB-4751 https://jira.hyperledger.org/browse/FAB-4626 https://jira.hyperledger.org/browse/FAB-4567 https://jira.hyperledger.org/browse/FAB-3715


####Known Issues & Workarounds####
none


####v1.0.0-beta-June 8,2017####
Bug fixes, documentation and test coverage improvements, UX improvements based on user feedback and changes to address a variety of static scan findings (unused code, static security scanning, spelling, linting and more).

Upgraded to latest version (a precursor to 1.4.0) of gRPC-go and implemented keep-alive feature for improved resiliency.

Added a new tool configtxlator to enable users to translate the contents of a channel configuration transaction into a human readable form.


####Known Vulnerabilities####
none


####Resolved Vulnerabilities####
none


####Known Issues & Workarounds####
BCCSP content in the configtx.yaml has been removed. This change will cause a panic when running configtxgen tool with a configtx.yaml file that includes the removed BCCSP content.

Java Chaincode support has been disabled until post 1.0.0 as it is not yet fully mature. It may be re-enabled for experimentation by cloning the hyperledger/fabric repository, reversing this commit and building your own fork.


####v1.0.0-alpha2####
The second alpha release of the v1.0.0 Hyperledger Fabric. The code is now feature complete. From now until the v1.0.0 release, the community is focused on documentation improvements, testing, hardening, bug fixing and tooling. We will be releasing successive release candidates periodically as the release firms up.


####v1.0.0-alpha-March 16,2017####
The first alpha release of the v1.0.0 Hyperledger Fabric. The code is being made available to developers to begin exploring the v1.0 architecture.


#####v0.6-preview September 16, 2016#####
A developer preview release of the Hyperledger Fabric intended to exercise the release logistics and stabilize a set of capabilities for developers to try out. This will be the last release under the original architecture. All subsequent releases will deliver on the v1.0 architecture.


####v0.5-developer-preview-June 17,2016####
A developer preview release of the Hyperledger Fabric intended to exercise the release logistics and stabilize a set of capabilities for developers to try out.

Key features:

Permissioned blockchain with immediate finality Chaincode (aka smart contract) execution environments Docker container (user chaincode) In-process with peer (system chaincode) Pluggable consensus with PBFT, NOOPS (development mode), SIEVE (prototype) Event framework supports pre-defined and custom events Client SDK (Node.js), basic REST APIs and CLIs Known Key Bugs and work in progress

+ 1895 - Client SDK interfaces may crash if wrong parameter specified
+ 1901 - Slow response after a few hours of stress testing
+ 1911 - Missing peer event listener on the client SDK
+ 889 - The attributes in the TCert are not encrypted. This work is still on-going


###十二、仍有问题？###
We try to maintain a comprehensive set of documentation for various audiences. However, we realize that often there are questions that remain unanswered. For any technical questions relating to Hyperledger Fabric not answered here, please use StackOverflow. Another approach to getting your questions answered to send an email to the mailing list (hyperledger-fabric@lists.hyperledger.org), or ask your questions on RocketChat (an alternative to Slack) on the #fabric or #fabric-questions channel.

<table>
	<tr>
		<td bgcolor=#6A5ACD>
			<img src="images/tip1.png" style="height:16px;width=16px;"> 注意
		</td>
	</tr>
	<tr>
		<td bgcolor=#7FFFD4>
		Please, when asking about problems you are facing tell us about the environment in which you are experiencing those problems including the OS, which version of Docker you are using, etc.
		</td>
	</tr>
</table>


###十三、状态###
Hyperledger Fabric is in the Active state. For more information on the history of this project see our wiki page. Information on what Active entails can be found in the Hyperledger Project Lifecycle document.


