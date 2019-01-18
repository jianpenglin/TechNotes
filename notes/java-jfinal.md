# Jfinal 源码分析

## jfinal 使用

### jfinal Config

```
public class DemoConfig extends JFinalConfig {
    public void configConstant(Constants me) {}//配置JFinal常量值
    public void configRoute(Routes me) {}//配置访问路由
    public void configEngine(Engine me) {}//配置Template Engine
    public void configPlugin(Plugins me) {}//配置JFinal的Plugin,比如druid、ActiveRecord
    public void configInterceptor(Interceptors me) {}//全局拦截器,配置粒度分为 Global、Inject、Class、Method四个层次
    public void configHandler(Handlers me) {}//Handler可以接管所有web请求
}
```
提供回调方法，读取配置工具类

### ActiveRecord

#### 基础用法

- Tx 拦截器是通过捕捉到异常以后才回滚事务的，所以上述代码中的 doIt() 方法中如果有 try catch 块捕获到异常，必须再次抛出，才能让 Tx 拦截器感知并回滚事务。
- JDBC 默认的事务级别为：Connection.TRANSACTION_READ_COMMITTED
- 通过调用 ActiveRecordPlugin.setCache(...) 便可切换 cache 实现
- Dialect配置
```
public class DemoConfig extends JFinalConfig {
  public void configPlugin(Plugins me) {
    ActiveRecordPlugin arp = new ActiveRecordPlugin(…);
    me.add(arp);
    // 配置Postgresql方言
    arp.setDialect(new PostgresqlDialect());
  }
}
```

#### 多数据源

- 当使用多数据源时，只需要对每个 ActiveRecordPlugin指定一个 configName即可:
```
public void configPlugin(Plugins me) {
  // mysql 数据源
  DruidPlugin dsMysql = new DruidPlugin(…);
  me.add(dsMysql);

  // mysql ActiveRecrodPlugin 实例，并指定configName为 mysql
  ActiveRecordPlugin arpMysql = new ActiveRecordPlugin("mysql", dsMysql);
  me.add(arpMysql);
  arpMysql.addMapping("user", User.class);

  // oracle 数据源
  DruidPlugin dsOracle = new DruidPlugin(…);
  me.add(dsOracle);

  // oracle ActiveRecrodPlugin 实例，并指定configName为 oracle
  ActiveRecordPlugin arpOracle = new ActiveRecordPlugin("oracle", dsOracle);
  me.add(arpOracle);
  arpOracle.setDialect(new OracleDialect());
  arpOracle.addMapping("blog", Blog.class);
}
```
- 切换需要使用Db.use(configName)方法得到数据库操作对象
```
// 查询 dsMysql数据源中的 user
List<Record> users = Db.use("mysql").find("select * from user");
// 查询 dsOracle数据源中的 blog
List<Record> blogs = Db.use("oracle").find("select * from blog");
```

#### 独立使用

ActiveRecordPlugin可以独立于java web 环境运行在任何普通的java程序中
```
public class ActiveRecordTest {
  public static void main(String[] args) {
    DruidPlugin dp = new DruidPlugin("localhost", "userName", "password");
    ActiveRecordPlugin arp = new ActiveRecordPlugin(dp);
    arp.addMapping("blog", Blog.class);

    // 与 jfinal web 环境唯一的不同是要手动调用一次相关插件的start()方法
    dp.start();
    arp.start();

    // 通过上面简单的几行代码，即可立即开始使用
    new Blog().set("title", "title").set("content", "cxt text").save();
    Blog.dao.findById(123);
  }
}
```

## Enjoy 模板引擎

简单易用，以扩展，可以独立和spring、spring boot整合，很不错的设计

## 提供扩展

- EhCachePlugin
- RdisPlugin
- Cron4jPlugin  *调用规则需要注意*
- Validator
- 国际化
- Json转换
- 扩展

## jfinal 源码












## 参考

- [Jfinal 文档](https://www.jfinal.com/doc/5-3)
