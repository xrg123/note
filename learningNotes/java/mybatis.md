# 基本概念

### 1、Mybatis

开源的持久层框架,MyBatis底层仍然是jdbc

平时我们都用JDBC访问数据库，除了需要自己写SQL之外，还必须操作Connection, Statement, ResultSet 这些其实只是手段的辅助类。 不仅如此，访问不同的表，还会写很多雷同的代码，显得繁琐和枯燥。那么用了Mybatis之后，只需要自己提供SQL语句，其他的工作，诸如建立连接，Statement， JDBC相关异常处理等等都交给Mybatis去做了，那些重复性的工作Mybatis也给做掉了，我们只需要关注在增删改查等操作层面上，而把技术细节都封装在了我们看不见的地方。

### 2、使用步骤

*导包

	<dependency>
	  <groupId>org.mybatis</groupId>
	    <artifactId>mybatis</artifactId>
	    <version>3.2.8</version>
	</dependency>
	
	<dependency>
		<groupId>com.jslsolucoes</groupId>
		<artifactId>ojdbc6</artifactId>
		<version>11.2.0.1.0</version>
	</dependency>
*配置

<?xml version="1.0" encoding="UTF-8" ?>  
<!DOCTYPE configuration PUBLIC "-//ibatis.apache.org//DTD Config 3.0//EN" 

	"http://ibatis.apache.org/dtd/ibatis-3-config.dtd">
<configuration>
	<environments default="environment">
		<environment id="environment">
			<transactionManager type="JDBC" />
			<dataSource type="POOLED">
				<property name="driver" value="oracle.jdbc.driver.OracleDriver" />
				<property name="url" value="jdbc:oracle:thin:@localhost:1521:xe" />
				<property name="username" value="system" />
				<property name="password" value="oracle" />
			</dataSource>
		</environment>
	</environments>
	<!--指定映射文件的位置 -->
	<mappers>
		<mapper resource="entity/EmpMapper.xml" />
	</mappers>
</configuration> 

*映射文件

<?xml version="1.0" encoding="UTF-8" ?>  
<!DOCTYPE mapper PUBLIC "-//ibatis.apache.org//DTD Mapper 3.0//EN"      
 "http://ibatis.apache.org/dtd/ibatis-3-mapper.dtd">

<mapper namespace="dao.EmployeeDAO">
<!-- id：要求唯一,parameterType:参数类型，填写实体类的完整名字一 -->
	<insert id="save" parameterType="entity.Employee">
		insert into t_emp values(t_emp_seq.nextval,#{name},#{age})
	</insert>
	
	<select id="findAll" resultType="entity.Employee">
		select * from t_emp
	</select>
	
	<update id="modify" parameterType="entity.Employee">
		update t_emp set name=#{name},age=#{age} where id=#{id}
	</update>
	
	<!-- 返回Map类型的结果
		map是java.util.Map的简写形式
		1)mybatis会将记录中的数据先放到一个Map对象里面（以字段名作为key,以字段值作为value,一条记录对应一个Map对象
		然后再将Map中的数据放到对应的实体对象里面）
		2）返回Map类型的结果，好处是不用实体类了，但不方便（因为要获得字段值，还需要调用Map对象提供的get方法） -->
		<select id="findById2" parameterType="int" resultType="map">
			SELECT * FROM  t_emp  where id=#{id1}
		</select>
	
	<!-- 使用resultMap解决表的字段名与实体类的属性名不一致的情况 -->
		<resultMap type="entity.Emp" id="empResultMap">
			<result property="empNo" column="id"/>
		</resultMap>
		<select id="findById3" parameterType="int" resultMap="empResultMap">
			select * from t_emp where id=#{id}
			<!-- select id as empNo,name,age from t_emp where id=#{id}  -->
		</select>
		
</mapper>

具体要求

a.方法名要与sql的id一致

b.方法的参数类型要与parameterType一致

