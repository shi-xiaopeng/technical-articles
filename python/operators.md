```
a // b     a 除以 b 后向下取整，丢弃小数部分
a ** b     a 的 b 次方
a & b      如果a, b 均为 True, 结果为True. 对于整数，执行按位与操作
a | b      a or b, 对于整数，执行按位或操作
a ^ b      a 或 b 为 True (但不都为True), 结果为True. 对于整数，执行按位异或操作。

三元运算符
value = true-expr if condition else false-expr

list 的 in 操作相比 dict 和 set 要慢得多，因为list查找是线性查找，而dict 和 set 是基于 hash table, 可以瞬间完成。
列表合并：1. 可以使用（+）实现 ；2. 通过extend实现
使用 + 会生成一个新的list, 而 extend 是在原先的 list 上扩展

list 的 sort 方法可以实现就地排序
b.sort(key, reverse), key接受一个函数的引用，reverse 为 True/False

bisect.bisect(a, x) ->> return the index of x insert into sorted array a and array is still sorted after insertion.
bisect.insort(c, x) ->> insert x into c and c is still sorted.

enumerate函数
enumerate(collection) -->> 逐个返回序列的(index, value)元组。
可以使用enumerate得到一个 value <--> key 映射字典
mapping = dict((v, i) for i, v in enumerate(some_list))

sorted函数可以将任何序列返回一个新的有序列表：
sorted(set('this is just some string')) --> 得到一个由序列中唯一元素组成的有序列表。

zip 用于将多个序列中的元素配对，产生新的元组列表
seq1 = ['foo', 'bar', 'baz']
seq2 = ['one', 'two', 'three']
zip(seq1, seq2)
Out[44]: <zip at 0x10d78a648>
seq3 = list(zip(seq1, seq2))
seq3
Out[47]: [('foo', 'one'), ('bar', 'two'), ('baz', 'three')]
seq4, seq5 = zip(*seq3)
seq4
Out[49]: ('foo', 'bar', 'baz')
seq5
Out[50]: ('one', 'two', 'three')

reversed方法
In[52]: reversed(range(10))
Out[52]: <range_iterator at 0x10d8eb420>
In[53]: list(reversed(range(10)))
Out[53]: [9, 8, 7, 6, 5, 4, 3, 2, 1, 0]

dict 字典
判断是否存在某个键，使用 in
del  d[key] 语法 或 pop语法
d.keys(), d.values() 会产生键和值的迭代器
d1.update(d2) 字典合并，如果存在相同的键，会使用d2中的值作为键值。

可以使用dict 直接接受二元元组列表
mapping = dict(zip(key_list, value_list))
```
## 可以使用setdefault
```
words = ['apple', 'bat', 'bar', 'atom', 'book']
by_letter = {}
for word in words:
    letter = word[0]
    # if letter not in by_letter:
    #     by_letter[letter] = [word]
    # else:
    #     by_letter[letter].append(word)
    by_letter.setdefault(letter, []).append(word)
```

## defaultdict 类
```
from collections import defaultdict
words = ['apple', 'bat', 'bar', 'atom', 'book']
by_letter = defaultdict(list)
for word in words:
    by_letter[word[0]].append(word)
```
defaultdict 的初始化器只需要一个可调用的对象，并不需要一个明确的类型。如果你想要默认值为 4， 只需要传入一个能够返回4的函数即可：`count = defaultdict(lambda: 4)`

dict 的键必须是 不可变对象，即需要具备 可hash性（hashablity）, 通过 hash 函数可判断。
hash([1, 2]) ->会产生  unhashable type 的 TypeError。
如果要将列表当做键，最简单的方法是将其转换成元组。

### set 集合
可以看做是只有键没有值得字典。
```
创建方式：
In [18]: set([2, 2, 3, 3, 1])
Out[18]: {1, 2, 3}

In [19]: {2, 2, 3, 3, 1}
Out[19]: {1, 2, 3}

a.add(x)  集合添加x
a.remove(x)  从集合中删除x
a.union(b)  a | b   a, b 的并集 
a.intersection(b)  a & b   a, b 的交集
a.difference(b)   a - b  a, b 的差集
a.symmetric_difference(b) <=> a ^ b <=> (a - b) | (b - a) 
a.issubset(b)   a 是否是 b 的子集； a 是否包含于 b
a.isuperset(b)  a 是否包含 b
a.isdisjoint(b)  a, b 没有公共元素则为True.
```
#### 生成式和推导式
```
列表推导式：[ expr for val in collection if condition ]
字典推导式：{ key-expr : value-expr for value in collection if condition }
集合推导式：{ expr for value in collection if condition }

In [27]: strings = ['a', 'as', 'bat', 'car', 'dove', 'python']
In [28]: loc_mapping = {val : index for index, val in enumerate(strings)}
In [29]: loc_mapping
Out[29]: {'a': 0, 'as': 1, 'bat': 2, 'car': 3, 'dove': 4, 'python': 5}

上面的推导式要优于下面这种：
In [30]: loc_mapping = dict((val, idx) for idx, val in enumerate(strings))
```
#### 嵌套列表推导式
```
In [32]: some_tuples = [(1, 2, 3), (4, 5, 6), (7, 8, 9)]
In [33]: flattend = [x for tup in some_tuples for x in tup if x%2==0]
In [34]: flattend
Out[34]: [2, 4, 6, 8]

嵌套顺序：嵌套 for 循环中各个for的顺序是怎样的，嵌套推导式中的 for 表达式的顺序就是怎样的。

In [35]: [[x for x in tup]for tup in some_tuples]
Out[35]: [[1, 2, 3], [4, 5, 6], [7, 8, 9]]


