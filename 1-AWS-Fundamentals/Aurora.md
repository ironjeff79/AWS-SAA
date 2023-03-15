# Amazon Aurora
Amazon Aurora 提供内置的安全性、几乎连续的备份、无服务器计算、最高 15 个只读副本、自动多区域复制以及与其他 AWS 服务的集成。
  
  Amazon Aurora 是一种关系数据库服务，既有高端商用数据库的高速度和可用性，也有开源数据库的简单性和成本效益。Aurora 与 MySQL 和 PostgreSQL 完全兼容，使现有应用程序和工具无需修改即可运行。
# 高性能和高可扩展性
## 最高为 MySQL 吞吐量的 5 倍，PostgreSQL 吞吐量的 3 倍
根据 SysBench 等标准基准进行的测试表明，其吞吐量最高可达到存储 MySQL 的 5 倍，在类似硬件上运行时，其吞吐量是类似硬件上运行的原版 PostgreSQL 的 3 倍。Amazon Aurora 使用各种不同的软件和硬件技术来确保数据库引擎能够充分利用可用计算、内存和联网。I/O 运算使用 Quorum 等分布式系统技术来提高性能一致性。
## 无服务器配置
Amazon Aurora Serverless 是一种面向 Aurora 的按需自动扩缩配置，其中的数据库将根据应用程序的需求自动启动、关闭以及扩展或缩减容量。在云中运行数据库，而无需管理任何数据库实例。
## 一键式计算扩展
您可以使用 Amazon Relational Database Service (Amazon RDS) API 或 AWS 管理控制台扩展预置的实例，以提高或降低部署能力。计算扩展操作通常可在几分钟之内完成。
## 存储自动扩展
Amazon Aurora 会随着您存储需求的增长而自动提高您的数据库容量大小。您的容量将以 10 GB 的增量增加，最大可增加到 128 TB。您无需为了满足未来增长需求，而为数据库预置多余存储空间。
## 低延迟只读副本
您可以通过创建多达 15 个数据库 Amazon Aurora 副本，增加读取吞吐量以支持大量应用程序请求。Aurora 副本与源实例共用同一个底层存储，从而降低成本并消除在副本节点执行写入操作的需要。这将释放更多的处理能力来提供读取请求并降低副本滞后时间，通常可降低到几毫秒。Aurora 提供一个读取器终端节点，应用程序可以直接连接，不必跟踪副本的添加和删除。它还支持自动扩展功能，通过自动添加或删除副本来响应您指定的性能指标的变化。

Aurora 支持跨区域只读副本。跨区域副本为您的用户提供快速本地读取，并且每个区域可以具有 15 个额外 Aurora 副本以进一步扩展本地读取。请参阅 Amazon Aurora Global Database 以了解详细信息。
# 自定义数据库终端节点
借助自定义端点功能，您可以在不同数据库实例集之间分配工作负载并对其执行负载均衡。例如，您可以预置一组 Aurora 副本以使用具有更高内存容量的实例类型，以便运行分析工作负载。然后，自定义终端节点可以帮助您将工作负载路由到这些经过适当配置的实例，同时使集群中的其他实例与此工作负载隔离。
# Aurora MySQL 的并行查询
Amazon Aurora 并行查询提供比当前数据更快的分析查询。它可以将查询速度提高多达两个数量级，同时保持核心事务工作负载的高吞吐量。通过将查询处理下移至 Aurora 存储层，它不仅获得了大量计算能力，还减少了网络流量。使用并行查询在同一个 Aurora 数据库中互不干扰地运行事务和分析工作负载。并行查询适用于兼容 MySQL 的 Amazon Aurora。
#  用 Amazon DevOps Guru for RDS 诊断和解决性能瓶颈
Amazon DevOps Guru 是一款由机器学习 (ML) 支持的云运维服务，可以提高应用程序的可用性。使用针对 RDS 的 Amazon DevOps Guru，您可以用机器学习（ML）支持的洞察轻松检测和诊断性能相关的关系数据库问题，并在几分钟内解决问题，而不是花费几天时间。开发人员和 DevOps 工程师可以使用针对 RDS 的 DevOps Guru，自动识别性能问题的根本原因，并获得解决问题的智能建议，无需数据库专家的帮助。

