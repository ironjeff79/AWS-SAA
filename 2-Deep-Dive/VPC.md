# Amazon Virtual Private Cloud (Amazon VPC)
## 在逻辑隔离的虚拟网络中定义和启动 AWS 资源


## 工作原理
+ Amazon Virtual Private Cloud (Amazon VPC) 让您能够全面地控制自己的虚拟网络环境，包括资源放置、连接性和安全性。首先在 AWS 服务控制台中设置 VPC。然后，向其中添加资源，例如 Amazon Elastic Compute Cloud (EC2) 和 Amazon Relational Database Service (RDS) 实例。最后，您可以定义 VPC 相互之间以及跨账户、可用区或 AWS 区域通信的方式。在以下示例中，每个区域内的两个 VPC 之间共享网络流量。

## IP 寻址
IP 地址使 VPC 中的资源能够相互通信以及与 Internet 上的资源进行通信。

无类域间路由 (CIDR) 表示法是一种表示 IP 地址及其网络掩码的方法。这些地址的格式如下：

+ 单个 IPv4 地址为 32 位，分为 4 组，每组包含最多 3 个十进制数字。例如：10.0.1.0。

+ IPv4 CIDR 块分为四组，每组包含最多 3 个十进制数字（0-255，以句点分隔），后跟斜杠和一个介于 0 到 32 的数字。示例：10.0.0.0/16。

+ 单个 IPv6 地址为 128 位，分为 8 组，每组包含最多 4 个十六进制数字。例如：2001:0db8:85a3:0000:0000:8a2e:0370:7334。

+ IPv6 CIDR 块分为四组，每组包含最多 4 个十六进制数字，用冒号分隔，后跟一个双冒号，后跟斜杠和一个介于 1 到 128 的数字。例如：2001:db8:1234:1a00::/56。

创建 VPC 时，需要为其分配一个 IPv4 CIDR 块（一系列私有 IPv4 地址）、一个 IPv6 CIDR 块或同时分配两种 CIDR 块（双堆栈）。

私有 IPv4 地址无法通过 Internet 访问。IPv6 地址具有全球唯一性，可以配置为保持私有或通过互联网进行访问。

## 比较 IPv4 与 IPv6
下表总结 Amazon EC2 和 Amazon VPC 中 IPv4 与 IPv6 之间的差异。


| 特征  | IPv4 |   IPv6 |
| :------------- | :----------: | ------------: |
| VPC 大小 |  最多 5 个 CIDR，从 /16 到 /28。配额可调整。 | 最多 5 个 CIDR，固定为 /56。配额不可调整。|
|    子网大小     |       从 /16 到 /28     |  固定为 /64   |
|   弹性 IP 地址     |    支持  |     不支持   |
|     NAT 网关    |    支持     |      不支持    |
|     VPC 端点    |    支持     |      不支持    |
|     AMI   |    支持所有AMI     |     支持配置了 DHCPv6 的 AMI    |
|     EC2 实例    |   支持所有实例类型     | 在所有当前一代实例以及 C3、R3 和 I2 实例上均支持。 |
|     DNS 名称    |  实例将接收 Amazon 提供的 IPBN 或基于 RBN 的 DNS 名称。DNS 名称将解析为为实例选择的 DNS 记录。  | 实例将接收 Amazon 提供的 IPBN 或基于 RBN 的 DNS 名称。DNS 名称将解析为为实例选择的 DNS 记录。 |

## 私有 IPv4 地址
私有 IPv4 地址（在本主题中也称作私有 IP 地址）无法通过 Internet 访问，但可用于 VPC 中实例之间的通信。当您在 VPC 中启动实例时，系统会将子网地址范围中的一个主要私有 IPv4 地址分配给该实例的默认网络接口 (eth0)。另外，还为每个实例指定一个可解析为实例私有 IP 地址的私有（内部）DNS 主机名。主机名可以有两种类型：基于资源或基于 IP。

您可以为 VPC 中运行的实例分配其他私有 IP 地址，即所谓的辅助私有 IP 地址。与主要私有 IP 地址不同的是，您可以将一个网络接口的辅助私有 IP 地址重新分配给另一个网络接口。私有 IP 地址会在实例停止并重新启动时保持与网络接口的关联，并在实例终止时释放。

