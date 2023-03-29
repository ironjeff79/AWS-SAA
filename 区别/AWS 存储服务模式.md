##Amazon Elastic Block Store（Amazon EBS）
Amazon EBS 是一种易于使用的高性能块存储服务。Amazon EBS 专为 Amazon EC2 中运行的任意规模吞吐率密集型和事务密集型工作负载设计。关系和非关系数据库，企业应用程序，容器化应用程序，大数据分析引擎，文件系统和媒体工作流等各种工作负载已广泛部署在 Amazon EBS 上。

Amazon EBS 适用于原本在本地环境使用 iSCSI 或 FC SAN 存储阵列的应用程序工作负载。

## Amazon Elastic File System（Amazon EFS）
Amazon EFS 提供了一种简单、可扩展、完全托管的弹性 NFS 文件系统，可供 AWS 云服务和本地资源使用。在设计上，该服务可在不影响应用程序运行的前提下按需扩展至 PB 级规模，可随着文件的添加和移除自动扩展或收缩，用户无需为了适应未来增长而预配并管理容量。Amazon EFS 是一种区域性服务，可提供个位数毫秒级别的延迟，同时在至少三个可用区中存储数据，其持久性设计为 99.999999999％（11个9）。

Amazon EFS 适用于原本在本地环境使用基于 NFS 协议的 NAS 存储阵列的应用程序和用户工作负载。

## Amazon FSx for Windows File Server


Amazon FSx for Windows File Server 提供了完全托管的高可靠、可扩展文件存储，可通过符合行业标准的 SMB 协议访问。该服务基于 Windows Server 构建，提供了丰富的管理功能，例如用户配额、最终用户文件还原以及与 Microsoft Active Directory 的集成。该服务提供了单一 AZ 和多 AZ 部署选项、完整的托管备份，以及对传输中和存储后的数据进行加密的能力。Amazon FSx 文件存储可通过 Windows、Linux 和 macOS 计算实例以及运行在 AWS 或本地的设备访问。用户可以使用 SSD 和 HDD 存储选件来优化成本和性能，以满足工作负载需求。

## Amazon Simple Storage Service（Amazon S3）
Amazon S3 是一种对象存储服务，提供了业内领先的可扩展性、数据可用性、安全性以及性能。这些能力使得客户能够存储和保护任意数量的数据，并将数据用于各种类型的用途，如网站、移动应用程序、备份和还原、归档、企业应用程序、IoT 设备，以及大数据分析等。Amazon S3 提供了易于使用的管理功能，用户可以借此整理自己的数据，并配置可细化调整的访问控制机制，以满足特定的业务、组织或合规要求。Amazon S3 的设计持久性为99.999999999％（11个9），目前已被全球大量企业的数以百万计企业应用程序所使用。

Amazon S3 针对不同用例提供了丰富的存储类。例如针对频繁访问数据的常规用途存储所提供的 S3 Standard；针对访问模式未知或频繁变化的数据所提供的 S3 Intelligent-Tiering；为需要长期保存，需要轻松重建但访问频率较低的数据所提供的S3 Standard-Infrequent Access（S3 Standard-IA）和 S3 One Zone-Infrequent Access（S3 One Zone-IA）；以及为长期归档和数字化保留所提供的 Amazon S3 Glacier 和 Amazon S3 Glacier Deep Archive。Amazon S3 还提供了数据全生命周期管理功能。在设置 S3 生命周期策略后，数据即可被自动转移至不同的存储类，而这一过程中完全不需要对应用程序进行任何改动。

Amazon S3 适用于基于本地对象存储和很多基于文件存储阵列构建的应用程序和用户工作负载。