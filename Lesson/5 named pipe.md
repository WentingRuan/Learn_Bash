# 5 named pipe

标签（空格分隔）： bash

---

[TOC]

##通道pipe
```
exec 9>aaa.txt

echo hi >&9

cat aaa.txt

 exec 10<aaa.txt #开一个信道，从aaa.txt这个地址拿东西

 cat <&10 #cat拿到文件后，信道里就没有东西了。
hi
```

```
exec 1> b.log
ls
cat b.log
cat: b.log: input file is output file #当前bash的1>子进程已经在运行了，已经是一个output file

#开一个新bash执行，1>还是bash的原始定义（输出到屏幕）

 cat b.log
```
```
ps aux 

ps aux | grep bash

ps | grep bash

```

##打开一个通道
###> 
```
exec 9>aaa.txt #定义9>为output通往aaa.txt通道

echo hi >&9 #hi去了aaa.txt

cat aaa.txt
hi
```  
### <
```
exec 10<aaa.txt #打开一个input来自aaa.txt这个文件的通道10<

cat <&10
hi
#从这个通道取文件aaa.txt的内容，aaa.txt的内容是一个standard input可以直接被cat命令print出来

cat <&10

cat <&10

echo hi >&10
bash: echo: write error: Bad file descriptor
#pipe closed
```
#named pipe
创建一个pipe
```
mkfifo xxx.pipe #fifo=first in first out
#PCM producer Consumer Mode
ls -l
echo hi > xxx.pipe
#目前pipe处于打开状态，等待信息传过去
#开一个新bash
cat xxx.pipe
```
打开pipe，把结果一次性传输给xxx.pipe
```
for i in `seq 10`;do echo hi;done > aaa.pipe
for i in `seq 10`;do echo hi;sleep 1s;done > aaa.pipe

#新bash
cat xxx.pipe #一次性把seq 10都显示了

##但是再次测试时，发现还是一个个显示hi,这是因为你加了sleep 1s在里面。所以本质是从pipe里，把进程输出了

#再开第三个bash
cat xxx.pipe
#cat: xxx.pipe: Device or resource busy
```
把结果分次（one by one）放进xxx.pipe，如果output没被接收，进程不会主动关闭
```
while True;do echo $i > xxx.pipe;sleep 2s;let i=$i+1 ;done
```
在其他的bash里cat
```
cat aaa.pipe
hi #一个hi
```
一直取结果,错误信息丢进null
```
#两个进程同时从pipe里取结果的情况下
while (true);do cat xxx.pipe 2> /dev/null ; done
```