c.方法的返回类型要与resultType一致

d.映射文件的namespace要等于接口的完整的名字

![](<https://github.com/xrg123/note/blob/master/image/mybatis.png>)

### 3、spring集成Mybatis

*导包

    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-webmvc</artifactId>
      <version>4.2.2.RELEASE</version>
    </dependency>
    
    <dependency>
      <groupId>org.mybatis</groupId>
      <artifactId>mybatis</artifactId>
      <version>3.2.8</version>
    </dependency>
    
    <dependency>	
      <groupId>org.mybatis</groupId>
      <artifactId>mybatis-spring</artifactId>
      <version>1.2.3</version>
    </dependency>
    
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-jdbc</artifactId>
      <version>5.0.0.RELEASE</version>	
    </dependency>
    
    <dependency>
      <groupId>com.jslsolucoes</groupId>
      <artifactId>ojdbc6</artifactId>
      <version>11.2.0.1.0</version>
    </dependency>
    
    <dependency>
      <groupId>commons-dbcp</groupId>
      <artifactId>commons-dbcp</artifactId>
      <version>1.4</version>
    </dependency>
    
  *配置文件

方式一：使用mapper映射器

1）集成步骤

step1:导包

spring-webmvc,mybatis,mybatis-spring,

dbcp,ojdcp,spring-jdbc

2)添加spring配置文件

注：不需要Mybatis的配置文件，可以在spring配置文件里面添加SqlSessionFactoryBean来代替

3）写实体类

4）映射文件

5）Mapper映射器

6）配置MapperScannerConfigurer

注：该bean会扫描指定包及其子包下面所有的Mapper映射器（即接口）

然后调用getMapper方法获得映射器的实现（比如，调用

EmployeeDAO dao=SqlSession.getMapper(EmployeeDAO.class)

并且将这些对象添加导Spring容器里面

<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans" 

	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xmlns:context="http://www.springframework.org/schema/context" 
	xmlns:jdbc="http://www.springframework.org/schema/jdbc"  
	xmlns:jee="http://www.springframework.org/schema/jee" 
	xmlns:tx="http://www.springframework.org/schema/tx"
	xmlns:aop="http://www.springframework.org/schema/aop" 
	xmlns:mvc="http://www.springframework.org/schema/mvc"
	xmlns:util="http://www.springframework.org/schema/util"
	xmlns:jpa="http://www.springframework.org/schema/data/jpa"
	xsi:schemaLocation="
		http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-3.2.xsd
		http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context-3.2.xsd
		http://www.springframework.org/schema/jdbc http://www.springframework.org/schema/jdbc/spring-jdbc-3.2.xsd
		http://www.springframework.org/schema/jee http://www.springframework.org/schema/jee/spring-jee-3.2.xsd
		http://www.springframework.org/schema/tx http://www.springframework.org/schema/tx/spring-tx-3.2.xsd
		http://www.springframework.org/schema/data/jpa http://www.springframework.org/schema/data/jpa/spring-jpa-1.3.xsd
		http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop-3.2.xsd
		http://www.springframework.org/schema/mvc http://www.springframework.org/schema/mvc/spring-mvc-3.2.xsd
		http://www.springframework.org/schema/util http://www.springframework.org/schema/util/spring-util-3.2.xsd">
	
	<!-- 读取db.propertise文件 -->
	<util:properties id="db" location="classpath:db.properties"></util:properties>
	
	<!-- 配置连接池 -->
	<bean id="ds" class="org.apache.commons.dbcp.BasicDataSource" destroy-method="close">
		<property name="driverClassName" value="#{db.driver}"/>
		<property name="url" value="#{db.url}"/>
		<property name="username" value="#{db.user}"/>
		<property name="password" value="#{db.pwd}"/>
	</bean>
	
	<!-- 配置mybatis -->
	<!-- 配置SqlSessionFactoryBean -->
	<bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
		<!-- 指定连接资源 -->
		<property name="dataSource" ref="ds"/>
		<!-- 指定映射文件 -->
		<property name="mapperLocations" value="classpath:entity/*.xml"/>
	</bean>
	
	<!-- 配置MapperScannerConfigurer 
	将Mapper映射器实例化，并注入spring容器中
	相当于EmpDao dao=SqlSession.getMapper(EmpDao.class)-->
	<bean class="org.mybatis.spring.mapper.MapperScannerConfigurer">
		<!-- 注入映射器所在的包名  可以写多个包，用逗号隔开-->
		<property name="basePackage" value="dao,abc"></property>
		<!-- 只扫描带有特定注解的接口 -->
		<property name="annotationClass" value="annotations.MyBatisRepository"></property>
	</bean>

