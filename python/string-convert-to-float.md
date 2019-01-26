这是把类似于 `'123.456'` 的字符串转换成浮点数 `123.456` 
```
def str2float(s):
    # 把小数点后面的数字转化成 0.xxx 的值，t 为小数的位数
    def decimalize(n, t):
        while t > 0:
            n = n / 10
            t = t - 1
        return n
    # 获得小数点的位置
    pos = s.find('.')
    if pos == -1:
        return s
    else:
        return int(s[:pos]) + decimalize(int(s[pos + 1:]), len(s[pos + 1:]))
```
