# 说明
本 repository 是最初学习Java开发时候做的一个例子，后续慢慢维护，希望成为最简单、最全的入门例子，麻雀虽小，五脏俱全
使用到的技术如下：

- maven 项目管理
- spring mvc 框架
- mybatis 持久层框架，例子中包括MySQL、SqlServer的连接案例，包含取多条（list)转换、where条件的in案例等[动态sql例子](https://mybatis.github.io/mybatis-3/zh/dynamic-sql.html)，详细可以阅读[mybaits动态sql语句学习](http://limingnihao.iteye.com/blog/782190)
- freemarker 模板框架

其它：
- [semantic ui前端框架](http://www.semantic-ui.com/)，负责整体的css、布局、交互等；

# 使用方法
1. fork 代码
2. 使用工具 idea 或者 eclipe 导入 现有maven项目，maven会自动下载所以来的jar包；
3. 将 `doc` 文件夹中的sql脚本部署到MySQL中，取的MySQL连接串，修改 `jdbc.properties` 中MySQL节点的url、user、password
4. 调试代码，即可在页面中看到效果
![doc/readme.png](doc/readme.png)



#xiongying
#date：2017.2.10
从Git上clone代码到本地，然后作为Maven工程导入到Myeclipse中时遇到了以下问题：

1.Maven编译报错，找不到sqljdbc4-4.0.jar文件
解决：手动下载该sqljdbc4-4.0.jar文件，使用maven进行安装，具体参考：http://outofmemory.cn/code-snippet/10750/sqljdbc-add-to-maven

2.修改spring-servlet-context.xml中有关数据库连接的配置
<beans:bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
        <beans:property name="configLocation" value="classpath:/config/spring-mybatis-config.xml" />
        <beans:property name="dataSource" ref="dataSourceAll" />
</beans:bean>
将ref="dataSourceAll"修改为ref="mysqlTestSource"

3.源代码中注释了获取userList值，导致程序启动后访问首页报错userList为null
解决：HomeController.java中将 
ArrayList<User> users=service.getAllUsers();
mv.addObject("userList",users);
注释去掉即可。
