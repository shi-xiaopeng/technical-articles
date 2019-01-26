### 1、减少进程数

修改配置文件`/etc/gitlab/gitlab.rb`中的`worker_processes`:

```
unicorn['worker_processes'] = 2
```

默认是被注释掉的，官方建议该值是CPU核心数加一，可以提高服务器的响应速度，如果内存只有4G，或者服务器上有其它业务，就不要改了，以免内存不足。另外，这个参数最小值是2，设为1，服务器可能会卡死。

### 2、减少数据库缓存

```
postgresql['shared_buffers'] = "256MB"
```

默认为256MB，可适当改小

### 3、减少数据库并发数

```
postgresql['max_worker_processes'] = 8
```

默认为8，可适当改小

### 4、减少sidekiq并发数

```
sidekiq['concurrency'] = 25
```

默认是25，可适当改小

### 5、启用Swap分区

使用Swap的方法，请自行搜索

需要注意的是，修改完配置以后，需要执行下面的命令使配置生效：

```
sudo gitlab-ctl reconfigure
sudo gitlab-ctl restart
```

