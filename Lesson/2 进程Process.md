# 2 进程Process
标签（空格分隔）： bash

---

#进程 Process
Process 就是正在运行中的 Program

#bash 进程
bash本身就是一个进程，内部有一个bash terminal，类似Rstudio与R Gui。
bash会将你的各种命令当作input，把运行的结果（output）输出到屏幕或者其指定的地方，所以bash本身就是一个人与bash进行交互式的进程

##内部命令
```
man bash
```
![image_1b9oa4mji1fju18mddjt2ne1la113.png-10.8kB][1]
```
/^\s+[argument]^
```
```
man bash
/^\s+exec #\s多个space
```
![image_1b9oa2012sl69jj5nl1peppfs9.png-17.5kB][2]
##外部命令
```
man cat
```
![image_1b9oa3gk8d2219a175s1rhu187om.png-9.7kB][3]
##fork
把原来的环境Clone一遍，开一个新的进程，跑新的代码/语言，并用新的PID表示这个新进程
current process 是 bash.exe PID是13100
fork vim 即clone bash的环境之后，跑新进程vim.exe，并给个新名字区分bash.exe，PID 13101

##bash & bash terminal
|父进程|子进程|
|---|---|
|bash terminal|vim|

##process & file
|进程|命令|进程流|
|---|---|---|
|input | < | 输入|
|output |1> or >| 输出流1|
|error| 2>|输出流2|

##基本命令
| 命令 | 解释 |
| --- | --- |
| jobs | 列出当前program |
| Ctrl+z | 暂停当前program，进入后台 |
| fg %1 | 回到第一个program |
| kill %1 | #terminate program |

##program -> file
```bash 
#output 1
echo hi > a.file
cat a.file

echo1 hi > a.file #put error output into screen(bash terminal)
echo1 hi 2> a.file #put error output into a.file 
cat a.file #show error output in a.file
```
##program1 -> program2
the output of `echo hi` becomes the input of `cat`
```bash
echo hi | cat 
```

```bash
ps > a.file
cat a.file | grep pty4 
grep -n pty4 a.file #grep [option] [file]
```
the output of the first program:`ps` that is supposed to show on the screen becomes the input of the next program:`grep pty4`, which run exactly the same as #2
```bash
ps | grep pty4
 
#2
ps > a.file
grep pty4 a.file
```
##/dev/null 空文件
```shell
echo1 hi 2> /dev/null
echo1 hi > /dev/null
```
## #1 || #2
1正确就不跑2

```shell
echo1 hi > /dev/null || echo bi 
#bash: echo1: command not found
#bi

echo1 hi 2> /hev/null || echo bi
#bi
```
```
echo hi > /dev/null || echo bi 
#无显示
echo hi 2> /dev/null || echo bi 
#hi

```
## #1 && #2
```shell
echo1 hi > /dev/null && echo bi 
#bash: echo1: command not found

echo1 hi 2> /dev/null && echo bi 
#无显示，错误流去了NULL
```
```
 echo hi 2> /dev/null && echo bi #hi bi
 echo hi > /dev/null && echo bi #bi
```




