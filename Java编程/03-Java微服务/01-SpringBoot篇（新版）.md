# SpringBoot篇

## 基础篇

### 相关概念

### 第一个SpringBoot程序

### 了解自动配置原理

#### SpringBoot特点

##### 依赖管理

##### 自动配置

#### 容器功能

##### 组件注册方式

###### @Configuration

###### @Bean、@Component、@Controller、@Service、@Repository

###### @ComponentScan、@Import

###### @Conditional

##### 原生配置文件引入@ImportResource

##### 配置绑定方式

###### @ConfigurationProperties

###### @EnableConfigurationProperties + @ConfigurationProperties

###### @Component + @ConfigurationProperties

#### 引导加载自动配置类

##### @SpringBootConfiguration

##### @ComponentScan

##### @EnableAutoConfiguration

###### @AutoConfigurationPackage

###### @Import(AutoConfigurationImportSelector.class)

#### 按需开启自动配置项

#### 修改默认配置

#### 最佳实践

### 开发小技巧

#### Lombok

#### dev-tools

#### Spring Initailizr（项目初始化向导）

##### 选择我们需要的开发场景

##### 自动依赖引入

##### 自动创建项目结构

##### 自动编写好主配置类

## 进阶篇

### 配置文件

### Web开发

### 数据访问

### 单元测试

### 指标监控

### 原理解析

## 原理篇

### 解决Bean的复杂配置--自动装配

#### 核心原理流程推导

#### 手写核心注解

#### 理解SPI机制

### SpringBoot启动流程及外部化配置

### SpringBoot Starter组件详解

### 自动装配核心原理及手写Starter组件