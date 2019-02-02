# 4.注解知识以及@PostConstruct

### 4.1@PostConstruct

spring自带的@schedule，没有开关，项目启动总会启动一个线程；

做项目的时候就使用Java的timer，这个设置开关即可自由的控制，关闭的时候，不会启动线程；

Java的timer也需要找到一个启动类，可以放到main函数里面启动，这样的话，代码的耦合性太高了，而使用PostConstruct是很干净的。

其实从依赖注入的字面意思就可以知道，要将对象p注入到对象a，那么首先就必须得生成对象p与对象a，才能执行注入。所以，如果一个类A中有个成员变量p被@Autowired注解，那么@Autowired注入是发生在A的构造方法执行完之后的。

如果想在生成对象时候完成某些初始化操作，而偏偏这些初始化操作又依赖于依赖注入，那么就无法在构造函数中实现。为此，可以使用@PostConstruct注解一个方法来完成初始化，@PostConstruct注解的方法将会在依赖注入完成后被自动调用。

> Constructor &gt;&gt; @Autowired &gt;&gt; @PostConstruct





