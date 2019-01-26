启动一个初始状态断开的screen会话：
[root@tivf06 tianq]# screen -dmS mygdb gdb execlp_test

连接该会话：
[root@tivf06 tianq]# screen -r mygdb

screen 选项：
```
-c file    使用配置文件file，而不使用默认的$HOME/.screenrc
-d|-D [pid.tty.host]	   不开启新的screen会话，而是断开其他正在运行的screen会话
-h num    指定历史回滚缓冲区大小为num行
-list|-ls    列出现有screen会话，格式为pid.tty.host
-d -m     启动一个开始就处于断开模式的会话
-r sessionowner/ [pid.tty.host]    重新连接一个断开的会话。多用户模式下连接到其他用户screen会话需要指定sessionowner，需要setuid-root权限
-S sessionname    创建screen会话时为会话指定一个名字
-v    显示screen版本信息
-wipe [match]    同-list，但删掉那些无法连接的会话
```

在 screen 窗口中：
```
C-a ?  显示所有键绑定信息
C-a w 显示所有窗口列表
C-a c  创建一个新的运行shell的窗口并切换到该窗口
C-a k  杀掉当前窗口
C-a n  切换到下一个窗口
C-a p  切换到上一个窗口
C-a d  暂时断开screen会话
```
