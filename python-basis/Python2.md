

## Python之什么是函数

我们知道圆的面积计算公式为：

    S = πr²

当我们知道半径r的值时，就可以根据公式计算出面积。假设我们需要计算3个不同大小的圆的面积：

    r1 = 12.34
    r2 = 9.08
    r3 = 73.1
    s1 = 3.14 * r1 * r1
    s2 = 3.14 * r2 * r2
    s3 = 3.14 * r3 * r3

当代码出现有规律的重复的时候，你就需要当心了，每次写3.14 * x * x不仅很麻烦，而且，如果要把3.14改成3.14159265359的时候，得全部替换。

有了函数，我们就不再每次写s = 3.14 * x * x，而是写成更有意义的函数调用 `s = area_of_circle(x)`，而函数 area_of_circle 本身只需要写一次，就可以多次调用。

抽象是数学中非常常见的概念。举个例子：

计算数列的和，比如：1 + 2 + 3 + ... + 100，写起来十分不方便，于是数学家发明了求和符号∑，可以把1 + 2 + 3 + ... + 100记作：

    100
    ∑n
    n=1
    
这种抽象记法非常强大，因为我们看到∑就可以理解成求和，而不是还原成低级的加法运算。

而且，这种抽象记法是可扩展的，比如：

100
∑(n²+1)
n=1

还原成加法运算就变成了：

    (1 x 1 + 1) + (2 x 2 + 1) + (3 x 3 + 1) + ... + (100 x 100 + 1)

可见，借助抽象，我们才能不关心底层的具体计算过程，而直接在更高的层次上思考问题。

写计算机程序也是一样，函数就是最基本的一种代码抽象的方式。

Python不但能非常灵活地定义函数，而且本身内置了很多有用的函数，可以直接调用。

## Python之调用函数

Python内置了很多有用的函数，我们可以直接调用。

要调用一个函数，需要知道函数的名称和参数，比如求绝对值的函数 abs，它接收一个参数。

    可以直接从Python的官方网站查看文档：
    http://docs.python.org/2/library/functions.html#abs

也可以在交互式命令行通过 help(abs) 查看abs函数的帮助信息。
调用 abs 函数：

    >>> abs(100)
    100
    >>> abs(-20)
    20
    >>> abs(12.34)
    12.34

调用函数的时候，如果传入的参数数量不对，会报TypeError的错误，并且Python会明确地告诉你：abs()有且仅有1个参数，但给出了两个：

    >>> abs(1, 2)
    Traceback (most recent call last):
      File "<stdin>", line 1, in <module>
    TypeError: abs() takes exactly one argument (2 given)
    
如果传入的参数数量是对的，但参数类型不能被函数所接受，也会报TypeError的错误，并且给出错误信息：str是错误的参数类型：

    >>> abs('a')
    Traceback (most recent call last):
      File "<stdin>", line 1, in <module>
    TypeError: bad operand type for abs(): 'str'

而比较函数 cmp(x, y) 就需要两个参数，如果 x<y，返回 -1，如果 x==y，返回 0，如果 x>y，返回 1：

    >>> cmp(1, 2)
    -1
    >>> cmp(2, 1)
    1
    >>> cmp(3, 3)
    0
    
Python内置的常用函数还包括数据类型转换函数，比如   int()函数可以把其他数据类型转换为整数：

    >>> int('123')
    123
    >>> int(12.34)
    12
    
str()函数把其他类型转换成 str：

    >>> str(123)
    '123'
    >>> str(1.23)
    '1.23'

**任务**

sum()函数接受一个list作为参数，并返回list所有元素之和。请计算 1*1 + 2*2 + 3*3 + ... + 100*100。

    L = [x*x for x in range(1,101)]
    print sum(L)


## Python之编写函数
  在Python中，定义一个函数要使用 def 语句，依次写出函数名、括号、括号中的参数和冒号:，然后，在缩进块中编写函数体，函数的返回值用 return 语句返回。
 我们以自定义一个求绝对值的 my_abs 函数为例：

     def my_abs(x):
    if x >= 0:
    return x
    else:
    return -x

