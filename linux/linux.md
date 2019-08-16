[TOC]



#### 0 linux style

1. 使用命令行
2. 写代码操作命令行（系统调用或glibc）
3. 了解内核机制（目标基本原理和流程）
4. 内核源码（核心逻辑和场景）
5. 定制化linux组件
6. 实战开发

##### 书单

* OSTEP(Operating System Three Easy Picies) 
* Unix/Linux编程实践教程(Understanding UNIX/LINUX Programming)
* 深入理解计算机系统
* 一个64位操作系统的设计与实现
*  从实模式到保护模式
*  《程序员的自我修养-链接、装载和库》

#### 1 系统概述

* 主要组成
  * 系统调用 kernel/
  * 进程管理 kernel/, arch/<arch>/kernel
  * 内存管理 mm/, arch/<arch>/mm
  * 文件 fs/
  * 设备 drivers/char, drivers/block
  * 网络 net/
  
* 常用命令

  * 用户管理 useradd\passwd     目录etc/

  * 文件管理 vim\chmod\chgrp\wget\cat\grep\find

  * 安装软件 export PATH = "xxx":$PATH

    * centos rpm -i\rpm -qa\yum search\yum install \yum erase  

      配置源 /etc/yum.repos.d/CentOS-Base.repo

    * ubuntu dpkg -i\dpkg-l\apt-get install\apt-get purge  

      配置源 /etc/apt/sources.list

  * 运行程序 后台服务systemctrl\ 普通运行./fileName\后台运行nohup 2>&1 &\kill -9\shutdown\reboot

* 新的开始
  * 创建进程 fork\ 执行新的文件execve\ waitpid
  * 内存分配 brk原基础上添加 \mmap 新分配
  * 文件管理 create\open\write\close\定位lseak
  * 进程通信 
    * 消息队列 msgget\msgsnd\msgrcv
    * 共享内存 shmget\shmat
    * 信号量 sem_wait\sem_post
  * 网络通信 socket
  * 信号处理 sigkill\sigaction 自定义处理函数
  * glibc 系统函数api封装 strace 命令追踪

#### 2 系统初始化

*  寄存器、汇编
  * CPU（运算单元、数据单元、控制单元(指令指针寄存器)）内存
  * 数据总线（一次能取多少数据）、地址总线（决定了寻址范围）
  * 通用寄存器 AX、BX、CX、DX、SP、BP、SI、DI
  * CS 代码段寄存器、DS 是数据段的寄存器、SS 是栈寄存器（Stack Register）ES附加段寄存器、IP 是指令指针寄存器
  * 实模式 1M(2^20) 保护模式 4G(2^32)
  * move a b :把b值赋给a,使a=b
    call和ret :call调用子程序，子程序以ret结尾
    jmp :无条件跳
    int :中断指令
    add a b : 加法,a=a+b
    or :或运算
    xor :异或运算
    shl :逻辑左移
    ahr :算术右移
    push xxx :压xxx入栈
    pop xxx: xxx出栈
    inc: 加1
    dec: 减1
    sub a b : a=a-b
    cmp: 减法比较，修改标志位
*  启动系统
  *  ROM上固化BIOS   0xF0000 到 0xFFFFF 这 64K 映射给 ROM
  *  Bootloader Grub2 (Grand Unified Bootloader Version 2 )
    *  grub2-mkconfig -o /boot/grub2/grub.cfg
  *  boot.img MBR -> core.img(diskboot.img\lzma_decompress.img\kernal.img\module)
  *  实模式切换到保护模式  
     *  启用分段, 辅助进程管理
    *  启动分页, 辅助内存管理
  *  grub_command_execute (“boot”, …）启动内核

* 内核初始化
  * init/main.c  start_kernal() 开始  
  * init_task 0号进程
  * trap_init 中断系统
  * mm_init 内存管理
  * sched_init 调度
  * vfs_caches_init()  roofts  文件系统初始化
  * reset_init
    * 1号进程 用户态、准备用户寄存器，用户态-系统调用-保存寄存器-内核态执行系统调用-恢复寄存器-返回用户态。ramdisk 是根文件系。
    * 2号进程 管理内核态进程
* 系统调用
  * glibc 系统调用中介  syscalls.list系统调用映射表 make-syscall.sh宏定义 syscall-template.S 调用方式
  * 32位系统
  * 64位系统
  * 系统调用表 sys_call_table
    * 32位  arch/x86/entry/syscalls/syscall_32.tbl 
    - 64位  arch/x86/entry/syscalls/syscall_64.tbl

#### 3 进程管理

* 进程从代码到执行
  
  * exec 参数 p、v、l、e
  
  * 写代码调用系统进程 -》编译(ELF Executeable and Linkable Format)
  
    -> .o文件（可重定位文件 Relocatable File） -》 .a -》 链接器 -》 可执行文件 --> 动态链接库（Shared Object）
  
  * load_elf_binary 加载elf文件  
  
  * 内核态祖先2号进程 中括号，用户态祖先1号进程
  
  * 工具
  
    * readelf 工具用于分析 ELF 的信息，
    * objdump工具用来显示二进制文件的信息，
    * hexdump 工具用来查看文件的十六进制编码
    * nm 工具用来显示关于指定文件中符号的信息
  
* 线程

  * 为完成进程建立的一项项具体的开发任务，并行执行
    * 多个进程会涉及资源占用、变量共享问题
  * pthread_attr_t声明属性， pthread_attr_init设置属性，PTHREAD_CREATE_JOINABLE表示将来主线程程等待这个线程的结束，并获取退出时的状态。
  * 每个线程都有自己栈空间，栈空间之间会有隔离段，全局数据区，私有数据
  * 条件变量与互斥锁
  
* 任务管理 task_struct

  * 任务id  pid 是 process id，tgid 是 thread group ID
    * 两个id方便展示，也方便下发任务
    * 信号处理函数默认使用用户态的函数栈。
  * 任务状态
    * TASK_INTERRUPTIBLE，可中断的睡眠状态
    * TASK_UNINTERRUPTIBLE，不可中断的睡眠状态
    * TASK_KILLABLE，可以终止的新睡眠状态
  * 运行信息
  * 用户函数栈、内核栈
  
* 调度

  * 针对实时进程（0~99）、普通进程（100~139） 调试策略不同

  * unsigned int policy; 

    ```c
    #define SCHED_NORMAL		0
    #define SCHED_FIFO		1
    #define SCHED_RR		2 时间片轮转
    #define SCHED_BATCH		3
    #define SCHED_IDLE		5
    #define SCHED_DEADLINE		6 距离完成时间最短
    ```

  * CFS 全称 Completely Fair Scheduling  CFS队列是红黑树 虚拟运行时间最小在左侧

  * chrt -p pid 查看当前策略    chrt -p pid -10

  * 主动调度

    * 第一是选取下一个进程，第二是进行上下文切换。而上下文切换又分用户态进程空间的切换和内核态的切换。
  
  * 抢占调试