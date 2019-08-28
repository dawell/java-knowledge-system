# JavaKnowledgeSystem


## 前言

作为Java后端要学习的内容实际是非常广泛的，一方面是技术深度，一方面是技术广度

自己作为互联网后端研发到架构一路跌跌撞撞走来的知识体系做个总结，后续定期更新，感兴趣的同学欢迎Star~



## 技术总结导航



### 知识广度

虽然是Java后端研发，但是其实工作要求是对自己的上下游工作样样要熟悉，一方面针对不同工种交流起来方便，一方面可以让自己的路走的更宽，比如做研发做到业务负责人就要理解产品，做活动带团队关注代码质量性能就要理解测试，做业务服务但是要排查问题就要理解中间件等等，同时架构的一种能力就是能放在全局视角看问题，上下游的知识是基础

以下根据自己常用组件记录，逐步完善

| 类型           | 技术栈核心                                                   | 备注                |
| -------------- | ------------------------------------------------------------ | ------------------- |
| Java领域       | Java生态、设计模式、虚拟机语言、其他线程模型Akka             | 需要深度掌握        |
| 工程能力       | IDE工具idea、maven、git版本管理、发布jenkins、效能工具       | 需要深度掌握        |
| 架构设计       | 领域驱动设计DDD、企业架构模式（事件驱动、分层、微服务）、开发模式（TDD、BDD）、技术演进与历史、UML | 资深研发需掌握      |
| 基础服务       | 爬虫、支付、用户会员、通知中心、中后台基础（登录、权限、工作流）、中间件、框架工具开发、安全 | 技术专家需掌握      |
| 运维能力       | linux、shell、docker、k8s、nginx、cdn、dns、监控告警、日志采集、时序DB、搜索ES、ServiceMesh、Serverless | 架构师需掌握        |
| 产品&业务能力  | 规划能力、抽象哲学、原则把控、PPT能力、管理能力、项目PMO能力&工程模式、沟通能力 | 技术管理需掌握      |
| 测试能力       | 单元测试、自动化测试、性能测试压测、全链路测试、动态链路     | 需要熟练            |
| 前端能力       | react、node、客户端、小程序、web基础（js、css、html）、中后台antdesign | 需要熟练            |
| 大数据领域技术 | HDFS、Spark、Flink、HBase、TiDB、Yarn                        | 架构师/技术专家熟练 |
| 身体能力       | 学习能力、抗压能力、身体健康                                 | 需要不断提升        |

如果是一个7年工作经验的研发，熟练掌握的技能应该可以超过100门



### Java生态

一流公司出规范，二流公司造轮子，三流公司做业务

Java规范其实包含了大量生态周边内容，这些都在JSR中，但是总结来看核心库周边的JSR都继续流行着，而扩展到外围是Spring的规范逐步支撑起一片天，目前Spring还在逐步统一分布式领域与大数据领域，所以Java生态里主要是标准规范`JSR + Spring`相关组件基本涵盖了Java的方方面面

另外还有一部分是遵循业界统一的规范



| 类别         | 核心点                                                       | 规范                                                   | 重要轮子                                      |
| ------------ | ------------------------------------------------------------ | ------------------------------------------------------ | --------------------------------------------- |
| Java语言语法 | 高级特性，面向对象，泛型、模块化、函数式、反射API            | JLS静态、Lang、Runtime、Annotation                     |                                               |
| 集合         | 数据结构、算法                                               | Collection规范                                         | guava                                         |
| 多线程       | 线程，并发工具，JUC，基于系统但扩展一套                      | Concurrent规范                                         | POSIX                                         |
| 虚拟机       | 编译优化、执行机制类加载、Java内存管理JMM、多线程Java内存模型 | 虚拟机规范（GC、字节码）、agent premain规范、debug规范 | Hotspot、在线诊断工具阿尔萨斯、greys、JDK工具 |
| IO           | 文件、网络、nio，都是基于系统API封装                         | tcpip、https、nio原生selector太难用改用                | netty、epoll                                  |



#### 工具API

| 类型        | 规范                                                         | 常用类库                                           |
| ----------- | ------------------------------------------------------------ | -------------------------------------------------- |
| 时间日期    | DateTime                                                     | Java8的                                            |
| 字符串&正则 |                                                              | 默认                                               |
| 小数        |                                                              | BigDecimal                                         |
| 封装对象    | JavaBean对象结构标准                                         | Properties扩展                                     |
| 数学函数    |                                                              | 默认Math                                           |
| 扩展        | ~~DI~~、~~SPI扩展~~                                          | ServiceLoader、DI与SPI用Spring                     |
| 格式准换    | ~~Mechanism&json&对象序列化~~、~~JAXB（统一XML&SAX）~~、~~JAF-header头转换~~ | fastjson、xml基本不用了，二进制：protobuf、hessian |
| 监控        | JMX管控                                                      | SpringBoot的web管理actuator-endpoint               |
| 安全        | JCA加密、~~JAAS认证授权~~                                    | apache加密包、认证授权Spring Security、Shiro       |
| 验证        | Bean Validation                                              | Hibernate validation                               |
| 持久化      | ~~JDO持久化~~                                                | DB/序列化文件                                      |
| 配置        | Property文件                                                 | SpringBoot自动配置                                 |
| 日志        |                                                              | slf4j、log4j2、logback                             |



#### 第三方交互

| 类型   | 规范                                                         | 常用类库                        |
| ------ | ------------------------------------------------------------ | ------------------------------- |
| 数据库 | JDBC、~~JPA-国内不用~~、SpringData封装了关系型与NoSQL数据库  | mybatis                         |
| 邮件   | Mail                                                         | 默认                            |
| 缓存   | ~~jcache~~、Spring Cache                                     | guava cache                     |
| 图形化 | ~~JTS图形相交~~                                              | swing                           |
| web    | J2EE、~~JSP~~、~~JSTL（jsp标签）~~、~~EL表达式~~、~~JSF~~、~~Portlet~~、WebSocket、Springboot | webFX、前端分离了改用react+node |
| 文档   |                                                              | swagger                         |



#### 服务治理组件

| 类型           | 常用                                          | 常用组件                                                     |
| -------------- | --------------------------------------------- | ------------------------------------------------------------ |
| 远程调用       | ~~RMI&JNDI~~、~~JAXWS&SOAP&WSDL(webservice)~~ | fegin、dubbo                                                 |
| HTTP           | REST                                          | apache httpclient                                            |
| 消息           | ~~JMS很少遵守~~、SpringCloudStream            | kafka、rabbitmq、rocketmq                                    |
| 事务           | JTA事务                                       | seata                                                        |
| 分布式配置     | SpringCloudConfig                             | config                                                       |
| 分布式注册中心 | SpringCloudDiscovery                          | eureka、zk、consul                                           |
| 分布式链路     | SpringCloudSleth                              | zipkin                                                       |
| 分布式短路降级 |                                               | alibaba sentinel、hystrix                                    |
| 分布式网关     |                                               | nginx、gateway                                               |
| 分布式负载均衡 |                                               | Ribbon、软负载                                               |
| 分布式协调     |                                               | zk                                                           |
| 分布式会话     |                                               | SpringSession                                                |
| 分布式调度     |                                               | 自研                                                         |
| 分布式ID生成   |                                               | 自研                                                         |
| 企业组件       | ~~EJB~~（可以学习下，目前微服务）             | [SpringCloud分布式组件全家桶](<http://dawell.cc/2018/08/01/SpringCloud/>) |