请注意，函数体内部的语句在执行时，一旦执行到return时，函数就执行完毕，并将结果返回。因此，函数内部通过条件判断和循环可以实现非常复杂的逻辑。

如果没有return语句，函数执行完毕后也会返回结果，只是结果为 None。

return None可以简写为return。

**任务**

请定义一个 square_of_sum 函数，它接受一个list，返回list中每个元素平方的和。

    def square_of_sum(L):
    return sum(num*num for num in L)
    
    print square_of_sum([1, 2, 3, 4, 5])
    print square_of_sum([-5, 0, 5, 15, 25])


## Python函数之返回多值

函数可以返回多个值吗？答案是肯定的。

比如在游戏中经常需要从一个点移动到另一个点，给出坐标、位移和角度，就可以计算出新的坐标：

# math包提供了sin()和 cos()函数，我们先用import引用它：

    import math
    def move(x, y, step, angle):
    nx = x + step * math.cos(angle)
    ny = y - step * math.sin(angle)
    return nx, ny

这样我们就可以同时获得返回值：

    >>> x, y = move(100, 100, 60, math.pi / 6)
    >>> print x, y
    151.961524227 70.0

但其实这只是一种假象，Python函数返回的仍然是单一值：

    >>> r = move(100, 100, 60, math.pi / 6)
    >>> print r
    (151.96152422706632, 70.0)

用print打印返回结果，原来返回值是一个tuple！

但是，在语法上，返回一个tuple可以省略括号，而多个变量可以同时接收一个tuple，按位置赋给对应的值，所以，Python的函数返回多值其实就是返回一个tuple，但写起来更方便


Python之递归函数

在函数内部，可以调用其他函数。如果一个函数在内部调用自身本身，这个函数就是递归函数。

举个例子，我们来计算阶乘 n! = 1 * 2 * 3 * ... * n，用函数 fact(n)表示，可以看出：

    fact(n) = n! = 1 * 2 * 3 * ... * (n-1) * n = (n-1)! * n = fact(n-1) * n


所以，fact(n)可以表示为 n * fact(n-1)，只有n=1时需要特殊处理。

于是，fact(n)用递归的方式写出来就是：
    def fact(n):
    if n==1:
    return 1
    return n * fact(n - 1)
    
上面就是一个递归函数。可以试试：

    >>> fact(1)
    1
    >>> fact(5)
    120
    >>> fact(100)
    93326215443944152681699238856266700490715968264381621468592963895217599993229915608941463976156518286253697920827223758251185210916864000000000000000000000000L


如果我们计算fact(5)，可以根据函数定义看到计算过程如下：

    ===> fact(5)
    ===> 5 * fact(4)
    ===> 5 * (4 * fact(3))
    ===> 5 * (4 * (3 * fact(2)))
    ===> 5 * (4 * (3 * (2 * fact(1))))
    ===> 5 * (4 * (3 * (2 * 1)))
    ===> 5 * (4 * (3 * 2))
    ===> 5 * (4 * 6)
    ===> 5 * 24
    ===> 120


递归函数的优点是定义简单，逻辑清晰。理论上，所有的递归函数都可以写成循环的方式，但循环的逻辑不如递归清晰。

使用递归函数需要注意防止栈溢出。在计算机中，函数调用是通过栈（stack）这种数据结构实现的，每当进入一个函数调用，栈就会加一层栈帧，每当函数返回，栈就会减一层栈帧。由于栈的大小不是无限的，所以，递归调用的次数过多，会导致栈溢出。可以试试计算 fact(10000)。

## Python之定义默认参数

定义函数的时候，还可以有默认参数。

例如Python自带的 int() 函数，其实就有两个参数，我们既可以传一个参数，又可以传两个参数：

    >>> int('123')
    123
    >>> int('123', 8)
    83
    

int()函数的第二个参数是转换进制，如果不传，默认是十进制 (base=10)，如果传了，就用传入的参数。


可见，**函数的默认参数的作用是简化调用**，你只需要把必须的参数传进去。但是在需要的时候，又可以传入额外的参数来覆盖默认参数值。

