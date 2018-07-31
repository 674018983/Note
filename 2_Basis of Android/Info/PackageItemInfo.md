# PackageItemInfo #

##

**解释** **：**  它是AndroidManifest.xml文件中所有节点的基类，代表一个应用包内所有组件和通用信息的基类。该类提供最基本的属性集合，如：label、icon、meta等。



**作用** **：** 一般不会直接用这个类，设计它的目的就是为包内其他基本组件提供统一的基础定义。它没有实现接口Parcelable，但它提供了传Parcel型的构造函数，以及writeToParcel()方法给它的子类来实现PackageItemInfo内部的成员Parcel化。

注：Parcel：是一个容器，它主要用于存储序列化数据，然后可以通过Binder在进程间传递这些数据，可以包含原始数据类型，可以包含Parcelable对象，它还包含了一个活动的IBinder对象的引用。

**使用小用例** **：**

##



### 重要成员变量简介: ###

- **public int icon** **：** 获取该组件项在R文件中drawable的资源id值，对应的是"android:icon"属性，如果不设置为0。

- **public int labelRes** **：** 获取该组件项在R文件中String型的资源idint值，对应的是"android:label"，如果不设置为0。

- **public String packageName** **：** 获取该组件项的包名，对应的是"android:packagename"属性。

- **public String name** **：** 获取该组件项的公共名称，对应的是"android:name"

- **public int banner** **：** 获取该组件项在R文件中drawable的资源id值，对应是"android:banner"，不设置为0

- **public int logo** **：** 获取该组件项在R文件中drawable的资源id值，比应用图标要大，一般用在ToolBar上面，对应是"android: logo"，不设置为0

- **public Bundle metaData** **：** 对应AndroidManifest中的<meta-data>标签。只有<activity>、<activity-alias>、<service>、<receiver>、<application>标签中可能包含<meta-data>子标签。

- **public int logo** **：** 获取该组件项在R文件中drawable的资源id值，比应用图标要大，一般用在ToolBar上面，对应是"android: logo"，不设置为0

- **public int showUserIcon** **：** 默认值是serHandle.USER_NULL、也可能是UserHandle.USER_OWNER，只有实例的引用来访问


### 重要方法简介: ###

- **PackageItemInfo()** **：** 构造函数

- **public PackageItemInfo(PackageItemInfo orig)** **：** 构造函数，传入一个orig，进行变量拷贝而已

- **protected PackageItemInfo(Parcel source)** **：** 反序列化时用到的构造函数，注释他是protected，说只要是PackageItemInfo的子类局均可以调用

- **public CharSequence loadLabel(PackageManager pm)** **：** 返回该组件项的标签，优先级为：nonLocalizedLabel>labelRes>name>packageName

- **public Drawable loadIcon(PackageManager pm)** **：** 获取当前组件的图标，其实是通过PackageManager的loadItemIcon()来获取的。

- **public Drawable loadBanner(PackageManager pm)** **：** 获取当前组件的的banner，内部是通过PackageManager的getDrawable()来获取的banner对应的Drawable，如果banner为0，返回loadDefaultBanner()的结果。

- **public Drawable loadLogo(PackageManager pm)** **：** 返回该组件项的大图标，通过PackageManager的getDrawable()方法获取logo对应的Drawable，如果logo为0，返回loadDefaultLogo()的结果

- **public Drawable loadDefaultIcon(PackageManager pm)** **：** 返回该组件项的默认图标，通过PackageManager的getDefaultActivityIcon()方法，返回的是com.android.internal.R.drawable.sym_def_app_icon对应的Drawable。

- **protected Drawable loadDefaultBanner(PackageManager pm)** **：** 返回null

- **protected Drawable loadDefaultLogo(PackageManager pm)** **：** 返回null

- **public XmlResourceParser loadXmlMetaData(PackageManager pm, String name)** **：** 找到metaData对应为name的资源id，通过PackageManager的getXml()方法返回id对应的XmlResourceParser。

- **protected ApplicationInfo getApplicationInfo()** **：** 返回null

- **public void writeToParcel(Parcel dest, int parcelableFlags)** **：** 为PackageItemInfo的子类Parcel化提供基类部分成员的写入。
	
##


### 更多扩展知识/具体命令详解 ###


 

### 具体个人分析 ###

是AndroidManifest.xml文件中所有节点的基类
##

### 参考文档 ###

[APK安装流程详解1——有关"安装ing"的实体类概述](https://www.jianshu.com/p/71c1ce538ee8)