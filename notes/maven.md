# maven 基础

## 下载

进入 maven 官网下载页面: http://maven.apache.org/download.cgi  点击 apache-maven-3.6.0-bin.zip 下载。建议最低下载 3.5.0 版本，高版本更加稳定

## 安装

将 maven 解压到某个目录中，配置一下环境变量即完成安装，环境变量的配置与 JDK 的配置方式类似，配置两个环境变量即可。以下是 linux 系统下的配置示例：
```
export MAVEN_HOME=/Users/zhanbo/app/maven-3.5.2
export PATH=$PATH:$JAVA_HOME/bin:$MAVEN_HOME/bin
```
如上所示，将上述两行代码放在 /etc/profile 或者 ~/.bash_profile 文件之中即完成了 maven 的安装。
最后，打开控制台输入如下命令检查 maven 是否安装成功，安装成功会显示 maven 版本号：
```
mvn -v
```

windows 安装

第一步：解压apche-maven-3.5.2.rar
第二步：把这个文件放在C:\Program Files\apache-maven-3.5.2
第三步：进行环境变量配置（右键计算机 -> 点击属性 -> 高级系统设置 -> 高级 -> 环境变量（打开））
第四步：新建
变量名：MAVEN_HOME
变量值：C:\Program Files\apache-maven-3.5.2
第五步：编辑PATH系统变量
注：在添加变量值的时候，会发现path有很多变量值，怎么操作？
点击键盘HOME键，让光标移动到属性值最前边，
首先打一个分号（英语的分号 ;而不是中文的分号；）
再把光标往前移动一位，之后添加属性值，最后点击确定
变量名：Path
变量值：%MAVEN_HOME%\bin;
第六步：配置完成，确定并应用
第七步：验证JDK是否安装成功
用键盘输入 win+R 弹出运行
在运行框中输入 cmd
之后输入 mvn –v
提示：出现Apche Maven 3.5.2表示成功

## 配置Eclipse Maven

eclipse 本身自带一个嵌入的 maven，但嵌入的 maven 使用并不可靠，也不方便，例如在控制台无法使用 maven 的命令行进行操作。所以一定不要使用 eclipse 嵌入的 maven。以下以简要介绍一下配置方式
打开配置主窗口，点击左侧的 Maven 下的 Installatioins 子菜单
点击上图中的 add 按钮会弹窗口
点击上图中的 Directory 选择 maven 解压到的那个目录，勾选刚刚添加的 maven，并去掉其它两个 maven 的勾选项，只保留刚刚安装的那个勾选
最后再点击左侧的 User Settings 菜单，然后分别点击右边两个的 Browe 按钮，为其配置好两个 settings.xml 文件即可，这两个文件在 maven 安装目录的 conf 子目录之下
点击 ok 按钮完成配置