想要开始使用，只需转到 Amazon RDS 管理控制台并打开 Amazon RDS 性能洞察。启用 Performance Insights（性能洞察）后，请前往 Amazon DevOps Guru 控制台，以便为 Amazon Aurora 资源、其他受支持的资源或您的整个账户启用 DevOps Guru。
# 高可用性和持久性
## 实例监控和修复
Amazon RDS 持续监控您的 Amazon Aurora 数据库和底层 Amazon Elastic Compute Cloud (EC2) 实例的运行状况。发生数据库故障时，Amazon RDS 将自动重启数据库及相关进程。Amazon Aurora 不需要对数据库重做日志进行崩溃恢复回放，因此大大缩短了重启时间。它还会将数据库缓冲缓存与数据库进程隔离开来，这样缓存在数据库重启时就不会丢失了。

## 包含 Aurora 副本的多可用区部署
发生实例故障时，Amazon Aurora 使用 Amazon RDS 多可用区技术，自动将故障转移到最多 15 个 Amazon Aurora 副本中的一个（您在 3 个可用区中的任意一个内创建的副本）。如果未预置任何 Amazon Aurora 副本，在发生故障的情况下，Amazon RDS 将尝试为您自动创建新的 Amazon Aurora 数据库实例。通过将社群 MySQL 和 PostgreSQL 驱动程序替换为开源的简易兼容的 AWS JDBC Driver for MySQL 和 AWS JDBC Driver for PostgreSQL 最大限度减少故障转移时间。您还可以使用 RDS Proxy 降低故障转移时间和提高可用性。发生故障转移时，RDS Proxy 将请求直接路由到新的数据库实例，以将故障转移时间最高降低 66%，同时保留应用程序连接。
## 全球数据库
对于全局分布式应用程序，您可以使用全局数据库，其中单个 Aurora 数据库可以跨多个 AWS 区域，以实现快速本地读取和快速灾难恢复。全局数据库使用基于存储的复制来跨多个 AWS 区域复制数据库，典型延迟小于 1 秒。您可以使用辅助区域作为备份选项，以防您需要从区域性降级或中断中快速恢复。可以在不到 1 分钟的时间内将辅助区域中的数据库提升为完全读/写功能。
## 容错和自我修复型存储
每 10GB 的数据库卷组块都能在三个可用区间用六种方法进行复制。Amazon Aurora 存储具有容错能力，能以透明方式应对多达两个数据副本的丢失，而不会影响数据库写入可用性，还能在不影响读取可用性的情况下应对多达三个副本的丢失。Amazon Aurora 存储还具有自我修复能力，可连续扫描数据块和磁盘是否存在任何错误，并自动更换。
## 自动、连续、增进式备份和时间点还原
借助 Amazon Aurora 的备份功能，您可以对实例进行时间点还原。这样，您就能够将数据库还原到保留期内任何一秒钟的状态，最多可还原到前五分钟的状态。您的自动备份保留期最长可配置为三十五天。自动备份存储在 Amazon Simple Storage Service (Amazon S3) 中，该服务设计具有 99.999999999% 的耐久性。Amazon Aurora 备份是自动、递增且连续的，对数据库性能没有影响。

## 数据库快照
数据库快照是用户对您存储在 Amazon S3 中的实例发起的备份，将保留到您明确删除它们之前。它们利用自动化的增量快照降低所需时间和存储。您可以在需要时随时从数据库快照创建新实例。

## 适用于 Aurora MySQL 的回溯
您可使用回溯将数据库快速倒回之前的时间点，而不需要利用备份还原数据。这使您可以快速从用户错误（比如删错表格或行）中恢复。当您启用回溯后，Aurora 将保留指定的回溯持续时间段内的数据记录。例如，您可以将回溯设置为最高可以将数据库回退 72 小时。回溯在几秒钟内即可完成，即使针对大型数据库也是如此，因为无需复制任何数据记录。您可以向前和向后追溯，以找到错误发生前的时间点。

