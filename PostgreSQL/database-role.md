
[Database Role] https://www.postgresql.org/docs/10/static/database-roles.html

sudo -u postgres psql gaidb

`brew install postgres`  使用 `homebrew` 安装 `postgres`
`brew services start postgresql`  开启 `postgres` 服务，系统启动时启动

`createdb` db_name    创建数据库 `db_name`
`createdb` 会创建一个以当前用户名为名的数据库
`dropdb` db_name  删除db_name 数据库

用户及权限管理
`CREATE ROLE name`;       创建用户  
`DROP ROLE name`;           删除已经存在的用户
createuser， dropuser 封装了以上的 SQL 语句，可以在Command Line 中直接调用。
`createuser name`
`dropuser name`

列出当前数据库上有哪些用户：
`SELECT * FROM pg_roles;`
或者使用 `\du` 元命令，这个可以列出各个用户的权限信息。

`CREATE ROLE name LOGIN;`
`CREATE USER name;`
create user 默认具有 login 权限，而 create role 默认没有，除这点区别外两者是等价的。
除了 Login 之外，superuser 会越过所有的权限检查。
必须由一个superuser 才可以创建一个数据库 superuser 。
`CREATE ROLE name SUPERUSER;`

数据库创建
除了superuser 外，一个角色（role）必须被明确地给予创建数据库的权限，否则不能创建数据库。 `CREATE ROLE name CREATEDB;`

角色创建
除 superuser 外，一个角色必须被明确给予用户创建权限，否则无法创建、修改role.一个拥有 createrole 权限的role, 可以创建、修改、删除其他的role, 创建和废除成员关系。但是涉及到superuser的创建、更改、删除、成员关系，createrole 的权限不够。
`CREATE ROLE name CREATEROLE;`

复制 replication
想要有流式复制权限的role, 必须用时具有 Login 权限.
`CREATE ROLE name REPLICATION LOGIN;`

创建时需要密码的role
`CREATE ROLE name PASSWORD 'string';`

修改role 的密码:
`ALTER ROLE davide WITH PASSWORD 'hu8jmn3';`

给一个role 创建用户和新数据库的权限: 
`ALTER ROLE miriam CREATEROLE CREATEDB;`

drop and reassign:
```
REASSIGN OWNED BY doomed_role TO successor_role;
DROP OWNED BY doomed_role;
-- repeat the above commands in each database of the cluster
DROP ROLE doomed_role;
```



