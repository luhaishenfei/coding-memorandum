# linux安装后配置


# 1. 查看网络接口详情，需要 net-tools 工具包，若没有被默认安装，就不能使用 ifconfig，安装 net-tools命令：
sudo apt-get install net-tools
# 查看网络接口详情：
ifconfig


# 2. 安装 OpenSSH 服务器，安装完成后，就可以通过Xshell等访问
sudo apt install openssh-server
# 安装完成后，请确保 OpenSSH 服务器已启动。通过运行以下命令来检查它的状态：
sudo systemctl status ssh
# 如果 OpenSSH 服务器尚未启动，通过运行以下命令来启动它：
sudo systemctl start ssh
# 设定 OpenSSH 服务器随系统启动而自动启动，运行以下命令：
sudo systemctl enable ssh


# 解决 E: Unable to lock directory /var/lib/apt/lists/ 问题
sudo fuser -vki /var/lib/apt/lists/lock

sudo apt update

# 安装curl
sudo apt install curl

# 安装docker 若下面命令不行，可尝试：curl -sSL https://get.daocloud.io/docker | sh
curl -fsSL https://get.docker.com | bash -s docker --mirror Aliyun
# 安装docker之后，暂时只能用root权限使用，根据提示，需要使用以下命令让普通用户可以使用
dockerd-rootless-setuptool.sh install
# 操作完成之后可能还需要添加环境变量（以命令行上的提示为准），将以下命令添加到~/.bashrc文件里
export PATH=/usr/bin:$PATH
export DOCKER_HOST=unix:///run/user/1000/docker.sock
# 测试一下
docker run hello-world



# 1.linux常用命令


ping：查看与某主机是否能联通

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