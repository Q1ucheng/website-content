# 记录学习和使用MySQL的过程

了解到开发过程中可能会涉及一些数据库的使用，遂先简单上手一下Mysql（CS61A的学习也让我有了一点SQL的基础）

## 前期配置

先安装Mysql：

```
pip install pymysql -i https://pypi.tuna.tsinghua.edu.cn/simple
```

发现好像需要一个数据库管理工具，在Github上找到SQLyog软件：[Github链接](https://github.com/webyog/sqlyog-community/wiki/Downloads)

> SQLyog是一款功能强大的MySQL数据库管理工具，旨在帮助用户更高效地管理和操作MySQL数据库

下载完成打开，新建（输入任意名称）--> 设置密码：

![](.\pic\image-20240805154435632.png)

结果报错：

```
错误号码2002
can't connect to serve on 'localhost' (10061)
```

查询后发现可能是没有开启Mysql服务，cmd以管理员身份命令`net start mysql`，提示我服务名无效，继续上网搜索，发现应该是我没有为MySQL设置环境变量（研究了一会发现是我没有安装官方的MySQL（一个完整的数据库管理系统））

> 发现一个小技巧，可以使用`pip show <package_name>`来找到`Location`（与后文无关）
>
> ![](.\pic\image-20240805163729860.png)

下载MySQL：[Download MySQL Community Server](https://dev.mysql.com/downloads/mysql/)

打开解压的文件夹 `F:\mysql-9.0.1-winx64`，在该文件夹下创建 **my.ini** 配置文件，编辑 **my.ini** 配置以下基本信息：

```ini linenums="1" hl_lines="8 9"
[client]
# 设置mysql客户端默认字符集
default-character-set=utf8
 
[mysqld]
# 设置3306端口
port=3306
# 设置mysql的安装目录
basedir=F:\\mysql-9.0.1-winx64
# 设置 mysql数据库的数据的存放目录，MySQL 8+ 不需要以下配置，系统自己生成即可，否则有可能报错
# datadir=F:\\mysql-9.0.1-winx64
# 允许最大连接数
max_connections=20
# 服务端使用的字符集默认为8比特编码的latin1字符集
character-set-server=utf8
# 创建新表时将使用的默认存储引擎
default-storage-engine=INNODB
```

以管理员身份打开 cmd 命令行工具，切换目录`F:\mysql-9.0.1-winx64\bin`

初始化数据库：

```
mysqld --initialize --console
```

执行完成后，会输出 root 用户的初始默认密码：`kkwf2+y86%YO`

```
F:\mysql-9.0.1-winx64\bin>mysqld --initialize --console
2024-08-05T08:31:47.128678Z 0 [System] [MY-015017] [Server] MySQL Server Initialization - start.
2024-08-05T08:31:47.135111Z 0 [System] [MY-013169] [Server] F:\mysql-9.0.1-winx64\bin\mysqld.exe (mysqld 9.0.1) initializing of server in progress as process 4220
2024-08-05T08:31:47.148120Z 0 [Warning] [MY-013242] [Server] --character-set-server: 'utf8' is currently an alias for the character set UTF8MB3, but will be an alias for UTF8MB4 in a future release. Please consider using UTF8MB4 in order to be unambiguous.
2024-08-05T08:31:47.186317Z 1 [System] [MY-013576] [InnoDB] InnoDB initialization has started.
2024-08-05T08:31:47.448596Z 1 [System] [MY-013577] [InnoDB] InnoDB initialization has ended.
2024-08-05T08:31:49.177117Z 6 [Note] [MY-010454] [Server] A temporary password is generated for root@localhost: kkwf2+y86%YO
2024-08-05T08:31:50.943082Z 0 [System] [MY-015018] [Server] MySQL Server Initialization - end.
```

> 感觉初始密码太复杂，开始更改：
>
> ```
> F:\mysql-9.0.1-winx64\bin>mysqladmin -uroot -p password
> Enter password: ************
> New password: ***********
> Confirm new password: ***********
> Warning: Since password will be sent to server in plain text, use ssl connection to ensure password safety.
> ```
>
> 记录一下，密码为`Zqc20040813`

接着就可以启动MySQL服务了

```
F:\mysql-9.0.1-winx64\bin>mysqld install
Service successfully installed.

F:\mysql-9.0.1-winx64\bin>net start mysql
MySQL 服务正在启动 .
MySQL 服务已经启动成功。
```

![](.\pic\image-20240805165220199.png)

----

## 创建数据库连接

```python
from pymysql import Connection

con = None
try:
    # 创建数据库连接
    con = Connection(
        host="localhost",  # 主机名
        port=3306,  # 端口
        user="root",  # 账户
        password="Zqc20040813",  # 密码
    )

    print(type(con))
    print(con.get_host_info())
    print(con.get_server_info())

except Exception as e:
    print("异常", e)

finally:
    if con:
        # 关闭连接
        con.close()
```

`print`结果为：（成功创建连接）

```python
<class 'pymysql.connections.Connection'>
socket localhost:3306
9.0.1
```

## Pymysql执行数据库模式定义语言

在Python中，连接MySQL数据库后，使用 `cursor()` 方法从连接对象中创建一个游标对象。游标对象用于执行SQL语句，并在需要时返回查询结果

> 先在SQLyog中新建（`ctrl`+`D`）一个数据库（我将其命名为db_python）

```python
from pymysql import Connection

con = None
try:
    # 创建数据库连接
    con = Connection(
        host="localhost",  # 主机名
        port=3306,  # 端口
        user="root",  # 账户
        password="Zqc20040813",  # 密码
        database="db_python"  # 指定操作的数据库
    )

    # 创建游标对象
    cursor = con.cursor()

    # 定义建表sql语句
    sql = """
    CREATE TABLE `t_student3` (
        `id` int(11) NOT NULL AUTO_INCREMENT,
        `name` varchar(10) DEFAULT NULL,
        `age` int(11) DEFAULT NULL,
        PRIMARY KEY (`id`)
    ) ENGINE=InnoDB DEFAULT CHARSET=utf8
    """

    # 使用游标对象，执行sql
    cursor.execute(sql)

except Exception as e:
    print("异常", e)

finally:
    if con:
        # 关闭连接
        con.close()
```

![](.\pic\image-20240805171612985.png)

> 继续创建表后需要刷新对象浏览器才能看到新建的结果

##  Pymysql执行数据操纵语言

为了测试，可以直接在SQLyog当中修改数据库内容：

![](.\pic\image-20240805172950422.png)

```python
from pymysql import Connection

con = None
try:
    # 创建数据库连接
    con = Connection(
        host="localhost",  # 主机名
        port=3306,  # 端口
        user="root",  # 账户
        password="Zqc20040813",  # 密码
        database="db_python"  # 指定操作的数据库
    )

    # 获取游标对象
    cursor = con.cursor()

    # 使用游标对象执行 SQL 语句
    cursor.execute("SELECT * FROM t_student3")

    # 获取查询所有结果
    result = cursor.fetchall()

    # 打印结果
    print(type(result), result)
    for row in result:
        print(row)

except Exception as e:
    print("异常：", e)

finally:
    if con:
        # 关闭连接
        con.close()
```

得到结果：

```
<class 'tuple'> ((1, 'wayne', 19), (2, 'Ronald', 19), (3, 'nothing', 20), (4, 'John', 30))
(1, 'wayne', 19)
(2, 'Ronald', 19)
(3, 'nothing', 20)
(4, 'John', 30)
```

插入操作也一样：

```python
# 使用游标对象执行 SQL 语句
    cursor.execute("INSERT INTO t_student3 VALUES (null, 'insert_man', 22)")
```

注意每次操作后需要提交，可以在`con`的设置中添加`autocommit=True`

```python
# 创建数据库连接
    con = Connection(
        ...
        autocommit=True  # 自动提交
    )
```

刷新就可以看到`insert_man`加入到数据库中了

![](.\pic\image-20240805173936634.png)

更新和删除操作也很简单：

```python
cursor.execute("UPDATE t_student3 SET age=999 WHERE id=5")
cursor.execute("delete from t_student3 WHERE id=5")
```

