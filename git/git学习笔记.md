# git 命令笔记
---
## 目录
 1. [本地仓库](#本地仓库)
 1. [初始化本地仓库](#初始化本地仓库)
 1. [添加文件到暂存区](#添加文件到暂存区)
 1. [完成提交](#完成提交，文件添加到本地仓库)

---

### 本地仓库
1. #### 初始化本地仓库
> git init     
2. #### 添加文件到暂存区    
> git add .    
3. #### 完成提交，文件添加到本地仓库    
> git commit --all -m "第一次提交"    



----
## **补充笔记**
+ **git config --global user.name '姓名'** : 设置全局的用户名。
+ **git push -u origin master** : push时使用`-u`可以直接设置上游分支。
+ **git pull origin master** : pull时，可拉取指定分支的代码。
+ **git remote add origin [仓库地址]** : 添加远程仓库地址的源。
+ **git log** : 查看变更历史的日志。
>**-p**：可以查看对应提交的文件变更详情。   
>**--stat**：可以查看粗略的文件修改情况。   
>**--graph**：使用图形显示分之合并历史。   
>**--since(--until)**：日志过滤功能，查看指定时间段的日志。例如`"--since="2017-12-04"`。     
+ **git commit**：提交暂存空间的文件。
>**--amend**：修改前一次提交时的文字说明内容。    
>**--all**：自动完成add的commit参数。   
+ **git remote**：远程仓库查看命令。
> **-v**：查看拉取和推送使用的远程仓库地址。    
> **add [name] [url]**：设置远程仓库别名。
+ **git rm --cached**：移除已暂存的文件。
+ **git branch [新分支名称] --track [origin/远程分支]** : 新建分支并跟踪指定的远程分支。
+ **git branch -b [新分支名称]** : 新建分支并切换到该分支。
+ **git config --global core.quotepath false** : 解决 git status 中文乱码问题。
