
Python手册
========
快速入门
--------

::

    三种运行:交互式的启动解释器、命令行启动脚本、集成开发环境

    特殊字符: 
         单行:#   多行 ''' '''
         换行\: 继续上一行
         赋值=: x,y,z=1,2,3  
         下划线标识符：_XXX类中的私有变量名
         ** 代表乘方

    字符串重要的操作符: 
         说明：[] 索引操作符、[i:j] 切片操作符，最后一个索引是 -1 ，引入了负索引值的用法，即从后向前开始计数
              [m:n:k] 切片具体用法 : m索引开始的地方,n索引结束的地方+1,k步长，根据k来计算索引，根据索引去取值
                    
         案例：如果是[3:5] 是从3开始到4结束 [3] 是从3到最后，，即 [lower, upper)

    列表相关的重要操作符:
         说明： 切片运算[:] 可以得到子集，这点和字符串相同
               + 列表连接 *2 元素重复相加
               del 删除元素 del xx[0]
               in 判断是否是从属 if xxx in array 
               indexof 是获取索引、sort是排序、reverse是反转
               

    字典
         说明： dict 或者 {} for key in dict
               出于hash的目的，Python中要求这些键值对的键必须是不可变的，而值可以是任意的Python对象。
               删除元素使用pop 或者 del["22"]
               in 可以用来判断字典中是否有某个特定的键
               keys 方法，values 方法和items 方法

    分支结构
         注意：代码块缩进，区分不同的代码块，可以使用 and ， or , not 等关键词结合多个判断条件：
              大部分表达式的值都会被当作True，但以下表达式值会被当作False：
                False、None、0、空字符串，空列表，空字典，空集合
         案例：     if <condition 1>:
                        <statement 1>
                        <statement 2>
                   elif <condition 2>: 
                        <statements>
                   else:
                        <statements>           

    for循环与range
         说明： 接受可迭代对象，每次迭代取一个元素，
               range()函数得到的其实是一个iterable类型，在python里解释为可以迭代的对象，可以使用for来遍历产生的结果，使用list()将结果转化为列表类型 
               推荐使用 for i in xrange(100000) 来完成迭代计算，range会生成临时列表，xrange则不会,xrange返回的是一个生成器，
                       一边循环一边计算，每次只返回一个值，这样就不必开辟这么大的内存空间了。
               在python3.x中，xrange被废除了，range功能跟xrange相同
                       
               搭配else:
                      与 if 一样， while 和 for 循环后面也可以跟着 else 语句，不过要和break一起连用。
                            当循环正常结束时，循环条件不满足， else 被执行；[Else clause on loop without a break statement]
                            当循环被 break 结束时，循环条件仍然满足， else 不执行        

    列表解析
         说明： [expression for iter_val in iterable if cond_expr] 使用循环将所有值放入一个列表中
         案例： squares = [x**2 for x in values if x <= 10]、{x: x**2 for x in values if x <= 10}

    错误和异常
         说明：  python无法正常处理程序，就会产生一个异常，try except语句可以捕获或者处理异常   
                使用Exception类来捕获所有的异常
         案例：
                try:
                    <语句>        #运行别的代码
                    except <名字>：
                    <语句>        #如果在try部份引发了'name'异常 
                    except <名字> as <数据>: 可以获取异常的具体信息
                    <语句>        #如果引发了'name'异常，获得附加的数据
                    else:
                    <语句>        #如果没有异常发生  
                finally: 无论是否有异常，这块代码总会执行
                    print("123")    

    函数定义
          不定参数：*args 表示参数数目不定，可以看成一个元组，把第一个参数后面的参数当作元组中的元素
                  **kwargs 表示参数数目不定，相当于一个字典，关键词和值对应于键值对

          返回多个值：
               return r, theta        

          案例：
               def foo(*args, **kwargs):
                    print args, kwargs
               foo(2, 3, x='bar', z=10)
               r, theta = to_polar(3, 4)
                        



========
开发模板
========

.. image:: images/python/template.png
   :height: 600px
   :width: 500px

::

    __name__如何能区分能在运行时检测该模块是被导入还是被直接执行呢？
    1。如果模块是被导入，__name__的值为模块名字；
    2.如果模块是被直接执行，__name__的值为‘main’
    3.将测试代码放在一个叫做main()或test()（或者你随便取个名字）的函数中，如果该模块是被当成脚本运行，就调用这个函数


========
内存管理
========

