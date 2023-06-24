# Dubbo篇

## 基础篇

### 应用与实践

#### 分布式架构下的网络通信需求

#### RPC协议和RPC框架

#### Apache Dubbo的背景说明

#### 基本使用

##### 安装zookeeper

略。

##### 安装dubbo-admin

安装dubbo-admin，从github上clone [duboo-admin](https://github.com/apache/dubbo-admin.git)

 ```bash
 cd dubbo-admin-ui
 npm install
 ```

回到dubbo-admin目录, 使用maven打包一下, 记得要跳过测试, 不然会很慢

```bash
mvn clean package -Dmaven.skip.test=ture
```

如果dubbo-admin-ui报错，找到pom.xml，删除之后，重新构建。

```xml
<goals>
    <goal>npm</goal>
</goals>
```

修改端口，进入`dubbo-amdin/dubbo-admin-server/src/main/resources` 修改`application.properties`, 新增`server.port=8081`。

然后，启动

```bash
mvn --projects dubbo-admin-server spring-boot:run
```

【注意：Zookeeper的服务一定要打开！】



### 高级用法

## 高级篇

### 微服务的演进之服务治理和Dubbo的由来

### Dubbo的应用场景和案例分析

### Dubbo和Spring的整合和原理剖析

### Dubbo扩展之SPI机制深度解析

### Dubbo服务的暴露流程源码分析

### Dubbo服务的发现流程源码分析

### Dubbo的Mock服务降级原理

### Dubbo的Router原理和dubbo-admin

### Dubbo的集群容错原理剖析

## Dubbo3.x新特性

