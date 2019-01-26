```
systemctl command [options] app.service
```
#### command
- start 启动
- stop 关闭
- restart 重启
- reload 重新载入配置并生效
- reload-or-restart 当不确认reload时候有效时使用
- status 查看状态
- enable 设置开机启动
- disable 取消开机启动
- [blank] == list-units  列出所有 loaded and active unit
- list-units --all  列出所有loaded and attempt to load unit
- list-unit-files  列出systemd路径下所有可用unit, 包括没有尝试载入的
- cat 查看配置文件
- list-dependencies 列出依赖的服务
- list-dependencies --all 列出所有依赖服务
- show 查看详细的底层配置
- edit 添加或者覆盖已有的unit file
- edit --full 可以看到并修改整个unit file
- deamon-reload 修改完成之后，应用修改
- is-active 是否是active 的
- is-enable 是否是开机启动
- is-failed 是否已已经失败
- mask 标识服务为masked, 不可以被启动
- unmask 去除服务的 masked 状态

### options
```
list-units 
--all 
--type=service/target   指定 unit 类型
--state=inactive/active   指定 unit 状态
```

# short cut
```
systemctl poweroff   关闭
systemctl reboot  重启
systemctl rescue   救援模式
systemctl halt 立即暂停   
```

#### Tips
.service 后缀可以省略不写