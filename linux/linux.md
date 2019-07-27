#### 0 前期准备

1. 使用命令行
2. 写代码操作命令行（系统调用或glibc）
3. 了解内核机制（目标基本原理和流程）
4. 内核源码（核心逻辑和场景）
5. 定制化linux组件
6. 实战开发

#### 1 核心原理

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

    

