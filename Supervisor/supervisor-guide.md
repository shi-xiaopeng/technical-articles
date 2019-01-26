 配置好的supervisor ，过一段时间登陆后，发现supervisorctl 连接出现错误
```
unix:///tmp/supervisor.sock no such file
```
原因是：`.sock` 文件配置在 `/tmp` 之下，而`/tmp`会定期被清理，这个文件被删除之后就会出现这个错误。

1、打开配置文件

vim /your_dir/supervisord.conf

这里把所有的/tmp路径改掉，/tmp/supervisor.sock 改成 /var/run/supervisor.sock，/tmp/supervisord.log 改成 /var/log/supervisor.log，/tmp/supervisord.pid 改成 /var/run/supervisor.pid 要不容易被linux自动清掉

2、修改权限

    sudo chmod 777 /run
    sudo chmod 777 /var/log

如果没改，启动报错 IOError: [Errno 13] Permission denied: '/var/log/supervisord.log'

3、创建supervisor.sock

sudo touch /var/run/supervisor.sock
sudo chmod 777 /var/run/supervisor.sock

4. kill supervisord 进程
ps aux | grep supervisor
kill pid

4、启动supervisord，注意stop之前的实例或杀死进程

supervisord -c supervisord.conf
