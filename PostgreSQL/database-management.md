查找存在的database
`SELECT * FROM pg_database; `  OR 在postgres shell 中键入 `\l` ，OR `psql -l` 命令选项
CREATE DATABASE name;
当前用户自动成为新建数据库的owner.
第一个数据库 在数据存储区初始化时经由 initdb 命令创建，名字是 postgres.
同时另一个名为 template1的数据库也在数据库群初始化的时候创建，每当要创建一个新的database时，就从temple1克隆一个。这意味着你对template1所做的任何更改都将体现在新创建的数据库中。所以除非你希望这个object出现在新创建的每一个database里，否则不要再template1中创建任何对象。

在shell 中执行，createdb dbname. 注意不带任何属性信息的createdb命令将以当前用户的名字创建数据库。如果要指定owner你可以用以下命令
CREATE DATEBASE dbname OWNER rolename;
or
createdb -O rolename dbname
还有一个标准系统数据库名为 template0, 这个数据库中包含和template1一样的内容，也就是只有postgresql 预定义标准对象。template0 在数据库集初始化后就不应该做任何修改。你可以用template0作为模板创建一个不包含template1中自定义对象的原生数据库。pg_dump导入数据库时为了不受自定义object的影响，以template0为模板创建数据库就很有必要。
另一个使用template0作为创建模板的原因是使用template0创建的database能够指定使用新的编码格式和本地设置，而使用template1创建的database，必须使用与其中包含的object相同的编码和设置。
从template0创建database:
CREATE DATABASE dbname TEMPLATE template0;
或者从 shell 环境执行：
createdb -T template0 dbname
pg_database中有两个很有用的属性：datistemplate, datallowconn.
datistemplate为True, 该数据库可以被作为template数据库被任何用户用户创建新数据；为False, 则只有superuser和这个数据库的owner才能clone它。
datallowconn 为False， 则该数据库将不再接受新的连接，之前的连接不会受影响。
template1 是作为 CREATE DATABASE命令的默认选项。

### Database Configuration
设置geqo属性：ALTER DATABASE mydb SET geqo TO off;
这个命令会保存这个设置，在接下来的链接中才会生效。
恢复设置：ALTER DATABASE dbname RESET varname

### Destroy a Database
删除数据库使用： DROP DATABASE name;
只有数据库的owner 或者 superuser 能够删除一个数据库。这个命令会不可修复地删除库中包含的所有对象。
当你处于数据库A 的链接中时，你无法执行DROP DATABASE A；删除A。但是你可以链接到其他数据库来执行删除操作。当你要删除最后一个用户数据库时，你将只能通过连接到template1进行操作。
shell 中的命令：dropdb dbname

### Tablespaces
创建 Tablespace
CREATE TABLESPACE fastspace LOCATION '/ssd1/postgresql/data';
地址必须是一个存在的空的目录，并且 owned by Postresql 系统用户.
Tables, indexes, database 都能被放到 特定的tablespace下。
CREATE TABLE foo(i, int) TABLESPACE space1;
或者可以设置默认的tablespace:
SET default_tablespace = space1;
CREATE TABLE foo(i, int);
temp_tablespace用于缓存表，index, temp files 等的放置。
当 default_tablespace 不是一个空字符串时，它将为没有指定 tablespace选项的 CREATE TABLE 和 CREATE INDEX 命令提供一个默认的tablespace.
两个 tablespace会被创建当cluster初始化时。pg_global 用于shared system catalogs; pg_default 是template0 template1的默认tablespace, 也是其他新建的数据库的默认tablespace, 除非被另外指定。
tablespace 一旦被创建，可以被任意数据库使用，只要用户有权限。这意味着，除非tablespace下的所有的database中的所有对象都已被删除， tablespace不能被删除。
删除空的tablespace使用， DROP TABLESPACE command.
查看已经存在的tablespace 可以查 pg_tablespace 表
SELECT * FROM pg_tablespace;
或者 元命令 \db 也可以列出所有的tablespace
PostgreSQL makes use of symbolic links to simplify the implementation of tablespaces.
This means that tablespaces can be used only on systems that support symbolic links.
由于postgres 使用了 symbolic links 来简化tablespace的实现，这意味着tablespace只能在支持 symbolic links 的系统上使用。

