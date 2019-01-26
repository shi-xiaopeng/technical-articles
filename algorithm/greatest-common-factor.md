最近在看数学桥，里面讲到寻找两个数的最大公因数的一个方法：长除法。
下面是书中提供的证明过程，很有意思。

原理如下：a, b 为两个正整数，求 a  b 的最大公约数。
假设 a > b,  则 a 可以表示为 a = b * p + r ，其中 r 为余数，r < b
假如 n 为 a, b 的一个公因数，那么 a/n = (b * p) /n + r/n
其中第一项，第二项为整数，所以第三项也必为整数；
此式表明，a, b 的公因数也是 r 的因数。

现假设 a, b 的最大公因数为 N,  则a, b, r 可以表示为 a = NA, b = NB, r = NR
则 a = b * p + r 可化为 A = B * p + R  , 其中 A, B 互素
现在假设，B, R 之间存在大于 1 的公因数 m (m > 1) , 
A/m = B * p / m + R/m，
由于A, B 互素，A/m 一定为分数，而第二项，第三项都为整数，矛盾。
所以，B, R 之间不存在大于 1 的公因数 m。也就是，B , R 也互素。

也就是说 a, b 之间的最大公因数 N，也是 b, r 之间的最大公因数。
如果要计算 a , b 的最大公因数，只要计算 b, r 之间的最大公因数就可以了。

````
python 代码实现如下：
def greatest_common_factor(a, b):
        big = max(a, b)
        small = min(a, b)
        if small == 0:
            return big
        elif small == 1:
            return 1
        else:
            return greatest_common_factor(small, big%small)
```` 
这里是递归方法，算法时间复杂度为 O(lg n).
