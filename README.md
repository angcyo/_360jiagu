# _360jiagu
[AS--›Gradle 360加固和Walle渠道打包](https://blog.csdn.net/angcyo/article/details/85404921)

# 使用方式

## 下载
使用Git下载:
```java
git clone --depth=1 https://github.com/angcyo/_360jiagu.git _360jiagu
```
使用git下载, 由于项目中的`java`环境比较大, 100+mb, 可能下载需要很长时间.您可以使用百度链接下载:


使用百度下载:

https://pan.baidu.com/s/1tKX4MCdqKlLDjBUnWX2IGg  
https://pan.baidu.com/s/187ENYv-Ey6DbO5CVJd07Ag

```java
// gradle 脚本部分  ~17mb
https://pan.baidu.com/s/1tKX4MCdqKlLDjBUnWX2IGg  
// java 环境部分 ~56mb
https://pan.baidu.com/s/187ENYv-Ey6DbO5CVJd07Ag
//下载之后, 将 java 环境 `java`文件夹 放在 gradle 脚本 中的 `jiagu/` 文件夹下.
```
![](https://raw.githubusercontent.com/angcyo/_360jiagu/master/png/jiagu1.png)

下载只有的`_360jiagu`文件夹, 尽量放在`工程的根目录`.

## 引入
在`APP Module`中, 加入
```java
apply from: '../_360jiagu/jiagu.gradle'
```
![](https://raw.githubusercontent.com/angcyo/_360jiagu/master/png/jiagu3.png)

> 请关注图中, 第一行即可.

## 执行加固
同步(sync)项目之后, 

![](https://raw.githubusercontent.com/angcyo/_360jiagu/master/png/jiagu2.png)

`Tasks`任务列表, 会多出`_360jiagu` , 双击即可.

或者使用命令行 `gradlew _360jiagu` 即可.

# 执行前须知:

**1:配置360的账号和密码**

**2:指定需要加固的文件路径**

>如果不指定加固文件路径,你至少需要使用`release`的方式打包过一次.脚本才能自己识别到文件路径.

![](https://raw.githubusercontent.com/angcyo/_360jiagu/master/png/jiagu4.png)

# 输出路径
请注意控制台的输出.

# 特别提醒

## 1.

如果在加固过程中出现 `签名配置中没有匹配的签名`

请使用命令行的方式单独导入签名信息.

```
java -jar jiagu.jar -importsign<keystore_path><keystore_password><alias><alias_password>
```
请将 命令行`cd 到 _360jiagu/jiagu/` 目录下, 否则会提示`jiagu.jar`找不到.

执行一次之后, 以后就不会出现了.

这有可能是360加固的BUG.

## 2.

如果未指定`加固文件路径`, 同时你又配置了`productFlavors`或者`buildTypes`, 

那么脚本自动获取的路径是`字母按照自然序排序后的最后一个配置路径`

啥意思?

比如:
```java
buildTypes{
  a {
  }
  b {
  }
  c {
  }
  d {
  }
}
```
那么, 就是 `d` 对应的文件路径.