回溯对于开发和测试也十分有用，特别是测试删除或以其他方式导致数据无效的情形下。可轻松回溯到原始数据库状态，并且您可以运行其他测试。您可以创建一个通过 API 调用回溯的脚本，然后再运行测试，以便轻松地将其集成到您的测试框架中。回溯适用于兼容 MySQL 的 Amazon Aurora。
# 高度安全
## 网络隔离
Amazon Aurora 在 Amazon Virtual Private Cloud（VPC）中运行，这将帮助您将数据库隔离在自己的虚拟网络中，并使用行业标准的加密 IPsec VPN 与您的本地部署 IT 基础设施连接。要了解有关 Amazon VPC 中的 Amazon Relational Database Service（RDS）的更多信息，请参阅 Amazon RDS 用户指南。此外，在使用 Amazon RDS 时，您可以配置防火墙设置并控制对数据库实例的网络访问。
## 资源级权限
Aurora 可与 AWS Identity and Access Management（IAM）集成，并允许您控制您的 IAM 用户和组可以对特定 Aurora 资源（例如，数据库实例、数据库快照、数据库参数组、数据库事件订阅、数据库选项组）执行的操作。此外，您还可以为 Aurora 资源添加标签，并控制您的 IAM 用户和组可以对各组具有相同标签（和标签值）的资源执行的操作。有关 IAM 集成的更多信息，请参阅 IAM 数据库身份验证文档。
## 加密
Aurora 将帮助您使用通过 AWS Key Management Service（KMS）创建和控制的密钥为您的数据库加密。在通过 Aurora 加密运行的数据库实例上，静态存储于底层存储的数据都经过加密，同一集群的自动备份、快照和副本也是如此。Aurora 使用 SSL（AES-256）保护动态数据安全。
## 高级审核
Aurora 将帮助您记录数据库事件，并且对数据库性能的影响最小。您日后可以对日志进行分析以执行数据库管理、确保安全性、进行管理、确保合规性等。您还可以通过将审核日志发送到 Amazon CloudWatch 来监控活动。
## 威胁检测
Aurora 与 Amazon GuardDuty 集成，帮助您识别存储在 Aurora 数据库中的数据的潜在威胁。GuardDuty RDS Protection 分析和监控您账户中现有和新数据库的登录活动，并使用定制的 ML 模型来准确检测对 Aurora 数据库的可疑登录。如果检测到潜在威胁，GuardDuty 会生成一个安全检测结果，其中包括数据库详细信息和有关可疑活动的丰富上下文信息。Aurora 与 GuardDuty 的集成提供了对数据库事件日志的直接访问，而无需修改数据库，而且其设计不会对数据库性能产生影响。
# 完全托管
## 易于使用
您可以十分轻松地开始使用 Amazon Aurora。只需使用 Amazon RDS 管理控制台或一个 API 调用或 CLI 即可启动新的 Amazon Aurora 数据库实例。Amazon Aurora 数据库实例为您所选择的数据库实例类预配置了合适的参数和设置集。您在几分钟之内即可启动数据库实例并连接应用程序，而无需其他配置。数据库参数组可以提供对数据库的精细控制和微调功能。

## 监控和指标
Amazon Aurora 提供您的数据库实例的 Amazon CloudWatch 指标，您无需支付额外费用。您可以使用 AWS 管理控制台查看有关您的数据库实例的 20 多个关键运营指标，包括计算、内存、存储、查询吞吐量、缓存点击率以及活动连接。此外，您还可以使用增强监控收集运行数据库的操作系统实例的各项指标。您可以将 Amazon RDS 性能详情（一种数据库监控工具，可方便地检测数据库性能问题并采取纠正措施）与简单易懂的控制面板配合使用，以可视化方式呈现数据库负载。最后，您还可以使用 Amazon DevOps Guru for RDS 轻松检测性能问题，自动识别性能问题的根本原因，并获得智能建议以帮助解决问题，而无需数据库专家的帮助。

## Amazon RDS 蓝绿部署
Amazon RDS 蓝绿部署让您能够在 Amazon Aurora MySQL 兼容版本上进行更安全、更简单、更快速的数据库更新，且不丢失任何数据。蓝绿部署可以通过简单几步创建一个暂存环境，该环境镜像生产环境，并使用逻辑复制保持两个环境的同步。您可以在不影响生产工作负载的情况下进行更改，如主要/次要版本升级、架构修改和参数设置更改。

在提升暂存环境时，蓝绿部署会阻止任何对蓝色和绿色环境的写入，直到切换完成。蓝绿部署采用内置的切换防护机制，如果超出最大可忍受的停机时间、检测到复制错误或检查实例运行状况等，则将超时。

## 自动执行软件修补
Amazon Aurora 会使用最新的补丁来使您的数据库保持最新状态。您可以通过数据库引擎版本管理控制是否以及何时修补实例。Aurora 尽可能使用零停机修补：如果出现合适的时段，则会更新实例，在修补过程中，应用程序会话将保留并且数据库引擎会重新启动，只会导致吞吐量短暂（大约 5 秒）下降。

## 数据库事件通知
Amazon Aurora 可通过电子邮件或短信通知您重要的数据库事件，例如自动故障转移。您可以使用 AWS 管理控制台或 Amazon RDS API 订阅与您的 Amazon Aurora 数据库相关的 40 多种不同的数据库事件。

## 数据库克隆
Amazon Aurora 支持快速高效的克隆操作，可在数分钟内克隆完整的数 TB 数据库集群。克隆可用于实现许多目的，其中包括应用程序开发、测试、数据库更新以及运行分析查询。如果数据立即可用，将能够大幅加快软件开发和升级项目，并提高分析准确度。

