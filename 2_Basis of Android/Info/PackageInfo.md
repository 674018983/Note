# PackageInfo #

##

**解释** **：**  

**作用** **：** PackageInfo是实现Parcelable接口，所以它可以在进程间传递

**使用小用例** **：** 

##

### 重要成员变量简介： ###
- **public String packageName** **：** 包名

- **public String versionName** **：** 版本名

- **public String versionCode** **：** 版本号

- **public String sharedUserId** **：** 共享用户ID，签名相同的情况下程序之间数据共享

- **public long firstInstallTime** **：** 第一次安装时间，忽略之前安装后卸载的情况单位ms

- **public long lastUpdateTime** **：** 最后更新时间，相同版本号的APK覆盖安装，该值也会发生变化，单位ms

- **public String[] requestedPermissions** **：** 请求的权限

- **public ApplicationInfo applicationInfo** **：** Applicationinfo对象

- **public ActivityInfo[] activities** **：** 注册的Activity

- **public ActivityInfo[] receivers** **：** 注册的Receiver，PS：注意这里是ActivityInfo[]

- **public ServiceInfo[] services** **：** 注册的服务

- **public ProviderInfo[] providers** **：** 注册的Providers


###重要方法介绍：###
- **public PackageInfo()** **：** 构造函数

- **private PackageInfo(Parcel source)** **：** 构造函数，反序列时用到的，注意这个方法是private，所以这个方法只是给反序列时用的，所以PackageInfo对外就提供一个构造函数

- **private void propagateApplicationInfo(ApplicationInfo appInfo, ComponentInfo[] components)** **：** 主要是给入参的components中的每一项ComponentInfo的applicationInfo变量指向第一个入参appInfo。


##
### 具体个人分析 ###

一个存储/获取包的序列化类

##

### 参考文档 ###

[APK安装流程详解1——有关"安装ing"的实体类概述](https://www.jianshu.com/p/71c1ce538ee8)