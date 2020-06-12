[TOC]

####  os comand

1. 登录: ssh [ -p port 可选 ]name@ip

2. 查看系统版本 cat /proc/version

3. 查看用户 users，whoami， cat /etc/passwd | cut -d: -f 1

4. 新增用户 adduser name， passwd name ，

5. 更新用户权限  chmod -v u+w /etc/sudoers， chmod -v u-w /etc/sudoers， 

   ```shell
   root ALL=(ALL) ALL # add below this line 
   dev ALL=(ALL) ALL 
   ```

6. 查看文件详细信息 ls -al

7. ps命令有一些参数： 
   -e : 显示所有进程 
   -f : 全格式 
   -h : 不显示标题 
   -l : 长格式 
   -w : 宽输出 
   a ：显示终端上的所有进程，包括其他用户的进程。 
   r ：只显示正在运行的进程。 
   u ：以用户为主的格式来显示程序状况。 
   x ：显示所有程序，不以终端机来区分。
   
8. ipcs\ipcrm

#### soft command

1. 安装py3， pip3
   *  yum -y install zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel readline-devel tk-devel gdbm-devel db4-devel libpcap-devel xz-devel
   * wget https://www.python.org/ftp/python/3.A.B/Python-3.A.B.tgz  [python link](https://www.python.org/ftp/python/)
   * mkdir /usr/local/python3
   * tar -zxvf Python-3.A.B.tgz ， cd Python-3.A.B
   * ./configure --prefix=/usr/local/python3, 
   *  make && make install **(要sudo执行)**
   * ln -s /usr/local/python3/bin/python3 /usr/bin/python3
   * ln -s /usr/local/python3/bin/pip3 /usr/bin/pip3 
2. spider
  
* pip3 install requets, selenium,beautifulsoup4,pymongo
  
3. mongodb 172.24.243.26 39.104.127.247

   * wget https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-4.0.4.tgz
   * tar -xvzf mongodb-linux-x86_64-4.0.4.tgz 
   * mv mongodb-linux-x86_64-3.6.3 /usr/mongodb
   * add this line "export PATH=$PATH:/usr/mongodb/bin" in file etc/profile 
   * 开 mongod --config /usr/mongodb/mongodb.conf
   * 关 mongod -f XXX/mongodb.conf --shutdown

4. ubuntu apt-get

   ```shell
   apt-get update//更新安装列表
   apt-get upgrade//升级软件
   apt-get install software_name //安装软件
   apt-get --purge remove  software_name //卸载软件及其配置
   apt-get autoremove software_name//卸载软件及其依赖的安装包
   ```


5. grep 

```shell
# 排除指定字符串
grep -v
# 排除指定目录，注意转义\ =前后不能有空格
grep -r --exclude-dir=\.svn

```

6. dd

```shell
# dd命令，可以从标准输入或指定的文件中读取数据，拷贝至新文件
dd if=/dev/zero of=big_file count=10 bs=1G
# time 查看时间
time dd if=/dev/zero of=big_file count=10 bs=1G
```

7. fallocate

```shell
# fallocate命令可以为文件预分配物理空间。-l后接空间大小，默认单位为字节。也可后跟k、m、g、t、p、e来指定单位，分别代表KB、MB、GB、TB、PB、EB。
fallocate -l 10G big_file

# 创建的文件是真实大小
du -sh big_file
10G    big_file
```

8. truncate

```shell
# truncate命令可以将文件缩减或扩展为指定大小，使用-s参数设置大小。
truncate -s 10G big_file

# 分别使用ls与du查看文件大小，创建的文件并不是真实大小
ls -lh big_file 
-rw-r--r-- 1 root root 10G Jun  2 11:11 big_file

$ du -sh big_file 
0    big_file
```

