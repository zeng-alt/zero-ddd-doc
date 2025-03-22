# 多租户组件架构

## 多租户模块

```
zero-ddd-tenant-component
├── zero-ddd-tenant-column-component      // 实现行区分租户
├── zero-ddd-tenant-database-component    // 实现database区分租户
├── zero-ddd-tenant-datasource-component  // 提供配置和注解
├── zero-ddd-tenant-management-component  // 提供接口和扩展
├── zero-ddd-tenant-mix-component         // 实现混合模式包含三种区分租户
├── zero-ddd-tenant-schema-component      // 实现schema区分租户
├── zero-ddd-tenant-service-component     // 实现查询租户信息
├── zero-ddd-tenant-sharded-component     // 实现多租户分库分表
```

## 模块之间的依赖关系

<figure><img src="../.gitbook/assets/屏幕截图 2025-03-22 215457.png" alt=""><figcaption></figcaption></figure>

## 使用多租户模块

### 在pom.xml引入依赖

```xml
<dependency>
    <groupId>com.zjj</groupId>
    <artifactId>zero-ddd-tenant-datasource-component</artifactId>
    <version>0.0.1-SNAPSHOT</version>
</dependency>
```

### 在配置类或启动类上添加注解, mode自己选择，默认MIXED

```java
@EnableMultiTenancy(mode = TenantMode.MIXED)
```

### 添加租户信息获取模块（column不用做处理，也不用引入获取租户信息模块）

1. 在服务启动时management模块会拿到所有租户数据源并添加到数据源类中（除了column不用做处理）
2. 租户信息提供模块分为两和模式
   1. 本地获取需要添加租户数据源连接配置
   2. 远程调用获取，租房信息提供服务要先启动

#### 使用本地提供者

* 引入service模块

```xml
<dependency>
    <groupId>com.zjj</groupId>
    <artifactId>zero-ddd-tenant-service-component</artifactId>
    <version>0.0.1-SNAPSHOT</version>
</dependency>
```

* 添加租户配置信息

```yaml
multi-tenancy:
  datasource:
    url: jdbc:postgresql://localhost:5432/zero-tenant
    username: postgres
    password: postgres
    driverClassName: org.postgresql.Driver
    type: com.zaxxer.hikari.HikariDataSource
  jpa:
    database-platform: org.hibernate.dialect.PostgreSQLDialect
```

* 如果是单体项目，要自已对租户进行管理请配置entity和respostity的包地址，自定义租户信息提供者，查看自定义提供者说明

#### 使用远程提供者

* 引入service模块, 如果有本地提供者则远程提供不生效

```xml
<dependency>
    <groupId>com.zjj</groupId>
    <artifactId>zero-ddd-exchange-tenant</artifactId>
    <version>0.0.1-SNAPSHOT</version>
</dependency>
```

* 加入注解, 要加入open feign相关依赖

```java
@EnableFeignClients(basePackages = "com.zjj")
```

#### 使用自定义提供者

1. 实现com.zjj.tenant.management.component.spi.TenantDataSourceProvider
2. 实现com.zjj.tenant.management.component.spi.TenantSingleDataSourceProvider

## 其他工具类

手动切换租户

```java
@SwitchTenant // 在方法层
```

```java
TenantContextHolder // 在方法内 mvc
```

```java
ReactiveTenantContextHolder // 在方法内 reactive
```

## web项目中在过滤器中切换租户

1. 使用TenantContextHolder或者ReactiveTenantContextHolder
2. 引入com.zjj:zero-ddd-security-tenant模块
3. 详细请查看安全组件架构
