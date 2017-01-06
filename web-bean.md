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