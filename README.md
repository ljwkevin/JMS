# JMS
Java消息中间件学习笔记

### [00.消息中间件概述](https://github.com/Letitmiss/JMS/blob/master/README.md)
## ActiveMQ
### [01.JMS规范解析](https://github.com/Letitmiss/JMS/blob/master/blog/JMS.md)
### [02.ActiveMQ入门](https://github.com/Letitmiss/JMS/blob/master/blog/activemq.md)
### [03.SpringJMS集成ActiveMQ](https://github.com/Letitmiss/JMS/blob/master/blog/springjms.md)
### [04.ActiveMQ集群实践](https://github.com/Letitmiss/JMS/blob/master/blog/ActiveMQCluster.md)
### [05.ActiveMQ企业实践中的问题](https://github.com/Letitmiss/JMS/blob/master/blog/companyuse.md)
### [06.其他消息中间件](https://github.com/Letitmiss/JMS/blob/master/blog/others.md)

## RabbitMQ
### [01.RabbitMQ基础介绍](https://github.com/Letitmiss/JMS/blob/master/blog/rabbitmq_1.md)
### [02.RabbitMQ安装Windows](https://github.com/Letitmiss/JMS/blob/master/blog/rabbitmq-install-win.md)
### [03.RabbitMQ安装Linux](https://github.com/Letitmiss/JMS/blob/master/blog/rabbitmq-install-linux.md)
### [04.RabbitMQ入门](https://github.com/Letitmiss/JMS/blob/master/blog/rabbitmqbase.md)

# 为什么需要消息中间件？
  老王给女儿讲故事
  ![最初讲故事](https://github.com/Letitmiss/JMS/blob/master/img/001.jpg)
  
  讲故事的优化
  ![故事的优化](https://github.com/Letitmiss/JMS/blob/master/img/002.jpg)
1. 老王不用分别给两个女儿讲故事
2. 老王也不用关心电话能否打通，或者对面是否正在听(解耦 ，异步)
3. 其他人喜欢老王的故事也可以，来听听(扩展方便)

## 服务调用使得其他系统感知事件发生
  ![服务调用](https://github.com/Letitmiss/JMS/blob/master/img/003.jpg)
 1. 主要服务模块主动调用其他模块使得其他模块
 2. 系统间耦合比较大，其他模块方法修改，登陆模块也需要修改
 
## 消息中件间解耦服务调用
![消息中间件](https://github.com/Letitmiss/JMS/blob/master/img/004.jpg)

1. 通过消息中间件，登陆系统主要关注登陆，同时发起一个登陆成功消息到中间件，其他模块订阅这个消息，执行登陆成功的一系列动作；
2. 系统的耦合性明显降低，登陆模块主要关注自己的业务即可
3. 执行是异步，消息可以做安全处理，可靠
4. 保证消息顺序执行

# 消息中间件相关概念 

### 消息中间概述
 
*  关注数据的发送和接受，利用高效可靠的异步消息传递机制集成了分布式系统

### 什么是JMS?
*  Java消息服务（Java Message Service）,是一个Java平台中关于面向消息的中间件的API，用于两个应用程序之间或者分布式
    系统中发布消息，进行异步通信。
    
### 什么是AMQP?
*  AMQP，即Advanced Message Queuing Protocol,一个提供统一消息服务的应用层标准高级消息队列协议,是应用层协议的一个开放标准,为面向消息的中间件设计。    基于此协议的客户端与消息中间件可传递消息，并不受客户端/中间件不同产品，不同的开发语言等条件的限制。Erlang中的实现有 RabbitMQ等。

### JMS和AMQP的比价
  ![对比](https://github.com/Letitmiss/JMS/blob/master/img/005.jpg)


### 常见的消息中间件

### 1.ActiveMQ
1.  ActiveMQ 是Apache出品，最流行的，能力强劲的开源消息总线。ActiveMQ 是一个完全支持JMS1.1和J2EE 1.4规范的 JMS Provider实现，尽管JMS规范出台已经是很久的事情了，但是JMS在当今的J2EE应用中间仍然扮演着特殊的地位。
2.  特性
*  多种语言和协议编写客户端。语言: Java,C,C++,C#,Ruby,Perl,Python,PHP。应用协议： OpenWire,Stomp REST,WS Notification,XMPP,AMQP
*  完全支持JMS1.1和J2EE 1.4规范 （持久化，XA消息，事务)
*  对Spring的支持，ActiveMQ可以很容易内嵌到使用Spring的系统里面去，而且也支持Spring2.0的特性
### 2.RabbitMQ
1. RabbitMQ是一个在AMQP基础上完整的，可复用的企业消息系统。它可以用于大型软件系统各个模块之间的高效通信，支持高并发，支持可扩展。MQ是消费-生产者模型的一个典型的代表，一端往消息队列中不断写入消息，而另一端则可以读取或者订阅队列中的消息。MQ和JMS类似，但不同的是JMS是SUN JAVA消息中间件服务的一个标准和API定义，而MQ则是遵循了AMQP协议的具体实现和产品。
2. 特性 
*  支持多种客户端
* AMQP的完整实现
* 事务支持/发布确认
* 消息持久化 
### 3.KafKa
1. Kafka是一种高吞吐量的分布式发布订阅消息系统，它可以处理消费者规模的网站中的所有动作流数据。 这种动作（网页浏览，搜索和其他用户的行动）是在现代网络上的许多社会功能的一个关键因素。 这些数据通常是由于吞吐量的要求而通过处理日志和日志聚合来解决。 对于像Hadoop的一样的日志数据和离线分析系统，但又要求实时处理的限制，这是一个可行的解决方案。Kafka的目的是通过Hadoop的并行加载机制来统一线上和离线的消息处理，也是为了通过集群来提供实时的消费。
2. 特性
* 通过O(1)的磁盘数据结构提供消息的持久化，这种结构对于即使数以TB的消息存储也能够保持长时间的稳定性能。
* 高吞吐量：即使是非常普通的硬件Kafka也可以支持每秒数百万 的消息。
* 支持通过Kafka服务器和消费机集群来分区消息。

### 消息中间件对比
 ![综合比较](https://github.com/Letitmiss/JMS/blob/master/img/009.jpg)









    




