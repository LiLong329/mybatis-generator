<p align="center">
  <a href="#"><img src="https://img.shields.io/badge/devTool-Eclipse%7CIDEA-yellow.svg" alt=""></a>
  <a href="#"><img src="https://travis-ci.org/Alamofire/Alamofire.svg?branch=master" alt=""></a>
  <a href="#"><img src="https://img.shields.io/packagist/l/doctrine/orm.svg" alt="LICENSE"></a>
  <a href="#"><img src="https://img.shields.io/badge/platform-OSX%7CWin%7CLinux-blue.svg" alt=""></a>
  <a href="#"><img src="https://badges.frapsoft.com/os/v1/open-source.svg?v=103" alt=""></a>   	
  <a href="#"><img src="https://img.shields.io/badge/language-java-blue.svg" alt=""></a>  
</p>

# 简介
该项目可以生成mybatis所需要的pojo、Mapper接口、xxxMapper.xml
# 如何使用

1. 将该项目导入到eclipse或者IDEA中

2. 编辑`generatorConfig.xml`，修改数据库连接信息

```
<jdbcConnection 
  driverClass="com.mysql.jdbc.Driver"
	connectionURL="jdbc:mysql://localhost:3306/test" 
	userId="root"
	password="root">
</jdbcConnection>
```
3. 修改pojo、xxxMapper.xml、Mapper接口的生成路径

```
<!-- targetProject:生成Entity类的路径 -->
<javaModelGenerator targetProject=".\src" targetPackage="com.leeyom.orm.pojo">
  <!-- enableSubPackages:是否让schema作为包的后缀 -->
  <property name="enableSubPackages" value="false" />
  <!-- 从数据库返回的值被清理前后的空格 -->
  <property name="trimStrings" value="true" />
</javaModelGenerator>
		
<!-- targetProject:XXXMapper.xml映射文件生成的路径 -->
<sqlMapGenerator targetProject=".\src" targetPackage="com.leeyom.orm.mapper">
  <!-- enableSubPackages:是否让schema作为包的后缀 -->
  <property name="enableSubPackages" value="false" />
</sqlMapGenerator>
		
<!-- targetPackage：Mapper接口生成的位置 -->
<javaClientGenerator type="XMLMAPPER" targetProject=".\src" targetPackage="com.leeyom.orm.mapper">
  <!-- enableSubPackages:是否让schema作为包的后缀 -->
  <property name="enableSubPackages" value="false" />
</javaClientGenerator>
```
4. 指定数据库表名以及我们要生成的pojo的实体类名

```
<table tableName="user" domainObjectName="User"/>
```

如果需要insert的时候返回主键，需要如下配置：
```xml
<!-- insert插入时返回数据库自增长主键id -->    
<table tableName="case" domainObjectName="Case">  
	<generatedKey column="case_id" sqlStatement="MySql" identity="true" />  
</table> 
```
5. 执行`MybatisGenerator.java`，刷新src目录，就可以看见生成的文件，将这些文件拷贝到你的项目中即可

# 注意
* 对于数据库中的表字段，尽量采用下划线分隔的形式，比如"user_name"，这样生成的pojo的属性才符合标准的驼峰命名法。
* 如果是mac或者linux环境下，需要将`targetProject=".\src"`中的"\\"换成"/"即可，否则无法生成对应的文件。

# 推荐项目

最近发现一个更加好的mybatis generator项目：[mybatis-generator-gui](https://github.com/zouzg/mybatis-generator-gui)，带有图形化界面，非常方便！
