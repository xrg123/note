

# Spring(<https://spring.io/>)

spring管理的对象成为Beans，spring支持xml和注解两种配置方式

## 基本知识点

### 1、依赖注入、控制反转

	IOC(控制反转Inversion of Control)     对象之间的依赖关系由容器来建立
	DI（依赖注入Dependency Injection)      容器调用set方法或者构造器来建立依赖关系

依赖注入、控制反转作用：A、B两个组件（类），A依赖于B, A要想使用B,必须先获得B的实例引用，若B是一个具体的类，可以通过new关键字创建组件B， 若B是一个接口，且有多个实现，A选择任意B的实现类，则重用性会大大降低。依赖注入、控制反转这样解决此类问题，让框架接管对象的创建工作，并将该对象的引用注入到需要该对象的组件中。

```java
public class A {
  public void method() {
    B b = new B();
    b.test();
  }
}
```

可用set方法或构造器方法进行注入

```java
public class A {
  private B b;
  
  public void setB(B b) {
    this.b = b;
  }
  
  public void method() {
    B b = new B();
    b.test();
  }
}
```

```java
public class A {
  private B b;
  
  public A(B b) {
    this.b = b;
  }
  
  public void method() {
    B b = new B();
    b.test();
  }
}
```

spring中在配置文件中完成注入

<!-- IOC/DI

	set 方法     <property name="b" ref="b1"/>
	构造器             <constructor-arg index="" ref=""/>
	自动装配   autowire:  byName(尽量用这个，id唯一，不会出错)   byType-->
	
	<!-- 
		set方式注入
		1.添加构造器    2.在配置文件中，使用<property>元素来配置
	 -->
	<bean id="b1" class="ioc.B"/>
	<bean id="c1" class="ioc.C"/>
	<!-- 
		property:让容器调用set方法来注入依赖关系，其中，name属性指定属性名，
		ref指定被注入的bean的id
	 -->
	<bean id="a1" class="ioc.A">
		<property name="b" ref="c1"></property>
	</bean>
	
	<!-- 构造器注入 
		1.添加构造器   2.在配置文件中使用<constructor-arg>元素来配置-->
	<!-- constructor-arg:容器会采用构造器来建立依赖关系，其中，index指定参数的下标 -->
	<bean id="cp1" class="ioc.Computer"/>
	<bean id="mg1" class="ioc.Manager">
		<constructor-arg index="0" ref="cp1"/>
	</bean>
	
	<bean id="foo" class="autowire.Foo"/>
		<!-- autowire：表示让容器自动建立对象之间的依赖关系
		byName:依据属性名建立容器之间的依赖关系，会将属性名作为Id来查找 -->
	<bean id="bar" class="autowire.Bar" autowire="byName"/>
注入基本类型数据：

