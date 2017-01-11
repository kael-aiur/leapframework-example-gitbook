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
## 
