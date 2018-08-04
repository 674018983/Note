# ComponentInfo #

##

**解释** **：**  它代表一个应用内部的组件(如ActivityInfo、ServiceInfo、ProviderInfo)，一般不会直接使用这个类。


**作用** **：** 它被设计出来是为了不同应用的组件共享统一的定义。它继承与PackageItemInfo，但它不像ApplicationInfo一样实现了Parcelable接口。它是没有实现Parcelable接口，但是它提供了入参是Parcel的构造函数，以及writeToParcel()方法给它的子类来实现ComponentInfo内部这部分的成员的Parcel化。

**使用小用例** **：** 

##


### 重要成员变量简介： ###

- **public ApplicationInfo applicationInfo：**组件所在的application/package信息，从<application>标签得到。

- **public String processName：**组件所运行的进程名称，String类型，从"android:process"属性得到

- **public int descriptionRes：**组件的描述，string型的资源id，从"android:description"，如果不设置则为0。

- **public boolean enabled：**当前组件是否被实例化，boolean类型，从"android:enabled"属性得到，如果它所在的Application中的enable为false，则这处的设置无效。

- **public boolean exported：**当前组件能否被其他Application的组件启动，boolean类型，可以从"android:exported"属性得到。

	如果当前组件没有一个<intent-filter>则它默认为false(没有任何<intent-filter>表明要组件的准确名称来启动)，exported=false表明当前组件只能被当前应用内组件启动，或者有相同的UID的应用。

	当然也可以使用permission来限制外部应用对组件的访问，如果该组件有"android:permission"属性，则访问这必须声明该权限。当该组件无permission属性而<application>标签有声明时，则访问者必须有<application>签名的permisson。

##

### 重要方法简介： ###

- **public ComponentInfo()：**构造函数

- **public ComponentInfo(ComponentInfo orig)：**构造函数，传入一个ComponentInfo，其实就是拷贝

- **protected ComponentInfo(Parcel source)：**构造函数，传入一个source，然后从source里面取出相应的值来完成字段的初始化

- **public CharSequence loadLabel(PackageManager pm)：**返回该组件的标签，CharSequence类型，优先级次序为：nonLocalizedLabel>labelRes>applicationInfo.nonLocalizedLabel>applicationInfo.labelRes

- **public boolean isEnable()：**该组件是否启动该组件及包含的应用程序，有且只有当enabled和applicationInfo.enable同时为true时，返回true。

- **public final int getIconResource()：**返回该组件的icon的资源id，类型是int，如果是0，则返回applicationInfo对应的资源id

- **public final int getLogoResource()：**返回该组件的logo对应的资源id，如果没有，则返回applicationInfo对应的资源id。

- **public final int getBannerResource()：**返回该组件banner对应的资源id，如果没有，则返回applicationInfo对应的资源id。

- **@hide public Drawable loadDefaultIcon(PackageManager pm)：**返回组件默认的icon，类型是Drawable，返回的是applicationInfo的loadIcon()

- **@hide protected Drawable loadDefaultBanner(PackageManager pm)：**返回组件默认的banner，类型是Drawable，返回的是applicationInfo的loadBanner()

- **@hide protected Drawable loadDefaultLogo(PackageManager pm)：**返回组件默认的logo，类型是Drawable，返回的是applicationInfo的loadLogo()

- **@hide protected ApplicationInfo getApplicationInfo()：**返回该组件的applicationInfo

- **public void writeToParcel(Parcel dest, int parcelableFlags)：**先调用父类PackageItemInfo的writeToParcel()方法，再完成自己的成员Parcel化



##


 

### 具体个人分析 ###

它代表一个应用内部的组件(如ActivityInfo、ServiceInfo、ProviderInfo)

##

### 参考文档 ###

[APK安装流程详解1——有关"安装ing"的实体类概述](https://www.jianshu.com/p/71c1ce538ee8)