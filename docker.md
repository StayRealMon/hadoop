## Docker环境安装准备
1. 更换阿里云内网镜像源，更新apt源
```bash
sudo cp /etc/apt/source.list source_backup.list
apt update
apt full-upgrade  -y
#
apt install apt-transport-https ca-certificates curl software-properties-common -y
#
curl -fsSL http://mirrors.cloud.aliyuncs.com/docker-ce/linux/ubuntu/gpg | apt-key add -
#
add-apt-repository \
"deb [arch=amd64] http://mirrors.cloud.aliyuncs.com/docker-ce/linux/ubuntu \
$(lsb_release -cs) \
stable"
#
apt update
#安装docker-ce
apt install docker-ce -y
```