您只需几次点击即可完成 Amazon Aurora 数据库的克隆，且不会发生任何存储费用，除非您使用额外的空间来存储数据的更改。

## 数据库的启动/停止
只需几次点击即可手动停止和启动 Amazon Aurora 数据库。从而可以轻松、经济地将 Aurora 用于无需数据库始终运行的开发和测试环境。停止数据库不会删除数据。有关详细信息，请参阅启动/停止文档。
# 迁移支持
## MySQL 数据库迁移
可将标准的 MySQL 导入和导出工具与 Amazon Aurora 配合使用。您还可以从 Amazon RDS for MySQL 数据库快照中轻松创建新的 Amazon Aurora 数据库。基于数据库快照的迁移操作一般在一个小时内完成，但具体根据所迁移数据的量和格式而异。

您还可以在 Aurora MySQL 兼容版数据库和在 AWS 内部或外部运行的外部 MySQL 数据库之间设置基于二进制日志的复制。
## PostgreSQL 数据库迁移
标准的 PostgreSQL 导入和导出工具可与 Amazon Aurora 配合使用（包括 pg_dump 和 pg_restore）。Amazon Aurora 还支持从 Amazon RDS for PostgreSQL 导入快照，以及使用 AWS Database Migration Service (AWS DMS) 进行复制。
## 商用数据库迁移
Amazon Aurora 为将数据库工作负载移出商业数据库提供了理想的环境。Aurora 具有与商用数据库引擎相当的功能，并提供了大多数企业数据库工作负载所需的企业级性能、持久性和高可用性。AWS Database Migration Service (AWS DMS) 可以帮助加速将数据库迁移到 Amazon Aurora。
## 适用于 Aurora PostgreSQL 的 Babelfish
Babelfish for Aurora PostgreSQL 是 Amazon Aurora PostgreSQL 兼容版本的一项新功能，让 Aurora 能够理解来自为 Microsoft SQL Server 编写的应用程序命令。借助 Babelfish，Aurora PostgreSQL 现在可以理解 Microsoft SQL Server 专有的 SQL 语言 T-SQL，并支持相同的通信协议，因此您最初为 SQL Server 编写的应用程序现在可以与 Aurora 一起使用，并且所需进行的代码更改更少。因此，修改 SQL Server 2005 或更高版本上运行的应用程序并将其移动到 Aurora 所需的工作量将减少，从而可实现更快、风险更低且更具成本效益的迁移。Babelfish 是 Amazon Aurora 的内置功能，无需额外费用。只需在 RDS 管理控制台中单击几下，您就可以在 Amazon Aurora 集群上启用 Babelfish。
# 成本效益
## 只需按实际用量付费
Amazon Aurora 不要求您支付预先承付款，您只需按小时为所启动的各个实例支付费用即可。此外，在完成某 Amazon Aurora 数据库实例后，您也可以轻松删除此实例。您无需预置多余的存储空间作为安全裕度，只需按实际使用的存储空间支付费用即可。要了解更多详细信息，请访问 Amazon Aurora 定价页面。

## 优化 I/O 成本
对于需要进行大量分析的工作负载，数据库成本的最大来源通常是 I/O 成本。I/O 是由 Aurora 数据库引擎依靠基于 SSD 的虚拟化存储层执行的输入/输出操作。每个数据库页面读取操作计为一个 I/O。Aurora 数据库引擎依靠存储层发出读取，以获取不在缓冲缓存中的数据库页面。 在兼容 PostgreSQL 的 Aurora 中，每个数据库页面为 8KB，在兼容 MySQL 的 Aurora 中，为 16KB。Aurora 的目的是消除不必要的 I/O 操作，以降低成本，并确保资源可服务于读/写流量。只有将事务日志记录推送到存储层，完成耐久型写入时，才消耗写入 I/O。写入输入/输出以 4 KB 单位计算。例如，1024 字节的事务日志记录计为一个 I/O 操作。然而，当事务日志小于 4KB 时，并发写入操作可通过 Aurora 数据库引擎批量进行，以便优化 I/O 消耗。与传统的数据库引擎不同，Amazon Aurora 从不将修改后的数据库页面推送到存储层，进一步节省了 I/O 消耗。

