这是我想到的第一种方法，比较笨一点，完全用的是高中数学组合知识。每一层的数字单独生成，与上一层没有关联。`get_item(n, r)`方法运用递归，每一个数字由前一个数字乘上 `(n - r + 1) / r`得到下一个数字
```
# _*_ coding: utf-8 _*_

def yh_tri():
    # n 表示层，层数以 0 开始
    n = 0
    while True:
        if n == 0:
            yield [1]
        elif n == 1:
            yield [1, 1]
        else:
            yield [int(get_item(n, r)) for r in range(n + 1)]
        n = n + 1
# 获得第 n 层的第 r 个数字， r 从 0 开始算
def get_item(n, r):
    if r == 0:
        return 1
    else:
        return get_item(n, r - 1) * (n - r + 1) / r
```
我看到一下其他人的实现方法，发现大部分人使用上一层的数据产生下一层的数据，顺着这个思路我重新实现了一遍。改进之后，我不得不承认，这个更简单。
```
# _*_ coding: utf-8 _*_
def yh_tri():
    L = []
    while True:
        # 生成下一层数据（除第 1 位数之外），赋值给 L (第 2 步)
        L = [L[i] + L[i + 1] for i in range(len(L) - 1)]
        # 插入第 1 位数字 1，构成完整的下一层数据 (第 3 步)
        L.insert(0, 1)
        yield L
        # 末尾补位，为生成下一层数据做准备（第 1 步)
        L.append(0)

# end

# test
n = 1
for item in yh_tri():
    print(item)
    if n == 10
        break
    n = n + 1

# test end
```
=========更新==========
我又发现一个更牛逼的写法，http://codecloud.net/111788.html 中说是在评论区找到的，但是我去找了一下并没有找到。
```
def triangles():
    N = [1]
    while True:
        yield N
        N.append(0)
        N = [N[r - 1] + N[r] for r in range(len(N))]
```
这里他使用了 N[ -1 ] + N[ 0 ] 表示新的第 0 位，就不需要前面再插入insert了
