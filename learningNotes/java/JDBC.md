JDBC允许用户访问任何形式的表格数据，尤其是关系数据库中的数据

### 1、执行流程

连接数据库     为数据库传递查询和更新指令      处理数据库响应并返回的结果

### 2、操作步骤

*导包 (导入ojdbc和dbcp包，java中仅仅提供了JDBC的接口(java.sql包中的Connection)，具体实现由数据库厂商来实现),ojdbc为jdbc包，dbcp为连接池包

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

第一步：注册驱动(不同数据库的驱动不同)

```java
Class.forName(driverClass)
//加载MySql驱动
Class.forName("com.mysql.jdbc.Driver")
//加载Oracle驱动
Class.forName("oracle.jdbc.driver.OracleDriver")
```

第二步：建立连接

```java
Connection conn = DriverManager.getConnection("jdbc:mysql://127.0.0.1:3306/imooc", "root", "root");
```

DriverManger是java.sql包中的类，用来管理驱动，注册驱动告诉DriverManager使用哪一套驱动（mysql还是oracle)，然后进行连接，连接数据库  

 Connection 为接口，但DriveraManager 返回的是接口类型的实现类

第三部：创建Statement\PreparedStatement对象

利用连接创建Statement，用来执行SQL。提供不同的方法

```java
Statement stmt = conn.createStatement();
ResultSet rs = stmt.executeQuery("SELECT user_name, age FROM imooc_goddess");
        //如果有数据，rs.next()返回true
        while(rs.next()){
            System.out.println(rs.getString("user_name")+" 年龄："+rs.getInt("age"));
        }

```

```java
//sql
        String sql = "INSERT INTO imooc_goddess(user_name, sex, age, birthday, email, mobile,"+
            "create_user, create_date, update_user, update_date, isdel)"
                +"values("+"?,?,?,?,?,?,?,CURRENT_DATE(),?,CURRENT_DATE(),?)";
        //预编译
        PreparedStatement ptmt = conn.prepareStatement(sql); //预编译SQL，减少sql执行

        //传参
        ptmt.setString(1, g.getUser_name());
        ptmt.setInt(2, g.getSex());
        ptmt.setInt(3, g.getAge());
        ptmt.setDate(4, new Date(g.getBirthday().getTime()));
        ptmt.setString(5, g.getEmail());
        ptmt.setString(6, g.getMobile());
        ptmt.setString(7, g.getCreate_user());
        ptmt.setString(8, g.getUpdate_user());
        ptmt.setInt(9, g.getIsDel());

        //执行
        ptmt.execute();
```

### 3、项目中如何操作

在正式项目中要对数据库进行访问，首先会建立domain层，（封装的数据对象可叫做entity,或vo/po/pojo）在domain层中建立与数据库表相对应的JavaBean

JavaBean规范要求：

```
JaveBean
* 满足如下规范的类：
* 必须有包
* 必须有无参构造器
* 必须实现序列化接口
* 通常会有get/set方法
```

再建立dao层（Data Access Object)数据访问对象，对数据库进行操作

-------------------------------------------------------------------------------------------------------------------------------------------------------

将数据库配置文件放在一个.properties文件中，如下

数据库连接参数

driver=oracle.jdbc.driver.OracleDriver
url=jdbc:oracle:thin:@localhost:1521:xe
user=system
pwd=oracle

连接池参数

initsize=1
maxsize=2

```java
Properties p=new Properties();
		try {
			//加载配置文件   读取.class中的db.properties,如果直接用文件流的话，读取的是resource中的，而resource
			//中的文件不会被copy到服务器中
			p.load(DBTool.class.getClassLoader().getResourceAsStream("db.properties"));
			//读取连接参数
			driver=p.getProperty("driver");
			url=p.getProperty("url");
			user=p.getProperty("user");
			pwd=p.getProperty("pwd");
```

然后注册驱动，建立连接，对数据库进行操作。

===================================================================================

```
**
 * 连接池
 * 1.不用连接池时的问题
 * 直接使用DriverManager时：
 * 每次调用它都会创建新连接，而没有复用
 * 它没有管理连接上限，当并发数大时可能导致数据库崩溃
 * 2.连接池作用
 * 连接池的作用就是解决上述问题：
 * 它能复用连接，提高效率
 * 它能管理连接上限，避免数据库崩溃
 * 3.有哪些常用连接池
 * DBCP     C3P0
 * 4.连接池的工作原理
 * 当创建连接池后，它会自动创建一批（配）连接放于池内
 * 当用户调用它时，它会给用户一个连接，并将连接标为占用
 * 当用户使用完连接后，将连接归还给连接池，它会将连接标为空闲
 * 若连接池发现连接快不够用时，它会再创建一批（配）连接
 * 若占用的连接达到数据库上限（配）时，连接池会让新用户等待
 * 在高峰期过后，连接池会关闭一批（配）连接
 * 5.如何使用连接池
 * sun规定了连接池的接口：DataSource
 * DBCP实现了连接池的接口：BasicDataSource
 * 
```

```
**
 * 直接使用JDBC访问数据库时，需要避免以下隐患:
1.每一次数据操作请求都需要建立数据库连接、打开连接、存取数据和关闭连接等步骤。而建立和打开数据库连接是一件既耗资源又费时的过程，如果频繁发生这种数据库操作，势必会使系统性能下降。
2. 连接对象代表着数据库系统的连接进程，是有限的资源。如果系统的使用用户非常多，有可能超出数据库服务器的承受极限，造成系统的崩溃。
数据库连接池是解决上述问题最常用的方法。所谓连接池，即可以创建并持有数据库连接的组件。连接池可以预先创建并封装一些连接对象并将其缓存起来，当需要使用连接对象时可以向连接池“借”一个连接，用完之后将其“归还”到连接池中。数据库连接池的主要功能如下：
1. 连接池对象的创建和释放。
2. 服务器启动时，创建指定数量的数据库连接。
3. 为用户请求提供可用连接。如果没有空闲连接，且连接数没有超出最大值，创建一个新的数据库连接。
4. 将用户不再使用的连接标识为可用连接，等待其他用户请求。
5. 当空闲的连接数过多时，释放连接对象。
连接池组件一般都需要实现JDBC规范中的javax.sql.DataSource接口。DataSource接口定义了获取连接的方法getConnection方法。常用的连接池组件有DBCP、c3p0和proxool等
 * @author 薛榕刚
 *
 */
```

```java
//连接池对象——由DBCP提供
private static BasicDataSource ds;

static{
   Properties p=new Properties();
   try {
      p.load(DBUtil.class.getClassLoader().getResourceAsStream("db.properties"));
      //读取参数
      String driver=p.getProperty("driver");
      String url=p.getProperty("url");
      String user=p.getProperty("user");
      String pwd=p.getProperty("pwd");
      String initsize=p.getProperty("initsize");
      String maxsize=p.getProperty("maxsize");
      //创建连接池
      ds=new BasicDataSource();
      //设置参数
      //使用这个参数注册驱动
      ds.setDriverClassName(driver);
      //使用这3个参数创建连接
      ds.setUrl(url);
      ds.setUsername(user);
      ds.setPassword(pwd);
      //使用其他参数管理连接
      ds.setInitialSize(new Integer(initsize));
      ds.setMaxActive(new Integer(maxsize));
     
     public static Connection getConnection() throws SQLException{
		return ds.getConnection();
	}
```

```
/*
 * 由连接池创建的连接，连接的close方法被连接池重写了，变为了归还连接的逻辑，即：
 * 连接池会将连接的状态设置为空闲，并清空连接中所包含的任何数据
 */
```

 