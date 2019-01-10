# Java-framework


## Spring 与扩展插件集成

是一个J2EE框架，轻量级IoC良好支持，也提供AOP技术非常好的封装。模块化独立完成特定工作。
Spring AOP、Sping ORM、Spring DAO、Spring Web、Spring Context、Spring Web MVC、Spring Core等。

### 核心功能IOC

控制反转（Inverse Of Control),有时也被称作依赖注入，在Java开发中，IoC意味着将你设计好的类交给系统去控制，而不是在你的类内部控制，是一种降低对象之间耦合关系的设计思想

IOC模式将耦合代码从程序中移出，放到统一的XML文件或者注解中管理。由IOC容器通过配置文件或者注解来管理对象的生命周期、依赖关系等，这样就不用重新修改并编译具体的代码，从而实现组件之间的解耦

### 核心功能AOP

可以通过预编译方式和运行期动态代理实现在不修改源代码的情况下给程序动态统一添加功能的一种技术。AOP实际是GoF设计模式的延续，设计模式孜孜不倦追求的是调用者和被调用者之间的解耦,提高代码的灵活性和可扩展性，AOP可以说也是这种目标的一种实现

将日志记录，性能统计，安全控制，事务处理，异常处理等代码从业务逻辑代码中划分出来，通过对这些行为的分离，我们希望可以将它们独立到非指导业务逻辑的方法中，进而改变这些行为的时候不影响业务逻辑的代码

### SpringJDBC

- `jdbcTemplate.getDataSource().getConnection().getMetaData().getDatabaseProductName()` 获取数据库名

### Alibaba Druid

提供sql语句分页，计算数量，sql分析，运行监控等功能

- sql语句分页，计算数量

```Java
PagerUtils.count("select * from sys_menu", "mysql");
PagerUtils.limit("select * from sys_menu", "mysql", 10, 10);
```
转换后
```SQL
SELECT COUNT(*)
FROM sys_menu
SELECT *
FROM sys_menu
LIMIT 10, 10
```

### Mybatis PageHelper

- 助力主流数据库分页


## 参考

- [spring官网](http://spring.io/)
- [spring 源码](https://github.com/spring-projects/)
- [druid 连接池](https://github.com/alibaba/druid)
- [jfinal](https://gitee.com/jfinal/jfinal)
- [mybatis](https://github.com/mybatis/)
