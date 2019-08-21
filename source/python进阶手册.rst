
python进阶手册
========
sys模块简介
--------

    1. 第一个参数 （sys.args[0]） 表示的始终是执行的文件名，然后依次显示传入的参数
    2. sys.exc_info() 可以显示 Exception 的信息，返回一个 (type, value, traceback) 组成的三元组，可以与 try/catch 块一起使用
    
    ::

        try:
            x = 1/0
        except Exception:
            print sys.exc_info()

    3. sys.path 表示 Python 搜索模块的路径和查找顺序
    4. sys.platform 显示当前操作系统信息

os模块简介[与操作系统交互]
--------

::

    os.remove(path) 或 os.unlink(path) ：删除指定路径的文件。路径可以是全名，也可以是当前工作目录下的路径。
    os.removedirs：删除文件，并删除中间路径中的空文件夹
    os.chdir(path)：将当前工作目录改变为指定的路径
    os.getcwd()：返回当前的工作目录
    os.curdir：表示当前目录的符号
    os.rename(old, new)：重命名文件
    os.renames(old, new)：重命名文件，如果中间路径的文件夹不存在，则创建文件夹
    os.listdir(path)：返回给定目录下的所有文件夹和文件名，不包括 '.' 和 '..' 以及子文件夹下的目录。（'.' 和 '..' 分别指当前目录和父目录）
    os.mkdir(name)：产生新文件夹
    os.makedirs(name)：产生新文件夹，如果中间路径的文件夹不存在，则创建文件夹
   
os.environ 是一个存储所有环境变量的值的字典，可以修改

os.path模块
--------
不同的操作系统使用不同的路径规范，这样当我们在不同的操作系统下进行操作时，可能会带来一定的麻烦，而 os.path 模块则帮我们解决了这个问题。

::

    通用算法
    os.path.isfile(path) ：检测一个路径是否为普通文件
    os.path.isdir(path)：检测一个路径是否为文件夹
    os.path.exists(path)：检测路径是否存在
    os.path.isabs(path)：检测路径是否为绝对路径
    split 和 join
    os.path.split(path)：拆分一个路径为 (head, tail) 两部分
    os.path.join(a, *p)：使用系统的路径分隔符，将各个部分合成一个路径
    其他
    os.path.abspath()：返回路径的绝对路径
    os.path.dirname(path)：返回路径中的文件夹部分
    os.path.basename(path)：返回路径中的文件部分
    os.path.slitext(path)：将路径与扩展名分开
    os.path.expanduser(path)：展开 '~' 和 '~user'

函数进阶
--------

在 Python 中，函数是一种基本类型的对象，这意味着

    1. 可以将函数作为参数传给另一个函数
    2. 将函数作为字典的值储存
    3. 将函数作为另一个函数的返回值

::

    def add(x,y):
        return x+y

    def sub(x,y):
        return x-y

    funcs=[add,sub]

    print(funcs[1](2,3))

引用传递
--------

Python 中的函数传递方式是 call by reference 即引用传递，这一点和java一样，函数内修改了引用相关对象的值，
函数调用后相关的值仍然会改变

::

    def mod_f(x):
        x[0] = 999
        return x

    x = [1, 2, 3]

    print x  
    print mod_f(x)
    print x

    输出：
        [1, 2, 3]
        [999, 2, 3]
        [999, 2, 3]

可变的默认参数
-----------
函数可以传递默认参数，默认参数的绑定发生在函数定义的时候，以后每次调用默认参数时都会使用同一个引用

::

    def f(x = []):
        x.append(1)
        return x

    print f()
    print f()
    print f()
    print f(x = [9,9,9])
    print f()
    print f()

    最终的效果：

    [1]
    [1, 1]
    [1, 1, 1]
    [9, 9, 9, 1]
    [1, 1, 1, 1]
    [1, 1, 1, 1, 1]


高阶函数
-----------
以函数作为参数，或者返回一个函数的函数是高阶函数，常用的例子有 map 和 filter 函数

::
    filter(f, sq) 函数的作用相当于，对于 sq 的每个元素 s，返回所有 f(s) 为 True 的 s 组成的列表
    filter(is_even, range(5))

    map(f, sq) 函数将 f 作用到 sq 的每个元素上去，并返回结果组成的列表
    map(square, range(5))

    reduce(f, sq) 函数接受一个二元操作函数 f(x,y)，并对于序列 sq 每次合并两个元素：
    reduce(my_add, [1,2,3,4,5]) 求和

    返回一个函数：

    def make_logger(target):
        def logger(data):
            with open(target, 'a') as f:
                f.write(data + '\n')
        return logger

    foo_logger = make_logger('foo.txt')

global变量
----------- 

一般来说，函数中是可以直接使用全局变量的值的，但是要在函数中修改全局变量的值，需要加上 global 关键字，如果不加上这句 global 那么全局变量的值不会改变