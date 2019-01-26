File
chmod 755 filename # set filename to -rwxr-xr-x permisions
Directory
r ：（在 x 有效时，）有效时，可读；无效时，可进入目录但是不可读
w：在 x 有效时，可修改、删除等
x：有效时目录可进入，没有时目录不可进入

su (short for substitute user), 执行之后输入密码，会进入superuser Session, 退出superuser Session 使用 exit.
Mac OS 上的 su 不可用，使用 sudo + command 代替，如果使用 superuser 身份运行的 shell, 可以使用命令 sudo su, sudo sh, sudo -s, 会进入 sh 或者 bash 界面，使用 exit 退出。

改变文件或目录的owner
chown sb somefiles   must execute using superuser permission
改变文件或目录的group, to do that, you must be file or directory's owner
chgrp new_group some_file_or_dir



