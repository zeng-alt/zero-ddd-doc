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

## jwt模块&#x20;

提供JWT认证和JWT续期过滤器，要先引入core模块，\[功能不灵活，后期完善]

### 引入依赖

```xml
<dependency>
    <groupId>com.zjj</groupId>
    <artifactId>zero-ddd-security-jwt-component</artifactId>
    <version>0.0.1-SNAPSHOT</version>
</dependency>
```

### 开启配置

更细节配置查看JwtProperties类

```yaml
security:
  jwt:
    enabled: true
```

### 引入缓存依赖，jwt基于缓存

缓存二选一，如果有二级缓存默认使用二级，相关配置查询多级缓存架构

1. redis缓存

```xml
<dependency>
    <groupId>com.zjj</groupId>
    <artifactId>zero-ddd-cache-component</artifactId>
    <version>0.0.1-SNAPSHOT</version>
</dependency>
```

1. 二级缓存

```xml
<dependency>
    <groupId>com.zjj</groupId>
    <artifactId>zero-ddd-l2-cache-component</artifactId>
    <version>0.0.1-SNAPSHOT</version>
</dependency>
```

### RBAC模块

1. 在请求级别进行拦截，能控制到按钮级别
2. 在请求级别进行graphql拦截

#### 引入依赖

```xml
<dependency>
    <groupId>com.zjj</groupId>
    <artifactId>zero-ddd-security-rbac-component</artifactId>
    <version>0.0.1-SNAPSHOT</version>
</dependency>
```

### 开启配置

```yaml
security:
  context:
    enabled-access: true
```

### 验证信息提供者接口

可以直接使用默认的，操作RbacCacheManage，最好使用二级缓存

1. ```
   AbstractResourceLocator
   ```
2. ```
   AbstractReactiveResourceLocator
   ```

### ABAC模块

等待完善

### Fast Auth模块

### 手机验证码登录

### 验证码模块

### 切换租户模块

### 自定义登录模块

### 自定义认证模块
