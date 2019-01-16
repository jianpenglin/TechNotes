# github-pages 配置

## github创建pages工程

1. 使用 `用户名.github.io` 的形式命名工程
2. 创建`CNAME`文件，设置网站地址`www.techinfo.vip`
3. 创建index.html，可以通过代码进行页面跳转，或者就直接当主页，或者创建README.md生成markdown pages，
我是直接跳转到另一个工程`<script type="text/javascript">window.location.href="http://www.techinfo.vip/TechNotes/";</script>`
4. 进入Settings-GitHub Pages 做github pages相关配置
    - Source  选择主分支点击保存
    - Theme Chooser 选择一个主题
    - Custom domain 输入 `www.techinfo.vip` 保存
5. 类似第4步方法，开启TechNotes工程的GitHub Pages功能

## 配置阿里云服务器

1. 添加DNS解析记录CNAME类型，记录值写github地址 `用户名.github.io`， 添加后主机记录显示`@`
2. 同上再添加一条主机记录为 www 的解析记录
