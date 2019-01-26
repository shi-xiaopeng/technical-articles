wildcard
\*  # 匹配任意字符，不限长度
? # 匹配任一字符，长度为1
[characters]  # 字符集合，匹配此集合中任一字符
[:alnum:]  # 字母和数字
[:alpha:]   # 字母
[:digit:]    # 数字
[:upper:]   # 大些字母
[:lower:]    # 小写字母
[!characters]  # 匹配不在集合中的任一字符

CP：
cp file1 file2  # 复制文件1的内容到文件2。 如果文件2不存在，创建。否则，文件2会被文件1静默覆盖。
cp -i file1 file2  # 同上，-i (interactive). 如果文件2存在，在文件2被覆盖之前会弹出提示
cp file1 file2 dir1  # 复制文件1和2到dir1目录下，名字不变
cp -R dir1 dir2  # 复制dir1下的内容到dir2下。如果dir2 不存在，创建。否则会在dir2下创建一个名为dir1的子目录，并将内容存入这个子目录下。

MV
mv file1 file2  # 如果file2不存在，file1会被重命名为file2. 如果file2存在，file2的内容会被静默替换成file1.
mv -i file1 file2  # 同上，-i (interactive)。当file2要被覆盖时，会提示。
mv file1 file2 file3 dir1  # 移动file 1, 2, 3到dir1目录下。如果dir1不存在，mv 会报错停止。
mv dir1 dir2  # 如果dir2不存在，dir1会被重命名为dir2；如果存在，dir1会被移动到dir2之下。

RM
rm file1 file2  # 删除file1 file2
rm -i file1 file2  # 同上，不同之处是，删除每个文件时会提示
rm -r dir1 dir2  # 递归删除dir1,dir2 下的所有文件, 连同目录本身
rm -d dir1 dir2   # 删除目录dir1 dir2, 只限空目录
由于Linux没有删除恢复命令，一旦使用rm 删除文件，文件就无法找回。所以对rm 要特别小心，特别是连同统配符使用时。一个比较好的做法是：使用ls 代替rm 命令，查看通配符所匹配的文件，确认无误后再使用把ls 替换回 rm。

mkdir
mkdir dir1 dir2 ...  #   创建目录
