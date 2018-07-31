# ProviderInfo #

##

**解释** **：**  它继承自ComponentInfo并实现了Parcelable接口，它对应manifest里面的<provider>节点的信息。

**作用** **：** 

**使用小用例** **：** 

##

### 重要成员变量简介： ###

- **public String authority：**提供者的名字

- **public String readPermission：**只读的provider的访问权限

- **public String writePermission：**读写的provider的访问权限

- **public boolean grantUriPermissions：**是否授予provider提供特定的Uris访问权限

- **public PatternMatcher[] uriPermissionPatterns：**provider的PatternMatcher数组

- **public PathPermission[] pathPermissions：**provider的PathPermission数组

- **public boolean multiprocess = false：**是否允许多进程多实例

- **public int initOrder = 0：**同一个进程运行的的provider的初始顺序，数字越高，优先级越高

- **public int flags：**provider的选项

		public static final int FLAG_SINGLE_USER = 0x40000000：设置为provider为单例模式。


##

 

### 具体个人分析 ###

它对应manifest里面的<provider>节点的信息。

##

### 参考文档 ###

[APK安装流程详解1——有关"安装ing"的实体类概述](https://www.jianshu.com/p/71c1ce538ee8)