我们来定义一个计算 x 的N次方的函数:

    def power(x, n):
    s = 1
    while n > 0:
    n = n - 1
    s = s * x
    return s

假设计算平方的次数最多，我们就可以把 n 的默认值设定为 2：

    def power(x, n=2):
    s = 1
    while n > 0:
    n = n - 1
    s = s * x
    return s

这样一来，计算平方就不需要传入两个参数了：
    >>> power(5)
    25
    
由于函数的参数按从左到右的顺序匹配，所以默认参数只能定义在必需参数的后面：
    
    # OK:
    def fn1(a, b=1, c=2):
    pass
    # Error:
    def fn2(a=1, b):
    pass
    
## Python之定义可变参数

如果想让一个函数能接受任意个参数，我们就可以定义一个可变参数：

    def fn(*args):
    print args

可变参数的名字前面有个 * 号，我们可以传入0个、1个或多个参数给可变参数：

    >>> fn()
    ()
    >>> fn('a')
    ('a',)
    >>> fn('a', 'b')
    ('a', 'b')
    >>> fn('a', 'b', 'c')
    ('a', 'b', 'c')

可变参数也不是很神秘，Python解释器会把传入的一组参数组装成一个tuple传递给可变参数，因此，在函数内部，直接把变量 args 看成一个 tuple 就好了。

定义可变参数的目的也是为了简化调用。假设我们要计算任意个数的平均值，就可以定义一个可变参数：

    def average(*args):
    ...

这样，在调用的时候，可以这样写：

    >>> average()
    0
    >>> average(1, 2)
    1.5
    >>> average(1, 2, 2, 3, 4)
    2.4




## 对list进行切片

取一个list的部分元素是非常常见的操作。比如，一个list如下：
    
    >>> L = ['Adam', 'Lisa', 'Bart', 'Paul']

取前3个元素，应该怎么做？

笨办法：

    >>> [L[0], L[1], L[2]]
    ['Adam', 'Lisa', 'Bart']

之所以是笨办法是因为扩展一下，取前N个元素就没辙了。

取前N个元素，也就是索引为0-(N-1)的元素，可以用循环：

    >>> r = []
    >>> n = 3
    >>> for i in range(n):
    ... r.append(L[i])
    ... 
    >>> r
    ['Adam', 'Lisa', 'Bart']


对这种经常取指定索引范围的操作，用循环十分繁琐，因此，Python提供了切片（Slice）操作符，能大大简化这种操作。

对应上面的问题，取前3个元素，用一行代码就可以完成切片：

    >>> L[0:3]
    ['Adam', 'Lisa', 'Bart']


L[0:3]表示，从索引0开始取，直到索引3为止，但不包括索引3。即索引0，1，2，正好是3个元素。

如果第一个索引是0，还可以省略：

    >>> L[:3]
    ['Adam', 'Lisa', 'Bart']

也可以从索引1开始，取出2个元素出来：

    >>> L[1:3]
    ['Lisa', 'Bart']


只用一个 : ，表示从头到尾：


    >>> L[:]
    ['Adam', 'Lisa', 'Bart', 'Paul']

因此，L[:]实际上复制出了一个新list。

切片操作还可以指定第三个参数：


    >>> L[::2]
    ['Adam', 'Bart']
    
第三个参数表示每N个取一个，上面的 L[::2] 会每两个元素取出一个来，也就是隔一个取一个。

把list换成tuple，切片操作完全相同，只是切片的结果也变成了tuple。



## 倒序切片

对于list，既然Python支持L[-1]取倒数第一个元素，那么它同样支持倒数切片，试试


    >>> L = ['Adam', 'Lisa', 'Bart', 'Paul']
    
    >>> L[-2:]
    ['Bart', 'Paul']
    
    >>> L[:-2]
    ['Adam', 'Lisa']
    
    >>> L[-3:-1]
    ['Lisa', 'Bart']
    
    >>> L[-4:-1:2]
    ['Adam', 'Bart']


记住倒数第一个元素的索引是-1。倒序切片包含起始索引，不包含结束索引。

