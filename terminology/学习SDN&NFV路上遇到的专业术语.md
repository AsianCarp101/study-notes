###学习SDN/NFV路上遇到的专业术语
>引用自：http://m.sanwen8.cn/p/142P453.html
>http://toutiao.com/i6285483616545800705/

**`SDN:`** `软件定义网络（Software Defined Network,SDN）`，是一种新型的网络创新架构，是网络虚拟化的一种实现方式，其核心技术 `OpenFlow` 通过将网络设备的**控制面**和**数据面**分离开来，从而实现了网络流量的灵活控制，使网络作为管道变得更加智能。

**`NFV:`** `网络功能虚拟化（Network Function Virtualization）`，通过X86等通用硬件以及虚拟化技术，来承载很多功能的软件处理。从而降低网络昂贵的设备成本，可通过 `软硬件解耦` 及 `功能抽象`，使网络设备不在依赖于专用硬件，资源可以充分灵活分享，实现新业务的快速开发和部署，并基于实际业务需求进行自动部署、弹性伸缩、故障隔离和自愈等。

**`VNF`** `Virtualized Network Function`（VNF）虚拟网络功能。NFV技术主要由3个部分构成，`VNF`、`NFVI`（网络功能虚拟化基础设施NFV Infrastructure）和 `MANO`（NFV管理与编排，Management and Orchestration）。虚拟网络层是共享同一物力OTS服务器的VNF集。对应的就是各个网元功能的软件实现，比如EPC网元，IMS网元等逻辑实现。

**`NFVI:`** `NFV Infrastructure`(网络功能虚拟化基础设施层)，从云计算的角度看，就是一个 `资源池(Resource Pool)`。NFVI需要将物理计算/存储/交换资源通过虚拟化转换为虚拟的计算/存储/交换资源池。NFVI映射到物理基础设施就是多个地理上分散的数据中心，通过高速通信网连接起来。

**`NFV MANO`** `NFV管理和业务编排`（**Management and Orchestration**）--管理和控制层，主要集中在贯穿整个NFV生命周期的虚拟化管理功能。每个组件有包含了一些不同的NFV技术，企业通过使用这些技术可以获得更好的灵活性、可扩展性和高效性。基于不同的 `服务等级协议`（Service Level Agreements，SLAs），NFV MANO运营支持层负责“公平”的分配物理资源，同时还负责冗余管理、错误管理和弹性调整等，相当于目前的OSS/BSS系统。

**`OpenFlow:`** 是一种新的网络交换模型。OpenFlow网络由 `OpenFlowSwitch` （OpenFlow交换机）、 `FlowVisor` （网络虚拟化层）和 `Controller` （控制器）三部分组成。OpenFlow交换机进行数据层的转发；FlowVisor对网络进行虚拟化；Controller对网络集中控制，实现控制层的功能。OpenFlow交换机由 `FlowTable` （流表）、`SecurChannel` （安全通道）和 `OpenFlowProtocol` （协议）三部分组成。`FlowTable` 流表有很多个流表项组成，每个流表项就是一个转发规则。进入交换机的数据包通过查询流表来获得转发的目的端口。`Secure Channel` ：安全通道是连接OpenFlow交换机到控制器的接口。控制器通过这个接口控制和管理交换机，同时控制器接收来自交换机的事件并向交换机发送数据包。交换机和控制器通过安全通道进行通信，而且所有的信息必须按照OpenFlow协议规定的格式来执行。

**`OpenFlow协议:`** 用来描述**控制器**和**交换机**之间交互所用信息的标准，以及控制器和交换机的接口标准。协议的核心部分是用于OpenFlow协议信息结构的集合。OpenFlow协议支持三种信息类型：`Controller-to-Switch`，`Asynchronous` 和 `Symmetric`，每一个类型都有多个子类型。Controller-to-Switch信息由控制器发起并且直接用于检测交换机的状态。Asynchronous信息由交换机发起并通常用于更新控制器的网络事件和改变交换机的状态。Symmetric信息可以在没有请求的情况下由控制器和交换机发起。

**`Vendor SDN`** 供应商SDN。随着SDN的发展很多厂商都推出了自己的SDN控制器，如VMware的NSX Controller，Juniper瞻博网络的NorthStar和Contrail SDN Controller，华为的Smart Network Controller，惠普的Virtual Application Networks SDN Controller，戴尔的Active Fabric Controller，思科的Application Policy Infrastructure Controller，博科的Vyatta Controller等。

**`OSS`** `运营商支持系统`（Operation Support System）。OSS是一个综合的业务运营和管理平台，同时也是真正融合了传统IP数据业务与移动增值业务的综合管理平台。OSS是电信运营商的一体化、信息资源共享的支持系统，它主要由网络管理、系统管理、计费、营业、账务和客户服务等部分组成，系统间通过统一的信息总线有机整合在一起。它不仅能在帮助运营商制订符合自身特点的运营支持系统的同时帮助确定系统的发展方向，还能帮助用户制订系统的整合标准，改善和提升用户的服务水平。

