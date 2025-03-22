# 项目架构

### 项目简介

* 支持多租户架构，基于jpa搭建SAAS系统，支持Column, Schema, Database, Mixed架构。
* 支持DDD CQRS架构基础层代码落地。
* 提供RBAC和ABAC权限架构。
* 后端采用Spring Boot、Spring Cloud & Alibaba。

### 系统模块

<pre><code>zero-ddd
├── zero-business
│       └── zero-main-business                // 主服务 [8082]
<strong>├── zero-ddd-ai        // ai服务 [知识库和命令助手]
</strong>├── zero-ddd-auth      // 认证服务 [8084]
├── zero-ddd-component // 组件模块
│       └── zero-ddd-autoconfigure-component // 提供接口，抽象类和配置信息
│       └── zero-ddd-bean-component          // bean组件 bena工具类
│       └── zero-ddd-component-bom           // 组件依赖管理，如果不想继承zero-ddd
│       └── zero-ddd-core-component          // 核心组件 工具类 全局返回类型，全局异常
│       └── zero-ddd-doc-component           // api接口生成文档
│       └── zero-ddd-domain-component        // 领域常用工具类
│       └── zero-ddd-excel-component         // excel组件，提供动态excel, 校验和国际化
│       └── zero-ddd-graphql-component       // 根据entity生成graphql接口，做读模型
│       └── zero-ddd-i18n-component          // 国际化组件，提供接口
│       └── zero-ddd-json-component          // json组件，使用jackson
│       └── zero-ddd-message-queue-component // 消息队列组件
│       └── zero-ddd-security-component      // 安全组件，提供登录，jwt,raba,abac
│       └── zero-ddd-storage-component       // 缓存组件，本地，远程，二级缓存
│       └── zero-ddd-tenant-component        // 租户组件，提供注解式开启不同租户模式
├── zero-ddd-exchange  // 接口模块
├── zero-ddd-gateway   // 网关模块 [8080]
├── zero-ddd-tenant    // 租户服务 [8081]
</code></pre>

### 架构图

<figure><img src=".gitbook/assets/未命名文件.png" alt=""><figcaption></figcaption></figure>

### 多模块代码架构

### 单模块代码架构

