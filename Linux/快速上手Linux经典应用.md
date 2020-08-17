# 快速上手Linux经典应用

## 1、Linux简介

服务器一般使用Linux操作系统

常见发行版版：Ubuntu、centos、Redhat、Linux min、xfce

### 能做什么？

服务器开发、嵌入式开发

### Linux的学习方法

- 给自己一个Linux环境
- 先自己尝试搜索解决问题
- 学会读懂Linux的错误提示

### 忘掉Windows的所有东西

- 没有exe安装程序
- 大小写是要区分的
- 一切皆文件
- 文件后缀名不是那么重要，只是为了好识别而已

## 2、Centos安装

### 虚拟机是什么

在一个系统上运行另一个系统

virtual box 和VMware

### 安装虚拟机

### 云服务器

阿里云

腾讯云

华为云

网易蜂巢

## 3、准备工作

查看IP

- ifconfig
- Ip addr
- vi /etc/sysconfig/network-scripts/ifcfg-xx

替换默认源

http://mirrors.163.com/.help/centos.html

安装vim

yum install vim

## 4、远程连接SSH

### ssh是什么

SSH：Secure Shell 安全外壳协议

建立在应用层基础上的安全协议

可靠，专为远程登录会话和其他网络提供安全性的协议

特点：

- 有效防止远程管理过程中的信息泄露问题
- SSH客户端适用于多种平台
- SSH服务端几乎支持所有UNIX平台

### 服务器安装SSH服务

安装SSH

yum install openssh-server

启动SSH

Service sshd start

设置开机运行

chkconfig sshd on

### 客户端安装SSH工具

Linux平台需要安装客户端软件

yum install openssh-clients

Windows平台

xshell

macOS平台

FinalShell

### 客户端连接ssh服务 

ssh root@118.89.186.38

### SSH config 配置

- config为了方便我们批量管理多个ssh
- config存放在 ~/.ssh/config
- config配置语法

```shell
host "mogo1"
				Hostname 118.89.186.38
				User mogo
				port 22
host "mogo2"
				Hostname 118.89.186.38
				User mogo
				port 22
```

|     Host     | 别名           |
| :----------: | -------------- |
|   HostName   | 主机名         |
|     Port     | 端口           |
|     User     | 用户名         |
| IdentityFile | 秘钥文件的路径 |

### SSH安全免密码登录：ssh Key

- ssh key 使用非对称加密方式生成公钥 和 私钥
- 私钥存放在本地~/.ssh目录
- 公钥可以对外公开，放在服务器的~/.ssh/authorized_keys（vim编辑）

LInux平台生成keys

ssh-keygen -t rsa

ssh-keygen -t dsa



Linux 加载秘钥的命令

ssh-add ~/.ssh/imooc_test



### ssh端口安全

端口安全指的是尽量避免服务器的远程端口被不法分子知道，为此而改变默认服务端口的操作。

修改端口： vim /etc/ssh/sshd_config

服务生效：service sshd restart

## 5、Linux常用命令

### 软件操作命令

- 软件包管理器：yum
- 安装软件：yum install xxx
- 卸载软件：yum remove xxx
- 搜索软件：yum serach xxx
- 清理缓存：yum clean packages
- 列出已安装：yum list
- 软件包信息：yum info xxx

### 服务器硬件资源信息

- 内存：free -m
- 硬盘：df -h
- 负载：w/top
  - load average:0.00, 0.01, 0.05 | 1分钟、5分钟、15分钟的负载
  - 达到1的时候非常危险，超过1时，超频运行。
  - 0.6、0.7都是一个健康值。
- CPU个数和核数
  - cat  /proc/cpuinfo
- 格式化磁盘
  - fdisk

### 文件操作命令

#### Linux文件的目录结构

- 根目录/
- 家目录/home
- 临时目录/tmp
- 配置目录/etc
- 用户程序目录/usr

#### 文本的基本操作

| 命令             | 解释             |
| ---------------- | ---------------- |
| ls               | 查看目录下的文件 |
| touch            | 新建文件         |
| mkdir (-p)       | 新建文件夹       |
| cd               | 进入目录         |
| rm(rm-r)/(rm-rf) | 删除文件和目录   |
| mv               | 移动             |
| cp               | 复制             |
| pwd              | 显示路径         |



#### vim命令

| 命令                 | 解释     |
| -------------------- | -------- |
| i                    | 插入     |
| ：wq                 | 保存     |
| G                    | 末尾     |
| gg                   | 行首     |
| dd                   | 删除行   |
| u                    | 恢复     |
| esc                  | 退出模式 |
| yy(选择行) + p(复制) | 复制     |
| :set number          | 显示行数 |
|                      |          |
|                      |          |
|                      |          |
|                      |          |
|                      |          |



#### 文件权限421

R W X | 4 2 1

#### 文件搜索、查找、读取

| 命令                        | 解释             |
| --------------------------- | ---------------- |
| tail                        | 从文件尾部开始读 |
| head                        | 从文件头部开始读 |
| cat                         | 读取整个文件     |
| more                        | 分页读取         |
| lees                        | 可控分页         |
| grep -n ""                  | 搜索关键字       |
| find(find .)( -name)(-type) | 查找文件         |
| wc  （cat imooc \| wc -l)   | 统计个数         |



#### 文件的压缩和解压

tar命令

man tar可以查看tar的命令帮助

```shell
tar - cf all.tar *.jpg
```

这条命令是所有.jpg的文件打成一个名为 all.tar 的包。-c产生新的包，-f指定包的文件名。

```shell
tar -rf all.tar *.gif
```

这条命令是将所有.gif的文件增加到all.tar的包里面去，-f是表示增加文件的意思。

```shell
tar -uf all.tar logo.gif
```

这条命令是更新原来tar包 all.tar中logo.gif文件， -u是表示更新文件的意思。

```shell
tar -tf all.tar
```

这条命令是列出all.tar包中所有文件，-t是列出文件的意思。-v详细信息。

```shell
tar -xf all.tar
```

这条命令是解出all.tar包中所有文件，x是解开的意思。

### 系统用户操作命令

| 命令    | 解释     |
| ------- | -------- |
| useradd | 添加用户 |
| adduser | 添加用户 |
| userdel | 删除用户 |
| passwd  | 设置密码 |

cd /home/

### 防火墙

安装：yum install firewalld

启动：service firewalld start

检查状态：service firewalld status

关闭或禁用防火墙：service firewalld stop/disable

### 提权和文件上传下载

- 提权：sudo
  - visudo
- 文件下载
  - wget curl
- 文件上传
  - scp
    - scp imooc.txt imooc@192.168.0.106:/tmp/
    - 下载：scp imooc@192.168.0.106:/tmp/imooc.txt ./



## Webserver

### Apache

yum install httpd

service httpd start

service httpd stop

sudo netstat -anpl | grep 'http'

配置：



### NGINX



### git

yum install git

| git config | git init   |
| ---------- | ---------- |
| git clone  | git remote |
| git fetch  | git commit |
| git rebase | git push   |