**`LSO`** `生命周期服务编排`（**Lifecycle Service Orchestration**），一个LSO平台能够处理从客户订单到服务交付的控制，从数据采集到确保性能等级，从故障修复到提供使用报告，再到为客户提供各种分析报告等等一切业务。MEF为完成跨越混合网络基础设施的端到端的业务管理提出的新方法和新架构。利用对产品、服务、资源的抽象化屏蔽了下面网络的复杂性。1）跨越物理和虚拟两网，支持真正端到端的业务管理，有助于现有烟囱时网络和管理系统向未来水平网络架构和管理架构的平滑演进。2）实现网络架构的自动化管理，节约40%的运营成本，减少约80%的业务开通时间。`MEF`基于其第三网络愿景列出了LSO的六大高层次功能：实施、控制、性能、保障、使用和分析。LSO的愿景颇为引人注目，它解决了日益复杂的网络服务带来的问题，这超越了单纯的带宽和其他基本连接问题，例如延迟性、服务保障和计费成本等，并努力满足客户需求。

**`MEF`** `城域以太网论坛`（MEF）是一个专注于解决城域网以太网技术问题的非盈利性组织。MEF主要从四个方面展开技术工作：城域以太网的架构、城域以太网提供的业务、城域以太网的保护和QoS、城域以太网的管理。MEF的主旨是促进光学以太网作为城域网的选择技术在世界范围内的广泛应用。

**`Docker容器`** 是一个开源的应用容器引擎，让开发者可以打包他们的应用以及依赖包到一个可移植的容器中，然后发布到任何流行的Linux机器上，也可实现虚拟化。容器是完全使用沙箱机制，相互之间不会有任何借口。几乎没有性能开销，可以很容易地在机器和数据中心中运行。最重要的是，他们不依懒于任何语言、框架包括系统。容器中直接跑应用进程，省却多个专用客户操作系统和hypervisor层，架构简单，性能优良（接近裸机），扩展性迁移性好（可运行于任意平台），部署快（启动时间秒级），效率高（内核级虚拟化），管理简单，运行成本低。可能的应用前景：
		1. 容器化面向上层的应用进程
		2. 基于虚拟机的虚拟化面向底层硬件
		3. 多数业务系统适用于虚拟机+Docker组合


**`ODL`** `OpenDaylight` （ODL）是一款基于Java开发的SDN控制器，包括网络应用、编排与服务，控制器平台，南向接口及协议，数据平面单元等。OpenDaylight是Linux基金会负责管理的开源项目，旨在建设一个开放的SDN网络系统控制平台，推动SDN和NFV技术的创新实施和透明化。

**`ONOS`** `ONOS` 是2014年12月由斯坦福大学和加州大学伯克利分校SDN创立的开源社区，AT&T、NTT等电信运营商为其主要的合作伙伴。ONOS旨在设计一款可用性高、性能优、抽象性和可扩展性好的运营商级的开源SDN网络操作系统。ONOS具有以下几大特点：
		1. 全分布式控制架构，支持分布式统一逻辑网络视图
		2. 支持OpenFlow和白盒硬件
		3. 支持插件式管理等

**`OTT`** `Over The Top`（OTT），指互联网公司越过运营商，发展基于开放互联网的各种视频及数据服务业务。


**`CPE`**  `Customer Premise Equipment` 客户终端设备，FTTX家客业务的客户端，用于提供家庭客户的有线宽带、IPTV、VOIP等业务的综合接入。CPE上联PON传输网络，下联具体业务设备，完成接入网络与用户设备的连接。

**`BNG`** `Broadband Network Gateway`（BNG）宽带网络网关控制设备，BRAS和SR都属于BNG的表现形式，BNG主要用于用户和业务控制，包括分配地址。


**`EPC`** `Evolved Packet Core`（EPC）一个全IP的分组核心网。该系统的特点为仅有分组域而无电路域、基于全IP结构、控制与承载分离且网络结构扁平化，其中主要包含`MME`、`SGW`、`PGW`、`PCRF`等网元。其中SGW和PGW常常合并被称为`SAE-GW`。

**`CDN`** `Content Delivery Network`，即内容分发网络。其基本思路是尽可能避开互联网有可能影响数据传输速度和稳定性的瓶颈和环节，使内容传输的更快、更稳定。通过在网络各处放置节点服务器所构成的在现有的互联网基础之上的一层智能虚拟网络，CDN系统能够实时地根据网络流量和各节点的连接、负载状况以及到用户的距离和响应时间等综合信息将用户的请求重新导向离用户最近的服务节点上。其目的是使用户可就近取得所需内容，解决 Internet网络拥挤的状况，提高用户访问网站的响应速度。

