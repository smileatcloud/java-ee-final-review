##  第一章
控制反转：

在使用Spring框架之后，对象的实例不再由调用者来创建，而是由Spring容器来创建，Spring容器会负责控制程序之间的关系，而不是由调用者的程序代码直接控制。
这样控制权由应用代码转移到了Spring容器，控制权发生了反转，这就是Spring的控制反转（IoC）

依赖注入：

从Spring容器的角度来看，Spring容器负责将被依赖对象赋值给调用者的成员变量，这相当于为调用者注入了它依赖的实力，这就是Spring的依赖注入（DI）

##  bean的装配方式有哪两种

1. 基于xml的装配
2. 基于annotation（注解）的装配


##  AOP
aop的代理具体有哪两种（aop的代理方式）

**1. JDK动态代理 **

**2. cglib代理**

## Spring的JDBC开发
**Spring的jdbc是如何配置的**

Spring JDBC模块主要由4个包组成，分别是core（核心包），dataSource（数据源包），object（对象包）和support（支持包），其中core包有jdbc的核心功能，包括JdbcTemplate类，SimpleJdbcInsert类以及NamedParameterJdbcTemplate类

可以看出，Spring对数据库的操作都封装在了这几个包中，而想要使用JDBC，就需要对其进行配置，在Spring中，JDBC的配置是在配置文件applicationContext.xml中完成的

1. 配置数据源

   <bean id = "dataSource" class="org.springframework.jdbc.xxxxxxxxx">

   <!-- 数据库驱动 -->

   <property name="driverClassName" value="com.mysql.jdbc.Driver"/>

   <!-- 连接数据库的url -->

   <property name="url" value="jdbc:mysql://localhost:3306/spring"/>

   <!-- 用户名 -->

   <property name="username" value="root"/>

   <!-- 密码 -->

   <property name="password" value="root"/>

   </bean>

2. 配置jdbc模板

   <bean id="jdbcTemplate" class="xxxxxx">

   <property name = "dataSource" ref="dataSource"/>

   </bean>

3. 配置注入类

   <bean id="xxx" class="xxx">

   <property name="jdbcTemplate" ref="jdbcTemplate" />

   </bean>



##  事务管理
**描述一下两种事务管理的方式**

spring中事务管理分为两种方式：一种是传统的编程式事务管理，另一种是声明式事务管理。

+ 编程式事务管理：是通过编写代码实现的事务管理，包括定义事务的开始、正常执行后的事务提交和异常时的事务回滚。
+ 声明式事务管理：是通过AOP技术实现的事务管理，其主要思想是将事务管理作为一个“切面”代码单独编写，然后通过AOP技术将事务管理的“切面”代码织入到业务目标类中

##  第六第七：MyBatis的核心配置
使用到的核心对象是哪两个？

1. SqlSessionFactory
2. SqlSession



```Java
// 1、读取配置文件
String resource = "mybatis-config.xml";
InputStream inputStream = Resources.getResourceAsStream(resource);
// 2、根据配置文件构建SqlSessionFactory
SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
// 3、通过SqlSessionFactory创建SqlSession
Sqlsession sqlSession = sqlSessionFactory.openSession();
```

配置文件应该按什么顺序进行

##  第九章 MyBatis的关联映射
哪三种关系映射？？？

```
一对一  一对多  多对多
```



##  第十章 MyBatis和Spring的整合
mapper接口方式（MapperFactoryBean 和 MapperScanner  的作用？？）

**MapperFactoryBean**：MapperFactoryBean的出现为了代替手工使用SqlSessionDaoSupport或SqlSessionTemplate编写数据访问对象(DAO)的代码,使用动态代理实现。

**MapperScanner：**

MapperFactoryBean 创建的代理类实现了 UserMapper 接口,并且注入到应用程序中。 因为代理创建在运行时环境中(Runtime,译者注) ,那么指定的映射器必须是一个接口,而 不是一个具体的实现类。

上面的配置有一个很大的缺点，就是系统有很多的配置文件时 全部需要手动编写，所以上述的方式已经很用了。

没有必要在 Spring 的 XML 配置文件中注册所有的映射器。相反,你可以使用一个 MapperScannerConfigurer , **它 将 会 查 找 类 路 径 下 的 映 射 器 并 自 动 将 它 们 创 建 成 MapperFactoryBean。**

##  应用题  MyBatis和Spring的整合
1. 建表（字段，至少有一条自己个人信息的记录）
2. MyBatis和Spring的文件中如何去写配置信息（先要知道怎么导入到eclipse当中，之后按照注释的内容去编写内容）
3. 根据题目要求去编写相应的映射文件
4. 编写测试代码，开始运行
5. 按照要求截图，把对应的内容贴在答题卡上相应的位置