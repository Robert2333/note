# 1. Java反射

### 1.类初始化

> 类初始化时类加载的最后一步，前面的类加载的过程中，除了在加载截断用户应用程序可以通过自定义_**类加载器**_参与之外，其余动作完全由虚拟机主导和控制。

### 2.类加载器

**通过一个类的全限定名来获取描述此类的二进制流。**

对于虚拟机而言，只有两种类加载器，一种是启动类加载器（bootstrap classloader），另一种是其他加载器。

> 启动加载器：这个类负责将存放在&lt;JAVA\_HOME&gt;\lib 目录中的，或者被-Xbootclasspath参数所指定的路金钟，并且是虚拟机识别的（仅按文件名识别，如rt.jar）类加载到虚拟机内存中。如果需要将加载请求委托给引导类加载器，直接使用null替换即可。

> 扩展类加载器（extension classloader）：这个加载器由sun.misc.Launcher$ExtClassLoader实现，它负责加载&lt;JAVA\_HOME&gt;\lib\ext 目录下，或者被java.ext.dirs系统变量指定的类库

> 应用程序加载器（Application Classloader）这个类由sun.misc.Launcher$AppClassLoader实现，它负责加载用户类路径下（classpath）上锁指定的类库。

* classpath就是存放.class等编译后文件的路径

#### 2.1 JAVA获取classpath路径：

ClassLoader 提供了两个方法用于从装载的类路径中取得资源：

```java
public URL  getResource (String name);  
public InputStream  getResourceAsStream (String name);  
```

  






