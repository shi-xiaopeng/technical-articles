进入sql命令交互环境
```
mysql -u root -p;
select * from tables;
show databases;
use database;
exit
```
1. sql语句对大小写不敏感
2. sql语句在句尾加不加分号，根据使用数据库的不同而不同，MySql需要分号
3. sql语言分为数据操纵语言(DML)和数据定义语言(DDL)
4. 数据操纵语言：select, update, delete, insert into
5. 数据定义语言主要有：
    create database - 创建新数据库
    alter database - 修改数据库
    create table - 创建新表
    alter table - 变更（改变）数据库表
    drop table - 删除表
    create index - 创建索引（搜索键）
    drop index - 删除索引
6. select 语句
    select <列名称>（, <列名称>）from <表名称>
    select * from <表名称>
7. 如果希望仅仅列出不同的值， 使用 ( distinct )
    select distinct <列名称> from <表名称>       
8. where 子句
    select <列名称> from 表名称  where  列  运算符  值
    select * from Persons where Year > 1965
    select * from Persons where City = 'Beijing'
    文本值使用单引号环绕
    操作符：
    ```
    =                  等于
    != 或者 <>         不等于
    > , <             大于， 小与
    >=,  <=           大于等于，小于等于
    between           在某个范围内
    like              搜索某种模式
    ```
9. and , or
    select * from Persons where firstname='Thomas'  and  lastname='Carter'
    select * from Persons where firstname='Thomas'  or  lastname='Carter'
    select * from Persons where  (firstname='Thomas' or firstname='William') and lastname='Carter'
10. order by 子句
    根据指定的列对结果进行排序，默认是升续，降续排列可用desc表示
    select Company,  OrderNumber from Orders order by Company
    select Company, OrderNumber from Orders order by Company, OrderNumber
    select Company, OrderNumber from Orders order by Company desc, OrderNumber
    select Company, OrderNumber from Orders order by Company desc, OrderNumber asc
11. insert into
    向表格中插入新的行，有两种写法：
    insert into <table_name> values ( 值1， 值2，··· ）
    insert into <table_name> ( 列1， 列2， 列3···）values  ( 值1 ，值2， 值3，···）
12. update 语句   用于修改表中的数据
    UPDATE <table_name> SET <列名1>=新值，<列名2>=新值 WHERE <条件>
    update Persons set Address='Jiangpu road', City='Shanghai' where Lastname='Wilson'
13. delete语句， 用于删除表中的行
    DELETE FROM <table_name> WHERE <子句>
    删除表中所有行 : delete * from <table_name> 或者 delete from <table_name>
    这是表的结构、属性、索引都是完整的。
14. LIMIT用法
     select * from <table_name> limit <num>     会截取搜索结果的前num条
     select * from <table_name> limit <num1>, <num2>  会截取搜索结果从num1开始num2个结果
15. Like用法
    select column(s) from <table_name> where column_name LIKE pattern
    select * from Person where city like "N%"    搜索城市以N开头的记录
    select * from Person where city like "%lon%"  搜索城市中包含lon的记录
    select * from Person where city NOT LIKE "%lon%"  搜索城市中不含lon的记录
16. SQL 通配符
    % : 代替一个或多个字符；
    _ : 仅代替一个字符
    [char_list] : 字符列中任何一个单字
    [^ char_list] 或 [! char_list] : 不在字符列中的任何一个单字 
    SELECT * FROM Persons WHERE City LIKE '[ALN]%' 表示城市以A、L、N开头的记录
17. between 用法
    select column_name(s) from table_name where column_name between value1 and value2;
    select * from Persons where lastname between 'Adams' and 'Carter' --- 会以字母顺序显示出介于 "Adams"（包括）和 "Carter"（不包括）之间的人
    select * from Persons where lastname NOT between 'Adams' and 'Carter' --- 会显示出'Adams' 和'Carter' 范围之外的人
18. 别名AS 用法
    select column_name AS alias_name from table_name;
19. inner join, left join, right join, full join
    left join  当右表不存在匹配项时依然返回行
    right join 当左表不存在匹配项是依然返回行
    inner join 是当两张表中都存在匹配项时，才返回结果，是left join与right join 结果的交集
    full join ，是left join 与right join结果的和集
20. 返回匹配指定条件的行数
    SELECT COUNT(column_name) FROM table_name; 返回指定列值得数目(不含NULL)
    SELECT COUNT(*) FROM table_name; ----返回表中的记录数
