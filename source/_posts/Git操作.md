---
title: 那些你不知道的Git实用操作
categories:
- tool
- git
tags: 
- git

---



# Git操作

## git cherry-pick [commitID]

代码开发的时候，有时需要把某分支（比如develop分支）的某一次提交合并到另一分支（比如master分支），这就需要用到```git cherry-pick```命令。

首先，切换到develop分支，敲 git log 命令，查找需要合并的commit记录，比如commitID：7fcb3defff；

然后，切换到master分支，使用``` git cherry-pick 7fcb3defff```  命令，就把该条commit记录合并到了master分支，这只是在本地合并到了master分支；

最后，git push 提交到master远程，至此，就把develop分支的这条commit所涉及的更改合并到了master分支。



# Q&A

## 问题描述： git push 报 HTTP Basic: Access denied 错误
 原因：本地git配置的用户名、密码与gitlabs上注册的用户名、密码不一致。


解决方案： 

- 1. 如果账号密码有变动 用这个命令 ```git config –system –unset credential.helper``` 重新输入账号密码 应该就能解决了 

- 2. 如果用了第一个命令 还不能解决问题那么 用这个命令： 
     ```git config –global http.emptyAuth true```
- 3. 如果以上两个方法不起作用，那么采用以下方法：进入控制面板》用户账号》凭据管理器？windows凭据》普通凭据，在里面找到git，点开编辑密码，更新为最新密码之后就可以正常操作了。



# 参考资料

1. [git将某分支的某次提交合并到另一分支](https://blog.csdn.net/I_recluse/article/details/93619400)
2. [git remote: HTTP Basic: Access denied 错误解决办法](https://www.cnblogs.com/lydiawork/p/10287797.html)