
Linux 命令大全
========
监控类的命令
--------

===========  =========================
命令                  备注
===========  =========================
nethogs        查看进程带宽网络占用
netstat        显示与IP、TCP、UDP和ICMP协议相关的统计数据
ps             显示系统中当前运行的那些进程
===========  =========================

:: 
   
   nethogs:查看进程带宽网络占用
    -d : delay for update refresh rate in seconds. default is 1. //延迟刷新时间，单位秒，默认1秒
    -t : tracemode. //跟踪模式
    -b : bughunt mode - implies tracemode. //bughunt模式
    -p : sniff in promiscious mode (not recommended). //混合模式下嗅探，不推荐
     r : Sort by received. //按received进行排序
     s : Sort by sent. //按send进行排序
     

::
   
   netstat:显示与IP、TCP、UDP和ICMP协议相关的统计数据
    -c : --continuous 不断地每秒输出所选的信息。
    -e : --extend 显示附加信息。使用这个选项两次来获得所有细节。
    -o : --timers 包含与网络定时器有关的信息。
    -p : --program 显示套接字所属进程的PID和名称。
    -l : --listening 只显示正在侦听的套接字(这是默认的选项)
    -a : --all 显示所有正在或不在侦听的套接字。
    -n : 以网络IP地址代替名称，显示出网络连接情形
    -t : 指明显示TCP端口
    -u : 指明显示UDP端口

    查看端口是否占用:netstat -an | grep 22

::
   
   ps:显示系统中当前运行的那些进程 Process Status
   -A : 所有的进程均显示出来，与 -e 具有同样的效用；
   -a : 显示现行终端机下的所有进程，包括其他用户的进程；
   -u : 以用户为主的进程状态 ；
   -x : 通常与 a 这个参数一起使用，可列出较完整信息
   -aux :    显示所有包含其他使用者的行程

   ps ax ps -e 查看所有进程 
   ps e 列出程序时，显示每个程序所使用的环境变量
   ps -A 显示所有进程
   ps -H 显示树状结构，表示程序间的相互关系
   ps -N 显示所有的程序，除了执行ps指令终端机下的程序之外

   

    