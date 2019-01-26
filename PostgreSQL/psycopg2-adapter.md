转载自 [Python连接PostgreSQL](http://qinqianshan.com/python-connection-postgresql/)
## 安装
```
$ pip install psycopg2
# or using setup.py
$ python setup.py build
$ sudo python setup.py install
```
## 连接到数据库
```
import psycopg2
conn = psycopg2.connect(database="testdb", user="postgres", password="pass123", host="127.0.0.1", port=“5432")
# 这个API打开一个连接到PostgreSQL数据库。如果成功打开数据库时，它返回一个连接对象conn。
```

## 创建表
```
import psycopg2
conn = psycopg2.connect(database="testdb", user="postgres", password="pass123", host="127.0.0.1", port="5432")
cur = conn.cursor()
#该程序创建一个光标将用于整个数据库使用Python编程。
cur.execute('''CREATE TABLE COMPANY
 (ID INT PRIMARY KEY NOT NULL,
 NAME TEXT NOT NULL,
 AGE INT NOT NULL,
 ADDRESS CHAR(50),
 SALARY REAL);''')
#cursor.execute(sql [, optional parameters])
此例程执行SQL语句。可被参数化的SQL语句（即占位符，而不是SQL文字）。 psycopg2的模块支持占位符用％s标志。例如：cursor.execute(“insert into people values (%s, %s)", (who, age))    
conn.commit()
#connection.commit() 此方法提交当前事务。如果不调用这个方法，无论做了什么修改，自从上次调用#commit()是不可见的，从其他的数据库连接。
conn.close() 
#connection.close() 此方法关闭数据库连接。请注意，这并不自动调用commit（）。如果你只是关闭数据库连接而不调用commit（）方法首先，那么所有更改将会丢失
```
## INSERT 插入
## SELECT
## UPDATE
## DELETE
