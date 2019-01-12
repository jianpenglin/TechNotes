# Java 设计模式

设计模式（Design Pattern）是一套被反复使用、多数人知晓的、经过分类编目的、代码设计经验的总结。使用设计模式是为了可重用代码、让代码更容易被他人理解、保证代码可靠性。


## 设计模式六原则

- 开闭原则（Open Close Principle）
开闭原则就是说对扩展开放，对修改关闭
- 里氏代换原则（Liskov Substitution Principle）
里氏代换原则(Liskov Substitution Principle LSP)面向对象设计的基本原则之一。 里氏代换原则中说，任何基类可以出现的地方，子类一定可以出现。氏代换原则是对“开-闭”原则的补充
- 依赖倒转原则（Dependence Inversion Principle）
这个是开闭原则的基础，具体内容：针对接口编程，依赖于抽象而不依赖于具体。
- 接口隔离原则（Interface Segregation Principle）
使用多个隔离的接口，比使用单个接口要好。降低类之间的耦合度
- 迪米特法则（最少知道原则）（Demeter Principle）
一个实体应当尽量少的与其他实体之间发生相互作用，使得系统功能模块相对独立
- 合成复用原则（Composite Reuse Principle）
原则是尽量使用合成/聚合的方式，而不是使用继

## 设计模式分类

总体来说设计模式分为三大类，GOF定义的是23种设计模式，实际上现在已经不止23种：
- 创建型模式，共五种：（简单工厂）、工厂方法模式、抽象工厂模式、单例模式、构建者模式、原型模式
- 结构型模式，共七种：适配器模式、装饰器模式、代理模式、外观模式、桥接模式、组合模式、享元模式
- 行为型模式，共十一种：策略模式、模板方法模式、观察者模式、迭代模式、责任链模式、命令模式、备忘录模式、状态模式、访问者模式、中介者模式、解释器模式、（空对象）
- J2EE WEB模式， MVC 模式（MVC Pattern）、业务代表模式（Business Delegate Pattern）、组合实体模式（Composite Entity Pattern）、数据访问对象模式（Data Access Object Pattern）、前端控制器模式（Front Controller Pattern）、拦截过滤器模式（Intercepting Filter Pattern）、服务定位器模式（Service Locator Pattern）、传输对象模式（Transfer Object Pattern）、MVVM 模式（MVVM Pattern）

## 创建型模式

### 1. 简单工厂（Simple Factory）

#### 说明

在创建一个对象时不向客户暴露内部细节，并提供一个创建对象的通用接口。

#### 使用场景

#### 类图

#### 代码实现

### 2. 工厂方法模式（Factory Method）

#### 说明

#### 使用场景

#### 类图

#### 代码实现

### 3. 抽象工厂模式（Abstract Factory）

#### 说明

#### 使用场景

#### 类图

#### 代码实现

### 4. 单例模式（Singleton）

#### 说明

#### 使用场景

#### 类图

#### 代码实现

### 5. 构建者模式（Builder）

#### 说明

#### 使用场景

#### 类图

#### 代码实现

### 6. 原形模   式（Prototype）

#### 说明

#### 使用场景

#### 类图

#### 代码实现

## 结构型模式

### 1. 适配器模式(Adapter)

### 2. 装饰器模式（Decorator）

### 3. 代理模式（Proxy）

### 4. 外观模式（Facade）

### 5. 桥接模式（Bridge）

### 6. 组合模式（Composite）

### 7. 享元模式(Flyweight)

## 行为型模式

### 1. 策略模式(Strategy)

### 2. 模板方法模式(Template Method)

### 3. 观察者模式(Observer)

### 4. 迭代模式（Iterator）

### 5. 责任链模式（Chain Of Responsibility）

### 6. 模板方法（Template Method）

### 7. 命令模式（Command）

### 8. 备忘录模式（Memento）

### 9. 状态模式（State）

### 10. 中介者模式（Mediator）

### 11. 解释器模式（Interpreter）

### 12. 空对象（Null）

## J2EE WEB 模式

### 1. MVC 模式（MVC Pattern）

### 2. 业务代表模式（Business Delegate Pattern）

### 3. 组合实体模式（Composite Entity Pattern）

### 4. 数据访问对象模式（Data Access Object Pattern）

### 5. 前端控制器模式（Front Controller Pattern）

### 6. 拦截过滤器模式（Intercepting Filter Pattern）

### 7. 服务定位器模式（Service Locator Pattern）

### 8. 传输对象模式（Transfer Object Pattern）

### 9. MVVM模式（MVVM Patter）