```
<!-- 注入基本类型的值 
	使用value属性来注入，spring容器会帮我们做一些类型的转换工作，比如将字符串转换为数字-->
	<!-- 注入集合类型的值
	方式一：直接注入
	方式二：引用的方式注入
	step1:将集合类型的值先配置成一个bean
	step2:再将这个bean注入到对应的bean里面 -->
	<bean id="vb1" class="value.ValueBean">
		<property name="name" value="shiyan"/>
		<property name="age" value="18"/>
		<property name="interest">
			<list>
				<value>电影</value>
				<value>美食</value>
				<value>运动</value>
			</list>
		</property>
		<property name="city">
			<set>
				<value>北京</value>
				<value>上海</value>
				<value>武汉</value>
				<value>武汉</value>
			</set>
		</property>
		<property name="score">
			<map>
				<entry key="english" value="70"></entry>
				<entry key="math" value="90"/>
				<entry key="yuwen" value="87"></entry>
			</map>
		</property>
		<property name="db">
			<props>
				<prop key="username">sally</prop>
				<prop key="password">1234</prop>
			</props>
		</property>
	</bean>
	
	<!-- <bean id="vb1" class="value.ValueBean">
		<constructor-arg index="0" value="shiyan"></constructor-arg>
		<constructor-arg index="1" value="19"/>
	</bean> -->
	
	<!-- 将集合类型的值配置成一个bean -->
	<!-- util:list 表示使用的时util命名空间下的list元素。
	命名空间：为了区分同名的元素而添加的前缀 -->
	<util:list id="interestBean">
		<value>唱歌</value>
		<value>跳舞</value>
		<value>看电影</value>
	</util:list>
	<util:set id="cityBean">
		<value>北京</value>
		<value>上海</value>
		<value>天津</value>
	</util:set>
	<util:map id="scoreBean">
		<entry key="english" value="80"></entry>
		<entry key="math" value="90"/>
	</util:map>
	<util:properties id="dbBean">
		<prop key="username">xiaoming</prop>
		<prop key="password">text</prop>
	</util:properties>
	<!-- 采用引用的方式注入集合类型的值 -->
	<bean id="eb1" class="value.ExampleBean">
		<property name="interest" ref="interestBean"></property>
		<property name="city" ref="cityBean"></property>
		<property name="score" ref="scoreBean"/>
		<property name="db" ref="dbBean"/>
	</bean>
	
	<!-- 读取.properties文件的内容 -->
	<!-- location:指定属性文件的位置(classpath:表示让容器依据类路径
	查找属性文件).容器会读取指定位置文件的内容，并且将这些内容存放到properties
	对象里面 -->
	<util:properties id="config" location="classpath:config.properties"></util:properties>
	
	<!-- 使用spring表达式读取其他的bean的属性 -->
	<bean id="ib1" class="value.InfoBean">
		<property name="name" value="#{vb1.name}"></property>
		<property name="interest" value="#{vb1.interest[1]}"/>
		<property name="score" value="#{vb1.score['english']}"/><!-- 也可vb1.score.english -->
		<property name="pageSize" value="#{config.pageSize}"/>
	</bean>
```

## spring操作

### 1、获得beans

导入springmvc模块，spring中包含二十多个模块

 <dependency>

	    <groupId>org.springframework</groupId>
	    <artifactId>spring-webmvc</artifactId>
	    <version>3.2.8.RELEASE</version>
	    <type>pom</type>
	 </dependency>
配置前端控制器

<!-- DispatcherServlet前端控制器配置 -->
  <servlet>
  	<servlet-name>springmvc</servlet-name>
  	<servlet-class>
  		org.springframework.web.servlet.DispatcherServlet	
  	</servlet-class>
  	<!-- DispatcherServlet的初始化方法会启动spring容器，
  	contextConfigLocation用来指定spring配置文件的位置 -->
  	<init-param>
  		<param-name>contextConfigLocation</param-name>
  		<param-value>classpath:spring-mvclab.xml</param-value>
  	</init-param>
  	<load-on-startup>1</load-on-startup>
  </servlet>
  <servlet-mapping>
  	<servlet-name>springmvc</servlet-name>
  	<url-pattern>*.do</url-pattern>
  </servlet-mapping>
</web-app>



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
		http://www.springframework.o rg/schema/jee http://www.springframework.org/schema/jee/spring-jee-3.2.xsd
		http://www.springframework.org/schema/tx http://www.springframework.org/schema/tx/spring-tx-3.2.xsd
		http://www.springframework.org/schema/data/jpa http://www.springframework.org/schema/data/jpa/spring-jpa-1.3.xsd
		http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop-3.2.xsd
		http://www.springframework.org/schema/mvc http://www.springframework.org/schema/mvc/spring-mvc-3.2.xsd
		http://www.springframework.org/schema/util http://www.springframework.org/schema/util/spring-util-3.2.xsd">
	
	<!-- 利用无参构造器创建对象 -->
	<!-- 
		id:bean的名字，要求唯一
		class:完整的类名（包括包名）
	 -->
	<bean id="stu1" class="first.Student"></bean>
	<bean id="date1" class="java.util.Date"></bean>
	
	<!-- 使用静态工厂方法创建对象 -->
	<!-- 
	factory-menthod:指定一个静态方法
	容器会调用该类的静态方法来创建一个对象
	 -->
	<bean id="cal1" class="java.util.Calendar" factory-method="getInstance"/>
	
	<!-- 使用实例工厂方法创建对象 -->
	<!-- 
		factory-bean:制定一个bean的id,容器会调用bean的实例方法来创建一个对象
	 -->
	<bean id="time1" factory-bean="cal1" factory-method="getTime"/>

</beans>

一些配置