**任务**

利用倒序切片对 1 - 100 的数列取出：

* 最后10个数；

* 最后10个5的倍数。

    L = range(1, 101)
    print L[-10:]
    print L[4::5][-10:]





## 对字符串切片

字符串 'xxx'和 Unicode字符串 u'xxx'也可以看成是一种list，每个元素就是一个字符。因此，字符串也可以用切片操作，只是操作结果仍是字符串：

    >>> 'ABCDEFG'[:3]
    'ABC'
    >>> 'ABCDEFG'[-3:]
    'EFG'
    >>> 'ABCDEFG'[::2]
    'ACEG'
    

在很多编程语言中，针对字符串提供了很多各种截取函数，其实目的就是对字符串切片。Python没有针对字符串的截取函数，只需要切片一个操作就可以完成，非常简单。

**任务**

字符串有个方法 upper() 可以把字符变成大写字母：

    >>> 'abc'.upper()
    'ABC'

但它会把所有字母都变成大写。请设计一个函数，它接受一个字符串，然后返回一个仅首字母变成大写的字符串。

提示：利用切片操作简化字符串操作。

    def firstCharUpper(s):
    return s[0].upper()+s[1:]
    
    print firstCharUpper('hello')
    print firstCharUpper('sunday')
    print firstCharUpper('september')


## 什么是迭代

在Python中，如果给定一个list或tuple，我们可以通过for循环来遍历这个list或tuple，这种遍历我们成为迭代（Iteration）。

在Python中，迭代是通过 for ... in 来完成的，而很多语言比如C或者Java，迭代list是通过下标完成的，比如Java代码：
    
    for (i=0; i<list.length; i++) {
    n = list[i];
    }

可以看出，Python的for循环抽象程度要高于Java的for循环。

因为 Python 的 for循环不仅可以用在list或tuple上，还可以作用在其他任何可迭代对象上。

因此，迭代操作就是对于一个集合，无论该集合是有序还是无序，我们用 for 循环总是可以依次取出集合的每一个元素。

因此，迭代操作就是对于一个集合，无论该集合是有序还是无序，我们用 for 循环总是可以依次取出集合的每一个元素。

    注意: 集合是指包含一组元素的数据结构，我们已经介绍的包括：
    1. 有序集合：list，tuple，str和unicode；
    2. 无序集合：set
    3. 无序集合并且具有 key-value 对：dict

而迭代是一个动词，它指的是一种操作，在Python中，就是 for 循环。

迭代与按下标访问数组最大的不同是，后者是一种具体的迭代实现方式，而前者只关心迭代结果，根本不关心迭代内部是如何实现的。


**任务**

请用for循环迭代数列 1-100 并打印出7的倍数。

    for i in range(1,101)[6::7]:
    print i

## 索引迭代

Python中，迭代永远是取出元素本身，而非元素的索引。

对于有序集合，元素确实是有索引的。有的时候，我们确实想在 for 循环中拿到索引，怎么办？

方法是使用 enumerate() 函数：

    >>> L = ['Adam', 'Lisa', 'Bart', 'Paul']
    >>> for index, name in enumerate(L):
    ... print index, '-', name
    ... 
    0 - Adam
    1 - Lisa
    2 - Bart
    3 - Paul

使用 enumerate() 函数，我们可以在for循环中同时绑定索引index和元素name。但是，这不是 enumerate() 的特殊语法。实际上，enumerate() 函数把：

    ['Adam', 'Lisa', 'Bart', 'Paul']
    
变成了类似：

    [(0, 'Adam'), (1, 'Lisa'), (2, 'Bart'), (3, 'Paul')]

因此，迭代的每一个元素实际上是一个tuple：

    for t in enumerate(L):
    index = t[0]
    name = t[1]
    print index, '-', name


如果我们知道每个tuple元素都包含两个元素，for循环又可以进一步简写为：
    
    for index, name in enumerate(L):
    print index, '-', name


这样不但代码更简单，而且还少了两条赋值语句。

