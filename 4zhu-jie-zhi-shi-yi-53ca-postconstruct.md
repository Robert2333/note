# 4.注解知识以及@PostConstruct

## 4.1 @PostConstruct

spring自带的@schedule，没有开关，项目启动总会启动一个线程；

做项目的时候就使用Java的timer，这个设置开关即可自由的控制，关闭的时候，不会启动线程；

Java的timer也需要找到一个启动类，可以放到main函数里面启动，这样的话，代码的耦合性太高了，而使用PostConstruct是很干净的。

其实从依赖注入的字面意思就可以知道，要将对象p注入到对象a，那么首先就必须得生成对象p与对象a，才能执行注入。所以，如果一个类A中有个成员变量p被@Autowired注解，那么@Autowired注入是发生在A的构造方法执行完之后的。

如果想在生成对象时候完成某些初始化操作，而偏偏这些初始化操作又依赖于依赖注入，那么就无法在构造函数中实现。为此，可以使用@PostConstruct注解一个方法来完成初始化，@PostConstruct注解的方法将会在依赖注入完成后被自动调用。

> Constructor &gt;&gt; @Autowired &gt;&gt; @PostConstruct

## 4.2 注解的语法

* **@Target：**

表示该注解可以用于什么地方，可能的ElementType参数有：

CONSTRUCTOR：构造器的声明

FIELD：域声明（包括enum实例）

LOCAL\_VARIABLE：局部变量声明

METHOD：方法声明

PACKAGE：包声明

PARAMETER：参数声明

TYPE：类、接口（包括注解类型）或enum声明

* **@Retention**

表示需要在什么级别保存该注解信息。可选的RetentionPolicy参数包括：

SOURCE：注解将被编译器丢弃

CLASS：注解在class文件中可用，但会被VM丢弃

RUNTIME：VM将在运行期间保留注解，因此可以通过反射机制读取注解的信息

* **@Document**

将注解包含在Javadoc中

* **@Inherited**

允许子类继承父类中的注解