<!-- 指定作用域 -->

	<!-- 
		scope:用来指定作用域，缺省值是singleton（单例，即只会创建一个对象）
		如果值是prototype，每调用一次getBean方法，就会创建一个新的对象。
		lazy-init:如果值为true,表示延迟加载
	 -->
	<bean id="t1" class="basic.Teacher" scope="singleton" lazy-init="true"></bean>
	
	<!-- 指定初始化方法 -->
	<!-- 
		init-method:指定初始化方法名
		destroy-method:指定销毁方法名
		注意：销毁方法只对作用域为singleton的bean有效
	 -->
	<bean id="ms1" class="basic.MessageService" init-method="init" destroy-method="destroy"/>

```java
String config="applicationContext.xml";
ApplicationContext ac=new ClassPathXmlApplicationContext(config);
/*
 * ApplicationContext是接口
 * ClassPathXmlApplicationContext是一个实现类，该类会依据路径去
 * 查找spring配置文件，然后启动容器，获得对象
 */
Student stu=ac.getBean("stu1",Student.class);
```

### 2、容器中bean元素的创建及注入

方法一：在配置文件中手动写入beans

方法二：配置组件扫描

<!-- 配置组件扫描 -->

	<!-- 容器会扫描指定的包及其子包下面的所有的类，若该类前面有特定的注解，比如（@Component),则
	容器会将其纳入容器进行管理（相当于在配置文件里面有一个bean元素） -->
	<!-- 如何进行组件扫描
	step1:在类前面添加特定的注解，比如@Component 注：默认的id是首字母小写之后的类名
	Step2:在配置文件当中，配置组件扫描 -->
	<context:component-scan base-package="ioc"></context:component-scan>
对bean的属性赋值

```java
@Component("user")
public class UserBean {
	@Value("李四")  //同样可以加在set方法前
	private String name;
	@Value("#{config.pageSize}")
	private String pageSize;
	
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	public String getPageSize() {
		return pageSize;
	}
	public void setPageSize(String pageSize) {
		this.pageSize = pageSize;
	}
	
	@Override
	public String toString() {
		return "UserBean [name=" + name + ", pageSize=" + pageSize + "]";
	}
	
	
}

```

其他配置通过注解来进行

```java
@Component("stu1")  //设置别名，不设置时，id默认为类名首字母小写
@Scope("singleton")  //作用域
@Lazy(true)   //延迟加载
public class Student {

	public Student() {
		System.out.println("student");
	}
	
	@PostConstruct   //初始化注解
	public void init(){
		System.out.println("init");
	}
	
	@PreDestroy   //销毁注解
	public void destroy(){
		System.out.println("destroy");
	}
}
```

通过注解注入依赖

```java
/*
 * 指定依赖注入关系
 * 具有依赖关系的Bean对象，利用下面任意一种注解都可以实现关系注入
 * @Autowired/@Qualifier   @Autowired默认通过Type注入，加入@Qualifier通过id注入
 * 可以处理构造器注入和Setter注入
 * @Inject/@Named（了解）
 * 和@Autowired用法一致,需要额外导包
 * @Resource(重点)
 * 只能处理Setter注入，但大部分情况下都是Setter注入
 * 
 * Setter注入推荐使用@Resource 
 * 构造器注入推荐使用@Autowired
 */
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Qualifier;
import org.springframework.stereotype.Component;

@Component("rest")
public class Restaurant {
	/*
	 * 这两个注释也可以直接添加到属性前，等价于加在set方法前
	 * 注：加载属性前，只是简单的赋值，相当于this.wt=wt;
	 * 注入Waiter对象，其id(bean唯一的名称）为"wt"
	 */
	@Autowired
	@Qualifier("wt")
	private Waiter wt;
	
	public Restaurant(){
		System.out.println("restaurant");
	}

	public Waiter getWt() {
		return wt;
	}
	
	/*@Autowired
	public void setWt(@Qualifier("wt") Waiter wt) {
		this.wt = wt;
	}*/

	@Override
	public String toString() {
		return "Restaurant [wt=" + wt + "]";
	}
	
	
}

```

