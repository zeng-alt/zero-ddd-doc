---
description: 基于spring-graphql进行二次开发
---

# 读模型组件API

```xml
<dependency>
    <groupId>com.zjj</groupId>
    <artifactId>zero-ddd-graphql-component</artifactId>
</dependency>
```

引入依赖后使用注解开启

```xml
@EnableGenEntityAll
```

## 生成基础curd

每种查询策略都支持单个，多个，分页

* 创建jpa实体

```java
@Getter
@Setter
@Entit
@Table(name = "MAIN_USER")
public class User extends BaseEntity<Long> implements TenantAuditable<String> {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    /**
     * 用户账号
     */
    private String username;

    /**
     * 用户昵称
     */
    private String nickName;


    /**
     * 用户邮箱
     */
    private String email;

    /**
     * 手机号码
     */
    private String phoneNumber;

    /**
     * 用户性别
     */
    private String gender;

    /**
     * 用户头像
     */
    private String avatar;

    /**
     * 密码
     */
    private String password;

    /**
     * 帐号状态（0正常 1停用）
     */
    private String status = "0";

    @TenantId
    @Nullable
    private String tenantBy;


}
```

* 创建jpa仓储

```java
@GraphQlRepository
public interface UserDao extends BaseRepository<User, Long> {}
```

### 精确查询

查询单个 findUser 多个 queryUser

```graphql
query MyQuery {
  findUser(
      userInput: {
      avatar: "", 
      email: "", 
      gender: "", 
      lastModifiedBy: "", 
      nickName: "", 
      password: "", 
      phoneNumber: "", 
      status: "", 
      tenantBy: ""
    }
  ) {
    avatar
    createdBy
    createdDate
    email
    gender
    id
    lastModifiedBy
    lastModifiedDate
    nickName
    password
    phoneNumber
    status
    tenantBy
  }
}
```

### 模糊查询

### 条件查询

### 保存或更新实体

### 根据id删除实体

### 批量保存实体

