# web-filter-interceptor

这个工程示例的是在web下如何使用leap提供的过滤器和拦截器。

在`leap.example.web.interceptor`这个包下有五个拦截器：

```java
leap.example.web.interceptor.ActionInterceptor
leap.example.web.interceptor.AnnotationInterceptor
leap.example.web.interceptor.BeanActionInterceptor
leap.example.web.interceptor.BeanRequestInterceptor
leap.example.web.interceptor.RequestInterceptor
```

其中：

```java
leap.example.web.interceptor.BeanActionInterceptor
leap.example.web.interceptor.BeanRequestInterceptor
```

配置成bean。

```java
leap.example.web.interceptor.ActionInterceptor
leap.example.web.interceptor.RequestInterceptor
```

在`Global`中：

```java
interceptors().add(new RequestInterceptor());
interceptors().add(new ActionInterceptor());
```

通过代码加入。

```java
leap.example.web.interceptor.AnnotationInterceptor
```

在`leap.example.web.controller.InterceptorController`使用注解：

```java
@InterceptedBy(AnnotationInterceptor.class)
```

加入。

> Interceptor有三种加入方式：
> * 通过配置bean对象
> * 通过主动new对象
> * 通过注解



