# web-datasource

这个示例工程在web的基础上增加了数据源的配置使用示例。

数据源的本质就是一个bean，在示例工程的`conf/beans.xml`中，配置了4个数据源。

使用的是leap内置的连接池`leap.db.cp.PooledDataSource`。

leap可以非常方便的支持多数据源，这里四个数据源分别为`default`，`datasource1`，`datasource2`，`datasource3`。

这里用`primary="true"`表示`default`数据源是主要数据源，如果Model没有指定数据源的话，默认会使用这个数据源。

整个示例工程一共有四个Model:

```java
leap.example.datasource.model.Datasource1Model
leap.example.datasource.model.Datasource2Model
leap.example.datasource.model.datasource3.Datasource3Model
leap.example.datasource.model.DatasourceDefaultModel
```

这里，`leap.example.datasource.model.Datasource2Model`通过`@DataSource("datasource2")`注解指定为数据源`datasource2`。

`leap.example.datasource.model.DatasourceDefaultModel`没有指定数据源，会使用默认的`default`数据源。

而`leap.example.datasource.model.datasource3.Datasource3Model`通过`config.xml`的配置指定为数据源`datasource3`:

```xml
<orm:models datasource="datasource3">
    <orm:package name="leap.example.datasource.model.datasource3"/>
</orm:models>
```

这里的配置是值所有在包`leap.example.datasource.model.datasource3`下的类都使用`datasource3`作为数据源。

