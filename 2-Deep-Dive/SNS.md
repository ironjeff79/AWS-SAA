# 什么是 Amazon SNS？
+ Amazon Simple Notification Service (Amazon SNS) 是一项托管服务，提供从发布者向订阅者（也称为创建者和使用者）的消息传输。发布者通过将消息发送至主题与订阅者进行异步交流，主题是一个逻辑访问点和通信渠道。客户端可以订阅 SNS 主题并使用受支持的终端节点类型接收已发布的消息，例如 Amazon Kinesis Data Firehose、Amazon SQS、AWS Lambda、HTTP、电子邮件、移动推送通知和移动短信 (SMS)。
## 工作原理
+ Amazon Simple Notification Service (SNS) 以两种方式发送通知：A2A 和 A2P。
    + A2A 在分布式系统、微服务和事件驱动型无服务器应用程序之间进行高吞吐量、基于推送的多对多消息传递。这些应用程序包括 Amazon Simple Queue Service (SQS)、Amazon Kinesis Data Firehose、AWS Lambda 和其他 HTTPS 端点。
    + A2P 功能允许您可以通过 SMS 文本、推送通知和电子邮件向客户发送消息。 

## 使用案例
###  将应用程序与 FIFO 消息传递集成
+ 以严格排序的先进先出 (FIFO) 方式传递消息，以保持独立应用程序之间的准确性和一致性。
### 安全加密通知消息传递
+ 使用 AWS Key Management Service (KMS) 加密消息，使用 AWS PrivateLink 确保流量隐私，以及使用资源策略和标签控制访问。
### 从超过 60 种 AWS 服务中捕获和扇出事件
+ 跨 AWS 类别扇出事件，例如分析、计算、容器、数据库、IoT、机器学习 (ML)、安全性和存储。
### 向 240 多个国家/地区的客户发送 SMS 文本
+ 使用提供跨提供商冗余的全球 SMS。使用发件人 ID、长代码、短代码、TFN 或 10DLC 设置 SMS 发端身份。

# SNS - Simple Notification Service
+ Pub/Sub model
+ The event produces only sends messages to one SNS topic
+ Each subscriber to the topic will get all the messages be default (we can filter them, if we want)
+ We can have up to 10 million subscribers per topic
+ We cave up to 100K topics
+ Subscribers to the topic can be:
    + SQS
    + HTTP/HTTPS
    + Lambda
    + Emails
    + SMS messages
    + Mobile Notifications
+ Many different services integrate with SNS for notifications, fo example:
    + CloudWatch (for alarms)
    + Auto Scaling Groups notifications
    + S3 (bucket events)
    + CloudFormation (state changes)
+ How to publish?
    + In order to publish we must create a topic using the SDK
    + We may create one or many subscriptions
    + We publish data to the topic
+ Direct Publish (for mobile apps SDK)
    + Create a platform application
    + Create a platform endpoint
    + Publish to the platform endpoint
+ Direct Publish works with Google GCM, Apple APNS, Amazon ADM
# Security
+ Encryption:
    + In-flight encryption using HTTPS API
    + At-rest encryption using the KMS keys
    + Client-side encryption if the client wants to perform encryption/decryption itself
+ Access Controls: IAM policies to regulate access to the SNS API
+ SNS Access Policies (similar to S3 bucket policies):
    + Useful for cross-account access to SNS topics
    + Useful for allowing other services (S3) to write to an SNS topic
# SNS + SQS Fan Out
+ Send a message to multiple SQS queues using SNS
+ Push one in SNS, receive in all SQS queues which are subscribers
+ Fully decouples, no data loss
+ SQS allows for data persistance, delayed processing and retries of work
+ Ability to add more SQS subscribers over time
+ SQS queues must have an allow access policy for SNS to be able to write to the queues
+ SNS cannot send messages to SQS FIFO queues (AWS limitation)!
## Use case: send S3 events to multiple queues:
+ For the same combination of even type and prefix we can only have one S3 Event rule
+ In case we want to send the same S3 event to many SQS queues, we must use SNS fan-out

