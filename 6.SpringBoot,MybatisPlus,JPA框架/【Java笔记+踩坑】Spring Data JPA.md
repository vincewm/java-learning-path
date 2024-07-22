>  **导航：**
>
> [【Java笔记+踩坑汇总】Java基础+JavaWeb+SSM+SpringBoot+SpringCloud+瑞吉外卖/谷粒商城/学成在线+设计模式+面试题汇总+性能调优/架构设计+源码解析](https://blog.csdn.net/qq_40991313/article/details/126646289)

------

[TOC]



# 一、JPA介绍

JPA即Java Persistence API，就是java持久化api，是SUN公司推出的一套基于`ORM`的规范。

> **ORM（Object-Relational Mapping）：**对象关系映射，简单来说为了不用JDBC那一套原始方法来操作数据库，ORM框架横空出世（mybatis、hibernate等等）。



# 二、准备

## 2.0 导入jpa依赖

```XML
		<!-- Spring Boot JPA 依赖 -->
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-data-jpa</artifactId>
		</dependency>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

## 2.1 用户表准备

```sql
CREATE TABLE `user` (
    `id` bigint(20) NOT NULL AUTO_INCREMENT,
    `name` varchar(20) DEFAULT NULL COMMENT '姓名',    #DEFAULT是默认约束，DEFAULT NULL即默认是空
    `age` int(11) DEFAULT NULL COMMENT '年龄',
    `sex` varchar(1) DEFAULT NULL COMMENT '性别',
    `address` varchar(255) DEFAULT NULL COMMENT '地址',
    `phone` varchar(20) DEFAULT NULL COMMENT '电话',
    `create_time` varchar(20) DEFAULT NULL,
    PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=4 DEFAULT CHARSET=utf8;
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

这里只有id是非空的，其他像姓名、年龄这些都可以是空。

```
+------------+---------------+------+-----+---------+-------+--------------+
|   列名     |     类型      | 空值 | 键  | 默认值  | 注释  |
+------------+---------------+------+-----+---------+-------+--------------+
|    id      |  bigint(20)   |  NO  | PRI |   AUTO_INCREMENT   | 供应商ID |
|   name     |  varchar(20)  |  YES |     |   NULL  | 姓名 |
|   age      |  int(11)      |  YES |     |   NULL  | 年龄 |
|   sex      |  varchar(1)   |  YES |     |   NULL  | 性别 |
|  address   |  varchar(255) |  YES |     |   NULL  | 地址 |
|   phone    |  varchar(20)  |  YES |     |   NULL  | 电话 |
| create_time|  varchar(20)  |  YES |     |   NULL  | 创建时间 |
+------------+---------------+------+-----+---------+-------+--------------+
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



该表格展示了表的结构，包括列名、数据类型、是否允许空值、主键约束、默认值和注释。

## 2.2 实体类：@Entity,@Table,@Id,@Column

### 2.2.1 核心注解

| 注解                | 作用                                                      | 常用属性                                                     |
| ------------------- | --------------------------------------------------------- | ------------------------------------------------------------ |
| @Entity             | 指定当前类是实体类                                        |                                                              |
| @Table("表名")      | 指定实体类和表之间的对应关系                              | name：指定数据库表的名称                                     |
| @EntityListeners    | 在实体类增删改的时候监听，为创建人/创建时间等基础字段赋值 | value：指定监听类                                            |
| @Id                 | 指定当前字段是主键                                        |                                                              |
| @SequenceGenerator  | 指定数据库序列别名                                        | sequenceName：数据库序列名  		name：取的别名           |
| @GeneratedValue     | 指定主键的生成方式                                        | strategy ：指定主键生成策略。默认AUTO自增，  		generator：选择主键别名 |
| @Column("表字段名") | 指定实体类属性和数据库表之间的对应关系                    | name：指定数据库表的列名称。  		unique：是否唯一  		nullable：是否可以为空  		nserttable：是否可以插入  		updateable：是否可以更新  		columnDefinition: 定义建表时创建此列的DDL |
| @CreatedBy          | 自动插入创建人，须搭配@EntityListeners                    |                                                              |
| @CreatedDate        | 自动插入创建时间，须搭配@EntityListeners                  |                                                              |
| @LastModifiedBy     | 自动修改更新人，须搭配@EntityListeners                    |                                                              |
| @LastModifiedDate   | 自动修改更细时间，须搭配@EntityListeners                  |                                                              |
| @Version            | 自动更新版本号                                            |                                                              |
| @JsonFormat         | 插入/修改/读取的时间转换成想要的格式                      | pattern：展示格式  		timezone：国际时间                |

### 2.2.2 代码示例：@Entity,@Table,@Id,@Column

```java
package com.example.entity;

import javax.persistence.*;

@Entity    // @Entity表明是一个实体类
@Table(name = "user")    //指定表名
public class User {
    @Id    //指定主键
    @GeneratedValue(strategy = GenerationType.IDENTITY)    //指定生成策略
    private Long id;
    private String name;
    private Integer age;
    private String sex;
    private String address;
    private String phone;
    @Column(name = "create_time")    //指定列名
    private String createTime;

    public Long getId() {
        return id;
    }

    public void setId(Long id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Integer getAge() {
        return age;
    }

    public void setAge(Integer age) {
        this.age = age;
    }

    public String getSex() {
        return sex;
    }

    public void setSex(String sex) {
        this.sex = sex;
    }

    public String getAddress() {
        return address;
    }

    public void setAddress(String address) {
        this.address = address;
    }

    public String getPhone() {
        return phone;
    }

    public void setPhone(String phone) {
        this.phone = phone;
    }

    public String getCreateTime() {
        return createTime;
    }

    public void setCreateTime(String createTime) {
        this.createTime = createTime;
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 2.2.3 主键策略：@GeneratedValue

1. 自增长（Auto Increment）策略：

   ```java
   @Id
   @GeneratedValue(strategy = GenerationType.IDENTITY)
   private Long id;
   ```

   ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

2. UUID策略：

   ```java
   @Id
   @GeneratedValue(generator = "uuid")
   @GenericGenerator(name = "uuid", strategy = "org.hibernate.id.UUIDGenerator")
   private String id;
   ```

   ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

JPA本身不支持雪花算法。 

## 2.3 增删改时填充用户名和日期

### 2.3.0 引导类开启审计：@EnableJpaAuditing

```java
@EnableJpaAuditing
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 2.3.1 设置填充的用户名：AuditorAware

```java
@Configuration
public class UserAuditorAware implements AuditorAware<String> {

    @Override
    public Optional<String> getCurrentAuditor() {
        // TODO: 根据实际情况取真实用户，这里固定返回"admin"
        return Optional.of("admin");
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



### 2.3.2 实体类填充注解：@EntityListeners(AuditingEntityListener.class)

```java
@Data
@Entity
@Table(name = "JPA_USER")
@EntityListeners(AuditingEntityListener.class)    //当Entity增改时，监听信息。
public class JpaUser {

    @Id
    @Column(name = "ID")
    @GeneratedValue(strategy = GenerationType.SEQUENCE, generator = "JPA_USER_S")
    @SequenceGenerator(sequenceName = "JPA_USER_S", name = "JPA_USER_S", allocationSize = 1)
    private Long id;

    @Column(name = "NAME")
    private String name;

    @Column(name = "OBJECT_VERSION" )
    @Version    //乐观锁。版本号字段会在每次更新实体时自动递增，并在更新时进行检查。如果两个并发的操作尝试更新同一个实体对象，只有其中一个操作会成功，而另一个操作会失败并抛出异常。
    private Long objectVersion;

    @Column(name = "CREATED_BY")
    @CreatedBy    //创建时，自动填充创建人。需要搭配上面的@EntityListeners
    private String createdBy;

    @Column(name = "CREATED_DATE")
    @CreatedDate    //创建时，自动填充创建时间。需要搭配上面的@EntityListeners
    @JsonFormat(pattern = "yyyy-MM-dd HH:mm:ss", timezone = "GMT+8")
    private Date createdDate;

    @Column(name = "LAST_UPDATED_BY" )
    @LastModifiedBy    //修改时，自动填充修改人。需要搭配上面的@EntityListeners
    private String lastUpdatedBy;

    @Column(name = "LAST_UPDATED_DATE" )
    @LastModifiedDate    //修改时，自动填充修改时间。需要搭配上面的@EntityListeners
    @JsonFormat(pattern = "yyyy-MM-dd HH:mm:ss", timezone = "GMT+8")
    private Date lastUpdatedDate;
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

# 二、DAO层

## 2.1 基本用法：继承JpaRepository<实体,ID类型> 

```java
@Repository
public interface UserRepository extends JpaRepository<User, Long> {

}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

## 2.2 常用增删改查方法

### 2.2.1 查：find

- `findById(id)`：根据ID查询单个实体对象。

```java
Optional<User> user = userRepository.findById(1L);
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



- `findAll()`：查询所有实体对象。

```java
List<User> users = userRepository.findAll();
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



- `findAllById(ids)`：根据ID列表查询多个实体对象。

```java
List<User> users = userRepository.findAllById(Arrays.asList(1L, 2L, 3L));
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



- `count()`：统计实体对象的总数。

```java
long count = userRepository.count();
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



### 2.2.2 增：save

save(entity)：保存单个实体对象，根据实体对象的状态（新建或已存在）执行插入或更新操作。

saveAll(List<entitiy>)：批量保存

```java
User user = new User("John Doe", 25);
userRepository.save(user);
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 2.2.3 改：save

save(entity)：保存单个实体对象，根据实体对象的状态（新建或已存在）执行插入或更新操作。

```java
User user = userRepository.findById(1L).orElse(null);
if (user != null) {
    user.setName("Updated Name");
    userRepository.save(user);
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 2.2.4 删：delete

- delete(entity)：删除单个实体对象。
- deleteById(id)：根据ID删除单个实体对象。
- deleteAll()：删除所有实体对象。
- deleteAll(List<entitiy>)：批量删除多个实体对象。

```java
User user = userRepository.findById(1L).orElse(null);
if (user != null) {
    userRepository.delete(user);
}


userRepository.deleteById(1L);

userRepository.deleteAll();

List<User> users = userRepository.findAllById(Arrays.asList(1L, 2L, 3L));
userRepository.deleteAll(users);
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

## 2.3 高级增删改查

### 2.3.1 分页查找

```java
    public Page<User> findPage(Integer pageNum, Integer pageSize, String name) {
        // 构建分页查询条件
        Sort sort = new Sort(Sort.Direction.DESC, "create_time");
        Pageable pageRequest = PageRequest.of(pageNum - 1, pageSize, sort);
        return userRepository.findByNameLike(name, pageRequest);
    }
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



# 三、Service层

```java
@Service
public class UserServiceImpl implements UserService {

    @Resource
    private UserRepository userRepository;

    public void save(User user) {
        String now = new SimpleDateFormat("yyyy-MM-dd").format(new Date());
        user.setCreateTime(now);
        userRepository.save(user);
    }

    public void delete(Long id) {
        userRepository.deleteById(id);
    }

    public User findById(Long id) {
        return userRepository.findById(id).orElse(null);
    }

    public List<User> findAll() {
        return userRepository.findAll();
    }

    public Page<User> findPage(Integer pageNum, Integer pageSize, String name) {
        // 构建分页查询条件，建议写SQL分页
        Sort sort = new Sort(Sort.Direction.DESC, "create_time");
        Pageable pageRequest = PageRequest.of(pageNum - 1, pageSize, sort);
        return userRepository.findByNameLike(name, pageRequest);
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



# 四、Controller层

```java
@RestController
@RequestMapping("/user")
public class JpaUserController {
    @Resource
    private JpaUserService jpaUserService;

    /**
     * 新增用户
     */
    @PostMapping("/add")
    public JpaUser addUser(@RequestBody JpaUser user){
        return jpaUserService.insertUser(user);
    }

    /**
     * 删除用户
     */
    @DeleteMapping("/delete/{id}")
    public void deleteUser(@PathVariable("id") Long id){
        jpaUserService.deleteUser(id);
    }

    /**
     * 修改用户
     */
    @PutMapping("/update")
    public JpaUser updateUser(@RequestBody JpaUser user){
        return jpaUserService.updateUser(user);
    }

    /**
     * 全查用户
     */
    @GetMapping("/all")
    public List<JpaUser> findAll(){
        return jpaUserService.findAllUser();
    }

    /**
     * id查用户
     */
    @GetMapping("/get/{id}")
    public JpaUser findbyId(@PathVariable("id") Long id){
        return jpaUserService.findUserById(id);
    }


}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)