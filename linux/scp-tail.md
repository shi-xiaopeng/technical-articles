pg_dump -U postgres -p 5777 -h localhost gaidb > gaidb.sql
将 gaidb 数据库数据导出到 gaidb.sql
psql -d gaidb -f gaidb.sql
- d 要导入到哪个数据库，数据库名；
- f  要导入的数据库文件，路径；

scp django@120.79.65.12:/home/django/gaidb.sql . 
从scp 远程服务器copy文件到本地当前目录

tail -f filename
循环读取文件内容到标准输出

命令从指定点开始将文件写到标准输出.使用tail命令的-f选项可以方便的查阅正在改变的日志文件,tail -f filename会把filename里最尾部的内容显示在屏幕上,并且不但刷新,使你看到最新的文件内容. 

