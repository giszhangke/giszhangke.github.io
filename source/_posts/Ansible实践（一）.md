---
title: Ansible实践（一）
categories:
- Tool
- Ansible
tags:
- Ansible
date: 2021-11-02 23:57:59
---
ansible实践，在三台服务器上安装JDK
<!--more-->

# Ansible实践（一）

##  服务器准备

| 服务器(CentOS Linux 7) | 作用        | 描述    |
| ---------------------- | ----------- | ------- |
| 192.168.241.139        | Ansible主机 |         |
| 192.168.241.140        | 受管服务器  | 安装JDK |
| 192.168.241.141        | 受管服务器  | 安装JDK |



## 安装Ansible

在192.168.241.139上安装ansible

```bash
yum -y install epel-release
yum -y install ansible
```



## 配置ssh授权

### Ansible主机生成密钥

在192.168.241.139上执行命令，遇到需要输入的地方直接敲回车

```bash
ssh-keygen -t rsa -P ""
```

### 复制公钥到受管服务器

复制公钥到受管服务器，方便Ansible免密登录

```bash
ssh-copy-id -i /root/.ssh/id_rsa.pub root@192.168.241.140
ssh-copy-id -i /root/.ssh/id_rsa.pub root@192.168.241.141
```

### 检查受管节点连通性

```
# 检查所有结点
ansible -m ping all

# 检查指定角色结点 
ansible webserver -m ping
```



## Ansible配置

### Ansible通用配置

配置文件

```
vim /etc/ansible/ansible.cfg
```



### 受管服务器host配置

```bash
vim /etc/ansible/hosts
```

在hosts文件中加入， 并保存

```
[jdk]
192.168.241.140
192.168.241.141
```

### 文件准备

上传jdk安装包jdk1.8.0_201.tar.gz到Ansible主机目录/opt/jdk/files

并在该目录下添加.bashrc文件，文件内容如下：

```bash
# .bashrc

# User specific aliases and functions

alias rm='rm -i'
alias cp='cp -i'
alias mv='mv -i'

# Source global definitions
if [ -f /etc/bashrc ]; then
        . /etc/bashrc
fi

# User specific environment and startup programs

export JAVA_HOME=/opt/jdk/jdk1.8.0_201
export PATH=$JAVA_HOME/bin:$HOME/bin:$PATH

```



### 编写Ansible剧本

```
vim /etc/ansible/roles/jdkinstall.yml
```

jdkinstall.yml内容如下：

```yml
- hosts: jdk
  vars:
   - ansible_python_interpreter: /usr/bin/python
   - ansible_ssh_user: root
  environment:
     JAVA_HOME: /opt/jdk/jdk1.8.0_201
  tasks:
   - name: Create directory /opt/jdk
     file: path=/opt/jdk state=directory owner=root group=root
   - name: Unarchive JDK Software
     unarchive: src=jdk/files/jdk1.8.0_201.tar.gz dest=/opt/jdk/
   - name: Copy JDK env .bashrc
     copy: src=jdk/files/.bashrc dest=/root/ mode=755
   - name: enable jdk env
     shell: source /root/.bashrc

```

注：src路径是相对role_path（可以在ansible.cfg中修改）的路径

### 执行Ansible剧本

```bash
ansible-playbook /etc/ansible/roles/jdkinstall.yml
```

执行过程下如

```bash
PLAY [jdk] ******************************************************************************

TASK [Gathering Facts] ******************************************************************
ok: [192.168.241.142]
ok: [192.168.241.140]
ok: [192.168.241.141]

TASK [Create directory /opt/jdk] ********************************************************
ok: [192.168.241.141]
ok: [192.168.241.140]
ok: [192.168.241.142]

TASK [Unarchive JDK Software] ***********************************************************
ok: [192.168.241.141]
ok: [192.168.241.140]
ok: [192.168.241.142]

TASK [Copy JDK env .bashrc] *************************************************************
ok: [192.168.241.140]
ok: [192.168.241.141]
ok: [192.168.241.142]

TASK [enable jdk env] *******************************************************************
changed: [192.168.241.140]
changed: [192.168.241.142]
changed: [192.168.241.141]

PLAY RECAP ******************************************************************************
192.168.241.140 : ok=5 changed=1 unreachable=0 failed=0 skipped=0 rescued=0 ignored=0   
192.168.241.141 : ok=5 changed=1 unreachable=0 failed=0 skipped=0 rescued=0 ignored=0   
192.168.241.142 : ok=5 changed=1 unreachable=0 failed=0 skipped=0 rescued=0 ignored=0  
```



## Q&A

### 环境变量修改

如果需要通过ansible修改环境变量，需要修改.bashrc文件，并用soucre命令使其生效，执行source命令时最好不要有其他客户端登录受控机器，因为这可能导致source命令执行不起作用

