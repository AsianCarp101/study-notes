###学习SDN/NFV路上遇到的专业术语
>引用自：http://m.sanwen8.cn/p/142P453.html


**`SDN:`** `软件定义网络（Software Defined Network,SDN）`，是一种新型的网络创新架构，是网络虚拟化的一种实现方式，其核心技术 `OpenFlow` 通过将网络设备的**控制面**和**数据面**分离开来，从而实现了网络流量的灵活控制，使网络作为管道变得更加智能。

**`NFV:`** `网络功能虚拟化（Network Function Virtualization）`，通过X86等通用硬件以及虚拟化技术，来承载很多功能的软件处理。从而降低网络昂贵的设备成本，可通过 `软硬件解耦` 及 `功能抽象`，使网络设备不在依赖于专用硬件，资源可以充分灵活分享，实现新业务的快速开发和部署，并基于实际业务需求进行自动部署、弹性伸缩、故障隔离和自愈等。

**`OpenFlow:`** 是一种新的网络交换模型。OpenFlow网络由 `OpenFlowSwitch` （OpenFlow交换机）、 `FlowVisor` （网络虚拟化层）和 `Controller` （控制器）三部分组成。OpenFlow交换机进行数据层的转发；FlowVisor对网络进行虚拟化；Controller对网络集中控制，实现控制层的功能。OpenFlow交换机由 `FlowTable` （流表）、`SecurChannel` （安全通道）和 `OpenFlowProtocol` （协议）三部分组成。`FlowTable` 流表有很多个流表项组成，每个流表项就是一个转发规则。进入交换机的数据包通过查询流表来获得转发的目的端口。`Secure Channel` ：安全通道是连接OpenFlow交换机到控制器的接口。控制器通过这个接口控制和管理交换机，同时控制器接收来自交换机的事件并向交换机发送数据包。交换机和控制器通过安全通道进行通信，而且所有的信息必须按照OpenFlow协议规定的格式来执行。

**`OpenFlow协议:`** 用来描述控制器和交换机之间交互所用信息的标准，以及控制器和交换机的接口标准。协议的核心部分是用于OpenFlow协议信息结构的集合。OpenFlow协议支持三种信息类型：`Controller-to-Switch`，`Asynchronous` 和 `Symmetric`，每一个类型都有多个子类型。Controller-to-Switch信息由控制器发起并且直接用于检测交换机的状态。Asynchronous信息由交换机发起并通常用于更新控制器的网络事件和改变交换机的状态。Symmetric信息可以在没有请求的情况下由控制器和交换机发起。