```java
@Component("leader")
public class Leader {
	@Resource(name="wt")
	private Waiter wt;
	
	/*@Resource(name="wt") //name指被注入的bean的id
	public void setWt(Waiter wt) {
		System.out.println("set");
		this.wt = wt;
	}*/

	public Leader() {
		System.out.println("leader");
	}

	@Override
	public String toString() {
		return "Leader [wt=" + wt + "]";
	}
	
	
}
```

```java
@Component("bar")
public class Bar {
	private Waiter wt;
	
	public Bar() {
		System.out.println("bar");
	}
	
	@Autowired
	//默认byType注入，加入@qualifier通过id注入
	public Bar(@Qualifier("wt") Waiter wt){
		System.out.println("bar(wt)");
		this.wt=wt;
	}

	@Override
	public String toString() {
		return "Bar [wt=" + wt + "]";
	}
	
}
```

### 3、spring中的Bean的id和name的区别

每个bean可以有一个id属性，并且可以更具该id在Ioc容器中查找该Bean， 该id属性值必须在Ioc容器中唯一

如果不指定id属性，只指定name,那么name为Bean的标识符，并且需要在容器中唯一

同时指定id和name此时id作为标识符，而name作为bean的别名，两者都可以找到目标bean

可以指定多个name,中间可以用分号、空格或逗号隔开，如果没有指定id,那么第一个name为表示符，区域name为别名，若指定了id属性，则id为标识符

### 4、springJDBC

spring框架对jdbc的封装

2）编程步骤

step1:导包

spring-mvc,spring-jdbc,ojdbc,dbcp,junit,annotation

step2:添加spring配置文件

step3:配置JdbcTemplate.模板

注：jdbdTemplate把一些重复性的代码，比如（获取连接，关闭连接，处理异常都写好了，我们只需要调用该对象就能很方便的访问数据库

step4:调用JdbcTemplate的方法来访问数据库

注：通常将JdbcTemplate注入到DAO 

<!-- 读取db.propertise文件 -->

	<util:properties id="db" location="classpath:db.properties"></util:properties>
	<!-- 配置连接池 -->
	<bean id="ds" class="org.apache.commons.dbcp.BasicDataSource" destroy-method="close">
		<property name="driverClassName" value="#{db.driver}"/>
		<property name="url" value="#{db.url}"/>
		<property name="username" value="#{db.user}"/>
		<property name="password" value="#{db.pwd}"/>
	</bean>
	<!-- 配置jdbcTemplate -->
	<bean id="jt" class="org.springframework.jdbc.core.JdbcTemplate">
		<property name="dataSource" ref="ds"></property>
	</bean>
	<!-- 配置组件扫描 -->
	<context:component-scan base-package="dao"></context:component-scan>
```java
@Repository("employeeDao")
public class EmployeeDAO {
   @Resource(name="jt")
   private JdbcTemplate jt;
   
   public void save(Employee e){
      String sql="insert into t_emp values(t_emp_seq.nextval,?,?)";
      Object[] args={e.getName(),e.getAge()};
      jt.update(sql,args);
   }

```

## SpringMVC

### 1、什么是springMVC

用来简化基于MVC架构的web应用程序开发的框架

简化：springjdbc

解耦：管理对象之间的依赖关系

集成：mybatis

=====================================================================================

五大组件

DispatcherServlet 前端控制器

HandlerMapping  映射处理器

Controller   处理器

ModelAndView   处理结果和视图名

ViewResolver   视图解析器

![]()

它们之间的关系

1）请求发送给DispatcherServlet来处理，DispatcherServlet会依据HandlerMapping的配置调用对应的Controller来处理

2）Controller将处理结果封装成ModelAndView，然后返回给DispatcherServlet

3)DispatcherServlet会依据ViewResolver的解析调用对应的视图对象（比如jsp）来生成相应的页面

注：视图部分可以使用jsp,也可以使用其他的视图技术，比如freemarker,velocity等等

=========================================================================

step1:导包   spring-MVC

step2:添加配置文件

step3：配置DispatcherServlet

step4:写Controller

step5:写jsp

step6:在配置文件当中，添加HandlerMapping，ViewResolver,controller

============================================================================

基于注解的springMVC应用

1）编程步骤：

step1:导包   spring-MVC

step2:添加配置文件

step3：配置DispatcherServlet

step4:写Controller

step5:写jsp

step6在配置文件当中，添加ViewResolver配置，添加组件扫描，添加MVC注解扫描

