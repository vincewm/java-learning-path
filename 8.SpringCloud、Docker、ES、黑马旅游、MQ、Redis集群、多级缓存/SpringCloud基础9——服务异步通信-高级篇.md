>  **导航：**
> 
> [【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析](https://blog.csdn.net/qq_40991313/article/details/126646289?csdn_share_tail=%7B%22type%22%3A%22blog%22%2C%22rType%22%3A%22article%22%2C%22rId%22%3A%22126646289%22%2C%22source%22%3A%22qq_40991313%22%7D "【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析")

**目录**

[服务异步通信-高级篇](#%E6%9C%8D%E5%8A%A1%E5%BC%82%E6%AD%A5%E9%80%9A%E4%BF%A1-%E9%AB%98%E7%BA%A7%E7%AF%87)

[1.消息可靠性](#1.%E6%B6%88%E6%81%AF%E5%8F%AF%E9%9D%A0%E6%80%A7)

[1.1.生产者消息确认](#1.1.%E7%94%9F%E4%BA%A7%E8%80%85%E6%B6%88%E6%81%AF%E7%A1%AE%E8%AE%A4)

[1.1.1.修改配置](#1.1.1.%E4%BF%AE%E6%94%B9%E9%85%8D%E7%BD%AE)

[1.1.2.定义Return回调](#1.1.2.%E5%AE%9A%E4%B9%89Return%E5%9B%9E%E8%B0%83)

[1.1.3.定义ConfirmCallback](#1.1.3.%E5%AE%9A%E4%B9%89ConfirmCallback)

[1.2.消息持久化](#1.2.%E6%B6%88%E6%81%AF%E6%8C%81%E4%B9%85%E5%8C%96)

[1.2.1.交换机持久化](#1.2.1.%E4%BA%A4%E6%8D%A2%E6%9C%BA%E6%8C%81%E4%B9%85%E5%8C%96)

[1.2.2.队列持久化](#1.2.2.%E9%98%9F%E5%88%97%E6%8C%81%E4%B9%85%E5%8C%96)

[1.2.3.消息持久化](#1.2.3.%E6%B6%88%E6%81%AF%E6%8C%81%E4%B9%85%E5%8C%96)

[1.3.消费者消息确认](#1.3.%E6%B6%88%E8%B4%B9%E8%80%85%E6%B6%88%E6%81%AF%E7%A1%AE%E8%AE%A4)

[1.3.1.演示none模式](#1.3.1.%E6%BC%94%E7%A4%BAnone%E6%A8%A1%E5%BC%8F)

[1.3.2.演示auto模式](#1.3.2.%E6%BC%94%E7%A4%BAauto%E6%A8%A1%E5%BC%8F)

[1.4.消费失败重试机制](#1.4.%E6%B6%88%E8%B4%B9%E5%A4%B1%E8%B4%A5%E9%87%8D%E8%AF%95%E6%9C%BA%E5%88%B6)

[1.4.1.本地重试](#1.4.1.%E6%9C%AC%E5%9C%B0%E9%87%8D%E8%AF%95)

[1.4.2.失败策略](#1.4.2.%E5%A4%B1%E8%B4%A5%E7%AD%96%E7%95%A5)

[1.5.总结](#1.5.%E6%80%BB%E7%BB%93)

[2.死信交换机](#2.%E6%AD%BB%E4%BF%A1%E4%BA%A4%E6%8D%A2%E6%9C%BA)

[2.1.初识死信交换机](#2.1.%E5%88%9D%E8%AF%86%E6%AD%BB%E4%BF%A1%E4%BA%A4%E6%8D%A2%E6%9C%BA)

[2.1.1.什么是死信交换机](#2.1.1.%E4%BB%80%E4%B9%88%E6%98%AF%E6%AD%BB%E4%BF%A1%E4%BA%A4%E6%8D%A2%E6%9C%BA)

[2.1.2.利用死信交换机接收死信（拓展）](#2.1.2.%E5%88%A9%E7%94%A8%E6%AD%BB%E4%BF%A1%E4%BA%A4%E6%8D%A2%E6%9C%BA%E6%8E%A5%E6%94%B6%E6%AD%BB%E4%BF%A1%EF%BC%88%E6%8B%93%E5%B1%95%EF%BC%89)

[2.1.3.总结](#2.1.3.%E6%80%BB%E7%BB%93)

[2.2.TTL](#2.2.TTL)

[2.2.1.接收超时死信的死信交换机](#2.2.1.%E6%8E%A5%E6%94%B6%E8%B6%85%E6%97%B6%E6%AD%BB%E4%BF%A1%E7%9A%84%E6%AD%BB%E4%BF%A1%E4%BA%A4%E6%8D%A2%E6%9C%BA)

[2.2.2.声明一个队列，并且指定TTL](#2.2.2.%E5%A3%B0%E6%98%8E%E4%B8%80%E4%B8%AA%E9%98%9F%E5%88%97%EF%BC%8C%E5%B9%B6%E4%B8%94%E6%8C%87%E5%AE%9ATTL)

[2.2.3.发送消息时，设定TTL](#2.2.3.%E5%8F%91%E9%80%81%E6%B6%88%E6%81%AF%E6%97%B6%EF%BC%8C%E8%AE%BE%E5%AE%9ATTL)

[2.2.4.总结](#2.2.4.%E6%80%BB%E7%BB%93)

[2.3.延迟队列](#2.3.%E5%BB%B6%E8%BF%9F%E9%98%9F%E5%88%97)

[2.3.1.安装DelayExchange插件](#2.3.1.%E5%AE%89%E8%A3%85DelayExchange%E6%8F%92%E4%BB%B6)

[2.3.2.DelayExchange原理](#2.3.2.DelayExchange%E5%8E%9F%E7%90%86)

[2.3.3.使用DelayExchange](#2.3.3.%E4%BD%BF%E7%94%A8DelayExchange)

[2.3.4.总结](#2.3.4.%E6%80%BB%E7%BB%93)

[3.惰性队列](#3.%E6%83%B0%E6%80%A7%E9%98%9F%E5%88%97)

[3.1.消息堆积问题](#3.1.%E6%B6%88%E6%81%AF%E5%A0%86%E7%A7%AF%E9%97%AE%E9%A2%98)

[3.2.惰性队列](#3.2.%E6%83%B0%E6%80%A7%E9%98%9F%E5%88%97)

[3.2.1.基于命令行设置lazy-queue](#3.2.1.%E5%9F%BA%E4%BA%8E%E5%91%BD%E4%BB%A4%E8%A1%8C%E8%AE%BE%E7%BD%AElazy-queue)

[3.2.2.基于@Bean声明lazy-queue](#3.2.2.%E5%9F%BA%E4%BA%8E%40Bean%E5%A3%B0%E6%98%8Elazy-queue)

[3.2.3.基于@RabbitListener声明LazyQueue](#3.2.3.%E5%9F%BA%E4%BA%8E%40RabbitListener%E5%A3%B0%E6%98%8ELazyQueue)

[3.3.总结](#3.3.%E6%80%BB%E7%BB%93)

[4.MQ集群](#4.MQ%E9%9B%86%E7%BE%A4)

[4.1.集群分类](#4.1.%E9%9B%86%E7%BE%A4%E5%88%86%E7%B1%BB)

[4.2.普通集群](#4.2.%E6%99%AE%E9%80%9A%E9%9B%86%E7%BE%A4)

[4.2.1.集群结构和特征](#4.2.1.%E9%9B%86%E7%BE%A4%E7%BB%93%E6%9E%84%E5%92%8C%E7%89%B9%E5%BE%81)

[4.2.2.部署](#4.2.2.%E9%83%A8%E7%BD%B2)

[4.3.镜像集群](#4.3.%E9%95%9C%E5%83%8F%E9%9B%86%E7%BE%A4)

[4.3.1.集群结构和特征](#4.3.1.%E9%9B%86%E7%BE%A4%E7%BB%93%E6%9E%84%E5%92%8C%E7%89%B9%E5%BE%81)

[4.3.2.部署](#4.3.2.%E9%83%A8%E7%BD%B2)

[4.4.仲裁队列](#4.4.%E4%BB%B2%E8%A3%81%E9%98%9F%E5%88%97)

[4.4.1.集群特征](#4.4.1.%E9%9B%86%E7%BE%A4%E7%89%B9%E5%BE%81)

[4.4.2.部署](#4.4.2.%E9%83%A8%E7%BD%B2)

[4.4.3.Java代码创建仲裁队列](#4.4.3.Java%E4%BB%A3%E7%A0%81%E5%88%9B%E5%BB%BA%E4%BB%B2%E8%A3%81%E9%98%9F%E5%88%97)

[4.4.4.SpringAMQP连接MQ集群](#4.4.4.SpringAMQP%E8%BF%9E%E6%8E%A5MQ%E9%9B%86%E7%BE%A4)

--

## 服务异步通信-高级篇

消息队列在使用过程中，面临着很多实际问题需要思考：

![image-20210718155003157](https://i-blog.csdnimg.cn/blog_migrate/38194bd8a5fb41db7808e518adb2b2c0.png)

## 1.消息可靠性

消息从发送，到消费者接收，会经理多个过程：

![image-20210718155059371](https://i-blog.csdnimg.cn/blog_migrate/e5c944c702935091b6ff80f8be7c25d8.png)

其中的每一步都可能导致消息丢失，常见的丢失原因包括：

-   发送时丢失：
    -   生产者发送的消息未送达exchange
    -   消息到达exchange后未到达queue
-   MQ宕机，queue将消息丢失
-   consumer接收到消息后未消费就宕机

针对这些问题，RabbitMQ分别给出了解决方案：

-   生产者确认机制
-   mq持久化
-   消费者确认机制
-   失败重试机制

下面我们就通过案例来演示每一个步骤。

首先，导入课前资料提供的demo工程：

![image-20210718155328927](https://i-blog.csdnimg.cn/blog_migrate/0aa23c3f45d8c5f0c1b284937079bf25.png)

项目结构如下：

![image-20210718155448734](https://i-blog.csdnimg.cn/blog_migrate/0146410a6286bb458fc9f08e62cb85c5.png)

### 1.1.生产者消息确认

RabbitMQ提供了publisher confirm机制来避免消息发送到MQ过程中丢失。这种机制必须给每个消息指定一个唯一ID。消息发送到MQ以后，会返回一个结果给发送者，表示消息是否处理成功。

返回结果有两种方式：

-   publisher-confirm，发送者确认
    -   消息成功投递到交换机，返回ack
    -   消息未投递到交换机，返回nack
-   publisher-return，发送者回执
    -   消息投递到交换机了，但是没有路由到队列。返回ACK，及路由失败原因。

![image-20210718160907166](https://i-blog.csdnimg.cn/blog_migrate/e9ce939e8bb999a9118a27973ff21017.png)

注意：

![image-20210718161707992](https://i-blog.csdnimg.cn/blog_migrate/6a4085e593de02afb35c0e1358487581.png)

#### 1.1.1.修改配置

首先，修改publisher服务中的application.yml文件，添加下面的内容：

```bash
spring:
  rabbitmq:
    publisher-confirm-type: correlated
    publisher-returns: true
    template:
      mandatory: true
   
```

说明：

-   `publish-confirm-type`：开启publisher-confirm，这里支持两种类型：
    -   `simple`：同步等待confirm结果，直到超时
    -   `correlated`：异步回调，定义ConfirmCallback，MQ返回结果时会回调这个ConfirmCallback
-   `publish-returns`：开启publish-return功能，同样是基于callback机制，不过是定义ReturnCallback
-   `template.mandatory`：定义消息路由失败时的策略。true，则调用ReturnCallback；false：则直接丢弃消息

#### 1.1.2.定义Return回调

每个RabbitTemplate只能配置一个ReturnCallback，因此需要在项目加载时配置：

修改publisher服务，添加一个：

```java
package cn.itcast.mq.config;

import lombok.extern.slf4j.Slf4j;
import org.springframework.amqp.rabbit.core.RabbitTemplate;
import org.springframework.beans.BeansException;
import org.springframework.context.ApplicationContext;
import org.springframework.context.ApplicationContextAware;
import org.springframework.context.annotation.Configuration;

@Slf4j
@Configuration
public class CommonConfig implements ApplicationContextAware {
    @Override
    public void setApplicationContext(ApplicationContext applicationContext) throws BeansException {
        // 获取RabbitTemplate
        RabbitTemplate rabbitTemplate = applicationContext.getBean(RabbitTemplate.class);
        // 设置ReturnCallback
        rabbitTemplate.setReturnCallback((message, replyCode, replyText, exchange, routingKey) -> {
            // 投递失败，记录日志
            log.info("消息发送失败，应答码{}，原因{}，交换机{}，路由键{},消息{}",
                     replyCode, replyText, exchange, routingKey, message.toString());
            // 如果有业务需要，可以重发消息
        });
    }
}
```

#### 1.1.3.定义ConfirmCallback

ConfirmCallback可以在发送消息时指定，因为每个业务处理confirm成功或失败的逻辑不一定相同。

在publisher服务的cn.itcast.mq.spring.SpringAmqpTest类中，定义一个单元测试方法：

```java
public void testSendMessage2SimpleQueue() throws InterruptedException {
    // 1.消息体
    String message = "hello, spring amqp!";
    // 2.全局唯一的消息ID，需要封装到CorrelationData中
    CorrelationData correlationData = new CorrelationData(UUID.randomUUID().toString());
    // 3.添加callback
    correlationData.getFuture().addCallback(
        result -> {
            if(result.isAck()){
                // 3.1.ack，消息成功
                log.debug("消息发送成功, ID:{}", correlationData.getId());
            }else{
                // 3.2.nack，消息失败
                log.error("消息发送失败, ID:{}, 原因{}",correlationData.getId(), result.getReason());
            }
        },
        ex -> log.error("消息发送异常, ID:{}, 原因{}",correlationData.getId(),ex.getMessage())
    );
    // 4.发送消息
    rabbitTemplate.convertAndSend("task.direct", "task", message, correlationData);

    // 休眠一会儿，等待ack回执
    Thread.sleep(2000);
}
```

### 1.2.消息持久化

生产者确认可以确保消息投递到RabbitMQ的队列中，但是消息发送到RabbitMQ以后，如果突然宕机，也可能导致消息丢失。

要想确保消息在RabbitMQ中安全保存，必须开启消息持久化机制。

-   交换机持久化
-   队列持久化
-   消息持久化

#### 1.2.1.交换机持久化

RabbitMQ中交换机默认是非持久化的，mq重启后就丢失。

SpringAMQP中可以通过代码指定交换机持久化：

```java
@Bean
public DirectExchange simpleExchange(){
    // 三个参数：交换机名称、是否持久化、当没有queue与其绑定时是否自动删除
    return new DirectExchange("simple.direct", true, false);
}
```

事实上，默认情况下，由SpringAMQP声明的交换机都是持久化的。

可以在RabbitMQ控制台看到持久化的交换机都会带上`D`的标示：

![image-20210718164412450](https://i-blog.csdnimg.cn/blog_migrate/d89ff5884903296ba521e2c83d76c6b8.png)

#### 1.2.2.队列持久化

RabbitMQ中队列默认是非持久化的，mq重启后就丢失。

SpringAMQP中可以通过代码指定交换机持久化：

```java
@Bean
public Queue simpleQueue(){
    // 使用QueueBuilder构建队列，durable就是持久化的
    return QueueBuilder.durable("simple.queue").build();
}
```

事实上，默认情况下，由SpringAMQP声明的队列都是持久化的。

可以在RabbitMQ控制台看到持久化的队列都会带上`D`的标示：

![image-20210718164729543](https://i-blog.csdnimg.cn/blog_migrate/860c18118d058f39f40fcf5fe8863aec.png)

#### 1.2.3.消息持久化

利用SpringAMQP发送消息时，可以设置消息的属性（MessageProperties），指定delivery-mode：

-   1：非持久化
-   2：持久化

用java代码指定：

![image-20210718165100016](https://i-blog.csdnimg.cn/blog_migrate/8ee9b457b8206e10d548e1a069e832b3.png)

默认情况下，SpringAMQP发出的任何消息都是持久化的，不用特意指定。

### 1.3.消费者消息确认

RabbitMQ是**阅后即焚**机制，RabbitMQ确认消息被消费者消费后会立刻删除。

而RabbitMQ是通过消费者回执来确认消费者是否成功处理消息的：消费者获取消息后，应该向RabbitMQ发送ACK回执，表明自己已经处理消息。

设想这样的场景：

-   1）RabbitMQ投递消息给消费者
-   2）消费者获取消息后，返回ACK给RabbitMQ
-   3）RabbitMQ删除消息
-   4）消费者宕机，消息尚未处理

这样，消息就丢失了。因此消费者返回ACK的时机非常重要。

而SpringAMQP则允许配置三种确认模式：

•manual：手动ack，需要在业务代码结束后，调用api发送ack。

•auto：自动ack，由spring监测listener代码是否出现异常，没有异常则返回ack；抛出异常则返回nack

•none：关闭ack，MQ假定消费者获取消息后会成功处理，因此消息投递后立即被删除

由此可知：

-   none模式下，消息投递是不可靠的，可能丢失
-   auto模式类似事务机制，出现异常时返回nack，消息回滚到mq；没有异常，返回ack
-   manual：自己根据业务情况，判断什么时候该ack

一般，我们都是使用默认的auto即可。

#### 1.3.1.演示none模式

修改consumer服务的application.yml文件，添加下面内容：

```bash
spring:
  rabbitmq:
    listener:
      simple:
        acknowledge-mode: none # 关闭ack
```

修改consumer服务的SpringRabbitListener类中的方法，模拟一个消息处理异常：

```java
@RabbitListener(queues = "simple.queue")
public void listenSimpleQueue(String msg) {
    log.info("消费者接收到simple.queue的消息：【{}】", msg);
    // 模拟异常
    System.out.println(1 / 0);
    log.debug("消息处理完成！");
}
```

测试可以发现，当消息处理抛异常时，消息依然被RabbitMQ删除了。

#### 1.3.2.演示auto模式

再次把确认机制修改为auto:

```bash
spring:
  rabbitmq:
    listener:
      simple:
        acknowledge-mode: auto # 关闭ack
```

在异常位置打断点，再次发送消息，程序卡在断点时，可以发现此时消息状态为unack（未确定状态）：

![image-20210718171705383](https://i-blog.csdnimg.cn/blog_migrate/d6625b31395afefa7962696ba6103795.png)

抛出异常后，因为Spring会自动返回nack，所以消息恢复至Ready状态，并且没有被RabbitMQ删除：

![image-20210718171759179](https://i-blog.csdnimg.cn/blog_migrate/ac4f8d1897f407e4fb7290927ccb7ab3.png)

### 1.4.消费失败重试机制

当消费者出现异常后，消息会不断requeue（重入队）到队列，再重新发送给消费者，然后再次异常，再次requeue，无限循环，导致mq的消息处理飙升，带来不必要的压力：

![image-20210718172746378](https://i-blog.csdnimg.cn/blog_migrate/267bd3c8f4a2917cfb2e59dd9e97a861.png)

怎么办呢？

#### 1.4.1.本地重试

我们可以利用Spring的retry机制，在消费者出现异常时利用本地重试，而不是无限制的requeue到mq队列。

修改consumer服务的application.yml文件，添加内容：

```bash
spring:
  rabbitmq:
    listener:
      simple:
        retry:
          enabled: true # 开启消费者失败重试
          initial-interval: 1000 # 初识的失败等待时长为1秒
          multiplier: 1 # 失败的等待时长倍数，下次等待时长 = multiplier * last-interval
          max-attempts: 3 # 最大重试次数
          stateless: true # true无状态；false有状态。如果业务中包含事务，这里改为false
```

重启consumer服务，重复之前的测试。可以发现：

-   在重试3次后，SpringAMQP会抛出异常AmqpRejectAndDontRequeueException，说明本地重试触发了
-   查看RabbitMQ控制台，发现消息被删除了，说明最后SpringAMQP返回的是ack，mq删除消息了

结论：

-   开启本地重试时，消息处理过程中抛出异常，不会requeue到队列，而是在消费者本地重试
-   重试达到最大次数后，Spring会返回ack，消息会被丢弃

#### 1.4.2.失败策略

在之前的测试中，达到最大重试次数后，消息会被丢弃，这是由Spring内部机制决定的。

在开启重试模式后，重试次数耗尽，如果消息依然失败，则需要有MessageRecovery接口来处理，它包含三种不同的实现：

-   RejectAndDontRequeueRecoverer：重试耗尽后，直接reject，丢弃消息。默认就是这种方式
    
-   ImmediateRequeueMessageRecoverer：重试耗尽后，返回nack，消息重新入队
    
-   RepublishMessageRecoverer：重试耗尽后，将失败消息投递到指定的交换机
    

比较优雅的一种处理方案是RepublishMessageRecoverer，失败后将消息投递到一个指定的，专门存放异常消息的队列，后续由人工集中处理。

1）在consumer服务中定义处理失败消息的交换机和队列

```java
@Bean
public DirectExchange errorMessageExchange(){
    return new DirectExchange("error.direct");
}
@Bean
public Queue errorQueue(){
    return new Queue("error.queue", true);
}
@Bean
public Binding errorBinding(Queue errorQueue, DirectExchange errorMessageExchange){
    return BindingBuilder.bind(errorQueue).to(errorMessageExchange).with("error");
}
```

2）定义一个RepublishMessageRecoverer，关联队列和交换机

```java
@Bean
public MessageRecoverer republishMessageRecoverer(RabbitTemplate rabbitTemplate){
    return new RepublishMessageRecoverer(rabbitTemplate, "error.direct", "error");
}
```

完整代码：

```java
package cn.itcast.mq.config;

import org.springframework.amqp.core.Binding;
import org.springframework.amqp.core.BindingBuilder;
import org.springframework.amqp.core.DirectExchange;
import org.springframework.amqp.core.Queue;
import org.springframework.amqp.rabbit.core.RabbitTemplate;
import org.springframework.amqp.rabbit.retry.MessageRecoverer;
import org.springframework.amqp.rabbit.retry.RepublishMessageRecoverer;
import org.springframework.context.annotation.Bean;

@Configuration
public class ErrorMessageConfig {
    @Bean
    public DirectExchange errorMessageExchange(){
        return new DirectExchange("error.direct");
    }
    @Bean
    public Queue errorQueue(){
        return new Queue("error.queue", true);
    }
    @Bean
    public Binding errorBinding(Queue errorQueue, DirectExchange errorMessageExchange){
        return BindingBuilder.bind(errorQueue).to(errorMessageExchange).with("error");
    }

    @Bean
    public MessageRecoverer republishMessageRecoverer(RabbitTemplate rabbitTemplate){
        return new RepublishMessageRecoverer(rabbitTemplate, "error.direct", "error");
    }
}
```

### 1.5.总结

如何确保RabbitMQ消息的可靠性？

-   开启生产者确认机制，确保生产者的消息能到达队列
-   开启持久化功能，确保消息未消费前在队列中不会丢失
-   开启消费者确认机制为auto，由spring确认消息处理成功后完成ack
-   开启消费者失败重试机制，并设置MessageRecoverer，多次重试失败后将消息投递到异常交换机，交由人工处理

## 2.死信交换机

### 2.1.初识死信交换机

#### 2.1.1.什么是死信交换机

什么是死信？

当一个队列中的消息满足下列情况之一时，可以成为死信（dead letter）：

-   消费者使用basic.reject或 basic.nack声明消费失败，并且消息的requeue参数设置为false
-   消息是一个过期消息，超时无人消费
-   要投递的队列消息满了，无法投递

如果这个包含死信的队列配置了`dead-letter-exchange`属性，指定了一个交换机，那么队列中的死信就会投递到这个交换机中，而这个交换机称为**死信交换机**（Dead Letter Exchange，检查DLX）。

如图，一个消息被消费者拒绝了，变成了死信：

![image-20210718174328383](https://i-blog.csdnimg.cn/blog_migrate/7bc97bc5c8b5af6eb6fd88e8ec07fc9c.png)

因为simple.queue绑定了死信交换机 dl.direct，因此死信会投递给这个交换机：

![image-20210718174416160](https://i-blog.csdnimg.cn/blog_migrate/9ee51f4a05ac2249fb172202ecc45618.png)

如果这个死信交换机也绑定了一个队列，则消息最终会进入这个存放死信的队列：

![image-20210718174506856](https://i-blog.csdnimg.cn/blog_migrate/9db83e8c55c9b673e4eb89b1b938c329.png)

另外，队列将死信投递给死信交换机时，必须知道两个信息：

-   死信交换机名称
-   死信交换机与死信队列绑定的RoutingKey

这样才能确保投递的消息能到达死信交换机，并且正确的路由到死信队列。

![image-20210821073801398](https://i-blog.csdnimg.cn/blog_migrate/4383351d9a6e54b7d44d0ea5586bd94b.png)

#### 2.1.2.利用死信交换机接收死信（拓展）

在失败重试策略中，默认的RejectAndDontRequeueRecoverer会在本地重试次数耗尽后，发送reject给RabbitMQ，消息变成死信，被丢弃。

我们可以给simple.queue添加一个死信交换机，给死信交换机绑定一个队列。这样消息变成死信后也不会丢弃，而是最终投递到死信交换机，路由到与死信交换机绑定的队列。

![image-20210718174506856](https://i-blog.csdnimg.cn/blog_migrate/9db83e8c55c9b673e4eb89b1b938c329.png)

我们在consumer服务中，定义一组死信交换机、死信队列：

```java
// 声明普通的 simple.queue队列，并且为其指定死信交换机：dl.direct
@Bean
public Queue simpleQueue2(){
    return QueueBuilder.durable("simple.queue") // 指定队列名称，并持久化
        .deadLetterExchange("dl.direct") // 指定死信交换机
        .build();
}
// 声明死信交换机 dl.direct
@Bean
public DirectExchange dlExchange(){
    return new DirectExchange("dl.direct", true, false);
}
// 声明存储死信的队列 dl.queue
@Bean
public Queue dlQueue(){
    return new Queue("dl.queue", true);
}
// 将死信队列 与 死信交换机绑定
@Bean
public Binding dlBinding(){
    return BindingBuilder.bind(dlQueue()).to(dlExchange()).with("simple");
}
```

#### 2.1.3.总结

什么样的消息会成为死信？

-   消息被消费者reject或者返回nack
-   消息超时未消费
-   队列满了

死信交换机的使用场景是什么？

-   如果队列绑定了死信交换机，死信会投递到死信交换机；
-   可以利用死信交换机收集所有消费者处理失败的消息（死信），交由人工处理，进一步提高消息队列的可靠性。

### 2.2.TTL

一个队列中的消息如果超时未消费，则会变为死信，超时分为两种情况：

-   消息所在的队列设置了超时时间
-   消息本身设置了超时时间

![image-20210718182643311](https://i-blog.csdnimg.cn/blog_migrate/f797425423f6f225b67d8e64d20eb251.png)

#### 2.2.1.接收超时死信的死信交换机

在consumer服务的SpringRabbitListener中，定义一个新的消费者，并且声明 死信交换机、死信队列：

```java
@RabbitListener(bindings = @QueueBinding(
    value = @Queue(name = "dl.ttl.queue", durable = "true"),
    exchange = @Exchange(name = "dl.ttl.direct"),
    key = "ttl"
))
public void listenDlQueue(String msg){
    log.info("接收到 dl.ttl.queue的延迟消息：{}", msg);
}
```

#### 2.2.2.声明一个队列，并且指定TTL

要给队列设置超时时间，需要在声明队列时配置x-message-ttl属性：

```java
@Bean
public Queue ttlQueue(){
    return QueueBuilder.durable("ttl.queue") // 指定队列名称，并持久化
        .ttl(10000) // 设置队列的超时时间，10秒
        .deadLetterExchange("dl.ttl.direct") // 指定死信交换机
        .build();
}
```

注意，这个队列设定了死信交换机为`dl.ttl.direct`

声明交换机，将ttl与交换机绑定：

```java
@Bean
public DirectExchange ttlExchange(){
    return new DirectExchange("ttl.direct");
}
@Bean
public Binding ttlBinding(){
    return BindingBuilder.bind(ttlQueue()).to(ttlExchange()).with("ttl");
}
```

发送消息，但是不要指定TTL：

```java
@Test
public void testTTLQueue() {
    // 创建消息
    String message = "hello, ttl queue";
    // 消息ID，需要封装到CorrelationData中
    CorrelationData correlationData = new CorrelationData(UUID.randomUUID().toString());
    // 发送消息
    rabbitTemplate.convertAndSend("ttl.direct", "ttl", message, correlationData);
    // 记录日志
    log.debug("发送消息成功");
}
```

发送消息的日志：

![image-20210718191657478](https://i-blog.csdnimg.cn/blog_migrate/f526fc7d857b0785b81e68844cb78f7e.png)

查看下接收消息的日志：

![image-20210718191738706](https://i-blog.csdnimg.cn/blog_migrate/173d901333d92afd5e69f3fbd9d77e31.png)

因为队列的TTL值是10000ms，也就是10秒。可以看到消息发送与接收之间的时差刚好是10秒。

#### 2.2.3.发送消息时，设定TTL

在发送消息时，也可以指定TTL：

```java
@Test
public void testTTLMsg() {
    // 创建消息
    Message message = MessageBuilder
        .withBody("hello, ttl message".getBytes(StandardCharsets.UTF_8))
        .setExpiration("5000")
        .build();
    // 消息ID，需要封装到CorrelationData中
    CorrelationData correlationData = new CorrelationData(UUID.randomUUID().toString());
    // 发送消息
    rabbitTemplate.convertAndSend("ttl.direct", "ttl", message, correlationData);
    log.debug("发送消息成功");
}
```

查看发送消息日志：

![image-20210718191939140](https://i-blog.csdnimg.cn/blog_migrate/391216bc3befb43b4efd3b93978c6ac2.png)

接收消息日志：

![image-20210718192004662](https://i-blog.csdnimg.cn/blog_migrate/9540f8dd7d9ce45a781eb868242986e9.png)

这次，发送与接收的延迟只有5秒。说明当队列、消息都设置了TTL时，任意一个到期就会成为死信。

#### 2.2.4.总结

消息超时的两种方式是？

-   给队列设置ttl属性，进入队列后超过ttl时间的消息变为死信
-   给消息设置ttl属性，队列接收到消息超过ttl时间后变为死信

如何实现发送一个消息20秒后消费者才收到消息？

-   给消息的目标队列指定死信交换机
-   将消费者监听的队列绑定到死信交换机
-   发送消息时给消息设置超时时间为20秒

### 2.3.延迟队列

利用TTL结合死信交换机，我们实现了消息发出后，消费者延迟收到消息的效果。这种消息模式就称为延迟队列（Delay Queue）模式。

延迟队列的使用场景包括：

-   延迟发送短信
-   用户下单，如果用户在15 分钟内未支付，则自动取消
-   预约工作会议，20分钟后自动通知所有参会人员

因为延迟队列的需求非常多，所以RabbitMQ的官方也推出了一个插件，原生支持延迟队列效果。

这个插件就是DelayExchange插件。参考RabbitMQ的插件列表页面：https://www.rabbitmq.com/community-plugins.html

![image-20210718192529342](https://i-blog.csdnimg.cn/blog_migrate/cab7a928e72e44b09dadb7a3b43e83ca.png)

使用方式可以参考官网地址：https://blog.rabbitmq.com/posts/2015/04/scheduling-messages-with-rabbitmq

#### 2.3.1.安装DelayExchange插件

参考课前资料：

![image-20210718193409812](https://i-blog.csdnimg.cn/blog_migrate/6fa560a400c033c5521fa3a2ed23d63b.png)

#### 2.3.2.DelayExchange原理

DelayExchange需要将一个交换机声明为delayed类型。当我们发送消息到delayExchange时，流程如下：

-   接收消息
-   判断消息是否具备x-delay属性
-   如果有x-delay属性，说明是延迟消息，持久化到硬盘，读取x-delay值，作为延迟时间
-   返回routing not found结果给消息发送者
-   x-delay时间到期后，重新投递消息到指定队列

#### 2.3.3.使用DelayExchange

插件的使用也非常简单：声明一个交换机，交换机的类型可以是任意类型，只需要设定delayed属性为true即可，然后声明队列与其绑定即可。

1）声明DelayExchange交换机

基于注解方式（推荐）：

![image-20210718193747649](https://i-blog.csdnimg.cn/blog_migrate/df827e348f66a3af031eb83003f60e42.png)

也可以基于@Bean的方式：

![image-20210718193831076](https://i-blog.csdnimg.cn/blog_migrate/555705bee4a3b96d3edb631cf2d69bd0.png)

2）发送消息

发送消息时，一定要携带x-delay属性，指定延迟的时间：

![image-20210718193917009](https://i-blog.csdnimg.cn/blog_migrate/a0382b48ce3bea9cbdd098824e952c1d.png)

#### 2.3.4.总结

延迟队列插件的使用步骤包括哪些？

•声明一个交换机，添加delayed属性为true

•发送消息时，添加x-delay头，值为超时时间

## 3.惰性队列

### 3.1.消息堆积问题

当生产者发送消息的速度超过了消费者处理消息的速度，就会导致队列中的消息堆积，直到队列存储消息达到上限。之后发送的消息就会成为死信，可能会被丢弃，这就是消息堆积问题。

![image-20210718194040498](https://i-blog.csdnimg.cn/blog_migrate/cfd333540e0f7401570673784d648746.png)

解决消息堆积有两种思路：

-   增加更多消费者，提高消费速度。也就是我们之前说的work queue模式
-   扩大队列容积，提高堆积上限

要提升队列容积，把消息保存在内存中显然是不行的。

### 3.2.惰性队列

从RabbitMQ的3.6.0版本开始，就增加了Lazy Queues的概念，也就是惰性队列。惰性队列的特征如下：

-   接收到消息后直接存入磁盘而非内存
-   消费者要消费消息时才会从磁盘中读取并加载到内存
-   支持数百万条的消息存储

#### 3.2.1.基于命令行设置lazy-queue

而要设置一个队列为惰性队列，只需要在声明队列时，指定x-queue-mode属性为lazy即可。可以通过命令行将一个运行中的队列修改为惰性队列：

```
rabbitmqctl set_policy Lazy "^lazy-queue$" '{"queue-mode":"lazy"}' --apply-to queues  
```

命令解读：

-   `rabbitmqctl` ：RabbitMQ的命令行工具
-   `set_policy` ：添加一个策略
-   `Lazy` ：策略名称，可以自定义
-   `"^lazy-queue$"` ：用正则表达式匹配队列的名字
-   `'{"queue-mode":"lazy"}'` ：设置队列模式为lazy模式
-   `--apply-to queues` ：策略的作用对象，是所有的队列

#### 3.2.2.基于@Bean声明lazy-queue

![image-20210718194522223](https://i-blog.csdnimg.cn/blog_migrate/d30fad6348d5dc6b6ea0bb2752f8af95.png)

#### 3.2.3.基于@RabbitListener声明LazyQueue

![image-20210718194539054](https://i-blog.csdnimg.cn/blog_migrate/4b1a59e5ac592770491607c2e335612c.png)

#### 3.3.总结

消息堆积问题的解决方案？

-   队列上绑定多个消费者，提高消费速度
-   使用惰性队列，可以再mq中保存更多消息

惰性队列的优点有哪些？

-   基于磁盘存储，消息上限高
-   没有间歇性的page-out，性能比较稳定

惰性队列的缺点有哪些？

-   基于磁盘存储，消息时效性会降低
-   性能受限于磁盘的IO

## 4.MQ集群

### 4.1.集群分类

RabbitMQ的是基于Erlang语言编写，而Erlang又是一个面向并发的语言，天然支持集群模式。RabbitMQ的集群有两种模式：

•**普通集群**：是一种分布式集群，将队列分散到集群的各个节点，从而提高整个集群的并发能力。

•**镜像集群**：是一种主从集群，普通集群的基础上，添加了主从备份功能，提高集群的数据可用性。

镜像集群虽然支持主从，但主从同步并不是强一致的，某些情况下可能有数据丢失的风险。因此在RabbitMQ的3.8版本以后，推出了新的功能：**仲裁队列**来代替镜像集群，底层采用Raft协议确保主从的数据一致性。

### 4.2.普通集群

#### 4.2.1.集群结构和特征

普通集群，或者叫标准集群（classic cluster），具备下列特征：

-   会在集群的各个节点间共享部分数据，包括：交换机、队列元信息。不包含队列中的消息。
-   当访问集群某节点时，如果队列不在该节点，会从数据所在节点传递到当前节点并返回
-   队列所在节点宕机，队列中的消息就会丢失

结构如图：

![image-20210718220843323](https://i-blog.csdnimg.cn/blog_migrate/15637833660c84c346412b2d4eae5fc3.png)

#### 4.2.2.部署

参考课前资料：《RabbitMQ部署指南.md》

### 4.3.镜像集群

#### 4.3.1.集群结构和特征

镜像集群：本质是主从模式，具备下面的特征：

-   交换机、队列、队列中的消息会在各个mq的镜像节点之间同步备份。
-   创建队列的节点被称为该队列的**主节点，**备份到的其它节点叫做该队列的**镜像**节点。
-   一个队列的主节点可能是另一个队列的镜像节点
-   所有操作都是主节点完成，然后同步给镜像节点
-   主宕机后，镜像节点会替代成新的主

结构如图：

![image-20210718221039542](https://i-blog.csdnimg.cn/blog_migrate/6f76f95c382d2188ae6991445b7f472e.png)

#### 4.3.2.部署

参考课前资料：《RabbitMQ部署指南.md》

### 4.4.仲裁队列

#### 4.4.1.集群特征

仲裁队列：仲裁队列是3.8版本以后才有的新功能，用来替代镜像队列，具备下列特征：

-   与镜像队列一样，都是主从模式，支持主从数据同步
-   使用非常简单，没有复杂的配置
-   主从同步基于Raft协议，强一致

#### 4.4.2.部署

参考课前资料：《RabbitMQ部署指南.md》

#### 4.4.3.Java代码创建仲裁队列

```java
@Bean
public Queue quorumQueue() {
    return QueueBuilder
        .durable("quorum.queue") // 持久化
        .quorum() // 仲裁队列
        .build();
}
```

#### 4.4.4.SpringAMQP连接MQ集群

注意，这里用address来代替host、port方式

```bash
spring:
  rabbitmq:
    addresses: 192.168.150.105:8071, 192.168.150.105:8072, 192.168.150.105:8073
    username: itcast
    password: 123321
    virtual-host: /
```