我们所说的私有 IP 地址是 VPC 的 IPv4 CIDR 范围内的 IP 地址。大部分 VPC IP 地址范围均处于 RFC 1918 中指定的私有（非公有可路由）IP 地址范围内；但是，您可为您的 VPC 使用公有可路由的 CIDR 块。不管您的 VPC 使用何种 IP 地址范围，我们都不支持从您的 VPC 的 CIDR 块（包括公共可路由的 CIDR 块）直接访问 Internet。您必须通过网关设置 Internet 访问，例如，通过 Internet 网关、虚拟专用网关、AWS Site-to-Site VPN 连接或 AWS Direct Connect。

## 公有 IPv4 地址
所有子网都有一个用于确定在子网中创建的网络接口是否自动接收公有 IPv4 地址（在本主题中也称作公有 IP 地址）的属性。因此，当您在启用了此属性的子网中启动实例时，系统会向为此实例创建的主网络接口 (eth0) 分配一个公有 IP 地址。公有 IP 地址通过网络地址转换 (NAT) 映射到主要私有 IP 地址。

您可以通过执行以下操作，控制实例是否接收公有 IP 地址：

+ 修改子网的公有 IP 寻址属性。有关更多信息，请参阅 修改子网的公有 IPv4 寻址属性。

+ 在实例启动过程中启用或禁用公有 IP 寻址功能，以覆盖子网的公有 IP 寻址属性。

公有 IP 地址将从 Amazon 的公有 IP 地址池分配，它不与您的账户关联。在公有 IP 地址与您的实例取消关联后，该地址即释放回该池，并且不再可供您使用。您不能手动关联或取消关联公有 IP 地址。而是在某些情况下，我们从您的实例释放该公有 IP 地址，或向其分配新地址。

如果您需要向您的账户分配一个永久公有 IP 地址（您可根据需要将其分配给实例或将其从实例中删除），请改为使用弹性 IP 地址。

如果您的 VPC 启用了对 DNS 主机名的支持，则系统还会向收到公有 IP 地址或弹性 IP 地址的每个实例分配一个公有 DNS 主机名。我们会将公有 DNS 主机名解析为该实例在实例网络外的公有 IP 地址和在实例网络内的私有 IP 地址。

## IPv6 地址
您可以选择向 VPC 和子网关联 IPv6 CIDR 块。

如果您的 VPC 和子网关联了 IPv6 CIDR 块，并且满足以下条件之一，则 VPC 中的实例会收到 IPv6 地址：

+ 您的子网配置为在启动期间向实例的主网络接口自动分配 IPv6 地址。

+ 您在启动期间向实例手动分配 IPv6 地址。

+ 您在启动后向实例分配 IPv6 地址。

+ 您向同一子网中的某个网络接口分配 IPv6 地址，并在启动后将此网络接口附加到您的实例。

当实例在启动期间收到 IPv6 地址时，此地址将与实例的主网络接口 (eth0) 关联。您可以取消 IPv6 地址与主网络接口的关联。我们不支持为您的实例使用 IPv6 DNS 主机名。

IPv6 地址会在您停止和启动实例时保留下来，并在您终止实例时释放出来。您无法重新分配已分配给某个网络接口的 IPv6 地址；您必须先取消分配此 IPv6 地址。

通过将 IPv6 地址分配给附加到实例的网络接口，您可以为实例分配更多的 IPv6 地址。可以分配给网络接口的 IPv6 地址数量以及可以附加到实例的网络接口数量因实例类型而异。

IPv6 地址具有全局唯一性，可以配置为保持私有或通过互联网进行访问。您可以通过控制子网的路由或通过使用安全组和网络 ACL 规则来控制能否通过实例的 IPv6 地址对其进行访问。