您可以在 AWS 控制台看到 Aurora 实例消耗的 I/O 数量。要查询 I/O 消耗，请转到控制台的 RDS 部分，查看您的实例列表，选择 Aurora 实例，然后在监控部分查找“计算的读取操作”和“计算的写入操作”指标。要了解更多详细信息，请访问 Amazon Aurora 定价页面。
# 开发人员生产力
## Trusted Language Extensions for PostgreSQL
Trusted Language Extensions (TLE) for PostgreSQL 是一个开发套件和开源项目，它使您能够快速构建高性能扩展并在 Amazon Aurora 上安全地运行，无需 AWS 验证代码。开发人员可以使用常见的受信任语言（如 JavaScript、PL/pgSQL、Perl 和 SQL）安全地编写扩展。TLE 专用于阻止访问不安全的资源和限制单个数据库连接的扩展缺陷。DBA 可以在线精确控制可安装扩展和创建用于运行这些扩展的权限模型的人员。Aurora 客户可以免费使用 TLE。

## 机器学习
Aurora 直接从数据库提供机器学习功能，让您可以通过熟悉的 SQL 编程语言将基于 ML 的预测添加到您的应用程序中。通过 Aurora 与 AWS 机器学习服务之间的简单、优化且安全的集成，您可以访问一系列 ML 算法，而无需构建自定义集成或移动数据。了解有关 Aurora 机器学习的更多信息。

## RDS Proxy 支持
Aurora 可以与完全托管式高可用数据库代理 Amazon RDS Proxy 结合使用，使应用程序更加可扩展，更能灵活地处理数据库故障，并且更具安全性。RDS Proxy 可使应用程序池化和共享已建立的数据库连接，从而提高数据库效率和应用程序的可扩展性。它通过在保留应用程序连接的同时自动连接新数据库实例来缩短故障转移时间。它通过与 AWS IAM 和 AWS Secrets Manager 集成来增强安全性。
# Amazon Aurora English
- Aurora is a proprietary technology from AWS (not open sourced)
- It provides support for both PostgreSQL and MySQL drivers in order to be able to connect to it
- Aurora is cloud optimized, it claims 5x performance over MySQL and over 3x performance over PostgreSQL
- Aurora storage automatically grows in increments from 10GB up to 64TB
- Aurora can have 15 replicas (while MySQL has only 5), replication process is faster
- Failover is Aurora is instantaneous
- Aurora costs more than classic RDS (around 20%)
- Aurora availability:
    - Stores 6 copies of the data across 3 AZs - only needs 4 copies for writes and 3 for reads
    - It has self healing properties with peer-to-peer replication
    - Storage is split across 100s of volumes
- In Aurora only one instance is used for writes (master instance)
- In case of master failure, the failover happens in less than 30 seconds
- Provides support for cross region replication

## Aurora DB Cluster

- In Aurora we always have one writer endpoint
- We can have up to 15 read replicas
- Read replicas can be inside an auto scaling groups which provides the right read capacity all the time
- Read endpoint: basically does load balancing between read replicas
- Aurora endpoints: we can map each connection to the appropriate instance or group of instances based on an use case. For example, to perform DDL statements we can connect to whichever instance is the primary instance. To perform queries, we can connect to the reader endpoint, with Aurora automatically performing load-balancing among all the Aurora Replicas. For clusters with DB instances of different capacities or configurations, we can connect to custom endpoints associated with different subsets of DB instances
- Custom endpoints: provide load-balanced database connections based on criteria other than the read-only or read-write capability of the DB instances. For example, we might define a custom endpoint to connect to instances that use a particular AWS instance class or a particular DB parameter group. Then we might tell particular groups of users about this custom endpoint. For example, we might direct internal users to low-capacity instances for report generation or ad hoc (one-time) querying, and direct production traffic to high-capacity instances

## Aurora Security

- It is similar to basic RDS security, because it is using the same engine under the hood
- Provides encryption at rest using KMS
- Provides automated backups, snapshots and replicas are also encrypted
- Encryption in flight is done using SSL
- Possibility to authenticate using IAM token
- The Aurora instance is protected with security groups (just like basic RDS)
- There is no way to SSH into an Aurora instance

## Aurora Serverless

- Provides automated database instantiation and auto-scaling based on actual usage
- Recommended for infrequent, intermittent or unpredictable workloads
- No capacity planning is needed
- Users pay per seconds, can be cost-effective

## Global Aurora

- There are two ways to have cross region replication:
    - Aurora Cross Region Read Replicas:
        - Useful for disaster recovery
        - Simple to put in place
    - Aurora Global Database (recommended):
        - We can specify one primary region for read/write
        - We can have up to 5 secondary regions (read-only)
        - Replication lag is bellow 1 second
        - We can have up to 16 read replicas per secondary region
        - In case we need to promote one region, the RTO (Recovery Time Objective) is bellow 1 minute