**`OF-CONFIG`** 本质是提供一个开放接口用于远程配置和控制OpenFlow交换机，但是它并不影响到流表的内容和数据转发行为，对实时性也没太高的要求。在ONF制定的SDN标准体系中，除了OpenFlow交换机规范外，还有一个名为 `OpenFlow Configuration and Management Protocol`（`OF-CONFIG`）的协议。OpenFlow定义的是SDN网络架构中的一种**南向接口**，提出了由控制器向OpenFlow交换机发送流表以控制数据流通过网络所经过的路径的方式，但是并没有规定怎样管理和配置这些网络设备，而OF-CONFIG就是为解决这一问题而提出的。OF-CONFIG的本质是提供一个开放接口用于远程配置和控制OpenFlow交换机，但是它并不会影响到流表的内容和数据转发行为，对实时性也没有太高的要求。具体地说，诸如构建流表和确定数据流走向等事项将由OpenFlow规范进行规定，而诸如如何在OpenFlow交换机上配置控制器IP地址、如何对交换机的各个端口进行enable/disable操作则由OF-CONFIG协议完成。OpenFlow交换机上所有参与数据转发的软硬件(例如端口、队列等)都可被视为网络资源，而OF-CONFIG的作用就是对这些资源进行管理。OF-CONFIG与OpenFlow的关系如下图所示。
![](http://w6.sanwen8.cn/mmbiz/u6UOjABnicbvXPQhFiaUKjjxtDjC17uA8kxvyaws8lzRBQfB1g3YfzY7d6Uxv4QmUC4YheqtMvrZZic3vnwhGfzTw/640?wx_fmt=jpeg)

**`NETCONF`** IETF在2003年5月成立了Netconf工作组，该工作组主要是为了提出一个全新的基于XML的网络配置（NETCONF）协议而成立的。该工作组已于2006年12月通过了NETCONF协议的基本标准RFC4741-4744。RFC4741- 4744，RFC4742- RFC4744 分别描述了NETCONF在三种不同的传输模式SOAP，BEEP和SSH下是如何工作的。2008 年7 月推出RFC5277，主要定义了NETCONF的事件通知机制，用于故障管理。2009 年5 月推出的RFC5539 描述了NETCONF如何保证传输层传输信息的安全机制，加强了NETCONF的安全体系。NETCONF 协议是完全基于XML 之上的，所有的配置数据和协议消息都用XML 表示，XML 可以表达复杂的、具有内在逻辑关系的、模型化的管理对象，而且由于它是W3C提出的国际标准，因而受到广大软件提供商的支持，易于进行数据交流和开发。

**`SD-LAN:`** `Software Defined Local Area Network`（`SD-LAN`），软件定义局域网。

**`SD-WAN:`** `Software Defined Wide Area Network`（`SD-WAN`），软件定义广域网

**`SD-DC:`** `Software Defined Data Center`（`SD-DC`），软件定义数据中心

**`OPNFV:`** `Open Platform for NFV`（OPNFV），OPNFV是NFV（网络功能虚拟化）开放平台项目，由Linux基金会于9月30日宣布成立。该开源社区旨在提供运营商级的综合开源平台以加速新产品和服务的引入。

**`IaaS:`** `Infrastructure as a Service`(基础设施即服务)。提供给消费者的服务是对所有计算基础设施的利用，包括处理CPU、内存、存储、网络和其它基本的计算资源，用户能够部署和运行任意软件，包括操作系统和应用程序。消费者不管理或控制任何云计算基础设施，但能控制操作系统的选择、存储空间、部署的应用，也有可能获得有限制的网络组件（例如路由器、防火墙、负载均衡等）的控制。

**`SaaS:`** `Software as a Service`(软件即服务)。提供给客户的服务是运营商运行在云计算基础设施上的应用程序，用户可以在各种设备上通过客户端界面访问，如浏览器。消费者不需要管理或控制任何云计算基础设施，包括网络、服务器、操作系统、存储等待。

**`PaaS:`** `Platform as a Service`(平台即服务)。提供给消费者的服务是把客户采用提供的开发语言和工具开发的或收购的应用程序部署到供应商的云计算基础设施上去。客户不需要管理或控制底层的云基础设施，包括网络、服务器、操作系统、存储等，但客户能控制部署的应用程序，也可控制运行引用程序的托管环境配置。

**`DPDK:`** `Data Plane Development Kit`(数据平面开发套件)。DPDK是一组库和驱动程序的快速分组处理，它被设计为在任何处理器上运行，第一个支持的CPU是Intel X86，现在已扩展支持IBM Power 8，EZchip TILE-Gx和ARM。

**`SOA:`** `Service-Oriented Architecture` 面向服务的体系架构。

**`AWS:`** `Amazon Web Service`，亚马逊公司旗下的云计算服务平台，为全世界各个国家和地区的客户提供一整套基础设施和云解决方案。AWS面向用户提供包括弹性计算、存储、数据库、应用程序在内的一整套云计算服务，能够帮助企业降低IT投入成本和维护成本。

**`RESTful：`** `Representational State Transfer`(表述状态转化)，描述了一个架构样式的网络系统，比如web应用程序。它首次出现在2000年Roy Fielding的博士论文中，他是HTTP规范的主要编写者之一。在目前主流的三种Web服务交互方案中，REST相比SOAP（Simpe Object Acess protocol，简单对象访问协议）以及XML-RPC更加简单明了，无论是URL的处理还是对Payload的编码，REST都倾向于更加简单轻量的方法设计和实现。值得注意的是REST并没有一个明确的标准，而更像是一种设计风格。