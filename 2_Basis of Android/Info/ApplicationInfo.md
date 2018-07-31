# ApplicationInfo #

##

**解释** **：**  它继承自PackageItemInfo并实现了Parcelable 接口，它对应manifest里面的<application>节点的信息。

**作用** **：** 

**使用小用例** **：** 

##


### 特殊成员变量flags如下: ###

- **int flags：**代表Application的类型，它是进行"位与"操作的选项，大家可以看下面的每一个只占用"1位"：
- 再执行具体步骤

- **FLAG_SYSTEM：**系统应用程序

- **FLAG_DEBUGGABLE：**应用程序允许debug，对应manifest里面的android:debuggable属性。

- **FLAG_HAS_CODE：**应用程序是否含有代码，平时比较少用，如果，对应manifest里面的android:hasCode，为true表明有代码，为false表明代码，如果没有代码则加载组件时系统不会尝试加载任何应用程序的代码。应用程序一般没有它自己的任何代码，除非它仅仅是由组件类的构建而成的。

- **FLAG_PERSISTENT：**应用程序是否永久驻留，对应manifest文件中的android:persistent="true"，理论上意思是应用程序所在进程不会被LMK杀死。但是这里有个前提，就是应用程序必须是系统应用。也就是说普通的应用程序设置这个属性其实是没有用的。如果你的应用程序的apk直接放到/system/app目录下。而且必须重启系统才能生效

- **FLAG_FACTORY_TEST：**应用程序支持Factory Test

- **FLAG_ALLOW_TASK_REPARENTING：**设置activity从一个task迁移到另一个task的标签，这块后面在activity启动流程中会详细讲解，对应的manifest文件是android:allowTaskReparenting。

- **FLAG_ALLOW_CLEAR_USER_DATA：**设置用户自动清除数据，对应manifest中为
android:allowClearUserData，该值设为true时，用户可以自己自己清除用户数据，反之则用户不能清除。

- **FLAG_UPDATED_SYSTEM_APP：**表明系统应用程序被用户升级后，也算用户的应用程序

- **FLAG_TEST_ONLY：**表示该应用仅仅用于测试，对应manifest里面的android:testOnly，如果设置为true，则表明仅仅用于测试

- **FLAG_SUPPORTS_SMALL_SCREENS：** 设置应用程序的window可以缩小到较小屏幕的大小，对应的manifest里面的android:smallScreens，值为true，则表明可以缩小。

- **FLAG_SUPPORTS_NORMAL_SCREENS：** 设置应用程序的window可以在正常的屏幕上显示，对应的manifest里面的android:normalScreens，值为true，则表明可以显示。

- **FLAG_SUPPORTS_LARGE_SCREENS：** 设置应用的window可以放大到较大屏幕的大小，对应的manifest里面的android:largeScreens，值为true，则表明可以放大。

- **FLAG_RESIZEABLE_FOR_SCREENS：** 设置应用程序自己知道如何去适应不同的屏幕密度，对应manifest里面是android:anyDensity，值为true，则应用程序自己调整。

- **FLAG_VM_SAFE_MODE：** 设置应用程序在安全模式下运行VM，即不运行JIT，对应manifest里面的 android:vmSafeMode，值为true则设置为安全模式

- **FLAG_ALLOW_BACKUP：** 设置允许操作系统备份数据，对应的manifest里面的android:allowBackup，设置true则允许备份

- **FLAG_KILL_AFTER_RESTORE：** 这块我也是不很清楚，设置在未来的某个事件点并且版本versionCode要大于当前版本的versionCode，则可以处理还原数据。对应的是manifest里面的android:restoreAnyVersion，值为true则设置。

- **FLAG_EXTERNAL_STORAGE：**表明应用程序安装在SD卡上

- **FLAG_SUPPORTS_XLARGE_SCREENS：**表明应用程序的window可以增加尺寸适用于超大屏幕。在manifest里面对应的android:xlargeScreens

- **FLAG_LARGE_HEAP：**表明应用程序为其进程要求申请更大的内存堆。manifest里面对应的是android:largeHeap

- **FLAG_STOPPED：**表明这个应用程序处于停止状态

- **FLAG_SUPPORTS_RTL：** 表明应用程序支持从右到左，所有Activity将变更为从右到左。

- **FLAG_INSTALLED：**表明该当前应用程序是被当前用户安装的。

- **FLAG_IS_DATA_ONLY：**表明当该应用程序仅仅安装其数据，应用程序包本身并不存在设备上。

