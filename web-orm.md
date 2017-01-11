# web-orm

这个工程基于web示例leap orm的使用。

在`leap.example.orm.controller.HomeController`中示例了orm的基本使用方法。

## 多租户支持

另外leap orm提供了一个多租户的数据隔离的功能。

在`models.xml`中，可以看到如下配置：

```xml
<global-field name="tenantId" column="tenant_id" jdbc-type="varchar" length="100"
                  nullable="false" 
                  insert="true" update="false" where="true" 
                  where-if="${true}" insert-value="${'m1_1'}" where-value="${env.tenant}">

                  <included-entities>MultiTenantModel1, MultiTenantModel2</included-entities>

</global-field>
```

这里配置了一个全局属性，并且指定了`MultiTenantModel1, MultiTenantModel2`给这两个类使用。

在`leap.example.orm.controller.HomeController.multiTenant()`中示例了如何使用。

把示例工程部署到tomcat，启动应用并访问`/web-orm/multi_tenant`，可以看到控制台输出：

```
SQL  : insert into multi_tenant_model1(id,name,tenant_id) values (?,?,?)
ARGS : ['m1a','m1a','m1_1']
SQL  : insert into multi_tenant_model1(id,name,tenant_id) values (?,?,?)
ARGS : ['m1b','m1b','m1_2']
SQL  : select t.* from multi_tenant_model1 t where 1=1  and t.tenant_id = ? 
ARGS : ['m1_1']
```

这里会在查询的过程自动增加`tenantId`字段的过滤条件。这样我们就可以方便的实现多租户之间的数据隔离了，而在查询代码方面可以不做任何改动。

## 动态sql使用

在`sqls.xml`中可以看到配置sql的基本方法，leap orm支持使用动态sql，可以使用动态表达式或者指令方式配置sql.

并且支持配置公用的sql片段并用`@include`指令来引入：

```xml
<command key="dynamic.sql3">
    select * from t_model1 where 1=1 @include(dynamic.fragment)
</command>

<fragment key="dynamic.fragment">
    AND name = :name
</fragment>
```