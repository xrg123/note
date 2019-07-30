# Servlet（菜鸟教程<https://www.runoob.com/servlet/servlet-intro.html> ）

Java Servlet是运行在 Web 服务器上的程序，作为浏览器和http服务器上的数据库或应用程序的中间层。tomcat是一款web服务器，浏览器端的请求会发送到tomcat服务器，服务器再将请求交给servlet处理，处理后的结果返回浏览器。Servlet 是服务 HTTP 请求并实现 **javax.servlet.Servlet** 接口的 Java 类。Web 应用程序开发人员通常编写 Servlet 来扩展 javax.servlet.http.HttpServlet，并实现 Servlet 接口的抽象类专门用来处理 HTTP 请求。

### 1、servlet实现方式

1、实现javax.servlet.servlet接口

该接口有5个方法，其中三个代表servlet的生命周期，分别为init()、service()、destroy(),另外两个为普通方法，分别为getServletConfig()和getServletInfo()

2、继承GenericServlet类

GenericServlet类是一个抽象类，实现了servlet接口

3、继承httpServlet抽象类

httpServlet进一步继承并封装了GenericServlet类

httpServlet扩展了Http的内容，一般都使用继承HttpServlet的方式来定义一个servlet

```java
//Tomcat创建Servlet的过程
//LoginServlet ls=new LoginServlet();
//ServletConfig cfg=new ServletConfig();
//ls.init(cfg);
//ls.service();
```

### 2、servlet生命周期

Servlet 生命周期可被定义为从创建直到毁灭的整个过程。以下是 Servlet 遵循的过程：

- Servlet 通过调用 **init ()** 方法进行初始化。

  init 方法被设计成只调用一次。它在第一次创建 Servlet 时被调用，在后续每次用户请求时不再调用。

  Servlet 创建于用户第一次调用对应于该 Servlet 的 URL 时，但是也可以指定 Servlet 在服务器第一次启动时被加载。当用户调用一个 Servlet 时，就会创建一个 Servlet 实例，每一个用户请求都会产生一个新的线程，适当的时候移交给 doGet 或 doPost 方法。init() 方法简单地创建或加载一些数据，这些数据将被用于 Servlet 的整个生命周期。

- Servlet 调用 **service()** 方法来处理客户端的请求。

  service() 方法是执行实际任务的主要方法。Servlet 容器（即 Web 服务器）调用 service() 方法来处理来自客户端（浏览器）的请求，并把格式化的响应写回给客户端。每次服务器接收到一个 Servlet 请求时，服务器会产生一个新的线程并调用服务。service() 方法检查 HTTP 请求类型（GET、POST、PUT、DELETE 等），并在适当的时候调用 doGet、doPost、doPut，doDelete 等方法。

  service() 方法由容器调用，service 方法在适当的时候调用 doGet、doPost、doPut、doDelete 等方法。所以，您不用对 service() 方法做任何动作，您只需要根据来自客户端的请求类型来重写 doGet() 或 doPost() 即可。

- Servlet 通过调用 **destroy()** 方法终止（结束）。

  destroy() 方法只会被调用一次，在 Servlet 生命周期结束时被调用。destroy() 方法可以让您的 Servlet 关闭数据库连接、停止后台线程、把 Cookie 列表或点击计数器写入到磁盘，并执行其他类似的清理活动。

  在调用 destroy() 方法之后，servlet 对象被标记为垃圾回收。

  每次浏览器发送完请求后，会初始化，执行，手动执行销毁后，没有立即被回收，当继续请求时，不再初始化，直接执行，销毁。servlet销毁时间（关闭servlet容器时）

- 最后，Servlet 是由 JVM 的垃圾回收器进行垃圾回收的。

  ### 3、多个用户同时请求同一个方法

  多个用户同时请求时，如果请求数量超过服务器的最大连接数量（nginx最大连接数为65535），则排队执行，服务器为每个请求创建一个线程，线程按同样顺序执行代码，线程间不相互干扰，但如果多个线程对对象中的共享变量进行操作，则可能产生线程安全问题，需要进行同步。

  ### 4、servlet特征

  ```
  --是满足规范（sun)的对象，也叫组件
  --可存储在服务器上，可动态的拼接资源（HTML,IMG),术语：处理HTTP协议
  --servlet是sun推出的用来在服务器端处理http协议的组件
  ```


