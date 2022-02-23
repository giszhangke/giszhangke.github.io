Docker 19.03+ 已经支持GPU虚拟化，不再需要额外安装nvidia-docker



# 安装yum-utils

``yum -y install yum-utils``

# 设置官方 Docker CE 仓库

```shell
yum-config-manager --add-repo=https://download.docker.com/linux/centos/docker-ce.repo
yum repolist -v
yum install -y https://download.docker.com/linux/centos/7/x86_64/stable/Packages/containerd.io-1.4.3-3.1.el7.x86_64.rpm
yum install docker-ce -y
systemctl --now enable docker
docker run --rm hello-world
```



# Centos7安装nvidia-container-toolkit

```
distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.repo | sudo tee /etc/yum.repos.d/nvidia-docker.repo
sudo yum install -y nvidia-container-toolkit
```



# 测试nvidia docker是否安装成功

```
docker run --rm --gpus all nvidia/cuda:10.2-base nvidia-smi
```



# Docker 重新打tag和删除tag

```
# 打tag
docker tag [image id] [repository]:[tag]

# 删除tag
docker rmi [repository]:[tag]
```



# 查看文件系统类型

``df -T``



# 查看nvidia CUDA版本

```
nvidia-smi
```



# 卸载docker

```
yum list installed | grep docker
yum -y remove  XXXXX
```



# 修改Docker存储

https://blog.csdn.net/BigData_Mining/article/details/104921479?spm=1001.2101.3001.6661.1&utm_medium=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7ECTRLIST%7Edefault-1.no_search_link&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7ECTRLIST%7Edefault-1.no_search_link&utm_relevant_index=1

使用方法2、软链接



# 参考资料

1. [installing-on-centos-7-8](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html#installing-on-centos-7-8)