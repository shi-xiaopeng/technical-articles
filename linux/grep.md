`grep ":pipe" . -r -n`
-R, -r, --recursive  Read all  files  under  each  directory,  recursively; 递归地读取每个目录下的每个文件
-n, --line-number  Prefix  each  line of output with the 1-based line number within its input file.  (-n is specified by POSIX.)
给输出的每一行开头加上一个以 1 开头的匹配行在输入文件中的行号。
--color=auto  # 用颜色标记匹配的部分

grep ":pipe" . -r -l   # 找出当前目录以及子目录下包含 ":pipe" 的文件
-l, --files-with-matches  找到每个文件中的第一个匹配，然后停止，输出文件名
-L, --files-without-match  与-l 相反，输出没有查找到匹配的文件
-c --count   # 计算每个输入文件匹配行的数量
-i, --ignore-case
Ignore case distinctions in  both  the  PATTERN  and  the  input files. 
忽略匹配字符和输入文件的字符大小写。
-A 3   # 显示匹配结果之后的 3 行
-B 2   # 显示匹配结果之前的 2 行
-C 3   # 显示匹配结果之前之后各 3 行

grep -e ":pipe" . -r -l --exclude="*.pyc"  包含:pipe 且 文件后缀非 .pyc
--exclude=pattern 排除文件类型
--exclude-dir=DIR  Exclude  directories  matching  the  pattern  DIR from recursive searches. 将符合DIR模式的目录排除出查找范围。

-x, --line-regexp     # Select only those matches that exactly  match  the  whole  line.  匹配整行。

在grep 中使用 OR
<strong>grep -E 'word1|word2' FILENAME</strong>
### OR ###
<strong>egrep 'word1|word2' FILENAME</strong>
-E 表示使用 extended regular expression 扩展正则表达式
使用AND
	
<strong>grep 'word1' FILENAME | grep 'word2'</strong>
<strong>grep 'word1.*word2' FILENAME 
	
`<strong>grep '\<b.t\>' FILENAME</strong>`
`\<` 在单词的开始位置匹配空格字符串
`\>` 在单词的结尾匹配空格字符串

The caret ^ and the dollar sign $ are meta-characters that respectively
       match the empty string at the beginning and end of a line.

The Backslash Character and Special Expressions
       The  symbols  \<  and  \>  respectively  match  the empty string at the beginning and end of a word.  The symbol \b matches the empty string at the  edge  of a word, and \B matches the empty string provided it's not at the edge of a word.  The symbol \w is a synonym for [[:alnum:]]  and \W is a synonym for [^[:alnum:]].


