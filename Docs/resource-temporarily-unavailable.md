# python multiprocessing 报错 [Errno 11] Resource temporarily unavailable

## 参考内容

* https://blog.csdn.net/boshuzhang/article/details/50608499

在linux进行非阻塞的socket接收数据时经常出现Resource temporarily unavailable，errno代码为11(EAGAIN)，这表明你在非阻塞模式下调用了阻塞操作，在该操作没有完成就返回这个错误。

对非阻塞socket而言，EAGAIN不是一种错误。在VxWorks和Windows上，EAGAIN的名字叫做EWOULDBLOCK。

* https://zhuanlan.zhihu.com/p/260199751

## 场景分析

在 python 语言编写的工具中，使用multiprocessing时，报此错误，模拟此操作，编写 test.py

```python
# -*- coding: utf-8 -*-
import fcntl, os, time
import multiprocessing

def main():
    manager = multiprocessing.Manager()
    MPA = manager.list()
    MPA.append("test")
    print ( len(MPA) )
    for mp in MPA:
        print (mp)
    # 此处暂停，另外启动终端，使用 lsof 查看执行此文件的进程
    time.sleep(100000)

if __name__ == '__main__':
    main()
```

执行test.py，另外启动终端，使用 lsof 查看执行此文件的进程信息

```
$ lsof -p 61005
COMMAND   PID    USER   FD   TYPE DEVICE SIZE/OFF      NODE NAME
python  61005 jenkins    0u   CHR  136,1      0t0         4 /dev/pts/1
python  61005 jenkins    1u   CHR  136,1      0t0         4 /dev/pts/1
python  61005 jenkins    2u   CHR  136,1      0t0         4 /dev/pts/1
python  61005 jenkins    4u  sock    0,8      0t0 251725295 protocol: UNIX
```

可以看到fd为4的连接是 protocol: UNIX，参考 https://blog.csdn.net/weixin_33617691/article/details/116621891

linux下进程间使用套接字通信(socket)时，有三种模型，参考 http://dljz.nicethemes.cn/news/show-331328.html

- 针对 TCP 协议通信的 socket 编程模型
- 针对 UDP 协议通信的 socket 编程模型
- 针对本地进程间通信的 socket 编程模型

python 使用 multiprocessing 的时候，即本地进程间的通信，会启动名为 `protocal: UNIX` 的 fd。如果将此fd设置为非阻塞，则会出现此问题。

写一个方案测试

```python
# -*- coding: utf-8 -*-
import fcntl, os, time
import multiprocessing

def main():
    manager = multiprocessing.Manager()
    MPA = manager.list()
    # 测试占用fd 4
    MPA.append("test")
    # 测试中 multiprocessing 占用的是 4，根据测试的实际情况设置
    fd = 4
    flags = fcntl.fcntl( fd, fcntl.F_GETFL )
    flags |= os.O_NONBLOCK
    fcntl.fcntl( fd, fcntl.F_SETFL, flags )
    print ( len(MPA) )
    for mp in MPA:
        print (mp)
    # 此处暂停，另外启动终端，使用 lsof 查看执行此文件的进程
    time.sleep(100000)

if __name__ == '__main__':
    main()
```


## 其他场景

根据场景分析中的内容，如果程序中调用了其他语言设置此内容，会产生相同的问题，比如使用C语言编写 `z.c`，设置fd 4为非阻塞

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <fcntl.h>
#include <error.h>

int main(int argc, char *argv[])
{
    # 测试占用fd 4
    int m_sockfd = 4;

    int flags = fcntl(m_sockfd, F_GETFL, 0);
    if(flags == -1)
    {
        perror("fcntl F_GETFL fail:");
        exit(1);
    }

    flags |= O_NONBLOCK;
    int retval = fcntl( m_sockfd, F_SETFL, flags );
    if(retval < 0)
    {
        perror("fcntl F_SETFL fail:");
        exit(1);
    }
    return 0;
}
```

然后通过python执行此文件，也会报此错误

```python
# -*- coding: utf-8 -*-
import fcntl, os, time
import multiprocessing

def main():
    manager = multiprocessing.Manager()
    MPA = manager.list()
    # 测试占用fd 4
    MPA.append("test")
    # 测试中 multiprocessing 占用的是 4，根据测试的实际情况设置
    os.system("cd /home/yang && gcc z.c && ./a.out")
    print ( len(MPA) )
    for mp in MPA:
        print (mp)
    # 此处暂停，另外启动终端，使用 lsof 查看执行此文件的进程
    time.sleep(100000)

if __name__ == '__main__':
    main()
```