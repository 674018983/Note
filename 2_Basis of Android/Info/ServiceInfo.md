# ServiceInfo #

##

**解释** **：**  它继承自ComponentInfo并实现了Parcelable接口，它对应manifest里面的<service>节点的信息。

**作用** **：** 

**使用小用例** **：** 

##


### 重要成员变量简介： ###

- **public String permission：**这个Service的访问权限

- **public int flags：**表示service在AndroidManifest设置的选项

		public static final int FLAG_STOP_WITH_TASK：
		如果用户删除了预计应程序的Activitiest，系统将自动停止这个Service

		public static final int FLAG_ISOLATED_PROCESS：
		Service在其独立的进程中运行

		public static final int FLAG_EXTERNAL_SERVICE：
		这个�Service可以被外部包调用

		public static final int FLAG_SINGLE_USER：
		表示Service就是一个单例。

##

 

### 具体个人分析 ###
它对应manifest里面的<service>节点的信息。

##

### 参考文档 ###

[APK安装流程详解1——有关"安装ing"的实体类概述](https://www.jianshu.com/p/71c1ce538ee8)