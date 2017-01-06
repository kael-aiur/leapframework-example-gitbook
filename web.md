# web

这是最简单的web工程，依赖配置从父工程继承过来，父工程的pom.xml配置如下：

```xml
<repositories>
    <!-- leap快照资源库 -->
    <repository>
        <id>leap-snapshots</id>
        <url>https://raw.githubusercontent.com/leapframework/repo/master/snapshots</url>
        <snapshots>
            <enabled>true</enabled>
            <updatePolicy>always</updatePolicy>
            <checksumPolicy>warn</checksumPolicy>
        </snapshots>
    </repository>

    <repository>
        <id>leap-releases</id>
        <url>https://raw.githubusercontent.com/leapframework/repo/master/releases</url>
        <releases>
            <enabled>true</enabled>
            <updatePolicy>never</updatePolicy>
            <checksumPolicy>warn</checksumPolicy>
        </releases>
    </repository>
</repositories>

<properties>
    <leap.version>0.4.0b-SNAPSHOT</leap.version>
    <slf4j.version>1.7.5</slf4j.version>
    <logback.version>1.0.13</logback.version>
    <h2.version>1.3.172</h2.version>
</properties>

<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <configuration>
                <source>1.8</source>
                <target>1.8</target>
                <encoding>UTF-8</encoding>
            </configuration>
        </plugin>
    </plugins>
</build>
<dependencies>
    <!-- leap框架依赖，必须 -->
    <dependency>
        <groupId>org.leapframework</groupId>
        <artifactId>leap</artifactId>
        <version>${leap.version}</version>
        <type>pom</type>
    </dependency>

    <!-- 依赖日志框架，非必须 -->
    <dependency>
        <groupId>org.slf4j</groupId>
        <artifactId>slf4j-api</artifactId>
        <version>${slf4j.version}</version>
        <type>jar</type>
        <scope>runtime</scope>
    </dependency>
    <dependency>
        <groupId>org.slf4j</groupId>
        <artifactId>jcl-over-slf4j</artifactId>
        <version>${slf4j.version}</version>
        <type>jar</type>
        <scope>runtime</scope>
    </dependency>
    <dependency>
        <groupId>ch.qos.logback</groupId>
        <artifactId>logback-classic</artifactId>
        <version>${logback.version}</version>
        <type>jar</type>
        <scope>runtime</scope>
    </dependency>
    
    <!-- 依赖 servlet 3.0标准api，非必须 -->
    <dependency>
        <groupId>javax.servlet</groupId>
        <artifactId>javax.servlet-api</artifactId>
        <version>3.1.0</version>
    </dependency>
        
    <!-- 依赖数据库连接驱动，以h2为例，可以换成其他任何数据库驱动，不使用数据库的情况下非必需 -->
    <dependency>
        <groupId>com.h2database</groupId>
        <artifactId>h2</artifactId>
        <version>${h2.version}</version>
    </dependency>
</dependencies>
```

在`conf/config.xml`中配置了：

```xml
<base-package>leap.example.web</base-package>
```

表示leap扫描的包。

这个示例中集成了`logback`日志框架，`logback.xml`是日志配置。

`webapp/WEB-INF/web.xml`中配置了leap的拦截器：

```xml
<filter>
	<filter-name>app-filter</filter-name>
    <filter-class>leap.web.AppFilter</filter-class>
</filter>

<filter-mapping>
    <filter-name>app-filter</filter-name>
    <url-pattern>/*</url-pattern>
</filter-mapping>	
```

这就是leap的web工程最基础的配置，有了这些配置leap就可以使用了。

`leap.example.web.Global`类是应用的启动类，类名是leap默认且固定的，并且只能在配置的`base-package`下，不能是子包。

`leap.example.web.controller.HomeController`是示例的控制器，把这个应用部署到tomcat下并访问应用根路径即可看到：

```
hello leap!
```