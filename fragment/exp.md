[TOC]

#### ecs安全设置

* ssh 空闲超时退出时间  etc/ssh/sshd_config 
  * ClientAliveInterval 设置为300到900，即5-15分钟，
  * 将ClientAliveCountMax设置为0-3之间

#### AS javadoc

* 生成javadocs Tools -》GenerateJavaDoc
  - 解决GBK编码错误Other command line arguments”输入-encoding utf-8 -charset utf-8