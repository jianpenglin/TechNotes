# http API 接口设计原则

REST全称是Representational State Transfer，中文意思是表述（编者注：通常译为表征）性状态转移。
如果一个架构符合REST的约束条件和原则，我们就称它为RESTful架构

## URL设计

- URL地址小写字母多个单词使用下划线分隔。?后面跟的参数使用驼峰模式
- 动词+宾语
Restful的核心思，比如 `GET  /article` ，`GET`是动词，`article`是宾语。
```HTML
GET (read)
POST  (create)
PUT (update)
PATCH (update) 一般不用
DELETE  (delete)
```
- 动词覆盖
有些客户端只能使用GET和POST这两种方法。服务器必须接受POST模拟其他三个方法（PUT、PATCH、DELETE）。
这时，客户端发出的 HTTP 请求，要加上X-HTTP-Method-Override属性，告诉服务器应该使用哪一个动词，覆盖POST方法。
```
POST /api/article/4 HTTP/1.1  
X-HTTP-Method-Override: PUT
```
上面代码中，X-HTTP-Method-Override指定本次请求的方法是PUT，而不是POST。
- 宾语必须是名词
宾语就是 API 的 URL，是 HTTP 动词作用的对象。它应该是名词，不能是动词。比如，/article这个 URL 就是正确的，而下面的 URL 不是名词，所以都是错误的:
```
/get_all_article
/create_new_article
/delete_all_article
```
- 不使用复数URL
- 避免多级URL
常见的情况是，资源需要多级分类，因此很容易写出多级的 URL，比如获取某个作者的某一类文章。
```
GET /author/12/categorie/2
```
这种 URL 不利于扩展，语义也不明确，往往要想一会，才能明白含义。
更好的做法是，除了第一级（也可以从第二级开始），其他级别都用查询字符串表达。
```
GET /author/12?categorie=2
```
下面是另一个例子，查询已发布的文章。你可能会设计成下面的 URL。这个比较特别
```
GET /articles/release
```
查询字符串的写法明显更好
```
GET /article?release=true
```
- 状态码
有很多服务器将返回状态码一直设为200，然后在返回body里面自定义一些状态码来表示服务器返回结果的状态码。由于rest api是直接使用的HTTP协议，所以它的状态码也要尽量使用HTTP协议的状态码。
```
200 OK 服务器返回用户请求的数据，该操作是幂等的
201 CREATED 新建或者修改数据成功
204 NOT CONTENT 删除数据成功
400 BAD REQUEST 用户发出的请求有问题，该操作是幂等的
401 Unauthoried 表示用户没有认证，无法进行操作
403 Forbidden 用户访问是被禁止的,没有权限
422 Unprocesable Entity 当创建一个对象时，发生一个验证错误
500 INTERNAL SERVER ERROR 服务器内部错误，用户将无法判断发出的请求是否成功
503 Service Unavailable 服务不可用状态，多半是因为服务器问题，例如CPU占用率大
```
- 发生错误时，不要返回 200 状态码，一般是状态码反映错误
- 正确的例子
```html
GET /token
GET /device/{id}
DELETE /device/{id}
GET /author/12?categorie=2
```
- 请求通用内容设计
请求参数尽量不使用嵌套结构，易于解析。请求参数命名规范：

|  字段  |  说明   |
| ------ | ------ |
| pageSize    |  每页显示条数  |
| pageNo    |  当前页数  |

返回内容命名规范

|  字段  |  说明   |
| ------ | ------ |
| respCode    |  响应码(数值型)  |
| respMsg    |  响应描述  |
| resource    |  返回资源信息集  |
