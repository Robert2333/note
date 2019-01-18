# 1. Java反射

### 1.类初始化

> 类初始化时类加载的最后一步，前面的类加载的过程中，除了在加载截断用户应用程序可以通过自定义_**类加载器**_参与之外，其余动作完全由虚拟机主导和控制。

### 2.类加载器

**通过一个类的全限定名来获取描述此类的二进制流。**

对于虚拟机而言，只有两种类加载器，一种是启动类加载器（bootstrap classloader），另一种是其他加载器。

> 启动加载器：这个类负责将存放在&lt;JAVA\_HOME&gt;\lib 目录中的，或者被-Xbootclasspath参数所指定的路金钟，并且是虚拟机识别的（仅按文件名识别，如rt.jar）类加载到虚拟机内存中。如果需要将加载请求委托给引导类加载器，直接使用null替换即可。
>
> 扩展类加载器（extension classloader）：这个加载器由sun.misc.Launcher$ExtClassLoader实现，它负责加载&lt;JAVA\_HOME&gt;\lib\ext 目录下，或者被java.ext.dirs系统变量指定的类库
>
> 应用程序加载器（Application Classloader）这个类由sun.misc.Launcher$AppClassLoader实现，它负责加载用户类路径下（classpath）上锁指定的类库。

* classpath就是存放.class等编译后文件的路径

---

tomca之类的web容器就不采用双亲委托机制（servlet规范中的建议），为了保证

* 依赖独立，不受影响
* tomcat使用的类库要和部署的分开
* 某些类库可以共享
* 部署的类库可以共享。

#### 2.1 JAVA获取classpath路径：

ClassLoader 提供了两个方法用于从装载的类路径中取得资源：

```java
public URL  getResource (String name);  
public InputStream  getResourceAsStream (String name);
```

#### 2.2 Java中的.class和getClass的区别

* getClass\(\)是Object类的方法，它可以获得一个实例的类型类。它是**运行时根据实际实例确定，getClass\(\)是动态而且是final的**。

> A a=new B\(\);//A为接口，B为实例，那么getClass\(\)获取到的class为B

* .class编译时确定，所以上述例子拿到的class就是A

### 3.反射

通过反射创建类对象主要有两种方式：通过 Class 对象的 newInstance\(\) 方法、通过 Constructor 对象的 newInstance\(\) 方法

\(1\).通过 Class 对象的 newInstance\(\) 方法。

```java
Class clz = Apple.class;
Apple apple = (Apple)clz.newInstance();
```

\(2\).通过 Constructor 对象的 newInstance\(\) 方法

```java
Class clz = Apple.class;
Constructor constructor = clz.getConstructor();
Apple apple = (Apple)constructor.newInstance();
```

通过 Constructor 对象创建类对象可以选择特定构造方法，而通过 Class 对象则只能使用默认的无参数构造方法。下面的代码就调用了一个有参数的构造方法进行了类对象的初始化。

```java
Class clz = Apple.class;
Constructor constructor = clz.getConstructor(String.class, int.class);
Apple apple = (Apple)constructor.newInstance("红富士", 15);
```

对应的类为

```java
public class Apple{
    public Apple(String name,int number){
        ....
    }
}
```

#### 3.1 获取属性值

```java
 Field[] fields = cls.getDeclaredFields();//不管私有还是public的都可以取到
 for (int i=0;i<fields.length;i++){//遍历
               try {
                   //得到属性
                   Field field = fields[i];
                   //打开私有访问
                   field.setAccessible(true);
                   //获取属性
                   String name = field.getName();
                   //获取属性值
                   Object value = field.get(obj);
                   //一个个赋值
                   nameVlues += field.getName()+":"+value+",";
               } catch (IllegalAccessException e) {
                   e.printStackTrace();
               }
```

#### 3.2 获取方法

```java
      Method[] methods = clz.getDeclaredMethods();//clz:instance of Class
      for (Method method : methods) {
         System.out.println("方法名：" + method.getName());
         //获取本方法所有参数类型，存入数组
         Class<?>[] getTypeParameters = method.getParameterTypes();
         if (getTypeParameters.length == 0) {
            System.out.println("此方法无参数");
         }
         for (Class<?> class1 : getTypeParameters) {
            String parameterName = class1.getName();
            System.out.println("参数类型：" + parameterName);
         }
         System.out.println("****************************");
      }
```

* 调用方法

```java
public class Test {

   public void hello(String s) {
      System.out.println(s);
   }

   public static void main(String[] args) throws IllegalAccessException, InstantiationException, NoSuchMethodException, InvocationTargetException {
      Class clz = Test.class;
      Object o = clz.newInstance();
      Method m = clz.getDeclaredMethod("hello", String.class);
      m.invoke(o, "222");
   }
}
```



