# 1 bash基本命令

标签（空格分隔）： bash

---

#shell
shell 是一个用C语言编写的程序，它是用户使用Linux的桥梁。Shell既是一种命令语言，又是一种程序设计语言。
Shell 是指一种应用程序，这个应用程序提供了一个界面，用户通过这个界面访问操作系统内核的服务。
Ken Thompson的sh是第一种Unix Shell，Windows Explorer是一个典型的图形界面Shell。
Shell 脚本（shell script），是一种为shell编写的脚本程序。
业界所说的shell通常都是指shell脚本，但读者朋友要知道，shell和shell script是两个不同的概念。
由于习惯的原因，简洁起见，本文出现的"shell编程"都是指shell脚本编程，不是指开发shell自身。

##Shell 环境
Shell 编程跟java、php编程一样，只要有一个能编写代码的文本编辑器和一个能解释执行的脚本解释器就可以了。
Linux的Shell种类众多，常见的有：
Bourne Shell（/usr/bin/sh或/bin/sh）
Bourne Again Shell（/bin/bash）
C Shell（/usr/bin/csh）
K Shell（/usr/bin/ksh）
Shell for Root（/sbin/sh）
##Bash
也就是 Bourne Again Shell，由于易用和免费，Bash在日常工作中被广泛使用。同时，Bash也是大多数Linux系统默认的Shell。

打开文本编辑器(可以使用vi/vim命令来创建文件)，新建一个文件test.sh，扩展名为sh（sh代表shell），扩展名并不影响脚本执行，见名知意就好，如果你用php写shell 脚本，扩展名就用php好了。


#基本命令语句

##返回/输出
`echo` 返回

##赋值
`d="123"` 赋值


##列出当前所有文件（夹）
```bash
ls
```
##进入文件（文件夹）
|命令 | 解释|
| --- | ---|
|cd /c| #进入c盘|
|cd ~| cd /Username|
|mkdir wtbash|创建文件夹|

##.和..

`.`表示当前文件夹
`..`表示上一级文件夹
```bash
cd .
cd ..
```
##输出文件
```
cat [option] file
cat -n
cat --help
cat -A
```
显示前几个以及序号
```bash
cat -n a.txt | head -n 8
```

##创建文件
```
echo 123
```
##重导向
```bash
echo 123 > a.txt
```
##追加
```bash
echo "123" >> a.log
```
##跑bash
```bash
bash XX.sh
```
##用vim打开文件进行编辑
```bash
vim a.log
vim a.sh
```


##中断（信号）
Ctrl c


##其他命令
###自定义信号
```shell
a=3
trap "let a=a+1" SIGINT

41914@DESKTOP-6SI2VOE MINGW64 ~/wtbash
$ ^C

41914@DESKTOP-6SI2VOE MINGW64 ~/wtbash
$ echo $a
4
```
##常用函数
###自定义命令
###alias
```
alias ls="ls -lh"
ls
alias
```
取消定义
```
unalias ls
alias
```

```
ls -a -h | head 
ls -ah | head
ls -al -h | head 
```
###sleep
 `sleep 1 == sleep 1s`
 默认单位为秒，还可以设置为h和m
 查看`sleep --help`
 
###grep
```
grep "^\." #.start
la | grep "^\."

grep "\.$" #.end
la | grep "\.txt$"
```
`.`表示语法字符，`.`不转译，`\.`表示需要匹配`.`
```
ls | grep "^[a-z]\.
ls | grep "^[a-z]."
```
其余的都要转义(\+,\{ \})，不然就是匹配+和{}
```
ls | grep "^[a-z]\+"
ls | grep "^[a-z]\{1,2\}"
cat b.txt | grep "^[0-9]\{1\}$" #只匹配个位数
```

#rm
rm a file or a directory
```
rm -r file #-r digui
rm -rf file #f force
```
#cd -
back the last diretory
```
cd ~/test
cd ~/wtbash
cd -
cd -
cd .
cd ..
```
```bash
for i in `seq 100`;do echo $i >> a.txt;done
```
```bash
for i in `seq 100`;do echo $i;done > b.txt
```
```bash
seq 100 > c.txt
```
###显示文件的前几个/后几个行
```bash
head -n 10 a.txt #n可以为任意数字
tail -n 10.txt
```
###标记 
```
m #mark
n
'
n
```
##搜索
```
/
```

  [1]: http://static.zybuluo.com/419145138/r9u6f8lrrn4w9zxzqvyispqg/image_1b92dnqkukgu1ful24b1ok116u6p.png
  [2]: http://static.zybuluo.com/419145138/dku675cyl3w0zxhyhb1n0gxz/image_1b92e62oe1g6aakj1chj1lgd1vo916.png