echo *  # 当前目录的文件名
echo d* # 以 d 开头的文件
echo \*s  # 以 s 结尾的文件
echo [[:upper:]]\*   # 以大写字母开头的 file 
echo /usr/*/share  # 找出 /usr 下所有文件中的 share 目录
echo ~  # 用户根目录
echo ~foo # 找出 /home/foo
echo Five divided by two equals $((5/2))  
\# Five divided by two equals 2
echo Front-{A,B,C}-Back  #  打印出 Front-A-Back Front-B-Back Front-C-Back
echo Number_{1..5}   
\# 打印出 Number_1 Number_2 Number_3 Number_4 Number_5
echo {Z..A}  
\# 打印 Z Y X W V U T S R Q P O N M L K J I H G F E D C B A
echo $USER   # 打印出当前用户名
printenv | less   # 输出当前环境变量，输出到 less 中
echo $(ls)    # 输出
ls -l $(which cp)   # 输出 cp 命令文件的信息
```
$ file $(ls /usr/bin/* | grep bin/zip)   
# 输出
/usr/bin/zip:            Mach-O 64-bit executable x86_64
/usr/bin/zipcloak:       Mach-O 64-bit executable x86_64
/usr/bin/zipdetails:     Perl script text executable
/usr/bin/zipdetails5.18: Perl script text executable
/usr/bin/zipgrep:        POSIX shell script text executable, ASCII text
/usr/bin/zipinfo:        Mach-O 64-bit executable x86_64
/usr/bin/zipnote:        Mach-O 64-bit executable x86_64
/usr/bin/zipsplit:       Mach-O 64-bit executable x86_64
```
ls -l \`which cp\`  等价于  ls -l $(which cp) 
```
[me@linuxbox me]$ echo text ~/*.txt {a,b} $(echo foo) $((2+2)) $USER
text /home/me/ls-output.txt a b foo 4 me
[me@linuxbox me]$ echo "text ~/*.txt {a,b} $(echo foo) $((2+2)) $USER"
text ~/*.txt {a,b} foo 4 me
[me@linuxbox me]$ echo 'text ~/*.txt {a,b} $(echo foo) $((2+2)) $USER'
text ~/*.txt {a,b} $(echo foo) $((2+2)) $USER
```
反斜杠作为 escape， 用于“$”, “!”, “&”, 还可作为换行标识
\n 换行；\t TAB符；\a Alert；\\\ 输出反斜杠

ls > list_file.txt   每次执行，覆盖原来的内容 overwrite
ls >> list_file.txt  每次执行，末尾增加 append

sort < list_file.txt   文件内容作为输入
sort < list_file.txt >sorted_list_file.txt    文件输入 并输出到文件

pipelines:
ls -l | less
ls -lt | head    # 显示当前目录10个最新的文件
du | sort -nr   # 计算当前目录中的目录和文件大小 并 从大到小排序
find . -type f -print | wc -l  # 找出当前目录及其子目录中的文件总数
tar tzvf name_of_file.tar.gz | less   # 查看 .tar.gz or .tgz 格式文件


