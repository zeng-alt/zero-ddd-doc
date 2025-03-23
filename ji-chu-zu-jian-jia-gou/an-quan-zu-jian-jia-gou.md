# 安全组件架构

## 安全模块

```
zero-ddd-security-component
├── zero-ddd-security-core-component      // 核心模块必须引入
├── zero-ddd-security-jwt-component       // jwt验证 对外服务
├── zero-ddd-security-rbac-component      // 基于角色权限认证
├── zero-ddd-security-abac-component      // 基于策略权限认证
├── zero-ddd-security-fast-auth-component // 快速jwt认证，对内服务[微服务]
├── zero-ddd-security-sms-component       // 手机验证登录
├── zero-ddd-security-tenant-component    // 切换认证租户
```

## 核心模块

1. 提供账号密码登录
2. 提供默认的登录和失败处理器
3. 提供白名单过滤器
4. 提供JWT工具类
5. 提供登录配置类
6. 提供配置过滤器接口

### 使用核心模块

#### 引入依赖

```xml
<dependency>
    <groupId>com.zjj</groupId>
    <artifactId>zero-ddd-security-core-component</artifactId>
    <version>0.0.1-SNAPSHOT</version>
</dependency>
```

#### 使用注解

1. mvc @EnableWebSecurity
2. webflux @EnableWebFluxSecurity\


#### 账号密码相关配置

```yaml
security:
  username-login:
    enabled: true                     // 是否开启账号密码登录过滤器
    login-path: /auth/login/username  // 过滤器拦截的url
    username-parameter: username      // 匹配的用户名字段
    password-parameter: password      // 匹配的密码字段
```
