# CloudWatch [工作方式和术语概念](https://www.jianshu.com/p/68397ea4588d)
使用 Amazon CloudWatch 可以收集和跟踪各项指标、收集和监控日志文件、设置警报以及自动应对 AWS 资源的更改。Amazon CloudWatch 可以监控各种 AWS 资源，例如 Amazon EC2 实例、Amazon DynamoDB 表、Amazon RDS 数据库实例、应用程序和服务生成的自定义指标以及应用程序生成的所有日志文件。您可通过使用 Amazon CloudWatch 全面地了解资源使用率、应用程序性能和运行状况。使用这些分析结果，您可以及时做出反应，保证应用程序顺畅运行。
- 监控资源和应用程序，捕获日志并发送事件。
- CloudWatch监控是保持AWS资源标签的标准机制。CloudWatch提供了大量**指标和维度**，使您可以创建基于时间的图形，**警报**和**仪表盘**。
- 警报是CloudWatch最实际的用法，允许您触发任何指定的指标。
- 警报可以触发*SNS通知*，*Auto Scaling操作*或*EC2操作*。
- 通过创建可自定义的仪表板视图来发布和共享指标图。
- 监视并报告EC2 实例系统检查失败警报。



## **使用CloudWatch事件**：
- 事件创建一种机制来自动化AWS上各种服务中的操作。您可以从实例状态，AWS API，Auto Scaling，运行命令，部署或基于时间的计划（想想Cron）创建事件规则。
- 触发事件可以调用Lambda函数，发送SNS / SQS / Kinesis消息，或执行实例操作（终止，重新启动，停止或快照卷）。
- 自定义有效载荷可以发送到JSON格式的目标，这在触发Lambdas时特别有用。

## 使用CloudWatch日志：
- CloudWatch Logs是一个流式日志存储系统。通过在AWS中存储日志，您可以访问无限制的付费存储，但是您也可以选择直接将日志流式传输到ElasticSearch或自定义Lambda。
- 安装在您的服务器上的日志代理将随着时间的推移处理日志，并将其发送到CloudWatch日志。
您可以将记录的数据导出到S3或将结果导出到其他AWS服务。
- 详细监控： 必须启用对EC2实例的详细监控才能获取详细指标，并在CloudWatch下进行收费。

## CloudWatch提示
- CloudWatch的一些非常常见的用例包括计费警报，实例或负载均衡器上/下警报以及磁盘使用警报。
- 可以使用EC2Config监视Windows平台实例上的监视内存和磁盘指标。对于Linux，有一些脚本可以做同样的事情。
- 可以使用AWS API 发布自己的指标。增加了额外的成本。
- 可以通过在日志组上创建订阅，直接从CloudWatch Logs流式传输到Lambda或ElasticSearch集群。
- 不要忘记利用CloudWatch不过期的免费套餐。

## 术语概念
Amazon CloudWatch 有以下几个核心术语和概念：

 命名空间
 指标
 维度
 统计数据
 百分位数
 警报
**1. 命名空间(Namespace)**
记录监控指标的所属，不同命名空间中的指标彼此独立。例如 CPUUtilization 是一个监控指标，表示 CPU使用率，如果单单只靠这个名字，我们很难判断这个是虚拟机、容器、还是物理主机的。
这时候就需要额外的概念（即这里的“命令空间”）来区分它，Amazon约定使用 AWS/service 的方式表示命名空间，例如：AWS/EC2 表示 Amazon EC2 虚拟机， AWS/ECS 表示容器，AWS/ELB 表示负载均衡。。。

**2. 指标(Metric)**
和其他监控系统的概念一样，表示监控的内容项目，如：CPU使用率，内存占用率。
指标数据点
是对于每个指标而言，具体某一时间（时间戳）的数据。
指标的所有监控数据，就是由间隔固定的时间段，所采集和记录的一个个数据点组成。
指标保留
每个时间段的指标数据点保存一定时间后，会进行聚合，以来实现长期存储。

- 时间段短于 60 秒的数据点，保持3小时
- 时间段为60 秒（1分钟）的数据点，保持15天
- 时间段为300秒（5分钟）的数据点，保持63天
- 时间段为3600秒（1小时）的数据点，保持455天（15个月）
较短时间段的数据点，在超过保持时间后，会聚合成较长一个时间段的数据点。即：60秒数据过期（超过15天），集合成300秒数据；300秒数据过期（超过63天），聚合成3600秒数据。
CloudWatch 会保留 5 分钟和 1 小时数据。

**3. 维度(Metric)**
维度可以理解是给指标追加的 label ，每个指标可以配置10个维度。
可以通过单个维度，或者维度组合来对指标和数据进行筛选。

**4. 统计数据(Statistics)**
是指定时间段内的指标数据聚合，可用的统计数据有：

- Minimum :最小值
- Maximum ：最大值
- Sum ：总和
- Average ：平均值
- SampleCount，数据点计数 (数量) ，用于统计信息的计算。
- pNN.NN，指定的百分位数的值

**5. 百分位数**
指示某个值在数据集中的相对位置。例如，第 95 个百分位数表示 95% 的数据低于此值，5% 的数据高于此值。百分位数可帮助您更好地了解指标数据的分布情况。

**6. 警报(Alarm)**
在指定的时间段内监控单个指标，并根据指标值相对于阈值的变化情况执行一项或多项指定操作。
Amazon CloudWatch 的警报不单单能发出警报通知，还可以执行一定的操作，例如重启/关闭虚拟机

https://blog.csdn.net/NewTyun/article/details/105384430