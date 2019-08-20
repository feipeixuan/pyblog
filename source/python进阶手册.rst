
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