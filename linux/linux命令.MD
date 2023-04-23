# linux安装后配置


# 安装使用ifconfig命令
1. 查看网络接口详情，需要 net-tools 工具包，若没有被默认安装，就不能使用 ifconfig，安装 net-tools命令：
sudo apt-get install net-tools
2.查看网络接口详情：
ifconfig


# 安装 OpenSSH 服务器
1.安装完成后，就可以通过Xshell等访问
sudo apt install openssh-server
2.安装完成后，请确保 OpenSSH 服务器已启动。通过运行以下命令来检查它的状态：
sudo systemctl status ssh
    2.1如果 OpenSSH 服务器尚未启动，通过运行以下命令来启动它：
    sudo systemctl start ssh
3.设定 OpenSSH 服务器随系统启动而自动启动，运行以下命令：
sudo systemctl enable ssh


# 安装lrzsz
0.可以通过Xshell 往linux里传文件
sudo apt install lrzsz


# 安装curl
sudo apt install curl


# 安装jdk
1.将jdk.tar.gz上传至自己创建的文件夹中
2.解压
tar -zxvf jdk.tar.gz
 2.1为了待会配置环境变量的时候方便，将文件夹名字改为jdk
 mv jdk1.8.0_161/ jdk
3.配置环境变量
移动到根目录
cd ../..
用vim编辑etc/profile文件，在最下面根据jdk文件位置添加如下信息
JAVA_HOME=/home/lsgf/environment/jdk/jdk1.8.0_161
PATH=/home/lsgf/environment/jdk/jdk1.8.0_161/bin:$PATH
export JAVA_HOME PATH
按ESC后输入:wq推出并保存
4.重新加载此文件
source /etc/profile
5.测试
javac


# 安装zookeeper
1.安装curl
sudo apt install curl
2.将apache-zookeeper-3.8.0-bin.tar.gz上传至linux文件夹中
3.在文件夹下使用命令解压
tar -zxvf apache-zookeeper-3.8.0-bin.tar.gz
4.进入到conf目录拷贝一个zoo_sample.cfg并完成配置
cd apache-zookeeper-3.8.0-bin/conf
cp  zoo_sample.cfg  zoo.cfg
5.在合适目录创建data文件夹
cd ..
mkdir  data
6.修改zoo.cfg
vim conf/zoo.cfg
 6.1若报错，则需安装vim，命令如下：
 sudo apt install vim
修改存储目录：
dataDir=/???/ZooKeeper/zkdata
7.启动zk
在bin/目录下启动server
./zkServer.sh  start
 7.1若报错Error: JAVA_HOME is not set and java could not be found in PATH.则需安装JAVA环境并配置环境变量


# 安装redis
1.安装redis之前先安装C++编译环境，使用以下命令查看目前服务器上gcc的版本：
gcc -v
    1.1 Linux系统没有安装gcc编译器，du会提示“Command not found，则按以下步骤安装gcc -c++
    sudo apt update
    sudo apt install build-essential
    安装后再查看下gcc版本
    gcc -v
2.上官网下载Redis 压缩包，地址：https://redis.io/download 下载稳定版即可
3.将压缩包拷贝到Linux服务器中，一般服务器之外的第三方软件装在opt这个文件夹中，执行解压操作。
tar xzf redis-6.0.4.tar.gz
4.进入到解压后的路径
cd redis-6.0.4
5.编译
make
    5.1若报错 pkg-config:not found，则安装pkg-config，即
    sudo apt-get install pkg-config
6.编译完成后进入src目录下
cd src
7.开启redis服务
./redis-server
8.启动成功后会显示redis的pid，如有需要，按住crtl+c 可以退出服务.
9.两种方式设置密码
    a.在redis-cli客户端输入以下命令(无需重启服务)
    config set requirepass 123456
    b.redis的配置文件—redis.conf文件，然后修改里面的requirepass，这个本来是注释起来了的，将注释去掉，并将后面对应的字段设置成自己想要的密码，保存退出。重启redis服务，即可。


# 安装yum命令（未成功）
1.安装
sudo apt install yum
如果报错，在ubuntu下按顺序执行以下步骤
1.在根目录下执行以下操作，备份sources.list文件
sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak
2.打开sources.list文件
sudo gedit /etc/apt/sources.list
3.删除源文件所有数据
4.粘贴以下内容到文件中

# 默认注释了源码镜像以提高 apt update 速度，如有需要可自行取消注释
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy-updates main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy-updates main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy-backports main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy-backports main restricted universe multiverse
# deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy-security main restricted universe multiverse
# # deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy-security main restricted universe multiverse
deb http://security.ubuntu.com/ubuntu/ jammy-security main restricted universe multiverse
# deb-src http://security.ubuntu.com/ubuntu/ jammy-security main restricted universe multiverse

 4.1 如果以上链接失效，可去网站https://mirrors.tuna.tsinghua.edu.cn/，找到Ubuntu，点击它旁边的问号！重要！点问号！进去之后就会发现你想要的源

5.更新下
sudo apt-get update
6.最后我们最开始的需求是，安装yum
sudo apt-get install yum





# 安装docker （未亲自尝试成功）
1.安装（需要curl）
curl -fsSL https://get.docker.com | bash -s docker --mirror Aliyun
    1.1若上面命令不行，可尝试：curl -sSL https://get.daocloud.io/docker | sh
2.安装docker之后，暂时只能用root权限使用，根据提示，需要使用以下命令让普通用户可以使用
dockerd-rootless-setuptool.sh install
3.操作完成之后可能还需要添加环境变量（以命令行上的提示为准），将以下命令添加到~/.bashrc文件里
export PATH=/usr/bin:$PATH
export DOCKER_HOST=unix:///run/user/1000/docker.sock
4.测试一下
docker run hello-world


# 解决 E: Unable to lock directory /var/lib/apt/lists/ 问题
sudo fuser -vki /var/lib/apt/lists/lock


# linux常用命令

# 删除文件
rm -f 文件名
# 删除文件夹
rm -rf 文件夹

# 查看与某主机是否能联通
ping：

ps -ef|grep 进程名称：查看进程号

lost -i 端口 ：查看端口占用情况

top:查看系统负载情况，包括系统时间、系统所有进程状态、cpu情况

free:查看内存占用情况

kill:正常杀死进程，发出的信号可能会被阻塞

kill -9:强制杀死进程，发送的是exit命令，不会被阻塞

# 2.防火墙firewall

执行关闭命令： systemctl stop firewalld.service

执行开机禁用防火墙自启命令  ： systemctl disable firewalld.service

执行查看防火墙命令：systemctl status firewalld.service

启动：systemctl start firewalld.service

防火墙随系统开启启动  ： systemctl enable firewalld.service