## 使用自带 IP 地址
您可以将部分或全部自带公有 IPv4 地址或 IPv6 地址范围引入到您的 AWS 账户。您继续拥有该地址范围，但 AWS 默认将其发布到 Internet 上。在将地址范围引入 AWS 中之后，它会在您的账户中显示为地址池。您可以从 IPv4 地址池创建弹性 IP 地址，也可以将 IPv6 地址池中的 IPv6 CIDR 块与 VPC 相关联。

# Amazon VPC 功能
Amazon Virtual Private Cloud (Amazon VPC) 提供以下功能，让您能提升和监控 VPC 的安全性。

## 流日志
您可以监控交付给 Amazon Simple Storage Service (Amazon S3) 或 Amazon CloudWatch 的 VPC 流日志，以获取对网络依赖性和流量模式的操作可见性，检测异常并防止数据泄露，以及对网络连接和配置问题进行故障排除。流日志中丰富的元数据可帮助您深入了解谁发起了 TCP 连接，以及流经中间层（如 NAT 网关）的流量的实际数据包级源和目的地。您还可以存档流日志，以帮助满足某些合规性要求。在此处了解如何开始使用此功能。

## IP 地址管理器 (IPAM)
IPAM 可让您更轻松地规划、跟踪和监控 AWS 工作负载的 IP 地址。IPAM 自动为您的 Amazon VPC 分配 IP 地址，消除了使用自主开发或基于电子表格的规划应用程序的需求。它还通过在统一的操作视图中显示跨多个账户和 VPC 的 IP 使用情况，增强您的网络可观察性。

## IP 寻址
通过 IP 地址，您的 VPC 中的资源可以相互通信并与互联网上的资源通信。Amazon VPC 支持 IPv4 和 IPv6 寻址协议。在 VPC 中，您可以创建仅 IPv4、双堆栈和仅 IPv6 子网，并在这些子网中启动 Amazon EC2 实例。Amazon 还为您提供了向实例分配公有 IP 地址的多个选项。您可以使用 Amazon 提供的公有 IPv4 地址、弹性 IPv4 地址或来自 Amazon 提供的 IPv6 CIDR 的 IP 地址。此外，您还可以选择将自己的 IPv4 或 IPv6 地址放入可分配给这些实例的 Amazon VPC 中。您可以从此处阅读更多关于在您的 VPC 中进行 IP 寻址的信息。

## 入口路由
借助此功能，您可以将所有往返互联网网关或虚拟私有网关的传入和传出流量路由到特定 Amazon EC2 实例的弹性网络接口。 配置 virtual private cloud，以在流量到达业务工作负载之前，将所有流量发送到网关或 Amazon EC2 实例。了解有关此功能的更多信息，单击此处。

## Network Access Analyzer
Network Access Analyzer 可帮助您验证 AWS 上的网络是否符合您的网络安全和合规性要求。通过 Network Access Analyzer，您可以指定网络安全和合规性要求，并识别不符合您指定要求的意外网络访问。您可以使用 Network Access Analyzer 来了解对您的资源的网络访问，帮助您确定云安保状况的改进并轻松证明合规性。

## 网络访问控制列表
网络访问控制列表（网络 ACL）是 VPC 的可选安全层，用作控制一个或多个子网内外流量的防火墙。您可以使用与您的安全组规则类似的规则设置网络 ACL。在此查阅安全组和网络 ACL 之间的差异。

## 网络管理器
网络管理器提供的工具和功能可帮助您在 AWS 上管理和监控网络。网络管理器可以更容易地执行连接管理、网络监控和故障排除、IP 管理以及网络安全和治理。

## Reachability Analyzer
此静态配置分析工具使您能够分析和调试 VPC 中两个资源之间的网络可访问性。指定源和目标资源后，Reachability Analyzer 将在它们之间可访问时生成它们之间虚拟路径的逐跳详细信息，并在它们不可访问时识别阻止组件。在此处了解如何开始使用此功能。

## 安全组
创建安全组，以作为关联的 Amazon EC2 实例的防火墙，在实例级别控制入站和出站流量。启动实例时，可以将其与一个或多个安全组关联。如果不指定组，实例会自动关联到 VPC 的默认组。VPC 中的每个实例都可以属于不同的安全组。在此了解关于安全组的更多信息。

