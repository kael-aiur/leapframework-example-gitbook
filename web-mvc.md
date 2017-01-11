# web-mvc

这个工程基于web示例leap mvc的使用。

## HomeController和MvcController

这两个控制器示例了最基础的路由映射规则和视图映射规则，具体的规则可以将示例工程部署到tomcat中并启动，启动完成后查看路由表：

```
METHOD  PATH              ACTION                                DEFAULT VIEW
------  ---------------   -----------------------------------   ------------------------------
*       /                 HomeController.index                  /index
*       /fav              FunctionAndVariableController.index   /fav/index
*       /mvc              MvcController.index                   /mvc/index
*       /path             HomeController.path                   /path
*       /index            HomeController.index                  /index
GET     /mvc/get          MvcController.get                     /mvc/get
*       /specify          MvcController.specifyPath             /specify
POST    /mvc/post         MvcController.post                    /mvc/post
*       /new_path         HomeController.newPath                /new_path
*       /redirect         HomeController.redirect               /redirect
*       /fav/index        FunctionAndVariableController.index   /fav/index
*       /mvc/index        MvcController.index                   /mvc/index
DELETE  /mvc/delete       MvcController.delete                  /mvc/delete
*       /file/upload      FileController.upload                 /file/upload
*       /mvc/new_path     MvcController.newPath                 /mvc/new_path
*       /specify_path     HomeController.specifyPath            /specify_path
*       /file/download1   FileController.download1              /file/download1
*       /file/download2   FileController.download2              /file/download2
```

另外，在`HomeController.redirect(Response response)`中示例了多种重定向的方式：

```java
response.sendRedirect("/");
Results.redirect("/");
return "redirect:/";
```

## FileController

文件上传下载示例，按照servlet 3.0的标准使用文件上传，只需要定义`leap.web.multipart.MultipartFile`类型的参数即可。

如：

```java
public String upload(MultipartFile file)
```

可以查看`/WEB-INF/views/file/index.html`，示例了html页面如何上传文件。

文件下载，有两种方式，一种是定义返回值为`leap.web.download.FileDownload`类型，如：

```java
public FileDownload download1()
```

另一种是返回字符串用leap默认的下载前缀并指定路径：

```java
public String download2() {
    return "download:classpath:/download.txt";
}
```
## FunctionAndVariableController

这个控制器示例了如何使用leap的环境变量和全局静态方法。

### 环境变量

环境变量实际上是一个bean，在`beans.xml`中，有如下配置：

```xml
<bean name="var" type="leap.core.variable.Variable" class="leap.example.mvc.variable.EnvVariable"/>
```

所有定义`type="leap.core.variable.Variable"`的bean都会被leap当成环境变量，环境变量的名字就是bean的名字，使用的时候需要加`env.`前缀，在`WEB-INF/views/fav/index.html`中可以看到环境变量的使用示例：

```html
env.var:${env.var}
```

> 环境变量可以在leap中的任何地方使用，比如sql中做为全局参数，或者视图中，或者其他注解中。

### 静态方法

静态方法可以配置一个静态的方法，在htpl模板中调用，可以不必为每个视图设置bean对象。在`config.xml`中有如下配置：

```xml
<el:functions prefix="fc" class="leap.example.mvc.function.Function">
    <el:function method="function(java.lang.String)"/>
</el:functions>
```

在`WEB-INF/views/fav/index.html`中可以看到使用示例：

```html
function("/url"):${fc:function('/url')}
<br/>
function(""):${fc:function('')}
<br/>
```

> 静态方法目前只能在htpl视图中使用。