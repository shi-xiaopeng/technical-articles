最近在学廖雪峰的python教程，这是filter一节中的问题
回数是指从左向右读和从右向左读都是一样的数，例如12321，909之类的数字。为了得到回文数，可以先写一个回文数判断方法is_palindrome(n)，然后使用filter方法过滤出序列中的回文数。
```
def is_palindrome(n):
    origin = str(n)
    return origin == origin[::-1]
```
    根据回文数的定义正序与反序一样的就是回文数 (当然首先是数字，简单起见判断条件先不写)。
这里难点是怎么得到一个数字的反序，数字不方便操作，首先转成 string。字符序列的反转，刚开始我以为像Java一样 会是string的一个方法，去找文档结果没有这个方法，后来想到切片操作里的step,可不可以是负数。在交互环境里试了一下，`'1234567'[::-1]` 回车，结果是`'7654321'`,那就成了。

我很好奇评论区里有没有这个解法，前几个都是一大坨一大坨的，略过，然后发现有个评论贴出了这个解法。。。唉，这个解法或许并不是什么秘密，可能只有初学者才会认为它是秘密吧。Anyway, 自己想出这个还是挺不错的。

```
# test
output = filter(is_palindrome, range(1, 1000))
print(list(output))
```