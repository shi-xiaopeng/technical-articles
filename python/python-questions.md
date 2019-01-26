1. what is object reference in python?

Answer: An object reference is nothing more than a concrete representation of the object’s identity (the memory address where the object is stored).

2. what is ‘is’ operation mean?
Answer: 

3. what is ‘id()’ function mean?
Answer: Return the “identity” of an object. This is an integer which is guaranteed to be unique and constant for this object during its lifetime. Two objects with non-overlapping lifetimes may have the same id() value.
CPython implementation detail: This is the address of the object in memory.

4. how do I write a function with output parameters ( call for references )?
Answer: the best way is by returning a tuple with the results.
````
def func2(a, b):
    a = 'new-value'        # a and b are local names
    b = b + 1              # assigned to new objects
    return a, b            # return new values

x, y = 'old-value', 99
x, y = func2(x, y)
print(x, y)                # output: new-value 100

This is almost always the clearest solution.
````

5. python 中的参数传递方式是什么？
Answer: 
````
def func(a, b):
    a = 'new-value'        # a and b are local names
    b = b + 1              # assigned to new objects
    return a, b            # return new values

x, y = 'old-value', 99
func(x, y)
print(x, y)                # output: old-value 99

调用函数func时，内部相当于执行了下面 2 条语句:

a = x
b = y

所以，当 a = ’new _value’；b = b + 1; 时，只是修改了 局部变量 a、b 的值，外部变量 x、y 并未被改变。
函数执行结束后，局部变量 a、b 被销毁。
所以不管是可变对象还是不可变对象，参数传递方式都是 引用复制。
````
6. range 和 xrange 有何不同?
Answer: 在python2 中 已经不存在 range() 结果是 list, xrange() 结果 是生成器；在 python3 中 range() 吸收整合了 xrange 的功能，已经不存在 xrange 方法。
````
range 的写法
class linspace(collections.abc.Sequence):
    """linspace(start, stop, num) -> linspace object
    
    Return a virtual sequence of num numbers from start to stop (inclusive).
    
    If you need a half-open range, use linspace(start, stop, num+1)[:-1].
    """
    
    def __init__(self, start, stop, num):
        if not isinstance(num, numbers.Integral) or num <= 1:
            raise ValueError('num must be an integer > 1')
        self.start, self.stop, self.num = start, stop, num
        self.step = (stop-start)/(num-1)
    def __len__(self):
        return self.num
    def __getitem__(self, i):
        if isinstance(i, slice):
            return [self[x] for x in range(*i.indices(len(self)))]
        if i < 0:
            i = self.num + i
        if i >= self.num:
            raise IndexError('linspace object index out of range')
        if i == self.num-1:
            return self.stop
        return self.start + i*self.step
    def __repr__(self):
        return '{}({}, {}, {})'.format(type(self).__name__,
                                       self.start, self.stop, self.num)
    def __eq__(self, other):
        if not isinstance(other, linspace):
            return False
        return ((self.start, self.stop, self.num) ==
                (other.start, other.stop, other.num))
    def __ne__(self, other):
        return not self==other
    def __hash__(self):
        return hash((type(self), self.start, self.stop, self.num))  
````

9. 容器(container) , 可迭代对象( iterable ), 迭代器( iterator ) , 生成器( generator), 生成器表达式（generator expression), 列表推导式
Answer: 
容器: 只提供一个 __ contains __方法，只拥有 判断关键字 in or not in 容器的功能。
可迭代对象： 凡是可以返回一个迭代器的对象都是可迭代对象，可迭代对象实现了一个 __ iter __ 方法，该方法返回一个迭代器对象。
迭代器： 直接继承自 iterable， 他是一个带状态的对象，他能在你调用 next() 方法时返回容器中的下一个值，任何实现了 __ iter __ 和
 __ next __ （python 2.x 中是 next 方法）方法的对象都是迭代器。 
 __ iter __返回迭代器自身； __ next __ 返回容器中的下一个值，如果容器中没有
更多元素了，则抛出 StopIteration 异常。
生成器：一种特殊的迭代器，不需要 __ iter __, __ next __, 只需要一个 yield 关键字，生成器一定是迭代器，迭代器却不一定是生成器。生成器只是以一种
懒加载的模式生成值。
````
0  def fib():
1      prev, curr = 0, 1
2      while True:
3          yield curr
4          prev, curr = curr, curr + prev

