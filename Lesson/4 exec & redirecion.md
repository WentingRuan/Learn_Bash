# 4 exec & redirecion

标签（空格分隔）： bash

---

#exec 
exec不执行内部命令，也不执行不存在的命令，只执行外部命令
做法：shut down current process，跑新的进程执行新的命令，跑完后就关闭
```
exec ls #ls 是外部命令
```
```
exec [-cl] [-a name] [command [arguments]]
``` 
    If  command  is specified(指定，命令被指定=command exists), it replaces the shell.  No new process is created. （取代shell进程，跑完新命令就关闭）
    The arguments become the arguments to command.  
    
    If the -l option is supplied, the shell places a dash at the beginning of the zeroth  argument  passed  to command.  This is what login(1) does.  
    The -c option causes command to be executed with an empty environment. 
    If -a is supplied, the shell passes name as the zeroth argument to the executed command. 
    
    If command  cannot  be  executed for  some  reason,  a  non-interactive  shell  exits, unless the exec fail shell option is enabled. In that case, it returns failure.  
    
    An interactive shell returns failure if the file cannot be executed. 
    
    If command is not specified,any redirections take effect in the current shell, and the return status is 0.  If there is a redirection error, the return status is 1.

#Redicrection
```
exec ls 1> a.log
cat a.log
```
```
cat <a.txt #a.txt作为一个standard input 
hi

cat -n < a.txt
   1 hi

echo hi >a.txt #无效操作
 echo - <a.txt #拒绝了a.txt这个input
-

grep h <a.txt
hi

echo "\ta" | cat -b
     1  \ta

echo -e "\ta" #输出执行"\ta"命令的output
     1   a

echo -e "\ta" | cat -t #显示tab
^Ia #^I是制表符，表示占位（空格），类似\n表示换行

```



  [1]: http://static.zybuluo.com/419145138/vy9tr9ifsmbx1m6vifzqe1w8/image_1b9oa4mji1fju18mddjt2ne1la113.png
  [2]: http://static.zybuluo.com/419145138/oxfzp18ouapf2gwc3h29501o/image_1b9oa2012sl69jj5nl1peppfs9.png
  [3]: http://static.zybuluo.com/419145138/c2ylrq6yxd7oa8c52vwck9ou/image_1b9oa3gk8d2219a175s1rhu187om.png