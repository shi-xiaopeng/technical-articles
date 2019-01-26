#### sys.getsizeof(object[, default]):
Return the size of an object in __bytes__. The object can be any type of object. All built-in objects will return correct results, but this does not have to hold true for third-party extensions as it is implementation specific.
The `default` argument allows to define a value which will be returned if the object type does not provide means to retrieve the size and would cause a _`TypeError`_.
`getsizeof` calls the object’s `__sizeof__` method and adds an additional garbage collector overhead if the object is managed by the garbage collector.
```
import sys
x = 2
sys.getsizeof(x)
ls = []
sys.getsizeof(ls)
```