5  f = fib()          #  并没有执行 fib() 中的任何语句，只是返回一个 generator 生成器对象，赋值给 f
6  a = next(f)     #  next(f), 转到开始执行 1,2,3 行，执行第 3 行后，转到继续执行第 6 行，给 a 赋值 1
7  b = next(f)     #  接着上次中断的地方，第3行，继续执行第 4 行 -> 第 2 行 -> 第 3 行 -> 返回curr -> 继续执行第 7 行 给 b 赋值

列表推导式：结果是列表 [it for it in range(5)] => [0, 1, 2, 3, 4]
生成器表达式： 结果返回一个 生成器对象  （it for it in range(5)）=> generator type
````
9. 什么是装饰器，用法和场景是什么？
Answer: 
````
1 @hello
2 def foo():
3    print "i am foo"

被解释成了：

1 foo = hello(foo)
比如：多个decorator

1 @decorator_one
2 @decorator_two
3 def func():
4     pass

相当于：

1 func = decorator_one(decorator_two(func))

比如：带参数的decorator：

1 @decorator(arg1, arg2)
2 def func():
3     pass

相当于：

1 func = decorator(arg1,arg2)(func)

这意味着decorator(arg1, arg2)这个函数需要返回一个“真正的decorator”。
from functools import wraps
def logged(func):
    @wraps(func)
    def with_logging(*args, **kwargs):
        print func.__name__      # 输出 'f'
        print func.__doc__       # 输出 'does some math'
        return func(*args, **kwargs)
    return with_logging

@logged
def f(x):
   """does some math"""
   return x + x * x


class myDecorator:
    def __init__(self, fn):
        print("inside myDecorator.__init__()")
        self.fn = fn

    def __call__(self):
        self.fn()
        print("inside myDecorator.__call__()")


@myDecorator
def aFunction():
    print("inside aFunction()")

类装饰器@myDecorator 首先会调用 __init__方法，当 调用 aFunction()时，会调用 __call__() 方法。
````
10. python 2.x 与 python 3.x 的主要区别有哪些？
Answer: 整数除法，9 / 4 => 2  (in 2.x)   2.25 (in 3.x) 
print 函数  statement in 2.x and a function in 3.x

unicode, In python 2.x we have ASCII str() type, sepatate from unicode() and no byte type;
In python 3.x we finally have unicode(utf-8) str , and two byte class byte , bytearray

handling exceptions
in python 2.x  try….except Error, name: print name
in python 3.x try… except Error as name: print(name)
 
Iterator.next() : in python 2.x next(), .next() both available; In python 3.x only next() available.

input return type: in python 2 the return type depends on the input type, in python 3 the return type is always str.

11. 你调试代码的方法有哪些？
Answer: pdb, pycharm 断点调试

12. 什么是 GIL ?
Answer: 首先GIL 不是 python 的特性，而是实现python 解析器 cpython时引入的一个概念。GIL 全称 Global Interpreter Lock
In CPython, the global interpreter lock, or GIL, is a mutex that prevents multiple native threads from executing Python bytecodes at once. This lock is necessary mainly because CPython’s memory management is not thread-safe. (However, since the GIL exists, other features have grown to depend on the guarantees that it enforces.)
* 因为GIL的存在，只有IO Bound场景下得多线程会得到较好的性能
* 如果对并行计算性能较高的程序可以考虑把核心部分也成C模块，或者索性用其他语言实现
The most popular way is to use a multi-processing approach where you use multiple processes instead of threads. Each Python process gets its own Python interpreter and memory space so the GIL won’t be a problem.

GIL最大的问题就是Python的多线程程序并不能利用多核CPU的优势 （比如一个使用了多个线程的计算密集型程序只会在一个单CPU上面运行）。GIL只会影响到那些严重依赖CPU的程序（比如计算型的）。 如果你的程序大部分只会涉及到I/O，比如网络交互，那么使用多线程就很合适， 因为它们大部分时间都在等待。而对于依赖CPU的程序，你需要弄清楚执行的计算的特点。 例如，优化底层算法要比使用多线程运行快得多。 类似的，由于Python是解释执行的，如果你将那些性能瓶颈代码移到一个C语言扩展模块中， 速度也会提升的很快。如果你要操作数组，那么使用NumPy这样的扩展会非常的高效。

13. how python memory management
Answer: Python uses reference counting for memory management. It means that objects created in Python have a reference count variable that keeps track of the number of references that point to the object. When this count reaches zero, the memory occupied by the object is released.

The GIL, although used by interpreters for other languages like Ruby, is not the only solution to this problem. Some languages avoid the requirement of a GIL for thread-safe memory management by using approaches other than reference counting, such as garbage collection.

On the other hand, this means that those languages often have to compensate for the loss of single threaded performance benefits of a GIL by adding other performance boosting features like JIT compilers.