可见，索引迭代也不是真的按索引访问，而是由 enumerate() 函数自动把每个元素变成 (index, element) 这样的tuple，再迭代，就同时获得了索引和元素本身


**任务**

zip()函数可以把两个 list 变成一个 list：

    >>> zip([10, 20, 30], ['A', 'B', 'C'])
    [(10, 'A'), (20, 'B'), (30, 'C')]

在迭代 `['Adam', 'Lisa', 'Bart', 'Paul']` 时，如果我们想打印出名次 - 名字（名次从1开始)，请考虑如何在迭代中打印出来。

提示：考虑使用zip()函数和range()函数

    L = ['Adam', 'Lisa', 'Bart', 'Paul']
    for index, name in zip(range(1, len(L)+1), L):
    print index, '-', name

## 迭代dict的value

我们已经了解了dict对象本身就是可迭代对象，用 for 循环直接迭代 dict，可以每次拿到dict的一个key。

如果我们希望迭代 dict 对象的value，应该怎么做？

dict 对象有一个 **values() 方法**，这个方法把dict转换成一个包含所有value的list，这样，我们迭代的就是 dict的每一个 value：

    d = { 'Adam': 95, 'Lisa': 85, 'Bart': 59 }
    print d.values()
    # [85, 95, 59]
    for v in d.values():
    print v
    # 85
    # 95
    # 59


如果仔细阅读Python的文档，还可以发现，dict除了values()方法外，还有一个 itervalues() 方法，用 itervalues() 方法替代 values() 方法，迭代效果完全一样：

    d = { 'Adam': 95, 'Lisa': 85, 'Bart': 59 }
    print d.itervalues()
    # <dictionary-valueiterator object at 0x106adbb50>
    for v in d.itervalues():
    print v
    # 85
    # 95
    # 59


**那这两个方法有何不同之处呢？**

1. values() 方法实际上把一个 dict 转换成了包含 value 的list。

2. 但是 itervalues() 方法不会转换，它会在迭代过程中依次从 dict 中取出 value，所以 itervalues() 方法比 values() 方法节省了生成 list 所需的内存。

3. 打印 itervalues() 发现它返回一个 <dictionary-valueiterator> 对象，这说明在Python中，**for 循环可作用的迭代对象远不止 list，tuple，str，unicode，dict等**，任何可迭代对象都可以作用于for循环，而内部如何迭代我们通常并不用关心。

**如果一个对象说自己可迭代，那我们就直接用 for 循环去迭代它，可见，迭代是一种抽象的数据操作，它不对迭代对象内部的数据有任何要求。**


## 迭代dict的key和value


我们了解了如何迭代 dict 的key和value，那么，在一个 for 循环中，能否同时迭代 key和value？答案是肯定的。

首先，我们看看 dict 对象的 items() 方法返回的值：

    >>> d = { 'Adam': 95, 'Lisa': 85, 'Bart': 59 }
    >>> print d.items()
    [('Lisa', 85), ('Adam', 95), ('Bart', 59)]


可以看到，items() 方法把dict对象转换成了包含tuple的list，我们对这个list进行迭代，可以同时获得key和value：


    >>> for key, value in d.items():
    ... print key, ':', value
    ... 
    Lisa : 85
    Adam : 95
    Bart : 59
    
和 values() 有一个 itervalues() 类似，** items() **也有一个对应的 iteritems()，iteritems() 不把dict转换成list，而是在迭代过程中不断给出 tuple，所以， iteritems() 不占用额外的内存。


## 生成列表

