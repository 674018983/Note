# Java反射 #

##

**解释** **：**  是Java 程序开发语言的特征之一，它允许运行中的 Java 程序获取自身的信息，并且可以操作类或对象的内部属性。

**作用** **：** 主要用于可以在运行时获得程序或程序集中每一个类型的成员和成员的信息，可以动态地创建对象并调用其属性。主要提供以下功能：

- 在运行时判断任意一个对象所属的类；
- 在运行时构造任意一个类的对象；
- 在运行时判断任意一个类所具有的成员变量和方法（通过反射甚至可以调用private方法）；
- 在运行时调用任意一个对象的方法；


**使用小用例** **：** 可以通过反射，动态获取安卓源码中的某些参数数值或者状态，甚至可以得到私有类的属性。

##

## 基本使用 ##

### 操作步骤: ###


- 1、获得Class对象(方法有三种)

(方法一)  使用Class类的forName静态方法:
			
		Class.forName(driver);

(方法二)  直接获取某一个对象的class	

		Class<?> klass = int.class;

		Class<?> classInt = Integer.TYPE


(方法三) 调用某个对象的getClass()方法

		StringBuilder str = new StringBuilder("123");
		Class<?> klass = str.getClass();

- 2、判断是否为某个类的实例（我们用instanceof关键字来判断是否为某个类的实例，同时我们也可以借助反射中Class对象的isInstance()方法来判断是否为某个类的实例）

			
		public native boolean isInstance(Object obj);


- 3、创建实例（通过反射来生成对象主要有两种方式）


(方法一)  使用Class对象的newInstance()方法来创建Class对象对应类的实例:
			
		Class<?> c = String.class;
		Object str = c.newInstance();

(方法二)  先通过Class对象获取指定的Constructor对象，再调用Constructor对象的newInstance()方法来创建实例。这种方法可以用指定的构造器构造类的实例。	

		//获取String所对应的Class对象
		Class<?> c = String.class;
		//获取String类带一个String参数的构造器
		Constructor constructor = c.getConstructor(String.class);
		//根据构造器创建实例
		Object obj = constructor.newInstance("23333");
		//System.out.println(obj);

- 4、获取方法（获取某个Class对象的方法集合，主要有以下几个方法：）（看test1实例）


(方法一)  getDeclaredMethods()方法返回类或接口声明的所有方法，包括公共、保护、默认（包）访问和私有方法，但不包括继承的方法。:
			
			
		public Method[] getDeclaredMethods() throws SecurityException

(方法二)  getMethods()方法返回某个类的所有公用（public）方法，包括其继承类的公用方法。

			
		public Method[] getMethods() throws SecurityException
	

(方法三)  getMethod方法返回一个特定的方法，其中第一个参数为方法名称，后面的参数为方法的参数对应Class的对象。

			
		public Method getMethod(String name, Class<?>... parameterTypes)

- 5、获取构造器信息（获取类构造器的用法与上述获取方法的用法类似。主要是通过Class类的getConstructor方法得到Constructor类的一个实例，而Constructor类有一个newInstance方法可以创建一个对象实例:）

			
		public T newInstance(Object ... initargs);
- 6、获取类的成员变量（字段）信息

		getFiled: 访问公有的成员变量
		getDeclaredField：所有已声明的成员变量。但不能得到其父类的成员变量
		getFileds和getDeclaredFields用法同上（参照Method）

- 7、调用方法（当我们从类中获取了一个方法后，我们就可以用invoke()方法来调用这个方法。invoke方法的原型为:）（test2实例）

			
		public Object invoke(Object obj, Object... args)
        throws IllegalAccessException, IllegalArgumentException,
           InvocationTargetException

- 8、利用反射创建数组（数组在Java里是比较特殊的一种类型，它可以赋值给一个Object Reference，利用反射创建数组的例子:）

			
		public static void testArray() throws ClassNotFoundException {
        Class<?> cls = Class.forName("java.lang.String");
        Object array = Array.newInstance(cls,25);
        //往数组里添加内容
        Array.set(array,0,"hello");
        Array.set(array,1,"Java");
        Array.set(array,2,"fuck");
        Array.set(array,3,"Scala");
        Array.set(array,4,"Clojure");
        //获取某一项的内容
        System.out.println(Array.get(array,3));
    	}

##

### 具体代码 ###
	public class test1 {
		public static void test() throws IllegalAccessException, InstantiationException, NoSuchMethodException, InvocationTargetException {
		        Class<?> c = methodClass.class;
		        Object object = c.newInstance();
		        Method[] methods = c.getMethods();
		        Method[] declaredMethods = c.getDeclaredMethods();
		        //获取methodClass类的add方法
		        Method method = c.getMethod("add", int.class, int.class);
		        //getMethods()方法获取的所有方法
		        System.out.println("getMethods获取的方法：");
		        for(Method m:methods)
		            System.out.println(m);
		        //getDeclaredMethods()方法获取的所有方法
		        System.out.println("getDeclaredMethods获取的方法：");
		        for(Method m:declaredMethods)
		            System.out.println(m);
		    }
	    }
	class methodClass {
	    public final int fuck = 3;
	    public int add(int a,int b) {
	        return a+b;
	    }
	    public int sub(int a,int b) {
	        return a+b;
	    }
	}

### 代码结果 ###
	getMethods获取的方法：
	public int org.ScZyhSoft.common.methodClass.add(int,int)
	public int org.ScZyhSoft.common.methodClass.sub(int,int)
	public final void java.lang.Object.wait() throws java.lang.InterruptedException
	public final void java.lang.Object.wait(long,int) throws java.lang.InterruptedException
	public final native void java.lang.Object.wait(long) throws java.lang.InterruptedException
	public boolean java.lang.Object.equals(java.lang.Object)
	public java.lang.String java.lang.Object.toString()
	public native int java.lang.Object.hashCode()
	public final native java.lang.Class java.lang.Object.getClass()
	public final native void java.lang.Object.notify()
	public final native void java.lang.Object.notifyAll()
	getDeclaredMethods获取的方法：
	public int org.ScZyhSoft.common.methodClass.add(int,int)
	public int org.ScZyhSoft.common.methodClass.sub(int,int)
##


	public class test2 {
	    public static void main(String[] args) throws IllegalAccessException, InstantiationException, NoSuchMethodException, InvocationTargetException {
	        Class<?> klass = methodClass.class;
	        //创建methodClass的实例
	        Object obj = klass.newInstance();
	        //获取methodClass类的add方法
	        Method method = klass.getMethod("add",int.class,int.class);
	        //调用method对应的方法 => add(1,4)
	        Object result = method.invoke(obj,1,4);
	        System.out.println(result);
	    }
	}
	class methodClass {
	    public final int fuck = 3;
	    public int add(int a,int b) {
	        return a+b;
	    }
	    public int sub(int a,int b) {
	        return a+b;
	    }
	}
### 实现效果/成效: ###

能反射出想要的对象及其属性参数/数值。
	
##

### 优点 ###

可以动态地创建对象并调用其属性

### 缺点/不足 ###

由于反射会额外消耗一定的系统资源，因此如果不需要动态地创建一个对象，那么就不需要用反射。另外，反射调用方法时可以忽略权限检查，因此可能会破坏封装性而导致安全问题。

##

### 更多扩展知识/具体命令详解 ###

暂无
 

### 具体个人分析 ###

能获取安卓中的一些私有类属性及数值，同时能反射获取安卓源码中的类，并对其进行相应的设置，如获取其中某个List的内容

##

### 参考文档 ###

[深入解析Java反射（1） - 基础](https://www.sczyh30.com/posts/Java/java-reflection-1/)