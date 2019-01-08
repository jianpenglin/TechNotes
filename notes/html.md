# HTML 协议与应用

## 协议介绍

## 发送请求与spring集成

当前台界面使用GET或POST方式提交数据时，数据编码格式由请求头的Content-Type指定。分为以下几种情况：
1. application/x-www-form-urlencoded，这种情况的数据@RequestParam、@ModelAttribute可以处理，@RequestBody也可以处理。
2. multipart/form-data，@RequestBody不能处理这种格式的数据。（form表单里面有文件上传时，必须要指定enctype属性值为multipart/form-data，意思是以二进制流的形式传输文件。）
3. application/json、application/xml等格式的数据， **必须** 使用@RequestBody来处理。