要生成list [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]，我们可以用range(1, 11)：

    >>> range(1, 11)
    [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

但如果要生成[1x1, 2x2, 3x3, ..., 10x10]怎么做？方法一是循环：

    >>> L = []
    >>> for x in range(1, 11):
    ...L.append(x * x)
    ... 
    >>> L
    [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]

但是循环太繁琐，而列表生成式则可以用一行语句代替循环生成上面的list：

    >>> [x * x for x in range(1, 11)]
    [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]


这种写法就是Python特有的列表生成式。利用列表生成式，可以以非常简洁的代码生成 list。

写列表生成式时，把要生成的元素 x * x 放到前面，后面跟 for 循环，就可以把list创建出来，十分有用，多写几次，很快就可以熟悉这种语法。

**任务**

请利用列表生成式生成列表 [1x2, 3x4, 5x6, 7x8, ..., 99x100]

提示：range(1, 100, 2) 可以生成list [1, 3, 5, 7, 9,...]

    print [x*(x+1) for  x in range(1,101,2)]



## 复杂表达式

使用for循环的迭代不仅可以迭代普通的list，还可以迭代dict。

假设有如下的dict：

    d = { 'Adam': 95, 'Lisa': 85, 'Bart': 59 }


完全可以通过一个复杂的列表生成式把它变成一个 HTML 表格：

    tds = ['<tr><td>%s</td><td>%s</td></tr>' % (name, score) for name, score in d.iteritems()]
    print '<table>'
    print '<tr><th>Name</th><th>Score</th><tr>'
    print '\n'.join(tds)
    print '</table>'

注：字符串可以通过 % 进行格式化，用指定的参数替代 %s。字符串的join()方法可以把一个 list 拼接成一个字符串。

把打印出来的结果保存为一个html文件，就可以在浏览器中看到效果了：

    <table border="1">
    <tr><th>Name</th><th>Score</th><tr>
    <tr><td>Lisa</td><td>85</td></tr>
    <tr><td>Adam</td><td>95</td></tr>
    <tr><td>Bart</td><td>59</td></tr>
    </table>

![](http://img.mukewang.com/540fcd2a0001ff4600940104.jpg)


## 条件过滤

列表生成式的 for 循环后面还可以加上 if 判断。例如：

    >>> [x * x for x in range(1, 11)]
    [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]


如果我们只想要偶数的平方，不改动 range()的情况下，可以加上 if 来筛选：

    >>> [x * x for x in range(1, 11) if x % 2 == 0]
    [4, 16, 36, 64, 100]

有了 if 条件，只有 if 判断为 True 的时候，才把循环的当前元素添加到列表中。

**任务**

请编写一个函数，它接受一个 list，然后把list中的所有字符串变成大写后返回，非字符串元素将被忽略。

提示：

1. isinstance(x, str) 可以判断变量 x 是否是字符串；

2. 字符串的 upper() 方法可以返回大写的字母。


    def toUppers(L):
    return [x.upper() for x in L if isinstance(x,str)]
    
    print toUppers(['Hello', 'world', 101])


    def toUppers(L):
    
    return [x.upper() for x in L if type(x) == str]
    
    print toUppers(['Hello', 'world', 101])


## 多层表达式

for循环可以嵌套，因此，在列表生成式中，也可以用多层 for 循环来生成列表。

对于字符串 'ABC' 和 '123'，可以使用两层循环，生成全排列：

    >>> [m + n for m in 'ABC' for n in '123']
    ['A1', 'A2', 'A3', 'B1', 'B2', 'B3', 'C1', 'C2', 'C3']


翻译成循环代码就像下面这样：


    L = []
    for m in 'ABC':
    for n in '123':
    L.append(m + n)

**任务**
利用 3 层for循环的列表生成式，找出对称的 3 位数。例如，121 就是对称数，因为从右到左倒过来还是 121。


    print [100*n1+10*n2+n3 for n1 in range(1,10) for n2 in range(10) for n3 in range(10) if n1==n3]


[101, 111, 121, 131, 141, 151, 161, 171, 181, 191, 202, 212, 222, 232, 242, 252, 262, 272, 282, 292, 303, 313, 323, 333, 343, 353, 363, 373, 383, 393, 404, 414, 424, 434, 444, 454, 464, 474, 484, 494, 505, 515, 525, 535, 545, 555, 565, 575, 585, 595, 606, 616, 626, 636, 646, 656, 666, 676, 686, 696, 707, 717, 727, 737, 747, 757, 767, 777, 787, 797, 808, 818, 828, 838, 848, 858, 868, 878, 888, 898, 909, 919, 929, 939, 949, 959, 969, 979, 989, 999]

