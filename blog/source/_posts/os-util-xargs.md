---
title: os-util-xargs
date: 2022-07-25 03:41:41
tags: linux os 
---

##  关于xargs实现的一些问题

> [MIT 6.S081: Operating System Engineering](https://pdos.csail.mit.edu/6.828/2021/labs/util.html)

### 背景知识
1. [linux下命令行参数和标准输入](https://zhuanlan.zhihu.com/p/337386886)
2. c指针和数组区别
> 数组用于存放数据，指针用于指向数据
3. string.h中字符串函数使用


### 结论
1. 个人开发少用指针，几乎不会用到二级指针，即 char**
2. char* args[]理解为指针的数组，自己存储了一份指针的值，而char**知识指向指针。 
> 本质是内存分配的问题，是否分配内存



### 解题思路
1. 读取命令和命令行参数
2. 用read()一个一个字节从标准输入读入，以read()==-1结束
> 用 ./grade 输出调试


### code:
```c++
#include "kernel/types.h"
#include "user/user.h"
#include "kernel/param.h"

void debug(char *buf[], int n)
{
    for (int i = 0; i < n; ++i)
    {
        printf("debug-mode arg: %s\n", buf[i]);
    }
}

int main(int argc, char *argv[])
{

    char buf[MAXARG][100];
    char *m[MAXARG];
    char *command = argv[1];
    for (int i = 2; i < argc; ++i)
    {
        strcpy(buf[i - 2], argv[i]);
    }
    int idx = argc - 2;

    char opt = ' ';
    int s = 0;
    while (read(0, &opt, 1) == 1)
    {
        // printf("*%c", opt);
        if (opt == ' ' || opt == '\n')
        {
            if (s == 0)
            {
                continue;
            }
            else
            {
                buf[idx++][s] = 0;
                s = 0;
            }
        }
        else
        {
            buf[idx][s++] = opt;
        }
    }

    if (fork() == 0)
    {
        for (int i = 0; i < idx; ++i)
        {
            m[i + 1] = buf[i];
        }
        m[0] = command;
        m[idx + 1] = 0;
        exec(command, m);
        exit(0);
    }
    else
    {
        wait((int *)0);
    }
    exit(0);
}

```