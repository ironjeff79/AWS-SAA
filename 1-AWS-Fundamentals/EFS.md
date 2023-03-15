# Amazon Elastic File System (Amazon EFS) 
为基于 Linux 的工作负载提供简单、可扩展的弹性文件系统，可与 AWS 云服务和本地资源配合使用。它可在不中断应用程序的情况下按需扩展到 PB 级，在您添加或删除文件时自动扩展或缩减，从而让您的应用程序在需要时获得所需存储。它旨在为数千个 Amazon EC2 实例提供大规模并行共享访问模式，可让您的应用程序在一致、低延迟的状态下实现高水平的总吞吐量和 IOPS。Amazon EFS 是一项完全托管的服务，不需要对现有应用程序和工具进行更改，并通过标准的文件系统界面提供访问以实现无缝集成。Amazon EFS 提供标准和不频繁访问存储类。通过使用生命周期管理，可将 30 天未访问的文件自动移动到成本优化型不频繁访问存储类，让您可以在同一文件系统中轻松存储和访问活动的不经常访问文件系统数据，同时存储成本降低高达 85%。Amazon EFS 是一种用于在多个可用区 (AZ) 中存储数据以提供高可用性和持久性的区域服务。您可以跨可用区、区域和 VPC 访问文件系统，并可以通过 AWS Direct Connect 或 AWS ××× 在数千个 Amazon EC2 实例与本地服务器之间共享文件。

| 			 | Application Load Balancer |   Network Load Balancer |   
| :------------- | :----------: | ------------: |
| 每次操作的延迟 |  低且一致的延迟 | 最低且一致的延迟 |
| 吞吐量规模 |  每秒10+GB | 每秒最多2GB |
| 可用性于持久性 |数据冗余存储在多个可用区中 | 数据冗余存储在一个可用区中 |
| 访问 | 多个可用区的多达数千个EC2实例可以同时连接到一个文件系统 | 一个可用区的一个EC2  实例可以链接到一个文件系统 |
| 使用案例 |  大数据和分析，媒体处理工作流，内容管理，Web服务和主目录 | 引导卷，事务型数据库和NoSQL数据库，数据仓库和ETL |


## EFS - Elastic File System
- EFS is a managed NFS (network file system) that can be mounted on many EC2 instances
- EFS works with EC2 instances across multi AZs
- EFS is highly available, scalable, but also more expensive (3x GP2) than EBS
- EFS is pay per use
- Use cases: content management, web service, data sharing, Wordpress
- Uses NFSv4.1 protocol
- We can use security groups to control access to EFS volumes
- EFS is only compatible with Linux based AMIs (not Windows)

## EFS Performance and Storage Classes
- EFS Scale
    - Thousands of concurrent NFS clients, 10 GB+ per second throughput
    - It can grow to petabyte scale NFS automatically
- Performance mode (can be set at EFS creation time)
    - General purpose (default): recommended for latency-sensitive use cases: web server, CMS, etc.
    - Max I/O - higher latency, throughput, highly parallel, recommended for big data, media processing
- Storage tiers: lifecycle manage feature
    - Standard: for frequently accessed files
    - Infrequent access (EFS-IA): there is a cost to retrieve files, lower price per storage