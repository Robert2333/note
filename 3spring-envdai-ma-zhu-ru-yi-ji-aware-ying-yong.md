# 3.spring ENV通过代码注入以及AWARE应用

> `aware`翻译过来是知道的，已感知的，意识到的,各种aware被称为_**容器感知技术**_



| AWARE | 作用 |
| :--- | :--- |
| ApplicationAware | 能获取spring context调用容器的服务 |
| BeanNameAware | 提供对BeanName进行操作 |
| ApplicationEventPublisherAware | 主要用于事件的发布 |
| BeanClassLoadAware | 相关的类加载器 |
| EnvironmentAware | 当所有env加载完毕之后会通知所有的继承了该接口的组件 |



## 方法1.直接继承EnvironmentAware，然后设置其setEnv

## 方法2：

```java
@Configuration
public class Config{
    private ConfigurableEnvironment env;
    public Config(ConfigurableEnvironment env){
        //这里的env就是我们要的  
        this.env=env;      
    }
}
```



#### 坑：cloud中，我需要将eureka通过starter的方式将默认的环境信息注入，但是发现怎么也不能在它自己的设置类_EurekaClientAutoConfiguration_之前进行设置，后面发现，是它的注入是通过_org.springframework.cloud.bootstrap.bootstrapConfiguration=xxx_注入的，该方法相当于配置bootstrap.yml

bootstrap参考链接：[https://blog.csdn.net/dulabing/article/details/80183662](https://blog.csdn.net/dulabing/article/details/80183662)

