Python百问：

##### 1、一行代码实现1--100之和

```python
print(sum[i for i in range(1,101)]) # or 求和公式(1+100)*100//2
```

##### 2、如何在一个函数内部修改全局变量

添加关键词，global

```python
a = 100
def testA():
   print(a)

def testB():
    global a		# 关键字声明a为全局变量，系统就会去找叫a的全局变量
    a = 200
    print(a)
# python的函数中能修改全局变量的值，除了字符串和元组那些不能够修
def test4():
    print(name)

def test5():
    name[0] = 99
    print(name)

testA()	 # 100
testB()  # 200
testA()  # 200

test4()	 # [1, 2, 3, 4, 5, 6]
test5()  # [99, 2, 3, 4, 5, 6]
test4()  # [99, 2, 3, 4, 5, 6]
```

##### 3、列出5个python标准库

| 名称     | 作用                                                         |
| -------- | ------------------------------------------------------------ |
| datetime | 为日期和时间处理同时提供了简单和复杂的方法。                 |
| zlib     | 直接支持通用的数据打包和压缩格式：zlib，gzip，bz2，zipfile，以及 tarfile。 |
| random   | 提供了生成随机数的工具。                                     |
| math     | 为浮点运算提供了对底层C函数库的访问。                        |
| sys      | 工具脚本经常调用命令行参数。这些命令行参数以链表形式存储于 sys 模块的 argv 变量。 |
| glob     | 提供了一个函数用于从目录通配符搜索中生成文件列表。           |
| os       | 提供了不少与操作系统相关联的函数。                           |
| urlopen  | 有几个模块用于访问互联网以及处理网络通信协议。其中最简单的两个是用于处理从 urls 接收的数据的 urllib.request 以及用于发送电子邮件的 smtplib: |
| re       | 字符串正则匹配                                               |

##### 4、字典如何删除键/合并两个字典/去重

删除：del dict[key] *# 删除键是'name'的条目* 

​			或 dict.clear() / del dict *# 清空词典所有条目 #*

合并：dict1.update(dict2). 但是重复key的value值会被覆盖