从三个方面来说,一对象的引用计数机制,二垃圾回收机制,三内存池机制

一、对象的引用计数机制

Python内部使用引用计数，来保持追踪内存中的对象，所有对象都有引用计数。

引用计数增加的情况：

1，一个对象分配一个新名称

2，将其放入一个容器中（如列表、元组或字典）

引用计数减少的情况：

1，使用del语句对对象别名显示的销毁

2，引用超出作用域或被重新赋值

sys.getrefcount( )函数可以获得对象的当前引用计数

多数情况下，引用计数比你猜测得要大得多。对于不可变数据（如数字和字符串），解释器会在程序的不同部分共享内存，以便节约内存。

二、垃圾回收

1，当一个对象的引用计数归零时，它将被垃圾收集机制处理掉。

2，当两个对象a和b相互引用时，del语句可以减少a和b的引用计数，并销毁用于引用底层对象的名称。然而由于每个对象都包含一个对其他对象的应用，因此引用计数不会归零，对象也不会销毁。（从而导致内存泄露）。为解决这一问题，解释器会定期执行一个循环检测器，搜索不可访问对象的循环并删除它们。

三、内存池机制

Python提供了对内存的垃圾收集机制，但是它将不用的内存放到内存池而不是返回给操作系统。

1，Pymalloc机制。为了加速Python的执行效率，Python引入了一个内存池机制，用于管理对小块内存的申请和释放。

2，Python中所有小于256个字节的对象都使用pymalloc实现的分配器，而大的对象则使用系统的malloc。

3，对于Python对象，如整数，浮点数和List，都有其独立的私有内存池，对象间不共享他们的内存池。也就是说如果你分配又释放了大量的整数，用于缓存这些整数的内存就不能再分配给浮点数。


垃圾回收(Garbage Collection)python提供了del方法来删除某个变量，它的作用是让某个对象引用数减少1。当某个对象引用数变为0时并不是直接将它从内存空间中清除掉，而是采用垃圾回收机制gc模块，当这些引用数为0的变量规模达到一定规模，就自动启动垃圾回收，将那些引用数为0的对象所占的内存空间释放。这里gc模块采用了分代回收方法，将对象根据存活的时间分为三“代”，所有新建的对象都是0代，当0代对象经过一次自动垃圾回收，没有被释放的对象会被归入1代，同理1代归入2代。每次当0代对象中引用数为0的对象超过700个时，启动一次0代对象扫描垃圾回收，经过10次的0代回收，就进行一次0代和1代回收，1代回收次数超过10次，就会进行一次0代、1代和2代回收。而这里的几个值是通过查询get_threshold()返回(700,10,10)得到的。此外，gc模块还提供了手动回收的函数，即gc.collect()。在人工调用gc.collect()的时候会有一个返回值，这个返回值就是这一次扫描unreachable的对象个数.

14. 各种操作对变量地址的改变 ？
Answer： 对于不可变对象的改变，赋值、加减乘除时，实际上导致变量指向的对象发生了改变，已经不是原来的那个对象了，并不是通过这个变量来改变它指向的对象的值。
增加减少list、dict对象内容是在对对象本身进行操作，此时变量的指向并没有改变，它作为对象的一个别名/引用，通过操纵变量来改变对应的对象内容。但是一旦将变量赋值到别的地方去，那么变量地址就改变了。
但是实际使用中，可能需要的是将里面的内容给复制出来到一个新的地址空间，这里可以使用python的copy模块，copy模块分为两种拷贝，一种是浅拷贝，一种是深拷贝。假设处理一个list对象，浅拷贝调用函数copy.copy()，产生了一块新的内存来存放list中的每个元素引用，也就是说每个元素的跟原来list中元素地址是一样的。所以从下面例子中可看出当原list中要是包含list对象，分别在a和b对list元素做操作时，两边都受到了影响。此外，通过b=list(a)来对变量b赋值时，也跟浅拷贝的效果一样。
而深拷贝则调用copy.deepcopy()，它将原list中每个元素都复制了值到新的内存中去了，因此跟原来的元素地址不相同，那么再对a和b的元素做操作，就是互相不影响了。
15. 什么是元类（meta_class)?
Answer: Everything, and I mean everything, is an object in Python. That includes ints, strings, functions and classes. 
So, a metaclass is just the stuff that creates class objects.

16. python 的交叉引用导入循环问题？
Answer: 当A module 全局import B module 变量， B module又全局import A module 变量 , 就会发生无法导入问题。只需要把其中一个变成局部import,
或者不要放在文件开头，需要了再引用。

