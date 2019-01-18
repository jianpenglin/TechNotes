# JAVA 基础

## 反射

Class 和 java.lang.reflect 一起对反射提供了支持，java.lang.reflect 类库主要包含了以下三个类：
- Field ：可以使用 get() 和 set() 方法读取和修改 Field 对象关联的字段；
- Method ：可以使用 invoke() 方法调用与 Method 对象关联的方法；
- Constructor ：可以用 Constructor 创建新的对象。

Method invoke()调用的例子：

```
// 1.获取字节码对象
Class<ReflectTest> clazz = (Class<ReflectTest>) Class.forName("vip.techinfo.reflect.ReflectTest");
// 2.获取一个对象
Constructor con = clazz.getConstructor();
ReflectTest intance = (ReflectTest) con.newInstance();
// 3.获取setFF Method对象
Method method = clazz.getMethod("setFF", String.class);
// 4.调用invoke方法来调用
method.invoke(intance, "abc");
```
