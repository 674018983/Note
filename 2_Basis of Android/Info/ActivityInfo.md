# ActivityInfo #

##

**解释** **：**  它继承自ComponentInfo并实现了Parcelable 接口，它对应manifest里面的<activity>或者<receiver>节点的信息。我们可以通过它来设置我们的任何属性，包括theme、launchMode等，常用方法继承至PackageItemInfo类中的loadIcon()和loadLabel()


**作用** **：** 

**使用小用例** **：** 

##


### 重要成员变量简介： ###

- **public int launchMode：**Activity的启动模式，对应Manifest的"launchMode"属性，可能是以下几种模式：

		public static final int LAUNCH_MULTIPLE = 0：普通模式

		public static final int LAUNCH_SINGLE_TOP = 1：同一个task如果是顶部，复用

		public static final int LAUNCH_SINGLE_TASK = 2：同一个task，无论是不是在顶部都复用

		public static final int LAUNCH_SINGLE_INSTANCE = 3：新开一个task

- **public int documentLaunchMode：**总览画面--overview screenActivity的启动模式，关于总览画面可以参考 Android 5.0 Overview Screen--总览画面，对应AndroidManifest里面的"documentLaunchMode"属性，如果一个Activity添加了这个属性，则该Activity被启动时永远会创建一个新的task。该属性有4个值，用户在应用中打开的一个document会有不同的效果如下：

		public static final int DOCUMENT_LAUNCH_NONE = 0：
		Activity不会为document创建新的task，App设置为single task模式。
		它会重新调用用户唤醒的所有activity中的最近的一个。

		public static final int DOCUMENT_LAUNCH_INTO_EXISTING = 1：
		activity 会为该document请求一个已经存在的task

		public static final int DOCUMENT_LAUNCH_ALWAYS = 2：
		即使docutment已经开打了，activity也会为document创建一个新的task。

		public static final int DOCUMENT_LAUNCH_NEVER = 3：
		activity不会为document创建一个新的task。


- **public int persistableMode：**activity持久化的模式，对应着AndroidManifest的"android:persistableMode"属性，它有三个模式如下：

		public static final int PERSIST_ROOT_ONLY = 0：
		默认值，仅仅会作用在跟activity活着task中。

		public static final int PERSIST_NEVER = 1：
		不起作用，不用两个持久化页面数据或状态

		public static final int PERSIST_ACROSS_REBOOTS = 2：
		重启设备或持久化页面的数据或者状态，
		如果在这个界面上的界面也设置这个值，上面的页面也会被持久化，
		最后系统会将你保存的数据，在重新打开这个页面的时候，
		会调用onCreate()具有两个参数的方法。
		你只要在你第二个参数PersistableBundle中取出你保存的数据就可以了

- **public String requestedVrComponent：**跑在Activity上面的VrListenerService的组件名称。
 
- **public int screenOrientation：**表示Activity运行的屏幕的方向。对应AndroidManifest里面的"android:screenOrientation"属性，具体属性值如下：

		public static final int SCREEN_ORIENTATION_UNSPECIFIED：
		未指定，它是默认值，由Android系统自己选择适当的方向，
		选择策略是具体设备的配置情况而定，因此不同的设备会有不同的方向选择。

		public static final int SCREEN_ORIENTATION_LANDSCAPE：
		表示横屏，显示时宽度大于高度

		public static final int SCREEN_ORIENTATION_PORTRAIT：
		表示书评，显示时高度大于宽度

		public static final int SCREEN_ORIENTATION_USER：
		表示用户当前的首选方向。

		public static final int SCREEN_ORIENTATION_BEHIND：
		表示用户继续Activity堆栈中当前Activity下面的那个Activity的方向。

		public static final int SCREEN_ORIENTATION_SENSOR：
		表示由物理感应器决定显示方向，它取决于用户如何持有设备，
		当设备被旋转时方向会随之变化——在横屏和竖屏之间切换
		
		public static final int SCREEN_ORIENTATION_NOSENSOR：
		忽略物理感应器——即显示方向和物理感应器无关，
		不管用户如何旋转设备，显示方向都不会发生改变。

		public static final int SCREEN_ORIENTATION_SENSOR_LANDSCAPE：
		表示Activity在横向屏幕上显示，但是可以根据方向传感器的指示来进行改变

		public static final int SCREEN_ORIENTATION_SENSOR_PORTRAIT：
		表示Activity在纵向屏幕上显示，可以根据方向传感器指示的方向来进行改变。

		public static final int SCREEN_ORIENTATION_REVERSE_LANDSCAPE：
		表示Activity横屏显示，当时与正常的横屏方向相反
		(比如原来很平方向是向左的，这时候也是横屏但是方向向右)

		public static final int SCREEN_ORIENTATION_REVERSE_PORTRAIT：
		表示Activity竖屏显示，但是与正常的纵向方向的屏幕方向相反

		public static final int SCREEN_ORIENTATION_FULL_SENSOR：
		表示Activity的方向由方向传感器决定，会根据用户设备的移动情况来旋转


##


### 具体个人分析 ###

它对应manifest里面的<activity>或者<receiver>节点的信息。

##

### 参考文档 ###

[APK安装流程详解1——有关"安装ing"的实体类概述](https://www.jianshu.com/p/71c1ce538ee8)