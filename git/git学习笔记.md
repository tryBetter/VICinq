## git学习笔记
---
+ **git push -u origin master** : push时使用`-u`可以直接设置上游分支。
+ **git pull origin master** : pull时，可拉取制定分支的代码。
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