```
服务器
1.名词解释
--java服务器
--WEB服务器
--java web 服务器
--servlet容器
2.本质
是一个软件，一个可以运行java项目的软件
3.举例
Tomcat(Apache)       JBoss     WebLogic     WebSphere
```

```
Tomcat使用方式
1.单独使用（软件上线时）
1）配置JAVA_HOME
2）下载及安装
Apache官网
2.通过Eclipse管理（开发时）
```

### 5、servlet开发步骤

*创建web项目

*写一个类继承HttpServlet类（或实现servlet接口，或继承GenericServlet类，在idea中直接新建servlet类）

该类中init()方法进行初始化，doGet()、doPost()方法处理请求，service()方法内拼接网页

*配置servlet

（也可以加注解免去配置，@WebServlet(name = "ServletDemo2",urlPatterns = "/test2") 新建servlet时，勾选 Create Java EE 6 annotated class)

在web/WEB-INF中的web.xml中进行配置

<!-- 配置Servlet -->
  <!-- 1.声明Servlet,并给它取个别名  完整包名 -->
  <servlet>
  	<servlet-name>time</servlet-name>
  	<servlet-class>web.TimeServlet</servlet-class>
  </servlet>
  <!-- 2.通过别名引用Servlet，并给它取个网名（网络访问路径） -->
  <servlet-mapping>
  	<servlet-name>time</servlet-name>
  	<!-- 网名必须以斜线开头 -->
  	<url-pattern>/ts</url-pattern>
  </servlet-mapping>

*启动tomcat

### 6、HttpServletRequest和ServletRequest区别

两者都是接口，HttpServletRequest继承自ServletRequest，多了一些征对Http协议的方法，如getHeader(),getMethod(),getSession(),实现HttpServlet中的service()方法时，应选用参数为HttpServletRequest的service()方法

### 7、一些概念区别

http协议中的报文包含请求报文和响应报文

请求报文中包括请求行，首部行和实体主体

响应报文中包括状态行，首部行和实体主体

java中请求报文及响应报文的首部行成为消息头，可通过迭代器获取消息头的信息

```java
Enumeration<String> e=req.getHeaderNames();
while(e.hasMoreElements()){
    String key=e.nextElement();
    String value=req.getHeader(key);
    System.out.println(key+":"+value);
}
```

请求报文消息头如下所示：

host:localhost:8080
connection:keep-alive
cache-control:max-age=0
upgrade-insecure-requests:1
user-agent:Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/75.0.3770.142 Safari/537.36
accept:text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3
accept-encoding:gzip, deflate, br
accept-language:zh-CN,zh;q=0.9
cookie:Hm_lvt_f8df255dfb46b5e00186a537e73370d1=1556417204,1556542749,1556774612; JSESSIONID=FBBD14C9BE729292D1FE1EE9FBDBDCAA

响应内容的消息头规则：

```java
   //大部分的消息头数据由服务器自动填写
   //只有ContentType必须由我们填写
   //告诉浏览器向它发送的是什么类型的内容
   res.setContentType("text/html");
   
   //3）实体内容   服务器向浏览器发送的业务数据
   //服务器向浏览器发送的具体内容
   //获取输出流，该流指向的目标是浏览器
   PrintWriter w=res.getWriter();
   //此处拼一个简化版 的网页
   w.println("<p>"+now+"</p>");
   w.close();
```

```
1）在开发时，很多事情不需要我们处理
--浏览器和服务器通信的步骤由浏览器和服务器自动实现
--请求数据中的请求行，消息头由浏览器自动填写
--响应数据中的状态行和消息头由服务器自动填写
2）少量数据需要我们处理
--请求数据中的实体内容由我们提供
--响应数据中的实体内容由我们提供
通过request处理请求数据，通过response处理响应数据
```

### 8、整个请求过程

浏览器发送请求到tomcat服务器，服务器会将请求交给HttpServlet对象，同时创建两个对象ServletRequeset和ServletResponse(如果调用service(HttpServletRequest request, HttpServletReaponse response)方法，这两个对象会被强转为HttpServletRequest和HttpServletResponse对象),当HttpServlet对象中存在Service()方法时，service()方法处理请求，当service()方法缺失时，会交由相应的doPost()和doGet()方法处理

----------------------------------------------------------------------------------------------------------------------------------------------------------

service()方法时servlet接口中的方法，servlet容器默认将请求发送到该方法，该方法默认行为时转发http请求到doxxx方法中，如果重载了该方法，默认操作被覆盖，不在进行转发。