# web-listener

这个工程基于web示例，在整个leap webapp启动的过程的扩展点。

在`leap.example.weblistener.Global`中，提供了如下几个事件：

```java
configure
init
start
stop
```

这几个事件是应用的基本事件，应用可以在这几个事件内做绝大部分相应的处理，某些情况下，我们可以不能修改Global的代码(比如做应用扩展包)，这种情况下leap提供了应用监听器`leap.web.AppListener`，实现这个接口并将实现类配置为bean即可，如`leap.example.weblistener.listener.WebAppListener`。

这里提供了如下事件：

```java
preAppConfigure
postAppConfigure
preAppInit
postAppInit
preAppStart
postAppStart
preAppStop
postAppStop
```

总体来说，上述事件在应用整个启动过程执行顺序如下：

```
preAppConfigure -> configure -> postAppConfigure -> preAppInit -> init -> postAppInit -> 
preAppStart -> start -> postAppStart。
```

当应用关闭时，执行的事件顺序如下：

```
preAppStop -> stop -> postAppStop
```