## 流量镜像
通过此功能，您可以从 Amazon EC2 实例的弹性网络接口复制网络流量，然后将其发送到带外安全和监视设备以进行深度数据包检查。您可以检测网络和安全异常、获得操作见解、实施合规性和安全控制以及对问题进行故障排除。流量镜像可让您直接访问流经 VPC 的网络数据包。在此处了解如何开始使用此功能。



## Network Access Control Lists (NACL) and Security Groups (SG)

- NACL is a like a firewall which controls traffic which goes outside of comes inside a subnet
- The default NACL allows everything outbound and everything inbound
- We define one NACL per subnet, new subnets are assigned the default NACL
- We can define NACL rules:
    - Rules have a number (1 - 32766) which defines the precedence
    - Rules with lower number have higher precedence
    - Rule with higher precedence wins at the time of evaluation
    - Last rule is has the precedence of asterisk (*) and denies all the requests. This rule is not editable
    - AWS recommends adding rules by increment of 100
- Newly created created NACL will deny everything (last rule)
- NACLs are great way of blocking a specific IP address at the subnet level

| Security Group                                           |  Network ACL                                                            |
|----------------------------------------------------------|-------------------------------------------------------------------------|
| Operates at the instance level                           | Operates at the subnet level                                            |
| Supports allow rules only                                | Supports allow rules and deny rules                                     |
| It is stateful: return traffic is automatically allowed  | It is stateless: return traffic must be explicitly allowed by the rules |
| All rules are evaluated before deciding to allow traffic | Rules have a precedence when deciding whether to allow or deny traffic  |
| It is associated to an instance inside of a VPC          | Automatically applies to all instances in the subnet                    |

- Example of NACL with ephemeral ports: https://docs.aws.amazon.com/vpc/latest/userguide/vpc-network-acls.html

## VPC Peering

- VPC Peering allows to connect two VPCs privately using AWS network. This will make them behave as if they were the same network
- Networks must have non-overlapping CIDRs
- VPC Peering connections is not transitive, which means it must be established for each VPC that needs to communicate with other
- VPC Peering can be done form one AWS account to another
- We must update the route tables in each VPC subnet to ensure instances can communicate with each other
- VPC peering can work inter-region, cross-account. We can reference a security group of a peered VPC (this works cross account also)


## VPC Endpoints

- Allow connection to AWS services from VPCs using a private network instead of the public internet
- They scale horizontally
- They remove the need of IGW, NAT, etc. to access AWS services
- There are 2 kinds of VPC Endpoints:
    - **Interface**: provisions an ENI (private IP address) as an entry point. A security group must be attached to it. Most AWS services use this method
    - **Gateway**: provisions a target and must be used in a route table. Gateway is used for S3 and DynamoDB
- In case of issues:
    - We have to check DNS settings resolution in the VPC
    - We have to check the route tables

## VPC FLow Logs

- Flow logs help capture information about the IP traffic going into the interfaces
- There are 2 kinds of Flow Logs:
    - VPC Flow Logs
    - Subnet Flow Logs
    - Elastic Network Interface Flow Logs
- Flow logs help monitor and troubleshoot connectivity issues
- Flow logs data can go to S3/CloudWatch logs
- It can capture network information from some of the AWS managed interface too: ELB, RDS, ElastiCache, Redshift, AWS Workspaces

## Bastion Hosts
- Bastion hosts are used to SSH into instances from private subnets
- The bastion host is sitting in the public subnet which is connected to the private subnets
- Bastion host SG must be really strict
- We have to make sure the bastion host only has port 22 traffic from the IP we need, not from the security group of other instances

## Site to Site VPN
- Virtual Private Gateway:
    + VPN concentrator on the AWS side of the VPN connection
    + Virtual Private Gateway (VPG) is created and attached to the VPC from which we want to create the site-to-site VPN connection
    + Possibility to customize the ASN
- Customer Gateway:
+ Software application or physical device on customer side of the VPN connection
+ IP Address: use static, internet-routable IP address for the customer device. If it is behind a NAT (with NAT-T enabled), use the public IP address of the NAT