去重：reduce and lambda function. [资料](https://blog.csdn.net/weixin_37994148/article/details/99731818)

##### 5、谈下python的GIL

Guido van Rossum（吉多·范罗苏姆）创建python时就只考虑到单核cpu，解决多线程之间数据完整性和状态同步的最简单方法自然就是加锁， 于是有了GIL这把超级大锁。因为cpython解析只允许拥有GIL全局解析器锁才能运行程序，这样就保证了保证同一个时刻只允许一个线程可以使用cpu。

即全局解释器所（[global interpreter lock](https://www.baidu.com/link?url=wcyORPNvihJlWYZsd97z3F3g6xZfs09N64Jc56POq3P7r3h5vIxVFcjGiZjosC6g3jhmBh13DS36rKld5eBfWq&wd=&eqid=aa7605a200005349000000025aa0f4fb)），每个线程在执行时候都需要先获取GIL，保证同一时刻只有一个线程可以执行代码，即同一时刻只有一个线程使用CPU，也就是说多线程并不是真正意义上的同时执行。

GIL 是python的全局解释器锁，同一进程中假如有多个线程运行，一个线程在运行python程序的时候会霸占python解释器（加了一把锁即GIL），使该进程内的其他线程无法运行，等该线程运行完后其他线程才能运行。如果线程运行过程中遇到耗时操作，则解释器锁解开，使其他线程运行。所以在多线程中，线程的运行仍是有先后顺序的，并不是同时进行。

多进程中因为每个进程都能被系统分配资源，相当于每个进程有了一个python解释器，所以多进程可以实现多个进程的同时运行，缺点是进程系统资源开销大

##### 6、python实现列表去重的方法

先通过集合去重，在转列表

![img](http://5b0988e595225.cdn.sohucs.com/images/20190328/f49b686e64f340e3a7dc8bcab73e8a5a.jpeg)

##### 7、fun(*args,**kwargs)中的*args,**kwargs什么意思？*

![img](http://5b0988e595225.cdn.sohucs.com/images/20190328/dd1a996b772d4bd4b7b23e1321518915.jpeg)

![img](http://5b0988e595225.cdn.sohucs.com/images/20190328/97f970c5dd9049369bbf3d8d51e27e7b.jpeg)

##### 8、python2和python3的range（100）的区别?

python2返回列表，python3返回迭代器，节约内存.

##### 9、一句话解释什么样的语言能够用装饰器?

函数可以作为参数传递的语言，可以使用装饰器。

[那么什么是装饰器呢？](https://www.zhihu.com/question/26930016/answer/1047233982)

**装饰器，就是增强函数或类的功能的一个函数。**

**装饰器的作用**：增强函数的功能，确切的说，可以装饰函数，也可以装饰类。

**装饰器的原理**：函数是python的一等公民，函数也是对象。

##### 10、python内建数据类型有哪些

整型--int	布尔型--bool	字符串--str

列表--list	元组--tuple		字典--dict

##### 11、简述面向对象中__new__和__init__区别

__init__是初始化方法，创建对象后，就立刻被默认调用了，可接收参数，如图

![img](http://5b0988e595225.cdn.sohucs.com/images/20190328/988372d37dee469f9f815e3f9702346f.jpeg)

​	1、__new__至少要有一个参数cls，代表当前类，此参数在实例化时由Python解释器自动识别。

​	2、__new__必须要有返回值，返回实例化出来的实例，这点在自己实现__new__时要特别注意，可以return父类（通过	super(当前类名, cls)）__new__出来的实例，或者直接是object的__new__出来的实例。

​	3、__init__有一个参数self，就是这个__new__返回的实例，__init__在__new__的基础上可以完成一些其它初始化的动作，__init__不需要返回值。

​	4、如果__new__创建的是当前类的实例，会自动调用__init__函数，通过return语句里面调用的__new__函数的第一个参数是cls来保证是当前类实例，如果是其他类的类名，；那么实际创建返回的就是其他类的实例，其实就不会调用当前类的__init__函数，也不会调用其他类的__init__函数。

##### 12、简述with方法打开处理文件帮我我们做了什么？

打开文件在进行读写的时候可能会出现一些异常状况，如果按照常规的f.open写法，我们需要try,except,finally，做异常判断，并且文件最终不管遇到什么情况，都要执行finally f.close()关闭文件，with方法帮我们实现了finally中f.close（当然还有其他自定义功能，有兴趣可以研究with方法源码）

##### 13、列表[1,2,3,4,5],请使用map()函数输出[1,4,9,16,25]，并使用列表推导式提取出大于10的数，最终输出[16,25]

```python
a = [1,2,3,4,5]

def func(ls):
    return ls**2

b = map(func, a)
res = [i for i in b if i > 10]
print(res)
```

##### 14、python中生成随机整数、随机小数、0--1之间小数方法

随机整数：random.randint(a,b),生成区间内的一个整数。

随机小数：习惯用numpy库，利用np.random.randn(5)生成5个随机小数。

0-1随机小数：random.random(),括号中不传参，生成一个小数。

##### 15、避免转义给字符串加哪个字母表示原始字符串？

r , 表示需要原始字符串，不转义特殊字符。

##### 16、<div class='nam'>中国</div>，用正则匹配出标签里面的内容（“中国”），其中class的类名是不确定的

##### 17、python中断言方法举例

assert（）方法，断言成功，则程序继续执行，断言失败，则程序报错。

![img](http://5b0988e595225.cdn.sohucs.com/images/20190328/f3ad4e5b72154aa79c49a1ab66f7ce8b.jpeg)

##### 18、数据表student有id,name,score,city字段，其中name中的名字可有重复，需要消除重复行,请写sql语句

select *distinct* name from student

##### 19、10个Linux常用命令

ls pwd cd touch rm mkdir tree cp mv cat more grep echo

##### 20、python2和python3区别？列举5个

​	1、Python3 使用 print 必须要以小括号包裹打印内容，比如 print('hi')

​	Python2 既可以使用带小括号的方式，也可以使用一个空格来分隔打印内容，比如 print 'hi'

​	2、python2 range(1,10)返回列表，python3中返回迭代器，节约内存

​	3、python2中使用ascii编码，python中使用utf-8编码

​	4、python2中unicode表示字符串序列，str表示字节序列

​	python3中str表示字符串序列，byte表示字节序列

​	5、python2中为正常显示中文，引入coding声明，python3中不需要

​	6、python2中是raw_input()函数，python3中是input()函数

##### 21、列出python中可变数据类型和不可变数据类型，并简述原理

不可变数据类型：数值型、字符串型string和元组tuple不允许变量的值发生变化，如果改变了变量的值，相当于是新建了一个对象，而对于相同的值的对象，在内存中则只有一个对象（一个地址），如下图用id()方法可以打印对象的id。

可变数据类型：列表list和字典dict；允许变量的值发生变化，即如果对变量进行append、+=等这种操作后，只是改变了变量的值，而不会新建一个对象，变量引用的对象的地址也不会变化，不过对于相同的值的不同对象，在内存中则会存在不同的对象，即每个对象都有自己的地址，相当于内存中对于同值的对象保存了多份，这里不存在引用计数，是实实在在的对象。

##### 22、s = 'ajldjlajfdljfddd'，去重并从小到大排序输出'adfjl'

```python
a = 'ajldjlajfdljfddd'
a = set(a)		# {'j', 'f', 'd', 'a', 'l'}
a = list(a)		# ['j', 'f', 'd', 'a', 'l']
a.sort(reverse=False)		# ['a', 'd', 'f', 'j', 'l']
res = ''.join(a)
print(res)		#adfjl
```

##### 23、用lambda函数实现两个数相乘 [解析](https://www.cnblogs.com/kaishirenshi/p/8611358.html)

```python
f = lambda x,y:x*y
# 函数名 = lambda x,y(变量):x*y(函数式)  --> 可以等化 def
```

##### 24、字典根据键从小到大排序

```python
dic={"name":"zs","age":"18","city":"深圳","tel":"1362626627"}
a = sorted(dic.items(), key = lambda x:x[0], reverse = False)	# 根据key排序
b = sorted(dic.items(), key = lambda x:x[1], reverse = False)	# 根据value排序
print(dict(a)) # list转dict
```

##### 25、利用collections库的Counter方法统计字符串每个单词出现的次数 'kjalfj;ldsjafl;hdsllfdhg;lahfbl;hl;ahlf;h'

```python
from collections import Counter
a = "kjalfj;ldsjafl;hdsllfdhg;lahfbl;hl;ahlf;h"
res = Counter(a)
print(res)
```

26、字符串a = 'not 404 found 张三 99 深圳'，每个词中间是空格，用正则过滤掉英文和数字，最终输出'张三 深圳'



##### 27、filter方法求出列表所有奇数并构造新列表，a = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

```python
a = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
f = lambda x: x%2==1
ls = filter(f, a)
ls = [i for i in ls]
print(ls)
```

##### 28、列表推导式求列表所有奇数并构造新列表，a = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

```python
ls1 = [i for i in a if i%2 == 1]
print(ls1)
```

##### 29、正则re.complie作用



##### 30、a=（1，）b=(1)，c=('1') 分别是什么类型的数据？

tuple, int , str

##### 31、两个列表[1,5,7,9]和[2,2,6,8]合并为[1,2,2,3,6,7,8,9]

```python
ls1 = [1,5,7,9]
ls2 = [2,2,6,8]
ls1.extend(ls2)
ls1.sort()
print(ls1)
```

##### 32、用python删除文件和用linux命令删除文件方法

python：os.remove(文件名)

linux: rm 文件名

##### 33、log日志中，我们需要用时间戳记录error,warning等的发生时间，请用datetime模块打印当前时间戳 “2018-04-01 11:38:54”

datetime模块

##### 34、数据库优化查询方法

外键、索引、联合查询、选择特定字段等等

##### 35、请列出你会的任意一种统计图（条形图、折线图等）绘制的开源库，第三方也行

pychart、matplotlib

##### 36、写一段自定义异常代码

```python
try:
    a = input("输入一个数：")
    #判断用户输入的是否为数字
    if(not a.isdigit()):
        raise ValueError("a 必须是数字")
except ValueError as e:
    print("引发异常：",repr(e))
```

##### 37、正则表达式匹配中，（.*）和（.*?）匹配区别？

（.*）是贪婪匹配，会把满足正则的尽可能多的往后匹配

（.*?）是非贪婪匹配，会把满足正则的尽可能少匹配

##### 38、简述Django的orm

ORM，全拼Object-Relation Mapping，意为对象-关系映射。实现了数据模型与数据库的解耦，通过简单的配置就可以轻松更换数据库，而不需要修改代码只需要面向对象编程,orm操作本质上会根据对接的数据库引擎，翻译成对应的sql语句,所有使用Django开发的项目无需关心程序底层使用的是MySQL、Oracle、sqlite....，如果数据库迁移，只需要更换Django的数据库引擎即可。

##### 39、[[1,2],[3,4],[5,6]]一行代码展开该列表，得出[1,2,3,4,5,6]

```python
a = [[1,2],[3,4],[5,6]]
b = [j for i in a for j in i]
print(b)
```

##### 40、x='abc',y='def',z=['d','e','f'],分别求出x.join(y)和x.join(z)返回的结果



##### 41、举例说明异常模块中try except else finally的相关意义

try..except..else没有捕获到异常，执行else语句。

try..except..finally不管是否捕获到异常，都执行finally语句。

![img](http://5b0988e595225.cdn.sohucs.com/images/20190328/0a0e0cb3225844cf813d80f101d3a4c2.jpeg)

##### 42、python中交换两个数值

a, b = b, a

##### 43、举例说明zip（）函数用法

zip()函数在运算时，会以一个或多个序列（可迭代对象）做为参数，返回一个**元组**的列表。同时将这些序列中并排的元素配对。

zip()参数可以接受任何类型的序列，同时也可以有两个以上的参数;**当传入参数的长度不同时，zip能自动以最短序列长度为准进行截取，获得元组**。

![img](http://5b0988e595225.cdn.sohucs.com/images/20190328/58666e5c104c4738806b9b6a69baa1a5.jpeg)

##### 44、a='张明 98分'，用re.sub，将98替换为100

```python
import re
a = '张明 98分'
res = re.sub(r'\d+','100',a)
print(res)
```

##### 45、numpy: unique 去重

```python
import numpy as np
data = np.array([[1,8,3,3,4],
                 [1,8,9,9,4],
                 [1,8,3,3,4]])
# 删除整个数组的重复元素
uniques = np.unique(data)
print(uniques)
# 删除重复行
uniques = np.unique(data, axis=0)
print(uniques)
# 删除重复列
uniques = np.unique(data, axis=1)
print(uniques)
```

##### 46、a='hello'和b='你好'编码成bytes类型

![img](http://5b0988e595225.cdn.sohucs.com/images/20190328/f436e86224a04a86adc1539c4f8adf57.jpeg)

##### 47、[1,2,3]+[4,5,6]的结果是多少？

两个列表相加，等价于extend。[1,2,3,4,5,6]

##### 48、提高python运行效率的方法

​	1、使用生成器，因为可以节约大量内存

​	2、循环代码优化，避免过多重复代码的执行

​	3、核心模块用Cython PyPy等，提高效率

​	4、多进程、多线程、协程

​	5、多个if elif条件判断，可以把最有可能先发生的条件放到前面写，这样可以减少程序判断的次数，提高效率

##### 49、简述mysql和redis区别

​	redis： 内存型非关系数据库，数据保存在内存中，速度快

​	mysql：关系型数据库，数据保存在磁盘中，检索的话，会有一定的Io操作，访问速度相对慢

##### 50、遇到bug如何处理

​	1、细节上的错误，通过print（）打印，能执行到print（）说明一般上面的代码没有问题，分段检测程序是否有问题，如果是js的话可以alert或console.log。

​	2、如果涉及一些第三方框架，会去查官方文档或者一些技术博客。

​	3、对于bug的管理与归类总结，一般测试将测试出的bug用teambin等bug管理工具进行记录，然后我们会一条一条进行修改，修改的过程也是理解业务逻辑和提高自己编程逻辑缜密性的方法，我也都会收藏做一些笔记记录。

​	4、导包问题、城市定位多音字造成的显示错误问题。

##### 51、正则匹配，匹配日期2018-03-20

##### 52、list=[2,3,5,4,9,6]，从小到大排序，不许用sort，输出[2,3,4,5,6,9]

##### 53、写一个单列模式

##### 54、保留两位小数

##### 55、求三个方法打印结果

fn("one",1）直接将键值对传给字典；

fn("two",2)因为字典在内存中是可变数据类型，所以指向同一个地址，传了新的额参数后，会相当于给字典增加键值对；

fn("three",3,{})因为传了一个新字典，所以不再是原先默认参数的字典。

![img](http://5b0988e595225.cdn.sohucs.com/images/20190328/31396b651c924d2292719b055669cbc2.jpeg)

##### 56、列出常见的状态码和意义

57、分别从前端、后端、数据库阐述web项目的性能优化

##### 58、使用pop和del删除字典中的'name'字段，dic={'name':'zs','age':18}

![img](https://images2018.cnblogs.com/blog/1303607/201808/1303607-20180828192120409-507789285.png)

59、列出常见MYSQL数据存储引擎



##### 60、计算代码运行结果，zip函数历史文章已经说了，得出[('a',1),('b',2)，('c',3),('d',4),('e',5)]

![img](https://images2018.cnblogs.com/blog/1303607/201808/1303607-20180828192154985-1998412011.png)

##### 61、简述同源策略

 同源策略需要同时满足以下三点要求： 

​	1）协议相同 

​	 2）域名相同 

​	3）端口相同 

​	 http:www.test.com与https:www.test.com 不同源——协议不同 

​	 http:www.test.com与http:www.admin.com 不同源——域名不同 

 	http:www.test.com与http:www.test.com:8081 不同源——端口不同

 	只要不满足其中任意一个要求，就不符合同源策略，就会出现“跨域”

##### 62、简述cookie和session的区别

​	1，session 在服务器端，cookie 在客户端（浏览器）

​	2、session 的运行依赖 session id，而 session id 是存在 cookie 中的，也就是说，如果浏览器禁用了 cookie ，同时 session 也会失效，存储Session时，键与Cookie中的session id相同，值是开发人员设置的键值对信息，进行了base64编码，过期时间由开发人员设置

​	3、cookie安全性比session差

##### 63、简述多线程、多进程

**进程：**

​	1、操作系统进行资源分配和调度的基本单位，多个进程之间相互独立

​	2、稳定性好，如果一个进程崩溃，不影响其他进程，但是进程消耗资源大，开启的进程数量有限制、

**线程：**

​	1、CPU进行资源分配和调度的基本单位，线程是进程的一部分，是比进程更小的能独立运行的基本单位，一个进程下的多个线程可以共享该进程的所有资源

​	2、如果IO操作密集，则可以多线程运行效率高，缺点是如果一个线程崩溃，都会造成进程的崩溃

**应用：**

​	IO密集的用多线程，在用户输入，sleep 时候，可以切换到其他线程执行，减少等待的时间

​	CPU密集的用多进程，因为假如IO操作少，用多线程的话，因为线程共享一个全局解释器锁，当前运行的线程会霸占GIL，其他线程没有GIL，就不能充分利用多核CPU的优势

##### 64、简述any()和all()方法

​	any():只要迭代器中有一个元素为真就为真

​	all():迭代器中所有的判断项返回都是真，结果才为真

​	python中什么元素为假？

​	答案：**（0，空字符串，空列表、空字典、空元组、None, False）**

##### 65、IOError、AttributeError、ImportError、IndentationError、IndexError、KeyError、SyntaxError、NameError分别代表什么异常

​	IOError：输入输出异常

​	AttributeError：试图访问一个对象没有的属性

​	ImportError：无法引入模块或包，基本是路径问题

​	IndentationError：语法错误，代码没有正确的对齐

​	IndexError：下标索引超出序列边界

​	KeyError:试图访问你字典里不存在的键

​	SyntaxError:Python代码逻辑语法出错，不能执行

​	NameError:使用一个还未赋予对象的变量

##### 66、python中copy和deepcopy区别

​	1、复制不可变数据类型，不管copy还是deepcopy,都是同一个地址当浅复制的值是不可变对象（数值，字符串，元组）时和=“赋值”的情况一样，对象的id值与浅复制原来的值相同。

​	2、复制的值是可变对象（列表和字典）

​	浅拷贝copy有两种情况：

​	第一种情况：复制的 对象中无 复杂 子对象，原来值的改变并不会影响浅复制的值，同时浅复制的值改变也并不会影响原来的值。原来值的id值与浅复制原来的值不同。

​	第二种情况：复制的对象中有 复杂 子对象 （例如列表中的一个子元素是一个列表）， 改变原来的值 中的复杂子对象的值 ，会影响浅复制的值。

​	深拷贝deepcopy：完全复制独立，包括内层列表和字典

![img](https://images2018.cnblogs.com/blog/1303607/201808/1303607-20180828192337339-173043852.png)

##### 67、列出几种魔法方法并简要介绍用途. [实例](https://www.cnblogs.com/zhouyixian/p/11129347.html)

##### 68、C:\Users\ry-wu.junya\Desktop>python 1.py 22 33命令行启动程序并传参，print(sys.argv)会输出什么数据？

​	文件名和参数构成的列表

##### 69、请将[i for i in range(3)]改成生成器

![img](https://images2018.cnblogs.com/blog/1303607/201808/1303607-20180828192439797-956979824.png)

70、a = ' hehheh ',去除收尾空格

##### 71、举例sort和sorted对列表排序，list=[0,-1,3,-10,5,9]

 sort无返回值，sorted输出新list

##### 72、对list排序foo = [-5,8,0,4,9,-4,-20,-2,8,2,-4],使用lambda函数从小到大排序

##### 73、使用lambda函数对list排序foo = [-5,8,0,4,9,-4,-20,-2,8,2,-4]，输出结果为[0,2,4,8,8,9,-2,-4,-4,-5,-20]，正数从小到大，负数从大到小（传两个条件，x<0和abs(x)）

```python
foo = [-5,8,0,4,9,-4,-20,-2,8,2,-4]
# 72
a = sorted(foo, key = lambda x:x)
print(a)	# [-20, -5, -4, -4, -2, 0, 2, 4, 8, 8, 9]
b = sorted(foo, key = lambda x:(x<0, abs(x)))
print(b)	# [0, 2, 4, 8, 8, 9, -2, -4, -4, -5, -20]
```

key = lambda x:(括号中输入条件参数)

##### 74、列表嵌套字典的排序，分别根据年龄和姓名排序

##### 75、列表嵌套元组，分别按字母和数字排序

##### 76、列表嵌套列表排序，年龄数字相同怎么办？

![img](https://images2018.cnblogs.com/blog/1303607/201808/1303607-20180828192551318-1294639125.png)

##### 77、根据键对字典排序（方法一，zip函数）

##### 78、根据键对字典排序（方法二,不用zip)

![img](https://images2018.cnblogs.com/blog/1303607/201808/1303607-20180828192744780-1759241546.png)

##### 79、列表推导式、字典推导式、生成器

##### 80、最后出一道检验题目，根据字符串长度排序，看排序是否灵活运用

![img](https://images2018.cnblogs.com/blog/1303607/201808/1303607-20180828192802934-710054967.png)

##### 81、举例说明SQL注入和解决办法

##### 82、s='info:xiaoZhang 33 shandong',用正则切分字符串输出['info', 'xiaoZhang', '33', 'shandong']

![img](https://images2018.cnblogs.com/blog/1303607/201808/1303607-20180828192839575-1983643091.png)

```python
import re
s='info:xiaoZhang//////33 shandong'
res = re.split(r':| |/*/',s)
print(res)
```

##### 83、正则匹配以163.com结尾的邮箱

```python
import re

email_ls = ['aaaa@163.com','bbbb@163.com','cccc@163.com','1@163.com']
for em in email_ls:
  	# [限定]
    res = re.match('[\w]{4,20}@163\.com$', em)
    if res:
        print(em, res.group())
    else:
        print('Its wrong', em)
```

##### 84、递归求和

![img](https://images2018.cnblogs.com/blog/1303607/201808/1303607-20180828192915829-408728688.png)

##### 85、python字典和json字符串相互转化方法

​	json.dumps()字典转json字符串，json.loads()json转字典

![img](https://images2018.cnblogs.com/blog/1303607/201808/1303607-20180828192945208-786963520.png)

##### 86、MyISAM 与 InnoDB 区别：

​	1、InnoDB 支持事务，MyISAM 不支持，这一点是非常之重要。事务是一种高

级的处理方式，如在一些列增删改中只要哪个出错还可以回滚还原，而 MyISAM

就不可以了；

​	2、MyISAM 适合查询以及插入为主的应用，InnoDB 适合频繁修改以及涉及到

安全性较高的应用；

​	3、InnoDB 支持外键，MyISAM 不支持；

​	4、对于自增长的字段，InnoDB 中必须包含只有该字段的索引，但是在 MyISAM

表中可以和其他字段一起建立联合索引；

​	5、清空整个表时，InnoDB 是一行一行的删除，效率非常慢。MyISAM 则会重

建表；

##### 87、统计字符串中某字符出现次数

```python
str = 'a a v v v b b d d'
print(str.count('a'))
```

##### 88、字符串转化大小写

​	upper(), lower()

##### 89、用两种方法去空格

​	replace(" ", ""), split(" ")

##### 90、正则匹配不是以4和7结尾的手机号

![img](https://images2018.cnblogs.com/blog/1303607/201808/1303607-20180828193039336-1301298582.png)

##### 91、简述python引用计数机制

​	python垃圾回收主要以引用计数为主，标记-清除和分代清除为辅的机制，其中标记-清除和分代回收主要是为了处理循环引用的难题。

##### 	引用计数算法

​	当有1个变量保存了对象的引用时，此对象的引用计数就会加1

​	当使用del删除变量指向的对象时，如果对象的引用计数不为1，比如3，那么此时只会让这个引用计数减1，即变为2，当再次调用del时，变为1，如果再调用1次del，此时会真的把对象进行删除

##### 92、int('1.4'),int(1.4)输出结果？

​	int("1.4")报错，int(1.4)输出1

##### 93、列举3条以上PEP8编码规范

​	1、顶级定义之间空两行，比如函数或者类定义。

​	2、方法定义、类定义与第一个方法之间，都应该空一行

​	3、三引号进行注释

​	4、使用Pycharm、Eclipse一般使用4个空格来缩进代码

##### 94、正则表达式匹配第一个URL

![img](https://images2018.cnblogs.com/blog/1303607/201808/1303607-20180828193121315-490390183.png)

95、正则匹配中文

##### 96、简述乐观锁和悲观锁

​	悲观锁, 就是很悲观，每次去拿数据的时候都认为别人会修改，所以每次在拿数据的时候都会上锁，这样别人想拿这个数据就会block直到它拿到锁。传统的关系型数据库里边就用到了很多这种锁机制，比如行锁，表锁等，读锁，写锁等，都是在做操作之前先上锁。

​	乐观锁，就是很乐观，每次去拿数据的时候都认为别人不会修改，所以不会上锁，但是在更新的时候会判断一下在此期间别人有没有去更新这个数据，可以使用版本号等机制，乐观锁适用于多读的应用类型，这样可以提高吞吐量

##### 97、r、r+、rb、rb+文件打开模式区别

![img](https://images2018.cnblogs.com/blog/1303607/201808/1303607-20180828193153520-908077286.png)

##### 98、Linux命令重定向 > 和 >>

Linux 允许将命令执行结果 重定向到一个 文件

将本应显示在终端上的内容 输出／追加 到指定文件中

\> 表示输出，会覆盖文件原有的内容

\>> 表示追加，会将内容追加到已有文件的末尾

用法示例：

```
将 echo 输出的信息保存到 1.txt 里echo Hello Python > 1.txt
将 tree 输出的信息追加到 1.txt 文件的末尾tree >> 1.txt
```

##### 99、正则表达式匹配出<html><h1>itcast.cn</h1></html>

![img](https://images2018.cnblogs.com/blog/1303607/201808/1303607-20180828193220045-1678225769.png)

100、python传参数是传值还是传址？

##### 101、求两个列表的交集、差集、并集

![img](https://images2018.cnblogs.com/blog/1303607/201808/1303607-20180828193306159-489969204.png)

102、生成0-100的随机数

103、lambda匿名函数好处

##### 104、常见的网络传输协议

​	UDP、TCP、FTP、HTTP、SMTP等等

##### 105、单引号、双引号、三引号用法

1、单引号和双引号没有什么区别，不过单引号不用按shift，打字稍微快一点。表示字符串的时候，单引号里面可以用双引号，而不用转义字符,反之亦然。

```python
'She said:"Yes." '` `or` `"She said: 'Yes.' "
```

2、但是如果直接用单引号扩住单引号，则需要转义，像这样：

```python
 ' She said:\'Yes.\' '
```

3、三引号可以直接书写多行，通常用于大段，大篇幅的字符串

```python
"""
hello
.....
world
"""
```

##### 106、python垃圾回收机制

​	python垃圾回收主要以引用计数为主，标记-清除和分代清除为辅的机制，其中标记-清除和分代回收主要是为了处理循环引用的难题。

##### 	**引用计数算法**

​	当有1个变量保存了对象的引用时，此对象的引用计数就会加1

​	当使用del删除变量指向的对象时，如果对象的引用计数不为1，比如3，那么此时只会让这个引用计数减1，即变为2，当再次调用del时，变为1，如果再调用1次del，此时会真的把对象进行删除

##### 107、HTTP请求中get和post区别

​	1、GET请求是通过URL直接请求数据，数据信息可以在URL中直接看到，比如浏览器访问；而POST请求是放在请求头中的，我们是无法直接看到的；

​	2、GET提交有数据大小的限制，一般是不超过1024个字节，而这种说法也不完全准确，HTTP协议并没有设定URL字节长度的上限，而是浏览器做了些处理，所以长度依据浏览器的不同有所不同；POST请求在HTTP协议中也没有做说明，一般来说是没有设置限制的，但是实际上浏览器也有默认值。总体来说，少量的数据使用GET，大量的数据使用POST。

​	3、GET请求因为数据参数是暴露在URL中的，所以安全性比较低，比如密码是不能暴露的，就不能使用GET请求；POST请求中，请求参数信息是放在请求头的，所以安全性较高，可以使用。在实际中，涉及到登录操作的时候，尽量使用HTTPS请求，安全性更好。

##### 108、python中读取Excel文件的方法

![img](https://images2018.cnblogs.com/blog/1303607/201808/1303607-20180828193344989-1961735569.png)

##### 109、简述多线程、多进程

​	**进程：**

​	1、操作系统进行资源分配和调度的基本单位，多个进程之间相互独立

​	2、稳定性好，如果一个进程崩溃，不影响其他进程，但是进程消耗资源大，开启的进程数量有限制

​	**线程：**

​	1、CPU进行资源分配和调度的基本单位，线程是进程的一部分，是比进程更小的能独立运行的基本单位，一个进程下的多个线程可以共享该进程的所有资源

​	2、如果IO操作密集，则可以多线程运行效率高，缺点是如果一个线程崩溃，都会造成进程的崩溃

​	**应用：**

​	IO密集的用多线程，在用户输入，sleep 时候，可以切换到其他线程执行，减少等待的时间

​	CPU密集的用多进程，因为假如IO操作少，用多线程的话，因为线程共享一个全局解释器锁，当前运行的线程会霸占GIL，其他线程没有GIL，就不能充分利用多核CPU的优势

##### 110、python正则中search和match

![img](https://images2018.cnblogs.com/blog/1303607/201808/1303607-20180828193405485-1112631319.png)

111、[类变量和实例变量区别](https://www.cnblogs.com/logo-88/p/8361916.html)

