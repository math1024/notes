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

#### 系统初始化

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