17. with statement 有什么好处，常用于什么地方？
Answer: 
要使用 with 语句，首先要明白上下文管理器这一概念。有了上下文管理器，with 语句才能工作。
下面是一组与上下文管理器和with 语句有关的概念。
上下文管理协议（Context Management Protocol）：包含方法 __enter__() 和 __exit__()，支持
该协议的对象要实现这两个方法。
上下文管理器（Context Manager）：支持上下文管理协议的对象，这种对象实现了
__enter__() 和 __exit__() 方法。上下文管理器定义执行 with 语句时要建立的运行时上下文，
负责执行 with 语句块上下文中的进入与退出操作。通常使用 with 语句调用上下文管理器，
也可以通过直接调用其方法来使用。
运行时上下文（runtime context）：由上下文管理器创建，通过上下文管理器的 __enter__() 和
__exit__() 方法实现，__enter__() 方法在语句体执行之前进入运行时上下文，__exit__() 在
语句体执行完后从运行时上下文退出。with 语句支持运行时上下文这一概念。
上下文表达式（Context Expression）：with 语句中跟在关键字 with 之后的表达式，该表达式
要返回一个上下文管理器对象。
语句体（with-body）：with 语句包裹起来的代码块，在执行语句体之前会调用上下文管
理器的 __enter__() 方法，执行完语句体之后会执行 __exit__() 方法。
with 语句的语法格式如下：
清单 1. with 语句的语法格式
````
1 with context_expression [as target(s)]:
2     with-body
````

这里 context_expression 要返回一个上下文管理器对象，该对象并不赋值给 as 子句中的 target(s) ，如果指定了 as 子句的话，会将上下文管理器的 __enter__() 方法的返回值赋值给 target(s)。target(s) 可以是单个变量，或者由“()”括起来的元组（不能是仅仅由“,”分隔的变量列表，必须加“()”）。
Python 对一些内建对象进行改进，加入了对上下文管理器的支持，可以用于 with 语句中，比如可以自动关闭文件、线程锁的自动获取和释放等。

18. inspect 模块有什么用？
Answer: There are four main kinds of services provided by this module: type checking, getting source code, inspecting classes and functions, and examining the interpreter stack.
````
活用 inspect 來達到使用 annotation 檢查型態的功能
>>> from functools import wraps
>>> def checked(func):
...     ann = func.__annotations__
...     sig = inspect.signature(func)
...     @wraps(func)
...     def wrapper(*args, **kwargs):
...         bound = sig.bind(*args, **kwargs)
...         for name, val in bound.arguments.items():
...             if name in ann:
...                 assert isinstance(val, ann[name]), \
...                     f'Expected {ann[name]}'
...         return func(*args, **kwargs)
...     return wrapper
...
>>> @checked
... def gcd(a: int, b: int) -> int:
...     while b:
...         a, b = b, a % b
...     return a
...
>>> gcd(2.7, 3.6)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "<stdin>", line 9, in wrapper
AssertionError: Expected <class 'int'>
>>> gcd(27, 36)
9
>>>
````
19. python 进程间通信的方式有哪些？
Answer: 

20. __init__, __new__, __call__
Answer: 

21. [x for x in range(9)], (x for x in range(9)),  {x/2 for x in range(9)}, {x: x/2 for x in range(9)}
Answer: 

22. 如何使类实例响应没有的方法？
Answer: __getattr__, 返回一个默认方法

23. 问题：一个包里有三个模块，mod1.py ,  mod2.py ,  mod3.py ，但使用 from demopack import * 导入模块时，如何保证只有 mod1 、 mod3 被导入了
Answer: 增加 __init__.py 文件，并在文件中增加：__all__ = [ ‘mod1’, ‘mod2’ ]

24. @property, @staticmethod, @classmethod
Answer: 
````
class Rectangle:

    def __init__(self, width, height):
        self.__width = width
        self.__height = height

    @property
    def height(self):
        return self.__height

    @height.setter
    def height(self, height):
        self.__height = height

    @height.deleter
    def height(self):
        del self.__height
        
    @property
    def area(self):
        return self.width * self.height

    # area = property(area)
````

25. 什么是python 协程？
Tornado中推荐使用 协程 写异步代码. 协程使用了Python的 yield 关键字代替链式回调来将程序挂起和恢复执行。
Tornado中所有的协程使用明确的上下文切换,并被称为异步函数。使用协程几乎像写同步代码一样简单, 并且不需要浪费额外的线程. 它们还通过减少上下文切换来 使并发编程更简单.

