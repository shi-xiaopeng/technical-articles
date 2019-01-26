```
def isiterable(obj):
    try:
        iter(obj)
        return True
    except TypeError:
        return False

if not isinstance(x, list) and isiterable(x):
    x = list(x)

is 用来判断两个引用是否指向同一对象，