- **FLAG_IS_GAME：**表明当该应用程序是一个程序

- **FLAG_FULL_BACKUP_ONLY：**表明定义一个android.app.backup.BackupAgent，通过这个BackupAgent对象来负责进行应用程序的全数据备份。

- **FLAG_USES_CLEARTEXT_TRAFFIC：**表明该应用程序的网络请求是明文，对WebView无用，如果是在Android N上配置网络配置，也无用。对应manifest里面的android:usesCleartextTraffic

- **FLAG_EXTRACT_NATIVE_LIBS：**表明从.apk中提取native库

- **FLAG_HARDWARE_ACCELERATED：**表明当该应用程序开启硬件加速渲染

- **FLAG_SUSPENDED：**表明当该应用程序当前处于挂起状态

- **FLAG_MULTIARCH：**表明当前应用程序的代码需要加载到其他应用程序的进程中。



##

### 重要成员变量简介: ###

- **public String taskAffinity：**和当前应用所有Activity的默认task有密切关系，可以参考下面ActivityInfo的taskAffinity，可以通过AndroidManifest的"android:taskAffinity"属性得到，具体taskAffinity是怎么影响到Activity在task的启动，后面会在Activity启动模式中细讲

- **public String permission：**访问当前应用的所有组件需要声明的权限，在AndroidManifest的"android:permission"属性得到

- **public String processName：**应用运行的进程名，可以在AndroidManifest的"android:process"得到，如果没有设置则默认为应用包名。

- **public String className：**Application类的类名，可以在AndroidManifest的"android:class"属性得到。

- **public int descriptionRes：**对Application组件的描述，可以在AndroidManifest的"android:description"属性得到，不设置则为0

- **public int theme：**应用的主题，可以在AndroidManifest的"android:theme"属性得到，若不设置则为0。

- **public String manageSpaceActivityName：**用于指定一个Activity来管理数据，它最终会出现在"设置->应用程序管理"中，默认按钮为"清楚数据"，可以在AndroidManifest的属性"android:manageSpaceActivity"中设置值，如果设定后，该按钮可点击跳转到该Activity，让用户选择性清除哪些数据，若不设置则为null。

- **public String backupAgentName：**Android原生的备份引擎BackupManagerService在应用端的实现类，是backupAgent的子类。默认不会由系统备份，可以在AndroidManifest属性"android:backupAgent"得到，如果设置"android:allowBackup"为false，则该属性设置无效。

- **public int fullBackupContent = 0：**表明应用是否支持自动备份

- **public int uiOptions = 0：**为应用内所有的Activity设置默认的UI选项，可选值为"none"、"splitActionBarWhenNarrow"。

- **public String sourceDir：**应用APK的全路径

- **public String publicSourceDir：**sourceDir公开可访问的部分，被forward lock锁定的应用该值可能与sourceDir不一样

- **public String[] resourceDirs：**如果当前应用有额外资源包时，表示全路径。通常为null。

- **public String seinfo：**来自Linux策略中seiInfo标签，这个值一般在设置应用进程的SELinux安全上下文时有用。

- **public String dataDir：**应用数据目录

- **public String dataDir：**应用JNI本地库路径

- **public int uid：**Linux Kernel的user ID，目前对每个引用还不是唯一的，存在几个应用共享一个UID的情况。

- **public int targetSdkVersion：**应用最低目标SDK版本号

- **public int versionCode：**应用的版本号

- **public boolean enabled = true：**表明当前应用所有组件是否可用。

	
##

### 重要方法简介: ###
- **public ApplicationInfo()：**构造函数

- **public ApplicationInfo(ApplicationInfo orig)：**构造函数，传入一个ApplicationInfo，进行拷贝。

- **private ApplicationInfo(Parcel source)：**私有的构造函数，序列化专用

- **protected ApplicationInfo getApplicationInfo()：**返回当前ApplicationInfo对象

- **public boolean isSystemApp()：**判断当前应用是否为系统应用。flags与ApplicationInfo.FLAG_SYSTEM按位与不等于0则返回true。

- **public boolean isForwardLocked()：**判断当前应用是否被锁定。flags与ApplicationInfo.PRIVATE_FLAG_FORWARD_LOCK按位与不等于0则返回true。

	
##



### 具体个人分析 ###

对应manifest里面的<application>节点的信息

##

### 参考文档 ###

[APK安装流程详解1——有关"安装ing"的实体类概述](https://www.jianshu.com/p/71c1ce538ee8)