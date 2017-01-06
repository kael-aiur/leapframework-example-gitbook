# web-datasource

这个示例工程在web的基础上增加了数据源的配置使用示例。

数据源的本质就是一个bean，在示例工程的`conf/beans.xml`中，配置了4个数据源。

使用的是leap内置的连接池`leap.db.cp.PooledDataSource`。

leap可以非常方便的支持多数据源，这里四个数据源分别为`default`，`datasource1`，`datasource2`，`datasource3`。