</beans>



方式二：

1）集成步骤

step1:导包

spring-webmvc,mybatis,mybatis-spring,

dbcp,ojdcp,spring-jdbc

2)添加spring配置文件

注：不需要Mybatis的配置文件，可以在spring配置文件里面添加SqlSessionFactoryBean来代替

3）写实体类

4）映射文件

注：namespace不再要求等接口名

5）DAO接口

注：接口方法没有特定要求

6）DAO接口的实现

注：可以注入SqlSessionTemplate

<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans" 

	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xmlns:context="http://www.springframework.org/schema/context" 
	xmlns:jdbc="http://www.springframework.org/schema/jdbc"  
	xmlns:jee="http://www.springframework.org/schema/jee" 
	xmlns:tx="http://www.springframework.org/schema/tx"
	xmlns:aop="http://www.springframework.org/schema/aop" 
	xmlns:mvc="http://www.springframework.org/schema/mvc"
	xmlns:util="http://www.springframework.org/schema/util"
	xmlns:jpa="http://www.springframework.org/schema/data/jpa"
	xsi:schemaLocation="
		http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-3.2.xsd
		http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context-3.2.xsd
		http://www.springframework.org/schema/jdbc http://www.springframework.org/schema/jdbc/spring-jdbc-3.2.xsd
		http://www.springframework.org/schema/jee http://www.springframework.org/schema/jee/spring-jee-3.2.xsd
		http://www.springframework.org/schema/tx http://www.springframework.org/schema/tx/spring-tx-3.2.xsd
		http://www.springframework.org/schema/data/jpa http://www.springframework.org/schema/data/jpa/spring-jpa-1.3.xsd
		http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop-3.2.xsd
		http://www.springframework.org/schema/mvc http://www.springframework.org/schema/mvc/spring-mvc-3.2.xsd
		http://www.springframework.org/schema/util http://www.springframework.org/schema/util/spring-util-3.2.xsd">
	
	<!-- 读取db.propertise文件 -->
	<util:properties id="db" location="classpath:db.properties"></util:properties>
	
	<!-- 配置连接池 -->
	<bean id="ds" class="org.apache.commons.dbcp.BasicDataSource" destroy-method="close">
		<property name="driverClassName" value="#{db.driver}"/>
		<property name="url" value="#{db.url}"/>
		<property name="username" value="#{db.user}"/>
		<property name="password" value="#{db.pwd}"/>
	</bean>
	
	<!-- 配置mybatis -->
	<!-- 配置SqlSessionFactoryBean -->
	<bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
		<!-- 指定连接资源 -->
		<property name="dataSource" ref="ds"/>
		<!-- 指定映射文件 -->
		<property name="mapperLocations" value="classpath:entity/*.xml"/>
	</bean>
	
	<!-- 配置SqlSessionTemplate -->
	<bean id="sst" class="org.mybatis.spring.SqlSessionTemplate">
		<constructor-arg index="0" ref="sqlSessionFactory"/>
	</bean>
	
	<!-- 配置组件扫描 -->
	<context:component-scan base-package="dao"></context:component-scan>


</beans>