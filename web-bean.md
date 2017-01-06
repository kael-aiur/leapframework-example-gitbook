# web-bean

这个工程基于web工程示例的是如何使用leap的bean配置。

在`conf/beans.xml`和`conf/beans/*.xml`配置的bean都会被leap扫描并根据配置自动生成bean。

在`conf/beans.xml`中，

```xml
<bean name="bean1" type="leap.example.webbean.bean.ServiceBean" class="leap.example.webbean.bean.ServiceBean1"></bean>
```

这个是最基础的bean配置，通过这个配置可以生成bean对象。

```xml
<bean type="leap.core.ioc.FactoryBean" class="leap.example.webbean.factory.CustomerFactoryBean">
    <register-bean-factory target-type="leap.example.webbean.bean.CustomerBean"/>
</bean>
```

这个是自定义bean工厂的配置，这个配置可以让leap在生成类`leap.example.webbean.bean.CustomerBean`的bean的时候使用这里配置的工程类`leap.example.webbean.factory.CustomerFactoryBean`来生成。

> bean工厂自身也是一个bean，因此需要自定义bean工厂的时候，要先定义工程bean，然后指定这个工程bean生成哪种类的bean对象，这就是上面这段配置的含义。

定义了工程bean之后，我们想要获得`leap.example.webbean.bean.CustomerBean`对象的bean就不用在xml中配置了，可以直接使用`@Inject`注入或者使用`BeanFactory`对象获取，在`leap.example.webbean.controller.HomeController`中可以看到：

```java
// custom factory
@Inject
private CustomerBean customerBean;
```

在`conf/beans/lazyAndNotLayzInitBean.xml`中，可以看到`leap.example.webbean.bean.NotLazyInitBean`bean的配置：

```xml
<bean class="leap.example.webbean.bean.NotLazyInitBean" lazy-init="false">
</bean>
```

这里的`lazy-init="false"`表示这个bean不是懒加载的，在leap启动完成的时候就创建出来。如果没有配置，默认所有的bean都是懒加载的，只在第一次使用的时候创建。

把这个应用部署到tomcat中并运行，可以看到在启动过程中，控制台会打印：

```
create NotLazyInitBean when load ....
```

leap也支持使用注解的方式配置bean，不过要求使用注解的类必须在`base-package`包或其子包下，如`leap.example.webbean.bean.ServiceBean3`。