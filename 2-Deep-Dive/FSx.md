# Amazon FSx
## Amazon FSx for Windows
- EFS is a shared POSIX file system for Linux, meaning it can not be used with Windows
- FSx for Windows is a fully managed Windows file system share drive
- Supports SMB protocol and Windows NTFS
- It has Active Directory integration, ACLs and user quotas
- It is built on top of SSD, it can scale up to 10s of GB/s, millions of IOPS and 100s PB of data
- It can accessed from on-premise infrastructure
- It can be configured to be Multi-AZ (high availability)
- Data is backed-up daily to S3

## Amazon FSx for Lustre
- Lustre is a type of parallel distributed file system for large-scale computing
- Lustre is derived from "Linux" and "cluster"
- FSx for Lustre is used with machine learning and High Performance Computing (HPC), example: video processing, financial modelling, electronic design automation
- Scales up to 100s GB/s, millions of IOPS, sub-ms latencies
- It has seamless integration with S3
    - Can "read" S3 as a file system
    - Can write the output of the computations back to S3
- It can be used with on-premise servers

## Storage Comparison
- S3: Object Storage
- Glacier: Object Archival
- EFS: Network File System for Linux instances, POSIX filesystem
- FSx for Windows: Network File System for Windows servers
- FSx for Lustre: High Performance Computing for Linux systems
- EBS volumes: Network storage for one EC2 instance at a time
- Instance Storage: Physical storage for EC2 instance (high IOPS)
- Storage Gateway
- Snowball / Snowmobile: move large data to the cloud, physical

## Fsx 和 EFS的区别
- FSx和EFS最大的区别是：EFS是多租户共享的文件系统，后台是一个统一的分布式文件系统基础设施。FSx是每个租户内建自己独立的一套文件服务器，所以在性能上有保障，功能更多样化，可以有不同的高可用级别设置和基于成本的灵活配置。

## Amazon FSx for windows
顾名思义，FSx for windows主要用于Windows系统，提供了Server Message Block（SMB）的协议。该系统在Windows Server上实现，并实现了 Microsoft Active Directory（AD）的集成，文件数据恢复和数据重删的功能。

FSx for Windows File Server提供了两个部署选项：single-AZ和multi-AZ。另外还提供了data backup，data encryption for data in transit and at rest。

主要的应用场景：web serving, home directories, content management, continuous integration (CI) workflows and data analytics.

## Amazon FSx for Lustre
Lustre是众所周知的开源的并行文件系统，主要用于高性能的场景，范围包括：machine leaning，video rendering，hight performance computing and financial simulations.

FSx for Lustre 可以提供 sub-millisecond的延迟， 上百万的IOPS，上百G的带宽。

## Amazon FSx for NetApp ONTAP
通过和NetApp的合作，AWS发布了Amazon FSx for NetApp ONTAP：一个基于云的共享文件和块的存储服务。通过NetApp的先进的数据管理系统，ONTAP提供NFS，SMB，iSCSC存储协议，主要的特点如下：

- 多种文件和block协议的支持
- 跨多个AZ的高可用
- 数据保护和数据恢复功能(data protection and disaster recovery)
- 自动分层存储到S3， 数据即时到克隆
- 丰富的管控能力：GUI or RESTful API access, control and automation through NetApp Cloud Manager
- 多云和混合云架构：Operation across hybrid and multicloud architectures

## Amazon FSx for OpenZFS
基于开源的OpenZFS文件系统建立的云上的文件存储。OpenZFS是一个共享的单机版的的文件系统，主要特点:

- 性能优异：达到1 million IOPS和数百微妙的延迟(up to 1 million IOPS and hundred of microseconds latency)
- OpenZFS实现了即时到快照和克隆的功能，对开发测试环境比较合适。
- 丰富的配置，数据压缩功能，可以很好的优化成本

Amazon FSx for OpenZFS的高可用基于文件系统内置的定期把文件系统的数据备份到S3 Bucket上实现。用户也可以自定义备份策略。

**推荐的应用场景**：

1. 无缝迁移：用户现有的运行在ZFS或者其它linux 文件服务器上的应用程序可以无缝的迁移到Amazon OpenZFS上。
2. 高性能的场景：Machine Leaning，financial analytics, and other data-intensive applications with high-IOPS storage.
3. Content Manager：file-based web serving and content management applications including WordPress, Drupal, and Magento.
4. 开发测试环境：Test changes efficiently by cloning application data in seconds, and reduce build times with fast storage for repositories and DevOps solutions, such as Git, Bitbucket, and Jenkins.

OpenZFS的优点是：性能优异，功能丰富（snapshot，clone，encryption，compression），适合原来使用Linux file Server的应用等无缝迁移。缺点也很明显：由于ZFS是个本地文件系统，基于ZFS的文件服务器也是单机版的文件服务器。性能虽然优异但是和Lustre比不在一个级别。由于高可用的问题，更多应用于开发测试环境和可用性要求不高的场景。

## 总结

- **EFS** is primarily used for NFS and Linux-based workloads
- **FSx for Windows** provides a managed file sharing solution for Windows-based workloads that use the SMB protocol
- **FSx for Lustre** is a high-performance file sharing solution for Linux-based workloads
- **Amazon FSx for NetApp ONTAP** supports NFS, SMB, and iSCSI, enables hybrid deployment, and provides advanced storage management features

从AWS在云上推出FSx系列文件系统就可以看出：

- **在云上运行传统的HPC，EDA等分布式文件系统等传统应用场景越来越多，FSx正是针对这一趋势而应对的解决方案。**
- **文件系统的应用场景比较广泛：没有one-fit-all的场景，不同的场景对文件系统的需求不同，各种类型的文件系统有自己的独特的应用场景。**
- **在目前多云的场景下，客户不希望被云厂商锁定，独立第三方的云上的分布式文件系统是一个机会。**