::

    1.无需声明，直接定义
    2.动态类型 
    3.自动完成内存分配回收【不智能】：变量引用对象，计算对象被不同变量引用的个数决定对象的生命周期
        3.1 引用计数法
            增加计数：对象被创建并（将其引用）赋值给变量时，该对象的引用计数就+1
            减小计数：
                    当变量被赋值给另外一个对象时
                    引用的局部变量被销毁
                    del 删除一个引用变量
        3.2 垃圾收集说明
            一个循环引用发生在当你有至少两个对象互相引用时，也就是说所有的引用都消失时，这些
            引用仍然存在，这说明只靠引用计数是不够的。Python的垃圾收集器实际上是一个引用计数
            器和一个循环垃圾收集器。当一个对象的引用计数变为0,解释器会暂停，释放掉这个对象和仅
            有这个对象可访问 （可到达）的其他对象。作为引用计数的补充，垃圾收集器也会留心被分
            配的总量很大的（及未通过引用计数销毁的那些）对象。在这种情况下，解释器会暂停下
            来，试图清理所有未引用的循环。            
    
    4.id函数:返回对象的内存地址,is:来判断是不是指向同一个事物 
    5.Python会为每个出现的对象进行赋值，哪怕它们的值是一样的，不过，为了提高内存利用效率，对于一些简单的对象，如一些数值较小的int对象，Python采用了重用对象内存的办法     

========
类型说明
========

::

    1.获取数据类型的内建函数type
    2.所有类型对象的类型都是type,它也是所有Python类型的根和所有Python标准类的默认元类（metadass）
    3.空对象、值为零的任何数字或者Null对象None的布尔值都是False
    4.Python提供了 is和is not操作符来测试两个变量是否指向同一个对象。
      type()和 isinstance(变量名，(类型))
    5.del 删除对象相关的引用，具体回收内存要垃圾回收器 
    6.整型 等价于C中的有符号长整型（long），与系统的最大整型一致,在Python 2.7中，整型的运算结果只能返回整型，
    7.长整型 是整型的超集，可以表示无限大的整数（实际上只受限于机器的虚拟内存大小），长整型字面值的后面带有字母“L”或“l，当整型超出范围时，Python会自动将整型转化为长整型，不过长整型计算速度会比整型慢
    8.浮点型 类似于C中的双精度浮点型（double）
    9.字符串不可变【Immutable】、列表是可变的 【Mutable】

.. image::
    images/python/mutable.png


========
模块相关
========  

::

    函数:将一组代码组织到一起，实现某种功能
    模块:为实现某种逻辑将相关连的函数写在同一个文件里，使逻辑更清楚，这就是一个模块,在python中文件以.py 结尾，那这个.py文件就可以称之为模块
    包：方便管理模块，python 中引入了包的概念，包是由关联的多个模块组成的目录，包下而都有一个__init__.py文件否则就是普通目录

    引入模块：
            import:导入模块的所有 import xx ,引用xx.a xx.b，import ex2 as e2 设置别名
            from import:导入模块的部分 
                from xx import yyy 或者 from os import * ,引用 yyy
                由于引用的时候没有模块的前缀，可能导致重名函数打乱命名空间
    
    Python import 的搜索路径：
            在当前目录下搜索该模块
            在环境变量 PYTHONPATH 中指定的路径列表中依次搜索
            在 Python 安装路径的 lib 库中搜索

    绝对导入和相对导入：
            绝对导入：一个模块只能导入自身的子模块或和它的顶层模块同级别的模块及其子模块
            相对导入：参照当前所在文件的文件夹为起始开始查找,称之为相对导入
                     符号: .代表当前所在文件的文件加,..代表上一级文件夹,...代表上一级的上一级文件夹
                     优点: 导入更加简单
                     缺点: 只能在导入包中的模块时才能使用,不能在执行文件中用

     常用库列表：
          re 正则表达式
          copy 复制
          math, cmath 数学
          decimal, fraction
          sqlite3 数据库
          os, os.path 文件系统
          gzip, bz2, zipfile, tarfile 压缩文件
          csv, netrc 各种文件格式
          xml
          htmllib
          ftplib, socket
          cmd 命令行
          pdb
          profile, cProfile, timeit
          collections, heapq, bisect 数据结构
          mmap
          threading, Queue 并行
          multiprocessing
          subprocess
          pickle, cPickle
          struct                

========
学习资料
========   

::

    相关模块和开发工具:
       1.相关书籍： Python风格指南、Python快速参考指南和Python常见问答
       2.相关模块： 调试器：pdbo 记录器：logging 性能测试器：profile、hotshot、cProfile

    博客：
       1.http://lijin-thu.github.io/ python入门知识+进阶知识讲解   

========
文件管理
========   

::

     基本操作：
          open 函数指定文件路径及操作类型 open("aaa.csv","r")
     
     附加说明：
          二进制读写模式 b
          在Python中，如果一个打开的文件不再被其他变量引用时，它会自动关闭这个文件。所以正常情况下，如果一个文件正常被关闭了，忘记调用文件的 close 方法不会有什么问题。
               关闭文件可以保证内容已经被写入文件，而不关闭可能会出现意想不到的结果
   
    
            
